---
title: Sonarr Appdata-mappe
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> Nedenfor er standardstiene for applikasjonsdata-mappen {.is-info}

> Alle forekomster av `$USER` er plassholdere for brukeren som applikasjonen kjører under. {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

Med mindre annet er spesifisert, vil Sonarr lagre applikasjonsdataene i hjemmemappen til brukeren Sonarr kjører under `/home/$USER/.config/Sonarr` eller `~/.config/Sonarr`

> For apt-repo-baserte installasjoner er standarden `/var/lib/Sonarr`
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` eller `~/.config/Sonarr`

# Synology

Hvis du bruker SynoCommunity-pakken for Sonarr, er dette hvor du kan forvente å finne appdataene dine. Hvis du bruker Docker på Synology NAS-en din, se nedenfor i Docker-seksjonen.

## DSM 7 og nyere

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6 og eldre

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> SynoCommunity bruker fortsatt det opprinnelige pakkenavnet `nzbdrone` for underliggende pakkenavn {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- Dette vil variere avhengig av hvor brukeren mapper `/config` til på verts-systemet sitt

# Argumenter

Argumentet `-data=` tvinger plasseringen av AppData-mappen, så oppstartskommandoen din kan tvinge en bestemt plassering. Dette er nødvendig når du prøver å kjøre flere forekomster. På Windows vil dette være `/data=`

Argumentet `-nobrowser` avstår fra å åpne nettleseren ved oppstart. På Windows vil dette være `/nobrowser`