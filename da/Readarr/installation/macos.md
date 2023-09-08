---
title: Readarr MacOS Installation
description: MacOS installationsguide til Readarr
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> Readarr er ikke kompatibel med OSX-versioner < 10.15 (Catalina) på grund af .NET-inkompatibiliteter.
{.is-warning}

1. Download [MacOS-appen](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) afhængigt af dit system.
1. Åbn arkivet og træk Readarr-ikonet til din Applications-mappe.
1. Selvsignér Readarr med følgende kommando: `codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. Gå til <http://localhost:8787> for at begynde at bruge Readarr.