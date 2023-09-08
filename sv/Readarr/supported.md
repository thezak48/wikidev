---
title: Readarr Supporterad
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> Den här sidan är under arbete och kräver ytterligare ansträngning.{.is-warning}

Den här sidan är en förtydligandesida för alla "supporterade" wiki-länkar (vanligtvis "Mer information" i användargränssnittet).

# Nedladdningsklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Flood {#flood}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se inställningssidan](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se inställningssidan](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se inställningssidan](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se inställningssidan](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se inställningssidan](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [Se inställningssidan](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se inställningssidan](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se inställningssidan](/readarr/settings#download-clients)
  - På grund av att uTorrent är adware och tidigare spyware rekommenderas det inte. De flesta användare använder qBittorrent istället.
- Vuze {#vuze}
  - [Se inställningssidan](/readarr/settings#download-clients)

# Indexerare

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se inställningssidan](/readarr/settings#indexer-settings)
  - Newznab är en standardiserad API som används av många usenet-indexeringssidor. Många förinställningar finns tillgängliga, men alla kräver en API-nyckel för att vara åtkomliga.
  - Indexeringsprogram som [Prowlarr](/prowlarr) och [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan erbjuda avancerade funktioner som statistikspårning.
- omgwtfnzbs {#omgwtfnzbs}
  - En privat usenet-indexerare
  - [Se inställningssidan](/readarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - [Se inställningssidan](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Se inställningssidan](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents nativa implementation stöder inte sökning {.is-info}
  - [Se inställningssidan](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker för japansk media (exklusivt anime).
  > Nyaa ogillar automatisering och kommer ofta att blockera din IP-adress. {.is-info}
  - [Se inställningssidan](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se inställningssidan](/readarr/settings#indexer-settings)
- Torrent RSS-flöde {#torrentrssindexer}
  - Generisk parser för torrent RSS-flöden.
  > RSS-flödet måste innehålla en `pubdate`. Det rekommenderas också att släppstorleken finns med.
  {.is-info}
  - [Se inställningssidan](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indexerare
  - [Se inställningssidan](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab är ett ordlek med Torrent och Newznab. Det använder samma struktur och syntax som Newznab API-specifikationen, men exponerar torrent-specifika attribut och .torrent-filer. Stöder därför både ett nyligen RSS-flöde OCH sökfunktion för äldre innehåll. Specifikationen underhålls inte och stöds inte av Newznab-organisationen. (Samma API-specifikation delas med nZEDb)
  - Detta stöds främst av [Prowlarr](/prowlarr) och [Jackett](https://github.com/Jackett/Jackett)
  - [Se inställningssidan](/readarr/settings#indexer-settings)

# Notifieringar

{#notification}

- Boxcar {#boxcar}
- Anpassat skript {#customscript}
  - Detta gör att du kan skapa ett anpassat skript som körs när en viss åtgärd inträffar. Se [Anpassade skript](/readarr/custom-scripts) för mer information.
- Discord {#discord}
  - Långt ifrån det vanligaste sättet att skicka notiser om händelser som inträffar i din Readarr
- E-post {#email}
  - Skicka helt enkelt e-post till dig själv eller någon annan som du vill irritera. Om du använder Gmail måste du aktivera mindre säkra appar. Om du använder Gmail och har tvåfaktorsautentisering aktiverat måste du använda ett appspecifikt lösenord.

 > Du kan använda en "snygg adress" som `SomePrettyName <email@example.org>` {.is-info}

- GoodReads bokhyllor {#goodreadsbookshelf}
- GoodReads ägda böcker {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se posten om [Användbara verktyg - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology-indexerare {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Se den här posten om [Tips och tricks](/useful-tools#twitter)
- Webhook {#webhook}

# Listor

{#importlist}

- GoodReads bokhyllor {#goodreadsbookshelf}
  - (Avancerad inställning) Användar-ID - Ange ett användar-ID här om det inte är ditt eget användar-ID som du lägger till.
  - Bokhyllor - Välj vilka bokhyllor som ska importeras från GoodReads
  - Autentisera med GoodReads - Klicka på knappen för att autentisera med GoodReads.

> Flera GoodReads-användare kan läggas till som separata listor. Förutom att använda en autentiserad användare kan andra användare läggas till genom att aktivera avancerade alternativ och ange användar-ID, och sedan klicka på Autentisera med GoodReads för att hämta användarens bokhyllor.
{.is-info}

- GoodReads ägda böcker {#goodreadsownedbooks}
  - (Avancerad inställning) Användar-ID - Ange ett användar-ID här om det inte är ditt eget användar-ID som du lägger till.
  - Bokhyllor - Välj vilka bokhyllor som ska importeras från GoodReads
  - Autentisera med GoodReads - Klicka på knappen för att autentisera med GoodReads.

> Flera GoodReads-användare kan läggas till som separata listor. Förutom att använda en autentiserad användare kan andra användare läggas till genom att aktivera avancerade alternativ och ange användar-ID, och sedan klicka på Autentisera med GoodReads för att hämta användarens bokhyllor.
{.is-info}

- GoodReads listor {#goodreadslistimportlist}
  - List-ID - Ange GoodReads offentliga list-ID för att lägga till som en lista
- GoodReads serier {#goodreadsseriesimportlist}
  - Serie-ID - Ange GoodReads serie-ID för att lägga till som en lista
- LazyLibrarian {#lazylibrarianimport}
  - URL - URL till din LazyLibrarian-instans
  - API-nyckel - API-nyckel till din LazyLibrarian-instans
- Readarr {#readarrimport}
  - Fullständig URL - Fullständig URL till Readarr-instansen att importera från, t.ex. `http://localhost:8787/readarr`
  - API-nyckel - API-nyckel till Readarr-instansen att importera från
  - Profiler - Profiler från Readarr-instansen att importera från
  - Taggar - Taggar från Readarr-instansen att importera från

# Metadata

{#metadata}

- Calibre {#calibre}
  - [Se inställningssidan](/readarr/settings#write-metadata-to-book-files)
- Ljudtaggning {#audiotagging}
  - [Se inställningssidan](/readarr/settings#write-metadata-to-book-files)