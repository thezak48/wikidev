---
title: Radarr MacOS Installation
description: MacOS installationsguide til Radarr
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> Radarr er ikke kompatibel med OSX-versioner < 10.15 (Catalina) på grund af .NET-inkompatibiliteter.
{.is-warning}

1. Download [MacOS-appen](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhængigt af dit system.
1. Åbn arkivet og træk Radarr-ikonet til din Applications-mappe.
1. Selvsignér Radarr med `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. Gå til <http://localhost:7878> for at begynde at bruge Radarr.

> Radarr bruger en medfølgende version af ffprobe til analyse af mediefiler og kræver ikke, at ffprobe eller ffmpeg er installeret på systemet. Hvis Radarr siger, at Ffprobe ikke findes, kan dette typisk løses med en geninstallation.
{.is-info}