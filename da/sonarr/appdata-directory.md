---
title: Sonarr Appdata Mappe
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> Herunder er standardstierne for programdata-mappen {.is-info}

> Alle forekomster af `$USER` er pladsholdere for brugeren, som programmet kører under. {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

Medmindre andet er angivet, gemmer Sonarr sin programdata i hjemmemappen for den bruger, som Sonarr kører under `/home/$USER/.config/Sonarr` eller `~/.config/Sonarr`

> For apt-repo-baserede installationer er standardstien `/var/lib/Sonarr`
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` eller `~/.config/Sonarr`

# Synology

Hvis du bruger SynoCommunity-pakken til Sonarr, er det her, du kan forvente at finde dine appdata. Hvis du bruger Docker på din Synology NAS, kan du se nedenfor i Docker-sektionen.

## DSM 7 og nyere

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6 og ældre

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> SynoCommunity bruger stadig det oprindelige pakkenavn `nzbdrone` som det underliggende pakkenavn {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- Dette vil variere afhængigt af, hvor brugeren mapper `/config` til på deres værtsystem

# Argumenter

Argumentet `-data=` tvinger placeringen af AppData-mappen, så din startkommando kan tvinge en bestemt placering. Dette er påkrævet, når du forsøger at køre flere forekomster. På Windows ville dette være `/data=`

Argumentet `-nobrowser` afholder fra at åbne browseren ved opstart. På Windows ville dette være `/nobrowser`