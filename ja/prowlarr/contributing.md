---
title: Prowlarrへの貢献方法
description: 
published: true
date: 2022-11-16T19:35:23.515Z
tags: prowlarr, 開発, 貢献
editor: markdown
dateCreated: 2021-12-11T19:42:15.627Z
---

# 貢献方法

Prowlarrをさらに良くするためには、常に人手が必要です。貢献する方法はいくつかあります。

# ドキュメント

セットアップガイド、[FAQ](/prowlarr/faq)、[wiki](https://wiki.servarr.com/prowlarr)に情報を追加すると、より良い情報が得られます。

# 開発

ProwlarrはC#（バックエンド）とJS（フロントエンド）で書かれています。バックエンドは.NET6フレームワークで構築されており、フロントエンドはReactjsを利用しています。

## 必要なツール

- Visual Studio 2022以上を推奨します（<https://www.visualstudio.com/vs/>）。コミュニティ版は無料で使用できます（<https://www.visualstudio.com/downloads/>）。

> .NET6 SDKが含まれているため、VS 2022 V17.0以上を推奨します
{.is-info}

- 好きなHTML/Javascriptエディタ（VS Code/Sublime Text/Webstorm/Atomなど）
- [Git](https://git-scm.com/downloads)
- [Node.js](https://nodejs.org/)ランタイムが必要です。以下のバージョンがサポートされています：
  - **12.0** 以降
  - **14.0** 以降
  - **16.0** 以降
{.grid-list}

> Prowlarrは、`10.x`、`8.x`、`6.x`、または12.0未満のバージョンでは動作しません！
{.is-warning}

- フロントエンドをビルドするために[Yarn](https://yarnpkg.com/getting-started/install)が必要です
  - Yarnは**Node 16.10**以降にデフォルトで含まれています。`corepack enable`で有効にします
  - 他のNodeのバージョンでは、`npm i -g corepack`でインストールします

## 開始方法

1. Prowlarrをフォークする
1. リポジトリを開発マシンにクローンする。[*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> コミットする前に、フロントエンドの変更に対してコードのリントを実行するために `yarn lint --fix` を実行してください。
CSSの変更に対しては `yarn stylelint-windows --fix` を実行してください。
{.is-info}

### フロントエンドのビルド

- クローンしたディレクトリに移動する
- 必要なNodeパッケージをインストールする

     ```bash
     yarn install
     ```

- 開発環境の変更を監視し、必要な後処理を行うためにwebpackを起動する

     ```bash
     yarn start
     ```

### バックエンドのビルド

バックエンドのソリューションは、Visual StudioやRiderで簡単にビルドおよび実行できます。ただし、フロントエンドUIの作業が唯一の優先事項である場合は、正しいSDKがインストールされている場合にはコマンドラインからも簡単にビルドできます。

#### Visual Studio

> 起動プロジェクトが `Prowlarr.Console` に設定されており、フレームワークが `net6.0` に設定されていることを確認してください
{.is-info}

1. Visual Studioでソリューションを「ビルド」すると、すべてのプロジェクトが正しくビルドされ、依存関係が復元されます
1. 次に、Visual Studioでプロジェクトを「デバッグ/実行」してProwlarrを起動します
1. <http://localhost:9696>を開きます

#### コマンドライン

1. ソリューションをクリーンアップする

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. 正しいプラットフォーム（PosixまたはWindows）のデバッグ構成を復元およびビルドする

```shell
dotnet msbuild -restore src/Prowlarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. `/_output`から生成された実行可能ファイルを実行する

## コードの貢献

- 既に要求されている新しい機能を追加する場合は、[GitHub Issues](https://github.com/Prowlarr/Prowlarr/issues)にコメントして重複作業を避けてください（まだ存在しないものを追加する場合は、まず私たちに相談してください）
- Prowlarrのdevelopブランチからリベースしてマージしないでください
- 意味のあるコミット、またはそれらをスカッシュしてください
- 作業が完了する前にプルリクエストを作成しても構いません。これにより、進捗状況を確認し、コメントや改善の提案を行うことができます
- 質問がある場合は、discordでお問い合わせください
- テスト（単体/統合）を追加してください
- 一貫性のために\*nixの行末でコミットしてください（Windowsでチェックアウトし、\*nixでコミットします）
- クリーンで理解しやすいため、1つの機能/バグ修正ごとに1つのプルリクエストを作成してください
- タブの代わりに4つのスペースを使用してください。これは、VS 2022とWebStormのデフォルトです

### インデクサーの貢献

### C# インデクサー

- C# インデクサーは、[Prowlarr App リポジトリ](https://github.com/prowlarr/prowlarr)の`develop`ブランチに対してプルリクエストを作成してください
- C# インデクサーを貢献する場合は、コミットのフレーズを次のようにしてください：`New: (Indexer) {Indexer Name}`、`New: (Indexer) {Usenet|Torrent} {Indexer Name}`、`New: (Indexer) {Torznab|Newznab} {Indexer Name}`
- C# インデクサーを更新する場合は、コミットのフレーズを次のようにしてください：`Fixed: (Indexer) {Indexer Name} {changes}` 例：`Fixed: (Indexer) Changed BHD to use API`

### Cardigann（YML）インデクサー

- CardigannおよびYMLインデクサーは、[Prowlarr Indexer リポジトリ](https://github.com/prowlarr/indexers)の`master`ブランチに対してプルリクエストを作成してください
- Cardigann/YMLインデクサーの詳細については、[Prowlarr Cardigann yml形式の定義と説明](/prowlarr/cardigann-yml-definition)を参照してください
- カスタムyml定義のテストについては、[インデクサーページのカスタムymlセクション](/prowlarr/indexers#adding-a-custom-yml-definition)を参照してください

## プルリクエスト

- `master`ではなく、`develop`にのみプルリクエストを作成してください。`master`にプルリクエストを作成すると、コメントを残してクローズします
- 私たちからコメントや質問があるかもしれませんが、それは一貫性と保守性を確保するためです
- プルリクエストにできるだけ早く対応しますが、1日または2日経っても返信がない場合は、お問い合わせください。見落としている可能性があります
- 各プルリクエストは、自分のフォークのdevelopではなく、[フィーチャーブランチ](http://martinfowler.com/bliki/FeatureBranch.html)から作成する必要があります。意味のあるブランチ名（追加/修正内容）にする必要があります
  - `new-feature`（良い例）
  - `fix-bug`（良い例）
  - `patch`（悪い例）
  - `develop`（悪い例）
- コミットは、`maintenance release`とは見なされない変更に対して `New:` または `Fixed:` と書かれるべきです

## ユニットテスト

Prowlarrでは、ユニット、統合、および自動化テストスイートにnunitを使用しています。

### テストの実行

テストは、含まれているnunit3testadapter nugetパッケージを使用してVS内から簡単に実行できます。または、`test.sh`というbashスクリプトを使用してコマンドラインから実行できます。

VSからは、テストエクスプローラに移動し、調べたいテストを実行またはデバッグします。

テストは、VSで一度にすべて実行するか、1つずつ実行することができます。

コマンドラインからは、`test.sh`スクリプトに3つのパラメータを指定します

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### テストの作成

楽しいとは言えないかもしれませんが、バックエンドのコード変更に対してはユニットテストの作成をお勧めします。これにより、変更が意図した通りに機能し、将来の変更が予想される動作を壊さないことが保証されます。

> 現在、PRを提出する際には新しいコードの80%のカバレッジが必要です
{.is-info}

これに関する質問がある場合は、お知らせください。

# 翻訳

Prowlarrは、自己ホスト型のオープンアクセス[Weblate](https://translate.servarr.com)インスタンスを使用して、json形式の翻訳ファイルを管理しています。これらのファイルは、リポジトリの`src/NzbDrone.Core/Localization`に保存されています。

## 既存の翻訳への貢献

Weblateは、英語以外のすべての言語の文字列の同期と翻訳を処理します。サポートされている言語の既存の文字列の編集や翻訳は、Prowlarrプロジェクトではそこで行う必要があります。

英語の翻訳である `en.json` は、すべての他の翻訳の元となり、GitHubリポジトリで管理されています。

## 言語の追加

Prowlarrへの翻訳の追加には2つの手順が必要です

- Weblateに言語を追加する
- Prowlarrのコードベースに言語を追加する

## コード内での翻訳文字列の追加

英語の翻訳である `src/NzbDrone.Core/Localization/en.json` は、すべての他の翻訳の元となり、GitHubリポジトリで管理されています。UIまたはバックエンドに新しい文字列を追加する場合、英語でのデフォルト値とともに `en.json` にキーを追加する必要があります。このキーは次のように使用できます：

> ログメッセージの翻訳のPRは受け付けません
{.is-warning}

### バックエンドの文字列

バックエンドの文字列は、Localization Serviceの `GetLocalizedString` メソッドを使用して追加できます

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### フロントエンドの文字列

新しい文字列は、translate関数をインポートし、`en.json` で指定されたキーを使用してフロントエンドに追加できます

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```