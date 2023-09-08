---
title: Sonarr Feilsøking
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, feilsøking
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Be om hjelp](#be-om-hjelp)
- [Logging og loggfiler](#logging-og-loggfiler)
  - [Standard plassering for logger](#standard-plassering-for-logger)
  - [Plassering for oppdateringslogger](#plassering-for-oppdateringslogger)
  - [Deling av logger](#deling-av-logger)
  - [Sporings-/feilsøkingslogger](#sporingsfeilsøkingslogger)
  - [Slette logger](#slette-logger)
- [Flere loggfiler](#flere-loggfiler)
- [Gjenopprette etter mislykket oppdatering](#gjenopprette-etter-mislykket-oppdatering)
  - [Fastslå problemet](#fastslå-problemet)
    - [Migreringsproblem](#migreringsproblem)
    - [Tillatelsesproblem](#tillatelsesproblem)
  - [Løse problemet](#løse-problemet)
    - [Tillatelsesproblemer](#tillatelsesproblemer)
    - [Manuell oppgradering](#manuell-oppgradering)
- [Nedlastinger og importering](#nedlastinger-og-importering)
  - [Test nedlastingsklienten](#test-nedlastingsklienten)
  - [Test en nedlasting](#test-en-nedlasting)
  - [Test en importering](#test-en-importering)
  - [Vanlige problemer](#vanlige-problemer)
    - [En eller flere forventede episoder i utgivelsen ble ikke importert eller mangler](#en-eller-flere-forventede-episoder-i-utgivelsen-ble-ikke-importert-eller-mangler)
    - [Bruker Sonarr v2](#bruker-sonarr-v2)
    - [Nettlesergrensesnittet til nedlastingsklienten er ikke aktivert](#nettlesergrensesnittet-til-nedlastingsklienten-er-ikke-aktivert)
    - [SSL i bruk og feil konfigurert](#ssl-i-bruk-og-feil-konfigurert)
    - [Kan ikke se delte ressurser på Windows](#kan-ikke-se-delte-ressurser-på-windows)
    - [Kartlagte nettverksstasjoner er ikke pålitelige](#kartlagte-nettverksstasjoner-er-ikke-pålitelige)
    - [Docker og bruker, gruppe, eierskap, tillatelser og stier](#docker-og-bruker-gruppe-eierskap-tillatelser-og-stier)
    - [Ekstern stiavbildning](#ekstern-stiavbildning)
      - [Ekstern montering eller ekstern synkronisering (Syncthing)](#ekstern-montering-eller-ekstern-synkronisering-syncthing)
    - [Tillatelser for biblioteksmappen](#tillatelser-for-biblioteksmappen)
    - [Tillatelser for nedlastingsmappen](#tillatelser-for-nedlastingsmappen)
    - [Nedlastingsmappen og biblioteksmappen er ikke forskjellige mapper](#nedlastingsmappen-og-biblioteksmappen-er-ikke-forskjellige-mapper)
    - [Feil kategori](#feil-kategori)
    - [Pakkede torrents](#pakkede-torrents)
    - [Gjentatte nedlastinger](#gjentatte-nedlastinger)
    - [Usenet-nedlasting savner importering](#usenet-nedlasting-savner-importering)
    - [Nedlastingsklienten fjerner elementer](#nedlastingsklienten-fjerner-elementer)
    - [Nedlastingen kan ikke matches med et bibliotekselement](#nedlastingen-kan-ikke-matches-med-et-bibliotekselement)
      - [Fant tilsvarende serie via grab-historikk, men serien ble matchet etter serie-ID. Automatisk importering er ikke mulig](#fant-tilsvarende-serie-via-grab-historikk-men-serien-ble-matchet-etter-serie-id-automatisk-importering-er-ikke-mulig)
    - [Episodenavn er TBA](#episodenavn-er-tba)
    - [Tilkobling tidsavbrutt](#tilkobling-tidsavbrutt)
  - [Problem som ikke er oppført](#problem-som-ikke-er-oppført)
- [Søk, indekser og sporere](#søk-indekser-og-sporere)
  - [Øke loggingen til sporingsnivå](#øke-loggingen-til-sporingsnivå)
  - [Test en indekser eller sporingsnettsted](#test-en-indekser-eller-sporingsnettsted)
  - [Test et søk](#test-et-søk)
  - [Vanlige problemer](#vanlige-problemer-1)
    - [Indekser blir ikke søkt](#indekser-blir-ikke-søkt)
    - [Dårlig navngitte utgivelser](#dårlig-navngitte-utgivelser)
    - [Sporingsnettsted trenger RawSearch-funksjoner](#sporingsnettsted-trenger-rawsearch-funksjoner)
    - [Serien trenger et alias](#serien-trenger-et-alias)
    - [Serien trenger en XEM-avbildning](#serien-trenger-en-xem-avbildning)
    - [Feil serietype](#feil-serietype)
      - [Daglig](#daglig)
      - [Standard](#standard)
      - [Anime](#anime)
    - [Mediet er ikke overvåket](#mediet-er-ikke-overvåket)
    - [Søk vellykket - ingen resultater returnert](#søk-vellykket-ingen-resultater-returnert)
    - [Feil kategorier](#feil-kategorier)
    - [Feil resultater](#feil-resultater)
    - [Manglende resultater](#manglende-resultater)
    - [Sertifikatvalidering](#sertifikatvalidering)
    - [Treffer rategrenser](#treffer-rategrenser)
    - [IP-blokkering](#ip-blokkering)
    - [Bruk av Jackett /all-endepunktet](#bruk-av-jackett-all-endepunktet)
    - [Bruk av NZBHydra2 som enkeltinngang](#bruk-av-nzbhydra2-som-enkeltinngang)
    - [Indekser blir ikke søkt](#indekser-blir-ikke-søkt-1)
    - [Jackett-manuelt søk finner flere resultater](#jackett-manuelt-søk-finner-flere-resultater)
    - [Releaseprofiler blir ikke respektert](#releaseprofiler-blir-ikke-respektert)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-1)
  - [Feil](#feil)
    - [Forbindelsen ble lukket: En uventet feil oppstod under sending](#forbindelsen-ble-lukket-en-uventet-feil-oppstod-under-sending)
    - [Forespørselen tidsavbrutt](#forespørselen-tidsavbrutt)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-2)

# Be om hjelp

Trenger du hjelp? Det er greit, alle trenger hjelp av og til. Du kan få hjelp i sanntid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Offisiell Sonarr Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offisiell Sonarr Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

Men før du går dit og poster, må du sørge for at forespørselen om hjelp er så god som mulig. Beskriv tydelig problemet og gi en kort beskrivelse av oppsettet ditt, inkludert ting som operativsystem/distribusjon, versjon av .net/Mono, versjon av Sonarr, nedlastingsklient og dens versjon. **Hvis du bruker [Docker](https://www.docker.com/), kan du kjøre gjennom [Docker Guide](/docker-guide) først, da dette vil løse vanlige og hyppige problemer med stier/tillatelser. Ellers må du ha en [docker compose](/docker-guide#docker-compose) klar. [Slik genererer du en Docker Compose](https://trash-guides.info/compose)**. Fortell oss hva du allerede har prøvd, hva du har sett på. Bruk [Logging og loggfiler](#logging-og-loggfiler) for å øke loggingen til sporingsnivå, gjenskap problemet, legg ut relevant kontekst på en pastebin og inkluder en lenke til den i innlegget ditt. Du kan til og med inkludere noen skjermbilder for å fremheve problemet.

Jo mer vi vet, desto enklere er det å hjelpe deg.

# Logging og loggfiler

Det kan være nyttig å også se gjennom vanlige feilsøkingsproblemer:
- [Vanlige problemer med nedlastinger og importering](#vanlige-problemer)
- [Vanlige problemer med søk i indekser og sporere](#vanlige-problemer-1)
{.links-list}

Hvis du blir bedt om feilsøkingslogger, vil loggene dine inneholde `debug`, og hvis du blir bedt om sporingslogger, vil loggene dine inneholde `trace`. Hvis loggene du gir ikke inneholder noen av disse, er de ikke de loggene som blir bedt om.

- Unngå å dele hele loggfilen med mindre du blir bedt om det.
- Ikke last opp logger direkte til Discord eller lim dem inn som tekstblokker, med mindre du blir bedt om det.
- Ikke del loggene som vedlegg, zip-arkiv eller noe annet enn tekst som deles via tjenestene som er nevnt nedenfor.

For å gi gode og nyttige logger for deling:

> Sørg for at en spamaktig oppgave IKKE kjører, for eksempel en RSS-oppdatering
{.is-warning}

1. [Øk loggingen til sporingsnivå (Innstillinger => Generelt => Loggnivå eller rediger konfigurasjonsfilen)](#sporingsfeilsøkingslogger)
2. [Slett logger (System => Logger => Slett logger eller slett alle loggene i logg-mappen)](#slette-logger)
3. Gjenskap problemet (Gjør det som ødelegger ting på nytt)
4. [Åpne sporingsloggfilen (sonarr.trace.txt) via brukergrensesnittet eller loggfilen](#standard-plassering-for-logger) på filsystemet og finn relevant kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del etter problemet.
6. Bruk [Gist](https://gist.github.com/), [0bin (**Sørg for å deaktivere fargelegging**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) eller lignende nettsteder - unntatt de som er nevnt nedenfor - for å dele de kopierte loggene ovenfor

**Advarsler:**
- **Ikke bruk [pastebin.com](https://pastebin.com), da filtrene deres har en tendens til å blokkere loggene.
- Ikke bruk [pastebin.pl](https://pastebin.pl), da nettstedet deres ofte ikke er tilgjengelig.
- Ikke bruk [JustPasteIt](https://justpaste.it/), da nettstedet deres ikke legger til rette for gjennomgang av logger.
- Ikke last opp loggen din som en fil.
- Ikke last opp og del loggene dine via Google Drive, Dropbox eller noen andre nettsteder som ikke er nevnt ovenfor.
- Ikke arkiver (zip, tar (tarball), 7zip, osv.) loggene dine.
- Ikke del konsollutdata, utdata fra Docker-container eller noe annet enn de spesifiserte programloggfilene

**Viktig merknad:**
- Når du bruker [0bin](https://0bin.net/), må du sørge for å deaktivere fargelegging og ikke brenne etter lesing.

- Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men er usikker på hvilken du kan bruke N++. Du kan bruke Notepad++-funksjonen "Søk i filer" for å søke i gamle loggfiler etter behov.
- **Bare Unix:** Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men er usikker på hvilken du kan bruke grep. Hvis du for eksempel vil finne informasjon om filmen/serien/boken/sangen/indekseren "Shooter", kan du kjøre følgende kommando: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Hvis [Appdata-mappen](/sonarr/appdata-directory) din er i hjemmemappen, kjører du: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggene har følgende funksjoner
    * -i: ignorere store/små bokstaver
    * -n: vis linjenummer
    * -r: søk rekursivt i alle filer i banen
    * -C: vis # linjer før og etter linjen den finnes på
    * -e: mønsteret å søke etter

```

## Standard plassering for logger

Loggfilene er plassert i Sonarrs [Appdata-mappen](/sonarr/appdata-directory), inne i mappen logs/. Du kan også få tilgang til loggfilene fra brukergrensesnittet ved å gå til System => Logger => Filer.

> Merk: Logg-tabellen ("Hendelser") i brukergrensesnittet er ikke det samme som loggfilene og er ikke like nyttig. Hvis du blir bedt om logger, kopier/lim inn fra loggfilene og ikke tabellen.
{.is-info}

## Plassering for oppdateringslogger

Oppdateringsloggfilene er plassert i Sonarrs [Appdata-mappen](/sonarr/appdata-directory), inne i mappen UpdateLogs/.

## Deling av logger

Loggene kan være lange og vanskelige å lese som en del av et forum- eller Reddit-innlegg, og de er spamaktige i Discord, så bruk [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller lignende pastebin-nettsteder. Hele filen er vanligvis ikke nødvendig, bare en god mengde kontekst fra før og etter problemet/feilen. Ikke glem å vente til spamaktige oppgaver som en RSS-synkronisering eller biblioteksoppdatering er ferdige.

## Sporings-/feilsøkingslogger

Du kan endre loggnivået på Innstillinger => Generelt => Logging. Sonarr trenger ikke å startes på nytt for at endringen skal tre i kraft. De nyeste debug-/sporingsloggfilene har navnene `sonarr.debug.txt` og `sonarr.trace.txt` henholdsvis.

Hvis du ikke har tilgang til brukergrensesnittet for å angi loggnivået, kan du gjøre det ved å redigere config.xml i AppData-mappen ved å angi LogLevel-verdien til Debug eller Trace i stedet for Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Slette logger

Du kan slette loggfilene og loggdatabasen direkte fra brukergrensesnittet, under System => Logger => Filer og System => Logger => Slett (Søppelbøtteikon)

# Flere loggfiler

Sonarr bruker rullerende loggfiler som er begrenset til 1 MB hver. Den nåværende loggfilen er alltid `sonarr.txt`, for de andre filene er `sonarr.0.txt` den nest nyeste (jo høyere nummer, jo eldre er den). Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.

Når feilsøkingsloggnivået er aktivert, vil det være tilgjengelige ekstra rullerende loggfiler for `sonarr.debug.txt`. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. De dekker vanligvis en periode på 40 timer.

Når sporingsloggnivået er aktivert, vil det være tilgjengelige ekstra rullerende loggfiler for `sonarr.trace.txt`. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsloggenes omfang dekker de vanligvis bare et par timer.

# Gjenopprette etter mislykket oppdatering

Vi gjør alt vi kan for å forhindre problemer ved oppgradering, men hvis de likevel oppstår, vil dette veilede deg gjennom trinnene du må ta for å gjenopprette installasjonen din.

## Fastslå problemet

Det beste stedet å se når programmet ikke starter etter en oppdatering, er å se gjennom [oppdateringsloggene](#plassering-for-oppdateringslogger) og se om oppdateringen ble fullført uten problemer. Hvis det ikke er noen problemer der, er neste steg å se på de vanlige programloggfilene dine. Før du prøver å starte på nytt, bruk [Logging](/sonarr/settings#logging) og [Loggfiler](/sonarr/system#loggfiler) for å finne dem og øke loggnivået.

### Migreringsproblem

- Migreringsfeil vil ikke være identiske, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Tillatelsesproblem

- Tillatelsesproblemer skyldes at programmet ikke får tilgang til de relevante midlertidige mappene og/eller appens binærmappe. Løs tillatelsesproblemene slik at brukeren/gruppen som programmet kjører som, har riktig tilgang.

- Synology-brukere kan oppleve denne Synology-feilen `Tilgang til banen '/proc/{noen tall}/maps er nektet`

- Synology-brukere kan også oppleve å være tom for plass i `/tmp` på visse NAS-er. Du må angi en annen `/tmp`-bane for appen. Se SynoCommunity eller andre Synology-støttekanaler for hjelp med dette.

## Løse problemet

Hvis det oppstår et migrasjonsproblem, er det ikke mye du kan gjøre umiddelbart. Hvis problemet er spesifikt for deg (eller det ikke er noen innlegg ennå), kan du opprette et innlegg på [subredditen vår](https://reddit.com/r/sonarr) eller besøke [discorden vår](https://discord.sonarr.tv/). Hvis det er andre med samme problem, kan du være trygg på at vi jobber med det.

> Forsikre deg om at du ikke prøvde å bruke en database fra `develop`-versjonen på den stabile versjonen. Å bytte mellom grener er ikke anbefalt.{.is-info}

### Tillatelsesproblemer

- Fiks tillatelsene for å sikre at bruker/gruppe som applikasjonen kjører som, har tilgang (lese- og skrivetilgang) til både `/tmp` og installasjonsmappen til applikasjonen.

- For Synology-brukere som opplever problemer med `/proc/###/maps` som stopper Sonarr eller de andre \*Arr-applikasjonene og oppdatering bør løse dette. Dette er et problem med SynoCommunity-pakken.

### Manuell oppgradering

Last ned den nyeste utgivelsen fra nettstedet vårt.

Installer oppdateringen (.exe) eller pakk ut innholdet (.zip) over den eksisterende installasjonen og kjør Sonarr på vanlig måte.

# Nedlastinger og importering

Nedlasting og importering er der *de fleste* opplever problemer. Fra et overordnet perspektiv må Sonarr kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det er et stort utvalg av støttede nedlastingsklienter og en enda *større* variasjon av oppsett. Dette betyr at selv om det er noen *vanlige* oppsett, er det ikke ett *riktig* oppsett, og alle oppsett kan være litt forskjellige.

> **Det første trinnet er å øke loggingen til Trace, se [Logging og loggfiler](#logging-og-loggfiler) for detaljer om hvordan du justerer loggingen og søker i loggene. Du vil deretter gjenskape problemet og bruke loggene på trace-nivå fra den tidsrammen til å undersøke problemet.**
> Hvis noen hjelper deg, legg kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem.
> Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet mens oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

Når du ber om hjelp, må du sørge for å lese [spørre om hjelp](#spørre-om-hjelp) slik at du kan gi oss de detaljene vi trenger.

## Teste nedlastingsklienten

Sørg for at nedlastingsklienten(e) dine kjører. Begynn med å teste nedlastingsklienten. Hvis det ikke fungerer, kan du se detaljer i loggene på trace-nivå. Du bør finne en URL du kan sette inn i nettleseren din og se om den fungerer. Det kan være et tilkoblingsproblem, som kan indikere feil IP-adresse, vertsnavn, port eller til og med en brannmur som blokkerer tilgangen. Det kan være åpenbart, som et autentiseringsproblem der du har skrevet feil brukernavn, passord eller API-nøkkel.

## Teste en nedlasting

Nå skal vi prøve en nedlasting. Velg en episode for en serie og gjør et manuelt søk. Velg en av disse filene og prøv å laste den ned. Blir den sendt til nedlastingsklienten? Havner den i riktig kategori? Vises den i Aktivitet? Havner den i loggene på trace-nivå under oppgavene **Sjekk for ferdig nedlasting** (Oppdater overvåkede nedlastinger og Behandle overvåkede nedlastinger) som kjører omtrent hvert minutt? Blir den riktig analysert under den oppgaven? Har den ventende nedlastingen et fornuftig navn? Siden søkene er basert på ID på noen indekserings-/sporingstjenester, kan den sette opp en nedlasting med et navn den ikke kan gjenkjenne.

## Teste en importering

Importproblemer bør nesten alltid vises som et element i Aktivitet med et oransje ikon du kan sveve over for å se feilen. Hvis de ikke vises i Aktivitet, er dette problemet du må fokusere på først, så gå tilbake og finn ut av det. De fleste importfeil skyldes *tillatelser*, husk at Sonarr må kunne lese og skrive i nedlastingsmappen. Noen ganger kan tillatelser i biblioteksmappen også være årsaken, så sørg for å sjekke begge deler.

Feil i banen kan også være mulig, selv om det er mindre vanlig i normale oppsett. Nøkkelen for å forstå baneproblemer er å vite at får banen til nedlastingen *fra* nedlastingsklienten via API-en. Dette kan være et problem i mer unike tilfeller, som når nedlastingsklienten kjører på et annet system (kanskje til og med et annet operativsystem\!). Det kan også skje i et Docker-oppsett når volumene ikke er konfigurert riktig. En ekstern banekartlegging er en god løsning der du ikke har kontroll, for eksempel i et seedbox-oppsett. I et Docker-oppsett er det bedre å fikse banene.

## Vanlige problemer

Her er noen vanlige problemer.

### En eller flere forventede episoder i utgivelsen ble ikke importert eller mangler

- Hvis alle episodene ble importert, er den vanligste årsaken at det ble lastet ned en sesongpakke, men den inneholder ikke alle episodene i sesongen. Klikk på `X` for å fjerne og ignorere utgivelsen.
- For alle andre problemer ble en eller flere episoder ikke importert. Gå gjennom informasjonen i brukergrensesnittet og andre vanlige problemer.

### Bruker Sonarr v2

Sonarr v2 har nådd slutten av livet og støttes ikke lenger siden 3/2021. Den er ikke kompatibel med qBittorrent v4.3.0 eller nyere. Oppgrader til Sonarr v3.

### Nedlastingsklientens WebUI er ikke aktivert

Sonarr kommuniserer med nedlastingsklienten via API-en og får tilgang til den via klientens webgrensesnitt. Du må sørge for at nedlastingsklientens webgrensesnitt er aktivert, og at porten den bruker ikke kommer i konflikt med andre klientporter som er i bruk eller porter som er i bruk på systemet ditt.

### Bruk av SSL og feil konfigurert

Sørg for at SSL-kryptering ikke er aktivert hvis du bruker både instansen og nedlastingsklienten din i et lokalt nettverk. Se [SSL-FAQ-en](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for mer informasjon.

### Kan ikke se deling på Windows

Standardbrukeren for en Windows-tjeneste er `LocalService`, som vanligvis ikke har tilgang til delingene dine. Rediger tjenesten og sett den opp til å kjøre som din egen bruker. Se FAQ-en [hvorfor kan jeg ikke se filene mine på en ekstern server](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server) for detaljer.

### Mappede nettverksstasjoner er ikke pålitelige

Selv om mappede nettverksstasjoner som `X:\` er praktiske, er de ikke like pålitelige som UNC-baner som `\\server\share`, og de er heller ikke tilgjengelige før pålogging. Konfigurer nedlastingsklienten(e) dine slik at de bruker UNC-baner etter behov. Hvis biblioteket ditt er på en deling, må du sørge for at rotmappene dine bruker UNC-baner. Hvis nedlastingsklienten din sender til en deling, må du konfigurere UNC-baner der, siden får nedlastingsbanen fra nedlastingsklienten. Det er greit å beholde de mappede nettverksstasjonene for egen bruk, bare ikke bruk dem til automatisering.

### Docker og bruker, gruppe, eierskap, tillatelser og baner

Docker legger til et ekstra lag med kompleksitet som er lett å gjøre feil, men likevel ende opp med et oppsett som fungerer, men har ulike problemer. I stedet for å gå gjennom dem her, les denne wiki-artikkelen [for disse automatiseringsprogrammene og Docker](/docker-guide) som handler om bruker, gruppe, eierskap, tillatelser og baner. Den er ikke spesifikk for et bestemt Docker-system, i stedet går den over ting på et overordnet nivå slik at du kan implementere dem i ditt eget miljø.

### Ekstern banekartlegging

Hvis du har Sonarr i Docker og nedlastingsklienten utenfor Docker (eller omvendt) eller har programmene på forskjellige servere, kan du trenge en ekstern banekartlegging.

Loggene vil se slik ut

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Dermed eksisterer ikke `/volume3/data` i Sonarrs konteiner eller er ikke tilgjengelig.

- [Innstillinger => Nedlastingsklienter => Ekstern banekartlegging](/sonarr/settings#remote-path-mappings)
- En ekstern banekartlegging brukes når nedlastingsklienten rapporterer en bane for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er en ekstern banekartlegging bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows eller omvendt. En ekstern banekartlegging kan også være nødvendig hvis du blander Docker og Native-klienter eller hvis du bruker en ekstern server.
- En ekstern banekartlegging er en ENKEL søk/erstatt (der den finner VERDIEN FJERN, erstatt den med VERDIEN LOKAL for den angitte verten).
- Hvis feilmeldingen om en feil bane ikke inneholder DEN ERSTATTEDE verdien, fungerer ikke banekartleggingen som forventet. Den vanlige løsningen er å legge til og fjerne kartleggingen.
- [Se TRaSHs veiledning for mer informasjon om ekstern banekartlegging](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-kontainere, er det sjelden behov for en ekstern banekartlegging. Det anbefales å [gjennomgå Docker-guiden](/docker-guide) og/eller [følge TRaSHs veiledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Ekstern montering eller ekstern synkronisering (Syncthing)

- Du må sørge for at det synkroniseres hele tiden mens det lastes ned. Og du må sørge for at det lokale synkmålet kan være hardlenker når \*Arr importerer, noe som betyr samme filsystem og ser ut som det.
  - Synkroniser til en lavere, felles mappe som inneholder både ufullstendige og fullførte filer.
  - Synkroniser til en plassering som er på samme filsystem lokalt som biblioteket ditt og ser ut som det (Docker og nettverksdelinger gjør det enkelt å konfigurere feil).
  - Du vil synkronisere de ufullstendige og fullførte filene slik at når torrentklienten flytter dem, reflekteres det lokalt, og alle filene er allerede "der" (selv om de fortsatt lastes ned). Deretter vil du bruke hardlenker fordi selv om det blir importert før det er ferdig, vil de fortsatt fullføres.
  - På denne måten synkroniseres det hele tiden mens det lastes ned, deretter flytter torrentklienten til en undermappe for TV og synkroniseringen reflekterer det. På den måten er nedlastingen stort sett der når den er erklært som ferdig. Og selv om de ikke er helt ferdige, betyr muligheten for hardlenker at det er greit.
  - (Valgfritt - hvis det er aktuelt og/eller nødvendig (f.eks. ekstern usenet-klient)) Konfigurer et tilpasset skript som skal kjøres ved importering/nedlasting/oppgradering for å fjerne den eksterne filen.
- Alternativt er en ekstern montering i stedet for en ekstern synkronisering betydelig mindre komplisert å konfigurere, men vanligvis tregere.
  - Monter den eksterne lagringsenheten med sshfs eller en annen nettverksfilsystemprotokoll.
  - Sørg for at brukeren og gruppen \*Arr er konfigurert til å kjøre som, har lese- eller skrivetilgang.
  - Konfigurer en ekstern banekartlegging for å finne DEN EKSTERNE banen og erstatte den med DEN LOKALE tilsvarende banen

### Tillatelser på biblioteksmappen

Loggene vil se slik ut

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Ikke glem å sjekke tillatelser og eierskap for *destinasjonen*. Det er lett å fokusere på nedlastingens eierskap og tillatelser, og det er *vanligvis* årsaken til tillatelsesrelaterte problemer, men det *kan* også være destinasjonen. Sjekk at destinasjonsmappen(e) eksisterer. Sjekk om en destinasjonsfil allerede eksisterer eller ikke kan slettes eller flyttes til papirkurven. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres, hardlenkes eller flyttes. Brukeren eller gruppen som kjører Sonarr, må kunne lese og skrive i rotmappen.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Alternativet til å gjøre dette tilbys under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunitys artikkel om tillatelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Tillatelser på nedlastingsmappen

Du vil se en feilmelding lignende følgende

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

eller

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

Ikke glem å sjekke tillatelser og eierskap for *kilden*. Det er lett å fokusere på destinasjonens eierskap og tillatelser, og det er en *mulig* årsak til tillatelsesrelaterte problemer, men det er vanligvis kilden. Sjekk at kildebanen(e) eksisterer. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres/hardlenkes eller kopieres+slettes/flyttes. Brukeren eller gruppen som Sonarr kjører som, må kunne lese og skrive nedlastingsfilene.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Alternativet til å gjøre dette tilbys under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunitys artikkel om tillatelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Nedlastingsmappe og biblioteksmappe er ikke forskjellige mapper

- Nedlastingsklienten skal laste ned til en mappe som er tilgjengelig for \*Arr og som ikke er rot-/biblioteksmappen din; du skal importere fra den separate nedlastingsmappen til biblioteksmappen din.
- Du skal aldri laste ned direkte til rotmappen din. Du skal heller ikke bruke rotmappen din som nedlastingsklientens fullførte mappe eller ufullstendige mappe.
- [**Dette vil også forårsake en helsesjekk i System**](/sonarr/system#downloading-into-root-folder)
- Innenfor applikasjonen er en rotmappe definert som den konfigurerte mediebibliotekmappen. Dette er ikke rotmappen til et monteringspunkt. Nedlastingsklienten din har en ufullstendig eller fullført mappe (eller flytter fullførte nedlastinger) til rotmappen (biblioteket) ditt. Dette forårsaker ofte problemer og anbefales ikke. For å løse dette, endre nedlastingsklienten din slik at den ikke plasserer nedlastinger i rotmappen din. Merk at 'plassering' også inkluderer om nedlastingsklienten din kategori er satt til rotmappen din eller om NZBGet/SABnzbd har sortering aktivert og sorterer til rotmappen din. Vær oppmerksom på at denne sjekken ser på alle definerte/konfigurerte rotmapper som er lagt til, ikke bare rotmapper som for øyeblikket er i bruk. Med andre ord skal ikke mappen der nedlastingsklienten din laster ned eller flytter fullførte nedlastinger til, være den samme mappen du har konfigurert som rot-/bibliotek-/endelige destinasjonsmappe for medier i \*Arr-applikasjonen.
- Konfigurerte rotmapper (også kjent som bibliotekmapper) finner du under [Innstillinger => Mediehåndtering => Rotmapper](/sonarr/settings/#root-folders)
- Et eksempel er hvis nedlastingen din går til `\data\downloads`, så har du en rotmappe satt som `\data\downloads`.
- Det anbefales å bruke stier som `\data\media\` for rotmappen/biblioteket ditt og `\data\downloads\` for nedlastingene dine.

> Nedlastingsmappen din og rot-/biblioteksmappen din **må være separate**
{.is-warning}

### Feil kategori

Sonarr skal være konfigurert til å bruke en kategori slik at den bare prøver å behandle sine egne nedlastinger. Det er sjelden at en torrent som er lagt til uten riktig kategori, men det kan skje. Hvis du legger til torrents manuelt og vil behandle dem, må de ha riktig kategori. Den kan settes når som helst, siden Sonarr prøver å behandle nedlastinger hvert minutt.

### Pakkede torrents

Logger vil vise feil som

```none
Ingen filer som er funnet, er kvalifisert for import
```

Hvis torrenten din er pakket i `.rar`-filer, må du sette opp utpakking. Vi anbefaler [Unpackerr](https://github.com/unpackerr/unpackerr) siden den gjør utpakking riktig: forhindrer korrupte delvise importeringer og rydder opp i de utpakkede filene etter importering.

Feilen kan også oppstå hvis det ikke finnes gyldige mediefiler i mappen.

### Gjentatte nedlastinger

Det er flere årsaker til gjentatte nedlastinger, men en av dem er relatert til begrensningen i indekseren i utgivelsesprofiler. Fordi indekseren *ikke* er lagret sammen med dataene, er alle "foretrukne ord"-poengene *null* for medier i biblioteket ditt, men under "RSS" og søk vil de bli brukt. Det samme gjelder for eventuelle begrensninger for "må inneholde" eller "må ikke inneholde" - de gjelder bare for den indekseren; alt annet er lov. Dette fører til en løkke der du laster ned elementene om og om igjen fordi det ser ut som en oppgradering, så er det ikke det, så dukker det opp igjen og ser ut som en oppgradering, så er det ikke det. Ikke begrens utgivelsesprofilen din til en indekser.

Dette kan også skyldes at nedlastingen faktisk aldri blir importert og deretter mangler fra køen, slik at en ny nedlasting stadig blir hentet og aldri importert. Se de forskjellige vanlige problemene og feilsøkingsstegene for dette.

### Usenet-nedlasting blir ikke importert

Sonarr ser bare på de 60 nyeste nedlastingene i SABnzbd og NZBGet, så hvis du *beholder* historikken din, betyr det at under store køer med importproblemer kan nedlastinger bli tapt og ikke importert. Den beste måten å unngå dette på er å holde historikken din ryddig, slik at eventuelle elementer som fortsatt vises, må undersøkes. Du kan oppnå dette ved å aktivere Fjern under Fullført og Mislykket nedlastingsbehandler. I NZBGet vil dette flytte elementer til den *skjulte* historikken, noe som er flott. Dessverre har ikke SABnzbd en lignende funksjon. Det beste du kan oppnå der er å bruke nzb-sikkerhetskopimappen.

### Nedlastingsklienten fjerner elementer

Nedlastingsklienten skal *ikke* være ansvarlig for å fjerne nedlastinger. Usenet-klienter skal konfigureres slik at de *ikke* fjerner nedlastinger fra historikken. Torrent-klienter skal settes opp slik at de *ikke* fjerner torrenter når de er ferdig med å seede (pause eller stopp i stedet). Dette er fordi Sonarr kommuniserer med nedlastingsklienten for å vite hva som skal importeres, så hvis de blir *fjernet*, er det ingenting å importere, selv om det er en mappe full av filer.

For SABnzbd håndteres dette med innstillingen for historiebevaring.

### Nedlastingen kan ikke matches med et bibliotekselement

Av forskjellige årsaker kan utgivelser ikke analyseres når de er hentet og sendt til nedlastingsklienten. Aktivitet => Alternativer => Vis ukjent (dette er nå aktivert som standard i nyere versjoner) vil vise alle elementer som ikke er ignorert/ikke allerede importert innenfor \*Arrs nedlastingsklientkategori. Disse må vanligvis tilordnes og importeres manuelt.

Dette kan også skje hvis du har en utgivelse i nedlastingsklienten din, men det medieelementet (film/episode/bok/sang) eksisterer ikke i applikasjonen.

#### Fant matchende serie via hentehistorikk, men serien ble matchet etter serie-ID. Automatisk import er ikke mulig

- Denne importfeilen ligner på feilen som ikke kan matches ovenfor.
- Sonarr hentet utgivelsen fordi indekseren eller sporingen din rapporterte at utgivelsen hadde TVDb-IDen (eller IMDb-IDen) for en serie du ønsket.
- Serien til den nedlastede filen samsvarer ikke med den rapporterte IDen, så Sonarr vil ikke importere filen.
- Avhengig av serietittelen og utgivelsesnavnet - under forutsetning av at utgivelsen er riktig for den tilknyttede serien IDen - vil Sonarr sannsynligvis trenge en alias som må legges til, [denne FAQ-oppføringen har mer informasjon](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) om hvordan du kan be om at et alias legges til.
- Alternativt kan utgivelsen være feilmerket og ikke for den rapporterte serien IDen. Dette bør rapporteres til indekseren din slik at de kan ta rettende tiltak.
- For å håndtere denne feilen:
  1. Bekreft serien til filen
  1. Be om et alias (hvis relevant)
  1. Importer filen manuelt (menneskeikonet til høyre) fra Aktivitet => Køen ELLER klikk på `X` i køen for å ignorere utgivelsen i klienten din og eventuelt blokkere den / eventuelt fjerne den fra klienten

### Episodenavn er TBA

På TVDB, når episodenavnene er ukjente, vil de bli kalt TBA, og det er en 24-timers buffer på APIen. Typisk tar endringer på TVDB-nettstedet 24-48 timer å nå Sonarr på grunn av TVDB-buffer, Skyhook-buffer og serieoppdateringsintervallet.

Innstillingen [Episode Title Required](/sonarr/settings#importing) i Sonarr kontrollerer importoppførselen når tittelen er TBA, men etter 24 timer fra episodens sendetidspunkt vil utgivelsen bli importert selv om tittelen fortsatt er TBA. Det er heller ingen automatisk omdøping av filer med TBA-titler.

### Forbindelsen ble lukket: En uventet feil oppstod under sendingen

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Sonarr => System => Status](/sonarr/system#status).

### Forespørselen tidsavbrutt

Sonarr får ingen respons fra klienten.

```none
    System.NET.WebException: Forespørselen tidsavbrutt: ’https://eksempel.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Forespørselen tidsavbrutt
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke koble til indekseren

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En oppgave ble avbrutt.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av en VPN
- feil konfigurert eller bruk av en proxy
- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
- lokale IPv6-problemer - typisk er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

## Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelses- og nettverksfeilsøkingskommandoer [i guiden vår](/permissions-and-networking). Ellers kan du diskutere det med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

# Søk i indekser og sporingssider

- [Hvorfor hentet ikke Sonarr en episode jeg forventet?](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) FAQ-oppføringen kan også være nyttig.
- Hvis du bruker [Prowlarr](/prowlarr), kan du se [Historikk](/prowlarr/history) over alle henvendelser Prowlarr mottok og hvordan de ble sendt til nettstedene. Sørg for at `Parametere` er aktivert i Prowlarr Historikk => Alternativer. (i)-ikonet gir ytterligere detaljer.
- Feilsøkingsstegene er ellers nedenfor

## Skru opp loggingen til sporingsnivå

> **Det første trinnet er å skru opp loggingen til sporingsnivå, se [Logging og loggfiler](#logging-and-log-files) for detaljer om hvordan du justerer loggingen og søker i loggene. Du gjenskaper deretter problemet og bruker sporingsnivåloggene fra den tidsrammen til å undersøke problemet.** Hvis noen hjelper deg, legg kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem. Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet mens oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

## Test av indekser eller sporingssider

Når du tester en indekser eller sporingsside, kan du finne URLen som ble brukt i feilsøkings- eller sporingslogger. Et eksempel på en vellykket test er nedenfor, der du kan se at den spør indekseren via en spesifikk URL med spesifikke parametere, og deretter svaret. Du kan teste denne URLen i nettleseren din ved å erstatte `apikey=(fjernet)` med riktig api-nøkkel som `apikey=123`. Du kan eksperimentere med parameterne hvis du får en feil fra indekseren, eller se om du har tilkoblingsproblemer hvis det ikke fungerer i det hele tatt. Etter at du har testet i nettleseren din, bør du teste fra systemet som kjører *hvis* du ikke allerede har gjort det.

## Test av et søk

På samme måte som testen av indekser/sporingssider ovenfor, når du utløser et søk mens loggingen er satt til Debug eller Trace-nivå, kan du få URLen som ble brukt fra loggfilene. Under testingen er det best å bruke et så smalt søk som mulig. Et manuelt (interaktivt) søk etter en enkelt episode eller sesong er bra fordi det er spesifikt, og du kan se resultatene i brukergrensesnittet mens du undersøker loggene. Manuelle (interaktive) søk utløses ved å gå til en serie og klikke på menneskeikonet for en episode eller sesong.

I denne testen ser du etter åpenbare feil og kjører noen enkle tester. Du kan se at søket brukte URLen `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(fjernet)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, som du kan prøve selv i en nettleser etter å ha erstattet (fjernet) med api-nøkkelen din for den indekseren. Fungerer det? Ser du de forventede resultatene? Gjelder denne FAQ-oppføringen? I den URLen kan du se at den har satt spesifikke kategorier med `cat=5030,5040,5045,5080`, så hvis du ikke ser forventede resultater, er dette en sannsynlig årsak. Du kan også se at den søkte etter tvdbid med `tvdbid=354629`, så hvis episoden ikke er riktig kategorisert på indekseren, må det fikses. Du kan også se at den søkte etter en spesifikk sesong og episode med season=1 og ep=1, så hvis det ikke er riktig på indekseren, vil du ikke se de resultatene. Se på eksempelet på XML-utdata for manuelt søk nedenfor for å se et eksempel på utdata for en fungerende forespørsel.

- XML-utdata for manuelt søk

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- Sporloggutdrag

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|Søker 1 indekser for [The Fix : S01E01]
2021-03-20 13:15:23.6|Debug|Newznab|Laster ned feeden https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- Full sporlogg for en søk

```none
2022-04-24 20:14:26.7|Info|NzbSearchService|Searching 1 indexers for [Fairy Tail : S02E91 (91)]
2022-04-24 20:14:26.7|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=123456&season=2&ep=91
2022-04-24 20:14:26.7|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=123456&season=2&ep=91
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'proxyenabled' defaultValue:'False'
2022-04-24 20:14:27.3|Trace|HttpClient|Res: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=123456&season=2&ep=91: 200.OK (680 ms)
2022-04-24 20:14:27.3|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Debug|NzbSearchService|Total of 2 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:27.3|Debug|NzbSearchService|Setting last search time to: 11/20/2019 13:15:24
2022-04-24 20:14:27.3|Info|DownloadDecisionMaker|Processing 2 releases
2022-04-24 20:14:27.3|Trace|DownloadDecisionMaker|Processing release 1/2
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.3|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.3|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.3|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.3|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.3|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:27.3|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.3|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.3|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.3|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.3|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.3|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.3|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:27.3|Trace|DownloadDecisionMaker|Processing release 2/2
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.3|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.3|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.3|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.3|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.3|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:27.3|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.3|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.3|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.3|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.3|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.3|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.3|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.3|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.3|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.3|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.3|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.3|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'autounmonitorpreviouslydownloadedepisodes' defaultValue:'False'
2022-04-24 20:14:27.3|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:27.3|Trace|ConfigService|Using default config value for 'downloadpropersandrepacks' defaultValue:'PreferAndUpgrade'
2022-04-24 20:14:27.3|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
2022-04-24 20:14:27.3|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (775 ms)
```

## Vanlige problemer

Her er noen vanlige problemer som er løsningen for nesten alle problemer som oppstår.

### Indexere blir ikke søkt

- Loggene vil se slik ut

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Søker indexere for [Fairy Tail : S02E91 (91)]. 0 aktive indexere
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Totalt 0 rapporter ble funnet for [Fairy Tail : S02E91 (91)] fra 0 indexere
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|Ingen resultater funnet
```

- Merk at i det ovennevnte tilfellet blir det ikke søkt i noen indexere. Dette antallet kan variere basert på din spesifikke oppsett. Hvis antallet ikke er det samme som antallet konfigurerte indexere, er følgende sannsynlige årsaker:
  - [Helsesjekker (System => Status)](/sonarr/system#health)
    - [Ingen indexere tilgjengelig med automatisk søk aktivert, Sonarr vil ikke gi noen automatiske søkeresultater](/sonarr/system#no-indexers-available-with-automatic-search-enabled-sonarr-will-not-provide-any-automatic-search-results)
    - [Ingen indexere er aktivert](/sonarr/system#no-indexers-are-enabled)
    - [Aktiverte indexere støtter ikke søk](/sonarr/system#enabled-indexers-do-not-support-searching)
    - [Ingen indexere tilgjengelig med interaktivt søk aktivert](/sonarr/system#no-indexers-available-with-interactive-search-enabled)
    - [Indexere er utilgjengelige på grunn av feil](/sonarr/system#indexers-are-unavailable-due-to-failures)
  - Søker en serietype som Anime og ingen anime-kategorier er konfigurert for sporingene dine. Indexere har [to forskjellige konfigurerbare kategorityper](/sonarr/settings#indexers).
  - Søker en serietype som Daglig eller Standard, og ingen standard (ikke-anime) kategorier er konfigurert for sporingene dine.
    - Kategorier - Standardkategorier vil bli brukt med mindre de blir redigert. Det er sannsynlig at disse standardkategoriene ikke er optimale. Når denne innstillingen blir redigert, spør Sonarr indexeren om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil forsvinne så snart en kategori blir vekslet.
  - Animekategorier - Kategoriene som Sonarr vil bruke for Anime-søk. Ingen kategorier vil bli brukt med mindre de blir redigert. Når denne innstillingen blir redigert, spør Sonarr indexeren om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil forsvinne så snart en kategori blir vekslet.
  - Indexerens funksjoner støtter ikke spørringstypen (f.eks. Sesong/Episode, osv.):
    - Innenfor Prowlarr kan indexerens funksjoner finnes i (I)-ikonet for indexeren.
    - Jackett viser ikke en indexers funksjoner innenfor sitt brukergrensesnitt.
  - Sporingslogger vil vise informasjon om hvorfor indexere blir ignorert hvis et søk blir utført etter ***omstart av Sonarr***.

### Dårlig navngitte utgivelser

- Seriespakker støttes ikke
- Flere sesongpakker støttes ikke
- I mange tilfeller klarer ikke Sonarr å matche det returnerte resultatet med en kjent serie. I slike tilfeller vil loggene dine se omtrent slik ut. Disse må sannsynligvis hentes og importeres manuelt. Nøkkelfrasen å se etter i loggene er `|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### Tracker trenger RawSearch Caps

- Sonarr søker etter `9 1 1`, men sporingen din har bare resultater for `9-1-1` eller `John s Show` og `John's Show`
- Dette skyldes at sporingen din ikke støtter normale standardiserte søk.
- Løsningen er at sporingens definisjon av søkefunksjoner må oppdateres for å indikere at den [krever og støtter `RawSearch`](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackett støtter flagget, men funksjonene må oppdateres for hver indekser. Åpne en funksjonsforespørsel for Jackett for å legge til denne funksjonaliteten for indekseren din.
- Prowlarr støtter flagget, men funksjonene må oppdateres for hver indekser. Åpne en funksjonsforespørsel for Prowlarr for å legge til denne funksjonaliteten for indekseren din.

### Serien trenger et alias

Utgivelser kan lastes opp som `The Series Name`, men TVDB har serien som `Series Name` eller lignende navneforskjeller. Se [denne FAQ-oppføringen](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x) for mer informasjon.

### Serien trenger en XEM-mapping

Utgivelser kan lastes opp som `Series Title S02E45` eller `Other Series Title S2022E42`, men TVDB har denne episoden som `Series Title S03E01` eller `Other Series Title S03E42`. Se [denne FAQ-oppføringen](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc) for mer informasjon.

### Feil serietype

Serietypen påvirker hvordan Sonarr søker. Serietypen bør velges basert på hvordan serien blir utgitt på indekserne.
[Se denne FAQ-oppføringen for mer informasjon](/sonarr/faq#whats-the-different-series-types)

> Hvis **Anime**-serietypen brukes, er det [mulig å også søke etter indekseren med standardtypen.](/sonarr/settings#indexers)
{.is-info}

#### Daglig

Loggene vil vise `Søker indekser for [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Loggene vil vise `Søker indekser for [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Loggene vil vise `Søker indekser for [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### Mediet er ikke overvåket

Loggene vil vise noe lignende

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

Serien/sesongen/episodene er ikke overvåket. Sjekk overvåkingsstatusen til serien, sesongen og episodene.

> Sesongpakker vil bare bli lastet ned hvis alle episodene i sesongen er overvåket, og sesongpakken oppgraderer alle eksisterende episoder eller alle episoder mangler.
{.is-info}

### Vellykket søk - Ingen resultater returnert

Du får en melding som ligner på `Query successful, but no results were returned from your indexer. This may be an issue with the indexer or your indexer category settings.`

Dette skyldes at indekseren ikke returnerer noen resultater innenfor kategoriene du har konfigurert for indekseren.

### Feil kategorier

Feil kategorier er sannsynligvis den vanligste årsaken til at resultater vises i manuelle søk på en indekser/sporing, men *ikke* i \*Arr. Indekseren/sporingen *bør* vise kategorien i søkeresultatene, noe som bør hjelpe deg med å finne ut hva som mangler. Hvis du bruker Jackett eller Prowlarr, har hver indekser en liste over spesifikt støttede kategorier. Sørg for at du bruker riktige kategorier for kategoriene. Mange finner det nyttig å ha listen synlig i ett nettleservindu mens de redigerer oppføringen i Sonarr.

> Merk at hvis du har `Anime Categories` tom i innstillingene for indekseren din, vil ikke indekseren bli brukt for søk av Anime-serietypen.
> På samme måte, hvis du har `Categories` tom i innstillingene for indekseren din, vil ikke indekseren bli brukt for Standard eller Daglig-serietypen.
{.is-info}

### Feil resultater

Noen ganger returnerer indekserne helt irrelevante resultater; Sonarr sender inn parametere for å begrense søket til en serie. Noen ganger er resultatene som returneres helt irrelevante. Eller noen ganger, hovedsakelig relatert med noen få feilaktige resultater. Den første årsaken er vanligvis et indekserproblem, og du kan se fra sporingsloggene hvilket indekser som forårsaker det. Du kan deaktivere den indekseren og rapportere problemet. Den andre årsaken er vanligvis kategoriserte utgivelser som kan rapporteres på indekseren/sporingen.

Visse sporinger - som EZTV og andre offentlige - returnerer tilfeldige resultater hvis de ikke har en nøyaktig kamp for serien/sesongen/episoden som blir forespurt. Det finnes ingen løsning for dette.

### Manglende resultater

Hvis du har resultater på nettstedet som du finner, men som ikke vises i Sonarr, er problemet sannsynligvis en av flere muligheter:

- [Feil kategorier - se over](#wrong-categories)
- Det blir gjort et ID-basert søk (IMDbId, TVDBId, osv.), og indekseren har ikke korrekt kartlagt utgivelsene til den ID-en. Dette er noe bare indekseren din kan løse. De må sørge for at utgivelsen er kartlagt til de riktige ID-ene som gjelder.
- Du søker ikke på samme måte som Sonarr søker; Det er svært sannsynlig at vilkårene du søker etter på indekseren ikke er hvordan Sonarr spør etter det. Du kan se hvordan Sonarr spør fra sporingsloggene. Tekstbaserte søk vil generelt være i formatet `q=ord%20og%20ting%20her` denne strengen er HTTP-kodet og kan enkelt dekodes ved hjelp av et hvilket som helst HTML-dekoderings-/kodingsverktøy på nettet.
- Manglende deler av RSS-feeden for nye opplastinger. Loggene vil se ut som følger, og en advarselshendelse vil bli merket.

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### Sertifikatvalidering

Du vil koble til de fleste indekser/sporinger via https, så du må sørge for at dette fungerer riktig på systemet ditt. Det betyr at tidssonen og tiden din må være satt *riktig*. Det betyr også at systemets sertifikater må være oppdaterte.

### Treff rategrenser

Hvis du bruker en VPN eller proxy, kan du konkurrere med 10-talls eller 100-talls eller 1000-talls andre personer som alle prøver å bruke tjenester som , theXEM og/eller indekserne og sporingene dine. Rategrenser og DDOS-beskyttelse blir ofte gjort etter IP-adresse, og VPN-/proxy-utgangspunktet ditt er *én* IP-adresse. Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, trenger du ikke VPN/proxy.

Rarbg har en tendens til å ha en form for rategrense i API-et sitt og vises som svarer uten resultater.

### IP-blokkering

På samme måte som rategrenser, kan visse indekser - som Nyaa - utestenge en IP-adresse helt. Dette er vanligvis halvpermanent, og løsningen er å få en ny IP fra internettleverandøren eller VPN-leverandøren din.

### Bruk av Jackett /all-endepunktet

Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan være potensielle problemer, så det kreves å legge til hver indekser individuelt. Alternativt kan du sjekke ut Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Selv Jackett sier at /all bør unngås og ikke bør brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)

Å bruke all-endepunktet har ingen fordeler (bortsett fra redusert administrasjonsarbeid), bare ulemper:

- du mister kontrollen over indekser-spesifikke innstillinger (kategorier, søkemåter, osv.)
- blanding av søkemåter (IMDB, spørring, osv.) kan føre til lavkvalitetsresultater
- indekser-spesifikke kategorier (\>= 100000) kan ikke brukes.
- treg indekser vil bremse ned det totale resultatet
- totalt antall resultater er begrenset til 1000
- irrelevante resultater
- manglende resultater

Å legge til hver indekser separat tillater finjustering av kategorier på en per-indeks-basis, noe som kan være et problem med `/all`-endepunktet hvis bruk av feil kategori forårsaker feil på noen indekser. I Sonarr er hver indekser begrenset til 1000 resultater hvis paginering støttes, eller 100 hvis ikke, noe som betyr at jo flere indekser du legger til i Jackett, desto mer sannsynlig er det at du klipper resultater. Til slutt, hvis *en* av indekserne i `/all` returnerer en feil, vil Jackett deaktivere den, og nå får du ingen resultater.

### Bruk av NZBHydra2 som en enkelt oppføring

Å bruke NZBHydra2 som en enkelt indekseroppføring (dvs. 1 NZBHydra2-oppføring i Sonarr for mange indekser i NZBHydra2) i stedet for flere (dvs. mange NZBHydra2-oppføringer i Sonarr for mange indekser i NZBHydra2) har de samme problemene som nevnt ovenfor med Jacketts `/all`-endepunkt.

### Indekseren blir ikke søkt

- Hvis en indekser ikke ser ut til å bli søkt, skyldes det sannsynligvis at indekseren ikke støtter forespørselstypen. Det vanligste tilfellet er at Nyaa bare støtter spørringsøk og ikke sesong-/episodesøk. Sporingsloggene indikerer etter en omstart på det første søket hvilke funksjoner en indekser har eller ikke har.

### Jackett manuelt søk finner flere resultater

- [Se denne FAQ-oppføringen](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### Utgivelsesprofiler blir ikke respektert

Det er noen årsaker til at det kan virke som om profilene dine blir ignorert. Den vanligste årsaken er relatert til indekserbegrensningen i utgivelsesprofilene. Fordi indekseren *ikke* lagres med dataene, er eventuelle "foretrukne ord"-poeng *null* for medier i biblioteket ditt, *men* under "RSS" og søk vil de bli brukt. På samme måte gjelder eventuelle restriksjoner for "må inneholde" eller "må ikke inneholde" bare for den indekseren; alt annet er fair game. Dette kan føre til at utgivelsesprofilene virker som om de blir ignorert, eller at oppgraderingsløkker oppstår.

### Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelses- og nettverkstroubleshootingkommandoer [i guiden vår](/permissions-and-networking). Ellers kan du diskutere med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

## Feil

Dette er noen av de vanlige feilene du kan se når du legger til en indekser

### The underlying connection was closed: An unexpected error occurred on a send

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Sonarr => System => Status](/sonarr/system#status).

### The request timed out

Sonarr får ingen respons fra indekseren.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av VPN
- feil konfigurert eller bruk av proxy
- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

### Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelses- og nettverkstroubleshootingkommandoer [i guiden vår](/permissions-and-networking). Ellers kan du diskutere med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.