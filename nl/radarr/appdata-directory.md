---
title: Radarr Appdata Directory
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> Hieronder staan de standaard paden voor de toepassingsgegevensdirectory {.is-info}

> Alle voorkomens van `$USER` zijn aanduidingen voor de gebruiker waar de toepassing onder draait. {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

Tenzij anders gespecificeerd, slaat Radarr zijn toepassingsgegevens op in de home-map van de gebruiker waar Radarr onder draait `/home/$USER/.config/Radarr` of `~/.config/Radarr`

De installatie-instructies specificeren `/var/lib/radarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Radarr` of `~/.config/Radarr`

# Synology

`/usr/local/Radarr/var/.config/Radarr`

`/volume1/@appstore/Radarr/var/.config/Radarr'

'/volume1/@appdata/radarr/.config/Radarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Radarr`

`/share/CACHEDEV1_DATA/Radarr_CONFIG`

# Docker

`/config`

- Dit kan variëren op basis van waar de gebruiker `/config` toewijst op hun host-systeem

# Argumenten

Het `-data=` argument dwingt de locatie van de AppData-map af, dus uw opstartopdracht kan een specifieke locatie afdwingen. Dit is vereist bij het proberen meerdere instanties uit te voeren. Op Windows zou dit `/data=` zijn

Het `-nobrowser` argument voorkomt het starten/openen van de browser bij het opstarten. Op Windows zou dit `/nobrowser` zijn