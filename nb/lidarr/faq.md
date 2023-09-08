---
title: Lidarr FAQ
description: Vanlige spørsmål om Lidarr
published: true
date: 2023-08-31T19:08:18.905Z
tags: lidarr, needs-love, faq
editor: markdown
dateCreated: 2021-06-14T14:33:41.344Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
  - [Hvordan fungerer Lidarr?](#hvordan-fungerer-lidarr)
  - [Hvordan finner Lidarr utgivelser?](#hvordan-finner-lidarr-utgivelser)
  - [Tvungen autentisering](#tvungen-autentisering)
  - [Hvordan sammenlignes mulige nedlastinger?](#hvordan-sammenlignes-mulige-nedlastinger)
  - [Lidarr sluttet å fungere etter oppdatering til Ubuntu 22.04](#lidarr-sluttet-å-fungere-etter-oppdatering-til-ubuntu-2204)
  - [Hvorfor kan jeg ikke legge til en ny utgivelse eller artist i Lidarr?](#hvorfor-kan-jeg-ikke-legge-til-en-ny-utgivelse-eller-artist-i-lidarr)
  - [Hvorfor kan jeg ikke legge til et album med forskjellige artister?](#hvorfor-kan-jeg-ikke-legge-til-et-album-med-forskjellige-artister)
  - [Hvorfor viser Lidarr bare studioalbum, hvordan finner jeg singler eller EP-er?](#hvorfor-viser-lidarr-bare-studioalbum-hvordan-finner-jeg-singler-eller-ep-er)
  - [Kan jeg legge til bare et album?](#kan-jeg-legge-til-bare-et-album)
  - [Kan jeg laste ned enkeltspor?](#kan-jeg-laste-ned-enkeltspor)
  - [Hvorfor vises ikke artisten X i søket?](#hvorfor-vises-ikke-artisten-x-i-søket)
  - [Lidarr matchet et album med for mange spor. Hvordan kan jeg endre albumet til riktig utgivelse?](#lidarr-matchet-et-album-med-for-mange-spor-hvordan-kan-jeg-endre-albumet-til-riktig-utgivelse)
  - [Jeg finner ikke en utgivelse i Lidarr, men den er på MusicBrainz](#jeg-finner-ikke-en-utgivelse-i-lidarr-men-den-er-på-musicbrainz)
  - [Hvor ofte synkroniseres Lidarrs og MusicBrainz-databasene?](#hvor-ofte-synkroniseres-lidarrs-og-musicbrainz-databasene)
  - [Hvordan kan jeg legge til manglende artistbilder?](#hvordan-kan-jeg-legge-til-manglende-artistbilder)
  - [Hvordan kan jeg få manglende albumbilder? (Cover Art)](#hvordan-kan-jeg-få-manglende-albumbilder-cover-art)
  - [Jeg har problemer med å importere artistene mine, hva kan det være?](#jeg-har-problemer-med-å-importere-artistene-mine-hva-kan-det-være)
  - [Hvordan kan jeg endre navn på artistmappene mine?](#hvordan-kan-jeg-endre-navn-på-artistmappene-mine)
  - [Hvordan kan jeg masse-slette artister fra ønskelisten?](#hvordan-kan-jeg-masse-slette-artister-fra-ønskelisten)
  - [Hvorfor fungerer ikke Lidarr bak en omvendt proxy](#hvorfor-fungerer-ikke-lidarr-bak-en-omvendt-proxy)
  - [Hvordan oppdaterer jeg Lidarr?](#hvordan-oppdaterer-jeg-lidarr)
    - [Kan jeg oppdatere Lidarr inne i Docker-kontaineren min?](#kan-jeg-oppdatere-lidarr-inne-i-docker-kontaineren-min)
    - [Installerer en nyere versjon](#installerer-en-nyere-versjon)
      - [Lokal](#lokal)
      - [Docker](#docker)
  - [Kan jeg bytte fra `nightly` tilbake til `develop`?](#kan-jeg-bytte-fra-nightly-tilbake-til-develop)
  - [Kan jeg bytte mellom grener?](#kan-jeg-bytte-mellom-grener)
  - [Jeg får en feilmelding: Database disk image is malformed](#jeg-får-en-feilmelding-database-disk-image-is-malformed)
  - [Hvordan sikkerhetskopierer/gjenoppretter jeg Lidarr?](#hvordan-sikkerhetskopierergjenoppretter-jeg-lidarr)
    - [Sikkerhetskopiering av Lidarr](#sikkerhetskopiering-av-lidarr)
      - [Bruke innebygd sikkerhetskopiering](#bruke-innebygd-sikkerhetskopiering)
      - [Bruke filsystemet direkte](#bruke-filsystemet-direkte)
    - [Gjenoppretting fra sikkerhetskopi](#gjenoppretting-fra-sikkerhetskopi)
      - [Bruke zip-sikkerhetskopi](#bruke-zip-sikkerhetskopi)
      - [Bruke filsystem-sikkerhetskopi](#bruke-filsystem-sikkerhetskopi)
      - [Gjenoppretting av filsystem på Synology NAS](#gjenoppretting-av-filsystem-på-synology-nas)
  - [Jeg bruker Lidarr på en Mac og det sluttet plutselig å fungere. Hva skjedde?](#jeg-bruker-lidarr-på-en-mac-og-det-sluttet-plutselig-å-fungere-hva-skjedde)
  - [Jeg bruker en Pi og Raspbian, og Lidarr vil ikke starte](#jeg-bruker-en-pi-og-raspbian-og-lidarr-vil-ikke-starte)
  - [Hvorfor tar synkronisering av lister så lang tid, og kan jeg endre det?](#hvorfor-tar-synkronisering-av-lister-så-lang-tid-og-kan-jeg-endre-det)
  - [Kan jeg deaktivere oppdatering av utgivelser?](#kan-jeg-deaktivere-oppdatering-av-utgivelser)
  - [Hvorfor kan ikke Lidarr se filene mine på en ekstern server?](#hvorfor-kan-ikke-lidarr-se-filene-mine-på-en-ekstern-server)
    - [Lidarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder](#lidarr-kjører-som-standard-under-localservice-kontoen-som-ikke-har-tilgang-til-beskyttede-eksterne-filområder)
    - [Du bruker et kartlagt nettverksstasjon (ikke en UNC-sti)](#du-bruker-et-kartlagt-nettverksstasjon-ikke-en-unc-sti)
  - [Hjelp, jeg har låst meg ute](#hjelp-jeg-har-låst-meg-ute)
  - [Hvordan stopper jeg nettleseren fra å starte ved oppstart?](#hvordan-stopper-jeg-nettleseren-fra-å-starte-ved-oppstart)
  - [Rare UI-problemer](#rare-ui-problemer)
  - [VPNs, Jackett og \*ARRs](#vpns-jackett-og-arrs)
  - [Jacketts /all-endepunkt](#jacketts-all-endepunkt)
    - [Jackett /All-løsninger](#jackett-all-løsninger)
  - [Hvorfor er det to filer? | Hvorfor er det en fil igjen i nedlastinger?](#hvorfor-er-det-to-filer--hvorfor-er-det-en-fil-igjen-i-nedlastinger)
  - [Jeg får stadig advarsler fra skyoppbevaringen min om API-grenser](#jeg-får-stadig-advarsler-fra-skyoppbevaringen-min-om-api-grenser)

## Hvordan fungerer Lidarr?

- Lidarr er avhengig av RSS-feeder for å automatisere nedlasting av utgivelser når de blir publisert, både nye utgivelser og tidligere utgitte utgivelser som blir publisert eller gjenutgitt. RSS-feeden er de nyeste utgivelsene fra et nettsted, vanligvis mellom 50 og 100 utgivelser, selv om noen nettsteder gir mer og noen mindre. RSS-feeden består av alle nylig tilgjengelige utgivelser, inkludert utgivelser for ønsket media du ikke følger. Hvis du ser på feilsøkingslogger, vil du se at disse utgivelsene blir behandlet, noe som er helt normalt.
- Lidarr tvinger en minimumsinterval på 10 minutter for RSS-synkronisering og en maksimumsinterval på 2 timer. 15 minutter er anbefalt minimum av de fleste indekseringsnettsteder, selv om noen tillater kortere intervaller, og 2 timer sikrer at Lidarr sjekker ofte nok til å ikke gå glipp av en utgivelse (selv om den kan bla gjennom RSS-feeden på mange indekseringsnettsteder for å hjelpe til med det). Noen indekseringsnettsteder tillater klienter å utføre en RSS-synkronisering oftere enn 10 minutter. I slike tilfeller anbefaler vi å bruke Lidarrs Release-Push API-endepunkt sammen med en IRC-annonsekanal for å sende utgivelser til Lidarr for behandling, noe som kan skje nesten i sanntid og med mindre belastning på indekseringsnettstedet og Lidarr, ettersom Lidarr ikke trenger å be om RSS-feeden for ofte og behandle de samme utgivelsene om og om igjen.

## Hvordan finner Lidarr utgivelser?

- Lidarr søker ''ikke'' regelmessig etter albumfiler som mangler eller ikke oppfyller kvalitetsmålene. I stedet spør den ganske ofte indekseringsnettstedene og sporingsserverne dine etter ''alle'' de nylig publiserte utgivelsene, og sammenligner deretter dette med listen over utgivelser som mangler eller trenger oppgradering. Eventuelle treff blir lastet ned. Dette gjør at Lidarr kan dekke et bibliotek av ''hvilken som helst størrelse'' med bare 24-100 spørringer per dag (RSS-intervall på 15-60 minutter). Hvis du forstår dette, vil du innse at det bare dekker ''fremtiden''.
- Så hvordan håndterer du nåtiden og fortiden? Når du legger til et album, må du angi riktig bane, profil og overvåkingsstatus, og deretter bruke avmerkingsboksen Start søk etter manglende album. Hvis albumet ikke er utgitt ennå, trenger du ikke å starte et søk.
- Med andre ord vil Lidarr bare finne utgivelser som nylig er lastet opp til indekseringsnettstedene dine. Den vil ikke aktivt prøve å finne utgivelser du ønsker som ble lastet opp tidligere.
- Hvis du allerede har lagt til albumet, men nå vil søke etter det, har du noen valg. Du kan gå til albumets side og bruke søkeknappen, som vil utføre et søk og deretter automatisk velge ett. Du kan bruke fanen Søk og se ''alle'' resultatene, og velge det du vil ha. Eller du kan bruke filtrene for `Mangler`, `Ønsket` eller `Kuttet ikke oppfylt`.
- Hvis Lidarr har vært frakoblet i lang tid, vil Lidarr forsøke å bla tilbake for å finne den siste utgivelsen den behandlet, for å unngå å gå glipp av en utgivelse. Så lenge indekseringsnettstedet ditt støtter blading og det ikke har gått for lang tid, vil Lidarr kunne behandle utgivelsene den ville ha gått glipp av, og du slipper å søke etter de utgivelsene.

## Tvungen autentisering

Hvis Lidarr er eksponert slik at brukergrensesnittet kan nås utenfor det lokale nettverket ditt, bør du ha en form for autentiseringsmetode aktivert for å få tilgang til brukergrensesnittet. Dette kreves også i økende grad av sporingsnettsteder og indekseringsnettsteder.

Fra og med Lidarr v2 er autentisering obligatorisk.

### Autentiseringsmetode

- `Basic` (Nettleser popup) - Denne opsjonen viser en liten popup når du får tilgang til Lidarr, som lar deg skrive inn et brukernavn og passord.
- `Forms` (Påloggingsside) - Denne opsjonen har en kjent påloggingsrute som ligner på andre nettsteder, som lar deg logge på Lidarr.
- `External` - Konfigurerbart via konfigurasjonsfilen
  - Hvis du bruker **ekstern autentisering** som Authelia, Authetik, NGINX Basic auth, osv., kan du unngå dobbel autentisering ved å lukke ned appen, angi `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurasjonsfilen](/lidarr/appdata-directory) og starte appen på nytt. **Merk at flere `AuthenticationMethod`-oppføringer i filen ikke støttes, og bare den øverste verdien vil bli brukt.**

### Påkrevd autentisering

- Hvis du ikke eksponerer appen eksternt og/eller ikke ønsker at autentisering skal være påkrevd for lokal (f.eks. LAN) tilgang, kan du endre innstillingen i Innstillinger => Generell sikkerhet => Påkrevd autentisering til `Deaktivert for lokale adresser`
  - Den tilsvarende konfigurasjonsfilen for dette er `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Hvordan sammenlignes mulige nedlastinger?

> Generelt sett har kvalitet prioritet. Hvis du ønsker at kvalitet ikke skal være hovedprioritet, kan du slå sammen kvalitetene dine. [Se TRaSHs guide](https://trash-guides.info/merge-quality)***
{.is-info}

- Den nåværende logikken [kan finnes her](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- Fra og med 2022-01-23 er logikken som følger:

1. Kvalitet
1. Foretrukket ordpoeng
1. Protokoll (som konfigurert i den relevante forsinkelsesprofilen)
1. Indekseringsprioritet
1. Seeder/leecher (hvis torrent)
1. Antall album
1. Alder (hvis Usenet)
1. Størrelse

## Lidarr sluttet å fungere etter oppdatering til Ubuntu 22.04

- Lidarr v0.8 er ikke kompatibel og ikke støttet på Ubuntu 22.04
- Bare Lidarr v1 støtter Ubuntu 22.04
- [Se dette FAQ-innlegget for grenene og versjonene](#hvordan-oppdaterer-jeg-lidarr)

## Hvorfor kan jeg ikke legge til en ny utgivelse eller artist i Lidarr?

- Utgivelsen er sannsynligvis av typen `ukjent` på MusicBrainz

## Hvorfor kan jeg ikke legge til et album med forskjellige artister?

- Diverse artister og andre meta-artister på MusicBrainz skyldes antall oppføringer de gir.

## Hvorfor viser Lidarr bare studioalbum, hvordan finner jeg singler eller EP-er?

- Lidarr viser som standard bare studioalbum for hver artist. Du kan imidlertid utvide albumtypene per artist eller for hele biblioteket ditt ved å bruke metadataprofiler.

## Kan jeg legge til bare et album?

- Ikke for øyeblikket.

## Kan jeg laste ned enkeltspor?

- Lidarr fungerer ved å søke etter og laste ned hele utgivelser, derfor kan ikke enkeltspor lastes ned med mindre de ble utgitt som en singel av artisten.

## Hvorfor vises ikke artisten X i søket?

- Søket er fortsatt under utvikling. Artister som ikke vises i søket kan legges til ved å søke etter `lidarr:mbid`, der `mbid` er MusicBrainz-ID-en til artisten.

## Lidarr matchet et album med for mange spor. Hvordan kan jeg endre albumet til riktig utgivelse?

- Åpne detaljsiden for albumet og velg redigeringsikonet i toppnavigasjonen. Der finner du en rullegardinliste over alle utgivelser knyttet til det albumet.

## Jeg finner ikke en utgivelse i Lidarr, men den er på MusicBrainz

- Dette skyldes sannsynligvis at utgivelsen har en `ukjent` utgivelsesstatus. Oppdater MusicBrainz.

## Hvor ofte synkroniseres Lidarrs og MusicBrainz-databasene?

- Hver time, 5 minutter over timen

## Hvordan kan jeg legge til manglende artistbilder?

- Legg til kunst på fanart.tv og vent i ~7+ dager for at det skal bli fjernet fra hurtigbufferen. Deretter oppdaterer du metadataen.

## Hvordan kan jeg få manglende albumbilder? (Cover Art)

- Legg til coverart på musicbrainz og vent i ~1 time+ for at det skal bli fjernet fra hurtigbufferen. Deretter oppdaterer du metadataen.

## Jeg har problemer med å importere artistene mine, hva kan det være?

- Artistimportprosessen importerer bare artistnavnene og baneområdene, som deretter lagres i databasen slik at a) metadata kan hentes og b) nedlastet innhold kan plasseres på samme sted i fremtiden. Til dette formålet trenger brukerkontoen som Lidarr kjører under, både lese- og skrivetilgang til datakatalogen din.

## Hvordan kan jeg endre navn på artistmappene mine?

{#rename-folders}

> Den samme prosessen gjelder også for å flytte/endre artistbaner.
{.is-info}

1. Bibliotek
1. Masseredigerer
1. Velg hvilke artister som trenger navnet på mappen endret
1. Endre rotmappen til samme rotmappe som artistene allerede eksisterer i
1. Velg "Ja, flytt filer"

## Hvordan kan jeg masse-slette artister fra ønskelisten?

- Bruk Masseredigerer => Velg artistene du vil slette => Slett

## Hvorfor fungerer ikke Lidarr bak en omvendt proxy

- Lidarr bruker .NET og en ny webserver. For at SignalR skal fungere, at knappene i brukergrensesnittet skal fungere, at databaseendringer skal tas, og andre elementer. Kreves følgende tillegg til plasseringsblokken for Lidarr:
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- Pass på at du `ikke` inkluderer `proxy_set_header Connection "Upgrade";` som foreslått av nginx-dokumentasjonen. `DETTE VIL IKKE FUNGERE`
- [Se dette ASP.NET Core-problemet](https://github.com/aspnet/AspNetCore/issues/17081)
- Hvis du bruker en CDN som Cloudflare, må du sørge for at websockets er aktivert for å tillate websockets-tilkoblinger.

## Hvordan oppdaterer jeg Lidarr?

- Gå til Innstillinger og deretter fanen Generelt og vis avanserte innstillinger (bruk vippebryteren ved siden av lagre-knappen).

1. Under Oppdateringer-seksjonen endrer du grennavnet til `master` eller `develop`
1. Lagre

*Dette vil ikke installere bitene fra den grenen umiddelbart, det vil skje under neste oppdatering.*

- `master` - ![Nåværende Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Denne versjonen er testet av brukere på utviklings- og nattlige grener, og det er ikke kjent at den har noen større problemer. Denne versjonen vil motta oppdateringer omtrent månedlig. På GitHub er dette `master`-grenen.

- `develop` - ![Nåværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (Beta): Dette er kanten for testing. Utgitt etter testing i nattlige for å sikre at det ikke er umiddelbare problemer. Nye funksjoner og feilrettinger blir først utgitt her etter nattlige. Den kan betraktes som halvstabil, men er fortsatt `beta`. Denne versjonen vil motta oppdateringer enten ukentlig eller annenhver uke, avhengig av utviklingen.

> **Advarsel: Du kan kanskje ikke gå tilbake til `master` etter å ha byttet til denne grenen.** På GitHub er dette et øyeblikksbilde av `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- `nightly` - ![Nåværende Nightly/Ustabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (Alpha/Ustabil): Dette er den nyeste versjonen. Den utgis så snart koden er bekreftet og består alle automatiserte tester. Denne bygningen er kanskje ikke brukt av oss eller andre brukere ennå. Det er ingen garanti for at den vil kjøre i noen tilfeller. Denne grenen anbefales bare for avanserte brukere. Problemer og egen undersøkelse forventes i denne grenen. ***Bruk denne grenen bare hvis du vet hva du gjør og er villig til å ta i bruk for å gjenopprette en mislykket oppdatering.*** Denne versjonen oppdateres umiddelbart.

> **Advarsel: Du kan kanskje ikke gå tilbake til `master` etter å ha byttet til denne grenen.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Merk: Hvis du installerer via Docker, legg til `:release`, `:latest`, `:testing` eller `:develop` på slutten av kontainermerket, avhengig av hvem som lager byggene dine. Vær oppmerksom på at `nightly`-grenene bevisst ikke er oppført nedenfor.

|                                                                    | `master` (stabil) ![Nåværende Master/Siste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Nåværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (alpha) ![Nåværende Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### Kan jeg oppdatere Lidarr inne i Docker-kontaineren min?

- *Teknisk sett, ja.* **Men du bør absolutt ikke gjøre det.** Det er en grunnleggende filosofi i Docker. Databaseproblemer kan oppstå hvis du oppgraderer installasjonen din til den nyeste `nightly`, men deretter oppdaterer Docker-kontaineren selv (muligens nedgraderer til en eldre versjon).

### Installere en nyere versjon

#### Native

1. Gå til System og deretter fanen Oppdateringer
1. Nyere versjoner som ikke er installert ennå, vil ha en oppdateringsknapp ved siden av dem. Klikk på denne knappen for å installere oppdateringen.

#### Docker

1. Dra inn merket på nytt og oppdater kontaineren din

## Kan jeg bytte fra `nightly` tilbake til `develop`?

## Kan jeg bytte mellom grenene?

- Hvis versjonen er identisk, kan du bytte, ellers sjekk med utviklingsteamet om du kan bytte fra `nightly` til `master`; `nightly` til `develop`; eller `develop` til `master` for ditt spesifikke bygg.
- Hvis du ikke følger disse instruksjonene, kan Lidarr bli ubrukelig eller kaste feil. Du er advart
  - Den vanligste feilen er noe som `Error parsing column 45 (Language=31 - Int64)` eller andre lignende databasefeil rundt manglende kolonner eller tabeller.

## Jeg får en feilmelding: Database disk image is malformed

- **Feil som `Error creating log database` indikerer problemer med logs.db**
  - Dette kan raskt løses ved å omdøpe eller fjerne databasen. Logs-databasen inneholder uvesentlig informasjon om kommandohistorikk og oppdateringsinstallasjonshistorikk, samt Info-, Warn- og Error-oppføringer
- **Feil som `Error creating main database` eller generell `database disk image is malformed` uten spesifisert database indikerer problemer med lidarr.db**
  - Fortsett med trinnene nedenfor
- Dette betyr at SQLite-databasen som lagrer mesteparten av informasjonen for Lidarr, er ødelagt. Du har muligheten til å prøve (en) sikkerhetskopi(er), prøve å gjenopprette den eksisterende databasen, prøve å gjenopprette sikkerhetskopi(er), eller hvis alt annet mislykkes, starte på nytt med en helt ny database.
- Denne feilen kan vises hvis databasefilen ikke kan skrives av bruker/gruppe \*Arr kjører som. Tillatelsesproblemer vil sannsynligvis bare være et problem for nye installasjoner, migrerte installasjoner til en ny server, hvis du nylig har endret tillatelsene for appdata-katalogen din, eller hvis du har endret brukeren og gruppen \*Arr kjører som.
- Ditt beste og første alternativ er å [prøve å gjenopprette fra en sikkerhetskopi](#hvordan-sikkerhetskopierer-gjenoppretter-jeg-lidarr)
- Du kan også prøve å gjenopprette databasen din. Dette er vanligvis det eneste alternativet når dette problemet oppstår etter en oppdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis sqlite ikke har `.recover` eller du ønsker en mer GUI-vennlig (f.eks. Windows) måte, følg [instruksjonene våre på dette wikiet.](/useful-tools#recovering-a-corrupt-db-ui)
- En annen mulig årsak til at du får en feil med databasen din, er at du plasserer databasen på en nettverksstasjon (nfs eller smb eller noe annet som ikke er lokalt). **SQLite er designet for situasjoner der data og applikasjon eksisterer på samme maskin.** Derfor må \*Arr AppData-mappen din (/config-monteringen for Docker) være på lokal lagring. [SQLite og nettverksstasjoner fungerer ikke bra sammen og vil til slutt føre til en ødelagt database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruker mergerFS, må du fjerne `direct_io` siden SQLite bruker mmap, som ikke støttes av `direct_io`, som forklart i mergerFS [dokumentasjonen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Hvordan sikkerhetskopierer/gjenoppretter jeg Lidarr?

### Sikkerhetskopiering av Lidarr

#### Bruke innebygd sikkerhetskopi

- Gå til System => Backup i Lidarr-brukergrensesnittet
- Klikk på Sikkerhetskopier-knappen
- Last ned zip-filen etter at sikkerhetskopien er opprettet for sikkerhets skyld

#### Bruke filsystemet direkte

- Finn plasseringen av AppData-katalogen for Lidarr  
  - Gå til System => Om i Lidarr-brukergrensesnittet  
  - [Lidarr Appdata-katalog](/lidarr/appdata-directory)
- Stopp Lidarr - Dette forhindrer at databasen blir ødelagt
- Kopier innholdet til et sikkert sted

### Gjenoppretting fra sikkerhetskopi

> Gjenoppretting til et operativsystem som bruker forskjellige stier, vil ikke fungere (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows), overføring mellom OS X og Linux kan fungere, siden begge bruker stier som inneholder `/` i stedet for `\` som Windows bruker, men det støttes ikke. Du må manuelt redigere alle stier i databasen.
{.is-warning}

#### Bruke zip-sikkerhetskopi

- Installer Lidarr på nytt (hvis aktuelt / ikke allerede installert)
- Kjør Lidarr
- Gå til System => Backup
- Velg Gjenopprett sikkerhetskopi
- Velg Velg fil
- Velg sikkerhetskopien din som zip-fil
- Velg Gjenopprett

#### Bruke filsystem-sikkerhetskopi

- Installer Lidarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen av AppData-katalogen for Lidarr  
  - Kjør Lidarr én gang og gå til System => Om i brukergrensesnittet  
  - [Lidarr Appdata-katalog](/lidarr/appdata-directory)
- Stopp Lidarr
- Slett innholdet i AppData-katalogen **(inkludert .db-wal/.db-journal-filene hvis de eksisterer)**
- Gjenopprett fra sikkerhetskopien din
- Start Lidarr
- Så lenge stiene er de samme, vil alt fortsette der det slapp

#### Gjenoppretting av filsystem på Synology NAS

> ADVARSEL: Gjenoppretting på en Synology krever kunnskap om Linux og rot SSH-tilgang til Synology-enheten.
{.is-warning}

- Installer Lidarr på nytt (hvis aktuelt / ikke allerede installert)
- Finn plasseringen av AppData-katalogen for Lidarr  
  - Kjør Lidarr én gang og gå til System => Om i brukergrensesnittet  
  - [Lidarr Appdata-katalog](/lidarr/appdata-directory)
- Stopp Lidarr
- Koble til Synology NAS via SSH og logg inn som root  

> På noen installasjoner er brukeren annerledes enn kommandoene nedenfor: `chown -R sc-Lidarr:Lidarr *` {.is-info}

- Utfør følgende kommandoer:

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- Oppdater tillatelser på filene:

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- Start Lidarr

## Jeg bruker Lidarr på en Mac, og den sluttet plutselig å fungere. Hva skjedde?

- Mest sannsynlig skyldes dette en MacOS-feil som førte til at en av databasene ble ødelagt.

- Se den ovennevnte oppføringen om at databasen er ødelagt.

- Prøv deretter å starte og se om det fungerer. Hvis det ikke fungerer, trenger du ytterligere støtte. Legg ut i [subredditen vår /r/lidarr](http://reddit.com/r/lidarr) eller bli med på [discord-serveren vår](https://lidarr.audio/discord) for hjelp.

## Jeg bruker en Pi og Raspbian, og Lidarr vil ikke starte

Raspbian har en versjon av libseccomp2 som er for gammel til å støtte kjøring av en Docker-container basert på Ubuntu 20.04, som både hotio og LinuxServer bruker som sin base. Du må enten bruke `--privileged`, oppdatere libseccomp2 fra Ubuntu eller få et bedre operativsystem (Vi anbefaler Ubuntu 20.04 arm64)

**Mulig løsning:**

Fikset problemet ved å installere backport fra debian repo. Det anbefales generelt ikke å bruke backport i blankettoppgraderingsmodus. Installering av en enkelt pakke kan være ok, men kan også føre til problemer. Så du må forstå hva du gjør.

Trinn for å fikse:

Først må du forsikre deg om at du kjører Raspbian buster, for eksempel ved å bruke `lsb_release -a`

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- Hvis du bruker buster:
  - Kjør følgende for å legge til backports i kildene dine

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - Installer backporten av libseccomp2

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## Hvorfor tar det så lang tid å synkronisere lister, og kan jeg endre det?

Lister har aldri vært eller er ment å være "legg det til nå", de er verktøy for "hei, jeg vil ha dette, legg det til etter hvert".

Du kan manuelt utløse en oppdatering av en liste, skript det og utløse det via API-en, eller legge til utgivelsene direkte i Lidarr.

Denne endringen ble gjort for å unngå at serveren vår blir drept av folk som oppdaterer lister hvert 10. minutt.

## Kan jeg deaktivere oppgaven for å oppdatere utgivelser?

Nei, og du bør heller ikke gjøre det gjennom noen SQL-hacking. Oppgaven for å oppdatere utgivelser spør oppstrøms Servarr-proxyen og sjekker om metadataen for hver utgivelse (ID-er, rollebesetning, sammendrag, rangering, oversettelser, alternative titler, osv.) har blitt oppdatert sammenlignet med det som er i Lidarr for øyeblikket. Hvis det er nødvendig, vil den deretter oppdatere de aktuelle utgivelsene.

En vanlig klage er at oppgaven for oppdatering forårsaker tung I/O-bruk. En innstilling som kan forårsake problemer er "Skann artistmappe etter oppdatering". Hvis disk I/O-bruken øker under en oppdatering, kan du vurdere å endre skanneinnstillingen til `Manuell`. Ikke endre dette til `Aldri` med mindre alle endringer i biblioteket ditt (nye utgivelser, oppgraderinger, slettinger osv.) blir gjort gjennom Lidarr. Hvis du sletter utgivelsesfiler manuelt eller med et program fra tredjepart, ikke sett dette til `Aldri`.

## Hvorfor kan ikke Lidarr se filene mine på en ekstern server?

- For alle operativsystemer må du forsikre deg om at brukeren/gruppen du kjører \*Arr som har lese- og skrivetilgang til den monterte disken.
- For Linux må du forsikre deg om:
  - Hvis du bruker en NFS-montering, må `nolock` være aktivert for monteringen din.
  - Hvis du bruker en SMB-montering, må `nobrl` være aktivert for monteringen din.
- For Windows: Kort sagt, brukeren \*Arr kjører som (hvis tjeneste) eller under (hvis bakgrunnsprogram) kan ikke få tilgang til filbanen på den eksterne serveren. Dette kan skyldes forskjellige årsaker, men det vanligste er at \*Arr kjører som en tjeneste, noe som forårsaker problemene som beskrives nedenfor.

### Lidarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder

- Kjør Lidarr-tjenesten som en annen bruker som har tilgang til det området
- Åpne vinduet "Administrative verktøy" \> "Tjenester" på Windows-serveren din.
- Stopp Lidarr-tjenesten.
- Åpne dialogboksen "Egenskaper" \> "Logg på".
- Endre brukerkontoen for tjenesten til målkontoen.
- Kjør Lidarr.exe ved hjelp av oppstartsmappen

### Du bruker en kartlagt nettverksstasjon (ikke en UNC-bane)

- Endre banene dine til UNC-baner (`\\server\share`)
- Kjør Lidarr.exe via oppstartsmappen

## Hjelp, jeg har låst meg ute

{#help-i-have-forgotten-my-password}

For å deaktivere autentisering (for å tilbakestille brukernavnet eller passordet du har glemt), må du redigere `config.xml`, som vil være inne i [Lidarr Appdata-mappen](/lidarr/appdata-directory)

1. Åpne config.xml i en tekstredigerer
1. Finn linjen for autentiseringsmetode, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Endre linjen for `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Lidarr på nytt
1. Lidarr vil nå være tilgjengelig uten passord. Du bør gå til "Innstillinger: Generelt" i brukergrensesnittet og angi brukernavnet og passordet ditt

## Hvordan stopper jeg nettleseren fra å starte ved oppstart?

Avhengig av operativsystemet ditt, er det flere mulige måter.

- I "Innstillinger" => "Generelt" på noen operativsystemer er det en avmerkingsboks for å starte nettleseren ved oppstart.
- Når du starter Lidarr, kan du legge til `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumentene.
- Stopp Lidarr og rediger config.xml-filen, og endre `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Rar brukergrensesnittproblemer

- Hvis du opplever rare problemer med brukergrensesnittet, som at bibliotekssiden ikke viser noe eller at en bestemt visning eller sortering ikke fungerer, kan du prøve å se det i et Chrome Inkognitovindu eller Firefox Privat vindu. Hvis det fungerer fint der, kan du tømme nettleserens hurtigbuffer og informasjonskapsler for din spesifikke IP/domene. For mer informasjon, se artikkelen [Tøm hurtigbuffer, informasjonskapsler og lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wikien.

## VPN-er, Jackett og \*ARR-ene

- Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, er torrentklienten din vanligvis det eneste som trenger å være bak en VPN. Fordi VPN-endepunktet deles av mange brukere, kan du oppleve begrensninger i hastigheten, DDOS-beskyttelse og IP-blokkering fra ulike tjenester som hver programvare bruker.
- Med andre ord kan det å sette \*Arr-ene (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bak en VPN gjøre applikasjonene ubrukelige i noen tilfeller på grunn av at tjenestene ikke er tilgjengelige.

> **For å være tydelig, det handler ikke om hvorvidt VPN-er vil forårsake problemer med \*Arr-ene, men når: bildetilbydere vil blokkere deg, og cloudflare er foran de fleste \*Arr-servere (oppdateringer, metadata osv.) og kan også blokkere deg**
{.is-warning}

- **Mange private sporere vil utestenge deg for å bruke eller få tilgang til dem (dvs. ved å bruke Jackett eller Prowlarr) via en VPN.**

### Bruk av en VPN

- Hvis en VPN er nødvendig og Docker brukes, anbefales det å bruke Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er nødvendig og Docker ikke brukes, må VPN-klienten din ***støtte delt tunnelering, slik at bare de nødvendige (nedlastingsklient) -appene er bak VPN-en.
- Mange problemer med å få tilgang til sporere kan løses ved å bruke Googles eller Cloudflares DNS-servere i stedet for ISP-ens DNS-servere.
- I noen tilfeller (f.eks. britiske ISP-er) kan du måtte sette torrentnedlastingsklienten bak en VPN og Jackett/Prowlarr som følger:
  - Sett Jackett bak VPN-en og sørg for at delt tunnelering tillater lokal tilgang
  - For Prowlarr kan du konfigurere VPN-klienten din til å gi en proxy og legge til proxyen i Innstillinger => Indekser. Gi proxyen en tagg, og gi de indekser som trenger å bruke den samme taggen.
    - Hvis det absolutt er nødvendig, og hvis VPN-en din ikke gir en måte å opprette en proxy på, kan du sette Prowlarr bak VPN-en og sørge for at delt tunnelering tillater lokal tilgang.

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nødvendig å legge til hver tracker individuelt. Alternativt kan du vurdere å prøve ut Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)
- **Oppdatering april 2022: Støtten for \*Arr er fjernet for jackett `/all` på grunn av at det bare forårsaker problemer.**
- Jackett /all-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nå nødvendig å legge til hver tracker individuelt.
- [Selv Jacketts utviklere sier at det bør unngås og ikke brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Bruk av /all-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over innstillingene for hver enkelt indekser (kategorier, søkemåter, osv.)
  - blanding av søkemåter (IMDB, søk, osv.) kan føre til dårlige resultater
  - indeksspesifikke kategorier (\>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned det generelle resultatet
  - totalt antall resultater er begrenset til 1000
  - hvis en av trackerne i /all returnerer en feil, vil \*Arr deaktivere den, og nå får du ingen resultater.

### Løsninger for Jackett /All

- Legg til hver tracker i Jackett manuelt som en indekser i \*Arr
- Sjekk ut [Prowlarr](/prowlarr), som kan synkronisere indekser til \*Arr og er utviklet av Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekser til \*Arr. Men ikke bruk deres enkeltstående aggregerte endepunkt, bruk `multi` hvis synkroniseringen skal brukes.

## Hvorfor er det to filer? | Hvorfor er det en fil igjen i nedlastinger?

Dette er forventet. Med en konfigurasjon som støtter [hardlinker](https://trash-guides.info/hardlinks), vil ikke dobbelt plass bli brukt. Her er hvordan torrentprosessen fungerer.

1. Lidarr sender en nedlastingsforespørsel til klienten din og assosierer den med etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: filmer, tv, serier, musikk, osv.
1. Lidarr overvåker de aktive nedlastingene i nedlastingsklienten din som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
1. Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forholdet eller tiden kan justeres i nedlastingsklienten eller fra innenfor under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil de bli hardlinket hvis det støttes av oppsettet ditt, eller kopiert hvis hardlinker ikke støttes.
1. Hvis alternativet "Behandling av fullførte nedlastinger - Fjern fullførte" er aktivert i Lidarrs innstillinger, vil Lidarr slette den opprinnelige filen og torrenten fra nedlastingsklienten din, men bare hvis nedlastingsklienten rapporterer at seeding er fullført og torrenten er stoppet (dvs. satt på pause). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for hvordan du konfigurerer nedlastingsklienten din optimalt.

> Hardlinker er aktivert som standard. [En hardlink vil ikke bruke ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for den fullførte nedlastingsmappen og mediebiblioteket ditt. Hvis opprettelsen av hardlinken mislykkes eller oppsettet ditt ikke støtter hardlinker, vil den falle tilbake og kopiere filen.
{.is-info}

## Jeg får stadig advarsler fra skytjenesten min om API-grenser

Lidarr er ikke som de andre Arr-ene. Den bruker koder i stedet for filnavn for å fungere. Hvis du lagrer Lidarr-filer på skytjenesten, må den laste ned filen for å lese kodene. Dette vil veldig raskt overstige eventuelle API-grenser du har hos tjenesteleverandøren din. Vi fraråder sterkt å lagre Lidarr-biblioteket ditt på en skytjenesteleverandør, og eventuelle problemer du opplever skyldes sannsynligvis den oppsettet.