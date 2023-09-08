---
title: Prowlarr Docker-installasjon
description: Docker-installasjonsveiledning for Prowlarr
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Prowlarr-teamet tilbyr ikke en offisiell Docker-bilde. Imidlertid har flere tredjeparter opprettet og vedlikeholder sine egne.

> For en mer detaljert forklaring av Docker og anbefalte praksiser, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikkelen.
{.is-info}

Synology-brukere kan se [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **Portainer bør unngås for å sette opp Docker-containere** {.is-danger}

- Portainer gir et pent GUI for å administrere containere, men det er alt det er nyttig for.
- Portainer bør kun brukes for å vise Docker-containerlogger / containerstatus.
- Det anbefales sterkt å bruke Docker Compose og ikke bruke Portainer.
- Portainer har mange problemer, som for eksempel:
  - Feil rekkefølge av kilde og mål for monteringer
  - Inkonsistent skiftfølsomhet
  - Ingen automatisk opprettede egendefinerte nettverk for inter-container kommunikasjon
  - Inkonsistente komposisjonsimplementeringer på forskjellige arkitekturer
  - Henter hver tagg ved oppdatering når du ikke angir en spesifikk tagg
  - Funksjoner er skjulte og noen fungerer ikke i det hele tatt på ARM-plattformer

Se denne [Docker-guiden](/docker-guide) og [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) i stedet for hvordan du setter opp Docker Compose.

## Installer Prowlarr

For å installere og bruke disse Docker-bildene, må du huske på det ovennevnte mens du følger dokumentasjonen deres. Det er mange måter å administrere Docker-bilder og containere på, så installasjon og vedlikehold av dem vil avhenge av ruten du velger.

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}