---
title: Lidarr Pris en charge
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> Cette page est en cours de construction et nécessite des efforts supplémentaires.{.is-warning}

Cette page est la page de désambiguïsation pour tous les liens wiki "pris en charge" (c'est-à-dire généralement `Plus d'informations` dans l'interface utilisateur).

# Clients de téléchargement

{#downloadclient}

- Deluge {#deluge}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Flood {#flood}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)
  - Étant donné que uTorrent est un logiciel publicitaire et anciennement un logiciel espion, il n'est pas recommandé. La plupart des utilisateurs utilisent qBittorrent.
- Vuze {#vuze}
  - [Voir la page des paramètres](/lidarr/settings#download-clients)

# Indexeurs

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
  - Newznab est une API standardisée utilisée par de nombreux sites d'indexation Usenet. De nombreux paramètres prédéfinis sont disponibles, mais tous nécessitent une clé API pour être accessibles.
  - Des applications d'indexation comme [Prowlarr](/prowlarr) et [NZBHydra2](https://github.com/theotherp/nzbhydra2) peuvent fournir des fonctionnalités avancées telles que le suivi des statistiques.

## Torrents

- FileList {#filelist}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Tracker privé
  > L'implémentation native d'IP Torrents ne prend pas en charge la recherche {.is-info}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Tracker public
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- Flux RSS Torrent {#torrentrssindexer}
  - Analyseur de flux RSS torrent générique.
  > Le flux RSS doit contenir une `pubdate`. La taille de la version est également recommandée.
  {.is-info}
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Indexeur privé
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab est un jeu de mots entre Torrent et Newznab. Il utilise la même structure et la même syntaxe que la spécification de l'API Newznab, mais expose des attributs spécifiques aux torrents et des fichiers .torrent. Il prend donc en charge un flux RSS récent ET des capacités de recherche dans les archives. La spécification n'est pas maintenue ni prise en charge par l'organisation Newznab. (La même spécification d'API est partagée avec nZEDb)
  - Cela est principalement pris en charge par [Prowlarr](/prowlarr) et [Jackett](https://github.com/Jackett/Jackett)
  - [Voir la page des paramètres](/lidarr/settings#indexer-settings)

# Notifications

{#notification}

- Boxcar {#boxcar}
- Script personnalisé {#customscript}
  - Cela vous permet de créer un script personnalisé qui s'exécutera lorsqu'une action particulière se produit. Consultez [Scripts personnalisés](/lidarr/custom-scripts) pour plus de détails.
- Discord {#discord}
  - De loin l'un des moyens les plus courants de recevoir des notifications des actions se produisant sur votre Lidarr
- Email {#email}
  - Envoyez simplement un e-mail à vous-même ou à quelqu'un que vous souhaitez ennuyer. Si vous utilisez Gmail, vous devez activer les applications moins sécurisées. Si vous utilisez Gmail et avez activé l'authentification à deux facteurs, vous devez utiliser un mot de passe spécifique à l'application.

 > Vous pouvez utiliser une "jolie adresse" comme `SomePrettyName <email@example.org>` {.is-info}

- Emby (Media Browser) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi est né de l'amour des médias. C'est un hub de divertissement qui rassemble tous vos médias numériques dans un package beau et convivial. Il est 100% gratuit et open source, très personnalisable et fonctionne sur une grande variété d'appareils. Il est soutenu par une équipe dévouée de bénévoles et une énorme communauté. En ajoutant Kodi en tant que connexion, vous pouvez mettre à jour la bibliothèque de Kodi lorsqu'une nouvelle chanson est ajoutée à Lidarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Voir l'entrée sur [Outils utiles - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Serveur multimédia Plex {#plexserver}
  - Le serveur pour votre système Plex auto-hébergé. En activant cette fonctionnalité, vous pourrez envoyer une mise à jour à votre serveur Plex pour lui signaler qu'un nouvel épisode ou une mise à jour est disponible.
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Indexeur Synology {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Voir cette entrée [Trucs et astuces](/useful-tools#twitter)
- Webhook {#webhook}

# Listes

{#importlist}

- Headphones {#headphonesimport}
- Balise Last.fm {#lastfmtag}
- Utilisateur Last.fm {#lastfmuser}
- Lidarr {#lidarrimport}
- Listes Lidarr {#lidarrlists}
- Série MusicBrainz {#musicbrainzseries}
- Artistes suivis sur Spotify {#spotifyfollowedartists}
- Playlists Spotify {#spotifyplaylist}
- Albums enregistrés sur Spotify {#spotifysavedalbums}

# Métadonnées

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}