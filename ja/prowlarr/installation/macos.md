---
title: ProwlarrのMacOSインストール
description: ProwlarrのMacOSインストールガイド
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS（OSX）

{#OSX}
  
> .NETの非互換性のため、ProwlarrはOSXバージョン10.15（Catalina）未満では動作しません。
{.is-warning}

1. [MacOSアプリ](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true)または[MacOS M1アプリ](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)をダウンロードします（システムに応じて選択）。
1. アーカイブを開き、Prowlarrアイコンを「Applications」フォルダにドラッグします。
1. Prowlarrに自己署名を行います。`codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. <http://localhost:9696>にアクセスして、Prowlarrを使用し始めます。