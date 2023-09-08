---
title: Readarr Appdata Directory
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> Hieronder staan de standaard paden voor de toepassingsgegevensdirectory {.is-info}

> Alle voorkomens van `$USER` zijn aanduidingen voor de gebruiker waar de toepassing onder wordt uitgevoerd. {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

Tenzij anders aangegeven, slaat Readarr zijn toepassingsgegevens op in de thuismap van de gebruiker waar Readarr onder wordt uitgevoerd: `/home/$USER/.config/Readarr` of `~/.config/Readarr`

De installatie-instructies geven `/var/lib/readarr` aan

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Readarr` of `~/.config/Readarr`

# Synology

`/usr/local/Readarr/var/.config/Readarr`

`/volume1/@appstore/Readarr/var/.config/Readarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Readarr`

`/share/CACHEDEV1_DATA/Readarr_CONFIG`

# Docker

`/config`

- Dit kan variëren op basis van waar de gebruiker `/config` toewijst op hun host-systeem

# Argumenten

Het argument `-data=` dwingt de locatie van de AppData-map af, dus uw opstartopdracht kan een specifieke locatie afdwingen. Dit is vereist bij het proberen meerdere exemplaren uit te voeren. Op Windows zou dit `/data=` zijn

Het argument `-nobrowser` weerhoudt de browser ervan om te starten/openen bij het opstarten. Op Windows zou dit `/nobrowser` zijn