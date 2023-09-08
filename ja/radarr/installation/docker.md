---
title: Radarr Docker インストール
description: Radarr の Docker インストールガイド
published: true
date: 2023-08-12T16:02:10.602Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:47.674Z
---

# Docker

Radarr チームは公式の Docker イメージを提供していません。ただし、いくつかのサードパーティが独自のイメージを作成し、メンテナンスしています。

以下の手順は、どの Radarr Docker イメージにも適用できる一般的なガイドラインを提供します。

Synology ユーザーは、[TRaSH の Synology Docker ガイド](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)を参照してください。

## Portainer

> **Docker コンテナの設定には Portainer を使用しないでください** {.is-danger}

- Portainer はコンテナを管理するための見やすい GUI を提供しますが、それ以外の用途には適していません。
- Portainer は、Docker コンテナのログやステータスを表示するためにのみ使用するべきです。
- Docker Compose を使用し、Portainer を使用しないことを強くお勧めします。
- Portainer には以下のような問題があります:
  - マウントのソースとターゲットの順序が正しくない
  - 大文字と小文字の区別が一貫していない
  - コンテナ間の通信のためのカスタムネットワークが自動的に作成されない
  - 異なるアーキテクチャでの一貫した Compose の実装がない
  - 特定のタグを設定しない場合、更新時にすべてのタグを取得する
  - ARM プラットフォームでは一部の機能が非表示になり、一部はまったく動作しない

Docker Compose のセットアップ方法については、[Docker ガイド](/docker-guide)と[TRaSH の Docker チュートリアル](https://trash-guides.info/hardlinks/)を参照してください。

## よくある問題を回避する

### ボリュームとパス

Docker ボリュームには2つの一般的な問題があります: Radarr コンテナとダウンロードクライアントコンテナ間のパスの違い、および高速な移動とハードリンクを妨げるパスです。

最初の問題は、ダウンロードクライアントがダウンロードのパスを `/torrents/My.Movie.2018/` と報告する一方、Radarr コンテナでは `/downloads/My.Movie.2018/` になるため問題となります。2番目の問題はパフォーマンスの問題であり、シーディングトレントに問題を引き起こします。これらの問題は、計画的かつ一貫したパスで解決することができます。

ほとんどの Docker イメージでは、`/movies` や `/downloads` のようなパスを推奨しています。これにより、遅い移動が発生し、ハードリンクが使用できなくなります。また、一部のイメージでは、ダウンロードクライアントコンテナのパスを Radarr コンテナとは異なるものにすることも推奨されています（例: `/torrents`）。

最良の解決策は、`/data` のようなコンテナ内の単一の共通ボリュームを使用することです。映画は `/data/Movies`、トレントは `/data/downloads/torrents`、または Usenet ダウンロードは `/data/downloads/usenet` に配置します。

このアドバイスに従わない場合、Radarr の Web UI（設定 › ダウンロードクライアント）でリモートパスマッピングを設定する必要があります。

### 所有権とパーミッション

ファイルの所有権とパーミッションは、Radarr ユーザーにとって最も一般的な問題の1つです。Docker 内外の両方で問題が発生します。ほとんどのイメージには、デフォルトのユーザー、グループ、および umask を上書きするための環境変数があります。すべての関連するコンテナで共通のグループを使用することをお勧めします。これにより、各コンテナは共有グループのパーミッションを使用してマウントされたボリューム上のファイルの読み書きができます。
Radarr は、ダウンロードフォルダと最終フォルダの両方に読み書きするため、これを念頭に置いてください。

> これらの問題の詳細な説明については、[The Best Docker Setup and Docker Guide](/docker-guide) のウィキ記事を参照してください。
{.is-info}

## Radarr のインストール

これらの Docker イメージをインストールして使用するには、上記の内容を考慮しながら、各イメージのドキュメントに従う必要があります。Docker イメージとコンテナを管理する方法はさまざまありますので、インストールとメンテナンスは選択した方法によって異なります。

- [hotio/radarr](https://hotio.dev/containers/radarr/)
- [lscr.io/linuxserver/radarr](https://docs.linuxserver.io/images/docker-radarr)
{.links-list}