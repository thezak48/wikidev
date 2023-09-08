---
title: Installation de Radarr sur MacOS
description: Guide d'installation de Radarr sur MacOS
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> Radarr n'est pas compatible avec les versions de OSX inférieures à 10.15 (Catalina) en raison d'incompatibilités avec .NET.
{.is-warning}

1. Téléchargez l'[application MacOS](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) ou l'[application MacOS M1](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true) en fonction de votre système.
1. Ouvrez l'archive et faites glisser l'icône Radarr vers votre dossier Applications.
1. Auto-signez Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. Accédez à <http://localhost:7878> pour commencer à utiliser Radarr.

> Radarr utilise une version intégrée de ffprobe pour l'analyse des fichiers multimédias et n'a pas besoin que ffprobe ou ffmpeg soit installé sur le système. Si Radarr indique que Ffprobe n'est pas trouvé, cela peut généralement être résolu en réinstallant.
{.is-info}