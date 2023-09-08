---
title: Lidarr MacOS Installation
description: Installationsguide för Lidarr på MacOS
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> Lidarr är inte kompatibel med OSX-versioner < 10.15 (Catalina) på grund av .NET-inkompatibiliteter.
{.is-warning}

1. Ladda ner [MacOS-appen](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) beroende på ditt system.
1. Öppna arkivet och dra Lidarr-ikonen till din Applications-mapp.
1. Självsignera Lidarr: `codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. Surfa till <http://localhost:8686> för att börja använda Lidarr.