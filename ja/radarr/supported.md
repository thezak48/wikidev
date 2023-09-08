---
title: Radarr サポートされているもの
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# 目次

> このページは作業中であり、追加の作業が必要です。{.is-warning}

このページは、一般的には UI での「詳細情報」を指す、すべての `supported` ウィキリンクの曖昧さ回避ページです。

# ダウンロードクライアント

{#downloadclient}

- Aria2 {#aria2}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Flood {#flood}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [設定ページを参照してください](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [設定ページを参照してください](/radarr/settings#download-clients)
  - uTorrent はアドウェアであり、以前はスパイウェアであったため、推奨されていません。ほとんどのユーザーは Qbittorrent を使用しています。
- Vuze {#vuze}
  - [設定ページを参照してください](/radarr/settings#download-clients)

# インデクサー

{#indexer}

## Usenet

- Newznab {#newznab}
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
  - Newznab は、多くの Usenet インデックスサイトで使用されている標準化された API です。多くのプリセットが利用可能ですが、すべてには API キーが必要です。
  - [Prowlarr](/prowlarr) や [NZBHydra2](https://github.com/theotherp/nzbhydra2) のようなインデクサーアプリケーションは、統計追跡などの高度な機能を提供できます。
- omgwtfnzbs {#omgwtfnzbs}
  - 非推奨のプライベート Usenet インデクサーの旧実装です。Newznab を代わりに使用してください。
  - [設定ページを参照してください](/radarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - プライベートトラッカー
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - プライベートトラッカー
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - プライベートトラッカー
  > IP Torrents のネイティブ実装は検索をサポートしていません。代わりに Prowlarr や Jackett を torznab として使用してください。{.is-info}
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 日本のメディア（アニメ）専用のトレントトラッカーです。
  > Nyaa は自動化を好まず、IP を頻繁に禁止することがあります。{.is-info}
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - プライベートトラッカー
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - パブリックトラッカー
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- Torrent RSS フィード {#torrentrssindexer}
  - 汎用のトレント RSS フィードパーサーです。
  > RSS フィードには `pubdate` が含まれている必要があります。リリースサイズも推奨されます。{.is-info}
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - Torznab フォーマットの Couchpotato の旧バージョンです。
  - [設定ページを参照してください](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab は Torrent と Newznab の言葉遊びです。Newznab API 仕様と同じ構造と構文を使用しますが、トレント固有の属性と .torrent ファイルを公開します。そのため、最新の RSS フィードとバックログ検索の機能をサポートします。この仕様は Newznab 組織によってメンテナンスやサポートされていません。（同じ API 仕様は nZEDb と共有されています）
  - これは主に [Prowlarr](/prowlarr) と [Jackett](https://github.com/Jackett/Jackett) によってサポートされています。
  - [設定ページを参照してください](/radarr/settings#indexer-settings)

> 多くのトレントトラッカーはコミュニティに依存しており、サイトの訪問、カルマ、投票、コメントなどのルールがある場合があります。
> トラッカールールとエチケットを確認し、コミュニティを活性化させてください。
> ルールに従わずにアカウントが禁止されたり、ヒットアンドラン（HnR）/低比率が蓄積されたりしても、私たちは責任を負いません。{.is-warning}

# 通知

{#notification}

- Boxcar {#boxcar}
- カスタムスクリプト {#customscript}
  - これにより、特定のアクションが発生したときにカスタムスクリプトを実行できます。詳細については、[カスタムスクリプト](/radarr/custom-scripts) を参照してください。
- Discord {#discord}
  - Radarr で発生するアクションの通知をプッシュするための最も一般的な方法の一つです。
- メール {#email}
  - 単に自分自身または迷惑をかけたい人にメールを送信します。Gmail を使用している場合は、安全でないアプリを有効にする必要があります。Gmail を使用しており、2要素認証が有効になっている場合は、アプリ固有のパスワードを使用する必要があります。

> `SomePrettyName <email@example.org>` のような「きれいなアドレス」を使用できます。{.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi はメディアの愛から生まれました。それはすべてのデジタルメディアを美しく使いやすいパッケージにまとめるエンターテイメントハブです。それは100％無料でオープンソースであり、非常にカスタマイズ可能で、さまざまなデバイスで実行できます。それは献身的なボランティアチームと巨大なコミュニティによってサポートされています。Kodi を接続することで、新しい映画が Radarr に追加されたときに Kodi のライブラリを更新することができます。
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - [Useful Tools - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier) のエントリを参照してください
- Plex Media Server {#plexserver}
  - セルフホスト型の Plex システムのサーバーです。これを有効にすると、Kodi のように Plex サーバーに新しい/アップグレードされた映画が利用可能であることを通知することができます。
  - これはほとんど必要ありませんし、Plex がファイルシステムの変更を監視できない場合にのみ必要です。
  - Plex が ionotify を使用してファイルシステムを監視できない場合（特定のタイプのリモートマウントや一部の古いネットワークマウントなど）、Plex 接続ではなくアプリ plexautoscan を使用することをお勧めします。
- [plexautoscan](https://github.com/l3uddz/plex_autoscan) のようなツールも選択肢の一つです。

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology インデクサー {#synologyindexer}
- Telegram {#telegram}
- Trakt {#trakt}
- Twitter {#twitter}
  - [Tips and Tricks エントリ](/useful-tools#twitter) を参照してください
- Webhook {#webhook}

# リスト

{#importlist}

- CouchPotato {#couchpotatoimport}
- カスタムリスト {#radarrlistimport}
- IMDb リスト {#imdblistimport}
  - IMDb ウォッチリストを追加するには、リストに移動して編集をクリックします。プライバシー設定がパブリックに設定されていることを確認してください。アドレスバーには、Radarr に入力する必要のある `lsxxxxxx` の番号が表示されます。

    1. IMDb リスト設定に移動します
    1. プライバシーが `Public`（つまり `Disabled`）に設定されていることを確認します
    1. URL 内の `ls` 番号を使用します

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex ウォッチリスト {#plex}
  - 必要条件: v4.1.0.6176+
  - 認証された Plex ユーザーの Plex ウォッチリストを Radarr に追加します。リストには映画が含まれている必要があります。
  - 複数のユーザーのウォッチリストを使用するには、各ユーザーのリストを追加し、その Plex ユーザーで認証する必要があります。
- Radarr {#radarrimport}
  - TRaSH には、2つのインスタンスを同期するための[ガイド](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)があります
- RSS リスト {#rssimport}
- StevenLu カスタム {#stevenluimport}
	- JSON 形式でカスタム映画リストを作成できます。
  	フィードには、各映画に対して `title` または `imdb_id` のいずれかを含める必要があります。両方を提供することもできます。
  		> `imdb_id` は `title` よりも広範な検索を必要としないため、安全です。{.is-info}
    以下は有効な JSON のサンプルです:
      ```
      [
          {
            "title": "The Wastetown",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/6J32RMp8uko8CUEM3rYP962hQun.jpg",
            "imdb_id": "tt22889064"
          },
          {
            "title": "Wild Sunflowers",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/tHK4c0UZKrqkmXZ2HJeGNhNetRz.jpg",
            "imdb_id": "tt13774830"
          }
      ]
      ```
      - アイテムには追加のキーを追加できます（無視されます）
      - 空のリストの場合は、空の JSON 配列 `[]` を返します
- StevenLu リスト {#stevenlu2import}
- TMDb コレクション {#tmdbcollectionimport}
  - Radarr v4.2 ではコレクションリストはサポートされなくなり、Radarr 内のコレクションに移行されました。詳細については、[コレクション](/radarr/library#collections) セクションを参照してください。
- TMDb 会社 {#tmdbcompanyimport}
- TMDb キーワード {#tmdbkeywordimport}
- TMDb リスト {#tmdblistimport}
- TMDb 人物 {#tmdbpersonimport}
  - TMDb 人物の URL が `https://www.themoviedb.org/person/500-tom-cruise` の場合、Person ID は `500` です
- TMDb 人気 {#tmdbpopularimport}
  - Top は <https://developers.themoviedb.org/3/movies/get-top-rated-movies> を使用します
  - Popular は <https://developers.themoviedb.org/3/movies/get-popular-movies> を使用します
  - Theaters は <https://developers.themoviedb.org/3/movies/get-now-playing> を使用します
  - Upcoming は <https://developers.themoviedb.org/3/movies/get-upcoming> を使用します
- TMDb ユーザー {#tmdbuserimport}
- Trakt リスト {#traktlistimport}
  - ユーザー名 - ユーザーの実際のユーザー名を入力し、ユーザーの名前ではないことを確認してください
  - リスト - リスト URL で表示されるリスト名を使用してください
  - 例: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - ユーザー名: `some-user-name`
    - リスト: `trakt-list-name`
- Trakt 人気リスト {#traktpopularimport}
- Trakt ユーザー {#traktuserimport}
  - 自分自身のウォッチリストを使用する場合に使用するタイプです

# メタデータ

{#metadata}

- Emby（レガシー） {#mediabrowsermetadata}
  - 有効にする - このメタデータタイプのメタデータファイルの作成を有効にします
  - 映画メタデータ - このメタデータタイプのメタデータファイルの作成を有効にします
- Kodi（XBMC）/ Emby {#xbmcmetadata}
  - 有効にする - このメタデータタイプのメタデータファイルの作成を有効にします
  - 映画メタデータ - 映画のメタデータを含む `<filename>.nfo` を作成します
  - （詳細オプション）映画メタデータ URL - TMDb と IMDb の映画 URL を含む `movie.nfo` を作成します
  - メタデータ言語 - 利用可能な場合に Radarr がメタデータを書き込むために使用する言語を選択します
  - 映画画像 - ポスターやバナーなどのさまざまなシーズン画像を作成します
  - Movie.nfo を使用する - デフォルトではなく `movie.nfo` として nfo ファイルを書き込みます
  - コレクション名 - Radarr は .nfo ファイルにコレクション名を書き込みます
- Roksbox {#roksboxmetadata}
  - 有効にする - このメタデータタイプのメタデータファイルの作成を有効にします
  - 映画メタデータ - 各映画のために xml ファイルを作成します
  - 映画画像 - `Movie.jpg` を作成します
- WDTV {#wdtvmetadata}
  - 有効にする - このメタデータタイプのメタデータファイルの作成を有効にします
  - 映画メタデータ - 各エピソードのために `<filename>.xml` を作成します
  - 映画画像 - `folder.jpg` を作成します