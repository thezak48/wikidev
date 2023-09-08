---
title: Sonarr Appdata Directory
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> Hieronder staan de standaard paden voor de toepassingsgegevensdirectory {.is-info}

> Alle voorkomens van `$USER` zijn aanduidingen voor de gebruiker waar de toepassing onder wordt uitgevoerd. {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

Tenzij anders aangegeven, slaat Sonarr zijn toepassingsgegevens op in de thuismap van de gebruiker waar Sonarr onder wordt uitgevoerd `/home/$USER/.config/Sonarr` of `~/.config/Sonarr`

> Voor apt-repo-gebaseerde installaties is de standaardlocatie `/var/lib/Sonarr`
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` of `~/.config/Sonarr`

# Synology

Als u het SynoCommunity-pakket voor Sonarr gebruikt, is dit waar u uw app-gegevens kunt vinden. Als u Docker op uw Synology NAS gebruikt, kijk dan hieronder in het Docker-gedeelte.

## DSM 7 en hoger

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6 en lager

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> De SynoCommunity gebruikt nog steeds de oorspronkelijke pakketnaam `nzbdrone` voor de onderliggende pakketnaam {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- Dit kan variëren op basis van waar de gebruiker `/config` toewijst op hun host-systeem

# Argumenten

Het argument `-data=` dwingt de locatie van de AppData-map af, dus uw opstartopdracht kan een specifieke locatie afdwingen. Dit is vereist bij het proberen meerdere exemplaren uit te voeren. Op Windows zou dit `/data=` zijn

Het argument `-nobrowser` weerhoudt ervan de browser te starten/openen bij het opstarten. Op Windows zou dit `/nobrowser` zijn