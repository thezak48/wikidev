# 目次

- [目次](#目次)
  - [強制認証](#強制認証)
  - [統計情報をリセットするにはどうすればいいですか？](#統計情報をリセットするにはどうすればいいですか)
  - [カテゴリが利用できないか、存在しない場合](#カテゴリが利用できないか存在しない場合)
  - [一般的なTorznabまたはNewznabインデクサを追加できますか？](#一般的なtorznabまたはnewznabインデクサを追加できますか)
  - [一般的なTorrent RSSフィードを追加できますか？](#一般的なtorrent-rssフィードを追加できますか)
  - [flaresolverrインデクサを使用できますか？](#flaresolverrインデクサを使用できますか)
  - [ダウンまたは機能しないインデクサを追加するにはどうすればいいですか？](#ダウンまたは機能しないインデクサを追加するにはどうすればいいですか)
  - [ProwlarrがSonarrに同期されません](#prowlarrがsonarrに同期されません)
  - [ProwlarrがXインデクサをアプリに同期しません](#prowlarrがxインデクサをアプリに同期しません)
  - [\*Arrインデクサ設定はアプリのフル同期において比較されますか？](#arrインデクサ設定はアプリのフル同期において比較されますか)
  - [Prowlarrを更新するにはどうすればいいですか？](#prowlarrを更新するにはどうすればいいですか)
    - [Dockerコンテナ内でProwlarrを更新できますか？](#dockerコンテナ内でprowlarrを更新できますか)
    - [新しいバージョンのインストール](#新しいバージョンのインストール)
      - [ネイティブ](#ネイティブ)
      - [Docker](#docker)
  - [`nightly`から`develop`に戻すことはできますか？](#nightlyからdevelopに戻すことはできますか)
  - [ブランチを切り替えることはできますか？](#ブランチを切り替えることはできますか)
  - [助けてください、Macが「開発元を検証できないため、Prowlarrを開けません」と表示されます](#助けてくださいmacが開発元を検証できないためprowlarrを開けませんと表示されます)
  - [助けてください、MacがProwlarr.appが破損していて開けないと表示されます](#助けてくださいmacがprowlarrappが破損していて開けないと表示されます)
  - [Prowlarrの機能をリクエストするにはどうすればいいですか？](#prowlarrの機能をリクエストするにはどうすればいいですか)
  - [エラー：データベースディスクイメージが壊れています](#エラーデータベースディスクイメージが壊れています)
  - [MacでProwlarrを使用していて突然動作が停止しました。何が起こったのでしょうか？](#macでprowlarrを使用していて突然動作が停止しました何が起こったのでしょうか)
  - [Windowsサービスからトレイアプリに切り替えるにはどうすればいいですか？](#windowsサービスからトレイアプリに切り替えるにはどうすればいいですか)
  - [Prowlarrのバックアップ/復元はどうすればいいですか？](#prowlarrのバックアップ復元はどうすればいいですか)
    - [Prowlarrのバックアップ](#prowlarrのバックアップ)
      - [組み込みのバックアップを使用する](#組み込みのバックアップを使用する)
      - [ファイルシステムを直接使用する](#ファイルシステムを直接使用する)
    - [バックアップからの復元](#バックアップからの復元)
      - [zipバックアップを使用する](#zipバックアップを使用する)
      - [ファイルシステムバックアップを使用する](#ファイルシステムバックアップを使用する)
      - [Synology NASでのファイルシステムの復元](#synology-nasでのファイルシステムの復元)
  - [WindowsでWebUIがlocalhostのみで読み込まれる](#windowsでwebuiがlocalhostのみで読み込まれる)
  - [Cookieの検索方法](#cookieの検索方法)
  - [uTorrentが動作しなくなりました](#utorrentが動作しなくなりました)
  - [config.xmlが破損しているというポップアップが表示されました。どうすればいいですか？](#configxmlが破損しているというポップアップが表示されましたどうすればいいですか)
  - [無効な証明書およびその他のHTTPSまたはSSLの問題](#無効な証明書およびその他のhttpsまたはsslの問題)
  - [助けてください、自分自身をロックアウトしてしまいました](#助けてください自分自身をロックアウトしてしまいました)
  - [奇妙なUIの問題](#奇妙なuiの問題)
  - [VPN、Prowlarr、および\*ARR](#vpn-prowlarr-およびarr)
  - [ブラウザの起動を起動時に停止するにはどうすればいいですか？](#ブラウザの起動を起動時に停止するにはどうすればいいですか)
  - [一度にすべてのインデクサを簡単に追加できますか？](#一度にすべてのインデクサを簡単に追加できますか)

## 強制認証

ProwlarrのUIに外部ネットワークからアクセスできるように公開している場合、UIにアクセスするためには認証方法を有効にする必要があります。これは、トラッカーやインデクサによってますます必要とされるようになっています。

Prowlarr v1以降、認証は必須です。

### 認証方法

- `Basic`（ブラウザのポップアップ）- このオプションを選択すると、Prowlarrにアクセスする際に、ユーザー名とパスワードを入力するための小さなポップアップが表示されます。
- `Forms`（ログインページ）- このオプションを選択すると、他のウェブサイトと同様のログイン画面が表示され、Prowlarrにログインできます。
- `External` - 設定ファイルでのみ設定可能
  - Authelia、Authetik、NGINX Basic authなどの**外部認証**を使用している場合、アプリをシャットダウンし、[設定ファイル](/prowlarr/appdata-directory)で`<AuthenticationMethod>External</AuthenticationMethod>`を設定し、アプリを再起動することで、二重認証を回避できます。**ファイル内の複数の`AuthenticationMethod`エントリはサポートされておらず、最上位の値のみが使用されます**

### 認証が必要な場合

- アプリを外部に公開しない場合や、ローカル（LANなど）へのアクセスに認証が必要ない場合は、設定 => 一般セキュリティ => 認証が必要な場合を`Disabled For Local Addresses`に変更してください
  - これに相当する設定ファイルは`<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`です

## 統計情報をリセットするにはどうすればいいですか？

- 統計情報をリセットし、履歴をクリアするには、以下の手順を実行してください。

1. 履歴 => オプション
1. 履歴のクリーンアップを`1`に設定します。これにより、昨日までの履歴と統計情報が保持されます。
1. システム => タスクに移動します
1. 「履歴のクリーンアップ」タスクを実行します
1. 「Housekeeping」タスクを実行します
1. 履歴 => オプションに戻ります
1. 履歴と統計情報の保持期間を設定します

## カテゴリが利用できないか、存在しない場合

- カスタム/非標準のインデクサ固有のカテゴリは、標準のカテゴリにマッピングされるため、標準のカテゴリで検索するとすべてのカスタムカテゴリが組み込まれます。詳細については、特定のインデクサのカテゴリマッピング定義を確認してください。

## 一般的なTorznabまたはNewznabインデクサを追加できますか？

- はい。
- `Indexers` => `Add Indexer` (<kb>+</kb>) => `Generic Torznab`または`Generic Newznab`に移動します。

## 一般的なTorrent RSSフィードを追加できますか？

はい。`TorrentRSS`を使用します。

以下の属性は必須です：

- guid
- title
- infohash
- enclosureまたはlink

以下の属性はオプションですが、推奨されます：

- size
- pubDate

## flaresolverrインデクサを使用できますか？

はい。

1. [設定 => インデクサ](/prowlarr/settings#indexer-proxies)でflaresolverrインスタンスを構成し、プロキシとして追加します。
1. 作成したflaresovlerrプロキシにタグを追加します。
1. [インデクサ](/prowlarr/indexers)に同じタグを追加します。

> タグは一致する必要があり、Flaresolverrを使用するためにはCloudflareが検出される必要があります。タグが使用されない場合、Flaresolverrプロキシは無効になります。
{.is-warning}

> 詳細については、[TRaSHの「Flaresolverrのセットアップ方法」ガイド](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/)を参照してください。
{.is-info}

## ダウンまたは機能しないインデクサを追加するにはどうすればいいですか？

- インデクサを追加するための標準的な手順に従い、以下の変更に注意してください。
- `Enabled`ボックスのチェックを外します（無効にします）
- `Save`を押します
- 再度`Save`を押して強制的に保存をトリガーします
- インデクサを編集します（レンチアイコン）
- `Enabled`ボックスにチェックを入れます（有効にします）
- `Save`を押します
- 再度`Save`を押して強制的に保存をトリガーします

## ProwlarrがSonarrに同期されません

- ProwlarrはSonarr v3以上をサポートしています。
- Sonarr v2（旧称nzbdrone）はProwlarrによってサポートされておらず、一般的にもサポートされておらず、2021年3月以降はエンドオブライフとなっています。

## ProwlarrがXインデクサをアプリに同期しません

- Prowlarrは、アプリの追加と削除またはフル同期が有効になっている場合にのみ同期されます。
- アプリとインデクサが一致するタグまたはタグがない場合にのみ、インデクサがアプリに同期されます。
- インデクサは、サポートする能力/カテゴリに基づいて同期されます。
  - インデクサがTVカテゴリのみをサポートしている場合、Lidarr、Radarr、Readarrには同期されません。
- 特定のインデクサは、設定されたカテゴリ内のリリースを含む結果を返さない空のクエリを使用しても、\*Arrに追加できません。
  - 具体的なエラーは、\*ArrからのHTTP 400で、「クエリは成功しましたが、設定されたカテゴリ内の結果がインデクサから返されませんでした。これはインデクサまたはインデクサのカテゴリ設定の問題かもしれません。」というものです。
  - おそらくそのインデクサはその\*Arrで使用できない可能性があります。これは、ReadarrやLidarrでパブリックトラッカーやUsenetインデクサを使用しようとする場合によくあることです。
  - Prowlarr内の\*Arrアプリケーションの詳細設定で、同期するカテゴリを調整してください。
    - 特定のトラッカー（主に「クラッピー」なパブリックトラッカー）では、「8000 - その他」カテゴリを選択して同期する必要があります。これは、Prowlarr内のトラッカーの詳細によって通常（必ずしも）指定されます。
  - 後でもう一度試してみてください
  - 問題が解決しない場合は、データベースが破損している可能性があります。ログを確認して、「Database disk image is malformed」または「Error creating main database」というエラーのインスタンスがあるかどうかを確認してください。可能な解決策については、[この見出し](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)を参照してください。

## \*Arrインデクサ設定はアプリのフル同期において比較されますか？

- アプリ/Prowlarr：インデクサ名
- アプリ/Prowlarr：RSSの有効化/無効化
- アプリ/Prowlarr：自動検索の有効化/無効化
- アプリ/Prowlarr：インタラクティブ検索の有効化/無効化
- アプリ/Prowlarr：インデクサの優先度
- アプリ/Prowlarr：APIキー
- アプリ/Prowlarr：URL
- アプリ/Prowlarr：ベースURL
- アプリ/Prowlarr：ポート
- アプリ/Prowlarr：カテゴリ
- アプリ/Prowlarr：シード比率とシード時間
- アプリ/Prowlarr：最小シーダー数
- アプリ/Prowlarr：*Prowlarrで設定可能なその他の設定*
- Prowlarr：実装（YMLまたはC＃など）

フル同期が有効になっている場合、上記のいずれかが\*ArrアプリとProwlarrの間で変更されると、インデクサが\*Arrに同期され、更新されます。

## Prowlarrを更新するにはどうすればいいですか？

- 設定に移動し、一般タブを開き、詳細設定を表示します（保存ボタンの横にあるトグルを使用します）。

1. 更新セクションでブランチ名を`master`、`develop`、または`nightly`に変更します
1. 保存

*これにより、そのブランチのビルドがすぐにインストールされるわけではありません。次回の更新時に行われます。*

- `master` - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    （デフォルト/安定版）：開発版とナイトリーブランチでユーザーによってテストされ、重大な問題がないことが確認されています。GitHubでは、これは`master`ブランチです。

- `develop` - ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  （ベータ版）：これはテストエッジです。ナイトリーでテストされ、即座の問題がないことが確認された後にリリースされます。新機能とバグ修正は、ナイトリーの後にここで最初にリリースされます。これは、セミステーブルと見なすことができますが、まだ`ベータ`です。

> GitHubでは、これは特定の時点での`develop`ブランチのスナップショットです。
{.is-warning}

- `nightly` - ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  （アルファ版/不安定版）：これは最新の開発版です。コードがコミットされ、すべての自動テストに合格した後にすぐにリリースされます。このビルドはまだ私たちや他のユーザーによって使用されたことがないかもしれません。場合によっては、実行できない場合もあります。このブランチは、上級ユーザーにのみお勧めです。このブランチでは、問題が発生し、自己調査が予想されます。***このブランチは、何をしているかを理解しており、失敗した更新を回復するために手を汚す覚悟がある場合にのみ使用してください。***このバージョンはすぐに更新されます。

> **警告：`develop`に切り替えた後に`develop`に戻ることができない場合があります。** GitHubでは、これは`develop`ブランチです。
{.is-danger}

- 注意：Dockerを使用してインストールしている場合は、コンテナタグの末尾に`：latest`、`：testing`、`：develop`、または`：nightly`を追加します。



|                                                                      | `master` (安定版) ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (ベータ版) ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (不安定版) ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### Docker コンテナ内で Prowlarr をアップデートできますか？

- *技術的には可能ですが、絶対に行わないでください。* これは Docker の主要な哲学です。最新の `nightly` にアップグレードした後に Docker コンテナ自体をアップデートすると（古いバージョンにダウングレードする可能性もあります）、データベースの問題が発生する可能性があります。

### 新しいバージョンのインストール

#### ネイティブ

1. システムに移動し、[更新] タブを選択します。
1. インストールされていない新しいバージョンには、その横に更新ボタンが表示されます。そのボタンをクリックして更新をインストールします。

#### Docker

1. タグを再プルし、コンテナを更新します。

## `nightly` から `develop` に切り替えることはできますか？

## ブランチ間を切り替えることはできますか？

- バージョンが同じ場合は切り替えることができますが、それ以外の場合は開発チームに確認してください。`nightly` から `develop` に切り替えることができるか、または `develop` から `nightly` に切り替えることができるかを確認してください。
- これらの手順に従わないと、Prowlarr が使用できなくなったりエラーが発生する可能性があります。警告しましたが、自己責任でお願いします。
  - 最も一般的なエラーは、欠落している列やテーブルに関するデータベースエラーです。

## ヘルプ、Mac が「開発元を検証できないため、Prowlarr を開けません」と表示されます

- これは簡単です。詳細については、[こちらのリンク](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)を参照してください。
- または、Prowlarr を自己署名する必要がある場合は、`codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine` を実行してください。

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## ヘルプ、Mac が「Prowlarr.app が破損しているため開けません」と表示されます

これは、破損したダウンロード（再試行してみてください）またはセキュリティの問題によるものです。

## Prowlarr の機能をリクエストする方法はありますか？

Prowlarr の機能をリクエストするには、まず GitHub で類似のリクエストが存在しないか検索し、[ここをクリックして](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=)リクエストを追加してください。

## エラーが発生しています: データベースディスクイメージが壊れています

- **`Error creating log database` のエラーは、logs.db の問題を示しています**
  - これは、データベースの名前を変更するか削除することで簡単に解決できます。ログデータベースには、コマンドの履歴や更新のインストール履歴、および Info、Warn、Error のエントリが含まれています。
- **`Error creating main database` または指定されたデータベースがない一般的な `database disk image is malformed` のエラーは、prowlarr.db の問題を示しています**
  - 以下の手順を続けてください
- これは、Prowlarr のほとんどの情報を保存している SQLite データベースが破損していることを意味します。バックアップを試してみたり、既存のデータベースを回復しようとしたり、バックアップを回復しようとしたり、すべてが失敗した場合は、新しいデータベースで最初からやり直すことができます。
- このエラーは、データベースファイルが \*Arr が実行されているユーザー/グループによって書き込み可能でない場合に表示されることがあります。許可は、新規インストール、新しいサーバーへの移行、最近アプリデータディレクトリの許可を変更した場合、または \*Arr の実行ユーザーとグループを変更した場合にのみ問題になる可能性があります。
- 最初のオプションは、[バックアップからの復元を試すことです](#how-do-i-backuprestore-my-prowlarr)
- データベースを回復することもできます。これは、通常、アップデート後にこの問題が発生した場合の唯一のオプションです。[sqlite3 の `.recover` コマンド](/useful-tools#recovering-a-corrupt-db)を試してみてください。
  - もし sqlite3 に `.recover` がない場合や、より GUI（Windows など）対応の方法を希望する場合は、[このウィキの手順に従ってください。](/useful-tools#recovering-a-corrupt-db-ui)
- データベースのエラーの別の可能な原因は、データベースをネットワークドライブ（nfs や smb などのローカルでないもの）に配置していることです。**SQLite は、データとアプリケーションが同じマシン上に共存する状況を想定しています。** したがって、\*Arr AppData フォルダー（Docker の /config マウント）はローカルストレージ上にある必要があります。[SQLite とネットワークドライブはうまく動作せず、最終的にデータベースが壊れる原因になります](https://www.sqlite.org/draft/useovernet.html)。
- mergerFS を使用している場合は、`direct_io` を削除する必要があります。なぜなら、SQLite は mmap を使用しており、`direct_io` ではサポートされていないためです。詳細については、mergerFS の[ドキュメント](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)を参照してください。

## Mac で Prowlarr を使用していて、突然動作しなくなりました。何が起こったのでしょうか？

おそらくこれは、MacOS のバグにより Prowlarr データベースが破損したためです。破損したデータベースを復元するための FAQ エントリを確認してください。

## Windows サービスからトレイアプリに切り替える方法はありますか？

- Prowlarr をシャットダウンします
- Prowlarr ディレクトリ内にある serviceuninstall.exe を実行します
- 管理者として Prowlarr.exe を一度実行して、適切な権限を与え、ファイアウォールを開きます。完了したら、それを閉じて通常通り実行できます。
- （オプション）Prowlarr.exe のショートカットをスタートアップフォルダーにドロップして、起動時に自動的に起動します。

## Prowlarr のバックアップ/リストアはどのように行いますか？

### Prowlarr のバックアップ

#### 組み込みのバックアップを使用する場合

- Prowlarr UI で [システム] => [バックアップ] に移動します。
- バックアップボタンをクリックします。
- バックアップが作成されたら、zip ファイルをダウンロードして安全な場所に保存します。

#### ファイルシステムを直接使用する場合

- Prowlarr の AppData ディレクトリの場所を見つけます
  - Prowlarr UI で [システム] => [About] に移動します
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Prowlarr を停止します。これにより、データベースが破損するのを防ぎます。
- 内容を安全な場所にコピーします。

### バックアップからのリストア

> 異なるパスを使用する OS にリストアすることはできません（Windows から Linux、Linux から Windows、Windows から OS X、または OS X から Windows）。OS X と Linux の間で移動する場合は動作する可能性がありますが、サポートされていません。データベース内のすべてのパスを手動で編集する必要があります。
{.is-warning}

#### zip バックアップを使用する場合

- Prowlarr を再インストールします（該当する場合 / まだインストールされていない場合）。
- Prowlarr を実行します。
- [システム] => [バックアップ] に移動します。
- バックアップを復元します。
- [Choose File] を選択します。
- バックアップの zip ファイルを選択します。
- [Restore] を選択します。

#### ファイルシステムのバックアップを使用する場合

- Prowlarr を再インストールします（該当する場合 / まだインストールされていない場合）。
- Prowlarr の AppData ディレクトリの場所を見つけます
  - Prowlarr を一度実行し、UI で [システム] => [About] に移動します
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Prowlarr を停止します。
- AppData ディレクトリの内容を削除します **（.db-wal/.db-journal ファイルも存在する場合は削除します）**
- バックアップから復元します。
- Prowlarr を起動します。
- パスが同じであれば、すべてが前回の状態から再開されます。

#### Synology NAS でのファイルシステムのリストア

> 注意: Synology でのリストアには Linux の知識とルート SSH アクセスが必要です。
{.is-warning}

- Prowlarr を再インストールします（該当する場合 / まだインストールされていない場合）。
- Prowlarr の AppData ディレクトリの場所を見つけます
  - Prowlarr を一度実行し、UI で [システム] => [About] に移動します
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Prowlarr を停止します。
- SSH を介して Synology NAS に接続し、root としてログインします。

> インストールによっては、ユーザーが以下のコマンドと異なる場合があります: `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- 次のコマンドを実行します:

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- ファイルのアクセス権を更新します:

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Prowlarr を起動します。

## WebUI が Windows の localhost のみで読み込まれます

Web インターフェースに `http://localhost:9696/` または `http://127.0.0.1:9696` でアクセスできる場合、少なくとも一度、おそらく常に Prowlarr を管理者として実行する必要があります。

## Cookie の検索

一部のサイトでは自動的にログインできず、手動でログインしてから Prowlarr にクッキーを提供する必要があります。詳細については、[この記事](/useful-tools#finding-cookies)を参照してください。

## uTorrent が動作しなくなりました

- Web UI が有効になっていることを確認してください

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- Web UI をオンにします

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Alt Listening Port（Advanced => Web UI）が Listening Port（Connections）と同じでないことを確認してください。接続のポートフォワーディングに影響を与えないように、Web UI Alt Listening Port を変更することをお勧めします。

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## config.xml が破損しているというポップアップが表示されました。どうすればいいですか？

Prowlarrは、起動時に設定ファイルを読み取ることができず、何らかの方法で破損してしまったため、オンラインに戻すためには、AppDataフォルダ内の `.xml` を削除する必要があります。削除した後、Prowlarrを起動し、デフォルトのポート（9696）で起動します。その後、[General Settings](/prowlarr/settings/general) ページで設定した設定を再構成する必要があります。

## 無効な証明書やその他のHTTPSまたはSSLの問題

ダウンロードクライアントが動作しなくなり、「Localhostは無効な証明書です」というエラーが表示されていますか？

ProwlarrはSSL証明書を検証します。ダウンロードクライアントにSSL証明書が設定されていない場合、または自己署名のhttps証明書を使用していて、CA証明書がローカルの証明書ストアに追加されていない場合、Prowlarrは接続を拒否します。無料で適切に署名された証明書は、Let's Encryptから入手できます。

ダウンロードクライアントとProwlarrが同じマシンにある場合、HTTPSを使用する必要はありませんので、最も簡単な解決策は接続のSSLを無効にすることです。ほとんどの場合、ローカルネットワークでは必要ありません。セキュリティの脆弱なSSL設定を維持したい場合は、詳細設定で証明書の検証を無効にすることも可能です。

## ログインできなくなりました

{#help-i-have-forgotten-my-password}

認証を無効にする（忘れたユーザー名やパスワードをリセットする）には、[Prowlarr Appdata Directory](/prowlarr/appdata-directory) 内にある `config.xml` を編集する必要があります。

1. テキストエディタで `config.xml` を開きます。
1. 認証メソッドの行を探します。行は `<AuthenticationMethod>Basic</AuthenticationMethod>` または `<AuthenticationMethod>Forms</AuthenticationMethod>` になります。
1. `AuthenticationMethod` の行を `<AuthenticationMethod>None</AuthenticationMethod>` に変更します。
1. Prowlarr を再起動します。
1. Prowlarr は今後パスワードなしでアクセスできるようになります。UIの `Settings: General` に移動し、ユーザー名とパスワードを設定してください。

## 奇妙なUIの問題

- 奇妙なUIの問題や特定のビューやソートが機能しない場合は、ChromeのシークレットウィンドウやFirefoxのプライベートウィンドウで表示してみてください。そこで正常に動作する場合は、特定のIP/ドメインのブラウザのキャッシュとクッキーをクリアしてください。詳細については、[Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) のウィキ記事を参照してください。

## VPN、Jackett、および \*ARRs

- 中国、オーストラリア、南アフリカなどの抑圧的な国を除いて、通常、トレントクライアントのみがVPNの背後にある必要があります。VPNエンドポイントは多くのユーザーと共有されているため、各ソフトウェアが使用するさまざまなサービスからのレート制限、DDOS保護、IP禁止が発生する可能性があります。
- 言い換えれば、\*Arrs（Lidarr、Prowlarr、Radarr、Readarr、Lidarr）をVPNの背後に配置すると、アプリケーションが使用できなくなる場合があります。

> **明確に言いますが、VPNは\*Arrsとの問題が発生するかどうかではなく、いつ発生するかです: 画像プロバイダーはブロックされ、Cloudflareは\*Arrサーバー（更新、メタデータなど）の前にあり、ブロックされる可能性があります**
{.is-warning}

- **多くのプライベートトラッカーは、VPNを使用してそれらにアクセスすること（JackettやProwlarrを使用すること）を禁止します。**

### VPNの使用

- VPNが必要であり、Dockerを使用している場合は、HotioまたはBinhexのDownload Client + VPNコンテナを使用することをお勧めします。
- VPNが必要であり、Dockerを使用していない場合は、VPNクライアントがスプリットトンネリングをサポートしている必要があります。これにより、必要な（Download Client）アプリのみがVPNの背後に配置されます。
- トラッカーへのアクセスに関する多くの問題は、ISPのDNSサーバーの代わりにGoogleやCloudflareのDNSサーバーを使用することで解決できます。
- 一部の場合（英国のISPなど）、トレントダウンロードクライアントをVPNの背後に配置し、Jackett/Prowlarrを次のように設定する必要があります：
  - JackettをVPNの背後に配置し、スプリットトンネリングがローカルアクセスを許可するようにします。
  - Prowlarrの場合、vpnクライアントを設定してプロキシを提供し、プロキシを [Settings => Indexers](/prowlarr/settings/indexers) に追加します。プロキシにタグを付け、それを使用する必要があるインデクサーにも同じタグを付けます。
    - 必要な場合、およびvpnがプロキシを作成する方法を提供していない場合は、ProwlarrをVPNの背後に配置し、スプリットトンネリングがローカルアクセスを許可するようにします。

## ブラウザの起動を停止するにはどうすればいいですか？

OSによって、複数の方法があります。

- 一部のOSでは、`Settings` => `General` にチェックボックスがあり、起動時にブラウザを起動するかどうかを選択できます。
- Prowlarrを起動する際に、引数に `-nobrowser`（*nix）または `/nobrowser`（Windows）を追加することができます。
- Prowlarrを停止し、config.xmlファイルを編集し、`<LaunchBrowser>True</LaunchBrowser>` を `<LaunchBrowser>False</LaunchBrowser>` に変更します。

## 一度にすべてのインデクサーを簡単に追加できますか？

いいえ。これは良いことではなく、この機能は追加されません。インデクサーを慎重に選択し、遅すぎるかつ取得できないインデクサーを削除するために統計に注意を払うことがはるかに良いです。インデクサーの適切な剪定とメンテナンスは、全体的にはるかに優れた結果をもたらし、アプリケーションの検索結果も速くなります。