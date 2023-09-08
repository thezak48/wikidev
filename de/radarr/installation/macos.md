---
title: Radarr MacOS Installation
description: Installationsanleitung für Radarr auf MacOS
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> Radarr ist nicht mit OSX-Versionen < 10.15 (Catalina) kompatibel aufgrund von .NET-Inkompatibilitäten.
{.is-warning}

1. Lade die [MacOS-App](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) oder die [MacOS M1-App](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) je nach System herunter.
1. Öffne das Archiv und ziehe das Radarr-Symbol in deinen Anwendungsordner.
1. Signiere Radarr selbst: `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. Gehe zu <http://localhost:7878>, um Radarr zu verwenden.

> Radarr verwendet eine gebündelte Version von ffprobe für die Analyse von Mediendateien und erfordert nicht, dass ffprobe oder ffmpeg auf dem System installiert sind. Wenn Radarr angibt, dass Ffprobe nicht gefunden wurde, kann dies in der Regel durch eine Neuinstallation behoben werden.
{.is-info}