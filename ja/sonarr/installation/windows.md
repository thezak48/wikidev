---
title: SonarrのWindowsインストール
description: SonarrのWindowsインストールガイド
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

SonarrはWindowsでネイティブにサポートされています。SonarrはWindowsサービスまたはシステムトレイアプリケーションとしてインストールすることができます。

> Windowsのバージョンは、Microsoftが現在サポートしているバージョンに制限されています。他のバージョンでも動作する場合がありますが、これはサポートされていない構成です。
{.is-warning}

Windowsサービスは、ユーザーがログインしていない場合でも実行されますが、ネットワークドライブ（X：\ マップドドライブまたは\\\server\share UNCパス）には特別な設定手順が必要です。

さらに、Windowsサービスはデフォルトで「ローカルサービス」アカウントで実行されますが、このアカウントは**ユーザーのホームディレクトリにアクセスする権限がない場合、手動で権限を割り当てる必要があります**。これは、ホームディレクトリにダウンロードクライアントを使用している場合に特に関連します。

そのため、ユーザーがログインしたままであれば、Sonarrをシステムトレイアプリケーションとしてインストールすることをお勧めします。インストーラーの実行中にこのオプションが提供されます。

> インストール後にアクセスエラーが発生する場合（たとえば、パス `C:\ProgramData\Sonarr\config.xml` へのアクセスが拒否されました）またはマップドネットワークドライブを使用している場合は、「管理者として実行」を1回実行する必要があります。これにより、Sonarrに必要な権限が与えられます。毎回「管理者として実行」する必要はありません。
{.is-warning}

1. 以下のリンクから、アーキテクチャに合った最新バージョンのSonarrをダウンロードします。
1. インストーラーを実行します。
1. <http://localhost:8989> にアクセスして、Sonarrを使用を開始します。

- [Windows x32 インストーラー](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> [x32 .zip ダウンロード](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows)を使用してSonarrを手動でインストールすることも可能です。ただし、その場合は依存関係、インストール、および権限について手動で処理する必要があります。
{.is-info}