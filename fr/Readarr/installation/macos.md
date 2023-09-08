---
title: Installation de Readarr sur MacOS
description: Guide d'installation de Readarr sur MacOS
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> Readarr n'est pas compatible avec les versions de OSX inférieures à 10.15 (Catalina) en raison d'incompatibilités avec .NET.
{.is-warning}

1. Téléchargez l'[application MacOS](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) ou l'[application MacOS M1](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) en fonction de votre système.
1. Ouvrez l'archive et faites glisser l'icône Readarr vers votre dossier Applications.
1. Auto-signez Readarr `codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. Accédez à <http://localhost:8787> pour commencer à utiliser Readarr