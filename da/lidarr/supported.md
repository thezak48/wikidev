---
title: Understøttet af Lidarr
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> Denne side er under udarbejdelse og kræver yderligere indsats.{.is-warning}

Denne side er en afklaringsside for alle "understøttede" wiki-links (dvs. typisk `Mere info` i brugergrænsefladen).

# Downloadklienter

{#downloadclient}

- Deluge {#deluge}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Flood {#flood}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se indstillingerne](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se indstillingerne](/lidarr/settings#download-clients)
  - På grund af at uTorrent er adware og tidligere spyware, anbefales det ikke. De fleste brugere bruger qBittorrent.
- Vuze {#vuze}
  - [Se indstillingerne](/lidarr/settings#download-clients)

# Indekseringsværktøjer

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
  - Newznab er en standardiseret API, der bruges af mange usenet-indekseringssider. Der er mange forudindstillinger, men alle kræver en API-nøgle for at være tilgængelige.
  - Indekseringsapplikationer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan give avancerede funktioner som statistiksporing.

## Torrents

- FileList {#filelist}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents' native implementering understøtter ikke søgning {.is-info}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-parser.
  > RSS-feedet skal indeholde en `pubdate`. Det anbefales også at inkludere filstørrelsen.
  {.is-info}
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indekseringsside
  - [Se indstillingerne](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er en ordleg på Torrent og Newznab. Den bruger den samme struktur og syntaks som Newznab API-specifikationen, men eksponerer torrent-specifikke attributter og .torrent-filer. Derfor understøtter den både en nyere RSS-feed og baglog-søgefunktioner. Specifikationen vedligeholdes ikke og understøttes ikke af Newznab-organisationen. (Den samme API-specifikation deles med nZEDb)
  - Dette understøttes primært af [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se indstillingerne](/lidarr/settings#indexer-settings)

# Notifikationer

{#notification}

- Boxcar {#boxcar}
- Brugerdefineret script {#customscript}
  - Dette giver dig mulighed for at oprette et brugerdefineret script, der skal køres, når en bestemt handling finder sted. Se [Brugerdefinerede scripts](/lidarr/custom-scripts) for flere detaljer.
- Discord {#discord}
  - Langt den mest almindelige måde at sende notifikationer om handlinger, der finder sted i din Lidarr.
- E-mail {#email}
  - Send en e-mail til dig selv eller en person, du gerne vil genere. Hvis du bruger Gmail, skal du aktivere mindre sikre apps. Hvis du bruger Gmail og har aktiveret totrinsbekræftelse, skal du bruge et app-specifikt kodeord.

 > Du kan bruge en "pæn adresse" som f.eks. `NogetFlotNavn <email@example.org>` {.is-info}

- Emby (Media Browser) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi opstod ud af kærligheden til medier. Det er en underholdningshub, der samler al din digitale medieindhold i en smuk og brugervenlig pakke. Det er 100% gratis og open source, meget tilpasseligt og kan køre på en bred vifte af enheder. Det understøttes af et dedikeret team af frivillige og et stort fællesskab. Ved at tilføje Kodi som en forbindelse kan du opdatere Kodis bibliotek, når en ny sang er blevet tilføjet til Lidarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se indgangen om [Nyttige værktøjer - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Serveren til dit selvhostede Plex-system. Ved at aktivere dette kan du, ligesom med Kodi, sende en opdatering til din Plex-server for at informere den om, at en ny/forbedret episode er tilgængelig.
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Se denne [Tips og tricks-indgang](/useful-tools#twitter)
- Webhook {#webhook}

# Lister

{#importlist}

- Headphones {#headphonesimport}
- Last.fm-tag {#lastfmtag}
- Last.fm-bruger {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr-lister {#lidarrlists}
- MusicBrainz-serier {#musicbrainzseries}
- Spotify fulgte kunstnere {#spotifyfollowedartists}
- Spotify-playlister {#spotifyplaylist}
- Spotify gemte albums {#spotifysavedalbums}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}