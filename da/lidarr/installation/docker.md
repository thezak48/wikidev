---
title: Lidarr Docker Installation
description: Docker installationsguide til Lidarr
published: true
date: 2023-08-12T16:03:02.989Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:37.188Z
---

# Docker

Lidarr-teamet tilbyder ikke et officielt Docker-billede. Dog har en række tredjeparter oprettet og vedligeholder deres egne.

Disse instruktioner giver generel vejledning, der bør gælde for ethvert Lidarr Docker-billede.

## Portainer

> **Portainer bør undgås til opsætning af Docker-containere** {.is-danger}

- Portainer giver et pænt GUI til styring af containere, men det er alt, det er nyttigt til.
- Portainer bør kun bruges til visning af Docker-containerlogs / containerstatus.
- Det anbefales stærkt at bruge Docker Compose og ikke bruge Portainer.
- Portainer har mange problemer, såsom:
  - Forkert rækkefølge af kilde og mål for monteringer
  - Inkonsistent forskel på store og små bogstaver
  - Ingen automatisk oprettelse af brugerdefinerede netværk til inter-container-kommunikation
  - Inkonsistente implementeringer af Docker Compose på forskellige arkitekturer
  - Henter hver tag ved opdatering, når du ikke angiver en specifik tag
  - Visse evner er skjulte og fungerer slet ikke på ARM-platforme

Se denne [Docker-guide](/docker-guide) og [TRaSH's Docker-tutorial](https://trash-guides.info/hardlinks/) i stedet for at få vejledning om, hvordan du opsætter Docker Compose.

## Undgå almindelige faldgruber

### Volumener og stier

Der er to almindelige problemer med Docker-volumener: Stier, der er forskellige mellem Lidarr- og downloadklientcontaineren, og stier, der forhindrer hurtige flytninger og hardlinks.

Det første problem opstår, fordi downloadklienten vil rapportere en downloads sti som `/torrents/My.Music.2018/`, men i Lidarr-containeren kan det være `/downloads/My.Music.2018/`. Det andet problem er en ydelsesproblem og forårsager problemer med at seede torrents. Begge problemer kan løses med velplanlagte, ensartede stier.

De fleste Docker-billeder foreslår stier som `/music` og `/downloads`. Dette medfører langsomme flytninger og tillader ikke hardlinks, fordi de betragtes som to forskellige filsystemer inde i containeren. Nogle anbefaler også stier til downloadklientcontaineren, der er forskellige fra Lidarr-containeren, f.eks. /torrents.

Den bedste løsning er at bruge et enkelt, fælles volumen inde i containerne, f.eks. /data. Din musik vil være i `/data/Music`, torrents i `/data/downloads/torrents` og/eller usenet-downloads i `/data/downloads/usenet`.

Hvis dette råd ikke følges, kan du blive nødt til at konfigurere en fjernsti-afbildning i Lidarr-webgrænsefladen (Indstillinger › Downloadklienter).

### Ejerskab og tilladelser

Tilladelser og ejerskab af filer er et af de mest almindelige problemer for Lidarr-brugere, både inde og uden for Docker. De fleste billeder har miljøvariabler, der kan bruges til at overskrive standardbrugeren, gruppen og umasken. Du bør beslutte dette, inden du opsætter alle dine containere. Anbefalingen er at bruge en fælles gruppe for alle relaterede containere, så hver container kan bruge de delte gruppetilladelser til at læse og skrive filer på de monterede volumener.
Husk, at Lidarr skal have læse- og skrivetilladelser til downloadmapperne samt de endelige mapper.

> For en mere detaljeret forklaring af disse problemer, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artiklen.
{.is-info}

## Installér Lidarr

For at installere og bruge disse Docker-billeder skal du huske ovenstående, mens du følger deres dokumentation. Der er mange måder at administrere Docker-billeder og containere på, så installation og vedligeholdelse af dem afhænger af den rute, du vælger.

- [hotio/lidarr](https://hotio.dev/containers/lidarr/)
- [lscr.io/linuxserver/lidarr](https://docs.linuxserver.io/images/docker-lidarr)
{.links-list}