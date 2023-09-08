---
title: Lidarr サポート対象
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> このページは作業中であり、追加の作業が必要です。{.is-warning}

このページは、通常 UI での `詳細情報` に相当するすべての「サポートされている」ウィキリンクの曖昧さ回避ページです。

# ダウンロードクライアント

{#downloadclient}

- Deluge {#deluge}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Flood {#flood}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [設定ページを参照してください](/lidarr/settings#download-clients)
  - uTorrent はアドウェアであり、以前はスパイウェアであったため、おすすめできません。ほとんどのユーザーは qBittorrent を使用しています。
- Vuze {#vuze}
  - [設定ページを参照してください](/lidarr/settings#download-clients)

# インデクサー

{#indexer}

## Usenet

- Newznab {#newznab}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
  - Newznab は、多くの Usenet インデックスサイトで使用されている標準化された API です。多くのプリセットが利用可能ですが、すべてには API キーが必要です。
  - [Prowlarr](/prowlarr) や [NZBHydra2](https://github.com/theotherp/nzbhydra2) のようなインデクサーアプリケーションは、統計追跡などの高度な機能を提供できます。

## Torrents

- FileList {#filelist}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - プライベートトラッカー
  > IP Torrents のネイティブ実装は検索をサポートしていません{.is-info}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - パブリックトラッカー
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- Torrent RSS フィード {#torrentrssindexer}
  - 汎用のトレント RSS フィードパーサーです。
  > RSS フィードには `pubdate` が含まれている必要があります。リリースサイズも推奨されます{.is-info}
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - プライベートインデクサー
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab は Torrent と Newznab の言葉遊びです。Newznab API 仕様と同じ構造と構文を使用しますが、トレント固有の属性と .torrent ファイルを公開します。そのため、最新の RSS フィードとバックログ検索の機能をサポートします。この仕様は、Newznab 組織によってメンテナンスやサポートされていません（同じ API 仕様は nZEDb と共有されています）。
  - これは主に [Prowlarr](/prowlarr) と [Jackett](https://github.com/Jackett/Jackett) によってサポートされています。
  - [設定ページを参照してください](/lidarr/settings#indexer-settings)

# 通知

{#notification}

- Boxcar {#boxcar}
- カスタムスクリプト {#customscript}
  - これにより、特定のアクションが発生したときにカスタムスクリプトを実行できます。詳細については、[カスタムスクリプト](/lidarr/custom-scripts) を参照してください。
- Discord {#discord}
  - Lidarr で発生するアクションの通知をプッシュするための最も一般的な方法の1つです。
- メール {#email}
  - 自分自身または迷惑メールを送りたい人にメールを送信します。Gmail を使用している場合は、安全でないアプリを有効にする必要があります。Gmail を使用しており、2要素認証が有効になっている場合は、アプリ固有のパスワードを使用する必要があります。

 > `SomePrettyName <email@example.org>` のような「きれいなアドレス」を使用できます{.is-info}

- Emby (Media Browser) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi はメディアの愛から生まれました。これは、すべてのデジタルメディアを美しく使いやすいパッケージにまとめるエンターテイメントハブです。100% 無料でオープンソースであり、非常にカスタマイズ可能で、さまざまなデバイスで実行できます。専任のボランティアチームと巨大なコミュニティによってサポートされています。Kodi を接続することで、Lidarr に新しい曲が追加されたときに Kodi のライブラリを更新することができます。
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - [有用なツール - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier) のエントリを参照してください。
- Plex Media Server {#plexserver}
  - 自己ホスト型の Plex システムのサーバーです。これを有効にすると、Kodi と同様に Plex サーバーに新しい/アップグレードされたエピソードが利用可能であることを通知する更新をプッシュできます。
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - [Tips and Tricks エントリ](/useful-tools#twitter) を参照してください。
- Webhook {#webhook}

# リスト

{#importlist}

- Headphones {#headphonesimport}
- Last.fm タグ {#lastfmtag}
- Last.fm ユーザー {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr リスト {#lidarrlists}
- MusicBrainz シリーズ {#musicbrainzseries}
- Spotify フォロー中のアーティスト {#spotifyfollowedartists}
- Spotify プレイリスト {#spotifyplaylist}
- Spotify 保存済みアルバム {#spotifysavedalbums}

# メタデータ

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}