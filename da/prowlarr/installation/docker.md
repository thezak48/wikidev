---
title: Prowlarr Docker Installation
description: Docker installationsguide til Prowlarr
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Prowlarr-teamet tilbyder ikke en officiel Docker-afbildning. Dog har flere tredjeparter oprettet og vedligeholder deres egne.

> For en mere detaljeret forklaring af Docker og anbefalede praksisser, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artiklen.
{.is-info}

Synology-brugere kan se [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **Portainer bør undgås til opsætning af Docker-containere** {.is-danger}

- Portainer giver et pænt GUI til styring af containere, men det er det eneste, det er nyttigt til.
- Portainer bør kun bruges til visning af Docker-containerlogs / containerstatus.
- Det anbefales kraftigt at bruge Docker Compose og ikke bruge Portainer.
- Portainer har mange problemer, såsom:
  - Forkert rækkefølge af kilde og destination for monteringer
  - Inkonsistent forskel på store og små bogstaver
  - Ingen automatisk oprettelse af brugerdefinerede netværk til inter-container-kommunikation
  - Inkonsistente kompositionsimplementeringer på forskellige arkitekturer
  - Henter hver tag ved opdatering, når du ikke angiver en specifik tag
  - Evner er skjulte, og nogle fungerer slet ikke på ARM-platforme

Se i stedet denne [Docker Guide](/docker-guide) og [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) for at få vejledning i, hvordan du opsætter Docker Compose.

## Installér Prowlarr

For at installere og bruge disse Docker-afbildninger skal du huske ovenstående og følge deres dokumentation. Der er mange måder at administrere Docker-afbildninger og containere på, så installation og vedligeholdelse af dem afhænger af den rute, du vælger.

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}