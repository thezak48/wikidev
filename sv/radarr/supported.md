---
title: Radarr Stöd
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# Innehållsförteckning

> Denna sida är under arbete och kräver ytterligare ansträngning.{.is-warning}

Denna sida är en avledningssida för alla `stödda` wiki-länkar (vanligtvis "mer information" i användargränssnittet).

# Nedladdningsklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Flood {#flood}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se inställningssidan](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se inställningssidan](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se inställningssidan](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se inställningssidan](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se inställningssidan](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [Se inställningssidan](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se inställningssidan](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se inställningssidan](/radarr/settings#download-clients)
  - På grund av att uTorrent är adware och tidigare spyware rekommenderas det inte. De flesta användare använder Qbittorrent istället.
- Vuze {#vuze}
  - [Se inställningssidan](/radarr/settings#download-clients)

# Indexerare

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se inställningssidan](/radarr/settings#indexer-settings)
  - Newznab är en standardiserad API som används av många usenet-indexeringssidor. Många förinställningar finns tillgängliga, men alla kräver en API-nyckel för att vara åtkomliga.
  - Indexeringsprogram som [Prowlarr](/prowlarr) och [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan erbjuda avancerade funktioner som statistikspårning.
- omgwtfnzbs {#omgwtfnzbs}
  - En föråldrad implementering av en privat usenet-indexerare. Använd istället Newznab.
  - [Se inställningssidan](/radarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - Privat tracker
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privat tracker
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents nativa implementation stöder inte sökning. Använd det via Prowlarr eller Jackett som torznab istället {.is-info}
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker för japansk media (anime) exklusivt.
  > Nyaa ogillar automatisering och kommer ofta att blockera din IP-adress. {.is-info}
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - Privat tracker
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- Torrent RSS-flöde {#torrentrssindexer}
  - Generisk torrent RSS-flödesparser.
  > RSS-flödet måste innehålla en `pubdate`. Släppstorleken rekommenderas också. {.is-info}
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - Ett äldre format för Couchpotato före Torznab.
  - [Se inställningssidan](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab är ett ordspel på Torrent och Newznab. Det använder samma struktur och syntax som Newznab API-specifikationen, men exponerar torrent-specifika attribut och .torrent-filer. Stöder därför både ett nytt RSS-flöde och sökfunktioner för backlog. Specifikationen underhålls inte och stöds inte av Newznab-organisationen. (Samma API-specifikation delas med nZEDb)
  - Detta stöds främst av [Prowlarr](/prowlarr) och [Jackett](https://github.com/Jackett/Jackett)
  - [Se inställningssidan](/radarr/settings#indexer-settings)

> Många torrent-trackers är beroende av gemenskapen och kan ha regler som kräver webbplatsbesök, karma, röster, kommentarer, etc.
> Vänligen granska dina trackers regler och etikett, håll din gemenskap vid liv.
> Vi ansvarar inte om ditt konto blir blockerat för att du inte följer reglerna eller för att du får för många Hit and Runs (HnRs)/låg ratio. {.is-warning}

# Notifikationer

{#notification}

- Boxcar {#boxcar}
- Anpassad skript {#customscript}
  - Detta gör att du kan skapa ett anpassat skript som körs när en specifik åtgärd inträffar. Se [Anpassade skript](/radarr/custom-scripts) för mer information.
- Discord {#discord}
  - Långt ifrån det vanligaste sättet att skicka notifikationer om händelser som inträffar i din Radarr
- E-post {#email}
  - Skicka helt enkelt e-post till dig själv eller någon annan som du vill irritera. Om du använder Gmail måste du aktivera mindre säkra appar. Om du använder Gmail och har tvåfaktorsautentisering aktiverat måste du använda ett appspecifikt lösenord.

> Du kan använda en "snygg adress" som `SomePrettyName <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi uppstod ur kärleken till media. Det är en underhållningshubb som samlar all din digitala media i en vacker och användarvänlig förpackning. Den är 100% gratis och öppen källkod, mycket anpassningsbar och fungerar på en mängd olika enheter. Den stöds av ett engagerat team av volontärer och en stor community. Genom att lägga till Kodi som en anslutning kan du uppdatera Kodis bibliotek när en ny film har lagts till i Radarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se posten om [Användbara verktyg - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Servern för ditt självhostade Plex-system. Att aktivera detta är i stort sett samma som Kodi och gör att du kan skicka en uppdatering till din Plex-server som meddelar att en ny/uppdaterad film är tillgänglig.
  - Detta behövs sällan och krävs endast om Plex inte kan övervaka filsystemet för ändringar.
  - I de få situationer där Plex inte kan övervaka filsystemet med hjälp av ionotify - som vissa typer av fjärrmonteringar och ett fåtal äldre nätverksmonteringar - rekommenderas att använda appen plexautoscan istället för Plex-anslutningen.
- Att använda ett verktyg som [plexautoscan](https://github.com/l3uddz/plex_autoscan) är ett annat alternativ.

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
  - Se denna post om [Tips och tricks](/useful-tools#twitter)
- Webhook {#webhook}

# Listor

{#importlist}

- CouchPotato {#couchpotatoimport}
- Anpassade listor {#radarrlistimport}
- IMDb-listor {#imdblistimport}
  - För att lägga till din IMDb Watchlist, gå till din lista och klicka på redigera. Se till att sekretessinställningen är inställd på offentlig. I adressfältet hittar du det `lsxxxxxx`-nummer som du behöver ange i Radarr

    1. Gå till dina IMDB-listinställningar
    1. Se till att sekretessen är inställd på `Offentlig` (dvs. `Inaktiverad`)
    1. Använd `ls`-numret i URL:en

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex Watchlist {#plex}
  - Kräver: v4.1.0.6176+
  - Lägg helt enkelt till en Plex watchlist för den autentiserade Plex-användaren i Radarr. Observera att det krävs att din lista innehåller filmer.
  - För att ha flera användares watchlistor måste du lägga till varje användares listor och autentisera med deras Plex-användare.
- Radarr {#radarrimport}
  - TRaSH har [en guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) för att synkronisera två instanser
- RSS-lista {#rssimport}
- StevenLu Anpassad {#stevenluimport}
	- Gör det möjligt att skapa anpassade filmlistor i JSON-format.
  	Ditt flöde kräver för varje film antingen en `title` eller en `imdb_id`, båda kan tillhandahållas.
  		> Observera att `imdb_id` är säkrare än `title` eftersom det inte kräver en bred sökning
    Här är ett exempel på giltig JSON: 
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
      - Ytterligare nycklar kan läggas till i objekt (kommer att ignoreras)
      - För en tom lista, returnera bara en tom JSON-array `[]`
- StevenLu Lista {#stevenlu2import}
- TMDb-samling {#tmdbcollectionimport}
  - Samlingslistor stöds inte längre i Radarr v4.2 och har migrerats till samlingar inom Radarr. Se avsnittet [Samlingar](/radarr/library#collections) för mer information.
- TMDb-företag {#tmdbcompanyimport}
- TMDb-nyckelord {#tmdbkeywordimport}
- TMDb-lista {#tmdblistimport}
- TMDb-person {#tmdbpersonimport}
  - Om TMDb Person-urlen är `https://www.themoviedb.org/person/500-tom-cruise` är person-ID:t `500`
- TMDb-populär {#tmdbpopularimport}
  - Topplistan använder <https://developers.themoviedb.org/3/movies/get-top-rated-movies>
  - Populär använder <https://developers.themoviedb.org/3/movies/get-popular-movies>
  - På bio använder <https://developers.themoviedb.org/3/movies/get-now-playing>
  - Kommande använder <https://developers.themoviedb.org/3/movies/get-upcoming>
- TMDb-användare {#tmdbuserimport}
- Trakt-lista {#traktlistimport}
  - Användarnamn - Se till att du anger användarnamnet för användaren och inte användarens namn
  - Lista - Se till att du använder listnamnet som presenteras i listans URL
  - Exempel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Användarnamn: `some-user-name`
    - Lista: `trakt-list-name`
- Trakt-populär lista {#traktpopularimport}
- Trakt-användare {#traktuserimport}
  - Denna typ bör användas när du använder din egen watchlist

# Metadata

{#metadata}

- Emby (Legacy) {#mediabrowsermetadata}
  - Aktivera - Aktivera skapande av metadatafiler för denna metadata-typ
  - Filmmetadata - Aktivera skapande av metadatafiler för denna metadata-typ
- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktivera - Aktivera skapande av metadatafiler för denna metadata-typ
  - Filmmetadata - Skapa en `<filnamn>.nfo` med filmens metadata
  - (Avancerad inställning) Filmmetadata-URL - Skapa `movie.nfo` med TMDb- och IMDb-film-URL:er
  - Metadataspråk - Välj det språk som Radarr ska använda för att skriva metadata om det finns tillgängligt på det språket
  - Filmavbilder - Skapa olika avbilder för filmen, inklusive affischer och banderoller
  - Använd Movie.nfo - Skriv nfo-filen som `movie.nfo` istället för standardvärdet
  - Samlingsnamn - Radarr kommer att skriva samlingens namn till .nfo-filen
- Roksbox {#roksboxmetadata}
  - Aktivera - Aktivera skapande av metadatafiler för denna metadata-typ
  - Filmmetadata - Skapa xml-fil för varje film
  - Filmavbilder - Skapa `Movie.jpg`
- WDTV {#wdtvmetadata}
  - Aktivera - Aktivera skapande av metadatafiler för denna metadata-typ
  - Filmmetadata - Skapa `<filnamn>.xml` för varje avsnitt
  - Filmavbilder - Skapa `folder.jpg`