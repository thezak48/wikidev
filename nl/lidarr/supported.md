---
title: Lidarr Ondersteund
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> Deze pagina is nog in ontwikkeling en vereist extra inspanning.{.is-warning}

Deze pagina is de verwijzingspagina voor alle "ondersteunde" wiki-links (meestal `Meer informatie` in de gebruikersinterface).

# Download Clients

{#downloadclient}

- Deluge {#deluge}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Flood {#flood}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)
  - Vanwege het feit dat uTorrent adware en voorheen spyware is, wordt het niet aanbevolen. De meeste gebruikers gebruiken qBittorrent.
- Vuze {#vuze}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#download-clients)

# Indexers

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
  - Newznab is een gestandaardiseerde API die wordt gebruikt door veel usenet-indexeringssites. Er zijn veel voorinstellingen beschikbaar, maar deze vereisen allemaal een API-sleutel om toegankelijk te zijn.
  - Indexer-toepassingen zoals [Prowlarr](/prowlarr) en [NZBHydra2](https://github.com/theotherp/nzbhydra2) kunnen geavanceerde mogelijkheden bieden, zoals statistiekregistratie.

## Torrents

- FileList {#filelist}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privé-tracker
  > De native implementatie van IP Torrents ondersteunt geen zoekopdrachten {.is-info}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Openbare tracker
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generieke torrent RSS-feedparser.
  > De RSS-feed moet een `pubdate` bevatten. De grootte van de release wordt ook aanbevolen.
  {.is-info}
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privé-indexer
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab is een woordspeling op Torrent en Newznab. Het gebruikt dezelfde structuur en syntaxis als de Newznab API-specificatie, maar met torrent-specifieke attributen en .torrent-bestanden. Hierdoor worden zowel recente RSS-feeds als backlog-zoekmogelijkheden ondersteund. De specificatie wordt niet onderhouden of ondersteund door de Newznab-organisatie. (Dezelfde API-specificatie wordt gedeeld met nZEDb)
  - Dit wordt voornamelijk ondersteund door [Prowlarr](/prowlarr) en [Jackett](https://github.com/Jackett/Jackett)
  - [Raadpleeg de instellingenpagina](/lidarr/settings#indexer-settings)

# Meldingen

{#notification}

- Boxcar {#boxcar}
- Aangepast script {#customscript}
  - Hiermee kunt u een aangepast script maken dat wordt uitgevoerd wanneer een bepaalde actie plaatsvindt. Zie [Aangepaste scripts](/lidarr/custom-scripts) voor meer informatie.
- Discord {#discord}
  - Veruit een van de meest voorkomende manieren om meldingen te ontvangen van acties die plaatsvinden op uw Lidarr
- E-mail {#email}
  - Stuur eenvoudig een e-mail naar uzelf of naar iemand die u wilt lastigvallen. Als u Gmail gebruikt, moet u minder veilige apps inschakelen. Als u Gmail gebruikt en tweefactorauthenticatie hebt ingeschakeld, moet u een specifiek app-wachtwoord gebruiken.

 > U kunt een "mooi adres" gebruiken zoals `MooieNaam <email@example.org>` {.is-info}

- Emby (Media Browser) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi is ontstaan uit de liefde voor media. Het is een entertainmenthub die al uw digitale media samenbrengt in een mooi en gebruiksvriendelijk pakket. Het is 100% gratis en open source, zeer aanpasbaar en werkt op een breed scala aan apparaten. Het wordt ondersteund door een toegewijd team van vrijwilligers en een enorme community. Door Kodi als verbinding toe te voegen, kunt u de bibliotheek van Kodi bijwerken wanneer er een nieuw nummer aan Lidarr is toegevoegd.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Zie de vermelding over [Handige tools - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - De server voor uw zelfgehoste Plex-systeem. Door dit in te schakelen, kunt u een update naar uw Plex-server pushen om deze op de hoogte te stellen dat er een nieuwe/geüpgradede aflevering beschikbaar is.
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Zie deze [Tips en trucs-vermelding](/useful-tools#twitter)
- Webhook {#webhook}

# Lijsten

{#importlist}

- Headphones {#headphonesimport}
- Last.fm-tag {#lastfmtag}
- Last.fm-gebruiker {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr-lijsten {#lidarrlists}
- MusicBrainz-serie {#musicbrainzseries}
- Spotify gevolgde artiesten {#spotifyfollowedartists}
- Spotify-afspeellijsten {#spotifyplaylist}
- Spotify opgeslagen albums {#spotifysavedalbums}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}