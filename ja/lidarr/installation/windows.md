---
title: LidarrのWindowsインストール
description: LidarrのWindowsインストールガイド
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

LidarrはWindowsでネイティブにサポートされています。LidarrはWindowsサービスまたはシステムトレイアプリケーションとしてインストールすることができます。
> Windowsのバージョンは、Microsoftが現在サポートしているものに限定されています。他のバージョンでも動作する場合がありますが、これはサポートされていない構成です。
{.is-warning}

Windowsサービスは、ユーザーがログインしていない場合でも実行されますが、特別な注意が必要です。なぜなら、Windowsサービスは特別な設定手順なしではネットワークドライブ（X:\ マップドドライブまたは \\\server\share UNC パス）にアクセスできないからです。

さらに、Windowsサービスはデフォルトで 'Local Service' アカウントで実行されますが、このアカウントは**ユーザーのホームディレクトリにアクセスする権限が手動で割り当てられていない限り、アクセスできません**。これは、ホームディレクトリにダウンロードクライアントを設定している場合に特に関連します。

そのため、ユーザーがログインしたままであれば、Lidarrをシステムトレイアプリケーションとしてインストールすることをお勧めします。インストーラー中にこのオプションが提供されます。

> トレイモードでインストールした後、アクセスエラー（たとえば、パス `C:\ProgramData\Lidarr\config.xml` へのアクセスが拒否されました）やマップドネットワークドライブの場合には、「管理者として実行」を1回実行する必要があるかもしれません。これにより、Lidarrに必要な権限が与えられます。毎回「管理者として実行」する必要はありません。
{.is-warning}

1. 以下のリンクから、アーキテクチャに合った最新バージョンのLidarrをダウンロードします。
1. インストーラーを実行します。
1. <http://localhost:8686> にアクセスして、Lidarrを使用を開始します。

- [Windows x64 インストーラー](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 インストーラー](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> [x64 .zip ダウンロード](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64)を使用してLidarrを手動でインストールすることも可能です。ただし、その場合は依存関係、インストール、および権限について手動で処理する必要があります。
{.is-info}