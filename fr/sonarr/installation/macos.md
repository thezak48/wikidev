---
title: Installation de Sonarr sur MacOS
description: Guide d'installation de Sonarr sur MacOS
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> À terme, Sonarr ne sera plus compatible avec les versions de OSX antérieures à 10.15 (Catalina) en raison d'incompatibilités avec .NET.
{.is-warning}

1. Téléchargez l'[application MacOS](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)
1. Ouvrez l'archive et faites glisser l'icône Sonarr vers votre dossier Applications.
1. Auto-signez Sonarr `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Accédez à <http://localhost:8989> pour commencer à utiliser Sonarr