---
title: Lidarr MacOS-installasjon
description: MacOS-installasjonsveiledning for Lidarr
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> Lidarr er ikke kompatibel med OSX-versjoner eldre enn 10.15 (Catalina) på grunn av .NET-inkompatibiliteter.
{.is-warning}

1. Last ned [MacOS-appen](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) avhengig av systemet ditt.
1. Åpne arkivet og dra Lidarr-ikonet til programmappen din.
1. Selvsigner Lidarr `codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. Gå til <http://localhost:8686> for å begynne å bruke Lidarr.