---
title: Radarr MacOS-installasjon
description: MacOS-installasjonsveiledning for Radarr
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> Radarr er ikke kompatibel med OSX-versjoner < 10.15 (Catalina) på grunn av .NET-inkompatibiliteter.
{.is-warning}

1. Last ned [MacOS App](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1 App](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) avhengig av systemet ditt.
1. Åpne arkivet og dra Radarr-ikonet til programmappen din.
1. Selvsigner Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. Gå til <http://localhost:7878> for å begynne å bruke Radarr.

> Radarr bruker en buntet versjon av ffprobe for analyse av mediefiler og krever ikke at ffprobe eller ffmpeg er installert på systemet. Hvis Radarr sier at Ffprobe ikke er funnet, kan dette vanligvis løses med en reinstallasjon.
{.is-info}