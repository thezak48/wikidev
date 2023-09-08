---
title: Sonarr Fejlfinding
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, fejlfinding
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [At bede om hjælp](#at-bede-om-hjælp)
- [Logging og logfiler](#logging-og-logfiler)
  - [Standardplacering for logfiler](#standardplacering-for-logfiler)
  - [Placering af opdateringslogfiler](#placering-af-opdateringslogfiler)
  - [Deling af logfiler](#deling-af-logfiler)
  - [Trace/Debug-logfiler](#tracedebug-logfiler)
  - [Rydning af logfiler](#rydning-af-logfiler)
- [Flere logfiler](#flere-logfiler)
- [Gendannelse efter en mislykket opdatering](#gendannelse-efter-en-mislykket-opdatering)
  - [Afgør problemet](#afgør-problemet)
    - [Migrationsproblem](#migrationsproblem)
    - [Tilladelsesproblem](#tilladelsesproblem)
  - [Løsning af problemet](#løsning-af-problemet)
    - [Tilladelsesproblemer](#tilladelsesproblemer)
    - [Manuel opgradering](#manuel-opgradering)
- [Downloads og import](#downloads-og-import)
  - [Test af downloadklienten](#test-af-downloadklienten)
  - [Test af en download](#test-af-en-download)
  - [Test af en import](#test-af-en-import)
  - [Almindelige problemer](#almindelige-problemer)
    - [En eller flere forventede episoder i udgivelsen blev ikke importeret eller mangler](#en-eller-flere-forventede-episoder-i-udgivelsen-blev-ikke-importeret-eller-mangler)
    - [Brug af Sonarr v2](#brug-af-sonarr-v2)
    - [Downloadklientens webgrænseflade er ikke aktiveret](#downloadklientens-webgrænseflade-er-ikke-aktiveret)
    - [SSL i brug og forkonfigureret](#ssl-i-brug-og-forkonfigureret)
    - [Kan ikke se deling på Windows](#kan-ikke-se-deling-på-windows)
    - [Kortlagte netværksdrev er ikke pålidelige](#kortlagte-netværksdrev-er-ikke-pålidelige)
    - [Docker og bruger, gruppe, ejerskab, tilladelser og stier](#docker-og-bruger-gruppe-ejerskab-tilladelser-og-stier)
    - [Fjernsti-mapping](#fjernsti-mapping)
      - [Fjernmontering eller fjernsynkronisering (Syncthing)](#fjernmontering-eller-fjernsynkronisering-syncthing)
    - [Tilladelser på biblioteksmappen](#tilladelser-på-biblioteksmappen)
    - [Tilladelser på downloadmappen](#tilladelser-på-downloadmappen)
    - [Downloadmappe og biblioteksmappe er ikke forskellige mapper](#downloadmappe-og-biblioteksmappe-er-ikke-forskellige-mapper)
    - [Forkert kategori](#forkert-kategori)
    - [Pakkede torrents](#pakkede-torrents)
    - [Gentagne downloads](#gentagne-downloads)
    - [Usenet-download går glip af import](#usenet-download-går-glip-af-import)
    - [Downloadklient rydder elementer](#downloadklient-rydder-elementer)
    - [Download kan ikke matches til et bibliotekselement](#download-kan-ikke-matches-til-et-bibliotekselement)
      - [Fandt matchende serie via grab-historik, men serien blev matchet efter seriens ID. Automatisk import er ikke mulig](#fandt-matchende-serie-via-grab-historik-men-serien-blev-matchet-efter-seriens-id-automatisk-import-er-ikke-mulig)
    - [Episodenavn er TBA](#episodenavn-er-tba)
    - [Forbindelse udløb](#forbindelse-udløb)
  - [Problem ikke opført](#problem-ikke-opført)
- [Søgning i indekser og trackere](#søgning-i-indekser-og-trackere)
  - [Øg logningsniveauet til trace](#øg-logningsniveauet-til-trace)
  - [Test af en indekser eller tracker](#test-af-en-indekser-eller-tracker)
  - [Test af en søgning](#test-af-en-søgning)
  - [Almindelige problemer](#almindelige-problemer-1)
    - [Indekser bliver ikke søgt](#indekser-bliver-ikke-søgt)
    - [Dårligt navngivne udgivelser](#dårligt-navngivne-udgivelser)
    - [Tracker har brug for RawSearch Caps](#tracker-har-brug-for-rawsearch-caps)
    - [Serie har brug for et alias](#serie-har-brug-for-et-alias)
    - [Serie har brug for en XEM-mapping](#serie-har-brug-for-en-xem-mapping)
    - [Forkert serietype](#forkert-serietype)
      - [Daglig](#daglig)
      - [Standard](#standard)
      - [Anime](#anime)
    - [Mediet er ikke overvåget](#mediet-er-ikke-overvåget)
    - [Søgning lykkedes - ingen resultater returneret](#søgning-lykkedes-ingen-resultater-returneret)
    - [Forkerte kategorier](#forkerte-kategorier)
    - [Forkerte resultater](#forkerte-resultater)
    - [Manglende resultater](#manglende-resultater)
    - [Certifikatvalidering](#certifikatvalidering)
    - [Rammer hastighedsgrænser](#rammer-hastighedsgrænser)
    - [IP-blokering](#ip-blokering)
    - [Brug af Jackett /all-endepunktet](#brug-af-jackett-all-endepunktet)
    - [Brug af NZBHydra2 som enkeltindgang](#brug-af-nzbhydra2-som-enkeltindgang)
    - [Indekser bliver ikke søgt](#indekser-bliver-ikke-søgt-1)
    - [Jackett-manuel søgning finder flere resultater](#jackett-manuel-søgning-finder-flere-resultater)
    - [Release-profiler bliver ikke respekteret](#release-profiler-bliver-ikke-respekteret)
    - [Problem ikke opført](#problem-ikke-opført-1)
  - [Fejl](#fejl)
    - [Forbindelsen blev lukket: Der opstod en uventet fejl under afsendelse](#forbindelsen-blev-lukket-der-opstod-en-uventet-fejl-under-afsendelse)
    - [Anmodningen udløb](#anmodningen-udløb)
    - [Problem ikke opført](#problem-ikke-opført-2)

# At bede om hjælp

Har du brug for hjælp? Det er okay, alle har brug for hjælp engang imellem. Du kan få hjælp i realtid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiel Sonarr Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiel Sonarr Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

Men inden du går derhen og poster, skal du sørge for, at din anmodning om hjælp er så god som muligt. Beskriv tydeligt problemet og beskriv kort din opsætning, herunder ting som dit OS/distribution, version af .net/Mono, version af Sonarr, downloadklient og dens version. **Hvis du bruger [Docker](https://www.docker.com/), skal du køre [Docker Guide](/docker-guide) først, da det vil løse almindelige og hyppige problemer med stier/tilladelser. Ellers skal du have en [docker compose](/docker-guide#docker-compose) klar. [Sådan genereres en Docker Compose](https://trash-guides.info/compose)** Fortæl os om, hvad du allerede har prøvet, hvad du har kigget på. Brug [Logging og logfiler](#logging-og-logfiler) til at øge logningsniveauet til trace, genskabe problemet, indsæt den relevante kontekst på en pastebin og inkluder et link til den i dit indlæg. Du kan endda inkludere nogle skærmbilleder for at fremhæve problemet.

Jo mere vi ved, jo nemmere er det at hjælpe dig.

# Logging og logfiler

Det kan være nyttigt at gennemgå de almindelige problemer med fejlfinding:
- [Almindelige problemer med downloads og import](#almindelige-problemer)
- [Almindelige problemer med søgning i indekser og trackere](#almindelige-problemer-1)
{.links-list}

Hvis du bliver bedt om fejlfindingslogfiler, vil dine logfiler indeholde `debug`, og hvis du bliver bedt om trace-logfiler, vil dine logfiler indeholde `trace`. Hvis de logfiler, du leverer, ikke indeholder nogen af disse, er det ikke de ønskede logfiler.

- Undgå at dele hele logfilen, medmindre du bliver bedt om det.
- Upload ikke logfiler direkte til Discord eller indsæt dem som vægge af tekst, medmindre du bliver bedt om det.
- Del ikke logfiler som vedhæftning, zip-arkiv eller noget andet end tekst, der deles via de nedenfor nævnte tjenester.

For at levere gode og nyttige logfiler til deling:

> Sørg for, at der ikke kører en spamopgave, f.eks. en RSS-opdatering
{.is-warning}

1. [Øg logningsniveauet til trace (Indstillinger => Generelt => Logningsniveau eller Rediger konfigurationsfilen)](#tracedebug-logfiler)
2. [Ryd logfiler (System => Logfiler => Ryd logfiler eller Slet alle logfiler i logmappen)](#rydning-af-logfiler)
3. Genskab problemet (Gentag det, der ødelægger tingene)
4. [Åbn trace-logfilen (sonarr.trace.txt) via brugergrænsefladen eller logfilen](#standardplacering-for-logfiler) på filsystemet og find den relevante kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del efter problemet.
6. Brug [Gist](https://gist.github.com/), [0bin (**Sørg for at deaktivere farvelægning**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntus Pastebin](https://pastebin.ubuntu.com/) eller lignende sider - undtagen dem, der skal undgås nedenfor - til at dele de kopierede logfiler fra ovenstående

**Advarsler:**
- **Brug ikke [pastebin.com](https://pastebin.com), da deres filtre har en tendens til at blokere logfilerne.
- Brug ikke [pastebin.pl](https://pastebin.pl), da deres websted ofte ikke er tilgængeligt.
- Brug ikke [JustPasteIt](https://justpaste.it/), da deres websted ikke faciliterer gennemgang af logfiler.
- Upload ikke din log som en fil.
- Upload ikke og del ikke dine logfiler via Google Drive, Dropbox eller andre websteder, der ikke er nævnt ovenfor.
- Arkiver ikke (zip, tar (tarball), 7zip osv.) dine logfiler.
- Del ikke konsoloutput, dockercontaineroutput eller noget andet end de angivne programlogfiler

**Vigtig bemærkning:**
- Når du bruger [0bin](https://0bin.net/), skal du sørge for at deaktivere farvelægning og ikke brænde efter læsning.

- Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken du skal bruge, kan du bruge N++. Du kan bruge Notepad++ "Find i filer"-funktionen til at søge i gamle logfiler efter behov.
- **Kun Unix:** Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken du skal bruge, kan du bruge grep. Hvis du f.eks. vil finde oplysninger om film/serie/bog/sang/indekseren "Shooter", kan du køre følgende kommando: `grep -inr -C 100 -e 'Shooter' /sti/til/logfiler/*.trace*.txt` Hvis din [Appdata-mappe](/sonarr/appdata-directory) er i din hjemmemappe, skal du køre: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flagene har følgende funktioner
    * -i: ignorér store/små bogstaver
    * -n: vis linjenummer
    *  -r: søg rekursivt i alle filer i stien
    * -C: angiv antallet af linjer før og efter linjen, den er fundet på
    * -e: mønsteret, der skal søges efter

```

## Standardplacering for logfiler

Logfilerne er placeret i Sonarrs [Appdata-mappe](/sonarr/appdata-directory), inde i mappen logs/. Du kan også få adgang til logfilerne fra brugergrænsefladen under System => Logfiler => Filer.

> Bemærk: Logtabelen ("Events") i brugergrænsefladen er ikke det samme som logfilerne og er ikke lige så nyttig. Hvis du bliver bedt om logfiler, skal du kopiere/indsætte fra logfilerne og ikke tabellen.
{.is-info}

## Placering af opdateringslogfiler

Opdateringslogfilerne er placeret i Sonarrs [Appdata-mappe](/sonarr/appdata-directory), inde i mappen UpdateLogs/.

## Deling af logfiler

Logfilerne kan være lange og svære at læse som en del af et forum- eller Reddit-indlæg, og de er spammy i Discord, så brug venligst [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller en hvilken som helst anden lignende pastebin-side. Hele filen er normalt ikke nødvendig, kun en god mængde kontekst før og efter problemet/fejlen. Glem ikke at vente på, at spamopgaver som f.eks. en RSS-synkronisering eller biblioteksopdatering bliver færdige.

## Trace/Debug-logfiler

Du kan ændre logningsniveauet under Indstillinger => Generelt => Logning. Sonarr behøver ikke genstartes for, at ændringen træder i kraft. Denne ændring påvirker kun logfilerne, ikke logningsdatabasen. De nyeste debug/trace-logfiler har navnene `sonarr.debug.txt` og `sonarr.trace.txt` henholdsvis.

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

Sonarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid `sonarr.txt`, og for de andre filer er `sonarr.0.txt` den næstnyeste (jo højere nummer, jo ældre er den). Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.

Når debug-logningsniveauet er aktiveret, vil der være yderligere `sonarr.debug.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. De dækker normalt en periode på 40 timer.

Når trace-logningsniveauet er aktiveret, vil der være yderligere `sonarr.trace.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af trace-verbosity dækker de kun et par timer.

# Gendannelse efter en mislykket opdatering

Vi gør alt, hvad vi kan, for at forhindre problemer under opgradering, men hvis de opstår, vil denne vejledning guide dig gennem de trin, du skal tage for at gendanne din installation.

## Afgør problemet

Det bedste sted at kigge, når programmet ikke starter efter en opdatering, er at gennemgå [opdateringslogfilerne](#placering-af-opdateringslogfiler) og se, om opdateringen blev gennemført uden problemer. Hvis der ikke er nogen problemer der, er næste skridt at kigge på dine almindelige programlogfiler. Før du prøver at starte igen, skal du bruge [Logging](/sonarr/settings#logging) og [Logfiler](/sonarr/system#log-files) til at finde dem og øge logningsniveauet.

### Migrationsproblem

- Migrationsfejl vil ikke være identiske, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Tilladelsesproblem

- Tilladelsesproblemer skyldes, at programmet ikke kan få adgang til de relevante midlertidige mapper og/eller programmets binærmappe. Ret tilladelserne, så den bruger/gruppe, som programmet kører som, har den passende adgang.

- Synology-brugere kan støde på denne Synology-fejl `Adgang til stien '/proc/{nogle nummer}/maps er nægtet`

- Synology-brugere kan også opleve at løbe tør for plads i `/tmp` på visse NAS-enheder. Du skal angive en anden `/tmp`-sti for appen. Se SynoCommunity eller andre Synology-supportkanaler for hjælp til dette.

## Løsning af problemet

Hvis der opstår et migrationsproblem, er der ikke meget, du kan gøre øjeblikkeligt. Hvis problemet er specifikt for dig (eller der endnu ikke er nogen indlæg), skal du oprette et indlæg på [vores subreddit](https://reddit.com/r/sonarr) eller besøge vores [discord](https://discord.sonarr.tv/). Hvis der er andre med samme problem, kan du være sikker på, at vi arbejder på det.

> Sørg for, at du ikke har forsøgt at bruge en database fra `develop`-versionen på den stabile version. Det frarådes at skifte mellem forskellige versioner af programmet.{.is-info}

### Problemer med tilladelser

- Ret tilladelserne, så den bruger/gruppe, som applikationen kører som, kan få adgang (læse og skrive) til både `/tmp` og installationsmappen for applikationen.

- For Synology-brugere, der oplever problemer med `/proc/###/maps`, bør det løse problemet at stoppe Sonarr eller de andre \*Arr-applikationer og opdatere. Dette er et problem med SynoCommunity-pakken.

### Manuel opgradering

Hent den nyeste version fra vores hjemmeside.

Installer opdateringen (.exe) eller udpak indholdet (.zip) over din eksisterende installation og kør Sonarr som du plejer.

# Downloads og import

Downloads og import er det punkt, hvor *de fleste* mennesker oplever problemer. Overordnet set skal Sonarr kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu *flere* forskellige opsætninger. Det betyder, at selvom der er nogle *almindelige* opsætninger, er der ikke én *rigtig* opsætning, og alle opsætninger kan være lidt forskellige.

> **Det første skridt er at øge logningsniveauet til Trace. Se [Logning og logfiler](#logning-og-logfiler) for detaljer om, hvordan du justerer logningsniveauet og søger i logfilerne. Du skal derefter genskabe problemet og bruge logfilerne med trace-niveau fra den tidsramme til at undersøge problemet.**
> Hvis nogen hjælper dig, skal du lægge kontekst fra før/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende side for at vise dem det.
> Det behøver ikke være hele filen, og det skal ikke *kun* være fejlen. Du skal også genskabe problemet, mens opgaver, der spammer logfilen, ikke kører.
{.is-danger}

Når du beder om hjælp, skal du sørge for at læse [sådan beder du om hjælp](#sådan-beder-du-om-hjælp), så du kan give os de oplysninger, vi har brug for.

## Test af downloadklienten

Sørg for, at dine downloadklient(er) kører. Start med at teste downloadklienten, hvis den ikke fungerer, kan du se detaljer i logfilerne med trace-niveau. Du skal finde en URL, du kan indsætte i din browser og se, om den virker. Det kan være et forbindelsesproblem, der kan indikere en forkert IP, værtsnavn, port eller endda en firewall, der blokerer adgangen. Det kan også være åbenlyst, som f.eks. et godkendelsesproblem, hvor du har indtastet brugernavn, adgangskode eller API-nøgle forkert.

## Test af en download

Nu vil vi prøve en download. Vælg en episode fra en serie og foretag en manuel søgning. Vælg en af disse filer og forsøg at downloade den. Bliver den sendt til downloadklienten? Ender den med den korrekte kategori? Viser den sig i Aktivitet? Viser den sig i logfilerne med trace-niveau under opgaverne **Tjek for færdig download** (opdater overvågede downloads og behandle overvågede downloads), som kører cirka hvert minut? Bliver den korrekt analyseret under den opgave? Har den download, der er i kø, et rimeligt navn? Da søgninger er baseret på id på nogle indexer/trackere, kan den sætte en download i kø med et navn, den ikke kan genkende.

## Test af en import

Importproblemer viser sig næsten altid som en post i Aktivitet med et orange ikon, hvor du kan holde musen hen over for at se fejlen. Hvis de ikke vises i Aktivitet, er dette det problem, du skal fokusere på først, så gå tilbage og find ud af det. De fleste importfejl skyldes *tilladelser*, husk at Sonarr skal kunne læse og skrive i downloadmappen. Nogle gange kan tilladelser i biblioteksmappen også være skyld i fejlen, så sørg for at kontrollere begge dele.

Forkerte sti-problemer er også mulige, men mindre almindelige i normale opsætninger. Nøglen til at forstå sti-problemer er at vide, at får stien til downloaden *fra* downloadklienten via dens API. Dette bliver et problem i mere unikke tilfælde, f.eks. når downloadklienten kører på et andet system (måske endda et andet operativsystem\!). Det kan også forekomme i en Docker-opsætning, når volumener ikke er konfigureret korrekt. En fjern sti-afbildning er en god løsning, når du ikke har kontrol, f.eks. i en seedbox-opsætning. I en Docker-opsætning er det bedre at rette stierne.

## Almindelige problemer

Her er nogle almindelige problemer.

### En eller flere forventede episoder i udgivelsen blev ikke importeret eller mangler

- Hvis alle episoder blev importeret, er den mest almindelige årsag, at der blev downloadet en sæsonpakke, der ikke indeholder alle episoder i sæsonen. Klik på `X` for at fjerne og ignorere udgivelsen.
- For alle andre problemer blev en eller flere episoder ikke importeret. Gennemgå oplysningerne i brugergrænsefladen og andre almindelige problemer.

### Brug af Sonarr v2

Sonarr v2 er blevet udfaset og ikke understøttet siden 3/2021. Den er ikke kompatibel med qBittorrent v4.3.0 eller nyere. Opgrader til Sonarr v3.

### Downloadklientens webgrænseflade er ikke aktiveret

Sonarr kommunikerer med din downloadklient via dens API og får adgang til den via klientens webgrænseflade. Du skal sikre dig, at klientens webgrænseflade er aktiveret, og at den port, den bruger, ikke konflikter med andre klientporte, der er i brug, eller porte, der er i brug på dit system.

### Forkert konfigureret SSL

Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din instans og din downloadklient på et lokalt netværk. Se [SSL FAQ-indlægget](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for mere information.

### Kan ikke se deling på Windows

Standardbrugeren for en Windows-tjeneste er `LocalService`, som typisk ikke har adgang til dine delinger. Rediger tjenesten og konfigurer den til at køre som din egen bruger. Se FAQ-indlægget [hvorfor kan jeg ikke se mine filer på en fjernserver](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server) for detaljer.

### Kortlagte netværksdrev er ikke pålidelige

Selvom kortlagte netværksdrev som `X:\` er praktiske, er de ikke så pålidelige som UNC-stier som `\\server\share`, og de er heller ikke tilgængelige før login. Konfigurer din downloadklient(e), så de bruger UNC-stier efter behov. Hvis dit bibliotek er på en deling, skal du sørge for, at dine rodmapper bruger UNC-stier. Hvis din downloadklient sender til en deling, er det der, du skal konfigurere UNC-stier, da får downloadstien fra downloadklienten. Det er fint at beholde dine kortlagte netværksdrev til personlig brug, bare brug dem ikke til automatisering.

### Docker og bruger, gruppe, ejerskab, tilladelser og stier

Docker tilføjer et ekstra lag af kompleksitet, som er nemt at gøre forkert, men stadig ende op med en opsætning, der fungerer, men har forskellige problemer. I stedet for at gennemgå dem her, skal du læse denne wiki-artikel [for disse automatiseringssoftware og Docker](/docker-guide), som handler om bruger, gruppe, ejerskab, tilladelser og stier. Den er ikke specifik for nogen Docker-system, i stedet går den over tingene på et overordnet niveau, så du kan implementere dem i din egen miljø.

### Fjern sti-afbildning

Hvis du har Sonarr i Docker og Downloadklienten uden for Docker (eller omvendt) eller har programmerne på forskellige servere, kan du have brug for en fjern sti-afbildning.

Logfilerne vil se sådan ud

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Derfor eksisterer `/volume3/data` ikke inden i Sonarrs container eller er ikke tilgængelig.

- [Indstillinger => Downloadklienter => Fjern sti-afbildninger](/sonarr/settings#remote-path-mappings)
- En fjern sti-afbildning bruges, når din downloadklient rapporterer en sti for fuldførte data enten på en anden server eller på en måde, som \*Arr ikke adresserer den mappe.
- Generelt er en fjern sti-afbildning kun nødvendig, hvis din downloadklient kører på Linux, når \*Arr kører på Windows eller omvendt. En fjern sti-afbildning kan også være nødvendig, hvis du blander Docker og Native-klienter, eller hvis du bruger en fjernserver.
- En fjern sti-afbildning er en DUMB søg/erstat (hvor den finder den FJERNE værdi og erstatter den med den LOKALE værdi for den angivne vært).
- Hvis fejlmeddelelsen om en dårlig sti ikke indeholder den ERSTATTEDE værdi, fungerer sti-afbildningen ikke, som du forventer. Den typiske løsning er at tilføje og fjerne afbildningen.
- [Se TRaSH's vejledning for yderligere oplysninger om fjern sti-afbildning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og din downloadklient er Docker-containere, er det sjældent nødvendigt med en fjern sti-afbildning. Det anbefales at [gennemgå Docker-guiden](/docker-guide) og/eller [følge TRaSH's vejledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Fjernmontering eller fjernsynkronisering (Syncthing)

- Du skal have synkroniseringen til at køre hele tiden, mens den downloader. Og du skal have den lokale synkroniseringsdestination til at kunne være hardlinks, når \*Arr importerer, hvilket betyder samme filsystem og se ud som det.
  - Synkroniser til en lavere, fælles mappe, der indeholder både ufuldstændige og fuldstændige filer.
  - Synkroniser til en placering, der er på samme filsystem lokalt som dit bibliotek og ser ud som det (Docker og netværksdelinger gør det nemt at konfigurere forkert).
  - Du vil gerne synkronisere de ufuldstændige og fuldstændige filer, så når torrentklienten flytter dem, afspejles det lokalt, og alle filerne er allerede "der" (selvom de stadig downloader). Derefter vil du bruge hardlinks, fordi selvom de importeres, før de er færdige, vil de stadig blive færdige.
  - På denne måde synkroniserer den hele tiden, mens den downloader, så torrentklienten flytter til undermappe for tv, og synkroniseringen afspejler det. På den måde er downloads stort set der, når de er erklæret færdige. Og selvom de ikke er helt færdige, betyder muligheden for hardlink stadig, at det er okay.
  - (Valgfrit - hvis det er relevant og/eller påkrævet (f.eks. fjern usenet-klient)) Konfigurer et brugerdefineret script, der skal køres ved import/download/opgradering for at fjerne den fjerneste fil.
- Alternativt er en fjernmontering i stedet for en fjernsynkroniseringssætning betydeligt mindre kompliceret at konfigurere, men typisk langsommere.
  - Monter din fjernlagring med sshfs eller en anden netværksfilsystemprotokol.
  - Sørg for, at brugeren og gruppen, som \*Arr er konfigureret til at køre som, har læse- eller skriveadgang.
  - Konfigurer en fjern sti-afbildning for at finde den FJERNE sti og erstatte den med den LOKALE ækvivalent.

### Tilladelser på biblioteksmappen

Logfilerne vil se sådan ud

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Glem ikke at kontrollere tilladelser og ejerskab for *destinationen*. Det er nemt at blive fokuseret på downloadens ejerskab og tilladelser, og det er *normalt* årsagen til tilladelsesrelaterede problemer, men det *kunne* også være destinationen. Kontrollér, at destinationsmappen(e) eksisterer. Kontrollér, at en destinations *fil* ikke allerede eksisterer eller ikke kan slettes eller flyttes til papirkurven. Kontrollér, at ejerskab og tilladelser tillader, at den downloadede fil kan kopieres, hardlinkes eller flyttes. Brugeren eller gruppen, der kører som, skal kunne læse og skrive i rodmappen.

- For Windows-brugere kan dette skyldes, at det kører som en tjeneste:
  - Windows-tjenesten kører under kontoen 'Local Service', som som standard ikke har tilladelser til at få adgang til din brugers hjemmemappe, medmindre der er tildelt tilladelser manuelt. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.
  - 'Local Service' har også generelt meget begrænsede tilladelser. Det anbefales derfor at installere appen som en systembakkeapplikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette tilbydes under installationen. Se FAQ'en for, hvordan du konverterer fra en tjeneste til en bakkeapp.

- For Synology-brugere henvises der til [SynoCommunity's artikel om tilladelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruger et NFS-mount, skal du sørge for, at `nolock` er aktiveret.
- Hvis du bruger et SMB-mount, skal du sørge for, at `nobrl` er aktiveret.

### Tilladelser på downloadmappen

Du vil se en fejl lignende følgende

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

eller

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

Glem ikke at kontrollere tilladelser og ejerskab for *kilden*. Det er nemt at blive fokuseret på destinationens ejerskab og tilladelser, og det er en *mulig* årsag til tilladelsesrelaterede problemer, men det er typisk kilden. Kontrollér, at kildekappen(e) eksisterer. Kontrollér, at ejerskab og tilladelser tillader, at den downloadede fil kan kopieres/hardlinkes eller kopieres+slettes/flyttes. Brugeren eller gruppen, der kører Sonarr, skal kunne læse og skrive i downloadfilerne.

- For Windows-brugere kan dette skyldes, at det kører som en tjeneste:
  - Windows-tjenesten kører under kontoen 'Local Service', som som standard ikke har tilladelser til at få adgang til din brugers hjemmemappe, medmindre der er tildelt tilladelser manuelt. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.
  - 'Local Service' har også generelt meget begrænsede tilladelser. Det anbefales derfor at installere appen som en systembakkeapplikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette tilbydes under installationen. Se FAQ'en for, hvordan du konverterer fra en tjeneste til en bakkeapp.

- For Synology-brugere henvises der til [SynoCommunity's artikel om tilladelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruger et NFS-mount, skal du sørge for, at `nolock` er aktiveret.
- Hvis du bruger et SMB-mount, skal du sørge for, at `nobrl` er aktiveret.

### Downloadmappe og biblioteksmappe er ikke forskellige mapper

- Downloadklienten skal downloade til en mappe, der er tilgængelig for \*Arr, og det må ikke være din rod-/biblioteksmappe. Du skal importere fra den separate downloadmappe til din biblioteksmappe.
- Du skal aldrig downloade direkte til din rodmappe. Du skal heller ikke bruge din rodmappe som downloadklientens færdige mappe eller ufuldstændige mappe.
- [**Dette vil også forårsage en helbredstjek i System**](/sonarr/system#downloading-into-root-folder)
- Inden for applikationen defineres en rodmappe som den konfigurerede mediebibliotekmappe. Dette er ikke rodmappen for et monteringspunkt. Din downloadklient har en ufuldstændig eller fuldstændig mappe (eller flytter fuldførte downloads) til din rod (biblioteks)mappe. Dette forårsager ofte problemer og frarådes. For at løse dette skal du ændre din downloadklient, så den ikke placerer downloads i din rodmappe. Bemærk, at 'placering' også inkluderer, hvis din downloadklients kategori er indstillet til din rodmappe, eller hvis NZBGet/SABnzbd har sortering aktiveret og sorterer til din rodmappe. Bemærk, at denne kontrol ser på alle definerede/konfigurerede rodmapper, der er tilføjet, ikke kun rodmapper, der i øjeblikket er i brug. Med andre ord skal mappen, din downloadklient downloader til eller flytter fuldførte downloads til, ikke være den samme mappe, du har konfigureret som din rod-/biblioteks-/endelige mediedestinationsmappe i \*Arr-applikationen.
- Konfigurerede rodmapper (også kendt som biblioteksmapper) kan findes under [Indstillinger => Mediehåndtering => Rodmapper](/sonarr/settings/#root-folders)
- Et eksempel er, hvis dine downloads går til `\data\downloads`, så har du en rodmappe, der er indstillet som `\data\downloads`.
- Det anbefales at bruge stier som `\data\media\` til din rodmappe/bibliotek og `\data\downloads\` til dine downloads.

> Din downloadmappe og din rod-/biblioteksmappe SKAL være adskilte
{.is-warning}

### Forkert kategori

Sonarr skal konfigureres til at bruge en kategori, så den kun forsøger at behandle sine egne downloads. Det er sjældent, at en torrent, der er tilføjet manuelt, ikke har den korrekte kategori, men det kan ske. Hvis du tilføjer torrents manuelt og vil behandle dem, skal de have den korrekte kategori. Den kan indstilles når som helst, da Sonarr forsøger at behandle downloads hvert minut.

### Pakkede torrents

Logs vil vise fejl som

```none
Ingen filer blev fundet, der er berettigede til import
```

Hvis din torrent er pakket i `.rar`-filer, skal du konfigurere udpakning. Vi anbefaler [Unpackerr](https://github.com/unpackerr/unpackerr), da det udpakker korrekt: forhindrer korrupte delvise importeringer og rydder op i de udpakkede filer efter import.

Fejlen kan også ses, hvis der ikke er nogen gyldig mediefil i mappen.

### Gentagne downloads

Der er flere årsager til gentagne downloads, men en af dem er relateret til begrænsningen i indekseren i udgivelsesprofilerne. Fordi indekseren *ikke* er gemt sammen med dataene, er alle `preferred word`-scores *nul* for medier i dit bibliotek, men under "RSS" og søgning vil de blive anvendt. Det samme gælder for eventuelle begrænsninger for `must contain` eller `must-not` contain, som kun gælder for den indekser; alt andet er fair game. Dette sætter dig i en løkke, hvor du downloader elementerne igen og igen, fordi det ser ud som en opgradering, så er det ikke, så dukker det op igen og ser ud som en opgradering, så er det ikke. Begræns ikke din udgivelsesprofil til en indekser.

Dette kan også skyldes, at downloaden aldrig faktisk importeres og derefter mangler i køen, så en ny download bliver konstant hentet og aldrig importeret. Se venligst de forskellige andre almindelige problemer og fejlfindingstrin for dette.

### Usenet-download går glip af import

Sonarr kigger kun på de 60 seneste downloads i SABnzbd og NZBGet, så hvis du *bevarer* din historik, betyder det, at under store køer med importproblemer kan downloads blive overset og ikke importeret. Den bedste måde at undgå dette på er at holde din historik ren, så eventuelle elementer, der stadig vises, skal undersøges. Du kan opnå dette ved at aktivere Fjern under Afsluttede og mislykkede downloadhåndteringer. I NZBGet flytter dette elementer til den *skjulte* historik, hvilket er fantastisk. Desværre har SABnzbd ikke en lignende funktion. Det bedste, du kan opnå der, er at bruge nzb-backupmappen.

### Downloadklient rydder elementer

Downloadklienten skal *ikke* være ansvarlig for at fjerne downloads. Usenet-klienter skal konfigureres, så de *ikke* fjerner downloads fra historikken. Torrent-klienter skal konfigureres, så de *ikke* fjerner torrents, når de er færdige med at seede (pause eller stop i stedet). Dette skyldes, at Sonarr kommunikerer med downloadklienten for at vide, hvad der skal importeres, så hvis de *fjernes*, er der intet at importere, selvom der er en mappe fuld af filer.

For SABnzbd håndteres dette med indstillingen Historisk opbevaring.

### Download kan ikke matches med et bibliotekselement

Af forskellige årsager kan udgivelser ikke parses, når de er hentet og sendt til downloadklienten. Aktivitet => Indstillinger => Vis ukendt (dette er nu aktiveret som standard i nyere versioner) vil vise alle elementer, der ikke allerede er ignoreret / importeret inden for \*Arr's downloadklientkategori. Disse skal typisk mappes og importeres manuelt.

Dette kan også ske, hvis du har en udgivelse i din downloadklient, men det medieelement (film/episode/bog/sang) findes ikke i applikationen.

#### Fandt matchende serie via hentningshistorik, men serien blev matchet efter seriens ID. Automatisk import er ikke mulig

- Denne importfejl ligner den ovenstående "kan ikke matches"-fejl.
- Sonarr hentede udgivelsen, fordi din indekser eller tracker rapporterede, at udgivelsen havde TVDb-ID'et (eller IMDb-ID'et) for en serie, du ønskede.
- Serien for den downloadede fil matcher ikke det rapporterede ID, så Sonarr vil ikke importere filen.
- Afhængigt af seriens titel og udgivelsesnavn - under forudsætning af at udgivelsen er korrekt for det ID, den er associeret med - vil Sonarr sandsynligvis have brug for, at der tilføjes en alias. [Denne FAQ-indgang har mere information](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) om at anmode om, at der tilføjes en alias.
- Alternativt er udgivelsen fejlmærket og ikke til seriens ID, der blev rapporteret. Dette skal rapporteres til din indekser, så de kan træffe rettelsesforanstaltninger.
- For at håndtere denne fejl:
  1. Verificer serien for filen
  1. Anmod om en alias (hvis relevant)
  1. Importer filen manuelt (menneskeikonet til højre) fra Aktivitet => Køen ELLER klik på `X` i køen for at ignorere udgivelsen i din klient og eventuelt blokere den / eventuelt fjerne den fra klienten

### Episodenavn er TBA

På TVDB får episoder, hvor navnene er ukendte, titlen TBA, og der er en cache på 24 timer på API'en. Typisk tager ændringer på TVDB-webstedet 24-48 timer om at nå Sonarr på grund af TVDB-cache, Skyhook-cache og seriens opdateringsinterval.

Indstillingen [Episode Title Required](/sonarr/settings#importing) i Sonarr styrer importadfærd, når titlen er TBA, men efter 24 timer fra episodens luftdato vil udgivelsen blive importeret, selvom titlen stadig er TBA. Der er heller ingen automatisk omdøbning af filer med TBA-titler.

### Forbindelsen blev lukket: Der opstod en uventet fejl under afsendelse

Dette skyldes, at indekseren bruger en SSL-protokol, der ikke understøttes af den aktuelle .NET-version, der findes i [Sonarr => System => Status](/sonarr/system#status).

### Anmodningen fik timeout

Sonarr modtager ingen respons fra klienten.

```none
    System.NET.WebException: Anmodningen fik timeout: ’https://example.org/api?t=caps&apikey=(fjernet) —> System.NET.WebException: Anmodningen fik timeout
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
- brug af Privoxy og forkert konfiguration af dette

## Problem ikke opført

Du kan også gennemgå nogle almindelige tilladelses- og netværksfejlfindingkommandoer [i vores guide](/permissions-and-networking). Ellers skal du diskutere det med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, skal du foreslå at tilføje det til wikien.

# Søgning i indekser og trackere

- [Hvorfor hentede Sonarr ikke en episode, jeg forventede?](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) FAQ-indgangen er sandsynligvis også nyttig.
- Hvis du bruger [Prowlarr](/prowlarr), kan du se [Historikken](/prowlarr/history) over alle forespørgsler, som Prowlarr har modtaget, og hvordan de blev sendt til webstederne. Sørg for, at `Parametre` er aktiveret i Prowlarr Historik => Indstillinger. (i)-ikonet giver yderligere detaljer.
- Fejlfindingstrinnene er ellers nedenfor

## Skru op for logning til sporingsniveau

> **Det første trin er at skrue op for logning til sporingsniveau, se [Logning og logfiler](#logging-and-log-files) for detaljer om justering af logning og søgning i logfiler. Du skal derefter reproducere problemet og bruge sporingsniveauets logfiler fra den tidsramme til at undersøge problemet.** Hvis nogen hjælper dig, skal du lægge kontekst fra før/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende side for at vise dem det. Det behøver ikke at være hele filen, og det skal ikke *kun* være fejlen. Du skal også reproducere problemet, mens opgaver, der spammer logfilen, ikke kører.
{.is-danger}

## Test af en indekser eller tracker

Når du tester en indekser eller tracker, kan du i debug- eller sporingslogfilerne finde den anvendte URL. Et eksempel på en vellykket test er nedenfor, hvor du kan se, at den forespørger indekseren via en specifik URL med specifikke parametre og derefter responsen. Du kan teste denne URL i din browser ved at erstatte `apikey=(fjernet)` med den korrekte api-nøgle som f.eks. `apikey=123`. Du kan eksperimentere med parametrene, hvis du får en fejl fra indekseren, eller se om du har forbindelsesproblemer, hvis det slet ikke virker. Efter at have testet i din egen browser skal du teste fra systemet, der kører, *hvis* du ikke allerede har gjort det.

## Test af en søgning

Ligesom testen af indekseren/trackeren ovenfor, når du udløser en søgning med logning på debug- eller sporingsniveau, kan du få URL'en fra logfilerne. Under testen er det bedst at bruge en så snæver søgning som muligt. En manuel (interaktiv) søgning efter en enkelt episode eller sæson er god, fordi den er specifik, og du kan se resultaterne i brugergrænsefladen, mens du undersøger logfilerne. Manuel (interaktiv) søgning udløses ved at gå til en serie og klikke på menneskeikonet for en episode eller sæson.

I denne test kigger du efter åbenlyse fejl og kører nogle enkle tests. Du kan se, at søgningen brugte URL'en `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(fjernet)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, som du kan prøve selv i en browser efter at have erstattet (fjernet) med din api-nøgle for den indekser. Virker det? Ser du de forventede resultater? Gælder denne FAQ-indgang? I den URL kan du se, at den har angivet specifikke kategorier med `cat=5030,5040,5045,5080`, så hvis du ikke ser de forventede resultater, er dette en sandsynlig årsag. Du kan også se, at den søgte efter tvdbid med `tvdbid=354629`, så hvis episoden ikke er korrekt kategoriseret på indekseren, skal det rettes. Du kan også se, at den søgte efter en specifik sæson og episode med sæson=1 og ep=1, så hvis det ikke er korrekt på indekseren, vil du ikke se de resultater. Se "Manuel søgning XML-output" nedenfor for at se et eksempel på output fra en fungerende forespørgsel.

- Manuel søgning XML-output

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

- Sporingsloguddrag

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|Søger 1 indekser for [The Fix : S01E01]
2021-03-20 13:15:23.6|Debug|Newznab|Downloader feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- Fuld sporingslog for en søgning

```none
2022-04-24 20:14:26.7|Info|NzbSearchService|Searching 1 indexers for [Fairy Tail : S02E91 (91)]
2022-04-24 20:14:26.7|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=1220&season=2&ep=91
2022-04-24 20:14:26.7|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=1220&season=2&ep=91
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'proxyenabled' defaultValue:'False'
2022-04-24 20:14:27.2|Trace|HttpClient|Res: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=1220&season=2&ep=91: 200.OK (491 ms)
2022-04-24 20:14:27.2|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|NzbSearchService|Total of 2 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:27.2|Debug|NzbSearchService|Setting last search time to: 4/24/2022 8:14:27 PM
2022-04-24 20:14:27.2|Info|DownloadDecisionMaker|Processing 2 releases
2022-04-24 20:14:27.2|Trace|DownloadDecisionMaker|Processing release 1/2
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.2|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.2|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.2|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.2|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:27.2|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.2|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.2|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.2|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.2|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.2|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.2|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:27.2|Trace|DownloadDecisionMaker|Processing release 2/2
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.2|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.2|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.2|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.2|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:27.2|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.2|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.2|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.2|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.2|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.2|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.2|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'autounmonitorpreviouslydownloadedepisodes' defaultValue:'False'
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'downloadpropersandrepacks' defaultValue:'PreferAndUpgrade'
2022-04-24 20:14:27.2|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (491 ms)
2022-04-24 20:14:27.2|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (491 ms)
```

## Almindelige problemer

Her er nogle almindelige problemer, der er løsningen på næsten alle problemer, der opleves.

### Indexere bliver ikke søgt

- Logs vil se sådan ud

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Søger indexere efter [Fairy Tail : S02E91 (91)]. 0 aktive indexere
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Der blev fundet i alt 0 rapporter for [Fairy Tail : S02E91 (91)] fra 0 indexere
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|Ingen resultater fundet
```

- Bemærk, at i det ovenstående tilfælde bliver der ikke søgt i nogen indexere. Dette tal kan variere afhængigt af din specifikke opsætning. Hvis antallet ikke er det samme som antallet af konfigurerede indexere, er følgende sandsynlige årsager:
  - [Sundhedstjek (System => Status)](/sonarr/system#health)
    - [Ingen indexere er tilgængelige med automatisk søgning aktiveret, Sonarr vil ikke give nogen automatiske søgeresultater](/sonarr/system#no-indexers-available-with-automatic-search-enabled-sonarr-will-not-provide-any-automatic-search-results)
    - [Ingen indexere er aktiveret](/sonarr/system#no-indexers-are-enabled)
    - [Aktiverede indexere understøtter ikke søgning](/sonarr/system#enabled-indexers-do-not-support-searching)
    - [Ingen indexere er tilgængelige med interaktiv søgning aktiveret](/sonarr/system#no-indexers-available-with-interactive-search-enabled)
    - [Indexere er utilgængelige på grund af fejl](/sonarr/system#indexers-are-unavailable-due-to-failures)
  - Søger en serietype af Anime, og der er ikke konfigureret nogen anime-kategorier for dine trackere. Indexere har [to forskellige konfigurerbare kategorityper](/sonarr/settings#indexers).
  - Søger en serietype af Daglig eller Standard, og der er ikke konfigureret nogen standard (ikke-anime) kategorier for dine trackere.
    - Kategorier - Standardkategorierne bruges, medmindre de redigeres. Det er sandsynligt, at disse standardkategorier ikke er optimale. Når denne indstilling redigeres, forespørger Sonarr indexeren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standarder ryddes, så snart en kategori aktiveres.
  - Animekategorier - De kategorier, som Sonarr vil bruge til anime-søgninger. Der bruges ingen kategorier, medmindre de redigeres. Når denne indstilling redigeres, forespørger Sonarr indexeren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standarder ryddes, så snart en kategori aktiveres.
  - Indexerens evner understøtter ikke forespørgselstypen (f.eks. Sæson/Episode osv.):
    - Inden for Prowlarr kan en indexers evner findes i (I)-ikonet for indexeren.
    - Jackett viser ikke en indexers evner inden for dets brugergrænseflade.
  - Trace-logs vil vise oplysninger om, hvorfor indexere bliver ignoreret, hvis der foretages en søgning efter ***genstart af Sonarr***.

### Dårligt navngivne udgivelser

- Serierpakker understøttes ikke
- Flere sæsonpakker understøttes ikke
- I mange tilfælde kan Sonarr simpelthen ikke matche det returnerede resultat med en kendt serie. I disse tilfælde vil dine logfiler se lignende ud som nedenfor. Disse skal sandsynligvis hentes og importeres manuelt. Den nøglefrase, du skal se i logfilerne, er `|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`

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

### Tracker har brug for RawSearch Caps

- Sonarr søger efter `9 1 1`, men din tracker har kun resultater for `9-1-1` eller `John s Show` og `John's Show`
- Dette skyldes, at din tracker ikke understøtter normale standardiserede søgninger.
- Løsningen er, at din trackers definition af søgeevner skal opdateres for at angive, at den [kræver og understøtter `RawSearch`](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackett understøtter flaget, men evnerne skal opdateres for hver indexer. Åbn en funktionanmodning til Jackett for at tilføje denne funktionalitet til din indexer.
- Prowlarr understøtter flaget, men evnerne skal opdateres for hver indexer. Åbn en funktionanmodning til Prowlarr for at tilføje denne funktionalitet til din indexer.

### Serien har brug for et alias

Udgivelser kan uploades som `The Series Name`, men TVDB har serien som `Series Name` eller lignende navneforskelle. Se venligst [dette FAQ-indlæg](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x)

### Serien har brug for en XEM-mapping

Udgivelser kan uploades som `Series Title S02E45` eller `Other Series Title S2022E42`, men TVDB har denne episode som `Series Title S03E01` eller `Other Series Title S03E42`. Se venligst [dette FAQ-indlæg](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

### Forkert serietype

Serietypen påvirker, hvordan Sonarr søger. Serietypen skal vælges baseret på, hvordan serien udgives på indexerne.
[Se dette FAQ-indlæg for flere detaljer](/sonarr/faq#whats-the-different-series-types)

> Hvis **Anime** serietypen bruges, er det [muligt også at få din indexer søgt med standardtypen](/sonarr/settings#indexers)
{.is-info}

#### Daglig

Logfilerne vil vise `Searching indexers for [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Logfilerne vil vise `Searching indexers for [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Logfilerne vil vise `Searching indexers for [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### Mediet er ikke overvåget

Logfilerne vil vise noget lignende

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

Serien/sæsonen/episoderne er ikke overvåget. Tjek overvågningsstatus for serien, sæsonen og episoderne.

> Sæsonpakker vil kun blive hentet, hvis alle episoder i sæsonen er overvåget, og sæsonpakken opgraderer alle eksisterende episoder, eller alle episoder mangler.
{.is-info}

### Søgning lykkedes - Ingen resultater returneret

Du modtager en besked lignende `Query successful, but no results were returned from your indexer. This may be an issue with the indexer or your indexer category settings.`

Dette skyldes, at din indexer ikke returnerer nogen resultater inden for de kategorier, du har konfigureret for indexer.

### Forkerte kategorier

Forkerte kategorier er sandsynligvis den mest almindelige årsag til, at resultater vises i manuelle søgninger på en indexer/tracker, men *ikke* i \*Arr. Indexer/trackeren *bør* vise kategorien i søgeresultaterne, hvilket bør hjælpe dig med at finde ud af, hvad der mangler. Hvis du bruger Jackett eller Prowlarr, har hver tracker en liste over specifikt understøttede kategorier. Sørg for at bruge de korrekte kategorier for kategorierne. Mange finder det nyttigt at have listen synlig i et browser vindue, mens de redigerer indtastningen i Sonarr.

> Bemærk, at hvis du har `Anime Categories` blank i dine indexerindstillinger, vil indexereren ikke blive brugt til søgninger af typen Anime Series.
> På samme måde, hvis du har `Categories` blank i dine indexerindstillinger, vil indexereren ikke blive brugt til søgninger af typen Standard eller Daglig serie.
{.is-info}

### Forkerte resultater

Nogle gange returnerer indexerne helt irrelevante resultater; Sonarr sender parametre for at begrænse søgningen til en serie. Nogle gange er de returnerede resultater helt irrelevante. Eller nogle gange, mest relateret med nogle få forkerte resultater. Den første er normalt et indexerproblem, og du kan se fra sporingslogfilerne, hvad der forårsager det. Du kan deaktivere den indexer og rapportere problemet. Den anden er normalt kategoriserede udgivelser, der kan rapporteres på indexer/trackeren.

Visse trackere - som f.eks. EZTV og andre offentlige - returnerer tilfældige resultater, hvis de ikke har et præcist match for den forespurgte serie/sæson/episode. Der er ingen løsning på dette.

### Manglende resultater

Hvis du har resultater på webstedet, som du kan finde, men som ikke vises i Sonarr, er dit problem sandsynligvis en af flere muligheder:

- [Kategorier er forkerte - Se ovenfor](#wrong-categories)
- Der udføres en ID-baseret søgning (IMDbId, TVDBId osv.), og indexereren har ikke korrekt kortlagt udgivelserne til den ID. Dette er noget, kun din indexer kan løse. De skal sikre, at udgivelsen er kortlagt til de korrekte ID'er.
- Du søger ikke på samme måde som Sonarr; Det er meget sandsynligt, at de vilkår, du søger på indexereren, ikke er, hvordan Sonarr forespørger det. Du kan se, hvordan Sonarr forespørger fra sporingslogfilerne. Tekstbaserede forespørgsler vil generelt være i formatet `q=words%20and%20things%20here` denne streng er HTTP-kodet og kan nemt afkodes ved hjælp af et hvilket som helst HTML-kodnings-/dekodningsværktøj online.
- Manglende RSS-feed af nye uploads. Logfilerne vil se ud som følger, og der vil blive bemærket en advarselshændelse.

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### Certifikatvalidering

Du vil oprette forbindelse til de fleste indexer/trackere via https, så du skal have det til at fungere korrekt på dit system. Det betyder, at din tidszone og tid begge skal være indstillet *korrekt*. Det betyder også, at dine systemcertifikater skal være opdaterede.

### Rammer grænser for anmodninger

Hvis du kører gennem en VPN eller proxy, kan du konkurrere med 10'er eller 100'er eller 1000'er af andre mennesker, der alle prøver at bruge tjenester som , theXEM og/eller dine indexer og trackere. Begrænsning af hastigheden og beskyttelse mod DDOS udføres ofte efter IP-adresse, og din VPN-/proxy-udgangspunkt er *én* IP-adresse. Medmindre du er i et undertrykkende land som Kina, Australien eller Sydafrika, har du ikke brug for en VPN-/proxy.

Rarbg har en tendens til at have en form for hastighedsbegrænsning inden for deres API og vises som svarer uden resultater.

### IP-blokering

På samme måde som hastighedsbegrænsninger kan visse indexer - som f.eks. Nyaa - direkte blokere en IP-adresse. Dette er typisk halvpermanent, og løsningen er at få en ny IP fra din internetudbyder eller VPN-udbyder.

### Brug af Jackett /all-endepunktet

Jackett `/all`-endepunktet er praktisk, men det er den eneste fordel. Alt andet er potentielle problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje at prøve Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

[Selv Jackett siger, at /all bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)

Brug af all-endepunktet har ingen fordele (udover reduceret administrationsoverhead), kun ulemper:

- du mister kontrollen over indexer-specifikke indstillinger (kategorier, søgemetoder osv.)
- blanding af søgemetoder (IMDB, forespørgsel osv.) kan medføre resultater af lav kvalitet
- indexer-specifikke kategorier (\>= 100000) kan ikke bruges.
- langsomme indexer vil bremse det samlede resultat
- det samlede antal resultater er begrænset til 1000
- irrelevante resultater
- manglende resultater

Ved at tilføje hver indexer separat kan du finjustere kategorierne på en per indexer-basis, hvilket kan være et problem med `/all`-endepunktet, hvis brug af den forkerte kategori forårsager fejl på nogle trackere. I Sonarr er hver indexer begrænset til 1000 resultater, hvis sideinddeling understøttes, eller 100, hvis det ikke er tilfældet, hvilket betyder, at jo flere trackere du tilføjer til Jackett, desto mere sandsynligt er det, at du klipper resultater. Endelig, hvis *én* af trackerne i `/all` returnerer en fejl, vil Sonarr deaktivere den, og nu får du ingen resultater.

### Brug af NZBHydra2 som en enkelt indgang

Brug af NZBHydra2 som en enkelt indexer-indgang (dvs. 1 NZBHydra2-indgang i Sonarr for mange indexere i NZBHydra2) i stedet for flere (dvs. mange NZBHydra2-indgange i Sonarr for mange indexere i NZBHydra2) har de samme problemer som nævnt ovenfor med Jacketts `/all`-endepunkt.

### Indexer bliver ikke søgt

- Hvis en indexer ikke ser ud til at blive søgt, skyldes det sandsynligvis, at indexereren ikke understøtter forespørgselstypen. Det mest almindelige tilfælde er, at Nyaa kun understøtter forespørgselsøgninger og ikke sæson-/episodesøgninger. Sporingslogfilerne indikerer efter en genstart på den første søgning, hvilke evner en indexer har eller ikke har.

### Jackett manuel søgning finder flere resultater

- [Se dette FAQ-indlæg](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### Release-profiler bliver ikke respekteret

Der er nogle årsager til, at det kan se ud til, at dine profiler bliver ignoreret. Den mest almindelige årsag er relateret til indexerens begrænsning i release-profiler. Fordi indexereren *ikke* er gemt sammen med dataene, er eventuelle `preferred word`-scores *nul* for medier i dit bibliotek, *men* under "RSS" og søgning vil de blive anvendt. På samme måde gælder det for eventuelle begrænsninger for `must contain` eller `must-not` contain, de gælder kun for den indexer; alt andet er fair game. Dette kan få release-profiler til at se ud til at blive ignoreret, eller det kan medføre opgraderingsløkker.

### Problem ikke angivet

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers diskuter problemet med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, skal du foreslå at tilføje det til wikien.

## Fejl

Dette er nogle af de almindelige fejl, du kan se, når du tilføjer en indexer

### The underlying connection was closed: An unexpected error occurred on a send

Dette skyldes, at indexereren bruger en SSL-protokol, der ikke understøttes af den aktuelle .NET-version, der findes i [Sonarr => System => Status](/sonarr/system#status).

### The request timed out

Sonarr modtager intet svar fra indexereren.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

Dette kan også skyldes:

- forkert konfigureret eller brug af en VPN
- forkert konfigureret eller brug af en proxy
- lokale DNS-problemer - Prøv at skifte til en anden DNS-udbyder
- lokale IPv6-problemer - typisk er IPv6 aktiveret, men ikke funktionsdygtig
- brug af Privoxy og forkert konfiguration af det

### Problem ikke angivet

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers diskuter problemet med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, skal du foreslå at tilføje det til wikien.