---
title: Readarr Appdata-Verzeichnis
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> Im Folgenden sind die Standardpfade für das Anwendungsdatenverzeichnis aufgeführt {.is-info}

> Alle Instanzen von `$USER` sind Platzhalter für den Benutzer, unter dem die Anwendung ausgeführt wird. {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

Sofern nicht anders angegeben, speichert Readarr seine Anwendungsdaten im Home-Verzeichnis des Benutzers, unter dem Readarr ausgeführt wird: `/home/$USER/.config/Readarr` oder `~/.config/Readarr`

Die Installationsanweisungen geben `/var/lib/readarr` an.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Readarr` oder `~/.config/Readarr`

# Synology

`/usr/local/Readarr/var/.config/Readarr`

`/volume1/@appstore/Readarr/var/.config/Readarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Readarr`

`/share/CACHEDEV1_DATA/Readarr_CONFIG`

# Docker

`/config`

- Dies variiert je nachdem, wohin der Benutzer `/config` auf seinem Host-System abbildet.

# Argumente

Das `-data=`-Argument erzwingt den Speicherort des AppData-Ordners, sodass Ihr Startbefehl möglicherweise einen bestimmten Speicherort erzwingt. Dies ist erforderlich, wenn Sie mehrere Instanzen ausführen möchten. Unter Windows wäre dies `/data=`

Das `-nobrowser`-Argument verhindert das Starten/Öffnen des Browsers beim Start. Unter Windows wäre dies `/nobrowser`