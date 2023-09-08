---
title: Sonarr Docker-installatie
description: Docker-installatiehandleiding voor Sonarr
published: true
date: 2023-08-12T16:03:21.613Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:15.754Z
---

# Docker

Het Sonarr-team biedt geen officiële Docker-image aan. Er zijn echter verschillende derde partijen die hun eigen image hebben gemaakt en onderhouden.

Deze instructies bieden algemene begeleiding die van toepassing zou moeten zijn op elke Sonarr Docker-image.

Synology-gebruikers kunnen de [Synology Docker-handleiding van TRaSH](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) raadplegen.

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

Bekijk in plaats daarvan deze [Docker-handleiding](/docker-guide) en [TRaSH's Docker-zelfstudie](https://trash-guides.info/hardlinks/) voor het instellen van Docker Compose.

## Veelvoorkomende valkuilen vermijden

### Volumes en paden

Er zijn twee veelvoorkomende problemen met Docker-volumes: paden die verschillen tussen de Sonarr-container en de downloadclient-container, en paden die snelle verplaatsingen en harde koppelingen voorkomen.

Het eerste probleem ontstaat doordat de downloadclient het pad van een download rapporteert als `/torrents/My.Series.2018/`, maar in de Sonarr-container kan dat bijvoorbeeld `/downloads/My.Series.2018/` zijn. Het tweede probleem is een prestatieprobleem en veroorzaakt problemen bij het seeden van torrents. Beide problemen kunnen worden opgelost met goed geplande, consistente paden.

De meeste Docker-images suggereren paden zoals `/tv` en `/downloads`. Dit veroorzaakt langzame verplaatsingen en staat geen harde koppelingen toe omdat ze binnen de container als twee verschillende bestandssystemen worden beschouwd. Sommige raden ook paden aan voor de downloadclient-container die verschillen van de Sonarr-container, zoals `/torrents`.

De beste oplossing is om een enkel gemeenschappelijk volume binnen de containers te gebruiken, zoals `/data`. Je series zouden zich bevinden in `/data/Series`, torrents in `/data/downloads/torrents` en/of usenet-downloads in `/data/downloads/usenet`.

Als je deze aanbeveling niet opvolgt, moet je mogelijk een externe padtoewijzing configureren in de Sonarr-webinterface (Instellingen › Downloadclients).

### Eigenaarschap en machtigingen

Machtigingen en eigenaarschap van bestanden zijn een van de meest voorkomende problemen voor Sonarr-gebruikers, zowel binnen als buiten Docker. De meeste images hebben omgevingsvariabelen die kunnen worden gebruikt om de standaardgebruiker, groep en umask te overschrijven. Je moet dit beslissen voordat je al je containers instelt. De aanbeveling is om een gemeenschappelijke groep te gebruiken voor alle gerelateerde containers, zodat elke container de gedeelde groepsmachtigingen kan gebruiken om bestanden te lezen en schrijven op de gemonteerde volumes.
Houd er rekening mee dat Sonarr lees- en schrijftoegang nodig heeft tot de downloadmappen en de uiteindelijke mappen.

> Voor een meer gedetailleerde uitleg van deze problemen, zie het [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikel.
{.is-info}

## Sonarr installeren

Om deze Docker-images te installeren en te gebruiken, moet je rekening houden met het bovenstaande en de documentatie volgen. Er zijn veel manieren om Docker-images en -containers te beheren, dus de installatie en het onderhoud ervan hangen af van de route die je kiest.

- [hotio/sonarr](https://hotio.dev/containers/sonarr/)
- [lscr.io/linuxserver/sonarr](https://docs.linuxserver.io/images/docker-sonarr)
{.links-list}