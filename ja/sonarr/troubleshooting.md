# ヘルプを求める

ヘルプが必要ですか？大丈夫です、誰でも時にはヘルプが必要です。リアルタイムのヘルプは以下のチャットで受けることができます。

- [<i class="fab fa-discord"></i>&emsp;Discord *公式Sonarr Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *公式Sonarr Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

ただし、そこに行って投稿する前に、ヘルプを求めるためのリクエストが最善であることを確認してください。問題を明確に説明し、OS/ディストリビューション、.net/Monoのバージョン、Sonarrのバージョン、ダウンロードクライアントとそのバージョンなどのセットアップについて簡単に説明してください。**[Docker](https://www.docker.com/)を使用している場合は、一般的で頻繁なパス/アクセス許可の問題を解決するために、最初に[Dockerガイド](/docker-guide)を実行してください。それ以外の場合は、[docker compose](/docker-guide#docker-compose)を手元に用意してください。[Docker Composeの生成方法](https://trash-guides.info/compose)** すでに試したこと、調べたことについて教えてください。問題を再現し、ログをトレースレベルに設定し、問題を再現し、関連するコンテキストをパステビンに貼り付け、そのリンクを投稿に含めてください。問題をハイライトするためにスクリーンショットを含めることもできます。

私たちが知っていることが多ければ多いほど、あなたを助けることが容易になります。

# ロギングとログファイル

一般的なトラブルシューティングの問題も確認することが有益です：
- [ダウンロードとインポートの一般的な問題](#common-problems)
- [検索インデクサとトラッカーの一般的な問題](#common-problems-1)
{.links-list}

デバッグログが必要な場合、ログには `debug` が含まれ、トレースログが必要な場合はログに `trace` が含まれます。提供するログにこれらのいずれかが含まれていない場合は、要求されているログではありません。

- 要求されていない限り、ログファイル全体を共有しないでください。
- Discordに直接ログをアップロードしたり、テキストの壁として貼り付けたりしないでください（要求されていない限り）。
- ログを添付ファイル、zipアーカイブ、またはそれ以外のテキスト以外の形式で共有しないでください。

共有するための良い有用なログを提供するためには：

> RSSの更新などのスパムタスクが実行されていないことを確認してください。
{.is-warning}

1. [ログレベルをトレースに設定する（設定 => 一般 => ログレベルまたは設定ファイルの編集）](#tracedebug-logs)
2. [ログをクリアする（システム => ログ => ログをクリアまたはログフォルダ内のすべてのログを削除）](#clearing-logs)
3. 問題を再現する（問題を引き起こしていることを再現する）
4. UIまたはファイルシステム上のログファイル（sonarr.trace.txt）を開き、関連するコンテキストを見つける
5. 問題の前、問題そのもの、問題の後ろの大きなチャンクをコピーする
6. [Gist](https://gist.github.com/)、[0bin（**カラーリングを無効にすることを忘れないでください**）](https://0bin.net/)、[PrivateBin](https://privatebin.net/)、[Notifiarr PrivateBin](http://logs.notifiarr.com/)、[Hastebin](https://hastebin.com/)、[UbuntuのPastebin](https://pastebin.ubuntu.com/)などのサイト（以下で回避するものを除く）を使用して、上記でコピーしたログを共有する

**注意事項：**
- **[pastebin.com](https://pastebin.com)は、フィルタがログをブロックする傾向があるため使用しないでください。
- [pastebin.pl](https://pastebin.pl)は、サイトに頻繁にアクセスできないため使用しないでください。
- [JustPasteIt](https://justpaste.it/)は、サイトがログの確認を容易にすることができないため使用しないでください。
- ログをファイルとしてアップロードしないでください。
- ログをGoogleドライブ、Dropbox、または上記以外の他のサイトでアップロードして共有しないでください。
- ログをアーカイブ（zip、tar（tarボール）、7zipなど）しないでください。
- コンソール出力、Dockerコンテナ出力、またはアプリケーションログ以外のものを共有しないでください

**重要な注意：**
- [0bin](https://0bin.net/)を使用する場合は、カラーリングを無効にし、読み終わった後に破棄しないようにしてください。

- また、古いログファイルで特定のエントリを探しているが、どのログファイルかわからない場合は、N++を使用することもできます。Notepad++の「ファイル内検索」機能を使用して、必要に応じて古いログファイルを検索できます。
- **Unixのみ：** 古いログファイルで特定のエントリを探しているが、どのログファイルかわからない場合は、grepを使用することもできます。たとえば、映画/番組/本/曲/インデクサ「Shooter」に関する情報を見つけたい場合は、次のコマンドを実行できます。`grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` [Appdataディレクトリ](/sonarr/appdata-directory)がホームフォルダにある場合は、次のように実行します。`grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * 各フラグの機能は次のとおりです
    * -i: 大文字と小文字を区別しない
    * -n: 行番号を表示する
    *  -r: パス内のすべてのファイルを再帰的にチェックする
    * -C: 見つかった行の前後の行数を指定する
    * -e: 検索するパターン

```

## 標準ログの場所

ログファイルは、Sonarrの[Appdataディレクトリ](/sonarr/appdata-directory)内のlogs/フォルダにあります。また、UIからもログファイルにアクセスできます（システム => ログ => ファイル）。

> 注意：UIのログ（「イベント」）テーブルはログファイルとは異なり、それほど有用ではありません。ログが要求された場合は、ログファイルからコピー/貼り付けてください。
{.is-info}

## 更新ログの場所

更新ログファイルは、Sonarrの[Appdataディレクトリ](/sonarr/appdata-directory)内のUpdateLogs/フォルダにあります。

## ログの共有

ログは長くて読みにくい場合があり、フォーラムやRedditの投稿の一部としては読みにくく、Discordではスパムの原因になるため、[Pastebin](https://pastebin.ubuntu.com/)、[Hastebin](https://hastebin.com/)、[Gist](https://gist.github.com)、[0bin](https://0bin.net)、または同様のパステビンサイトを使用してください。通常、ファイル全体は必要ありません。問題/エラーの前後の十分なコンテキストを共有してください。スパムタスク（RSSの同期やライブラリの更新など）が終了するのを忘れないでください。

## トレース/デバッグログ

ログレベルは、設定 => 一般 => ロギングで変更できます。Sonarrを再起動する必要はありません。この変更はログファイルのみに影響を与えます。最新のデバッグ/トレースログファイルは、それぞれ `sonarr.debug.txt` と `sonarr.trace.txt` という名前です。

ログレベルを設定するためにUIにアクセスできない場合は、AppDataディレクトリのconfig.xmlを編集して、LogLevelの値をInfoではなくDebugまたはTraceに設定することで設定できます。

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## ログのクリア

ログファイルとログデータベースは、UIから直接クリアできます。システム => ログ => ファイルおよびシステム => ログ => 削除（ゴミ箱アイコン）を使用します。

# 複数のログファイル

Sonarrは、1MBに制限されたローリングログファイルを使用します。現在のログファイルは常に `sonarr.txt` であり、他のファイル `sonarr.0.txt` は次に新しいものです（番号が大きいほど古いものです）。このログファイルには `fatal`、`error`、`warn`、`info` のエントリが含まれます。

デバッグログレベルが有効になっている場合、追加の `sonarr.debug.txt` ローリングログファイルが存在します。このログファイルには `fatal`、`error`、`warn`、`info`、`debug` のエントリが含まれます。通常、40時間分のログが含まれます。

トレースログレベルが有効になっている場合、追加の `sonarr.trace.txt` ローリングログファイルが存在します。このログファイルには `fatal`、`error`、`warn`、`info`、`debug`、`trace` のエントリが含まれます。トレースの冗長性のため、最大で数時間分しかカバーされません。

# 失敗したアップデートからの復旧

アップグレード時の問題を防ぐためにできる限りのことをしていますが、問題が発生した場合は、この手順に従ってインストールを復旧します。

## 問題の特定

アプリケーションがアップデート後に起動しない場合、最初に[アップデートログ](#update-logs-location)を確認し、アップデートが正常に完了したかどうかを確認します。それでも問題が解決しない場合は、起動を試みる前に、[ログ](/sonarr/settings#logging)と[ログファイル](/sonarr/system#log-files)を使用して通常のアプリケーションログファイルを確認して、ログレベルを上げます。

### 移行の問題

- 移行エラーは同一ではありませんが、以下は例です：

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### アクセス許可の問題

- アクセス許可の問題は、アプリケーションが関連する一時フォルダやアプリのバイナリフォルダにアクセスできないために発生します。アプリケーションが実行されるユーザー/グループが適切なアクセス権を持つようにアクセス許可を修正してください。

- Synologyユーザーは、Synologyのバグ「アクセスパス '/proc/{some number}/maps' へのアクセスが拒否されました」という問題に遭遇することがあります。

- Synologyユーザーは、特定のNASで`/tmp`の容量不足の問題にも遭遇することがあります。アプリケーションのために異なる`/tmp`パスを指定する必要があります。この問題の解決には、SynoCommunityまたは他のSynologyサポートチャンネルのヘルプを参照してください。

## 問題の解決

移行の問題が発生した場合、すぐに対処できることはほとんどありません。もし問題が特定のユーザーに固有のものである場合（またはまだ投稿がない場合）、[当社のサブレディット](https://reddit.com/r/sonarr)で投稿を作成するか、[discord](https://discord.sonarr.tv/)に参加してください。同じ問題を抱えている他のユーザーがいる場合は、私たちが対応に取り組んでいることを保証します。

> 安定版で`develop`からデータベースを使用しようとしたことを確認してください。ブランチの切り替えはお勧めしません。{.is-info}

### 権限の問題

- `/tmp`とアプリケーションのインストールディレクトリの両方に対して、アプリケーションが実行されているユーザー/グループがアクセス（読み取りおよび書き込み）できるように、権限を修正してください。

- `/proc/###/maps`の問題でSonarrまたは他の\*Arrアプリケーションが停止しているSynologyユーザーは、Sonarrを更新することで問題が解決するはずです。これはSynoCommunityパッケージの問題です。

### 手動でのアップグレード

ウェブサイトから最新のリリースを取得してください。

アップデート（.exe）をインストールするか、既存のインストールにコンテンツを抽出（.zip）し、通常どおりSonarrを実行してください。

# ダウンロードとインポート

ダウンロードとインポートは、*ほとんどの*ユーザーが問題を抱える場所です。大まかな視点から見ると、Sonarrはダウンロードクライアントと通信し、ダウンロードしたファイルにアクセスする必要があります。サポートされているダウンロードクライアントの種類はさまざまで、設定もさまざまです。つまり、*一般的な*設定がいくつかありますが、*正しい*設定は1つではなく、すべての設定が少し異なる可能性があります。

> **最初のステップは、ログをトレースレベルに設定することです。詳細については、[ログとログファイル](#logging-and-log-files)を参照してください。問題を再現し、その時間枠のトレースレベルのログを使用して問題を調査します。**
> 誰かが助けてくれる場合は、[pastebin](https://0bin.net)、[Gist](https://gist.com)、または類似のサイトに前後のコンテキストを表示してください。
> ファイル全体である必要はありませんし、*エラーだけ*であってはなりません。ログファイルにスパムタスクが実行されていない状態で問題を再現する必要があります。
{.is-danger}

ヘルプを求める際には、必要な詳細を提供できるようにするために、[ヘルプを求める](#asking-for-help)を必ず読んでください。

## ダウンロードクライアントのテスト

ダウンロードクライアントが実行されていることを確認してください。まず、ダウンロードクライアントをテストしてください。うまくいかない場合、トレースレベルのログで詳細を確認できます。ブラウザに入力できるURLを見つけて、それが機能するかどうか確認してください。接続の問題かもしれません。間違ったIP、ホスト名、ポート、またはファイアウォールによるアクセスのブロックなどが考えられます。ユーザー名、パスワード、またはAPIキーが間違っている場合など、明らかな認証の問題かもしれません。

## ダウンロードのテスト

次に、ダウンロードを試してみましょう。シリーズのエピソードを選び、手動で検索を実行します。そのファイルのうちの1つをダウンロードしようとしてください。ダウンロードクライアントに送信されますか？正しいカテゴリに表示されますか？アクティビティに表示されますか？トレースレベルのログには表示されますか（監視中のダウンロードの更新と監視中のダウンロードの処理タスクがおおよそ1分ごとに実行されます）？そのタスク中に正しく解析されますか？キューに入れられたダウンロードには適切な名前が付いていますか？一部のインデクサ/トラッカーではIDで検索されるため、認識できない名前でキューに入れることがあります。

## インポートのテスト

インポートの問題はほとんど常に、アクティビティにエラーが表示されるアイテムとして現れます。アクティビティに表示されない場合、まずこの問題に焦点を当てる必要がありますので、戻って解決してください。ほとんどのインポートエラーは*権限*の問題です。ダウンロードフォルダー内で読み取りと書き込みができるようにする必要があります。ライブラリフォルダーの権限も問題の原因になることがありますので、両方を確認してください。

パスの問題も可能性がありますが、通常の設定ではあまり一般的ではありません。パスの問題を理解するためのキーは、ダウンロードクライアントからのダウンロードパスを、そのAPIを介して取得することです。これは、ダウンロードクライアントが別のシステム（おそらく別のOS）で実行されている場合など、よりユニークな使用例で問題になります。Dockerのセットアップでは、ボリュームがうまく設定されていない場合にも問題が発生することがあります。シードボックスのセットアップなど、制御できない場所では、リモートパスマップが良い解決策です。Dockerのセットアップでは、パスを修正することがより良いオプションです。

## よくある問題

以下は一部の一般的な問題です。

### リリースに期待される1つ以上のエピソードがインポートされなかったり、欠落していたりする

- すべてのエピソードがインポートされた場合、最も一般的な原因は、シーズンパックがダウンロードされたが、シーズンのすべてのエピソードが含まれていないことです。`X`をクリックしてリリースを削除し、無視してください。
- その他の問題の場合、1つ以上のエピソードがインポートできませんでした。UIの情報とその他の一般的な問題を確認してください。

### Sonarr v2の使用

Sonarr v2は2021年3月以降、サポートが終了しており、サポートされていません。qBittorrent v4.3.0以降と互換性がありません。Sonarr v3にアップグレードしてください。

### ダウンロードクライアントのWebUIが有効になっていない

Sonarrは、ダウンロードクライアントとの通信をAPI経由で行い、クライアントのWebUIを介してアクセスします。クライアントのWebUIが有効になっていることを確認してください。使用しているポートが他のクライアントポートやシステムで使用中のポートと競合していないことを確認してください。

### SSLが使用され、正しく構成されていない

ローカルネットワークでインスタンスとダウンロードクライアントの両方を使用している場合、SSL暗号化がオンになっていないことを確認してください。詳細については、[SSL FAQエントリ](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues)を参照してください。

### Windowsで共有が表示されない

Windowsサービスのデフォルトユーザーは`LocalService`ですが、通常は共有にアクセスできません。サービスを編集し、自分自身のユーザーとして実行するように設定してください。詳細については、FAQエントリの[リモートサーバー上のファイルが表示されない理由](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server)を参照してください。

### マップされたネットワークドライブは信頼性がない

`X:\`のようなマップされたネットワークドライブは便利ですが、UNCパス（`\\server\share`のような）ほど信頼性がありませんし、ログイン前には利用できません。必要に応じて、設定とダウンロードクライアントをUNCパスを使用するように構成してください。ライブラリが共有にある場合は、ルートフォルダーがUNCパスを使用していることを確認してください。ダウンロードクライアントが共有に送信する場合は、ダウンロードパスをダウンロードクライアントから取得するため、そこでUNCパスを構成する必要があります。マップされたネットワークドライブを自分自身で使用することは問題ありませんが、自動化には使用しないでください。

### Dockerとユーザー、グループ、所有権、権限、パス

Dockerは、間違いやすい複雑さを追加しますが、それでも機能するセットアップを作成することができますが、さまざまな問題が発生する可能性があります。ここではそれらについて説明する代わりに、このウィキの記事を読んでください。[これらの自動化ソフトウェアとDockerについて](/docker-guide)は、ユーザー、グループ、所有権、権限、パスについてのものです。これは特定のDockerシステムに固有のものではなく、代わりに高レベルでの説明を行っており、独自の環境で実装できるようになっています。

### リモートパスマッピング

SonarrをDockerで使用し、ダウンロードクライアントを非Dockerで使用している場合（またはその逆）、またはプログラムを異なるサーバーで使用している場合は、リモートパスマップが必要な場合があります。

ログは次のようになります。

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

したがって、`/volume3/data`はSonarrのコンテナ内に存在しないか、アクセスできないことがわかります。

- [設定 => ダウンロードクライアント => リモートパスマッピング](/sonarr/settings#remote-path-mappings)
- リモートパスマッピングは、ダウンロードクライアントが別のサーバー上の完了したデータのパスを報告している場合、または\*Arrがそのフォルダーに対応していない方法で報告している場合に使用されます。
- 一般的に、リモートパスマップは、ダウンロードクライアントがLinux上にある場合に\*ArrがWindows上にある場合、またはその逆の場合にのみ必要です。リモートパスマップは、DUMBな検索/置換（REMOTEの値を見つけて、指定されたホストのLOCALの値に置き換える）です。
- パスのエラーメッセージにREPLACEDの値が含まれていない場合、パスマッピングが期待どおりに機能していない可能性があります。通常の解決策は、マッピングを追加して削除することです。
- [リモートパスマッピングに関する詳細な情報については、TRaSHのチュートリアルを参照してください](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> \*Arrとダウンロードクライアントの両方がDockerコンテナである場合、リモートパスマップはほとんど必要ありません。[Dockerガイド](/docker-guide)を確認するか、[TRaSHのチュートリアル](https://trash-guides.info/hardlinks)に従うことをお勧めします。
{.is-info}

#### リモートマウントまたはリモート同期（Syncthing）

- ダウンロード中に常に同期されるようにする必要があります。また、ローカルの同期先が\*Arrのインポート時にハードリンク可能である必要があります。つまり、同じファイルシステムであり、同じように見える必要があります。
  - 不完全なものと完全なものの両方を含む一般的なフォルダーで同期します。
  - ライブラリと同じファイルシステム上の場所に同期します（Dockerとネットワーク共有の場合、これは誤った構成になる可能性があります）。
  - ダウンロードクライアントが移動を行うと、同期がローカルに反映されます。これにより、ダウンロードが「ほぼ完了」の状態になります。完全に終了していなくても、ハードリンクが可能であるため、インポートが完了することができます。
  - これにより、ダウンロード中は常に同期され、トレントクライアントがtvサブフォルダーに移動すると、同期が反映されます。これにより、ダウンロードはほぼ完了した状態になります。完全に終了していなくても、ハードリンクが可能であるため、問題ありません。
  - （オプション - 必要な場合および/または必要な場合（例：リモートUsenetクライアント））インポート/ダウンロード/アップグレード時にリモートファイルを削除するためのカスタムスクリプトを設定します。
- 代わりに、リモート同期設定よりもリモートマウント設定の方がはるかに簡単に構成できますが、通常は遅くなります。
  - sshfsや他のネットワークファイルシステムプロトコルを使用して、リモートストレージをマウントします。
  - \*Arrが実行されるユーザーとグループが読み取りまたは書き込みアクセス権を持っていることを確認します。
  - リモートパスマップを構成して、REMOTEパスを見つけて、それをLOCALの同等のパスに置き換えます。

### ライブラリフォルダーの権限

ログは次のようになります。

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

*宛先*の権限と所有権を確認するのを忘れないでください。ダウンロードの所有権と権限にこだわりすぎることが簡単であり、*通常*権限関連の問題の原因ですが、*宛先*も原因になる可能性があります。宛先フォルダーが存在することを確認してください。宛先*ファイル*がすでに存在しないか、削除またはごみ箱に移動できないか確認してください。所有権と権限が、ダウンロードしたファイルのコピー、ハードリンク、または移動を許可するようになっているか確認してください。実行するユーザーまたはグループは、ルートフォルダーを読み取りおよび書き込みできる必要があります。

- Windowsユーザーの場合、これはサービスとして実行しているためかもしれません：
  - Windowsサービスはデフォルトで「Local Service」アカウントで実行されますが、このアカウントは通常、手動で権限を割り当てない限り、ユーザーのホームディレクトリにアクセスできません。これは、ホームディレクトリにダウンロードを設定したダウンロードクライアントを使用する場合に特に関連します。
  - 「Local Service」は一般的に非常に制限された権限しか持っていません。したがって、ユーザーがログインしたままであれば、システムトレイアプリケーションとしてアプリをインストールすることをお勧めします。インストーラーでこのオプションが提供されます。サービスからトレイアプリに変換する方法については、FAQを参照してください。

- Synologyユーザーは、[SynoCommunityのパッケージの権限管理に関する記事](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)を参照してください。

- Windows以外の場合：NFSマウントを使用している場合は、`nolock`が有効になっていることを確認してください。
- SMBマウントを使用している場合は、`nobrl`が有効になっていることを確認してください。

### ダウンロードフォルダーの権限

次のようなエラーが表示されます。

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

または

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

*ソース*の権限と所有権を確認するのを忘れないでください。ダウンロードファイルの所有権と権限にこだわりすぎることが簡単であり、権限関連の問題の原因ですが、通常はソースです。ソースフォルダーが存在することを確認してください。所有権と権限が、ダウンロードしたファイルをコピー/ハードリンクするか、コピー+削除/移動するかを許可するようになっているか確認してください。Sonarrが実行されるユーザーまたはグループは、ダウンロードファイルを読み取りおよび書き込みできる必要があります。

- Windowsユーザーの場合、これはサービスとして実行しているためかもしれません：
  - Windowsサービスはデフォルトで「Local Service」アカウントで実行されますが、このアカウントは通常、手動で権限を割り当てない限り、ユーザーのホームディレクトリにアクセスできません。これは、ホームディレクトリにダウンロードを設定したダウンロードクライアントを使用する場合に特に関連します。
  - 「Local Service」は一般的に非常に制限された権限しか持っていません。したがって、ユーザーがログインしたままであれば、システムトレイアプリケーションとしてアプリをインストールすることをお勧めします。インストーラーでこのオプションが提供されます。サービスからトレイアプリに変換する方法については、FAQを参照してください。

- Synologyユーザーは、[SynoCommunityのパッケージの権限管理に関する記事](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)を参照してください。

- Windows以外の場合：NFSマウントを使用している場合は、`nolock`が有効になっていることを確認してください。
- SMBマウントを使用している場合は、`nobrl`が有効になっていることを確認してください。

### ダウンロードフォルダーとライブラリフォルダーが同じフォルダーではない



- ダウンロードクライアントは、\*Arrからアクセス可能なフォルダにダウンロードする必要があります。ルート/ライブラリフォルダではないフォルダにダウンロードする必要があります。また、ダウンロードクライアントの完了フォルダや未完了フォルダとしてルートフォルダを使用しないでください。
- ルートフォルダとして直接ダウンロードすることはありません。また、ダウンロードクライアントの完了フォルダや未完了フォルダとしてルートフォルダを使用しないでください。
- [**これはシステムのヘルスチェックも引き起こします**](/sonarr/system#downloading-into-root-folder)
- アプリケーション内では、ルートフォルダは設定されたメディアライブラリフォルダとして定義されます。これはマウントのルートフォルダではありません。ダウンロードクライアントは、未完了または完了したダウンロードをルート（ライブラリ）フォルダに移動しています。これは頻繁に問題を引き起こし、推奨されません。これを修正するには、ダウンロードクライアントを変更して、ダウンロードをルートフォルダ内に配置しないようにします。なお、「配置」とは、ダウンロードクライアントのカテゴリがルートフォルダに設定されている場合や、NZBGet/SABnzbdがソートが有効になっており、ルートフォルダにソートされている場合も含まれます。このチェックは、現在使用されているルートフォルダだけでなく、追加されたすべての定義済み/設定済みのルートフォルダを確認します。つまり、ダウンロードクライアントがダウンロードまたは完了したダウンロードを移動するフォルダは、\*Arrアプリケーションで設定したルート/ライブラリ/最終メディアの宛先フォルダと同じであってはなりません。
- 設定されたルートフォルダ（またはライブラリフォルダ）は、[設定 => メディア管理 => ルートフォルダ](/sonarr/settings/#root-folders)で見つけることができます。
- 例えば、ダウンロードが `\data\downloads` に行っている場合、`\data\downloads` がルートフォルダとして設定されています。
- ルートフォルダ/ライブラリフォルダには `\data\media\` のようなパスを使用することをお勧めします。ダウンロードには `\data\downloads\` のようなパスを使用してください。

> ダウンロードフォルダとルート/ライブラリフォルダは必ず別々にする必要があります
{.is-warning}

### カテゴリが間違っています

Sonarrは、自分自身のダウンロードのみを処理するようにカテゴリを設定する必要があります。手動でトレントを追加して処理する場合、正しいカテゴリが必要です。いつでも設定できますが、はダウンロードを毎分処理しようとします。

### 圧縮されたトレント

ログには次のようなエラーが表示されます。

```none
インポート対象のファイルが見つかりません
```

トレントが `.rar` ファイルに圧縮されている場合、展開を設定する必要があります。[Unpackerr](https://github.com/unpackerr/unpackerr)を使用することをおすすめします。これにより、破損した部分的なインポートが防止され、インポート後に展開されたファイルがきれいに削除されます。

また、フォルダに有効なメディアファイルがない場合にもこのエラーが表示される場合があります。

### 繰り返しダウンロード

繰り返しダウンロードの原因はいくつかありますが、その1つはリリースプロファイルのインデクサ制限に関連しています。インデクサはデータと一緒に保存されないため、メディアライブラリ内のメディアに対しては「優先ワード」スコアがゼロになりますが、「RSS」や検索では適用されます。同様に、「含む必要がある」または「含まない」制限はそのインデクサにのみ適用され、それ以外は問題ありません。これにより、アップグレードのように見えてダウンロードを繰り返し、それからアップグレードではなくなり、再び表示されてアップグレードのように見える、というループに入ることがあります。リリースプロファイルをインデクサに制限しないでください。

これは、ダウンロードが実際にインポートされず、キューから欠落しているため、新しいダウンロードが永遠に取得されず、インポートされない場合もあります。これに関しては、この問題の他の一般的な問題とトラブルシューティング手順を参照してください。

### Usenetダウンロードがインポートされない

Sonarrは、SABnzbdとNZBGetの最新の60件のダウンロードのみを参照するため、履歴を保持している場合、大量のキューでインポートの問題が発生すると、ダウンロードが静かに見落とされ、インポートされません。これを回避するためには、履歴をクリアしておくことが最善です。これにより、まだ表示されているアイテムが調査されるようになります。これを実現するには、完了したダウンロードと失敗したダウンロードハンドラの下で「削除」を有効にします。NZBGetでは、これによりアイテムが*非表示*の履歴に移動されます。残念ながら、SABnzbdには同様の機能はありません。そこで、nzbバックアップフォルダを使用することができます。

### ダウンロードクライアントがアイテムをクリアしてしまう

ダウンロードクライアントは、ダウンロードの削除には責任を持たないでください。Usenetクライアントは、履歴からダウンロードを削除しないように設定する必要があります。トレントクライアントは、シーディングが終了したらトレントを削除するのではなく、一時停止または停止するように設定する必要があります。これは、インポートするものがないため、ダウンロードクライアントと通信するためです。フォルダにはファイルがいっぱいある場合でも、削除された場合はインポートするものがありません。

SABnzbdでは、これは履歴の保持設定で処理されます。

### ライブラリアイテムに一致するダウンロードができません

さまざまな理由で、ダウンロードが取得され、ダウンロードクライアントに送信された後に解析できない場合があります。Activity => Options => Show Unknown（最近のビルドではデフォルトで有効になっています）を使用すると、\*Arrのダウンロードクライアントカテゴリ内で無視されていない/すでにインポートされていないすべてのアイテムが表示されます。これらは通常、手動でマッピングしてインポートする必要があります。

これは、ダウンロードクライアントにリリースがあるが、そのメディアアイテム（映画/エピソード/本/曲）がアプリケーションに存在しない場合にも発生する可能性があります。

#### グラブ履歴で一致するシリーズが見つかりましたが、シリーズはシリーズIDで一致しました。自動インポートはできません

- このインポートエラーは、上記の一致しないエラーと似ています。
- Sonarrは、インデクサまたはトラッカーが望んでいるシリーズのTVDb ID（またはIMDb ID）を持つリリースを報告したため、リリースを取得しました。
- ダウンロードされたファイルのシリーズが報告されたIDと一致しないため、Sonarrはファイルをインポートしません。
- シリーズのタイトルとリリース名によっては、リリースがシリーズIDに関連付けられている正しいリリースであると仮定すると、Sonarrにエイリアスが追加される必要があります。[このFAQエントリには、追加をリクエストするための詳細があります](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)。
- または、リリースが誤ってラベル付けされ、報告されたシリーズIDではない場合もあります。これは、インデクサに報告して修正する必要があります。
- このエラーを処理するには：
  1. ファイルのシリーズを確認します
  1. エイリアスをリクエストします（該当する場合）
  1. ファイルを手動でインポートします（Activity => Queueの右側にあるHumanアイコン）またはキュー内の`X`をクリックして、クライアント内のリリースを無視し、オプションでブロックリストに追加/クライアントから削除します

### エピソード名がTBAです

TVDBでは、エピソード名が不明な場合、TBAというタイトルが付けられ、APIには24時間のキャッシュがあります。通常、TVDBのウェブサイトの変更は、TVDBキャッシュ、Skyhookキャッシュ、およびシリーズの更新間隔のために24〜48時間かかります。

Sonarrの[エピソードタイトルが必要](/sonarr/settings#importing)設定は、タイトルがTBAの場合のインポート動作を制御しますが、エピソードの放送日から24時間後には、タイトルがまだTBAの場合でもリリースがインポートされます。また、TBAのタイトルのファイルの自動的なリネームはありません。

### The underlying connection was closed: An unexpected error occurred on a send

これは、インデクサが現在の.NETバージョンでサポートされていないSSLプロトコルを使用しているためです。[Sonarr => System => Status](/sonarr/system#status)で現在の.NETバージョンを確認してください。

### The request timed out

Sonarrは、クライアントからの応答を受け取っていません。

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

これは、次の原因でも発生する可能性があります。

- VPNの設定が正しくないか、使用されている
- プロキシの設定が正しくないか、使用されている
- ローカルのDNSの問題 - 異なるDNSプロバイダに変更してみてください
- ローカルのIPv6の問題 - 通常、IPv6は有効になっていますが、機能していません
- Privoxyの使用と、それが正しく設定されていないこと

## リストされていない問題

一般的なアクセス許可とネットワーキングのトラブルシューティングコマンドについては、[ガイド](/permissions-and-networking)を参照してください。それ以外の場合は、ディスコードのサポートチームと相談してください。これが一般的な問題である可能性がある場合は、ウィキに追加することを提案してください。

# インデクサとトラッカーの検索

- [なぜSonarrは期待していたエピソードを取得しなかったのか？](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting)のFAQエントリも役立つでしょう。
- [Prowlarr](/prowlarr)を使用している場合、[履歴](/prowlarr/history)でProwlarrが受信したすべてのクエリとそれらがサイトに送信された方法を表示できます。Prowlarr History => Optionsで`Parameters`が有効になっていることを確認してください。詳細については(i)アイコンをクリックしてください。
- 以下にトラブルシューティング手順があります

## ログをトレースレベルに設定する

> **最初のステップは、ログをトレースレベルに設定することです。ログの調整と検索の詳細については、[ログとログファイル](#logging-and-log-files)を参照してください。その後、問題を再現し、その時間枠のトレースレベルのログを使用して問題を調査します。** 誰かが助けてくれる場合は、彼らに示すために前後の文脈を[pastebin](https://0bin.net)、[Gist](https://gist.com)、または類似のサイトに表示してください。ファイル全体である必要はありませんし、エラーだけであってはいけません。また、ログファイルにスパムを送るタスクが実行されていない状態で問題を再現する必要があります。
{.is-danger}

## インデクサまたはトラッカーのテスト

インデクサまたはトラッカーをテストするときは、デバッグまたはトレースログで使用されるURLを見つけることができます。以下に成功したテストの例があります。特定のURLと特定のパラメータを使用してインデクサにクエリを送信し、その応答を確認できます。このURLをブラウザでテストし、`apikey=(removed)`を正しいapikey（例：`apikey=123`）で置き換えて試してみてください。動作しますか？期待される結果が表示されますか？このFAQエントリは適用されますか？このURLでは、`cat=5030,5040,5045,5080`のように特定のカテゴリが設定されていることがわかります。したがって、期待される結果が表示されない場合、これが1つの可能性があります。また、`tvdbid=354629`のようにtvdbidで検索していることがわかります。したがって、インデクサ上でエピソードが正しくカテゴリ分類されていない場合、修正する必要があります。また、`season=1`および`ep=1`で特定のシーズンとエピソードで検索していることがわかります。したがって、インデクサ上でそれが正しくない場合、それらの結果は表示されません。動作するクエリの出力の例については、Manual Search XML Outputを参照してください。

- Manual Search XML Output



```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- トレースログスニペット

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|Searching 1 indexers for [The Fix : S01E01]
2021-03-20 13:15:23.6|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- 検索の完全なトレースログ

```none
2022-04-24 20:14:26.7|Info|NzbSearchService|Searching 1 indexers for [Fairy Tail : S02E91 (91)]
2022-04-24 20:14:26.7|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'proxyenabled' defaultValue:'False'
2022-04-24 20:14:27.2|Trace|HttpClient|Res: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91: 200.OK (524 ms)
2022-04-24 20:14:27.2|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.HDTV.x264
2022-04-24 20:14:27.2|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.720p.HDTV.x264
2022-04-24 20:14:27.2|Debug|NzbSearchService|Total of 2 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:27.2|Debug|NzbSearchService|Setting last search time to: 11/20/2019 20:14:27
2022-04-24 20:14:27.2|Info|DownloadDecisionMaker|Processing 2 releases
2022-04-24 20:14:27.2|Trace|DownloadDecisionMaker|Processing release 1/2
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.HDTV.x264' from 'NZBgeek'
2022-04-24 20:14:27.2|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.HDTV.x264'
2022-04-24 20:14:27.2|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.2|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.2|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.2|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.HDTV.x264
2022-04-24 20:14:27.2|Debug|Parser|Quality parsed: SDTV v1
2022-04-24 20:14:27.2|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.HDTV.x264'
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.HDTV.x264': 0
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.HDTV.x264
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.HDTV.x264, meets size constraints.
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.2|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.2|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. SDTV v1
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.HDTV.x264
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.HDTV.x264] No restrictions apply, allowing
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.2|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.2|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.2|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.2|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] SDTV is not wanted in profile
2022-04-24 20:14:27.2|Trace|DownloadDecisionMaker|Processing release 2/2
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.HDTV.x264' from 'NZBgeek'
2022-04-24 20:14:27.2|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.HDTV.x264'
2022-04-24 20:14:27.2|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.2|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.2|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.2|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.HDTV.x264
2022-04-24 20:14:27.2|Debug|Parser|Quality parsed: HDTV-720p v1
2022-04-24 20:14:27.2|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.HDTV.x264'
2022-04-24 20:14:27.2|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.HDTV.x264': 0
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.HDTV.x264
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.2|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.HDTV.x264, meets size constraints.
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.2|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.2|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.2|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. HDTV-720p v1
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.HDTV.x264
2022-04-24 20:14:27.2|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.HDTV.x264] No restrictions apply, allowing
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.2|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.2|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.2|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.2|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.2|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'autounmonitorpreviouslydownloadedepisodes' defaultValue:'False'
2022-04-24 20:14:27.2|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:27.2|Trace|ConfigService|Using default config value for 'downloadpropersandrepacks' defaultValue:'PreferAndUpgrade'
2022-04-24 20:14:27.2|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (509 ms)
2022-04-24 20:14:27.2|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (509 ms)
```

- In the above case, the releases `Fairy.Tail.S02E91.HDTV.x264` and `Fairy.Tail.S02E91.720p.HDTV.x264` are being rejected because they do not meet the quality requirements specified in the profile. The specific rejection reason is `[Permanent] SDTV is not wanted in profile` for the first release and `[Permanent] HDTV-720p is not wanted in profile` for the second release.
- To resolve this issue, you can do one of the following:
  - Adjust the quality requirements in the profile to include the desired qualities. For example, if you want to allow SDTV and HDTV-720p qualities, you can add them to the profile.
  - Make sure the releases are named correctly according to the quality requirements specified in the profile. In this case, the releases should be named `Fairy.Tail.S02E91.SDTV.x264` and `Fairy.Tail.S02E91.720p.HDTV.x264` to match the desired qualities.
  - If the releases are consistently named incorrectly, you may need to check the settings of your indexer or download client to ensure they are configured correctly.

- シリーズパックはサポートされていません
- 複数のシーズンパックはサポートされていません
- 多くの場合、Sonarrは返された結果を既知のシリーズに一致させることができません。これらの場合、ログは以下のようになります。これらは手動で取得し、おそらく手動でインポートする必要があります。ログで確認するキーフレーズは、`|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`です。

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### トラッカーがRawSearch Capsを必要としています

- Sonarrは`9 1 1`を検索していますが、トラッカーには`9-1-1`や`John s Show`、`John's Show`の結果しかありません
- これは、トラッカーが通常の標準化された検索をサポートしていないためです
- 解決策は、トラッカーの定義の検索機能を更新して、[RawSearchを必要とし、サポートすることを示すようにすることです](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackettはこのフラグをサポートしていますが、機能を追加するためにJackettに機能リクエストをオープンする必要があります
- Prowlarrもこのフラグをサポートしていますが、機能を追加するためにProwlarrに機能リクエストをオープンする必要があります

### シリーズにエイリアスが必要です

リリースは「The Series Name」としてアップロードされる場合、TVDBでは「Series Name」などのシリーズ名の違いがあります。[このFAQエントリ](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x)を参照してください。

### シリーズにXEMマッピングが必要です

リリースは「Series Title S02E45」や「Other Series Title S2022E42」としてアップロードされる場合、TVDBではこのエピソードが「Series Title S03E01」や「Other Series Title S03E42」として表示されます。[このFAQエントリ](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)を参照してください。

### シリーズのタイプが間違っています

シリーズのタイプは、Sonarrの検索方法に影響を与えます。シリーズのタイプは、インデクサーでのリリース方法に基づいて選択する必要があります。
[詳細については、このFAQエントリを参照してください](/sonarr/faq#whats-the-different-series-types)

> **アニメ**シリーズタイプを使用する場合、[標準タイプでもインデクサーを検索することができます](/sonarr/settings#indexers)
{.is-info}

#### デイリー

ログには `Searching indexers for [The Witcher : 2021-12-20]` と表示されます。

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### 標準

ログには `Searching indexers for [The Witcher : S01E09]` と表示されます。

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### アニメ

ログには `Searching indexers for [The Witcher : S01E09 (09)]` と表示されます。

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### メディアが監視されていません

ログには次のような内容が表示されます。

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

シリーズ/シーズン/エピソードは監視されていません。シリーズ、シーズン、およびエピソードの監視状態を確認してください。

> シーズンパックは、すべてのエピソードが監視されており、シーズンパックがすべての既存のエピソードをアップグレードするか、すべてのエピソードが欠落している場合にのみ取得されます。
{.is-info}

### クエリが成功しましたが、結果が返されませんでした

「クエリは成功しましたが、インデクサーから結果が返されませんでした。これはインデクサーまたはインデクサーのカテゴリ設定に問題がある可能性があります。」というメッセージが表示されます。

これは、インデクサーが構成したカテゴリ内の結果を返さないために発生します。

### カテゴリが間違っています

カテゴリが間違っていることは、インデクサー/トラッカーの手動検索では結果が表示されるが、\*Arrには表示されないという問題の最も一般的な原因です。インデクサー/トラッカーは、検索結果にカテゴリを表示するはずであり、これが何が欠けているかを特定するのに役立ちます。JackettやProwlarrを使用している場合、各トラッカーには特定のサポートされているカテゴリのリストがあります。Sonarrでエントリを編集する際に、カテゴリのリストを1つのブラウザウィンドウで表示しておくと便利です。

> インデクサーの設定で「アニメカテゴリ」が空白の場合、インデクサーはアニメシリーズタイプの検索に使用されません。
> 同様に、「カテゴリ」がインデクサーの設定で空白の場合、インデクサーは標準またはデイリーシリーズタイプの検索に使用されません。
{.is-info}

### 間違った結果

インデクサーが関連のない結果を返すことがあります。Sonarrは検索の制限を設定してシリーズに絞り込むため、返される結果が完全に関連性のない場合や、ほとんど関連性があるが一部の間違った結果がある場合があります。前者は通常インデクサーの問題であり、トレースログから原因を特定することができます。そのインデクサーを無効にして問題を報告することができます。後者は通常、カテゴリに分類されたリリースであり、インデクサー/トラッカーで報告できるものです。

EZTVなどの一部のトラッカーは、クエリに完全な一致がない場合にランダムな結果を返すことがあります。これに対する解決策はありません。

### 結果が見つからない

Sonarrに表示されないが、サイトで見つけることができる結果がある場合、問題は次のいずれかの可能性です。

- [カテゴリが間違っている - 上記を参照してください](#wrong-categories)
- ID（IMDbId、TVDBIdなど）に基づいた検索が行われ、インデクサーがリリースを正しくそのIDにマッピングしていない場合。これはインデクサーだけが解決できる問題です。彼らはリリースが正しい適用可能なIDにマッピングされるようにする必要があります。
- Sonarrが検索している方法とは異なる方法で検索している可能性があります。Sonarrがクエリをどのように検索しているかは、トレースログから確認できます。テキストベースのクエリは一般的に `q=words%20and%20things%20here` の形式であり、この文字列はHTTPエンコードされており、オンラインのHTMLデコード/エンコードツールを使用して簡単にデコードできます。
- RSSフィードの新しいアップロードのチャンクが欠落している。ログは次のように表示され、警告のイベントが記録されます。

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### 証明書の検証

ほとんどのインデクサー/トラッカーにはhttps経由で接続する必要があるため、システム上で正常に機能する必要があります。つまり、タイムゾーンと時刻の両方が正しく設定されている必要があります。また、システムの証明書も最新である必要があります。

### レート制限に達する

VPNやプロキシを介して実行している場合、他の多くの人々と競合している可能性があります。これらの人々は、theXEMやインデクサー/トラッカーなどのサービスを利用しようとしています。レート制限とDDOS保護は、IPアドレスごとに行われることがよくあります。VPN/プロキシの出口ポイントは*1つの*IPアドレスです。中国、オーストラリア、南アフリカなどの抑圧的な国以外では、VPN/プロキシは必要ありません。

RarbgはAPI内で何らかのレート制限を持つ傾向があり、結果が表示されないことがあります。

### IPブロック

レート制限と同様に、特定のインデクサー（Nyaaなど）はIPアドレスを完全にブロックする場合があります。これは通常、半永久的なものであり、解決策はISPまたはVPNプロバイダから新しいIPを取得することです。

### Jackettの/allエンドポイントの使用

Jackettの`/all`エンドポイントは便利ですが、それ以外の利点はありません。その他のすべては潜在的な問題ですので、個々のトラッカーを個別に追加する必要があります。または、JackettとNZBHydra2の代替として[Prowlarr](/prowlarr)をご覧ください。

[Jackett自体も、/allは避けるべきであり、使用してはいけないと言っています。](https://github.com/Jackett/Jackett#aggregate-indexers)

/allエンドポイントの使用には利点はありません（管理のオーバーヘッドが削減されること以外）、デメリットのみがあります。

- インデクサー固有の設定（カテゴリ、検索モードなど）を制御できなくなります
- 検索モード（IMDB、クエリなど）を混在させると、低品質の結果が発生する可能性があります
- インデクサー固有のカテゴリ（100000以上）は使用できません。
- 遅いインデクサーは全体の結果を遅くします
- 合計結果は1000に制限されます
- 関連のない結果
- 結果が見つからない

それぞれのインデクサーを個別に追加することで、カテゴリをインデクサーごとに細かく調整することができます。これは、`/all`エンドポイントを使用する場合、間違ったカテゴリがいくつかのトラッカーでエラーを引き起こす可能性があるためです。Sonarrでは、ページネーションがサポートされている場合は各インデクサーが1000の結果に制限され、サポートされていない場合は100の結果に制限されます。そのため、Jackettにトラッカーを追加するにつれて、結果が切り取られる可能性が高くなります。最後に、`/all`の中の1つのトラッカーがエラーを返すと、それを無効にして結果が得られなくなります。

### 単一のエントリとしてNZBHydra2を使用する

NZBHydra2を単一のインデクサーエントリ（つまり、NZBHydra2の中に多くのインデクサーがある場合）として使用する場合、Jackettの`/all`エンドポイントと同じ問題が発生します。

### インデクサーが検索されていない

- インデクサーが検索されていない場合、おそらくクエリタイプをサポートしていないためです。最も一般的な例は、Nyaaがクエリ検索のみをサポートし、シーズン/エピソード検索をサポートしていないことです。トレースログは、再起動後の最初の検索後に、インデクサーが持っているまたは持っていない機能を示します。

### Jackettの手動検索でより多くの結果が見つかる

- [このFAQエントリを参照してください](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### リリースプロファイルが尊重されていない

プロファイルが無視されているように見える原因はいくつかあります。最も一般的な原因は、リリースプロファイルのインデクサー制限に関連しています。インデクサーはデータとともに保存されないため、メディアライブラリ内のメディアに対しては「優先ワード」スコアがゼロになりますが、「RSS」と検索時には適用されます。同様に、「含む必要がある」または「含まない必要がある」制限は、そのインデクサーにのみ適用されます。それ以外は問題ありません。これにより、リリースプロファイルが無視されるか、アップグレードループが発生する場合があります。

### リストにない問題

一般的なアクセス許可とネットワーキングのトラブルシューティングコマンドについては、[ガイド](/permissions-and-networking)を参照してください。それ以外の場合は、ディスコードのサポートチームと相談してください。これが一般的な問題である可能性がある場合は、ウィキに追加することを提案してください。

## エラー

インデクサーを追加する際に表示される一部の一般的なエラーは次のとおりです。

### The underlying connection was closed: An unexpected error occurred on a send

これは、インデクサーが現在の.NETバージョンでサポートされていないSSLプロトコルを使用しているためです。[Sonarr => System => Status](/sonarr/system#status)で見つかる現在の.NETバージョンを確認してください。

### The request timed out

Sonarrがインデクサーから応答を受け取っていません。

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

これは次の原因でも発生する可能性があります。

- VPNの設定が誤っているか、使用方法が間違っている
- プロキシの設定が誤っているか、使用方法が間違っている
- ローカルのDNSの問題 - 異なるDNSプロバイダに変更してみてください
- ローカルのIPv6の問題 - 通常、IPv6は有効になっていますが、機能していません
- Privoxyの使用とその設定が正しくない場合

### リストにない問題

一般的なアクセス許可とネットワーキングのトラブルシューティングコマンドについては、[ガイド](/permissions-and-networking)を参照してください。それ以外の場合は、ディスコードのサポートチームと相談してください。これが一般的な問題である可能性がある場合は、ウィキに追加することを提案してください。