---
title: Lidarr Appdata-katalog
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> Nedenfor er standardbanene for applikasjonsdatakatalogen {.is-info}

> Alle forekomster av `$USER` er plassholdere for brukeren som applikasjonen kjører under. {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

Med mindre annet er spesifisert, vil Lidarr lagre applikasjonsdataene i hjemmemappen til brukeren Lidarr kjører under `/home/$USER/.config/Lidarr` eller `~/.config/Lidarr`

Installasjonsinstruksjonene spesifiserer `/var/lib/lidarr`

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

- Dette vil variere avhengig av hvor brukeren mapper `/config` til på verts-systemet sitt

# Argumenter

Argumentet `-data=` tvinger plasseringen av AppData-mappen, så oppstartskommandoen din kan tvinge en bestemt plassering. Dette er nødvendig når du prøver å kjøre flere forekomster. På Windows vil dette være `/data=`

Argumentet `-nobrowser` avstår fra å starte/åpne nettleseren ved oppstart. På Windows vil dette være `/nobrowser`