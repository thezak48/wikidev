---
title: Sonarr MacOS Installatie
description: Installatiehandleiding voor Sonarr op MacOS
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> Sonarr zal uiteindelijk niet langer compatibel zijn met OSX-versies < 10.15 (Catalina) vanwege .NET-incompatibiliteiten.
{.is-warning}

1. Download de [MacOS App](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)
1. Open het archief en sleep het Sonarr-pictogram naar je Toepassingen-map.
1. Onderteken Sonarr zelf `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Ga naar <http://localhost:8989> om Sonarr te gebruiken.