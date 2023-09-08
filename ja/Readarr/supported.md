---
title: Readarrのサポート
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> このページは作業中であり、追加の作業が必要です。{.is-warning}

このページは、通常UIの「詳細情報」に対応するすべての「サポートされている」ウィキリンクの曖昧さ回避ページです。

# ダウンロードクライアント

{#downloadclient}

- Aria2 {#aria2}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Flood {#flood}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [設定ページを参照してください](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [設定ページを参照してください](/readarr/settings#download-clients)
  - uTorrentはアドウェアであり、以前はスパイウェアであったため、推奨されていません。ほとんどのユーザーはqBittorrentを使用しています。
- Vuze {#vuze}
  - [設定ページを参照してください](/readarr/settings#download-clients)

# インデクサー

{#indexer}

## Usenet

- Newznab {#newznab}
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
  - Newznabは、多くのUsenetインデックスサイトで使用されている標準化されたAPIです。多くのプリセットが利用可能ですが、すべてAPIキーが必要です。
  - [Prowlarr](/prowlarr)や[NZBHydra2](https://github.com/theotherp/nzbhydra2)などのインデクサーアプリケーションは、統計追跡などの高度な機能を提供できます。
- omgwtfnzbs {#omgwtfnzbs}
  - プライベートなUsenetインデクサー
  - [設定ページを参照してください](/readarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - プライベートトラッカー
  > IP Torrentsのネイティブ実装は検索をサポートしていません{.is-info}
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 日本のメディア（アニメ）専用のトレントトラッカーです。
  > Nyaaは自動化を好まず、IPを頻繁に禁止することがあります{.is-info}
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - パブリックトラッカー
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
- Torrent RSSフィード {#torrentrssindexer}
  - 汎用のトレントRSSフィードパーサーです。
  > RSSフィードには`pubdate`が含まれている必要があります。リリースサイズも推奨されています{.is-info}
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - プライベートインデクサー
  - [設定ページを参照してください](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - TorznabはTorrentとNewznabの言葉遊びです。Newznab APIの仕様と同じ構造と構文を使用しますが、トレント固有の属性と.torrentファイルを公開します。したがって、最新のRSSフィードとバックログ検索の機能をサポートしています。この仕様は、Newznab組織によってメンテナンスやサポートされていません（同じAPI仕様はnZEDbと共有されています）。
  - これは主に[Prowlarr](/prowlarr)と[Jackett](https://github.com/Jackett/Jackett)によってサポートされています。
  - [設定ページを参照してください](/readarr/settings#indexer-settings)

# 通知

{#notification}

- Boxcar {#boxcar}
- カスタムスクリプト {#customscript}
  - これにより、特定のアクションが発生した場合にカスタムスクリプトが実行されます。詳細については、[カスタムスクリプト](/readarr/custom-scripts)を参照してください。
- Discord {#discord}
  - Readarrで発生するアクションの通知をプッシュするための最も一般的な方法の1つです。
- メール {#email}
  - 単純に自分自身または迷惑をかけたい他の誰かにメールを送信します。Gmailを使用している場合は、安全でないアプリを有効にする必要があります。Gmailを使用しており、2要素認証が有効になっている場合は、アプリ固有のパスワードを使用する必要があります。

 > `SomePrettyName <email@example.org>`のような「きれいなアドレス」を使用できます{.is-info}

- GoodReadsの本棚 {#goodreadsbookshelf}
- GoodReadsの所有書籍 {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - [有用なツール - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)のエントリを参照してください。
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synologyインデクサー {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - この[Tips and Tricksのエントリ](/useful-tools#twitter)を参照してください。
- Webhook {#webhook}

# リスト

{#importlist}

- GoodReadsの本棚 {#goodreadsbookshelf}
  - (高度なオプション) ユーザーID - 自分のユーザーIDではない場合は、ここにユーザーIDを入力します。
  - 本棚 - GoodReadsからインポートする本棚を選択します。
  - GoodReadsで認証する - GoodReadsで認証するためのボタンをクリックします。

> 複数のGoodReadsユーザーは、別々のリストとして追加できます。認証されたユーザーを使用するだけでなく、詳細オプションを有効にしてユーザーIDを入力し、GoodReadsで認証してユーザーの本棚を取得することもできます{.is-info}

- GoodReadsの所有書籍 {#goodreadsownedbooks}
  - (高度なオプション) ユーザーID - 自分のユーザーIDではない場合は、ここにユーザーIDを入力します。
  - 本棚 - GoodReadsからインポートする本棚を選択します。
  - GoodReadsで認証する - GoodReadsで認証するためのボタンをクリックします。

> 複数のGoodReadsユーザーは、別々のリストとして追加できます。認証されたユーザーを使用するだけでなく、詳細オプションを有効にしてユーザーIDを入力し、GoodReadsで認証してユーザーの本棚を取得することもできます{.is-info}

- GoodReadsのリスト {#goodreadslistimportlist}
  - リストID - 追加するGoodReadsの公開リストIDを入力します。
- GoodReadsのシリーズ {#goodreadsseriesimportlist}
  - シリーズID - 追加するGoodReadsのシリーズIDを入力します。
- LazyLibrarian {#lazylibrarianimport}
  - URL - LazyLibrarianインスタンスのURL
  - APIキー - LazyLibrarianインスタンスのAPIキー
- Readarr {#readarrimport}
  - フルURL - インポート元のReadarrインスタンスのフルURL（例：`http://localhost:8787/readarr`）
  - APIキー - インポート元のReadarrインスタンスのAPIキー
  - プロファイル - インポート元のReadarrインスタンスのプロファイル
  - タグ - インポート元のReadarrインスタンスのタグ

# メタデータ

{#metadata}

- Calibre {#calibre}
  - [設定ページを参照してください](/readarr/settings#write-metadata-to-book-files)
- オーディオタグ付け {#audiotagging}
  - [設定ページを参照してください](/readarr/settings#write-metadata-to-book-files)