---
title: Sonarr v4 Beta FAQ
description: Sonarr v4 Beta FAQ
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# Sonarr v4 Beta FAQ

> Sonarr v4は現在ベータ版です。そのため、エラーや問題が発生する可能性があります。v4ベータ版に関する質問や問題の報告、フィードバックは、サポートチャンネルを利用してください。必要に応じて、[Github](https://github.com/Sonarr/Sonarr)で問題を開くように求められる場合があります。その際は、元のディスカッションへのリンクと他の要求された情報を提供してください。{.is-warning}

## 変更点

詳細については、[v4ベータ版の発表](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)を参照してください。

以下は、ハイライトや目立つ変更のいくつかです。

- [強制認証](#forced-authentication)
- Mono => Dotnet (高速化; もはやmonoではない)。この変更により、リバースプロキシの設定の更新が必要になる場合があります:
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Preferred Wordsがなくなりました](#preferred-words-to-custom-formats-migration)。代わりにカスタムフォーマットが導入されました。
- [言語プロファイルがなくなりました](#where-have-language-profiles-gone)。代わりにカスタムフォーマットが導入されました。
- ダーク/ライトテーマ
- SysLogとインスタンス名のサポート
- マスエディターが[シリーズ概要](#where-has-the-mass-editor-gone)に統合されました
- その他多数の変更

## 強制認証

SonarrのUIに外部ネットワークからアクセスできるように公開している場合、UIにアクセスするためには認証方法を有効にする必要があります。これは、トラッカーやインデクサーでもますます必要とされるようになっています。

Sonarr v4では、認証が必須です。

### 認証方法

- `Basic` (ブラウザのポップアップ) - このオプションを選択すると、Sonarrにアクセスする際にユーザー名とパスワードを入力するための小さなポップアップが表示されます。
- `Forms` (ログインページ) - このオプションを選択すると、他のウェブサイトと同様のログイン画面が表示され、Sonarrにログインすることができます。
- `External` - 設定ファイルでのみ設定可能
  - Authelia、Authetik、NGINX Basic authなどの**外部認証**を使用している場合、アプリをシャットダウンし、[設定ファイル](/sonarr/appdata-directory)で`<AuthenticationMethod>External</AuthenticationMethod>`を設定し、アプリを再起動することで、二重認証を回避することができます。**ファイル内の複数の`AuthenticationMethod`エントリはサポートされておらず、最上位の値のみが使用されます**

### 認証の必要性

- アプリを外部に公開しない場合や、ローカル（LANなど）へのアクセスに認証を必要としない場合は、設定 => 一般セキュリティ => 認証が必要な場所で`Disabled For Local Addresses`に変更してください。
  - これに相当する設定ファイルのエントリは`<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`です。

## Preferred WordsからCustom Formatsへの移行

Preferred Wordsシステムは、Custom Formatsシステムに置き換えられました。これにより、Sonarrが行う判断にはより細かい設定が可能になりました。Preferred Wordsはすべての品質プロファイルに適用されるのに対し、Custom Formatsは各品質プロファイルごとに異なる重要度を持つことができます。

Custom Formatsには、好みのレベルが達成されたらアップグレードを停止するためのカットオフレベルを設定することもできます。一方、以前のPreferred Wordsシステムでは、より良いリリースが見つかった場合は常にアップグレードが行われました。

### 含む/含まない

含む/含まないは、リリースプロファイルの設定で引き続き使用できます。

### ファイル名トークン

`{Preferred Words}`のファイル名トークンは、ファイルの命名に使用される正規表現エントリに一致する用語を使用します。
`{Custom Formats}`のファイル名トークンは、ファイルの命名にカスタムフォーマット名を使用します。

> アップグレードする前に、Preferred Wordsリリースプロファイルをスクリーンショットするか削除することをお勧めします。移行後、各Preferred Word行は独自のCustom Formatになります。{.is-warning}

## 言語プロファイルはどこにありますか？

Sonarr v4では、言語は異なる方法で処理されます。以前の言語プロファイルシステムでは管理されなくなり、代わりにカスタムフォーマットの一部となりました。取得したい言語のためにカスタムフォーマットを作成し、これらのカスタムフォーマットを適切な評価値で品質プロファイルに追加する必要があります。

> TRaSH Guideの[言語カスタムフォーマットの設定方法](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/)を参照してください。{.is-info}

### 英語のみ

**[TRaSH => 言語: 英語のみ](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

英語のリリースのみを取得したい場合は、次のカスタムフォーマットを使用できます。このカスタムフォーマットをインポートし、品質プロファイルごとにスコア-10000で割り当ててください。最小カスタムフォーマットスコアが0であると仮定すると、これにより、英語として解析されないリリースはすべて拒否されます。

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Language: English Only",
  "name": "Language: Not English",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Not English Language",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 1
      }
    }
  ]
}
```

### オリジナルのみ

**[TRaSH => 言語: オリジナルのみ](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

シリーズのTVDbオリジナル言語のリリースのみを取得したい場合は、次のカスタムフォーマットを使用できます。このカスタムフォーマットをインポートし、品質プロファイルごとにスコア-10000で割り当ててください。最小カスタムフォーマットスコアが0であると仮定すると、これにより、The SeriesのTVDbオリジナル言語として解析されないリリースはすべて拒否されます。

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Language: Original Only",
  "name": "Language: Not Original",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Not Original Language",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": -2
      }
    }
  ]
}
```

## リバースプロキシが動作しなくなりましたか？

Sonarrのバックエンドの変更（monoからdonnetへの移行）により、リバースプロキシが動作しなくなる場合があります。

### Nginx

Nginxの設定ファイルを変更する必要があります。次の行を置き換えてください。

```nginx
   proxy_set_header   Host $proxy_host;
```

次の行に置き換えてください。

```nginx
  proxy_set_header   Host $host;
```

### Apache

Apacheの仮想ホストの設定ファイルを変更する必要があります。次の行を追加してください。

```apache2
  ProxyPreserveHost On
```

## この新しい「*Override and add to download queue*」ボタンは何ですか？

インタラクティブな検索を行う際に、「Override and add to download queue」という2番目のダウンロードボタンが追加されました。このボタンを使用すると、次の2つの操作が可能になります。

- ダウンロードを送信するダウンロードクライアントを選択することができます。これは、同じプロトコルの複数のダウンロードクライアント（たとえば、複数のトレントクライアントのインスタンス）を持っている場合に便利です。Sonarrがどのクライアントを使用するかを自動的に決定するのではなく、自分で選択することができます。
- Sonarrがリリースタイトルを誤って解析した場合や、Sonarrが解析できなかった場合でも、リリースを取得したい場合に、リリースタイトルの解析を上書きすることができます。以下の解析フィールドを上書きすることができます:
  - シリーズ
  - シーズン番号
  - エピソード
  - 品質
  - 言語

## マスエディターはどこにありますか？

マスエディターの独立したページは削除され、その機能はシリーズ概要ページに統合されました。ショーを一括編集するには、まずシリーズ概要の上部にある「Select Series」ボタンをクリックし、編集したいショーを選択します。

シーズンパスページも廃止されました。一部の機能はシリーズ概要エディターに残っており、テーブルビューを選択して「Select Series」を押します。選択モードに入ると、シーズン列の数値にカーソルを合わせると、そのショーのシーズンパスポップオーバーにアクセスできます。

## エピソードの実行時間が0になっています

v4では、エピソードごとにTVDbから実行時間を取得します。エピソードの実行時間が0の場合、シリーズの実行時間にフォールバックします。
シリーズの実行時間も0の場合、Sonarrは最初のエピソードから24時間以内に放送されたエピソードの実行時間として45を使用します。