---
title: Lidarr MacOS Installation
description: Anleitung zur Installation von Lidarr auf MacOS
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> Lidarr ist nicht mit OSX-Versionen < 10.15 (Catalina) kompatibel aufgrund von .NET-Inkompatibilitäten.
{.is-warning}

1. Lade die [MacOS-App](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) oder die [MacOS M1-App](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) je nach System herunter.
1. Öffne das Archiv und ziehe das Lidarr-Symbol in deinen Anwendungsordner.
1. Signiere Lidarr selbst: `codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. Gehe zu <http://localhost:8686>, um Lidarr zu verwenden.