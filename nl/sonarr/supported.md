---
title: Ondersteunde Sonarr
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> Deze pagina is nog in ontwikkeling en vereist extra inspanning. {.is-warning}

Deze pagina is de verduidelijkingspagina voor alle "ondersteunde" wiki-links (meestal `Meer informatie` in de gebruikersinterface).

# Downloadclients

{#downloadclient}

- Aria2 {#aria2}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Flood {#flood}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)
  - Vanwege het feit dat uTorrent adware en voormalige spyware is, wordt het niet aanbevolen. De meeste gebruikers gebruiken Qbittorrent
- Vuze {#vuze}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#download-clients)

# Indexers

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - Usenet-indexer exclusief voor Japanse media (Anime).
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
  - Newznab is een gestandaardiseerde API die wordt gebruikt door veel Usenet-indexeringssites. Er zijn veel voorinstellingen beschikbaar, maar deze vereisen allemaal een API-sleutel om toegankelijk te zijn.
  - Indexer-toepassingen zoals [Prowlarr](/prowlarr) en [NZBHydra2](https://github.com/theotherp/nzbhydra2) kunnen geavanceerde mogelijkheden bieden, zoals statistiektracking.
- omgwtfnzbs {#omgwtfnzbs}
  - Een verouderde legacy-implementatie van een privé Usenet-indexer. Gebruik in plaats daarvan Newznab.
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)

## Torrents

- BroadcasTheNet (BTN) {#broadcasthenet}
  - Privé-tracker
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - Privé-tracker
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privé-tracker
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privé-tracker
  > De native implementatie van IP Torrents ondersteunt geen zoekopdrachten. Gebruik het via Prowlarr of Jackett als torznab in plaats daarvan {.is-info}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker exclusief voor Japanse media (Anime).
  - Nyaa ondersteunt alleen zoeken naar Anime-serietypes
  - Er zijn bekende problemen met de native Sonarr-versie
    - [Nyaa seeders/leechers worden niet meer correct geparseerd. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - Dit kan worden opgelost wanneer / als [Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637) wordt samengevoegd
  - > Nyaa keurt automatisering af en zal uw IP-adres vaak blokkeren. {.is-warning}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Openbare tracker
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generieke torrent RSS-feedparser.
  > De RSS-feed moet een `pubdate` bevatten. De releasesize wordt ook aanbevolen.
  {.is-info}
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privé-indexer
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab is een woordspeling op Torrent en Newznab. Het gebruikt dezelfde structuur en syntaxis als de Newznab API-specificatie, maar exposeert torrent-specifieke attributen en .torrent-bestanden. Het ondersteunt dus een recente RSS-feed EN mogelijkheden voor het doorzoeken van backlog. De specificatie wordt niet onderhouden of ondersteund door de Newznab-organisatie. (Dezelfde API-specificatie wordt gedeeld met nZEDb)
  - Dit wordt voornamelijk ondersteund door [Prowlarr](/prowlarr) en [Jackett](https://github.com/Jackett/Jackett)
  - [Raadpleeg de instellingenpagina](/sonarr/settings#indexer-settings)

> Veel torrent-trackers gedijen op de gemeenschap en hebben regels die sitebezoeken, karma, stemmen, opmerkingen, enz. vereisen.
> Bekijk alstublieft de regels en etiquette van uw tracker en houd uw gemeenschap levend.
> Wij zijn niet verantwoordelijk als uw account wordt verbannen vanwege het niet naleven van de regels of het oplopen van Hit and Runs (HnR's)/lage ratio's.
{.is-warning}

# Meldingen

{#notification}

- Boxcar {#boxcar}
- Aangepast script {#customscript}
  - Hiermee kunt u een aangepast script maken dat wordt uitgevoerd wanneer een bepaalde actie plaatsvindt. Zie [Aangepaste scripts](/sonarr/custom-scripts) voor meer informatie.
- Discord {#discord}
  - Veruit een van de meest voorkomende manieren om meldingen te ontvangen van acties die plaatsvinden op uw Sonarr
  - Ondersteunde veldtypen:
  `Overzicht, Beoordeling, Genres, Kwaliteit, Groep, Grootte, Links, Release, Poster, Fanart, Aangepaste formaten, Aangepaste format score, Indexer`
- E-mail {#email}
  - Stuur eenvoudig een e-mail naar uzelf of naar iemand die u wilt lastigvallen. Als u Gmail gebruikt, moet u minder veilige apps inschakelen. Als u Gmail gebruikt en tweefactorauthenticatie hebt ingeschakeld, moet u een specifiek app-wachtwoord gebruiken.

> U kunt een "mooi adres" gebruiken zoals `SomePrettyName <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi is ontstaan uit de liefde voor media. Het is een entertainmenthub die al uw digitale media samenbrengt in een mooie en gebruiksvriendelijke verpakking. Het is 100% gratis en open source, zeer aanpasbaar en werkt op een breed scala aan apparaten. Het wordt ondersteund door een toegewijd team van vrijwilligers en een enorme community. Door Kodi toe te voegen als een verbinding, kunt u de bibliotheek van Kodi bijwerken wanneer er een nieuwe aflevering aan Sonarr is toegevoegd.
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - Verouderd
- Plex Media Center {#plexclient}
  - Verouderd
- Plex Media Server {#plexserver}
  - De server voor uw zelfgehoste Plex-systeem. Door dit in te schakelen, kunt u een update naar uw Plex-server pushen om deze op de hoogte te stellen dat er een nieuwe/opgewaardeerde aflevering beschikbaar is.
  - Dit is zelden nodig en is alleen vereist als Plex niet in staat is om wijzigingen in het bestandssysteem te volgen.
  - In de handvol situaties waarin Plex niet in staat is om het bestandssysteem te volgen met behulp van ionotify - zoals bepaalde soorten externe mounts en een handvol oudere netwerkmounts - wordt aangeraden om de app plexautoscan te gebruiken in plaats van de Plex-verbinding

> Houd er rekening mee dat dit mogelijk een volledige bibliotheekscan kan activeren voor de bibliotheek/hoofdmap waarin de serie zich bevindt. Het wordt sterk aanbevolen om de native Plex-functionaliteit te gebruiken die alleen het bestandssysteem volgt of om een tool zoals [plexautoscan](https://github.com/l3uddz/plex_autoscan) te gebruiken
{.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Zie deze [Tips en trucs vermelding](/useful-tools#twitter)
- Webhook {#webhook}

# Lijsten

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH heeft [een handleiding](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/) voor het synchroniseren van twee instanties
- Plex Watchlist {#pleximport}
  - Voeg eenvoudig een Plex-watchlist toe voor de geauthenticeerde Plex-gebruiker aan Sonarr. Let op dat uw lijst shows moet bevatten.
  - Om meerdere watchlists van gebruikers te hebben, moet u de lijsten van elke gebruiker toevoegen en authenticeren met hun Plex-gebruiker.
- Trakt-lijst {#traktlistimport}
  - Gebruikersnaam - Zorg ervoor dat u de daadwerkelijke gebruikersnaam van de gebruiker invoert en niet de naam van de gebruiker
  - Lijst - Zorg ervoor dat u de lijstnaam gebruikt zoals deze wordt weergegeven in de lijst-URL
  - Voorbeeld: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Gebruikersnaam: `some-user-name`
    - Lijst: `trakt-list-name`
- Trakt Populaire Lijst {#traktpopularimport}
- Trakt-gebruiker {#traktuserimport}

> Trakt-lijsten moeten shows bevatten, geen individuele afleveringen. Sonarr zal alleen overeenkomende shows vinden en toevoegen.
{.is-info}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Inschakelen - Metadata-bestanden maken voor dit metadatatype inschakelen
  - Series-metadata - Maak een `tvshow.nfo` met volledige series-metadata
  - (Geavanceerde optie) Series-metadata-URL - Maak tvshow.nfo met de URL van de TheTVDb-serie
  - Afleveringsmetadata - Maak `<bestandsnaam>.nfo` voor elke aflevering
  - Series-afbeeldingen - Maak verschillende series-afbeeldingen, waaronder posters en banners met de namen `poster.jpg` en `banner.jpg`
  - Seizoensafbeeldingen - Maak verschillende seizoensafbeeldingen, waaronder posters en banners met de namen `season##-poster.jpg` en `season##-banner.jpg`
  - Afbeeldingen van afleveringen - Maak verschillende afbeeldingen van afleveringen, zoals miniaturen met de naam `<bestandsnaam>-thumb.jpg`
- Roksbox {#roksboxmetadata}
  - Inschakelen - Metadata-bestanden maken voor dit metadatatype inschakelen
  - Afleveringsmetadata - Maak `Season##\<bestandsnaam>.xml` voor elke aflevering
  - Series-afbeeldingen - Maak `Series Title.jpg`
  - Seizoensafbeeldingen - Maak `Season ##.jpg`
  - Afbeeldingen van afleveringen - Maak `Season##\<bestandsnaam>.jpg`
- WDTV {#wdtvmetadata}
  - Inschakelen - Metadata-bestanden maken voor dit metadatatype inschakelen
  - Afleveringsmetadata - Maak `Season##\<bestandsnaam>.xml` voor elke aflevering
  - Series-afbeeldingen - Maak `folder.jpg`
  - Seizoensafbeeldingen - Maak `Season ##\folder.jpg`
  - Afbeeldingen van afleveringen - Maak `Season##\<bestandsnaam>.metathumb`