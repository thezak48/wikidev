---
title: Sonarr Støttet
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> Denne siden er under arbeid og krever ytterligere innsats. {.is-warning}

Denne siden er en avklaringsside for alle "støttede" wiki-lenker (dvs. vanligvis `Mer informasjon` i brukergrensesnittet).

# Nedlastingsklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Flood {#flood}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se innstillingssiden](/sonarr/settings#download-clients)
  - På grunn av at uTorrent er adware og tidligere spionprogramvare, anbefales det ikke. De fleste brukere bruker Qbittorrent
- Vuze {#vuze}
  - [Se innstillingssiden](/sonarr/settings#download-clients)

# Indekseringsverktøy

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - Usenet-indeks for japansk media (anime) eksklusivt.
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
  - Newznab er en standardisert API som brukes av mange usenet-indekseringssider. Mange forhåndsinnstillinger er tilgjengelige, men alle krever en API-nøkkel for å være tilgjengelige.
  - Indekseringsprogrammer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan gi avanserte funksjoner som statistikksporing.
- omgwtfnzbs {#omgwtfnzbs}
  - En utdatert implementering av en privat usenet-indeks. Bruk heller Newznab.
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)

## Torrenter

- BroadcasTheNet (BTN) {#broadcasthenet}
  - Privat tracker
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - Privat tracker
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privat tracker
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents' native implementering støtter ikke søk. Bruk den via Prowlarr eller Jackett som torznab i stedet {.is-info}
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker for japansk media (anime) eksklusivt.
  - Nyaa støtter bare søk etter anime-serier
  - Det er kjente problemer med den native Sonarr-versjonen
    - [Nyaa seeders/leechers parses ikke riktig lenger. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - Dette kan løses når / hvis [Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637) blir slått sammen
  - > Nyaa misliker automatisering og vil ofte banne IP-adressen din. {.is-warning}
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-analyser
  > RSS-feeden må inneholde en `pubdate`. Det anbefales også å inkludere filstørrelsen.
  {.is-info}
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indekser
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er en ordlek på Torrent og Newznab. Den bruker den samme strukturen og syntaksen som Newznab API-spesifikasjonen, men eksponerer torrent-spesifikke attributter og .torrent-filer. Støtter derfor en nylig RSS-feed OG bakloggsøk. Spesifikasjonen vedlikeholdes ikke eller støttes av Newznab-organisasjonen. (Den samme API-spesifikasjonen deles med nZEDb)
  - Dette støttes primært av [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se innstillingssiden](/sonarr/settings#indexer-settings)

> Mange torrent-trackere er avhengige av fellesskapet og kan ha regler på plass som krever besøk på nettstedet, karma, stemmer, kommentarer, osv.
> Vennligst gjennomgå reglene og etiketten til trackerne, hold fellesskapet i live.
> Vi er ikke ansvarlige hvis kontoen din blir utestengt for å bryte reglene eller akkumulere Hit and Runs (HnRs)/lav ratio. {.is-warning}

# Varsler

{#notification}

- Boxcar {#boxcar}
- Egendefinert skript {#customscript}
  - Dette lar deg lage et egendefinert skript som skal kjøres når en bestemt handling skjer. Se [Egendefinerte skript](/sonarr/custom-scripts) for mer informasjon.
- Discord {#discord}
  - Langt den vanligste måten å sende varsler om handlinger som skjer i Sonarr på
  - Støttede felttyper:
  `Oversikt, Vurdering, Sjangre, Kvalitet, Gruppe, Størrelse, Lenker, Utgivelse, Plakat, Fanart, Egendefinerte formater, Egendefinert formatpoeng, Indekserer`
- E-post {#email}
  - Send enkelt e-post til deg selv eller noen du vil plage. Hvis du bruker Gmail, må du aktivere mindre sikre apper. Hvis du bruker Gmail og har tofaktorautentisering aktivert, må du bruke et appspesifikt passord.

> Du kan bruke en "pen adresse" som `NoenPenNavn <epost@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi ble til ut fra kjærligheten til media. Det er en underholdningshub som samler all digital media på en vakker og brukervennlig måte. Den er 100% gratis og åpen kildekode, veldig tilpasningsdyktig og kan kjøre på en rekke enheter. Den støttes av et dedikert team av frivillige og et stort fellesskap. Ved å legge til Kodi som en tilkobling kan du oppdatere Kodi-biblioteket når en ny episode er lagt til i Sonarr.
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - Utdatert
- Plex Media Center {#plexclient}
  - Utdatert
- Plex Media Server {#plexserver}
  - Serveren for ditt selvhostede Plex-system. Å aktivere dette er som med Kodi, og lar deg sende en oppdatering til Plex-serveren din som varsler om at en ny/oppgradert episode er tilgjengelig.
  - Dette er sjelden nødvendig og kreves bare hvis Plex ikke kan overvåke filsystemet for endringer.
  - I de få situasjonene der Plex ikke kan overvåke filsystemet ved hjelp av ionotify - for eksempel visse typer eksterne monteringer og noen eldre nettverksmonteringer - anbefales det å bruke appen plexautoscan i stedet for Plex-tilkoblingen

> Merk at dette kan utløse en full biblioteksskanning for bibliotek-/rotmappen serien er i. Det anbefales sterkt å bruke den innebygde Plex-funksjonaliteten som bare overvåker filsystemet, eller å bruke et verktøy som [plexautoscan](https://github.com/l3uddz/plex_autoscan)
{.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology-indeks {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Se denne [Tips og triks-innføringen](/useful-tools#twitter)
- Webhook {#webhook}

# Lister

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH har [en guide](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/) for synkronisering av to instanser
- Plex Watchlist {#pleximport}
  - Legg til en Plex watchlist for den autentiserte Plex-brukeren i Radarr. Merk at listen må inneholde serier.
  - For å ha flere brukeres watchlister må du legge til hver brukers lister og autentisere med deres Plex-bruker.
- Trakt-liste {#traktlistimport}
  - Brukernavn - Sørg for at du skriver inn det faktiske brukernavnet til brukeren og ikke brukerens navn
  - Liste - Sørg for at du bruker listenavnet som vises i listenettadressen
  - Eksempel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Brukernavn: `some-user-name`
    - Liste: `trakt-list-name`
- Trakt populær liste {#traktpopularimport}
- Trakt-bruker {#traktuserimport}

> Trakt-lister bør inneholde serier, ikke enkeltepisoder. Sonarr vil bare matche og legge til serier.
{.is-info}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktiver - Aktiver opprettelse av metadatafiler for denne metadatatypen
  - Seriemetadata - Opprett en `tvshow.nfo` med full seriemetadata
  - (Avansert alternativ) Seriemetadata-URL - Opprett tvshow.nfo med TheTVDb-serie-URL
  - Episodemetadata - Opprett `<filnavn>.nfo` for hver episode
  - Seriebilde - Opprett forskjellige serie