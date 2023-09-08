---
title: Radarr Docker-installasjon
description: Docker-installasjonsguide for Radarr
published: true
date: 2023-08-12T16:02:10.602Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:47.674Z
---

# Docker

Radarr-teamet tilbyr ikke en offisiell Docker-bilde. Imidlertid har en rekke tredjeparter opprettet og vedlikeholder sine egne.

Disse instruksjonene gir generell veiledning som skal gjelde for alle Radarr Docker-bilder.

Synology-brukere kan se [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **Portainer bør unngås for oppsett av Docker-containere** {.is-danger}

- Portainer gir et pent GUI for administrasjon av containere, men det er alt det er nyttig for.
- Portainer bør kun brukes for å vise Docker-containerlogger / containerstatus.
- Det anbefales sterkt å bruke Docker-compose og ikke bruke Portainer.
- Portainer har mange problemer, som:
  - Feil rekkefølge av kilde og mål for monteringer
  - Inkonsistent skriftfølsomhet
  - Ingen automatisk opprettede egendefinerte nettverk for kommunikasjon mellom containere
  - Inkonsistente komposisjonsimplementeringer på forskjellige arkitekturer
  - Henter hver tagg ved oppdatering når du ikke angir en spesifikk tagg
  - Evner er skjulte og noen fungerer ikke i det hele tatt på ARM-plattformer

Se denne [Docker-guiden](/docker-guide) og [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) i stedet for hvordan du setter opp Docker Compose.

## Unngå vanlige fallgruver

### Volum og stier

Det er to vanlige problemer med Docker-volumer: Stier som er forskjellige mellom Radarr- og nedlastingsklientcontaineren og stier som hindrer raske flyttinger og hardlinker.

Det første er et problem fordi nedlastingsklienten vil rapportere en nedlastingsbane som `/torrents/My.Movie.2018/`, men i Radarr-containeren kan den være på `/downloads/My.Movie.2018/`. Det andre er et ytelsesproblem og forårsaker problemer for seeding av torrents. Begge problemene kan løses med godt planlagte, konsistente stier.

De fleste Docker-bilder foreslår stier som `/movies` og `/downloads`. Dette forårsaker treg flytting og tillater ikke hardlinker fordi de anses som to forskjellige filsystemer inne i containeren. Noen anbefaler også stier for nedlastingsklientcontaineren som er forskjellige fra Radarr-containeren, som /torrents.

Den beste løsningen er å bruke et enkelt, felles volum inne i containerne, for eksempel /data. Filmene dine vil være i `/data/Movies`, torrents i `/data/downloads/torrents` og/eller usenet-nedlastinger i `/data/downloads/usenet`.

Hvis dette rådet ikke følges, må du konfigurere en ekstern stiavbilding i Radarr-webgrensesnittet (Innstillinger › Nedlastingsklienter).

### Eierskap og tillatelser

Tillatelser og eierskap av filer er et av de vanligste problemene for Radarr-brukere, både inne og utenfor Docker. De fleste bilder har miljøvariabler som kan brukes til å overstyre standardbruker, gruppe og umask, du bør bestemme dette før du setter opp alle containerne dine. Anbefalingen er å bruke en felles gruppe for alle relaterte containere, slik at hver container kan bruke de delte gruppetillatelsene til å lese og skrive filer på de monterte volumene.
Husk at Radarr vil trenge lese- og skrivetilgang til nedlastingsmappene samt de endelige mappene.

> For en mer detaljert forklaring av disse problemene, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikkelen.
{.is-info}

## Installer Radarr

For å installere og bruke disse Docker-bildene, må du huske på det ovennevnte mens du følger dokumentasjonen deres. Det er mange måter å administrere Docker-bilder og containere på, så installasjon og vedlikehold av dem vil avhenge av ruten du velger.

- [hotio/radarr](https://hotio.dev/containers/radarr/)
- [lscr.io/linuxserver/radarr](https://docs.linuxserver.io/images/docker-radarr)
{.links-list}