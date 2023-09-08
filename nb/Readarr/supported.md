---
title: Readarr Støttet
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> Denne siden er under arbeid og krever ytterligere innsats.{.is-warning}

Denne siden er en avklaringsside for alle "støttede" wiki-lenker (dvs. vanligvis `Mer informasjon` i brukergrensesnittet).

# Nedlastingsklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Flood {#flood}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se innstillingssiden](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se innstillingssiden](/readarr/settings#download-clients)
  - På grunn av at uTorrent er adware og tidligere spionprogramvare, anbefales det ikke. De fleste brukere bruker qBittorrent
- Vuze {#vuze}
  - [Se innstillingssiden](/readarr/settings#download-clients)

# Indekserer

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
  - Newznab er en standardisert API som brukes av mange usenet-indeksnettsteder. Mange forhåndsinnstillinger er tilgjengelige, men alle krever en API-nøkkel for å være tilgjengelige.
  - Indekseringsprogrammer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan gi avanserte funksjoner som statistikksporing.
- omgwtfnzbs {#omgwtfnzbs}
  - En privat usenet-indeks
  - [Se innstillingssiden](/readarr/settings#indexer-settings)

## Torrenter

- FileList {#filelist}
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat sporingsnettsted
  > IP Torrents' native implementering støtter ikke søk {.is-info}
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrentsporingsnettsted for japansk media (anime) eksklusivt.
  > Nyaa ser ned på automatisering og vil ofte blokkere IP-adressen din. {.is-info}
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig sporingsnettsted
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-parser.
  > RSS-feeden må inneholde en `pubdate`. Utgivelsesstørrelsen anbefales også. {.is-info}
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indekserer
  - [Se innstillingssiden](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er et ordspill på Torrent og Newznab. Det bruker den samme strukturen og syntaksen som Newznab API-spesifikasjonen, men eksponerer torrent-spesifikke attributter og .torrent-filer. Støtter dermed en nylig RSS-feed OG bakloggsøkefunksjoner. Spesifikasjonen vedlikeholdes ikke eller støttes av Newznab-organisasjonen. (Den samme API-spesifikasjonen deles med nZEDb)
  - Dette støttes primært av [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se innstillingssiden](/readarr/settings#indexer-settings)

# Varsler

{#notification}

- Boxcar {#boxcar}
- Egendefinert skript {#customscript}
  - Dette lar deg lage et egendefinert skript som kjører når en bestemt handling skjer. Se [Egendefinerte skript](/readarr/custom-scripts) for mer informasjon.
- Discord {#discord}
  - Langt den vanligste måten å sende varsler om handlinger som skjer på Readarr
- E-post {#email}
  - Send enkelt deg selv eller noen du vil plage med e-post. Hvis du bruker Gmail, må du aktivere mindre sikre apper. Hvis du bruker Gmail og har aktivert totrinnsbekreftelse, må du bruke et appspesifikt passord.

 > Du kan bruke en "pen adresse" som `NoePenNavn <epost@example.org>` {.is-info}

- GoodReads bokhyller {#goodreadsbookshelf}
- GoodReads eide bøker {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se oppføringen om [Nyttige verktøy - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
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

- GoodReads bokhyller {#goodreadsbookshelf}
  - (Avansert alternativ) Bruker-ID - Skriv inn en bruker-ID her hvis det ikke er din bruker-ID som er lagt til.
  - Bokhyller - Velg hvilke bokhyller som skal importeres fra GoodReads
  - Autentiser med GoodReads - Klikk på knappen for å autentisere med GoodReads.

> Flere GoodReads-brukere kan legges til som separate lister. I tillegg til å bruke en autentisert bruker kan andre brukere legges til ved å aktivere avanserte alternativer og skrive inn bruker-ID-en, og deretter klikke på Autentiser med GoodReads for å hente brukerens bokhyller.
{.is-info}

- GoodReads eide bøker {#goodreadsownedbooks}
  - (Avansert alternativ) Bruker-ID - Skriv inn en bruker-ID her hvis det ikke er din bruker-ID som er lagt til.
  - Bokhyller - Velg hvilke bokhyller som skal importeres fra GoodReads
  - Autentiser med GoodReads - Klikk på knappen for å autentisere med GoodReads.

> Flere GoodReads-brukere kan legges til som separate lister. I tillegg til å bruke en autentisert bruker kan andre brukere legges til ved å aktivere avanserte alternativer og skrive inn bruker-ID-en, og deretter klikke på Autentiser med GoodReads for å hente brukerens bokhyller.
{.is-info}

- GoodReads-lister {#goodreadslistimportlist}
  - Liste-ID - Skriv inn den offentlige liste-ID-en fra GoodReads for å legge til som en liste
- GoodReads-serier {#goodreadsseriesimportlist}
  - Serie-ID - Skriv inn GoodReads-serie-ID-en for å legge til som en liste
- LazyLibrarian {#lazylibrarianimport}
  - URL - URL-en til LazyLibrarian-instansen din
  - API-nøkkel - API-nøkkelen til LazyLibrarian-instansen din
- Readarr {#readarrimport}
  - Full URL - Full URL til Readarr-instansen du vil importere fra, f.eks. `http://localhost:8787/readarr`
  - API-nøkkel - API-nøkkelen til Readarr-instansen du vil importere fra
  - Profiler - Profiler fra Readarr-instansen du vil importere fra
  - Merker - Merker fra Readarr-instansen du vil importere fra

# Metadata

{#metadata}

- Calibre {#calibre}
  - [Se innstillingssiden](/readarr/settings#write-metadata-to-book-files)
- Lydtagging {#audiotagging}
  - [Se innstillingssiden](/readarr/settings#write-metadata-to-book-files)