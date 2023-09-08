---
title: Ondersteunde Readarr-functies
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> Deze pagina is nog in ontwikkeling en vereist extra inspanning.{.is-warning}

Deze pagina is de verduidelijkingspagina voor alle "ondersteunde" wiki-links (meestal `Meer info` in de gebruikersinterface).

# Downloadclients

{#downloadclient}

- Aria2 {#aria2}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Flood {#flood}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)
  - Vanwege het feit dat uTorrent adware en voorheen spyware is, wordt het niet aanbevolen. De meeste gebruikers gebruiken qBittorrent.
- Vuze {#vuze}
  - [Raadpleeg de instellingenpagina](/readarr/settings#download-clients)

# Indexers

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
  - Newznab is een gestandaardiseerde API die wordt gebruikt door veel Usenet-indexeringssites. Er zijn veel voorinstellingen beschikbaar, maar ze vereisen allemaal een API-sleutel om toegankelijk te zijn.
  - Indexer-toepassingen zoals [Prowlarr](/prowlarr) en [NZBHydra2](https://github.com/theotherp/nzbhydra2) bieden geavanceerde mogelijkheden zoals statistiektracking.
- omgwtfnzbs {#omgwtfnzbs}
  - Een privé-Usenet-indexer
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privé-tracker
  > De native implementatie van IP Torrents ondersteunt geen zoekopdrachten {.is-info}
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker exclusief voor Japanse media (anime).
  > Nyaa keurt automatisering af en zal vaak je IP-adres blokkeren. {.is-info}
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Openbare tracker
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generieke torrent RSS-feedparser.
  > De RSS-feed moet een `pubdate` bevatten. De grootte van de release wordt ook aanbevolen. {.is-info}
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privé-indexer
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab is een woordspeling op Torrent en Newznab. Het gebruikt dezelfde structuur en syntaxis als de Newznab API-specificatie, maar biedt torrent-specifieke attributen en .torrent-bestanden. Hierdoor worden zowel recente RSS-feeds als mogelijkheden voor het doorzoeken van oudere releases ondersteund. De specificatie wordt niet onderhouden of ondersteund door de Newznab-organisatie. (Dezelfde API-specificatie wordt gedeeld met nZEDb)
  - Dit wordt voornamelijk ondersteund door [Prowlarr](/prowlarr) en [Jackett](https://github.com/Jackett/Jackett)
  - [Raadpleeg de instellingenpagina](/readarr/settings#indexer-settings)

# Meldingen

{#notification}

- Boxcar {#boxcar}
- Aangepast script {#customscript}
  - Hiermee kunt u een aangepast script maken dat wordt uitgevoerd wanneer een bepaalde actie plaatsvindt. Zie [Aangepaste scripts](/readarr/custom-scripts) voor meer informatie.
- Discord {#discord}
  - Veruit een van de meest voorkomende manieren om meldingen te ontvangen van acties die plaatsvinden op uw Readarr
- E-mail {#email}
  - Stuur eenvoudig een e-mail naar uzelf of naar iemand die u wilt lastigvallen. Als u Gmail gebruikt, moet u minder veilige apps inschakelen. Als u Gmail gebruikt en tweefactorauthenticatie hebt ingeschakeld, moet u een specifiek app-wachtwoord gebruiken.

 > U kunt een "mooi adres" gebruiken zoals `MooieNaam <email@example.org>` {.is-info}

- GoodReads-boekenplanken {#goodreadsbookshelf}
- GoodReads-eigendomsboeken {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Zie de vermelding over [Handige tools - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
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

- GoodReads-boekenplanken {#goodreadsbookshelf}
  - (Geavanceerde optie) Gebruikers-ID - Voer hier een gebruikers-ID in als het niet uw eigen gebruikers-ID is.
  - Boekenplanken - Selecteer welke boekenplanken moeten worden geïmporteerd vanuit GoodReads.
  - Authenticeren met GoodReads - Klik op de knop om te authenticeren met GoodReads.

> Meerdere GoodReads-gebruikers kunnen als aparte lijsten worden toegevoegd. Naast het gebruik van een geauthenticeerde gebruiker kunnen andere gebruikers worden toegevoegd door geavanceerde opties in te schakelen en de gebruikers-ID in te voeren, en vervolgens op Authenticeren met GoodReads te klikken om de boekenplanken van de gebruiker op te halen. {.is-info}

- GoodReads-eigendomsboeken {#goodreadsownedbooks}
  - (Geavanceerde optie) Gebruikers-ID - Voer hier een gebruikers-ID in als het niet uw eigen gebruikers-ID is.
  - Boekenplanken - Selecteer welke boekenplanken moeten worden geïmporteerd vanuit GoodReads.
  - Authenticeren met GoodReads - Klik op de knop om te authenticeren met GoodReads.

> Meerdere GoodReads-gebruikers kunnen als aparte lijsten worden toegevoegd. Naast het gebruik van een geauthenticeerde gebruiker kunnen andere gebruikers worden toegevoegd door geavanceerde opties in te schakelen en de gebruikers-ID in te voeren, en vervolgens op Authenticeren met GoodReads te klikken om de boekenplanken van de gebruiker op te halen. {.is-info}

- GoodReads-lijsten {#goodreadslistimportlist}
  - Lijst-ID - Voer de openbare lijst-ID van GoodReads in om toe te voegen als lijst.
- GoodReads-series {#goodreadsseriesimportlist}
  - Serie-ID - Voer de serie-ID van GoodReads in om toe te voegen als lijst.
- LazyLibrarian {#lazylibrarianimport}
  - URL - URL van uw LazyLibrarian-instantie
  - API-sleutel - API-sleutel van uw LazyLibrarian-instantie
- Readarr {#readarrimport}
  - Volledige URL - Volledige URL van de Readarr-instantie om van te importeren, bijv. `http://localhost:8787/readarr`
  - API-sleutel - API-sleutel van de Readarr-instantie om van te importeren
  - Profielen - Profielen van de Readarr-instantie om van te importeren
  - Tags - Tags van de Readarr-instantie om van te importeren

# Metadata

{#metadata}

- Calibre {#calibre}
  - [Raadpleeg de instellingenpagina](/readarr/settings#write-metadata-to-book-files)
- Audiogegevens taggen {#audiotagging}
  - [Raadpleeg de instellingenpagina](/readarr/settings#write-metadata-to-book-files)