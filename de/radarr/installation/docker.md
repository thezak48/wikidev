---
title: Radarr Docker Installation
description: Docker-Installationsanleitung für Radarr
published: true
date: 2023-08-12T16:02:10.602Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:47.674Z
---

# Docker

Das Radarr-Team bietet kein offizielles Docker-Image an. Es gibt jedoch eine Reihe von Drittanbietern, die ihre eigenen Images erstellt und gepflegt haben.

Diese Anleitung bietet allgemeine Anweisungen, die auf jedes Radarr Docker-Image angewendet werden können.

Synology-Benutzer können sich die [Synology Docker-Anleitung von TRaSH](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) ansehen.

## Portainer

> **Portainer sollte vermieden werden, um Docker-Container einzurichten** {.is-danger}

- Portainer bietet eine hübsche Benutzeroberfläche zum Verwalten von Containern, ist aber nur dafür nützlich.
- Portainer sollte nur zum Anzeigen von Docker-Container-Logs / Container-Status verwendet werden.
- Es wird dringend empfohlen, Docker Compose zu verwenden und Portainer nicht zu verwenden.
- Portainer hat viele Probleme, wie zum Beispiel:
  - Falsche Reihenfolge von Quelle und Ziel von Mounts
  - Inkonsistente Groß-/Kleinschreibung
  - Keine automatisch erstellten benutzerdefinierten Netzwerke für die Kommunikation zwischen Containern
  - Inkonsistente Compose-Implementierungen auf verschiedenen Architekturen
  - Zieht bei einem Update jede Tag-Version, wenn keine bestimmte Tag-Version festgelegt ist
  - Fähigkeiten sind verborgen und einige funktionieren überhaupt nicht auf ARM-Plattformen

Stattdessen sollten Sie sich diese [Docker-Anleitung](/docker-guide) und [TRaSH's Docker-Tutorial](https://trash-guides.info/hardlinks/) ansehen, um Docker Compose einzurichten.

## Häufige Probleme vermeiden

### Volumes und Pfade

Es gibt zwei häufige Probleme mit Docker-Volumes: Pfade, die sich zwischen dem Radarr- und dem Download-Client-Container unterscheiden, und Pfade, die schnelle Verschiebungen und Hardlinks verhindern.

Das erste Problem besteht darin, dass der Download-Client den Pfad eines Downloads als `/torrents/Mein.Film.2018/` angibt, aber im Radarr-Container könnte dieser Pfad `/downloads/Mein.Film.2018/` sein. Das zweite Problem ist eine Leistungsfrage und verursacht Probleme beim Seeden von Torrents. Beide Probleme können mit gut geplanten, konsistenten Pfaden gelöst werden.

Die meisten Docker-Images schlagen Pfade wie `/movies` und `/downloads` vor. Dies führt zu langsamen Verschiebungen und erlaubt keine Hardlinks, da sie innerhalb des Containers als zwei verschiedene Dateisysteme betrachtet werden. Einige empfehlen auch Pfade für den Download-Client-Container, die sich vom Radarr-Container unterscheiden, z.B. `/torrents`.

Die beste Lösung besteht darin, ein einzelnes gemeinsames Volume innerhalb der Container zu verwenden, z.B. `/data`. Ihre Filme würden sich in `/data/Movies`, Torrents in `/data/downloads/torrents` und/oder Usenet-Downloads in `/data/downloads/usenet` befinden.

Wenn dieser Ratschlag nicht befolgt wird, müssen Sie möglicherweise eine Remote-Pfadzuordnung in der Radarr-Web-Oberfläche konfigurieren (Einstellungen › Download-Clients).

### Besitz und Berechtigungen

Berechtigungen und Besitz von Dateien sind eines der häufigsten Probleme für Radarr-Benutzer, sowohl innerhalb als auch außerhalb von Docker. Die meisten Images haben Umgebungsvariablen, die verwendet werden können, um den Standardbenutzer, die Standardgruppe und die Standardumask zu überschreiben. Sie sollten dies festlegen, bevor Sie alle Ihre Container einrichten. Die Empfehlung besteht darin, eine gemeinsame Gruppe für alle verwandten Container zu verwenden, damit jeder Container die gemeinsamen Gruppenberechtigungen zum Lesen und Schreiben von Dateien auf den eingebundenen Volumes verwenden kann.
Beachten Sie, dass Radarr Lese- und Schreibzugriff auf die Download-Ordner sowie auf die endgültigen Ordner benötigt.

> Für eine detailliertere Erklärung dieser Probleme siehe den Wiki-Artikel [Die beste Docker-Setup und Docker-Anleitung](/docker-guide).
{.is-info}

## Radarr installieren

Um diese Docker-Images zu installieren und zu verwenden, müssen Sie die oben genannten Punkte beachten und die entsprechende Dokumentation befolgen. Es gibt viele Möglichkeiten, Docker-Images und -Container zu verwalten, daher hängt die Installation und Wartung von der von Ihnen gewählten Methode ab.

- [hotio/radarr](https://hotio.dev/containers/radarr/)
- [lscr.io/linuxserver/radarr](https://docs.linuxserver.io/images/docker-radarr)
{.links-list}