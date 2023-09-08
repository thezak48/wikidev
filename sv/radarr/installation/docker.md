---
title: Radarr Docker Installation
description: Docker installationsguide för Radarr
published: true
date: 2023-08-12T16:02:10.602Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:47.674Z
---

# Docker

Radarr-teamet erbjuder inte en officiell Docker-bild. Dock har ett antal tredjepartsleverantörer skapat och underhåller sina egna.

Dessa instruktioner ger generell vägledning som bör gälla för vilken Radarr Docker-bild som helst.

Synology-användare kan se [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **Portainer bör undvikas för att konfigurera Docker-containrar** {.is-danger}

- Portainer ger ett snyggt grafiskt gränssnitt för att hantera containrar, men det är allt det är användbart för.
- Portainer bör endast användas för att visa Docker-containerloggar / containerstatus.
- Det rekommenderas starkt att använda Docker Compose och inte använda Portainer.
- Portainer har många problem, såsom:
  - Felaktig ordning av källa och mål för monteringar
  - Inkonsekvent skiftlägeskänslighet
  - Inga automatiskt skapade anpassade nätverk för kommunikation mellan containrar
  - Inkonsekventa kompositionsimplementationer på olika arkitekturer
  - Hämtar varje tagg vid uppdatering om du inte anger en specifik tagg
  - Förmågor är dolda och vissa fungerar inte alls på ARM-plattformar

Se denna [Docker Guide](/docker-guide) och [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) istället för hur man konfigurerar Docker Compose.

## Undvik vanliga fallgropar

### Volymer och sökvägar

Det finns två vanliga problem med Docker-volymer: Sökvägar som skiljer sig mellan Radarr- och nedladdningsklientcontainrar och sökvägar som förhindrar snabba flyttar och hårda länkar.

Det första är ett problem eftersom nedladdningsklienten kommer att rapportera en nedladdnings sökväg som `/torrents/My.Movie.2018/`, men i Radarr-containern kan den vara på `/downloads/My.Movie.2018/`. Det andra är ett prestandaproblem och orsakar problem med att seeda torrents. Båda problemen kan lösas med välplanerade, konsekventa sökvägar.

De flesta Docker-bilder föreslår sökvägar som `/movies` och `/downloads`. Detta orsakar långsamma flyttar och tillåter inte hårda länkar eftersom de anses vara två olika filsystem inne i containern. Vissa rekommenderar också sökvägar för nedladdningsklientcontainern som skiljer sig från Radarr-containern, som /torrents.

Den bästa lösningen är att använda en enda gemensam volym inuti containrarna, som t.ex. /data. Dina filmer skulle vara i `/data/Movies`, torrents i `/data/downloads/torrents` och/eller usenet-nedladdningar i `/data/downloads/usenet`.

Om detta råd inte följs kan du behöva konfigurera en fjärrsökvägsmappning i Radarr-webbgränssnittet (Inställningar › Nedladdningsklienter).

### Ägande och behörigheter

Behörigheter och ägande av filer är ett av de vanligaste problemen för Radarr-användare, både inuti och utanför Docker. De flesta bilder har miljövariabler som kan användas för att åsidosätta standardanvändaren, gruppen och umasken. Du bör bestämma detta innan du konfigurerar alla dina containrar. Rekommendationen är att använda en gemensam grupp för alla relaterade containrar så att varje container kan använda delade grupprättigheter för att läsa och skriva filer på de monterade volymerna.
Kom ihåg att Radarr kommer att behöva läsa och skriva till nedladdningsmapparna samt de slutliga mapparna.

> För en mer detaljerad förklaring av dessa problem, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikeln.
{.is-info}

## Installera Radarr

För att installera och använda dessa Docker-bilder måste du ha ovanstående i åtanke när du följer deras dokumentation. Det finns många sätt att hantera Docker-bilder och containrar på, så installation och underhåll av dem kommer att bero på den väg du väljer.

- [hotio/radarr](https://hotio.dev/containers/radarr/)
- [lscr.io/linuxserver/radarr](https://docs.linuxserver.io/images/docker-radarr)
{.links-list}