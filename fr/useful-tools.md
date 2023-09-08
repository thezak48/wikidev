---
title: Outils utiles
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: outils-utiles
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Récupération d'une base de données corrompue](#récupération-dune-base-de-données-corrompue)
  - [Récupération d'une base de données corrompue (UI) (Windows)](#récupération-dune-base-de-données-corrompue-ui-windows)
  - [Récupération de la base de données en ligne de commande](#récupération-de-la-base-de-données-en-ligne-de-commande)
- [Recherche de cookies](#recherche-de-cookies)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [Effacement des cookies et du stockage local](#effacement-des-cookies-et-du-stockage-local)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
  {.links-list}
- [Autres projets et programmes - Applications de demande \*Arrs](#autres-projets-et-programmes-applications-de-demande-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
  {.links-list}
- [Autres projets et programmes - Liés à \*Arr](#autres-projets-et-programmes-liés-à-arr)
  - [Télécommande](#télécommande)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Application Android](#radarr-sonarr-companion-application-android)
    - [nzb360 - Application Android](#nzb360-application-android)
    {.links-list}
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [Sous-titres](#sous-titres)
    - [Bazarr](#bazarr)
- [Autres projets et programmes - Torrents/Téléchargement](#autres-projets-et-programmes-torrentstéléchargement)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [Gestion de qBit](#gestion-de-qbit)
- [Autres projets et programmes](#autres-projets-et-programmes)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
  {.links-list}
- [Instructions de connexion à Twitter](#instructions-de-connexion-à-twitter)

Les applications suivantes sont des compagnons de la suite d'applications \*Arr ou de l'archivage de médias en général. Elles ne sont pas maintenues, développées ou prises en charge par l'équipe de développement \*Arr. Veuillez adresser toutes les questions de support spécifiques à l'équipe de développement de l'application respective.

# Récupération d'une base de données corrompue

Notez que la base de données de l'application peut être trouvée dans le répertoire des données d'application qui sont liés ci-dessous. Le répertoire peut également être passé en argument datadir.

- [Répertoire des données d'application Lidarr](/lidarr/appdata-directory)
- [Répertoire des données d'application Prowlarr](/prowlarr/appdata-directory)
- [Répertoire des données d'application Radarr](/radarr/appdata-directory)
- [Répertoire des données d'application Readarr](/readarr/appdata-directory)
- [Répertoire des données d'application Sonarr](/sonarr/appdata-directory)
{.links-list}

> Il existe deux options pour récupérer la base de données qui sont répertoriées ci-dessous.{.is-info}

- [Utilisation de DB Browser for SQLite et de l'interface utilisateur](#récupération-dune-base-de-données-corrompue-ui)
- [Utilisation de la fonction `.recover` de Sqlite en ligne de commande](#récupération-de-la-base-de-données-en-ligne-de-commande)
{.links-list}

## Récupération d'une base de données corrompue (UI) (Windows)

{#windows}
{#recovering-a-corrupt-db-ui}

> Notez que cela fait essentiellement la même chose que `.recover` qui nécessite Sqlite v3.29 | [Veuillez vous référer à la documentation de Sqlite pour plus de détails sur la commande `.recover`](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database). Les étapes à suivre sont liées ci-dessous {.is-info}

> [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/) est un outil open source de haute qualité, visuel et permettant de créer, concevoir et éditer des fichiers de base de données compatibles avec SQLite. DB4S est destiné aux utilisateurs et aux développeurs qui souhaitent créer, rechercher et éditer des bases de données. DB4S utilise une interface familière de type feuille de calcul et il n'est pas nécessaire d'apprendre des commandes SQL compliquées.
{.is-info}

1. Arrêtez l'application
1. Faites une copie de votre base de données corrompue (`.db`) et copiez également les fichiers `.shm` et `.wal`
1. Ouvrez votre base de données corrompue dans [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/)
1. Fichier => Exporter => Exporter la base de données vers un fichier SQL
1. Sélectionnez toutes les tables
1. Cochez/Activez "Conserver les noms de colonnes dans INSERT INTO"
1. Exporter tout
1. Écraser l'ancien schéma
1. Enregistrer
1. Fermez la base de données
1. Nouvelle base de données => Fichier => Importer => importez ce fichier de l'étape d'exportation précédente
1. En cas d'erreurs d'importation ou de problèmes de contrainte, nettoyez l'instruction d'insertion problématique si possible ou supprimez-la
1. Exécutez la requête SQL suivante `VACUUM;`
1. Enregistrez la base de données lorsque vous y êtes invité.
1. Outils => Vérification de l'intégrité ; le résultat devrait indiquer OK
1. Fermez la base de données
1. Supprimez tous les fichiers `wal`, `shm` et `db` du dossier de configuration
1. Enregistrez (ou copiez, si \*Arr n'est pas sur le même système que DB4S) la nouvelle base de données dans le dossier de configuration et pointez l'application vers celle-ci. Tous les \*Arrs nomment leur base de données `<nomapp>.db` par exemple `radarr.db`
1. Corrigez les autorisations pour la base de données récupérée si nécessaire. Le propriétaire doit être l'utilisateur et le groupe configurés pour exécuter \*Arr.
1. Démarrez l'application

Veuillez noter que le gif ne couvre pas la commande `VACUUM;`

![dbrecover.gif](/dbrecover.gif)

## Récupération de la base de données en ligne de commande

{#nix}

Les instructions ci-dessous sont pour les systèmes d'exploitation \*Nix, mais le concept sera similaire sur la ligne de commande Windows.

> Cela utilise la commande [sqlite3 `.recover`](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database) qui est idéale. Notez qu'elle nécessite Sqlite 3.29+
{.is-info}

> Étant donné que sqlite3 est requis par \*Arrs, il est supposé que vous avez sqlite3 installé sur votre système {.is-info}

1. Arrêtez l'application
1. Connectez-vous en SSH à votre boîte ou ouvrez un terminal
1. Entrez `sqlite3 <chemin vers la base de données corrompue> ".recover" | sqlite3 <chemin de sortie pour la base de données récupérée>`
1. Corrigez les autorisations pour la base de données récupérée si nécessaire. Le propriétaire doit être l'utilisateur et le groupe configurés pour exécuter \*Arr.
1. Supprimez ou déplacez/renommez l'ancienne base de données corrompue et tous les fichiers `wal` ou `shm` du dossier
1. Renommez la base de données récupérée. Tous les \*Arrs nomment leur base de données `<nomapp>.db` par exemple `radarr.db`
1. Démarrez l'application

# Recherche de cookies

- Certains sites ne peuvent pas être connectés automatiquement et nécessitent une connexion manuelle, puis vous devez fournir les cookies pour qu'ils fonctionnent. Les pages ci-dessous décrivent comment faire cela.

## Instructions générales

1. Connectez-vous au site Web avec votre navigateur en utilisant l'adresse du lien du site que vous avez choisi d'utiliser à partir de la configuration de l'indexeur Prowlarr
1. Ouvrez le panneau DevTools en appuyant sur F12
1. Sélectionnez l'onglet Réseau
1. Cliquez sur le bouton Doc (navigateur Chrome) ou sur le bouton HTML (navigateur Firefox)
1. Rafraîchissez la page en appuyant sur F5
1. Cliquez sur la première entrée de la ligne
1. Sélectionnez l'onglet En-têtes dans le panneau de droite
1. Recherchez 'cookie:' dans la section En-têtes de la requête. Consultez le texte d'aide dans l'interface utilisateur de votre tracker pour plus de détails
1. Sélectionnez et copiez la chaîne de cookies entière (tout ce qui se trouve après cookie: )
1. Supprimez tout ce qui se trouve déjà dans la boîte de cookies de configuration de l'indexeur Prowlarr
1. Collez la chaîne de cookies copiée dans cette boîte
1. Cliquez sur Enregistrer

> Si l'agent utilisateur est requis pour votre tracker, il peut être trouvé dans les en-têtes de la requête
{.is-info}

### Notes

- Assurez-vous d'utiliser le navigateur à partir de la même machine sur laquelle s'exécute Prowlarr, car les cookies fonctionnent rarement sur d'autres plates-formes.
- Sur la page de connexion du site Web, ne cochez aucune option qui restreint votre session à une adresse IP ou qui se déconnecte après un court laps de temps. S'il y a une option Se souvenir de moi, utilisez-la.
- Assurez-vous qu'avant de récupérer le cookie, vous pouvez accéder à la page de recherche de torrents du site, car tout ce que le site fait pour empêcher cela (alertes, notifications non lues ou messages privés non lus, ou un avertissement de ratio faible) empêchera Prowlarr de réussir le test après l'utilisation du cookie.

## Chrome

- Accédez au site du tracker de torrents et connectez-vous.

- Appuyez sur F12

- Sous l'onglet Application en haut, il y aura "Stockage" sur le côté gauche. Vous verrez une sous-section "Cookies", et en dessous, vous verrez l'URL de votre tracker. Cliquez dessus.

- Cliquez sur "Pass" sur cet onglet ou une entrée similaire, et une boîte apparaîtra avec la mention "Valeur du cookie" et une chaîne d'environ 25 à 30 caractères. Copiez cela et collez-le dans l'application qui en a besoin.

  - Si la chaîne ressemble à `cid=cid-que-vous-avez-obtenu-à-partir-du-navigateur; sid=sid-que-vous-avez-obtenu-à-partir-du-navigateur`, alors toute l'entrée doit être utilisée.

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- Vous pouvez également consulter les documents de Chrome [Cookies Chrome](https://developer.chrome.com/docs/devtools/storage/cookies/)

## Firefox

- [Veuillez consulter la documentation de Mozilla](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# Effacement des cookies et du stockage local

## Chrome

1. Accédez à `chrome://settings/siteData`
1. Entrez le nom du site (ou de l'application) que vous souhaitez effacer
1. Cliquez sur l'icône de la corbeille pour le site

## Firefox

- Veuillez consulter [l'article d'aide de Mozilla](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)

## Microsoft Edge (Chromium)

1. Accédez à `edge://settings/siteData`
1. Entrez le nom du site (ou de l'application) que vous souhaitez effacer
1. Cliquez sur la flèche pour le site
1. Cliquez sur l'icône de la corbeille pour le site

# Autres projets et programmes - Applications de demande \*Arrs

## Notifiarr (fka Discord Notifier)

[Notifiarr](https://notifiarr.com/) est un outil créé pour faciliter les notifications Discord plus détaillées par l'un des développeurs \*Arr. Il permet d'ajouter des notifications configurables (y compris des réactions) en fonction des déclencheurs que vous choisissez. Le site propose une interface utilisateur pour choisir ce qui doit être affiché dans la notification. Il prend en charge les notifications de Grab, Import, Upgrade, Health et Failed, ainsi que bien d'autres.

[Wiki](https://notifiarr.wiki/)

Points forts

- État de l'application
- Demandes et approbations (\~Ombi)
- Notifications personnalisables des applications \*ARR
- Système de demande avec approbations
- Système de suivi pour les utilisateurs afin de surveiller une série ou un film et être notifié (via des mentions @)
- État du serveur
- Nouvelles fonctionnalités fréquentes

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/) permet aux utilisateurs de demander des films, des séries TV (saisons ou épisodes uniques) et des albums de musique.

## Overseerr

[Overseerr](https://overseerr.dev/) est un outil de gestion des demandes et de découverte de médias conçu pour fonctionner avec votre écosystème Plex existant.

## Petio

[Petio](https://petio.tv/) est une application compagnon tierce disponible pour les propriétaires de serveurs Plex afin de permettre à leurs utilisateurs de demander, d'examiner et de découvrir du contenu.

L'application est conçue pour être instantanément familière et intuitive, même pour les utilisateurs les moins technophiles. Petio vous aidera à gérer les demandes de vos utilisateurs, à vous connecter à d'autres applications tierces telles que Sonarr et Radarr, à informer les utilisateurs lorsque du contenu est disponible et à suivre l'avancement des demandes. Petio permet également aux utilisateurs de découvrir des médias sur votre serveur et en dehors, de trouver rapidement et facilement du contenu connexe et de laisser leur avis pour les autres utilisateurs.

# Autres projets et programmes - Liés à \*Arr

## Télécommande

### LunaSea

[LunaSea](https://www.lunasea.app/) est un contrôleur auto-hébergé entièrement équipé et open source ! Il se concentre sur vous offrir une expérience transparente entre tous vos logiciels multimédias auto-hébergés.

### Radarr & Sonarr Companion - Application Android

Ajoutez facilement de nouveaux films/séries à votre système avec votre téléphone. Application disponible sur [Google Play](https://play.google.com/store/apps/details?id=easy.radarr)

### nzb360 - Application Android

nzb360 permet de gérer Sonarr, Radarr, Lidarr, les torrents, Usenet et d'autres services. Application disponible sur [Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360) Consultez le [site officiel](https://nzb360.com/) pour plus d'informations.

## Lidarr

### AMD

[Téléchargeur de musique automatisé](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd est un script compagnon de Lidarr pour télécharger automatiquement de la musique pour Lidarr

### AMVD

[Téléchargeur de clips musicaux automatisé](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd est un script compagnon de Lidarr pour télécharger et taguer automatiquement des clips musicaux pour une utilisation dans d'autres applications vidéo (plex/kodi/jellyfin/emby)

## Radarr

## AMTD

[Téléchargeur de bandes-annonces de films automatisé](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd est un script compagnon de Radarr pour télécharger automatiquement des bandes-annonces de films et des bonus pour une utilisation dans d'autres applications vidéo (plex/kodi/jellyfin/emby)

## Sous-titres

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr) est une application compagnon de Sonarr et Radarr qui gère et télécharge des sous-titres en fonction de vos besoins.

# Autres projets et programmes - Torrents/Téléchargement

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed) est une application conçue pour vous aider à télécharger des torrents que vous pouvez croiser en fonction de vos torrents existants. Elle est conçue pour faire correspondre de manière conservatrice afin de minimiser les interventions manuelles. Elle prend en charge Jackett et Qbittorrent/rTorrent pour le moment.

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr) fournit une suite d'utilitaires pour résoudre les problèmes avec les applications Starr. Toolbarr vous permet d'effectuer diverses actions sur vos applications Starr et leurs bases de données SQLite3.

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr) Cette application s'exécute en tant que démon sur votre hôte de téléchargement. Elle vérifie les téléchargements terminés et les extrait pour que \*Arr puisse les importer.

Il existe plusieurs options pour extraire et supprimer les fichiers après leur téléchargement par votre client. Captain n'aimait aucune d'entre elles, alors il a écrit la sienne. Il voulait un petit fichier unique avec une journalisation raisonnable qui peut extraire les archives téléchargées et nettoyer le désordre après leur importation.

## Gestion de qBit

[qBit Management alias "qbit_manage"](https://github.com/StuffAnThings/qbit_manage) est un programme utilisé pour gérer votre instance qBittorrent, par exemple :



- Tagger les torrents en fonction de l'URL du tracker (tagger uniquement les torrents qui n'ont pas de tags)
- Mettre à jour les catégories en fonction du répertoire de sauvegarde
- Supprimer les torrents non enregistrés (supprimer les données et le torrent s'il n'est pas en cours de cross-seeding, sinon il supprimera uniquement le torrent)
- Ajouter automatiquement les torrents de cross-seed en état de pause (utilisé en conjonction avec le [script de cross-seed](#cross-seed))
- Vérifier à nouveau les torrents en pause triés par taille la plus petite et les reprendre s'ils sont terminés
- Supprimer les fichiers orphelins de votre répertoire racine qui ne sont pas référencés par qBittorrent
- Tagger les torrents qui n'ont pas de liens physiques et permettre une suppression facultative de ces torrents et de leur contenu en fonction du ratio maximum et/ou du temps de partage

# Autres projets et programmes

## Filebot

[FileBot](https://www.filebot.net/) est l'outil ultime pour organiser et renommer vos films, séries TV et anime, ainsi que pour récupérer les sous-titres et les illustrations. Il est intelligent et fonctionne parfaitement.

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes) est un programme permettant d'identifier et d'agir sur les fichiers en double.

> TRaSH [a un guide](https://trash-guides.info/jdupes) également {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= cela vérifierait les fichiers en double et afficherait un résumé des résultats

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= cela les recréerait en tant que liens physiques, réduisant ainsi l'espace utilisé par les doublons

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md) est un script PowerShell pour rechercher manuellement n éléments qui ne sont pas tagués avec un tag spécifique dans votre bibliothèque multimédia Radarr/Sonarr. n est le nombre d'éléments que ce script recherchera, cela a l'avantage supplémentaire de ne pas surcharger vos indexeurs et d'être banni :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager) est un script Python permettant de mettre à jour les informations de métadonnées pour les films, les séries et les collections, ainsi que de créer automatiquement des collections.

## Tautulli

[Tautulli](https://tautulli.com/) est une application tierce que vous pouvez exécuter aux côtés de votre serveur multimédia Plex pour surveiller l'activité et suivre diverses statistiques. Ces statistiques incluent notamment ce qui a été regardé, qui l'a regardé, quand et où il a été regardé, et comment il a été regardé. La seule chose qui manque, c'est "pourquoi ils l'ont regardé", mais qui suis-je pour remettre en question vos 42 lectures de La Reine des neiges. Toutes les statistiques sont présentées dans une interface agréable et propre avec de nombreux tableaux et graphiques, ce qui facilite la vantardise de votre serveur auprès de tout le monde.

## Tdarr

[Tdarr](https://tdarr.io) est une application web auto-hébergée, non open source, permettant d'automatiser la gestion de la transcodification/remux de la bibliothèque multimédia et de vous assurer que vos fichiers sont exactement comme vous en avez besoin en termes de codecs/flux/conteneurs, etc. Conçu pour fonctionner aux côtés de [Sonarr](/sonarr)/[Radarr](/radarr) et construit dans le but de modularité, de parallélisme et de scalabilité, chaque bibliothèque que vous ajoutez a ses propres paramètres de transcodification, filtres et planning. Les travailleurs peuvent être démarrés et arrêtés selon les besoins et sont répartis en 3 types : "général", "transcodage" et "vérification de l'état de santé". Les limites des travailleurs peuvent être gérées par le planificateur ainsi que manuellement.

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform) est un script personnalisé pour Sonarr et Radarr permettant d'informer Tdarr des nouveaux/fichiers modifiés/supprimés sans dépendre des événements du système de fichiers ou de l'analyse fréquente du disque.

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr) est un outil permettant de supprimer les médias obsolètes et inactifs de Plex/Sonarr/Radarr. Il aide à gérer l'espace limité lorsque vous autorisez les utilisateurs à demander des émissions via Overseerr/Ombi, mais que vous ne souhaitez pas surveiller manuellement l'espace disque disponible. Il est configurable pour ne supprimer que les médias répondant à vos critères définis.

## Connexion Twitter

Créez une application Twitter (si ce n'est pas déjà fait) sur <https://apps.twitter.com/>

Remplissez les champs obligatoires ainsi que l'URL de rappel, définissez-la sur une URL publiquement disponible (pas localhost), elle n'a pas besoin d'exister, mais elle doit être définie, en utilisant <https://sonarr.tv/twitter> ou <https://radarr.video> est suffisant.