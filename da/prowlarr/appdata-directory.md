---
title: Prowlarr Appdata Mappe
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> Nedenfor er standardstierne for programdata-mappen {.is-info}

> Alle forekomster af `$USER` er pladsholdere for brugeren, som programmet kører under. {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

Medmindre andet er angivet, gemmer Prowlarr sin programdata i hjemmemappen for den bruger, som Prowlarr kører under `/home/$USER/.config/Prowlarr` eller `~/.config/Prowlarr`

Installationsinstruktionerne angiver `/var/lib/prowlarr`

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

- Dette vil variere afhængigt af, hvor brugeren mapper `/config` til på deres værtsystem

# Argumenter

Argumentet `-data=` tvinger placeringen af AppData-mappen, så din startkommando kan tvinge en bestemt placering. Dette er påkrævet, når du forsøger at køre flere instanser. På Windows ville dette være `/data=`

Argumentet `-nobrowser` afholder fra at åbne browseren ved opstart. På Windows ville dette være `/nobrowser`