---
title: Readarr Docker Installation
description: Docker installationsguide för Readarr
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Readarr-teamet erbjuder inte en officiell Docker-bild. Dock har ett antal tredjepartsleverantörer skapat och underhåller sina egna bilder.

Dessa instruktioner ger generell vägledning som bör gälla för vilken Readarr Docker-bild som helst.

## Portainer

> **Portainer bör undvikas för att konfigurera Docker-behållare** {.is-danger}

- Portainer ger ett snyggt gränssnitt för att hantera behållare, men det är allt det är användbart för.
- Portainer bör endast användas för att visa Docker-behållarloggar / behållarstatus.
- Det rekommenderas starkt att använda Docker Compose och att inte använda Portainer.
- Portainer har många problem, såsom:
  - Felaktig ordning av källa och mål för monteringar
  - Inkonsekvent skiftlägeskänslighet
  - Ingen automatiskt skapad anpassad nätverk för kommunikation mellan behållare
  - Inkonsekventa kompositionsimplementationer på olika arkitekturer
  - Hämtar varje tagg vid uppdatering om du inte anger en specifik tagg
  - Förmågor är dolda och vissa fungerar inte alls på ARM-plattformar

Se denna [Docker Guide](/docker-guide) och [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) istället för hur man konfigurerar Docker Compose.

## Undvik vanliga fallgropar

### Volymer och sökvägar

Det finns två vanliga problem med Docker-volymer: Sökvägar som skiljer sig mellan Readarr- och nedladdningsklientbehållaren och sökvägar som förhindrar snabba flyttar och hårda länkar.

Det första problemet uppstår eftersom nedladdningsklienten rapporterar en nedladdnings sökväg som `/torrents/My.Movie.2018/`, men i Readarr-behållaren kan den vara `/downloads/My.Movie.2018/`. Det andra är en prestandafråga och orsakar problem för att seeda torrents. Båda problemen kan lösas med välplanerade, konsekventa sökvägar.

De flesta Docker-bilder föreslår sökvägar som `/books` och `/downloads`. Detta orsakar långsamma flyttar och tillåter inte hårda länkar eftersom de anses vara två olika filsystem inuti behållaren. Vissa rekommenderar också sökvägar för nedladdningsklientbehållaren som skiljer sig från Readarr-behållaren, som /torrents.

Den bästa lösningen är att använda en enda gemensam volym inuti behållarna, som t.ex. /data. Dina böcker skulle vara i `/data/Books`, torrents i `/data/downloads/torrents` och/eller usenet-nedladdningar i `/data/downloads/usenet`.

Om detta råd inte följs kan du behöva konfigurera en fjärrsökvägsmappning i Readarr-webbgränssnittet (Inställningar › Nedladdningsklienter).

### Calibre-integration

När du skapar en rotmapp kan du välja att använda Calibre-integration eller inte. Detta val kan bara göras vid mappskapande, och om du väljer att inte använda Calibre kan du inte lägga till det senare. Om du för närvarande använder Calibre för att hantera ditt bokbibliotek bör du välja detta alternativ. Om du använder det kommer Calibre att namnge och organisera dina bokfiler åt dig.

Om du kör Calibre måste du först starta Calibre Content Server (Inställningar / Delning över nätet) och också ställa in en användare och lösenord. Detta kräver en omstart av Calibre.

> Observera att Calibre Content Server och Calibre INTE är Calibre Web. Calibre Web är ett separat verktyg som inte har något att göra med någon av dessa program och som inte krävs eller används av Readarr på något sätt.
{.is-warning}

### Ägande och behörigheter

Behörigheter och ägande av filer är ett av de vanligaste problemen för Readarr-användare, både inom och utanför Docker. De flesta bilder har miljövariabler som kan användas för att åsidosätta standardanvändaren, gruppen och umasken. Du bör bestämma detta innan du konfigurerar alla dina behållare. Rekommendationen är att använda en gemensam grupp för alla relaterade behållare så att varje behållare kan använda delade grupprättigheter för att läsa och skriva filer på de monterade volymerna.
Kom ihåg att Readarr kommer att behöva läsa och skriva till nedladdningsmapparna samt de slutliga mapparna.

> För en mer detaljerad förklaring av dessa problem, se [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikeln.
{.is-info}

## Installera Readarr

För att installera och använda dessa Docker-bilder måste du ha ovanstående i åtanke när du följer deras dokumentation. Det finns många sätt att hantera Docker-bilder och behållare på, så installation och underhåll av dem kommer att bero på den väg du väljer.

> Tillfälligtvis måste du använda :nightly eller :develop taggarna med Docker-bilder, eftersom det inte finns någon huvudgren. [Se denna FAQ-post för betydelsen av grenarna](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}