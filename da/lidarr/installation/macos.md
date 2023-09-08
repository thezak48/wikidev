---
title: Lidarr MacOS Installation
description: MacOS installationsguide til Lidarr
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> Lidarr er ikke kompatibel med OSX-versioner under 10.15 (Catalina) på grund af .NET-inkompatibiliteter.
{.is-warning}

1. Download [MacOS-appen](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhængigt af dit system.
1. Åbn arkivet og træk Lidarr-ikonet til din Applications-mappe.
1. Selvsignér Lidarr med følgende kommando: `codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. Gå til <http://localhost:8686> for at begynde at bruge Lidarr.