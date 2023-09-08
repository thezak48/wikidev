---
title: Prowlarr Appdata Directory
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> Hieronder staan de standaard paden voor de toepassingsgegevensdirectory {.is-info}

> Alle voorkomens van `$USER` zijn aanduidingen voor de gebruiker waar de toepassing onder draait. {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

Tenzij anders aangegeven, slaat Prowlarr zijn toepassingsgegevens op in de thuismap van de gebruiker waar Prowlarr onder draait `/home/$USER/.config/Prowlarr` of `~/.config/Prowlarr`

De installatie-instructies geven `/var/lib/prowlarr` aan

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Prowlarr` of `~/.config/Prowlarr`

# Synology

`/usr/local/Prowlarr/var/.config/Prowlarr`

`/volume1/@appstore/Prowlarr/var/.config/Prowlarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Prowlarr`

`/share/CACHEDEV1_DATA/Prowlarr_CONFIG`

# Docker

`/config`

- Dit kan variëren op basis van waar de gebruiker `/config` toewijst op hun host-systeem

# Argumenten

Het argument `-data=` dwingt de locatie van de AppData-map af, dus uw opstartopdracht kan een specifieke locatie afdwingen. Dit is vereist bij het proberen meerdere exemplaren uit te voeren. Op Windows zou dit `/data=` zijn

Het argument `-nobrowser` voorkomt het starten/openen van de browser bij het opstarten. Op Windows zou dit `/nobrowser` zijn