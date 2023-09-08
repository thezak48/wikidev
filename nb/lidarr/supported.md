---
title: Lidarr Støttet
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> Denne siden er under arbeid og krever ytterligere innsats.{.is-warning}

Denne siden er en avklaringsside for alle "støttede" wiki-lenker (dvs. vanligvis `Mer informasjon` i brukergrensesnittet).

# Nedlastingsklienter

{#downloadclient}

- Deluge {#deluge}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Flood {#flood}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se innstillingssiden](/lidarr/settings#download-clients)
  - På grunn av at uTorrent er adware og tidligere spionprogramvare, anbefales det ikke. De fleste brukere bruker qBittorrent.
- Vuze {#vuze}
  - [Se innstillingssiden](/lidarr/settings#download-clients)

# Indekserer

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
  - Newznab er en standardisert API som brukes av mange usenet-indeksnettsteder. Mange forhåndsinnstillinger er tilgjengelige, men alle krever en API-nøkkel for å være tilgjengelige.
  - Indekseringsprogrammer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan gi avanserte funksjoner som statistikksporing.

## Torrenter

- FileList {#filelist}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents' egen implementering støtter ikke søk {.is-info}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-parser.
  > RSS-feeden må inneholde en `pubdate`. Det anbefales også å inkludere utgivelsesstørrelsen.
  {.is-info}
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indekserer
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er et ordspill på Torrent og Newznab. Det bruker den samme strukturen og syntaksen som Newznab API-spesifikasjonen, men eksponerer torrent-spesifikke attributter og .torrent-filer. Støtter derfor en nylig RSS-feed OG bakloggsøkefunksjoner. Spesifikasjonen vedlikeholdes ikke og støttes ikke av Newznab-organisasjonen. (Den samme API-spesifikasjonen deles med nZEDb)
  - Dette støttes primært av [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se innstillingssiden](/lidarr/settings#indexer-settings)

# Varsler

{#notification}

- Boxcar {#boxcar}
- Egendefinert skript {#customscript}
  - Dette lar deg lage et egendefinert skript som kjører når en bestemt handling skjer. Se [Egendefinerte skript](/lidarr/custom-scripts) for mer informasjon.
- Discord {#discord}
  - Langt på vei en av de vanligste måtene å sende varsler om handlinger som skjer på Lidarr
- E-post {#email}
  - Send enkelt deg selv eller noen du vil plage med e-post. Hvis du bruker Gmail, må du aktivere mindre sikre apper. Hvis du bruker Gmail og har tofaktorautentisering aktivert, må du bruke et appspesifikt passord.

 > Du kan bruke en "pen adresse" som `NoeFintNavn <epost@example.org>` {.is-info}

- Emby (Media Browser) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi oppsto fra kjærligheten til media. Det er en underholdningshub som samler all digital media på en vakker og brukervennlig måte. Den er 100% gratis og åpen kildekode, veldig tilpasningsdyktig og kjører på et bredt utvalg av enheter. Den støttes av et dedikert team av frivillige og et stort samfunn. Ved å legge til Kodi som en tilkobling kan du oppdatere Kodis bibliotek når en ny sang er lagt til i Lidarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se oppføringen om [Nyttige verktøy - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Serveren for ditt selvhostede Plex-system. Å aktivere dette er mye som med Kodi, og vil tillate deg å sende en oppdatering til Plex-serveren din som varsler om at en ny/oppgradert episode er tilgjengelig.
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology-indeks {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Se denne [Tips og triks-oppføringen](/useful-tools#twitter)
- Webhook {#webhook}

# Lister

{#importlist}

- Headphones {#headphonesimport}
- Last.fm-tag {#lastfmtag}
- Last.fm-bruker {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr-lister {#lidarrlists}
- MusicBrainz-serier {#musicbrainzseries}
- Spotify fulgte artister {#spotifyfollowedartists}
- Spotify-spillelister {#spotifyplaylist}
- Spotify-lagrede album {#spotifysavedalbums}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}