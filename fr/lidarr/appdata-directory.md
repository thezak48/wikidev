---
title: Répertoire Appdata de Lidarr
description: 
published: true
date: 2021-11-24T19:22:06.078Z
tags: lidarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:53:13.142Z
---

> Ci-dessous se trouvent les chemins par défaut pour le répertoire des données d'application {.is-info}

> Toutes les instances de `$USER` sont des espaces réservés pour l'utilisateur sous lequel l'application s'exécute. {.is-warning}

# Windows

`C:\ProgramData\Lidarr`

# Linux

Sauf indication contraire, Lidarr stockera ses données d'application dans le dossier personnel de l'utilisateur sous lequel Lidarr s'exécute `/home/$USER/.config/Lidarr` ou `~/.config/Lidarr`

Les instructions d'installation spécifient `/var/lib/lidarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Lidarr` ou `~/.config/Lidarr`

# Synology

`/usr/local/Lidarr/var/.config/Lidarr`

`/volume1/@appstore/Lidarr/var/.config/Lidarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Lidarr`

`/share/CACHEDEV1_DATA/Lidarr_CONFIG`

# Docker

`/config`

- Cela variera en fonction de l'endroit où l'utilisateur mappe `/config` sur son système hôte

# Arguments

L'argument `-data=` force l'emplacement du dossier AppData, donc votre commande de démarrage peut forcer un emplacement spécifique. Cela est nécessaire lorsque vous essayez d'exécuter plusieurs instances. Sur Windows, cela serait `/data=`

L'argument `-nobrowser` empêche le lancement/ouverture du navigateur au démarrage. Sur Windows, cela serait `/nobrowser`