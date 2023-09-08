---
title: LidarrのMacOSインストール
description: LidarrのMacOSインストールガイド
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS（OSX）

{#OSX}

> Lidarrは、.NETの非互換性のため、OSXバージョン10.15（Catalina）未満では動作しません。
{.is-warning}

1. [MacOSアプリ](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true)または[MacOS M1アプリ](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)をダウンロードします（システムに応じて選択）。
1. アーカイブを開き、Lidarrアイコンをアプリケーションフォルダにドラッグします。
1. Lidarrに自己署名を行います。`codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. Lidarrを使用するには、<http://localhost:8686>にアクセスします。