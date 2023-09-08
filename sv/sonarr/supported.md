---
title: Sonarr Supportade
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> Denna sida är under arbete och kräver ytterligare ansträngning. {.is-warning}

Denna sida är en förtydligandesida för alla "supportade" wiki-länkar (vanligtvis `Mer information` i gränssnittet).

# Nedladdningsklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Flood {#flood}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se inställningssidan](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se inställningssidan](/sonarr/settings#download-clients)
  - På grund av att uTorrent är adware och tidigare spionprogramvara rekommenderas det inte. De flesta användare använder Qbittorrent istället.
- Vuze {#vuze}
  - [Se inställningssidan](/sonarr/settings#download-clients)

# Indexerare

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - Usenet Indexerare för japansk media (Anime) exklusivt.
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
  - Newznab är en standardiserad API som används av många usenet indexeringswebbplatser. Många förinställningar finns tillgängliga, men alla kräver en API-nyckel för att vara åtkomliga.
  - Indexeringsprogram som [Prowlarr](/prowlarr) och [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan erbjuda avancerade funktioner som statistikspårning.
- omgwtfnzbs {#omgwtfnzbs}
  - En föråldrad äldre implementation av en privat usenet indexerare. Använd istället Newznab.
  - [Se inställningssidan](/sonarr/settings#indexer-settings)

## Torrents

- BroadcasTheNet (BTN) {#broadcasthenet}
  - Privat Tracker
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - Privat Tracker
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privat Tracker
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat Tracker
  > IP Torrents' native implementation does not support Search. Use it via Prowlarr or Jackett as torznab instead {.is-info}
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent Tracker för japansk media (Anime) exklusivt.
  - Nyaa stöder endast sökning efter Anime-serier
  - Kända problem finns med den inbyggda versionen av Sonarr
    - [Nyaa seeders/leechers not parsed properly anymore. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - Detta kan åtgärdas när / om [Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637) slås samman
  - > Nyaa ogillar automatisering och kommer ofta att blockera din IP-adress. {.is-warning}
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig Tracker
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- Torrent RSS-flöde {#torrentrssindexer}
  - Generisk torrent RSS-flödesparser.
  > RSS-flödet måste innehålla en `pubdate`. Releasestorleken rekommenderas också.
  {.is-info}
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat Indexerare
  - [Se inställningssidan](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab är ett ordlek med Torrent och Newznab. Det använder samma struktur och syntax som Newznab API-specifikationen, men exponerar torrent-specifika attribut och .torrent-filer. Stöder därför en nyligen RSS-flöde OCH bakloggssökningsfunktioner. Specifikationen underhålls inte eller stöds av Newznab-organisationen. (Samma API-specifikation delas med nZEDb)
  - Detta stöds främst av [Prowlarr](/prowlarr) och [Jackett](https://github.com/Jackett/Jackett)
  - [Se inställningssidan](/sonarr/settings#indexer-settings)

> Många torrentspårare frodas på gemenskapen och kan ha regler på plats som kräver webbplatsbesök, karma, röster, kommentarer, etc.
> Var vänlig och granska dina spårarregler och etikett, håll din gemenskap vid liv.
> Vi ansvarar inte om ditt konto blir blockerat för att du inte följer reglerna eller för att du får för många misslyckade nedladdningar (HnRs)/låg kvot.
{.is-warning}

# Notifikationer

{#notification}

- Boxcar {#boxcar}
- Anpassat skript {#customscript}
  - Detta gör att du kan skapa ett anpassat skript för när en särskild åtgärd inträffar kommer detta skript att köras. Se [Anpassade skript](/sonarr/custom-scripts) för mer information.
- Discord {#discord}
  - Långt ifrån det vanligaste sättet att få notifikationer om händelser som sker i din Sonarr
  - Stödda fälttyper:
  `Översikt, Betyg, Genrer, Kvalitet, Grupp, Storlek, Länkar, Släpp, Affisch, Fanart, Anpassade format, Anpassat formatbetyg, Indexerare`
- E-post {#email}
  - Skicka helt enkelt e-post till dig själv eller någon du vill irritera. Om du använder Gmail måste du aktivera mindre säkra appar. Om du använder Gmail och har tvåfaktorsautentisering aktiverat måste du använda ett appspecifikt lösenord.

> Du kan använda en "snygg adress" som `Något fint namn <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi uppstod ur kärleken till media. Det är en underhållningshubb som samlar all din digitala media i en vacker och användarvänlig förpackning. Den är 100% gratis och öppen källkod, mycket anpassningsbar och fungerar på en mängd olika enheter. Den stöds av ett engagerat team av volontärer och en enorm gemenskap. Genom att lägga till Kodi som en anslutning kan du uppdatera Kodis bibliotek när en ny episod har lagts till i Sonarr.
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - Föråldrad
- Plex Media Center {#plexclient}
  - Föråldrad
- Plex Media Server {#plexserver}
  - Servern för ditt självhostade Plex-system. Genom att aktivera detta kan du, precis som med Kodi, skicka en uppdatering till din Plex-server och meddela att en ny/uppdaterad episod är tillgänglig.
  - Detta behövs sällan och krävs endast om Plex inte kan övervaka filsystemet för ändringar.
  - I de få situationer där Plex inte kan övervaka filsystemet med hjälp av ionotify - som vissa typer av fjärrmonteringar och ett fåtal äldre nätverksmonteringar - rekommenderas det att använda appen plexautoscan istället för Plex-anslutningen

> Observera att detta kan utlösa en fullständig bibliotekssökning för biblioteket/rotmappen där serien finns. Det rekommenderas starkt att använda den inbyggda Plex-funktionaliteten som bara övervakar filsystemet eller att använda ett verktyg som [plexautoscan](https://github.com/l3uddz/plex_autoscan)
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
  - Se detta [Tips och tricks-inlägg](/useful-tools#twitter)
- Webhook {#webhook}

# Listor

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH har [en guide](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/) för att synkronisera två instanser
- Plex Watchlist {#pleximport}
  - Lägg helt enkelt till en Plex watchlist för den autentiserade Plex-användaren i Radarr. Observera att det krävs att din lista innehåller serier.
  - För att ha flera användares watchlistor måste du lägga till varje användares listor och autentisera med deras Plex-användare.
- Traktlista {#traktlistimport}
  - Användarnamn - Se till att du anger det faktiska användarnamnet för användaren och inte användarens namn
  - Lista - Se till att du använder listnamnet som visas i listans URL
  - Exempel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Användarnamn: `some-user-name`
    - Lista: `trakt-list-name`
- Trakt populär lista {#traktpopularimport}
- Trakt användare {#traktuserimport}

> Traktlistor bör innehålla serier, inte enskilda avsnitt. Sonarr matchar och lägger bara till serier.
{.is-info}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktivera - Aktivera skapande av metadatafiler för denna metadata-typ
  - Seriemetadata - Skapa en `tvshow.nfo` med fullständig seriemetadata
  - (Avancerad inställning) Seriemetadata-URL - Skapa tvshow.nfo med TheTVDb-seriens URL
  - Avsnittsmetadata - Skapa `<filnamn>.nfo` för varje avsnitt
  - Seriebilder - Skapa olika bilder för serier, inklusive affischer och banderoller med namnen `poster.jpg` och `banner.jpg`
  - Säsongsbilder - Skapa olika bilder för säsonger, inklusive affischer och banderoller med namnen `season##-poster.jpg` och `season##-banner.jpg`
  - Avsnittsbilder - Skapa olika bilder för avsnitt, till exempel tumnaglar med namnet `<filnamn>-thumb.jpg`
- Roksbox {#roksboxmetadata}
  - Aktivera - Aktivera skapande av metadatafiler för denna metadata-typ
  - Avsnittsmetadata - Skapa `Season##\<filnamn>.xml` för varje avsnitt
  - Seriebilder - Skapa `Series Title.jpg`
  - Säsongsbilder - Skapa `Season ##.jpg`
  - Avsnittsbilder - Skapa `Season##\<filnamn>.jpg`
- WDTV {#wdtvmetadata}
  - Aktivera - Aktivera skapande av metadatafiler för denna metadata-typ
  - Avsnittsmetadata - Skapa `Season##\<filnamn>.xml` för varje avsnitt
  - Seriebilder - Skapa `folder.jpg`
  - Säsongsbilder - Skapa `Season ##\folder.jpg`
  - Avsnittsbilder - Skapa `Season##\<filnamn>.metathumb`