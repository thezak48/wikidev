---
title: Readarr Docker Installation
description: Docker installationsguide til Readarr
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Readarr-teamet tilbyder ikke et officielt Docker-billede. Dog har en række tredjeparter oprettet og vedligeholder deres egne.

Disse instruktioner giver generel vejledning, der bør gælde for ethvert Readarr Docker-billede.

## Portainer

> **Portainer bør undgås til opsætning af Docker-containere** {.is-danger}

- Portainer giver et pænt GUI til styring af containere, men det er alt, det er nyttigt til.
- Portainer bør kun bruges til visning af Docker-containerlogs / containerstatus.
- Det anbefales stærkt at bruge Docker Compose og ikke bruge Portainer.
- Portainer har mange problemer, såsom:
  - Forkert rækkefølge af kilde og mål for monteringer
  - Inkonsistent forskel på store og små bogstaver
  - Ingen automatisk oprettelse af brugerdefinerede netværk til inter-container-kommunikation
  - Inkonsistente compose-implementeringer på forskellige arkitekturer
  - Henter hver tag ved opdatering, når du ikke angiver et specifikt tag
  - Funktioner er skjulte, og nogle fungerer slet ikke på ARM-platforme

Se denne [Docker-guide](/docker-guide) og [TRaSH's Docker-tutorial](https://trash-guides.info/hardlinks/) i stedet for at lære, hvordan man opsætter Docker Compose.

## Undgå almindelige faldgruber

### Volumener og stier

Der er to almindelige problemer med Docker-volumener: Stier, der er forskellige mellem Readarr- og downloadklientcontaineren, og stier, der forhindrer hurtige flytninger og hardlinks.

Det første problem opstår, fordi downloadklienten vil rapportere en downloads sti som `/torrents/My.Movie.2018/`, men i Readarr-containeren kan det være `/downloads/My.Movie.2018/`. Det andet er et ydelsesproblem og forårsager problemer med at seede torrents. Begge problemer kan løses med velplanlagte, ensartede stier.

De fleste Docker-billeder foreslår stier som `/books` og `/downloads`. Dette medfører langsomme flytninger og tillader ikke hardlinks, fordi de betragtes som to forskellige filsystemer inde i containeren. Nogle anbefaler også stier til downloadklientcontaineren, der er forskellige fra Readarr-containeren, f.eks. /torrents.

Den bedste løsning er at bruge et enkelt, fælles volumen inde i containerne, f.eks. /data. Dine bøger vil være i `/data/Books`, torrents i `/data/downloads/torrents` og/eller usenet-downloads i `/data/downloads/usenet`.

Hvis dette råd ikke følges, kan du blive nødt til at konfigurere en fjernsti-afbildning i Readarr-webgrænsefladen (Indstillinger › Downloadklienter).

### Calibre-integration

Når du opretter en rodmappe, kan du vælge at bruge Calibre-integration eller ej. Denne mulighed kan kun vælges under oprettelse af mappen, og hvis du vælger ikke at bruge Calibre, kan du ikke tilføje det senere. Hvis du i øjeblikket bruger Calibre til at administrere dit bogbibliotek, bør du vælge denne mulighed. Hvis du bruger det, vil Calibre navngive og organisere dine bogfiler for dig.

Hvis du kører Calibre, skal du først starte Calibre Content Server (Indstillinger / Deling over netværket) og også oprette en bruger og adgangskode. Dette kræver en genstart af Calibre.

> Bemærk venligst, at Calibre Content Server og Calibre IKKE er Calibre Web. Calibre Web er et separat værktøj, der ikke har noget at gøre med nogen af disse programmer og ikke er nødvendigt eller bruges af Readarr på nogen måde.
{.is-warning}

### Ejerskab og tilladelser

Tilladelser og ejerskab af filer er et af de mest almindelige problemer for Readarr-brugere, både inde og uden for Docker. De fleste billeder har miljøvariabler, der kan bruges til at overskrive standardbrugeren, gruppen og umasken. Du bør beslutte dette, inden du opsætter alle dine containere. Anbefalingen er at bruge en fælles gruppe for alle relaterede containere, så hver container kan bruge de delte gruppetilladelser til at læse og skrive filer på de monterede volumener.
Husk, at Readarr skal have læse- og skrivetilladelser til downloadmapperne samt de endelige mapper.

> For en mere detaljeret forklaring af disse problemer, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artiklen.
{.is-info}

## Installér Readarr

For at installere og bruge disse Docker-billeder skal du huske ovenstående, mens du følger deres dokumentation. Der er også mange måder at administrere Docker-billeder og containere på, så installation og vedligeholdelse af dem afhænger af den rute, du vælger.

> Midlertidigt skal du bruge :nightly eller :develop-tags med Docker-billeder, da der ikke er nogen master-gren. [Se dette FAQ-indlæg for betydningen af grenene](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}