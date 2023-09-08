---
title: Guide de démarrage rapide de Prowlarr
description: 
published: true
date: 2023-04-06T16:04:33.682Z
tags: 
editor: markdown
dateCreated: 2023-04-06T16:04:33.682Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Indexeurs](#indexeurs)
- [Applications](#applications)
  - [Paramètres de l'application](#paramètres-de-lapplication)
- [Clients de téléchargement](#clients-de-téléchargement)
  - [Paramètres du client Usenet](#paramètres-du-client-usenet)
  - [Paramètres du client Torrent](#paramètres-du-client-torrent)
  - [Tester le client de téléchargement](#tester-le-client-de-téléchargement)
- [Configuration terminée](#configuration-terminée)

> Cette page est encore en cours de rédaction et n'est pas complète.

> Pour une description plus détaillée de tous les paramètres, consultez [Prowlarr => Paramètres](/prowlarr/settings)

Dans ce guide, nous allons essayer d'expliquer la configuration de base que vous devez effectuer pour commencer avec Prowlarr. Nous allons passer en revue certaines options que vous pouvez voir à l'écran. Si vous souhaitez approfondir ces options, veuillez consulter la page appropriée dans la FAQ et la documentation pour une explication complète.

> Veuillez noter que dans les captures d'écran et les paramètres de l'interface utilisateur en `orange`, il s'agit d'options avancées. Vous devrez cliquer sur `Afficher les options avancées` en haut de la page pour les rendre visibles.

# Indexeurs

La première chose à configurer dans Prowlarr est les indexeurs. Vous ajouterez chaque indexeur individuellement à Prowlarr.

Cliquez sur `Indexeurs`, puis cliquez sur le + pour ajouter un nouvel indexeur.

![addindexer.png](/assets/prowlarr/addindexer.png)

Tous les indexeurs que vous pouvez ajouter (Usenet et Torrent) sont répertoriés, et vous pouvez taper pour faire correspondre partiellement une entrée existante. Si l'indexeur que vous souhaitez ajouter n'existe pas dans la liste, vous pouvez ajouter "Generic Newznab" (pour Usenet) ou "Generic Torznab" (pour Torrent).

![addgeneric.png](/assets/prowlarr/addgeneric.png)

Certains indexeurs ont des paramètres spéciaux, mais la plupart sont standard comme indiqué.

![addnewindexer.png](/assets/prowlarr/addnewindexer.png)

- Nom - Sélectionnez un nom pour cet indexeur. Lorsqu'il se synchronise avec vos applications, il ajoutera `(Prowlarr)` derrière.
- Activer - Cochez la case pour activer cet indexeur.
- Redirection - Cochez la case si une redirection est nécessaire. Il y a seulement quelques indexeurs où cela est nécessaire pour éviter d'être banni. Si activé, cela transmettra directement le lien de téléchargement à l'application plutôt que de le faire transiter par Prowlarr.

> La redirection est généralement nécessaire uniquement pour quelques indexeurs très spécifiques.

- Profil de synchronisation - Sélectionnez votre profil de synchronisation ici. Vous pouvez les créer dans [`Paramètres` => `Applications`](/prowlarr/settings#applications). Le profil standard par défaut existe déjà et ressemble à ceci :

> Vous pouvez avoir différents paramètres par application en créant plusieurs instances de l'indexeur.

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Sélectionnez l'URL à utiliser pour Prowlarr. Si vide, l'URL par défaut/première est utilisée.
- Lien de téléchargement - Si vous ajoutez un indexeur Torrent, vous devrez peut-être choisir le type de lien de téléchargement à utiliser.
- (Option avancée) Chemin de l'API - Chemin de l'API de l'indexeur. Généralement `/api`
- Identifiants - De nombreux indexeurs et trackers nécessitent une authentification/connexion d'une manière ou d'une autre. Vous devrez peut-être entrer une clé API, une clé RSS, un ID de session, un cookie ou d'autres identifiants provenant de votre indexeur (généralement trouvés sur votre page de profil ou sous Sécurité), sélectionner des ordres de recherche ou d'autres options spécifiques à votre indexeur.
  - Clé API
  - Clé RSS
  - ID de session
  - Cookie
  - Nom d'utilisateur/Mot de passe
  - etc.
- (Option avancée) Paramètres supplémentaires - Paramètres supplémentaires à ajouter aux requêtes pour cet indexeur.
- Expiration VIP - Entrez la date au format ISO (aaaa-MM-jj) pour être notifié 1 semaine avant l'expiration ; sinon, laissez vide
- Balises - Utilisez des balises pour spécifier les clients de téléchargement par défaut, spécifier des proxys d'indexeur, spécifier des indexeurs aux applications ou simplement organiser vos indexeurs.
- (Option avancée) Limite de requête - Si votre indexeur limite vos requêtes API par jour, vous pouvez entrer ce nombre ici pour éviter de dépasser la limite.
- (Option avancée) Limite de téléchargement - Si votre indexeur limite vos téléchargements par jour, vous pouvez entrer ce nombre ici pour éviter de dépasser la limite. Une fois la limite de téléchargement atteinte, d'autres requêtes déclencheront une exception non gérée dans les applications \*Arr. D'autres applications peuvent varier.
- (Option avancée) Ratio de partage - Pour les indexeurs Torrent uniquement : le ratio qu'un torrent doit atteindre avant de s'arrêter, vide est la valeur par défaut de l'application
- (Option avancée) Durée de partage - Pour les indexeurs Torrent uniquement : la durée pendant laquelle un torrent doit être partagé avant de s'arrêter, vide est la valeur par défaut de l'application
- (Option avancée) Priorité de l'indexeur - Sélectionnez la priorité de l'indexeur ici de 1 à 50 (1 étant la plus élevée). Ces priorités seront synchronisées avec vos applications.

Testez votre entrée. Si une coche verte apparaît, vous pouvez enregistrer votre entrée et répéter l'opération si nécessaire pour chaque indexeur que vous souhaitez utiliser avec Prowlarr. S'il échoue, vous devrez vérifier votre journal pour l'erreur (URL, clé API, etc.).

# Applications

Une fois que vous avez ajouté vos indexeurs, vous pouvez connecter Prowlarr à vos autres applications.

Cliquez sur `Paramètres` => `Applications`, puis cliquez sur le + pour ajouter une application prise en charge.

![addapps.png](/assets/prowlarr/addapps.png)

Tous les programmes que vous pouvez ajouter sont répertoriés. Vous ne devez ajouter que les programmes que vous avez déjà installés, et si vous en avez plusieurs instances, vous devez les ajouter séparément.

> Les applications actuellement prises en charge peuvent être trouvées sur la page [Plus d'informations (Prises en charge)](/prowlarr/supported#applications) pour cette section

Lorsque vous ajoutez une application, vous devrez saisir des valeurs dans la fenêtre contextuelle :

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Remarque : Les indexeurs sont synchronisés en fonction des fonctionnalités/catégories qu'ils prétendent prendre en charge. Si un indexeur ne prend en charge que les catégories `tv`, il ne sera pas synchronisé avec Lidarr, Radarr et Readarr. Il sera uniquement synchronisé avec Sonarr. Les catégories "Prises en charge" peuvent être sélectionnées comme paramètre avancé pour chaque application. **Notez également que les \*Arr n'acceptent que les indexeurs dont les requêtes de test renvoient des résultats contenant au moins l'une des catégories configurées.**

## Paramètres de l'application

- Nom - Saisissez un nom pour cette application.
- Niveau de synchronisation - Sélectionnez le niveau de synchronisation à utiliser
  - `Ajouter et supprimer uniquement` - Lorsque des indexeurs sont ajoutés ou supprimés de Prowlarr, cela mettra à jour cette application distante. Si l'indexeur est indisponible au moment de la synchronisation, il sera désactivé dans l'application distante.
  - `Synchronisation complète` - La synchronisation complète maintiendra les indexeurs de cette application entièrement synchronisés. Les modifications apportées aux indexeurs dans Prowlarr sont ensuite synchronisées avec cette application. Toute modification apportée aux paramètres sur la FAQ pour ces indexeurs à distance dans cette application sera remplacée par Prowlarr lors de la prochaine synchronisation. Une liste des facteurs utilisés pour comparer et déterminer si une synchronisation doit avoir lieu peut être trouvée dans la [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Désactivé` - empêchera la synchronisation des indexeurs avec le programme.

> `Synchronisation complète` signifie que Prowlarr remplacera la plupart des paramètres, y compris les catégories sélectionnées par l'utilisateur configurables dans Prowlarr. Cependant, les paramètres gérés par Prowlarr ne seront pas modifiés. Cependant, [presque tous les autres facteurs de modifications](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) déclencheront une synchronisation et écraseront les paramètres correspondants dans les \*Arr
{.is-warning}

- Balises - Si vous avez ajouté une balise à votre indexeur lors de la configuration, seuls les indexeurs avec cette balise seront utilisés pour cette entrée de programme.
- Serveur Prowlarr - Saisissez l'URL du serveur Prowlarr (y compris http, le port et l'URL de base si nécessaire) telle que l'application y accéderait ici.

> Notez que si vous utilisez un proxy inverse, vous devez ajouter l'URL de base à cela ! Si vous ne le faites pas, lorsque les indexeurs se synchronisent, ils seront cassés, et si vous avez sélectionné Ajouter et supprimer uniquement, cela ne sera pas corrigé lorsque vous l'éditez !

- Serveur de l'application - Saisissez l'URL du serveur de l'application (y compris http, le port et l'URL de base si nécessaire) ici. Encore une fois, saisissez l'URL de base complète si elle est utilisée.
- Clé API - Saisissez la clé API de votre programme ici. Pour les \*Arrs, vous pouvez la trouver dans Paramètres => Général. Vous pouvez l'obtenir à partir de votre programme dans l'onglet `Paramètres` => `Général`, puis la copier/coller ici.
- (Paramètre avancé) Synchroniser les catégories - Sélectionnez les catégories à synchroniser avec cette application. Les indexeurs prenant en charge ces catégories seront synchronisés.
  - Les catégories personnalisées de l'indexeur sont mappées dans les catégories Torznab/Newznab standard, de sorte que la recherche des catégories standard inclut toutes les catégories personnalisées sous-jacentes. Les catégories personnalisées de l'indexeur sont répertoriées pour un réglage fin si vous ne les voulez pas toutes en même temps.

> Lorsque vous enregistrez cela, cela va synchroniser vos indexeurs avec l'application. Ils sont tous ajoutés avec le nom que vous avez choisi pour votre indexeur suivi de (Prowlarr). par exemple `{Nom de l'indexeur} (Prowlarr)`

![nzbgeek.png](/assets/prowlarr/nzbgeek.png)

Vous devriez ensuite entrer dans votre programme et désactiver la version non-Prowlarr de l'indexeur. Une fois que tout fonctionne correctement, vous pouvez supprimer ces entrées et ne laisser que les versions (Prowlarr) à leur place.

Vous voudrez peut-être vérifier les catégories des indexeurs Prowlarr dans vos programmes. Les catégories par défaut à mapper dans l'application sont configurables en tant que paramètre avancé pour l'application dans Prowlarr.

> **Veuillez noter que les catégories spécifiques à l'indexeur personnalisées/non standard sont mappées sur des catégories standard, donc la recherche avec des catégories standard inclura toutes les catégories personnalisées**

## Profils de synchronisation

Configurez les profils de synchronisation à utiliser pour une ou plusieurs applications

- Nom - Nom unique du profil de synchronisation
- Activer RSS - Pour les indexeurs avec ce profil, activer les recherches/interrogations RSS pour l'application \*Arr
- Activer la recherche interactive - Pour les indexeurs avec ce profil, activer les recherches interactives (manuelles) pour l'application \*Arr
- Activer la recherche automatique - Pour les indexeurs avec ce profil, activer les recherches automatiques pour l'application \*Arr
- Nombre minimum de sources - Pour les indexeurs avec ce profil, le nombre minimum de sources requis pour que \*Arr récupère un torrent

# Clients de téléchargement (Recherches Prowlarr)

> Si vous avez l'intention de faire des recherches directement dans Prowlarr, vous devez ajouter des clients de téléchargement. Sinon, vous n'avez pas besoin de les ajouter ici. Pour les recherches à partir de vos applications, les clients de téléchargement configurés là-bas sont utilisés à la place.

> Les clients de téléchargement sont uniquement destinés aux recherches dans l'application Prowlarr et ne se synchronisent pas avec les applications. Il n'est pas prévu d'ajouter une telle fonctionnalité.

Cliquez sur `Paramètres` => `Clients de téléchargement`, puis cliquez sur le + pour ajouter un nouveau client de téléchargement. Votre client de téléchargement doit déjà être configuré selon ce guide.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

> Les clients de téléchargement actuellement pris en charge peuvent être trouvés sur la page [Plus d'informations (Pris en charge)](/prowlarr/supported#downloadclient) pour cette section

Sélectionnez le client de téléchargement que vous souhaitez ajouter, et une boîte contextuelle s'affichera pour saisir les détails de connexion. Ces détails sont similaires pour la plupart des clients. Certains vous demanderont un nom d'utilisateur ou un mot de passe, d'autres vous demanderont si vous souhaitez ajouter de nouveaux téléchargements en pause/en cours, etc.
![nzbget.png](/assets/prowlarr/nzbget.png)

> La priorité du client n'a d'importance que lorsque 2 clients du même type (Usenet ou Torrent) sont ajoutés. 1 est la priorité la plus élevée, et si plusieurs clients du même type existent et ont la même priorité, Prowlarr les alternera.

## Paramètres du client Usenet

- Nom - Le nom du client de téléchargement dans Prowlarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- URL de base - Ajoutez un préfixe à l'URL ; cela est souvent nécessaire pour les proxys inverses.
- Clé API - la clé API pour s'authentifier auprès de votre client
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Catégorie - la catégorie dans votre client de téléchargement que Prowlarr utilisera
- Priorité - priorité du client de téléchargement pour les éléments ajoutés
- Priorité du client - Priorité du client de téléchargement dans Prowlarr. Le round-robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité.

## Paramètres du client Torrent

- Nom - Le nom du client de téléchargement dans Prowlarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- URL de base - Ajoutez un préfixe à l'URL ; cela est souvent nécessaire pour les proxys inverses.
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client
- Catégorie - la catégorie dans votre client de téléchargement que Prowlarr utilisera
- Priorité - priorité du client de téléchargement pour les éléments ajoutés
- État initial - État initial des torrents (uniquement pour Qbittorrent : Forcé ignore tous les seuils de partage)
- Priorité du client - Priorité du client de téléchargement dans Prowlarr. Le round-robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité.

## Tester le client de téléchargement

Testez votre entrée. Si une coche verte apparaît, vous pouvez enregistrer votre entrée et répéter l'opération si nécessaire pour chaque client de téléchargement que vous souhaitez utiliser avec Prowlarr. S'il échoue, vous devrez vérifier votre journal pour l'erreur (connexion, identifiants, etc.).

# Configuration terminée

C'est tout pour les bases ! Vous pouvez ensuite ajouter des notifications et d'autres options de configuration plus avancées selon vos besoins. Celles-ci sont documentées dans la page complète des paramètres.