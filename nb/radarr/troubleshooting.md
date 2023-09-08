---
title: Radarr Feilsøking
description: Feilsøking for Radarr, inkludert hvordan du får loggfiler, feilsøking av søk og vanlige problemer, og feilsøking og vanlige problemer med nedlasting/importering
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, feilsøking
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
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
    - [Database disk image is malformed](#database-disk-image-is-malformed)
    - [Migrasjonsproblem](#migrasjonsproblem)
    - [UI-migrasjonsproblemer](#ui-migrasjonsproblemer)
    - [Tillatelsesproblem](#tillatelsesproblem)
  - [Løse problemet](#løse-problemet)
    - [Migrasjonsproblemer](#migrasjonsproblemer)
    - [Tillatelsesproblemer](#tillatelsesproblemer)
    - [Manuell oppgradering](#manuell-oppgradering)
- [Nedlastinger og importering](#nedlastinger-og-importering)
  - [Teste nedlastingsklienten](#teste-nedlastingsklienten)
  - [Teste en nedlasting](#teste-en-nedlasting)
  - [Teste en importering](#teste-en-importering)
  - [Vanlige problemer](#vanlige-problemer)
    - [Nedlastingsklientens WebUI er ikke aktivert](#nedlastingsklientens-webui-er-ikke-aktivert)
    - [Feil konfigurert SSL](#feil-konfigurert-ssl)
    - [Kan ikke se deling på Windows](#kan-ikke-se-deling-på-windows)
    - [Kartlagte nettverksstasjoner er ikke pålitelige](#kartlagte-nettverksstasjoner-er-ikke-pålitelige)
    - [Docker og bruker, gruppe, eierskap, tillatelser og stier](#docker-og-bruker-gruppe-eierskap-tillatelser-og-stier)
    - [Fjernsti-kartlegging](#fjernsti-kartlegging)
      - [Fjernmontering eller fjernsynkronisering (Syncthing)](#fjernmontering-eller-fjernsynkronisering-syncthing)
    - [Tillatelser for biblioteksmappen](#tillatelser-for-biblioteksmappen)
    - [Tillatelser for nedlastingsmappen](#tillatelser-for-nedlastingsmappen)
    - [Nedlastingsmappe og biblioteksmappe er ikke forskjellige mapper](#nedlastingsmappe-og-biblioteksmappe-er-ikke-forskjellige-mapper)
    - [Feil kategori](#feil-kategori)
    - [Pakkede torrents](#pakkede-torrents)
    - [Gjentatte nedlastinger](#gjentatte-nedlastinger)
    - [Usenet-nedlasting savner importering](#usenet-nedlasting-savner-importering)
    - [Nedlastingsklient tømmer elementer](#nedlastingsklient-tømmer-elementer)
    - [Nedlastingen kan ikke matches med et bibliotekselement](#nedlastingen-kan-ikke-matches-med-et-bibliotekselement)
    - [Tilkoblingstidsavbrudd](#tilkoblingstidsavbrudd)
  - [Problem som ikke er oppført](#problem-som-ikke-er-oppført)
- [Søk, indekser og sporere](#søk-indekser-og-sporere)
  - [Øke loggingen til spor](#øke-loggingen-til-spor)
  - [Teste en indekser eller spor](#teste-en-indekser-eller-spor)
  - [Teste et søk](#teste-et-søk)
  - [Vanlige problemer](#vanlige-problemer-1)
    - [Sporer krever RawSearch Caps](#sporer-krever-rawsearch-caps)
    - [Medie er ikke overvåket](#medie-er-ikke-overvåket)
    - [Feil kategorier](#feil-kategorier)
    - [Vellykket søk - ingen resultater returnert](#vellykket-søk-ingen-resultater-returnert)
    - [Feil resultater](#feil-resultater)
    - [Manglende resultater](#manglende-resultater)
    - [Sertifikatvalidering](#sertifikatvalidering)
    - [Treffer rategrenser](#treffer-rategrenser)
    - [IP-blokkering](#ip-blokkering)
    - [År stemmer ikke overens](#år-stemmer-ikke-overens)
    - [Manglende år](#manglende-år)
    - [Bruke Jackett /all-endepunktet](#bruke-jackett-all-endepunktet)
    - [Bruke NZBHydra2 som enkeltinngang](#bruke-nzbhydra2-som-enkeltinngang)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-1)
  - [Feil](#feil)
    - [The underlying connection was closed: An unexpected error occurred on a send](#the-underlying-connection-was-closed-an-unexpected-error-occurred-on-a-send)
    - [The request timed out](#the-request-timed-out)
    - [Problem som ikke er oppført](#problem-som-ikke-er-oppført-2)

# Be om hjelp

Trenger du hjelp? Det er greit, alle trenger hjelp av og til. Du kan få hjelp i sanntid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Offisiell Radarr Discord*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offisiell Radarr Subreddit*](https://reddit.com/r/radarr)
{.links-list}

Men før du går dit og legger ut spørsmålet ditt, må du sørge for at forespørselen om hjelp er så god som mulig. Beskriv tydelig problemet og gi en kort beskrivelse av oppsettet ditt, inkludert ting som operativsystem/distribusjon, versjon av .NET, versjon av Radarr, nedlastingsklient og versjonen av denne. **Hvis du bruker [Docker](https://www.docker.com/), må du først gå gjennom [Docker Guide](/docker-guide) da dette vil løse vanlige og gjentatte problemer med stier/tillatelser. Ellers bør du ha en [docker compose](/docker-guide#docker-compose) klar. [Slik genererer du en Docker Compose](https://trash-guides.info/compose)** Fortell oss hva du allerede har prøvd, hva du har sett på. Bruk [Logging og loggfiler](#logging-og-loggfiler) for å øke loggingen til spor, gjenskap problemet, legg relevant kontekst på en pastebin og inkluder en lenke til den i innlegget ditt. Du kan til og med inkludere noen skjermbilder for å fremheve problemet.

Jo mer vi vet, jo enklere er det å hjelpe deg.

# Logging og loggfiler

Det kan være nyttig å også se gjennom vanlige feilsøkingsproblemer:
- [Vanlige problemer med nedlastinger og importering](#vanlige-problemer)
- [Vanlige problemer med søk, indekser og sporere](#vanlige-problemer-1)
{.links-list}

Hvis du blir bedt om feilsøkingslogger, vil loggene dine inneholde `debug`, og hvis du blir bedt om sporingslogger, vil loggene dine inneholde `trace`. Hvis loggene du gir ikke inneholder noen av disse, er de ikke de etterspurte loggene.

- Unngå å dele hele loggfilen med mindre du blir bedt om det.
- Ikke last opp logger direkte til Discord eller lim dem inn som tekstvegger, med mindre du blir bedt om det.
- Ikke del loggene som vedlegg, zip-arkiv eller noe annet enn tekst som deles via tjenestene som er nevnt nedenfor.

For å gi gode og nyttige logger for deling:

> Sørg for at det ikke kjører noen spam-oppgave, som for eksempel en RSS-oppdatering
{.is-warning}

1. [Øk loggingen til spor (Innstillinger => Generelt => Loggnivå eller rediger konfigurasjonsfilen)](#tracedebug-logger)
2. [Slett logger (System => Logger => Slett logger eller slett alle logger i loggmappen)](#slette-logger)
3. Gjenskap problemet (Gjør det som forårsaker problemene på nytt)
4. [Åpne sporingsloggfilen (radarr.trace.txt) via brukergrensesnittet eller loggfilen](#standard-plassering-for-logger) på filsystemet og finn relevant kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del etter problemet.
6. Bruk [Gist](https://gist.github.com/), [0bin (**Sørg for å deaktivere fargelegging**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) eller lignende nettsteder - unntatt de som er nevnt nedenfor - for å dele de kopierte loggene ovenfor

**Advarsler:**
- **Ikke bruk [pastebin.com](https://pastebin.com) da filtrene deres har en tendens til å blokkere loggene.
- Ikke bruk [pastebin.pl](https://pastebin.pl) da nettstedet deres ofte ikke er tilgjengelig.
- Ikke bruk [JustPasteIt](https://justpaste.it/) da nettstedet deres ikke er egnet for gjennomgang av logger.
- Ikke last opp loggen din som en fil.
- Ikke last opp og del loggene dine via Google Drive, Dropbox eller noen andre nettsteder som ikke er nevnt ovenfor.
- Ikke arkiver (zip, tar (tarball), 7zip, osv.) loggene dine.
- Ikke del konsollutdata, utdata fra Docker-container eller noe annet enn de spesifiserte applikasjonsloggene.

**Viktig merknad:**
- Når du bruker [0bin](https://0bin.net/), må du sørge for å deaktivere fargelegging og ikke brenne etter lesing.

- Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men ikke er sikker på hvilken du skal bruke, kan du bruke N++. Du kan bruke Notepad++-funksjonen "Søk i filer" for å søke i gamle loggfiler etter behov.
- **Bare Unix:** Alternativt, hvis du leter etter en bestemt oppføring i en gammel loggfil, men ikke er sikker på hvilken du skal bruke, kan du bruke grep. Hvis du for eksempel vil finne informasjon om filmen/serien/boken/sangen/indeksen "Shooter", kan du kjøre følgende kommando: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Hvis [Appdata-katalogen](/radarr/appdata-directory) din er i hjemmemappen din, kan du kjøre: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flaggene har følgende funksjoner
    * -i: ignorere store/små bokstaver
    * -n: vise linjenummer
    * -r: søke rekursivt i alle filer i banen
    * -C: gi antall linjer før og etter linjen det er funnet på
    * -e: mønsteret som skal søkes etter

```

## Standard plassering for logger

Loggfilene er plassert i Radarr sin [Appdata-katalog](/radarr/appdata-directory), inne i mappen logs/. Du kan også få tilgang til loggfilene fra brukergrensesnittet ved å gå til System => Logger => Filer.

> Merk: Logg ("Hendelser")-tabellen i brukergrensesnittet er ikke det samme som loggfilene og er ikke like nyttig. Hvis du blir bedt om logger, kopier/lim inn fra loggfilene og ikke tabellen.
{.is-info}

## Plassering for oppdateringslogger

Oppdateringsloggfilene er plassert i Radarr sin [Appdata-katalog](/radarr/appdata-directory), inne i mappen UpdateLogs/.

## Deling av logger

Loggene kan være lange og vanskelige å lese som en del av et forum- eller Reddit-innlegg, og de er spammy i Discord, så bruk [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller lignende pastebin-nettsteder. Hele filen er vanligvis ikke nødvendig, bare en god mengde kontekst fra før og etter problemet/feilen. Ikke glem å vente til spam-oppgaver som en RSS-synkronisering eller biblioteksoppdatering er ferdig.

## Trace/Debug-logger

Du kan endre loggnivået ved å gå til Innstillinger => Generelt => Logging. Radarr trenger ikke å startes på nytt for at endringen skal tre i kraft. De nyeste debug/sporingsloggfilene har navnene `radarr.debug.txt` og `radarr.trace.txt` henholdsvis.

Hvis du ikke har tilgang til brukergrensesnittet for å angi loggnivået, kan du gjøre det ved å redigere config.xml i AppData-katalogen ved å sette LogLevel-verdien til Debug eller Trace i stedet for Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Slette logger

Du kan slette loggfilene og loggdatabasen direkte fra brukergrensesnittet, under System => Logger => Filer og System => Logger => Slett (søppelbøtteikonet)

# Flere loggfiler

Radarr bruker rullerende loggfiler begrenset til 1 MB hver. Den nåværende loggfilen er alltid `radarr.txt`, for de andre filene er `radarr.0.txt` den nest nyeste (jo høyere nummer, jo eldre er den). Denne loggfilen inneholder `fatal`, `error`, `warn` og `info`-oppføringer.

Når Debug-loggnivået er aktivert, vil det være tilgjengelige ekstra `radarr.debug.txt` rullerende loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info` og `debug`-oppføringer. De dekker vanligvis en periode på 40 timer.

Når Trace-loggnivået er aktivert, vil det være tilgjengelige ekstra `radarr.trace.txt` rullerende loggfiler. Disse loggfilene inneholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-oppføringer. På grunn av sporingsnøyaktigheten dekker de vanligvis bare et par timer.

# Gjenopprette etter en mislykket oppdatering

- Vi gjør alt vi kan for å forhindre problemer ved oppgradering, men hvis de likevel oppstår, vil dette veilede deg gjennom trinnene du må ta for å gjenopprette installasjonen din.
- Denne delen dekker også vanlige problemer etter oppdatering.

## Identifisere problemet

- Det beste stedet å se når programmet ikke starter etter en oppdatering, er å se gjennom [oppdateringsloggene](#plassering-for-oppdateringslogger) og se om oppdateringen ble fullført. Hvis det ikke er noen problemer der, er neste steg å se på de vanlige programloggfilene dine. Før du prøver å starte på nytt, bruk [Logging](/radarr/settings#logging) og [Loggfiler](/radarr/system#loggfiler) for å finne dem og øke loggnivået.
- Det mest vanlige problemet er at systemet der appen er installert, har rotet med `/tmp`-mappen og slettet kritiske \*Arr-filer under oppgraderingen, noe som forårsaker at både oppgraderingen og tilbakerulling mislykkes. I dette tilfellet kan du bare reinstallere på stedet over den eksisterende ødelagte installasjonen.

### Database disk image is malformed

- Se vår [FAQ-innlegg](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)

### Migrasjonsproblem

- Migrasjonsfeil vil ikke være identiske, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### UI-migrasjonsproblemer

- Hvis du bytter mellom [ikke-støttede versjoner/grenser](/radarr/faq#can-i-switch-between-branches), kan du oppleve et migrasjonsproblem som ser ut som det nedenfor. Løsningen er å [gå tilbake til grensen eller høyere versjonen du var på tidligere](/radarr/faq#how-do-i-update-radarr), eller [gjenopprette en sikkerhetskopi](/radarr/faq#how-do-i-backuprestore-radarr) for gjeldende versjon.

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### Tillatelsesproblem

- Tillatelsesproblemer skyldes at programmet ikke får tilgang til de relevante midlertidige mappene og/eller appens binærmappe. Løs tillatelsesproblemene slik at brukeren/gruppen som programmet kjører som, har riktig tilgang.

- Synology-brukere kan oppleve denne Synology-feilen `Tilgang til banen '/proc/{noen tall}/maps er nektet`

- Synology-brukere kan også oppleve å være tom for plass i `/tmp` på visse NAS-er. Du må spesifisere en annen `/tmp`-bane for appen. Se SynoCommunity eller andre Synology-støttekanaler for hjelp med dette.

## Løse problemet

### Migrasjonsproblemer

Ved migrasjonsproblemer er det ikke mye du kan gjøre umiddelbart. Hvis problemet er spesifikt for deg (eller det ikke er noen innlegg ennå), kan du opprette et innlegg på [subredditen vår](https://reddit.com/r/radarr) eller besøke [discorden vår](https://radarr.video/discord). Hvis det er andre med samme problem, kan du være trygg på at vi jobber med det.

> Sørg for at du ikke prøvde å bruke en database fra `nightly`-versjonen på den stabile versjonen. Å bytte mellom grener er ikke anbefalt.{.is-info}

### Tillatelsesproblemer

- Fiks tillatelsene for å sikre at brukeren/gruppen som applikasjonen kjører som, har tilgang (lese- og skrivetilgang) til både `/tmp` og installasjonsmappen til applikasjonen.

- For Synology-brukere som opplever problemer med `/proc/###/maps` som stopper Sonarr eller de andre \*Arr-applikasjonene, bør oppdatering løse dette. Dette er et problem med SynoCommunity-pakken.

### Manuell oppgradering

Last ned den nyeste utgivelsen fra nettstedet vårt.

Installer oppdateringen (.exe) eller pakk ut (.zip) innholdet over den eksisterende installasjonen og kjør Radarr på vanlig måte.

# Nedlastinger og importering

Nedlasting og importering er der *de fleste* opplever problemer. Fra et overordnet perspektiv må Radarr kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes et stort utvalg av støttede nedlastingsklienter og en enda *større* variasjon av oppsett. Dette betyr at selv om det finnes noen *vanlige* oppsett, er det ikke ett *riktig* oppsett, og alle oppsett kan være litt forskjellige.

> **Det første trinnet er å øke loggingen til Trace, se [Logging og loggfiler](#logging-og-loggfiler) for detaljer om hvordan du justerer loggingen og søker i loggene. Deretter gjenskaper du problemet og bruker loggene på trace-nivå fra den tidsrammen til å undersøke problemet.** Hvis noen hjelper deg, legg til kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem. Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet mens oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

Når du ber om hjelp, må du sørge for å lese [å be om hjelp](#å-be-om-hjelp) slik at du kan gi oss de detaljene vi trenger.

## Teste nedlastingsklienten

Sørg for at nedlastingsklienten(e) dine kjører. Begynn med å teste nedlastingsklienten. Hvis det ikke fungerer, kan du se detaljer i loggene på trace-nivå. Du bør finne en URL du kan sette inn i nettleseren din og se om den fungerer. Det kan være et tilkoblingsproblem, som kan indikere feil IP-adresse, vertsnavn, port eller til og med en brannmur som blokkerer tilgangen. Det kan være åpenbart, som et autentiseringsproblem der du har skrevet feil brukernavn, passord eller API-nøkkel. Merk at noen seedbokser krever bruk av HTTPS, port 443 og en URL-base (avanserte alternativer), i stedet for den faktiske porten til nedlastingsklienten din.

## Teste en nedlasting

Nå skal vi prøve en nedlasting. Velg en film og gjør et manuelt søk. Velg en av disse filene og prøv å laste den ned. Blir den sendt til nedlastingsklienten? Havner den i riktig kategori? Vises den i Aktivitet? Havner den i loggene på trace-nivå under oppgavene **Sjekk for ferdig nedlasting** (Oppdater overvåkede nedlastinger og Behandle overvåkede nedlastinger), som kjører omtrent hvert minutt? Blir den riktig analysert under den oppgaven? Har den ventende nedlastingen et fornuftig navn? Siden søkene er basert på ID på noen indekserer/sporere, kan den sette opp en ventende nedlasting med et navn den ikke kan gjenkjenne.

## Teste en importering

Importproblemer bør nesten alltid vises som et element i Aktivitet med et oransje ikon du kan sveve over for å se feilen. Hvis de ikke vises i Aktivitet, er dette problemet du må fokusere på først, så gå tilbake og finn ut av det. De fleste importfeil skyldes *tillatelser*, husk at Radarr må kunne lese og skrive i nedlastingsmappen. Noen ganger kan tillatelser i biblioteksmappen også være årsaken, så sørg for å sjekke begge deler.

Feilaktige baneproblemer er også mulige, men mindre vanlige i normale oppsett. Nøkkelen for å forstå baneproblemer er å vite at Radarr får banen til nedlastingen *fra* nedlastingsklienten via API-en. Dette blir et problem i mer unike tilfeller, som når nedlastingsklienten kjører på et annet system (kanskje til og med et annet operativsystem\!). Det kan også skje i et Docker-oppsett når volumene ikke er konfigurert riktig. En ekstern banekartlegging er en god løsning der du ikke har kontroll, som i et seedbox-oppsett. I et Docker-oppsett er det bedre å fikse banene.

## Vanlige problemer

Her er noen vanlige problemer.

### Nedlastingsklientens webgrensesnitt er ikke aktivert

Radarr kommuniserer med nedlastingsklienten via API-en og får tilgang til den via klientens webgrensesnitt. Du må sørge for at nedlastingsklientens webgrensesnitt er aktivert, og at porten den bruker ikke kommer i konflikt med andre klientporter som er i bruk eller porter som er i bruk på systemet ditt.

### Bruk av SSL og feil konfigurert

Sørg for at SSL-kryptering ikke er aktivert hvis du bruker både instansen og nedlastingsklienten din i et lokalt nettverk. Se [SSL-FAQ-en](/radarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for mer informasjon.

### Kan ikke se deling på Windows

Standardbrukeren for en Windows-tjeneste er `LocalService`, som vanligvis ikke har tilgang til delingene dine. Rediger tjenesten og sett den opp til å kjøre som din egen bruker. Se FAQ-en [hvorfor kan jeg ikke se filene mine på en ekstern server](/radarr/faq#why-cant-i-see-my-files-on-a-remote-server) for detaljer.

### Mappede nettverksstasjoner er ikke pålitelige

Selv om mappede nettverksstasjoner som `X:\` er praktiske, er de ikke like pålitelige som UNC-baner som `\\server\share`, og de er heller ikke tilgjengelige før pålogging. Konfigurer nedlastingsklienten(e) slik at de bruker UNC-baner etter behov. Hvis biblioteket ditt er på en deling, må du sørge for at rotmappene dine bruker UNC-baner. Hvis nedlastingsklienten sender til en deling, må du konfigurere UNC-baner der, siden Radarr får nedlastingsbanen fra nedlastingsklienten. Det er greit å beholde de mappede nettverksstasjonene for personlig bruk, bare ikke bruk dem til automatisering.

### Docker og bruker, gruppe, eierskap, tillatelser og baner

Docker legger til et ekstra lag med kompleksitet som er lett å gjøre feil, men likevel ende opp med et oppsett som fungerer, men har ulike problemer. I stedet for å gå gjennom dem her, les denne wikien [for disse automatiseringsprogrammene og Docker](/docker-guide), som handler om bruker, gruppe, eierskap, tillatelser og baner. Den er ikke spesifikk for et bestemt Docker-system, i stedet går den gjennom ting på et overordnet nivå slik at du kan implementere dem i ditt eget miljø.

### Ekstern banekartlegging

Hvis du har Radarr i Docker og nedlastingsklienten utenfor Docker (eller omvendt), eller har programmene på forskjellige servere, kan du trenge en ekstern banekartlegging.

Loggene vil indikere noe lignende.

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Dermed eksisterer ikke `/volume3/data` i Radarrs konteiner eller er ikke tilgjengelig.

- [Innstillinger => Nedlastingsklienter => Ekstern banekartlegging](/radarr/settings#remote-path-mappings)
- En ekstern banekartlegging brukes når nedlastingsklienten din rapporterer en bane for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er en ekstern banekartlegging bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows, eller omvendt. En ekstern banekartlegging kan også være nødvendig hvis du blander Docker- og Native-klienter, eller hvis du bruker en ekstern server.
- En ekstern banekartlegging er en DUMB søk/erstatt (hvor den finner VERDIEN FJERN, erstatt den med VERDIEN LOKAL for den angitte verten).
- Hvis feilmeldingen om en ugyldig bane ikke inneholder den ERSTATTEDE verdien, fungerer ikke banekartleggingen som forventet. Den vanlige løsningen er å legge til og fjerne kartleggingen.
- [Se TRaSHs veiledning for mer informasjon om ekstern banekartlegging](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-kontainere, er det sjelden behov for en ekstern banekartlegging. Det anbefales å [gjennomgå Docker-guiden](/docker-guide) og/eller [følge TRaSHs veiledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Ekstern montering eller ekstern synkronisering (Syncthing)

- Du trenger at synkroniseringen skjer hele tiden mens den laster ned. Og du trenger at den lokale synkroniseringsdestinasjonen kan være hardlenker når \*Arr importerer, noe som betyr samme filsystem og ser ut som det.
  - Synkroniser til en lavere, felles mappe som inneholder både ufullstendige og fullførte filer.
  - Synkroniser til en plassering som er på samme filsystem lokalt som biblioteket ditt og ser ut som det (Docker og nettverksdelinger gjør det enkelt å konfigurere feil).
  - Du vil synkronisere det ufullstendige og fullførte, slik at når torrentklienten flytter, reflekteres det lokalt, og alle filene er allerede "der" (selv om de fortsatt lastes ned). Deretter vil du bruke hardlenker, for selv om det importeres før det er ferdig, vil de fortsatt fullføres.
  - På denne måten laster den ned hele tiden, synkroniserer, deretter flytter torrentklienten til tv-undermappen, og synkroniseringen reflekterer det. På den måten er nedlastingen stort sett der når den er ferdig. Og selv om de ikke er helt ferdige, betyr muligheten for hardlenker at det er greit.
  - (Valgfritt - hvis det er aktuelt og/eller nødvendig (f.eks. ekstern usenet-klient)) Konfigurer et tilpasset skript som skal kjøres ved importering/nedlasting/oppgradering for å fjerne den eksterne filen
- Alternativt er en ekstern montering i stedet for en ekstern synkronisering betydelig mindre komplisert å konfigurere, men vanligvis tregere.
  - Monter den eksterne lagringen med sshfs eller en annen nettverksfilsystemprotokoll.
  - Sørg for at brukeren og gruppen \*Arr er konfigurert til å kjøre som, har lese- eller skrivetilgang.
  - Konfigurer en ekstern banekartlegging for å finne den EKSTERNE banen og erstatte den med den LOKALE tilsvarende banen.

### Tillatelser på biblioteksmappen

Loggene vil se slik ut

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Ikke glem å sjekke tillatelser og eierskap for *destinasjonen*. Det er lett å bli fokusert på nedlastingens eierskap og tillatelser, og det er *vanligvis* årsaken til tillatelsesrelaterte problemer, men det *kan* også være destinasjonen. Sjekk at destinasjonsmappene eksisterer. Sjekk om en destinasjonsfil allerede eksisterer eller ikke kan slettes eller flyttes til papirkurven. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres, hardlenkes eller flyttes. Brukeren eller gruppen som kjører \*Arr må kunne lese og skrive i rotmappen.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Du får muligheten til å gjøre dette under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunity's artikkel om tillatelser for pakkene deres](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- For ikke-Windows-brukere: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Tillatelser på nedlastingsmappen

Loggene vil se slik ut

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Ikke glem å sjekke tillatelser og eierskap for *kilden*. Det er lett å bli fokusert på destinasjonens eierskap og tillatelser, og det er en *mulig* årsak til tillatelsesrelaterte problemer, men det er vanligvis kilden. Sjekk at kildekatalogene eksisterer. Sjekk at eierskap og tillatelser tillater at den nedlastede filen kan kopieres/hardlenkes eller kopieres+slettes/flyttes. Brukeren eller gruppen som kjører \*Arr må kunne lese og skrive i nedlastingsmappen.

- For Windows-brukere kan dette skyldes at det kjører som en tjeneste:
  - Windows-tjenesten kjører under kontoen 'Local Service', som som standard ikke har tillatelse til å få tilgang til brukerens hjemmekatalog med mindre tillatelser er tildelt manuelt. Dette er spesielt relevant når du bruker nedlastingsklienter som er konfigurert til å laste ned til hjemmekatalogen din.
  - 'Local Service' har også generelt sett svært begrensede tillatelser. Det anbefales derfor å installere appen som en systemstatusapplikasjon hvis brukeren kan være logget inn. Du får muligheten til å gjøre dette under installasjonen. Se FAQ-en for hvordan du konverterer fra en tjeneste til en statusapplikasjon.

- For Synology-brukere, se [SynoCommunity's artikkel om tillatelser for pakkene deres](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- For ikke-Windows-brukere: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
- Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.

### Nedlastingsmappen og biblioteksmappen er ikke forskjellige mapper

Nedlastingsklienten skal laste ned til en mappe som er tilgjengelig for \*Arr og som ikke er rot-/biblioteksmappen din. Den skal importere fra den separate nedlastingsmappen til biblioteksmappen din.

Du bør aldri laste ned direkte til rotmappen din. Du bør heller ikke bruke rotmappen din som nedlastingsklientens fullførte mappe eller ufullstendige mappe.

> Nedlastingsmappen din og rot-/biblioteksmappen din **må** være separate
{.is-warning}

### Feil kategori

Radarr bør være konfigurert til å bruke en kategori slik at den bare prøver å behandle sine egne nedlastinger. Det er sjelden at en torrent som er sendt inn av blir lagt til uten riktig kategori, men det kan skje. Hvis du legger til torrents manuelt og vil behandle dem, må de ha riktig kategori. Den kan settes når som helst, siden prøver å behandle nedlastinger hvert minutt.

### Pakkede torrents

Loggene vil vise feilmeldinger som

```none
No files found are eligible for import
```

Hvis torrenten din er pakket i `.rar`-filer, må du sette opp utpakking. Vi anbefaler [Unpackerr](https://github.com/unpackerr/unpackerr), da den gjør utpakking riktig: forhindrer korrupte delvise importeringer og rydder opp i de utpakkede filene etter importering.

Feilen kan også vises hvis det ikke finnes noen gyldig mediefil i mappen.

### Gjentatte nedlastinger

Det er noen få årsaker til gjentatte nedlastinger, men en av dem er relatert til egendefinerte formater. Det er mulig at utgivelsesnavnet samsvarer med et egendefinert format, men nedlastingsfilene gjør det ikke. Dette fører til en løkke der du laster ned elementene om og om igjen fordi det ser ut som en oppgradering, deretter ikke er det, deretter vises det igjen og ser ut som en oppgradering, deretter ikke er det. Avhengig av ditt egendefinerte format kan du kanskje løse dette ved å inkludere det egendefinerte formatet i navneendringsskjemaet ditt. (Aktiver egendefinert format for å inkludere det i navneendringen og legg deretter til egendefinert format i navneendringsskjemaet ditt)

Dette kan også skyldes at nedlastingen faktisk aldri blir importert og deretter mangler fra køen, slik at en ny nedlasting stadig blir hentet og aldri importert. Se de forskjellige andre vanlige problemene og feilsøkingsstegene for dette.

### Usenet-nedlasting blir ikke importert

Radarr ser bare på de 60 nyeste nedlastingene i SABnzbd og NZBGet, så hvis du beholder historikken din, betyr dette at under store køer med importproblemer kan nedlastinger bli stillestående og ikke importert. Den beste måten å unngå dette på er å holde historikken ryddig, slik at eventuelle elementer som fortsatt vises, må undersøkes. Du kan oppnå dette ved å aktivere Fjern under Fullført og Mislykket nedlastingsbehandler. I NZBGet vil dette flytte elementer til den skjulte historikken, noe som er flott. Dessverre har ikke SABnzbd en lignende funksjon. Det beste du kan oppnå der er å bruke nzb-sikkerhetskopimappen.

### Nedlastingsklient fjerner elementer

Nedlastingsklienten skal *ikke* være ansvarlig for å fjerne nedlastinger. Usenet-klienter bør konfigureres slik at de *ikke* fjerner nedlastinger fra historikken. Torrent-klienter bør settes opp slik at de *ikke* fjerner torrenter når de er ferdig med å seede (pause eller stopp i stedet). Dette skyldes at Radarr kommuniserer med nedlastingsklienten for å vite hva som skal importeres, så hvis de blir *fjernet*, er det ingenting å importere ... selv om det er en mappe full av filer.

For SABnzbd håndteres dette med innstillingen Historiebevaring.

### Nedlastingen kan ikke matches med et bibliotekselement

Av forskjellige årsaker kan utgivelser ikke analyseres når de er hentet og sendt til nedlastingsklienten. Aktivitet => Alternativer => Vis ukjent (dette er nå aktivert som standard i nyere bygg) vil vise alle elementer som ikke er ignorert / allerede importert innenfor \*Arrs nedlastingsklientkategori. Disse må vanligvis kartlegges og importeres manuelt.

Årsaker inkluderer:
- Filnavnet har et `:` på TMDb og TMDb har ingen alternativ tittel med en `-` eller med en ` ` som erstatter `:`
- Filnavnet mangler året som er påkrevd
- AKA eller rare flere navn; Radarr har begrenset støtte for disse
- Filnavnet samsvarer med flere filmer
- Utgivelsesnavnet eller utgivelses-IDen fra indekseren samsvarer ikke med filnavnet

Dette kan også skje hvis du har en utgivelse i nedlastingsklienten din, men det medieelementet (film/episode/bok/sang) eksisterer ikke i applikasjonen.

### Forbindelsen ble lukket: En uventet feil oppstod under sendingen

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Radarr => System => Status](/radarr/system#status).

### Forespørselen ble tidsavbrutt

Radarr får ingen respons fra klienten.

```none
    System.NET.WebException: Forespørselen ble tidsavbrutt: ’https://eksempel.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Forespørselen ble tidsavbrutt
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke koble til indekser

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En oppgave ble avbrutt.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av en VPN
- feil konfigurert eller bruk av en proxy
- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

## Problem som ikke er oppført

Du kan også se gjennom noen vanlige tillatelser og nettverksfeilsøkingskommandoer [i vår guide](/permissions-and-networking). Ellers kan du diskutere med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

# Søk indekser og trackere

- Hvis du bruker [Prowlarr](/prowlarr), kan du se [Historikk](/prowlarr/history) over alle spørringer Prowlarr mottok og hvordan de ble sendt til nettstedene. Sørg for at `Parametere` er aktivert i Prowlarr Historikk => Alternativer. (i)-ikonet gir ytterligere detaljer.

## Skru opp loggingen til sporingsnivå

> **Det første trinnet er å skru opp loggingen til sporingsnivå, se [Logging og loggfiler](#logging-og-loggfiler) for detaljer om hvordan du justerer loggingen og søker i loggene. Du vil deretter gjenskape problemet og bruke sporingsnivåloggene fra den tidsrammen til å undersøke problemet.** Hvis noen hjelper deg, legg kontekst fra før/etter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende nettsted for å vise dem. Det trenger ikke å være hele filen, og det bør ikke *bare* være feilen. Du bør også gjenskape problemet mens oppgaver som spammer loggfilen ikke kjører.
{.is-danger}

## Test av en indekser eller tracker

Når du tester en indekser eller tracker, kan du finne URLen som ble brukt i feilsøkings- eller sporingslogger. Et eksempel på en vellykket test er nedenfor, der du kan se at den spør indekseren via en spesifikk URL med spesifikke parametere, og deretter responsen. Du kan teste denne URLen i nettleseren din ved å erstatte `apikey=(fjernet)` med riktig api-nøkkel som `apikey=123`. Du kan eksperimentere med parameterne hvis du får en feil fra indekseren, eller se om du har tilkoblingsproblemer hvis det ikke fungerer i det hele tatt. Etter at du har testet i nettleseren din, bør du teste fra systemet som kjører *hvis* du ikke allerede har gjort det.

## Testing av et søk

På samme måte som indekser-/tracker-testen ovenfor, når du utløser et søk mens du har logging på feilsøkings- eller sporingsnivå, kan du få URLen som ble brukt fra loggfilene. Under testing er det best å bruke et så smalt søk som mulig. Et manuelt søk er bra fordi det er spesifikt, og du kan se resultatene i brukergrensesnittet mens du undersøker loggene.

I denne testen ser du etter åpenbare feil og kjører noen enkle tester. Du kan se at søket brukte URLen `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(fjernet)&q=O+Brother+Where+Art+Thou`, som du kan prøve selv i en nettleser etter å ha erstattet `(fjernet)` med api-nøkkelen din for den indekseren. Fungerer det? Ser du de forventede resultatene? I den URLen kan du se at den har satt den spesifikke kategorien 2000, så hvis du ikke ser forventede resultater, er dette en sannsynlig årsak. Hvis filmen ikke er riktig kategorisert på indekseren, må det fikses. Se på eksempel på XML-utdata for manuelt søk nedenfor for å se et eksempel på utdata for en fungerende spørring.

- XML-utdata for manuelt søk

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(fjernet)&q=O+Brother+Where+Art+Thou" rel="self" type="application/rss+xml"/>
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
<newznab:response offset="0" total="17"/>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=e83b7ae75bca71e92367fab29b036731&apikey=(fjernet)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(fjernet)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=e83b7ae75bca71e92367fab29b036731</comments>
<pubDate>Sat, 10 Jul 2021 08:33:22 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(fjernet)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="e83b7ae75bca71e92367fab29b036731"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=c00a92567863801ab1a4901458ae31ba&apikey=(fjernet)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(fjernet)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=c00a92567863801ab1a4901458ae31ba</comments>
<pubDate>Sun, 28 Mar 2021 10:50:38 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(fjernet)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="c00a92567863801ab1a4901458ae31ba"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=75f5be8b4cd573c2359b638350689f73&apikey=(fjernet)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(fjernet)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=75f5be8b4cd573c2359b638350689f73</comments>
<pubDate>Sun, 28 Jul 2019 00:46:00 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(fjernet)" length="936738000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="936738000"/>
<newznab:attr name="guid" value="75f5be8b4cd573c2359b638350689f73"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(fjernet)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(fjernet)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=a0fe801d9ba0a703db7d2164e996aa1f</comments>
<pubDate>Mon, 14 Aug 2017 15:34:36 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(fjernet)" length="9746182000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="9746182000"/>
<newznab:attr name="guid" value="a0fe801d9ba0a703db7d2164e996aa1f"/>
</item>
</channel>
</rss>
```

***Bilder som trengs***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- Sporingsloggutklipp

```none
Utklipp av sporingslogg for et manuelt søk som trengs
```

- Full sporingslogg for et søk

```none
Full seksjon av sporingslogg for et manuelt søk som trengs
```

## Vanlige problemer

Her er noen vanlige problemer.

### Tracker trenger RawSearch Caps

- Radarr søker etter `Kikis Delivery Service`, men trackeren din har bare resultater for `Kiki's Delivery Service`
- Dette skyldes at trackeren din ikke støtter normale standardiserte søk.
- Løsningen er at søkefunksjonene i trackerens definisjon må oppdateres for å indikere at den [krever og støtter `RawSearch`](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905)
- Jackett støtter flagget, men funksjonene må oppdateres for hver indekser. Åpne en funksjonsforespørsel for Jackett for å legge til denne funksjonaliteten for indekseren din.
- Prowlarr støtter flagget, men funksjonene må oppdateres for hver indekser. Åpne en funksjonsforespørsel for Prowlarr for å legge til denne funksjonaliteten for indekseren din.

### Mediet er ikke overvåket

Filmen(e) er ikke overvåket.

### Feil kategorier

Feilaktige kategorier er sannsynligvis den vanligste årsaken til at resultater vises i manuelle søk på en indekser/tracker, men *ikke* i Radarr. Indekseren/trackeren *bør* vise kategorien i søkeresultatene, noe som kan hjelpe deg med å finne ut hva som mangler. Hvis du bruker Jackett eller Prowlarr, har hver tracker en liste over spesifikt støttede kategorier. Sørg for at du bruker de riktige kategoriene for Radarr. Mange finner det nyttig å ha listen synlig i ett nettleservindu mens de redigerer oppføringen.

### Vellykket søk - Ingen resultater returnert

Du mottar en melding som ligner på `Søket var vellykket, men ingen resultater ble returnert fra indekseren din. Dette kan være et problem med indekseren eller innstillingene for indekseringskategorier.`

Dette skyldes at indekseren din ikke returnerer noen resultater som er innenfor kategoriene du har konfigurert for indekseren.

### Feilaktige resultater

Noen ganger returnerer indekserere helt irrelevante resultater. Radarr vil sende inn parametere for å begrense søket, men resultatene som returneres er helt irrelevante. Eller noen ganger, mest relatert med noen få feilaktige resultater. Den første situasjonen skyldes vanligvis et indekseringsproblem, og du vil kunne se fra sporingsloggene hvilken indekserer som forårsaker det. Du kan deaktivere den indekseren og rapportere problemet. Den andre situasjonen skyldes vanligvis kategoriserte utgivelser som kan rapporteres til indekseren/trackeren.

### Manglende resultater

Hvis du har resultater på nettstedet som du kan finne, men som ikke vises i Radarr, er problemet sannsynligvis en av flere muligheter:

- [Feilaktige kategorier - se over](#wrong-categories)
- Det blir utført et søk basert på en ID (IMDbId, TMDbId, osv.), og indekseren har ikke riktig kartlegging av utgivelsene til den ID-en. Dette er noe bare indekseren din kan løse. De må sørge for at utgivelsen er kartlagt til de riktige ID-ene som gjelder.
- Du søker ikke på samme måte som Radarr. Det er svært sannsynlig at vilkårene du søker etter i indekseren ikke er slik Radarr utfører søket. Du kan se hvordan Radarr søker i sporingsloggene. Tekstbaserte søk vil vanligvis være i formatet `q=ord%20og%20ting%20her`. Denne strengen er HTTP-kodet og kan enkelt dekodes ved hjelp av et hvilket som helst nettbasert verktøy for HTML-koding/avkoding.
- [Se FAQ-en for hvordan Radarr håndterer utenlandske filmtitler og når Radarr søker etter dem](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### Sertifikatvalidering

Du vil koble til de fleste indekserere/trackere via https, så du må sørge for at dette fungerer riktig på systemet ditt. Det betyr at tidssonen og klokkeslettet ditt må være satt *riktig*. Det betyr også at systemsertifikatene dine må være oppdaterte.

### Treff rategrenser

Hvis du bruker en VPN eller proxy, kan du konkurrere med 10-talls, 100-talls eller 1000-talls andre personer som alle prøver å bruke tjenester som , theXEM og/eller indekserne og trackerne dine. Rategrenser og DDOS-beskyttelse blir ofte gjort basert på IP-adresse, og VPN-/proxy-utgangspunktet ditt er *én* IP-adresse. Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, trenger du ikke VPN/proxy .

Rarbg har en tendens til å ha en form for rategrense i API-en sin og vises som svar uten resultater.

### IP-blokkering

På samme måte som rategrenser, kan visse indekserere - som Nyaa - utestenge en IP-adresse fullstendig. Dette er vanligvis halvpermanent, og løsningen er å få en ny IP fra internettleverandøren eller VPN-leverandøren din.

### År stemmer ikke

- [Se denne FAQ-innføringen](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr får metadata fra TMDb
  - Radarr bruker året for den eldste **kinoutgivelsesdatoen** og det eldste **premiere**-året for sammenligning
- I noen tilfeller har filmen blitt utsatt eller flyttet rundt, og året som brukes av utgivelsesgruppene stemmer verken med det eldste premiereåret eller det eldste kinoutgivelsesåret. I slike situasjoner må du laste ned og importere manuelt.

### Manglende år

Radarr vil ikke laste ned en utgivelse hvis utgivelsesnavnet ikke inneholder et årstall. Dette er en dårlig utgivelse og kan bare lastes ned manuelt. Dette er en vanlig ting å overse når man prøver å finne ut hvorfor en film ikke ble lastet ned som forventet.

### Bruk av Jackett /all-endepunktet

Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan potensielt føre til problemer, så det er nødvendig å legge til hver tracker individuelt. Alternativt kan du vurdere å prøve Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Selv Jackett sier at /all bør unngås og ikke bør brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)

Å bruke all-endepunktet har ingen fordeler (bortsett fra redusert administrasjonsarbeid), bare ulemper:

- du mister kontrollen over indekser-spesifikke innstillinger (kategorier, søkemoduser, osv.)
- blanding av søkemoduser (IMDB, søk, osv.) kan føre til resultater av lav kvalitet
- indekser-spesifikke kategorier (\>= 100000) kan ikke brukes.
- treg indekser vil bremse ned det totale resultatet
- totalt antall resultater er begrenset til 1000

Ved å legge til hver indekser separat, kan du finjustere kategoriene for hver indekser, noe som kan være et problem med `/all`-endepunktet hvis feil kategori forårsaker feil på noen trackere. I , er hver indekser begrenset til 1000 resultater hvis paginering støttes, eller 100 hvis ikke, noe som betyr at jo flere trackere du legger til i Jackett, desto større er sjansen for at du mister resultater. Til slutt, hvis *én* av trackerne i `/all` returnerer en feil, vil  deaktivere den, og nå får du ingen resultater.

### Bruk av NZBHydra2 som en enkelt oppføring

Å bruke NZBHydra2 som en enkelt indekseroppføring (dvs. 1 NZBHydra2-oppføring i Radarr for mange indexere i NZBHydra2) i stedet for flere (dvs. mange NZBHydra2-oppføringer i Radarr for mange indexere i NZBHydra2) har de samme problemene som nevnt ovenfor med Jacketts `/all`-endepunkt.

### Problem som ikke er oppført

Du kan også gå gjennom noen vanlige tillatelser og nettverkstilkoblingsfeilsøkingskommandoer [i guiden vår](/permissions-and-networking). Ellers kan du diskutere det med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.

## Feil

Dette er noen av de vanlige feilene du kan se når du legger til en indekser

### Forbindelsen ble lukket: En uventet feil oppstod under sendingen

Dette skyldes at indekseren bruker en SSL-protokoll som ikke støttes av gjeldende .NET-versjon som finnes i [Radarr => System => Status](/radarr/system#status).

### Forespørselen tidsavbrutt

Radarr får ingen respons fra indekseren.

```none
    System.NET.WebException: Forespørselen tidsavbrutt: ’https://eksempel.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Forespørselen tidsavbrutt
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke koble til indekserer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En oppgave ble avbrutt.
```

Dette kan også skyldes:

- feil konfigurert eller bruk av VPN
- feil konfigurert eller bruk av proxy
- lokale DNS-problemer - Prøv å bytte til en annen DNS-leverandør
- lokale IPv6-problemer - vanligvis er IPv6 aktivert, men ikke funksjonell
- bruk av Privoxy og feil konfigurering av det

### Problem som ikke er oppført

Du kan også gå gjennom noen vanlige tillatelser og nettverkstilkoblingsfeilsøkingskommandoer [i guiden vår](/permissions-and-networking). Ellers kan du diskutere det med supportteamet på Discord. Hvis dette er noe som kan være et vanlig problem, kan du foreslå å legge det til i wikien.