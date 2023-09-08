---
title: Readarr Docker インストール
description: Readarr の Docker インストールガイド
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Readarr チームは公式の Docker イメージを提供していません。ただし、いくつかのサードパーティが独自の Docker イメージを作成・メンテナンスしています。

以下の手順は、どの Readarr Docker イメージにも適用できる一般的なガイドラインを提供します。

## Portainer

> **Docker コンテナの設定には Portainer を使用しないでください** {.is-danger}

- Portainer はコンテナを管理するための見栄えの良い GUI ツールですが、それ以外の用途には適していません。
- Portainer は Docker コンテナのログやステータスを表示するためにのみ使用するべきです。
- Docker Compose を使用し、Portainer を使用しないことを強くお勧めします。
- Portainer には次のような問題があります:
  - マウントのソースとターゲットの順序が正しくない
  - 大文字と小文字の区別が一貫していない
  - コンテナ間通信のためのカスタムネットワークが自動的に作成されない
  - 異なるアーキテクチャでの一貫した Docker Compose の実装がない
  - 特定のタグを設定しない場合、更新時にすべてのタグを取得する
  - ARM プラットフォームでは一部の機能が非表示になり、一部はまったく機能しない

Docker Compose のセットアップ方法については、[Docker ガイド](/docker-guide)と[TRaSH の Docker チュートリアル](https://trash-guides.info/hardlinks/)を参照してください。

## よくある問題を回避する

### ボリュームとパス

Docker ボリュームには2つの一般的な問題があります: Readarr コンテナとダウンロードクライアントコンテナ間のパスの違い、および高速な移動とハードリンクができないパスです。

最初の問題は、ダウンロードクライアントがダウンロードのパスを `/torrents/My.Movie.2018/` と報告する一方、Readarr コンテナでは `/downloads/My.Movie.2018/` になるため問題となります。2つ目の問題はパフォーマンスの問題であり、トレントのシーディングに問題を引き起こします。これらの問題は、計画的かつ一貫したパスで解決できます。

ほとんどの Docker イメージでは、`/books` や `/downloads` のようなパスを提案しています。これにより移動が遅くなり、ハードリンクができなくなります。また、ダウンロードクライアントコンテナのパスも Readarr コンテナとは異なるパス（例: `/torrents`）を使用するように推奨するものもあります。

最良の解決策は、`/data` のようなコンテナ内の共通のボリュームを使用することです。Books は `/data/Books`、トレントは `/data/downloads/torrents`、Usenet ダウンロードは `/data/downloads/usenet` に配置します。

このアドバイスに従わない場合、Readarr の Web UI（設定 › ダウンロードクライアント）でリモートパスマッピングを設定する必要があります。

### Calibre の統合

ルートフォルダを作成する際に、Calibre の統合を使用するかどうかを選択できます。この選択はフォルダの作成時にのみ行えます。Calibre を使用して書籍ライブラリを管理している場合は、このオプションを選択する必要があります。Calibre を使用すると、Calibre が書籍ファイルの名前付けと整理を行います。

Calibre を実行している場合、まず Calibre コンテンツサーバーを起動する必要があります（設定 / ネットワーク共有）。また、ユーザーとパスワードも設定する必要があります。これには Calibre の再起動が必要です。

> Calibre コンテンツサーバーと Calibre は Calibre Web ではありません。Calibre Web はこれらのプログラムとは関係のない別のツールであり、Readarr では必要ありませんし使用されません。
{.is-warning}

### 所有権とパーミッション

ファイルの所有権とパーミッションは、Readarr ユーザーにとって最も一般的な問題の1つです。Docker 内外の両方で問題が発生します。ほとんどのイメージには、デフォルトのユーザー、グループ、および umask を上書きするための環境変数があります。コンテナを設定する前にこれを決定する必要があります。おすすめは、関連するすべてのコンテナに共通のグループを使用することで、各コンテナがマウントされたボリューム上のファイルを読み書きするための共有グループのパーミッションを使用することです。
Readarr はダウンロードフォルダと最終フォルダの両方に読み書きの権限が必要です。

> これらの問題の詳細な説明については、[The Best Docker Setup and Docker Guide](/docker-guide) の Wiki 記事を参照してください。
{.is-info}

## Readarr のインストール

これらの Docker イメージをインストールして使用するには、上記の内容を考慮しながら、各イメージのドキュメントに従う必要があります。Docker イメージとコンテナを管理する方法はさまざまありますので、インストールとメンテナンスは選択した方法によって異なります。

> 現時点では、:nightly や :develop のタグを Docker イメージと一緒に使用する必要があります。マスターブランチは存在しないため、[ブランチの意味についてはこの FAQ エントリを参照してください](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}