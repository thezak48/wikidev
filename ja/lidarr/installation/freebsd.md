---
title: Lidarr FreeBSD インストール
description: Lidarr の FreeBSD インストールガイド
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Lidarr チームは FreeBSD 向けのビルドのみ提供しています。プラグインとポートは FreeBSD コミュニティによってメンテナンスおよび作成されています。

FreeBSD のインストール手順は、GitHub アカウントを持つ任意のユーザーが必要に応じて Wiki を更新できるように、FreeBSD コミュニティによってメンテナンスされています。

[Freshports Lidarr リンク](https://www.freshports.org/net-p2p/lidarr/)

## TrueNAS GUI を使用した Jail のセットアップ

1. メイン画面から Jails を選択します。

1. ADD をクリックします。

1. Advanced Jail Creation をクリックします。

1. 名前（任意の名前で構いません）: Lidarr

1. Jail タイプ: デフォルト（クローン Jail）

1. リリース: 12.2-Release（またはそれ以降）

1. 好みに応じて基本プロパティを設定します。

1. 好みに応じて Jail プロパティを設定しますが、以下を追加します。

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` はトラブルシューティング（ping、traceroute など）に役立ちますが、必須ではありません。{.is-info}

1. 好みに応じてネットワークプロパティを設定します。

1. 好みに応じてカスタムプロパティを設定します。

1. Save をクリックします。

1. Jail が作成されると、自動的に開始されます。Lidarr がマウントされたメディアのストレージスペースを表示できるようにするために、サーバーで root シェルを開き、次のコマンドを入力します。

```shell
iocage stop <jailname>
iocage set enforce_statfs=1 <jailname>
iocage start <jailname>
```

## Lidarr のインストール

Jails リストで `lidarr` の新しく作成された Jail を見つけ、"Shell" をクリックします。

Lidarr をインストールするには

> \* pkg リポジトリが `/latest` からパッケージを取得するように設定されていることを確認してください
> \* `/usr/local/etc/pkg/repos/FreeBSD.conf` を確認します
> \* それが存在しない場合は、`/etc/pkg/FreeBSD.conf` をその場所にコピーし、`quarterly` を `latest` に置き換えます
{.is-warning}

```shell
pkg install lidarr
```

まだシェルを閉じないで、もう少しやることがあります！

## Lidarr の設定

インストールが完了したら、さらにいくつかの手順が必要です。

### サービスの設定

サービスを有効にする時間ですが、注意が必要です。

デフォルトでは、アップデーターは無効になっています。`pkg-message` にはアップデーターを有効にする方法の指示が記載されていますが、`pkg check -s` や `pkg remove` のような Lidarr の組み込みアップデーターがファイルを置き換えると、これらの機能が壊れる可能性があることに注意してください。

サービスを有効にするには:

```shell
sysrc lidarr_enable=TRUE
```

user/group `lidarr` を使用したくない場合は、サービスファイルに実行するユーザー/グループを指定する必要があります。

```shell
sysrc lidarr_user="USER_YOU_WANT"
```

```shell
sysrc lidarr_group="GROUP_YOU_WANT"
```

`lidarr` はデフォルトでデータ、設定、ログ、PID ファイルを `/usr/local/lidarr` に保存します。サービスファイルはこれを作成し、所有権を取得しますが、それが存在しない場合に限ります。これらのファイルを別の場所に保存したい場合（例：スナップショットを容易にするために Jail にマウントされたデータセットなど）、`sysrc` を使用して変更する必要があります。

```shell
sysrc lidarr_data_dir="DIR_YOU_WANT"
```

注意: 既存の場所を使用している場合は、所有権を UID/GID `lidarr` が使用するものに手動で変更するか、書き込みアクセス権を持つ GID に `lidarr` を追加する必要があります。

ほぼ完了です。サービスを開始しましょう。

```shell
service lidarr start
```

すべてが計画どおりに進んだ場合、lidarr は Jail の IP（ポート 8686）で起動して実行されているはずです。

シェルを安全に閉じることができます。

## トラブルシューティング

- サービスは実行されているようですが、UI が読み込まれないか、ページがタイムアウトしています
  - Jail で `allow_mlock` が有効になっていることを再確認してください。
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Jail の `VNET` がオンになっていること、ip6=inherit または ip6=new であることを確認してください。

> サービススクリプトは現在、VNET や IP6 の不足を回避し、VNET または ip6=inherit の要件を削除するように動作するはずです。{.is-info}