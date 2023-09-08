---
title: Prowlarr Docker-installatie
description: Docker-installatiehandleiding voor Prowlarr
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Het Prowlarr-team biedt geen officiële Docker-image aan. Er zijn echter verschillende derde partijen die hun eigen image hebben gemaakt en onderhouden.

> Voor een gedetailleerde uitleg over Docker en aanbevolen werkwijzen, zie het wiki-artikel [De beste Docker-setup en Docker-gids](/docker-guide).
{.is-info}

Synology-gebruikers kunnen de [Synology Docker-gids van TRaSH](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) raadplegen.

## Portainer

> **Portainer moet worden vermeden voor het instellen van Docker-containers** {.is-danger}

- Portainer biedt een mooie GUI voor het beheren van containers, maar dat is ook alles waar het nuttig voor is.
- Portainer moet alleen worden gebruikt voor het bekijken van Docker-containerlogs of de status van containers.
- Het wordt sterk aanbevolen om Docker Compose te gebruiken en geen gebruik te maken van Portainer.
- Portainer heeft veel problemen, zoals:
  - Onjuiste volgorde van bron en doel van koppelingen
  - Inconsistentie in hoofdlettergevoeligheid
  - Geen automatisch aangemaakte aangepaste netwerken voor inter-container communicatie
  - Inconsistentie in Compose-implementaties op verschillende architecturen
  - Haalt elke tag op bij een update wanneer je geen specifieke tag instelt
  - Mogelijkheden zijn verborgen en sommige werken helemaal niet op ARM-platforms

Bekijk in plaats daarvan deze [Docker-gids](/docker-guide) en [TRaSH's Docker-zelfstudie](https://trash-guides.info/hardlinks/) voor het instellen van Docker Compose.

## Prowlarr installeren

Om deze Docker-images te installeren en te gebruiken, moet je rekening houden met het bovenstaande en de documentatie van de images volgen. Er zijn ook veel manieren om Docker-images en -containers te beheren, dus de installatie en het onderhoud ervan zijn afhankelijk van de route die je kiest.

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}