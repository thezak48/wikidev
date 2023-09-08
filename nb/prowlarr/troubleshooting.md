---
title: Prowlarr Feilsøking
description: 
published: true
date: 2023-08-20T00:20:04.841Z
tags: prowlarr, feilsøking
editor: markdown
dateCreated: 2021-06-20T20:05:25.223Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Be om hjelp](#be-om-hjelp)
- [Logging og loggfiler](#logging-og-loggfiler)
  - [Standard plassering for logger](#standard-plassering-for-logger)
  - [Plassering for oppdateringslogger](#plassering-for-oppdateringslogger)
  - [Deling av logger](#deling-av-logger)
  - [Sporings-/feilsøkingslogger](#sporingsfeilsøkingslogger)
  - [Tømme logger](#tømme-logger)
- [Flere loggfiler](#flere-loggfiler)
- [Gjenopprette etter en mislykket oppdatering](#gjenopprette-etter-en-mislykket-oppdatering)
  - [Fastslå problemet](#fastslå-problemet)
    - [Migreringsproblem](#migreringsproblem)
    - [Tillatelsesproblem](#tillatelsesproblem)
  - [Løse problemet](#løse-problemet)
    - [Tillatelsesproblemer](#tillatelsesproblemer)
    - [Manuell oppgradering](#manuell-oppgradering)
- [NGINX-feil](#nginx-feil)
- [Problemer med indekser, applikasjoner og nedlastingsklienter](#problemer-med-indekser-applikasjoner-og-nedlastingsklienter)
  - [Kan ikke bestemme rammestørrelsen eller mottok en korrupt ramme](#kan-ikke-bestemme-rammestørrelsen-eller-mottok-en-korrupt-ramme)
  - [Tilkobling tidsavbrutt](#tilkobling-tidsavbrutt)
  - [Sonarr HTTP 404-feil](#sonarr-http-404-feil)
  - [\*Arr HTTP 400-feil](#arr-http-400-feil)
  - [503 HTTP-tjenesten er utilgjengelig](#503-http-tjenesten-er-utilgjengelig)
  - [Ugyldige torrents](#ugyldige-torrents)
  - [Søk og indekser](#søk-og-indekser)

# Be om hjelp

Trenger du hjelp? Det er greit, alle trenger hjelp av og til. Du kan få hjelp i sanntid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Offisiell Prowlarr Discord*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offisiell Prowlarr Subreddit*](https://reddit.com/r/prowlarr)
{.links-list}

Men før du går dit og legger ut en melding, må du sørge for at forespørselen om hjelp er så god som mulig. Beskriv tydelig problemet og gi en kort beskrivelse av oppsettet ditt, inkludert ting som operativsystem/distribusjon, versjon av .NET, versjon av Prowlarr, nedlastingsklient og dens versjon. **Hvis du bruker [Docker](https://www.docker.com/), kjør gjennom [Docker Guide](/docker-guide) først, da dette vil løse vanlige og hyppige problemer med stier/tillatelser. Ellers ha en [docker compose](/docker-guide#docker-compose) klar. [Slik genererer du en Docker Compose](https://trash-guides.info/compose)** Fortell oss om hva du allerede har prøvd, hva du har sett på. Bruk [Logging og loggfiler](#logging-og-loggfiler) for å øke loggingen til sporingsnivå, gjenskap problemet, legg ut relevant kontekst på en pastebin og inkluder en lenke til den i innlegget ditt. Kanskje til og med inkluder noen skjermbilder for å markere problemet.

Jo mer vi vet, desto enklere er det å hjelpe deg.

# Logging og loggfiler

Det kan være nyttig å også se gjennom [Vanlige problemer med indekser, applikasjoner og nedlastingsklienter](#problemer-med-indekser-applikasjoner-og-nedlastingsklienter).

> Hvis du blir bedt om å gi indekssvaret for utvikling eller feilsøking, kan du fortsette å lese denne blå seksjonen...ellers fortsett til trinnene nedenfor. Når du feilsøker indekssvar, kan det være nyttig å gå til `settings/development` (skjult side) i Prowlarr og midlertidig aktivere forbedret indekssporing for å logge indekssvaret. Det bør ikke være aktivert hele tiden
{.is-info}

Hvis du blir bedt om feilsøkingslogger, vil loggene dine inneholde `debug`, og hvis du blir bedt om sporingslogger, vil loggene dine inneholde `trace`. Hvis loggene du gir ikke inneholder noen av disse, er de ikke de etterspurte loggene.

- Unngå å dele hele loggfilen med mindre du blir bedt om det.
- Ikke last opp logger direkte til Discord eller lim dem inn som tekstvegger, med mindre du blir bedt om det.
- Ikke del loggene som vedlegg, som en zip-fil eller noe annet enn tekst som deles via tjenestene som er nevnt nedenfor

For å gi gode og nyttige logger for deling:

> Sørg for at det ikke kjører noen spamoppgave, for eksempel en RSS-oppdatering
{.is-warning}

1. [Øk loggingen til sporingsnivå (Innstillinger => Generelt => Loggnivå eller rediger konfigurasjonsfilen)](#sporingsfeilsøkingslogger)
2. [Tøm logger (System => Logger => Tøm logger eller slett alle loggene i logg-mappen)](#tømme-logger)
3. Gjenskap problemet (Gjør det som ødelegger ting på nytt)
4. [Åpne sporingsloggfilen (Lidarr.trace.txt) via brukergrensesnittet eller loggfilen](#standard-plassering-for-logger) på filsystemet og finn relevant kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del etter problemet.
6. Bruk [Gist](https://gist.github.com/), [0bin (**Sørg for å deaktivere fargelegging**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) eller lignende nettsteder - unntatt de som er nevnt nedenfor - for å dele de kopierte loggene fra ovenfor

**Advarsler:**
- **Ikke bruk [pastebin.com](https://pastebin.com), da filtrene deres har en tendens til å blokkere loggene.
- Ikke bruk [pastebin.pl](https://pastebin.pl), da nettstedet deres ofte ikke er tilgjengelig.
- Ikke bruk [JustPasteIt](https://justpaste.it/), da nettstedet deres ikke legger til rette for gjennomgang av logger.
- Ikke last opp loggen din som en fil.
- Ikke last opp og del loggene dine via Google Drive, Dropbox eller noen andre nettsteder som ikke er nevnt ovenfor.
- Ikke arkiver (zip, tar (tarball), 7zip, osv.) loggene dine.
- Ikke del konsollutdata, utdata fra Docker-container eller noe annet enn de spesifiserte applikasjonsloggene

**Viktig merknad:**
- Når du bruker [0bin](https://0bin.net/), må du deaktivere fargelegging og ikke brenne etter lesing.

- Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men ikke er sikker på hvilken du kan bruke N++. Du kan bruke Notepad++ "Søk i filer"-funksjonen for å søke i gamle loggfiler etter behov.
- **Bare Unix:** Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men ikke er sikker på hvilken du kan bruke grep. Hvis du for eksempel vil finne informasjon om film/serie/bok/sang/indeks "Shooter", kan du kjøre følgende kommando `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Hvis [Appdata-katalogen](/prowlarr/appdata-directory) din er i hjemmemappen, kjører du: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggene har følgende funksjoner
    * -i: ignorere store/små bokstaver
    * -n: vis linjenummer
    *  -r: sjekk rekursivt alle filer i banen
    * -C: gi antall linjer før og etter linjen den finnes på
    * -e: mønsteret å søke etter

```

## Standard plassering for logger

Loggfilene ligger i Prowlarrs [Appdata-katalog](/prowlarr/appdata-directory), inne i logs/-mappen. Du kan også få tilgang til loggfilene fra brukergrensesnittet ved System => Logger => Filer.

> Merk: Logg-tabellen ("Hendelser") i brukergrensesnittet er ikke det samme som loggfilene og er ikke like nyttig. Hvis du blir bedt om logger, kopier/lim inn fra loggfilene og ikke tabellen.
{.is-info}

## Plassering for oppdateringslogger

Oppdateringsloggfilene ligger i Prowlarrs [Appdata-katalog](/prowlarr/appdata-directory), inne i UpdateLogs/-mappen.

## Deling av logger

Loggene kan være lange og vanskelige å lese som en del av et forum- eller Reddit-innlegg, og de er spamaktige i Discord, så bruk [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller lignende pastebin-nettsteder. Hele filen er vanligvis ikke nødvendig, bare en god mengde kontekst fra før og etter problemet/feilen. Ikke glem å vente på at spamoppgaver som en RSS-synkronisering eller biblioteksoppdatering skal fullføres.

## Sporings-/feilsøkingslogger

Du kan endre loggnivået på Innstillinger => Generelt => Logging. Prowlarr trenger ikke å startes på nytt for at endringen skal tre i kraft. De nyeste debug-/sporingsloggfilene har navnene `prowlarr.debug.txt` og `prowlarr.trace.txt` henholdsvis.

Hvis du ikke kan få tilgang til brukergrensesnittet for å angi loggnivået, kan du gjøre det ved å redigere config.xml i AppData-katalogen ved å angi LogLevel-verdien til Debug eller Trace i stedet for Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Tømme logger

Du kan tømme loggfilene og loggdatabasen direkte fra brukergrensesnittet, under `System` => `Logger` => `Filer` og `System` => `Logger` => `Slett` (søppelbøtteikon).

# Flere loggfiler

Prowlarr bruker rullerende loggfiler begrenset til 1 MB hver. Den nåværende loggfilen er alltid Prowlarr.txt, for de andre filene er Prowlarr.0.txt den nest nyeste (jo høyere nummer, jo eldre er den). Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.

Når Debug-loggnivået er aktivert, vil det være tilgjengelige ekstra `prowlarr.debug.txt` rullerende loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. Den dekker vanligvis en periode på 40 timer.

Når Trace-loggnivået er aktivert, vil det være tilgjengelige ekstra `prowlarr.trace.txt` rullerende loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsnøyaktighet dekker den bare et par timer, og noen ganger mindre enn ett minutt hvis du gjør noe intensivt.

# Gjenopprette etter en mislykket oppdatering

Vi gjør alt vi kan for å forhindre problemer ved oppgradering, men hvis de oppstår, vil dette veilede deg gjennom trinnene du må ta for å gjenopprette installasjonen din.

## Fastslå problemet

- Det beste stedet å se når programmet ikke starter etter en oppdatering, er å se gjennom [oppdateringsloggene](#plassering-for-oppdateringslogger) og se om oppdateringen ble fullført uten problemer. Hvis det ikke er noen problemer der, er neste trinn å se på de vanlige programloggfilene dine. Før du prøver å starte på nytt, bruk [Logging](/prowlarr/settings#logging) og [Loggfiler](/prowlarr/system#log-files) for å finne dem og øke loggnivået.
- Det mest vanlige problemet er at systemet der appen er installert, har rotet til med `/tmp`-katalogen og slettet kritiske \*Arr-filer under oppgraderingen, noe som forårsaker at både oppgraderingen og tilbakerulling mislykkes. I dette tilfellet installerer du bare på nytt over den eksisterende ødelagte installasjonen.

### Migreringsproblem

- Migreringsfeil vil ikke være identiske, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Tillatelsesproblem

- Tillatelsesproblemer skyldes at applikasjonen ikke kan få tilgang til de relevante midlertidige mappene og/eller appens binærmappe. Fiks tillatelsene slik at brukeren/gruppen applikasjonen kjører som, har riktig tilgang.

- Synology-brukere kan oppleve denne Synology-feilen `Access to the path '/proc/{noen tall}/maps is denied`

- Synology-brukere kan også oppleve at det er tomt for plass i `/tmp` på visse NAS-er. Du må angi en annen `/tmp`-bane for appen. Se SynoCommunity eller andre Synology-støttekanaler for hjelp med dette.

## Løse problemet

Hvis det oppstår et migreringsproblem, er det ikke mye du kan gjøre umiddelbart. Hvis problemet gjelder deg spesifikt (eller det ikke er noen innlegg ennå), kan du opprette et innlegg på [subredditen vår](https://reddit.com/r/prowlarr) eller besøke [discorden vår](https://prowlarr.com/discord). Hvis det er andre med samme problem, kan du være trygg på at vi jobber med det.

> Sørg for at du ikke prøvde å bruke en database fra `nightly`-versjonen på den stabile versjonen. Å bytte mellom grener er ikke anbefalt.{.is-info}

### Tillatelsesproblemer

- Fiks tillatelsene slik at brukeren/gruppen applikasjonen kjører som, kan få tilgang (lese og skrive) til både `/tmp` og installasjonsmappen til applikasjonen.

- For Synology-brukere som opplever problemer med `/proc/###/maps` vil stoppe Sonarr eller de andre \*Arr-applikasjonene og oppdatere løse dette. Dette er et problem med SynoCommunity-pakken.

### Manuell oppgradering

Last ned den nyeste utgivelsen fra nettstedet vårt.

Installer oppdateringen (.exe) eller pakk ut innholdet (.zip) over den eksisterende installasjonen og kjør Prowlarr som du pleier.

# NGINX-feil

I Prowlarr-oppsettet ditt trenger du denne linjen:

`proxy_set_header Host $host;`

Hvis du har en annen `proxy_set_header`, må du erstatte den med linjen ovenfor.

# Problemer med indekser, applikasjoner og nedlastingsklienter

- På et grunnleggende nivå må Prowlarr kunne kommunisere med indeksene dine.
- Hvis du bruker applikasjonssynkronisering, må Prowlarr også kunne kommunisere med applikasjonene dine, og applikasjonene må kunne kommunisere med Prowlarr.
- Hvis du har en nedlastingsklient i Prowlarr for manuelle nedlastinger i Prowlarr, må Prowlarr kunne kommunisere med nedlastingsklienten din.

> Merk at logger som indikerer spørring av indekser-ID 0: ID 0 er en generisk testendepunkt som lar oss teste om \*Arr kan ringe tilbake og koble til Prowlarr uten å faktisk stole på at en indekser fungerer.
{.is-info}

Her er noen vanlige årsaker

## Kan ikke bestemme rammestørrelsen eller mottok en korrupt ramme

`Cannot determine the frame size or a corrupted frame was received.`

Prowlarr hadde et sikkerhetsproblem med å koble til nettstedet.

Dette skyldes vanligvis:

- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør

## Tilkobling tidsavbrutt

`The request timed out`

Prowlarr får ingen respons fra klienten. [Se vår generelle nettverks- og tillatelsesfeilsøkingsguide](/permissions-and-networking)

Dette skyldes vanligvis:

- feil konfigurert eller bruk av en VPN
- feil konfigurert eller bruk av en proxy
- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy

## Sonarr HTTP 404-feil

- Dette skyldes vanligvis at du kjører en utdatert (EOL) versjon av Sonarr som ikke har v3 API-endepunktene
- Prowlarr støtter ikke Sonarr v2
- Prowlarr støtter bare Sonarr v3

## \*Arr HTTP 400-feil

- Se denne FAQ-posten: [Prowlarr vil ikke synkronisere X-indeks med appen](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 HTTP-tjenesten er utilgjengelig

- Dette skyldes vanligvis at sporingen din blokkerer deg via Cloudflare og krever [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)

## Ugyldige torrents

- Prøv å laste ned lenken via URL-en og variablene Prowlarr brukte.
- Prøv å laste ned torrenten via prowlarr (dvs. bruk lenken prowlarr-appen brukte for å hente filen).
- Sørg for at informasjonskapselen eller andre påloggingsopplysninger for indekseren din ikke er utløpt og er gyldige.
- Hvis problemet skyldes Prowlarr, vennligst rapporter en feil.

## Søk, indekser og trackere

- [Lidarr Søk og indekser](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Radarr Søk og indekser](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Readarr Søk og indekser](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Sonarr Søk og indekser](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}