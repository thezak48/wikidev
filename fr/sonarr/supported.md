---
title: Sonarr Pris en charge
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> Cette page est en cours de construction et nécessite des efforts supplémentaires. {.is-warning}

Cette page est la page de désambiguïsation pour tous les liens wiki "pris en charge" (c'est-à-dire généralement `Plus d'informations` dans l'interface utilisateur).

# Clients de téléchargement

{#downloadclient}

- Aria2 {#aria2}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Flood {#flood}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)
  - Étant donné que uTorrent est un logiciel publicitaire et anciennement un logiciel espion, il n'est pas recommandé. La plupart des utilisateurs utilisent Qbittorrent.
- Vuze {#vuze}
  - [Voir la page des paramètres](/sonarr/settings#download-clients)

# Indexeurs

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - Indexeur Usenet pour les médias japonais (anime) exclusivement.
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
  - Newznab est une API standardisée utilisée par de nombreux sites d'indexation Usenet. De nombreux paramètres prédéfinis sont disponibles, mais tous nécessitent une clé API pour être accessibles.
  - Des applications d'indexation comme [Prowlarr](/prowlarr) et [NZBHydra2](https://github.com/theotherp/nzbhydra2) peuvent fournir des fonctionnalités avancées telles que le suivi des statistiques.
- omgwtfnzbs {#omgwtfnzbs}
  - Une implémentation obsolète d'un indexeur Usenet privé. Utilisez plutôt Newznab.
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)

## Torrents

- BroadcasTheNet (BTN) {#broadcasthenet}
  - Tracker privé
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - Tracker privé
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Tracker privé
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Tracker privé
  > L'implémentation native d'IP Torrents ne prend pas en charge la recherche. Utilisez-la via Prowlarr ou Jackett en tant que torznab à la place {.is-info}
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Tracker torrent pour les médias japonais (anime) exclusivement.
  - Nyaa ne prend en charge que la recherche de types de séries anime.
  - Des problèmes connus existent avec la version native de Sonarr
    - [Nyaa seeders/leechers not parsed properly anymore. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - Cela peut être corrigé lorsque / si [Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637) est fusionné
  - > Nyaa n'apprécie pas l'automatisation et bannit fréquemment votre adresse IP. {.is-warning}
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Tracker public
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- Flux RSS de torrents {#torrentrssindexer}
  - Analyseur générique de flux RSS de torrents.
  > Le flux RSS doit contenir une `pubdate`. La taille de la version est également recommandée.
  {.is-info}
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Indexeur privé
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab est un jeu de mots entre Torrent et Newznab. Il utilise la même structure et la même syntaxe que la spécification de l'API Newznab, mais expose des attributs spécifiques aux torrents et des fichiers .torrent. Il prend donc en charge un flux RSS récent ET des capacités de recherche dans les archives. La spécification n'est pas maintenue ni prise en charge par l'organisation Newznab. (La même spécification d'API est partagée avec nZEDb)
  - Cela est principalement pris en charge par [Prowlarr](/prowlarr) et [Jackett](https://github.com/Jackett/Jackett)
  - [Voir la page des paramètres](/sonarr/settings#indexer-settings)

> De nombreux trackers torrent prospèrent grâce à la communauté et peuvent avoir des règles en place qui exigent des visites sur le site, du karma, des votes, des commentaires, etc.
> Veuillez consulter les règles et l'étiquette de votre tracker pour maintenir votre communauté en vie.
> Nous ne sommes pas responsables si votre compte est banni pour non-respect des règles ou accumulation de Hit and Runs (HnRs)/faible ratio.
{.is-warning}

# Notifications

{#notification}

- Boxcar {#boxcar}
- Script personnalisé {#customscript}
  - Cela vous permet de créer un script personnalisé qui s'exécutera lorsqu'une action particulière se produit. Consultez [Scripts personnalisés](/sonarr/custom-scripts) pour plus de détails.
- Discord {#discord}
  - De loin l'un des moyens les plus courants de recevoir des notifications sur les actions se produisant sur votre Sonarr
  - Types de champs pris en charge :
  `Aperçu, Évaluation, Genres, Qualité, Groupe, Taille, Liens, Version, Affiche, Fanart, Formats personnalisés, Score de format personnalisé, Indexeur`
- Email {#email}
  - Envoyez simplement un e-mail à vous-même ou à quelqu'un que vous voulez ennuyer. Si vous utilisez Gmail, vous devez activer les applications moins sécurisées. Si vous utilisez Gmail et que vous avez activé l'authentification à deux facteurs, vous devez utiliser un mot de passe spécifique à l'application.

> Vous pouvez utiliser une "adresse jolie" comme `NomJoli <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi est né de l'amour des médias. C'est un centre de divertissement qui regroupe tous vos médias numériques dans une interface conviviale et esthétique. Il est entièrement gratuit et open source, très personnalisable et fonctionne sur une grande variété d'appareils. Il est soutenu par une équipe dévouée de bénévoles et une immense communauté. En ajoutant Kodi en tant que connexion, vous pouvez mettre à jour la bibliothèque de Kodi lorsqu'un nouvel épisode est ajouté à Sonarr.
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - Obsolète
- Plex Media Center {#plexclient}
  - Obsolète
- Plex Media Server {#plexserver}
  - Le serveur pour votre système Plex auto-hébergé. L'activation de cette option, tout comme Kodi, vous permettra de pousser une mise à jour vers votre serveur Plex pour lui signaler qu'un nouvel épisode est disponible ou a été mis à niveau.
  - Cela est rarement nécessaire et n'est requis que si Plex ne peut pas surveiller le système de fichiers pour détecter les modifications.
  - Dans les quelques situations où Plex ne peut pas surveiller le système de fichiers à l'aide d'ionotify - comme certains types de montages distants et quelques anciens montages réseau - il est recommandé d'utiliser l'application plexautoscan plutôt que la connexion Plex

> Notez que cela peut déclencher une analyse complète de la bibliothèque pour le dossier racine où se trouve la série. Il est fortement recommandé d'utiliser la fonctionnalité native de Plex qui surveille simplement le système de fichiers ou d'utiliser un outil comme [plexautoscan](https://github.com/l3uddz/plex_autoscan)
{.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Indexeur Synology {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Voir cette [entrée Trucs et astuces](/useful-tools#twitter)
- Webhook {#webhook}

# Listes

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH a [un guide](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/) pour synchroniser deux instances
- Liste de surveillance Plex {#pleximport}
  - Ajoutez simplement une liste de surveillance Plex pour l'utilisateur Plex authentifié à Radarr. Notez qu'il est nécessaire que votre liste contienne des émissions.
  - Pour avoir plusieurs listes d'utilisateurs, vous devrez ajouter les listes de chaque utilisateur et vous authentifier avec leur utilisateur Plex.
- Liste Trakt {#traktlistimport}
  - Nom d'utilisateur - Assurez-vous d'entrer le nom d'utilisateur réel de l'utilisateur et non le nom de l'utilisateur
  - Liste - Assurez-vous d'utiliser le nom de la liste tel qu'il apparaît dans l'URL de la liste
  - Exemple : `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Nom d'utilisateur : `some-user-name`
    - Liste : `trakt-list-name`
- Liste populaire Trakt {#traktpopularimport}
- Utilisateur Trakt {#traktuserimport}

> Les listes Trakt doivent contenir des émissions, pas des épisodes individuels. Sonarr ne correspondra et n'ajoutera que des émissions.
{.is-info}

# Métadonnées

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Activer - Activer la création de fichiers de métadonnées pour ce type de métadonnées
  - Métadonnées de la série - Créer un `tvshow.nfo` avec les métadonnées complètes de la série
  - (Option avancée) URL des métadonnées de la série - Créer un tvshow.nfo avec l'URL de la série TheTVDb
  - Métadonnées de l'épisode - Créer un `<nom de fichier>.nfo` pour chaque épisode
  - Images de la série - Créer différentes images de la série, y compris des affiches et des bannières nommées `poster.jpg` et `banner.jpg`
  - Images de la saison - Créer différentes images de la saison, y compris des affiches et des bannières nommées `season##-poster.jpg` et `season##-banner.jpg`
  - Images de l'épisode - Créer différentes images d'épisode telles que des vignettes nommées `<nom de fichier>-thumb.jpg`
- Roksbox {#roksboxmetadata}
  - Activer - Activer la création de fichiers de métadonnées pour ce type de métadonnées
  - Métadonnées de l'épisode - Créer `Season##\<nom de fichier>.xml` pour chaque épisode
  - Images de la série - Créer `Titre de la série.jpg`
  - Images de la saison - Créer `Saison ##.jpg`
  - Images de l'épisode - Créer `Season##\<nom de fichier>.jpg`
- WDTV {#wdtvmetadata}
  - Activer - Activer la création de fichiers de métadonnées pour ce type de métadonnées
  - Métadonnées de l'épisode - Créer `Season##\<nom de fichier>.xml` pour chaque épisode
  - Images de la série - Créer `folder.jpg`
  - Images de la saison - Créer `Season ##\folder.jpg`
  - Images de l'épisode - Créer `Season##\<nom de fichier>.metathumb`