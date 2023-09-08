---
title: Répertoire Appdata de Readarr
description: 
published: true
date: 2021-11-24T19:24:45.782Z
tags: readarr, appdata
editor: markdown
dateCreated: 2021-06-09T15:54:32.028Z
---

> Ci-dessous se trouvent les chemins par défaut pour le répertoire des données d'application {.is-info}

> Toutes les occurrences de `$USER` sont des espaces réservés pour l'utilisateur sous lequel l'application s'exécute. {.is-warning}

# Windows

`C:\ProgramData\Readarr`

# Linux

Sauf indication contraire, Readarr stockera ses données d'application dans le dossier personnel de l'utilisateur sous lequel Readarr s'exécute `/home/$USER/.config/Readarr` ou `~/.config/Readarr`

Les instructions d'installation spécifient `/var/lib/readarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Readarr` ou `~/.config/Readarr`

# Synology

`/usr/local/Readarr/var/.config/Readarr`

`/volume1/@appstore/Readarr/var/.config/Readarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Readarr`

`/share/CACHEDEV1_DATA/Readarr_CONFIG`

# Docker

`/config`

- Cela variera en fonction de l'endroit où l'utilisateur mappe `/config` sur son système hôte

# Arguments

L'argument `-data=` force l'emplacement du dossier AppData, donc votre commande de démarrage peut forcer un emplacement spécifique. Cela est nécessaire lorsque vous essayez d'exécuter plusieurs instances. Sur Windows, cela serait `/data=`

L'argument `-nobrowser` empêche le lancement/ouverture du navigateur au démarrage. Sur Windows, cela serait `/nobrowser`