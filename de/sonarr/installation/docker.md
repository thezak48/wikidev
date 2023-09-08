---
title: Sonarr Docker Installation
description: Docker-Installationsanleitung für Sonarr
published: true
date: 2023-08-12T16:03:21.613Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:15.754Z
---

# Docker

Das Sonarr-Team bietet kein offizielles Docker-Image an. Es gibt jedoch eine Reihe von Drittanbietern, die ihre eigenen Images erstellt und gepflegt haben.

Diese Anleitung bietet allgemeine Anweisungen, die auf jedes Sonarr Docker-Image angewendet werden können.

Synology-Benutzer können [TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) ansehen.

## Portainer

> **Portainer sollte vermieden werden, um Docker-Container einzurichten** {.is-danger}

- Portainer bietet eine hübsche GUI zur Verwaltung von Containern, ist aber nur dafür nützlich.
- Portainer sollte nur zum Anzeigen von Docker-Container-Logs / Container-Status verwendet werden.
- Es wird dringend empfohlen, Docker Compose zu verwenden und nicht Portainer.
- Portainer hat viele Probleme, wie zum Beispiel:
  - Falsche Reihenfolge von Quelle und Ziel von Mounts
  - Inkonsistente Groß-/Kleinschreibung
  - Keine automatisch erstellten benutzerdefinierten Netzwerke für die Kommunikation zwischen Containern
  - Inkonsistente Compose-Implementierungen auf verschiedenen Architekturen
  - Lädt bei einem Update jeden Tag herunter, wenn kein bestimmter Tag festgelegt ist
  - Fähigkeiten sind verborgen und einige funktionieren überhaupt nicht auf ARM-Plattformen

Stattdessen sollten Sie sich diesen [Docker Guide](/docker-guide) und [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) ansehen, um Docker Compose einzurichten.

## Häufige Probleme vermeiden

### Volumes und Pfade

Es gibt zwei häufige Probleme mit Docker-Volumes: Pfade, die sich zwischen dem Sonarr- und dem Download-Client-Container unterscheiden, und Pfade, die schnelle Verschiebungen und Hardlinks verhindern.

Das erste Problem besteht darin, dass der Download-Client den Pfad eines Downloads als `/torrents/Meine.Serie.2018/` angibt, aber im Sonarr-Container könnte er unter `/downloads/Meine.Serie.2018/` liegen. Das zweite Problem ist eine Leistungsfrage und verursacht Probleme beim Seeden von Torrents. Beide Probleme können mit gut geplanten, konsistenten Pfaden gelöst werden.

Die meisten Docker-Images schlagen Pfade wie `/tv` und `/downloads` vor. Dies führt zu langsamen Verschiebungen und erlaubt keine Hardlinks, da sie innerhalb des Containers als zwei verschiedene Dateisysteme betrachtet werden. Einige empfehlen auch Pfade für den Download-Client-Container, die sich vom Sonarr-Container unterscheiden, z.B. /torrents.

Die beste Lösung besteht darin, ein einzelnes gemeinsames Volume innerhalb der Container zu verwenden, z.B. /data. Ihre Serien befinden sich in `/data/Serien`, Torrents in `/data/downloads/torrents` und/oder Usenet-Downloads in `/data/downloads/usenet`.

Wenn Sie diesen Ratschlag nicht befolgen, müssen Sie möglicherweise eine Remote-Pfadzuordnung in der Sonarr-Web-Oberfläche (Einstellungen › Download-Clients) konfigurieren.

### Besitz und Berechtigungen

Berechtigungen und Besitz von Dateien sind eines der häufigsten Probleme für Sonarr-Benutzer, sowohl innerhalb als auch außerhalb von Docker. Die meisten Images haben Umgebungsvariablen, die verwendet werden können, um den Standardbenutzer, die Standardgruppe und die Standardumask zu überschreiben. Sie sollten dies festlegen, bevor Sie alle Ihre Container einrichten. Die Empfehlung besteht darin, eine gemeinsame Gruppe für alle verwandten Container zu verwenden, damit jeder Container die gemeinsamen Gruppenberechtigungen zum Lesen und Schreiben von Dateien auf den eingebundenen Volumes verwenden kann.
Beachten Sie, dass Sonarr Lese- und Schreibzugriff auf die Download-Ordner sowie auf die endgültigen Ordner benötigt.

> Für eine ausführlichere Erklärung dieser Probleme siehe den Wiki-Artikel [The Best Docker Setup and Docker Guide](/docker-guide).
{.is-info}

## Sonarr installieren

Um diese Docker-Images zu installieren und zu verwenden, müssen Sie die oben genannten Punkte beachten und die entsprechende Dokumentation befolgen. Es gibt viele Möglichkeiten, Docker-Images und -Container zu verwalten. Daher hängt die Installation und Wartung von der von Ihnen gewählten Methode ab.

- [hotio/sonarr](https://hotio.dev/containers/sonarr/)
- [lscr.io/linuxserver/sonarr](https://docs.linuxserver.io/images/docker-sonarr)
{.links-list}