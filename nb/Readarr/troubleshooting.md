---
title: Readarr Feilsøking
description: 
published: true
date: 2023-07-24T19:54:33.343Z
tags: readarr, feilsøking
editor: markdown
dateCreated: 2021-06-20T20:06:25.552Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Be om hjelp](#be-om-hjelp)
- [Logging og loggfiler](#logging-og-loggfiler)
  - [Standard plassering for logger](#standard-plassering-for-logger)
  - [Plassering for oppdateringslogger](#plassering-for-oppdateringslogger)
  - [Deling av logger](#deling-av-logger)
  - [Trace/Debug-logger](#tracedebug-logger)
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
    - [Du foretrekker ett format, men det ble importert et annet format](#du-foretrekker-ett-format-men-det-ble-importert-et-annet-format)
    - [Nettlesergrensesnittet for nedlastingsklienten er ikke aktivert](#nettlesergrensesnittet-for-nedlastingsklienten-er-ikke-aktivert)
    - [SSL er i bruk og er feilkonfigurert](#ssl-er-i-bruk-og-er-feilkonfigurert)
    - [Kan ikke se delte filer på Windows](#kan-ikke-se-delte-filer-på-windows)
    - [Kartlagte nettverksstasjoner er ikke pålitelige](#kartlagte-nettverksstasjoner-er-ikke-pålitelige)
    - [Docker og bruker, gruppe, eierskap, tillatelser og stier](#docker-og-bruker-gruppe-eierskap-tillatelser-og-stier)
    - [Fjernstyring av sti](#fjernstyring-av-sti)
      - [Fjernmontering eller fjernsynkronisering (Syncthing)](#fjernmontering-eller-fjernsynkronisering-syncthing)
    - [Tillatelser for biblioteksmappen](#tillatelser-for-biblioteksmappen)
    - [Tillatelser for nedlastingsmappen](#tillatelser-for-nedlastingsmappen)
    - [Nedlastingsmappen og biblioteksmappen er ikke forskjellige mapper](#nedlastingsmappen-og-biblioteksmappen-er-ikke-forskjellige-mapper)
    - [Feil kategori](#feil-kategori)
    - [Pakkede torrents](#pakkede-torrents)
    - [Gjentatte nedlastinger](#gjentatte-nedlastinger)
    - [Usenet-nedlasting savner importering](#usenet-nedlasting-savner-importering)
    - [Nedlastingsklienten tømmer elementer](#nedlastingsklienten-tømmer-elementer)
    - [Nedlastingen kan ikke matches med et bibliotekselement](#nedlastingen-kan-ikke-matches-med-et-bibliotekselement)
    - [Tilkoblingstidsavbrudd](#tilkoblingstidsavbrudd)
  - [Problem som ikke er oppført](#problem-som-ikke-er-oppført)
- [Søk, indekser og sporere](#søk-indekser-og-sporere)
  - [Øke loggingen til spor](#øke-loggingen-til-spor)
  - [Teste en indekser eller spor](#teste-en-indekser-eller-spor)
  - [Teste et søk](#teste-et-søk)
  - [Vanlige problemer](#vanlige-problemer-1)
    - [Mediet er ikke overvåket](#mediet-er-ikke-overvåket)
    - [Feil kategorier](#feil-kategorier)
    - [Feil resultater](#feil-resultater)
    - [Vellykket forespørsel - ingen resultater returnert](#vellykket-forespørsel-ingen-resultater-returnert)
    - [Manglende resultater](#manglende-resultater)
    - [Sertifikatvalidering](#sertifikatvalidering)
    - [Treffer grenser for hastighet](#treffer-grenser-for-hastighet)
    - [IP-blokkering](#ip-blokkering)
    - [Bruke Jackett /all-endepunktet](#bruke-jackett-all-endepunktet)
    - [Bruke NZBHydra2 som en enkelt inngang](#bruke-nzbhydra2-som-en-enkelt-inngang)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-1)
  - [Feil](#feil)
    - [The underlying connection was closed: An unexpected error occurred on a send](#the-underlying-connection-was-closed-an-unexpected-error-occurred-on-a-send)
    - [The request timed out](#the-request-timed-out)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-2)

# Be om hjelp

Trenger du hjelp? Det er greit, alle trenger hjelp av og til. Du kan få hjelp i sanntid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Offisiell Readarr Discord*](https://readarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offisiell Readarr Subreddit*](https://reddit.com/r/readarr)
{.links-list}

Men før du går dit og poster, må du sørge for at forespørselen om hjelp er så god som mulig. Beskriv tydelig problemet og gi en kort beskrivelse av oppsettet ditt, inkludert ting som operativsystem/distribusjon, versjon av .NET, versjon av Readarr, nedlastingsklient og versjonen av denne. **Hvis du bruker [Docker](https://www.docker.com/), kjør gjennom [Docker Guide](/docker-guide) først, da dette vil løse vanlige og hyppige problemer med stier og tillatelser. Ellers må du ha en [docker compose](/docker-guide#docker-compose) klar. [Slik genererer du en Docker Compose](https://trash-guides.info/compose)** Fortell oss hva du allerede har prøvd, hva du har sett på. Bruk [Logging og loggfiler](#logging-og-loggfiler) for å øke loggingen til spor, gjenskap problemet, legg relevant kontekst ut på en pastebin og inkluder en lenke til den i innlegget ditt. Kanskje til og med inkluder noen skjermbilder for å illustrere problemet.

Jo mer vi vet, jo enklere er det å hjelpe deg.

# Logging og loggfiler

Det kan være nyttig å også se gjennom vanlige feilsøkingsproblemer:
- [Vanlige problemer med nedlastinger og importering](#vanlige-problemer)
- [Vanlige problemer med søk, indekser og sporere](#vanlige-problemer-1)
{.links-list}

Hvis du blir bedt om feilsøkingslogger, vil loggene dine inneholde `debug`, og hvis du blir bedt om sporingslogger, vil loggene dine inneholde `trace`. Hvis loggene du gir ikke inneholder noen av disse, er de ikke de loggene som er etterspurt.

- Unngå å dele hele loggfilen med mindre du blir bedt om det.
- Ikke last opp logger direkte til Discord eller lim dem inn som tekstblokker, med mindre du blir bedt om det.
- Ikke del loggene som vedlegg, som en zip-fil eller noe annet enn tekst som deles via tjenestene som er nevnt nedenfor.

For å gi gode og nyttige logger for deling:

> Sørg for at det ikke kjører noen spam-oppgave, som for eksempel en RSS-oppdatering
{.is-warning}

1. [Øk loggingen til spor (Innstillinger => Generelt => Loggnivå eller rediger konfigurasjonsfilen)](#tracedebug-logger)
2. [Slett logger (System => Logger => Slett logger eller slett alle logger i loggmappen)](#slette-logger)
3. Gjenskap problemet (Gjør det som forårsaker problemene på nytt)
4. [Åpne sporingsloggen (readarr.trace.txt) via brukergrensesnittet eller loggfilen](#standard-plassering-for-logger) på filsystemet og finn relevant kontekst
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
- **Bare Unix:** Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men ikke er sikker på hvilken du kan bruke grep. Hvis du for eksempel vil finne informasjon om filmen/serien/boken/sangen/indekseren "Shooter", kan du kjøre følgende kommando: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Hvis [Appdata-mappen](/readarr/appdata-directory) din er i hjemmemappen, kan du kjøre: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggene har følgende funksjoner
    * -i: ignorere store/små bokstaver
    * -n: vis linjenummer
    *  -r: søk rekursivt i alle filer i stien
    * -C: gi antall linjer før og etter linjen det er funnet på
    * -e: mønsteret som skal søkes etter

```

## Standard plassering for logger

Loggfilene er plassert i Readarrs [Appdata-mappen](/readarr/appdata-directory), inne i mappen logs/. Du kan også få tilgang til loggfilene fra brukergrensesnittet ved å gå til System => Logger => Filer.

> Merk: Tabellen "Logger" i brukergrensesnittet er ikke det samme som loggfilene og er ikke like nyttig. Hvis du blir bedt om logger, kopier/lim inn fra loggfilene og ikke tabellen.
{.is-info}

## Plassering for oppdateringslogger

Oppdateringsloggfilene er plassert i Readarrs [Appdata-mappen](/readarr/appdata-directory), inne i mappen UpdateLogs/.

## Deling av logger

Loggene kan være lange og vanskelige å lese som en del av et forum- eller Reddit-innlegg, og de er spamaktige i Discord, så bruk [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller lignende pastebin-nettsteder. Hele filen er vanligvis ikke nødvendig, bare en god mengde kontekst fra før og etter problemet/feilen. Ikke glem å vente til spam-oppgaver som en RSS-synkronisering eller biblioteksoppdatering er ferdig.

## Trace/Debug-logger

Du kan endre loggnivået under Innstillinger => Generelt => Logging. Readarr trenger ikke å startes på nytt for at endringen skal tre i kraft. De nyeste debug/sporingsloggfilene har navnene `readarr.debug.txt` og `readarr.trace.txt` henholdsvis.

Hvis du ikke har tilgang til brukergrensesnittet for å angi loggnivået, kan du gjøre det ved å redigere config.xml i AppData-mappen ved å sette LogLevel-verdien til Debug eller Trace i stedet for Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Slette logger

Du kan slette loggfiler og loggdatabasen direkte fra brukergrensesnittet, under System => Logger => Filer og System => Logger => Slett (Søppelbøtteikon)

# Flere loggfiler

Readarr bruker rullerende loggfiler begrenset til 1 MB hver. Den nåværende loggfilen er alltid `readarr.txt`, for de andre filene er `readarr.0.txt` den nest nyeste (jo høyere nummer, jo eldre er den). Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.

Når Debug-loggnivået er aktivert, vil det være tilgjengelige ekstra `readarr.debug.txt`-loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. Den dekker vanligvis en periode på 40 timer.

Når Trace-loggnivået er aktivert, vil det være tilgjengelige ekstra `readarr.trace.txt`-loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsloggenes omfang dekker den bare et par timer.

# Gjenopprette etter en mislykket oppdatering

Vi gjør alt vi kan for å forhindre problemer ved oppgradering, men hvis de likevel oppstår, vil dette veilede deg gjennom trinnene du må ta for å gjenopprette installasjonen din.

## Identifisere problemet

- Det beste stedet å se når programmet ikke starter etter en oppdatering, er å se gjennom [oppdateringsloggene](#plassering-for-oppdateringslogger) og se om oppdateringen ble fullført uten problemer. Hvis det ikke er noen problemer der, er neste steg å se på de vanlige programloggfilene dine. Før du prøver å starte på nytt, bruk [Logging](/readarr/settings#logging) og [Loggfiler](/readarr/system#loggfiler) for å finne dem og øke loggnivået.
- Det mest vanlige problemet er at systemet der appen er installert, har rotet med `/tmp`-mappen og slettet kritiske \*Arr-filer under oppdateringen, noe som fører til at både oppdateringen og tilbakerulling mislykkes. I dette tilfellet installerer du bare på nytt over den eksisterende ødelagte installasjonen.

### Migreringsproblem

- Migreringsfeil vil ikke være identiske, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Tillatelsesproblem

- Tillatelsesproblemer skyldes at programmet ikke kan få tilgang til de relevante midlertidige mappene og/eller appens binærmappe. Løs tillatelsesproblemene slik at brukeren/gruppen som programmet kjører som, har riktig tilgang.

- Synology-brukere kan oppleve denne Synology-feilen `Access to the path '/proc/{noen tall}/maps is denied`

- Synology-brukere kan også oppleve at det er tomt for plass i `/tmp` på visse NAS-er. Du må angi en annen `/tmp`-bane for appen. Se SynoCommunity eller andre Synology-støttekanaler for hjelp med dette.

## Løse problemet

Hvis det oppstår et migreringsproblem, er det ikke mye du kan gjøre umiddelbart. Hvis problemet er spesifikt for deg (eller det ikke er noen innlegg om det ennå), kan du opprette et innlegg på [subredditen vår](https://reddit.com/r/readarr) eller besøke [discorden vår](https://readarr.com/discord). Hvis det er andre med samme problem, kan du være trygg på at vi jobber med det.

> Forsikre deg om at du ikke prøvde å bruke en database fra `nightly`-versjonen på den stabile versjonen. Å bytte mellom versjoner anbefales ikke.{.is-info}

### Tillatelsesproblemer

- Løs tillatelsesproblemene slik at brukeren/gruppen som programmet kjører som, får tilgang (lese- og skrivetilgang) til både `/tmp` og installasjonsmappen til programmet.

- For Synology-brukere som opplever problemer med `/proc/###/maps` vil det å stoppe Sonarr eller de andre \*Arr-applikasjonene og oppdatere dem løse dette. Dette er et problem med SynoCommunity-pakken.

### Manuell oppgradering

Last ned den nyeste utgivelsen fra nettstedet vårt.

Installer oppdateringen (.exe) eller pakk ut (.zip) innholdet over den eksisterende installasjonen og kjør Readarr på vanlig måte.

# Nedlastinger og importering

Nedlasting og importering er der de fleste opplever problemer. Fra et overordnet perspektiv må Readarr kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes et stort utvalg av støttede nedlastingsklienter og en enda større variasjon av oppsett. Dette betyr at selv om det finnes noen vanlige oppsett, finnes det ikke ett riktig oppsett, og alle oppsett kan være litt forskjellige.

> **Det første trinnet er å øke loggingen til Trace-nivå. Se [Logging og loggfiler](#logging-og-loggfiler) for detaljer om hvordan du justerer loggingen og søker i loggene. Du vil deretter gjenskape problemet og bruke loggene på Trace-nivå fra den tidsrammen til å undersøke problemet.** Hvis noen hjelper deg, legg kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem. Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet når oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

Når du ber om hjelp, må du sørge for å lese [spørre om hjelp](#spørre-om-hjelp) slik at du kan gi oss de detaljene vi trenger.

## Test nedlastingsklienten

Sørg for at nedlastingsklienten(e) dine kjører. Begynn med å teste nedlastingsklienten. Hvis den ikke fungerer, kan du se detaljer i loggene på Trace-nivå. Du bør finne en URL du kan sette inn i nettleseren din og se om den fungerer. Det kan være et tilkoblingsproblem, som kan indikere feil IP-adresse, vertsnavn, port eller til og med en brannmur som blokkerer tilgangen. Det kan være åpenbart, som et autentiseringsproblem der du har skrevet feil brukernavn, passord eller API-nøkkel.

## Test en nedlasting

Nå skal vi prøve en nedlasting. Velg en bok og gjør et manuelt søk. Velg en av filene og prøv å laste den ned. Blir den sendt til nedlastingsklienten? Havner den i riktig kategori? Vises den i Aktivitet? Havner den i loggene på Trace-nivå under oppgaven **Sjekk etter ferdig nedlasting**, som kjører omtrent hvert minutt? Blir den riktig analysert under den oppgaven? Har den nedlastede filen en fornuftig navn? Siden søkene er basert på ID på noen indekserer/sporere, kan den sette opp en nedlasting med et navn den ikke kan gjenkjenne.

## Test en importering

Problemer med importering bør nesten alltid vises som en post i Aktivitet med et oransje ikon du kan sveve over for å se feilen. Hvis de ikke vises i Aktivitet, er dette problemet du må fokusere på først, så gå tilbake og finn ut av det. De fleste importeringsfeil skyldes *tillatelser*, husk at Readarr må kunne lese og skrive i nedlastingsmappen. Noen ganger kan tillatelser i biblioteksmappen også være problemet, så sørg for å sjekke begge deler.

Feil i sti er også mulig, selv om det er mindre vanlig i normale oppsett. Nøkkelen for å forstå problemene med stier er å vite at Readarr får stien til nedlastingen *fra* nedlastingsklienten via API-en. Dette kan bli et problem i mer unike tilfeller, som når nedlastingsklienten kjører på et annet system (kanskje til og med et annet operativsystem\!). Det kan også skje i et Docker-oppsett når volumene ikke er konfigurert riktig. En ekstern stistavle er en god løsning der du ikke har kontroll, for eksempel i et seedbox-oppsett. I et Docker-oppsett er det bedre å fikse stiene.

## Vanlige problemer

Her er noen vanlige problemer.

### Du foretrekker ett format, men det ble importert et annet format

Når Readarr importerer, importerer den i rekkefølgen du har satt opp i kvalitetsprofilen din, uavhengig av om de er merket av eller ikke. For å løse dette problemet må du dra de merkede formatene til toppen av kvalitetslisten. For eksempel, i alternativene nedenfor, selv om bare EPUB er ønsket, hvis nedlastingen inneholder en AZW3 sammen med EPUB, vil den bli importert med høyere prioritet enn EPUB, noe som fører til at uønskede formater blir importert.

![qualities.png](/assets/readarr/qualities.png)

### Nedlastingsklientens WebUI er ikke aktivert

Readarr kommuniserer med nedlastingsklienten via API-en og får tilgang til den via klientens WebUI. Du må sørge for at nedlastingsklientens WebUI er aktivert, og at porten den bruker ikke kommer i konflikt med andre klientporter som er i bruk eller porter som er i bruk på systemet ditt.

### Feil konfigurert SSL-bruk

Sørg for at SSL-kryptering ikke er aktivert hvis du bruker både Readarr-instansen og nedlastingsklienten på et lokalt nettverk. Se [SSL-FAQ-posten](/readarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for mer informasjon.

### Kan ikke se delte mapper på Windows

Standardbrukeren for en Windows-tjeneste er `LocalService`, som vanligvis ikke har tilgang til delte mapper. Rediger tjenesten og sett den opp til å kjøre som din egen bruker. Se FAQ-posten [why can’t see my files on a remote server](/readarr/faq#why-cant-i-see-my-files-on-a-remote-server) for detaljer.

### Mappede nettverksstasjoner er ikke pålitelige

Selv om mappede nettverksstasjoner som `X:\` er praktiske, er de ikke like pålitelige som UNC-stier som `\\server\share`, og de er heller ikke tilgjengelige før pålogging. Konfigurer nedlastingsklienten(e) slik at de bruker UNC-stier etter behov. Hvis biblioteket ditt er på en delt mappe, må du sørge for at rotmappene dine bruker UNC-stier. Hvis nedlastingsklienten sender til en delt mappe, må du konfigurere UNC-stier der, siden Readarr får nedlastingsstien fra nedlastingsklienten. Det er greit å beholde de mappede nettverksstasjonene for egen bruk, bare ikke bruk dem til automatisering.

### Docker og bruker, gruppe, eierskap, tillatelser og stier

Docker legger til et ekstra lag av kompleksitet som er lett å gjøre feil, men likevel ende opp med et oppsett som fungerer, men har ulike problemer. I stedet for å gå gjennom dem her, les denne wiki-artikkelen [for disse automatiseringsprogrammene og Docker](/docker-guide), som handler om bruker, gruppe, eierskap, tillatelser og stier. Den er ikke spesifikk for et bestemt Docker-system, i stedet går den gjennom ting på et overordnet nivå slik at du kan implementere dem i ditt eget miljø.

### Ekstern stistavle

Hvis du har Readarr i Docker og nedlastingsklienten utenfor Docker (eller omvendt), eller har programmene på forskjellige servere, kan du trenge en ekstern stistavle.

Loggene vil se slik ut

```none
2022-02-03 14:03:54.3|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /volume3/data/torrents/audiobooks/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Dermed eksisterer ikke `/volume3/data` i Readarrs konteiner eller er ikke tilgjengelig.

- [Innstillinger => Nedlastingsklienter => Ekstern stistavle](/readarr/settings#remote-path-mappings)
- En ekstern stistavle brukes når nedlastingsklienten rapporterer en sti for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er en ekstern stistavle bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows, eller omvendt. En ekstern stistavle kan også være nødvendig hvis du blander Docker- og Native-klienter, eller hvis du bruker en ekstern server.
- En ekstern stistavle er en enkel søk/erstatt-operasjon (der den finner VERDIEN FJERN, erstatter den med VERDIEN LOKAL for den angitte verten).
- Hvis feilmeldingen om en ugyldig sti ikke inneholder den ERSTATTEDE verdien, fungerer ikke stistavlen som forventet. Den vanlige løsningen er å legge til og fjerne stistavlen.
- [Se TRaSHs opplæring for mer informasjon om ekstern stistavle](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-konteinere, er det sjelden behov for en ekstern stistavle. Det anbefales å [gjennomgå Docker-guiden](/docker-guide) og/eller [følge TRaSHs opplæring](https://trash-guides.info/hardlinks)
{.is-info}

#### Ekstern montering eller ekstern synkronisering (Syncthing)

- Du må sørge for at det synkroniseres hele tiden mens det lastes ned. Og du må sørge for at den lokale synkroniseringsdestinasjonen kan være hardlenker når \*Arr importerer, noe som betyr at den må være på samme filsystem og se ut som det.
  - Synkroniser til en lavere, felles mappe som inneholder både ufullstendige og fullførte filer.
  - Synkroniser til en plassering som er på samme filsystem lokalt som biblioteket ditt og ser ut som det (Docker og nettverksdelinger gjør det enkelt å konfigurere feil).
  - Du vil synkronisere ufullstendige og fullførte filer slik at når torrentklienten flytter dem, blir det gjenspeilet lokalt, og alle filene er allerede "der" (selv om de fortsatt lastes ned). Deretter vil du bruke hardlenker, fordi selv om de blir importert før de er ferdige, vil de fortsatt fullføres.
  - På denne måten synkroniseres det hele tiden mens det lastes ned, deretter flytter torrentklienten til undermapper for bøker, og synkroniseringen gjenspeiler det. På den måten er nedlastingen stort sett ferdig når den er erklært som fullført. Og selv om de ikke er helt ferdige, betyr muligheten for hardlenker at det er greit.
  - (Valgfritt - hvis det er aktuelt og/eller nødvendig (f.eks. ekstern Usenet-klient)) Konfigurer et tilpasset skript som skal kjøres ved importering/nedlasting/oppgradering for å fjerne den eksterne filen.
- Alternativt er en ekstern montering i stedet for en ekstern synkronisering betydelig mindre komplisert å konfigurere, men vanligvis tregere.
  - Monter den eksterne lagringsplassen med sshfs eller en annen nettverksfilsystemprotokoll.
  - Sørg for at brukeren og gruppen \*Arr er konfigurert til å kjøre som har lese- eller skrivetilgang.
  - Konfigurer en ekstern stistavle for å finne den EKSTERNE stien og erstatte den med den LOKALE ekvivalenten.

### Tillatelser på biblioteksmappen

Loggene vil se slik ut

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/media/books/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Ikke glem å sjekke tillatelser og eierskap for *destinasjonen*. Det er lett å bli fokusert på nedlastingens eierskap og tillatelser, og det er *vanligvis* årsaken til tillatelsesrelaterte problemer, men det *kan* også være destinasjonen. Sjekk at destinasjonsmappen(e) eksisterer. Sjekk om en destinasjonsfil allerede eksisterer eller ikke kan slettes eller flyttes til papirkurven. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres, hardlenkes eller flyttes. Brukeren eller gruppen som kjører Readarr må kunne lese og skrive i rotmappen.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Du får muligheten til å gjøre dette under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunitys artikkel om tillatelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- For ikke-Windows-brukere: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Tillatelser på nedlastingsmappen

Loggene vil se slik ut

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/torrents/books/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Ikke glem å sjekke tillatelser og eierskap for *kilden*. Det er lett å bli fokusert på destinasjonens eierskap og tillatelser, og det er en *mulig* årsak til tillatelsesrelaterte problemer, men det er vanligvis kilden. Sjekk at kildekatalogen(e) eksisterer. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres/hardlenkes eller kopieres+slettes/flyttes. Brukeren eller gruppen som kjører Readarr må kunne lese og skrive i nedlastingsmappen.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Du får muligheten til å gjøre dette under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunitys artikkel om tillatelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- For ikke-Windows-brukere: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Nedlastingsmappen og biblioteksmappen er ikke forskjellige mapper

Nedlastingsklienten skal laste ned til en mappe som er tilgjengelig for \*Arr og som ikke er rot-/biblioteksmappen din. Den skal importere fra den separate nedlastingsmappen til biblioteksmappen din.

Du bør aldri laste ned direkte til rotmappen din. Du bør heller ikke bruke rotmappen din som nedlastingsklientens fullførte mappe eller ufullstendige mappe.

> Nedlastingsmappen din og rot-/biblioteksmappen din **må** være separate
{.is-warning}

### Feil kategori

Readarr skal være konfigurert til å bruke en kategori slik at den bare prøver å behandle sine egne nedlastinger. Det er sjelden at en torrent som er sendt inn av blir lagt til uten riktig kategori, men det kan skje. Hvis du legger til torrents manuelt og vil behandle dem, må de ha riktig kategori. Kategorien kan settes når som helst, siden Readarr prøver å behandle nedlastinger hvert minutt.

### Pakkede torrents

Loggene vil vise feilmeldinger som

```none
No files found are eligible for import
```

Hvis torrenten din er pakket i `.rar`-filer, må du sette opp utpakking. Vi anbefaler [Unpackerr](https://github.com/unpackerr/unpackerr), da det gjør utpakking riktig: forhindrer korrupte delvise importeringer og rydder opp i de utpakkede filene etter importering.

Feilen kan også vises hvis det ikke finnes noen gyldig mediefil i mappen.

### Gjentatte nedlastinger

Det er noen årsaker til gjentatte nedlastinger, men en av dem er relatert til begrensningen i indekseringskildene i utgivelsesprofilene. Fordi indekseringskilden *ikke* lagres sammen med dataene, er alle foretrukne ordkarakterer *null* for medier i biblioteket ditt, men under "RSS" og søk blir de brukt. Dette fører til en løkke der du laster ned elementene om og om igjen fordi det ser ut som en oppgradering, deretter ikke, deretter dukker den opp igjen og ser ut som en oppgradering, deretter ikke. Ikke begrens utgivelsesprofilen din til en indekseringskilde.

Dette kan også skyldes at nedlastingen faktisk aldri blir importert og deretter mangler i køen, slik at en ny nedlasting stadig blir lastet ned og aldri importert. Se de ulike andre vanlige problemene og feilsøkingsstegene for dette.

### Usenet-nedlasting går glipp av importering

Readarr ser kun på de 60 nyeste nedlastningene i SABnzbd og NZBGet, så hvis du beholder historikken din betyr det at under store køer med importproblemer kan nedlastinger bli oversett og ikke importert. Den beste måten å unngå dette på er å holde historikken din ryddig, slik at eventuelle elementer som fortsatt vises, må undersøkes. Du kan oppnå dette ved å aktivere "Fjern" under "Fullførte og mislykkede nedlastinger". I NZBGet vil dette flytte elementer til den *skjulte* historikken, noe som er flott. Dessverre har ikke SABnzbd en lignende funksjon. Det beste du kan oppnå der er å bruke nzb-sikkerhetskopimappen.

### Fjerning av elementer fra nedlastingsklienten

Nedlastingsklienten bør *ikke* være ansvarlig for å fjerne nedlastinger. Usenet-klienter bør konfigureres slik at de *ikke* fjerner nedlastinger fra historikken. Torrent-klienter bør settes opp slik at de *ikke* fjerner torrents når de er ferdig med å seede (pause eller stopp i stedet). Dette er fordi Readarr kommuniserer med nedlastingsklienten for å vite hva som skal importeres, så hvis de blir *fjernet*, er det ingenting å importere... selv om det er en mappe full av filer.

For SABnzbd håndteres dette med innstillingen for historikklagring.

### Nedlastingen kan ikke matches til et bibliotekselement

Av ulike årsaker kan utgivelser ikke analyseres når de er lastet ned og sendt til nedlastingsklienten. Aktivitet => Alternativer => Vis ukjent (dette er nå aktivert som standard i nyere versjoner) vil vise alle elementer som ikke er ignorert / allerede importert innenfor \*Arr's nedlastingsklientkategori. Disse må vanligvis kartlegges og importeres manuelt.

Dette kan også skje hvis du har en utgivelse i nedlastingsklienten din, men det medieelementet (film/episode/bok/sang) eksisterer ikke i applikasjonen.

### Forbindelsen ble avbrutt: En uventet feil oppstod under sendingen

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Readarr => System => Status](/readarr/system#status).

### Forespørselen tidsavbrutt

Readarr får ingen respons fra klienten.

```none
    System.NET.WebException: Forespørselen tidsavbrutt: ’https://eksempel.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Forespørselen tidsavbrutt
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke koble til indekser

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En oppgave ble avbrutt.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av VPN
- feil konfigurert eller bruk av proxy
- lokale DNS-problemer
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

## Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelser og nettverksfeilsøkingskommandoer [i vår guide](/permissions-and-networking). Ellers kan du diskutere det med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

# Søk i indekser og trackere

- Hvis du bruker [Prowlarr](/prowlarr), kan du se [Historikk](/prowlarr/history) over alle forespørsler Prowlarr mottok og hvordan de ble sendt til nettstedene. Sørg for at `Parametere` er aktivert i Prowlarr Historikk => Alternativer. (i)-ikonet gir ytterligere detaljer.

## Øk loggingen til sporingsnivå

> **Det første trinnet er å øke loggingen til sporingsnivå, se [Logging og loggfiler](#logging-og-loggfiler) for detaljer om hvordan du justerer loggingen og søker i loggene. Du vil deretter gjenskape problemet og bruke sporingsnivåloggene fra den tidsrammen til å undersøke problemet.** Hvis noen hjelper deg, legg kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem det. Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet mens oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

## Test av en indekser eller tracker

Når du tester en indekser eller tracker, kan du finne URL-en som ble brukt i feilsøkings- eller sporingslogger. Et eksempel på en vellykket test er nedenfor, der du kan se at den spør indekseren via en spesifikk URL med spesifikke parametere, og deretter responsen. Du kan teste denne URL-en i nettleseren din ved å erstatte `apikey=(fjernet)` med riktig api-nøkkel som `apikey=123`. Du kan eksperimentere med parameterne hvis du får en feil fra indekseren, eller se om du har tilkoblingsproblemer hvis det ikke fungerer i det hele tatt. Etter at du har testet i nettleseren din, bør du teste fra systemet som kjører *hvis* du ikke allerede har gjort det.

## Test av et søk

På samme måte som indekser-/tracker-testen ovenfor, når du utløser et søk mens du har logging på nivået Debug eller Trace, kan du få URL-en som ble brukt fra loggfilene. Under testing er det best å bruke et så smalt søk som mulig. Et manuelt søk er bra fordi det er spesifikt, og du kan se resultatene i brukergrensesnittet samtidig som du undersøker loggene.

I denne testen ser du etter åpenbare feil og kjører noen enkle tester. Du kan se at søket brukte URL-en ***OPPDATERT URL FOR BOK ER NØDVENDIG - DETTE ER ET SONARR URL-EKSEMPEL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(fjernet)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, som du kan prøve selv i en nettleser etter å ha erstattet (fjernet) med api-nøkkelen din for den indekseren. Fungerer det? Ser du de forventede resultatene? Gjelder denne FAQ-oppføringen? I den URL-en kan du se at den har spesifikke kategorier med `cat=5030,5040,5045,5080`, så hvis du ikke ser forventede resultater, er dette en sannsynlig årsak. Du kan også se at den søkte etter tvdbid med `tvdbid=354629`, så hvis episoden ikke er riktig kategorisert på indekseren, må det fikses. Du kan også se at den søkte etter en bestemt sesong og episode med season=1 og ep=1, så hvis det ikke er riktig på indekseren, vil du ikke se de resultatene. Se på eksemplet for XML-utdata for manuelt søk nedenfor for å se et eksempel på utdata fra en fungerende forespørsel.

- XML-utdata for manuelt søk

```xml
EKSEMPEL PÅ INDEKSER-SØKERESULTAT NØDVENDIG
```

***Bilder er nødvendig***

![searches-indexers-and-trackers1.png](/assets/readarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/readarr/searches-indexers-and-trackers2.png)

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

Boken(e) er ikke overvåket.

### Feil kategorier

Feil kategorier er sannsynligvis den vanligste årsaken til at resultater vises i manuelle søk på en indekser/tracker, men *ikke* i . Indekseren/trackeren *bør* vise kategorien i søkeresultatene, noe som bør hjelpe deg med å finne ut hva som mangler. Hvis du bruker Jackett eller Prowlarr, har hver tracker en liste over spesifikt støttede kategorier. Sørg for at du bruker de riktige for kategoriene. Mange finner det nyttig å ha listen synlig i ett nettleservindu mens de redigerer oppføringen i .

### Feil resultater

Noen ganger returnerer indekserne helt irrelevante resultater, Readarr sender inn parametere for å begrense søket, men resultatene som returneres er helt irrelevante. Eller noen ganger, mest relatert med noen få feilaktige resultater. Den første årsaken er vanligvis et indekserproblem, og du kan se fra sporingsloggene hvilken indekser som forårsaker det. Du kan deaktivere den indekseren og rapportere problemet. Den andre årsaken er vanligvis kategoriserte utgivelser som bør kunne rapporteres til indekseren/trackeren.

### Søk vellykket - Ingen resultater returnert

Du får en melding som ligner på `Søket var vellykket, men ingen resultater ble returnert fra indekseren din. Dette kan være et problem med indekseren eller innstillingene for indekserkategoriene dine.`

Dette skyldes at indekseren din ikke returnerer noen resultater som er innenfor kategoriene du har konfigurert for indekseren.

### Manglende resultater

Hvis du har resultater på nettstedet som du finner, men som ikke vises i Readarr, er problemet sannsynligvis en av flere muligheter:

- [Kategoriene er feil - se ovenfor](#feil-kategorier)
- Det blir gjort et ID-basert søk, og indekseren har ikke riktig kartlagt utgivelsene til den ID-en. Dette er noe bare indekseren din kan løse. De må sørge for at utgivelsen er kartlagt til de riktige gjeldende ID-ene.
- Du søker ikke på samme måte som Readarr søker; Det er svært sannsynlig at vilkårene du søker etter på indekseren ikke er hvordan Readarr spør etter det. Du kan se hvordan Readarr spør ved å se på sporingsloggene. Tekstbaserte søk vil generelt ha formatet `q=ord%20og%20ting%20her`, denne strengen er HTTP-kodet og kan enkelt dekodes ved hjelp av et hvilket som helst HTML-kodings-/dekodingverktøy på nettet.

### Sertifikatvalidering

Du vil koble til de fleste indekserne/trackerne via https, så du må ha det til å fungere skikkelig på systemet ditt. Det betyr at tidssonen og tiden din må være satt *riktig*. Det betyr også at systemets sertifikater må være oppdaterte.

### Treffet rategrenser

Hvis du kjører gjennom en VPN eller proxy, kan du konkurrere med 10-talls eller 100-talls eller 1000-talls andre mennesker som alle prøver å bruke tjenester som , theXEM og/eller indekserne og trackerne dine. Rategrenser og DDOS-beskyttelse blir ofte gjort etter IP-adresse, og VPN-/proxy-utgangspunktet ditt er *én* IP-adresse. Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, trenger du ikke VPN/proxy .

Rarbg har en tendens til å ha en form for rategrense i API-en sin og vises som svar uten resultater.

### IP-blokkering

På samme måte som rategrenser kan visse indeksere - som Nyaa - utestenge en IP-adresse. Dette er vanligvis halvpermanent, og løsningen er å få en ny IP fra Internettleverandøren eller VPN-leverandøren din.

### Bruk av Jackett /all-endepunktet

Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet er potensielle problemer, så det kreves at hver tracker legges til individuelt. Alternativt kan du sjekke ut Jackett- og NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Selv Jackett sier at /all bør unngås og ikke bør brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)

Å bruke all-endepunktet har ingen fordeler (bortsett fra redusert administrasjonsarbeid), bare ulemper:

- du mister kontrollen over indekser-spesifikke innstillinger (kategorier, søkemåter, osv.)
- blanding av søkemåter (IMDB, spørring, osv.) kan føre til resultater av lav kvalitet
- indekser-spesifikke kategorier (\>= 100000) kan ikke brukes.
- treg indekser vil bremse ned den totale resultatet
- totalt antall resultater er begrenset til 1000

Ved å legge til hver indekser separat, kan du finjustere kategoriene for hver indekser, noe som kan være et problem med `/all`-endepunktet hvis feil kategori forårsaker feil på noen trackere. I , er hver indekser begrenset til 1000 resultater hvis paginering støttes, eller 100 hvis ikke, noe som betyr at jo flere trackere du legger til i Jackett, desto mer sannsynlig er det at du får færre resultater. Til slutt, hvis *en* av trackerne i `/all` returnerer en feil, vil deaktivere den, og nå får du ingen resultater.

### Bruk av NZBHydra2 som en enkelt oppføring

Å bruke NZBHydra2 som en enkelt indekseroppføring (dvs. 1 NZBHydra2-oppføring i Readarr for mange indeksere i NZBHydra2) i stedet for flere (dvs. mange NZBHydra2-oppføringer i Readarr for mange indeksere i NZBHydra2) har de samme problemene som nevnt ovenfor med Jacketts `/all`-endepunkt.

### Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelser og nettverksfeilsøkingskommandoer [i vår guide](/permissions-and-networking). Ellers kan du diskutere det med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

## Feil

Dette er noen av de vanlige feilene du kan se når du legger til en indekser

### Forbindelsen ble avbrutt: En uventet feil oppstod under sendingen

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Readarr => System => Status](/readarr/system#status).

### Forespørselen tidsavbrutt

Readarr får ingen respons fra indekseren.

```none
    System.NET.WebException: Forespørselen tidsavbrutt: ’https://eksempel.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Forespørselen tidsavbrutt
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke koble til indekser

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En oppgave ble avbrutt.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av VPN
- feil konfigurert eller bruk av proxy
- lokale DNS-problemer
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

### Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelser og nettverksfeilsøkingskommandoer [i vår guide](/permissions-and-networking). Ellers kan du diskutere det med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.