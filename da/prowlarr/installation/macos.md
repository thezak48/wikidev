---
title: Prowlarr MacOS Installation
description: MacOS installationsguide til Prowlarr
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> Prowlarr er ikke kompatibel med OSX-versioner under 10.15 (Catalina) på grund af .NET-inkompatibiliteter.
{.is-warning}

1. Download [MacOS-appen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhængigt af dit system.
1. Åbn arkivet og træk Prowlarr-ikonet til din Applications-mappe.
1. Selvsignér Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. Gå til <http://localhost:9696> for at begynde at bruge Prowlarr.