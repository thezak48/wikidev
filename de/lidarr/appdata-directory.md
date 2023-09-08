---
title: Lidarr Appdata-Verzeichnis
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> Im Folgenden sind die Standardpfade für das Anwendungsdatenverzeichnis aufgeführt {.is-info}

> Alle Instanzen von `$USER` sind Platzhalter für den Benutzer, unter dem die Anwendung ausgeführt wird. {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

Sofern nicht anders angegeben, speichert Lidarr seine Anwendungsdaten im Home-Verzeichnis des Benutzers, unter dem Lidarr ausgeführt wird: `/home/$USER/.config/Lidarr` oder `~/.config/Lidarr`

Die Installationsanweisungen geben `/var/lib/lidarr` an.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Lidarr` oder `~/.config/Lidarr`

# Synology

`/usr/local/Lidarr/var/.config/Lidarr`

`/volume1/@appstore/Lidarr/var/.config/Lidarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Lidarr`

`/share/CACHEDEV1_DATA/Lidarr_CONFIG`

# Docker

`/config`

- Dies variiert je nachdem, wohin der Benutzer `/config` auf seinem Host-System abbildet.

# Argumente

Das `-data=`-Argument erzwingt den Speicherort des AppData-Ordners, sodass Ihr Startbefehl einen bestimmten Speicherort erzwingen kann. Dies ist erforderlich, wenn Sie mehrere Instanzen ausführen möchten. Unter Windows wäre dies `/data=`

Das `-nobrowser`-Argument verhindert das Starten/Öffnen des Browsers beim Start. Unter Windows wäre dies `/nobrowser`