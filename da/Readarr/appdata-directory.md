---
title: Readarr Appdata Mappe
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> Herunder er standardstierne til programdata-mappen {.is-info}

> Alle forekomster af `$USER` er pladsholdere for brugeren, som programmet kører under. {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

Medmindre andet er angivet, gemmer Readarr sin programdata i hjemmemappen for den bruger, som Readarr kører under: `/home/$USER/.config/Readarr` eller `~/.config/Readarr`

Installationsinstruktionerne angiver `/var/lib/readarr`

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

- Dette vil variere afhængigt af, hvor brugeren mapper `/config` til på deres værtsystem

# Argumenter

Argumentet `-data=` tvinger placeringen af AppData-mappen, så din startkommando kan tvinge en bestemt placering. Dette er påkrævet, når du forsøger at køre flere forekomster. På Windows ville dette være `/data=`

Argumentet `-nobrowser` afholder fra at åbne browseren ved opstart. På Windows ville dette være `/nobrowser`