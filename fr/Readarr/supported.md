---
title: Readarr Pris en charge
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> Cette page est en cours de construction et nécessite des efforts supplémentaires.{.is-warning}

Cette page est la page de désambiguïsation pour tous les liens wiki "pris en charge" (c'est-à-dire généralement `Plus d'informations` dans l'interface utilisateur).

# Clients de téléchargement

{#downloadclient}

- Aria2 {#aria2}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Flood {#flood}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Voir la page des paramètres](/readarr/settings#download-clients)
  - Étant donné que uTorrent est un logiciel publicitaire et anciennement un logiciel espion, il n'est pas recommandé. La plupart des utilisateurs utilisent qBittorrent.
- Vuze {#vuze}
  - [Voir la page des paramètres](/readarr/settings#download-clients)

# Indexeurs

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
  - Newznab est une API standardisée utilisée par de nombreux sites d'indexation Usenet. De nombreux paramètres prédéfinis sont disponibles, mais tous nécessitent une clé API pour être accessibles.
  - Des applications d'indexation comme [Prowlarr](/prowlarr) et [NZBHydra2](https://github.com/theotherp/nzbhydra2) peuvent fournir des fonctionnalités avancées telles que le suivi des statistiques.
- omgwtfnzbs {#omgwtfnzbs}
  - Un indexeur Usenet privé
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Tracker privé
  > L'implémentation native d'IP Torrents ne prend pas en charge la recherche {.is-info}
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Tracker de torrents exclusivement pour les médias japonais (anime).
  > Nyaa n'apprécie pas l'automatisation et bannit fréquemment votre adresse IP. {.is-info}
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Tracker public
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
- Flux RSS de torrents {#torrentrssindexer}
  - Analyseur générique de flux RSS de torrents.
  > Le flux RSS doit contenir une `pubdate`. La taille de la version est également recommandée. {.is-info}
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Indexeur privé
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab est un jeu de mots entre Torrent et Newznab. Il utilise la même structure et la même syntaxe que la spécification de l'API Newznab, mais expose des attributs spécifiques aux torrents et des fichiers .torrent. Il prend donc en charge un flux RSS récent ET des capacités de recherche dans les archives. La spécification n'est pas maintenue ni prise en charge par l'organisation Newznab. (La même spécification d'API est partagée avec nZEDb)
  - Cela est principalement pris en charge par [Prowlarr](/prowlarr) et [Jackett](https://github.com/Jackett/Jackett)
  - [Voir la page des paramètres](/readarr/settings#indexer-settings)

# Notifications

{#notification}

- Boxcar {#boxcar}
- Script personnalisé {#customscript}
  - Cela vous permet de créer un script personnalisé qui s'exécutera lorsqu'une action particulière se produira. Consultez [Scripts personnalisés](/readarr/custom-scripts) pour plus de détails.
- Discord {#discord}
  - De loin l'un des moyens les plus courants de recevoir des notifications des actions se produisant sur votre Readarr
- E-mail {#email}
  - Envoyez simplement un e-mail à vous-même ou à quelqu'un que vous voulez ennuyer. Si vous utilisez Gmail, vous devez activer les applications moins sécurisées. Si vous utilisez Gmail et que vous avez activé l'authentification à deux facteurs, vous devez utiliser un mot de passe spécifique à l'application.

 > Vous pouvez utiliser une "jolie adresse" comme `UnJoliNom <email@example.org>` {.is-info}

- GoodReads Bookshelves {#goodreadsbookshelf}
- GoodReads Owned Books {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Voir l'entrée sur [Outils utiles - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
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

- GoodReads Bookshelves {#goodreadsbookshelf}
  - (Option avancée) Identifiant utilisateur - Entrez un identifiant utilisateur ici s'il ne s'agit pas de votre identifiant.
  - Étagères de livres - Sélectionnez les étagères de livres à importer depuis GoodReads
  - Authentification avec GoodReads - Cliquez sur le bouton pour vous authentifier avec GoodReads.

> Plusieurs utilisateurs de GoodReads peuvent être ajoutés en tant que listes distinctes. En plus d'utiliser un utilisateur authentifié, d'autres utilisateurs peuvent être ajoutés en activant les options avancées et en entrant l'identifiant utilisateur, puis en cliquant sur Authentifier avec GoodReads pour récupérer les étagères de l'utilisateur.
{.is-info}

- GoodReads Owned Books {#goodreadsownedbooks}
  - (Option avancée) Identifiant utilisateur - Entrez un identifiant utilisateur ici s'il ne s'agit pas de votre identifiant.
  - Étagères de livres - Sélectionnez les étagères de livres à importer depuis GoodReads
  - Authentification avec GoodReads - Cliquez sur le bouton pour vous authentifier avec GoodReads.

> Plusieurs utilisateurs de GoodReads peuvent être ajoutés en tant que listes distinctes. En plus d'utiliser un utilisateur authentifié, d'autres utilisateurs peuvent être ajoutés en activant les options avancées et en entrant l'identifiant utilisateur, puis en cliquant sur Authentifier avec GoodReads pour récupérer les étagères de l'utilisateur.
{.is-info}

- Listes GoodReads {#goodreadslistimportlist}
  - ID de liste - Entrez l'ID de liste publique GoodReads à ajouter en tant que liste
- Séries GoodReads {#goodreadsseriesimportlist}
  - ID de série - Entrez l'ID de série GoodReads à ajouter en tant que liste
- LazyLibrarian {#lazylibrarianimport}
  - URL - URL de votre instance LazyLibrarian
  - Clé API - Clé API de votre instance LazyLibrarian
- Readarr {#readarrimport}
  - URL complète - URL complète de l'instance Readarr à importer, par exemple `http://localhost:8787/readarr`
  - Clé API - Clé API de l'instance Readarr à importer
  - Profils - Profils de l'instance Readarr à importer
  - Tags - Tags de l'instance Readarr à importer

# Métadonnées

{#metadata}

- Calibre {#calibre}
  - [Voir la page des paramètres](/readarr/settings#write-metadata-to-book-files)
- Balises audio {#audiotagging}
  - [Voir la page des paramètres](/readarr/settings#write-metadata-to-book-files)