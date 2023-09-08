---
title: Radarr Appdata Mappe
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> Herunder er standardstierne til programdata-mappen {.is-info}

> Alle forekomster af `$USER` er pladsholdere for brugeren, som programmet kører under. {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

Medmindre andet er angivet, gemmer Radarr sin programdata i hjemmemappen for den bruger, som Radarr kører under: `/home/$USER/.config/Radarr` eller `~/.config/Radarr`

Installationsinstruktionerne angiver `/var/lib/radarr`

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

- Dette vil variere afhængigt af, hvor brugeren mapper `/config` til på deres værtsystem

# Argumenter

Argumentet `-data=` tvinger placeringen af AppData-mappen, så din startkommando kan tvinge en bestemt placering. Dette er påkrævet, når du forsøger at køre flere forekomster. På Windows ville dette være `/data=`

Argumentet `-nobrowser` afholder fra at åbne browseren ved opstart. På Windows ville dette være `/nobrowser`