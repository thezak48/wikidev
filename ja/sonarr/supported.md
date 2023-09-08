---
title: Sonarrのサポート対象
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> このページは作業中であり、追加の作業が必要です。 {.is-warning}

このページは、通常UIの「詳細情報」で表示されるすべての「サポート対象」ウィキリンクの曖昧さ回避ページです。

# ダウンロードクライアント

{#downloadclient}

- Aria2 {#aria2}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Flood {#flood}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [設定ページを参照してください](/sonarr/settings#download-clients)
  - uTorrentは広告付きのソフトウェアであり、以前はスパイウェアであったため、推奨されていません。ほとんどのユーザーはqBittorrentを使用しています。
- Vuze {#vuze}
  - [設定ページを参照してください](/sonarr/settings#download-clients)

# インデクサー

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - 日本のメディア（アニメ）専用のUsenetインデクサーです。
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
  - Newznabは、多くのUsenetインデックスサイトで使用される標準化されたAPIです。多くのプリセットが利用可能ですが、すべてにはAPIキーが必要です。
  - [Prowlarr](/prowlarr)や[NZBHydra2](https://github.com/theotherp/nzbhydra2)などのインデクサーアプリケーションは、統計追跡などの高度な機能を提供できます。
- omgwtfnzbs {#omgwtfnzbs}
  - 非推奨のプライベートUsenetインデクサーの旧実装です。Newznabを代わりに使用してください。
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)

## トレント

- BroadcasTheNet (BTN) {#broadcasthenet}
  - プライベートトラッカー
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - プライベートトラッカー
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - プライベートトラッカー
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - プライベートトラッカー
  > IP Torrentsのネイティブ実装は検索をサポートしていません。代わりにProwlarrやJackettをtorznabとして使用してください。 {.is-info}
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 日本のメディア（アニメ）専用のトレントトラッカーです。
  - Nyaaはアニメシリーズの検索のみをサポートしています
  - ネイティブのSonarrバージョンには既知の問題があります
    - [Nyaa seeders/leechers not parsed properly anymore. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - これは、[Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637)がマージされた場合に修正できます
  - > Nyaaは自動化を好まず、頻繁にIPを禁止します。 {.is-warning}
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - パブリックトラッカー
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- Torrent RSSフィード {#torrentrssindexer}
  - 汎用のトレントRSSフィードパーサーです。
  > RSSフィードには`pubdate`が含まれている必要があります。リリースサイズも推奨されます。 {.is-info}
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - プライベートインデクサー
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - TorznabはTorrentとNewznabのかばん語です。Newznab APIの仕様と同じ構造と構文を使用しますが、トレント固有の属性と.torrentファイルを公開します。したがって、最新のRSSフィードとバックログ検索の機能をサポートします。この仕様は、Newznab組織によってメンテナンスやサポートされていません（同じAPI仕様はnZEDbと共有されています）。
  - これは主に[Prowlarr](/prowlarr)と[Jackett](https://github.com/Jackett/Jackett)によってサポートされています。
  - [設定ページを参照してください](/sonarr/settings#indexer-settings)

> 多くのトレントトラッカーはコミュニティに依存しており、サイトの訪問、カルマ、投票、コメントなどを義務付ける規則がある場合があります。
> トラッカーのルールとエチケットを確認し、コミュニティを活性化させてください。
> ルールに従わずにアカウントが禁止されたり、ヒットアンドラン（HnR）/低比率が蓄積されたりした場合、私たちは責任を負いません。 {.is-warning}

# 通知

{#notification}

- Boxcar {#boxcar}
- カスタムスクリプト {#customscript}
  - これにより、特定のアクションが発生した場合にカスタムスクリプトが実行されます。詳細については、[カスタムスクリプト](/sonarr/custom-scripts)を参照してください。
- Discord {#discord}
  - Sonarrで発生するアクションの通知をプッシュする最も一般的な方法の1つです。
  - サポートされるフィールドのタイプ：
  `Overview, Rating, Genres, Quality, Group, Size, Links, Release, Poster, Fanart, CustomFormats, CustomFormatScore, Indexer`
- メール {#email}
  - 単に自分自身または迷惑をかけたい他の誰かにメールを送信します。Gmailを使用している場合は、安全でないアプリを有効にする必要があります。Gmailを使用しており、2要素認証が有効になっている場合は、アプリ固有のパスワードを使用する必要があります。

> `SomePrettyName <email@example.org>`のような「きれいなアドレス」を使用できます。 {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodiはメディアへの愛から生まれました。それはすべてのデジタルメディアを美しく使いやすいパッケージにまとめるエンターテイメントハブです。それは100％無料でオープンソースであり、非常にカスタマイズ可能で、さまざまなデバイスで実行できます。それは献身的なボランティアチームと巨大なコミュニティによってサポートされています。Kodiを接続することで、新しいエピソードがSonarrに追加されたときにKodiのライブラリを更新することができます。
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - 廃止予定
- Plex Media Center {#plexclient}
  - 廃止予定
- Plex Media Server {#plexserver}
  - セルフホスト型のPlexシステムのサーバーです。これを有効にすると、Kodiと同様に、新しい/アップグレードされたエピソードが利用可能であることを通知するためにPlexサーバーに更新をプッシュすることができます。
  - これはほとんど必要ありませんし、Plexがファイルシステムの変更を監視できない場合にのみ必要です。
  - Plexがionotifyを使用してファイルシステムを監視できない特定のリモートマウントや一部の古いネットワークマウントなどの状況では、Plex接続ではなく、アプリのplexautoscanを使用することをお勧めします。

> これにより、シリーズが含まれているライブラリ/ルートフォルダのフルスキャンがトリガーされる場合があります。ネイティブのPlex機能を使用するか、[plexautoscan](https://github.com/l3uddz/plex_autoscan)のようなツールを使用することを強くお勧めします。 {.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - この[Tips and Tricksエントリー](/useful-tools#twitter)を参照してください。
- Webhook {#webhook}

# リスト

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSHには、2つのインスタンスを同期するための[ガイド](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)があります。
- Plexウォッチリスト {#pleximport}
  - 認証済みのPlexユーザーのPlexウォッチリストをRadarrに追加します。リストには番組が含まれている必要があります。
  - 複数のユーザーのウォッチリストを使用するには、各ユーザーのリストを追加し、それぞれのPlexユーザーで認証する必要があります。
- Traktリスト {#traktlistimport}
  - ユーザー名 - ユーザーの実際のユーザー名を入力してください
  - リスト - リストURLで表示されるリスト名を使用してください
  - 例：`https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - ユーザー名：`some-user-name`
    - リスト：`trakt-list-name`
- Trakt人気リスト {#traktpopularimport}
- Traktユーザー {#traktuserimport}

> Traktのリストには番組が含まれている必要があります。Sonarrは番組のみを一致させて追加します。 {.is-info}

# メタデータ

{#metadata}

- Kodi（XBMC）/ Emby {#xbmcmetadata}
  - 有効にする-このメタデータタイプのメタデータファイルの作成を有効にします
  - シリーズメタデータ-フルシリーズメタデータを含む`tvshow.nfo`を作成します
  - （詳細オプション）シリーズメタデータURL-`tvshow.nfo`をTheTVDbシリーズURLで作成します
  - エピソードメタデータ-各エピソードごとに`<filename>.nfo`を作成します
  - シリーズイメージ-`poster.jpg`および`banner.jpg`という名前のさまざまなシリーズイメージを作成します
  - シーズンイメージ-`season##-poster.jpg`および`season##-banner.jpg`という名前のさまざまなシーズンイメージを作成します
  - エピソードイメージ-`<filename>-thumb.jpg`などのさまざまなエピソードイメージを作成します
- Roksbox {#roksboxmetadata}
  - 有効にする-このメタデータタイプのメタデータファイルの作成を有効にします
  - エピソードメタデータ-各エピソードごとに`Season##\<filename>.xml`を作成します
  - シリーズイメージ-`Series Title.jpg`を作成します
  - シーズンイメージ-`Season ##.jpg`を作成します
  - エピソードイメージ-`Season##\<filename>.jpg`を作成します
- WDTV {#wdtvmetadata}
  - 有効にする-このメタデータタイプのメタデータファイルの作成を有効にします
  - エピソードメタデータ-各エピソードごとに`Season##\<filename>.xml`を作成します
  - シリーズイメージ-`folder.jpg`を作成します
  - シーズンイメージ-`Season ##\folder.jpg`を作成します
  - エピソードイメージ-`Season##\<filename>.metathumb`を作成します