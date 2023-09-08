---
title: RadarrのWindowsインストール
description: RadarrのWindowsインストールガイド
published: true
date: 2023-07-04T15:22:03.589Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:19.928Z
---

# Windows

RadarrはWindowsでネイティブにサポートされています。RadarrはWindowsサービスまたはシステムトレイアプリケーションとしてインストールすることができます。
> Windowsのバージョンは、Microsoftが現在サポートしているものに限定されています。他のバージョンでも動作する場合がありますが、これはサポートされていない構成です。
{.is-warning}

Windowsサービスは、ユーザーがログインしていない場合でも実行されますが、ネットワークドライブ（X:\ マップドドライブまたは \\\server\share UNC パス）には特別な設定手順が必要です。

さらに、Windowsサービスはデフォルトで 'Local Service' アカウントで実行されますが、このアカウントは**ユーザーのホームディレクトリにアクセスする権限がないため、手動で権限を割り当てない限りアクセスできません**。これは、ホームディレクトリにダウンロードクライアントを設定している場合に特に関連します。

そのため、ユーザーがログインしたままであれば、Radarrをシステムトレイアプリケーションとしてインストールすることをお勧めします。インストーラー中にこのオプションが提供されます。

> インストール後にアクセスエラーが発生する場合（たとえば、パス `C:\ProgramData\Radarr\config.xml` へのアクセスが拒否されました）や、マップドネットワークドライブを使用している場合は、一度「管理者として実行」する必要があるかもしれません。これにより、Radarrに必要な権限が与えられます。毎回「管理者として実行」する必要はありません。
{.is-warning}

1. 以下のリンクから、アーキテクチャに合った最新バージョンのRadarrをダウンロードします。
1. インストーラーを実行します。
1. <http://localhost:7878> にアクセスして、Radarrを使用を開始します。

- [Windows x64 インストーラー](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 インストーラー](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> [x64 .zip ダウンロード](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64)を使用してRadarrを手動でインストールすることも可能です。ただし、その場合は依存関係、インストール、および権限について手動で処理する必要があります。
{.is-info}