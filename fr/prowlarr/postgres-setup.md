---
title: Configuration de Prowlarr avec une base de données PostgreSQL
description: Configuration de Prowlarr avec une base de données Postgres
published: true
date: 2022-11-29T13:19:38.953Z
tags: 
editor: markdown
dateCreated: 2022-01-10T15:38:53.538Z
---

# Prowlarr et Postgres

Ce document présente les points clés de la migration et de la configuration de la prise en charge de Postgres dans Prowlarr.

Ce guide a été créé par le formidable [Roxedus](https://github.com/Roxedus).

> Les bases de données Postgres ne sont PAS sauvegardées par Prowlarr, toutes les sauvegardes doivent être mises en place et gérées par l'utilisateur
{.is-danger}

## Configuration de Postgres

 Tout d'abord, nous avons besoin d'une instance Postgres. Ce guide est écrit pour une utilisation de l'image Docker `postgres:14`.

 > N'envisagez même pas d'utiliser le tag `latest` ! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=prowlarr-main \
    -p 5432:5432/tcp \
    -v /path/to/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Création de la base de données

Prowlarr a besoin de deux bases de données, dont les noms par défaut sont :

- `prowlarr-main`   Celle-ci est utilisée pour stocker toutes les configurations et l'historique
- `prowlarr-log`    Celle-ci est utilisée pour stocker les événements qui produisent une entrée de journal

> Prowlarr ne créera pas les bases de données pour vous. Assurez-vous de les créer à l'avance{.is-warning}

Créez les bases de données mentionnées ci-dessus en utilisant votre méthode préférée - par exemple [pgAdmin](https://www.pgadmin.org/) ou [Adminer](https://www.adminer.org/).

> Pour que la tâche `Housekeeping` s'exécute, cet utilisateur doit être un superutilisateur, car il effectue la tâche de vidage{.is-info}

Vous pouvez donner n'importe quel nom aux bases de données, mais assurez-vous que le fichier `config.xml` contient les noms corrects. Pour plus d'informations, consultez [la création du schéma](/prowlarr/postgres-setup#schema-creation).

### Création du schéma

 Nous devons indiquer à Prowlarr d'utiliser Postgres. Le fichier `config.xml` devrait déjà être rempli avec les entrées dont nous avons besoin :

```xml
<PostgresUser>qstick</PostgresUser>
<PostgresPassword>qstick</PostgresPassword>
<PostgresPort>5432</PostgresPort>
<PostgresHost>postgres14</PostgresHost>
```

Si vous souhaitez spécifier un nom de base de données, vous devez également inclure la configuration suivante :

```xml
<PostgresMainDb>NomBaseDeDonnéesPrincipale</PostgresMainDb>
<PostgresLogDb>NomBaseDeDonnéesJournal</PostgresLogDb>
```

Seulement **après avoir créé** les deux bases de données, vous pouvez commencer la migration de Prowlarr de SQLite vers Postgres.

## Migration des données

> Si vous ne souhaitez pas migrer une base de données SQLite existante vers Postgres, vous avez déjà terminé ce guide ! {.is-info}

Pour migrer les données, nous pouvons utiliser [PGLoader](https://github.com/dimitri/pgloader). Cependant, il y a quelques points à prendre en compte :

- Par défaut, les transactions ne sont pas sensibles à la casse, nous utilisons `--with "quote identifiers"` pour les rendre sensibles.
- La version fournie dans le référentiel apt de Debian et Ubuntu est trop ancienne pour les versions plus récentes de Postgres (Roxedus n'a pas testé les paquets dans d'autres distributions).
  Roxedus a [construit un binaire](https://github.com/Roxedus/Pgloader-bin) pour activer cette prise en charge (aucune modification de code n'était nécessaire, il suffisait de le construire avec des dépendances mises à jour).

> Ne supprimez aucune table dans l'instance Postgres {.is-danger}

Avant de commencer une migration, assurez-vous d'avoir exécuté Prowlarr sur les bases de données Postgres créées **au moins une fois avec succès**. Commencez la migration en effectuant les étapes suivantes :

1. Arrêtez Prowlarr
1. Ouvrez votre outil de gestion de base de données préféré et connectez-vous à l'instance de base de données Postgres
1. Démarrez la migration en utilisant l'une de ces options :

    - ```bash
      pgloader --with "quote identifiers" --with "data only" prowlarr.db 'postgresql://qstick:qstick@localhost/prowlarr-main'
      ```

    - ```bash
      docker run --rm -v /absolute/path/to/prowlarr.db:/prowlarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /prowlarr.db "postgresql://qstick:qstick@localhost/prowlarr-main"
      ```

  > Si vous rencontrez une erreur lors de l'utilisation de pgloader, cela peut être dû à la taille trop importante de votre base de données, pour résoudre ce problème, essayez d'ajouter `--with "prefetch rows = 100" --with "batch size = 1MB"` à la commande ci-dessus
  {.is-warning}

  > Une fois ces problèmes résolus, cela devient assez simple en indiquant de ne pas toucher au schéma avec `--with "data only"`
  {.is-info}

1. Démarrez Prowlarr