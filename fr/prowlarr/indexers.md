---
title: Indexeurs Prowlarr
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

Cette page explique comment ajouter et configurer des indexeurs dans Prowlarr.

# Ajouter un indexeur

Pour ajouter un indexeur, cliquez d'abord sur `Indexeurs` à gauche, puis sur <kb>+</kb> `Ajouter un indexeur` en haut de la page.

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

Choisissez votre indexeur dans la liste, ou tapez un nom partiel dans la boîte pour trouver votre indexeur. Si votre indexeur ne figure pas dans la liste, vous pouvez peut-être utiliser "Generic Newznab" (pour Usenet) ou "Generic Torznab" (pour les torrents). Sinon, visitez notre [site de demande d'indexeur](https://requests.prowlarr.com/).

> L'utilisation de `Generic Newznab` ou `Generic Torznab` suppose que votre indexeur prend en charge les formats *znab standardisés. Sinon, cela ne fonctionnera pas.
{.is-info}

> Remarque : presque tous les sites Usenet sont compatibles avec Generic Newznab.
{.is-warning}

> Si votre tracker ou indexeur ne figure pas dans la liste et n'est pas sur notre page des [indexeurs pris en charge](/prowlarr/supported-indexers), vous pouvez demander son ajout via notre [site de demande d'indexeur](https://requests.prowlarr.com).
{.is-info}

# Modifier un indexeur

Pour modifier un indexeur, cliquez d'abord sur `Indexeurs` à gauche, puis cliquez sur l'icône de clé à molette à l'extrême droite de l'indexeur que vous souhaitez modifier.

# Afficher un identifiant ou une URL d'indexeur

Pour afficher les détails d'un indexeur, cliquez d'abord sur `Indexeurs` à gauche, puis cliquez sur le lien de l'indexeur dans la colonne Nom de l'indexeur. (Anciennement l'icône (i) à droite)

Les détails disponibles peuvent inclure :

- Identifiant dans Prowlarr
- Description
- Encodage
- Langue
- Site
- URL Prowlarr Newznab/Torznab
- Capacités du site

# Paramètres de l'indexeur

Une fois que vous avez sélectionné votre indexeur, une fenêtre contextuelle contenant des informations supplémentaires nécessaires à sa configuration s'affiche. Notez que les paramètres spécifiques changeront légèrement pour chaque indexeur en fonction des champs requis et du type d'indexeur que vous configurez.

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Nom - Sélectionnez un nom pour cet indexeur. Lorsqu'il se synchronise avec vos applications, il ajoutera `(Prowlarr)` derrière.
- Activer - Cochez la case pour activer cet indexeur.
- Redirection - Cochez la case si une redirection est nécessaire. Il n'y a que quelques indexeurs pour lesquels cela est nécessaire pour éviter d'être banni. Si cette option est activée, le lien de téléchargement direct sera transmis directement à l'application plutôt que d'être acheminé via Prowlarr.

> La redirection est généralement nécessaire uniquement pour quelques indexeurs très spécifiques.
{.is-info}

- Profil de synchronisation - Sélectionnez ici votre profil de synchronisation. Vous pouvez les créer dans [`Paramètres` => `Applications`](/prowlarr/settings#applications). Le profil par défaut standard existe déjà et ressemble à ceci :

> Vous pouvez avoir des paramètres différents par application en créant plusieurs instances de l'indexeur.
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Sélectionnez l'URL à utiliser pour Prowlarr. Si elle est vide, l'URL par défaut/la première URL est utilisée.
- Lien de téléchargement - Si vous ajoutez un indexeur de torrents, vous devrez peut-être choisir le type de lien de téléchargement à utiliser.
- (Option avancée) Chemin de l'API - Chemin de l'API de l'indexeur. Généralement `/api`
- Identifiants - De nombreux indexeurs et trackers nécessitent une authentification/connexion d'une manière ou d'une autre. Vous devrez peut-être entrer une clé API, une clé RSS, un ID de session, un cookie ou d'autres identifiants provenant de votre indexeur (généralement trouvés sur votre page de profil ou dans la section Sécurité), sélectionner des ordres de recherche ou d'autres options propres à votre indexeur spécifique.
  - Clé API
  - Clé RSS
  - ID de session
  - Cookie
  - Nom d'utilisateur/Mot de passe
  - etc.
- (Option avancée) Paramètres supplémentaires - Paramètres supplémentaires à ajouter aux requêtes pour cet indexeur.
- Expiration VIP - Entrez la date au format ISO (aaaa-MM-jj) pour être averti 1 semaine avant l'expiration ; sinon, laissez vide.
- Balises - Utilisez des balises pour spécifier les clients de téléchargement par défaut, spécifier des proxies d'indexeur, spécifier des indexeurs pour des applications ou simplement organiser vos indexeurs.
- (Option avancée) Limite de requête - Si votre indexeur limite vos requêtes API par jour, vous pouvez entrer ce nombre ici pour éviter de dépasser la limite.
- (Option avancée) Limite de téléchargement - Si votre indexeur limite vos téléchargements par jour, vous pouvez entrer ce nombre ici pour éviter de dépasser la limite. Une fois la limite de téléchargement atteinte, d'autres requêtes déclencheront une exception non gérée dans les applications \*Arr. D'autres applications peuvent varier.
- (Option avancée) Ratio de partage - Pour les indexeurs de torrents uniquement : le ratio qu'un torrent doit atteindre avant de s'arrêter, vide pour la valeur par défaut de l'application.
- (Option avancée) Durée de partage - Pour les indexeurs de torrents uniquement : la durée pendant laquelle un torrent doit être partagé avant de s'arrêter, vide pour la valeur par défaut de l'application. Les valeurs sont en minutes.
- (Option avancée) Priorité de l'indexeur - Priorité de cet indexeur pour privilégier un indexeur par rapport à un autre dans les scénarios de résolution des conflits de versions. 1 est la priorité la plus élevée et 50 est la priorité la plus basse. Ces priorités seront synchronisées avec les applications \*Arr.

- Testez votre indexeur et si une coche verte apparaît, vous pouvez l'enregistrer. Lorsque vous l'enregistrez, en fonction de vos paramètres de synchronisation, il sera automatiquement ajouté à vos applications.

## Ajout d'une définition YML personnalisée

- Notez que la définition YML est mise en cache pendant une courte période et si vous apportez des modifications à des fins de développement, vous devrez attendre la fin du cache ou redémarrer Prowlarr.
- Si vous souhaitez ajouter un fichier de définition YML compatible avec Cardigann personnalisé pour un indexeur qui n'est pas pris en charge ou pour tester des modifications à une définition existante :
  - Accédez (ou créez) au dossier de définitions personnalisées nommé `Custom` dans le dossier `Definitions` du [dossier des données de l'application Prowlarr](/prowlarr/appdata-directory)
    - Exemples de chemins :
      - Windows : `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux : `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX : `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - Enregistrez le fichier YML compatible avec Cardigann [dans le dossier](/prowlarr/cardigann-yml-definition) et assurez-vous que Prowlarr a les autorisations pour y accéder.

> Le nom de fichier et l'identifiant dans la définition doivent être uniques et ne doivent pas entrer en conflit avec d'autres définitions existantes. Il est fortement conseillé que le nom dans la définition soit également unique.
{.is-info}

# Indexeurs pris en charge

- [Consultez cette page du wiki pour une liste des indexeurs pris en charge à la dernière version nightly.](/prowlarr/supported-indexers/)