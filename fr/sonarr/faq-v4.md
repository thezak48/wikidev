---
title: FAQ de la version bêta de Sonarr v4
description: FAQ de la version bêta de Sonarr v4
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# FAQ de la version bêta de Sonarr v4

> Sonarr v4 est actuellement en version bêta, il est donc normal de rencontrer des erreurs et des problèmes. Veuillez utiliser nos canaux de support pour poser des questions, signaler des problèmes ou fournir des commentaires sur la version bêta v4. Si nécessaire, on peut vous demander d'ouvrir un problème sur Github, si on vous demande d'ouvrir un problème sur [Github](https://github.com/Sonarr/Sonarr). Veuillez fournir un lien vers la discussion originale ainsi que toutes les autres informations demandées. {.is-warning}

## Qu'est-ce qui a changé ?

Consultez l'[annonce de la version bêta v4](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/) pour plus d'informations.

Voici quelques-unes des nouveautés et des changements les plus importants :

- [Authentification obligatoire](#authentification-obligatoire)
- Mono => Dotnet (plus de rapidité ; plus de mono). En raison de ce changement, il est probable que des mises à jour de la configuration du proxy inverse soient nécessaires :
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Les mots préférés ont disparu](#migration-des-mots-préférés-vers-les-formats-personnalisés) et ont été remplacés par des formats personnalisés
- [Les profils de langue ont disparu](#où-sont-passés-les-profils-de-langue) et ont été remplacés par des formats personnalisés
- Thème sombre/clair
- Prise en charge de SysLog et du nom d'instance
- Fusion de l'éditeur de masse dans [l'aperçu de la série](#où-est-passé-l'éditeur-de-masse)
- Et bien plus encore

## Authentification obligatoire

Si Sonarr est exposé de manière à ce que l'interface utilisateur puisse être accessible depuis l'extérieur de votre réseau local, vous devez avoir une méthode d'authentification activée pour accéder à l'interface utilisateur. Cela est également de plus en plus nécessaire pour les trackers et les indexeurs.

À partir de Sonarr v4, l'authentification est obligatoire.

### Méthode d'authentification

- `Basic` (fenêtre contextuelle du navigateur) - Cette option, lors de l'accès à Sonarr, affiche une petite fenêtre contextuelle vous permettant de saisir un nom d'utilisateur et un mot de passe.
- `Forms` (page de connexion) - Cette option affiche une page de connexion familière, comme sur d'autres sites web, vous permettant de vous connecter à Sonarr.
- `External` - Configurable uniquement via le fichier de configuration
  - Si vous utilisez une **authentification externe** telle que Authelia, Authetik, NGINX Basic auth, etc., vous pouvez éviter de devoir vous authentifier deux fois en arrêtant l'application, en définissant `<AuthenticationMethod>External</AuthenticationMethod>` dans le [fichier de configuration](/sonarr/appdata-directory) et en redémarrant l'application. **Notez que plusieurs entrées `AuthenticationMethod` dans le fichier ne sont pas prises en charge et seule la valeur la plus élevée sera utilisée.**

### Authentification requise

- Si vous n'exposez pas l'application à l'extérieur et/ou si vous ne souhaitez pas que l'authentification soit requise pour l'accès local (par exemple, le réseau local), modifiez les paramètres dans Paramètres => Sécurité générale => Authentification requise pour mettre sur `Désactivé pour les adresses locales`
  - L'équivalent dans le fichier de configuration est `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Migration des mots préférés vers les formats personnalisés

Le système des mots préférés a été remplacé par le système des formats personnalisés. Cela permet une granularité beaucoup plus fine dans les décisions que Sonarr peut prendre. Alors que les mots préférés s'appliquaient à tous les profils de qualité, les formats personnalisés peuvent avoir une importance différente pour chaque profil de qualité.

Les formats personnalisés peuvent également avoir un niveau de coupure afin que les mises à niveau s'arrêtent une fois qu'un niveau de préférence souhaité est atteint, alors que l'ancien système des mots préférés effectuait toujours des mises à niveau si une meilleure version était trouvée.

### Doit (ne pas) contenir

Les options Doit contenir et Ne doit pas contenir restent dans les paramètres du profil de publication, comme dans la version 3.

### Jetons de nom de fichier

Le jeton de nom `{Preferred Words}` utilisait le terme correspondant à l'entrée regex pour le nommage des fichiers.
Le jeton de nom `{Custom Formats}` utilise le nom du format personnalisé pour le nommage des fichiers.

> Il est recommandé de prendre une capture d'écran ou de supprimer vos profils de publication des mots préférés AVANT la mise à niveau. Chaque ligne de mot préféré deviendra son propre format personnalisé après la migration.
{.is-warning}

## Où sont passés les profils de langue ?

Les langues sont gérées différemment dans Sonarr v4. Elles ne sont plus gérées via l'ancien système de profils de langue, mais font désormais partie des formats personnalisés. Vous devrez créer des formats personnalisés pour les langues que vous souhaitez télécharger, puis ajouter ces formats personnalisés à vos profils de qualité avec une note appropriée pour forcer le téléchargement de cette langue.

> Consultez le guide TRaSH [Comment configurer des formats personnalisés de langue](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/) pour plus d'informations.
{.is-info}

### Uniquement l'anglais

**Depuis [TRaSH => Langue : Anglais uniquement](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

Si vous souhaitez uniquement télécharger des versions en anglais, vous pouvez utiliser le format personnalisé suivant. Importez ce format personnalisé, puis attribuez-le à chacun de vos profils de qualité avec une note de -10000. En supposant que votre note minimale pour les formats personnalisés est de 0, cela rejettera toutes les versions qui ne sont pas analysées comme étant en anglais.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Langue : Anglais uniquement",
  "name": "Langue : Pas anglais",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Langue non anglaise",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 1
      }
    }
  ]
}
```

### Uniquement l'original

**Depuis [TRaSH => Langue : Uniquement l'original](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

Si vous souhaitez uniquement télécharger des versions dans la langue d'origine de la série selon TVDb, vous pouvez utiliser le format personnalisé suivant. Importez ce format personnalisé, puis attribuez-le à chacun de vos profils de qualité avec une note de -10000. En supposant que votre note minimale pour les formats personnalisés est de 0, cela rejettera toutes les versions qui ne sont pas analysées comme étant dans la langue d'origine de la série selon TVDb.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Langue : Uniquement l'original",
  "name": "Langue : Pas l'original",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Langue non originale",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": -2
      }
    }
  ]
}
```

## Mon proxy inverse ne fonctionne plus ?

En raison des changements dans le backend de Sonarr (migration de mono à dotnet), votre proxy inverse peut ne plus fonctionner.

### Nginx

Votre fichier de configuration Nginx doit être modifié. Remplacez cette ligne :

```nginx
   proxy_set_header   Host $proxy_host;
```

par cette ligne :

```nginx
  proxy_set_header   Host $host;
```

### Apache

Votre fichier de configuration de virtualhost Apache doit être modifié. Ajoutez cette ligne :

```apache2
  ProxyPreserveHost On
```

## Qu'est-ce que ce nouveau bouton "*Override and add to download queue*" ?

Lors d'une recherche interactive, un deuxième bouton de téléchargement intitulé "Override and add to download queue" a été ajouté. Ce bouton vous permet de faire deux choses :

- Choisir le client de téléchargement vers lequel le téléchargement est envoyé. Cela est utile dans le cas où vous avez plusieurs clients de téléchargement pour le même protocole (par exemple, plusieurs instances d'un client torrent) au lieu de laisser Sonarr décider quel client utiliser.
- Remplacer l'analyse du titre de la version effectuée par Sonarr au cas où Sonarr l'aurait analysée de manière incorrecte ou si Sonarr n'a pas pu l'analyser, mais que vous souhaitez quand même télécharger la version. Les champs d'analyse suivants peuvent être modifiés :
  - Série
  - Numéro de saison
  - Épisode(s)
  - Qualité
  - Langue

## Où est passé l'éditeur de masse ?

La page autonome de l'éditeur de masse a été supprimée et la fonctionnalité a été fusionnée dans la page d'aperçu de la série. Pour modifier en masse des séries, cliquez d'abord sur le bouton `Sélectionner la série` en haut de l'aperçu de la série, puis sélectionnez les séries que vous souhaitez modifier.

La page de gestion des saisons a également été supprimée. Une partie de la fonctionnalité reste dans l'éditeur de l'aperçu de la série, choisissez la vue en tableau et appuyez sur `Sélectionner la série`. Une fois en mode de sélection, survolez le nombre dans la colonne des saisons pour accéder à la fenêtre contextuelle de gestion des saisons pour cette série.

## Les durées des épisodes affichent 0

La version 4 utilise une durée par épisode provenant de TVDb. Si la durée de l'épisode est de 0, il essaiera de revenir à la durée de la série.
Si la durée de la série est également de 0, Sonarr utilisera une durée de 45 minutes pour tout épisode diffusé dans les 24 heures suivant le premier épisode.