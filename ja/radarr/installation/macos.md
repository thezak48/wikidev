---
title: RadarrのMacOSインストール
description: RadarrのMacOSインストールガイド
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS（OSX）

{#OSX}

> .NETの非互換性のため、RadarrはOSXバージョン10.15（Catalina）未満では動作しません。
{.is-warning}

1. [MacOSアプリ](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true)または[MacOS M1アプリ](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)をダウンロードします（システムに応じて選択）。
1. アーカイブを開き、Radarrアイコンをアプリケーションフォルダにドラッグします。
1. Radarrを自己署名します。`codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. <http://localhost:7878>にアクセスして、Radarrを使用し始めます。

> Radarrはメディアファイルの解析にffprobeのバンドルバージョンを使用しており、システムにffprobeやffmpegをインストールする必要はありません。もしRadarrがFfprobeが見つからないと表示された場合は、再インストールで問題が解決することがあります。
{.is-info}