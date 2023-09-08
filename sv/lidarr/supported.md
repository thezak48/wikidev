---
title: Lidarr Stöd
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> Den här sidan är under arbete och kräver ytterligare ansträngning.{.is-warning}

Den här sidan är en förtydligandesida för alla "stödda" wiki-länkar (vanligtvis `Mer information` i gränssnittet).

# Nedladdningsklienter

{#downloadclient}

- Deluge {#deluge}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Flood {#flood}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se inställningssidan](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se inställningssidan](/lidarr/settings#download-clients)
  - På grund av att uTorrent är adware och tidigare spionprogramvara rekommenderas det inte. De flesta användare använder qBittorrent.
- Vuze {#vuze}
  - [Se inställningssidan](/lidarr/settings#download-clients)

# Indexerare

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
  - Newznab är en standardiserad API som används av många usenet-indexeringssidor. Många förinställningar finns tillgängliga, men alla kräver en API-nyckel för att vara åtkomliga.
  - Indexeringsprogram som [Prowlarr](/prowlarr) och [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan erbjuda avancerade funktioner som statistikspårning.

## Torrents

- FileList {#filelist}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat spårare
  > IP Torrents' inbyggda implementation stöder inte sökning {.is-info}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig spårare
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- Torrent RSS-flöde {#torrentrssindexer}
  - Generisk parser för torrent RSS-flöden.
  > RSS-flödet måste innehålla en `pubdate`. Releasens storlek rekommenderas också.
  {.is-info}
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indexerare
  - [Se inställningssidan](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab är ett ordspel på Torrent och Newznab. Det använder samma struktur och syntax som Newznab API-specifikationen, men exponerar torrent-specifika attribut och .torrent-filer. Stöder därför ett nyligen RSS-flöde OCH möjligheter att söka i arkivet. Specifikationen underhålls inte eller stöds av Newznab-organisationen. (Samma API-specifikation delas med nZEDb)
  - Detta stöds främst av [Prowlarr](/prowlarr) och [Jackett](https://github.com/Jackett/Jackett)
  - [Se inställningssidan](/lidarr/settings#indexer-settings)

# Meddelanden

{#notification}

- Boxcar {#boxcar}
- Anpassad skript {#customscript}
  - Detta gör att du kan skapa ett anpassat skript som körs när en specifik åtgärd inträffar. Se [Anpassade skript](/lidarr/custom-scripts) för mer information.
- Discord {#discord}
  - Långt ifrån en av de vanligaste sätten att skicka meddelanden om händelser som inträffar på din Lidarr
- E-post {#email}
  - Skicka helt enkelt e-post till dig själv eller någon du vill irritera. Om du använder Gmail måste du aktivera mindre säkra appar. Om du använder Gmail och har tvåfaktorsautentisering aktiverat måste du använda ett appspecifikt lösenord.

 > Du kan använda en "snygg adress" som `EttSnyggtNamn <email@example.org>` {.is-info}

- Emby (Media Browser) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi uppstod ur kärleken till media. Det är en underhållningshubb som samlar all din digitala media i en vacker och användarvänlig förpackning. Den är 100% gratis och öppen källkod, mycket anpassningsbar och fungerar på en mängd olika enheter. Den stöds av ett engagerat team av volontärer och en enorm community. Genom att lägga till Kodi som en anslutning kan du uppdatera Kodis bibliotek när en ny låt har lagts till i Lidarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se posten om [Användbara verktyg - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Servern för ditt självhostade Plex-system. Genom att aktivera detta kan du skicka en uppdatering till din Plex-server och meddela att en ny/uppdaterad episod är tillgänglig.
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Se denna [Tips och tricks-post](/useful-tools#twitter)
- Webhook {#webhook}

# Listor

{#importlist}

- Headphones {#headphonesimport}
- Last.fm-tag {#lastfmtag}
- Last.fm-användare {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr-listor {#lidarrlists}
- MusicBrainz-serier {#musicbrainzseries}
- Spotify följda artister {#spotifyfollowedartists}
- Spotify spellistor {#spotifyplaylist}
- Spotify sparade album {#spotifysavedalbums}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}