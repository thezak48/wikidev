---
title: Nyttige værktøjer
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: useful-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Gendannelse af en korrupt database](#gendannelse-af-en-korrupt-database)
  - [Gendannelse af en korrupt database (UI) (Windows)](#gendannelse-af-en-korrupt-database-ui-windows)
  - [Kommandolinjegenopretning af database](#kommandolinjegenopretning-af-database)
- [Find cookies](#find-cookies)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [Rydning af cookies og lokal lagring](#rydning-af-cookies-og-lokal-lagring)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
  {.links-list}
- [Andre projekter og programmer - Anmodningsapps \*Arrs](#andre-projekter-og-programmer-anmodningsapps-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
  {.links-list}
- [Andre projekter og programmer - \*Arr-relaterede](#andre-projekter-og-programmer-arr-relaterede)
  - [Fjernbetjening](#fjernbetjening)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Android-app](#radarr-sonarr-companion-android-app)
    - [nzb360 - Android-app](#nzb360-android-app)
    {.links-list}
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [Undertekster](#undertekster)
    - [Bazarr](#bazarr)
- [Andre projekter og programmer - Torrents/Downloading](#andre-projekter-og-programmer-torrentsdownloading)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit Management](#qbit-management)
- [Andre projekter og programmer](#andre-projekter-og-programmer)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
  {.links-list}
- [Twitter-forbindelsesinstruktioner](#twitter-forbindelsesinstruktioner)

Følgende apps er ledsagere til \*Arr Suite of Applications eller medieopbevaring generelt. De vedligeholdes, udvikles eller understøttes ikke af \*Arr Development Team. Ret eventuelle specifikke supportspørgsmål til det respektive applikationsudviklingsteam.

# Gendannelse af en korrupt database

Bemærk, at applikationens database kan findes i Application Data Directory, som er linket nedenfor. Mappen kan også angives som et datadir-argument.

- [Lidarr Appdata-mappen](/lidarr/appdata-directory)
- [Prowlarr Appdata-mappen](/prowlarr/appdata-directory)
- [Radarr Appdata-mappen](/radarr/appdata-directory)
- [Readarr Appdata-mappen](/readarr/appdata-directory)
- [Sonarr Appdata-mappen](/sonarr/appdata-directory)
{.links-list}

> Der er to muligheder for at gendanne databasen, som er angivet nedenfor.{.is-info}

- [Brug af DB Browser til SQLite og brug af UI](#gendannelse-af-en-korrupt-db-ui)
- [Brug af Sqlite's `.recover`-funktion](#kommandolinjegenopretning-af-database)
{.links-list}

## Gendannelse af en korrupt database (UI) (Windows)

{#windows}
{#recovering-a-corrupt-db-ui}

> Bemærk, at dette i princippet gør det samme som `.recover`, der kræver Sqlite v3.29 | [Se Sqlite-dokumentationen for flere detaljer om kommandoen `.recover`](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database). Fremgangsmåden er linket nedenfor {.is-info}

> [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/) er et kvalitetsværktøj med åben kildekode til at oprette, designe og redigere databasefiler, der er kompatible med SQLite. DB4S er til brugere og udviklere, der ønsker at oprette, søge og redigere databaser. DB4S bruger en velkendt grænseflade, der ligner et regneark, og der er ikke behov for at lære komplicerede SQL-kommandoer.
{.is-info}

1. Stop applikationen
1. Lav en kopi af din korrupte database (`.db`) og kopier eventuelle `.shm`- og `.wal`-filer med den
1. Åbn din korrupte database i [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/)
1. Fil => Eksport => Eksporter database til SQL-fil
1. Vælg alle tabeller
1. Markér/aktiver "Behold kolonnenavne i INSERT INTO"
1. Eksporter alt
1. Overskriv gammelt skema
1. Gem
1. Luk databasen
1. Ny database => Fil => Importer => importer den fil fra den tidligere eksporttrin
1. Hvis der opstår importfejl eller begrænsningsproblemer, skal du rydde op i den problematiske indsættelseserklæring, hvis det er muligt, eller slette den
1. Udfør følgende SQL: `VACUUM;`
1. Gem databasen, når du bliver bedt om det.
1. Værktøjer => Integritetskontrol; resultatet skal sige OK
1. Luk databasen
1. Fjern alle `wal`, `shm` og `db`-filer fra konfigurationsmappen
1. Gem (eller kopier, hvis \*Arr ikke er på samme system som DB4S) den nye database i konfigurationsmappen og peg applikationen på den. Alle \*Arrs navngiver deres database som `<appnavn>.db`, f.eks. `radarr.db`
1. Ret tilladelserne for den gendannede database om nødvendigt. Ejer skal være brugeren og gruppen, som \*Arr er konfigureret til at køre som.
1. Start applikationen

Bemærk, at gif'en ikke dækker kommandoen `VACUUM;`

![dbrecover.gif](/dbrecover.gif)

## Kommandolinjegenopretning af database

{#nix}

Nedenstående instruktioner er til \*Nix-operativsystemer, men konceptet vil være lignende i Windows-kommandolinjen.

> Dette bruger [sqlite3 `.recover`-kommandoen](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database), som er ideel. Bemærk, at det kræver Sqlite 3.29+
{.is-info}

> Da sqlite3 er påkrævet af \*Arrs, antages det, at du har sqlite3 installeret på dit system {.is-info}

1. Stop applikationen
1. SSH ind på din server eller få adgang til en kommandolinje
1. Indtast `sqlite3 <sti til dårlig database> ".recover" | sqlite3 <outputsti til gendannet database>`
1. Ret tilladelserne for den gendannede database om nødvendigt. Ejer skal være brugeren og gruppen, som \*Arr er konfigureret til at køre som.
1. Fjern eller flyt/omdøb den gamle korrupte database og eventuelle `wal`- eller `shm`-filer i mappen
1. Omdøb den gendannede database. Alle \*Arrs navngiver deres database som `<appnavn>.db`, f.eks. `radarr.db`
1. Start applikationen

# Find cookies

- Nogle websteder kan ikke logges ind automatisk og kræver, at du logger ind manuelt og derefter giver cookies for at fungere. Siderne nedenfor beskriver, hvordan du gør det.

## Generelle instruktioner

1. Log ind på webstedet med din browser ved hjælp af den valgte webstedsadresse, du har valgt at bruge fra Prowlarr indexer-konfigurationen
1. Åbn DevTools-panelet ved at trykke på F12
1. Vælg fanen Netværk
1. Klik på knappen Doc (Chrome Browser) eller HTML-knappen (Firefox Browser)
1. Opdater siden ved at trykke på F5
1. Klik på den første rækkeindgang
1. Vælg fanen Overskrifter i højre panel
1. Find 'cookie:' i afsnittet Anmodningshoveder. Se hjælpeteksten i brugergrænsefladen for din tracker for detaljer
1. Vælg og kopier hele cookiestrengen (alt efter cookie: )
1. Slet alt, der allerede er i Prowlarr indexer-konfigurationens cookiefelt
1. Indsæt den kopierede cookiestreng i dette felt
1. Klik på Gem

> Hvis brugeragent er påkrævet for din tracker, kan den findes i anmodningshovederne
{.is-info}

### Noter

- Sørg for at bruge browseren fra samme maskine, der kører Prowlarr, da cookies sjældent fungerer fra andre platforme.
- På login-siden til webstedet skal du ikke markere nogen indstillinger, der begrænser din session til en IP-adresse eller logger ud efter kort tid. Hvis der er en Husk mig-indstilling, skal du bruge den.
- Sørg for, at du kan få adgang til webstedets torrent-søgeside, inden du henter cookien, da alt, hvad webstedet gør for at forhindre dette (advarsler, ulæste meddelelser eller ulæste PM'er eller en advarsel om lav forhold), vil stoppe Prowlarr fra at have en vellykket test efter brug af cookien.

## Chrome

- Gå til torrent-tracker-webstedet og log ind.

- Tryk på F12

- Under fanen Applikation øverst vil der være "Lager" på venstre side. Du vil se en "Cookies"-undersektion, og under det vil du se din trackers webadresse. Klik på det.

- Klik på "Pass" på den fane eller en lignende post, og der vises en boks med teksten "Cookieværdi" med en streng på ca. 25-30 tegn. Kopier det og indsæt det i applikationen, der har brug for det.

  - Hvis strengen ligner `cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser`, skal hele posten bruges.

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- Du kan også se Chrome-dokumentationen [Chrome cookies](https://developer.chrome.com/docs/devtools/storage/cookies/)

## Firefox

- [Se venligst Mozillas dokumentation](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# Rydning af cookies og lokal lagring

## Chrome

1. Gå til `chrome://settings/siteData`
1. Indtast navnet på webstedet (eller appen), du vil rydde
1. Klik på papirkurven for webstedet

## Firefox

- Se venligst [Mozillas hjælpeartikel](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)

## Microsoft Edge (Chromium)

1. Gå til `edge://settings/siteData`
1. Indtast navnet på webstedet (eller appen), du vil rydde
1. Klik på pilen for webstedet
1. Klik på papirkurven for webstedet

# Andre projekter og programmer - Anmodningsapps \*Arrs

## Notifiarr (fka Discord Notifier)

[Notifiarr](https://notifiarr.com/) er et værktøj, der er oprettet for at lette mere detaljerede Discord-meddelelser af en af \*Arr-udviklerne. Det giver en konfigurerbar måde at tilføje meddelelser (inklusive reaktioner) baseret på de valgte udløsere. Hjemmesiden giver en brugergrænseflade til at vælge, hvad der skal vises i meddelelsen. Inkluderer support til Grab, Import, Upgrade, Health og Failed-meddelelser samt meget mere.

[Wiki](https://notifiarr.wiki/)

Højdepunkter

- Applikationsstatus
- Anmodninger og godkendelser (\~Ombi)
- Tilpassede *ARR-applikationsmeddelelser
- Anmodningssystem med godkendelser
- Følgesystem til brugere til overvågning af en serie eller film og få besked (via @mentions)
- Serverstatus
- Hyppige nye funktioner

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/) giver brugerne mulighed for at anmode om film, tv-shows (serier, sæsoner eller enkeltepisoder) og musikalbummer.

## Overseerr

[Overseerr](https://overseerr.dev/) er et værktøj til anmodningsstyring og medieopdagelse, der er bygget til at fungere med dit eksisterende Plex-økosystem.

## Petio

[Petio](https://petio.tv/) er en tredjeparts ledsager-app, der er tilgængelig for ejere af Plex-servere for at tillade deres brugere at anmode, gennemgå og opdage indhold.

Appen er designet til at være øjeblikkeligt genkendelig og intuitiv, selv for de mest teknologisk agnostiske brugere. Petio hjælper dig med at administrere anmodninger fra dine brugere, oprette forbindelse til andre tredjepartsapps som Sonarr og Radarr, underrette brugerne, når indhold er tilgængeligt, og spore anmodningsstatus. Petio giver også brugerne mulighed for at opdage medier både på og uden for din server, finde relateret indhold hurtigt og nemt og give deres mening til andre brugere.

# Andre projekter og programmer - \*Arr-relaterede

## Fjernbetjening

### LunaSea

[LunaSea](https://www.lunasea.app/) er en fuldt udstyret, open source selvhostet controller! Fokuseret på at give dig en problemfri oplevelse mellem al din selvhostede mediesoftware

### Radarr & Sonarr Companion - Android-app

Tilføj nye film/serier til dit system nemt med din telefon. App tilgængelig på [Google Play](https://play.google.com/store/apps/details?id=easy.radarr)

### nzb360 - Android-app

nzb360 giver styring af Sonarr, Radarr, Lidarr, torrents, usenet og andre tjenester. App tilgængelig på [Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360) Tjek [officiel hjemmeside](https://nzb360.com/) for mere information.

## Lidarr

### AMD

[Automated Music Downloader](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd er et Lidarr ledsager-script til automatisk at downloade musik til Lidarr

### AMVD

[Automated Music Video Downloader](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd er et Lidarr ledsager-script til automatisk at downloade og tagge musikvideoer til brug i andre videoapplikationer (plex/kodi/jellyfin/emby)

## Radarr

## AMTD

[Automated Movie Trailer Downloader](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd er et Radarr ledsager-script til automatisk at downloade filmtrailere og ekstramateriale til brug i andre videoapplikationer (plex/kodi/jellyfin/emby)

## Undertekster

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr) er en ledsagerapplikation til Sonarr og Radarr, der administrerer og downloader undertekster baseret på dine krav.

# Andre projekter og programmer - Torrents/Downloading

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed) er en app designet til at hjælpe dig med at downloade torrents, som du kan krydse seede baseret på dine eksisterende torrents. Den er designet til at matche konservativt for at minimere manuel indgriben. Den understøtter i øjeblikket Jackett og Qbittorrent/rTorrent.

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr) giver en række værktøjer til at løse problemer med Starr-applikationer. Toolbarr giver dig mulighed for at udføre forskellige handlinger mod dine Starr-apps og deres SQLite3-databaser.

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr) Denne applikation kører som en daemon på din downloadvært. Den kontrollerer, om der er fuldførte downloads, og udpakker dem, så \*Arr kan importere dem.

Der er en håndfuld muligheder derude for at udpakke og slette filer efter, at din klient har downloadet dem. Captain kunne bare ikke lide nogen af dem, så han skrev sin egen. Han ønskede en lille enkelt binær med rimelig logging, der kan udpakke downloadede arkiver og rydde op efter, at de er blevet importeret.

## qBit Management

[qBit Management også kendt som "qbit_manage"](https://github.com/StuffAnThings/qbit_manage) er et program, der bruges til at administrere din qBittorrent-instans, f.eks.:



- Mærk torrents baseret på tracker URL (mærk kun torrents, der ikke har nogen tags)
- Opdater kategorier baseret på gemmested
- Fjern ikke-registrerede torrents (slet data og torrent, hvis den ikke er cross-seedet, ellers fjernes kun torrenten)
- Tilføj automatisk cross-seed torrents i paused tilstand (bruges i forbindelse med [cross-seed scriptet](#cross-seed))
- Genkontrollér pausede torrents sorteret efter laveste størrelse og genoptag, hvis de er færdige
- Fjern forældreløse filer fra din rodmappe, som ikke refereres af qBittorrent
- Mærk torrents, der ikke har nogen hard links, og tillad valgfri oprydning for at slette disse torrents og indhold baseret på maksimal ratio og/eller tid seedet

# Andre projekter og programmer

## Filebot

[FileBot](https://www.filebot.net/) er det ultimative værktøj til organisering og omdøbning af dine film, tv-serier og anime samt hentning af undertekster og kunstværker. Det er smart og fungerer bare.

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes) er et program til identifikation og handling af duplikerede filer.

> TRaSH [har en guide](https://trash-guides.info/jdupes) også {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= dette vil kontrollere for dobbelte filer og udskrive en opsummering af resultaterne

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= dette vil genskabe dem som hardlinks og dermed reducere den brugte duplikerede plads

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md) er et PowerShell-script til manuelt at søge efter n elementer, der ikke er mærket med en bestemt tag i dit Radarr/Sonarr-mediebibliotek. n er antallet af elementer, som dette script vil søge efter. Dette har den ekstra fordel, at du ikke overbelaster dine indexere og bliver udelukket :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager) er et Python-script til opdatering af metadataoplysninger for film, serier og samlinger samt automatisk opbygning af samlinger.

## Tautulli

[Tautulli](https://tautulli.com/) er en tredjepartsapplikation, som du kan køre sammen med din Plex Media Server for at overvåge aktivitet og spore forskellige statistikker. Disse statistikker inkluderer, hvad der er blevet set, hvem der har set det, hvornår og hvor de har set det, og hvordan det blev set. Det eneste, der mangler, er "hvorfor de så det", men hvem er jeg til at spørge om dine 42 afspilninger af Frost. Alle statistikker præsenteres i et pænt og rent interface med mange tabeller og grafer, hvilket gør det nemt at prale af din server over for alle andre.

## Tdarr

[Tdarr](https://tdarr.io) er en lukket selvhostet web-app til automatisering af transcode/remux-styring af mediebiblioteket og sikring af, at dine filer er præcis, som du har brug for dem i forhold til codecs/streams/containere osv. Designet til at fungere sammen med [Sonarr](/sonarr)/[Radarr](/radarr) og bygget med fokus på modularisering, parallelisering og skalerbarhed. Hver tilføjet bibliotek har sine egne transcode-indstillinger, filtre og tidsplan. Arbejdere kan startes og lukkes efter behov og er opdelt i 3 typer - 'generel', 'transcode' og 'sundhedstjek'. Arbejdsgrænser kan styres af planlæggeren såvel som manuelt.

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform) er et brugerdefineret script til Sonarr og Radarr til at informere Tdarr om nye/ændrede/slettede filer uden at skulle stole på filsystembegivenheder eller hyppig diskscanning.

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr) er et værktøj til at slette forældede og inaktive medier fra Plex/Sonarr/Radarr. Det hjælper med at administrere begrænset plads, når du tillader brugere at anmode om shows via Overseerr/Ombi, men ikke ønsker at overvåge tilgængelig diskplads manuelt. Det kan konfigureres til kun at slette medier, der opfylder dine definerede kriterier.

## Twitter Connect

Opret en Twitter-applikation (hvis du ikke allerede har en) på <https://apps.twitter.com/>

Udfyld de obligatoriske felter samt callback-URL'en, sæt den til en offentligt tilgængelig URL (ikke localhost), den behøver ikke at eksistere, men den skal være angivet. Brug af <https://sonarr.tv/twitter> eller <https://radarr.video> er tilstrækkeligt.