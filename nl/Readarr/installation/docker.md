---
title: Readarr Docker-installatie
description: Docker-installatiehandleiding voor Readarr
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Het Readarr-team biedt geen officiële Docker-image aan. Er zijn echter verschillende derde partijen die hun eigen Docker-images hebben gemaakt en onderhouden.

Deze instructies bieden algemene begeleiding die van toepassing zou moeten zijn op elke Readarr Docker-image.

## Portainer

> **Portainer moet worden vermeden voor het instellen van Docker-containers** {.is-danger}

- Portainer biedt een mooie GUI voor het beheren van containers, maar dat is ook het enige waar het nuttig voor is.
- Portainer moet alleen worden gebruikt voor het bekijken van Docker-containerlogs / containerstatus.
- Het wordt sterk aanbevolen om Docker Compose te gebruiken en geen gebruik te maken van Portainer.
- Portainer heeft veel problemen, zoals:
  - Onjuiste volgorde van bron en doel van koppelingen
  - Inconsistentie in hoofdlettergevoeligheid
  - Geen automatisch aangemaakte aangepaste netwerken voor inter-container communicatie
  - Inconsistentie in de implementatie van compose op verschillende architecturen
  - Haalt elke tag op bij een update wanneer je geen specifieke tag instelt
  - Mogelijkheden zijn verborgen en sommige werken helemaal niet op ARM-platforms

Bekijk in plaats daarvan deze [Docker-gids](/docker-guide) en [TRaSH's Docker-tutorial](https://trash-guides.info/hardlinks/) voor het instellen van Docker Compose.

## Veelvoorkomende valkuilen vermijden

### Volumes en paden

Er zijn twee veelvoorkomende problemen met Docker-volumes: paden die verschillen tussen de Readarr-container en de downloadclient-container, en paden die snelle verplaatsingen en harde koppelingen voorkomen.

Het eerste probleem ontstaat doordat de downloadclient het pad van een download rapporteert als `/torrents/My.Movie.2018/`, maar in de Readarr-container kan dat bijvoorbeeld `/downloads/My.Movie.2018/` zijn. Het tweede probleem is een prestatieprobleem en veroorzaakt problemen bij het seeden van torrents. Beide problemen kunnen worden opgelost met goed geplande, consistente paden.

De meeste Docker-images suggereren paden zoals `/books` en `/downloads`. Dit veroorzaakt langzame verplaatsingen en staat geen harde koppelingen toe omdat ze binnen de container als twee verschillende bestandssystemen worden beschouwd. Sommige raden ook paden aan voor de downloadclient-container die verschillen van de Readarr-container, zoals /torrents.

De beste oplossing is om een enkelvoudig, gemeenschappelijk volume te gebruiken binnen de containers, zoals /data. Je boeken zouden zich bevinden in `/data/Books`, torrents in `/data/downloads/torrents` en/of usenet-downloads in `/data/downloads/usenet`.

Als dit advies niet wordt opgevolgd, moet je mogelijk een externe padtoewijzing configureren in de Readarr-webinterface (Instellingen › Downloadclients).

### Calibre-integratie

Bij het maken van een hoofdmap kun je ervoor kiezen om al dan niet Calibre-integratie te gebruiken. Deze keuze kan alleen worden gemaakt tijdens het maken van de map en als je ervoor kiest om geen gebruik te maken van Calibre, kun je het later niet toevoegen. Als je momenteel Calibre gebruikt om je boekenbibliotheek te beheren, moet je deze optie kiezen. Als je het gebruikt, zal Calibre je boekbestanden voor je benoemen en organiseren.

Als je Calibre gebruikt, moet je eerst de Calibre Content Server starten (Voorkeuren / Delen via het netwerk) en ook een gebruikersnaam en wachtwoord instellen. Hiervoor is een herstart van Calibre vereist.

> Let op: Calibre Content Server en Calibre zijn NIET Calibre Web. Calibre Web is een aparte tool die niet gerelateerd is aan een van deze programma's en wordt niet vereist of gebruikt door Readarr op enige manier.
{.is-warning}

### Eigendom en machtigingen

Machtigingen en eigendom van bestanden zijn een van de meest voorkomende problemen voor Readarr-gebruikers, zowel binnen als buiten Docker. De meeste images hebben omgevingsvariabelen die kunnen worden gebruikt om de standaardgebruiker, groep en umask te overschrijven. Je moet dit beslissen voordat je al je containers instelt. De aanbeveling is om een gemeenschappelijke groep te gebruiken voor alle gerelateerde containers, zodat elke container de gedeelde groepsmachtigingen kan gebruiken om bestanden te lezen en schrijven op de gemounte volumes.
Houd er rekening mee dat Readarr lees- en schrijfrechten nodig heeft voor de downloadmappen en de uiteindelijke mappen.

> Voor een meer gedetailleerde uitleg van deze problemen, zie het [The Best Docker Setup and Docker Guide](/docker-guide) wiki-artikel.
{.is-info}

## Readarr installeren

Om deze Docker-images te installeren en te gebruiken, moet je rekening houden met het bovenstaande terwijl je hun documentatie volgt. Er zijn ook veel manieren om Docker-images en -containers te beheren, dus de installatie en het onderhoud ervan zijn afhankelijk van de route die je kiest.

> Tijdelijk moet je de :nightly- of :develop-tags gebruiken bij Docker-images, omdat er geen master-tak is. [Bekijk deze FAQ voor de betekenis van de takken](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}