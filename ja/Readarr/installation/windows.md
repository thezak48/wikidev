---
title: ReadarrのWindowsインストール
description: ReadarrのWindowsインストールガイド
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

ReadarrはWindowsでネイティブにサポートされています。ReadarrはWindowsサービスまたはシステムトレイアプリケーションとしてインストールすることができます。
> Windowsのバージョンは、Microsoftが現在サポートしているものに限定されています。他のバージョンでも動作する場合がありますが、これはサポートされていない構成です。
{.is-warning}

Windowsサービスは、ユーザーがログインしていない場合でも実行されますが、特別な設定が必要です。Windowsサービスは、特別な設定手順なしではネットワークドライブ（X：\ マップドドライブまたは\ \ \ server \ share UNCパス）にアクセスできません。

さらに、Windowsサービスはデフォルトで「ローカルサービス」アカウントで実行されますが、このアカウントは**ユーザーのホームディレクトリにアクセスする権限が手動で割り当てられていない限り、アクセスできません**。これは、ホームディレクトリにダウンロードクライアントを設定している場合に特に関連します。

したがって、ユーザーがログインしたままであれば、Readarrをシステムトレイアプリケーションとしてインストールすることをお勧めします。インストーラー中にこのオプションが提供されます。

> インストール後にアクセスエラーが発生する場合（たとえば、パス `C:\ProgramData\Readarr\config.xml` へのアクセスが拒否されました）またはマップドネットワークドライブを使用する場合は、「管理者として実行」を1回実行する必要がある場合があります。これにより、Readarrに必要な権限が与えられます。毎回管理者として実行する必要はありません。
{.is-warning}

> 注意: [PmsService](https://github.com/cjmurph/PmsService)を介してPlexをサービスとして実行している場合、PMsServiceのポートを`8787`から変更するか、`config.xml`ファイルでReadarrが実行されるポートを変更する必要があります。
{.is-info}

1. 下記のリンクから、使用しているアーキテクチャに対応した最新バージョンのReadarrをダウンロードします。
1. インストーラーを実行します。
1. <http://localhost:8787> にアクセスして、Readarrを使用を開始します。

- [Windows x64 インストーラー](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 インストーラー](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> [x64 .zip ダウンロード](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64)を使用してReadarrを手動でインストールすることも可能です。ただし、その場合は依存関係、インストール、および権限について手動で処理する必要があります。
{.is-info}