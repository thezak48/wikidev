---
title: Prowlarr Appdata-Verzeichnis
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> Im Folgenden sind die Standardpfade für das Anwendungsdatenverzeichnis aufgeführt {.is-info}

> Alle Instanzen von `$USER` sind Platzhalter für den Benutzer, unter dem die Anwendung ausgeführt wird. {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

Sofern nicht anders angegeben, speichert Prowlarr seine Anwendungsdaten im Home-Verzeichnis des Benutzers, unter dem Prowlarr ausgeführt wird: `/home/$USER/.config/Prowlarr` oder `~/.config/Prowlarr`

Die Installationsanweisungen geben `/var/lib/prowlarr` an.

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Prowlarr` oder `~/.config/Prowlarr`

# Synology

`/usr/local/Prowlarr/var/.config/Prowlarr`

`/volume1/@appstore/Prowlarr/var/.config/Prowlarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Prowlarr`

`/share/CACHEDEV1_DATA/Prowlarr_CONFIG`

# Docker

`/config`

- Dies variiert je nachdem, wohin der Benutzer `/config` auf seinem Host-System abbildet.

# Argumente

Das `-data=`-Argument erzwingt den Speicherort des AppData-Ordners, sodass Ihr Startbefehl einen bestimmten Speicherort erzwingen kann. Dies ist erforderlich, wenn Sie mehrere Instanzen ausführen möchten. Unter Windows wäre dies `/data=`

Das `-nobrowser`-Argument unterlässt das Starten/Öffnen des Browsers beim Start. Unter Windows wäre dies `/nobrowser`