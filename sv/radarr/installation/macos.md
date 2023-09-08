---
title: Radarr MacOS Installation
description: Installationsguide för Radarr på MacOS
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> Radarr är inte kompatibel med OSX-versioner < 10.15 (Catalina) på grund av .NET-inkompatibiliteter.
{.is-warning}

1. Ladda ner [MacOS-appen](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) beroende på ditt system.
1. Öppna arkivet och dra Radarr-ikonen till din mapp för applikationer.
1. Självsignera Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. Gå till <http://localhost:7878> för att börja använda Radarr.

> Radarr använder en buntad version av ffprobe för analys av mediefiler och kräver inte att ffprobe eller ffmpeg är installerade på systemet. Om Radarr säger att Ffprobe inte hittas kan detta vanligtvis åtgärdas genom en ominstallation.
{.is-info}