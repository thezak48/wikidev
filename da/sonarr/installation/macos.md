---
title: Sonarr MacOS Installation
description: MacOS installationsguide til Sonarr
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> Sonarr vil på et tidspunkt ikke længere være kompatibel med OSX-versioner under 10.15 (Catalina) på grund af .NET-inkompatibiliteter.
{.is-warning}

1. Download [MacOS-appen](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)
1. Åbn arkivet og træk Sonarr-ikonet til din Applications-mappe.
1. Selvsignér Sonarr `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Gå til <http://localhost:8989> for at begynde at bruge Sonarr