---
title: Répertoire des données d'application Radarr
description: 
published: true
date: 2023-05-09T17:51:34.896Z
tags: radarr, appdata
editor: markdown
dateCreated: 2021-05-25T02:34:50.549Z
---

> Ci-dessous se trouvent les chemins par défaut pour le répertoire des données d'application {.is-info}

> Toutes les instances de `$USER` sont des espaces réservés pour l'utilisateur sous lequel l'application s'exécute. {.is-warning}

# Windows

`C:\ProgramData\Radarr`

# Linux

Sauf indication contraire, Radarr stockera ses données d'application dans le dossier personnel de l'utilisateur sous lequel Radarr s'exécute `/home/$USER/.config/Radarr` ou `~/.config/Radarr`

Les instructions d'installation spécifient `/var/lib/radarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Radarr` ou `~/.config/Radarr`

# Synology

`/usr/local/Radarr/var/.config/Radarr`

`/volume1/@appstore/Radarr/var/.config/Radarr'

'/volume1/@appdata/radarr/.config/Radarr'

# QNAP

`/share/MD0_DATA/homes/admin/.config/Radarr`

`/share/CACHEDEV1_DATA/Radarr_CONFIG`

# Docker

`/config`

- Cela variera en fonction de l'endroit où l'utilisateur mappe `/config` sur son système hôte

# Arguments

L'argument `-data=` force l'emplacement du dossier AppData, donc votre commande de démarrage peut forcer un emplacement spécifique. Cela est nécessaire lorsque vous essayez d'exécuter plusieurs instances. Sur Windows, cela serait `/data=`

L'argument `-nobrowser` empêche le lancement/ouverture du navigateur au démarrage. Sur Windows, cela serait `/nobrowser`