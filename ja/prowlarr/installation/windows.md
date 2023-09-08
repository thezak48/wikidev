---
title: ProwlarrのWindowsインストール
description: ProwlarrのWindowsインストールガイド
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

ProwlarrはWindowsでネイティブにサポートされています。ProwlarrはWindowsサービスまたはシステムトレイアプリケーションとしてインストールすることができます。
> Windowsのバージョンは、Microsoftが現在サポートしているバージョンに限定されています。他のバージョンでも動作する場合がありますが、これはサポートされていない構成です。
{.is-warning}

Windowsサービスは、ユーザーがログインしていない場合でも実行されます。
それ以外の場合は、ユーザーがログインしたままであればシステムトレイアプリケーションを使用することができます。インストーラー中にそのオプションが提供されます。

> インストール後に「管理者として実行」する必要がある場合、アクセスエラー（たとえば、アクセスが拒否されましたというパス `C:\ProgramData\Prowlarr\config.xml`）が発生します。これにより、Prowlarrに必要な権限が与えられます。毎回管理者として実行する必要はありません。
{.is-warning}

1. 以下のリンクから、アーキテクチャに合った最新バージョンのProwlarrをダウンロードします。
1. インストーラーを実行します。
1. <http://localhost:9696> にアクセスして、Prowlarrを使用し始めます。

- [Windows x64 インストーラー](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 インストーラー](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> [x64 .zip ダウンロード](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64)を使用してProwlarrを手動でインストールすることも可能です。ただし、その場合は依存関係、インストール、および権限について手動で処理する必要があります。
{.is-info}

> IISのLetsEncrypt証明書管理に[Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/)を使用しており、同じマシンにProwlarrをインストールする場合、ポート`9696`はバックグラウンドサービスによって使用されます。Prowlarrの`config.xml`でリスニングポートを変更するか、Certify The Webバックグラウンドサービスのポートを変更する必要があります。
{.is-info}