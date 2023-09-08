---
title: Sonarr Docker Installation
description: Docker installationsguide för Sonarr
published: true
date: 2023-08-12T16:03:21.613Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:15.754Z
---

# Docker

Sonarr-teamet erbjuder inte en officiell Docker-bild. Dock har ett antal tredjepartsleverantörer skapat och underhåller sina egna.

Dessa instruktioner ger generell vägledning som bör gälla för alla Sonarr Docker-bilder.

Synology-användare kan se [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **Portainer bör undvikas för att konfigurera Docker-containrar** {.is-danger}

- Portainer ger ett snyggt GUI för att hantera containrar, men det är allt det är användbart för.
- Portainer bör endast användas för att visa Docker-containerloggar / containerstatus.
- Det rekommenderas starkt att använda Docker compose och att inte använda Portainer.
- Portainer har många problem, såsom:
  - Felaktig ordning av källa och mål för monteringar
  - Inkonsekvent skiftlägeskänslighet
  - Inga automatiskt skapade anpassade nätverk för kommunikation mellan containrar
  - Inkonsekventa compose-implementeringar på olika arkitekturer
  - Hämtar varje tagg vid uppdatering om du inte anger en specifik tagg
  - Vissa behörigheter är dolda och vissa fungerar inte alls på ARM-plattformar

Se denna [Docker Guide](/docker-guide) och [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) istället för hur du konfigurerar Docker Compose.

## Undvik vanliga fallgropar

### Volymer och sökvägar

Det finns två vanliga problem med Docker-volymer: Sökvägar som skiljer sig mellan Sonarr- och nedladdningsklientcontainrar och sökvägar som förhindrar snabba flyttar och hårda länkar.

Det första problemet uppstår eftersom nedladdningsklienten rapporterar en nedladdnings sökväg som `/torrents/My.Series.2018/`, men i Sonarr-containern kan den vara `/downloads/My.Series.2018/`. Det andra är en prestandafråga och orsakar problem för att seeda torrents. Båda problemen kan lösas med välplanerade, konsekventa sökvägar.

De flesta Docker-bilder föreslår sökvägar som `/tv` och `/downloads`. Detta orsakar långsamma flyttar och tillåter inte hårda länkar eftersom de anses vara två olika filsystem inuti containern. Vissa rekommenderar också sökvägar för nedladdningsklientcontainern som skiljer sig från Sonarr-containern, som /torrents.

Den bästa lösningen är att använda en enda gemensam volym inuti containrarna, som t.ex. /data. Dina serier skulle vara i `/data/Series`, torrents i `/data/downloads/torrents` och/eller usenet-nedladdningar i `/data/downloads/usenet`.

Om detta råd inte följs kan du behöva konfigurera en fjärrsökvägsmappning i Sonarr-webbgränssnittet (Inställningar › Nedladdningsklienter).

### Ägande och behörigheter

Behörigheter och ägande av filer är ett av de vanligaste problemen för Sonarr-användare, både inuti och utanför Docker. De flesta bilder har miljövariabler som kan användas för att åsidosätta standardanvändaren, gruppen och umasken. Du bör bestämma detta innan du konfigurerar alla dina containrar. Rekommendationen är att använda en gemensam grupp för alla relaterade containrar så att varje container kan använda delade grupprättigheter för att läsa och skriva filer på monterade volymer.
Kom ihåg att Sonarr kommer att behöva läsa och skriva till nedladdningsmapparna samt de slutliga mapparna.

> För en mer detaljerad förklaring av dessa problem, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikeln.
{.is-info}

## Installera Sonarr

För att installera och använda dessa Docker-bilder måste du ha detta i åtanke när du följer deras dokumentation. Det finns många sätt att hantera Docker-bilder och containrar på, så installation och underhåll av dem kommer att bero på den väg du väljer.

- [hotio/sonarr](https://hotio.dev/containers/sonarr/)
- [lscr.io/linuxserver/sonarr](https://docs.linuxserver.io/images/docker-sonarr)
{.links-list}