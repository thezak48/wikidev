---
title: Sonarr Docker インストール
description: Sonarr の Docker インストールガイド
published: true
date: 2023-08-12T16:03:21.613Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:15.754Z
---

# Docker

Sonarr チームは公式の Docker イメージを提供していません。ただし、いくつかのサードパーティが独自のイメージを作成し、メンテナンスしています。

以下の手順は、どの Sonarr Docker イメージにも適用できる一般的なガイダンスを提供します。

Synology ユーザーは、[TRaSH の Synology Docker ガイド](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)を参照してください。

## Portainer

> **Docker コンテナの設定には Portainer を使用しないでください** {.is-danger}

- Portainer はコンテナを管理するための見やすい GUI を提供しますが、それ以外の用途には適していません。
- Portainer は、Docker コンテナのログやステータスを表示するためにのみ使用するべきです。
- Docker Compose を使用し、Portainer を使用しないことを強くお勧めします。
- Portainer には以下のような問題があります:
  - マウントのソースとターゲットの順序が正しくない
  - 大文字と小文字の区別が一貫していない
  - コンテナ間通信のためのカスタムネットワークが自動的に作成されない
  - 異なるアーキテクチャでの一貫した Docker Compose の実装がない
  - 特定のタグを設定しない場合、更新時にすべてのタグを取得する
  - ARM プラットフォームでは一部の機能が非表示になり、動作しないものもある

Docker Compose のセットアップ方法については、[Docker ガイド](/docker-guide)と[TRaSH の Docker チュートリアル](https://trash-guides.info/hardlinks/)を参照してください。

## よくある問題を回避する

### ボリュームとパス

Docker ボリュームには2つの一般的な問題があります: Sonarr コンテナとダウンロードクライアントコンテナ間のパスの違い、および高速な移動とハードリンクを妨げるパスです。

前者は、ダウンロードクライアントがダウンロードのパスを `/torrents/My.Series.2018/` と報告する一方、Sonarr コンテナでは `/downloads/My.Series.2018/` になるため問題となります。後者はパフォーマンスの問題であり、シーディングトレントに問題を引き起こします。これらの問題は、計画的かつ一貫性のあるパスで解決できます。

ほとんどの Docker イメージでは、`/tv` や `/downloads` のようなパスを提案しています。これにより、移動が遅くなり、ハードリンクができなくなります。また、一部のイメージでは、ダウンロードクライアントコンテナのパスを Sonarr コンテナとは異なるものにすることも推奨されています（例: `/torrents`）。

最適な解決策は、`/data` のようなコンテナ内の共通のボリュームを使用することです。シリーズは `/data/Series`、トレントは `/data/downloads/torrents`、ユーズネットのダウンロードは `/data/downloads/usenet` に配置します。

このアドバイスに従わない場合、Sonarr の Web UI（設定 › ダウンロードクライアント）でリモートパスマッピングを設定する必要があります。

### 所有権とパーミッション

ファイルの所有権とパーミッションは、Sonarr ユーザーにとって最も一般的な問題の1つです。Docker 内外の両方で問題が発生します。ほとんどのイメージには、デフォルトのユーザー、グループ、および umask を上書きするための環境変数があります。コンテナを設定する前にこれを決定する必要があります。おすすめは、関連するすべてのコンテナに共通のグループを使用し、各コンテナがマウントされたボリューム上のファイルの読み書きに共有グループのパーミッションを使用することです。
Sonarr は、ダウンロードフォルダと最終フォルダの両方に読み書きの権限が必要です。

> これらの問題の詳細な説明については、[The Best Docker Setup and Docker Guide](/docker-guide) の Wiki 記事を参照してください。
{.is-info}

## Sonarr のインストール

これらの Docker イメージをインストールして使用するには、上記の内容を考慮しながら、各イメージのドキュメントに従う必要があります。Docker イメージとコンテナを管理する方法はさまざまありますので、インストールとメンテナンスは選択した方法によって異なります。

- [hotio/sonarr](https://hotio.dev/containers/sonarr/)
- [lscr.io/linuxserver/sonarr](https://docs.linuxserver.io/images/docker-sonarr)
{.links-list}