---
title: Prowlarr Fejlfinding
description: 
published: true
date: 2023-08-20T00:20:04.841Z
tags: prowlarr, fejlfinding
editor: markdown
dateCreated: 2021-06-20T20:05:25.223Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [At bede om hjælp](#at-bede-om-hjælp)
- [Logging og logfiler](#logging-og-logfiler)
  - [Standardplacering for logfiler](#standardplacering-for-logfiler)
  - [Placering af opdateringslogfiler](#placering-af-opdateringslogfiler)
  - [Deling af logfiler](#deling-af-logfiler)
  - [Trace/debug-logfiler](#tracedebug-logfiler)
  - [Rydning af logfiler](#rydning-af-logfiler)
- [Flere logfiler](#flere-logfiler)
- [Gendannelse efter en mislykket opdatering](#gendannelse-efter-en-mislykket-opdatering)
  - [Afgør problemet](#afgør-problemet)
    - [Migrationsproblem](#migrationsproblem)
    - [Tilladelsesproblem](#tilladelsesproblem)
  - [Løsning af problemet](#løsning-af-problemet)
    - [Tilladelsesproblemer](#tilladelsesproblemer)
    - [Manuel opgradering](#manuel-opgradering)
- [NGINX-fejl](#nginx-fejl)
- [Problemer med indexer, applikation og downloadklient](#problemer-med-indexer-applikation-og-downloadklient)
  - [Kan ikke bestemme ramme størrelse eller en korrupt ramme blev modtaget](##kan-ikke-bestemme-ramme-størrelse-eller-en-korrupt-ramme-blev-modtaget)
  - [Forbindelse udløbet](#forbindelse-udløbet)
  - [Sonarr HTTP 404-fejl](#sonarr-http-404-fejl)
  - [\*Arr HTTP 400-fejl](#arr-http-400-fejl)
  - [503 HTTP-tjeneste utilgængelig](#503-http-tjeneste-utilgængelig)
  - [Ugyldige torrents](#ugyldige-torrents)
  - [Søgning og indexer](#søgning-og-indexer)

# At bede om hjælp

Har du brug for hjælp? Det er okay, alle har brug for hjælp nogle gange. Du kan få hjælp i realtid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiel Prowlarr Discord*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiel Prowlarr Subreddit*](https://reddit.com/r/prowlarr)
{.links-list}

Men inden du går derhen og poster, skal du sikre dig, at din anmodning om hjælp er så god som muligt. Beskriv tydeligt problemet og beskriv kort din opsætning, herunder ting som dit OS/distribution, version af .NET, version af Prowlarr, downloadklient og dens version. **Hvis du bruger [Docker](https://www.docker.com/), skal du køre [Docker Guide](/docker-guide) først, da det vil løse almindelige og hyppige sti-/tilladelsesproblemer. Ellers skal du have en [docker compose](/docker-guide#docker-compose) klar. [Sådan genereres en Docker Compose](https://trash-guides.info/compose)** Fortæl os om, hvad du allerede har prøvet, hvad du har kigget på. Brug [Logging og logfiler-sektionen](#logging-og-logfiler) til at øge logningen til trace, genskab problemet, pastebin den relevante kontekst og inkluder et link til det i dit indlæg. Måske endda inkludere nogle skærmbilleder for at fremhæve problemet.

Jo mere vi ved, jo lettere er det at hjælpe dig.

# Logging og logfiler

Det kan være nyttigt også at gennemgå [Indexer, Application og Download Client Issues Common Problems](#indexer-application-og-download-client-issues).

> Hvis du bliver bedt om at give indexerrespons til udvikling eller fejlfinding, skal du læse videre i denne blå sektion...ellers fortsæt til trinene nedenfor. Når du fejlfinder indexerrespons, er det sandsynligvis nyttigt at gå til `settings/development` (skjult side) i Prowlarr og midlertidigt aktivere Enhanced Indexer Logging for at logge indexerens respons. Det skal ikke være aktiveret hele tiden
{.is-info}

Hvis du bliver bedt om debuglogfiler, vil dine logfiler indeholde `debug`, og hvis du bliver bedt om tracelogfiler, vil dine logfiler indeholde `trace`. Hvis de logfiler, du giver, ikke indeholder nogen af disse, er det ikke de logfiler, der er blevet anmodet om.

- Undgå at dele hele logfilen, medmindre du bliver bedt om det.
- Upload ikke logfiler direkte til Discord eller indsæt dem som tekstvægge, medmindre du bliver bedt om det.
- Del ikke logfiler som vedhæftning, zip-arkiv eller noget andet end tekst, der deles via de nedenfor nævnte tjenester

For at give gode og nyttige logfiler til deling:

> Sørg for, at der ikke kører en spamagtig opgave, f.eks. en RSS-opdatering
{.is-warning}

1. [Øg logningen til trace (Indstillinger => Generelt => Logniveau eller Rediger konfigurationsfilen)](#tracedebug-logfiler)
2. [Ryd logfiler (System => Logfiler => Ryd logfiler eller Slet alle logfiler i logmappen)](#rydning-af-logfiler)
3. Genskab problemet (Gentag det, der ødelægger tingene)
4. [Åbn trace-logfilen (Lidarr.trace.txt) via brugergrænsefladen eller logfilen](#standardplacering-for-logfiler) på filsystemet og find den relevante kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del efter problemet.
6. Brug [Gist](https://gist.github.com/), [0bin (**Sørg for at deaktivere farvelægning**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) eller lignende sider - undtagen dem, der er nævnt for at undgå nedenfor - til at dele de kopierede logfiler fra ovenstående

**Advarsler:**
- **Brug ikke [pastebin.com](https://pastebin.com), da deres filtre har en tendens til at blokere logfilerne.
- Brug ikke [pastebin.pl](https://pastebin.pl), da deres websted ofte ikke er tilgængeligt.
- Brug ikke [JustPasteIt](https://justpaste.it/), da deres websted ikke gør det nemt at gennemgå logfiler.
- Upload ikke din log som en fil.
- Upload ikke og del ikke dine logfiler via Google Drive, Dropbox eller nogen anden side, der ikke er nævnt ovenfor.
- Arkiver ikke (zip, tar (tarball), 7zip osv.) dine logfiler.
- Del ikke konsoloutput, docker-containeroutput eller noget andet end de angivne applikationslogfiler

**Vigtig note:**
- Når du bruger [0bin](https://0bin.net/), skal du sørge for at deaktivere farvelægning og ikke brænde efter læsning.

- Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken du kan bruge N++. Du kan bruge Notepad++ "Find i filer"-funktionen til at søge i gamle logfiler efter behov.
- **Kun Unix:** Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken du kan bruge grep. Hvis du f.eks. vil finde oplysninger om film/serier/bøger/sange/indexer "Shooter", kan du køre følgende kommando `grep -inr -C 100 -e 'Shooter' /sti/til/logfiler/*.trace*.txt` Hvis din [Appdata-mappe](/prowlarr/appdata-directory) er i din hjemmemappe, skal du køre: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flagene har følgende funktioner
    * -i: ignorer store/små bogstaver
    * -n: vis linjenummer
    *  -r: søg rekursivt i alle filer i stien
    * -C: angiv antallet af linjer før og efter linjen, den findes på
    * -e: mønsteret, der skal søges efter

```

## Standardplacering for logfiler

Logfilerne findes i Prowlarrs [Appdata-mappe](/prowlarr/appdata-directory), inde i mappen logs/. Du kan også få adgang til logfilerne fra brugergrænsefladen under System => Logs => Filer.

> Bemærk: Logtabelen ("Events") i brugergrænsefladen er ikke det samme som logfilerne og er ikke lige så nyttig. Hvis du bliver bedt om logfiler, skal du kopiere/indsætte fra logfilerne og ikke tabellen.
{.is-info}

## Placering af opdateringslogfiler

Opdateringslogfilerne findes i Prowlarrs [Appdata-mappe](/prowlarr/appdata-directory), inde i mappen UpdateLogs/.

## Deling af logfiler

Logfilerne kan være lange og svære at læse som en del af et forum- eller Reddit-indlæg, og de er spamagtige i Discord, så brug venligst [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller en anden lignende pastebin-side. Hele filen er normalt ikke nødvendig, kun en god mængde kontekst før og efter problemet/fejlen. Glem ikke at vente på spamagtige opgaver som f.eks. en RSS-synkronisering eller biblioteksopdatering for at blive færdige.

## Trace/debug-logfiler

Du kan ændre logniveauet under Indstillinger => Generelt => Logning. Prowlarr behøver ikke genstartes for, at ændringen træder i kraft. Denne ændring påvirker kun logfilerne, ikke logningsdatabasen. De nyeste debug/trace-logfiler hedder henholdsvis `prowlarr.debug.txt` og `prowlarr.trace.txt`.

Hvis du ikke kan få adgang til brugergrænsefladen for at indstille logningsniveauet, kan du gøre det ved at redigere config.xml i AppData-mappen ved at sætte værdien LogLevel til Debug eller Trace i stedet for Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Rydning af logfiler

Du kan rydde logfiler og logningsdatabasen direkte fra brugergrænsefladen under `System` => `Logs` => `Filer` og `System` => `Logs` => `Slet` (Skraldespandssymbol).

# Flere logfiler

Prowlarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid Prowlarr.txt, og for de andre filer er Prowlarr.0.txt den næstnyeste (jo højere nummeret er, jo ældre er den). Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.

Når debug-logniveauet er aktiveret, vil der være yderligere `prowlarr.debug.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. Den dækker normalt en periode på 40 timer.

Når trace-logniveauet er aktiveret, vil der være yderligere `prowlarr.trace.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af trace-omfang dækker den kun et par timer eller endda mindre end et minut, hvis du laver noget intensivt.

# Gendannelse efter en mislykket opdatering

Vi gør alt, hvad vi kan, for at forhindre problemer ved opgradering, men hvis de opstår, vil dette guide dig gennem de trin, du skal tage for at gendanne din installation.

## Afgør problemet

- Det bedste sted at kigge, når programmet ikke starter efter en opdatering, er at gennemgå [opdateringslogfilerne](#placering-af-opdateringslogfiler) og se, om opdateringen blev fuldført uden problemer. Hvis der ikke er nogen problemer der, er næste skridt at kigge på dine almindelige programlogfiler, før du prøver at starte igen, brug [Logging](/prowlarr/settings#logging) og [Logfiler](/prowlarr/system#log-files) til at finde dem og øge logniveauet.
- Det mest almindelige problem er, at systemet, som appen er installeret på, har rodet med `/tmp`-mappen og slettet kritiske \*Arr-filer under opgraderingen, hvilket får både opgraderingen og tilbagerulningen til at mislykkes. I dette tilfælde skal du blot geninstallere oven i den eksisterende fejlbehæftede installation.

### Migrationsproblem

- Migrationsfejl vil ikke være ens, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Tilladelsesproblem

- Tilladelsesproblemer skyldes, at appen ikke kan få adgang til de relevante midlertidige mapper og/eller appens binære mappe. Ret tilladelserne, så brugeren/gruppen, som appen kører som, har den passende adgang.

- Synology-brugere kan støde på denne Synology-fejl `Access to the path '/proc/{noget nummer}/maps is denied`

- Synology-brugere kan også støde på, at der ikke er plads i `/tmp` på visse NAS-enheder. Du skal angive en anden sti til `/tmp` for appen. Se SynoCommunity eller andre Synology-supportkanaler for hjælp til dette.

## Løsning af problemet

Hvis der opstår et migrationsproblem, er der ikke meget, du kan gøre med det samme. Hvis problemet er specifikt for dig (eller der endnu ikke er nogen indlæg), skal du oprette et indlæg på [vores subreddit](https://reddit.com/r/prowlarr) eller kigge forbi vores [discord](https://prowlarr.com/discord). Hvis der er andre med samme problem, kan du være sikker på, at vi arbejder på det.

> Sørg for, at du ikke har forsøgt at bruge en database fra `nightly`-versionen på den stabile version. Det frarådes at skifte mellem versioner.{.is-info}

### Tilladelsesproblemer

- Ret tilladelserne, så brugeren/gruppen, som appen kører som, kan få adgang (læse og skrive) til både `/tmp` og installationsmappen for appen.

- For Synology-brugere, der oplever problemer med `/proc/###/maps`, bør stop af Sonarr eller de andre \*Arr-applikationer og opdatering løse dette. Dette er et problem med SynoCommunity-pakken.

### Manuel opgradering

Hent den nyeste version fra vores hjemmeside.

Installer opdateringen (.exe) eller udpak indholdet (.zip) over din eksisterende installation og kør Prowlarr som du plejer.

# NGINX-fejl

I din Prowlarr-opsætning skal du bruge denne linje:

`proxy_set_header Host $host;`

Hvis du har en anden `proxy_set_header`, skal du erstatte den med linjen ovenfor.

# Problemer med indexer, applikation og downloadklient

- På et grundlæggende niveau skal Prowlarr kunne kommunikere med dine indexers.
- Hvis du bruger applikationssynkronisering, skal Prowlarr også kunne kommunikere med dine applikationer, og applikationerne skal kunne kommunikere med Prowlarr.
- Hvis du har en downloadklient i Prowlarr til manuelle downloads i Prowlarr, skal Prowlarr kunne kommunikere med din downloadklient.

> Bemærk, at logfiler, der angiver forespørgsel af indexer-ID 0: ID 0 er en generisk test-endepunkt, der giver os mulighed for at teste, om \*Arr kan kalde tilbage og oprette forbindelse til Prowlarr uden faktisk at stole på, at en indexer fungerer.
{.is-info}

Her er nogle almindelige årsager

## Kan ikke bestemme ramme størrelse eller en korrupt ramme blev modtaget

`Cannot determine the frame size or a corrupted frame was received.`

Prowlarr havde et sikkerhedsproblem med at oprette forbindelse til webstedet.

Dette skyldes normalt:

- lokale DNS-problemer - Prøv at skifte til en anden DNS-udbyder

## Forbindelse udløbet

`The request timed out`

Prowlarr får ingen respons fra klienten. [Se vores generelle netværks- og tilladelsesfejlfinding](/permissions-and-networking)

Dette skyldes normalt:

- forkert konfigureret eller brug af en VPN
- forkert konfigureret eller brug af en proxy
- lokale DNS-problemer - Prøv at skifte til en anden DNS-udbyder
- lokale IPv6-problemer - normalt er IPv6 aktiveret, men ikke funktionel
- brug af Privoxy

## Sonarr HTTP 404-fejl

- Dette skyldes normalt, at du kører en version af Sonarr, der er nået end of life (EOL) og ikke har v3 API-endepunkterne
- Prowlarr understøtter ikke Sonarr v2
- Prowlarr understøtter kun Sonarr v3

## \*Arr HTTP 400-fejl

- Se denne FAQ-indgang: [Prowlarr vil ikke synkronisere X Indexer til App](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 HTTP-tjeneste utilgængelig

- Dette skyldes normalt, at din tracker blokerer dig via Cloudflare og kræver [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)

## Ugyldige torrents

- Prøv at downloade linket via URL'en og variablerne, som Prowlarr brugte.
- Prøv at downloade torrenten via prowlarr-proxy (dvs. brug linket fra prowlarr, som appen brugte til at hente filen).
- Sørg for, at din cookie eller andre legitimationsoplysninger til din indexer ikke er udløbet og er gyldige.
- Hvis problemet skyldes Prowlarr, bedes du indsende en fejlrapport.

## Søgning på indexere og trackere

- [Lidarr Søgning og Indexere](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Radarr Søgning og Indexere](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Readarr Søgning og Indexere](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Sonarr Søgning og Indexere](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}