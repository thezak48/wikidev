---
title: Synologyパッケージ
description: Servarr Synologyパッケージ
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synologyパッケージ](#servarr-synology-packages)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [DSM 7.XでのBubblewrapのインストール](#bubblewrap-installation-on-dsm-7x)
    - [シンプルなBubblewrapのインストール](#simple-bubblewrap-installation)
    - [マニュアルでのBubblewrapのインストール](#manual-bubblewrap-installation)

# Servarr Synologyパッケージ

> これらのパッケージは「ベータ版」と考えられます
{.is-danger}

- ServarrチームがSynologyパッケージを作成およびメンテナンスしています
- インストール手順は、特定のDSMバージョンについて以下に記載されています

> 通常、Servarrバージョンと互換性のある既存のSynoCommunityバージョンはいくつかの手順が必要です。これは、旧パッケージを削除する必要があります。[データベースのバックアップの方法 *リンクはRadarrの例ですが、手順/概念は同じです*](/radarr/faq#how-do-i-backuprestore-radarr)を参照してください。これは、\*ArrアプリのWebインターフェースを介して行うことができます。
{.is-warning}

> SynoCommunityには、[NASごとのアーキテクチャのリスト](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model)があり、正しいパッケージを特定するのに役立ちます。
{.is-info}

# DSM 6.x

- Lidarr-Official、Prowlarr-Official、Radarr-Official、Readarr-Official、およびSonarrパッケージは*動作するはずです*。
- SynoCommunityからのスタンドアロンのMonoパッケージはもはや必要ではありません。現在は当社のパッケージにバンドルされています。
- [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)から、NASのアーキテクチャに対応したアプリケーションのリリースをダウンロードし、[パッケージマネージャーを介してパッケージを手動でインストール](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)してください。

# DSM 7.x

- Lidarr-Official、Prowlarr-Official、Radarr-Official、およびReadarr-Officialパッケージは、ほとんどのアーキテクチャで*動作するはずです*。
  - `comcerto2k`を搭載したNASでは、Lidarr、Prowlarr、Radarr、およびReadarrには追加の手順が必要です。[手順を参照してください](#bubblewrap-installation-on-dsm-7x)。
- Sonarrパッケージは、**すべての**アーキテクチャに対して追加の手順が必要です。
- SynoCommunityからのスタンドアロンのMonoパッケージはもはや必要ではありません。現在は当社のパッケージにバンドルされています。

> `comcerto2k`を搭載したNAS（*すべてのパッケージ*）およびSonarr（*すべてのNASアーキテクチャ*）では、Bubblewrapパッケージをインストールし、手動で指示された手順を実行する必要があります。**\*Arrパッケージをインストールする前にBubblewrapをインストールする必要があります**
{.is-warning}

- [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)から、NASのアーキテクチャに対応したBubblewrapのリリースをダウンロードし、[パッケージマネージャーを介してパッケージを手動でインストール](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)してください。
- DSM 7.Xの以下のBubblewrapインストール手順を完了してください。
- Bubblewrapがインストールされたら、[Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)から、NASのアーキテクチャに対応したアプリケーションのリリースをダウンロードし、[パッケージマネージャーを介してパッケージを手動でインストール](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)してください。

## DSM 7.XでのBubblewrapのインストール

Bubblewrapを使用すると、.NET6を実行するために十分な新しいライブラリを使用してプログラムを基本的なコンテナで実行できます。

> **DSM 7.0+の制限により、インストール後にいくつかの手動設定が必要です。**
{.is-danger}

### シンプルなBubblewrapのインストール

1. DSM内でトリガータスクを作成します：

- ユーザー：`root`
  - イベント：`起動時`

1. `実行コマンド`に以下を入力します：

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. トリガータスクを保存し、1回実行します。

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### マニュアルでのBubblewrapのインストール

1. [SynologyにSSHでログインし、`root`に昇格します](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. 次のコマンドを実行します：

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```