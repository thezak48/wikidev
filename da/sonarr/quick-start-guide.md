---
title: Sonarr Hurtig Start Guide
description: 
published: true
date: 2022-07-14T14:07:19.793Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-09-03T19:14:22.283Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Hurtig Start Opsætningsguide](#hurtig-start-opsætningsguide)
- [Opstart](#opstart)
- [Mediehåndtering](#mediehåndtering)
  - [Episodenavngivning](#episodenavngivning)
  - [Importering](#importering)
  - [Rodmapper](#rodmapper)
- [Profiler](#profiler)
- [Indexere](#indexere)
- [Downloadklienter](#downloadklienter)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
- [Sådan importerer du dit eksisterende organiserede mediebibliotek](#sådan-importerer-du-dit-eksisterende-organiserede-mediebibliotek)
  - [Importer episoder](#importer-episoder)
    - [Importering af eksisterende medier](#importering-af-eksisterende-medier)
    - [Ingen match fundet](#ingen-match-fundet)
    - [Ret fejlagtigt mappenavn efter importering](#ret-fejlagtigt-mappenavn-efter-importering)
- [Tilføj ny serie](#tilføj-ny-serie)

# Hurtig Start Opsætningsguide

> Denne side er stadig under udarbejdelse og er ikke komplet. Bidrag er velkomne.

> For en mere detaljeret gennemgang af alle indstillinger, se [Sonarr => Indstillinger](/sonarr/settings)
{.is-info}

I denne guide vil vi forsøge at forklare den grundlæggende opsætning, du skal udføre for at komme i gang med Sonarr. Vi vil springe nogle af de muligheder over, som du måske ser på skærmen. Hvis du vil dykke dybere ned i disse, kan du se den relevante side i FAQ'en og dokumentationen for en fuld forklaring.

> Bemærk venligst, at inden for skærmbillederne og GUI-indstillingerne i `orange` er avancerede indstillinger, så du skal klikke på `Vis avanceret` øverst på siden for at gøre dem synlige.
{.is-warning}

# Opstart

Efter installation og opstart åbner du en browser og går til `http://{din_ip_her}:8989`

![qs_startup.png](/assets/sonarr/qs_startup.png)

# Mediehåndtering

Først kigger vi på indstillingerne for `Mediehåndtering`, hvor vi kan konfigurere vores foretrukne navngivning og filhåndteringsindstillinger.

Klik på `Indstillinger` => `Mediehåndtering` i venstremenuen.

## Episodenavngivning

![qs_episodenaming.png](/assets/sonarr/qs_episodenaming.png)

- Markér afkrydsningsfeltet for at aktivere Omdøb episoder.
- Beslut dig for dine standard-, daglige- og anime-episodenavngivelseskonventioner. Du bør gennemgå de anbefalede navngivelseskonventioner [her](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/).

> Hvis du vælger ikke at inkludere kvalitet/opløsning eller udgivelsesgruppe, er dette information, du ikke kan få tilbage senere. Det anbefales kraftigt, at du inkluderer disse i din navngivelsesstruktur.
{.is-info}

## Importering

![mm_importing.png](/assets/sonarr/mm_importing.png)

- (Avanceret indstilling) Hvis du vil have TBA-episoder importeret med det samme, skal du ændre "Episode Title Required" til "Never".
- (Avanceret indstilling) Aktivér `Brug hardlinks i stedet for kopi` for mere information om, hvordan og hvorfor med eksempler [TRaSH's Hardlinks Guide](https://trash-guides.info/hardlinks).
- Markér afkrydsningsfeltet for at importere ekstra filer og tilføj mindst `.srt` til listen.

## Rodmapper

Her tilføjer vi rodmappen, som Sonarr vil bruge til at importere dit eksisterende organiserede mediebibliotek, og hvor Sonarr vil importere (kopiere/hardlinke/flytte) dine medier efter, at din downloadklient har downloadet dem. Dette er mappen, hvor dine serier og episoder er gemt, så din medieafspiller kan afspille dem. Det er IKKE her, du downloader filer til!

> \* Brugere af ikke-Windows: Hvis du bruger en NFS-mount, skal du sørge for, at `nolock` er aktiveret.
> \* Hvis du bruger en SMB-mount, skal du sørge for, at `nobrl` er aktiveret.
{.is-warning}

> **Brugeren og gruppen, du har konfigureret Sonarr til at køre som, skal have læse- og skriveadgang til dette sted.**
{.is-info}

> **Din downloadmappe og mediemappe kan ikke være det samme sted**
{.is-danger}

Glem ikke at gemme dine ændringer!

# Profiler

`Indstillinger` => `Profiler`

Vi anbefaler, at du opretter dine egne profiler og kun vælger de kvalitetskilder, du rent faktisk ønsker. Der er dog flere forudfyldte kvalitetsprofiler at vælge imellem, hvis en af disse passer. Hvis du har brug for mere information om profiler, kan du se den [relevante wiki-side](/sonarr/settings#profiles) for den sektion.

# Indexere

`Indstillinger` => `Indexere`

Her tilføjer du indexeren/trackeren, som du vil bruge til at downloade dine filer.

Når du har klikket på <kb>+</kb>-knappen for at tilføje en ny indexer, får du en ny vindue med mange forskellige muligheder. I Sonarr betragtes både Usenet Indexere og Torrent Trackere som "Indexere".

Der er to sektioner her: Usenet og Torrents. Afhængigt af hvilken downloadklient du vil bruge, skal du vælge den type indexer, du vil bruge.

De fleste Usenet indexere kræver en API-nøgle, som kan findes på din profilside på indexerens hjemmeside.

De fleste torrent trackere kræver, at [Prowlarr](/prowlarr) eller Jackett bruges i Sonarr.

Tilføj mindst en indexer for, at Sonarr kan fungere korrekt.

> Se [indstillingerne](/sonarr/settings#indexers) og [Mere info (Understøttet)](/sonarr/supported#indexers)-siden for denne sektion for mere information.
{.is-info}

# Downloadklienter

`Indstillinger` => `Downloadklienter`

Download og importering er, hvor de fleste mennesker oplever problemer. Overordnet set skal softwaren kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Det betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alles opsætning kan være lidt anderledes. Men der er mange forkerte opsætninger.

> Se [indstillingerne](/sonarr/settings#download-clients), [Mere info (Understøttet)](/sonarr/supported#download-clients)-siden for denne sektion og [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for mere information.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Sonarr sender en downloadanmodning til din klient og tilknytter den etiket eller kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Sonarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er fuldført, vil Sonarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe og tilgængelig for Sonarr.
- Sonarr scanner denne fuldførte filplacering for filer, som Sonarr kan bruge. Den analyserer filnavnet for at matche det med det ønskede medie. Hvis det kan gøre det, omdøber den filen i henhold til dine specifikationer og flytter den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Sonarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er IO-intensivt.
- Hvis indstillingen "Fjern håndtering af fuldførte downloads" er aktiveret i Sonarrs indstillinger, vil eventuelle resterende filer fra downloaden blive sendt til papirkurven eller genbrugsbeholderen via en anmodning til din klient om at slette/fjerne udgivelsen.

### BitTorrent

{#bittorrent}

- Sonarr sender en downloadanmodning til din klient og tilknytter den etiket eller kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Sonarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Færdige filer efterlades på deres oprindelige placering, så du kan seede filen (ratio eller tid kan justeres i downloadklienten eller fra Sonarr under den specifikke downloadklient). Når filerne importeres til din mediemappe, vil Sonarr oprette en hardlink til filen, hvis det understøttes af din opsætning, eller kopiere den, hvis hardlinks ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Sonarr falde tilbage og kopiere filen.
- Hvis indstillingen "Fjern håndtering af fuldførte downloads" er aktiveret i Sonarrs indstillinger, vil Sonarr slette torrenten fra din klient og bede klienten om at fjerne torrentdataene, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet (sat på pause ved fuldførelse).

# Sådan importerer du dit eksisterende organiserede mediebibliotek

> Bemærk, at Sonarr ikke regelmæssigt søger efter episoder. Se FAQ-indgangen for detaljer for at forstå, hvordan Sonarr fungerer.
[Hvordan finder Sonarr episoder?](/sonarr/faq#how-does-sonarr-find-episodes)
{.is-info}

Efter at have konfigureret dine profiler/kvalitetsstørrelser og tilføjet dine indexere og downloadklient(er), er det tid til at importere dit eksisterende organiserede mediebibliotek.

Kommer snart - Bidrag er velkomne

## Importering af eksisterende medier

Afhængigt af hvor godt dine eksisterende seriemapper er navngivet, vil Sonarr forsøge at matche dem med den korrekte serie. Du bør gennemgå denne liste omhyggeligt, inden du importerer.

Biblioteksimport skal kun bruges på et eksisterende organiseret bibliotek og må ikke bruges på en downloadmappe eller til ad hoc-import af medier.

1. Gå til Biblioteksimport
1. Læs og forstå hjælpeteksten til Biblioteksimport
1. Vælg eller tilføj rodmappen (biblioteksmappen) for at importere serier fra
1. Gennemgå Sonarrs kortlægning/matching af seriemapper til TVDb-serier
1. Indstil dine overvågningsindstillinger og kvalitetsprofil, som det passer
1. Klik på Start importering

### Ingen match fundet

1. Søg efter seriens navn eller TVDbId i serievælgeren
1. Se [denne FAQ-indgang](/sonarr/faq#why-can-i-not-add-a-series), hvis serien ikke kan findes

### Ret fejlagtigt mappenavn efter importering

1. Fjern serien fra Sonarr
1. Biblioteksimport
1. Sørg for, at serien er kortlagt korrekt

# Tilføj ny serie

[Se Bibliotekssiden for yderligere information](/sonarr/library#add-new)

# Importer episoder

- Brug Ønsket => Manuel import til at importere episodefiler til deres seriemapper på ad hoc-basis
- Brug Administrer episoder på en seriens side til at omkartlægge eller kortlægge eksisterende episodefiler i en seriemappe