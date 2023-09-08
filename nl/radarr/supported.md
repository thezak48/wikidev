---
title: Radarr Ondersteund
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# Inhoudsopgave

> Deze pagina is nog in ontwikkeling en vereist extra inspanning.{.is-warning}

Deze pagina is de verduidelijkingspagina voor alle `ondersteunde` wiki-links (meestal "meer informatie" in de UI).

# Download Clients

{#downloadclient}

- Aria2 {#aria2}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Flood {#flood}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)
  - Vanwege het feit dat uTorrent adware en voorheen spyware is, wordt het niet aanbevolen. De meeste gebruikers gebruiken Qbittorrent.
- Vuze {#vuze}
  - [Raadpleeg de instellingenpagina](/radarr/settings#download-clients)

# Indexers

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
  - Newznab is een gestandaardiseerde API die wordt gebruikt door veel usenet-indexeringssites. Er zijn veel voorinstellingen beschikbaar, maar allemaal vereisen ze een API-sleutel om toegankelijk te zijn.
  - Indexer-toepassingen zoals [Prowlarr](/prowlarr) en [NZBHydra2](https://github.com/theotherp/nzbhydra2) kunnen geavanceerde mogelijkheden bieden, zoals statistiektracking.
- omgwtfnzbs {#omgwtfnzbs}
  - Een verouderde legacy-implementatie van een privé-usenet-indexer. Gebruik in plaats daarvan Newznab.
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - Prive-tracker
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Prive-tracker
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Prive-tracker
  > De native implementatie van IP Torrents ondersteunt geen zoekopdrachten. Gebruik het via Prowlarr of Jackett als torznab in plaats daarvan {.is-info}
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker exclusief voor Japanse media (anime).
  > Nyaa is geen voorstander van automatisering en zal vaak je IP-adres blokkeren. {.is-info}
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - Prive-tracker
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Openbare tracker
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generieke torrent RSS-feedparser.
  > De RSS-feed moet een `pubdate` bevatten. De grootte van de release wordt ook aanbevolen. {.is-info}
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - Een verouderd Couchpotato-formaat voor Torznab.
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab is een woordspeling op Torrent en Newznab. Het gebruikt dezelfde structuur en syntaxis als de Newznab API-specificatie, maar exposeert torrent-specifieke attributen en .torrent-bestanden. Hierdoor worden zowel recente RSS-feeds als zoekmogelijkheden in het archief ondersteund. De specificatie wordt niet onderhouden of ondersteund door de Newznab-organisatie. (Dezelfde API-specificatie wordt gedeeld met nZEDb)
  - Dit wordt voornamelijk ondersteund door [Prowlarr](/prowlarr) en [Jackett](https://github.com/Jackett/Jackett)
  - [Raadpleeg de instellingenpagina](/radarr/settings#indexer-settings)

> Veel torrent-trackers gedijen op de gemeenschap en hebben regels die sitebezoeken, karma, stemmen, opmerkingen, enz. vereisen.
> Bekijk de regels en etiquette van je tracker en houd je gemeenschap levend.
> We zijn niet verantwoordelijk als je account wordt verbannen vanwege het niet naleven van de regels of het oplopen van Hit and Runs (HnR's)/lage ratio's.
{.is-warning}

# Meldingen

{#notification}

- Boxcar {#boxcar}
- Aangepast script {#customscript}
  - Hiermee kunt u een aangepast script maken dat wordt uitgevoerd wanneer een bepaalde actie plaatsvindt. Zie [Aangepaste scripts](/radarr/custom-scripts) voor meer informatie.
- Discord {#discord}
  - Veruit een van de meest voorkomende manieren om meldingen te ontvangen van acties die plaatsvinden op je Radarr
- E-mail {#email}
  - Stuur eenvoudig een e-mail naar jezelf of naar iemand die je wilt lastigvallen. Als je Gmail gebruikt, moet je minder veilige apps inschakelen. Als je Gmail gebruikt en tweefactorauthenticatie hebt ingeschakeld, moet je een specifiek app-wachtwoord gebruiken.

> Je kunt een "mooi adres" gebruiken zoals `MooieNaam <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi is ontstaan uit de liefde voor media. Het is een entertainmenthub die al je digitale media samenbrengt in een mooi en gebruiksvriendelijk pakket. Het is 100% gratis en open source, zeer aanpasbaar en werkt op een breed scala aan apparaten. Het wordt ondersteund door een toegewijd team van vrijwilligers en een enorme community. Door Kodi als verbinding toe te voegen, kun je de bibliotheek van Kodi bijwerken wanneer er een nieuwe film aan Radarr is toegevoegd.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Zie de vermelding over [Handige tools - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - De server voor je zelfgehoste Plex-systeem. Door dit in te schakelen, kun je een update naar je Plex-server sturen om deze op de hoogte te stellen dat er een nieuwe/geüpgradede film beschikbaar is.
  - Dit is zelden nodig en is alleen vereist als Plex niet in staat is om wijzigingen in het bestandssysteem te volgen.
  - In de handvol situaties waarin Plex niet in staat is om het bestandssysteem te volgen met behulp van ionotify - zoals bepaalde soorten externe mounts en een handvol oudere netwerkmounts - wordt aangeraden om de app plexautoscan te gebruiken in plaats van de Plex-verbinding.
- Een tool zoals [plexautoscan](https://github.com/l3uddz/plex_autoscan) is een andere optie.

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Trakt {#trakt}
- Twitter {#twitter}
  - Zie deze [Tips en trucs-vermelding](/useful-tools#twitter)
- Webhook {#webhook}

# Lijsten

{#importlist}

- CouchPotato {#couchpotatoimport}
- Aangepaste lijsten {#radarrlistimport}
- IMDb-lijsten {#imdblistimport}
  - Om je IMDb-kijklijst toe te voegen, ga je naar je lijst en klik je op bewerken. Zorg ervoor dat de privacy-instelling is ingesteld op openbaar. In de adresbalk vind je het `lsxxxxxx`-nummer dat je in Radarr moet invoeren.

    1. Ga naar de instellingen van je IMDb-lijst
    1. Zorg ervoor dat Privacy is ingesteld op `Openbaar` (dwz `Uitgeschakeld`)
    1. Gebruik het `ls`-nummer in de URL

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex-kijklijst {#plex}
  - Vereist: v4.1.0.6176+
  - Voeg eenvoudig een Plex-kijklijst toe voor de geauthenticeerde Plex-gebruiker aan Radarr. Let op dat je lijst films moet bevatten.
  - Om meerdere gebruikerslijsten te hebben, moet je de lijsten van elke gebruiker toevoegen en authenticeren met hun Plex-gebruiker.
- Radarr {#radarrimport}
  - TRaSH heeft [een handleiding](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) voor het synchroniseren van twee instanties
- RSS-lijst {#rssimport}
- StevenLu Aangepast {#stevenluimport}
	- Hiermee kun je aangepaste filmlisten maken in JSON-indeling.
  	Je feed moet voor elke film een `title` of een `imdb_id` bevatten, beide kunnen worden verstrekt.
  		> Merk op dat `imdb_id` veiliger is dan `title`, omdat het geen brede zoekopdracht vereist
    Hier is een voorbeeld van een geldige JSON:
      ```
      [
          {
            "title": "The Wastetown",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/6J32RMp8uko8CUEM3rYP962hQun.jpg",
            "imdb_id": "tt22889064"
          },
          {
            "title": "Wild Sunflowers",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/tHK4c0UZKrqkmXZ2HJeGNhNetRz.jpg",
            "imdb_id": "tt13774830"
          }
      ]
      ```
      - Er kunnen extra sleutels worden toegevoegd in items (worden genegeerd)
      - Voor een lege lijst retourneer je gewoon een lege JSON-array `[]`
- StevenLu Lijst {#stevenlu2import}
- TMDb-collectie {#tmdbcollectionimport}
  - Collectielijsten worden niet langer ondersteund in Radarr v4.2 en zijn gemigreerd naar collecties binnen Radarr. Zie het gedeelte [Collecties](/radarr/library#collections) voor meer informatie.
- TMDb-bedrijf {#tmdbcompanyimport}
- TMDb-zoekwoord {#tmdbkeywordimport}
- TMDb-lijst {#tmdblistimport}
- TMDb-persoon {#tmdbpersonimport}
  - Als de TMDb-persoons-URL `https://www.themoviedb.org/person/500-tom-cruise` is, is het persoons-ID `500`
- TMDb-populair {#tmdbpopularimport}
  - Top gebruikt <https://developers.themoviedb.org/3/movies/get-top-rated-movies>
  - Populair gebruikt <https://developers.themoviedb.org/3/movies/get-popular-movies>
  - In de bioscoop gebruikt <https://developers.themoviedb.org/3/movies/get-now-playing>
  - Aankomend gebruikt <https://developers.themoviedb.org/3/movies/get-upcoming>
- TMDb-gebruiker {#tmdbuserimport}
- Trakt-lijst {#traktlistimport}
  - Gebruikersnaam - Zorg ervoor dat je de daadwerkelijke gebruikersnaam van de gebruiker invoert en niet de naam van de gebruiker
  - Lijst - Zorg ervoor dat je de lijstnaam gebruikt zoals deze wordt weergegeven in de lijst-URL
  - Voorbeeld: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Gebruikersnaam: `some-user-name`
    - Lijst: `trakt-list-name`
- Trakt-populaire lijst {#traktpopularimport}
- Trakt-gebruiker {#traktuserimport}
  - Dit type moet worden gebruikt bij het gebruik van je eigen kijklijst

# Metadata

{#metadata}

- Emby (Legacy) {#mediabrowsermetadata}
  - Inschakelen - Metadata-bestandscreatie inschakelen voor dit metadatatype
  - Film-metadata - Metadata-bestandscreatie inschakelen voor dit metadatatype
- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Inschakelen - Metadata-bestandscreatie inschakelen voor dit metadatatype
  - Film-metadata - Maak een `<bestandsnaam>.nfo` met de film-metadata
  - (Geavanceerde optie) Film-metadata-URL - Maak `movie.nfo` met TMDb- en IMDb-film-URL's
  - Metadatalanguage - Selecteer de taal die Radarr moet gebruiken om de metadata te schrijven als deze beschikbaar is in die taal
  - Filmafbeeldingen - Maak verschillende seizoensafbeeldingen, waaronder posters en banners
  - Gebruik Movie.nfo - Schrijf het nfo-bestand als `movie.nfo` in plaats van de standaard
  - Collectienaam - Radarr schrijft de naam van de collectie naar het .nfo-bestand
- Roksbox {#roksboxmetadata}
  - Inschakelen - Metadata-bestandscreatie inschakelen voor dit metadatatype
  - Film-metadata - Maak een xml-bestand voor elke film
  - Filmafbeeldingen - Maak `Movie.jpg`
- WDTV {#wdtvmetadata}
  - Inschakelen - Metadata-bestandscreatie inschakelen voor dit metadatatype
  - Film-metadata - Maak `<bestandsnaam>.xml` voor elke aflevering
  - Filmafbeeldingen - Maak `folder.jpg`