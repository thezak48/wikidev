---
title: Lidarr Appdata-katalog
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> Nedan finns standardvägarna för applikationsdatakatalogen {.is-info}

> Alla förekomster av `$USER` är platshållare för användaren som applikationen körs under. {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

Om inte annat anges kommer Lidarr att lagra sin applikationsdata i hemmappen för användaren som Lidarr körs under `/home/$USER/.config/Lidarr` eller `~/.config/Lidarr`

Installationsinstruktionerna anger `/var/lib/lidarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Lidarr` eller `~/.config/Lidarr`

# Synology

`/usr/local/Lidarr/var/.config/Lidarr`

`/volume1/@appstore/Lidarr/var/.config/Lidarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Lidarr`

`/share/CACHEDEV1_DATA/Lidarr_CONFIG`

# Docker

`/config`

- Detta kommer att variera beroende på var användaren kartlägger `/config` på sitt värdsystem

# Argument

Argumentet `-data=` tvingar platsen för AppData-mappen, så din startkommando kan tvinga en specifik plats. Detta krävs när du försöker köra flera instanser. På Windows skulle detta vara `/data=`

Argumentet `-nobrowser` avstår från att starta/öppna webbläsaren vid start. På Windows skulle detta vara `/nobrowser`