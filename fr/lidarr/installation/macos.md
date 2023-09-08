---
title: Installation de Lidarr sur MacOS
description: Guide d'installation de Lidarr sur MacOS
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> Lidarr n'est pas compatible avec les versions de OSX inférieures à 10.15 (Catalina) en raison d'incompatibilités avec .NET.
{.is-warning}

1. Téléchargez l'[application MacOS](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) ou l'[application MacOS M1](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) en fonction de votre système.
1. Ouvrez l'archive et faites glisser l'icône Lidarr vers votre dossier Applications.
1. Auto-signez Lidarr `codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. Accédez à <http://localhost:8686> pour commencer à utiliser Lidarr.