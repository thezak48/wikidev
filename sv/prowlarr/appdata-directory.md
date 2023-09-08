---
title: Prowlarr Appdata-katalog
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> Nedan finns standardvägarna för applikationsdatakatalogen {.is-info}

> Alla förekomster av `$USER` är platshållare för användaren som applikationen körs under. {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

Om inget annat anges lagrar Prowlarr sin applikationsdata i hemmappen för användaren som Prowlarr körs under `/home/$USER/.config/Prowlarr` eller `~/.config/Prowlarr`

Installationsinstruktionerna specificerar `/var/lib/prowlarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Prowlarr` eller `~/.config/Prowlarr`

# Synology

`/usr/local/Prowlarr/var/.config/Prowlarr`

`/volume1/@appstore/Prowlarr/var/.config/Prowlarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Prowlarr`

`/share/CACHEDEV1_DATA/Prowlarr_CONFIG`

# Docker

`/config`

- Detta varierar beroende på var användaren mappar `/config` till på sitt värdsystem

# Argument

Argumentet `-data=` tvingar platsen för AppData-mappen, så din startkommando kan tvinga en specifik plats. Detta krävs när du försöker köra flera instanser. På Windows skulle detta vara `/data=`

Argumentet `-nobrowser` avstår från att starta/öppna webbläsaren vid start. På Windows skulle detta vara `/nobrowser`