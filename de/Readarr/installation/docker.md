---
title: Readarr Docker Installation
description: Docker-Installationsanleitung für Readarr
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Das Readarr-Team bietet kein offizielles Docker-Image an. Es gibt jedoch verschiedene Drittanbieter, die ihre eigenen Images erstellt und pflegen.

Diese Anleitung bietet allgemeine Anweisungen, die auf jedes Readarr Docker-Image angewendet werden können.

## Portainer

> **Portainer sollte vermieden werden, um Docker-Container einzurichten** {.is-danger}

- Portainer bietet eine hübsche Benutzeroberfläche zur Verwaltung von Containern, ist aber nur dafür nützlich.
- Portainer sollte nur zum Anzeigen von Docker-Container-Logs und -Status verwendet werden.
- Es wird dringend empfohlen, Docker Compose zu verwenden und Portainer nicht zu verwenden.
- Portainer hat viele Probleme, wie z.B.:
  - Falsche Reihenfolge von Quelle und Ziel von Mounts
  - Inkonsistente Groß-/Kleinschreibung
  - Keine automatisch erstellten benutzerdefinierten Netzwerke für die Kommunikation zwischen Containern
  - Inkonsistente Compose-Implementierungen auf verschiedenen Architekturen
  - Lädt bei einem Update jeden Tag herunter, wenn kein bestimmter Tag festgelegt ist
  - Fähigkeiten sind versteckt und einige funktionieren auf ARM-Plattformen überhaupt nicht

Siehe diese [Docker-Anleitung](/docker-guide) und [TRaSH's Docker-Tutorial](https://trash-guides.info/hardlinks/) für die Einrichtung von Docker Compose.

## Häufige Probleme vermeiden

### Volumes und Pfade

Es gibt zwei häufige Probleme mit Docker-Volumes: Pfade, die sich zwischen dem Readarr- und dem Download-Client-Container unterscheiden, und Pfade, die schnelle Verschiebungen und Hardlinks verhindern.

Das erste Problem besteht darin, dass der Download-Client den Pfad eines Downloads als `/torrents/Mein.Film.2018/` angibt, aber im Readarr-Container könnte dieser Pfad `/downloads/Mein.Film.2018/` sein. Das zweite Problem ist eine Leistungsfrage und verursacht Probleme beim Seeden von Torrents. Beide Probleme können mit gut geplanten, konsistenten Pfaden gelöst werden.

Die meisten Docker-Images schlagen Pfade wie `/books` und `/downloads` vor. Dies führt zu langsamen Verschiebungen und erlaubt keine Hardlinks, da sie innerhalb des Containers als zwei verschiedene Dateisysteme betrachtet werden. Einige empfehlen auch Pfade für den Download-Client-Container, die sich vom Readarr-Container unterscheiden, z.B. /torrents.

Die beste Lösung besteht darin, ein einziges gemeinsames Volume innerhalb der Container zu verwenden, z.B. /data. Ihre Bücher würden sich in `/data/Bücher`, Torrents in `/data/downloads/torrents` und/oder Usenet-Downloads in `/data/downloads/usenet` befinden.

Wenn dieser Ratschlag nicht befolgt wird, müssen Sie möglicherweise eine Remote-Pfadzuordnung in der Readarr-Web-Oberfläche konfigurieren (Einstellungen › Download-Clients).

### Calibre-Integration

Bei der Erstellung eines Stammordners können Sie wählen, ob Sie die Calibre-Integration nutzen möchten oder nicht. Diese Wahl kann nur bei der Erstellung des Ordners getroffen werden, und wenn Sie sich gegen die Nutzung von Calibre entscheiden, können Sie es später nicht hinzufügen. Wenn Sie derzeit Calibre zur Verwaltung Ihrer Büchersammlung verwenden, sollten Sie diese Option wählen. Wenn Sie es verwenden, benennt und organisiert Calibre Ihre Buchdateien für Sie.

Wenn Sie Calibre verwenden, müssen Sie zuerst den Calibre Content Server starten (Einstellungen / Freigabe über das Netzwerk) und auch einen Benutzer und ein Passwort einrichten. Dies erfordert einen Neustart von Calibre.

> Bitte beachten Sie, dass Calibre Content Server und Calibre NICHT Calibre Web sind. Calibre Web ist ein separates Tool, das mit keinem dieser Programme in Verbindung steht und von Readarr in keiner Weise verwendet wird.
{.is-warning}

### Besitz und Berechtigungen

Berechtigungen und Besitz von Dateien sind eines der häufigsten Probleme für Readarr-Benutzer, sowohl innerhalb als auch außerhalb von Docker. Die meisten Images haben Umgebungsvariablen, die verwendet werden können, um den Standardbenutzer, die Standardgruppe und die Standardumask zu überschreiben. Sie sollten dies festlegen, bevor Sie alle Ihre Container einrichten. Die Empfehlung besteht darin, eine gemeinsame Gruppe für alle verwandten Container zu verwenden, damit jeder Container die gemeinsamen Gruppenberechtigungen zum Lesen und Schreiben von Dateien auf den eingebundenen Volumes verwenden kann.
Beachten Sie, dass Readarr Lese- und Schreibzugriff auf die Download-Ordner sowie auf die endgültigen Ordner benötigt.

> Für eine ausführlichere Erklärung dieser Probleme siehe den Wiki-Artikel [Die beste Docker-Installation und Docker-Anleitung](/docker-guide).
{.is-info}

## Readarr installieren

Um diese Docker-Images zu installieren und zu verwenden, müssen Sie die oben genannten Punkte beachten und die entsprechende Dokumentation befolgen. Es gibt viele Möglichkeiten, Docker-Images und -Container zu verwalten. Daher hängt die Installation und Wartung von der von Ihnen gewählten Methode ab.

> Vorübergehend müssen Sie die Tags :nightly oder :develop mit den Docker-Images verwenden, da es keinen Master-Zweig gibt. [Siehe diesen FAQ-Eintrag für die Bedeutung der Zweige](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}