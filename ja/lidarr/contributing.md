---
title: Lidarrへの貢献方法
description: 
published: true
date: 2022-09-26T15:56:35.364Z
tags: lidarr, 貢献
editor: markdown
dateCreated: 2021-05-26T02:28:31.770Z
---

# 貢献方法

Lidarrをより良くするためには、常に人々の協力を求めています。貢献する方法はいくつかあります。

# ドキュメント

セットアップガイド、[FAQ](/lidarr/faq)、[wiki](https://wiki.servarr.com/lidarr)にある情報が多ければ多いほど良いです。

# 開発

LidarrはC#（バックエンド）とJS（フロントエンド）で書かれています。バックエンドは.NET6フレームワークで構築されており、フロントエンドはReactjsを利用しています。

## 必要なツール

- Visual Studio 2022以降が推奨されます（<https://www.visualstudio.com/vs/>）。コミュニティ版は無料で使用できます（<https://www.visualstudio.com/downloads/>）。

> .NET6 SDKが含まれているため、VS 2022 V17.0以降を推奨します
{.is-info}

- 好きなHTML/Javascriptエディタ（VS Code/Sublime Text/Webstorm/Atomなど）
- [Git](https://git-scm.com/downloads)
- [Node.js](https://nodejs.org/)ランタイムが必要です。以下のバージョンがサポートされています：
  - **12.0**以降
  - **14.0**以降
  - **16.0**以降
{.grid-list}

> Lidarrは、`10.x`、`8.x`、`6.x`、または12.0未満のバージョンなど、古いバージョンでは動作しません！
{.is-warning}

- フロントエンドをビルドするために[Yarn](https://yarnpkg.com/getting-started/install)が必要です
  - Yarnは**Node 16.10**以降にデフォルトで含まれています。`corepack enable`で有効にします
  - 他のNodeのバージョンでは、`npm i -g corepack`でインストールします

## 初めての操作

1. Lidarrをフォークします
1. リポジトリを開発マシンにクローンします。[*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> コミットする前に、フロントエンドの変更に対してコードのリントを実行するために `yarn lint --fix` を実行してください。
CSSの変更に対しては `yarn stylelint-windows --fix` を実行してください。
{.is-info}

### フロントエンドのビルド

- クローンしたディレクトリに移動します
- 必要なNodeパッケージをインストールします

     ```bash
     yarn install
     ```

- 開発環境の変更を監視し、必要な後処理を行うためにwebpackを起動します

     ```bash
     yarn start
     ```

### バックエンドのビルド

バックエンドのソリューションは、Visual StudioやRiderで簡単にビルドおよび実行できます。ただし、フロントエンドのUIに重点を置く場合は、正しいSDKがインストールされている場合にコマンドラインからも簡単にビルドできます。

#### Visual Studio

> 起動プロジェクトが `Lidarr.Console` に設定されており、フレームワークが `net6.0` に設定されていることを確認してください
{.is-info}

1. Visual Studioでソリューションを`ビルド`すると、すべてのプロジェクトが正しくビルドされ、依存関係が復元されます
1. 次に、Visual Studioでプロジェクトを`デバッグ/実行`してLidarrを起動します
1. <http://localhost:8686>を開きます

#### コマンドライン

1. ソリューションをクリーンアップします

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. 正しいプラットフォーム（PosixまたはWindows）のデバッグ構成を復元およびビルドします

```shell
dotnet msbuild -restore src/Lidarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. `/_output`から生成された実行可能ファイルを実行します

## コードの貢献

- 既に要求されている新しい機能を追加する場合は、[GitHub Issues](https://github.com/Lidarr/Lidarr/issues)にコメントして、作業が重複しないようにしてください（まだそこにないものを追加したい場合は、まず私たちに相談してください）
- Lidarrのdevelopブランチからリベースし、マージしないでください
- 意味のあるコミット、またはそれらをスカッシュしてください
- 作業が完了する前にプルリクエストを作成しても構いません。これにより、進捗状況を確認し、コメントや改善の提案をすることができます
- 質問がある場合は、discordでお問い合わせください
- テスト（単体/統合）を追加してください
- 一貫性のために\*nixの改行でコミットしてください（Windowsでチェックアウトし、\*nixでコミットします）
- クリーンで理解しやすいように、1つの機能/バグ修正ごとに1つのプルリクエストを作成してください
- タブの代わりに4つのスペースを使用してください。これは、VS 2022とWebStormのデフォルトです

## プルリクエスト

- `master`ではなく、`develop`にのみプルリクエストを作成してください。`master`にPRを作成すると、コメントを追加してクローズします
- 私たちからコメントや質問があるかもしれませんが、それは一貫性と保守性を確保するためです
- プルリクエストにできるだけ早く対応しますが、1日または2日経っても対応がない場合は、お問い合わせください。見落としている可能性があります
- 各PRは、自分のフォーク内の[feature branch](http://martinfowler.com/bliki/FeatureBranch.html)から作成する必要があります。意味のあるブランチ名（追加/修正内容）にする必要があります
  - `new-feature`（良い例）
  - `fix-bug`（良い例）
  - `patch`（悪い例）
  - `develop`（悪い例）
- コミットは、`New:`または`Fixed:`として記述する必要があります。これは`メンテナンスリリース`とは見なされない変更のためです

## ユニットテスト

Lidarrは、ユニット、統合、および自動化テストスイートにnunitを使用しています。

### テストの実行

テストは、含まれているnunit3testadapter nugetパッケージを使用してVS内から簡単に実行できます。または、`test.sh`というbashスクリプトを使用してコマンドラインから実行できます。

VSからは、テストエクスプローラに移動し、調べたいテストを実行またはデバッグします。

VSでは、一度にすべてのテストを実行するか、1つずつ実行することができます。

コマンドラインからは、`test.sh`スクリプトに3つのパラメータを指定します

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### テストの作成

楽しいとは言えないかもしれませんが、バックエンドのコード変更に対しては、ユニットテストを作成することをお勧めします。これにより、変更が意図した通りに機能し、将来の変更が予期した動作を壊さないことが保証されます。

> 現在、PRを提出する際には、新しいコードの80%のカバレッジが必要です
{.is-info}

これに関する質問がある場合は、お知らせください。

# 翻訳

Lidarrは、json形式の翻訳ファイルを管理するための自己ホスト型のオープンアクセス[Weblate](https://translate.servarr.com)インスタンスを使用しています。これらのファイルは、リポジトリの`src/NzbDrone.Core/Localization`に保存されています。

## 既存の翻訳への貢献

Weblateは、英語以外のすべての言語の文字列の同期と翻訳を処理します。Lidarrプロジェクトの既存の言語の翻訳の編集や翻訳は、Weblateで行う必要があります。

英語の翻訳である `en.json` は、他のすべての翻訳の元となり、GitHubリポジトリで管理されています。

## 言語の追加

Lidarrへの翻訳の追加には、2つの手順が必要です

- Weblateに言語を追加する
- Lidarrのコードベースに言語を追加する

## コード内での翻訳文字列の追加

英語の翻訳である `src/NzbDrone.Core/Localization/en.json` は、他のすべての翻訳の元となり、GitHubリポジトリで管理されています。UIまたはバックエンドに新しい文字列を追加する場合、英語でのデフォルト値とともに `en.json` にキーを追加する必要があります。このキーは、次のように使用できます：

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