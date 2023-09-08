---
title: Lidarr Appdata Directory
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> Hieronder staan de standaard paden voor de toepassingsgegevensdirectory {.is-info}

> Alle voorkomens van `$USER` zijn aanduidingen voor de gebruiker waar de toepassing onder wordt uitgevoerd. {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

Tenzij anders aangegeven, slaat Lidarr zijn toepassingsgegevens op in de thuismap van de gebruiker waar Lidarr onder wordt uitgevoerd: `/home/$USER/.config/Lidarr` of `~/.config/Lidarr`

De installatie-instructies geven `/var/lib/lidarr` aan

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Lidarr` of `~/.config/Lidarr`

# Synology

`/usr/local/Lidarr/var/.config/Lidarr`

`/volume1/@appstore/Lidarr/var/.config/Lidarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Lidarr`

`/share/CACHEDEV1_DATA/Lidarr_CONFIG`

# Docker

`/config`

- Dit kan variëren op basis van waar de gebruiker `/config` toewijst op hun host-systeem

# Argumenten

Het argument `-data=` dwingt de locatie van de AppData-map af, dus uw opstartopdracht kan een specifieke locatie afdwingen. Dit is vereist bij het proberen meerdere exemplaren uit te voeren. Op Windows zou dit `/data=` zijn

Het argument `-nobrowser` weerhoudt ervan de browser te starten/openen bij het opstarten. Op Windows zou dit `/nobrowser` zijn