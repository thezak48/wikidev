---
title: Radarr Appdata-mappe
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> Nedenfor er standardstiene for applikasjonsdata-mappen {.is-info}

> Alle forekomster av `$USER` er plassholdere for brukeren som applikasjonen kjører under. {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

Med mindre annet er spesifisert, vil Radarr lagre applikasjonsdataene i hjemmemappen til brukeren Radarr kjører under `/home/$USER/.config/Radarr` eller `~/.config/Radarr`

Installasjonsinstruksjonene spesifiserer `/var/lib/radarr`

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

- Dette vil variere avhengig av hvor brukeren mapper `/config` til på vertsoperativsystemet sitt

# Argumenter

Argumentet `-data=` tvinger plasseringen av AppData-mappen, så oppstartskommandoen din kan tvinge en bestemt plassering. Dette er nødvendig når du prøver å kjøre flere forekomster. På Windows vil dette være `/data=`

Argumentet `-nobrowser` avstår fra å åpne nettleseren ved oppstart. På Windows vil dette være `/nobrowser`