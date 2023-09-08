---
title: Radarr Støttet
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# Innholdsfortegnelse

> Denne siden er under arbeid og krever ytterligere innsats.{.is-warning}

Denne siden er en avklaringsside for alle `støttede` wiki-lenker (vanligvis "mer informasjon" i brukergrensesnittet).

# Nedlastingsklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Flood {#flood}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se innstillingssiden](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se innstillingssiden](/radarr/settings#download-clients)
  - På grunn av at uTorrent er adware og tidligere spionprogramvare, anbefales det ikke. De fleste brukere bruker Qbittorrent.
- Vuze {#vuze}
  - [Se innstillingssiden](/radarr/settings#download-clients)

# Indekserere

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
  - Newznab er en standardisert API som brukes av mange usenet-indeksider. Mange forhåndsinnstillinger er tilgjengelige, men alle krever en API-nøkkel for å være tilgjengelige.
  - Indekseringsprogrammer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan gi avanserte funksjoner som statistikksporing.
- omgwtfnzbs {#omgwtfnzbs}
  - En utdatert implementering av en privat usenet-indeks. Bruk heller Newznab.
  - [Se innstillingssiden](/radarr/settings#indexer-settings)

## Torrenter

- FileList {#filelist}
  - Privat sporingsnettsted
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privat sporingsnettsted
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat sporingsnettsted
  > IP Torrents' native implementering støtter ikke søk. Bruk den via Prowlarr eller Jackett som torznab i stedet {.is-info}
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrentsporingsnettsted for japansk media (anime) eksklusivt.
  > Nyaa ser ned på automatisering og vil ofte banne IP-adressen din. {.is-info}
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - Privat sporingsnettsted
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig sporingsnettsted
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-analyser
  > RSS-feeden må inneholde en `pubdate`. Utgivelsesstørrelsen anbefales også. {.is-info}
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - En utdatert Couchpotato-pre-Torznab-format.
  - [Se innstillingssiden](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er et ordspill på Torrent og Newznab. Det bruker den samme strukturen og syntaksen som Newznab API-spesifikasjonen, men eksponerer torrent-spesifikke attributter og .torrent-filer. Støtter derfor en nylig RSS-feed OG backlog-søkefunksjoner. Spesifikasjonen vedlikeholdes ikke eller støttes av Newznab-organisasjonen. (Den samme API-spesifikasjonen deles med nZEDb)
  - Dette støttes primært av [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se innstillingssiden](/radarr/settings#indexer-settings)

> Mange torrentsporingsnettsteder trives på fellesskapet og kan ha regler på plass som krever besøk på nettstedet, karma, stemmer, kommentarer, osv.
> Vennligst gjennomgå retningslinjene og etiketten for ditt sporingsnettsted, hold fellesskapet i live.
> Vi er ikke ansvarlige hvis kontoen din blir utestengt for å bryte reglene eller for å akkumulere Hit and Runs (HnRs)/lav ratio. {.is-warning}

# Varsler

{#notification}

- Boxcar {#boxcar}
- Egendefinert skript {#customscript}
  - Dette lar deg lage et egendefinert skript som skal kjøres når en bestemt handling skjer. Se [Egendefinerte skript](/radarr/custom-scripts) for mer informasjon.
- Discord {#discord}
  - Langt den vanligste måten å sende varsler om handlinger som skjer i Radarr
- E-post {#email}
  - Send enkelt deg selv eller noen du vil plage med e-post. Hvis du bruker Gmail, må du aktivere mindre sikre apper. Hvis du bruker Gmail og har aktivert tofaktorautentisering, må du bruke et appspesifikt passord.

> Du kan bruke en "pen adresse" som `NoenPenNavn <epost@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi ble født ut av kjærligheten til media. Det er en underholdningshub som samler all digital media på en vakker og brukervennlig måte. Den er 100% gratis og åpen kildekode, veldig tilpasningsdyktig og kjører på en rekke enheter. Den støttes av et dedikert team av frivillige og et stort fellesskap. Ved å legge til Kodi som en tilkobling kan du oppdatere Kodis bibliotek når en ny film er lagt til i Radarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se oppføringen om [Nyttige verktøy - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Serveren for ditt selvhostede Plex-system. Å aktivere dette er mye som Kodi og vil tillate deg å sende en oppdatering til Plex-serveren din for å varsle om at en ny/oppgradert film er tilgjengelig.
  - Dette er sjelden nødvendig og kreves bare hvis Plex ikke kan overvåke filsystemet for endringer.
  - I de få situasjonene der Plex ikke kan overvåke filsystemet ved hjelp av ionotify - for eksempel visse typer eksterne monteringer og noen eldre nettverksmonteringer - anbefales det å bruke appen plexautoscan i stedet for Plex-tilkoblingen
- Bruk et verktøy som [plexautoscan](https://github.com/l3uddz/plex_autoscan) er et annet alternativ.

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology-indeks {#synologyindexer}
- Telegram {#telegram}
- Trakt {#trakt}
- Twitter {#twitter}
  - Se denne [Tips og triks-opføringen](/useful-tools#twitter)
- Webhook {#webhook}

# Lister

{#importlist}

- CouchPotato {#couchpotatoimport}
- Egendefinerte lister {#radarrlistimport}
- IMDb-lister {#imdblistimport}
  - For å legge til IMDb-seanselisten din, gå til listen din og klikk på rediger. Sørg for at personverninnstillingen er satt til offentlig. I adressefeltet finner du nummeret `lsxxxxxx` som du må legge inn i Radarr

    1. Gå til IMDB-listeinnstillingene dine
    1. Sørg for at personvernet er satt til `Public` (dvs. `Disabled)`
    1. Bruk `ls`-nummeret i URL-en

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex-seanseliste {#plex}
  - Krever: v4.1.0.6176+
  - Legg enkelt til en Plex-seanseliste for den autentiserte Plex-brukeren i Radarr. Merk at listen din må inneholde filmer.
  - For å ha flere brukeres seanselister må du legge til hver brukers lister og autentisere med deres Plex-bruker.
- Radarr {#radarrimport}
  - TRaSH har [en guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) for synkronisering av to instanser
- RSS-liste {#rssimport}
- StevenLu-tilpasset {#stevenluimport}
	- Lar deg opprette tilpassede filmlister i JSON-format.
  - Feeden din krever for hver film enten en `title` eller en `imdb_id`, begge kan oppgis.
  		> Merk at `imdb_id` er tryggere enn `title` siden det ikke krever et bredt søk
    Her er et eksempel på gyldig JSON:
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
      - Flere nøkler kan legges til i elementer (vil bli ignorert)
      - For en tom liste, returner bare en tom JSON-matrise `[]`
- StevenLu-liste {#stevenlu2import}
- TMDb-samling {#tmdbcollectionimport}
  - Samlingslister støttes ikke lenger i Radarr v4.2 og har blitt migrert til samlinger i Radarr. Se [Samlinger](/radarr/library#collections) -delen for mer informasjon.
- TMDb-selskap {#tmdbcompanyimport}
- TMDb-nøkkelord {#tmdbkeywordimport}
- TMDb-liste {#tmdblistimport}
- TMDb-person {#tmdbpersonimport}
  - Hvis TMDb-person-URL-en er `https://www.themoviedb.org/person/500-tom-cruise`, er person-ID-en `500`
- TMDb-populær {#tmdbpopularimport}
  - Top bruker <https://developers.themoviedb.org/3/movies/get-top-rated-movies>
  - Populær bruker <https://developers.themoviedb.org/3/movies/get-popular-movies>
  - Theaters bruker <https://developers.themoviedb.org/3/movies/get-now-playing>
  - Kommende bruker <https://developers.themoviedb.org/3/movies/get-upcoming>
- TMDb-bruker {#tmdbuserimport}
- Trakt-liste {#traktlistimport}
  - Brukernavn - Sørg for at du skriver inn den faktiske brukernavnet til brukeren og ikke brukerens navn
  - Liste - Sørg for at du bruker listenavnet som vises i listenettadressen
  - Eksempel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Brukernavn: `some-user-name`
    - Liste: `trakt-list-name`
- Trakt-populær liste {#traktpopularimport}
- Trakt-bruker {#traktuserimport}
  - Denne typen skal brukes når du bruker din egen seanseliste

# Metadata

{#metadata}

- Emby (Legacy) {#mediabrowsermetadata}
  - Aktiver - Aktiver opprettelse av metadatafil for denne metadatatypen
  - Filmmetadata - Aktiver opprettelse av metadatafil for denne metadatatypen
- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktiver - Aktiver opprettelse av metadatafil for denne metadatatypen
  - Filmmetadata - Opprett en `<filnavn>.nfo` med filmmetadataen
  - (Avansert alternativ) Filmmetadata-URL - Opprett `movie.nfo` med TMDb- og IMDb-film-URL-er
  - Metadataspråk - Velg språket Radarr skal bruke for å skrive metadataen hvis den er tilgjengelig på det språket
  - Film bilder - Opprett forskjellige bilder for filmen, inkludert plakater og bannere
  - Bruk Movie.nfo - Skriv nfo-filen som `movie.nfo` i stedet for standard
  - Samlingens navn - Radarr vil skrive samlingens navn til .nfo-filen
- Roksbox {#roksboxmetadata}
  - Aktiver - Aktiver opprettelse av metadatafil for denne metadatatypen
  - Filmmetadata - Opprett XML-fil for hver film
  - Film bilder - Opprett `Movie.jpg`
- WDTV {#wdtvmetadata}
  - Aktiver - Aktiver opprettelse av metadatafil for denne metadatatypen
  - Filmmetadata - Opprett `<filnavn>.xml` for hver episode
  - Film bilder - Opprett `folder.jpg`