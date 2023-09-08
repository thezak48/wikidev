---
title: Lidarr Docker-installasjon
description: Docker-installasjonsveiledning for Lidarr
published: true
date: 2023-08-12T16:03:02.989Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:37.188Z
---

# Docker

Lidarr-teamet tilbyr ikke en offisiell Docker-bilde. Imidlertid har flere tredjeparter opprettet og vedlikeholder sine egne.

Disse instruksjonene gir generell veiledning som skal gjelde for ethvert Lidarr Docker-bilde.

## Portainer

> **Portainer bør unngås for oppsett av Docker-containere** {.is-danger}

- Portainer gir et pent GUI for administrasjon av containere, men det er alt det er nyttig for.
- Portainer bør kun brukes for å vise Docker-containerlogger / containerstatus.
- Det anbefales sterkt å bruke Docker Compose og ikke bruke Portainer.
- Portainer har mange problemer, som:
  - Feil rekkefølge av kilde og mål for monteringer
  - Inkonsistent forskjell på store og små bokstaver
  - Ingen automatisk opprettede egendefinerte nettverk for kommunikasjon mellom containere
  - Inkonsistente implementeringer av Docker Compose på forskjellige arkitekturer
  - Henter hver tagg ved oppdatering når du ikke angir en spesifikk tagg
  - Evner er skjulte og noen fungerer ikke i det hele tatt på ARM-plattformer

Se denne [Docker-guiden](/docker-guide) og [TRaSH's Docker-opplæring](https://trash-guides.info/hardlinks/) i stedet for hvordan du setter opp Docker Compose.

## Unngå vanlige fallgruver

### Volumer og stier

Det er to vanlige problemer med Docker-volumer: Stier som er forskjellige mellom Lidarr- og nedlastingsklientcontaineren og stier som hindrer raske flyttinger og hardlenker.

Det første er et problem fordi nedlastingsklienten vil rapportere en nedlastings sti som `/torrents/My.Music.2018/`, men i Lidarr-containeren kan den være på `/downloads/My.Music.2018/`. Det andre er et ytelsesproblem og forårsaker problemer med seeding av torrents. Begge problemene kan løses med godt planlagte, konsistente stier.

De fleste Docker-bilder foreslår stier som `/music` og `/downloads`. Dette forårsaker treg flytting og tillater ikke hardlenker fordi de anses som to forskjellige filsystemer inne i containeren. Noen anbefaler også stier for nedlastingsklientcontaineren som er forskjellige fra Lidarr-containeren, som f.eks. /torrents.

Den beste løsningen er å bruke et enkelt, felles volum inne i containerne, som f.eks. /data. Musikken din vil være i `/data/Music`, torrents i `/data/downloads/torrents` og/eller usenet-nedlastinger i `/data/downloads/usenet`.

Hvis dette rådet ikke følges, må du konfigurere en ekstern stiavbilding i Lidarr webgrensesnittet (Innstillinger › Nedlastingsklienter).

### Eierskap og tillatelser

Tillatelser og eierskap av filer er et av de vanligste problemene for Lidarr-brukere, både inne og utenfor Docker. De fleste bilder har miljøvariabler som kan brukes til å overstyre standardbruker, gruppe og umask. Du bør bestemme dette før du setter opp alle containerne dine. Anbefalingen er å bruke en felles gruppe for alle relaterte containere, slik at hver container kan bruke delte gruppetillatelser til å lese og skrive filer på monterte volumer.
Husk at Lidarr vil trenge lese- og skrivetilgang til nedlastingsmappene samt de endelige mappene.

> For en mer detaljert forklaring av disse problemene, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikkelen.
{.is-info}

## Installer Lidarr

For å installere og bruke disse Docker-bildene, må du huske på det ovennevnte mens du følger dokumentasjonen deres. Det er mange måter å administrere Docker-bilder og containere på, så installasjon og vedlikehold av dem vil avhenge av ruten du velger.

- [hotio/lidarr](https://hotio.dev/containers/lidarr/)
- [lscr.io/linuxserver/lidarr](https://docs.linuxserver.io/images/docker-lidarr)
{.links-list}