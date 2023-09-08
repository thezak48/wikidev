---
title: Readarr Docker-installasjon
description: Docker-installasjonsveiledning for Readarr
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Readarr-teamet tilbyr ikke en offisiell Docker-avbildning. Imidlertid har flere tredjeparter opprettet og vedlikeholder sine egne.

Disse instruksjonene gir generell veiledning som skal gjelde for alle Readarr Docker-avbildninger.

## Portainer

> **Portainer bør unngås for oppsett av Docker-beholdere** {.is-danger}

- Portainer gir et pent GUI for administrasjon av beholdere, men det er alt det er nyttig for.
- Portainer bør kun brukes for å vise Docker-beholderlogger / beholderstatus.
- Det anbefales sterkt å bruke Docker Compose og ikke bruke Portainer.
- Portainer har mange problemer, som:
  - Feil rekkefølge av kilde og mål for monteringer
  - Inkonsistent forskjell på store og små bokstaver
  - Ingen automatisk opprettede egendefinerte nettverk for kommunikasjon mellom beholdere
  - Inkonsistente komposisjonsimplementeringer på forskjellige arkitekturer
  - Henter hver tagg ved oppdatering når du ikke angir en spesifikk tagg
  - Evner er skjulte og noen fungerer ikke i det hele tatt på ARM-plattformer

Se denne [Docker-guiden](/docker-guide) og [TRaSH's Docker-opplæring](https://trash-guides.info/hardlinks/) i stedet for hvordan du setter opp Docker Compose.

## Unngå vanlige fallgruver

### Volumer og stier

Det er to vanlige problemer med Docker-volumer: Stier som er forskjellige mellom Readarr- og nedlastingsklientbeholderen og stier som hindrer raske flyttinger og hardlenker.

Det første er et problem fordi nedlastingsklienten vil rapportere en nedlastings sti som `/torrents/My.Movie.2018/`, men i Readarr-beholderen kan den være på `/downloads/My.Movie.2018/`. Det andre er et ytelsesproblem og forårsaker problemer med å dele torrents. Begge problemene kan løses med godt planlagte, konsistente stier.

De fleste Docker-avbildninger foreslår stier som `/books` og `/downloads`. Dette forårsaker treg flytting og tillater ikke hardlenker fordi de anses som to forskjellige filsystemer inne i beholderen. Noen anbefaler også stier for nedlastingsklientbeholderen som er forskjellige fra Readarr-beholderen, som /torrents.

Den beste løsningen er å bruke et enkelt, felles volum inne i beholderne, for eksempel /data. Bøkene dine vil være i `/data/Books`, torrents i `/data/downloads/torrents` og/eller usenet-nedlastinger i `/data/downloads/usenet`.

Hvis dette rådet ikke følges, må du konfigurere en ekstern stiavbildning i Readarr-webgrensesnittet (Innstillinger › Nedlastingsklienter).

### Calibre-integrasjon

Når du oppretter en rotmappe, kan du velge å bruke Calibre-integrasjon eller ikke. Dette valget kan bare gjøres under opprettelse av mappen, og hvis du velger å ikke bruke Calibre, kan du ikke legge det til senere. Hvis du for øyeblikket bruker Calibre til å administrere bokbiblioteket ditt, bør du velge denne opsjonen. Hvis du bruker det, vil Calibre navngi og organisere bokfilene dine for deg.

Hvis du kjører Calibre, må du først starte Calibre Content Server (Innstillinger / Deling over nettet), og også sette opp en bruker og et passord. Dette vil kreve en omstart av Calibre.

> Vær oppmerksom på at Calibre Content Server og Calibre IKKE er Calibre Web. Calibre Web er et separat verktøy som ikke har noe med noen av disse programmene å gjøre, og er ikke nødvendig eller brukt av Readarr på noen måte.
{.is-warning}

### Eierskap og tillatelser

Tillatelser og eierskap av filer er et av de vanligste problemene for Readarr-brukere, både inne og utenfor Docker. De fleste avbildninger har miljøvariabler som kan brukes til å overstyre standardbruker, gruppe og umask. Du bør bestemme dette før du setter opp alle beholderne dine. Anbefalingen er å bruke en felles gruppe for alle relaterte beholdere, slik at hver beholder kan bruke delte gruppetillatelser til å lese og skrive filer på monterte volumer.
Husk at Readarr vil trenge lese- og skrivetilgang til nedlastingsmappene samt de endelige mappene.

> For en mer detaljert forklaring av disse problemene, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikkelen.
{.is-info}

## Installer Readarr

For å installere og bruke disse Docker-avbildningene, må du huske på det ovennevnte mens du følger dokumentasjonen deres. Det er mange måter å administrere Docker-avbildninger og beholdere på, så installasjon og vedlikehold av dem vil avhenge av ruten du velger.

> Midlertidig må du bruke :nightly eller :develop-taggene med Docker-avbildninger, siden det ikke finnes en hovedgren. [Se denne FAQ-posten for betydningen av grenene](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}