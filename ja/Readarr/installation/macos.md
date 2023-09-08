---
title: ReadarrのMacOSインストール
description: ReadarrのMacOSインストールガイド
published: true
date: 2023-07-28T11:16:36.367Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:47.465Z
---

# MacOS (OSX)

{#OSX}

> .NETの非互換性のため、ReadarrはOSXバージョン10.15（Catalina）未満では動作しません。
{.is-warning}

1. [MacOS App](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=x64&installer=true)または[MacOS M1 App](https://readarr.servarr.com/v1/update/develop/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)をダウンロードします（システムに応じて選択）。
1. アーカイブを開き、Readarrアイコンをアプリケーションフォルダにドラッグします。
1. Readarrに自己署名を付けます。`codesign --force --deep -s - /Applications/Readarr.app && xattr -rd com.apple.quarantine /Applications/Readarr.app`
1. <http://localhost:8787>にアクセスして、Readarrを使用を開始します。