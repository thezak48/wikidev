---
title: Sonarrの設定
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, needs-love, settings
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# 目次

- [目次](#目次)
- [メニューオプション](#メニューオプション)
- [メディア管理](#メディア管理)
  - [コミュニティの命名提案](#コミュニティの命名提案)
  - [エピソードの命名](#エピソードの命名)
    - [標準エピソードフォーマット](#標準エピソードフォーマット)
    - [シリーズの命名](#シリーズの命名)
    - [シリーズID](#シリーズid)
    - [シーズン](#シーズン)
    - [エピソード](#エピソード)
    - [放送日](#放送日)
    - [エピソードタイトル](#エピソードタイトル)
    - [品質](#品質)
    - [メディア情報](#メディア情報)
    - [その他](#その他)
    - [オリジナル](#オリジナル)
  - [デイリーエピソードフォーマット](#デイリーエピソードフォーマット)
  - [アニメエピソードフォーマット](#アニメエピソードフォーマット)
    - [絶対エピソード番号](#絶対エピソード番号)
  - [シリーズフォルダフォーマット](#シリーズフォルダフォーマット)
    - [シリーズの命名](#シリーズの命名-1)
    - [シリーズID](#シリーズid-1)
  - [シーズンフォルダフォーマット](#シーズンフォルダフォーマット)
    - [シーズン](#シーズン-1)
  - [シーズンフォルダフォーマット](#シーズンフォルダフォーマット-1)
    - [スペシャル](#スペシャル)
  - [マルチエピソードスタイル](#マルチエピソードスタイル)
  - [フォルダ](#フォルダ)
  - [インポート](#インポート)
  - [ファイル管理](#ファイル管理)
  - [権限](#権限)
  - [ルートフォルダ](#ルートフォルダ)
- [プロファイル](#プロファイル)
  - [品質プロファイル](#品質プロファイル)
  - [言語プロファイル](#言語プロファイル)
  - [遅延プロファイル](#遅延プロファイル)
    - [使用方法](#使用方法)
    - [遅延プロファイルの動作](#遅延プロファイルの動作)
      - [例](#例)
        - [例1](#例1)
        - [例2](#例2)
        - [例3](#例3)
  - [リリースプロファイル](#リリースプロファイル)
- [品質](#品質-1)
  - [品質テーブルの意味](#品質テーブルの意味)
  - [定義された品質](#定義された品質)
- [インデクサ](#インデクサ)
  - [サポートされているインデクサ](#サポートされているインデクサ)
    - [インデクサの設定](#インデクサの設定)
    - [Usenetインデクサの設定](#usenetインデクサの設定)
    - [トレントトラッカーの設定](#トレントトラッカーの設定)
  - [オプション](#オプション)
- [ダウンロードクライアント](#ダウンロードクライアント)
  - [概要](#概要)
  - [ダウンロードクライアントのプロセス](#ダウンロードクライアントのプロセス)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [ダウンロードクライアント](#ダウンロードクライアント-1)
    - [サポートされているダウンロードクライアント](#サポートされているダウンロードクライアント)
    - [Usenetクライアントの設定](#usenetクライアントの設定)
    - [トレントクライアントの設定](#トレントクライアントの設定)
    - [トレントクライアントのダウンロードの互換性の削除](#トレントクライアントのダウンロードの互換性の削除)
  - [完了したダウンロードの処理](#完了したダウンロードの処理)
    - [完了したダウンロードの削除](#完了したダウンロードの削除)
    - [ダウンロードの失敗の処理](#ダウンロードの失敗の処理)
  - [リモートパスマッピング](#リモートパスマッピング)
- [インポートリスト](#インポートリスト)
  - [リスト](#リスト)
  - [リストの除外](#リストの除外)
- [接続](#接続)
  - [接続](#接続)
  - [接続トリガー](#接続トリガー)
- [メタデータ](#メタデータ)
  - [メタデータ](#メタデータ-1)
- [タグ](#タグ)
- [一般](#一般)
  - [ホスト](#ホスト)
  - [セキュリティ](#セキュリティ)
  - [プロキシ](#プロキシ)
  - [ログ](#ログ)
  - [アナリティクス](#アナリティクス)
  - [アップデート](#アップデート)
  - [バックアップ](#バックアップ)
- [UI](#ui)
  - [カレンダー](#カレンダー)
  - [日付](#日付)
  - [スタイル](#スタイル)
  
このページでは、Sonarrで利用可能なすべての設定とその動作について説明します。これは包括的な「Sonarrの設定方法」ではありません。代わりに、[クイックスタート](/sonarr/quick-start-guide)ページを参照してください。

# メニューオプション

設定ページに移動するには、左のメニューから「設定」を選択してください。以下のサブメニューオプションが利用可能になります：

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

また、各個別の設定ページには、メニューの上部にいくつかのオプションがあります：

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- 「高度なオプションを非表示/表示」は、以下で「(高度なオプション)」とマークされている項目に対して重要です。それ以外の場合、これらの項目は表示されません。これらのメニューアイテムは、スクリーンショットでオレンジ色で表示されます。

- 画面を離れる前に変更を保存する必要があります。ディスクアイコンをクリックして保存します。変更がない場合は、「変更なし」と表示され、グレーアウトされます。

# メディア管理

> これらの設定の一部は、「高度な設定を表示」を有効にする必要があります。これは、検索バーの上部にある上部バーにあります{.is-info}

## コミュニティの命名提案

> 以下は、[TRaSH's Guides](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/)からのコミュニティの命名提案です{.is-info}

> 注意: v3.0.6.1431以降、SonarrはDolby Vision (DV) およびHigh Dynamic Range (HDR)のタイプを認識するようになりました。バージョンが低い場合は、`{[MediaInfo VideoDynamicRangeType]}`を`{[MediaInfoVideoDynamicRange]}`に置き換えてください{.is-warning}

- 標準シリーズ: `{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- デイリーシリーズ: `{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- アニメシリーズ: `{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- シーズンフォルダ: `Season {season:00}`

- マルチエピソードスタイル: `Scene`

- シリーズフォルダ: `{Series TitleYear} [imdb-{ImdbId}]`

## エピソードの命名

- エピソードのリネーム - ファイルのリネームを有効にするにはチェックを入れます
  - チェックを外すと:
    - ダウンロードクライアントのインポート
      - シーズンパック以外: ダウンロードクライアントのリリースタイトルが使用されます
      - シーズンパック: オリジナルファイル名
    - 手動（アドホック）インポート: オリジナルファイル名

- 非合法な文字の置換 - チェックを外すと、Sonarrはそれらを削除します。
  - 文字は次のとおりです: `:` `\` `/` `>` `<` `?` `*` `|` `"`

### 標準エピソードフォーマット

標準エピソードフォーマット - 標準シリーズタイプのエピソードの命名規則を設定します。`?`アイコンをクリックして`ファイル名トークン`ダイアログボックスを表示します。

- ドロップダウンボックス（右上のコーナー）
  - 左のボックス - スペースの処理
  - スペース ( ) - スペースを使用して命名する（デフォルト）
  - ピリオド (.) - スペースの代わりにピリオドを使用して命名する
  - アンダースコア (_) - スペースの代わりにアンダースコアを使用して命名する
  - ダッシュ (-) - スペースの代わりにダッシュを使用して命名する
  - 右のボックス - 大文字と小文字の処理
  - デフォルトのケース - タイトルを大文字と小文字にする（~キャメルケース）（デフォルト）
  - 大文字 - タイトルをすべて大文字にする
  - 小文字 - タイトルをすべて小文字にする

### シリーズの命名

- `{Series Title}` = シリーズ名のタイトル！
- `{Series CleanTitleYear}` = シリーズ名 タイトル！ 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = シリーズ名 タイトル！
- `{Series TitleThe}` = シリーズ名 タイトル！, The
- `{Series TitleYear}` = シリーズ名 タイトル (2010)
- `{Series Year}` = (2010)

### シリーズID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### シーズン

- `{season:0}` = 1
- `{season:00}` =  01

### エピソード

- `{episode:0}` = 1
- `{episode:00}` = 01

### 放送日

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### エピソードタイトル

- `{Episode Title}` = エピソードタイトル
- `{Episode CleanTitle}` =  エピソードタイトル

### 品質

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### メディア情報

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguagesAll}` = \[DE\]
- `{MediaInfo AudioLanguagesAll}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`、`AudioLanguages`、および`SubtitleLanguages`は、ファイル名に含まれる言語をフィルタリングするための`:EN+DE`サフィックスをサポートしています。特定の言語を除外するには、`-DE`を使用します。 <kb>+</kb>を追加すると（例：`:EN+`）、除外された言語に応じて`[EN]`、`[EN+--]`、または`[--]`が出力されます。たとえば、`{MediaInfo Full:EN+DE}`とします。
{.is-info}

> `AudioLanguages`は、オーディオの言語が1つしか存在せず、それがEN（英語）である場合、言語を表示しません。所望の動作を得るために、例えばドイツ語と英語を表示するには、`{MediaInfo AudioLanguagesAll:DE+EN}`を使用します。
{.is-info}

> `MediaInfo VideoDynamicRangeType`には、DV、DV HDR10、HDR10、HDR10Plus、HLG、PQ、およびHDRの可能な値が表示されます。
{.is-info}

### その他

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNALまたはNF

> \* Preferred wordsは、リテラルマッチした単語または単語のいずれかです。上記の例では、`iNTERNAL`という優先ワードが返されます。同様に、`/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i`という優先ワードを使用すると、`AMZN`または`Amazon`が返されます。
\* `{Preferred Words:<Release Profile Name>}`は、特定のリリースプロファイルのマッチを使用するための追加のオプションです。
{.is-info}

### オリジナル

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> `Original Title`はリリース名であり、使用することが推奨されています。
{.is-info}

>`Original Filename`は推奨されません。これはリテラルな元のファイル名であり、`t1i0p3s7i8yu7ti`のように曖昧になる可能性があります。
{.is-warning}

## デイリーエピソードフォーマット

デイリーエピソードフォーマット - デイリーシリーズタイプのエピソードの命名規則を設定します。`?`アイコンをクリックして`ファイル名トークン`ダイアログボックスを表示します。

詳細については、[標準エピソードフォーマット](/sonarr/settings#標準エピソードフォーマット)を参照してください。

## アニメエピソードフォーマット

アニメエピソードフォーマット - アニメシリーズタイプのエピソードの命名規則を設定します。`?`アイコンをクリックして`ファイル名トークン`ダイアログボックスを表示します。

詳細については、[標準エピソードフォーマット](/sonarr/settings#標準エピソードフォーマット)を参照してください。

### 絶対エピソード番号

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## シリーズフォルダフォーマット

(高度なオプション) - シリーズフォルダ - フォルダの命名規則を設定します。`?`アイコンをクリックして`ファイル名トークン`ダイアログボックスを表示します。

### シリーズの命名

- `{Series Title}` = シリーズ名！
- `{Series CleanTitleYear}` = シリーズ名 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = シリーズ名
- `{Series TitleThe}` = シリーズ名, The
- `{Series TitleYear}` = シリーズ名 (2010)
- `{Series Year}` = (2010)

### シリーズID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## シーズンフォルダフォーマット

### シーズン

- `{season:0}` = 1
- `{season:00}` = 01

## シーズンフォルダフォーマット

### スペシャル

`スペシャル`（シーズン）フォルダの名前

- `スペシャル`

> `スペシャル`を使用することをお勧めします。
{.is-info}

## マルチエピソードスタイル

- `Extend` = `S01E01-02-03`
- `Duplicate` = `S01E01.S01E01`
- `Repeat` = `S01E01E02E03`
- `Scene` = `S01E01-E02-E03`
- `Range` = `S01E01-03`
- `Prefixed Range` = `S01E01-E03`

> `Scene`を使用することをお勧めします。
{.is-info}

## フォルダ

- 空のメディアフォルダを作成 - ディスクスキャン中に存在しないシリーズフォルダを作成します
- 空のフォルダを削除 - ディスクスキャン中およびエピソードファイルが削除されたときに、空のシリーズおよびシーズンフォルダを削除します

## インポート



- SDTV: Standard Definition TV. Low-quality video with a resolution of 480i or 576i.
- DVD: DVD quality. Video sourced from DVDs with a resolution of 480p or 576p.
- WEBDL-480p: Video sourced from online streaming platforms with a resolution of 480p.
- HDTV-720p: High Definition TV. Video captured from broadcast television with a resolution of 720p.
- WEBDL-720p: Video sourced from online streaming platforms with a resolution of 720p.
- HDTV-1080p: High Definition TV. Video captured from broadcast television with a resolution of 1080p.
- WEBDL-1080p: Video sourced from online streaming platforms with a resolution of 1080p.
- BluRay-720p: Video sourced from Blu-ray discs with a resolution of 720p.
- BluRay-1080p: Video sourced from Blu-ray discs with a resolution of 1080p.
- WEBDL-2160p: Video sourced from online streaming platforms with a resolution of 2160p (4K).
- BluRay-2160p: Video sourced from Blu-ray discs with a resolution of 2160p (4K).
- Unknown: Quality information is not available.

- 不明 - 自明
- SDTV - アナログソース（通常はケーブルテレビまたはOTA標準解像度）からの放送後のリップ。画質は一般的に良好です（解像度に対して）。通常、DivX / XviDまたはMP4でエンコードされます。
- WEBDL-480p - WEB-DL（P2P）は、Netflix、Amazon Video、Hulu、Crunchyroll、Discovery GO、BBC iPlayerなどのストリーミングサービスから無損失でリッピングされたファイルを指します。またはiTunesなどのオンライン配信ウェブサイトからダウンロードされます。品質はかなり良好で、再エンコードされていません。ビデオ（H.264またはH.265）とオーディオ（AC3 / AAC）ストリームは通常、iTunesまたはAmazon Videoから抽出され、品質を損なうことなくMKVコンテナにリマックスされます。これらのリリースの利点は、BD / DVDRipsと同様に、通常、画面上にネットワークのロゴが表示されないことです。これらはほぼBlu-rayソースと同じくらい優れていますが、ストリーミングサービスの適応ビットレートによるオーディオの遅延やビジュアルアーティファクトの問題が発生する可能性があります。リッパーのインターネット接続がビットレートが低下するまで落ちると、ソースのビットレートが動的に変化するため、画質にばらつきが生じる可能性があります。極端な量のビジュアルアーティファクトに苦しむほとんどのリリースはNUKEDされ、適応ビットレートの乱れを修正するために通常PROPERがリリースされます。これは480p（SD）の品質です。
- WEBRip-480p - WEB-Rip（P2P）では、ファイルは通常、HLSまたはRTMP / Eプロトコルを使用して抽出され、TS、MP4、またはFLVコンテナからMKVにリマックスされます。これは480p（SD）の品質です。
- DVD - 最終リリースされたDVD9の再エンコード。可能な場合、これは小売前にリリースされます。解像度に対して非常に優れた品質であるはずです。DVDリップは通常、DivX / XviDまたはMP4でリリースされます。
- Bluray-480p - 最終リリースされたBlu-rayの再エンコードで、480pの解像度に縮小されます（720x480 @ 16：9、他のアスペクト比は異なる解像度になる場合があります）。可能な場合、これは小売前にリリースされます。解像度に対して非常に優れた品質です。ビットレートは異なる場合がありますが、これらは一般的にDivX、XviD、またはAVCにエンコードされ、元のソースに比べてわずかな品質の低下とファイルサイズの大幅な削減のトレードオフを提供します。これらは一般的にMKVまたはMP4ですが、AVIを使用するDivX / XviDもあります。
- HDTV-720p - 最終リリースされたBlu-rayの再エンコードですが、HDケーブルまたは衛星で放送されます（1280x720 @ 16：9、他のアスペクト比は異なる解像度になる場合があります）。ネットワークによってランタイムまたはコンテンツが変更される場合があります。これは通常、小売リリースの数ヶ月後にリリースされますが、STARZやHBOなどのケーブルチャンネルで標準解像度の映画の拡大バージョンがリリースされることがあり、それらがその特定の映画の唯一のHDコピーになります。これらは一般的にMKVまたはMP4です。
- HDTV-1080p - 最終リリースされたBlu-rayの再エンコードですが、HDケーブルまたは衛星で放送されます（1920x1080 @ 16：9、他のアスペクト比は異なる解像度になる場合があります）。ネットワークによってランタイムまたはコンテンツが変更される場合があります。これは通常、小売リリースの数ヶ月後にリリースされますが、STARZやHBOなどのケーブルチャンネルで標準解像度の映画の拡大バージョンがリリースされることがあり、それらがその特定の映画の唯一のHDコピーになります。これらは一般的にMKVまたはMP4コンテナです。
- Raw-HD - HDストリームの生のフィード。
- WEBRip-720p - WEB-Rip（P2P）では、ファイルは通常、HLSまたはRTMP / Eプロトコルを使用して抽出され、TS、MP4、またはFLVコンテナからMKVにリマックスされます。これは720pの品質です。
- Bluray-720p - 最終リリースされたBlu-rayの再エンコードで、720pの解像度に縮小されます（1280x720 @ 16：9、他のアスペクト比は異なる解像度になる場合があります）。可能な場合、これは小売前にリリースされます。解像度に対して非常に優れた品質です。ビットレートは異なる場合がありますが、これらは一般的にAVCまたはHEVCにエンコードされ、元のソースに比べてわずかな品質の低下とファイルサイズの大幅な削減のトレードオフを提供します。これらは一般的にMKVまたはMP4コンテナです。
- WEBDL-1080p - WEB-DL（P2P）は、Netflix、Amazon Video、Hulu、Crunchyroll、Discovery GO、BBC iPlayerなどのストリーミングサービスから無損失でリッピングされたファイルを指します。またはiTunesなどのオンライン配信ウェブサイトからダウンロードされます。品質はかなり良好で、再エンコードされていません。ビデオ（H.264またはH.265）とオーディオ（AC3 / AAC）ストリームは通常、iTunesまたはAmazon Videoから抽出され、品質を損なうことなくMKVコンテナにリマックスされます。これらのリリースの利点は、BD / DVDRipsと同様に、通常、画面上にネットワークのロゴが表示されないことです。これらはほぼBlu-rayソースと同じくらい優れていますが、ストリーミングサービスの適応ビットレートによるオーディオの遅延やビジュアルアーティファクトの問題が発生する可能性があります。リッパーのインターネット接続がビットレートが低下するまで落ちると、ソースのビットレートが動的に変化するため、画質にばらつきが生じる可能性があります。極端な量のビジュアルアーティファクトに苦しむほとんどのリリースはNUKEDされ、適応ビットレートの乱れを修正するために通常PROPERがリリースされます。これは1080pの品質です。
- WEBRip-1080p - WEB-Rip（P2P）では、ファイルは通常、HLSまたはRTMP / Eプロトコルを使用して抽出され、TS、MP4、またはFLVコンテナからMKVにリマックスされます。これは1080pの品質です。
- Bluray-1080p - 最終リリースされたBlu-rayの再エンコードで、元のソースと同じ解像度のネイティブ1080p（1920x1080 @ 16：9、他のアスペクト比は異なる解像度になる場合があります）。可能な場合、これは小売前にリリースされます。解像度に対してわずかな品質の低下とファイルサイズのわずかな削減のトレードオフを提供しますが、一般的にAVCまたはHEVCにエンコードされます。これらは一般的にMKVまたはMP4コンテナです。
- Remux-1080p - リマックスは、Blu-rayまたはHD DVDディスクを別のコンテナ形式にリッピングするか、メニューやボーナス素材を削除してオーディオとビデオストリームの内容をそのまま保持する（現在のコーデックも保持する）リッピングです。これは1080pの品質です。
- HDTV-2160p - TVRipはキャプチャカードからのキャプチャソースです。HDTVはHDテレビからのキャプチャソースを表します。HDTVソースでは、品質はDVDを上回ることがあります。この形式の映画は人気が高まっています。一部のリリースでは、再生中に広告や商業バナーが表示される場合があります。これは2160p（4K）の品質です。
- WEBDL-2160p - WEB-DL（P2P）は、Netflix、Amazon Video、Hulu、Crunchyroll、Discovery GO、BBC iPlayerなどのストリーミングサービスから無損失でリッピングされたファイルを指します。またはiTunesなどのオンライン配信ウェブサイトからダウンロードされます。品質はかなり良好で、再エンコードされていません。ビデオ（H.264またはH.265）とオーディオ（AC3 / AAC）ストリームは通常、iTunesまたはAmazon Videoから抽出され、品質を損なうことなくMKVコンテナにリマックスされます。これらのリリースの利点は、BD / DVDRipsと同様に、通常、画面上にネットワークのロゴが表示されないことです。これらはほぼBlu-rayソースと同じくらい優れていますが、ストリーミングサービスの適応ビットレートによるオーディオの遅延やビジュアルアーティファクトの問題が発生する可能性があります。リッパーのインターネット接続がビットレートが低下するまで落ちると、ソースのビットレートが動的に変化するため、画質にばらつきが生じる可能性があります。極端な量のビジュアルアーティファクトに苦しむほとんどのリリースはNUKEDされ、適応ビットレートの乱れを修正するために通常PROPERがリリースされます。これは2160p（4K）の品質です。
- WEBRip-2160p - WEB-Rip（P2P）では、ファイルは通常、HLSまたはRTMP / Eプロトコルを使用して抽出され、TS、MP4、またはFLVコンテナからMKVにリマックスされます。これは2160p（4K）の品質です。
- Bluray-2160p - 最終リリースされたBlu-rayの再エンコードで、ネイティブの2160p解像度（3840x2160 @ 16：9、他のアスペクト比は異なる解像度になる場合があります）です。一般的にはHEVCコーデックでリリースされ、8ビットまたは10ビットのカラーレプロダクションまたはHDRソースから取得されます。わずかなファイルサイズの削減。これらは一般的にMKVまたはMP4コンテナです。
- Remux-2160p - リマックスは、Blu-rayまたはHD DVDディスクを別のコンテナ形式にリッピングするか、メニューやボーナス素材を削除してオーディオとビデオストリームの内容をそのまま保持する（現在のコーデックも保持する）リッピングです。これは2160p（4K）の品質です。

# インデクサー

> サポートされているインデクサーの情報は、このセクションの[詳細情報（サポートされている）](/sonarr/supported#indexers)ページで確認できます
{.is-info}

## サポートされているインデクサー

- サポートされているインデクサーのリストは、[詳細情報（サポートされている）](/sonarr/supported#indexers)ページにあります

### インデクサーの設定

- 新しいインデクサーを追加するために<kb>+</kb>ボタンをクリックすると、さまざまなオプションが表示される新しいウィンドウが表示されます。このWikiの目的において、SonarrではUsenetインデクサーとTorrentトラッカーの両方を「インデクサー」と見なしています。

- ここには2つのセクションがあります：UsenetとTorrents。使用するダウンロードクライアントに基づいて、使用するインデクサーのタイプを選択する必要があります。

### Usenetインデクサーの設定

- Newznab - ここでは、一部の人気のあるUsenetインデクサーのプリセット（事前に入力されており、選択したUsenetインデクサーから提供されるAPIキーのみが必要です）とカスタムインデクサーを作成する機能があります。
- Usenetと非常にうまく統合するソフトウェアは、[NZBHydra2](https://github.com/theotherp/nzbhydra2/)または[Prowlarr](/prowlarr)です。これらはUsenetとTorrentの両方と統合されています。
- プリセットのインデクサーまたはカスタムのインデクサー設定を選択すると、新しいウィンドウが表示され、すべての設定を入力するように求められます。
- プリセットから選択するか、カスタムインデクサー（NZBHydra2やProwlarrなど）を追加します。
- 名前 - Sonarrでのインデクサーの名前
- RSSを有効にする - 有効にすると、このインデクサーを使用して欲しいファイルを監視し、欠落しているかまだカットオフに達していないファイルを見つけます。
- 自動検索を有効にする - 有効にすると、このインデクサーを自動検索（追加時の検索を含む）に使用します。
- インタラクティブ検索を有効にする - 有効にすると、このインデクサーを手動のインタラクティブ検索に使用します。
- URL - インデクサーが提供するURL（例：`https://api.nzbgeek.info`）。
- APIパス - APIへのパス。通常は`/api`です。
- APIキー - APIにアクセスするためのキー。
- カテゴリ - 編集されない限り、デフォルトのカテゴリが使用されます。これらのデフォルトのカテゴリは最適ではない可能性があります。この設定を編集すると、Sonarrはインデクサーに利用可能なカテゴリを問い合わせ、選択可能なリストで表示します。カテゴリが切り替えられると、古いデフォルトはすぐにクリアされます。
- アニメカテゴリ - Sonarrがアニメの検索に使用するカテゴリ。編集されない限り、カテゴリは使用されません。この設定を編集すると、Sonarrはインデクサーに利用可能なカテゴリを問い合わせ、選択可能なリストで表示します。カテゴリが切り替えられると、古いデフォルトはすぐにクリアされます。
- アニメの標準形式の検索 - アニメシリーズタイプにのみ適用される標準の番号を使用してアニメを検索します（[シリーズタイプの詳細はこちら](/sonarr/faq#whats-the-different-series-types)）。
- （高度なオプション）追加パラメータ - クエリリンクに追加する追加のNewznabパラメータ
- （高度なオプション）インデクサーの優先度 - リリースのタイブレーカーシナリオで1つのインデクサーを他のインデクサーより優先するためのこのインデクサーの優先度。1が最も優先度が高く、50が最も優先度が低いです。
- （高度なオプション）ダウンロードクライアント - このインデクサーからのダウンロードのために使用するダウンロードクライアントを選択して指定します。
- タグ - 少なくとも1つの一致するタグを持つシリーズにのみこのインデクサーを使用します。すべてのシリーズで使用するには空白のままにします。

### Torrentトラッカーの設定

- Usenetと同様に、いくつかのプリセットのTorrentトラッカー情報があります。これらの特定のトラッカーのメンバーでない場合、これらのトラッカーは役に立ちません。
- SonarrでネイティブにサポートされていないTorrentトラッカーを利用するための最も良くて最も簡単な方法の1つは、[Prowlarr](/prowlarr)や[Jackett](https://github.com/Jackett/Jackett)などの2番目のプログラムを利用することです。これらのソフトウェアは、Sonarrと連携して、すべての情報を保持し、Sonarrに送信する検索インデクサーとして非常にうまく機能します。
- Torznab - このオプションは、Jackettのプリセットを設定します。複数のトラッカーを利用する場合は、各エントリに一意の名前を持たせる必要があります。
- Torznabインデクサー
- プリセットから選択するか、カスタムインデクサー（JackettやProwlarrなど）を追加します。
- 名前 - Sonarrでのインデクサーの名前
- RSSを有効にする - 有効にすると、このインデクサーを使用して欲しいファイルを監視し、欠落しているかまだカットオフに達していないファイルを見つけます。
- 自動検索を有効にする - 有効にすると、このインデクサーを自動検索（追加時の検索を含む）に使用します。
- インタラクティブ検索を有効にする - 有効にすると、このインデクサーを手動のインタラクティブ検索に使用します。
- URL - `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`などのインデクサーが提供するURL。
- APIパス - APIへのパス。通常は`/api`です。
- APIキー - APIにアクセスするためのキー。
- カテゴリ - 編集されない限り、デフォルトのカテゴリが使用されます。これらのデフォルトのカテゴリは最適ではない可能性があります。この設定を編集すると、Sonarrはインデクサーに利用可能なカテゴリを問い合わせ、選択可能なリストで表示します。カテゴリが切り替えられると、古いデフォルトはすぐにクリアされます。
- アニメカテゴリ - Sonarrがアニメの検索に使用するカテゴリ。編集されない限り、カテゴリは使用されません。この設定を編集すると、Sonarrはインデクサーに利用可能なカテゴリを問い合わせ、選択可能なリストで表示します。カテゴリが切り替えられると、古いデフォルトはすぐにクリアされます。
- アニメの標準形式の検索 - アニメシリーズタイプにのみ適用される標準の番号を使用してアニメを検索します（[シリーズタイプの詳細はこちら](/sonarr/faq#whats-the-different-series-types)）。
- （高度なオプション）追加パラメータ - クエリリンクに追加する追加のTorznabパラメータ
- （高度なオプション）最小シーダー数 - このトラッカーからのリリースを取得するために必要な最小のシーダー数。
- （高度なオプション）シード比率 - 空白の場合、ダウンロードクライアントのデフォルトが使用されます。それ以外の場合、ダウンロードクライアントがこのインデクサーからのリリースに対して満たす必要のある最小シード比率（完了したダウンロード処理 - 削除が有効になっている場合）。
- （高度なオプション）シード時間 - 空白の場合、ダウンロードクライアントのデフォルトが使用されます。それ以外の場合、ダウンロードクライアントがこのインデクサーからのリリースに対して満たす必要のある最小シード時間（完了したダウンロード処理 - 削除が有効になっている場合）。
- （高度なオプション）インデクサーの優先度 - リリースのタイブレーカーシナリオで1つのインデクサーを他のインデクサーより優先するためのこのインデクサーの優先度。1が最も優先度が高く、50が最も優先度が低いです。
- （高度なオプション）ダウンロードクライアント - このインデクサーからのダウンロードに使用するダウンロードクライアントを選択して指定します。
- タグ - 少なくとも1つの一致するタグを持つシリーズにのみこのインデクサーを使用します。すべてのシリーズで使用するには空白のままにします。

## オプション

- 最小年齢 - Usenetのみ：NZBが取得される前の最小年齢（分単位）。これにより、新しいリリースがUsenetプロバイダに伝播するのに十分な時間が与えられます。
- 保持期間 - Usenetのみ：無制限の保持期間に設定するにはゼロに設定します
- 最大サイズ - 取得するリリースの最大サイズ（MB）。無制限に設定するにはゼロに設定します。この設定はグローバルに適用されます。
- RSS同期間隔 - 分単位の間隔。無効にするにはゼロに設定します（これにより、すべての自動リリースの取得が停止します）。最小：10分 最大：120分
  - RSS同期がどのようにエピソードを見つけるのかについては、[Sonarrはエピソードをどのように見つけるのか？](/sonarr/faq#how-does-sonarr-find-episodes)を参照してください。

> Sonarrが長時間オフラインになった場合、Sonarrは最後に処理したリリースを検索して、リリースを見逃さないようにします。インデクサーがページングをサポートしており、それほど長い時間が経過していない場合、見逃したリリースを処理できるはずであり、見逃したリリースを検索する必要はありません。{.is-info}

# ダウンロードクライアント

> サポートされているダウンロードクライアントの情報は、このセクションの[詳細情報（サポートされている）](/sonarr/supported#download-clients)ページで確認できます
{.is-info}

## 概要

- ダウンロードとインポートは、ほとんどの人が問題を抱える場所です。大まかな観点からは、ソフトウェアはダウンロードクライアントと通信し、ダウンロードしたファイルにアクセスできる必要があります。サポートされているダウンロードクライアントはさまざまあり、さらにさまざまなセットアップがあります。これは、一部の共通のセットアップがある一方で、正しいセットアップは1つではなく、すべてのセットアップが少し異なる可能性があることを意味します。ただし、間違ったセットアップは多くあります。

## ダウンロードクライアントのプロセス

## Usenet

- Sonarr allows you to exclude certain series or episodes from being imported or monitored from your lists.
- To exclude a series, go to the series details page and click on the "..." button, then select "Exclude from Lists".
- To exclude specific episodes, go to the episode details page and click on the "..." button, then select "Exclude from Lists".
- Excluded series or episodes will not be imported or monitored, even if they are included in your lists.

- リストの除外をインポートする - これにより、再び表示したくないシリーズをリストから削除できます。これは、リストに外国語のシリーズが含まれており、自分の母国語でこの映画を見つけることはほとんどなく、字幕付きで視聴したくない場合の例です。将来の追加を防ぐためにシリーズを除外できます。ただし、リストの除外セクションでは、リストに再度追加することができますので、リストが再実行されるとライブラリに読み込まれます。

# 接続

> サポートされている接続タイプの情報は、このセクションの[詳細情報（サポート）](/sonarr/supported#notifications)ページで確認できます
{.is-info}

## 接続

- 接続は、Sonarrが外部と通信する方法です。

- <kb>+</kb>ボタンを押すと、さまざまなエンドポイントを設定できる新しいウィンドウが表示されます。

- サポートされている通知と接続のリストは、[詳細情報（サポート）](/sonarr/supported#notifications)にあります。

## 接続トリガー

- 取得時 - エピソードがダウンロード可能になり、ダウンロードクライアントに送信されたときに通知を受け取る
- インポート時 - {以前のダウンロード時として知られています} エピソードが正常にインポートされたときに通知を受け取る
- アップグレード時 - エピソードがより高品質にアップグレードされたときに通知を受け取る
- 名前変更時 - エピソードが名前変更されたときに通知を受け取る
- シリーズ削除時 - シリーズが削除されたときに通知を受け取る
- エピソードファイル削除時 - エピソードファイルが削除されたときに通知を受け取る
- アップグレードのためのエピソードファイル削除時 - アップグレードのためにエピソードファイルが削除されたときに通知を受け取る
- ヘルスの問題時 - ヘルスチェックの失敗時に通知を受け取る
  - ヘルスの警告を含む - エラーに加えてヘルスの警告も通知を受け取る
- アプリケーションの更新時 - Sonarrが新しいバージョンに更新されたときに通知を受け取る

# メタデータ

## メタデータ

> サポートされているメタデータコンシューマの情報は、このセクションの[詳細情報（サポート）](/sonarr/supported#metadata)ページで確認できます
{.is-info}

- ここでは、メディアプレーヤーが消費するメタデータのタイプを選択できます。

- Kodiは、お使いのソフトウェアがそれである場合、ここで最も一般的に使用されるオプションの1つです。これにより、SonarrがNFOファイルを作成し、関連する映画のポスターをプレーヤーにスクレイピングすることができます。

# タグ

- Sonarrのタグセクションは、Sonarrのさまざまな側面をリンクするために使用されます。
- タグは、次のような場合に特に便利です。
  - 遅延プロファイル
  - リリースプロファイル
  - インデクサ
- タグは、遅延プロファイル、リリースプロファイル、インデクサ、およびシリーズをリンクするために使用できます。
- 例：
  - 特定のインデクサを特定のシリーズに使用したい場合、タグを作成し、そのタグにシリーズとインデクサを割り当てます。
  - 特定のリリースプロファイルが特定の遅延プロファイルのみを使用するようにしたい場合、タグを作成し、そのタグにリリースプロファイルと遅延プロファイルを割り当てます。

> シリーズは、タグが一致するインデクサとタグがないインデクサの両方を使用します。
{.is-warning}

> 注意：タグは、「含む必要がある」、「含まれてはならない」、「優先される」など、上記に記載されていない他の要素には影響しません。
{.is-info}

# 一般

## ホスト

- バインドアドレス - 有効なIPv4アドレスまたはすべてのインターフェースの'*'
  - 0.0.0.0または`*` - すべてのアドレスが接続できます
  - 127.0.0.1またはlocalhost - ローカルホストアプリケーションのみが接続できます
  - その他のIP（例：1.2.3.4） - そのIP（1.2.3.4）のみが接続できます
- ポート番号 - SonarrのWebUIにアクセスするために使用するポート番号

> 注意：Dockerを使用している場合は、この設定を変更しないでください。
{.is-warning}

- URLベース - リバースプロキシのサポートのため、デフォルトは空です

> 注意：リバースプロキシを使用している場合（例：mydomain.com/sonarr）、URLベースに'/sonarr'を入力します。
{.is-info}

- インスタンス名 - タブとSyslogアプリ名のインスタンス名

> 複数のインスタンスを実行している場合、これによりインスタンス名がWebブラウザのタブ名に追加されます。{.is-info}

- SSLを有効にする - SSLの資格情報を持っており、Sonarrとの通信を安全にする場合は、このオプションを有効にします。

> 注意：自己責任で使用してください。
{.is-warning}

## セキュリティ

- 認証 - Sonarrにアクセスするための認証方法を選択します
  - なし - Sonarrにアクセスするための認証はありません。通常、ネットワークの唯一のユーザーであり、Sonarrにアクセスするために誰もいないか、SonarrがWebに公開されていない場合に選択します
  - 基本認証（ブラウザのポップアップ） - Sonarrにアクセスする際に、ユーザー名とパスワードを入力する小さなポップアップが表示されます
  - フォーム（ログインページ） - このオプションを選択すると、Sonarrにログインするための一般的なログイン画面が表示されます
- APIキー - 他のプログラムがSonarrと通信したり、Sonarrが他のプログラムと通信するためのキーです。このキーがアクセス可能な誤った人に渡されると、ライブラリにさまざまな操作を行うことができます。このため、ログではAPIキーが伏せられます
- 証明書の検証 - HTTPS証明書の検証の厳密さを変更します
  - 有効 - すべてのHTTPS証明書を検証します（推奨）
  - ローカルアドレスの場合は無効 - localhostおよびLAN上のアドレスを除くすべてのHTTPS証明書を検証しません
  - 無効 - すべてのHTTPS証明書を検証しません

## プロキシ

- プロキシ - このオプションを使用すると、Sonarrが取得および検索する情報をプロキシ経由で実行できます。Torrentファイルのダウンロードが許可されていない国にいる場合に便利です。

- プロキシの使用 - プロキシを使用するには有効にします
- プロキシの種類 - プロキシの種類を選択します（HTTPS、Socks4、またはSocks5）
- ホスト名 - プロキシのホスト名を入力します（http/httpsやその他のプロトコルは含めないでください）
- ポート - プロキシのポートを入力します
- ユーザー名 - 適用される場合はプロキシのユーザー名を入力します
- パスワード - 適用される場合はプロキシのパスワードを入力します
- 無視するアドレス - プロキシをバイパスするアドレスのカンマ区切りのリストを入力します
- ローカルアドレスのプロキシをバイパスする - ローカルアドレスのプロキシをバイパスするには、チェックボックスをオンにします。ローカルリクエストは、URIにピリオド（.）が含まれていないことで識別されます。たとえば、<http://webserver/>、またはローカルサーバーにアクセスする場合は、<http://localhost>、<http://loopback>、または<http://127.0.0.1>です。チェックを外すと、すべてのインターネットリクエストがプロキシサーバーを介して行われます。

## ロギング

- ログレベル - おそらく最も便利なトラブルシューティングツールの1つ
  - 情報 - これはSonarrが情報を収集する最も基本的な方法で、ログには非常に少量の情報が含まれます。このログファイルには、致命的なエントリ、エラーエントリ、警告エントリ、情報エントリが含まれます。
  - デバッグ - デバッグには、情報に加えてさらに有用な情報が含まれます。このログファイルには、致命的なエントリ、エラーエントリ、警告エントリ、情報エントリ、デバッグエントリが含まれます。
  - トレース - Sonarrの最も詳細なログであり、情報とデバッグで収集された情報に加えて、さらに詳細な情報が含まれます。これは、DiscordやRedditでトラブルシューティングを行う際に要求される最も一般的なログのタイプです。ヘルプが必要な場合は、ログをトレースに設定し、問題が発生しているタスクをやり直してログをキャプチャするようにしてください。このログファイルには、致命的なエントリ、エラーエントリ、警告エントリ、情報エントリ、デバッグエントリ、トレースエントリが含まれます。

## アナリティクス

- アナリティクス - 匿名の使用状況およびエラー情報をSonarrのサーバー（SkyHook）に送信します。これには、ブラウザの情報、使用するSonarr WebUIページ、エラーレポート、OSおよびランタイムバージョンの情報が含まれます。この情報を使用して、機能とバグ修正の優先順位を決定します。

## 更新

- （高度なオプション）ブランチ - 実行しているSonarrのブランチです。
  - [詳細については、このFAQエントリを参照してください](/sonarr/faq#how-do-i-update-sonarr)
- 自動 - 更新を自動的にダウンロードしてインストールします。System: Updatesからもインストールできます。注意：Windowsユーザーは常に自動的に更新されます。
- メカニズム - Sonarrの組み込みの更新プログラムまたはスクリプトを使用します
  - 組み込み - Sonarr独自の更新プログラムを使用します
  - スクリプト - Sonarrに更新スクリプトを実行させます
  - Docker - Docker内部からSonarrを更新せず、新しい更新を持つ新しいイメージをプルします
  - Apt - 更新がAptを介して管理される場合にDebian/Ubuntuパッケージによって設定されます
- スクリプト - メカニズムがスクリプトに設定されている場合にのみ表示されます - 更新スクリプトへのパス
- 更新プロセス - Sonarrは更新ファイルをダウンロードし、その整合性を確認し、一時的な場所に展開し、選択したメソッドを呼び出します。更新プロセスは、Sonarrが実行されているユーザーと同じユーザーで実行されます。Sonarrファイルを更新するためのアクセス許可とSonarrの停止/開始が必要です。
- 組み込み - 組み込みの方法では、Sonarrファイルと設定をバックアップし、Sonarrを停止し、インストールを更新し、Sonarrを開始します。システムがSonarrの停止を処理できず、自動的に再起動しようとする場合は、代わりにスクリプトを使用することが最善です。失敗した場合、以前のバージョンのSonarrが再起動されます。
- スクリプト - スクリプトは組み込みの更新プログラムと同じように処理するはずです。サービスの停止と開始を処理する必要がある場合（upstart/launchdなど）、ここで行う必要があります。

## バックアップ

- バックアップセクションでは、Sonarrがバックアップをどのように処理するかを指定できます。

- フォルダー - バックアップの場所を選択できます。Dockerでは、コンテナが表示できるものに制限されます。パスはappdataフォルダに対して相対的です。必要に応じて、appdataフォルダの外部にバックアップするための絶対パスを設定できます。
- インターバル - Sonarrがバックアップを作成する頻度
- 保持期間 - 各バックアップを保持する期間。新しいバックアップが作成されると、最も古いバックアップが削除されます

# UI

## カレンダー

- 週の最初の日 - 週の最初の日を選択できます。
- 週の列ヘッダー - 列のヘッダーを選択できます

## 日付

- 短い日付形式 - Sonarrが短い日付を表示する方法を選択します。
- 長い日付形式 - Sonarrが長い形式の日付を表示する方法を選択します。
- 時間形式 - 12時間制または24時間制の形式を選択しますか？
- 相対日付の表示 - Sonarrが相対的な日付（今日/昨日など）または絶対的な日付を表示するかどうかを選択します。

## スタイル

- 色覚障害者モードを有効にする - 色覚障害のあるユーザーが色付きの情報をより明確に区別できるようにスタイルを変更します