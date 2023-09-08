---
title: Nyttige verktøy
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: useful-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Gjenopprette en korrupt database](#gjenopprette-en-korrupt-database)
  - [Gjenopprette en korrupt database (UI) (Windows)](#gjenopprette-en-korrupt-database-ui-windows)
  - [Kommandolinjegjenoppretting av database](#kommandolinjegjenoppretting-av-database)
- [Finne informasjonskapsler](#finne-informasjonskapsler)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [Slette informasjonskapsler og lokal lagring](#slette-informasjonskapsler-og-lokal-lagring)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
  {.links-list}
- [Andre prosjekter og programmer - Arr-forespørselsapper](#andre-prosjekter-og-programmer-arr-forespørselsapper)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
  {.links-list}
- [Andre prosjekter og programmer - Arr-relatert](#andre-prosjekter-og-programmer-arr-relatert)
  - [Fjernkontroll](#fjernkontroll)
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
- [Andre prosjekter og programmer - Torrenter/Nedlasting](#andre-prosjekter-og-programmer-torrenternedlasting)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit Management](#qbit-management)
- [Andre prosjekter og programmer](#andre-prosjekter-og-programmer)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
  {.links-list}
- [Instruksjoner for tilkobling til Twitter](#instruksjoner-for-tilkobling-til-twitter)

Følgende apper er følgesvenner til \*Arr Suite of Applications eller generell medieoppbevaring. De blir ikke vedlikeholdt, utviklet eller støttet av \*Arr Development Team. Vennligst rett spesifikke brukerstøttespørsmål til den respektive applikasjonsutviklingsteamet.

# Gjenopprette en korrupt database

Merk at applikasjonens database kan finnes i Application Data Directory, som er lenket nedenfor. Katalogen kan også sendes som et datadir-argument.

- [Lidarr Appdata Directory](/lidarr/appdata-directory)
- [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- [Radarr Appdata Directory](/radarr/appdata-directory)
- [Readarr Appdata Directory](/readarr/appdata-directory)
- [Sonarr Appdata Directory](/sonarr/appdata-directory)
{.links-list}

> Det er to alternativer for å gjenopprette databasen, som er oppført nedenfor.{.is-info}

- [Bruke DB Browser for SQLite og bruke brukergrensesnittet](#gjenopprette-en-korrupt-db-ui)
- [Bruke Sqlite's `.recover`-funksjon](#kommandolinjegjenoppretting-av-database)
{.links-list}

## Gjenopprette en korrupt database (UI) (Windows)

{#windows}
{#recovering-a-corrupt-db-ui}

> Merk at dette i praksis gjør det samme som `.recover`, som krever Sqlite v3.29 | [Se Sqlite-dokumentasjonen for mer informasjon om `.recover`-kommandoen](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database). Fremgangsmåten for å gjøre dette er lenket nedenfor {.is-info}

> [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/) er et kraftig, visuelt, åpen kildekode-verktøy for å opprette, designe og redigere databasefiler som er kompatible med SQLite. DB4S er for brukere og utviklere som ønsker å opprette, søke og redigere databaser. DB4S bruker et kjent regneark-lignende grensesnitt, og komplekse SQL-kommandoer trenger ikke å læres.
{.is-info}

1. Stopp applikasjonen
1. Lag en kopi av den korrupte databasen (`.db`) og kopier eventuelle `.shm`- og `.wal`-filer sammen med den
1. Åpne den korrupte databasen i [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/)
1. Fil => Eksporter => Eksporter database til SQL-fil
1. Velg alle tabeller
1. Sjekk/Aktiver "Behold kolonnenavn i INSERT INTO"
1. Eksporter alt
1. Overskriv gammelt skjema
1. Lagre
1. Lukk databasen
1. Ny database => Fil => Importer => importer den filen fra forrige eksporttrinn
1. Hvis det oppstår importfeil eller begrensninger, rydd opp i den problematiske INSERT INTO-setningen hvis det er mulig, eller slett den
1. Kjør følgende SQL: `VACUUM;`
1. Lagre databasen når du blir bedt om det.
1. Verktøy => Integritetssjekk; resultatet skal si OK
1. Lukk databasen
1. Fjern alle `wal`-, `shm`- og `db`-filer fra konfigurasjonsmappen
1. Lagre (eller kopier, hvis \*Arr ikke er på samme system som DB4S) den nye databasen i konfigurasjonsmappen og pek applikasjonen til den. Alle \*Arrs navngir databasen sin som `<appnavn>.db`, f.eks. `radarr.db`
1. Rett opp tillatelser for den gjenopprettede databasen hvis nødvendig. Eieren skal være brukeren og gruppen som \*Arr er konfigurert til å kjøre som.
1. Start applikasjonen

Vær oppmerksom på at gifen ikke dekker `VACUUM;`-kommandoen

![dbrecover.gif](/dbrecover.gif)

## Kommandolinjegjenoppretting av database

{#nix}

Nedenstående instruksjoner gjelder for \*Nix-operativsystemer, men konseptet vil være likt på Windows-kommandolinjen.

> Dette bruker [sqlite3 `.recover`-kommandoen](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database), som er ideell. Merk at det krever Sqlite 3.29+
{.is-info}

> Siden sqlite3 er nødvendig for \*Arrs, antas det at du har sqlite3 installert på systemet ditt {.is-info}

1. Stopp applikasjonen
1. SSH inn på maskinen din eller få på annen måte opp en kommandolinje
1. Skriv inn `sqlite3 <sti til den ødelagte databasen> ".recover" | sqlite3 <utdatasti for gjenopprettet database>`
1. Rett opp tillatelser for den gjenopprettede databasen hvis nødvendig. Eieren skal være brukeren og gruppen som \*Arr er konfigurert til å kjøre som.
1. Fjern eller flytt/omdøp den gamle ødelagte databasen og eventuelle `wal`- eller `shm`-filer i mappen
1. Gi den gjenopprettede databasen et nytt navn. Alle \*Arrs navngir databasen sin som `<appnavn>.db`, f.eks. `radarr.db`
1. Start applikasjonen

# Finne informasjonskapsler

- Noen nettsteder kan ikke logges inn automatisk og krever at du logger inn manuelt og deretter gir informasjonskapslene for å fungere. Sidene nedenfor beskriver hvordan du gjør det.

## Generelle instruksjoner

1. Logg inn på nettstedet med nettleseren din ved å bruke nettstedets lenkeadresse du har valgt å bruke fra Prowlarr-indekskonfigurasjonen
1. Åpne DevTools-panelet ved å trykke F12
1. Velg nettverkfanen
1. Klikk på Dokument-knappen (Chrome-nettleser) eller HTML-knappen (Firefox-nettleser)
1. Oppdater siden ved å trykke F5
1. Klikk på den første radoppføringen
1. Velg fanen Headers i høyre panel
1. Finn 'cookie:' i delen Request Headers. Se hjelpeteksten i brukergrensesnittet for spesifikk informasjon om sporingen din
1. Velg og kopier hele informasjonskapselstrengen (alt etter cookie:)
1. Slett alt som allerede er i informasjonskapselboksen i Prowlarr-indekskonfigurasjonen
1. Lim inn den kopierte informasjonskapselstrengen i den boksen
1. Klikk Lagre

> Hvis brukeragenten er nødvendig for sporingen din, finner du den i Request Headers
{.is-info}

### Merknader

- Sørg for å bruke nettleseren fra samme maskin som kjører Prowlarr, da informasjonskapsler sjelden fungerer fra andre plattformer.
- På påloggingssiden for nettstedet, ikke merk av for alternativer som begrenser økten din til én IP-adresse, eller logg ut etter kort tid. Hvis det er et alternativ for Husk meg, bruk det.
- Sørg for at du kan få tilgang til nettstedets torrentsøkeside før du henter informasjonskapselen, da alt nettstedet gjør for å forhindre dette (varsler, uleste meldinger eller uleste PM-er, eller en advarsel om lav forhold) vil stoppe Prowlarr fra å ha en vellykket test etter bruk av informasjonskapselen.

## Chrome

- Gå til torrentsporingsnettstedet og logg inn.

- Trykk F12

- Under fanen Application øverst vil det være "Storage" på venstre side. Du vil se en "Cookies"-underseksjon, og under den vil du se nettstedets URL for sporingen din. Klikk på den.

- Klikk på "Pass" på den fanen eller en lignende oppføring, og det vil dukke opp en boks som sier "Cookie Value" med en streng på ca. 25-30 tegn. Kopier den og lim den inn i applikasjonen som trenger den.

  - Hvis strengen ser lignende ut som `cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser`, bør hele oppføringen brukes.

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- Du kan også se Chrome-dokumentasjonen [Chrome cookies](https://developer.chrome.com/docs/devtools/storage/cookies/)

## Firefox

- [Se Mozillas dokumentasjon](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# Slette informasjonskapsler og lokal lagring

## Chrome

1. Gå til `chrome://settings/siteData`
1. Skriv inn navnet på nettstedet (eller appen) du vil slette
1. Klikk på søppelikonet for nettstedet

## Firefox

- Se [Mozillas hjelpeartikkel](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)

## Microsoft Edge (Chromium)

1. Gå til `edge://settings/siteData`
1. Skriv inn navnet på nettstedet (eller appen) du vil slette
1. Klikk på pilen for nettstedet
1. Klikk på søppelikonet for nettstedet

# Andre prosjekter og programmer - Arr-forespørselsapper

## Notifiarr (fka Discord Notifier)

[Notifiarr](https://notifiarr.com/) er et verktøy opprettet for å lette mer detaljerte Discord-varsler av en av \*Arr-utviklerne. Det gir en konfigurerbar måte å legge til varsler (inkludert reaksjoner) basert på valgte utløsere. Nettstedet gir et brukergrensesnitt for å velge hva som skal vises i varselet. Inkluderer støtte for varsler om Grab, Import, Upgrade, Health og Failed, i tillegg til mye mer.

[Wiki](https://notifiarr.wiki/)

Høydepunkter

- Applikasjonsstatus
- Forespørsler og godkjenninger (\~Ombi)
- Tilpassbare *ARR-applikasjonsvarsler
- Forespøringsystem med godkjenninger
- Følgesystem for brukere for å overvåke en serie eller film og bli varslet (via @mentions)
- Serverstatus
- Hyppige nye funksjoner

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/) gir brukerne muligheten til å be om filmer, TV-serier (serier, sesonger eller enkeltavsnitt) og musikkalbum.

## Overseerr

[Overseerr](https://overseerr.dev/) er et verktøy for håndtering av forespørsler og medieoppdagelse som er bygget for å fungere med ditt eksisterende Plex-økosystem.

## Petio

[Petio](https://petio.tv/) er en tredjeparts følgeapp tilgjengelig for Plex-servereiere for å la brukerne deres be om, vurdere og oppdage innhold.

Appen er utformet for å umiddelbart virke kjent og intuitiv selv for de mest teknologiagnostiske brukerne. Petio hjelper deg med å håndtere forespørslene fra brukerne dine, koble til andre tredjepartsapper som Sonarr og Radarr, varsle brukerne når innhold er tilgjengelig og spore fremdriften for forespørsler. Petio lar også brukerne oppdage medier både på og utenfor serveren din, raskt og enkelt finne relatert innhold og legge igjen sin mening for andre brukere.

# Andre prosjekter og programmer - Arr-relatert

## Fjernkontroll

### LunaSea

[LunaSea](https://www.lunasea.app/) er en fullverdig, åpen kildekode selvvertet kontroller! Fokusert på å gi deg en sømløs opplevelse mellom all din selvvertede medieprogramvare

### Radarr & Sonarr Companion - Android-app

Legg til nye filmer/serier i systemet ditt enkelt med telefonen din. App tilgjengelig på [Google Play](https://play.google.com/store/apps/details?id=easy.radarr)

### nzb360 - Android-app

nzb360 gir administrasjon av Sonarr, Radarr, Lidarr, torrents, usenet og andre tjenester. App tilgjengelig på [Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360) Sjekk [offisiell nettside](https://nzb360.com/) for mer informasjon.

## Lidarr

### AMD

[Automated Music Downloader](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd er et Lidarr-følgeskript for å laste ned musikk automatisk for Lidarr

### AMVD

[Automated Music Video Downloader](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd er et Lidarr-følgeskript for å laste ned og merke musikkvideoer for bruk i andre videoprogrammer (plex/kodi/jellyfin/emby)

## Radarr

## AMTD

[Automated Movie Trailer Downloader](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd er et Radarr-følgeskript for å laste ned filmtrailere og ekstramateriale for bruk i andre videoprogrammer (plex/kodi/jellyfin/emby)

## Undertekster

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr) er en følgeapplikasjon til Sonarr og Radarr som administrerer og laster ned undertekster basert på dine krav.

# Andre prosjekter og programmer - Torrenter/Nedlasting

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed) er en app designet for å hjelpe deg med å laste ned torrents som du kan krysse-seede basert på dine eksisterende torrents. Den er designet for å matche konservativt for å minimere manuell inngripen. Den støtter Jackett og Qbittorrent/rTorrent for øyeblikket.

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr) gir en pakke med verktøy for å løse problemer med Starr-applikasjoner. Toolbarr lar deg utføre ulike handlinger mot Starr-appene og deres SQLite3-databaser.

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr) Denne applikasjonen kjører som en daemon på nedlastingsverten din. Den sjekker for fullførte nedlastinger og pakker dem ut slik at \*Arr kan importere dem.

Det finnes en håndfull alternativer der ute for å pakke ut og slette filer etter at klienten din har lastet dem ned. Captain likte bare ingen av dem, så han skrev sin egen. Han ønsket en liten enkeltstående binærfil med rimelig logging som kan pakke ut nedlastede arkiver og rydde opp etter at de har blitt importert.

## qBit Management

[qBit Management a.k.a. "qbit_manage"](https://github.com/StuffAnThings/qbit_manage) er et program som brukes til å administrere qBittorrent-instansen din, for eksempel:



- Merk torrents med tagger basert på tracker-URL (merk bare torrents som ikke har noen tagger)
- Oppdater kategorier basert på lagringskatalog
- Fjern uregistrerte torrents (slett data og torrent hvis den ikke blir kryss-seedet, ellers vil den bare fjerne torrenten)
- Legg automatisk til kryss-seed torrents i pausemodus (brukes i kombinasjon med [kryss-seed skriptet](#cross-seed))
- Kontroller på nytt torrents i pausemodus sortert etter lavest størrelse og fortsett hvis fullført
- Fjern foreldreløse filer fra rotkatalogen din som ikke er referert til av qBittorrent
- Merk torrents som ikke har hardlinker og tillater valgfri opprydding for å slette disse torrentene og innholdet basert på maksimal ratio og/eller tid seedet

# Andre prosjekter og programmer

## Filebot

[FileBot](https://www.filebot.net/) er det ultimate verktøyet for å organisere og gi nye navn til filmene dine, TV-seriene dine og animasjonene dine, samt hente undertekster og kunstverk. Det er smart og fungerer bare.

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes) er et program for å identifisere og utføre handlinger på duplikatfiler.

> TRaSH [har en guide](https://trash-guides.info/jdupes) også {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= dette vil sjekke for doble filer og skrive ut en oppsummering av resultatene

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= dette vil gjenskape dem som hardlinker og dermed redusere den brukte duplikatplassen

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md) er et PowerShell-skript for å søke manuelt etter n elementer som ikke er merket med en spesifikk tagg i mediebiblioteket ditt i Radarr/Sonarr. n er antall elementer dette skriptet vil søke etter, dette har den ekstra fordelen at du ikke overbelaster indekseringsverktøyene dine og blir utestengt :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager) er et Python-skript for å oppdatere metadatainformasjon for filmer, serier og samlinger, samt automatisk bygge samlinger.

## Tautulli

[Tautulli](https://tautulli.com/) er en tredjepartsapplikasjon som du kan kjøre sammen med Plex Media Server for å overvåke aktivitet og spore ulike statistikker. Viktigst av alt inkluderer disse statistikkene hva som er blitt sett, hvem som så det, når og hvor de så det, og hvordan det ble sett. Det eneste som mangler er "hvorfor de så det", men hvem er jeg til å spørre om dine 42 avspillinger av Frost. Alle statistikker presenteres i et pent og ryddig grensesnitt med mange tabeller og diagrammer, noe som gjør det enkelt å skryte av serveren din til alle andre.

## Tdarr

[Tdarr](https://tdarr.io) er en lukket selvhostet web-app for automatisering av transkode/remux-håndtering av mediebiblioteket og for å sikre at filene dine er akkurat slik du trenger dem når det gjelder kodeker/strømmer/containere osv. Designet for å fungere sammen med [Sonarr](/sonarr)/[Radarr](/radarr) og bygget med mål om modularisering, parallelisering og skalerbarhet, har hver bibliotek du legger til sine egne transkodeinnstillinger, filtre og plan. Arbeidere kan startes opp og avsluttes etter behov, og de er delt inn i 3 typer - 'generell', 'transkode' og 'helsekontroll'. Arbeidsgrenser kan administreres av planleggeren så vel som manuelt.

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform) er et tilpasset skript for Sonarr og Radarr for å informere Tdarr om nye/endrede/slettede filer uten å være avhengig av filsystemhendelser eller hyppig disk-skanning.

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr) er et verktøy for å slette utdatert og inaktivt media fra Plex/Sonarr/Radarr. Det hjelper til med å administrere begrenset plass når du lar brukere be om TV-serier via Overseerr/Ombi, men ikke ønsker å overvåke tilgjengelig diskplass manuelt. Det kan konfigureres til å bare slette media som oppfyller dine definerte kriterier.

## Twitter Connect

Opprett en Twitter-applikasjon (hvis du ikke allerede har gjort det) på <https://apps.twitter.com/>

Fyll ut de obligatoriske feltene samt tilbakeringings-URL-en, sett den til en offentlig tilgjengelig URL (ikke localhost), den trenger ikke å eksistere, men den må være satt, bruk av <https://sonarr.tv/twitter> eller <https://radarr.video> er tilstrekkelig.