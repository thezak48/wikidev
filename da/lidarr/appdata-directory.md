---
title: Lidarr Appdata-mappe
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> Herunder er standardstierne til programdata-mappen {.is-info}

> Alle forekomster af `$USER` er pladsholdere for brugeren, som programmet kører under. {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

Medmindre andet er angivet, gemmer Lidarr sin programdata i hjemmemappen for den bruger, som Lidarr kører under: `/home/$USER/.config/Lidarr` eller `~/.config/Lidarr`

Installationsinstruktionerne angiver `/var/lib/lidarr`

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

- Dette vil variere afhængigt af, hvor brugeren mapper `/config` til på deres værtsystem

# Argumenter

Argumentet `-data=` tvinger placeringen af AppData-mappen, så din startkommando kan tvinge en bestemt placering. Dette er påkrævet, når du forsøger at køre flere instanser. På Windows ville dette være `/data=`

Argumentet `-nobrowser` afholder fra at åbne browseren ved opstart. På Windows ville dette være `/nobrowser`