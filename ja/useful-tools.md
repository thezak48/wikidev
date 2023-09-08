---
title: 便利なツール
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: useful-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# 目次

- [目次](#目次)
- [データベースの回復](#データベースの回復)
  - [データベースの回復（UI）（Windows）](#データベースの回復uiwindows)
  - [コマンドラインでのデータベースの回復](#コマンドラインでのデータベースの回復)
- [クッキーの検索](#クッキーの検索)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [クッキーとローカルストレージのクリア](#クッキーとローカルストレージのクリア)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge（Chromium）](#microsoft-edge-chromium)
{.links-list}
- [その他のプロジェクトとプログラム - リクエストアプリ \*Arrs](#その他のプロジェクトとプログラム-リクエストアプリ-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
{.links-list}
- [その他のプロジェクトとプログラム - \*Arr 関連](#その他のプロジェクトとプログラム-arr-関連)
  - [リモートコントロール](#リモートコントロール)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Android アプリ](#radarr-sonarr-companion-android-アプリ)
    - [nzb360 - Android アプリ](#nzb360-android-アプリ)
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [字幕](#字幕)
    - [Bazarr](#bazarr)
{.links-list}
- [その他のプロジェクトとプログラム - トレント/ダウンロード](#その他のプロジェクトとプログラム-トレントダウンロード)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit Management](#qbit-management)
{.links-list}
- [その他のプロジェクトとプログラム](#その他のプロジェクトとプログラム)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
{.links-list}
- [Twitter Connect の手順](#twitter-connect-の手順)

以下のアプリは、\*Arr Suite of Applicationsやメディアの保管に関連するものです。これらは\*Arr開発チームによってメンテナンス、開発、サポートされていません。具体的なサポートについては、各アプリケーションの開発チームにお問い合わせください。

# データベースの回復

アプリケーションのデータベースは、以下にリンクされているアプリケーションデータディレクトリにあります。ディレクトリはdatadir引数として渡すこともできます。

- [Lidarr アプリデータディレクトリ](/lidarr/appdata-directory)
- [Prowlarr アプリデータディレクトリ](/prowlarr/appdata-directory)
- [Radarr アプリデータディレクトリ](/radarr/appdata-directory)
- [Readarr アプリデータディレクトリ](/readarr/appdata-directory)
- [Sonarr アプリデータディレクトリ](/sonarr/appdata-directory)
{.links-list}

> 以下にデータベースを回復するための2つのオプションがあります。{.is-info}

- [DB Browser for SQLiteとUIを使用する方法](#データベースの回復ui)
- [Sqliteの`.recover`関数を使用する方法](#コマンドラインでのデータベースの回復)
{.links-list}

## データベースの回復（UI）（Windows）

{#windows}
{#データベースの回復ui}

> これは、Sqlite v3.29が必要な`.recover`と同じ効果を持つものです。`.recover`コマンドの詳細については、[Sqliteのドキュメントを参照してください](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database)。手順は以下のリンク先にあります{.is-info}

> [DB Browser for SQLite（DB4S）](https://SQLitebrowser.org/)は、SQLiteと互換性のあるデータベースファイルを作成、設計、編集するための高品質でビジュアルなオープンソースツールです。DB4Sは、データベースの作成、検索、編集を行いたいユーザーや開発者向けに、使い慣れたスプレッドシートのようなインターフェースを使用し、複雑なSQLコマンドを学ぶ必要はありません。
{.is-info}

1. アプリケーションを停止します。
1. 破損したデータベース（`.db`）のコピーを作成し、それに`.shm`および`.wal`ファイルをコピーします。
1. [DB Browser for SQLite（DB4S）](https://SQLitebrowser.org/)で破損したデータベースを開きます。
1. ファイル => エクスポート => SQLファイルにデータベースをエクスポートします。
1. すべてのテーブルを選択します。
1. "INSERT INTOで列名を保持する"をチェック/有効にします。
1. すべてをエクスポートします。
1. 古いスキーマを上書きします。
1. 保存します。
1. データベースを閉じます。
1. 新しいデータベース => ファイル => インポート => 前のエクスポート手順で作成したファイルをインポートします。
1. インポートエラーまたは制約の問題がある場合は、可能な限り問題のある挿入ステートメントを修正するか、削除します。
1. 次のSQLを実行します：`VACUUM;`
1. プロンプトが表示されたら、データベースを保存します。
1. ツール => 整合性のチェック。結果はOKと表示されるはずです。
1. データベースを閉じます。
1. 設定フォルダからすべての`wal`、`shm`、`db`ファイルを削除します。
1. （\*ArrがDB4Sと同じシステム上にない場合は）新しいデータベースを設定フォルダに保存（またはコピー）し、アプリケーションにポイントします。すべての\*Arrは、データベースを`<appname>.db`という名前で保存します（例：`radarr.db`）。
1. 必要に応じて、回復したデータベースのアクセス許可を正しく設定します。所有者は、\*Arrが実行されるように構成されているユーザーとグループである必要があります。
1. アプリケーションを起動します。

なお、gifには`VACUUM;`コマンドは含まれていません。

![dbrecover.gif](/dbrecover.gif)

## コマンドラインでのデータベースの回復

{#nix}

以下の手順は\*Nixオペレーティングシステム用ですが、Windowsコマンドラインでも同様の概念が適用されます。

> これには、[sqlite3の`.recover`コマンド](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database)が理想的です。ただし、Sqlite 3.29以上が必要です。
{.is-info}

> \*Arrsでsqlite3が必要なので、システムにsqlite3がインストールされていることを前提としています。{.is-info}

1. アプリケーションを停止します。
1. ボックスにSSHで接続するか、シェルを起動します。
1. `sqlite3 <path to bad database> ".recover" | sqlite3 <output path for recovered database>"`と入力します。
1. 必要に応じて、回復したデータベースのアクセス許可を正しく設定します。所有者は、\*Arrが実行されるように構成されているユーザーとグループである必要があります。
1. 古い破損したデータベースとフォルダ内の`wal`または`shm`を削除または移動/名前変更します。
1. 回復したデータベースの名前を変更します。すべての\*Arrは、データベースを`<appname>.db`という名前で保存します（例：`radarr.db`）。
1. アプリケーションを起動します。

# クッキーの検索

- 一部のサイトは自動的にログインできず、手動でログインしてからクッキーを提供する必要があります。以下のページでは、その方法について説明しています。

## 一般的な手順

1. ブラウザを使用して、Prowlarrインデクサの設定で使用するサイトリンクアドレスでWebサイトにログインします。
1. F12キーを押してDevToolsパネルを開きます。
1. ネットワークタブを選択します。
1. ドキュメントボタン（Chromeブラウザ）またはHTMLボタン（Firefoxブラウザ）をクリックします。
1. F5キーを押してページを更新します。
1. 最初の行エントリをクリックします。
1. 右側のパネルでヘッダータブを選択します。
1. リクエストヘッダーセクションで 'cookie:' を検索します。トラッカーのヘルプテキストを参照して詳細を確認してください。
1. クッキー文字列全体（cookie: の後のすべて）を選択してコピーします。
1. Prowlarrインデクサのクッキーボックスにすでに何かがある場合は、それを削除します。
1. コピーしたクッキー文字列をそのボックスに貼り付けます。
1. 保存をクリックします。

> トラッカーにユーザーエージェントが必要な場合は、リクエストヘッダーにあります。
{.is-info}

### ノート

- Prowlarrを実行しているマシンと同じマシンからブラウザを使用することを確認してください。クッキーは他のプラットフォームからはほとんど機能しません。
- Webサイトのログインページでは、セッションを1つのIPアドレスに制限するオプションをチェックしないでください。また、短時間後にログアウトするオプションもチェックしないでください。Remember me オプションがある場合は使用してください。
- クッキーを使用した後、サイトのトレント検索ページにアクセスできることを確認してください。サイトがこれを防止するために行うすべての操作（アラート、未読の通知または未読のPM、または低い比率の警告など）は、クッキーを使用した後のProwlarrのテストを成功させるのを妨げます。

## Chrome

- トレントトラッカーウェブサイトに移動してログインします。

- F12キーを押します。

- 上部のアプリケーションタブに「ストレージ」という項目があります。左側に「クッキー」というサブセクションが表示され、その下にトラッカーのURLが表示されます。それをクリックします。

- そのタブまたは類似のエントリの「Pass」をクリックすると、「Cookie Value」というボックスが表示され、25〜30文字程度の文字列が表示されます。それをコピーして必要なアプリケーションに貼り付けます。

  - 文字列が`cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser`に似ている場合、エントリ全体を使用する必要があります。

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- Chromeのドキュメント[Chrome cookies](https://developer.chrome.com/docs/devtools/storage/cookies/)も参照できます。

## Firefox

- [Mozillaのドキュメントを参照してください](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# クッキーとローカルストレージのクリア

## Chrome

1. `chrome://settings/siteData`に移動します。
1. クリアしたいサイト（またはアプリ）の名前を入力します。
1. サイトの横にあるゴミ箱アイコンをクリックします。

## Firefox

- [Mozillaのヘルプ記事を参照してください](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)

## Microsoft Edge（Chromium）

1. `edge://settings/siteData`に移動します。
1. クリアしたいサイト（またはアプリ）の名前を入力します。
1. サイトの矢印をクリックします。
1. サイトの横にあるゴミ箱アイコンをクリックします。

# その他のプロジェクトとプログラム - リクエストアプリ \*Arrs

## Notifiarr（旧称 Discord Notifier）

[Notifiarr](https://notifiarr.com/)は、\*Arr開発者の1人によって作成されたツールで、より詳細なDiscord通知を提供します。トリガーに基づいて通知（リアクションを含む）を追加するための設定可能な方法を提供します。Grab、Import、Upgrade、Health、Failedの通知に対応しています。

[Wiki](https://notifiarr.wiki/)

ハイライト

- アプリケーションのステータス
- リクエストと承認（\~Ombi）
- カスタマイズ可能な\*ARRアプリケーションの通知
- 承認付きのリクエストシステム
- シリーズや映画をモニターし、通知を受け取るためのフォローシステム（@mentionsを使用）
- サーバーステータス
- 頻繁な新機能

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/)は、ユーザーが映画、テレビ番組（シリーズ、シーズン、または単一のエピソード）、音楽アルバムをリクエストできるようにする機能を提供します。

## Overseerr

[Overseerr](https://overseerr.dev/)は、既存のPlexエコシステムと連携するために作成されたリクエスト管理およびメディアディスカバリーツールです。

## Petio

[Petio](https://petio.tv/)は、Plexサーバーの所有者がユーザーにコンテンツのリクエスト、レビュー、および発見を許可するためのサードパーティのコンパニオンアプリです。

このアプリは、最もテクノロジーアグノスティックなユーザーにもすぐに馴染み、直感的に感じるように作られています。Petioは、ユーザーからのリクエストを管理し、SonarrやRadarrなどのサードパーティのアプリに接続し、コンテンツが利用可能になったときにユーザーに通知し、リクエストの進行状況を追跡します。Petioはまた、ユーザーがサーバー内外のメディアを発見し、関連コンテンツを簡単かつ迅速に見つけ、他のユーザーに対して意見を残すためのレビューを行うこともできます。

# その他のプロジェクトとプログラム - \*Arr 関連

## リモートコントロール

### LunaSea

[LunaSea](https://www.lunasea.app/)は、完全な機能を備えたオープンソースのセルフホスト型コントローラーです。セルフホスト型のメディアソフトウェア間でシームレスなエクスペリエンスを提供することに重点を置いています。

### Radarr & Sonarr Companion - Android アプリ

電話で簡単に新しい映画/番組をシステムに追加できます。アプリは[Google Play](https://play.google.com/store/apps/details?id=easy.radarr)で利用できます。

### nzb360 - Android アプリ

nzb360は、Sonarr、Radarr、Lidarr、トレント、Usenetなどのサービスの管理を提供します。アプリは[Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360)で利用できます。詳細については、[公式ウェブサイト](https://nzb360.com/)をご覧ください。

## Lidarr

### AMD

[Automated Music Downloader](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amdは、Lidarrのコンパニオンスクリプトで、Lidarrのために音楽を自動的にダウンロードします。

### AMVD

[Automated Music Video Downloader](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvdは、Lidarrのコンパニオンスクリプトで、他のビデオアプリケーション（plex/kodi/jellyfin/emby）で使用するために、音楽ビデオを自動的にダウンロードしてタグ付けします。

## Radarr

## AMTD

[Automated Movie Trailer Downloader](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtdは、Radarrのコンパニオンスクリプトで、他のビデオアプリケーション（plex/kodi/jellyfin/emby）で使用するために、映画の予告編とエクストラを自動的にダウンロードします。

## 字幕

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr)は、SonarrとRadarrのコンパニオンアプリケーションで、要件に基づいて字幕を管理およびダウンロードします。

# その他のプロジェクトとプログラム - トレント/ダウンロード

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed)は、既存のトレントに基づいてクロスシードできるトレントをダウンロードするのを支援するアプリです。手動の介入を最小限に抑えるために、保守的に一致させるように設計されています。現時点では、JackettとQbittorrent/rTorrentをサポートしています。

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr)は、Starrアプリケーションの問題を修正するためのユーティリティスイートを提供します。Toolbarrを使用すると、StarrアプリケーションとそのSQLite3データベースに対してさまざまな操作を実行できます。

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr)は、ダウンロードホストでデーモンとして実行されるアプリケーションです。完了したダウンロードをチェックし、\*Arrがそれをインポートできるように展開します。

ダウンロードクライアントがファイルをダウンロードした後、それらを抽出し、インポートされた後にメッセを片付けるためのオプションはいくつかあります。Captainはそれらのいずれも気に入らなかったので、自分で作りました。彼は、手動の介入を最小限に抑え、インポート後の混乱を片付けるための合理的なログを持つ小さな単一のバイナリを望んでいました。

## qBit Management

[qBit Management（または "qbit_manage"）](https://github.com/StuffAnThings/qbit_manage)は、qBittorrentインスタンスを管理するためのプログラムです。以下の操作を実行できます。



- トラッカーのURLに基づいてトレントにタグを付ける（タグのないトレントのみにタグを付ける）
- 保存ディレクトリに基づいてカテゴリを更新する
- 未登録のトレントを削除する（データとトレントを削除するが、クロスシードされていない場合のみ。それ以外の場合はトレントのみを削除する）
- 一時停止状態のままクロスシードトレントを自動的に追加する（[クロスシードスクリプト](#cross-seed)と併用する）
- サイズが最小の一時停止トレントを再チェックし、完了している場合は再開する
- qBittorrentによって参照されていないルートディレクトリの孤立したファイルを削除する
- ハードリンクを持たないトレントにタグを付け、最大比率と/またはシード時間に基づいてこれらのトレントと内容をオプションで削除するためのクリーンアップを許可する

# その他のプロジェクトとプログラム

## Filebot

[FileBot](https://www.filebot.net/)は、映画、テレビ番組、アニメの整理とリネーム、字幕とアートワークの取得に最適なツールです。スマートで使いやすいです。

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes)は、重複ファイルを特定し、それに対してアクションを実行するためのプログラムです。

> TRaSHにも[ガイド](https://trash-guides.info/jdupes)があります {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= これにより、重複ファイルがチェックされ、結果の要約が表示されます

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= これにより、重複したファイルがハードリンクとして再作成され、使用される重複領域が減少します

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md)は、Radarr/Sonarrメディアライブラリに特定のタグが付いていないn個のアイテムを手動で検索するためのPowerShellスクリプトです。nはこのスクリプトが検索するアイテムの数であり、これによりインデクサを過負荷にすることなく、禁止されることなく検索できるという利点があります :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager)は、映画、番組、コレクションのメタデータ情報を更新し、自動的にコレクションを作成するためのPythonスクリプトです。

## Tautulli

[Tautulli](https://tautulli.com/)は、Plexメディアサーバーと一緒に実行できるサードパーティのアプリケーションで、アクティビティを監視し、さまざまな統計情報を追跡することができます。最も重要な統計情報には、何が視聴されたか、誰が視聴したか、いつ、どこで、どのように視聴されたかが含まれます。ただし、「なぜそれを見たのか」という情報は欠落していますが、あなたが「アナと雪の女王」を42回再生した理由を疑問視する私は誰でしょうか。すべての統計情報は、見やすくてきれいなインターフェースで表示され、多くのテーブルやグラフで提供されるため、他の人にサーバーの自慢をするのが簡単です。

## Tdarr

[Tdarr](https://tdarr.io)は、メディアライブラリのトランスコード/リムックス管理を自動化し、ファイルがコーデック/ストリーム/コンテナなどの要件に完全に合致するようにするためのクローズドソースのセルフホスト型Webアプリです。[Sonarr](/sonarr)/[Radarr](/radarr)と連携して動作するように設計され、モジュール化、並列化、スケーラビリティを目指して構築されています。追加するライブラリごとに独自のトランスコード設定、フィルタ、スケジュールがあります。必要に応じてワーカーを起動および終了でき、3つのタイプ（「一般」「トランスコード」「ヘルスチェック」）に分割されます。ワーカーの制限はスケジューラによって管理されるだけでなく、手動でも管理できます。

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform)は、ファイルシステムのイベントや頻繁なディスクスキャンに頼らずに、SonarrとRadarrに新しい/変更された/削除されたファイルの情報を通知するためのカスタムスクリプトです。

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr)は、Plex/Sonarr/Radarrから古くなったメディアや非アクティブなメディアを削除するためのツールです。Overseerr/Ombiを介してユーザーが番組をリクエストできるようにしておきながら、利用可能なディスク容量を手動で監視する必要はありません。定義した基準に合致するメディアのみを削除するように設定できます。

## Twitter Connect

<https://apps.twitter.com/>でTwitterアプリケーションを作成します（まだ作成していない場合）。

必須フィールドとコールバックURLを入力し、パブリックにアクセス可能なURL（localhostではない）に設定します。存在する必要はありませんが、設定する必要があります。[https://sonarr.tv/twitter](https://sonarr.tv/twitter)または[https://radarr.video](https://radarr.video)を使用することで十分です。