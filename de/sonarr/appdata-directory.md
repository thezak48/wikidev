---
title: Sonarr Appdata-Verzeichnis
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> Unten sind die Standardpfade für das Anwendungsdatenverzeichnis {.is-info}

> Alle Instanzen von `$USER` sind Platzhalter für den Benutzer, unter dem die Anwendung ausgeführt wird. {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

Sofern nicht anders angegeben, speichert Sonarr seine Anwendungsdaten im Home-Verzeichnis des Benutzers, unter dem Sonarr ausgeführt wird: `/home/$USER/.config/Sonarr` oder `~/.config/Sonarr`

> Bei apt-Repository-basierten Installationen ist der Standardpfad `/var/lib/Sonarr`
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` oder `~/.config/Sonarr`

# Synology

Wenn Sie das SynoCommunity-Paket für Sonarr verwenden, sollten Sie hier Ihre App-Daten erwarten. Wenn Sie Docker auf Ihrem Synology NAS verwenden, schauen Sie unten im Docker-Abschnitt nach.

## DSM 7 und höher

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6 und niedriger

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> Die SynoCommunity verwendet immer noch den ursprünglichen Paketnamen `nzbdrone` für den zugrunde liegenden Paketnamen {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- Dies variiert je nachdem, wohin der Benutzer `/config` auf seinem Host-System abbildet

# Argumente

Das `-data=`-Argument erzwingt den Speicherort des AppData-Ordners, sodass Ihr Startbefehl einen bestimmten Speicherort erzwingen kann. Dies ist erforderlich, wenn Sie mehrere Instanzen ausführen möchten. Unter Windows wäre dies `/data=`

Das `-nobrowser`-Argument verhindert das Starten/Öffnen des Browsers beim Start. Unter Windows wäre dies `/nobrowser`