---
title: Prowlarr MacOS Installation
description: Installationsanleitung für Prowlarr auf MacOS
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> Prowlarr ist nicht mit OSX-Versionen < 10.15 (Catalina) kompatibel aufgrund von .NET-Inkompatibilitäten.
{.is-warning}

1. Lade die [MacOS-App](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) oder die [MacOS M1-App](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) je nach System herunter.
1. Öffne das Archiv und ziehe das Prowlarr-Symbol in deinen Anwendungsordner.
1. Signiere Prowlarr selbst: `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. Gehe zu <http://localhost:9696>, um Prowlarr zu verwenden.