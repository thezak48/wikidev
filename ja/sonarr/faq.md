<!-- How do I change from the Windows Service to a Tray App? -->
## Windowsサービスからトレイアプリに変更するにはどうすればいいですか？

- Sonarr can be run as a Windows Service or as a Tray Application. If you want to switch from running Sonarr as a Windows Service to a Tray App, follow these steps:

1. Stop the Sonarr service. You can do this by opening the Services app (`services.msc`), finding the Sonarr service, and stopping it.
2. Open Sonarr's settings page in your web browser. The URL should be `http://localhost:8989/sonarr/settings`.
3. Scroll down to the "General" section.
4. In the "Startup" dropdown, select "Start Sonarr on Login".
5. Click the "Save Changes" button at the bottom of the page.
6. Restart your computer to ensure that Sonarr starts as a Tray App on login.

- After following these steps, Sonarr will start as a Tray App whenever you log in to your computer. You can access Sonarr by clicking on its icon in the system tray.

> Note: If you want to switch back to running Sonarr as a Windows Service, simply follow the same steps but select "Run Sonarr as a Windows Service" in the "Startup" dropdown.

1. Sonarrをシャットダウンします。
1. Sonarrディレクトリ内にあるserviceuninstall.exeを実行します。
1. 管理者としてSonarr.exeを1回実行して、適切な権限を与え、ファイアウォールを開きます。完了したら、Sonarrを閉じて通常通り実行できます。
1. (オプション) Sonarr.exeのショートカットをスタートアップフォルダにドロップして、起動時に自動的に起動するようにします。

## Sonarrのバックアップ/リストアはどのように行いますか？

### Sonarrのバックアップ

#### 組み込みのバックアップを使用する

- SonarrのUIでSystem => Backupに移動します。
- バックアップボタンをクリックします。
- バックアップが作成されたら、zipファイルをダウンロードして安全な場所に保存します。

#### ファイルシステムを直接使用する

- SonarrのAppDataディレクトリの場所を見つけます。
  - SonarrのUIでSystem => Aboutに移動します。
  - [SonarrのAppDataディレクトリ](/sonarr/appdata-directory)
- Sonarrを停止します。これにより、データベースが破損するのを防ぎます。
- 内容を安全な場所にコピーします。

### バックアップからのリストア

> 異なるパスを使用するOSにリストアすることはできません（WindowsからLinux、LinuxからWindows、WindowsからOS X、またはOS XからWindows）。OS XとLinuxの間で移動する場合は、両方ともWindowsが使用する`\`ではなく`/`を含むパスを使用しているため、動作する可能性がありますが、サポートされていません。データベース内のすべてのパスを手動で編集するか、[Toolbarr](https://github.com/Notifiarr/toolbarr)を使用する必要があります。
{.is-warning}

#### zipバックアップを使用する

- Sonarrを再インストールします（該当する場合/すでにインストールされていない場合）。
- Sonarrを実行します。
- System => Backupに移動します。
- バックアップを復元を選択します。
- Choose Fileを選択します。
- バックアップのzipファイルを選択します。
- リストアを選択します。

#### ファイルシステムのバックアップを使用する

- Sonarrを再インストールします（該当する場合/すでにインストールされていない場合）。
- SonarrのAppDataディレクトリの場所を見つけます。
  - Sonarrを1回実行し、UIでSystem => Aboutに移動します。
  - [SonarrのAppDataディレクトリ](/sonarr/appdata-directory)
- Sonarrを停止します。
- AppDataディレクトリの内容を削除します（.db-wal/.db-journalファイルも含む）。
- バックアップからリストアします。
- Sonarrを起動します。
- パスが同じである限り、すべての設定が以前の状態から引き継がれます。

#### Synology NASでのファイルシステムのリストア

> 注意: SynologyでのリストアにはLinuxの知識とRoot SSHアクセスが必要です。
{.is-warning}

- Sonarrを再インストールします（該当する場合/すでにインストールされていない場合）。
- SonarrのAppDataディレクトリの場所を見つけます。
  - Sonarrを1回実行し、UIでSystem => Aboutに移動します。
  - [SonarrのAppDataディレクトリ](/sonarr/appdata-directory)
- Sonarrを停止します。
- SSHを介してSynology NASに接続し、rootとしてログインします。

> インストールによっては、ユーザーが以下のコマンドと異なる場合があります: `chown -R sc-Sonarr:Sonarr *` {.is-info}

- 次のコマンドを実行します。

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- ファイルの権限を更新します。

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Sonarrを起動します。

## ヘルプ、自分自身をロックアウトしてしまいました

{#help-i-have-forgotten-my-password}

> Sonarrのv4では、`AuthenticationMethod`タイプの`None`は使用できません。詳細については、[FAQ](/sonarr/faq-v4)を参照してください。
{.is-info}

パスワードを忘れた場合、認証を無効にするためには`config.xml`を編集する必要があります。このファイルは[SonarrのAppDataディレクトリ](/sonarr/appdata-directory)内にあります。

1. テキストエディタでconfig.xmlを開きます。
1. 認証方法の行を探します。行は`<AuthenticationMethod>Basic</AuthenticationMethod>`または`<AuthenticationMethod>Forms</AuthenticationMethod>`になります。
1. `AuthenticationMethod`行を`<AuthenticationMethod>None</AuthenticationMethod>`に変更します。
1. Sonarrを再起動します。
1. Sonarrはパスワードなしでアクセスできるようになります。UIの「Settings: General」に移動し、ユーザー名とパスワードを設定してください。

## なぜ2つのファイルがあるのですか？ \| ダウンロードフォルダにファイルが残っているのはなぜですか？

これは正常です。ハードリンクをサポートするセットアップでは、二重のスペースは使用されません。以下はトレント処理の動作です。

1. Sonarrはクライアントにダウンロードリクエストを送信し、設定したラベルまたはカテゴリ名と関連付けます。例: movies、tv、series、musicなど。
1. Sonarrは、そのカテゴリ名を使用してダウンロードクライアントのアクティブなダウンロードを監視します。この監視は、ダウンロードクライアントのAPIを介して行われます。
1. 完了したファイルは元の場所に残され、ファイルをシードするために使用できます（シードの比率や時間は、ダウンロードクライアントまたは特定のダウンロードクライアントの設定から調整できます）。ファイルがメディアフォルダにインポートされると、セットアップによってファイルがハードリンクされるか、ハードリンクがサポートされていない場合はコピーされます。
1. Sonarrの設定で「完了したダウンロードの処理 - 完了後に削除」オプションが有効になっている場合、Sonarrはダウンロードクライアントから元のファイルとトレントを削除しますが、ダウンロードクライアントがシードが完了し、トレントが停止（一時停止）されたことを報告している場合のみです。ダウンロードクライアントの設定方法については、[TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/)を参照してください。

> ハードリンクはデフォルトで有効になっています。[ハードリンクは追加のディスクスペースを使用しません](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)。完了したダウンロードディレクトリとメディアライブラリのファイルシステムとマウントは同じである必要があります。ハードリンクの作成に失敗した場合やハードリンクがサポートされていない場合は、ファイルのコピーにフォールバックします。
{.is-info}

## 特定の機能/バグが修正されたと表示されていますが、なぜ表示されないのですか？

Sonarrには、`main`と`develop`の2つのメインコードブランチがあります。

- `main`は、`develop`ブランチが安定しているときに定期的にリリースされます。
- `develop`は、プレリリースのテストと、エッジでの使用を希望するユーザー向けです。機能が`develop`にマークされると、`develop`ブランチを実行しているユーザーのみで利用可能であり、`main`（`main`）に移動した後に公式にリリースされます。

## エピソードの進行状況はどのように計算されますか？

- エピソードのカウントには、エピソード数（エピソードカウント）とファイルを持つエピソード数（エピソードファイルカウント）の2つのパートがあります。それぞれが異なるロジックを使用して、シリーズまたはシーズンの全体的な進行状況を示します。

  - エピソードカウント => エピソードが既に放送され、かつ監視されている または - エピソードにファイルがある
  - エピソードファイルカウント => エピソードにファイルがある

- シリーズに10のエピソードがあり、すべてが放送されており、ファイルがない場合、エピソードは0/10となります。そのシリーズのすべてのエピソードを監視解除すると、0/0になります。そのシリーズのすべてのエピソードを取得した場合、エピソードが監視されているかどうかに関係なく、10/10のエピソードがあります。

## 別のコンピュータからSonarrにアクセスするにはどうすればよいですか？

- デフォルトでは、Sonarrはすべてのシステムからのリクエストを受け付けません（管理者として実行していない場合）。ローカルホストのみでリクエストを受け付けます。これは、Sonarrが使用するWebサーバーがWindowsと統合する方法によるものです（現在の代替手段にも同様のことが当てはまります）。Sonarrを管理者として実行すると、Windowsに正しく登録され、ファイアウォールのポートが開かれるため、ネットワーク上の他のシステムからアクセスできるようになります。管理者として実行する必要があるのは1回だけです（ポートを変更する場合は再実行する必要があります）。

## なぜSonarrはシリーズ情報を頻繁に更新するのですか？

- Sonarrは、シリーズとエピソードの情報を12時間ごとに更新します。これは積極的に見えるかもしれませんが、非常に重要なプロセスです。TVDbプロキシからのデータの更新は重要です。新しいエピソード情報が同期されます（放送日、エピソード数、ステータス（継続中/終了））。放送されていない番組でも、新しい情報が更新されます。
- ディスクのスキャンはそれほど重要ではありませんが、Sonarrによってソートされていない新しいファイルや削除されたファイルを検出するために使用されます。
- 最も時間がかかるのは情報の更新です（合理的なディスクアクセス速度を想定しています）。エピソードの数によって処理時間が長くなります。

> このタスクを無効にすることはできません。このタスクが実行される時間が十分に長いと感じる場合、問題の解決にはこのタスクを停止するのではなく、他の問題が発生している可能性があります。
{.is-warning}

## アクティビティの横に数字が表示されているのはなぜですか？

この数字は、ダウンロードクライアントのキュー内のエピソードの数と、まだインポートされていない履歴の最後の60アイテムを示しています。数字が青色の場合、正常に動作しており、エピソードが完了したときにインポートされるはずです。黄色はエピソードに警告があることを意味します。赤はエラーが発生したことを意味します。黄色（警告）と赤（エラー）の場合、問題の内容を確認するためにアクティビティのキューを確認する必要があります（アイコンの上にカーソルを合わせると詳細が表示されます）。
- キューまたは履歴からアイテムを削除すると、それらはSonarrのキューから削除されます。

## シリーズタイプにはどのような違いがありますか？

- シリーズタイプは、Sonarrがシリーズを検索する方法に影響を与えます。シリーズタイプは、インデクサー上でシリーズがリリースされる方法に基づいており、必ずしもシリーズの真の「タイプ」ではありません。
- ほとんどの番組は`Standard`である必要があります。通常、日付を使用してリリースされるデイリーショーには`Daily`を使用します。最後に、アニメでは`Anime`を使用することが*通常*ですが、問題が発生する場合は`Standard`の方が適している場合もあるため、*他の*方を試してみてください。
- シリーズタイプがアニメに設定されている場合、有効なインデクサーにアニメのカテゴリが設定されていない場合、インデクサーはスキップされ、検索されていないように見えることがあります。
- アニメタイプにはシーズンパックやシーズンの概念がなく、各エピソードが個別に検索されます。
- すべてのインデクサーがシーズン/エピソード（標準）の検索をサポートしているわけではありません。
- シリーズタイプは、Mass Editorまたはシリーズを表示しているときの「編集」から変更できます。シリーズタイプはインポート時に選択できます。

- **Anime** - 絶対エピソード番号を使用してリリースされたエピソード
- **Daily** - 毎日またはそれより低い頻度でリリースされるエピソード（年-月-日の形式）
- **Standard** - SxxEyyパターンでリリースされるエピソード

以下は各シリーズタイプの例です。特定の違いを太字で示しています。

> アニメのシリーズタイプを使用している場合、[標準タイプでもインデクサーを検索することができます。](/sonarr/settings#indexers)
{.is-info}

#### Daily

ログには`Searching indexers for [The Witcher : 2021-12-20]`と表示されます。

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

ログには`Searching indexers for [The Witcher : S01E09]`と表示されます。

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

ログには`Searching indexers for [The Witcher : S01E09 (09)]`と表示されます。

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## シリーズフォルダの名前を変更するにはどうすればよいですか？

{#rename-folders}

> 同じ手順は、シリーズのパスを移動/変更する場合にも適用されます{.is-info}

Sonarrが既にいくつかのシリーズフォルダを作成した後にシリーズ名の形式を調整した場合、Sonarrは自動的に既存のフォルダの名前を変更しません。これらのフォルダの名前を変更するためには、次の手順を実行する必要があります。

1. シリーズ
1. Mass Editor
1. フォルダの名前を変更する必要があるシリーズを選択します。
1. ルートフォルダを現在のルートフォルダと同じに変更します。
1. 「はい、ファイルを移動する」を選択して、ファイルも移動します。

> PlexやEmbyを使用している場合、これによりイントロ、サムネイル、チャプター、プレビューメタデータの再検出がトリガーされます。
{.is-warning}

## Sonarrを更新するにはどうすればよいですか？

- 設定に移動し、一般タブを表示し、詳細設定を表示します（保存ボタンの横のトグルを使用します）。

1. 更新セクションでブランチ名を`main`または`develop`に変更します。
1. 保存します。

*これにより、そのブランチのビルドがすぐにインストールされるわけではありません。次回の更新時にインストールされます。*

- main - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (デフォルト/安定版): このバージョンは、夜間（`develop`）ブランチでユーザーによってテストされ、重大な問題がないことが確認されています。このブランチは、ほとんどのユーザーに使用されるべきです。GitHubでは、これは`main`ブランチです。
- develop - ![Current Develop/Nightly](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (アルファ/不安定) : これは非Dockerユーザーにとっては、現在のv3リリースと同じです。

> ~~**警告: `main`に切り替えた後は、`main`に戻すことはできません。** GitHubでは、これは`develop`ブランチです。~~
{.is-danger}

- v4 develop - ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (アルファ/不安定) : **非Dockerユーザーの場合、ブランチは`develop`です。Dockerユーザーの場合、これはおそらく`develop`タグです**。これはSonarr v4ベータ版の最新情報です。コードがコミットされ、すべての自動テストに合格した直後にリリースされます。このビルドはまだ私たちや他のユーザーによって使用されていない場合があります。実行できない場合もあるため、このブランチは上級ユーザーにのみ推奨されます。このブランチでは、問題が発生することが予想されるため、問題の解決と自己調査が必要です。GitHubでは、これは`develop`ブランチです。

> **警告: v3から直接v4にアップグレードすることはできず、Sonarr v4をインストールする必要があります。**
{.is-info}

- 注意: Dockerを使用している場合、コンテナタグの末尾に`:release`、`:latest`、`:nightly`、または`:develop`を追加します。

|                                                                    | `main` (安定版) ![Current Main/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (ベータ版) ![Current v3 Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 ベータ版) ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### 新しいバージョンのインストール

#### ネイティブ

1. システムに移動し、[アップデート] タブを開きます。
1. インストールされていない新しいバージョンには、その横にアップデートボタンが表示されます。そのボタンをクリックすると、アップデートがインストールされます。

> v3 からベータ版の v4 にはアップデートできず、手動でインストールする必要があります。[v4 ベータ版の発表](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)を参照してください。
{.is-info}

#### Docker

1. タグを再プルし、コンテナを更新します。

## `develop` から `main` に戻ることはできますか？

- 以下のエントリを参照してください。

## ブランチ間を切り替えることはできますか？

> （ほぼ）常にリスクが増えます。{.is-info}

- `main` から `develop` に切り替えることができます。
- 以下を参照するか、開発チームに確認して、指定されたビルドの `develop` から `main` に切り替えることができるかどうかを確認してください。
- これらの手順に従わないと、Sonarr が使用できなくなったりエラーが発生する可能性があります。以下のエラーメッセージが表示された場合は、古い \*Arr バージョンで新しいデータベースを使用している可能性があります。サポートされていません。以前のバージョン以上の \*Arr バージョンにアップグレードするか、それ以降のバージョンにアップグレードしてください。
  - エラーメッセージの例:
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - その他、欠落している列やテーブルに関する類似のデータベースエラー。
- **2022年8月7日の更新**
  - `3.0.9.1549` が main/安定版としてリリースされました。
  - develop で `3.0.9.1549` またはそれ以下のバージョンを使用している場合、安全に main にダウングレードできます。
  - より新しいバージョンを使用している場合、新しい安定版がリリースされるまで nightly/develop にとどまる可能性があります。上記のバージョンを超えてアップグレードする前のバックアップがある場合は、バックアップを再インストールして復元できます。安全にダウングレードできるかどうかは、開発チームに確認してください。

# Sonarr とシリーズの問題 + メタデータ

## Sonarr はシーンナンバリングの問題 (American Dad! など) をどのように処理しますか？

### Sonarr がシーンナンバリングの問題を処理する方法

- Sonarr は、ユーザーがシーン（ファイルを投稿する人々）と TheTVDb（通常はネットワークのナンバリングに従う）の間のマッピングを作成できるコミュニティ駆動のサイトである [TheXEM](http://thexem.info/) を利用しています。既に多くの番組が登録されていますが、別の番組を追加することも簡単で、通常は数日以内に変更が承認されます（正しい場合）。TheXEM は、エピソードのナンバリングの違い（エピソードが特別なものかどうかについての意見の相違）や、エピソードが S10E01 としてリリースされたが、TheTVDb では同じエピソードが S2017E01 としてリストされているなど、シーズン番号の違いを修正するために使用されます。
- XEM は、リリースグループ（俗に「シーン」と呼ばれる）のナンバリングが TVDb のナンバリングと一致しない場合に問題を修正し、Sonarr が正常に動作しないようにします。[XEM](http://thexem.info) は、Sonarr が参照するマップを作成します。
- リリースグループは、エピソードを個別にリリースするため、2つのエピソードを1つのファイルにまとめますが、TVDb では各エピソードを個別にマークします。
- リリースグループはシーズンに年を使用します（S2010）、TVDb では S01 を使用します。
- [XEM](http://thexem.info) はほとんどの場合に機能し、問題が発生していることを気づかずにスムーズに動作します。ただし、ほとんどの場合、問題のある例外が常に存在することを覚えておいてください。

> 特定のインデクサーまたはリリースグループが `Scene`（XEM）ではなく TVDb に従う場合は、シーンマッピングフォームを使用してそれらを提出してください。
{.is-info}

- [Services Requested Mappings *エイリアスとリリースがすでにリクエストまたは追加されていないか確認してください*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Services Scene Mapping Request Form *新しいエイリアスのリクエストを作成します。フォームを完全に記入してください*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### 問題のある番組

> これは、シーンマッピングに問題がある番組のすべてを網羅したリストではありませんが、一部の一般的な番組です。
{.is-info}

- 以下は、問題のある番組の一部です。
- American Dad {#problemshow-americandad}
  - ネットワークのシーズン変更により、American Dad は通常、リリースと TVDb の間で 1 シーズンずれています。詳細については、XEM マップを参照してください。
  - [American Dad](https://thexem.info/xem/show/4948) は、この執筆時点で TVDb に基づく S19 または Scene に基づく S18 です。そのため、Sonarr でシーズン 19 を検索すると、XEM マップのため、**S18 の結果のみ**が返されます。
  - シーズン 19 のエピソードを持つインデクサー / リリースグループがある場合は、シーンマッピングフォームを使用してそれらを提出し、すでにリクエストされていないことを確認してください。
    - [Services Requested Mappings *エイリアスとリリースがすでにリクエストまたは追加されていないか確認してください*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Services Scene Mapping Request Form *新しいエイリアスのリクエストを作成します。フォームを完全に記入してください*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - 2つのエピソードを含むファイルと、TVDb の単一のエピソードがありますが、すべてのエピソードが2つずつではないため、マップが誤って追加され、どれが単一のエピソードでどれが2つのエピソードかを指し示すことができなくなる場合があります。
- Pokémon {#problemshow-pokemon}
  - [Pokemon](http://thexem.info/xem/show/4638) は TheXEM で「吹き替え」のエピソードを追跡しています。したがって、字幕付きのエピソードを望む場合は、運が悪いかもしれません。特定のリリースグループが TVDb に従っており、XEM マッピングではない場合は、シーンマッピングフォームを使用してそれらを提出し、すでにリクエストされていないことを確認してください。
    - [Services Requested Mappings *エイリアスとリリースがすでにリクエストまたは追加されていないか確認してください*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Services Scene Mapping Request Form *新しいエイリアスのリクエストを作成します。フォームを完全に記入してください*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb にはスペインのネットワークからのオリジナルの放送順がありますが、Netflix が権利を買い取り、シリーズを異なるエピソード数に再編集しました。これにより、「シーズン 5」が既存の「シーズン 3」のエピソードに上書きされることがあります。[詳細はこの Reddit スレッドで確認できます](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- Kamen Rider {#problemshow-kamenrider}
  - この番組は、アンソロジーエントリ（[TVDb ID 74096](https://thetvdb.com/series/kamen-rider)）が Sonarr の自動化に使用されるべきです。なぜなら、この番組はアンソロジーエントリ（すべてのシーズンをまとめたもの）と、TVDb 上で個別のシーズンとしてリストされている個別のシーズンエントリの両方があるためです。アンソロジーエントリには [TheXEM](https://thexem.info/xem/show/5376) で個別のシーズン名のマッピングがあるため、個別のシーズンエントリを手動でダウンロードしてインポートすることはできません。
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - Bleach: Thousand-Year Blood War の最新シーズンは、さまざまな名前付けスキームでリリースされており、自動化が困難で、既存のエピソードの一部を上書きする可能性があります。自動化するには、リリースグループが次のいずれかを行っている必要があります。
    - エピソードを S17Exx の番号付けでリリースしているか、
    - 正しいシーズン 2 シリーズタイトル（ここで見つけることができます <https://thexem.info/xem/show/5476>）でリリースを開始し、この新しいアークを絶対エピソード番号 1 で開始しているか。
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys は最初に 20 の小さなエピソードとして放送されましたが、後に 10 の長いエピソードとして再放送されました。これらの長い結合エピソードは特別番組として追加され、それに応じて名前が付けられる必要があります（S00E01 など）。
- Horizon {#problemshow-horizon}
  - 1964 年以来、断続的にエピソードが放送されている番組です。これにより、マッピングが特に困難になります。[TheXEM](https://thexem.info/xem/show/5495) で確認できるようになっています。興味がある方は、Sonarr の Discord での元のディスカッションを[こちら](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312)で見つけることができます。
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023) は、Netflix で非線形のショーとしてリリースされました。つまり、ユーザーごとに異なる順序でシリーズを視聴できます。これにより、リリースグループが番組のエピソードの異なる順序を持つことになり、Sonarr がエピソードのマッピングを誤ってしまう可能性があります。そのため、Sonarr は自動的にエピソードを取得せず、エピソードを手動で取得してインポートする必要があります。エピソードのタイトルに基づいて一致させるか、最初の数秒をプレビューしてタイトルに一致するエピソードの「色」を確認することができます。

他の一般的な問題を抱える番組の例には、以下のようなものがあります。これらのほとんどは、TheXEMのマッピングによって解決できる可能性があります：Arrested Development、Kitchen Nightmares（US）、Mythbusters、Pawn Stars。

## なぜSonarrはシリーズXのエピソードファイルをインポートできないのですか？ / なぜSonarrはシリーズXのリリースを見つけられないのですか？

特定のシリーズのエピソードをSonarrが見つけられないかインポートできない理由はいくつかあります。

> SonarrはTVDbからエイリアスや翻訳（つまり、外国語のタイトル）を使用しません。
{.is-warning}

> **IDベースの検索をサポートするインデクサーの場合**、検索にはシリーズのTVDbIDまたはIMDbIDが使用されます。シリーズのタイトルやエイリアスは、IDベースの検索が結果を返さない場合にのみ使用されます。
{.is-info}

- Sonarrはタイトルを一致させることに依存しています。アップローダーはしばしば異なるタイトルでエピソードを投稿します。たとえば、「CSI: Crime Scene Investigation」は「CSI」として投稿されるため、Sonarrは助けなしでは名前を一致させることができません。これらは、Sonarrチームが管理しているScene Mappingによって処理されます。
- [問題のある番組とリリースグループ対TVDbの番号付けの問題に関するFAQエントリを確認してください](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

> **すべての日本のアニメには、[thexem.info](https://thexem.info)にエイリアスを追加する必要があります**。新しいマッピングをリクエストするための他のシリーズの手順については、以下の手順を参照してください。詳細な情報は、Sonarr Discordの#XEMディスコードチャンネルでXEMのメンバーのいくつかから見つけることができます。
{.is-danger}

- [サービスリクエストマッピング *エイリアスとリリースがすでにリクエストまたは追加されていないことを確認してください*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [サービスシーンマッピングリクエストフォーム *エイリアスの新しいリクエストを作成します。フォームを完全に記入してください*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> 通常、サービスリクエストは1〜5日以内に追加されます
{.is-info}

> 日本のアニメのマッピングをリクエストしないでください。それにはXEMを使用してください。
> 詳細な情報は、Sonarr Discordの[\#XEMディスコードチャンネル](https://discord.gg/Z3D6u5hBJb)でXEMのメンバーのいくつかから見つけることができます。
{.is-danger}

> 非日本のシリーズがシーズンマッピングを必要とする場合（たとえば、S25E26としてリリースされたが、TVDBはS26E2としている場合）、XEMマッピングが必要です。これはサービスマッピングではできません。
{.is-info}

> TVDbのIDが`343189`および`252077`のシリーズ「Helt Perfekt」は、TVDbが同じ名前を持つ2つのシリーズに対して、TVDb自体のルールに違反しているため、自動化が困難です。シリーズの最初のエントリが名前を取得します。シリーズの将来のエントリは、シリーズ名に年を含める必要があります。ただし、リリース（大文字と小文字を区別するマッピング）Helt Perfektリリースには`NORWEGIAN`が含まれている場合は`252077`、`SWEDISH`が含まれている場合は`343189`にマッピングするためのシーン例外が追加されました。
{.is-info}

## TVDbが更新されてもSonarrが更新されないのはなぜですか？

{#tvdb}

- TVDbにはAPIの24時間キャッシュがあります。
- TVDbのAPIは、数時間かかるCDNキャッシュを介して展開する必要があります。
- SonarrのSkyhookには、それに加えて数時間のキャッシュがあります。
- さらに、SonarrはRefresh Seriesタスクを12時間ごとに実行します。このタスクは、システム=>タスクから手動で実行できます。「シリーズインデックス」から「すべて更新」を選択するか、特定のシリーズのページで手動で実行できます。

- したがって、TVDbの変更がSonarrに自動的に反映されるには、通常36〜48時間かかります（24 + 〜3 + 〜3 + 12）

- TVDbまたはエピソードがTVDbに存在しない場合、それらがSonarrインスタンスに表示されるまでに36〜48時間かかります。

{#missing-episodes}

- TVDbの更新が48時間以上前に行われたことを知っている場合は、[Discord](https://discord.sonarr.tv/)でディスカッションしてください。

## なぜシリーズを追加できないのですか？

{#why-can-i-not-add-a-new-series}

- TheTVDbが利用できない場合、Sonarrは検索結果を取得できず、検索して新しいシリーズを追加することはできません。TVDbIDを知っている場合は、IDで追加する方法についてUIで説明されています。
- Sonarrは、英語のタイトルを持たないシリーズを追加することはできません。TVDb IDを使用してシリーズを追加しようとする場合、TheTVDbにそのシリーズの英語のタイトルが存在しない場合は、そのシリーズを追加する必要があります。その後、[TVDbのキャッシュがクリアされるのを待つ必要があります](#tvdb)。
- ショーはテレビシリーズでなければなりません。映画ではなく、TVDbに存在する必要があります。IMDB、TMDB、または他の場所にある場合でも、TVDbにない場合はショーを追加できません。
- シリーズはTVDbに存在する必要があります。
- 特定のシリーズは、実際には主要なシリーズの継続とシーズンと見なされる場合があります。
  - いくつかの既知のシリーズ/シーズンは次のとおりです：
  - [Dexter New Bloodはシーズン9でした](https://thetvdb.com/series/dexter/seasons/official/9)が、[独自のシリーズになりました](https://thetvdb.com/series/dexter-new-blood)

## TVDbのIDを知っているのにシリーズを追加できないのはなぜですか？

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarrは、英語のタイトルを持たないシリーズを追加することはできません。TVDb IDを使用して追加しようとするシリーズに英語のタイトルがない場合、そのシリーズは見つかりません。TheTVDbにそのシリーズの英語のタイトルが存在しない場合は、追加する必要があります（利用可能な場合）。
- URL / シリーズを確認してください - Sonarrは映画をサポートしていません。映画には[Radarr](/radarr)を使用してください

## タイトルスラッグが使用中です

- このエラーの主な原因は2つあります。

## 重複した名前がありません

- このエラーは、TheTVDBで同じタイトルの2つのシリーズが名前付けられている場合によく発生します。この場合、2番目のシリーズにはシリーズタイトルに年が追加される必要があります。
  - シリーズA
  - シリーズA（2021年）
- これを修正するには、誰かがTVDbを更新するのを待つか、自分でTVDbを更新します。修正された後、**TVDbのモデレーターによって承認された後**、[TVDbのキャッシュがクリアされるまで（TVDbのAPIの問題により）30時間以上待つ必要があります。Sonarrで修正されたタイトルを使用できるようになります。

## 重複した名前の句読点

- 句読点の違いだけで区別される2つの似たような名前のシリーズでも、このエラーが発生します。この場合は、[Sonarr Discord](https://discord.sonarr.tv/)で報告してください。
  - Joe's Show（2022年）
  - Joes Show（2022年）

## エピソードに絶対番号がありません

- TVDbのエピソードには絶対番号が割り当てられていません。必要に応じてTVDbのシリーズを更新し、36〜48時間待ってから更新がTVDbの内部キャッシュからクリアされ、Sonarrにロードされるようにします。

## エピソードの放送時間

- Sonarr内で、ブラウザに表示されるエピソードの放送日時は、クライアントの時間/タイムゾーンに基づいています。すべての時間は、Sonarrからブラウザに送信されるときにUTC時間（ISO-8601形式）として送信されます。
- TVDbは、ストリーミングサービスを除いて、放送時間と日付が、主要な放送ネットワークの現地時間に基づいていることを定めています。[詳細については、TVDbのFAQエントリを参照してください](https://support.thetvdb.com/kb/faq.php?id=29)
- TVDbのエピソードの放送日と放送時間は、UTCに変換され、TVDbがシリーズに対して持つネットワークのタイムゾーン（SonarrチームによってSkyhookでマッピングされている）を使用します。
  - ネットワークがマッピングされていない場合は、TVDbの時間が米国EST（UTC-5）であると見なされます。
  - ネットワークのローカルタイムゾーンからブラウザのタイムゾーンに変換する際に放送時間が一致しない場合は、おそらくネットワークをSkyhookにマッピングする必要があります。[開発チームに連絡して、ネットワークのタイムゾーンを更新するためのサポートを受けてください](https://discord.sonarr.tv/)。

# Sonarrの一般的な問題

## パスは既存のシリーズにすでに設定されています

- ライブラリのインポートが「既存」と表示されるか、「パスは既存のシリーズに設定されています」というエラーが表示される場合があります。
- これは、既に別のシリーズに割り当てられているパスを追加しようとしたり、既存のシリーズのパスを編集しようとしたりした場合に発生します。
- おそらく、ユーザーがライブラリをインポートする際に一致しないシリーズを修正しなかったことが原因です。
- ライブラリの問題のあるパスにある映画を特定して修正します。
  - シリーズインデックス
  - テーブルビュー
  - オプション => 列としてパスを追加
  - ソートして、問題のあるパスにある映画を見つけます。
- または、既存のパスを使用してシリーズをSonarrから削除します。

## システムとログが無限に読み込まれる

- これは、easy-privacyブロックリストによるものです。これらは基本的に`/api/log?`を含むURLをブロックします。リストを確認し、そのリスト内のすべてのURLをブロックすることが合理的かどうかを判断してください。多くのURLが含まれており、サイトが壊れる可能性があります。これを広告ブロッカーで選択しました。簡単な解決策は、Sonarrが実行されているドメインをホワイトリストに登録することです。ただし、リストを確認することをお勧めします。

## 奇妙なUIの問題

- ライブラリページが何も表示されない、特定のビューやソートが機能しないなど、奇妙なUIの問題が発生した場合は、ChromeのシークレットウィンドウまたはFirefoxのプライベートウィンドウで表示してみてください。そこで正常に動作する場合は、特定のIP/ドメインのブラウザのキャッシュとクッキーをクリアしてください。詳細については、[キャッシュ、クッキー、およびローカルストレージのクリア](/useful-tools#clearing-cookies-and-local-storage)のウィキ記事を参照してください。

## WebインターフェースがWindowsのlocalhostでのみ読み込まれる

- Webインターフェースに<http://localhost:8989/>または<http://127.0.0.1:8989>でのみアクセスできる場合、少なくとも一度Sonarrを管理者として実行する必要があります。

## ポップアップが表示され、「config.xmlが破損しているため開けません」と表示されました。今どうすればいいですか？

- Sonarrは、起動時に設定ファイルを読み取ることができなかったため、`.xml`を[AppDataフォルダ](/sonarr/appdata-directory)から削除する必要があります。削除したら、Sonarrを起動し、デフォルトのポート（8989）で起動します。その後、一般設定ページで設定した設定を再構成する必要があります。

## 無効な証明書およびその他のHTTPSまたはSSLの問題

- Windows以外の場合、おそらくmonoの証明書が最新でなく、同期する必要があります。[インストール記事のmono sslに関するセクションを参照してください](/sonarr/installation#mono-ssl-issues)
- ダウンロードクライアントが機能しなくなり、「Localhost is an invalid certificate」というエラーが表示される場合は？
  - Sonarrは現在、SSL証明書を検証します。ダウンロードクライアントにSSL証明書が設定されていない場合、または自己署名のhttps証明書を使用していても、CA証明書がローカルの証明書ストアに追加されていない場合、Sonarrは接続を拒否します。無料の適切に署名された証明書は[let's encrypt](https://letsencrypt.org/)から入手できます。
  - ダウンロードクライアントとSonarrが同じマシンにある場合、ローカルネットワークではHTTPSを使用する必要はありませんので、最も簡単な解決策は接続のためのSSLを無効にすることです。ほとんどの場合、ローカルネットワークでは必要ありません。セキュリティの問題がない限り、不安全なSSLの設定を保持したい場合は、詳細設定で証明書の検証を無効にすることも可能です。

## ブラウザが起動しないようにするにはどうすればよいですか？

OSによって、複数の方法があります。

- 一部のOSでは、`設定` => `一般`で、ブラウザを起動するためのチェックボックスがあります。
- Sonarrを起動する際に、引数に`-nobrowser`（*nix）または`/nobrowser`（Windows）を追加することができます。
- Sonarrを停止し、config.xmlファイルを編集し、`<LaunchBrowser>True</LaunchBrowser>`を`<LaunchBrowser>False</LaunchBrowser>`に変更します。

## VPN、Jackett、および\*ARRs

- 中国、オーストラリア、南アフリカなどの抑圧的な国を除いて、通常、トレントクライアントのみがVPNの背後にある必要があります。VPNエンドポイントは多くのユーザーによって共有されているため、さまざまなサービスからのレート制限、DDOS保護、IP禁止を経験することがあります。
- 言い換えれば、\*Arrs（Lidarr、Prowlarr、Radarr、Readarr、Lidarr）をVPNの背後に配置すると、サービスにアクセスできないため、アプリケーションが使用できなくなる場合があります。

> **VPNが\*Arrsと問題を引き起こすかどうかではなく、いつ問題が発生するかの問題です：画像プロバイダーはブロックされ、クラウドフレアは\*Arrサーバー（更新、メタデータなど）の前にあり、ブロックされる可能性があります**
{.is-warning}

- **多くのプライベートトラッカーは、VPNを使用したりアクセスしたりすると（JackettやProwlarrを使用するなど）、ユーザーを禁止します。**

### VPNの使用

- VPNが必要であり、Dockerを使用している場合は、HotioまたはBinhexのDownload Client + VPNコンテナを使用することをお勧めします。
- VPNが必要であり、Dockerを使用していない場合は、VPNクライアントがスプリットトンネリングをサポートしている必要があります。必要な（ダウンロードクライアント）アプリのみがVPNの背後にあるようにします。
- トラッカーへのアクセスに関する多くの問題は、ISPのDNSサーバーの代わりにGoogleやCloudflareのDNSサーバーを使用することで解決できます。
- 一部の場合（英国のISPなど）、次のようにトレントダウンロードクライアントをVPNの背後に配置し、Jackett/Prowlarrを使用します：
  - JackettをVPNの背後に配置し、スプリットトンネリングがローカルアクセスを許可するようにします。
  - Prowlarrの場合、VPNクライアントを構成してプロキシを提供し、設定=>インデクサーでプロキシを追加します。プロキシにタグを付け、それを使用する必要があるインデクサーに同じタグを付けます。
    - 必要な場合、およびVPNがプロキシを作成する方法を提供しない場合は、ProwlarrをVPNの背後に配置し、スプリットトンネリングがローカルアクセスを許可するようにします。

## 私は持っていない/必要のない番組のログメッセージを見ます

- これらのメッセージは完全に正常であり、Sonarrがエピソードを望んでいるかどうかを確認するためにチェックするRSSフィードから来ます。通常、これらはデバッグ/トレースログでのみ表示されますが、アイテムの処理に問題が発生した場合には警告またはエラーが表示される場合もあります。これらの警告/エラーは無視しても安全です。なぜなら、それらは望んでいない番組のためのものだからです。望んでいる番組の場合は、フォーラムでサポートスレッドを開いてください。

## シーディング中のトレントが自動的に削除されません

- まだシーディング中のトレントがインポートされると、トレントクライアントがシーディングを続けるためにコピーまたはハードリンク（有効で*可能な場合）されます。理想的なセットアップでは、トレントのダウンロードフォルダとライブラリフォルダが同じファイルシステム上にあり、それらが*同じように見える*（Dockerやネットワーク共有はこれを間違えやすくします）、これによりハードリンクが可能になり、無駄なスペースが最小限に抑えられます。
- さらに、Sonarrまたはダウンロードクライアントでシード時間/比率の目標を設定し、ダウンロードクライアントを設定して、それらが満たされたときに*一時停止*または*停止*するようにし、完了および失敗したダウンロードハンドラーの下で削除を有効にします。これにより、シーディングが完了したトレントはSonarrによってダウンロードクライアントから削除されます。

## ヘルプ、私のMacはSonarrが開発元を検証できないため開けませんと表示されます

- これは簡単です。詳細については、[こちらのリンク](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)を参照してください。
[![Developer Cannot be verified](/assets/general/faq_1_mac.png)]

## ヘルプ、私のMacはSonarr.appが破損していて開けません

- それは破損したダウンロードのためか、[セキュリティの問題です。関連するFAQエントリを参照してください。](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## エラーが表示されます：データベースディスクイメージが壊れています

> sqlite3を3.41にアップグレードした後、このエラーが発生する場合があります。Sonarr v3.0.9は、sqlite3 3.41をサポートしていないため、デフォルトの破壊的な変更が原因です。[問題の詳細については、Sonarr GHI #5464を参照してください](https://github.com/Sonarr/Sonarr/issues/5464)
> これはSonarr v3.0.10で解決され、ユーザーは適切にSonarrをアップグレードする必要があります。
{.is-warning}

- **`Error creating log database`のエラーは、logs.dbに関する問題を示しています**
  - これは、データベースの名前を変更するか削除することで簡単に解決できます。ログデータベースには、コマンドの履歴や更新のインストール履歴、およびInfo、Warn、Errorのエントリが含まれています。
- **`Error creating main database`または一般的な`database disk image is malformed`のエラー（特定のデータベースが指定されていない場合）は、sonarr.dbに関する問題を示しています**
  - 以下の手順を続けてください
- これは、Sonarrのほとんどの情報を格納するSQLiteデータベースが破損していることを意味します。バックアップを試したり、既存のデータベースを回復しようとしたり、バックアップを回復しようとしたり、すべてが失敗した場合は、新しいデータベースを作り直すことができます。
- このエラーは、データベースファイルが\*Arrが実行されているユーザー/グループによって書き込み可能でない場合に表示される場合があります。許可が原因である可能性は、新規インストール、新しいサーバーへの移行、最近appdataディレクトリの許可を変更した場合、または\*Arrが実行されるユーザーとグループを変更した場合にのみ問題になる可能性があります。
- 最良かつ最初のオプションは、[バックアップからの復元を試すことです](#how-do-i-backuprestore-my-sonarr)
- データベースの回復も試すことができます。通常、この問題がアップデート後に発生した場合は、このオプションしかありません。[sqlite3の`.recover`コマンド](/useful-tools#recovering-a-corrupt-db)を試してみてください。
  - もしsqliteに`.recover`がない場合、またはよりGUI（Windowsなど）対応の方法を希望する場合は、[このウィキの手順に従ってください。](/useful-tools#recovering-a-corrupt-db-ui)
- データベースに関するエラーの別の可能性は、データベースをネットワークドライブ（nfsまたはsmbまたはその他のローカルではないもの）に配置していることです。**SQLiteは、データとアプリケーションが同じマシン上に共存する状況を想定して設計されています。**そのため、\*Arr AppDataフォルダ（Dockerの/configマウント）はローカルストレージ上に配置する必要があります。[SQLiteとネットワークドライブはうまく動作せず、最終的にデータベースが破損する可能性があります](https://www.sqlite.org/draft/useovernet.html)。
- mergerFSを使用している場合は、SQLiteがmmapを使用しているため、`direct_io`にサポートされていないため、`direct_io`を削除する必要があります。詳細については、mergerFSの[ドキュメント](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)を参照してください。

## MacでSonarrを使用していて突然動作しなくなりました。何が起こったのでしょうか？

- おそらくこれは、MacOSのバグにより、Sonarrのデータベースの1つが破損したためです。
- [以下の手順に従って解決してください](#i-am-getting-an-error-database-disk-image-is-malformed)
- その後、Sonarrを起動して動作するかどうか確認してください。動作しない場合は、さらなるサポートが必要です。[reddit](http://reddit.com/r/Sonarr)に投稿するか、[discord](https://discord.sonarr.tv/)でヘルプを求めてください。

## Sonarrがリモートサーバー上のファイルを見つけられないのはなぜですか？

- すべてのOSで、\*Arrが実行されるユーザー/グループがマウントされたドライブに読み書きアクセス権限を持っていることを確認してください。
- Linuxの場合は、次のことを確認してください：
  - NFSマウントを使用している場合は、マウントに`nolock`が有効になっていることを確認してください。
  - SMBマウントを使用している場合は、マウントに`nobrl`が有効になっていることを確認してください。
- Windowsの場合：要するに、\*Arrが実行されているユーザー（サービスの場合）またはその下で（トレイアプリの場合）ファイルパスにアクセスできないことです。これにはさまざまな理由がありますが、最も一般的なのは、\*Arrがサービスとして実行されていることです。これにより、以下で説明する問題が発生します。

### Sonarrは、保護されたリモートファイル共有にアクセスできないようです

- Sonarrのサービスを、その共有にアクセスできる別のユーザーアカウントとして実行します
- Windowsサーバーで、管理ツール \> サービスウィンドウを開きます。
- Sonarrサービスを停止します。
- プロパティ \> ログオンダイアログを開きます。
- サービスユーザーアカウントをターゲットユーザーアカウントに変更します。
- スタートアップフォルダーを使用してSonarr.exeを実行します

### マップされたネットワークドライブを使用しています（UNCパスではありません）

- パスをUNCパス（`\\server\share`）に変更します
- スタートアップフォルダーを使用してSonarr.exeを実行します

## マップされたネットワークドライブとUNCパス

- マップされたネットワークドライブを使用することは一般的にうまく機能しません、特にSonarrがサービスとして設定されている場合です。共有を設定するより良い方法は、UNCパスを使用することです。つまり、`X:\TV`の代わりに`\\Server\TV`を使用します。

- 覚えておくべき重要なポイントは、Sonarrがパス情報をダウンローダーから取得するため、NZBGet、SABNzbd、または他のダウンローダーもUNCパスを使用する必要があるということです。

## SonarrはBig Surでは動作しません

次のコマンドを実行してください。

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## v2からアップグレードした後、カスタムスクリプトが動作しなくなりました

- おそらく、接続\...で引数を渡していたためです。
- これを修正するには：
  1. 引数をパスに変更します
  1. スクリプトのシバンがpwshのパスにマップされていることを確認します（シバンの定義がない場合は追加します）
  1. pwshスクリプトが実行可能であることを確認します

# Sonarrの検索とダウンロードの一般的な問題

## クエリは成功しましたが、結果が返されませんでした

- [このトラブルシューティングエントリを参照してください](/sonarr/troubleshooting#query-successful-no-results-returned)

## Sonarrが期待していたエピソードを取得しなかったのはなぜですか？

まず、Sonarrがエピソードを見つける方法について説明した上記のセクション「[Sonarrはエピソードをどのように見つけるのか](#how-does-sonarr-find-episodes)」を読み、理解していることを確認してください。次に、少なくとも1つのインデクサーが期待していたエピソードを持っていることを確認してください。

1. Sonarrのエピソードリストの横にある「Manual Search」アイコンをクリックします。結果はありますか？ない場合は、Sonarrがインデクサーとの通信に問題があるか、インデクサーがエピソードを持っていないか、エピソードがインデクサーで適切に名前付け/分類されていない可能性があります。
1. ステップ1の結果がある場合、赤い感嘆符アイコンが横に表示されているかどうかを確認してください。アイコンの上にカーソルを合わせると、そのリリースが自動ダウンロードの候補にならない理由が表示されます。すべての結果にアイコンがある場合、自動ダウンロードは行われません。
1. ステップ2で少なくとも1つの有効なマニュアル検索結果がある場合、自動ダウンロードが行われるはずです。行われなかった場合、最も可能性が高いのは、インデクサーからのRSS同期を妨げる一時的な通信の問題です。最良の結果を得るために、複数のインデクサーを設定することをお勧めします。
1. ショーのマニュアル結果がないが、インデクサーのウェブサイトを閲覧すると見つけることができる場合 - これはさまざまな理由によるものです。たとえば、リリースがインデクサーで適切にタグ付けされていないため、自動検索でSonarrに返されない場合があります。この[トラブルシューティングエントリ](/sonarr/troubleshooting#searches-indexers-and-trackers)では、原因を特定するためのいくつかのヒントを提供しています。複数のインデクサーをアクティブにしておくと、同じコンテンツのさまざまなソースを提供することで、この問題を解決するのに役立ちます。

## ダウンロード履歴で一致するシリーズが見つかりましたが、リリースはシリーズIDで一致されました。自動インポートはできません

- [このトラブルシューティングエントリを参照してください](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- TVDbでは、エピソード名が不明な場合、それらはTBAというタイトルになり、TVDb APIには24時間のキャッシュがあります。通常、TVDbのウェブサイトの変更は、TVDbキャッシュ（24時間）、skyhookキャッシュ（数時間）、およびシリーズの更新間隔（12時間ごと）のため、Sonarrに到達するまでに24〜48時間かかります。[エピソードタイトルが必要な設定](/sonarr/settings#importing)は、タイトルがTBAの場合のインポート動作を制御しますが、シリーズの放送から48時間後には、タイトルがまだTBAの場合でもリリースがインポートされます。また、TBAのタイトルのファイルの自動的なリネームは行われません。TBAタイマーは、エピソードの放送日時から計算されます。

## Sonarrは、検索またはインポート時に不明なシリーズと表示されます

- [「なぜSonarrはシリーズXのエピソードファイルをインポートできないのですか？/なぜSonarrはシリーズXのリリースを見つけられないのですか？」](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)を参照してください。

## Jackettの/allエンドポイント

{#jackett-all-endpoint}

- Jackettの`/all`エンドポイントは便利ですが、それ以外は潜在的な問題がありますので、各トラッカーを個別に追加する必要があります。また、JackettとNZBHydra2の代替として[Prowlarr](/prowlarr)をご覧ください。

- **2022年2月5日の更新：v3.0.6.1457以降、\*Arrサポートはjackettの`\all`エンドポイントに対して終了しました。Jackettの/allエンドポイントはサポートされなくなりました（警告が表示されます）**。

- Jackettの`/all`エンドポイントは便利ですが、それ以外は潜在的な問題がありますので、各トラッカーを個別に追加する必要があります。
- [Jackettの開発者自身も、これを避けるべきであり、使用しないでくださいと言っています。](https://github.com/Jackett/Jackett#aggregate-indexers)
- /allエンドポイントの使用には利点はありませんが、以下のような欠点があります：
  - インデクサー固有の設定（カテゴリ、検索モードなど）を制御できなくなります。
  - 検索モード（IMDB、クエリなど）を混在させると、品質の低い結果が発生する可能性があります。
  - インデクサー固有のカテゴリ（100000以上）は使用できません。
  - 遅いインデクサーは全体の結果を遅くします。
  - 合計結果は1000に制限されます。
  - /allのトラッカーのいずれかがエラーを返すと、\*Arrはそれを無効にし、結果が得られなくなります。

### Jackett /Allの解決策

- Jackettで各トラッカーを個別にインデクサーとして追加します
- [Prowlarr](/prowlarr)をチェックしてみてください。これはJackettとNZBHydra2の代替であり、Lidarr/Radarr/Readarr開発チームから提供されています。
- [NZBHydra2](https://github.com/theotherp/nzbhydra2)をチェックしてみてください。これはインデクサーを\*Arrに同期できます。ただし、単一の集約エンドポイントを使用せず、同期に`multi`を使用してください。

## Jackettの手動検索時にSonarrよりも多くの結果が表示される

- Sonarrで設定されたトラッカーのカテゴリを確認してください
- これは、SonarrがJackettを検索する方法が異なるためです。[このトラブルシューティング記事を参照して、詳細を確認してください](/sonarr/troubleshooting#searches-indexers-and-trackers)。

## Cookieの検索

- 一部のサイトは自動的にログインできず、手動でログインしてからクッキーをSonarrに提供する必要があります。[詳細については、この記事を参照してください。](/useful-tools#finding-cookies)

## トレントの解凍

- ほとんどのトレントクライアントには、ユーズネットの対応製品とは異なり、自動的な圧縮アーカイブの処理機能が付属していません。[unpackerr](https://github.com/unpackerr/unpackerr)をおすすめします。

## 権限

- Sonarrは、ダウンローダーがファイルを配置する場所からそれらを最終的な場所に移動する必要があるため、Sonarrはソースディレクトリと宛先ディレクトリおよびファイルの読み取り/書き込みが必要です。
- Linuxでは、サービスが独自のユーザーとして実行されるというベストプラクティスがあるため、ダウンローダとSonarrの両方でフォルダのパーミッションを`775`、ファイルのパーミッションを`664`に設定する必要があります。umask表記では、これは`002`になります。

## 強制認証

- Sonarr v4（ベータ版）では、認証が必須です。詳細については、[Sonarr v4 FAQ - Forced Authentication](/sonarr/faq-v4#forced-authentication)を参照してください。