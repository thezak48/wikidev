---
title: Sonarr MacOS Installation
description: Installationsguide för Sonarr på MacOS
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> Sonarr kommer inte längre vara kompatibel med OSX-versioner < 10.15 (Catalina) på grund av .NET-inkompatibiliteter.
{.is-warning}

1. Ladda ner [MacOS-appen](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)
1. Öppna arkivet och dra Sonarr-ikonen till din Applications-mapp.
1. Självsignera Sonarr `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Gå till <http://localhost:8989> för att börja använda Sonarr