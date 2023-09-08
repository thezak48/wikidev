---
title: Sonarr Rask Startveiledning
description: 
published: true
date: 2022-07-14T14:07:19.793Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-09-03T19:14:22.283Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Rask Start Oppsettveiledning](#rask-start-oppsettveiledning)
- [Oppstart](#oppstart)
- [Mediehåndtering](#mediehåndtering)
  - [Episodenavn](#episodenavn)
  - [Importering](#importering)
  - [Rotmapper](#rotmapper)
- [Profiler](#profiler)
- [Indekser](#indekser)
- [Nedlastingsklienter](#nedlastingsklienter)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
- [Hvordan importere ditt eksisterende organiserte mediebibliotek](#hvordan-importere-ditt-eksisterende-organiserte-mediebibliotek)
  - [Importer episoder](#importer-episoder)
    - [Importering av eksisterende medier](#importering-av-eksisterende-medier)
    - [Ingen treff funnet](#ingen-treff-funnet)
    - [Fiks feilaktig mappenavn etter importering](#fiks-feilaktig-mappenavn-etter-importering)
- [Legg til nye serier](#legg-til-nye-serier)

# Rask Start Oppsettveiledning

> Denne siden er fortsatt under arbeid og er ikke komplett. Bidrag er velkomne.

> For en mer detaljert gjennomgang av alle innstillingene, sjekk [Sonarr => Innstillinger](/sonarr/settings)
{.is-info}

I denne veiledningen vil vi prøve å forklare det grunnleggende oppsettet du trenger å gjøre for å komme i gang med Sonarr. Vi kommer til å hoppe over noen alternativer som du kan se på skjermen. Hvis du ønsker å gå dypere inn i disse, kan du se den relevante siden i FAQ og dokumentasjonen for en fullstendig forklaring.

> Vær oppmerksom på at innenfor skjermbildene og GUI-innstillingene i `orange` er avanserte alternativer, så du må klikke på `Vis avansert` øverst på siden for å gjøre dem synlige.
{.is-warning}

# Oppstart

Etter installasjon og oppstart åpner du en nettleser og går til `http://{din_ip_her}:8989`

![qs_startup.png](/assets/sonarr/qs_startup.png)

# Mediehåndtering

Først skal vi se på innstillingene for `Mediehåndtering` der vi kan sette opp våre foretrukne navngivings- og filhåndteringsinnstillinger.

Klikk på `Innstillinger` => `Mediehåndtering` i venstremenyen.

## Episodenavn

![qs_episodenaming.png](/assets/sonarr/qs_episodenaming.png)

- Merk av i boksen for å aktivere Omdøp episoder.
- Bestem deg for dine standard-, daglige- og anime-episodenavnkonvensjoner. Du bør se gjennom de anbefalte navngivingskonvensjonene [her](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/).

> Hvis du velger å ikke inkludere kvalitet/oppløsning eller utgivelsesgruppe, er dette informasjon du ikke kan få tilbake senere. Det anbefales på det sterkeste at du inkluderer disse i navngivingsordningen din.
{.is-info}

## Importering

![mm_importing.png](/assets/sonarr/mm_importing.png)

- (Avansert alternativ) Hvis du vil at TBA-episoder skal importeres umiddelbart, endrer du "Episode Title Required" til "Never".
- (Avansert alternativ) Aktiver `Bruk hardlenker i stedet for kopi` for mer informasjon om hvordan og hvorfor med eksempler, se [TRaSH's Hardlinks Guide](https://trash-guides.info/hardlinks).
- Merk av i boksen for å importere ekstra filer, og legg til minst `.srt` i listen.

## Rotmapper

Her skal vi legge til rotmappen som Sonarr vil bruke for å importere ditt eksisterende organiserte mediebibliotek, og hvor Sonarr vil importere (kopiere/hardlenke/flytte) medier etter at nedlastingsklienten din har lastet dem ned. Dette er mappen der seriene og episodene dine er lagret for at mediespilleren din skal kunne spille dem av. Det er IKKE der du laster ned filer til!

> \* Brukere av ikke-Windows: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
> \* Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.
{.is-warning}

> **Brukeren og gruppen du konfigurerte Sonarr til å kjøre som, må ha lese- og skrivetilgang til dette stedet.**
{.is-info}

> **Nedlastingsmappen og mediamappen kan ikke være samme sted**
{.is-danger}

Ikke glem å lagre endringene dine!

# Profiler

`Innstillinger` => `Profiler`

Vi anbefaler at du oppretter dine egne profiler og bare velger de kvalitetskildene du faktisk ønsker. Det finnes imidlertid flere forhåndsutfylte kvalitetsprofiler å velge mellom, hvis en av disse passer. Hvis du trenger mer informasjon om profiler, kan du se den [relevante wikisiden](/sonarr/settings#profiles) for den delen.

# Indekser

`Innstillinger` => `Indekser`

Her legger du til indekser/sporere som du vil bruke til å faktisk laste ned filene dine.

Når du har klikket på <kb>+</kb>-knappen for å legge til en ny indekser, vil du få opp et nytt vindu med mange forskjellige alternativer. For Sonarr betrakter vi både Usenet-indekser og Torrent-sporere som "indekser".

Det er to seksjoner her: Usenet og Torrents. Basert på hvilken nedlastingsklient du vil bruke, vil du velge hvilken type indekser du vil gå for.

De fleste Usenet-indekser krever en API-nøkkel, som kan finnes på profilsiden din på indekserens nettsted.

De fleste torrent-sporere krever at [Prowlarr](/prowlarr) eller Jackett brukes i Sonarr.

Legg til minst en indekser for at Sonarr skal fungere ordentlig.

> Se [innstillingssiden](/sonarr/settings#indexers) og [Mer informasjon (Støttet)](/sonarr/supported#indexers)-siden for denne seksjonen for mer informasjon.
{.is-info}

# Nedlastingsklienter

`Innstillinger` => `Nedlastingsklienter`

Nedlasting og importering er der de fleste opplever problemer. Fra et overordnet perspektiv må programvaren kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes et stort utvalg av støttede nedlastingsklienter og en enda større variasjon av oppsett. Dette betyr at selv om det finnes noen vanlige oppsett, er det ikke én riktig oppsett, og alle oppsett kan være litt forskjellige. Men det finnes mange feilaktige oppsett.

> Se [innstillingssiden](/sonarr/settings#download-clients), [Mer informasjon (Støttet)](/sonarr/supported#download-clients)-siden for denne seksjonen, og [TRaSH's Nedlastingsklientguider](https://trash-guides.info/Downloaders/) for mer informasjon.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Sonarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Sonarr vil overvåke nedlastingsklientens aktive nedlastinger som bruker det kategorinavnet. Den overvåker dette via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Sonarr kjenne den endelige filplasseringen som rapportert av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din og tilgjengelig for Sonarr.
- Sonarr vil skanne denne fullførte filplasseringen etter filer som Sonarr kan bruke. Den vil analysere filnavnet for å matche det med den forespurte medien. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte medielokasjonen.
- Atomiske flyttinger (umiddelbare flyttinger) er aktivert som standard. Filsystemet og monteringene må være de samme for nedlastingsmappen og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Sonarr falle tilbake og kopiere filen og deretter slette den fra kilden, noe som er I/O-intensivt.
- Hvis alternativet "Behandling av fullførte nedlastinger - Fjern" er aktivert i Sonarrs innstillinger, vil gjenværende filer fra nedlastingen bli sendt til papirkurven eller resirkuleringen via en forespørsel til klienten din om å slette/fjerne utgivelsen.

### BitTorrent

{#bittorrent}

- Sonarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Sonarr vil overvåke nedlastingsklientens aktive nedlastinger som bruker det kategorinavnet. Denne overvåkingen skjer via nedlastingsklientens API.
- Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Sonarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil Sonarr opprette en hardlenke til filen hvis det støttes av oppsettet ditt, eller kopiere den hvis hardlenker ikke støttes.
- Hardlenker er aktivert som standard. [En hardlenke vil ikke bruke noe ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringene må være de samme for nedlastingsmappen og mediebiblioteket ditt. Hvis opprettelsen av hardlenken mislykkes eller oppsettet ditt ikke støtter hardlenker, vil Sonarr falle tilbake og kopiere filen.
- Hvis alternativet "Behandling av fullførte nedlastinger - Fjern" er aktivert i Sonarrs innstillinger, vil Sonarr slette torrenten fra klienten din og be klienten om å fjerne torrentdataene, men bare hvis klienten rapporterer at seeding er fullført og torrenten er stoppet (pauset ved fullføring).

# Hvordan importere ditt eksisterende organiserte mediebibliotek

> Merk at Sonarr ikke søker regelmessig etter episoder. Se FAQ-innlegget for detaljer for å forstå hvordan Sonarr fungerer.
[Hvordan finner Sonarr episoder?](/sonarr/faq#hvordan-finner-sonarr-episoder)
{.is-info}

Etter at du har satt opp profilene/kvalitetsstørrelsene dine og lagt til indekser og nedlastingsklient(er), er det på tide å importere ditt eksisterende organiserte mediebibliotek.

Kommer snart - Bidrag er velkomne

## Importering av eksisterende medier

Avhengig av hvor godt dine eksisterende seriemapper er navngitt, vil Sonarr prøve å matche dem med riktig serie. Du bør gå gjennom denne listen nøye før du importerer.

Biblioteksimport skal bare brukes på et eksisterende organisert bibliotek og skal ikke brukes på en nedlastingsmappe eller for å ad hoc-importere medier.

1. Gå til Biblioteksimport
1. Les og forstå hjelpeteksten for Biblioteksimport
1. Velg eller legg til rotmappen (biblioteket) for å importere serier fra
1. Gå gjennom Sonarrs kartlegging/matching av seriemapper til TVDb-serier
1. Angi overvåkingsinnstillingene og kvalitetsprofilen din som passer
1. Klikk på Start Import

### Ingen treff funnet

1. Søk etter serienavnet eller TVDbId i serievalgboksen
1. Se [dette FAQ-innlegget](/sonarr/faq#hvorfor-kan-jeg-ikke-legge-til-en-serie) hvis serien ikke kan bli funnet

### Fiks feilaktig mappenavn etter importering

1. Fjern serien fra Sonarr
1. Biblioteksimport
1. Sørg for at serien er riktig kartlagt

# Legg til nye serier

[Se bibliotekssiden for ytterligere informasjon](/sonarr/library#legg-til-ny)

# Importer episoder

- Bruk Wanted => Manuell import for å importere episodfiler til deres seriemapper på ad hoc-basis
- Bruk Administrer episoder på en seriens side for å omkartlegge eller kartlegge eksisterende episodfiler i en seriemappe