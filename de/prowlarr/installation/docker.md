---
title: Prowlarr Docker Installation
description: Docker-Installationsanleitung für Prowlarr
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Das Prowlarr-Team bietet kein offizielles Docker-Image an. Es gibt jedoch verschiedene Drittanbieter, die ihre eigenen Images erstellt und pflegen.

> Für eine detailliertere Erklärung von Docker und empfohlene Vorgehensweisen siehe den Wiki-Artikel [Die beste Docker-Setup und Docker-Anleitung](/docker-guide).
{.is-info}

Synology-Benutzer können die [Synology Docker-Anleitung von TRaSH](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) verwenden.

## Portainer

> **Portainer sollte vermieden werden, um Docker-Container einzurichten** {.is-danger}

- Portainer bietet eine benutzerfreundliche GUI zur Verwaltung von Containern, ist aber nur dafür nützlich.
- Portainer sollte nur zum Anzeigen von Docker-Container-Logs und -Status verwendet werden.
- Es wird dringend empfohlen, Docker Compose zu verwenden und nicht Portainer.
- Portainer hat viele Probleme, wie z.B.:
  - Falsche Reihenfolge von Quelle und Ziel bei Mounts
  - Inkonsistente Groß-/Kleinschreibung
  - Keine automatisch erstellten benutzerdefinierten Netzwerke für die Kommunikation zwischen Containern
  - Inkonsistente Implementierungen von Compose auf verschiedenen Architekturen
  - Lädt bei Aktualisierung alle Tags herunter, wenn kein bestimmter Tag festgelegt ist
  - Fähigkeiten sind versteckt und einige funktionieren auf ARM-Plattformen überhaupt nicht

Verwenden Sie stattdessen diese [Docker-Anleitung](/docker-guide) und das [Docker-Tutorial von TRaSH](https://trash-guides.info/hardlinks/), um Docker Compose einzurichten.

## Prowlarr installieren

Um diese Docker-Images zu installieren und zu verwenden, müssen Sie die oben genannten Hinweise beachten und der entsprechenden Dokumentation folgen. Es gibt viele Möglichkeiten, Docker-Images und -Container zu verwalten. Die Installation und Wartung hängen daher von der von Ihnen gewählten Methode ab.

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}