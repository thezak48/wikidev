---
title: Radarr Appdata-katalog
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> Nedan finns standardvägarna för applikationsdatakatalogen {.is-info}

> Alla förekomster av `$USER` är platshållare för användaren som applikationen körs under. {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

Om inte annat anges kommer Radarr att lagra sin applikationsdata i hemmappen för användaren som Radarr körs under `/home/$USER/.config/Radarr` eller `~/.config/Radarr`

Installationsinstruktionerna specificerar `/var/lib/radarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Radarr` eller `~/.config/Radarr`

# Synology

`/usr/local/Radarr/var/.config/Radarr`

`/volume1/@appstore/Radarr/var/.config/Radarr'

'/volume1/@appdata/radarr/.config/Radarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Radarr`

`/share/CACHEDEV1_DATA/Radarr_CONFIG`

# Docker

`/config`

- Detta kommer att variera beroende på var användaren kartlägger `/config` på sitt värdsystem

# Argument

Argumentet `-data=` tvingar platsen för AppData-mappen, så din startkommando kan tvinga en specifik plats. Detta krävs när du försöker köra flera instanser. På Windows skulle detta vara `/data=`

Argumentet `-nobrowser` avstår från att starta/öppna webbläsaren vid start. På Windows skulle detta vara `/nobrowser`