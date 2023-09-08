---
title: Lidarr Docker Installation
description: Docker installationsguide för Lidarr
published: true
date: 2023-08-12T16:03:02.989Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:37.188Z
---

# Docker

Lidarr-teamet erbjuder inte en officiell Docker-bild. Men ett antal tredjepartsleverantörer har skapat och underhåller sina egna.

Dessa instruktioner ger generell vägledning som bör gälla för alla Lidarr Docker-bilder.

## Portainer

> **Portainer bör undvikas för att konfigurera Docker-containrar** {.is-danger}

- Portainer ger ett snyggt gränssnitt för att hantera containrar, men det är allt det är användbart för.
- Portainer bör endast användas för att visa Docker-containerloggar / containerstatus.
- Det rekommenderas starkt att använda Docker Compose och inte använda Portainer.
- Portainer har många problem, till exempel:
  - Felaktig ordning av källa och mål för monteringar
  - Inkonsekvent skiftlägeskänslighet
  - Inga automatiskt skapade anpassade nätverk för kommunikation mellan containrar
  - Inkonsekventa kompositionsimplementationer på olika arkitekturer
  - Hämtar varje tagg vid uppdatering om du inte anger en specifik tagg
  - Förmågor är dolda och vissa fungerar inte alls på ARM-plattformar

Se denna [Docker Guide](/docker-guide) och [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) istället för hur du konfigurerar Docker Compose.

## Undvik vanliga fallgropar

### Volymer och sökvägar

Det finns två vanliga problem med Docker-volymer: Sökvägar som skiljer sig mellan Lidarr- och nedladdningsklientcontainrar och sökvägar som förhindrar snabba flyttar och hårda länkar.

Det första är ett problem eftersom nedladdningsklienten kommer att rapportera en nedladdnings sökväg som `/torrents/My.Music.2018/`, men i Lidarr-containern kan den vara på `/downloads/My.Music.2018/`. Det andra är ett prestandaproblem och orsakar problem med att seeda torrents. Båda problemen kan lösas med välplanerade, konsekventa sökvägar.

De flesta Docker-bilder föreslår sökvägar som `/music` och `/downloads`. Detta orsakar långsamma flyttar och tillåter inte hårda länkar eftersom de anses vara två olika filsystem inne i containern. Vissa rekommenderar också sökvägar för nedladdningsklientcontainern som skiljer sig från Lidarr-containern, som /torrents.

Den bästa lösningen är att använda en enda gemensam volym inuti containrarna, som t.ex. /data. Din musik skulle vara i `/data/Music`, torrents i `/data/downloads/torrents` och/eller usenet-nedladdningar i `/data/downloads/usenet`.

Om detta råd inte följs kan du behöva konfigurera en fjärrsökvägsmappning i Lidarr-webbgränssnittet (Inställningar › Nedladdningsklienter).

### Ägande och behörigheter

Behörigheter och ägande av filer är ett av de vanligaste problemen för Lidarr-användare, både inuti och utanför Docker. De flesta bilder har miljövariabler som kan användas för att åsidosätta standardanvändaren, gruppen och umasken. Du bör bestämma detta innan du konfigurerar alla dina containrar. Rekommendationen är att använda en gemensam grupp för alla relaterade containrar så att varje container kan använda delade grupprättigheter för att läsa och skriva filer på de monterade volymerna.
Kom ihåg att Lidarr kommer att behöva läsa och skriva till nedladdningsmapparna samt de slutliga mapparna.

> För en mer detaljerad förklaring av dessa problem, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikeln.
{.is-info}

## Installera Lidarr

För att installera och använda dessa Docker-bilder måste du ha ovanstående i åtanke när du följer deras dokumentation. Det finns många sätt att hantera Docker-bilder och containrar på, så installation och underhåll av dem kommer att bero på den väg du väljer.

- [hotio/lidarr](https://hotio.dev/containers/lidarr/)
- [lscr.io/linuxserver/lidarr](https://docs.linuxserver.io/images/docker-lidarr)
{.links-list}