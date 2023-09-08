---
title: Sonarr Docker-installasjon
description: Docker-installasjonsveiledning for Sonarr
published: true
date: 2023-08-12T16:03:21.613Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:15.754Z
---

# Docker

Sonarr-teamet tilbyr ikke en offisiell Docker-bilde. Imidlertid har flere tredjeparter opprettet og vedlikeholder sine egne.

Disse instruksjonene gir generell veiledning som skal gjelde for alle Sonarr Docker-bilder.

Synology-brukere kan se [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **Portainer bør unngås for oppsett av Docker-containere** {.is-danger}

- Portainer gir et pent GUI for administrasjon av containere, men det er alt det er nyttig for.
- Portainer bør kun brukes for å vise Docker-containerlogger / containerstatus.
- Det anbefales sterkt å bruke Docker Compose og ikke bruke Portainer.
- Portainer har mange problemer, som:
  - Feil rekkefølge av kilde og mål for monteringer
  - Inkonsistent forskjell på store og små bokstaver
  - Ingen automatisk opprettede egendefinerte nettverk for kommunikasjon mellom containere
  - Inkonsistente compose-implementeringer på forskjellige arkitekturer
  - Henter hver tagg ved oppdatering når du ikke angir en spesifikk tagg
  - Evner er skjulte og noen fungerer ikke i det hele tatt på ARM-plattformer

Se denne [Docker-guiden](/docker-guide) og [TRaSH's Docker-tutorial](https://trash-guides.info/hardlinks/) i stedet for hvordan du setter opp Docker Compose.

## Unngå vanlige fallgruver

### Volumer og stier

Det er to vanlige problemer med Docker-volumer: Stier som er forskjellige mellom Sonarr- og nedlastingsklientcontaineren og stier som hindrer raske flyttinger og hardlinker.

Det første er et problem fordi nedlastingsklienten vil rapportere en nedlastingsbane som `/torrents/My.Series.2018/`, men i Sonarr-containeren kan den være på `/downloads/My.Series.2018/`. Det andre er et ytelsesproblem og forårsaker problemer for seeding av torrents. Begge problemene kan løses med godt planlagte, konsistente stier.

De fleste Docker-bilder foreslår stier som `/tv` og `/downloads`. Dette forårsaker treg flytting og tillater ikke hardlinker fordi de anses som to forskjellige filsystemer inne i containeren. Noen anbefaler også stier for nedlastingsklientcontaineren som er forskjellige fra Sonarr-containeren, som /torrents.

Den beste løsningen er å bruke et enkelt, felles volum inne i containerne, for eksempel /data. Seriene dine vil være i `/data/Series`, torrents i `/data/downloads/torrents` og/eller usenet-nedlastinger i `/data/downloads/usenet`.

Hvis dette rådet ikke følges, må du konfigurere en ekstern stiavbilding i Sonarr webgrensesnittet (Innstillinger › Nedlastingsklienter).

### Eierskap og tillatelser

Tillatelser og eierskap av filer er et av de vanligste problemene for Sonarr-brukere, både inne og utenfor Docker. De fleste bilder har miljøvariabler som kan brukes til å overstyre standardbruker, gruppe og umask. Du bør bestemme dette før du setter opp alle containerne dine. Anbefalingen er å bruke en felles gruppe for alle relaterte containere, slik at hver container kan bruke de delte gruppetillatelsene til å lese og skrive filer på de monterte volumene.
Husk at Sonarr vil trenge lese- og skrivetilgang til nedlastingsmappene samt de endelige mappene.

> For en mer detaljert forklaring av disse problemene, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikkelen.
{.is-info}

## Installer Sonarr

For å installere og bruke disse Docker-bildene, må du huske på det ovennevnte mens du følger dokumentasjonen deres. Det er mange måter å administrere Docker-bilder og containere på, så installasjon og vedlikehold av dem vil avhenge av ruten du velger.

- [hotio/sonarr](https://hotio.dev/containers/sonarr/)
- [lscr.io/linuxserver/sonarr](https://docs.linuxserver.io/images/docker-sonarr)
{.links-list}