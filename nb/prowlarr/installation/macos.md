---
title: Prowlarr MacOS-installasjon
description: MacOS-installasjonsveiledning for Prowlarr
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> Prowlarr er ikke kompatibel med OSX-versjoner eldre enn 10.15 (Catalina) på grunn av .NET-inkompatibiliteter.
{.is-warning}

1. Last ned [MacOS-appen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) avhengig av systemet ditt.
1. Åpne arkivet og dra Prowlarr-ikonet til programmappen din.
1. Selvsigner Prowlarr: `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. Gå til <http://localhost:9696> for å begynne å bruke Prowlarr.