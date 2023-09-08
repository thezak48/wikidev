---
title: Prowlarr Docker インストール
description: Prowlarr の Docker インストールガイド
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Prowlarr チームは公式の Docker イメージを提供していません。ただし、いくつかのサードパーティが独自のイメージを作成し、メンテナンスしています。

> Docker の詳細な説明や推奨されるプラクティスについては、[The Best Docker Setup and Docker Guide](/docker-guide) のウィキ記事を参照してください。
{.is-info}

Synology ユーザーは、[TRaSH's Synology Docker Guide](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) を参照してください。

## Portainer

> **Docker コンテナの設定には Portainer を使用しないでください** {.is-danger}

- Portainer はコンテナを管理するための見栄えの良い GUI ですが、それ以上の役割はありません。
- Portainer は Docker コンテナのログやステータスを表示するためにのみ使用するべきです。
- Docker Compose を使用し、Portainer を使用しないことを強くお勧めします。
- Portainer には次のような問題があります:
  - マウントのソースとターゲットの順序が正しくない
  - 大文字と小文字の区別が一貫していない
  - コンテナ間の通信のためのカスタムネットワークが自動的に作成されない
  - 異なるアーキテクチャでの一貫した Compose の実装がない
  - 特定のタグを設定しない場合、更新時にすべてのタグを取得する
  - ARM プラットフォームでは一部の機能が非表示になり、動作しないものもある

Docker Compose の設定方法については、[Docker Guide](/docker-guide) と [TRaSH's Docker Tutorial](https://trash-guides.info/hardlinks/) を参照してください。

## Prowlarr のインストール

これらの Docker イメージをインストールして使用するには、上記の内容を考慮しながら、それぞれのドキュメントに従う必要があります。Docker イメージとコンテナを管理する方法はさまざまありますので、インストールとメンテナンスは選択した方法によって異なります。

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}