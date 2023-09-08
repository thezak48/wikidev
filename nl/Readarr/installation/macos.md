---
title: Readarr MacOS-installatie
description: Installatiehandleiding voor Readarr op MacOS
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> Readarr is niet compatibel met OSX-versies < 10.15 (Catalina) vanwege .NET-incompatibiliteiten.
{.is-warning}

1. Download de [MacOS-app](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) of de [MacOS M1-app](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhankelijk van je systeem.
1. Open het archief en sleep het Readarr-pictogram naar je toepassingsmap.
1. Onderteken Readarr zelf met `codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. Ga naar <http://localhost:8787> om Readarr te gebruiken.