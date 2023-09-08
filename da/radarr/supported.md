---
title: Radarr Understøttet
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# Indholdsfortegnelse

> Denne side er under udarbejdelse og kræver yderligere indsats.{.is-warning}

Denne side er disambigueringssiden for alle `understøttede` wiki-links (dvs. typisk "mere info" i brugergrænsefladen).

# Downloadklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Flood {#flood}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se indstillingerne](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se indstillingerne](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se indstillingerne](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se indstillingerne](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se indstillingerne](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [Se indstillingerne](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se indstillingerne](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se indstillingerne](/radarr/settings#download-clients)
  - På grund af at uTorrent er adware og tidligere spyware, anbefales det ikke. De fleste brugere bruger Qbittorrent.
- Vuze {#vuze}
  - [Se indstillingerne](/radarr/settings#download-clients)

# Indexere

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Se indstillingerne](/radarr/settings#indexer-settings)
  - Newznab er en standardiseret API, der bruges af mange usenet-indekssider. Der er mange forudindstillinger, men alle kræver en API-nøgle for at være tilgængelige.
  - Indexer-applikationer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan give avancerede funktioner som statistiksporing.
- omgwtfnzbs {#omgwtfnzbs}
  - En forældet implementering af en privat usenet-indeks. Brug i stedet Newznab.
  - [Se indstillingerne](/radarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - Privat tracker
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privat tracker
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents' native implementering understøtter ikke søgning. Brug det via Prowlarr eller Jackett som torznab i stedet {.is-info}
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker for japansk medie (anime) eksklusivt.
  > Nyaa ser skævt til automatisering og vil ofte blokere din IP. {.is-info}
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - Privat tracker
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-parser.
  > RSS-feedet skal indeholde en `pubdate`. Det anbefales også at inkludere udgivelsesstørrelsen.
  {.is-info}
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - En forældet Couchpotato i præ-Torznab-format.
  - [Se indstillingerne](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er et ordspil på Torrent og Newznab. Det bruger den samme struktur og syntaks som Newznab API-specifikationen, men eksponerer torrent-specifikke attributter og .torrent-filer. Derfor understøtter det både en nyere RSS-feed og bagudrettet søgning. Specifikationen vedligeholdes ikke og understøttes ikke af Newznab-organisationen. (Den samme API-specifikation deles med nZEDb)
  - Dette understøttes primært kun af [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se indstillingerne](/radarr/settings#indexer-settings)

> Mange torrent-trackere er afhængige af fællesskabet og kan have regler på plads, der kræver besøg på webstedet, karma, stemmer, kommentarer osv.
> Gennemgå venligst dine trackeregler og etikette, og hold dit fællesskab i live.
> Vi er ikke ansvarlige, hvis din konto bliver blokeret for at overtræde reglerne eller akkumulere Hit and Runs (HnRs)/lav ratio.
{.is-warning}

# Notifikationer

{#notification}

- Boxcar {#boxcar}
- Brugerdefineret script {#customscript}
  - Dette giver dig mulighed for at oprette et brugerdefineret script, der skal køres, når en bestemt handling finder sted. Se [Brugerdefinerede scripts](/radarr/custom-scripts) for flere detaljer.
- Discord {#discord}
  - Langt den mest almindelige måde at sende notifikationer om handlinger, der finder sted i din Radarr.
- E-mail {#email}
  - Send simpelthen en e-mail til dig selv eller en person, du gerne vil genere. Hvis du bruger Gmail, skal du aktivere mindre sikre apps. Hvis du bruger Gmail og har aktiveret totrinsbekræftelse, skal du bruge et appspecifikt kodeord.

> Du kan bruge en "pæn adresse" som `EtPæntNavn <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi opstod ud af kærligheden til medier. Det er en underholdningshub, der samler al din digitale medieindhold i en smuk og brugervenlig pakke. Det er 100% gratis og open source, meget tilpasseligt og kan køre på en bred vifte af enheder. Det understøttes af et dedikeret team af frivillige og et stort fællesskab. Ved at tilføje Kodi som en forbindelse kan du opdatere Kodis bibliotek, når en ny film er blevet tilføjet til Radarr.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Se indgangen om [Nyttige værktøjer - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Serveren til dit selvhostede Plex-system. Hvis du aktiverer dette, kan du sende en opdatering til din Plex-server for at give besked om, at en ny/forbedret film er tilgængelig.
  - Dette er sjældent nødvendigt og kræves kun, hvis Plex ikke kan overvåge filsystemet for ændringer.
  - I de få situationer, hvor Plex ikke kan overvåge filsystemet ved hjælp af ionotify - f.eks. visse typer fjernmonteringer og et par ældre netværksmonteringer - anbefales det at bruge appen plexautoscan i stedet for Plex-forbindelsen.
- Du kan også bruge et værktøj som [plexautoscan](https://github.com/l3uddz/plex_autoscan).

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
  - Se denne [Tips og tricks-indgang](/useful-tools#twitter)
- Webhook {#webhook}

# Lister

{#importlist}

- CouchPotato {#couchpotatoimport}
- Brugerdefinerede lister {#radarrlistimport}
- IMDb-lister {#imdblistimport}
  - For at tilføje din IMDb Watchlist skal du gå til din liste og klikke på rediger. Sørg for, at privatlivsindstillingen er indstillet til offentlig. I adresselinjen finder du det `lsxxxxxx`-nummer, som du skal indtaste i Radarr.

    1. Gå til dine IMDB-listeindstillinger
    1. Sørg for, at privatlivet er indstillet til `Public` (dvs. `Disabled)`
    1. Brug `ls`-nummeret i URL'en

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex Watchlist {#plex}
  - Kræver: v4.1.0.6176+
  - Tilføj blot en Plex-watchliste for den godkendte Plex-bruger til Radarr. Bemærk, at det er nødvendigt, at din liste indeholder film.
  - Hvis du vil have flere brugeres watchlister, skal du tilføje hver brugers lister og godkende med deres Plex-bruger.
- Radarr {#radarrimport}
  - TRaSH har [en guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) til synkronisering af to instanser
- RSS-liste {#rssimport}
- StevenLu Custom {#stevenluimport}
	- Giver dig mulighed for at oprette brugerdefinerede film-lister i JSON-format.
  	Dit feed skal for hver film indeholde enten en `title` eller en `imdb_id`, begge kan angives.
  		> Bemærk, at `imdb_id` er sikrere end `title`, da det ikke kræver en bred søgning
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
      - Yderligere nøgler kan tilføjes i elementer (vil blive ignoreret)
      - For en tom liste skal du blot returnere en tom JSON-array `[]`
- StevenLu List {#stevenlu2import}
- TMDb Collection {#tmdbcollectionimport}
  - Collection-lister understøttes ikke længere i Radarr v4.2 og er blevet migreret til samlinger i Radarr. Se [Samlinger](/radarr/library#collections) for flere detaljer.
- TMDb Company {#tmdbcompanyimport}
- TMDb Keyword {#tmdbkeywordimport}
- TMDb List {#tmdblistimport}
- TMDb Person {#tmdbpersonimport}
  - Hvis TMDb Person-url'en er `https://www.themoviedb.org/person/500-tom-cruise`, er Person ID'et `500`
- TMDb Popular {#tmdbpopularimport}
  - Top bruger <https://developers.themoviedb.org/3/movies/get-top-rated-movies>
  - Populære bruger <https://developers.themoviedb.org/3/movies/get-popular-movies>
  - I biografen bruger <https://developers.themoviedb.org/3/movies/get-now-playing>
  - Kommende bruger <https://developers.themoviedb.org/3/movies/get-upcoming>
- TMDb User {#tmdbuserimport}
- Trakt List {#traktlistimport}
  - Brugernavn - Sørg for at indtaste brugernavnet på brugeren og ikke brugerens navn
  - Liste - Sørg for at bruge listenavnet, som det vises i listen URL'en
  - Eksempel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Brugernavn: `some-user-name`
    - Liste: `trakt-list-name`
- Trakt Popular List {#traktpopularimport}
- Trakt User {#traktuserimport}
  - Denne type skal bruges, når du bruger din egen watchlist

# Metadata

{#metadata}

- Emby (Legacy) {#mediabrowsermetadata}
  - Aktivér - Aktivér oprettelse af metadatafil for denne metadatatype
  - Film-metadata - Aktivér oprettelse af metadatafil for denne metadatatype
- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktivér - Aktivér oprettelse af metadatafil for denne metadatatype
  - Film-metadata - Opret en `<filnavn>.nfo` med film-metadata
  - (Avanceret indstilling) Film-metadata-URL - Opret `movie.nfo` med TMDb- og IMDb-film-URL'er
  - Metadatasprog - Vælg det sprog, som Radarr skal bruge til at skrive metadata, hvis det er tilgængeligt på det sprog
  - Film-billeder - Opret forskellige billedfiler til film, herunder plakater og bannere
  - Brug Movie.nfo - Skriv nfo-filen som `movie.nfo` i stedet for standarden
  - Samlingens navn - Radarr skriver samlingens navn til .nfo-filen
- Roksbox {#roksboxmetadata}
  - Aktivér - Aktivér oprettelse af metadatafil for denne metadatatype
  - Film-metadata - Opret XML-fil for hver film
  - Film-billeder - Opret `Movie.jpg`
- WDTV {#wdtvmetadata}
  - Aktivér - Aktivér oprettelse af metadatafil for denne metadatatype
  - Film-metadata - Opret `<filnavn>.xml` for hver episode
  - Film-billeder - Opret `folder.jpg`