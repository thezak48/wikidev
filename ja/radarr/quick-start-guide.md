---
title: Radarrクイックスタートガイド
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, クイックスタート
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# 目次

- [目次](#目次)
- [クイックスタートセットアップガイド](#クイックスタートセットアップガイド)
- [起動](#起動)
- [メディア管理](#メディア管理)
  - [映画の命名](#映画の命名)
  - [インポート](#インポート)
  - [ファイル管理](#ファイル管理)
  - [ルートフォルダ](#ルートフォルダ)
- [プロファイル](#プロファイル)
- [品質](#品質)
- [インデクサ](#インデクサ)
- [ダウンロードクライアント](#ダウンロードクライアント)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [既存の整理されたメディアライブラリのインポート方法](#既存の整理されたメディアライブラリのインポート方法)
  - [映画のインポート](#映画のインポート)
  - [既存のメディアのインポート](#既存のメディアのインポート)
    - [一致が見つからない場合](#一致が見つからない場合)
    - [インポート後のフォルダ名の修正](#インポート後のフォルダ名の修正)
  - [映画の追加方法](#映画の追加方法)

# クイックスタートセットアップガイド

> このページはまだ作成中であり、完全ではありません。貢献は歓迎します。

> すべての設定の詳細な説明については、[Radarr => 設定](/radarr/settings)を参照してください。
{.is-info}

このガイドでは、Radarrを始めるために必要な基本的なセットアップ方法を説明します。画面上で表示されるいくつかのオプションは省略します。これらについて詳しく知りたい場合は、FAQやドキュメントの適切なページを参照してください。

> スクリーンショットとGUI設定の`オレンジ`は高度なオプションです。これらを表示するには、ページの上部にある`詳細表示`をクリックする必要があります。
{.is-warning}

# 起動

インストールと起動後、ブラウザを開き、`http://{your_ip_here}:7878`にアクセスします。

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# メディア管理

まず、メディア管理の設定を見てみましょう。ここでは、好みの命名規則やファイル管理の設定を行うことができます。

`設定` => `メディア管理`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## 映画の命名

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. 映画の名前を変更するかどうかを有効化/無効化します（現在の名前のままにするか、ダウンロード時の名前のままにするか）。
2. 違法な文字を置換または削除するかどうか（`\ / : * ? " < > | ~ # % & + { }`）。
3. この設定によって、Radarrが映画ファイル内のコロンをどのように処理するかが決まります。
4. 実際の映画ファイルの命名規則を選択します。
5. *(高度なオプション) ビデオファイルを含むフォルダの命名規則を設定する場所です。*

> 推奨される命名規則と例については、[TRaSHの推奨命名規則](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/)を参照してください。
{.is-info}

## インポート

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(高度なオプション) `コピー`の代わりに`ハードリンク`を使用する場合の詳細については、[TRaSHのハードリンクガイド](https://trash-guides.info/hardlinks)を参照してください。
1. *(高度なオプション) ファイルのインポート後に一致する追加ファイル（字幕、nfoなど）をインポートする場合は、ここを有効にします。

## ファイル管理

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. ディスクから削除された映画は、Radarrで自動的に監視解除されます。
    - 映画を削除したいが、Radarrに再ダウンロードさせたくない場合にこのオプションを使用します。
1. *(高度なオプション) 削除されたファイルが保存される場所を指定します（ゴミ箱が回収される前に取り出したい場合など）。
1. *(高度なオプション) ファイルが永久に削除される前にどれくらい古くなるかを設定します。

## ルートフォルダ

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

ここで、Radarrが既存の整理されたメディアライブラリをインポートするために使用するルートフォルダを追加し、ダウンロードクライアントがダウンロードしたメディアをインポート（コピー/ハードリンク/移動）する場所を指定します。

> \* Windows以外の場合：NFSマウントを使用している場合は、`nolock`が有効になっていることを確認してください。
> \* SMBマウントを使用している場合は、`nobrl`が有効になっていることを確認してください。
{.is-warning}

> **Radarrの実行に設定したユーザーとグループは、この場所に対して読み取りと書き込みのアクセス権を持っている必要があります。** {.is-info}

> ダウンロードクライアントはダウンロードフォルダにダウンロードし、Radarrはメディアフォルダ（最終目的地）にインポートします。これはメディアサーバーが使用する場所です。
{.is-info}

> **ダウンロードフォルダとメディア（ライブラリ/ルート）フォルダは同じ場所にすることはできません。**
{.is-danger}

変更を保存するのを忘れないでください。

# プロファイル

`設定` => `プロファイル`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

ここでは、映画の品質、好みの言語、およびカスタム形式のスコアリングに対してプロファイルを設定できます。

自分自身のプロファイルを作成し、実際に必要な品質ソースと言語のみを選択することをお勧めします。

外国のタイトルと言語についての詳細については、[このFAQエントリ](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)を参照してください。

多くのユーザーは、[TRaSHのカスタム形式言語ガイド](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats)が役立つと考えています。これにより、希望する映画の言語を指定できます。

プロファイルはカスタム形式スコアも設定できます。不要なダウンロードを避けるために、以下のカスタム形式を[TRaSHのガイド](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)から追加することを強くお勧めします。詳細については、リンク先のTRaSHガイドカスタム形式記事と、カスタム形式のコレクションページの上部にある3つの参照先のTRaSHカスタム形式ガイドを参照してください。

- [DV（WEB-DL）](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl)は、DV（Dolby Vision）をサポートしていない場合に緑色の色調があるDVリリースを取得しないようにします。
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk)は、BR-DISKの品質解析に一致しない名前のBR-DISKを取得しないようにします。

> 詳細は[設定 => プロファイル](/radarr/settings#profiles)を参照してください。
> 品質ソースの違いについては、[品質の定義](/radarr/settings#qualities-defined)を参照してください。
{.is-info}

# 品質

`設定` => `品質`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

ここでは、希望するメディアファイルの最小および最大サイズを変更/微調整できます（Usenetを使用する場合はRAR/PAR2ファイルに注意してください）。

> 品質設定に何を使用するかについてのヘルプが必要な場合は、[TRaSHのサイズの推奨事項](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/)を参照して、テスト済みの例を確認してください。
{.is-info}

# インデクサ

`設定` => `インデクサ`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

ここでは、実際にファイルをダウンロードするために使用するインデクサ/トラッカーを追加します。

新しいインデクサを追加するために<kb>+</kb>ボタンをクリックすると、さまざまなオプションが表示されるウィンドウが表示されます。このWikiでは、UsenetインデクサとTorrentトラッカーの両方を「インデクサ」として扱います。

ここには2つのセクションがあります：UsenetとTorrents。使用するダウンロードクライアントに基づいて、使用するインデクサのタイプを選択する必要があります。

トレントトラッカーの場合、ほとんどの場合、[Prowlarr](/prowlarr)または[Jackett](https://github.com/Jackett/Jackett)の使用が必要です。

# ダウンロードクライアント

`設定` => `ダウンロードクライアント`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

ダウンロードとインポートは、ほとんどの人が問題を抱える場所です。大まかな視点から言えば、ソフトウェアはダウンロードクライアントと通信できるようにする必要があり、ダウンロードクライアントが報告するファイルの場所に読み取りと書き込みのアクセス権を持つ必要があります。サポートされているダウンロードクライアントはさまざまで、さらにさまざまなセットアップがあります。つまり、一般的なセットアップがいくつかあるものの、正しいセットアップはなく、すべてのセットアップは少し異なる場合があります。ただし、間違ったセットアップは多数存在します。

> 詳細については、[設定ページ](/radarr/settings#download-clients)、[詳細情報（サポートされている）](/radarr/supported#download-clients)ページ、および[TRaSHのダウンロードクライアントガイド](https://trash-guides.info/Downloaders/)を参照してください。
{.is-info}

## ダウンロードプロトコル {.tabset}

### Usenet

{#usenet}

- Radarrは、クライアントにダウンロードリクエストを送信し、ダウンロードクライアントの設定で構成したラベルまたはカテゴリ名と関連付けます。
  - 例：movies、tv、series、musicなど。
- Radarrは、そのカテゴリ名を使用してダウンロードクライアントのアクティブなダウンロードを監視します。これは、ダウンロードクライアントのAPIを介して監視されます。
- ダウンロードが完了すると、Radarrはダウンロードクライアントが報告する最終ファイルの場所を把握します。このファイルの場所は、メディアフォルダとは別の場所であればどこでも構いませんが、Radarrからアクセスできる必要があります。
- Radarrは、完了したファイルの場所をスキャンし、Radarrが使用できるファイルを検出します。ファイル名を解析して要求されたメディアと一致させることができれば、指定された仕様に従ってファイル名を変更し、指定されたメディアの場所に移動します。
- アトミックムーブ（インスタントムーブ）はデフォルトで有効になっています。ファイルシステムとマウントは、完了したダウンロードディレクトリとメディアライブラリで同じである必要があります。アトミックムーブが失敗するか、セットアップがハードリンクとアトミックムーブをサポートしていない場合、Radarrはファイルをコピーしてからソースから削除するか、IOが集中する場合にフォールバックします。
- Radarrの設定で「完了したダウンロードの処理 - 削除」オプションが有効になっている場合、ダウンロードから残されたファイルは、クライアントに削除/削除リクエストを送信してゴミ箱またはリサイクルに送信されます。

### BitTorrent

{#bittorrent}

- Radarrは、クライアントにダウンロードリクエストを送信し、ダウンロードクライアントの設定で構成したラベルまたはカテゴリ名と関連付けます。
  - 例：movies、tv、series、musicなど。
- Radarrは、そのカテゴリ名を使用してダウンロードクライアントのアクティブなダウンロードを監視します。この監視は、ダウンロードクライアントのAPIを介して行われます。
- シーディング中の完了したダウンロードは、ファイルを元の場所に残しておくことで、ファイルをシードできるようにします（ダウンロードクライアントまたはRadarr内の特定のダウンロードクライアントの内部から、比率または時間を調整できます）。メディアフォルダにインポートされると、Radarrはサポートされている場合はハードリンクを作成し、サポートされていない場合はコピーします。一時停止され、シーディングが完了したトレントは、ハードリンクがサポートされている場合はアトミックムーブされ、サポートされていない場合はコピー+削除されます。
- ハードリンクはデフォルトで有効になっています。[ハードリンクを使用すると、追加のディスクスペースを使用しません。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)ファイルシステムとマウントは、完了したダウンロードディレクトリとメディアライブラリで同じである必要があります。ハードリンクの作成に失敗するか、セットアップがハードリンクをサポートしていない場合、Radarrはファイルをコピーします。
- Radarrの設定で「完了したダウンロードの処理 - 削除」オプションが有効になっている場合、Radarrはクライアントからトレントを削除し、クライアントにトレントデータの削除を要求しますが、クライアントがシーディングが完了し、トレントが停止（完了時に一時停止）されていると報告する場合のみです。

# 既存の整理されたメディアライブラリのインポート方法

> Radarrは定期的に映画を検索しません。Radarrの動作については、[Radarrの動作方法？](/radarr/faq#how-does-radarr-work)のFAQエントリを参照してください。
{.is-info}

プロファイル/品質サイズの設定を行い、インデクサとダウンロードクライアントを追加したら、既存の整理されたメディアライブラリをインポートする準備が整いました。

`映画`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

`既存の映画のインポート`を選択するか、サイドバーから`インポート`を選択します。

## 映画のインポート

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

以前に[ルートフォルダセクションで追加したルートパス](#ルートフォルダ)を選択します。

## 既存のメディアのインポート

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

既存の映画フォルダの命名がどれほど正確かによって、Radarrは正しい映画と一致させようとします（Nr.5で表示されるように）。すべての映画が単一のディレクトリにある場合は、この[ガイド](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)に従ってください。

1. 映画のフォルダ名。
1. 監視 - 映画をRadarrに追加する方法。

- なし - 映画やコレクションの新しいリリースを監視しない
- 映画のみ - 映画の新しいリリースのみを監視する
- 映画とコレクション - 映画の新しいリリースを監視し、映画のコレクション（存在する場合）の映画を追加して監視する

1. 利用可能性 - Radarrが映画が利用可能と見なすタイミング。

- **発表済み**：Radarrは、映画がRadarrに追加されたときに利用可能と見なします。この設定は、フェイクがない優れたプライベートトラッカーを持っている場合に*推奨*されます。
- **公開中**：Radarrは、映画が映画館に公開されたときに利用可能と見なします。このオプションは*推奨されません*。
- **リリース済み**：Radarrは、Blu-rayがリリースされたときに映画が利用可能と見なします。このオプションは、インデクサに頻繁にフェイクが含まれる場合に*推奨*されます。

1. 品質プロファイル - 使用する希望のプロファイルを選択します。
1. 映画 - Radarrが一致したと思われる映画です。これを確認し、一致が正しくない場合は編集/検索して修正する必要があります。一致が正しくない場合は、フォルダ名が正しくないことが原因です。
1. モニターステータスを一括選択します。
1. 最小利用可能性を一括選択します。
1. 品質プロファイルを一括選択します。
1. 既存のメディアライブラリをインポートを開始します。

映画がRadarrに追加されると、Radarrは映画のフォルダをスキャンし、フォルダ内のビデオファイルを映画と一致させようとします。Radarrがファイルと映画を一致させない最も一般的な原因は、ファイル名に年が含まれていないことです。Radarrは、ファイル名を解析するためにファイル名に年が必要です。  

### 一致が見つからない場合

次のようなエラーが表示される場合は、

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

おそらく映画フォルダの命名に誤りがあります。

この問題を修正するには、次の手順を試すことができます。

エラーメッセージを展開します

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

そして、[themoviedb](https://www.themoviedb.org/)で年またはタイトルが一致するかどうかを確認します。この例では、年が間違っていることがわかり、年を変更してリフレッシュアイコンをクリックして修正できます。

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

または、tmdb:idまたはimdb:id（tmdbがimdbにリンクされている場合）を使用し、一致した場合に見つかった映画を選択することもできます。

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### インポート後のフォルダ名の修正

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

インポート中に修正を行った後、フォルダ名がまだ間違っていることに気付くでしょう。これを修正するために、少しマジックを使います。

映画の概要に移動します

`Movies`

上部で`Movie Editor`をクリックします

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

有効にした後、フォルダ名を変更したい映画を選択します。

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. フォルダ名を以前に設定したフォルダ命名スキームに変更する場合は、すべての映画フォルダを選択します [映画の命名セクション](#movie-naming)。
2. フォルダ名を変更したい映画を選択します。
3. 同じ`Root Folder`を選択します。

新しいポップアップが表示されます

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

`Yes, Move the files`を選択します

そしてマジック

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

フォルダが正しい年にリネームされ、命名スキームに従っています。

## 映画の追加方法

整理されたメディアライブラリをインポートした後、追加したい映画を追加する時間です。

`Movies` => `Add New`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

ボックスに追加したい映画の名前を入力するか、tmdb:idまたはimdb:idを使用します。

映画名を入力すると、結果が表示され始めることがわかります。

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

追加したい映画が表示されたら、それをクリックします。

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. Root Folder - Radarrは、[ルートフォルダのセクション](#root-folders)で設定したルートフォルダに映画を追加します。
2. Monitor - Radarrに映画を追加する方法です。

- Movie Only = Radarrは、ライブラリ内にまだ存在しない映画をRSSフィードで監視し、または既存の映画をより高品質なものにアップグレードします。
- Movie & Collection = Radarrは、ライブラリ内にまだ存在しない映画をRSSフィードで監視し、または既存の映画をより高品質なものにアップグレードします。また、この映画のコレクション（ある場合）のすべての映画を選択した設定で追加します。
- None = RadarrはRSSフィードを監視せず、アップグレードや新しい映画は無視され、手動で行う必要があります。監視されていない映画のすべての検索は、手動でトリガーされる検索または対話型検索で行う必要があります。

1. Availability - Radarrが映画が利用可能と見なすタイミングです。

> 以下の利用可能性に影響を与えるTMDBの日付に関する詳細は、[Radarrが映画の年をどのように決定するか](#how-does-radarr-determine-the-year-of-a-movie)を参照してください。
{.is-info}

- **Announced**: Radarrは、映画がRadarrに追加されたときに利用可能と見なします。この設定は、フェイクがない良いプライベートトラッカー（または本当に良いパブリックトラッカー、例：rarbg.to）を持っている場合に推奨されます。
- **In Cinemas**: Radarrは、映画が映画館に上映された直後（TMDbの劇場公開日）に利用可能と見なします。このオプションはお勧めしません。
- **Released**: Radarrは、Blu-Rayやストリーミング版がリリースされた直後（TMDbのデジタルおよび物理的な日付）に映画が利用可能と見なします。このオプションは推奨され、通常は利用可能性の遅延に`-14`または`-21`日を組み合わせる必要があります。
  - TMDbに日付が入力されていない場合、劇場公開日（劇場で最も古い日付）から90日後に映画がウェブまたは物理的なサービスで利用可能と見なされます。

1. Quality Profile - この映画に使用するプロファイルを選択します。
1. Tags - ここでは、高度な使用のために特定のタグを追加できます。
1. Search on Add - 追加時にRadarrが欠落している映画を検索する場合は、これを有効にしてください [詳細はこちら](/radarr/faq#how-does-radarr-find-movies)
1. `Add Movie`をクリックして映画をRadarrに追加します。

- "path is already configured"というエラーが表示される場合は、[このFAQエントリー](/radarr/faq#path-is-already-configured-for-an-existing-movie)を参照してください。