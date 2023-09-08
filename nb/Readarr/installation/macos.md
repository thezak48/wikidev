---
title: Readarr MacOS-installasjon
description: MacOS-installasjonsveiledning for Readarr
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> Readarr er ikke kompatibel med OSX-versjoner eldre enn 10.15 (Catalina) på grunn av .NET-inkompatibiliteter.
{.is-warning}

1. Last ned [MacOS-appen](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) avhengig av systemet ditt.
1. Åpne arkivet og dra Readarr-ikonet til Program-mappen din.
1. Selvsigner Readarr `codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. Gå til <http://localhost:8787> for å begynne å bruke Readarr