---
title: Lidarr Feilsøking
description: 
published: true
date: 2023-07-24T19:53:24.970Z
tags: lidarr, needs-love, feilsøking
editor: markdown
dateCreated: 2021-06-14T21:36:46.193Z
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
- [Gjenopprette etter en mislykket oppdatering](#gjenopprette-etter-en-mislykket-oppdatering)
  - [Identifisere problemet](#identifisere-problemet)
    - [Migreringsproblem](#migreringsproblem)
    - [Tillatelsesproblem](#tillatelsesproblem)
  - [Løse problemet](#løse-problemet)
    - [Tillatelsesproblemer](#tillatelsesproblemer)
    - [Manuell oppgradering](#manuell-oppgradering)
- [Nedlastinger og importering](#nedlastinger-og-importering)
  - [Teste nedlastingsklienten](#teste-nedlastingsklienten)
  - [Teste en nedlasting](#teste-en-nedlasting)
  - [Teste en importering](#teste-en-importering)
  - [Vanlige problemer](#vanlige-problemer)
    - [Nettlesergrensesnittet for nedlastingsklienten er ikke aktivert](#nettlesergrensesnittet-for-nedlastingsklienten-er-ikke-aktivert)
    - [Feil konfigurert SSL](#feil-konfigurert-ssl)
    - [Kan ikke se deling på Windows](#kan-ikke-se-deling-på-windows)
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
    - [Usenet-nedlasting går glipp av importering](#usenet-nedlasting-går-glipp-av-importering)
    - [Nedlastingsklient tømmer elementer](#nedlastingsklient-tømmer-elementer)
    - [Nedlastingen kan ikke matches med et bibliotekselement](#nedlastingen-kan-ikke-matches-med-et-bibliotekselement)
    - [Tilkobling tidsavbrutt](#tilkobling-tidsavbrutt)
  - [Problem som ikke er oppført](#problem-som-ikke-er-oppført)
- [Søk, indekser og sporere](#søk-indekser-og-sporere)
  - [Øke loggingen til sporingsnivå](#øke-loggingen-til-sporingsnivå)
  - [Teste en indekser eller sporingsklient](#teste-en-indekser-eller-sporingsklient)
  - [Teste et søk](#teste-et-søk)
  - [Vanlige problemer](#vanlige-problemer-1)
    - [Mediet er ikke overvåket](#mediet-er-ikke-overvåket)
    - [Sporeren krever RawSearch-funksjoner](#sporeren-krever-rawsearch-funksjoner)
    - [Feil kategorier](#feil-kategorier)
    - [Feil resultater](#feil-resultater)
    - [Spørring vellykket - ingen resultater returnert](#spørring-vellykket---ingen-resultater-returnert)
    - [Mangler resultater](#mangler-resultater)
    - [Sertifikatvalidering](#sertifikatvalidering)
    - [Treffer rategrenser](#treffer-rategrenser)
    - [IP-blokkering](#ip-blokkering)
    - [Bruke Jackett /all-endepunktet](#bruke-jackett-all-endepunktet)
    - [Bruke NZBHydra2 som enkeltinngang](#bruke-nzbhydra2-som-enkeltinngang)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-1)
  - [Feil](#feil)
    - [The underlying connection was closed: An unexpected error occurred on a send](#the-underlying-connection-was-closed-an-unexpected-error-occurred-on-a-send)
    - [The request timed out](#the-request-timed-out)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-2)

# Be om hjelp

Trenger du hjelp? Det er greit, alle trenger hjelp av og til. Du kan få hjelp i sanntid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Offisiell Lidarr Discord*](https://lidarr.audio/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offisiell Lidarr Subreddit*](https://reddit.com/r/lidarr)
{.links-list}

Men før du går dit og legger ut en melding, må du sørge for at forespørselen om hjelp er så god som mulig. Beskriv tydelig problemet og gi en kort beskrivelse av oppsettet ditt, inkludert ting som operativsystem/distribusjon, versjon av .NET, versjon av Lidarr, nedlastingsklient og versjonen av denne. **Hvis du bruker [Docker](https://www.docker.com/), kan du kjøre gjennom [Docker Guide](/docker-guide) først, da dette vil løse vanlige og hyppige problemer med stier/tillatelser. Ellers kan du ha en [docker compose](/docker-guide#docker-compose) klar. [Slik genererer du en Docker Compose](https://trash-guides.info/compose)** Fortell oss hva du allerede har prøvd, hva du har sett på. Bruk [Logging og loggfiler](#logging-og-loggfiler) for å øke loggingen til sporingsnivå, gjenskap problemet, legg relevant kontekst ut på en pastebin og inkluder en lenke til den i innlegget ditt. Kanskje du til og med kan inkludere noen skjermbilder for å fremheve problemet.

Jo mer vi vet, jo enklere er det å hjelpe deg.

# Logging og loggfiler

Det kan være nyttig å også se gjennom vanlige feilsøkingsproblemer:
- [Vanlige problemer med nedlastinger og importering](#vanlige-problemer)
- [Vanlige problemer med søk, indekser og sporere](#vanlige-problemer-1)
{.links-list}

Hvis du blir bedt om feilsøkingslogger, vil loggene dine inneholde `debug`, og hvis du blir bedt om sporingslogger, vil loggene dine inneholde `trace`. Hvis loggene du gir ikke inneholder noen av disse, er de ikke de loggene som er etterspurt.

- Unngå å dele hele loggfilen med mindre du blir bedt om det.
- Ikke last opp logger direkte til Discord eller lim dem inn som store tekstblokker, med mindre du blir bedt om det.
- Ikke del loggene som vedlegg, zip-arkiv eller noe annet enn tekst som deles via tjenestene som er nevnt nedenfor.

For å gi gode og nyttige logger for deling:

> Sørg for at en spamaktig oppgave IKKE kjører, for eksempel en RSS-oppdatering
{.is-warning}

1. [Øk loggingen til sporingsnivå (Innstillinger => Generelt => Loggnivå eller rediger konfigurasjonsfilen)](#sporingsfeilsøkingslogger)
2. [Slett logger (System => Logger => Slett logger eller slett alle loggene i loggmappen)](#slette-logger)
3. Gjenskap problemet (Gjør det som forårsaker problemene på nytt)
4. [Åpne sporingsloggfilen (Lidarr.trace.txt) via brukergrensesnittet eller loggfilen](#standard-plassering-for-logger) på filsystemet og finn relevant kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del etter problemet.
6. Bruk [Gist](https://gist.github.com/), [0bin (**Sørg for å deaktivere fargelegging**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) eller lignende nettsteder - unntatt de som er nevnt nedenfor - for å dele de kopierte loggene fra ovenfor

**Advarsler:**
- **Ikke bruk [pastebin.com](https://pastebin.com), da filtrene deres har en tendens til å blokkere loggene.
- Ikke bruk [pastebin.pl](https://pastebin.pl), da nettstedet deres ofte ikke er tilgjengelig.
- Ikke bruk [JustPasteIt](https://justpaste.it/), da nettstedet deres ikke er egnet for gjennomgang av logger.
- Ikke last opp loggen din som en fil.
- Ikke last opp og del loggene dine via Google Drive, Dropbox eller noen andre nettsteder som ikke er nevnt ovenfor.
- Ikke arkiver (zip, tar (tarball), 7zip, osv.) loggene dine.
- Ikke del konsollutdata, utdata fra Docker-container eller noe annet enn de spesifiserte programloggfilene

**Viktig merknad:**
- Når du bruker [0bin](https://0bin.net/), må du sørge for å deaktivere fargelegging og ikke brenne etter lesing.

- Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men ikke er sikker på hvilken du kan bruke N++. Du kan bruke Notepad++-funksjonen "Søk i filer" for å søke i gamle loggfiler etter behov.
- **Bare Unix:** Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men ikke er sikker på hvilken du kan bruke grep. Hvis du for eksempel vil finne informasjon om filmen/serien/boken/sangen/indekseren "Shooter", kan du kjøre følgende kommando: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Hvis [Appdata-mappen](/lidarr/appdata-directory) din er i hjemmemappen, kan du kjøre: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggene har følgende funksjoner
    * -i: ignorere store/små bokstaver
    * -n: vis linjenummer
    *  -r: sjekk rekursivt alle filer i banen
    * -C: gi antall linjer før og etter linjen den er funnet på
    * -e: mønsteret som skal søkes etter

```

## Standard plassering for logger

Loggfilene ligger i Lidarrs [Appdata-mappen](/lidarr/appdata-directory), inne i mappen logs/. Du kan også få tilgang til loggfilene fra brukergrensesnittet på System => Logger => Filer.

> Merk: Tabellen "Logger" i brukergrensesnittet er ikke det samme som loggfilene og er ikke like nyttig. Hvis du blir bedt om logger, kopier/lim inn fra loggfilene og ikke tabellen.
{.is-info}

## Plassering for oppdateringslogger

Oppdateringsloggfilene ligger i Lidarrs [Appdata-mappen](/lidarr/appdata-directory), inne i mappen UpdateLogs/.

## Deling av logger

Loggene kan være lange og vanskelige å lese som en del av et forum- eller Reddit-innlegg, og de er spamaktige i Discord, så bruk [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller lignende pastebin-nettsteder. Hele filen er vanligvis ikke nødvendig, bare en god mengde kontekst fra før og etter problemet/feilen. Ikke glem å vente til spamaktige oppgaver som en RSS-synkronisering eller biblioteksoppdatering er ferdige.

## Sporings-/feilsøkingslogger

Du kan endre loggnivået på Innstillinger => Generelt => Logging. Lidarr trenger ikke å startes på nytt for at endringen skal tre i kraft. De nyeste debug-/sporingsloggfilene har navnene `lidarr.debug.txt` og `lidarr.trace.txt` henholdsvis.

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

Lidarr bruker rullerende loggfiler som er begrenset til 1 MB hver. Den nåværende loggfilen er alltid `lidarr.txt`, for de andre filene er `.0.txt` den nest nyeste (jo høyere nummer, jo eldre er den). Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.

Når Debug-loggnivået er aktivert, vil det være tilgjengelige ekstra `lidarr.debug.txt` rullerende loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. De dekker vanligvis en periode på 40 timer.

Når Trace-loggnivået er aktivert, vil det være tilgjengelige ekstra `lidarr.trace.txt` rullerende loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsomfanget dekker de bare et par timer eller mindre.

# Gjenopprette etter en mislykket oppdatering

Vi gjør alt vi kan for å forhindre problemer ved oppgradering, men hvis de likevel oppstår, vil dette veilede deg gjennom trinnene du må ta for å gjenopprette installasjonen din.

## Identifisere problemet

- Det beste stedet å se når programmet ikke starter etter en oppdatering, er å se gjennom [oppdateringsloggene](#plassering-for-oppdateringslogger) og se om oppdateringen ble fullført. Hvis det ikke er noen problemer der, er neste steg å se på de vanlige programloggfilene dine. Før du prøver å starte på nytt, bruk [Logging](/lidarr/settings#logging) og [Loggfiler](/lidarr/system#log-files) for å finne dem og øke loggnivået.
- Det mest vanlige problemet er at systemet der appen er installert, har rotet med `/tmp`-mappen og slettet kritiske \*Arr-filer under oppdateringen, noe som fører til at både oppdateringen og tilbakerulling mislykkes. I dette tilfellet kan du bare reinstallere over den eksisterende ødelagte installasjonen.

### Migreringsproblem

- Migreringsfeil vil ikke være identiske, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Tillatelsesproblem

- Tillatelsesproblemer skyldes at programmet ikke kan få tilgang til de relevante midlertidige mappene og/eller appens binærmappe. Løs tillatelsene slik at brukeren/gruppen som appen kjører som, har riktig tilgang.

- Synology-brukere kan oppleve denne Synology-feilen `Access to the path '/proc/{noen tall}/maps is denied`

- Synology-brukere kan også oppleve at det er tomt for plass i `/tmp` på visse NAS-er. Du må angi en annen `/tmp`-bane for appen. Se SynoCommunity eller andre Synology-støttekanaler for hjelp med dette.

## Løse problemet

Hvis det oppstår et migreringsproblem, er det ikke mye du kan gjøre umiddelbart. Hvis problemet er spesifikt for deg (eller det ikke er noen innlegg ennå), kan du opprette et innlegg på [subredditen vår](https://reddit.com/r/lidarr) eller komme innom [discorden vår](https://lidarr.audio/discord). Hvis det er andre med samme problem, kan du være trygg på at vi jobber med det.

> Sørg for at du ikke prøvde å bruke en database fra `nightly`-versjonen på den stabile versjonen. Å bytte mellom grener er ikke anbefalt.{.is-info}

### Tillatelsesproblemer

- Løs tillatelsene slik at brukeren/gruppen som appen kjører som, får tilgang (lese- og skrivetilgang) til både `/tmp` og installasjonsmappen for appen.

- For Synology-brukere som opplever problemer med `/proc/###/maps` vil det å stoppe Sonarr eller de andre \*Arr-appene og oppdatere dem løse dette. Dette er et problem med SynoCommunity-pakken.

### Manuell oppgradering

Last ned den nyeste utgivelsen fra nettstedet vårt.

Installer oppdateringen (.exe) eller pakk ut (.zip) innholdet over den eksisterende installasjonen og kjør Lidarr som du vanligvis ville gjort.

# Nedlastinger og importering

Nedlasting og importering er der *de fleste* opplever problemer. Fra et overordnet perspektiv må Lidarr kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes et stort utvalg av støttede nedlastingsklienter og en enda *større* variasjon av oppsett. Dette betyr at selv om det finnes noen *vanlige* oppsett, finnes det ikke ett *riktig* oppsett, og alle oppsett kan være litt forskjellige.

> **Det første trinnet er å øke loggingen til Trace-nivå. Se [Logging og loggfiler](#logging-og-loggfiler) for detaljer om hvordan du justerer loggingen og søker i loggene. Du vil deretter gjenskape problemet og bruke loggene på Trace-nivå fra den tidsrammen til å undersøke problemet.** Hvis noen hjelper deg, legg kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem. Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet mens oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

Når du ber om hjelp, må du sørge for å lese [be om hjelp](#be-om-hjelp) slik at du kan gi oss de detaljene vi trenger.

## Test nedlastingsklienten

Sørg for at nedlastingsklienten(e) dine kjører. Begynn med å teste nedlastingsklienten. Hvis den ikke fungerer, kan du se detaljer i loggene på Trace-nivå. Du bør finne en URL du kan sette inn i nettleseren din og se om den fungerer. Det kan være et tilkoblingsproblem, som kan indikere feil IP-adresse, vertsnavn, port eller til og med en brannmur som blokkerer tilgangen. Det kan være åpenbart, som et autentiseringsproblem der du har skrevet feil brukernavn, passord eller API-nøkkel.

## Test en nedlasting

Nå skal vi prøve en nedlasting. Velg en sang og gjør et manuelt søk. Velg en av disse filene og prøv å laste den ned. Blir den sendt til nedlastingsklienten? Havner den i riktig kategori? Vises den i Aktivitet? Havner den i loggene på Trace-nivå under oppgavene **Sjekk ferdig nedlasting** (Oppdater overvåkede nedlastinger og Behandle overvåkede nedlastinger) som kjører omtrent hvert minutt? Blir den riktig analysert under den oppgaven? Har den ventende nedlastingen et fornuftig navn? Siden søkene er basert på ID på noen indekserer/sporingsenheter, kan den sette opp en ventende nedlasting med et navn som den ikke kan gjenkjenne.

## Test en import

Importproblemer bør nesten alltid vises som et element i Aktivitet med et oransje ikon du kan sveve over for å se feilen. Hvis de ikke vises i Aktivitet, er dette problemet du må fokusere på først, så gå tilbake og finn ut av det. De fleste importfeil skyldes *tillatelser*, husk at Lidarr må kunne lese og skrive i nedlastingsmappen. Noen ganger kan tillatelser i biblioteksmappen også være årsaken, så sørg for å sjekke begge deler.

Feil med feil sti er også mulig, selv om det er mindre vanlig i normale oppsett. Nøkkelen for å forstå stiproblemer er å vite at får stien til nedlastingen *fra* nedlastingsklienten via API-en. Dette blir et problem i mer unike brukstilfeller, som når nedlastingsklienten kjører på et annet system (kanskje til og med et annet operativsystem\!). Det kan også skje i et Docker-oppsett når volumene ikke er satt opp riktig. En ekstern stibilde er en god løsning der du ikke har kontroll, som for eksempel et seedbox-oppsett. I et Docker-oppsett er det bedre å fikse stiene.

## Vanlige problemer

Her er noen vanlige problemer.

### Nedlastingsklientens WebUI er ikke aktivert

Lidarr kommuniserer med nedlastingsklienten via API-en og får tilgang til den via klientens WebUI. Du må sørge for at nedlastingsklientens WebUI er aktivert, og at porten den bruker ikke kommer i konflikt med andre klientporter som er i bruk eller porter som er i bruk på systemet ditt.

### Bruk av SSL og feil konfigurert

Sørg for at SSL-kryptering ikke er aktivert hvis du bruker både din instans og nedlastingsklienten din i et lokalt nettverk. Se [SSL FAQ-innlegget](/lidarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for mer informasjon.

### Kan ikke se delte mapper på Windows

Standardbrukeren for en Windows-tjeneste er `LocalService`, som vanligvis ikke har tilgang til delte mapper. Rediger tjenesten og sett den opp til å kjøre som din egen bruker. Se FAQ-innlegget [hvorfor kan jeg ikke se filene mine på en ekstern server](/lidarr/faq#why-cant-see-my-files-on-a-remote-server) for detaljer.

### Mappede nettverksstasjoner er ikke pålitelige

Selv om mappede nettverksstasjoner som `X:\` er praktiske, er de ikke like pålitelige som UNC-stier som `\\server\share`, og de er heller ikke tilgjengelige før pålogging. Konfigurer nedlastingsklienten(e) slik at de bruker UNC-stier etter behov. Hvis biblioteket ditt er på en delt mappe, må du sørge for at rotmappene dine bruker UNC-stier. Hvis nedlastingsklienten sender til en delt mappe, må du konfigurere UNC-stier der, siden får nedlastingsstien fra nedlastingsklienten. Det er greit å beholde de mappede nettverksstasjonene for egen bruk, bare ikke bruk dem til automatisering.

### Docker og bruker, gruppe, eierskap, tillatelser og stier

Docker legger til et ekstra lag av kompleksitet som er lett å gjøre feil, men som likevel kan ende opp med et oppsett som fungerer, men har ulike problemer. I stedet for å gå gjennom dem her, les denne wiki-artikkelen [for disse automatiseringsprogrammene og Docker](/docker-guide), som handler om bruker, gruppe, eierskap, tillatelser og stier. Den er ikke spesifikk for et bestemt Docker-system, i stedet går den gjennom ting på et overordnet nivå slik at du kan implementere dem i ditt eget miljø.

### Ekstern stibilde

Hvis du har Lidarr i Docker og nedlastingsklienten utenfor Docker (eller omvendt), eller har programmene på forskjellige servere, kan du trenge et eksternt stibilde.

Loggene vil se slik ut

```none
2022-02-03 14:03:54.3|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /volume3/data/torrents/music/Five Finger Death Punch - F8 (2020) FLAC. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Dermed eksisterer ikke `/volume3/data` i Lidarrs container eller er ikke tilgjengelig.

- [Innstillinger => Nedlastingsklienter => Eksterne stibilder](/lidarr/settings#remote-path-mappings)
- Et eksternt stibilde brukes når nedlastingsklienten din rapporterer en sti for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er et eksternt stibilde bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows, eller omvendt. Et eksternt stibilde kan også være nødvendig hvis du blander Docker- og Native-klienter, eller hvis du bruker en ekstern server.
- Et eksternt stibilde er en DUMB søk/erstatt (hvor den finner VERDIEN FJERN, erstatt den med VERDIEN LOKAL for den angitte verten).
- Hvis feilmeldingen om en ugyldig sti ikke inneholder DEN ERSTATTEDE verdien, fungerer ikke stibildet som du forventer. Den vanlige løsningen er å legge til og fjerne stibildet.
- [Se TRaSHs veiledning for mer informasjon om eksterne stibilder](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-containere, er det sjelden behov for et eksternt stibilde. Det anbefales å [gjennomgå Docker-guiden](/docker-guide) og/eller [følge TRaSHs veiledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Ekstern montering eller ekstern synkronisering (Syncthing)

- Du må sørge for at det synkroniseres hele tiden mens det lastes ned. Og du må sørge for at den lokale synkroniseringsdestinasjonen kan være hardlenker når \*Arr importerer, noe som betyr samme filsystem og ser ut som det.
  - Synkroniser til en lavere, felles mappe som inneholder både ufullstendige og fullførte filer.
  - Synkroniser til en plassering som er på samme filsystem lokalt som biblioteket ditt og ser ut som det (Docker og nettverksdelinger gjør det enkelt å konfigurere dette feil).
  - Du vil synkronisere de ufullstendige og fullførte filene slik at når torrentklienten flytter dem, reflekteres det lokalt, og alle filene er allerede "der" (selv om de fortsatt lastes ned). Deretter vil du bruke hardlenker fordi selv om det importeres før det er ferdig, vil de fortsatt fullføres.
  - På denne måten synkroniseres det hele tiden mens det lastes ned, deretter flytter torrentklienten til undermappen for TV og synkroniseringen reflekterer det. På den måten er nedlastinger stort sett der når de er erklært som ferdige. Og selv om de ikke er helt ferdige, betyr muligheten for hardlenke at det er greit.
  - (Valgfritt - hvis det er aktuelt og/eller nødvendig (f.eks. ekstern Usenet-klient)) Konfigurer et egendefinert skript som skal kjøres ved import/nedlasting/oppgradering for å fjerne den eksterne filen.
- Alternativt er en ekstern montering i stedet for en ekstern synkronisering betydelig mindre komplisert å konfigurere, men vanligvis tregere.
  - Monter den eksterne lagringsenheten med sshfs eller en annen nettverksfilsystemprotokoll.
  - Sørg for at brukeren og gruppen \*Arr er konfigurert til å kjøre med har lese- eller skrivetilgang.
  - Konfigurer et eksternt stibilde for å finne den EKSTERNE stien og erstatte den med den LOKALE ekvivalenten.

### Tillatelser på biblioteksmappen

Loggene vil se slik ut

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/media/music/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Ikke glem å sjekke tillatelser og eierskap for *destinasjonen*. Det er lett å bli opptatt av nedlastingens eierskap og tillatelser, og det er *vanligvis* årsaken til tillatelsesrelaterte problemer, men det *kan* også være destinasjonen. Sjekk at destinasjonsmappen(e) eksisterer. Sjekk om en destinasjonsfil allerede eksisterer eller ikke kan slettes eller flyttes til papirkurven. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres, hardlenkes eller flyttes. Brukeren eller gruppen som kjører Lidarr må kunne lese og skrive i rotmappen.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Du får muligheten til å gjøre dette under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunitys artikkel om tillatelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- For ikke-Windows-brukere: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Tillatelser på nedlastingsmappen

Loggene vil se slik ut

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/downloads/music/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Ikke glem å sjekke tillatelser og eierskap for *kilden*. Det er lett å bli opptatt av destinasjonens eierskap og tillatelser, og det er en *mulig* årsak til tillatelsesrelaterte problemer, men det er vanligvis kilden. Sjekk at kildekatalogen(e) eksisterer. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres/hardlenkes eller kopieres+slettes/flyttes. Brukeren eller gruppen som kjører Lidarr må kunne lese og skrive i nedlastingsmappen.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Du får muligheten til å gjøre dette under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunitys artikkel om tillatelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- For ikke-Windows-brukere: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Nedlastingsmappe og biblioteksmappe er ikke forskjellige mapper

Nedlastingsklienten skal laste ned til en mappe som er tilgjengelig for \*Arr og som ikke er rot-/biblioteksmappen din. Den skal importere fra den separate nedlastingsmappen til biblioteksmappen din. Du skal aldri laste ned direkte til rotmappen din. Du skal heller ikke bruke rotmappen din som nedlastingsklientens fullførte mappe eller ufullstendige mappe.

> Nedlastingsmappen din og rot-/biblioteksmappen din **må** være separate
{.is-warning}

### Feil kategori

Lidarr skal være konfigurert til å bruke en kategori slik at den bare prøver å behandle sine egne nedlastinger. Det er sjelden at en torrent som er sendt inn av blir lagt til uten riktig kategori, men det kan skje. Hvis du legger til torrents manuelt og vil behandle dem, må de ha riktig kategori. Den kan settes når som helst, siden prøver å behandle nedlastinger hvert minutt.

### Pakkede torrents

Loggene vil vise feilmeldinger som

```none
No files found are eligible for import
```

Hvis torrenten din er pakket i `.rar`-filer, må du sette opp utpakking. Vi anbefaler [Unpackerr](https://github.com/unpackerr/unpackerr) fordi det gjør utpakking riktig: forhindrer korrupte delvise importeringer og rydder opp i de utpakkede filene etter importeringen.

Feilen kan også vises hvis det ikke finnes noen gyldig mediefil i mappen.

### Gjentatte nedlastinger

Det er noen årsaker til gjentatte nedlastinger, men en av dem er relatert til begrensningen i indekseringsprofilene. Fordi indekseringen *ikke* lagres sammen med dataene, er alle foretrukne ordpoeng *null* for medier i biblioteket ditt, men under "RSS" og søk blir de brukt. Dette fører til en løkke der du laster ned elementene om og om igjen fordi det ser ut som en oppgradering, deretter ikke er det, deretter dukker opp igjen og ser ut som en oppgradering, deretter ikke er det. Ikke begrens indekseringsprofilen din til en indekserer.

Dette kan også skyldes at nedlastingen faktisk aldri blir importert og deretter mangler fra køen, slik at en ny nedlasting stadig blir lastet ned og aldri importert. Se de ulike andre vanlige problemene og feilsøkingsstegene for dette.

### Usenet-nedlasting blir ikke importert

Lidarr ser bare på de 60 siste nedlastingene i SABnzbd og NZBGet, så hvis du *bevarer* historikken din, betyr dette at under store køer med importproblemer kan nedlastinger bli stillestående og ikke importert. Den beste måten å unngå dette på er å holde historikken ryddig, slik at eventuelle elementer som fortsatt vises, må undersøkes. Du kan oppnå dette ved å aktivere Fjern under Fullførte og mislykkede nedlastingsbehandlere. I NZBGet vil dette flytte elementer til den *skjulte* historikken, noe som er flott. Dessverre har ikke SABnzbd en tilsvarende funksjon. Det beste du kan oppnå der er å bruke nzb-sikkerhetskopimappen.

### Nedlastingsklienten tømmer elementer

Nedlastingsklienten skal *ikke* være ansvarlig for å fjerne nedlastinger. Usenet-klienter bør konfigureres slik at de *ikke* fjerner nedlastinger fra historikken. Torrent-klienter bør settes opp slik at de *ikke* fjerner torrenter når de er ferdig med å seede (pause eller stopp i stedet). Dette er fordi Lidarr kommuniserer med nedlastingsklienten for å vite hva som skal importeres, så hvis de blir *fjernet*, er det ingenting å importere... selv om det er en mappe full av filer.

For SABnzbd håndteres dette med innstillingen for historiebevaring.

### Nedlastingen kan ikke matches med et bibliotekselement

Av ulike årsaker kan utgivelser ikke parses når de er lastet ned og sendt til nedlastingsklienten. Aktivitet => Alternativer => Vis ukjent (dette er nå aktivert som standard i nyere versjoner) vil vise alle elementer som ikke er ignorert / allerede importert innenfor *Arrs nedlastingsklientkategori. Disse må vanligvis kartlegges og importeres manuelt.

Dette kan også skje hvis du har en utgivelse i nedlastingsklienten din, men at medieelementet (film/episode/bok/sang) ikke eksisterer i applikasjonen.

### Forbindelsen ble avbrutt: En uventet feil oppstod under sendingen

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Lidarr => System => Status](/lidarr/system#status).

### Forespørselen ble tidsavbrutt

Lidarr får ingen respons fra klienten.

```none
    System.NET.WebException: Forespørselen ble tidsavbrutt: ’https://eksempel.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Forespørselen ble tidsavbrutt
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke koble til indekser

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En oppgave ble avbrutt.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av VPN
- feil konfigurert eller bruk av proxy
- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

## Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelses- og nettverkstroubleshootingkommandoer [i vår guide](/permissions-and-networking). Ellers kan du diskutere problemet med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

# Søk i indekser og trackere

- Hvis du bruker [Prowlarr](/prowlarr), kan du se [Historikk](/prowlarr/history) over alle henvendelser Prowlarr mottok og hvordan de ble sendt til nettstedene. Sørg for at `Parametere` er aktivert i Prowlarr Historikk => Alternativer. (i)-ikonet gir ytterligere detaljer.

## Skru opp loggingen til sporingsnivå

> **Det første trinnet er å skru opp loggingen til sporingsnivå, se [Logging og loggfiler](#logging-og-loggfiler) for detaljer om hvordan du justerer loggingen og søker i loggene. Deretter gjenskaper du problemet og bruker sporingsnivåloggene fra den tidsrammen til å undersøke problemet.** Hvis noen hjelper deg, legg kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem. Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet mens oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

## Teste en indekser eller tracker

Når du tester en indekser eller tracker, kan du finne URL-en som ble brukt i feilsøkings- eller sporingslogger. Her er et eksempel på en vellykket test, der du kan se at den spør indekseren via en spesifikk URL med spesifikke parametere, og deretter svaret. Du kan teste denne URL-en i nettleseren din ved å erstatte `apikey=(fjernet)` med riktig api-nøkkel, for eksempel `apikey=123`. Du kan eksperimentere med parameterne hvis du får en feil fra indekseren, eller se om du har tilkoblingsproblemer hvis det ikke fungerer i det hele tatt. Etter at du har testet i nettleseren din, bør du teste fra systemet som kjører *hvis* du ikke allerede har gjort det.

## Teste et søk

På samme måte som indekser-/tracker-testen ovenfor, når du utløser et søk mens du har loggingen på Debug eller Trace-nivå, kan du få URL-en som ble brukt fra loggfilene. Under testing er det best å bruke et så smalt søk som mulig. Et manuelt søk er bra fordi det er spesifikt, og du kan se resultatene i brukergrensesnittet mens du undersøker loggene.

I denne testen ser du etter åpenbare feil og kjører noen enkle tester. Du kan se at søket brukte URL-en ***OPPDATERT URL FOR MUSIKK ER NØDVENDIG - DETTE ER ET SONARR URL-EKSEMPEL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(fjernet)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, som du kan prøve selv i en nettleser ved å erstatte (fjernet) med api-nøkkelen din for den indekseren. Fungerer det? Ser du de forventede resultatene? Gjelder denne FAQ-oppføringen? I den URL-en kan du se at den har satt spesifikke kategorier med `cat=5030,5040,5045,5080`, så hvis du ikke ser forventede resultater, er dette en sannsynlig årsak. Du kan også se at den søkte etter tvdbid med `tvdbid=354629`, så hvis episoden ikke er riktig kategorisert på indekseren, må det fikses. Du kan også se at den søker etter en bestemt sesong og episode med season=1 og ep=1, så hvis det ikke er riktig på indekseren, vil du ikke se de resultatene. Se på eksempelet på XML-utdata for manuelt søk nedenfor for å se et eksempel på utdata fra en fungerende forespørsel.

- XML-utdata for manuelt søk

```xml
EKSEMPEL PÅ INDEKSERINGSRESPONS FOR SØK NØDVENDIG
```

***Bilder er nødvendig***

![searches-indexers-and-trackers1.png](/assets/lidarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/lidarr/searches-indexers-and-trackers2.png)

- Sporingsloggutdrag

```none
Utdrag av sporingsloggen for et manuelt søk er nødvendig
```

- Full sporingslogg for et søk

```none
Full seksjon av sporingsloggen for et manuelt søk er nødvendig
```

## Vanlige problemer

Her er noen vanlige problemer.

### Mediet er ikke overvåket

Sangen(e) er ikke overvåket.

### Trackeren trenger RawSearch Caps

- Lidarr søker etter `Kikis leveringstjeneste`, men trackeren din har bare resultater for `Kiki's leveringstjeneste`.
- Dette skyldes at trackeren din ikke støtter normale standardiserte søk.
- Løsningen er at søkefunksjonene i trackerdefinisjonen din må oppdateres for å indikere at den krever og støtter `RawSearch`.
- Jackett støtter flagget, men funksjonene må oppdateres for hver enkelt indekser. Opprett en funksjonsforespørsel for Jackett for å legge til denne funksjonaliteten for indekseren din.
- Prowlarr støtter flagget, men funksjonene må oppdateres for hver enkelt indekser. Opprett en funksjonsforespørsel for Prowlarr for å legge til denne funksjonaliteten for indekseren din.

### Feil kategorier

Feil kategorier er sannsynligvis den vanligste årsaken til at resultater vises i manuelle søk i en indekser/tracker, men *ikke* i . Indekseren/trackeren *bør* vise kategorien i søkeresultatene, noe som bør hjelpe deg med å finne ut hva som mangler. Hvis du bruker Jackett eller Prowlarr, har hver tracker en liste over spesifikt støttede kategorier. Sørg for at du bruker de riktige kategoriene. Mange finner det nyttig å ha listen synlig i ett nettleservindu mens de redigerer oppføringen i .

### Feil resultater

Noen ganger returnerer indekserne helt irrelevante resultater, selv om sender inn parametere for å begrense søket. Eller noen ganger, mest relatert med noen få feilaktige resultater. Den første årsaken er vanligvis et indekserproblem, og du kan se fra sporingsloggene hvilken indekser som forårsaker det. Du kan deaktivere den indekseren og rapportere problemet. Den andre årsaken er vanligvis kategoriserte utgivelser som bør rapporteres til indekseren/trackeren.

### Søk vellykket - Ingen resultater returnert

Du får en melding som ligner på `Søket var vellykket, men ingen resultater ble returnert fra indekseren din. Dette kan være et problem med indekseren eller indekseringskategoriinnstillingene dine.`

Dette skyldes at indekseren din ikke returnerer noen resultater innenfor kategoriene du har konfigurert for indekseren.

### Manglende resultater

Hvis du har resultater på nettstedet som du ikke ser i Lidarr, er problemet sannsynligvis en av flere muligheter:

- [Feil kategorier - Se ovenfor](#feil-kategorier)
- Det blir gjort et ID-basert søk, og indekseren har ikke riktig kartlagt utgivelsene til den ID-en. Dette er noe bare indekseren din kan løse. De må sørge for at utgivelsen er kartlagt til de riktige ID-ene som gjelder.
- Du søker ikke på samme måte som Lidarr; Det er svært sannsynlig at vilkårene du søker på indekseren ikke er hvordan Lidarr spør etter det. Du kan se hvordan Lidarr spør ved å se på sporingsloggene. Tekstbaserte søk vil generelt ha formatet `q=ord%20og%20ting%20her`, denne strengen er HTTP-kodet og kan enkelt dekodes ved hjelp av et hvilket som helst nettbasert verktøy for HTML-koding/avkoding.

### Sertifikatvalidering

Du vil koble til de fleste indekserne/trackerne via https, så du må ha det til å fungere riktig på systemet ditt. Det betyr at tidssonen og tiden din må være satt *riktig*. Det betyr også at systemets sertifikater må være oppdaterte.

### Treffer rategrenser

Hvis du kjører gjennom en VPN eller proxy, kan du konkurrere med 10-talls eller 100-talls eller 1000-talls andre personer som alle prøver å bruke tjenester som , theXEM og/eller indekserne og trackerne dine. Rategrenser og DDOS-beskyttelse blir ofte gjort etter IP-adresse, og VPN-/proxy-utgangspunktet ditt er *én* IP-adresse. Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, trenger du ikke VPN/proxy .

Rarbg har en tendens til å ha en form for rategrense i API-en sin og vises som svar uten resultater.

### IP-blokkering

På samme måte som rategrenser kan visse indeksere - som Nyaa - utestenge en IP-adresse. Dette er vanligvis halvpermanent, og løsningen er å få en ny IP fra Internettleverandøren eller VPN-leverandøren din.

### Bruke Jackett /all-endepunktet

Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan være potensielle problemer, så det er nødvendig å legge til hver enkelt tracker separat. Alternativt kan du sjekke ut Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Selv Jackett sier at /all bør unngås og ikke bør brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)

Å bruke all-endepunktet har ingen fordeler (bortsett fra redusert administrasjonsarbeid), bare ulemper:

- du mister kontrollen over indekser-spesifikke innstillinger (kategorier, søkemåter, osv.)
- blanding av søkemåter (IMDB, spørring, osv.) kan føre til resultater av lav kvalitet
- indekser-spesifikke kategorier (\>= 100000) kan ikke brukes.
- treg indekser vil bremse ned den totale resultatet
- totalt antall resultater er begrenset til 1000

Å legge til hver enkelt indekser separat gjør det mulig å finjustere kategoriene for hver enkelt indekser, noe som kan være et problem med `/all`-endepunktet hvis feil kategori forårsaker feil på noen trackere. I , er hver indekser begrenset til 1000 resultater hvis paginering støttes, eller 100 hvis ikke, noe som betyr at jo flere trackere du legger til i Jackett, desto mer sannsynlig er det at du får avkortede resultater. Til slutt, hvis *en* av trackerne i `/all` returnerer en feil, vil deaktivere den, og nå får du ingen resultater.

### Bruke NZBHydra2 som en enkelt oppføring

Å bruke NZBHydra2 som en enkelt indekseroppføring (dvs. 1 NZBHydra2-oppføring i Lidarr for mange indeksere i NZBHydra2) i stedet for flere (dvs. mange NZBHydra2-oppføringer i Lidarr for mange indeksere i NZBHydra2) har de samme problemene som nevnt ovenfor med Jacketts `/all`-endepunkt.

### Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelses- og nettverkstroubleshootingkommandoer [i vår guide](/permissions-and-networking). Ellers kan du diskutere problemet med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

## Feil

Dette er noen av de vanlige feilene du kan se når du legger til en indekser

### Forbindelsen ble avbrutt: En uventet feil oppstod under sendingen

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Lidarr => System => Status](/lidarr/system#status).

### Forespørselen ble tidsavbrutt

Lidarr får ingen respons fra indekseren.

```none
    System.NET.WebException: Forespørselen ble tidsavbrutt: ’https://eksempel.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Forespørselen ble tidsavbrutt
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke koble til indekser

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En oppgave ble avbrutt.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av VPN
- feil konfigurert eller bruk av proxy
- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

### Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelses- og nettverkstroubleshootingkommandoer [i vår guide](/permissions-and-networking). Ellers kan du diskutere problemet med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.