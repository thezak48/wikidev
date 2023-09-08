---
title: Sonarr MacOS-installasjon
description: MacOS-installasjonsveiledning for Sonarr
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> Sonarr vil etter hvert ikke lenger være kompatibel med OSX-versjoner eldre enn 10.15 (Catalina) på grunn av .NET-inkompatibiliteter.
{.is-warning}

1. Last ned [MacOS-appen](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)
1. Åpne arkivet og dra Sonarr-ikonet til Program-mappen din.
1. Selvsigner Sonarr `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Gå til <http://localhost:8989> for å begynne å bruke Sonarr