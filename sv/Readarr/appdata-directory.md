---
title: Readarr Appdata-katalog
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> Nedan finns standardvägarna för applikationsdatakatalogen {.is-info}

> Alla förekomster av `$USER` är platshållare för användaren som applikationen körs under. {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

Om inte annat anges kommer Readarr att lagra sin applikationsdata i hemmappen för användaren som Readarr körs under `/home/$USER/.config/Readarr` eller `~/.config/Readarr`

Installationsinstruktionerna specificerar `/var/lib/readarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Readarr` eller `~/.config/Readarr`

# Synology

`/usr/local/Readarr/var/.config/Readarr`

`/volume1/@appstore/Readarr/var/.config/Readarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Readarr`

`/share/CACHEDEV1_DATA/Readarr_CONFIG`

# Docker

`/config`

- Detta varierar beroende på var användaren mappar `/config` till på sitt värdsystem

# Argument

Argumentet `-data=` tvingar platsen för AppData-mappen, så din startkommando kan tvinga en specifik plats. Detta krävs när du försöker köra flera instanser. På Windows skulle detta vara `/data=`

Argumentet `-nobrowser` avstår från att starta/öppna webbläsaren vid start. På Windows skulle detta vara `/nobrowser`