---
title: Prowlarr インデクサー
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

このページでは、Prowlarr でのインデクサーの追加と設定方法について説明します。

# インデクサーの追加

インデクサーを追加するには、まず左側のメニューで `Indexers` をクリックし、ページの上部にある <kb>+</kb> `Add Indexer` をクリックします。

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

リストからインデクサーを選択するか、インデクサーの部分名を入力してインデクサーを検索します。リストにインデクサーが表示されない場合は、Usenet 用の "Generic Newznab" またはトレント用の "Generic Torznab" を使用できる場合があります。それ以外の場合は、[Indexer Request サイト](https://requests.prowlarr.com/) を訪れてください。

> `Generic Newznab` または `Generic Torznab` を使用する場合、インデクサーが標準化された *znab フォーマットをサポートしていることを前提としています。サポートされていない場合、これは機能しません。
{.is-info}

> 注意: ほとんどの Usenet サイトは Generic Newznab と互換性があります。
{.is-warning}

> トラッカーやインデクサーがリストに表示されず、[supported indexers](/prowlarr/supported-indexers) ページにもない場合は、[Indexer Requests Site](https://requests.prowlarr.com) を通じて追加をリクエストすることができます。
{.is-info}

# インデクサーの編集

インデクサーを編集するには、まず左側のメニューで `Indexers` をクリックし、編集したいインデクサーの横にあるレンチアイコンをクリックします。

# インデクサーの ID または URL の表示

インデクサーの詳細を表示するには、まず左側のメニューで `Indexers` をクリックし、インデクサー名の列にあるインデクサーリンクをクリックします。（以前は右側の (i) アイコンでした）

表示可能な詳細には次のものがあります:

- Prowlarr 内の ID
- 説明
- エンコーディング
- 言語
- サイト
- Newznab/Torznab Prowlarr URL
- サイトの機能

# インデクサーの設定

インデクサーを選択すると、設定するために必要な詳細が含まれたポップアップが表示されます。インデクサーごとに必要なフィールドやインデクサーの種類によって、具体的な設定は若干異なります。

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Name - このインデクサーに名前を付けます。アプリと同期すると、末尾に `(Prowlarr)` が追加されます。
- Enable - このインデクサーを有効にするには、チェックボックスをオンにします。
- Redirect - リダイレクトが必要な場合は、チェックボックスをオンにします。リダイレクトが必要なのは、いくつかのインデクサーだけです。リダイレクトが有効になっている場合、グラブリンクは Prowlarr を経由せずに直接アプリケーションに渡されます。

> リダイレクトは、非常に特定のインデクサーにのみ必要です。
{.is-info}

- Sync Profile - ここで Sync Profile を選択します。これらは [`Settings` => `Apps`](/prowlarr/settings#applications) で作成できます。標準のデフォルトプロファイルは既に存在し、次のようになります:

> インデクサーごとに異なる設定を持つことができます。複数のインデクサーインスタンスを作成することで、アプリごとに異なる設定を行うことができます。
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Prowlarr が使用する URL を選択します。空白の場合は、デフォルト/最初の URL が使用されます。
- Download Link - トレントインデクサーを追加する場合、使用するダウンロードリンクの種類を選択する必要がある場合があります。
- (Advanced Option) API Path - インデクサーの API のパス。通常は `/api` です。
- Credentials - 多くのインデクサーやトラッカーでは、何らかの方法で認証/ログインが必要です。API キー、RSS キー、セッション ID、クッキーなど、インデクサーからの他の資格情報（通常はプロフィールページまたはセキュリティの下にあります）を入力する必要があります。検索順序を選択したり、特定のインデクサーに対するその他のオプションを選択したりする必要がある場合もあります。
  - API キー
  - RSS キー
  - セッション ID
  - クッキー
  - ユーザー名/パスワード
  - その他
- (Advanced Option) Additional Parameters - このインデクサーのリクエストに追加する追加パラメーター。
- VIP Expiration - ISO 形式（yyyy-MM-DD）で有効期限の 1 週間前に通知される日付を入力します。それ以外の場合は空白のままにします。
- Tags - タグを使用して、デフォルトのダウンロードクライアントを指定したり、インデクサープロキシを指定したり、インデクサーをアプリケーションに指定したり、インデクサーを整理したりすることができます。
- (Advanced Option) Query Limit - インデクサーが API ヒット数を制限している場合、ここにその数を入力して制限を超えないようにすることができます。
- (Advanced Option) Grab Limit - インデクサーが 1 日のグラブ数を制限している場合、ここにその数を入力して制限を超えないようにすることができます。グラブ制限に達すると、さらなるクエリは \*Arr アプリで未処理の例外をトリガーします。他のアプリは異なる場合があります。
- (Advanced Option) Seed Ratio - トレントインデクサーの場合のみ: 停止する前にトレントが達するべき比率。空白の場合はアプリのデフォルトが使用されます。
- (Advanced Option) Seed Time - トレントインデクサーの場合のみ: 停止する前にトレントがシードされるべき時間。空白の場合はアプリのデフォルトが使用されます。値は分単位です。
- (Advanced Option) Indexer Priority - リリースの優先度付けシナリオで他のインデクサーよりも優先するためのこのインデクサーの優先度。1 が最も高い優先度で、50 が最も低い優先度です。これらの優先度は \*Arr アプリに同期されます。

- インデクサーをテストし、緑色のチェックマークが表示されたら保存して問題ありません。保存すると、同期設定に応じて自動的にアプリに追加されます。

## カスタム YML 定義の追加

- YML 定義は一時的にキャッシュされるため、開発目的で変更を行った場合はキャッシュを待つか、Prowlarr を再起動する必要があります。
- サポートされていないインデクサーを追加するか、既存の定義をテストするために、カスタムの Cardigann 互換の YML 定義ファイルを追加する場合は次の手順に従ってください:
  - [Prowlarr の App Data フォルダ](/prowlarr/appdata-directory) の `Definitions` フォルダ内に `Custom` という名前のカスタムインデクサー定義フォルダを移動（または作成）します。
    - 例:
      - Windows: `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux: `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX: `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - [Cardigann 互換の YML ファイル](/prowlarr/cardigann-yml-definition) をフォルダに保存し、Prowlarr がアクセスできるようにします。

> ファイル名と定義内の ID は一意であり、他の既存の定義と競合してはなりません。定義内の名前も一意であることが強く推奨されます。
{.is-info}

# サポートされているインデクサー

- [最新のナイトリーリリース時点でサポートされているインデクサーのリストについては、このウィキページを参照してください。](/prowlarr/supported-indexers/)