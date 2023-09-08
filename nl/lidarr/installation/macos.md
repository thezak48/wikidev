---
title: Lidarr MacOS-installatie
description: Installatiehandleiding voor Lidarr op MacOS
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> Lidarr is niet compatibel met OSX-versies < 10.15 (Catalina) vanwege .NET-incompatibiliteiten.
{.is-warning}

1. Download de [MacOS-app](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) of de [MacOS M1-app](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhankelijk van je systeem.
1. Open het archief en sleep het Lidarr-pictogram naar je map 'Toepassingen'.
1. Onderteken Lidarr zelf: `codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. Ga naar <http://localhost:8686> om Lidarr te gebruiken.