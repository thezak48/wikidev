---
title: Radarr MacOS Installatie
description: Installatiehandleiding voor Radarr op MacOS
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> Radarr is niet compatibel met OSX-versies < 10.15 (Catalina) vanwege .NET-incompatibiliteiten.
{.is-warning}

1. Download de [MacOS App](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) of de [MacOS M1 App](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhankelijk van je systeem.
1. Open het archief en sleep het Radarr-pictogram naar je Toepassingen-map.
1. Onderteken Radarr zelf `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. Ga naar <http://localhost:7878> om Radarr te gebruiken.

> Radarr gebruikt een gebundelde versie van ffprobe voor het analyseren van mediabestanden en vereist geen installatie van ffprobe of ffmpeg op het systeem. Als Radarr aangeeft dat Ffprobe niet gevonden is, kan dit meestal worden opgelost door opnieuw te installeren.
{.is-info}