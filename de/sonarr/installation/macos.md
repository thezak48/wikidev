---
title: Sonarr MacOS Installation
description: Anleitung zur Installation von Sonarr auf MacOS
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> Sonarr wird in Zukunft nicht mehr mit OSX-Versionen < 10.15 (Catalina) kompatibel sein, aufgrund von .NET-Inkompatibilitäten.
{.is-warning}

1. Lade die [MacOS App](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true) herunter.
1. Öffne das Archiv und ziehe das Sonarr-Symbol in deinen Anwendungsordner.
1. Signiere Sonarr selbst: `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Gehe zu <http://localhost:8989>, um Sonarr zu verwenden.