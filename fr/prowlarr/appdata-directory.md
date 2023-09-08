---
title: Répertoire des données d'application Prowlarr
description: 
published: true
date: 2021-11-24T19:22:49.484Z
tags: prowlarr, appdata
editor: markdown
dateCreated: 2021-06-08T01:06:44.136Z
---

> Ci-dessous se trouvent les chemins par défaut pour le répertoire des données d'application {.is-info}

> Toutes les instances de `$USER` sont des espaces réservés pour l'utilisateur sous lequel l'application s'exécute. {.is-warning}

# Windows

`C:\ProgramData\Prowlarr`

# Linux

Sauf indication contraire, Prowlarr stockera ses données d'application dans le dossier personnel de l'utilisateur sous lequel Prowlarr s'exécute `/home/$USER/.config/Prowlarr` ou `~/.config/Prowlarr`

Les instructions d'installation spécifient `/var/lib/prowlarr`

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Prowlarr` ou `~/.config/Prowlarr`

# Synology

`/usr/local/Prowlarr/var/.config/Prowlarr`

`/volume1/@appstore/Prowlarr/var/.config/Prowlarr`

# QNAP

`/share/MD0_DATA/homes/admin/.config/Prowlarr`

`/share/CACHEDEV1_DATA/Prowlarr_CONFIG`

# Docker

`/config`

- Cela variera en fonction de l'endroit où l'utilisateur mappe `/config` sur son système hôte

# Arguments

L'argument `-data=` force l'emplacement du dossier AppData, donc votre commande de démarrage peut forcer un emplacement spécifique. Cela est nécessaire lorsque vous essayez d'exécuter plusieurs instances. Sur Windows, cela serait `/data=`

L'argument `-nobrowser` empêche le lancement/ouverture du navigateur au démarrage. Sur Windows, cela serait `/nobrowser`