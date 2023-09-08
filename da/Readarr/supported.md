---
title: Readarr Understøttet
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> Denne side er under udarbejdelse og kræver yderligere indsats.{.is-warning}

Denne side er en afklaringsside for alle "understøttede" wiki-links (dvs. typisk `Mere info` i brugergrænsefladen).

# Downloadklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Flood {#flood}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se indstillingerne](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se indstillingerne](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se indstillingerne](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se indstillingerne](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se indstillingerne](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [Se indstillingerne](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se indstillingerne](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se indstillingerne](/readarr/settings#download-clients)
  - På grund af at uTorrent er adware og tidligere spyware, anbefales det ikke. De fleste brugere bruger qBittorrent
- Vuze {#vuze}
  - [Se indstillingerne](/readarr/settings#download-clients)

# Indexere

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se indstillingerne](/readarr/settings#indexer-settings)
  - Newznab er en standardiseret API, der bruges af mange usenet-indekseringssider. Der er mange forudindstillinger, men alle kræver en API-nøgle for at være tilgængelige.
  - Indexeringsapplikationer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan give avancerede funktioner som statistiksporing.
- omgwtfnzbs {#omgwtfnzbs}
  - En privat usenet-indeks
  - [Se indstillingerne](/readarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - [Se indstillingerne](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Se indstillingerne](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents' native implementering understøtter ikke søgning {.is-info}
  - [Se indstillingerne](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker for japansk medie (anime) eksklusivt.
  > Nyaa er imod automatisering og vil ofte blokere din IP-adresse. {.is-info}
  - [Se indstillingerne](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se indstillingerne](/readarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-parser.
  > RSS-feedet skal indeholde en `pubdate`. Det anbefales også at inkludere udgivelsesstørrelsen.
  {.is-info}
  - [Se indstillingerne](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indexer
  - [Se indstillingerne](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er en ordleg på Torrent og Newznab. Den bruger den samme struktur og syntaks som Newznab API-specifikationen, men eksponerer torrent-specifikke attributter og .torrent-filer. Derfor understøtter den både en nyere RSS-feed og bagudrettet søgning. Specifikationen vedligeholdes ikke og understøttes ikke af Newznab-organisationen. (Den samme API-specifikation deles med nZEDb)
  - Dette understøttes primært af [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se indstillingerne](/readarr/settings#indexer-settings)

# Notifikationer

{#notification}

- Boxcar {#boxcar}
- Brugerdefineret script {#customscript}
  - Dette giver dig mulighed for at lave et brugerdefineret script, der skal køres, når en bestemt handling finder sted. Se [Brugerdefinerede scripts](/readarr/custom-scripts) for flere detaljer.
- Discord {#discord}
  - Langt den mest almindelige måde at sende notifikationer om handlinger, der sker på din Readarr
- E-mail {#email}
  - Send dig selv eller en person, du gerne vil genere, en e-mail. Hvis du bruger Gmail, skal du aktivere mindre sikre apps. Hvis du bruger Gmail og har aktiveret totrinsbekræftelse, skal du bruge et app-specifikt kodeord.

 > Du kan bruge en "pæn adresse" som f.eks. `NogetPæntNavn <email@example.org>` {.is-info}

- GoodReads boghylder {#goodreadsbookshelf}
- GoodReads ejede bøger {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se indgangen om [Nyttige værktøjer - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
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

- GoodReads boghylder {#goodreadsbookshelf}
  - (Avanceret indstilling) Bruger-id - Indtast et bruger-id her, hvis det ikke er dit eget bruger-id, der er tilføjet.
  - Boghylder - Vælg hvilke boghylder der skal importeres fra GoodReads
  - Godkend med GoodReads - Klik på knappen for at godkende med GoodReads.

> Flere GoodReads-brugere kan tilføjes som separate lister. Ud over at bruge en godkendt bruger kan andre brugere tilføjes ved at aktivere avancerede indstillinger og indtaste bruger-id'et, og derefter klikke på Godkend med GoodReads for at hente brugerens boghylder.
{.is-info}

- GoodReads ejede bøger {#goodreadsownedbooks}
  - (Avanceret indstilling) Bruger-id - Indtast et bruger-id her, hvis det ikke er dit eget bruger-id, der er tilføjet.
  - Boghylder - Vælg hvilke boghylder der skal importeres fra GoodReads
  - Godkend med GoodReads - Klik på knappen for at godkende med GoodReads.

> Flere GoodReads-brugere kan tilføjes som separate lister. Ud over at bruge en godkendt bruger kan andre brugere tilføjes ved at aktivere avancerede indstillinger og indtaste bruger-id'et, og derefter klikke på Godkend med GoodReads for at hente brugerens boghylder.
{.is-info}

- GoodReads lister {#goodreadslistimportlist}
  - Liste-id - Indtast den offentlige liste-id fra GoodReads, der skal tilføjes som en liste
- GoodReads serier {#goodreadsseriesimportlist}
  - Serie-id - Indtast den offentlige serie-id fra GoodReads, der skal tilføjes som en liste
- LazyLibrarian {#lazylibrarianimport}
  - URL - URL'en til din LazyLibrarian-instans
  - API-nøgle - API-nøglen til din LazyLibrarian-instans
- Readarr {#readarrimport}
  - Fuld URL - Fuld URL til Readarr-instansen, der skal importeres fra, f.eks. `http://localhost:8787/readarr`
  - API-nøgle - API-nøglen til Readarr-instansen, der skal importeres fra
  - Profiler - Profiler fra Readarr-instansen, der skal importeres fra
  - Tags - Tags fra Readarr-instansen, der skal importeres fra

# Metadata

{#metadata}

- Calibre {#calibre}
  - [Se indstillingerne](/readarr/settings#write-metadata-to-book-files)
- Lydtagging {#audiotagging}
  - [Se indstillingerne](/readarr/settings#write-metadata-to-book-files)