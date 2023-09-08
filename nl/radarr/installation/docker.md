---
title: Radarr Docker Installatie
description: Docker installatiegids voor Radarr
published: true
date: 2023-08-12T16:02:10.602Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:47.674Z
---

# Docker

Het Radarr-team biedt geen officiële Docker-image aan. Er zijn echter verschillende derde partijen die hun eigen image hebben gemaakt en onderhouden.

Deze instructies bieden algemene begeleiding die van toepassing zou moeten zijn op elke Radarr Docker-image.

Synology-gebruikers kunnen [TRaSH's Synology Docker-gids](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) raadplegen.

## Portainer

> **Portainer moet worden vermeden voor het instellen van Docker-containers** {.is-danger}

- Portainer biedt een mooie GUI voor het beheren van containers, maar dat is ook het enige waar het nuttig voor is.
- Portainer moet alleen worden gebruikt voor het bekijken van docker-containerlogs / containerstatus.
- Het wordt sterk aanbevolen om Docker Compose te gebruiken en geen gebruik te maken van Portainer.
- Portainer heeft veel problemen, zoals:
  - Onjuiste volgorde van bron en doel van koppelingen
  - Inconsistentie in hoofdlettergevoeligheid
  - Geen automatisch aangemaakte aangepaste netwerken voor inter-container communicatie
  - Inconsistentie in compose-implementaties op verschillende architecturen
  - Haalt elke tag op bij een update wanneer je geen specifieke tag instelt
  - Mogelijkheden zijn verborgen en sommige werken helemaal niet op ARM-platforms

Raadpleeg in plaats daarvan deze [Docker-gids](/docker-guide) en [TRaSH's Docker-tutorial](https://trash-guides.info/hardlinks/) voor het instellen van Docker Compose.

## Veelvoorkomende valkuilen vermijden

### Volumes en paden

Er zijn twee veelvoorkomende problemen met Docker-volumes: paden die verschillen tussen de Radarr- en downloadclient-container en paden die snelle verplaatsingen en harde koppelingen voorkomen.

Het eerste probleem is een probleem omdat de downloadclient het pad van een download rapporteert als `/torrents/My.Movie.2018/`, maar in de Radarr-container kan dat bijvoorbeeld `/downloads/My.Movie.2018/` zijn. Het tweede probleem is een prestatieprobleem en veroorzaakt problemen bij het seeden van torrents. Beide problemen kunnen worden opgelost met goed geplande, consistente paden.

De meeste Docker-images suggereren paden zoals `/movies` en `/downloads`. Dit veroorzaakt langzame verplaatsingen en staat geen harde koppelingen toe omdat ze binnen de container als twee verschillende bestandssystemen worden beschouwd. Sommige raden ook paden aan voor de downloadclient-container die verschillen van de Radarr-container, zoals `/torrents`.

De beste oplossing is om een enkelvoudig, gemeenschappelijk volume binnen de containers te gebruiken, zoals `/data`. Je films zouden zich bevinden in `/data/Movies`, torrents in `/data/downloads/torrents` en/of usenet-downloads in `/data/downloads/usenet`.

Als je deze aanbeveling niet opvolgt, moet je mogelijk een externe padtoewijzing configureren in de Radarr-webinterface (Instellingen › Downloadclients).

### Eigenaarschap en machtigingen

Machtigingen en eigenaarschap van bestanden zijn een van de meest voorkomende problemen voor Radarr-gebruikers, zowel binnen als buiten Docker. De meeste images hebben omgevingsvariabelen die kunnen worden gebruikt om de standaardgebruiker, groep en umask te overschrijven. Je moet dit beslissen voordat je al je containers instelt. De aanbeveling is om een gemeenschappelijke groep te gebruiken voor alle gerelateerde containers, zodat elke container de gedeelde groepsmachtigingen kan gebruiken om bestanden te lezen en schrijven op de gemonteerde volumes.
Houd er rekening mee dat Radarr lees- en schrijftoegang nodig heeft tot de downloadmappen en de uiteindelijke mappen.

> Voor een meer gedetailleerde uitleg van deze problemen, zie het wiki-artikel [De beste Docker-setup en Docker-gids](/docker-guide).
{.is-info}

## Radarr installeren

Om deze Docker-images te installeren en te gebruiken, moet je rekening houden met het bovenstaande terwijl je hun documentatie volgt. Er zijn ook veel manieren om Docker-images en -containers te beheren, dus de installatie en het onderhoud ervan zijn afhankelijk van de route die je kiest.

- [hotio/radarr](https://hotio.dev/containers/radarr/)
- [lscr.io/linuxserver/radarr](https://docs.linuxserver.io/images/docker-radarr)
{.links-list}