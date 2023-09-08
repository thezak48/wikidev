---
title: Installation de Prowlarr sur MacOS
description: Guide d'installation de Prowlarr sur MacOS
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> Prowlarr n'est pas compatible avec les versions de OSX antérieures à 10.15 (Catalina) en raison d'incompatibilités avec .NET.
{.is-warning}

1. Téléchargez l'[application MacOS](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) ou l'[application MacOS M1](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) en fonction de votre système.
1. Ouvrez l'archive et faites glisser l'icône Prowlarr vers votre dossier Applications.
1. Auto-signez Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. Accédez à <http://localhost:9696> pour commencer à utiliser Prowlarr.