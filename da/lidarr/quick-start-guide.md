---
title: Lidarr Hurtigstart
description: 
published: true
date: 2022-07-14T14:10:13.343Z
tags: 
editor: markdown
dateCreated: 2021-06-13T06:14:53.615Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Hurtigstartopsætningsguide](#hurtigstartopsætningsguide)
- [Forbehold](#forbehold)
- [Koncept](#koncept)
  - [Udgivelser (Metadata)](#udgivelser-metadata)
  - [Kunstner (Metadata)](#kunstner-metadata)
- [Første start](#første-start)
- [Indstillinger](#indstillinger)
  - [Mediehåndtering](#mediehåndtering)
  - [Profiler](#profiler)
  - [Kvalitet](#kvalitet)
  - [Indexere](#indexere)
  - [Downloadklienter](#downloadklienter)
    - [{.tabset}](#tabset)
      - [Usenet](#usenet)
      - [BitTorrent](#bittorrent)
- [Første kunstner](#første-kunstner)
- [Første download/import](#første-downloadimport)
- [Hurtigstart - Avanceret](#hurtigstart-avanceret)
  - [Lidarr-brugssag](#lidarr-brugssag)
    - [Løse filer](#løse-filer)
    - [Specialbiblioteker](#specialbiblioteker)
  - [Import af eksisterende bibliotek eller filer](#import-af-eksisterende-bibliotek-eller-filer)
    - [Forberedelse af eksisterende filer](#forberedelse-af-eksisterende-filer)
      - [Mappestruktur](#mappestruktur)
      - [Tagning](#tagning)
    - [Overvejelser før import](#overvejelser-før-import)
    - [Begynd import](#begynd-import)

# Hurtigstartopsætningsguide

> Denne side er stadig under udarbejdelse og er ikke komplet. Bidrag er velkomne.

> For en mere detaljeret gennemgang af alle indstillinger, se [Lidarr => Indstillinger](/lidarr/indstillinger)
{.is-info}

I denne guide vil vi forsøge at forklare den grundlæggende opsætning, du skal gøre for at komme i gang med Lidarr. Vi vil springe nogle af de muligheder over, som du måske ser på skærmen. Hvis du vil dykke dybere ned i dem, kan du se den relevante side i FAQ'en og dokumentationen for en fuld forklaring.

> Bemærk venligst, at indstillingerne i `orange` på skærmbillederne og i GUI'en er avancerede indstillinger, så du skal klikke på `Vis avanceret` øverst på siden for at gøre dem synlige.
{.is-warning}

# Forbehold

I denne guide vil vi forklare de grundlæggende trin til at begynde at arbejde med Lidarr. Denne guide antager, at du allerede har installeret applikationen. Installationsinstruktioner kan findes på følgende side [installation](/lidarr/installation). Vi vil fokusere på den minimale opsætning og de nødvendige indstillinger for at få en fungerende konfiguration. Der er yderligere opsætning og overvejelser, hvis nogen af følgende situationer gælder:

- Eksisterende bibliotek eller filer
- Forkert brugssag
- Forkert mappestruktur
- Forkert eller ekstremt kompliceret tagning
- Løs samling af filer
- Specialiserede musikbiblioteker: Klassisk, singler, elektronisk

Hvis nogen af ​​ovenstående situationer gælder, henvises der til afsnittet Hurtigstart - Avanceret.

Denne guide er opdelt i sektioner. Det anbefales at læse hele guiden for at få en fuld forståelse, men du kan springe til specifikke sektioner for øjeblikkelige bekymringer. Brug oversigten til venstre for at springe hurtigt.

# Koncept

For at bruge Lidarr korrekt skal de underliggende koncepter forstås. På et overordnet niveau følger det principperne for de andre Arr-applikationer. Lidarr fungerer som et musikbiblioteksstyringssystem, en dataaggregator og en automatiseringsplatform til at finde og downloade medier.

Herfra er afvigelsen ret betydelig. Styring af musikbiblioteker er en meget kompliceret proces, da der er mange konkurrerende variabler, der hindrer processen. I modsætning til styring af film eller tv-shows er der ikke en konsistent sæt standarder for musiktagning, navngivning eller opbevaring. Dette er yderligere kompliceret af de ændrede metoder til musikdistribution fra fysiske medier til elektroniske. Endelig er meningerne om, hvordan man håndterer denne styring, vidt forskellige.

Lidarr bruger oplysninger fra dataaggregatortjenester til at tagge og administrere musikbiblioteket korrekt. Disse tredjepartsdata repræsenterer medier i definerede kategorier og typer.

> Hvis dataen ikke findes i tredjepartstjenesterne, kan den IKKE administreres af Lidarr.
Detaljer findes nedenfor for at deltage og bidrage.
{.is-warning}

Den vigtigste tjeneste, der bruges, er [MusicBrainz](https://musicbrainz.org/). Dette er en gratis tjeneste, der er drevet af fællesskabet og eksisterer og overlever i sidste ende på dine bidrag og deltagelse. Oprettelse og bidrag til udgivelser ligger uden for denne guides omfang. Instruktioner kan findes her: [Sådan bidrager du](https://musicbrainz.org/doc/How_to_Contribute)

Dataen defineres i sidste ende af tredjepartsdatastandarderne. Hvis standarderne ikke stemmer overens med din brugssag, kan **Lidarr muligvis ikke være den rette løsning**. Andre applikationer til styring af dine medier kan omfatte:

[Beets Media Management](https://beets.io/)
[MusicBrainz Picard](https://picard.musicbrainz.org/)
[Music Bee](https://getmusicbee.com/)

Disse implementeringer kan bruges sammen med Lidarr, men dette ligger uden for denne guides omfang.

## Udgivelser (Metadata)

Lidarr har valgt standarden `Udgivelse` til styring af musikmedier. Dette betyder, at for at systemet fungerer korrekt, skal alle medier, der behandles af systemet, være en `Udgivelse`.

Eksempler på udgivelser:

- Album
- EP
- Single
- Broadcast

Hvert element, der skal administreres, skal have en korresponderende `Udgivelse` i tredjepartsdatatjenesten.

> `Udgivelser` skal eksistere i tredjepartstjenesterne for at kunne administreres i Lidarr.

## Kunstner (Metadata)

Kunstnere er præcis, hvad der kan forventes af `Udgivelseskunstneren`. Desværre har kunstnernavngivning, stilændringer over tid, brugerpræferencer og andre årsager forvirret, hvad der udgør denne `Udgivelseskunstner`.

Eksempler på korrekte og ukorrekte "kunstnere":

- Bob Dylan
- BOB DYLAN
- The Bob Dylan
- Bob Dylan, The
- Bob Dylan & the Band
- Bob Dylan feat. The Band
- The Band featuring Bob Dylan
- ...

Denne liste kunne fortsætte og fortsætte. Igen er alle `Udgivelser` korreleret med en `Kunstner`. Du skal finde (trin senere i denne guide) og bruge den korrekte `Kunstner` til at downloade en `Udgivelse`.

> `Udgivelseskunstnere` skal eksistere i tredjepartstjenesterne for at kunne administreres i Lidarr.

# Første start

Efter installation og start af Lidarr får du adgang ved at åbne en browser og gå til `http://{din_ip_her}:8686`

![lidarr_qs_startup.png](/assets/lidarr/quick-start-guide/lidarr_qs_startup.png)

Der vises to muligheder på startskærmen, men vi vil ikke bruge dem i starten.

# Indstillinger

Vi vil bruge standardkonfigurationen af indstillinger til at konfigurere Lidarr. Dette vil bruge de eksisterende profiler, kvalitet, tags osv.

> For en mere detaljeret gennemgang af alle indstillinger, se [Lidarr > Indstillinger](/lidarr/indstillinger)
{.is-info}

## Mediehåndtering

Først kigger vi på `Mediehåndtering`, hvor vi vil indstille `Rodmappe`. Dette vil være placeringen, hvor mediefilerne vil blive gemt.

> Opbevar ikke Lidarr-medier på en cloud-lagringsudbyder! På grund af den måde, Lidarr bruger tags på, vil dette dræbe eventuelle API-begrænsninger og forårsage problemer. Opbevar dit bibliotek på dit netværk.
{.is-warning}

Klik på `Indstillinger` > `Mediehåndtering` i venstre menu.

![lidarr_qs_mediamanagement.png](/assets/lidarr/quick-start-guide/lidarr_qs_mediamanagement.png)

Klik på `Tilføj (+)` for `Rodmapper`.

Du vil blive præsenteret for følgende vindue:

![lidarr_qs_rootfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_rootfolder.png)

- **Navn** - Dette er det `venlige navn` for opbevaringsstedet.
- **Sti** - Dette er den faktiske `sti` til opbevaringsstedet for data. Systemet/brugeren skal have de nødvendige tilladelser til denne opbevaringssti. Denne mappe kan ikke være din downloadplacering!

Lad de andre indstillinger være på deres standardværdier.

> Hvis du bruger en `Rodmappe` med eksisterende filer, skal du gennemgå afsnittet Hurtigstart - Avanceret for at få overvejelser.
{.is-warning}

> \* Ikke-Windows: Hvis du bruger en NFS-montering, skal du sørge for, at `nolock` er aktiveret.
> \* Hvis du bruger en SMB-montering, skal du sørge for, at `nobrl` er aktiveret.
{.is-warning}

> **Brugeren og gruppen, du har konfigureret Lidarr til at køre som, skal have læse- og skrivetilladelser til dette sted.** {.is-info}

> Din downloadklient downloader til en downloadmappe, og Lidarr importerer det til din mediemappe (endelige destination), som din medieserver bruger.
{.is-info}

> **Din downloadmappe og mediemappe kan ikke være det samme sted**
{.is-danger}

## Profiler

`Indstillinger` > `Profiler`

Profilindstillingerne forbliver på deres standardværdier.

## Kvalitet

`Indstillinger` > `Kvalitet`

Kvalitetsindstillingerne forbliver på deres standardværdier.

## Indexere

`Indstillinger` > `Indexere`

Dette afsnit indstiller indexeren/trackeren, som du vil bruge til at finde downloadbare mediefiler.

Klik på `Tilføj (+)` for `Indexere`. Du vil blive præsenteret for et nyt vindue med mange forskellige muligheder. Lidarr betragter både Usenet-indexere og BitTorrent-trackere som `Indexere`.

Tilføj mindst en `Indexer`, så Lidarr kan finde tilgængelige filer korrekt.

Forståelsen af konfigurationen/koncepterne bag `Indexere` ligger uden for denne guides omfang. Internettet rummer en masse information om emnet.

## Downloadklienter

`Indstillinger` => `Downloadklienter`

![Lidarr-settings-download-clients.png](/assets/lidarr/Lidarr-settings-download-clients.png)

Download og import er det, hvor de fleste mennesker oplever problemer. Set fra et overordnet perspektiv skal softwaren kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange understøttede downloadklienter og endnu flere forskellige opsætninger. Dette betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alles opsætning kan være lidt anderledes. Men der er mange forkerte opsætninger.

> Se [indstillingssiden](/lidarr/indstillinger#downloadklienter), på siden [Mere info (Understøttet)](/lidarr/understøttet#downloadklienter) for dette afsnit og [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for mere information.
{.is-info}

### {.tabset}

#### Usenet

{#usenet}

- Lidarr sender en downloadanmodning til din klient og forbinder den med etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Lidarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er fuldført, vil Lidarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe og kan tilgås af Lidarr.
- Lidarr scanner denne fuldførte filplacering for filer, som Lidarr kan bruge. Den analyserer filnavnet for at matche det med den ønskede medie. Hvis det kan gøre det, omdøber den filen i henhold til dine specifikationer og flytter den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Lidarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er IO-intensivt.
- Hvis indstillingen "Behandling af fuldførte downloads - Fjern" er aktiveret i Lidarrs indstillinger, sendes eventuelle resterende filer fra downloaden til papirkurven eller genbrugsbeholderen via en anmodning til din klient om at slette/fjerne udgivelsen.

#### BitTorrent

{#bittorrent}

- Lidarr sender en downloadanmodning til din klient og forbinder den med etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Lidarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Færdige filer efterlades på deres oprindelige placering, så du kan seede filen (forhold eller tid kan justeres i downloadklienten eller fra Lidarr under den specifikke downloadklient). Når filerne importeres til din mediemappe, opretter Lidarr en hardlink til filen, hvis det understøttes af din opsætning, eller kopierer den, hvis hardlinks ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Lidarr falde tilbage og kopiere filen.
- Hvis indstillingen "Behandling af fuldførte downloads - Fjern" er aktiveret i Lidarrs indstillinger, sletter Lidarr torrenten fra din klient og beder klienten om at fjerne torrentdataene, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet (sat på pause ved fuldførelse).

# Første kunstner

Hvis du følger denne guide, og din `Rodmappe` ikke havde nogen mediefiler, skal du tilføje en `Kunstner`.

`Bibliotek` > `Tilføj ny`

![lidarr_qs_addnew.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnew.png)

Dette vil linke til søgeskærmen for at finde en kunstner. Søg og vælg den `Kunstner`, du vil tilføje. Dette vil åbne vinduet "Tilføj ny kunstner".

![lidarr_qs_addnewdylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnewdylan.png)

Vi vil bruge standardvalgene, som bør inkludere:

- Rodmappe - Mappen, du oprettede
- Overvågning - Ingen
- Kvalitetsprofil - Enhver
- Tags - (tom)
- Start søgning efter manglende album - Ikke markeret

Dette vil starte downloaden af `Kunstner`-metadata. Dette vil tage noget tid afhængigt af mængden af data, der skal indsamles. Husk, at disse oplysninger kommer fra tredjepartskilder og kun er så komplette som det, fællesskabet har bidraget med.

Klik på den nytilføjede `Kunstner`. (Bob Dylan i dette eksempel)

> Standard `Metadataprofil` bruges, og kun `Udgivelser` af typen `Studioalbums` vises.

![lidarr_qs_dylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylan.png)

> Kan du ikke lide den downloadede metadata? - Bidrag til at gøre den bedre!
{.is-info}

# Første download/import

Endelig tid til at downloade/importere din første `Udgivelse`!

Find den `Udgivelse`, du vil tilføje til dit bibliotek. Vælg ikonet for manuel søgning (menneske) ved siden af udgivelsen.

![lidarr_qs_dylanrelease.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanrelease.png)

Dette vil åbne vinduet til valg af `Udgivelse`. Dette vindue viser resultaterne af `Indexer`-forespørgslen eller med andre ord søgeresultaterne for tilgængelige downloads.

> Standard `Kvalitetsprofil` tillader enhver filtype. Standard `Udgivelsesprofil` tillader alle downloads. For en detaljeret gennemgang af disse avancerede indstillinger, se [Lidarr > Indstillinger](/lidarr/indstillinger)

![lidarr_qs_dylandownload.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylandownload.png)

Gennemgå downloadvinduet for de forskellige angivne oplysninger:

1. Titel - Dette er navnet på downloaden, som returneres af `Indexeren`.
1. Kvalitet - Dette er kvaliteten som bestemt af Lidarr ved hjælp af titlen.
1. Advarselsindikatorerne giver en beskrivelse af, hvorfor downloaden ikke bestod Lidarrs kontrol. I eksemplet blev der returneret "Forkert album" i søgningen.

Når du har gennemgået det, skal du vælge downloadikonet (nummer 4) for at downloade den tilgængelige `Udgivelse`.

Hvis konfigureret korrekt, sendes downloaden til din `Downloadklient`.

Downloaden tilføjes til `Køen` og vil gennemgå de forskellige tilstande for din type `Downloadklient`.

Endelig importeres downloaden til din `Rodmappe`. Hvis alt er vellykket, skal det se ud som nedenfor.

![lidarr_qs_dylansucess.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylansuccess.png)

Du kan finde dine downloadede filer i din `Rodmappe` og kan bruge dem med din foretrukne medieafspiller.

![lidarr_qs_dylanfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanfolder.png)

# Hurtig start - Avanceret

Dette avancerede afsnit er beregnet til opsætninger, der måske har særlige hensyn. Gennemgå det, hvis det gælder for din konfiguration, og spar dig selv for nogle hovedpine.

> De følgende afsnit vil hjælpe med almindelige faldgruber og problemer.
{.is-warning}

## Lidarr-brugssag

Som tidligere nævnt i afsnittet om konceptet. Lidarr bør ikke bruges, hvis dit tilsigtede brug ikke matcher Lidarrs administrationsystem for `Udgivelser`. Lidarr fungerer IKKE med følgende brugssager:

- Løs samling af filer - Filer fra flere kunstnere (ikke kompilationer) eller flere `Udgivelser`
- Specialiserede musikbiblioteker: Klassisk, Singler, Elektronisk

### Løse filer

Lidarr fungerer ikke godt med løse filer, der ikke er organiseret. Det er bedst ikke at forsøge at bruge disse filer med Lidarr.

### Specialiserede biblioteker

Specialiserede biblioteker skaber unikke problemer for ethvert administrationsystem. Disse situationer kan fungere med Lidarr, men det kan kræve omfattende arbejde fra din side og i praksis betyde, at automatiseringen ikke kan anvendes. For eksempel:

- **Klassisk musik** - Har normalt omfattende krav eller ønsker til tagging. Metadata for `Udgivelser` vil sandsynligvis ikke eksistere eller være forkerte.
- **Singler** - Singler kan ikke være faktiske `Udgivelser`. Tredjepartsdatatjenester vil ikke returnere metadata. De vil ikke blive automatiseret, og Lidarr vil ikke kunne administrere dem.
- **Elektronisk** - Dette gælder IKKE for `Udgivelser` inden for den elektroniske genre. Dette handler om biblioteker med mix, beats, samples osv. (Beatport). Tredjepartsdatakilder genkender ikke disse som `Udgivelser`. De vil ikke blive automatiseret, og Lidarr vil ikke kunne administrere dem.

## Import af eksisterende bibliotek eller filer

> Bemærk, at Lidarr ikke regelmæssigt søger efter `Udgivelser`. Se disse to FAQ-indlæg for detaljer om, hvordan Lidarr fungerer.
[Hvordan finder Lidarr udgivelser?](/lidarr/faq#hvordan-finder-lidarr-udgivelser) og [Hvordan fungerer Lidarr?](/lidarr/faq#hvordan-fungerer-lidarr)
{.is-info}

> Automatisk import er en planlagt proces og kan ikke stoppes, når den er startet.
TILFØJ IKKE en `Rodmappe` med eksisterende filer, før du har gennemgået dette afsnit fuldt ud.
{.is-warning}

Lidarr bruger et automatiseret system til at tilføje `Udgivelseskunstnere` og `Udgivelser`, der findes i din `Rodmappe`.

Hvis Lidarrs brugssag matcher, og du ikke har unikke eller specialiserede biblioteker, kan du fortsætte med at importere dit eksisterende bibliotek.

Det er afgørende, at dine eksisterende biblioteksfiler er strukturerede og følger Lidarrs administrationsystem for `Udgivelser`. Dette betyder, at følgende ikke vil fungere:

- Forkert mappestruktur - Filer placeret i en enkelt mappe - Se afsnittet Forberedelse>Mappestruktur
- Forkert eller ekstremt kompliceret tagging - Se afsnittet Forberedelse>Tagging

### Forberedelse af dine eksisterende filer

For at den automatiserede proces kan fungere, skal dine filer være forberedt, så det hele fungerer effektivt eller overhovedet fungerer.

#### Mappestruktur

Det anbefales at følge den standardiserede mappestruktur:

\Rodmappe\Udgivelseskunstner\Udgivelse\XX - Spor

Dette, kombineret med korrekte tags, vil tillade næsten 95% eller mere genkendelse af medieafspillere.

#### Tagging

Tagging kan være en kompliceret procedure. Antallet af filer og den måde, de er tagget på i øjeblikket, vil bestemme, hvor meget arbejde der kræves.

De anbefalede metoder til tagging af dine filer inkluderer:

- MusicBrainz Picard
- Beets
- MusicBee, MediaMonkey, JRiver

Brugen af disse applikationer er uden for denne vejlednings omfang, men det er at foretrække at tilknytte MusicBrainz-udgivelses-ID'er som en del af tagging-processen.

> De fleste tagging-software kan oprette mappestrukturer og omdøbe filer, samtidig med at de tagger dem korrekt.
{.is-info}

### Overvejelser før import

Når filerne er korrekt tagget og navngivet, skal følgende elementer verificeres for at sikre, at processen fuldføres succesfuldt:

- **Systemarkitektur** - Anbefalet x64 / 64-bit - Import af store biblioteker kræver, at systemet har adgang til store mængder RAM og kører mere effektivt. x86 / 32-bit understøttes, men vil ikke være lige så effektivt og vil tage væsentligt længere tid.
- **Systemkrav til hukommelse (RAM)** - Minimum 4 GB, anbefalet 8 GB - Importprocessen kræver meget hukommelse, og hvis Lidarr importerer, mens en browser er åben, vil der blive brugt store mængder RAM.
- **Begrænsninger for `Udgivelses`-disk/spor** - Udgivelser med mange spor eller diske bør fjernes fra importprocessen. De kan importeres manuelt ved hjælp af de indbyggede procedurer. Der er ingen nøjagtig grænse, men for at være på den sikre side bør udgivelser med mere end 25 diske eller 250 spor fjernes.
- **`Udgivelseskunstner` med mange `Udgivelser`** - Lidarrs automatiserede proces sammenligner udgivelser med dine filer. Selvom det ikke er sandsynligt, at det vil mislykkes, vil det tage betydeligt længere tid at importere disse filer ved hjælp af den automatiserede procedure. Der er enkelte kunstnere med tusindvis af udgivelser.
- **Tid** - Den automatiserede importprocedure tager tid. Et rimeligt estimat vil være 1 time for 500 korrekt taggete `Udgivelser`. Dette varierer meget afhængigt af din lagring, internethastighed og systemets ydeevne.

### Begynd import

//

Kommer snart

- Overvågning * - Dette indstiller standardovervågningsindstillingen (`Udgivelser`) for `Rodmappen`.
- Kvalitetsprofil * - Dette indstiller standardkvalitetsindstillingen for `Rodmappen`.
- Metadataprofil * - Dette indstiller standardmetadataindstillingen for `Rodmappen`.