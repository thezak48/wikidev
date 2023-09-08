---
title: Radarr Appdata-Verzeichnis
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> Im Folgenden sind die Standardpfade für das Anwendungsdatenverzeichnis aufgeführt {.is-info}

> Alle Instanzen von `$USER` sind Platzhalter für den Benutzer, unter dem die Anwendung ausgeführt wird. {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

Sofern nicht anders angegeben, speichert Radarr seine Anwendungsdaten im Home-Verzeichnis des Benutzers, unter dem Radarr ausgeführt wird: `/home/$USER/.config/Radarr` oder `~/.config/Radarr`

Die Installationsanweisungen geben `/var/lib/radarr` an.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Radarr` oder `~/.config/Radarr`

# Synology

`/usr/local/Radarr/var/.config/Radarr`

`/volume1/@appstore/Radarr/var/.config/Radarr'

'/volume1/@appdata/radarr/.config/Radarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Radarr`

`/share/CACHEDEV1_DATA/Radarr_CONFIG`

# Docker

`/config`

- Dies variiert je nachdem, wohin der Benutzer `/config` auf seinem Host-System abbildet.

# Argumente

Das `-data=`-Argument erzwingt den Speicherort des AppData-Ordners, sodass Ihr Startbefehl möglicherweise einen bestimmten Speicherort erzwingt. Dies ist erforderlich, wenn Sie mehrere Instanzen ausführen möchten. Unter Windows wäre dies `/data=`

Das `-nobrowser`-Argument verhindert das Starten/Öffnen des Browsers beim Start. Unter Windows wäre dies `/nobrowser`