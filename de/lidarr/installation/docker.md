---
title: Lidarr Docker Installation
description: Docker-Installationsanleitung für Lidarr
published: true
date: 2023-08-12T16:03:02.989Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:37.188Z
---

# Docker

Das Lidarr-Team bietet kein offizielles Docker-Image an. Es gibt jedoch verschiedene Drittanbieter, die ihre eigenen Images erstellt und pflegen.

Diese Anleitung bietet allgemeine Anweisungen, die auf jedes Lidarr Docker-Image angewendet werden können.

## Portainer

> **Portainer sollte vermieden werden, um Docker-Container einzurichten** {.is-danger}

- Portainer bietet eine benutzerfreundliche grafische Benutzeroberfläche zur Verwaltung von Containern, ist aber nur dafür nützlich.
- Portainer sollte nur zum Anzeigen von Docker-Container-Logs / Container-Status verwendet werden.
- Es wird dringend empfohlen, Docker Compose zu verwenden und nicht Portainer.
- Portainer hat viele Probleme, wie zum Beispiel:
  - Falsche Reihenfolge von Quelle und Ziel von Mounts
  - Inkonsistente Groß-/Kleinschreibung
  - Keine automatisch erstellten benutzerdefinierten Netzwerke für die Kommunikation zwischen Containern
  - Inkonsistente Compose-Implementierungen auf verschiedenen Architekturen
  - Zieht bei Aktualisierung jede Tag-Version, wenn kein bestimmter Tag festgelegt ist
  - Fähigkeiten sind versteckt und einige funktionieren auf ARM-Plattformen überhaupt nicht

Siehe stattdessen diesen [Docker-Leitfaden](/docker-guide) und das [Docker-Tutorial von TRaSH](https://trash-guides.info/hardlinks/) zur Einrichtung von Docker Compose.

## Häufige Probleme vermeiden

### Volumes und Pfade

Es gibt zwei häufige Probleme mit Docker-Volumes: Pfade, die sich zwischen dem Lidarr- und dem Download-Client-Container unterscheiden, und Pfade, die schnelle Verschiebungen und Hardlinks verhindern.

Das erste Problem besteht darin, dass der Download-Client den Pfad eines Downloads als `/torrents/My.Music.2018/` angibt, aber in dem Lidarr-Container könnte er unter `/downloads/My.Music.2018/` liegen. Das zweite Problem ist eine Leistungsfrage und verursacht Probleme beim Seeden von Torrents. Beide Probleme können mit gut geplanten, konsistenten Pfaden gelöst werden.

Die meisten Docker-Images schlagen Pfade wie `/music` und `/downloads` vor. Dies führt zu langsamen Verschiebungen und erlaubt keine Hardlinks, da sie innerhalb des Containers als zwei verschiedene Dateisysteme betrachtet werden. Einige empfehlen auch Pfade für den Download-Client-Container, die sich vom Lidarr-Container unterscheiden, z.B. `/torrents`.

Die beste Lösung besteht darin, ein einziges gemeinsames Volume innerhalb der Container zu verwenden, z.B. `/data`. Ihre Musik würde sich in `/data/Music` befinden, Torrents in `/data/downloads/torrents` und/oder Usenet-Downloads in `/data/downloads/usenet`.

Wenn dieser Ratschlag nicht befolgt wird, müssen Sie möglicherweise eine Remote-Pfadzuordnung in der Lidarr-Web-Oberfläche konfigurieren (Einstellungen › Download-Clients).

### Besitz und Berechtigungen

Berechtigungen und Besitz von Dateien sind eines der häufigsten Probleme für Lidarr-Benutzer, sowohl innerhalb als auch außerhalb von Docker. Die meisten Images haben Umgebungsvariablen, die verwendet werden können, um den Standardbenutzer, die Standardgruppe und die Standard-umask zu überschreiben. Sie sollten dies festlegen, bevor Sie alle Ihre Container einrichten. Die Empfehlung besteht darin, eine gemeinsame Gruppe für alle verwandten Container zu verwenden, damit jeder Container die gemeinsamen Gruppenberechtigungen zum Lesen und Schreiben von Dateien auf den eingebundenen Volumes verwenden kann.
Beachten Sie, dass Lidarr Lese- und Schreibzugriff auf die Download-Ordner sowie auf die endgültigen Ordner benötigt.

> Für eine detailliertere Erklärung dieser Probleme siehe den Artikel [Die beste Docker-Konfiguration und Docker-Leitfaden](/docker-guide) im Wiki.
{.is-info}

## Lidarr installieren

Um diese Docker-Images zu installieren und zu verwenden, müssen Sie die oben genannten Punkte beachten und die entsprechende Dokumentation befolgen. Es gibt viele Möglichkeiten, Docker-Images und Container zu verwalten, daher hängt die Installation und Wartung von der von Ihnen gewählten Methode ab.

- [hotio/lidarr](https://hotio.dev/containers/lidarr/)
- [lscr.io/linuxserver/lidarr](https://docs.linuxserver.io/images/docker-lidarr)
{.links-list}