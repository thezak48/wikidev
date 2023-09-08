---
title: Sonarr Appdata-katalog
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> Nedan finns standardvägarna för applikationsdatakatalogen {.is-info}

> Alla förekomster av `$USER` är platshållare för användaren som applikationen körs under. {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

Om inte annat anges kommer Sonarr att lagra sin applikationsdata i hemmappen för användaren som Sonarr körs under `/home/$USER/.config/Sonarr` eller `~/.config/Sonarr`

> För apt-repo-baserade installationer är standarden `/var/lib/Sonarr`
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` eller `~/.config/Sonarr`

# Synology

Om du använder SynoCommunity-paketet för Sonarr är det här du förväntas hitta dina appdata. Om du använder Docker på din Synology NAS, titta nedan i avsnittet om Docker.

## DSM 7 och senare

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6 och tidigare

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> SynoCommunity använder fortfarande det ursprungliga paketnamnet `nzbdrone` för det underliggande paketnamnet {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- Detta kommer att variera beroende på var användaren mappar `/config` till på sitt värdsystem

# Argument

Argumentet `-data=` tvingar platsen för AppData-mappen, så din startkommando kan tvinga en specifik plats. Detta krävs när du försöker köra flera instanser. På Windows skulle detta vara `/data=`

Argumentet `-nobrowser` avstår från att starta/öppna webbläsaren vid start. På Windows skulle detta vara `/nobrowser`