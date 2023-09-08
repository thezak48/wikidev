---
title: Lidarr Docker インストール
description: Lidarr の Docker インストールガイド
published: true
date: 2023-08-12T16:03:02.989Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:37.188Z
---

# Docker

Lidarr チームは公式の Docker イメージを提供していません。ただし、いくつかのサードパーティが独自に作成し、メンテナンスしています。

以下の手順は、どの Lidarr Docker イメージにも適用できる一般的なガイダンスを提供します。

## Portainer

> **Docker コンテナの設定には Portainer を使用しないでください** {.is-danger}

- Portainer はコンテナを管理するための見やすい GUI ですが、それ以外の用途には適していません。
- Portainer は Docker コンテナのログやステータスを表示するためにのみ使用するべきです。
- Docker Compose を使用し、Portainer を使用しないことを強くお勧めします。
- Portainer には次のような問題があります:
  - マウントのソースとターゲットの順序が正しくない
  - 大文字と小文字の区別が一貫していない
  - コンテナ間通信のための自動作成されたカスタムネットワークが存在しない
  - 異なるアーキテクチャでの一貫した Compose の実装がない
  - 特定のタグを設定しない場合、更新時にすべてのタグを取得する
  - ARM プラットフォームでは一部の機能が非表示になり、一部はまったく機能しない

Docker Compose のセットアップ方法については、[Docker ガイド](/docker-guide)と[TRaSH の Docker チュートリアル](https://trash-guides.info/hardlinks/)を参照してください。

## よくある問題を回避する

### ボリュームとパス

Docker ボリュームには2つの一般的な問題があります: Lidarr コンテナとダウンロードクライアントコンテナ間のパスの違い、および高速な移動とハードリンクを妨げるパスです。

最初の問題は、ダウンロードクライアントがダウンロードのパスを `/torrents/My.Music.2018/` と報告するが、Lidarr コンテナでは `/downloads/My.Music.2018/` になるため問題となります。2番目の問題はパフォーマンスの問題であり、シーディングトレントに問題を引き起こします。これらの問題は、計画的で一貫性のあるパスで解決できます。

ほとんどの Docker イメージでは、`/music` や `/downloads` のようなパスを提案しています。これにより、移動が遅くなり、ハードリンクができなくなります。また、Lidarr コンテナとは異なるパスをダウンロードクライアントコンテナに設定することもあります。

最良の解決策は、`/data` のようなコンテナ内の単一の共通ボリュームを使用することです。音楽は `/data/Music`、トレントは `/data/downloads/torrents`、または Usenet ダウンロードは `/data/downloads/usenet` に配置します。

このアドバイスに従わない場合、Lidarr の Web UI (設定 › ダウンロードクライアント) でリモートパスマッピングを設定する必要があります。

### 所有権とパーミッション

ファイルの所有権とパーミッションは、Lidarr ユーザーにとって最も一般的な問題の1つです。Docker 内外の両方で問題が発生します。ほとんどのイメージには、デフォルトのユーザー、グループ、および umask を上書きするための環境変数があります。すべての関連するコンテナで共通のグループを使用することをお勧めします。これにより、各コンテナは共有グループのパーミッションを使用してマウントされたボリューム上のファイルの読み書きができます。
Lidarr はダウンロードフォルダーと最終フォルダーの読み書きが必要です。

> これらの問題の詳細な説明については、[The Best Docker Setup and Docker Guide](/docker-guide) のウィキ記事を参照してください。
{.is-info}

## Lidarr のインストール

これらの Docker イメージをインストールして使用するには、上記の内容を考慮しながら、それぞれのドキュメントに従う必要があります。Docker イメージとコンテナを管理する方法はさまざまですので、インストールとメンテナンスは選択した方法によって異なります。

- [hotio/lidarr](https://hotio.dev/containers/lidarr/)
- [lscr.io/linuxserver/lidarr](https://docs.linuxserver.io/images/docker-lidarr)
{.links-list}