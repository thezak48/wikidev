---
title: Répertoire des données de l'application Sonarr
description: 
published: true
date: 2021-11-24T19:25:42.806Z
tags: 
editor: markdown
dateCreated: 2021-06-09T15:53:57.860Z
---

> Ci-dessous se trouvent les chemins par défaut pour le répertoire des données de l'application {.is-info}

> Toutes les occurrences de `$USER` sont des espaces réservés pour l'utilisateur sous lequel l'application s'exécute. {.is-warning}

# Windows

`C:\ProgramData\Sonarr`

# Linux

Sauf indication contraire, Sonarr stockera ses données d'application dans le dossier personnel de l'utilisateur sous lequel Sonarr s'exécute `/home/$USER/.config/Sonarr` ou `~/.config/Sonarr`

> Pour les installations basées sur le référentiel apt, le chemin par défaut est `/var/lib/Sonarr`
{.is-info}

# MacOS (OSX)

{#os-x}

`/Users/$USER/.config/Sonarr` ou `~/.config/Sonarr`

# Synology

Si vous utilisez le package SynoCommunity pour Sonarr, c'est là que vous devriez trouver vos données d'application. Si vous utilisez Docker sur votre NAS Synology, consultez la section Docker ci-dessous.

## DSM 7 et supérieur

`/volume1/@appdata/nzbdrone/.config/Sonarr`

## DSM 6 et inférieur

`/volume1/@appstore/nzbdrone/.config/Sonarr`

> SynoCommunity utilise toujours le nom de package d'origine `nzbdrone` pour le nom de package sous-jacent {.is-info}

# QNAP

`/share/MD0_DATA/homes/admin/.config/Sonarr`

`/share/CACHEDEV1_DATA/Sonarr_CONFIG`

# Docker

`/config`

- Cela variera en fonction de l'endroit où l'utilisateur mappe `/config` sur son système hôte

# Arguments

L'argument `-data=` force l'emplacement du dossier AppData, donc votre commande de démarrage peut forcer un emplacement spécifique. Cela est nécessaire lorsque vous essayez d'exécuter plusieurs instances. Sur Windows, cela serait `/data=`

L'argument `-nobrowser` empêche le lancement/ouverture du navigateur au démarrage. Sur Windows, cela serait `/nobrowser`