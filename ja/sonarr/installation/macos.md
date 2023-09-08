---
title: SonarrのMacOSインストール
description: SonarrのMacOSインストールガイド
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> .NETの非互換性のため、Sonarrは将来的にはOSXバージョン<10.15（Catalina）と互換性がなくなる予定です。
{.is-warning}

1. [MacOSアプリ](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)をダウンロードします。
1. アーカイブを開き、Sonarrアイコンをアプリケーションフォルダにドラッグします。
1. Sonarrに自己署名を行います。`codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. Sonarrを使用するには、<http://localhost:8989>にアクセスします。