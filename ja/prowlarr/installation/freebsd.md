---
title: Prowlarr FreeBSD インストール
description: Prowlarr の FreeBSD インストールガイド
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Prowlarr チームは FreeBSD 向けのビルドのみ提供しています。プラグインとポートは FreeBSD コミュニティによって管理および作成されています。

FreeBSD のインストール手順は、GitHub アカウントを持つ誰でも必要に応じて Wiki を更新できるように、FreeBSD コミュニティによっても管理されています。

[Freshports Prowlarr リンク](https://www.freshports.org/net-p2p/prowlarr/)

## TrueNAS GUI を使用した Jail のセットアップ

1. メイン画面から Jail を選択します。

1. 追加をクリックします。

1. 高度な Jail 作成をクリックします。

1. 名前（任意の名前で構いません）: Prowlarr

1. Jail タイプ: デフォルト（クローン Jail）

1. リリース: 12.2-Release（またはそれ以降）

1. 基本プロパティを好みに設定します。

1. Jail プロパティを好みに設定しますが、以下を追加します。

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` はトラブルシューティング（ping、traceroute など）に役立ちますが、必須ではありません。{.is-info}

1. ネットワークプロパティを好みに設定します。

1. カスタムプロパティを好みに設定します。

1. 保存をクリックします。

## Prowlarr のインストール

Jails リストで新しく作成した `prowlarr` の Jail を見つけ、"Shell" をクリックします。

Prowlarr をインストールするには

> \* pkg リポジトリが `/latest` からパッケージを取得するように設定されていることを確認してください
> \* `/usr/local/etc/pkg/repos/FreeBSD.conf` を確認します
> \* それが存在しない場合は、`/etc/pkg/FreeBSD.conf` をその場所にコピーし、`quarterly` を `latest` に置き換えて開きます
{.is-warning}

```shell
pkg install prowlarr
```

まだシェルを閉じないで、もう少しやることがあります！

## Prowlarr の設定

インストールが完了したので、さらにいくつかの手順が必要です。

### サービスの設定

サービスを有効にする時間ですが、注意点があります。

アップデーターはデフォルトで無効になっています。`pkg-message` にはアップデーターを有効にする方法の指示がありますが、注意してください: これにより、ビルトインのアップデーターがファイルを置き換えると、`pkg check -s` や `pkg remove` などの prowlarr に対するものが壊れる可能性があります。

サービスを有効にするには:

```shell
sysrc prowlarr_enable=TRUE
```

ユーザー/グループ `prowlarr` を使用したくない場合は、サービスファイルに実行するユーザー/グループを指定する必要があります。

```shell
sysrc prowlarr_user="USER_YOU_WANT"
```

```shell
sysrc prowlarr_group="GROUP_YOU_WANT"
```

`prowlarr` はデフォルトでデータ、設定、ログ、PID ファイルを `/usr/local/prowlarr` に保存します。サービスファイルは、これを作成し、所有権を取得します（存在しない場合のみ）。これらのファイルを別の場所に保存したい場合（例: スナップショットを容易にするために Jail にマウントされたデータセット）、`sysrc` を使用して変更する必要があります。

```shell
sysrc prowlarr_data_dir="DIR_YOU_WANT"
```

注意: 既存の場所を使用している場合は、所有権を UID/GID `prowlarr` が使用するものに手動で変更するか、書き込みアクセス権を持つ GID に `prowlarr` を追加する必要があります。

ほぼ完了です。サービスを起動しましょう:

```shell
service prowlarr start
```

すべてが計画どおりに進んだ場合、prowlarr は Jail の IP（ポート 9696）で起動して実行されているはずです！

シェルを安全に閉じることができます。

## トラブルシューティング

- サービスは実行されているようですが、UI が読み込まれないか、ページがタイムアウトしています
  - Jail で `allow_mlock` が有効になっていることを再確認してください
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Jail の `VNET` がオンになっていること、ip6=inherit または ip6=new であることを確認してください

> サービススクリプトは、VNET や IP6 の不足を回避し、VNET または ip6=inherit の要件をなくすようになりました。{.is-info}