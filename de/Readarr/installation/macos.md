---
title: Readarr MacOS Installation
description: Anleitung zur Installation von Readarr auf MacOS
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> Readarr ist nicht mit OSX-Versionen < 10.15 (Catalina) kompatibel aufgrund von .NET-Inkompatibilitäten.
{.is-warning}

1. Lade die [MacOS-App](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) oder die [MacOS M1-App](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) je nach System herunter.
1. Öffne das Archiv und ziehe das Readarr-Symbol in deinen Anwendungsordner.
1. Signiere Readarr selbst: `codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. Gehe zu <http://localhost:8787>, um Readarr zu verwenden.