---
title: Prowlarr MacOS Installation
description: Installationsguide för Prowlarr på MacOS
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> Prowlarr är inte kompatibelt med OSX-versioner < 10.15 (Catalina) på grund av .NET-inkompatibiliteter.
{.is-warning}

1. Ladda ner [MacOS-appen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) beroende på ditt system.
1. Öppna arkivet och dra Prowlarr-ikonen till din Applications-mapp.
1. Självsignera Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. Surfa till <http://localhost:9696> för att börja använda Prowlarr.