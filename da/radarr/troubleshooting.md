---
title: Radarr Fejlfinding
description: Fejlfinding for Radarr, herunder indhentning af logfiler, fejlfinding og almindelige problemer med søgning, og fejlfinding og almindelige problemer med download/import.
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, fejlfinding
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Bed om hjælp](#bed-om-hjælp)
- [Logging og logfiler](#logging-og-logfiler)
  - [Standardplacering for logfiler](#standardplacering-for-logfiler)
  - [Placering af opdateringslogfiler](#placering-af-opdateringslogfiler)
  - [Deling af logfiler](#deling-af-logfiler)
  - [Trace/Debug-logfiler](#tracedebug-logfiler)
  - [Rydning af logfiler](#rydning-af-logfiler)
- [Flere logfiler](#flere-logfiler)
- [Gendannelse efter en mislykket opdatering](#gendannelse-efter-en-mislykket-opdatering)
  - [Afgør problemet](#afgør-problemet)
    - [Database disk image er beskadiget](#database-disk-image-er-beskadiget)
    - [Migrationsproblem](#migrationsproblem)
    - [UI-migrationsproblemer](#ui-migrationsproblemer)
    - [Tilladelsesproblem](#tilladelsesproblem)
  - [Løsning af problemet](#løsning-af-problemet)
    - [Migrationsproblemer](#migrationsproblemer)
    - [Tilladelsesproblemer](#tilladelsesproblemer)
    - [Manuel opgradering](#manuel-opgradering)
- [Downloads og import](#downloads-og-import)
  - [Test af downloadklient](#test-af-downloadklient)
  - [Test af download](#test-af-download)
  - [Test af import](#test-af-import)
  - [Almindelige problemer](#almindelige-problemer)
    - [Downloadklientens webgrænseflade er ikke aktiveret](#downloadklientens-webgrænseflade-er-ikke-aktiveret)
    - [SSL er i brug og er konfigureret forkert](#ssl-er-i-brug-og-er-konfigureret-forkert)
    - [Kan ikke se deling på Windows](#kan-ikke-se-deling-på-windows)
    - [Mapperede netværksdrev er ikke pålidelige](#mapperede-netværksdrev-er-ikke-pålidelige)
    - [Docker og bruger, gruppe, ejerskab, tilladelser og stier](#docker-og-bruger-gruppe-ejerskab-tilladelser-og-stier)
    - [Fjernstyring af sti](#fjernstyring-af-sti)
      - [Fjernmontering eller fjernsynkronisering (Syncthing)](#fjernmontering-eller-fjernsynkronisering-syncthing)
    - [Tilladelser for biblioteksmappen](#tilladelser-for-biblioteksmappen)
    - [Tilladelser for downloadmappen](#tilladelser-for-downloadmappen)
    - [Downloadmappe og biblioteksmappe er ikke forskellige mapper](#downloadmappe-og-biblioteksmappe-er-ikke-forskellige-mapper)
    - [Forkert kategori](#forkert-kategori)
    - [Pakkede torrents](#pakkede-torrents)
    - [Gentagne downloads](#gentagne-downloads)
    - [Usenet-download mangler import](#usenet-download-mangler-import)
    - [Downloadklient rydder elementer](#downloadklient-rydder-elementer)
    - [Download kan ikke matches med et bibliotekselement](#download-kan-ikke-matches-med-et-bibliotekselement)
    - [Forbindelse fik timeout](#forbindelse-fik-timeout)
  - [Problem ikke opført](#problem-ikke-opført)
- [Søgning, indekser og trackere](#søgning-indekser-og-trackere)
  - [Øg logningsniveauet til trace](#øg-logningsniveauet-til-trace)
  - [Test af en indexer eller tracker](#test-af-en-indexer-eller-tracker)
  - [Test af en søgning](#test-af-en-søgning)
  - [Almindelige problemer](#almindelige-problemer-1)
    - [Tracker kræver RawSearch Caps](#tracker-kræver-rawsearch-caps)
    - [Mediet er ikke overvåget](#mediet-er-ikke-overvåget)
    - [Forkerte kategorier](#forkerte-kategorier)
    - [Søgningen returnerede ingen resultater](#søgningen-returnerede-ingen-resultater)
    - [Forkerte resultater](#forkerte-resultater)
    - [Manglende resultater](#manglende-resultater)
    - [Validering af certifikat](#validering-af-certifikat)
    - [Rammer hastighedsbegrænsninger](#rammer-hastighedsbegrænsninger)
    - [IP-blokering](#ip-blokering)
    - [År stemmer ikke overens](#år-stemmer-ikke-overens)
    - [Manglende år](#manglende-år)
    - [Brug af Jackett /all-endepunktet](#brug-af-jackett-all-endepunktet)
    - [Brug af NZBHydra2 som enkeltindgang](#brug-af-nzbhydra2-som-enkeltindgang)
    - [Problem ikke opført](#problem-ikke-opført-1)
  - [Fejl](#fejl)
    - [Forbindelsen blev lukket: Der opstod en uventet fejl under afsendelse](#forbindelsen-blev-lukket-der-opstod-en-uventet-fejl-under-afsendelse)
    - [Anmodningen fik timeout](#anmodningen-fik-timeout)
    - [Problem ikke opført](#problem-ikke-opført-2)

# Bed om hjælp

Har du brug for hjælp? Det er helt i orden, alle har brug for hjælp engang imellem. Du kan få hjælp i realtid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiel Radarr Discord*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiel Radarr Subreddit*](https://reddit.com/r/radarr)
{.links-list}

Men inden du går derhen og poster, skal du sørge for, at din anmodning om hjælp er så god som muligt. Beskriv tydeligt problemet og beskriv kort din opsætning, herunder ting som dit OS/distribution, version af .NET, version af Radarr, downloadklient og dens version. **Hvis du bruger [Docker](https://www.docker.com/), skal du køre [Docker Guide](/docker-guide) først, da det vil løse almindelige og hyppige problemer med stier/tilladelser. Ellers skal du have en [docker compose](/docker-guide#docker-compose) klar. [Sådan genereres en Docker Compose](https://trash-guides.info/compose)** Fortæl os om, hvad du allerede har prøvet, hvad du har kigget på. Brug [Logging og logfiler-sektionen](#logging-og-logfiler) til at øge logningsniveauet til trace, genskabe problemet, indsæt den relevante kontekst på en pastebin og inkluder et link til den i dit indlæg. Du kan måske endda inkludere nogle skærmbilleder for at fremhæve problemet.

Jo mere vi ved, jo nemmere er det at hjælpe dig.

# Logging og logfiler

Det kan være nyttigt at gennemgå de almindelige problemer med fejlfinding:
- [Almindelige problemer med downloads og import](#almindelige-problemer)
- [Almindelige problemer med søgning, indekser og trackere](#almindelige-problemer-1)
{.links-list}

Hvis du bliver bedt om debug-logfiler, vil dine logfiler indeholde `debug`, og hvis du bliver bedt om trace-logfiler, vil dine logfiler indeholde `trace`. Hvis de logfiler, du giver, ikke indeholder nogen af disse, er de ikke de ønskede logfiler.

- Undgå at dele hele logfilen, medmindre du bliver bedt om det.
- Upload ikke logfiler direkte til Discord eller indsæt dem som vægge af tekst, medmindre du bliver bedt om det.
- Del ikke logfiler som vedhæftning, zip-arkiv eller noget andet end tekst, der deles via de nedenfor nævnte tjenester.

For at levere gode og nyttige logfiler til deling:

> Sørg for, at der ikke kører spamopgaver, f.eks. en RSS-opdatering
{.is-warning}

1. [Øg logningsniveauet til trace (Indstillinger => Generelt => Logningsniveau eller Rediger konfigurationsfilen)](#tracedebug-logfiler)
2. [Ryd logfiler (System => Logfiler => Ryd logfiler eller Slet alle logfiler i logmappen)](#rydning-af-logfiler)
3. Genskab problemet (Gentag det, der ødelægger tingene)
4. [Åbn trace-logfilen (radarr.trace.txt) via brugergrænsefladen eller logfilen](#standardplacering-for-logfiler) på filsystemet og find den relevante kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del efter problemet.
6. Brug [Gist](https://gist.github.com/), [0bin (**Sørg for at deaktivere farvegengivelse**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntus Pastebin](https://pastebin.ubuntu.com/) eller lignende websteder - undtagen dem, der er nævnt nedenfor - til at dele de kopierede logfiler fra ovenstående

**Advarsler:**
- **Brug ikke [pastebin.com](https://pastebin.com), da deres filtre har en tendens til at blokere logfilerne.
- Brug ikke [pastebin.pl](https://pastebin.pl), da deres websted ofte ikke er tilgængeligt.
- Brug ikke [JustPasteIt](https://justpaste.it/), da deres websted ikke faciliterer gennemgang af logfiler.
- Upload ikke din log som en fil.
- Upload ikke og del ikke dine logfiler via Google Drive, Dropbox eller andre websteder, der ikke er nævnt ovenfor.
- Arkiver ikke (zip, tar (tarball), 7zip osv.) dine logfiler.
- Del ikke konsoloutput, docker-containeroutput eller noget andet end de angivne programlogfiler

**Vigtig bemærkning:**
- Når du bruger [0bin](https://0bin.net/), skal du sørge for at deaktivere farvegengivelse og ikke brænde efter læsning.

- Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken fil det er, kan du bruge N++. Du kan bruge Notepad++-funktionen "Find i filer" til at søge i gamle logfiler efter behov.
- **Kun Unix:** Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken fil det er, kan du bruge grep. Hvis du f.eks. vil finde oplysninger om film/serier/bøger/sange/indexer "Shooter", kan du køre følgende kommando: `grep -inr -C 100 -e 'Shooter' /sti/til/logfiler/*.trace*.txt` Hvis din [Appdata-mappe](/radarr/appdata-directory) er i din hjemmemappe, skal du køre: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flagene har følgende funktioner
    * -i: ignorér store/små bogstaver
    * -n: vis linjenummer
    *  -r: søg rekursivt i alle filer i stien
    * -C: angiv antallet af linjer før og efter linjen, hvor den blev fundet
    * -e: mønsteret, der skal søges efter

```

## Standardplacering for logfiler

Logfilerne er placeret i Radarrs [Appdata-mappe](/radarr/appdata-directory), inde i mappen logs/. Du kan også få adgang til logfilerne fra brugergrænsefladen under System => Logfiler => Filer.

> Bemærk: Logtabelen ("Events") i brugergrænsefladen er ikke det samme som logfilerne og er ikke lige så nyttig. Hvis du bliver bedt om logfiler, skal du kopiere/indsætte fra logfilerne og ikke tabellen.
{.is-info}

## Placering af opdateringslogfiler

Opdateringslogfilerne er placeret i Radarrs [Appdata-mappe](/radarr/appdata-directory), inde i mappen UpdateLogs/.

## Deling af logfiler

Logfilerne kan være lange og svære at læse som en del af et forum- eller Reddit-indlæg, og de er spamagtige i Discord, så brug venligst [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller en lignende pastebin-tjeneste. Hele filen er normalt ikke nødvendig, kun en god mængde kontekst før og efter problemet/fejlen. Glem ikke at vente på, at spamopgaver som f.eks. en RSS-synkronisering eller biblioteksopdatering bliver færdige.

## Trace/Debug-logfiler

Du kan ændre logningsniveauet under Indstillinger => Generelt => Logning. Radarr behøver ikke genstartes for, at ændringen træder i kraft. Denne ændring påvirker kun logfilerne, ikke logningsdatabasen. De nyeste debug/trace-logfiler har henholdsvis navnene `radarr.debug.txt` og `radarr.trace.txt`.

Hvis du ikke kan få adgang til brugergrænsefladen for at indstille logningsniveauet, kan du gøre det ved at redigere config.xml i AppData-mappen ved at indstille værdien LogLevel til Debug eller Trace i stedet for Info.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Rydning af logfiler

Du kan rydde logfiler og logningsdatabasen direkte fra brugergrænsefladen under System => Logfiler => Filer og System => Logfiler => Slet (Skraldespandsikon)

# Flere logfiler

Radarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid `radarr.txt`, og for de andre filer er `radarr.0.txt` den næstnyeste (jo højere nummer, jo ældre er den). Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.

Når logningsniveauet Debug er aktiveret, vil der være yderligere `radarr.debug.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. De dækker normalt en periode på 40 timer.

Når logningsniveauet Trace er aktiveret, vil der være yderligere `radarr.trace.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af trace-udskriftens omfang dækker de kun et par timer.

# Gendannelse efter en mislykket opdatering

- Vi gør alt, hvad vi kan, for at forhindre problemer ved opgradering, men hvis de opstår, vil dette guide dig gennem trinnene til at gendanne din installation.
- Denne sektion dækker også almindelige problemer efter opdateringen.

## Afgør problemet

- Det bedste sted at kigge, når programmet ikke starter efter en opdatering, er at gennemgå [opdateringslogfilerne](#placering-af-opdateringslogfiler) og se, om opdateringen blev gennemført korrekt. Hvis der ikke er nogen problemer der, er næste skridt at kigge på dine almindelige programlogfiler. Før du prøver at starte igen, skal du bruge [Logging](/radarr/settings#logging) og [Logfiler](/radarr/system#log-files) til at finde dem og øge logningsniveauet.
- Det mest almindelige problem er, at systemet, som appen er installeret på, har rodet med `/tmp`-mappen og slettet kritiske \*Arr-filer under opgraderingen, hvilket forårsager, at både opgraderingen og tilbagerulningen mislykkes. I dette tilfælde skal du blot geninstallere oven på den eksisterende fejlbehæftede installation.

### Database disk image er beskadiget

- Se vores [FAQ-indlæg](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)

### Migrationsproblem

- Migrationsfejl vil ikke være ens, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### UI-migrationsproblemer

- Hvis du skifter mellem [ikke-understøttede versioner/grene](/radarr/faq#can-i-switch-between-branches), kan du opleve et migrationsproblem, der ser ud som nedenstående. Løsningen er at [gå tilbage til den gren eller højere version, du var på tidligere](/radarr/faq#how-do-i-update-radarr) eller [gendan en sikkerhedskopi](/radarr/faq#how-do-i-backuprestore-radarr) for din nuværende version.

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### Tilladelsesproblem

- Tilladelsesproblemer skyldes, at programmet ikke kan få adgang til de relevante midlertidige mapper og/eller programmets binærmappe. Ret tilladelserne, så den bruger/gruppe, som programmet kører som, har den passende adgang.

- Synology-brugere kan støde på denne Synology-fejl "Adgang til stien '/proc/{noget nummer}/maps er nægtet"

- Synology-brugere kan også opleve pladsmangel i `/tmp` på visse NAS-enheder. Du skal angive en anden `/tmp`-sti for appen. Se SynoCommunity eller andre Synology-supportkanaler for hjælp til dette.

## Løsning af problemet

### Migrationsproblemer

Hvis der opstår et migrationsproblem, er der ikke meget, du kan gøre øjeblikkeligt. Hvis problemet er specifikt for dig (eller der endnu ikke er nogen indlæg), skal du oprette et indlæg på [vores subreddit](https://reddit.com/r/radarr) eller besøge vores [discord](https://radarr.video/discord). Hvis der er andre med samme problem, kan du være sikker på, at vi arbejder på det.

> Sørg for, at du ikke har forsøgt at bruge en database fra `nightly`-versionen på den stabile version. Det er ikke en god idé at skifte mellem forskellige versioner af programmet.{.is-info}

### Tilladelsesproblemer

- Ret tilladelserne, så den bruger/gruppe, som applikationen kører som, har adgang (læse- og skriveadgang) til både `/tmp` og installationsmappen for applikationen.

- For Synology-brugere, der oplever problemer med `/proc/###/maps`, bør det løse problemet at stoppe Sonarr eller de andre \*Arr-applikationer og opdatere. Dette er et problem med SynoCommunity-pakken.

### Manuel opgradering

Hent den nyeste version fra vores hjemmeside.

Installer opdateringen (.exe) eller udpak indholdet (.zip) over din eksisterende installation og kør Radarr som du plejer.

# Downloads og import

Downloads og import er det punkt, hvor *de fleste* mennesker oplever problemer. Overordnet set skal Radarr kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Det betyder, at selvom der er nogle *almindelige* opsætninger, er der ikke én *rigtig* opsætning, og alle opsætninger kan være lidt forskellige.

> **Det første skridt er at øge logningsniveauet til Trace. Se [Logning og logfiler](#logning-og-logfiler) for detaljer om, hvordan du justerer logningsniveauet og søger i logfilerne. Du skal derefter genskabe problemet og bruge logfilerne med trace-niveau fra den tidsramme til at undersøge problemet.** Hvis nogen hjælper dig, skal du lægge kontekst fra før/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende side for at vise dem det. Det behøver ikke være hele filen, og det bør ikke *kun* være fejlen. Du skal også genskabe problemet, mens opgaver, der spammer logfilen, ikke kører.
{.is-danger}

Når du beder om hjælp, skal du sørge for at læse [om at bede om hjælp](#om-at-bede-om-hjælp), så du kan give os de oplysninger, vi har brug for.

## Test af downloadklienten

Sørg for, at dine downloadklient(er) kører. Start med at teste downloadklienten, hvis den ikke fungerer, kan du se detaljer i logfilerne med trace-niveau. Du skal finde en URL, som du kan indsætte i din browser og se, om den virker. Det kan være et forbindelsesproblem, der kan indikere en forkert IP, værtsnavn, port eller endda en firewall, der blokerer adgangen. Det kan også være åbenlyst, f.eks. et godkendelsesproblem, hvor du har indtastet brugernavn, adgangskode eller API-nøgle forkert. Bemærk, at nogle seedboxes kræver brug af https, port 443 og en URL-base (avancerede indstillinger) i stedet for din downloadklients rigtige port.

## Test af en download

Nu vil vi prøve en download. Vælg en film og foretag en manuel søgning. Vælg en af disse filer og forsøg at downloade den. Bliver den sendt til downloadklienten? Ender den i den korrekte kategori? Viser den sig i Aktivitet? Viser den sig i logfilerne med trace-niveau under opgaverne **Check For Finished Download** (opdater overvågede downloads og behandle overvågede downloads), som kører cirka hvert minut? Bliver den korrekt analyseret i den opgave? Har den download, der er sat i kø, et rimeligt navn? Da søgninger foretages efter id på nogle indexer/trackere, kan den sætte en download i kø med et navn, den ikke kan genkende.

## Test af en import

Importproblemer bør næsten altid vise sig som en post i Aktivitet med et orange ikon, hvor du kan holde musen hen over for at se fejlen. Hvis de ikke vises i Aktivitet, er dette det problem, du skal fokusere på først, så gå tilbage og find ud af det. De fleste importfejl skyldes *tilladelser*, så husk, at Radarr skal kunne læse og skrive i downloadmappen. Nogle gange kan tilladelser i biblioteksmappen også være problemet, så sørg for at kontrollere begge dele.

Forkerte stistrengsproblemer er også mulige, selvom de er mindre almindelige i normale opsætninger. Nøglen til at forstå stistrengsproblemer er at vide, at Radarr får stien til downloaden *fra* downloadklienten via dens API. Dette bliver et problem i mere unikke tilfælde, f.eks. når downloadklienten kører på et andet system (måske endda et andet operativsystem\!). Det kan også forekomme i en Docker-opsætning, når volumener ikke er konfigureret korrekt. En fjern stistrengsafbildning er en god løsning, når du ikke har kontrol, f.eks. i en seedbox-opsætning. I en Docker-opsætning er det bedre at rette stierne.

## Almindelige problemer

Her er nogle almindelige problemer.

### Downloadklientens webgrænseflade er ikke aktiveret

Radarr kommunikerer med din downloadklient via dens API og får adgang til den via klientens webgrænseflade. Du skal sikre dig, at klientens webgrænseflade er aktiveret, og at den port, den bruger, ikke konflikter med andre klientporte, der er i brug, eller porte, der er i brug på dit system.

### Forkert konfigureret SSL

Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din instans og din downloadklient på et lokalt netværk. Se [SSL FAQ-indlægget](/radarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for mere information.

### Kan ikke se deling på Windows

Standardbrugeren for en Windows-tjeneste er `LocalService`, som typisk ikke har adgang til dine delinger. Rediger tjenesten og konfigurer den til at køre som din egen bruger. Se FAQ-indlægget [hvorfor kan jeg ikke se mine filer på en fjernserver](/radarr/faq#why-cant-i-see-my-files-on-a-remote-server) for detaljer.

### Kortlagte netværksdrev er ikke pålidelige

Selvom kortlagte netværksdrev som `X:\` er praktiske, er de ikke så pålidelige som UNC-stier som `\\server\share`, og de er heller ikke tilgængelige før login. Konfigurer din opsætning og dine downloadklient(er), så de bruger UNC-stier efter behov. Hvis dit bibliotek er på en delt mappe, skal du sørge for, at dine rodmapper bruger UNC-stier. Hvis din downloadklient sender til en delt mappe, er det der, du skal konfigurere UNC-stier, da Radarr får downloadstien fra downloadklienten. Det er fint at beholde dine kortlagte netværksdrev til personlig brug, bare brug dem ikke til automatisering.

### Docker og bruger, gruppe, ejerskab, tilladelser og stier

Docker tilføjer et ekstra lag af kompleksitet, som er nemt at gøre forkert, men stadig ende op med en opsætning, der fungerer, men har forskellige problemer. I stedet for at gennemgå dem her, skal du læse denne wiki-artikel [om disse automatiseringssoftware og Docker](/docker-guide), som handler om bruger, gruppe, ejerskab, tilladelser og stier. Den er ikke specifik for nogen Docker-system, i stedet går den over tingene på et overordnet niveau, så du kan implementere dem i din egen miljø.

### Fjern stistrengsafbildning

Hvis du har Radarr i Docker og Downloadklienten uden for Docker (eller omvendt) eller har programmerne på forskellige servere, kan du have brug for en fjern stistrengsafbildning.

Logfilerne vil angive noget lignende.

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Så `/volume3/data` eksisterer ikke inden for Radarrs container eller er ikke tilgængelig.

- [Indstillinger => Downloadklienter => Fjern stistrengsafbildninger](/radarr/settings#remote-path-mappings)
- En fjern stistrengsafbildning bruges, når din downloadklient rapporterer en sti for fuldførte data enten på en anden server eller på en måde, som \*Arr ikke adresserer den mappe.
- Generelt er en fjern stistrengsafbildning kun nødvendig, hvis din downloadklient kører på Linux, når \*Arr kører på Windows eller omvendt. En fjern stistrengsafbildning kan også være nødvendig, hvis du blander Docker- og Native-klienter, eller hvis du bruger en fjernserver.
- En fjern stistrengsafbildning er en DUMB søgning/erstatning (hvor den finder den FJERNE værdi og erstatter den med den LOKALE værdi for den angivne vært).
- Hvis fejlmeddelelsen om en forkert sti ikke indeholder den ERSTATTEDE værdi, fungerer sti-afbildningen ikke, som du forventer. Den typiske løsning er at tilføje og fjerne afbildningen.
- [Se TRaSH's vejledning for yderligere oplysninger om fjern stistrengsafbildning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og din downloadklient er Docker-containere, er det sjældent nødvendigt med en fjern stistrengsafbildning. Det anbefales at [gennemgå Docker-guiden](/docker-guide) og/eller [følge TRaSH's vejledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Fjernmontering eller fjernsynkronisering (Syncthing)

- Du skal sørge for, at det synkroniserer hele tiden, mens det downloader. Og du skal sørge for, at den lokale synkroniseringsdestination kan være hardlinks, når \*Arr importerer, hvilket betyder samme filsystem og ser ud som det.
  - Synkronisér til en lavere, fælles mappe, der indeholder både ufuldstændige og fuldstændige filer.
  - Synkronisér til en placering, der er på samme filsystem lokalt som dit bibliotek og ser ud som det (Docker og netværksdelinger gør det nemt at konfigurere forkert).
  - Du vil gerne synkronisere det ufuldstændige og fuldstændige, så når torrentklienten flytter, afspejles det lokalt, og alle filerne er allerede "der" (selvom de stadig downloades). Derefter vil du bruge hardlinks, fordi selvom det importerer, før det er færdigt, vil det stadig blive færdigt.
  - På denne måde synkroniserer det hele tiden, mens det downloader, så torrentklienten flytter til undermappe til tv, og synkroniseringen afspejler det. På den måde er downloads stort set der, når de er erklæret færdige. Og selvom de ikke er helt færdige, betyder muligheden for hardlink stadig, at det er okay.
  - (Valgfrit - hvis det er relevant og/eller påkrævet (f.eks. fjern usenet-klient)) Konfigurer et brugerdefineret script, der skal køres ved import/download/opgradering for at fjerne den fjerneste fil.
- Alternativt er en fjernmontering i stedet for en fjernsynkroniseringssætning betydeligt mindre kompliceret at konfigurere, men typisk langsommere.
  - Monter din fjernlagring med sshfs eller en anden netværksfilsystemprotokol.
  - Sørg for, at brugeren og gruppen, som \*Arr er konfigureret til at køre som, har læse- eller skriveadgang.
  - Konfigurer en fjern stistrengsafbildning for at finde den FJERNE sti og erstatte den med den LOKALE ækvivalent.

### Tilladelser på biblioteksmappen

Logfilerne vil se sådan ud

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Glem ikke at kontrollere tilladelser og ejerskab for *destinationen*. Det er nemt at fokusere på downloadens ejerskab og tilladelser, og det er *normalt* årsagen til tilladelsesrelaterede problemer, men det *kan* også være destinationen. Kontrollér, at destinationsmappen(e) eksisterer. Kontrollér, at en destinations *fil* ikke allerede eksisterer eller ikke kan slettes eller flyttes til papirkurven. Kontrollér, at ejerskab og tilladelser tillader, at den downloadede fil kan kopieres, hardlinkes eller flyttes. Brugeren eller gruppen, der kører som, skal kunne læse og skrive i rodmappen.

- For Windows-brugere kan dette skyldes, at det kører som en tjeneste:
  - Windows-tjenesten kører under kontoen 'Local Service', som som standard ikke har tilladelser til at få adgang til din brugers hjemmemappe, medmindre der er tildelt tilladelser manuelt. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.
  - 'Local Service' har også generelt meget begrænsede tilladelser. Det anbefales derfor at installere appen som en systembakkeapplikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette tilbydes under installationen. Se FAQ'en for, hvordan du konverterer fra en tjeneste til en bakkeapp.

- For Synology-brugere henvises der til [SynoCommunity's artikel om tilladelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruger en NFS-montering, skal du sørge for, at `nolock` er aktiveret.
- Hvis du bruger en SMB-montering, skal du sørge for, at `nobrl` er aktiveret.

### Tilladelser på downloadmappen

Logfilerne vil se sådan ud

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Glem ikke at kontrollere tilladelser og ejerskab for *kilden*. Det er nemt at fokusere på destinationens ejerskab og tilladelser, og det er en *mulig* årsag til tilladelsesrelaterede problemer, men det er typisk kilden. Kontrollér, at kildekappen(e) eksisterer. Kontrollér, at ejerskab og tilladelser tillader, at den downloadede fil kan kopieres/hardlinkes eller kopieres+slettes/flyttes. Brugeren eller gruppen, der kører som, skal kunne læse og skrive i downloadmappen.

- For Windows-brugere kan dette skyldes, at det kører som en tjeneste:
  - Windows-tjenesten kører under kontoen 'Local Service', som som standard ikke har tilladelser til at få adgang til din brugers hjemmemappe, medmindre der er tildelt tilladelser manuelt. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.
  - 'Local Service' har også generelt meget begrænsede tilladelser. Det anbefales derfor at installere appen som en systembakkeapplikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette tilbydes under installationen. Se FAQ'en for, hvordan du konverterer fra en tjeneste til en bakkeapp.

- For Synology-brugere henvises der til [SynoCommunity's artikel om tilladelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruger en NFS-montering, skal du sørge for, at `nolock` er aktiveret.
- Hvis du bruger en SMB-montering, skal du sørge for, at `nobrl` er aktiveret.

### Downloadmappe og biblioteksmappe er ikke forskellige mapper

Downloadklienten skal downloade til en mappe, som \*Arr kan få adgang til, og som ikke er din rod-/biblioteksmappe. Den skal importere fra den separate downloadmappe til din biblioteksmappe. Du skal aldrig downloade direkte til din rodmappe. Du skal heller ikke bruge din rodmappe som downloadklientens fuldførte mappe eller ufuldstændige mappe.

> Din downloadmappe og din rod-/biblioteksmappe SKAL være separate
{.is-warning}

### Forkert kategori

Radarr skal konfigureres til at bruge en kategori, så den kun forsøger at behandle sine egne downloads. Det er sjældent, at en torrent, der er indsendt af \*Arr, bliver tilføjet uden den korrekte kategori, men det kan ske. Hvis du manuelt tilføjer torrents og vil behandle dem, skal de have den korrekte kategori. Den kan indstilles når som helst, da \*Arr forsøger at behandle downloads hvert minut.

### Pakkede torrents

Logfilerne vil angive fejl som

```none
No files found are eligible for import
```

Hvis din torrent er pakket i `.rar`-filer, skal du konfigurere udpakning. Vi anbefaler [Unpackerr](https://github.com/unpackerr/unpackerr), da det gør udpakning rigtigt: forhindrer korrupte delvise importeringer og rydder op i de udpakkede filer efter importen.

Fejlen kan også ses, hvis der ikke er nogen gyldig mediefil i mappen.

### Gentagne downloads

Der er flere årsager til gentagne downloads, men en af dem er relateret til brugerdefinerede formater. Det er muligt, at udgivelsesnavnet matcher et brugerdefineret format, men downloadfilerne gør det ikke. Dette får dig ind i en løkke, hvor du downloader elementerne igen og igen, fordi det ser ud som en opgradering, så er det ikke, så vises det igen og ser ud som en opgradering, så er det ikke. Afhængigt af dit brugerdefinerede format kan du muligvis omgå dette ved at inkludere det brugerdefinerede format i dit omdøbningsskema. (Aktivér brugerdefineret format for at blive inkluderet i omdøbning og tilføj derefter brugerdefineret format til dit omdøbningsskema)

Dette kan også skyldes, at downloaden faktisk aldrig importeres og derefter mangler fra køen, så der hentes en ny download konstant og aldrig importeres. Se venligst de forskellige andre almindelige problemer og fejlfindingstrin for dette.

### Usenet-download mangler import

Radarr ser kun på de 60 seneste downloads i SABnzbd og NZBGet, så hvis du beholder din historik, betyder det, at under store køer med importproblemer kan downloads blive overset og ikke importeret. Den bedste måde at undgå dette på er at holde din historik ren, så eventuelle elementer, der stadig vises, skal undersøges. Du kan opnå dette ved at aktivere Fjern under Afsluttede og Mislykkede Download Handler. I NZBGet flytter dette elementer til den skjulte historik, hvilket er fantastisk. Desværre har SABnzbd ikke en lignende funktion. Det bedste, du kan opnå der, er at bruge nzb-backupmappen.

### Downloadklient rydder elementer

Downloadklienten skal *ikke* være ansvarlig for at fjerne downloads. Usenet-klienter skal konfigureres, så de *ikke* fjerner downloads fra historikken. Torrent-klienter skal konfigureres, så de *ikke* fjerner torrents, når de er færdige med at seede (pause eller stop i stedet). Dette skyldes, at Radarr kommunikerer med downloadklienten for at vide, hvad der skal importeres, så hvis de *fjernes*, er der intet at importere... selvom der er en mappe fuld af filer.

For SABnzbd håndteres dette med indstillingen Historikbevaring.

### Download kan ikke matches med et bibliotekselement

Af forskellige årsager kan udgivelser ikke analyseres, når de er hentet og sendt til downloadklienten. Aktivitet => Indstillinger => Vis ukendt (dette er nu aktiveret som standard i nyere versioner) viser alle elementer, der ikke er ignoreret / allerede importeret inden for \*Arr's downloadklientkategori. Disse skal typisk manuelt tilknyttes og importeres.

Årsager inkluderer:
- Filnavnet har et `:` på TMDb, og TMDb har ingen alternativ titel med en `-` eller med et mellemrum, der erstatter `:`
- Filnavnet mangler året, som er påkrævet
- AKA eller mærkelige flere navne; Radarr har begrænset support til disse
- Filnavnet matcher flere film
- Udgivelsesnavn eller udgivelses-ID fra indekseren stemmer ikke overens med filnavnet

Dette kan også forekomme, hvis du har en udgivelse i din downloadklient, men det medieelement (film/episode/bog/sang) eksisterer ikke i applikationen.

### Forbindelsen blev lukket: Der opstod en uventet fejl under afsendelse

Dette skyldes, at indekseren bruger en SSL-protokol, som ikke understøttes af den aktuelle .NET-version, der findes i [Radarr => System => Status](/radarr/system#status).

### Anmodningen udløb

Radarr modtager ingen respons fra klienten.

```none
    System.NET.WebException: Anmodningen udløb: ’https://example.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Anmodningen udløb
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke oprette forbindelse til indekser

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En opgave blev annulleret.
```

Dette kan også skyldes:

- forkert konfigureret eller brug af en VPN
- forkert konfigureret eller brug af en proxy
- lokale DNS-problemer - Prøv at skifte til en anden DNS-udbyder
- lokale IPv6-problemer - typisk er IPv6 aktiveret, men ikke funktionsdygtig
- brugen af Privoxy og at det er forkert konfigureret

## Problem ikke angivet

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers diskuter problemet med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, skal du foreslå at tilføje det til wikien.

# Søgning i indekser og trackere

- Hvis du bruger [Prowlarr](/prowlarr), kan du se [Historikken](/prowlarr/history) over alle forespørgsler, som Prowlarr har modtaget, og hvordan de blev sendt til webstederne. Sørg for, at `Parametre` er aktiveret i Prowlarr Historik => Indstillinger. (i) ikonet giver yderligere detaljer.

## Skru logningen op til sporingsniveau

> **Det første skridt er at skrue logningen op til Sporingsniveau, se [Logning og logfiler](#logning-og-logfiler) for detaljer om justering af logning og søgning i logfilerne. Du vil derefter reproducere problemet og bruge sporingsniveau-logfilerne fra den tidsramme til at undersøge problemet.** Hvis nogen hjælper dig, skal du lægge kontekst fra før/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende side for at vise dem det. Det behøver ikke at være hele filen, og det bør ikke *kun* være fejlen. Du skal også reproducere problemet, mens opgaver, der spammer logfilen, ikke kører.
{.is-danger}

## Test af en indekser eller tracker

Når du tester en indekser eller tracker, kan du i debug- eller sporingslogfilerne finde den anvendte URL. Et eksempel på en vellykket test er nedenstående, hvor du kan se, at den forespørger indekseren via en specifik URL med specifikke parametre og derefter responsen. Du kan teste denne URL i din browser ved at erstatte `apikey=(fjernet)` med den korrekte api-nøgle som f.eks. `apikey=123`. Du kan eksperimentere med parametrene, hvis du får en fejl fra indekseren, eller se om du har forbindelsesproblemer, hvis det slet ikke virker. Efter at have testet i din egen browser, skal du teste fra systemet, der kører *hvis* du ikke allerede har gjort det.

## Test af en søgning

Ligesom testen af indekser/tracker ovenfor, når du udløser en søgning ved hjælp af debug- eller sporingsniveau-logning, kan du få URL'en fra logfilerne. Under testen er det bedst at bruge en så snæver søgning som muligt. En manuel søgning er god, fordi den er specifik, og du kan se resultaterne i brugergrænsefladen, mens du undersøger logfilerne.

I denne test vil du kigge efter åbenlyse fejl og køre nogle simple tests. Du kan se, at søgningen brugte URL'en `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(fjernet)&q=O+Brother+Where+Art+Thou`, som du kan prøve selv i en browser efter at have erstattet `(fjernet)` med din api-nøgle for den indekser. Virker det? Ser du de forventede resultater? I den URL kan du se, at den har angivet den specifikke kategori 2000, så hvis du ikke ser de forventede resultater, er dette en sandsynlig årsag. Hvis filmen ikke er korrekt kategoriseret på indekseren, skal det rettes. Se Manual Søgning XML Output nedenfor for at se et eksempel på output fra en fungerende forespørgsel.

- Manuel Søgning XML Output

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

***Billeder er nødvendige***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- Sporingslogudsnit

```none
Uddrag af sporingslog for en manuel søgning er nødvendigt
```

- Fuld sporingslog for en søgning

```none
Fuld sektion af sporingslog for en manuel søgning er nødvendigt
```

## Almindelige problemer

Her er nogle almindelige problemer.

### Tracker kræver RawSearch Caps

- Radarr søger efter `Kikis Delivery Service`, men din tracker har kun resultater for `Kiki's Delivery Service`
- Dette skyldes, at din tracker ikke understøtter normale standardiserede søgninger.
- Løsningen er, at din trackers definition af søgefunktioner skal opdateres for at angive, at den [kræver og understøtter `RawSearch`](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905)
- Jackett understøtter flaget, men funktionerne skal opdateres for hver indekser. Opret en funktionanmodning til Jackett for at tilføje denne funktionalitet for din indekser.
- Prowlarr understøtter flaget, men funktionerne skal opdateres for hver indekser. Opret en funktionanmodning til Prowlarr for at tilføje denne funktionalitet for din indekser.

### Mediet er ikke overvåget

Filmene er ikke overvåget.

### Forkerte kategorier

Forkerte kategorier er sandsynligvis den mest almindelige årsag til, at resultater vises i manuelle søgninger på en indexer/tracker, men *ikke* i Radarr. Indexeren/trackeren *bør* vise kategorien i søgeresultaterne, hvilket burde hjælpe dig med at finde ud af, hvad der mangler. Hvis du bruger Jackett eller Prowlarr, har hver tracker en liste over specifikt understøttede kategorier. Sørg for at bruge de korrekte kategorier for Radarr. Mange finder det nyttigt at have listen synlig i et browser-vindue, mens de redigerer indtastningen.

### Søgning lykkedes - Ingen resultater returneret

Du modtager en besked lignende `Søgning lykkedes, men der blev ikke returneret nogen resultater fra din indexer. Dette kan være et problem med indexerens eller dine indexer-kategorioptællinger.`

Dette skyldes, at din indexer ikke returnerer nogen resultater, der er inden for de kategorier, du har konfigureret for indexereren.

### Forkerte resultater

Nogle gange returnerer indexere helt irrelevante resultater, Radarr vil give parametre for at begrænse søgningen, men de returnerede resultater er helt irrelevante. Eller nogle gange, mest relateret med nogle forkerte resultater. Det første er normalt et indexer-problem, og du kan se det fra sporlogs, der viser, hvad der forårsager det. Du kan deaktivere den indexer og rapportere problemet. Det andet er normalt kategoriserede udgivelser, som kan rapporteres på indexer/trackeren.

### Manglende resultater

Hvis du har resultater på webstedet, som du kan finde, men som ikke vises i Radarr, er dit problem sandsynligvis en af flere muligheder:

- [Kategorier er forkerte - Se ovenfor](#forkerte-kategorier)
- Der udføres en søgning baseret på en ID (IMDbId, TMDbId osv.), og indexereren har ikke korrekt kortlagt udgivelserne til den ID. Dette er noget, kun din indexer kan løse. De skal sikre, at udgivelsen er kortlagt til de korrekte anvendelige id'er.
- Du søger ikke på samme måde som Radarr søger; Det er meget sandsynligt, at de vilkår, du søger på indexereren, ikke er, hvordan Radarr søger det. Du kan se, hvordan Radarr søger i sporlogs. Tekstbaserede forespørgsler vil generelt være i formatet `q=ord%20og%20ting%20her` denne streng er HTTP-kodet og kan nemt afkodes ved hjælp af et hvilket som helst HTML-afkodnings-/kodningsværktøj online.
- [Se FAQ'en for, hvordan udenlandske film eller udenlandske titler håndteres af Radarr og hvornår Radarr vil søge efter dem](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### Certifikatvalidering

Du vil oprette forbindelse til de fleste indexere/trackere via https, så du skal have det til at fungere korrekt på dit system. Det betyder, at din tidszone og tid begge skal være indstillet *korrekt*. Det betyder også, at dine systemcertifikater skal være opdaterede.

### Rammer rategrænser

Hvis du kører din gennem en VPN eller proxy, kan du konkurrere med 10'er eller 100'er eller 1000'er af andre mennesker, der alle prøver at bruge tjenester som , theXEM og/eller dine indexere og trackere. Ratebegrænsning og DDOS-beskyttelse udføres ofte efter IP-adresse, og din VPN-/proxy-udgangspunkt er *én* IP-adresse. Medmindre du er i et undertrykkende land som Kina, Australien eller Sydafrika, behøver du ikke VPN/proxy .

Rarbg har en tendens til at have en form for ratebegrænsning inden for deres API og vises som svarer med ingen resultater.

### IP-blokering

På samme måde som rategrænser kan visse indexere - som Nyaa - direkte blokere en IP-adresse. Dette er typisk halvpermanent, og løsningen er at få en ny IP fra din internetudbyder eller VPN-udbyder.

### År stemmer ikke overens

- [Se dette FAQ-indlæg](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr får metadata fra TMDb
  - Radarr bruger året for den ældste **biografudgivelses**dato og den ældste **premiere**dato til matchning
- I nogle tilfælde blev filmen skubbet eller flyttet rundt, og året, der bruges af udgivelsesgrupperne, stemmer ikke overens med hverken det ældste premiereårs dato eller det ældste biografudgivelsesårs dato. I disse situationer skal du hente og importere manuelt.

### Manglende år

Radarr vil ikke hente en udgivelse, hvis udgivelsesnavnet ikke indeholder et år. Dette er en dårlig udgivelse og kan kun hentes manuelt. Dette er en almindelig ting at overse, når man prøver at finde ud af, hvorfor en film ikke blev hentet som forventet.

### Brug af Jackett /all-endepunktet

Jackett `/all`-endepunktet er praktisk, men det er den eneste fordel. Alt andet kan være potentielle problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje at prøve Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Selv Jackett siger, at /all bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)

Brug af all-endepunktet har ingen fordele (udover reduceret administrationsarbejde), kun ulemper:

- du mister kontrol over indexer-specifikke indstillinger (kategorier, søgemetoder osv.)
- blanding af søgemetoder (IMDB, forespørgsel osv.) kan medføre resultater af lav kvalitet
- indexer-specifikke kategorier (\>= 100000) kan ikke bruges.
- langsomme indexere vil bremse det samlede resultat
- det samlede antal resultater er begrænset til 1000

Ved at tilføje hver indexer separat kan du finjustere kategorierne for hver indexer, hvilket kan være et problem med `/all`-endepunktet, hvis brug af den forkerte kategori forårsager fejl på nogle trackere. I , er hver indexer begrænset til 1000 resultater, hvis sideinddeling understøttes, eller 100, hvis det ikke er tilfældet, hvilket betyder, at jo flere trackere du tilføjer til Jackett, desto mere sandsynligt er det, at du klipper resultater. Endelig, hvis *én* af trackerne i `/all` returnerer en fejl, vil  deaktivere den, og nu får du ingen resultater.

### Brug af NZBHydra2 som en enkelt indgang

Brug af NZBHydra2 som en enkelt indexer-indgang (dvs. 1 NZBHydra2-indgang i Radarr for mange indexere i NZBHydra2) i stedet for flere (dvs. mange NZBHydra2-indgange i Radarr for mange indexere i NZBHydra2) har de samme problemer som nævnt ovenfor med Jacketts `/all`-endepunkt.

### Problem ikke nævnt

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers diskuter det med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, kan du foreslå at tilføje det til wikien.

## Fejl

Her er nogle af de almindelige fejl, du kan se, når du tilføjer en indexer

### Forbindelsen blev lukket: Der opstod en uventet fejl under afsendelse

Dette skyldes, at indexereren bruger en SSL-protokol, som ikke understøttes af den aktuelle .NET-version, der findes i [Radarr => System => Status](/radarr/system#status).

### Anmodningen udløb

Radarr modtager intet svar fra indexereren.

```none
    System.NET.WebException: Anmodningen udløb: ’https://example.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Anmodningen udløb
```

```none
2022-11-01 10:16:54.3|Advarsel|Newznab|Kan ikke oprette forbindelse til indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: En opgave blev annulleret.
```

Dette kan også skyldes:

- forkert konfigureret eller brug af en VPN
- forkert konfigureret eller brug af en proxy
- lokale DNS-problemer - Prøv at skifte til en anden DNS-udbyder
- lokale IPv6-problemer - typisk er IPv6 aktiveret, men ikke funktionsdygtig
- brug af Privoxy og forkert konfiguration af det

### Problem ikke nævnt

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers diskuter det med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, kan du foreslå at tilføje det til wikien.