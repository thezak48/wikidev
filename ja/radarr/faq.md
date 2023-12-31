すべての映画ファイルを1つのフォルダに保存できますか？

- はい、Radarrではすべての映画ファイルを1つのフォルダに保存することができます。これを実現するには、次の手順に従ってください：

1. RadarrのWebインターフェースにアクセスします。
2. 「設定」メニューに移動します。
3. 「メディア管理」タブを選択します。
4. 「ファイル管理」セクションで、「ファイルフォルダ」オプションを選択します。
5. 「ファイルフォルダ」フィールドに、すべての映画ファイルを保存するフォルダのパスを入力します。
6. 変更を保存します。

これで、すべての映画ファイルが指定したフォルダに保存されます。ただし、注意点があります。フォルダ内のファイル名は一意である必要があります。同じ名前のファイルが存在する場合、Radarrは正常に動作しない可能性があります。また、フォルダ内のファイルはすべて映画ファイルである必要があります。他のファイルが含まれている場合、Radarrはそれらを無視します。

この機能を使用する前に、注意してください。ファイルの整理やバックアップの観点から、複数のフォルダに映画ファイルを分けて保存することをお勧めします。

- いいえ、理由はRadarrが[Sonarr](/sonarr)のフォークであり、すべての番組にはフォルダがあります。この制限は多くのユーザーにとって既知の問題であり、将来のバージョンで実装されるかもしれません。ただし、これは単純な変更ではなく、バックエンドの完全な書き直しを必要とします。
- [カスタムフォルダのGitHub Issue](https://github.com/Radarr/Radarr/issues/153)はこのリクエストをカバーしていますが、その時点で1つのフォルダにすべての映画ファイルが実装される保証はありません。
- 以下に、ややハック的な解決策が説明されています。ただし、Radarrで再スキャンをトリガーしないでください。再スキャンすると、映画が見つからないと表示され、映画は決してアップグレードされません。
  - カスタムスクリプトを使用する
    - スクリプトはインポート時にトリガーされるようにする必要があります
    - ファイルを移動するように設計する必要があります
    - その後、Radarr APIを呼び出して映画を監視対象外に変更する必要があります。
- すべての映画を個別のフォルダに移動する場合は、[Tips and Tricksセクション => Create a Folder for Each Movie](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)の記事を参照してください。

## ライブラリのすべての映画を1つのフォルダに配置できますか？

- いいえ、上記を参照してください。

## Radarrを更新する方法は？

- 設定に移動し、一般タブに移動し、詳細設定を表示します（保存ボタンの横のトグルを使用します）。

1. 更新セクションでブランチ名を「master」または「develop」に変更します。
1. 保存します。

*これにより、そのブランチのビットがすぐにインストールされるわけではありません。次の更新時にインストールされます。*

- ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) -（デフォルト/安定版）：開発版とナイトリーブランチでユーザーによってテストされ、重大な問題がないことがわかっています。このバージョンはおおよそ月に1回更新されます。GitHubでは、これは「master」ブランチです。

- ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) -（ベータ版）：これはテストのエッジです。ナイトリーでテストされた後にリリースされ、即座の問題がないことが確認されます。新機能とバグ修正は、ナイトリーの後にここで最初にリリースされます。比較的安定していますが、まだ「ベータ」です。このバージョンは、開発に応じて週に1回または2週に1回更新されます。

> **警告：`master`に戻ることができない場合があります。** GitHubでは、これは特定の時点での`develop`ブランチのスナップショットです。
{.is-warning}

- ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) -（アルファ/不安定）：これは最新のものです。コードがコミットされ、すべての自動テストに合格した直後にリリースされます。このビルドはまだ私たちや他のユーザーによって使用されていない場合があります。一部の場合では、実行さえされない可能性があります。このブランチは、上級ユーザーにのみ推奨されます。このブランチでは、問題が発生し、自己調査が予想されます。***更新に失敗した場合に復旧するために、自分で手を汚す覚悟がある場合にのみ、このブランチを使用してください。***このバージョンはすぐに更新されます。

> **警告：`master`に戻ることができない場合があります。** GitHubでは、これは`develop`ブランチです。
{.is-danger}

- 注意：Dockerを使用してインストールしている場合は、コンテナタグの末尾に`:release`、`:latest`、`:testing`、または`:develop`を追加します。

|                                                                    | ![Current Master/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Dockerコンテナ内でRadarrを更新できますか？

- *技術的には可能ですが、絶対に行ってはいけません。* これはDockerの主要な哲学です。最新の`nightly`にアップグレードした場合、Dockerコンテナ自体を更新（古いバージョンにダウングレードする可能性もあります）すると、データベースの問題が発生する可能性があります。

### 新しいバージョンのインストール

#### ネイティブ

1. システムに移動し、アップデートタブに移動します。
1. まだインストールされていない新しいバージョンには、その横にアップデートボタンが表示されます。そのボタンをクリックしてアップデートをインストールします。

#### Docker

1. タグを再プルし、コンテナを更新します。

## `nightly`から`develop`に切り替えることはできますか？

## ブランチ間を切り替えることはできますか？

- バージョンが同じ場合は切り替えることができますが、それ以外の場合は開発チームに確認してください。`nightly`から`master`に切り替えることができるか、`nightly`から`develop`に切り替えることができるか、または`develop`から`master`に切り替えることができるかを確認してください。
- これらの手順に従わないと、Radarrが使用できなくなったりエラーが発生する可能性があります。以下のエラーが発生した場合は、新しいデータベースを古い\*Arrバージョンで使用している可能性があります。サポートされていません。以前のバージョン以上の\*Arrにアップグレードしてください。
  - エラーメッセージの例：
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - その他、欠落している列やテーブルに関する類似のデータベースエラー。

## Radarrをバックアップ/復元する方法は？

### Radarrのバックアップ

#### ビルトインバックアップを使用する

- RadarrのUIでシステムに移動し、バックアップタブに移動します。
- バックアップボタンをクリックします。
- バックアップが作成された後、zipファイルをダウンロードして安全な場所に保存します。

#### ファイルシステムを直接使用する

- RadarrのAppDataディレクトリの場所を見つけます
  - RadarrのUIでシステムに移動し、Aboutに移動します
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Radarrを停止します-これにより、データベースが破損するのを防ぎます
- 内容を安全な場所にコピーします

### バックアップからの復元

> 異なるパスを使用するOSに復元することはできません（WindowsからLinux、LinuxからWindows、WindowsからOS X、またはOS XからWindows）。OS XとLinuxの間の移動は、おそらく動作しますが、サポートされていません。データベース内のすべてのパスを手動で編集するか、[Toolbarr](https://github.com/Notifiarr/toolbarr)を使用してください。
{.is-warning}

#### zipバックアップを使用する

- Radarrを再インストールします（該当する場合/すでにインストールされていない場合）
- Radarrを実行します
- システムに移動します=> バックアップ
- バックアップを復元を選択します
- ファイルの選択を選択します
- バックアップのzipファイルを選択します
- 復元を選択します

#### ファイルシステムのバックアップを使用する

- Radarrを再インストールします（該当する場合/すでにインストールされていない場合）
- RadarrのAppDataディレクトリの場所を見つけます
  - Radarrを一度実行し、UIでシステムに移動し、Aboutに移動します
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Radarrを停止します
- AppDataディレクトリの内容を削除します（.db-wal/.db-journalファイルが存在する場合も削除します）
- バックアップから復元します
- Radarrを起動します
- パスが同じである限り、すべてのものが前回の状態から再開されます

#### Synology NASでのファイルシステムの復元

> 注意：Synologyでの復元には、Linuxの知識とSynologyデバイスへのルートSSHアクセスが必要です。
{.is-warning}

- Radarrを再インストールします（該当する場合/すでにインストールされていない場合）
- RadarrのAppDataディレクトリの場所を見つけます
  - Radarrを一度実行し、UIでシステムに移動し、Aboutに移動します
  - [Radarr Appdata Directory](/radarr/appdata-directory)
- Radarrを停止します
- SSHを介してSynology NASに接続し、rootとしてログインします

> インストールによっては、ユーザーが以下のコマンドと異なる場合があります：`chown -R sc-Radarr:Radarr *` {.is-info}

- 次のコマンドを実行します：

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- ファイルのアクセス権を更新します：

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Radarrを起動します

# Radarrの一般的な問題

## タスクがキャンセルされました

- Radarrは、リクエストが行われたサーバーからの応答を100秒後に受信できませんでした。
- ログには `System.Threading.Tasks.TaskCanceledException: A task was canceled.` というエラーメッセージが含まれています。
- これは次のような原因によって引き起こされることがよくあります：
  - VPNの設定が不正確または使用方法が間違っている
  - プロキシの設定が不正確または使用方法が間違っている
  - ローカルDNSの問題-別のDNSプロバイダに変更してみてください
  - ローカルIPv6の問題- *最も一般的な* - 通常、ホストシステムでIPv6が有効になっていますが、機能していません
  - Privoxyの使用とその不正確な設定
  - PiHoleの[Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit)リクエスト
- DNSのトラブルシューティングには、`nslookup <トレースログからのドメイン.tld>` を使用し、IPv6のトラブルシューティングには、`curl -sv -6 "<トレースログからのURL>"` またはその他の接続性には `curl -sv -4 "<トレースログからのURL>"` を使用します。

## パスは既存の映画にすでに設定されています

![existing-movie.png](/assets/radarr/existing-movie.png)

- ライブラリのインポートが「既存」と表示されるか、「パスは既存の映画に設定されています」というエラーが表示される場合があります。
- これは、既に別の映画に割り当てられているパスを追加しようとしたり、既存の映画のパスを編集しようとしたりした場合に発生します。
- おそらく、ユーザーがライブラリをインポートする際に、一致しない映画を修正しなかったことが原因です。
- 既にその映画のパスに割り当てられている映画を見つけて修正します。
  - 映画インデックス
  - テーブルビュー
  - オプション => 列としてパスを追加
  - ソートして、問題のあるパスにある映画を見つけます。
- または、既存のパスを使用して映画をRadarrから削除します。

## 映画フォルダの名前を変更する方法はありますか？

{#rename-folders}

> 同じ手順が映画のパスの移動/変更にも適用されます。Radarrでパスを更新するだけで、ファイルを移動する必要がない場合は、ステップ5で「Yes Move files」を選択しないでください。
{.is-info}

1. 映画
1. 映画エディタ
1. フォルダ名を変更する必要のある映画を選択します
1. ルートフォルダを現在の映画が存在する同じルートフォルダに変更します
1. 「Yes move files」を選択します

> Plexを使用している場合、これによりイントロ、サムネイル、チャプター、およびプレビューメタデータの再検出がトリガーされます。
{.is-warning}

## 映画のファイルとフォルダの命名

- 現在、Radarrでは、各映画が少なくとも`Movie Title (Year)/`を含む形式のフォルダにある必要があります。オプションで、`_`または`.`は有効な区切り文字です。インポート中に正しい品質と解像度の識別を容易にするために、`Movie Title (Year) [Quality-Resolution].ext`のようなファイル名が最適です。再度、`_`または`.`は有効な区切り文字です。

  - この変更をコレクションに適用するための便利なツールは、[filebot](http://www.filebot.net/#download)です。Apple StoreとWindows Storeの両方に有料バージョンがありますが、無料で[SourceForge](https://sourceforge.net/projects/filebot/files/latest/download)で入手できます。GUIとCLIの両方がありますので、お好きなものを使用できます。上記の例では、`{ny}`は`Name (Year)`に展開され、`{vf}`は`1080p`のような解像度を提供します。品質を推測する必要はないため、`{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`を使用して、720p未満のものを`[DVD-572p]`と名付け、720p以上のものを`[Bluray-1080p]`のように名付けることができます。

- 詳細については、[Tips and Tricksセクション => Create a Folder for Each Movie](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie)を参照してください。

## 映画のフォルダ名が間違っています

- 映画のフォルダ名は、映画が追加された時点のメタデータ（名前/年）に基づいています。リリース前に映画を追加した場合、新しい現在のデータを反映するために、上記のフォルダ名の変更トリックを使用する必要がある場合があります。
- 映画がすでにフォルダに入っている場合でも、フォルダ名が正しくない場合があります。フォルダ名は`Movie Title (Year)`である必要があります。タイトルと年をフォルダ名に含めることは現在重要です。

  - うまく機能する例：
    - `/mnt/Movies/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Kid Movies/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - 動作するが、手動で管理する必要がある例：
    - 文字で：`/mnt/Movies/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - 評価で：`/mnt/Movies/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - ジャンルで：`/mnt/Movies/Crime, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - これらの例では、映画が追加されるときに手動で管理する必要があります。各例には、最初の文字の例では`A-D`と`E-G`のような多くのルートディレクトリがあり、評価の例では`R`と`PG-13`のようなものがあり、ジャンルフォルダのバラエティを推測できます。新しい映画を追加するときに、この形式が機能するように正しいベースフォルダを選択する必要があります。
  - 機能しない例：
    - 単一のフォルダ：`/mnt/Kid Movies/Frozen (2013) [Bluray-1080p].mkv`
      - 現時点では、映画は単に映画の名前に基づいたフォルダにある必要があります。この機能を追加するための開発作業が完了するまで、これには回避策はありません。
    - v0.2の**映画**フォルダの命名形式には、**ファイル**のプロパティが**映画フォルダ**の名前に含まれる``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}``のようなものは、v3では機能しません。
      - フォルダは映画に関連しており、ファイルとは独立しています。さらに、これは計画されている1つの映画に対する複数のファイルのサポートとの互換性がなくなるため、壊れやすくなります。
      - これを削除したもう1つの理由は、頻繁な混乱、データベースの破損、および一般的には半分しかできていなかったためです。
  - [Tips and Tricksセクション => Create a Folder for Each Movie](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)は、ファイルとフォルダの構造が正常に機能することを確認するための素晴らしい情報源です。

## リフレッシュ映画タスクを無効にできますか？

- いいえ、また、SQLのハッカリーを通じて行ってはいけません。リフレッシュ映画タスクは、各映画のメタデータ（ID、キャスト、概要、評価、翻訳、代替タイトルなど）がRadarrに現在保存されている情報と比較して更新されたかどうかを、上流のServarrプロキシにクエリーします。必要な場合、該当する映画を更新します。
- リフレッシュタスクがI/O使用量が多くなるという一般的な苦情があります。
- メインの設定は「リフレッシュ後に映画フォルダを再スキャンする」です。リフレッシュ中にディスクI/O使用量が急増する場合は、リスキャン設定を`Manual`に変更することをお勧めします。
  - すべてのライブラリの変更（新しい映画、アップグレード、削除など）がRadarrを介して行われる場合を除き、これを`Never`に変更しないでください。
  - 映画ファイルを手動で削除するか、Plexや他のサードパーティのプログラムを介して削除する場合は、これを`Never`に設定しないでください。
- 変更できるもう1つの設定は、「ビデオファイルの分析」です。これは、tdarrを使用するか、他の方法でファイルを外部で変更する場合に有効にすることをお勧めします。使用しない場合は、「ビデオファイルの分析」を無効にして、一部のI/Oを削減できます。

## Radarrの機能をリクエストするにはどうすればよいですか？

- これは簡単です。[ここをクリックしてください](https://github.com/Radarr/Radarr/issues)

## ヘルプ、MacでRadarrが開けません。開発元が確認できないためです

- これは簡単です。詳細については、[こちらのリンク](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)を参照してください。 ![Developer Cannot be verified](developer-cannot-be-verified.png "Developer Cannot be verified")
- または、Radarrを自己署名する必要がある場合は、`codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`を実行する必要があります。

## ヘルプ、MacでRadarr.appが破損して開けません

- それは破損したダウンロードのためか、[セキュリティの問題](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)のためです。再試行してみてください。

## エラーが発生しました：データベースディスクイメージが壊れています

> \* v4.Xバージョンにアップグレードした後にこの問題が発生しているRadarrユーザー向け。v4バージョンでは、データベースの以前の破損がどこかにあった場合（以前のRadarrの実行時に検出できなかった可能性があります）、マイグレーションは失敗します。これにより、Radarrの起動に失敗します。バックアップもすべて破損している可能性が高いため、それらを復元しても問題は解決しない可能性があります。
> \* マイグレーション後のデータベースが開かないか、回復できない場合は、最新のバックアップからデータベースのコピーを作成し、そのファイルにデータベース回復プロセスを適用してから、回復したバックアップファイルを使用してRadarrを起動してみてください。それにより、問題なくマイグレーションが行われるはずです。
{.is-warning}

- **「ログデータベースの作成エラー」というエラーは、logs.dbに問題があることを示しています**
  - これは、データベースを名前変更または削除することで簡単に解決できます。ログデータベースには、コマンドの履歴や更新インストールの履歴、およびInfo、Warn、Errorのエントリが含まれています。
- **「メインデータベースの作成エラー」または一般的な「データベースディスクイメージが壊れています」と特定のデータベースが指定されていないエラーは、radarr.dbに問題があることを示しています**
  - 以下の手順を続けてください
- これは、Radarrのほとんどの情報を保存するSQLiteデータベースが破損していることを意味します。バックアップを試す、既存のデータベースを回復する、バックアップを回復する、またはすべてが失敗した場合は、新しいデータベースで最初からやり直すことができます。
- このエラーは、データベースファイルが\*Arrが実行されているユーザー/グループによって書き込み可能でない場合に表示される場合があります。許可が原因である可能性は、新しいインストール、新しいサーバーへの移行、最近のappdataディレクトリのアクセス許可の変更、または\*Arrの実行ユーザーとグループの変更の場合にのみ問題になる可能性があります。
- 最善かつ最初のオプションは、[バックアップからの復元を試す](#how-do-i-backuprestore-my-radarr)ことです。ただし、v4にアップグレードした後にこれを受け取ったユーザーにとっては、バックアップ自体が機能しない可能性が非常に高いため、他の回復方法を試す必要があります。
- データベースを回復することもできます。通常、この問題がアップデート後に発生した場合の唯一のオプションです。[sqlite3の`.recover`コマンド](/useful-tools#recovering-a-corrupt-db)を試してみてください。
  - sqliteに`.recover`がない場合、またはよりGUI（Windows）フレンドリーな方法を希望する場合は、[このウィキの手順に従ってください。](/useful-tools#recovering-a-corrupt-db-ui)
- データベースのエラーの別の可能な原因は、データベースをネットワークドライブ（nfsまたはsmbまたは他のローカルでないもの）に配置していることです。**SQLiteは、データとアプリケーションが同じマシン上に共存する状況を想定しています。**したがって、\*Arr AppDataフォルダ（Dockerの/configマウント）はローカルストレージ上にある必要があります。[SQLiteとネットワークドライブはうまく動作せず、データベースが壊れる可能性があります](https://www.sqlite.org/draft/useovernet.html)。
- mergerFSを使用している場合は、SQLiteがmmapを使用しているため、`direct_io`ではサポートされていないため、`direct_io`を削除する必要があります。詳細については、mergerFSの[ドキュメント](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)を参照してください。

## MacでRadarrを使用していて、突然動作しなくなりました。何が起こったのですか？

- おそらくこれは、MacOSのバグによって、データベースの1つが破損したためです。
- 上記のデータベースが壊れているエントリを参照してください。
- 次に起動して動作するかどうかを確認してください。動作しない場合は、さらなるサポートが必要です。[サブレディット/r/radarr](http://reddit.com/r/radarr)に投稿するか、[discord](https://radarr.video/discord)に参加してヘルプを求めてください。

## リモートサーバー上のファイルがRadarrで表示されないのはなぜですか？

- すべてのOSで、\*Arrを実行しているユーザー/グループがマウントされたドライブに読み取りおよび書き込みアクセス権を持っていることを確認してください。
- Linuxの場合は、次のことを確認してください：
  - NFSマウントを使用している場合は、マウントに`nolock`が有効になっていることを確認してください。
  - SMBマウントを使用している場合は、マウントに`nobrl`が有効になっていることを確認してください。
- Windowsの場合：簡単に言えば、\*Arrがリモートサーバー上のファイルパスにアクセスできないことです。これにはさまざまな理由がありますが、最も一般的なのは、\*Arrがサービスとして実行されているためです。これにより、以下で説明する問題が発生します。

### デフォルトでは、Radarrは保護されたリモートファイル共有にアクセスできないLocalServiceアカウントで実行されています

- Radarrのサービスを、その共有にアクセスできる別のユーザーアカウントとして実行します
- Windowsサーバーの「管理ツール」\>「サービス」ウィンドウを開きます。
- Radarrサービスを停止します。
- 「プロパティ」\>「ログオン」ダイアログを開きます。
- サービスユーザーアカウントをターゲットユーザーアカウントに変更します。
- スタートアップフォルダにあるRadarr.exeを実行します

### マップされたネットワークドライブを使用している場合（UNCパスではない場合）

- パスをUNCパス（`\\server\share`）に変更します
- スタートアップフォルダにあるRadarr.exeを実行します

## Windowsサービスからトレイアプリに変更する方法は？

1. Radarrをシャットダウンします
1. Radarrディレクトリにあるserviceuninstall.exeを実行します
1. 管理者として`Radarr.exe`を1回実行して、適切なアクセス許可を与え、ファイアウォールを開きます。完了したら、それを閉じて通常通り実行できます。
1. （オプション）ショートカットをスタートアップフォルダにドロップして、起動時に自動的に起動します。

## ヘルプ、自分自身をロックアウトしてしまいました

{#help-i-have-forgotten-my-password}

認証を無効にする（忘れたユーザー名またはパスワードをリセットする）には、`config.xml`を編集する必要があります。これは[Radarr Appdataディレクトリ](/radarr/appdata-directory)の中にあります。

1. テキストエディタでconfig.xmlを開きます
1. 認証方法の行を見つけます。`<AuthenticationMethod>Basic</AuthenticationMethod>`または`<AuthenticationMethod>Forms</AuthenticationMethod>`になります
1. `AuthenticationMethod`行を`<AuthenticationMethod>None</AuthenticationMethod>`に変更します
1. Radarrを再起動します
1. Radarrは今やパスワードなしでアクセスできるようになります。UIの「設定：一般」に移動し、ユーザー名とパスワードを設定してください

## 起動時にブラウザが起動するのを止めるにはどうすればよいですか？

OSによって、複数の方法があります。

- 一部のOSでは、「設定」=>「一般」にチェックボックスがあり、起動時にブラウザを起動するかどうかを設定できます。
- Radarrを起動する際に、引数に`-nobrowser`（*nix）または`/nobrowser`（Windows）を追加することができます。
- Radarrを停止して、config.xmlファイルを編集し、`<LaunchBrowser>True</LaunchBrowser>`を`<LaunchBrowser>False</LaunchBrowser>`に変更します。

## 奇妙なUIの問題

- ライブラリページが何も表示されない、特定のビューやソートが機能しないなど、奇妙なUIの問題が発生した場合は、ChromeのシークレットウィンドウまたはFirefoxのプライベートウィンドウで表示してみてください。そこで正常に動作する場合は、特定のIP/ドメインのブラウザのキャッシュとクッキーをクリアしてください。詳細については、[Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage)のウィキ記事を参照してください。

## WebインターフェースがWindows上のlocalhostのみで読み込まれます

- Webインターフェースに<http://localhost:7878/>または<http://127.0.0.1:7878/>でのみアクセスできる場合、少なくとも1回は管理者として実行する必要があります。

## アクセス許可

- Radarrは、ダウンローダーがファイルを配置する場所からファイルを最終的な場所に移動する必要があるため、ソースと宛先のディレクトリとファイルの読み取り/書き込みが必要です。
- Linuxでは、サービスが独自のユーザーとして実行されるというベストプラクティスがあるため、共有グループを使用し、ダウンローダとフォルダのアクセス許可を`775`に設定し、ファイルを`664`に設定する必要があります。umask表記では、これは`002`になります。

## システムとログが無限に読み込まれます

- これはEasy-Privacyブロックリストのせいです。彼らは基本的に`/api/log?`を含むすべてのURLをブロックします。リストを確認して、そのリスト内のすべてのURLをブロックすることが合理的かどうかを判断してください。そのリストには、サイトを壊す可能性のある数十のURLが含まれています。これを選択したのはあなたの広告ブロッカーです。簡単な解決策は、Radarrが実行されているドメインをホワイトリストに登録することです。ただし、リストを確認することをお勧めします。

## トレントの解凍

- ほとんどのトレントクライアントには、ユーズネットの対応クライアントとは異なり、自動的な圧縮アーカイブの処理機能がありません。[unpackerr](https://github.com/unpackerr/unpackerr)をお勧めします。

## uTorrentが動作しなくなりました

- Web UIが有効になっていることを確認してください
- Alt Listening Port（詳細設定=> Web UI）がListening Port（接続）と同じでないことを確認してください
- 接続のポートフォワーディングに影響を与えないように、Web UI Alt Listening Portを変更することをお勧めします。

## ポップアップが表示され、config.xmlが破損していると表示されました。どうすればよいですか？

- Radarrは、スタートアップ時に設定ファイルを読み取ることができなかったため、いかなるオンライン状態に戻るためには、[appdata-directory](/radarr/appdata-directory)の中の`.xml`を削除する必要があります。削除したら、デフォルトのポート（7878）で起動します。その後、設定ページで設定した設定を再構成してください。

## 無効な証明書およびその他のHTTPSまたはSSLの問題



- ダウンロードクライアントが動作しなくなり、「Localhost is an invalid certificate」というエラーが表示されていますか？
  - RadarrはSSL証明書を検証します。ダウンロードクライアントにSSL証明書が設定されていない場合、または自己署名のhttps証明書を使用していても、ローカル証明書ストアにCA証明書が追加されていない場合、接続を拒否します。無料で適切に署名された証明書は[let's encrypt](https://letsencrypt.org/)から入手できます。
  - ダウンロードクライアントと同じマシン上にある場合、HTTPSを使用する必要はありませんので、接続のSSLを無効にするのが最も簡単な解決策です。多くの人は、ローカルネットワークでも必要ではないと考えるでしょう。セキュリティの低いSSL設定を維持したい場合は、詳細設定で証明書の検証を無効にすることも可能です。

## VPN、Jackett、および \*ARRs

- 中国、オーストラリア、南アフリカなどの抑圧的な国にいない限り、トレントクライアントは通常、VPNの背後にある必要がある唯一のものです。VPNのエンドポイントは多くのユーザーと共有されているため、さまざまなサービスからのレート制限、DDOS保護、およびIPブロックが発生する可能性があります。
- 言い換えれば、\*Arrs（Lidarr、Prowlarr、Radarr、Readarr、Lidarr）をVPNの背後に配置すると、サービスにアクセスできないため、アプリケーションが使用できなくなる場合があります。

> **VPNが\*Arrsに問題を引き起こすかどうかではなく、いつ問題が発生するかです: 画像プロバイダーはあなたをブロックし、cloudflareは\*Arrサーバー（更新、メタデータなど）の前面にあり、あなたをブロックする可能性があります**
{.is-warning}

- **多くのプライベートトラッカーは、VPNを使用してアクセスすること（JackettやProwlarrを使用すること）を禁止します。**

### VPNの使用

- Dockerを使用している場合、VPNが必要な場合は、HotioまたはBinhexのDownload Client + VPNコンテナを使用することをお勧めします。
- Dockerを使用していない場合、VPNクライアントはスプリットトンネリングをサポートしている必要があります。必要な（ダウンロードクライアント）アプリのみがVPNの背後にあるようにします。
- トラッカーへのアクセスに関する多くの問題は、ISPのDNSサーバーの代わりにGoogleやCloudflareのDNSサーバーを使用することで解決できます。
- 一部の場合（英国のISPなど）、次のようにトレントダウンロードクライアントをVPNの背後に配置する必要があります：
  - JackettをVPNの背後に配置し、スプリットトンネリングがローカルアクセスを許可するようにします。
  - Prowlarrの場合、VPNクライアントを構成してプロキシを提供し、設定=>インデクサーにプロキシを追加します。プロキシにタグを付け、それを使用する必要があるインデクサーにも同じタグを付けます。
    - 必要な場合、およびVPNがプロキシを作成する方法を提供していない場合は、ProwlarrをVPNの背後に配置し、スプリットトンネリングがローカルアクセスを許可するようにします。

# Radarrの検索とダウンロードの一般的な問題

## なぜ新しい映画をRadarrに追加できないのですか？

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarrは映画情報やファンアート、バナー、背景などの画像について、[The Movie Database (TMDb)](http://themoviedb.org)を使用しています。一般的に、映画を追加できない理由はいくつかあります：
  - TMDbは、映画の検索に特殊文字の使用を好まない（Radarrが使用するAPIを介した検索）ため、翻訳された名前で検索したり、特殊文字を使用せずに検索したりしてみてください。
  - TMDbのIDまたは、TMDbに存在する場合はIMDbのIDで追加することもできます。
  - 映画がまだTMDbに追加されていない場合は、[ガイド](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006)に従って追加してください。

## Jackettの結果が手動検索よりも多いのはなぜですか？

- これは通常、Jackettの検索方法が異なるためです。詳細については、[トラブルシューティング記事](/radarr/troubleshooting)を参照してください。

## Radarrは映画の年をどのように決定するのですか？

- Radarrは[TMDb](https://www.themoviedb.org/)からメタデータを取得します。
- Radarrは、最も古い**劇場公開**日と最も古い**プレミア**日の年を使用して一致を行います。
  - 劇場公開が存在しない場合、ロジックは最も古い物理的またはデジタルリリース日にフォールバックします。
- 映画にデジタル、物理、劇場、またはプレミアリリース日がない場合は、TMDbを更新する必要があります。
- [TMDbの貢献ガイド](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013)では、次のようにリリースタイプについて説明しています。
  - **プレミア** - プレミア上映は、映画祭上映（例：TIFF）またはキャストとクルーが参加する大都市（例：LA、ロンドン、トロント）でのプレミアイベントの形を取ることがあります。
  - **劇場** - オリジナルリリースおよびその後の公式リリースに使用できます。広範なリリースまたは飽和リリースに使用されます。アメリカ合衆国では、600〜1,999スクリーンが広範なリリースと見なされ、2000以上が飽和リリースと見なされます。
  - **劇場（限定）** - 限定劇場公開は、通常、主要な大都市市場でいくつかの劇場で新しい映画を公開する映画配給戦略です。アメリカ合衆国では、劇場の数は600未満です。
  - **物理** - すべてのVHS、DVD、Blu-rayリリースを含みます。
  - **デジタル** - ストリーミングプラットフォーム、VODレンタルまたは購入を含む、すべての関連するリリースを追加できます。オンライン映画祭やバーチャルシネマリリースなどのデジタル上映もデジタルリリースとしてカウントされます。

## Radarrは外国映画や外国語のタイトルをどのように扱うのですか？

> [TRaSH's Custom Format Language Guide](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats)は、希望の言語で映画を取得するのに役立つかもしれません。{.is-info}

> 2023年2月12日以降、Radarrのメタデータキャッシュは、TMDbのスポークン言語が映画の元の言語である場合にのみ、TMDbのスポークン言語を映画の元の言語とみなすようになります。それ以外の場合は、映画の元のTMDb言語が使用されます。
{.is-warning}

## ID検索

- **IDベースの検索をサポートするインデクサー** - TMDbId、IMDbIdなどのIDベースの検索をサポートするインデクサーやトラッカーでの検索 - たとえば、多くのUsenetインデクサーや多くのプライベートトレントトラッカー - テキストクエリはIDベースの検索で結果が返された場合は使用されません。結果が返された場合、名前/テキスト検索にフォールバックしません。インデクサーから結果が返されない場合は、インデクサーに関連付けられたリリースが間違った映画IDに関連付けられているためです。
  - リリースの言語も、提供された場合には名前から解析されるのではなく、インデクサーやトラッカーのリリースの言語から派生する場合があります。

## テキスト検索

- **IDベースの検索または結果のないIDベースの検索をサポートしないインデクサー** - オリジナルタイトル、英語タイトル、および[映画の品質プロファイルと品質プロファイル内のスコアがゼロより大きいカスタムフォーマットで設定された任意の言語](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/)を使用して検索します。
- パース（インポート）は、すべての翻訳と代替タイトルで一致を探します。
  - リリースの言語も、提供された場合には名前から解析されるのではなく、インデクサーやトラッカーのリリースの言語から派生する場合があります。

## 外国映画の取得方法

- 外国語の映画を取得するには、映画の品質プロファイルの言語をオリジナル（映画の元の言語\*）、そのプロファイルの特定の言語、または`Any`に設定し、スコアが0より大きい[言語条件付きのカスタムフォーマットを作成して、どの言語を取得するかを決定します - 詳細については、リンク先のTRaSH's Guideを参照してください](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/)。
- これには、インデクサーの設定で`multi`として構成されたインデクサーの言語は含まれません。
  - [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c)以降、`multi`はもはや英語を含まないとは限らないということに注意してください。
  - ユーザーは、`multi`が示す言語を定義するために、インデクサーごとに設定を調整できます。

## Radarrは名前に「multi」をどのように扱うのですか？

- Radarr v4.1以降、Radarrは
`multi`は以前のバージョンとは異なり、映画の言語のみを表すものとして扱います。
  - ユーザーは、`multi`が示す言語を定義するために、インデクサーごとに設定を調整できます。
- `multi`の定義は、リリースのパースにのみ役立ち、外国語のタイトルや映画の検索には役立ちません。

## ヘルプ、映画は追加されましたが検索されません

- Radarrは、欠落している映画を自動的に*積極的に*検索しません。代わりに、新しい投稿の定期的なクエリが、RSSに設定されたすべてのインデクサーに対して行われます。そのリストに欲しい映画やカットオフが満たされていない映画が表示されると、ダウンロードされます。つまり、映画が投稿されるまで（または再投稿されるまで）、ダウンロードされません。
- 今すぐに欲しい映画を追加する場合は、*追加映画*（**1**）ボタンの左側にある「欠落している映画の検索を開始する」ボックスをチェックするのが最適なオプションです。または、追加した映画のページに移動し、虫眼鏡の「検索」（**2**）ボタンをクリックするか、欠落している映画やカットオフが満たされていない映画を検索するためにWantedビューを使用できます。

  - 映画を追加するときに映画を追加して検索する
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - 既存の映画を検索する
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jackettの/allエンドポイント

{#jackett-all-endpoint}

- Jackettの`/all`エンドポイントは便利ですが、それ以外の利点はありません。その他のすべては潜在的な問題ですので、各トラッカーを個別に追加する必要があります。または、JackettとNZBHydra2の代替として[Prowlarr](/prowlarr)をご覧ください。

- **2022年1月1日の更新：Jackettの`/all`エンドポイントは、4.0.0.5730以降サポートされなくなります（警告が表示されます）ので、使用しないでください。**
- Jackettの`/all`エンドポイントは便利ですが、それ以外の利点はありません。その他のすべては潜在的な問題ですので、各トラッカーを個別に追加する必要があります。
- [Jackettの開発者自身も、これを避けることを推奨しており、使用しないでください。](https://github.com/Jackett/Jackett#aggregate-indexers)
- `/all`エンドポイントの使用には利点はなく、デメリットのみがあります：
  - インデクサー固有の設定（カテゴリ、検索モードなど）を制御できなくなります。
  - 検索モード（IMDB、クエリなど）を混在させると、低品質の結果が表示される場合があります。
  - インデクサー固有のカテゴリ（100000以上）は使用できません。
  - 遅いインデクサーは全体の結果を遅くします。
  - 合計結果は1000に制限されます。
  - `/all`のトラッカーの1つがエラーを返すと、\*Arrはそれを無効にし、結果が得られなくなります。

### Jackett /Allの解決策

- Jackettで各トラッカーを個別にインデクサーとして追加します。
- [Prowlarr](/prowlarr)をチェックしてみてください。これはLidarr/Radarr/Readarrの開発チームによるもので、インデクサーを\*Arrに同期することができます。
- [NZBHydra2](https://github.com/theotherp/nzbhydra2)をチェックしてみてください。これはインデクサーを\*Arrに同期することができます。ただし、シングルの集約エンドポイントを使用せず、同期を使用する場合は`multi`を使用しないでください。

## なぜ2つのファイルがあるのですか？ | ダウンロードにファイルが残っているのはなぜですか？

これは正常です。ハードリンクをサポートするセットアップでは、二重のスペースは使用されません。以下はトレントプロセスの動作です。

1. Radarrは、ダウンロードリクエストをクライアントに送信し、設定したラベルまたはカテゴリ名と関連付けます。例：movies、tv、series、musicなど。
1. Radarrは、そのカテゴリ名を使用して、ダウンロードクライアントの設定で構成したアクティブなダウンロードを監視します。この監視は、ダウンロードクライアントのAPIを介して行われます。
1. 完了したファイルは、元の場所に残され、ファイルをシードするために使用できるようになります（比率や時間は、ダウンロードクライアント内または特定のダウンロードクライアントの下で調整できます）。ファイルがメディアフォルダにインポートされると、サポートされている場合はハードリンクが作成され、サポートされていない場合はコピーされます。
1. Radarrの設定で「完了したダウンロードの処理 - 完了したものを削除」オプションが有効になっている場合、Radarrは、ダウンロードクライアントがシードが完了し、トレントが停止（一時停止）されていることを報告する場合にのみ、元のファイルとトレントを削除します。最適なダウンロードクライアントの設定方法については、[TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/)を参照してください。

> ハードリンクはデフォルトで有効になっています。[ハードリンクを使用すると、追加のディスクスペースを使用しません。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)完了したダウンロードディレクトリとメディアライブラリのファイルシステムとマウントは同じである必要があります。ハードリンクの作成に失敗した場合や、ハードリンクがサポートされていない場合は、ファイルのコピーにフォールバックします。
{.is-info}

## なぜRadarrはリバースプロキシの背後で動作しないのですか？

- v3以降、Radarrは.NETと新しいWebサーバーに切り替えました。SignalRが動作するためには、UIボタンが動作し、データベースの変更が適用され、その他の項目が必要です。そのため、Radarrの場所ブロックには次の追加が必要です。

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- nginxのドキュメントで提案されているように、`proxy_set_header Connection "Upgrade";`を含めないでください。**これは機能しません**
- [ASP.NET Coreの問題を参照してください](https://github.com/aspnet/AspNetCore/issues/17081)
- CloudflareのようなCDNを使用している場合は、WebSocket接続を許可するためにWebSocketが有効になっていることを確認してください。
- 予期しないリダイレクトが発生する場合は、ホストヘッダーが転送されていることを確認してください。