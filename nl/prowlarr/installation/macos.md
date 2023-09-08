---
title: Prowlarr MacOS Installatie
description: Installatiehandleiding voor Prowlarr op MacOS
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> Prowlarr is niet compatibel met OSX-versies < 10.15 (Catalina) vanwege .NET-incompatibiliteiten.
{.is-warning}

1. Download de [MacOS-app](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) of de [MacOS M1-app](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhankelijk van je systeem.
1. Open het archief en sleep het Prowlarr-pictogram naar je map 'Toepassingen'.
1. Onderteken Prowlarr zelf: `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. Ga naar <http://localhost:9696> om Prowlarr te gebruiken.