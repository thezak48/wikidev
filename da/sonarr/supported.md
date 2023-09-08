---
title: Sonarr Understøttet
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> Denne side er under udarbejdelse og kræver yderligere indsats. {.is-warning}

Denne side er disambigueringssiden for alle "understøttede" wiki-links (dvs. typisk `Mere info` i brugergrænsefladen).

# Downloadklienter

{#downloadclient}

- Aria2 {#aria2}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Flood {#flood}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Se indstillingerne](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Se indstillingerne](/sonarr/settings#download-clients)
  - På grund af at uTorrent er adware og tidligere spyware, anbefales det ikke. De fleste brugere bruger Qbittorrent i stedet.
- Vuze {#vuze}
  - [Se indstillingerne](/sonarr/settings#download-clients)

# Indekseringssteder

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - Usenet-indekseringssted til japansk medie (anime) eksklusivt.
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
  - Newznab er en standardiseret API, der bruges af mange usenet-indekseringssider. Der er mange forudindstillinger, men alle kræver en API-nøgle for at være tilgængelige.
  - Indekseringsapplikationer som [Prowlarr](/prowlarr) og [NZBHydra2](https://github.com/theotherp/nzbhydra2) kan give avancerede funktioner som statistiksporing.
- omgwtfnzbs {#omgwtfnzbs}
  - En forældet implementering af en privat usenet-indekser. Brug i stedet Newznab.
  - [Se indstillingerne](/sonarr/settings#indexer-settings)

## Torrents

- BroadcasTheNet (BTN) {#broadcasthenet}
  - Privat tracker
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - Privat tracker
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privat tracker
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privat tracker
  > IP Torrents' native implementering understøtter ikke søgning. Brug den i stedet via Prowlarr eller Jackett som torznab {.is-info}
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-tracker til japansk medie (anime) eksklusivt.
  - Nyaa understøtter kun søgning efter anime-serietyper
  - Der er kendte problemer med den native version af Sonarr
    - [Nyaa seeders/leechers parses ikke korrekt længere. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - Dette kan løses, når/hvis [Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637) bliver fusioneret
  - > Nyaa ser skævt til automatisering og vil ofte blokere din IP. {.is-warning}
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Offentlig tracker
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- Torrent RSS-feed {#torrentrssindexer}
  - Generisk torrent RSS-feed-parser.
  > RSS-feedet skal indeholde en `pubdate`. Det anbefales også at inkludere filstørrelsen.
  {.is-info}
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privat indekseringsside
  - [Se indstillingerne](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab er en ordleg på Torrent og Newznab. Den bruger den samme struktur og syntaks som Newznab API-specifikationen, men eksponerer torrent-specifikke attributter og .torrent-filer. Derfor understøtter den både en nyere RSS-feed og baglog-søgefunktioner. Specifikationen vedligeholdes ikke og understøttes ikke af Newznab-organisationen. (Den samme API-specifikation deles med nZEDb)
  - Dette understøttes primært kun af [Prowlarr](/prowlarr) og [Jackett](https://github.com/Jackett/Jackett)
  - [Se indstillingerne](/sonarr/settings#indexer-settings)

> Mange torrent-trackere trives på fællesskabet og kan have regler på plads, der kræver besøg på webstedet, karma, stemmer, kommentarer osv.
> Gennemgå venligst dine trackeregler og etikette for at holde dit fællesskab i live.
> Vi er ikke ansvarlige, hvis din konto bliver blokeret for at overtræde reglerne eller akkumulere Hit and Runs (HnRs)/lav ratio. {.is-warning}

# Underretninger

{#notification}

- Boxcar {#boxcar}
- Brugerdefineret script {#customscript}
  - Dette giver dig mulighed for at lave et brugerdefineret script, der kører, når en bestemt handling finder sted. Se [Brugerdefinerede scripts](/sonarr/custom-scripts) for flere detaljer.
- Discord {#discord}
  - Langt den mest almindelige måde at sende underretninger om handlinger, der finder sted i Sonarr, på
  - Understøttede felttyper:
  `Oversigt, Bedømmelse, Genrer, Kvalitet, Gruppe, Størrelse, Links, Udgivelse, Plakat, Fanart, Brugerdefinerede formater, Brugerdefineret formatvurdering, Indekseringssted`
- E-mail {#email}
  - Send simpelthen en e-mail til dig selv eller en person, du gerne vil genere. Hvis du bruger Gmail, skal du aktivere mindre sikre apps. Hvis du bruger Gmail og har aktiveret totrinsbekræftelse, skal du bruge et appspecifikt kodeord.

> Du kan bruge en "pæn adresse" som `NogetFlotNavn <email@example.org>` {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi opstod ud af kærligheden til medier. Det er en underholdningshub, der samler al din digitale medieindhold i en smuk og brugervenlig pakke. Det er 100% gratis og open source, meget tilpasseligt og kan køre på en bred vifte af enheder. Det understøttes af et dedikeret team af frivillige og et stort fællesskab. Ved at tilføje Kodi som en forbindelse kan du opdatere Kodis bibliotek, når en ny episode er blevet tilføjet til Sonarr.
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - Forældet
- Plex Media Center {#plexclient}
  - Forældet
- Plex Media Server {#plexserver}
  - Serveren til dit selvhostede Plex-system. Hvis du aktiverer dette, kan du på samme måde som med Kodi sende en opdatering til din Plex-server, der informerer den om, at en ny/forbedret episode er tilgængelig.
  - Dette er sjældent nødvendigt og kræves kun, hvis Plex ikke kan overvåge filsystemet for ændringer.
  - I de få situationer, hvor Plex ikke kan overvåge filsystemet ved hjælp af ionotify - f.eks. visse typer fjernmonteringer og nogle ældre netværksmonteringer - anbefales det at bruge appen plexautoscan i stedet for Plex-forbindelsen

> Bemærk, at dette kan udløse en fuld biblioteksskanning for biblioteket/rodfolderen, som serien er i. Det anbefales kraftigt at bruge den native Plex-funktionalitet, der kun overvåger filsystemet, eller at bruge et værktøj som [plexautoscan](https://github.com/l3uddz/plex_autoscan) {.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Se denne [Tips og tricks-indgang](/useful-tools#twitter)
- Webhook {#webhook}

# Lister

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH har [en guide](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/) til synkronisering af to instanser
- Plex Watchlist {#pleximport}
  - Tilføj simpelthen en Plex-watchliste for den godkendte Plex-bruger til Sonarr. Bemærk, at det er nødvendigt, at din liste indeholder shows.
  - Hvis du vil have flere brugeres watchlister, skal du tilføje hver brugers lister og godkende med deres Plex-bruger.
- Trakt-liste {#traktlistimport}
  - Brugernavn - Sørg for at indtaste brugernavnet på brugeren og ikke brugerens navn
  - Liste - Sørg for at bruge listenavnet, som det vises i listen URL'en
  - Eksempel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Brugernavn: `some-user-name`
    - Liste: `trakt-list-name`
- Trakt-populær liste {#traktpopularimport}
- Trakt-bruger {#traktuserimport}

> Trakt-lister skal indeholde shows, ikke individuelle episoder. Sonarr vil kun matche og tilføje shows. {.is-info}

# Metadata

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktivér - Aktivér oprettelse af metadatafiler for denne metadatatype
  - Seriemetadata - Opret en `tvshow.nfo` med fuld seriemetadata
  - (Avanceret indstilling) Seriemetadata-URL - Opret tvshow.nfo med TheTVDb-serie-URL'en
  - Episodemetadata - Opret `<filnavn>.nfo` for hver episode
  - Seriebilleder - Opret forskellige serie