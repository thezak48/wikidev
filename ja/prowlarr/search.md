---
title: Prowlarrの検索
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

このページでは、Prowlarr内での検索方法を紹介します。通常、検索はアプリを介して行われますが、Prowlarr内でも直接検索することができます。

# 検索の実行

検索を開始するには、左側のメニューで「検索」をクリックします。画面下部にいくつかのオプションが表示されたほぼ空のページが表示されます。

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- クエリ - クエリフィールドに検索語を入力します。
  - 検索タイプを変更するには、虫眼鏡アイコンをクリックします。利用可能なオプションは次のとおりです。
    - 基本検索 - 基本的なテキストクエリ
    - TV検索 - TVパラメータを使用した検索（TVDbId、IMDbId、TMDbIDなど）およびシーズン/エピソード検索
    - 映画検索 - 映画パラメータを使用した検索（TMDbId、IMDbId、ジャンルなど）
    - オーディオ検索 - 音楽パラメータを使用した検索（アーティスト、アルバム、レーベル、ジャンルなど）
    - 書籍検索 - 書籍パラメータを使用した検索（著者、タイトルなど）

> これらは一般的に`{VariableName:SearchValue}`という形式でフォーマットされます。たとえば、「The Simpsons Season 32」のTV検索の場合、検索入力は`{TvdbId:71663} {Season:32}`となります。
{.is-info}

> すべてのインデクサがすべてのクエリタイプをサポートしているわけではないことに注意してください。
{.is-info}

- インデクサ - インデクサのドロップダウンからインデクサを選択します。自動的にカテゴリ「Usenet」または「Torrents」のすべてのインデクサを選択するか、任意のグループから特定のインデクサを選択することもできます。
- カテゴリ - インデクサで検索するカテゴリをドロップダウンから選択します。トップレベルのカテゴリ（TV、映画など）を選択すると、サブカテゴリが自動的にすべて選択されます。また、任意のグループから特定のカテゴリを選択することもできます。

その後、「検索」ボタンをクリックします。結果が表示されるまで数秒かかる場合があります。結果が表示されたら、「オプション」ボタンを使用して列を追加または削除できます。また、列ヘッダをクリックするか、「フィルター」ボタンを使用して結果をソートおよびフィルタリングすることもできます。

結果をダウンロードするには、結果の右側にあるダウンロードアイコンをクリックします。これにより、構成済みの適切なダウンロードクライアントに送信されます。

左側の選択ボックスをチェックし、「リリースを取得」ボタンをクリックすることで、一度に複数の結果を一括で取得することもできます。

> ダウンロードされるものは、Prowlarrで設定したカテゴリの割り当てを持っています。これには、アプリプログラムで非標準のディレクトリからの手動インポートが必要な場合があります。
{.is-info}

# APIエンドポイント

## RSS互換 - シングルインデクサフィード

- 標準のNewznab/Torznab互換のエンドポイント/パラメータ。定義された標準に従って必要に応じてクエリを調整できます。

> 複数のインデクサをまとめたエンドポイントは、その機能の重大な欠点のため追加されません。
{.is-info}

### クエリ内のAPIキー

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - 例: `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={yourkey}&cat=5000,2000`

### ヘッダ内のAPIキー

> ヘッダとしてAPIキーを渡すために`X-Api-Key`を必ず渡してください。
{.is-info}

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - 例: `http://192.168.1.100:9696/{indexerid}/api?t=search&q=mike&cat=5000,2000`

## 検索フィード

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/api/v1/search?query={encoded term}&indexerIds={comma separated list}&categories={comma separated list}&type={searchtype}`
  - 例: `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - 例: `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

パラメータ

- `query` - URLエンコードされた検索文字列
- `indexerIds` - インデクサIDのカンマ区切りリスト
  - すべてのインデクサの場合はパラメータをURLから省略します
  - `-2`はすべてのトレントを表します
  - `-1`はすべてのUsenetを表します
  - インデクサID
- `categories` - 使用するカテゴリのカンマ区切りリスト
  - すべての場合はパラメータを省略します
- `type` - 実行する検索タイプ
  - `search` - 基本テキストクエリ
  - `tvsearch` - TVクエリ - TVパラメータをサポート
  - `moviesearch` - 映画クエリ - 映画パラメータをサポート
  - `audiosearch` - オーディオ/音楽クエリ - 音楽パラメータをサポート
  - `booksearch` - 書籍クエリ - 書籍パラメータをサポート