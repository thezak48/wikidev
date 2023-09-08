---
title: Readarr Appdata-katalog
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> Nedenfor er standardbanene for applikasjonsdatakatalogen {.is-info}

> Alle forekomster av `$USER` er plassholdere for brukeren som applikasjonen kjører under. {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

Med mindre annet er spesifisert, vil Readarr lagre applikasjonsdataene i hjemmemappen til brukeren Readarr kjører under `/home/$USER/.config/Readarr` eller `~/.config/Readarr`

Installasjonsinstruksjonene spesifiserer `/var/lib/readarr`

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

- Dette vil variere avhengig av hvor brukeren mapper `/config` til på vertsoperativsystemet sitt

# Argumenter

Argumentet `-data=` tvinger plasseringen av AppData-mappen, så oppstartskommandoen din kan tvinge en bestemt plassering. Dette er nødvendig når du prøver å kjøre flere forekomster. På Windows vil dette være `/data=`

Argumentet `-nobrowser` avstår fra å åpne nettleseren ved oppstart. På Windows vil dette være `/nobrowser`