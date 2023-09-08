---
title: Readarr MacOS Installation
description: Installationsguide för Readarr på MacOS
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> Readarr är inte kompatibelt med OSX-versioner < 10.15 (Catalina) på grund av .NET-inkompatibiliteter.
{.is-warning}

1. Ladda ner [MacOS-appen](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) eller [MacOS M1-appen](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) beroende på ditt system.
1. Öppna arkivet och dra Readarr-ikonen till din Applications-mapp.
1. Självsignera Readarr `codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. Surfa till <http://localhost:8787> för att börja använda Readarr