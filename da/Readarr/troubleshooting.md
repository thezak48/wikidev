---
title: Readarr Fejlfinding
description: 
published: true
date: 2023-07-24T19:54:33.343Z
tags: readarr, fejlfinding
editor: markdown
dateCreated: 2021-06-20T20:06:25.552Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Bede om hjælp](#bede-om-hjælp)
- [Logging og logfiler](#logging-og-logfiler)
  - [Standardplacering for logfiler](#standardplacering-for-logfiler)
  - [Opdateringslogfiler placering](#opdateringslogfiler-placering)
  - [Deling af logfiler](#deling-af-logfiler)
  - [Trace/Debug-logfiler](#tracedebug-logfiler)
  - [Rydning af logfiler](#rydning-af-logfiler)
- [Flere logfiler](#flere-logfiler)
- [Gendannelse efter en mislykket opdatering](#gendannelse-efter-en-mislykket-opdatering)
  - [Afgøre problemet](#afgøre-problemet)
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
    - [Du foretrækker et format, men det importerer i stedet et andet format](#du-foretrækker-et-format-men-det-importerer-i-stedet-et-andet-format)
    - [Downloadklientens webgrænseflade er ikke aktiveret](#downloadklientens-webgrænseflade-er-ikke-aktiveret)
    - [SSL i brug og forkonfigureret](#ssl-i-brug-og-forkonfigureret)
    - [Kan ikke se deling på Windows](#kan-ikke-se-deling-på-windows)
    - [Mappede netværksdrev er ikke pålidelige](#mappede-netværksdrev-er-ikke-pålidelige)
    - [Docker og bruger, gruppe, ejerskab, tilladelser og stier](#docker-og-bruger-gruppe-ejerskab-tilladelser-og-stier)
    - [Fjernstyring af sti](#fjernstyring-af-sti)
      - [Fjernmontering eller fjernsynkronisering (Syncthing)](#fjernmontering-eller-fjernsynkronisering-syncthing)
    - [Tilladelser for biblioteksmappen](#tilladelser-for-biblioteksmappen)
    - [Tilladelser for downloadmappen](#tilladelser-for-downloadmappen)
    - [Downloadmappe og biblioteksmappe er ikke forskellige mapper](#downloadmappe-og-biblioteksmappe-er-ikke-forskellige-mapper)
    - [Forkert kategori](#forkert-kategori)
    - [Pakkede torrents](#pakkede-torrents)
    - [Gentagne downloads](#gentagne-downloads)
    - [Usenet-download går glip af import](#usenet-download-går-glip-af-import)
    - [Downloadklient rydder elementer](#downloadklient-rydder-elementer)
    - [Download kan ikke matches til et bibliotekselement](#download-kan-ikke-matches-til-et-bibliotekselement)
    - [Forbindelse fik timeout](#forbindelse-fik-timeout)
  - [Problem ikke opført](#problem-ikke-opført)
- [Søgning, indekser og trackere](#søgning-indekser-og-trackere)
  - [Øg logningsniveauet til trace](#øg-logningsniveauet-til-trace)
  - [Test af en indekser eller tracker](#test-af-en-indekser-eller-tracker)
  - [Test af en søgning](#test-af-en-søgning)
  - [Almindelige problemer](#almindelige-problemer-1)
    - [Mediet er ikke overvåget](#mediet-er-ikke-overvåget)
    - [Forkerte kategorier](#forkerte-kategorier)
    - [Forkerte resultater](#forkerte-resultater)
    - [Søgningen var vellykket - ingen resultater returneret](#søgningen-var-vellykket-ingen-resultater-returneret)
    - [Manglende resultater](#manglende-resultater)
    - [Certifikatvalidering](#certifikatvalidering)
    - [Rammer hastighedsgrænser](#rammer-hastighedsgrænser)
    - [IP-blokering](#ip-blokering)
    - [Brug af Jackett /all-endepunktet](#brug-af-jackett-all-endepunktet)
    - [Brug af NZBHydra2 som enkeltindgang](#brug-af-nzbhydra2-som-enkeltindgang)
    - [Problem ikke opført](#problem-ikke-opført-1)
  - [Fejl](#fejl)
    - [Forbindelsen blev lukket: Der opstod en uventet fejl under afsendelse](#forbindelsen-blev-lukket-der-opstod-en-uventet-fejl-under-afsendelse)
    - [Anmodningen fik timeout](#anmodningen-fik-timeout)
    - [Problem ikke opført](#problem-ikke-opført-2)

# Bede om hjælp

Har du brug for hjælp? Det er okay, alle har brug for hjælp nogle gange. Du kan få hjælp i realtid via chat på

- [<i class="fab fa-discord"></i>&emsp;Discord *Officiel Readarr Discord*](https://readarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Officiel Readarr Subreddit*](https://reddit.com/r/readarr)
{.links-list}

Men inden du går derhen og poster, skal du sørge for, at din anmodning om hjælp er så god som muligt. Beskriv tydeligt problemet og beskriv kort din opsætning, herunder ting som dit OS/distribution, version af .NET, version af Readarr, downloadklient og dens version. **Hvis du bruger [Docker](https://www.docker.com/), skal du køre [Docker Guide](/docker-guide) først, da det vil løse almindelige og hyppige sti/tilladelsesproblemer. Ellers skal du have en [docker compose](/docker-guide#docker-compose) klar. [Sådan genereres en Docker Compose](https://trash-guides.info/compose)** Fortæl os om, hvad du allerede har prøvet, hvad du har kigget på. Brug [Logging og logfiler](#logging-og-logfiler) til at øge logningsniveauet til trace, genskabe problemet, upload den relevante kontekst til en pastebin og inkluder et link til den i dit indlæg. Du kan endda inkludere nogle skærmbilleder for at fremhæve problemet.

Jo mere vi ved, jo nemmere er det at hjælpe dig.

# Logging og logfiler

Det kan være nyttigt at gennemgå de almindelige fejlfindingsspørgsmål:
- [Downloads og import - Almindelige problemer](#almindelige-problemer)
- [Søgning, indekser og trackere - Almindelige problemer](#almindelige-problemer-1)
{.links-list}

Hvis du bliver bedt om debuglogfiler, vil dine logfiler indeholde `debug`, og hvis du bliver bedt om trace-logfiler, vil dine logfiler indeholde `trace`. Hvis de logfiler, du giver, ikke indeholder nogen af disse, er det ikke de ønskede logfiler.

- Undgå at dele hele logfilen, medmindre du bliver bedt om det.
- Upload ikke logfiler direkte til Discord eller indsæt dem som vægge af tekst, medmindre du bliver bedt om det.
- Del ikke logfiler som vedhæftning, zip-arkiv eller noget andet end tekst, der deles via de nedenfor nævnte tjenester

For at give gode og nyttige logfiler til deling:

> Sørg for, at der ikke kører en spamagtig opgave, f.eks. en RSS-opdatering
{.is-warning}

1. [Øg logningsniveauet til trace (Indstillinger => Generelt => Logningsniveau eller Rediger konfigurationsfilen)](#tracedebug-logfiler)
2. [Ryd logfiler (System => Logfiler => Ryd logfiler eller Slet alle logfiler i logmappen)](#rydning-af-logfiler)
3. Genskab problemet (Gentag det, der ødelægger tingene)
4. [Åbn trace-logfilen (readarr.trace.txt) via brugergrænsefladen eller logfilen](#standardplacering-for-logfiler) på filsystemet og find den relevante kontekst
5. Kopier en stor del før problemet, problemet selv og en stor del efter problemet.
6. Brug [Gist](https://gist.github.com/), [0bin (**Sørg for at deaktivere farvelægning**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntus Pastebin](https://pastebin.ubuntu.com/) eller lignende sider - undtagen dem, der er nævnt nedenfor - til at dele de kopierede logfiler fra ovenstående

**Advarsler:**
- **Brug ikke [pastebin.com](https://pastebin.com), da deres filtre har en tendens til at blokere logfilerne.
- Brug ikke [pastebin.pl](https://pastebin.pl), da deres websted ofte ikke er tilgængeligt.
- Brug ikke [JustPasteIt](https://justpaste.it/), da deres websted ikke gør det nemt at gennemgå logfiler.
- Upload ikke din log som en fil.
- Upload ikke og del ikke dine logfiler via Google Drive, Dropbox eller andre websteder, der ikke er nævnt ovenfor.
- Arkiver ikke (zip, tar (tarball), 7zip osv.) dine logfiler.
- Del ikke konsoloutput, dockercontaineroutput eller noget andet end de angivne programlogfiler

**Vigtig bemærkning:**
- Når du bruger [0bin](https://0bin.net/), skal du sørge for at deaktivere farvelægning og ikke brænde efter læsning.
- Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken du kan bruge N++. Du kan bruge Notepad++ "Find i filer"-funktionen til at søge i gamle logfiler efter behov.
- **Kun Unix:** Alternativt, hvis du leder efter en bestemt post i en gammel logfil, men ikke er sikker på, hvilken du kan bruge grep. Hvis du f.eks. vil finde oplysninger om film/serier/bøger/sange/indekseren "Shooter", kan du køre følgende kommando: `grep -inr -C 100 -e 'Shooter' /sti/til/logfiler/*.trace*.txt` Hvis din [Appdata-mappe](/readarr/appdata-directory) er i din hjemmemappe, skal du køre: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Flagene har følgende funktioner
    * -i: ignorer store/små bogstaver
    * -n: vis linjenummer
    *  -r: søg rekursivt i alle filer i stien
    * -C: vis # linjer før og efter linjen, den findes på
    * -e: mønsteret, der skal søges efter

```

## Standardplacering for logfiler

Logfilerne findes i Readarrs [Appdata-mappe](/readarr/appdata-directory), inde i mappen logs/. Du kan også få adgang til logfilerne fra brugergrænsefladen under System => Logfiler => Filer.

> Bemærk: Tabelen "Logs" i brugergrænsefladen er ikke det samme som logfilerne og er ikke lige så nyttig. Hvis du bliver bedt om logfiler, skal du kopiere/indsætte fra logfilerne og ikke tabellen.
{.is-info}

## Opdateringslogfiler placering

Opdateringslogfilerne findes i Readarrs [Appdata-mappe](/readarr/appdata-directory), inde i mappen UpdateLogs/.

## Deling af logfiler

Logfilerne kan være lange og svære at læse som en del af et forum- eller Reddit-indlæg, og de er spamagtige i Discord, så brug venligst [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) eller en hvilken som helst anden lignende pastebin-side. Hele filen er normalt ikke nødvendig, kun en god mængde kontekst før og efter problemet/fejlen. Glem ikke at vente på spamagtige opgaver som f.eks. en RSS-synkronisering eller biblioteksopdatering for at blive færdige.

## Trace/Debug-logfiler

Du kan ændre logningsniveauet under Indstillinger => Generelt => Logning. Readarr behøver ikke at blive genstartet for, at ændringen træder i kraft. Denne ændring påvirker kun logfilerne, ikke logningsdatabasen. De nyeste debug/trace-logfiler har navnene `readarr.debug.txt` og `readarr.trace.txt` henholdsvis.

Hvis du ikke kan få adgang til brugergrænsefladen for at indstille logningsniveauet, kan du gøre det ved at redigere config.xml i AppData-mappen ved at sætte værdien LogLevel til Debug eller Trace i stedet for Info.

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

Readarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid `readarr.txt`, og for de andre filer er `readarr.0.txt` den næstnyeste (jo højere nummer, jo ældre er den). Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.

Når debug-logningsniveauet er aktiveret, vil der være yderligere `readarr.debug.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. Den dækker normalt en periode på 40 timer.

Når trace-logningsniveauet er aktiveret, vil der være yderligere `readarr.trace.txt` rullende logfiler. Disse logfiler indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af trace-udskrivning dækker den kun et par timer.

# Gendannelse efter en mislykket opdatering

Vi gør alt, hvad vi kan, for at forhindre problemer ved opgradering, men hvis de opstår, vil dette guide dig gennem trinnene til at gendanne din installation.

## Afgøre problemet

- Det bedste sted at kigge, når programmet ikke starter efter en opdatering, er at gennemgå [opdateringslogfilerne](#opdateringslogfiler-placering) og se, om opdateringen blev fuldført korrekt. Hvis der ikke er nogen problemer der, er næste trin at kigge på dine almindelige programlogfiler. Før du prøver at starte igen, skal du bruge [Logging](/readarr/settings#logging) og [Logfiler](/readarr/system#log-files) til at finde dem og øge logningsniveauet.
- Det mest almindelige problem er, at systemet, som appen er installeret på, har rodet med `/tmp`-mappen og slettet kritiske \*Arr-filer under opdateringen, hvilket forårsager, at både opdateringen og tilbagerulningen mislykkes. I dette tilfælde skal du blot geninstallere oven på den eksisterende ødelagte installation.

### Migrationsproblem

- Migrationsfejl vil ikke være ens, men her er et eksempel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Tilladelsesproblem

- Tilladelsesproblemer skyldes, at programmet ikke kan få adgang til de relevante midlertidige mapper og/eller programmets binære mappe. Ret tilladelserne, så den bruger/gruppe, som programmet kører som, har den passende adgang.

- Synology-brugere kan støde på denne Synology-fejl `Access to the path '/proc/{noget nummer}/maps is denied`

- Synology-brugere kan også opleve, at der ikke er plads i `/tmp` på visse NAS-enheder. Du skal angive en anden sti til `/tmp` for appen. Se SynoCommunity eller andre Synology-supportkanaler for hjælp til dette.

## Løsning af problemet

I tilfælde af et migrationsproblem er der ikke meget, du kan gøre med det samme. Hvis problemet er specifikt for dig (eller der endnu ikke er nogen indlæg), skal du oprette et indlæg på [vores subreddit](https://reddit.com/r/readarr) eller kigge forbi vores [discord](https://readarr.com/discord), hvis der er andre med samme problem, kan du være sikker på, at vi arbejder på det.

> Sørg for, at du ikke har forsøgt at bruge en database fra `nightly`-versionen på den stabile version. Det frarådes at skifte mellem grene.{.is-info}

### Tilladelsesproblemer

- Ret tilladelserne, så den bruger/gruppe, som programmet kører som, kan få adgang (læse og skrive) til både `/tmp` og installationsmappen for programmet.

- For Synology-brugere, der oplever problemer med `/proc/###/maps`, bør det løse problemet at stoppe Sonarr eller de andre \*Arr-applikationer og opdatere. Dette er et problem med SynoCommunity-pakken.

### Manuel opgradering

Hent den nyeste version fra vores hjemmeside.

Installér opdateringen (.exe) eller udpak indholdet (.zip) over din eksisterende installation og kør Readarr som du plejer.

# Downloads og import

De fleste oplever problemer under download og import. Fra et overordnet perspektiv skal Readarr kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Det betyder, at selvom der er nogle almindelige opsætninger, er der ikke én rigtig opsætning, og alles opsætning kan være lidt anderledes.

> **Det første skridt er at øge logningsniveauet til Trace. Se [Logning og logfiler](#logning-og-logfiler) for detaljer om, hvordan du justerer logningen og søger i logfilerne. Du skal derefter genskabe problemet og bruge logfilerne med trace-niveau fra den tidsramme til at undersøge problemet.** Hvis nogen hjælper dig, skal du lægge kontekst fra før/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende side for at vise dem det. Det behøver ikke at være hele filen, og det bør ikke *kun* være fejlen. Du skal også genskabe problemet, mens opgaver, der spammer logfilen, ikke kører.
{.is-danger}

Når du beder om hjælp, skal du sørge for at læse [at bede om hjælp](#at-bede-om-hjælp), så du kan give os de oplysninger, vi har brug for.

## Test af downloadklienten

Sørg for, at din downloadklient(er) kører. Start med at teste downloadklienten, hvis den ikke virker, kan du se detaljer i logfilerne med trace-niveau. Du skal finde en URL, du kan indsætte i din browser og se, om den virker. Det kan være et forbindelsesproblem, der kan indikere en forkert IP, værtsnavn, port eller endda en firewall, der blokerer adgangen. Det kan være åbenlyst, som f.eks. et godkendelsesproblem, hvor du har indtastet brugernavn, adgangskode eller API-nøgle forkert.

## Test af en download

Nu vil vi prøve en download. Vælg en bog og foretag en manuel søgning. Vælg en af disse filer og forsøg at downloade den. Bliver den sendt til downloadklienten? Endes den med den korrekte kategori? Viser den sig i Aktivitet? Endes den i logfilerne med trace-niveau under opgaven **Tjek for færdig download**, som kører cirka hvert minut? Bliver den korrekt analyseret under den opgave? Har den download, der er sat i kø, et rimeligt navn? Da søgninger er efter id på nogle indexer/trackere, kan den sætte en i kø med et navn, den ikke kan genkende.

## Test af en import

Importproblemer bør næsten altid vise sig som en post i Aktivitet med et orange ikon, som du kan svæve over for at se fejlen. Hvis de ikke vises i Aktivitet, er dette problemet, du skal fokusere på først, så gå tilbage og find ud af det. De fleste importfejl skyldes *tilladelser*, husk at skal kunne læse og skrive i downloadmappen. Nogle gange kan tilladelser i biblioteksmappen også være skyld i fejlen, så sørg for at kontrollere begge dele.

Forkerte sti-problemer er også mulige, men mindre almindelige i normale opsætninger. Nøglen til at forstå sti-problemer er at vide, at får stien til downloaden *fra* downloadklienten via dens API. Dette bliver et problem i mere unikke tilfælde, f.eks. når downloadklienten kører på et andet system (måske endda et andet operativsystem\!). Det kan også forekomme i en Docker-opsætning, når volumener ikke er konfigureret korrekt. En fjern sti-mapping er en god løsning, når du ikke har kontrol, f.eks. en seedbox-opsætning. I en Docker-opsætning er det bedre at rette stierne.

## Almindelige problemer

Her er nogle almindelige problemer.

### Du foretrækker et format, men det importerer et andet format i stedet

Når Readarr importerer, importerer det i rækkefølge efter dine prioriteter i din kvalitetsprofil, uanset om de er markeret eller ej. For at løse dette problem skal du trække dine markerede formater til toppen af kvalitetslisten. For eksempel, i nedenstående indstillinger, selvom kun EPUB ønskes, hvis downloaden indeholder en AZW3 sammen med EPUB'en, vil den blive importeret med højere prioritet end EPUB'en, hvilket resulterer i, at uønskede formater bliver importeret.

![qualities.png](/assets/readarr/qualities.png)

### Downloadklientens WebUI er ikke aktiveret

Readarr kommunikerer med din downloadklient via dens API og får adgang til den via klientens webui. Du skal sikre dig, at klientens webui er aktiveret, og at den port, den bruger, ikke konflikter med andre klientporte, der er i brug, eller porte, der er i brug på dit system.

### SSL i brug og forkonfigureret

Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din instans og din downloadklient på et lokalt netværk. Se [SSL FAQ-indgangen](/readarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues) for mere information.

### Kan ikke se deling på Windows

Standardbrugeren for en Windows-tjeneste er `LocalService`, som typisk ikke har adgang til dine delinger. Rediger tjenesten og konfigurer den til at køre som din egen bruger, se FAQ-indgangen [hvorfor kan jeg ikke se mine filer på en fjernserver](/readarr/faq#why-cant-i-see-my-files-on-a-remote-server) for detaljer.

### Mappede netværksdrev er ikke pålidelige

Selvom mappede netværksdrev som `X:\` er praktiske, er de ikke så pålidelige som UNC-stier som `\\server\share`, og de er heller ikke tilgængelige før login. Konfigurer din downloadklient (er), så de bruger UNC-stier efter behov. Hvis dit bibliotek er på en delt mappe, skal du sørge for, at dine rodmapper bruger UNC-stier. Hvis din downloadklient sender til en delt mappe, er det der, du skal konfigurere UNC-stier, da får downloadstien fra downloadklienten. Det er fint at beholde dine mappede netværksdrev til personlig brug, bare brug dem ikke til automatisering.

### Docker og bruger, gruppe, ejerskab, tilladelser og stier

Docker tilføjer et ekstra lag af kompleksitet, der er nemt at få forkert, men stadig ende op med en opsætning, der fungerer, men har forskellige problemer. I stedet for at gennemgå dem her, skal du læse denne wiki-artikel [for disse automatiseringssoftware og Docker](/docker-guide), som handler om bruger, gruppe, ejerskab, tilladelser og stier. Den er ikke specifik for nogen Docker-system, i stedet går den over tingene på et overordnet niveau, så du kan implementere dem i din egen miljø.

### Fjern sti-mapping

Hvis du har Readarr i Docker og Downloadklienten i ikke-Docker (eller omvendt) eller har programmerne på forskellige servere, kan du have brug for en fjern sti-mapping.

Logfilerne vil se sådan ud

```none
2022-02-03 14:03:54.3|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /volume3/data/torrents/audiobooks/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Så `/volume3/data` eksisterer ikke inden for Readarr's container eller er ikke tilgængelig.

- [Indstillinger => Downloadklienter => Fjern sti-mapping](/readarr/settings#remote-path-mappings)
- En fjern sti-mapping bruges, når din downloadklient rapporterer en sti for fuldførte data enten på en anden server eller på en måde, som \*Arr ikke adresserer den mappe.
- Generelt er en fjern sti-mapping kun nødvendig, hvis din downloadklient kører på Linux, når \*Arr kører på Windows eller omvendt. En fjern sti-mapping kan også være nødvendig, hvis du blander Docker- og Native-klienter eller hvis du bruger en fjernserver.
- En fjern sti-mapping er en DUMB søg/erstat (hvor den finder den FJERNE værdi og erstatter den med den LOKALE værdi for den angivne vært).
- Hvis fejlmeddelelsen om en dårlig sti ikke indeholder den ERSTATTEDE værdi, fungerer sti-mappingen ikke, som du forventer. Den typiske løsning er at tilføje og fjerne mappingen.
- [Se TRaSH's vejledning for yderligere oplysninger om fjern sti-mapping](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og din Downloadklient er Docker-containere, er det sjældent nødvendigt med en fjern sti-mapping. Det anbefales at [gennemgå Docker-guiden](/docker-guide) og/eller [følge TRaSH's vejledning](https://trash-guides.info/hardlinks)
{.is-info}

#### Fjernmontering eller fjernsynkronisering (Syncthing)

- Du skal have synkroniseringen kørende hele tiden, den downloader. Og du skal have den lokale synkroniseringsdestination i stand til at være hardlinks, når \*Arr importerer, hvilket betyder, at det er det samme filsystem og ser sådan ud.
  - Synkroniser til en lavere, fælles mappe, der indeholder både ufuldstændige og fuldstændige filer.
  - Synkroniser til en placering, der er på samme filsystem lokalt som dit bibliotek og ser sådan ud (Docker og netværksdelinger gør det nemt at konfigurere forkert).
  - Du vil gerne synkronisere de ufuldstændige og fuldstændige filer, så når torrentklienten flytter dem, afspejles det lokalt, og alle filerne er allerede "der" (selvom de stadig downloader). Derefter vil du bruge hardlinks, fordi selvom de importerer, før de er færdige, vil de stadig blive færdige.
  - På denne måde downloader den hele tiden, den downloader, synkroniserer, så torrentklienten flytter til undermappe til tv, og synkroniseringen afspejler det. På den måde er downloads stort set færdige, når de er erklæret færdige. Og selvom de ikke er helt færdige, betyder muligheden for hardlink stadig, at det er okay.
  - (Valgfrit - hvis det er relevant og/eller påkrævet (f.eks. fjern usenetklient)) Konfigurer et brugerdefineret script, der skal køres ved import/download/opgradering for at fjerne den fjerneste fil
- Alternativt er en fjernmontering i stedet for en fjernsynkroniseringsopsætning betydeligt mindre kompliceret at konfigurere, men typisk langsommere.
  - Monter din fjernlagring med sshfs eller en anden protokol til netværksfiler.
  - Sørg for, at brugeren og gruppen, som \*Arr er konfigureret til at køre som, har læse- eller skriveadgang.
  - Konfigurer en fjern sti-mapping til at finde den FJERNE sti og erstatte den med den LOKALE ækvivalent.

### Tilladelser på biblioteksmappen

Logfilerne vil se sådan ud

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/media/books/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Glem ikke at kontrollere tilladelser og ejerskab for *destinationen*. Det er nemt at blive fokuseret på downloadens ejerskab og tilladelser, og det er *normalt* årsagen til tilladelsesrelaterede problemer, men det *kan* også være destinationen. Kontrollér, at destinationsmappen(e) eksisterer. Kontrollér, at en destinations *fil* ikke allerede eksisterer eller ikke kan slettes eller flyttes til papirkurven. Kontrollér, at ejerskab og tilladelser tillader, at den downloadede fil kan kopieres, hardlinkes eller flyttes. Brugeren eller gruppen, der kører som, skal kunne læse og skrive i rodmappen.

- For Windows-brugere kan dette skyldes, at det kører som en tjeneste:
  - Windows-tjenesten kører under kontoen 'Local Service', som som standard ikke har tilladelser til at få adgang til din brugers hjemmemappe, medmindre tilladelserne er tildelt manuelt. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.
  - 'Local Service' har også generelt meget begrænsede tilladelser. Det anbefales derfor at installere appen som en systembakkeapplikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette gives under installationen. Se FAQ'en for, hvordan du konverterer fra en tjeneste til en bakkeapp.

- For Synology-brugere henvises til [SynoCommunity's artikel om tilladelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruger et NFS-mount, skal du sørge for, at `nolock` er aktiveret.
- Hvis du bruger et SMB-mount, skal du sørge for, at `nobrl` er aktiveret.

### Tilladelser på downloadmappen

Logfilerne vil se sådan ud

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/torrents/books/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Glem ikke at kontrollere tilladelser og ejerskab for *kilden*. Det er nemt at blive fokuseret på destinationens ejerskab og tilladelser, og det er en *mulig* årsag til tilladelsesrelaterede problemer, men det er normalt kilden. Kontrollér, at kildekappen(e) eksisterer. Kontrollér, at ejerskab og tilladelser tillader, at den downloadede fil kan kopieres/hardlinkes eller kopieres+slettes/flyttes. Brugeren eller gruppen, der kører som, skal kunne læse og skrive i downloadmappen.

- For Windows-brugere kan dette skyldes, at det kører som en tjeneste:
  - Windows-tjenesten kører under kontoen 'Local Service', som som standard ikke har tilladelser til at få adgang til din brugers hjemmemappe, medmindre tilladelserne er tildelt manuelt. Dette er særligt relevant, når du bruger downloadklienter, der er konfigureret til at downloade til din hjemmemappe.
  - 'Local Service' har også generelt meget begrænsede tilladelser. Det anbefales derfor at installere appen som en systembakkeapplikation, hvis brugeren kan forblive logget ind. Muligheden for at gøre dette gives under installationen. Se FAQ'en for, hvordan du konverterer fra en tjeneste til en bakkeapp.

- For Synology-brugere henvises til [SynoCommunity's artikel om tilladelser for deres pakker](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Ikke-Windows: Hvis du bruger et NFS-mount, skal du sørge for, at `nolock` er aktiveret.
- Hvis du bruger et SMB-mount, skal du sørge for, at `nobrl` er aktiveret.

### Downloadmappe og biblioteksmappe er ikke forskellige mapper

Downloadklienten skal downloade til en mappe, der er tilgængelig for \*Arr, og som ikke er din rod-/biblioteksmappe; den skal importere fra den separate downloadmappe til din biblioteksmappe. Du skal aldrig downloade direkte til din rodmappe. Du skal heller ikke bruge din rodmappe som downloadklientens fuldførte mappe eller ufuldstændige mappe.

> Din downloadmappe og din rod-/biblioteksmappe SKAL være separate
{.is-warning}

### Forkert kategori

Readarr skal konfigureres til at bruge en kategori, så den kun forsøger at behandle sine egne downloads. Det er sjældent, at en torrent, der er indsendt af , bliver tilføjet uden den korrekte kategori, men det kan ske. Hvis du tilføjer torrents manuelt og vil behandle dem, skal de have den korrekte kategori. Den kan indstilles når som helst, da forsøger at behandle downloads hvert minut.

### Pakkede torrents

Logfilerne vil vise fejl som

```none
No files found are eligible for import
```

Hvis din torrent er pakket i `.rar`-filer, skal du konfigurere udpakning. Vi anbefaler [Unpackerr](https://github.com/unpackerr/unpackerr), da det gør udpakning rigtigt: forhindrer korrupte delvise importeringer og rydder op i de udpakkede filer efter import.

Fejlen kan også ses, hvis der ikke er nogen gyldig mediefil i mappen.

### Gentagne downloads

Der er flere årsager til gentagne downloads, men en af dem er relateret til begrænsningen i indexeringsprofilen. Fordi indexeringsprofilen *ikke* gemmes sammen med dataene, er eventuelle foretrukne ordpoint *nul* for medier i dit bibliotek, men under "RSS" og søgning vil de blive anvendt. Dette får dig ind i en løkke, hvor du downloader elementerne igen og igen, fordi det ser ud som en opgradering, så er det ikke, så vises det igen og ser ud som en opgradering, så er det ikke. Begræns ikke din releaseprofil til en indexer.

Dette kan også skyldes, at downloaden aldrig faktisk importerer og derefter mangler i køen, så en ny download bliver grebet og aldrig importeret. Se venligst de forskellige andre almindelige problemer og fejlfindingstrin for dette.

### Usenet-download går glip af importering

Readarr kigger kun på de 60 seneste downloads i SABnzbd og NZBGet, så hvis du beholder din historik, betyder det, at downloads kan blive overset og ikke importeres under store køer med importproblemer. Den bedste måde at undgå dette på er at holde din historik ren, så eventuelle elementer, der stadig vises, skal undersøges. Du kan opnå dette ved at aktivere "Fjern" under "Afsluttede og mislykkede downloadhåndteringer". I NZBGet vil dette flytte elementer til den skjulte historik, hvilket er fantastisk. Desværre har SABnzbd ikke en lignende funktion. Det bedste, du kan opnå der, er at bruge nzb-backupmappen.

### Rydning af elementer i downloadklienten

Downloadklienten bør *ikke* være ansvarlig for at fjerne downloads. Usenet-klienter skal konfigureres, så de *ikke* fjerner downloads fra historikken. Torrent-klienter skal konfigureres, så de *ikke* fjerner torrents, når de er færdige med at seede (pause eller stop i stedet). Dette skyldes, at Readarr kommunikerer med downloadklienten for at vide, hvad der skal importeres, så hvis de *fjernes*, er der intet at importere... selvom der er en mappe fuld af filer.

For SABnzbd håndteres dette med indstillingen Historisk bevarelse.

### Download kan ikke matches med et bibliotekselement

Af forskellige årsager kan udgivelser ikke parses, når de er hentet og sendt til downloadklienten. Aktivitet => Indstillinger => Vis ukendt (dette er nu aktiveret som standard i nyere versioner) vil vise alle elementer, der ikke allerede er ignoreret / importeret inden for \*Arr's downloadklientkategori. Disse skal typisk manuelt mappes og importeres.

Dette kan også ske, hvis du har en udgivelse i din downloadklient, men det medieelement (film/episode/bog/sang) findes ikke i applikationen.

### Forbindelsen blev afbrudt: Der opstod en uventet fejl under afsendelse

Dette skyldes, at indekseren bruger en SSL-protokol, som den nuværende .NET-version i [Readarr => System => Status](/readarr/system#status) ikke understøtter.

### Anmodningen udløb

Readarr modtager ingen respons fra klienten.

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
- lokale DNS-problemer
- lokale IPv6-problemer - typisk er IPv6 aktiveret, men ikke funktionsdygtig
- brug af Privoxy og forkert konfiguration af denne

## Problem ikke angivet

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers skal du diskutere det med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, skal du foreslå at tilføje det til wikien.

# Søgning i indekser og trackere

- Hvis du bruger [Prowlarr](/prowlarr), kan du se [Historikken](/prowlarr/history) over alle forespørgsler, som Prowlarr har modtaget, og hvordan de blev sendt til siderne. Sørg for, at "Parametre" er aktiveret i Prowlarr Historik => Indstillinger. (i) ikonet giver yderligere detaljer.

## Skru logningen op til sporingsniveau

> **Det første skridt er at skrue logningen op til sporingsniveau, se [Logning og logfiler](#logging-and-log-files) for detaljer om justering af logningen og søgning i logfilerne. Du skal derefter reproducere problemet og bruge sporingsniveau-logfilerne fra den tidsramme til at undersøge problemet.** Hvis nogen hjælper dig, skal du indsætte kontekst fra før/efter i en [pastebin](https://0bin.net), [Gist](https://gist.com) eller lignende side for at vise dem det. Det behøver ikke at være hele filen, og det bør ikke *kun* være fejlen. Du skal også reproducere problemet, mens opgaver, der spammer logfilen, ikke kører.
{.is-danger}

## Test af en indekser eller tracker

Når du tester en indekser eller tracker, kan du i debug- eller sporingslogfilerne finde den anvendte URL. Et eksempel på en vellykket test er vist nedenfor, hvor du kan se, at den forespørger indekseren via en specifik URL med specifikke parametre og derefter får svar. Du kan teste denne URL i din browser ved at erstatte `apikey=(fjernet)` med den korrekte api-nøgle som f.eks. `apikey=123`. Du kan eksperimentere med parametrene, hvis du får en fejl fra indekseren, eller se om du har forbindelsesproblemer, hvis det slet ikke virker. Når du har testet det i din egen browser, skal du teste det fra systemet, der kører *hvis* du ikke allerede har gjort det.

## Test af en søgning

På samme måde som testen af indekseren/trackeren ovenfor, når du udløser en søgning med logningsniveauet Debug eller Trace, kan du få URL'en fra logfilerne. Under testen er det bedst at bruge en så snæver søgning som muligt. En manuel søgning er god, fordi den er specifik, og du kan se resultaterne i brugergrænsefladen, mens du undersøger logfilerne.

I denne test vil du lede efter åbenlyse fejl og køre nogle enkle tests. Du kan se, at søgningen brugte URL'en ***OPDATERET URL SPECIFIK FOR BØGER ER NØDVENDIG - DETTE ER ET SONARR URL-EKSEMPEL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(fjernet)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`, som du kan prøve selv i en browser efter at have erstattet (fjernet) med din api-nøgle for den indekser. Virker det? Ser du de forventede resultater? Gælder denne FAQ-indgang? I den URL kan du se, at den indstiller specifikke kategorier med `cat=5030,5040,5045,5080`, så hvis du ikke ser forventede resultater, er det en sandsynlig årsag. Du kan også se, at den søgte efter tvdbid med `tvdbid=354629`, så hvis episoden ikke er korrekt kategoriseret på indekseren, skal det rettes. Du kan også se, at den søgte efter en bestemt sæson og episode med season=1 og ep=1, så hvis det ikke er korrekt på indekseren, vil du ikke se de resultater. Se "Manuel søgning XML-output" nedenfor for at se et eksempel på output fra en fungerende forespørgsel.

- Manuel søgning XML-output

```xml
EKSEMPEL PÅ INDEKSERINGSSØGNINGSRESPONS NØDVENDIG
```

***Billeder nødvendige***

![searches-indexers-and-trackers1.png](/assets/readarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/readarr/searches-indexers-and-trackers2.png)

- Sporingslogsnip

```none
Snippet af sporingslog for en manuel søgning er nødvendig
```

- Fuld sporingslog for en søgning

```none
Fuld sektion af sporingslog for en manuel søgning er nødvendig
```

## Almindelige problemer

Her er nogle almindelige problemer.

### Mediet er ikke overvåget

Bogen(e) er ikke overvåget.

### Forkerte kategorier

Forkerte kategorier er sandsynligvis den mest almindelige årsag til, at resultater vises i manuelle søgninger på en indekser/tracker, men *ikke* i . Indekseren/trackeren *bør* vise kategorien i søgeresultaterne, hvilket bør hjælpe dig med at finde ud af, hvad der mangler. Hvis du bruger Jackett eller Prowlarr, har hver tracker en liste over specifikt understøttede kategorier. Sørg for, at du bruger de korrekte kategorier. Mange finder det nyttigt at have listen synlig i et browser-vindue, mens de redigerer indgangen i .

### Forkerte resultater

Nogle gange returnerer indekserne helt irrelevante resultater, Readarr sender parametre for at begrænse søgningen, men de returnerede resultater er helt irrelevante. Eller nogle gange, mest relateret med nogle få forkerte resultater. Den første er normalt et indekserproblem, og du kan se fra sporingslogfilerne, hvilken indekser der forårsager det. Du kan deaktivere den indekser og rapportere problemet. Den anden er normalt kategoriserede udgivelser, som kan rapporteres på indekseren/trackeren.

### Forespørgsel vellykket - Ingen resultater returneret

Du modtager en besked lignende `Forespørgsel vellykket, men der blev ikke returneret nogen resultater fra din indekser. Dette kan være et problem med indekseren eller dine indstillinger for indekserkategorier.`

Dette skyldes, at din indekser ikke returnerer nogen resultater, der er inden for de kategorier, du har konfigureret for indekseren.

### Manglende resultater

Hvis du har resultater på webstedet, som du kan finde, men som ikke vises i Readarr, er dit problem sandsynligvis en af flere muligheder:

- [Kategorier er forkerte - Se ovenfor](#wrong-categories)
- Der udføres en søgning baseret på en ID, og indekseren har ikke korrekt kortlagt udgivelserne til den ID. Dette er noget, kun din indekser kan løse. De skal sikre, at udgivelsen er kortlagt til de korrekte gældende id'er.
- Du søger ikke på samme måde som Readarr; Det er meget sandsynligt, at de vilkår, du søger på indekseren, ikke er, hvordan Readarr forespørger det. Du kan se, hvordan Readarr forespørger det fra sporingslogfilerne. Tekstbaserede forespørgsler vil generelt være i formatet `q=ord%20og%20ting%20her` denne streng er HTTP-kodet og kan nemt afkodes ved hjælp af et hvilket som helst online HTML-kodnings-/afkodningsværktøj.

### Certifikatvalidering

Du vil oprette forbindelse til de fleste indeksere/trackere via https, så du skal have det til at fungere korrekt på dit system. Det betyder, at din tidszone og tid begge skal være indstillet *korrekt*. Det betyder også, at dine systemcertifikater skal være opdaterede.

### Ramme begrænsninger

Hvis du kører din gennem en VPN eller proxy, kan du konkurrere med 10'er eller 100'er eller 1000'er af andre mennesker, der alle prøver at bruge tjenester som , theXEM og/eller dine indeksere og trackere. Begrænsning af hastigheden og beskyttelse mod DDOS udføres ofte efter IP-adresse, og din VPN/proxy-udgangspunkt er *én* IP-adresse. Medmindre du er i et undertrykkende land som Kina, Australien eller Sydafrika, behøver du ikke en VPN/proxy .

Rarbg har en tendens til at have en form for hastighedsbegrænsning inden for deres API og vises som svarer uden resultater.

### IP-blokering

På samme måde som hastighedsbegrænsninger kan visse indeksere - som f.eks. Nyaa - direkte blokere en IP-adresse. Dette er typisk halvpermanent, og løsningen er at få en ny IP fra din internetudbyder eller VPN-udbyder.

### Brug af Jackett /all-endepunktet

Jackett `/all`-endepunktet er praktisk, men det er dens eneste fordel. Alt andet er potentielle problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje at prøve den alternative løsning med Jackett & NZBHydra2, [Prowlarr](/prowlarr)

[Selv Jackett siger, at /all bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)

Brug af all-endepunktet har ingen fordele (udover reduceret administrativ arbejdsbyrde), kun ulemper:

- du mister kontrollen over indekser-specifikke indstillinger (kategorier, søgemetoder osv.)
- blanding af søgemetoder (IMDB, forespørgsel osv.) kan medføre resultater af lav kvalitet
- indekser-specifikke kategorier (\>= 100000) kan ikke bruges.
- langsomme indeksere vil sænke den samlede hastighed
- det samlede antal resultater er begrænset til 1000

Ved at tilføje hver indekser separat kan du finjustere kategorierne for hver indekser, hvilket kan være et problem med `/all`-endepunktet, hvis brug af den forkerte kategori forårsager fejl på nogle trackere. I er hver indekser begrænset til 1000 resultater, hvis paginering understøttes, eller 100, hvis det ikke er tilfældet, hvilket betyder, at jo flere trackere du tilføjer til Jackett, desto mere sandsynligt er det, at du klipper resultater. Endelig, hvis *én* af trackerne i `/all` returnerer en fejl, vil deaktivere den, og nu får du ingen resultater.

### Brug af NZBHydra2 som en enkelt indgang

Brug af NZBHydra2 som en enkelt indekserindgang (dvs. 1 NZBHydra2-indgang i Readarr for mange indeksere i NZBHydra2) i stedet for flere (dvs. mange NZBHydra2-indgange i Readarr for mange indeksere i NZBHydra2) har de samme problemer som nævnt ovenfor med Jacketts `/all`-endepunkt.

### Problem ikke angivet

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers skal du diskutere det med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, skal du foreslå at tilføje det til wikien.

## Fejl

Her er nogle af de almindelige fejl, du kan se, når du tilføjer en indekser

### Forbindelsen blev afbrudt: Der opstod en uventet fejl under afsendelse

Dette skyldes, at indekseren bruger en SSL-protokol, som den nuværende .NET-version i [Readarr => System => Status](/readarr/system#status) ikke understøtter.

### Anmodningen udløb

Readarr modtager ingen respons fra indekseren.

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
- lokale DNS-problemer
- lokale IPv6-problemer - typisk er IPv6 aktiveret, men ikke funktionsdygtig
- brug af Privoxy og forkert konfiguration af denne

### Problem ikke angivet

Du kan også gennemgå nogle almindelige tilladelser og netværksfejlfinding kommandoer [i vores guide](/permissions-and-networking). Ellers skal du diskutere det med supportteamet på Discord. Hvis dette er noget, der kan være et almindeligt problem, skal du foreslå at tilføje det til wikien.