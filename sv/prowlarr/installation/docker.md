---
title: Prowlarr Docker Installation
description: Docker installationsguide för Prowlarr
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Prowlarr-teamet erbjuder inte en officiell Docker-bild. Dock har ett antal tredjepartsleverantörer skapat och underhåller sina egna.

> För en mer detaljerad förklaring av Docker och rekommenderade metoder, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikeln.
{.is-info}

Synology-användare kan se [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **Portainer bör undvikas för att konfigurera Docker-containrar** {.is-danger}

- Portainer ger ett snyggt GUI för att hantera containrar, men det är allt det är användbart för.
- Portainer bör endast användas för att visa Docker-containerloggar / containerstatus.
- Det rekommenderas starkt att använda Docker Compose och inte använda Portainer.
- Portainer har många problem, såsom:
  - Felaktig ordning av källa och mål för monteringar
  - Inkonsekvent skiftlägeskänslighet
  - Inga automatiskt skapade anpassade nätverk för kommunikation mellan containrar
  - Inkonsekventa kompositionsimplementationer på olika arkitekturer
  - Hämtar varje tagg vid uppdatering när du inte anger en specifik tagg
  - Förmågor är dolda och vissa fungerar inte alls på ARM-plattformar

Se istället denna [Docker Guide](/docker-guide) och [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) för hur man konfigurerar Docker Compose.

## Installera Prowlarr

För att installera och använda dessa Docker-bilder måste du ha ovanstående i åtanke när du följer deras dokumentation. Det finns många sätt att hantera Docker-bilder och containrar på, så installation och underhåll av dem kommer att bero på den väg du väljer.

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}