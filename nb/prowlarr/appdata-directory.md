---
title: Prowlarr Appdata-katalog
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> Nedenfor er standardstiene for applikasjonsdatakatalogen {.is-info}

> Alle forekomster av `$USER` er plassholdere for brukeren som applikasjonen kjører under. {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

Med mindre annet er spesifisert, vil Prowlarr lagre applikasjonsdataene i hjemmemappen til brukeren Prowlarr kjører under `/home/$USER/.config/Prowlarr` eller `~/.config/Prowlarr`

Installasjonsinstruksjonene spesifiserer `/var/lib/prowlarr`

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

- Dette vil variere avhengig av hvor brukeren mapper `/config` til på verts-systemet sitt

# Argumenter

Argumentet `-data=` tvinger plasseringen av AppData-mappen, så oppstartskommandoen din kan tvinge en bestemt plassering. Dette er nødvendig når du prøver å kjøre flere forekomster. På Windows vil dette være `/data=`

Argumentet `-nobrowser` avstår fra å åpne nettleseren ved oppstart. På Windows vil dette være `/nobrowser`