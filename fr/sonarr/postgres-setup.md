---
title: Configuration de Sonarr avec une base de données PostgreSQL
description: Configuration de Sonarr avec une base de données PostgreSQL
published: true
date: 2023-08-21T19:37:53.766Z
tags: 
editor: markdown
dateCreated: 2023-08-12T12:26:25.094Z
---

# Sonarr et Postgres

Ce document présente les points clés de la migration et de la configuration de la prise en charge de Postgres dans Sonarr.

> Sonarr v4.0.0.615 ou une version ultérieure est requise
{.is-info}

Ce guide a été créé par le formidable [Roxedus](https://github.com/Roxedus).

> Les bases de données Postgres NE sont PAS sauvegardées par Sonarr, toutes les sauvegardes doivent être mises en place et gérées par l'utilisateur
{.is-danger}

## Configuration de Postgres

 Tout d'abord, nous avons besoin d'une instance Postgres. Ce guide est écrit pour une utilisation de l'image Docker `postgres:14`.

 > N'envisagez même pas d'utiliser l'étiquette `latest` ! {.is-danger}

```bash
docker create --name=postgres14 \
    -e POSTGRES_PASSWORD=qstick \
    -e POSTGRES_USER=qstick \
    -e POSTGRES_DB=sonarr-main \
    -p 5432:5432/tcp \
    -v /chemin/vers/appdata/postgres14:/var/lib/postgresql/data \
    postgres:14
```

## Création de la base de données

Sonarr a besoin de deux bases de données, dont les noms par défaut sont :

- `sonarr-main`   Celle-ci est utilisée pour stocker toutes les configurations et l'historique
- `sonarr-log`    Celle-ci est utilisée pour stocker les événements qui produisent une entrée de journal

> Sonarr ne créera pas les bases de données pour vous. Assurez-vous de les créer à l'avance{.is-warning}

Créez les bases de données mentionnées ci-dessus en utilisant votre méthode préférée - par exemple [pgAdmin](https://www.pgadmin.org/) ou [Adminer](https://www.adminer.org/).

Vous pouvez donner n'importe quel nom aux bases de données, mais assurez-vous que le fichier `config.xml` a les noms corrects. Pour plus d'informations, consultez [la création du schéma](/sonarr/postgres-setup#schema-creation).

### Création du schéma

 Nous devons indiquer à Sonarr d'utiliser Postgres. Le fichier `config.xml` devrait déjà être rempli avec les entrées dont nous avons besoin :

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

Seulement **après avoir créé** les deux bases de données, vous pouvez commencer la migration de Sonarr de SQLite vers Postgres.

## Migration des données

> Si vous ne souhaitez pas migrer une base de données SQLite existante vers Postgres, vous avez déjà terminé ce guide ! {.is-info}

Pour migrer les données, nous pouvons utiliser [PGLoader](https://github.com/dimitri/pgloader). Cependant, il y a quelques points à prendre en compte :

- Par défaut, les transactions ne sont pas sensibles à la casse, nous utilisons `--with "quote identifiers"` pour les rendre sensibles.
- La version fournie dans le référentiel apt de Debian et Ubuntu est trop ancienne pour les versions plus récentes de Postgres (Roxedus n'a pas testé les packages dans d'autres distributions).
  Roxedus a [construit un binaire](https://github.com/Roxedus/Pgloader-bin) pour activer cette prise en charge (aucune modification de code n'était nécessaire, il suffisait de le construire avec des dépendances mises à jour).

> Ne supprimez aucune table dans l'instance Postgres {.is-danger}

Avant de commencer une migration, assurez-vous d'avoir exécuté Sonarr sur les bases de données Postgres créées **au moins une fois** avec succès. Commencez la migration en effectuant les étapes suivantes :

1. Arrêtez Sonarr
1. Ouvrez votre outil de gestion de base de données préféré et connectez-vous à l'instance de base de données Postgres
1. Exécutez les commandes suivantes :

```SQL
DELETE FROM "QualityProfiles";
DELETE FROM "QualityDefinitions";
DELETE FROM "DelayProfiles";
DELETE FROM "Metadata";
```

1. Démarrez la migration en utilisant l'une de ces options :

    - ```bash
      pgloader --with "quote identifiers" --with "data only" sonarr.db 'postgresql://qstick:qstick@localhost/sonarr-main'
      ```

    - ```bash
      docker run --rm -v /chemin/absolu/vers/sonarr.db:/sonarr.db:ro --network=host ghcr.io/roxedus/pgloader --with "quote identifiers" --with "data only" /sonarr.db "postgresql://qstick:qstick@localhost/sonarr-main"
      ```

  > Si vous rencontrez une erreur lors de l'utilisation de pgloader, cela peut être dû à la taille trop importante de votre base de données. Pour résoudre ce problème, essayez d'ajouter `--with "prefetch rows = 100" --with "batch size = 1MB"` à la commande ci-dessus
  {.is-warning}

  > Une fois ces problèmes résolus, cela devient assez simple après avoir indiqué de ne pas toucher au schéma en utilisant `--with "data only"`
  {.is-info}


2. Démarrez Sonarr


3. Pour ceux qui rencontrent des problèmes d'ajout de séries ou des erreurs dans le journal après la POST-MIGRATION depuis SQLite, exécutez les commandes suivantes :
```SQL
select setval('public."AutoTagging_Id_seq"',(SELECT MAX("Id")+1 FROM "AutoTagging"));
select setval('public."Blacklist_Id_seq"',(SELECT MAX("Id")+1 FROM "Blocklist"));
select setval('public."Commands_Id_seq"',(SELECT MAX("Id")+1 FROM "Commands"));
select setval('public."Config_Id_seq"',(SELECT MAX("Id")+1 FROM "Config"));
select setval('public."CustomFilters_Id_seq"',(SELECT MAX("Id")+1 FROM "CustomFilters"));
select setval('public."CustomFormats_Id_seq"',(SELECT MAX("Id")+1 FROM "CustomFormats"));
select setval('public."DelayProfiles_Id_seq"',(SELECT MAX("Id")+1 FROM "DelayProfiles"));
select setval('public."DownloadClientStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadClientStatus"));
select setval('public."DownloadClients_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadClients"));
select setval('public."DownloadHistory_Id_seq"',(SELECT MAX("Id")+1 FROM "DownloadHistory"));
select setval('public."EpisodeFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "EpisodeFiles"));
select setval('public."Episodes_Id_seq"',(SELECT MAX("Id")+1 FROM "Episodes"));
select setval('public."ExtraFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "ExtraFiles"));
select setval('public."History_Id_seq"',(SELECT MAX("Id")+1 FROM "History"));
select setval('public."ImportListExclusions_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportListExclusions"));
select setval('public."ImportListStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportListStatus"));
select setval('public."ImportLists_Id_seq"',(SELECT MAX("Id")+1 FROM "ImportLists"));
select setval('public."IndexerStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "IndexerStatus"));
select setval('public."Indexers_Id_seq"',(SELECT MAX("Id")+1 FROM "Indexers"));
select setval('public."MetadataFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "MetadataFiles"));
select setval('public."Metadata_Id_seq"',(SELECT MAX("Id")+1 FROM "Metadata"));
select setval('public."NamingConfig_Id_seq"',(SELECT MAX("Id")+1 FROM "NamingConfig"));
select setval('public."NotificationStatus_Id_seq"',(SELECT MAX("Id")+1 FROM "NotificationStatus"));
select setval('public."Notifications_Id_seq"',(SELECT MAX("Id")+1 FROM "Notifications"));
select setval('public."PendingReleases_Id_seq"',(SELECT MAX("Id")+1 FROM "PendingReleases"));
select setval('public."QualityDefinitions_Id_seq"',(SELECT MAX("Id")+1 FROM "QualityDefinitions"));
select setval('public."QualityProfiles_Id_seq"',(SELECT MAX("Id")+1 FROM "QualityProfiles"));
select setval('public."RemotePathMappings_Id_seq"',(SELECT MAX("Id")+1 FROM "RemotePathMappings"));
select setval('public."Restrictions_Id_seq"',(SELECT MAX("Id")+1 FROM "Restrictions"));
select setval('public."RootFolders_Id_seq"',(SELECT MAX("Id")+1 FROM "RootFolders"));
select setval('public."SceneMappings_Id_seq"',(SELECT MAX("Id")+1 FROM "SceneMappings"));
select setval('public."ScheduledTasks_Id_seq"',(SELECT MAX("Id")+1 FROM "ScheduledTasks"));
select setval('public."Series_Id_seq"',(SELECT MAX("Id")+1 FROM "Series"));
select setval('public."SubtitleFiles_Id_seq"',(SELECT MAX("Id")+1 FROM "SubtitleFiles"));
select setval('public."Tags_Id_seq"',(SELECT MAX("Id")+1 FROM "Tags"));
select setval('public."Users_Id_seq"',(SELECT MAX("Id")+1 FROM "Users"));
```
