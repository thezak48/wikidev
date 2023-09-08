以下のMarkdownコンテンツを日本語に翻訳してください。

```markdown
# Getting Started

Welcome to our platform! This guide will help you get started with using our services.

## Sign Up

To get started, you need to sign up for an account. Visit our [Sign Up](https://www.example.com/signup) page and fill out the registration form. Once you have completed the form, click the "Sign Up" button.

## Logging In

After signing up, you can log in to your account by visiting our [Login](https://www.example.com/login) page. Enter your username and password, then click the "Log In" button.

## Resetting Password

If you forget your password, you can reset it by clicking the "Forgot Password" link on the login page. Enter your email address and click the "Reset Password" button. You will receive an email with instructions on how to reset your password.

## Navigating the Dashboard

Once you are logged in, you will be taken to the dashboard. The dashboard provides an overview of your account and allows you to access various features and settings.

## Contacting Support

If you have any questions or need assistance, you can contact our support team by visiting our [Contact Us](https://www.example.com/contact) page. Fill out the contact form and click the "Submit" button. Our support team will get back to you as soon as possible.

{/*examples*/}
```


---
title: Lidarr システム
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, system
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# 目次

- [目次](#目次)
- [ステータス](#ステータス)
  - [ヘルス](#ヘルス)
    - [システムの警告](#システムの警告)
      - [ブランチが有効なリリースブランチではありません](#ブランチが有効なリリースブランチではありません)
      - [.NET バージョンに更新してください](#net-バージョンに更新してください)
        - [Docker インストールの修正方法](#docker-インストールの修正方法)
        - [スタンドアロンインストールの修正方法](#スタンドアロンインストールの修正方法)
      - [現在のインストールされている mono バージョンは古く、サポートされていません](#現在のインストールされている-mono-バージョンは古くサポートされていません)
      - [現在のインストールされている SQLite バージョンはサポートされていません](#現在のインストールされている-sqlite-バージョンはサポートされていません)
      - [新しいアップデートが利用可能です](#新しいアップデートが利用可能です)
      - [ユーザーがスタートアップフォルダに書き込みできないため、アップデートをインストールできません](#ユーザーがスタートアップフォルダに書き込みできないためアップデートをインストールできません)
      - [アップデートは AppData の削除を防ぐために不可能です](#アップデートは-appdata-の削除を防ぐために不可能です)
      - [ブランチは以前のバージョン用です](#ブランチは以前のバージョン用です)
      - [signalR に接続できませんでした](#signalr-に接続できませんでした)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [設定されたプロキシホストの IP アドレスを解決できませんでした](#設定されたプロキシホストの-ip-アドレスを解決できませんでした)
      - [プロキシのテストに失敗しました](#プロキシのテストに失敗しました)
      - [システムの時刻が 1 日以上ずれています](#システムの時刻が-1-日以上ずれています)
      - [Mono レガシー TLS が有効になっています](#mono-レガシー-tls-が有効になっています)
      - [Mono と x86 ビルドは終了します](#mono-と-x86-ビルドは終了します)
      - [FPcalc を更新する必要があります](#fpcalc-を更新する必要があります)
    - [ダウンロードクライアント](#ダウンロードクライアント)
      - [ダウンロードクライアントが利用できません](#ダウンロードクライアントが利用できません)
      - [ダウンロードクライアントとの通信ができません](#ダウンロードクライアントとの通信ができません)
      - [ダウンロードクライアントが失敗したため、ダウンロードクライアントは利用できません](#ダウンロードクライアントが失敗したためダウンロードクライアントは利用できません)
      - [完了したダウンロードの処理を有効にする](#完了したダウンロードの処理を有効にする)
      - [Docker のリモートパスマッピングが正しくありません](#docker-のリモートパスマッピングが正しくありません)
      - [ルートフォルダにダウンロードしています](#ルートフォルダにダウンロードしています)
      - [ダウンロードクライアントの設定が正しくありません](#ダウンロードクライアントの設定が正しくありません)
      - [リモートパスマッピングが正しくありません](#リモートパスマッピングが正しくありません)
      - [権限エラー](#権限エラー)
      - [処理中にリモートファイルが削除されました](#処理中にリモートファイルが削除されました)
      - [リモートパスが使用され、インポートに失敗しました](#リモートパスが使用されインポートに失敗しました)
    - [完了/失敗したダウンロードの処理](#完了失敗したダウンロードの処理)
      - [完了したダウンロードの処理は無効です](#完了したダウンロードの処理は無効です)
    - [インデクサ](#インデクサ)
      - [自動検索が有効なインデクサが利用できません。Lidarr は自動検索結果を提供しません](#自動検索が有効なインデクサが利用できませんlidarr-は自動検索結果を提供しません)
      - [RSS 同期が有効なインデクサが利用できません。Lidarr は新しいリリースを自動的に取得しません](#rss-同期が有効なインデクサが利用できませんlidarr-は新しいリリースを自動的に取得しません)
      - [インデクサが有効になっていません](#インデクサが有効になっていません)
    - [有効なインデクサは検索をサポートしていません](#有効なインデクサは検索をサポートしていません)
      - [インタラクティブ検索が有効なインデクサがありません](#インタラクティブ検索が有効なインデクサがありません)
      - [インデクサが障害のため利用できません](#インデクサが障害のため利用できません)
      - [Jackett の全エンドポイントが使用されています](#jackett-の全エンドポイントが使用されています)
        - [解決策](#解決策)
    - [アーティストフォルダ](#アーティストフォルダ)
      - [ルートフォルダが見つかりません](#ルートフォルダが見つかりません)
      - [リストが障害のため利用できません](#リストが障害のため利用できません)
  - [ディスクスペース](#ディスクスペース)
  - [情報](#情報)
  - [詳細情報](#詳細情報)
- [タスク](#タスク)
  - [スケジュールされたタスク](#スケジュールされたタスク)
  - [キュー](#キュー)
- [バックアップ](#バックアップ)
- [アップデート](#アップデート)
- [イベント](#イベント)
- [ログファイル](#ログファイル)

> 警告: このページは作業中であり、現在は Readarr を基にした草案です
{.is-danger}

# ステータス

## ヘルス

このページには、ヘルスチェックエラーのリストが含まれています。これらのヘルスチェックは、Lidarr によって定期的に実行され、特定のイベントで実行されます。警告やエラーの結果は、解決方法についてのアドバイスを提供するためにここにリストされています。

### システムの警告

#### ブランチが有効なリリースブランチではありません

設定したブランチは有効なリリースブランチではありません。アップデートは受信できません。[現在のリリースブランチ](/lidarr/faq#how-do-i-update-lidarr) のいずれかに変更してください。

#### .NET バージョンに更新してください

{#update-to-net-core-version}

- Lidarr の新しいバージョンは .NET6 以降を対象としています。v1.0 リリース後にレガシーな mono ビルドは提供されなくなります。現在、これらのレガシービルドを実行していますが、プラットフォームは .NET をサポートしています。

##### Docker インストールの修正方法

- コンテナを再取得してください。

##### スタンドアロンインストールの修正方法

- 次のステップの前に、既存の設定をバックアップしてください。
- これは通常、Linux ホストでのみ発生します。Microsoft の .NET ランタイムまたは SDK をインストールしないでください。
- 修正するには、アーキテクチャに合った正しいビルドをダウンロードし、既存のバイナリ（アプリケーション）を置き換える必要があります。
- 要するに、既存のバイナリ（/opt/Lidarr の内容またはフォルダー）を削除し、ダウンロードした .tar.gz の内容で置き換える必要があります。

> 既存のバイナリの上にダウンロードを展開しないでください。
> まず古いバイナリを削除する必要があります。
{.is-warning}

- 以下は、ユーザーが開発したスクリプトで、mono のインストールを削除し、.NET のインストールに置き換えるものです。貢献や修正は歓迎します。
- これは、`master` Lidarr ブランチを想定しています。必要に応じて変数を更新してください。
- これは、Lidarr がユーザー `lidarr` として実行されていることを前提としています。必要に応じて変数を更新してください。
- これは、Lidarr が `/opt/Lidarr` にインストールされていることを前提としています。必要に応じて変数を更新してください。

```bash
#!/bin/bash
## User Variables
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /User Variables
app="lidarr"
ARCH=$(dpkg --print-architecture)
# Stop \*arr
sudo systemctl stop $app
# get arch
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arch not supported"
    exit 1
    ;;
esac
echo "Downloading..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installation files downloaded and extracted"
echo "Moving existing installation"
sudo mv "$installdir/" "$installdir.old/"
echo "Installing..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App Installed"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### 現在のインストールされている mono バージョンは古く、サポートされていません

- Lidarr は .NET で書かれており、非常に古い ARM プロセッサで実行するために Mono が必要です。ただし、v1.0 以降、Mono ビルドはサポートされなくなります。
- Lidarr の最低バージョンは Mono 5.20 です。
- Mono のアップグレード手順はプラットフォームによって異なります。

#### 現在のインストールされている SQLite バージョンはサポートされていません

- Lidarr はデータを SQLite データベースに保存しています。システムにインストールされている SQLite3 ライブラリが古すぎます。Lidarr にはバージョン 3.9.0 以上が必要です。Lidarr は SQLite3 のアップグレードパッケージに含まれている場合もある `libSQLite3.so` を使用しています。

#### 新しいアップデートが利用可能です

- 開発者が新しいアップデートをリリースしました。これは通常、素晴らしい新機能とバグの修正を意味します（そうですよね？）。自動更新が有効になっていないため、自分でアップデートする方法を見つける必要があります。おそらく、`System => Updates` ページのインストールボタンを押すことが良い出発点になるでしょう。

> 現在のバージョンが 14 日未満の場合、この警告は表示されません
{.is-info}

#### ユーザーがスタートアップフォルダに書き込みできないため、アップデートをインストールできません

- これは Lidarr が自身をアップデートできないことを意味します。Lidarr を手動でアップデートするか、Lidarr のスタートアップディレクトリ（インストールディレクトリ）のアクセス許可を設定して、Lidarr が自身をアップデートできるようにする必要があります。

#### アップデートは AppData の削除を防ぐために不可能です

- Lidarr は、AppData フォルダがオペレーティングシステムのディレクトリ内にあることを検出しました。通常、Windows の場合は `C:\ProgramData`、Linux の場合は `~/.config` です。

- 現在の AppData とスタートアップディレクトリの場所を確認するには、`System => Info` を参照してください。
- これは、データの損失のリスクを避けるために Lidarr が自身をアップデートできないことを意味します。
- Linux の場合、Lidarr を実行しているユーザーのホームディレクトリを変更し、現在の `~/.config/Lidarr` ディレクトリの内容をコピーする必要があります。

#### ブランチは以前のバージョン用です

- `Settings => General` で設定されたアップデートブランチは以前のバージョンの Lidarr 用です。したがって、インスタンスは `System => Updates` フィードで正しいアップデート情報を表示せず、リリース時に新しいアップデートを受信しない可能性があります。

#### signalR に接続できませんでした

- signalR は動的な UI の更新を行います。したがって、ブラウザがサーバーの signalR に接続できない場合、UI でリアルタイムの更新が表示されません。

- これは、リバースプロキシや Cloudflare の使用時に最も一般的に発生します。
- Cloudflare では、WebSockets を有効にする必要があります。

##### NGINX

- Nginx では、アプリケーションの場所ブロックに次の追加が必要です:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> nginx のドキュメントで提案されているように `proxy_set_header Connection "Upgrade";` を含めないでください。これは機能しません
> 参照: <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- Apache2 のリバースプロキシでは、次のモジュールを有効にする必要があります: proxy、proxy_http、および proxy_wstunnel。次に、次の WebSocket トンネルディレクティブを vhost の設定に追加します:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- Caddy（V1）の場合は、次のようにします。
- 注意: Lidarr の設定にも websocket ディレクティブを追加する必要があります。

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### 設定されたプロキシホストの IP アドレスを解決できませんでした

プロキシの設定を確認し、正確な情報を入力してください。
プロキシが稼働しており、アクセス可能であることを確認してください。

#### プロキシのテストに失敗しました

設定されたプロキシのテストに失敗しました。提供された HTTP エラーを確認するか、詳細についてはログを確認してください。

#### システムの時刻が 1 日以上ずれています

システムの時刻が 1 日以上ずれています。時刻が修正されるまで、スケジュールされたタスクが正しく実行されない場合があります。
システムの時刻を確認し、信頼できる時刻サーバーに同期されていることを確認してください。

#### Mono レガシー TLS が有効になっています

Mono 4.x の TLS 回避策がまだ有効になっています。`MONO_TLS_PROVIDER=legacy` 環境オプションを削除することを検討してください。

#### Mono と x86 ビルドは終了します

次のビルドでは、Mono と x86 ビルドはサポートされなくなります。このエラーが表示される場合、アプリケーションの mono バージョンまたは x86 バージョンを実行しています。これらのレガシーバージョンの開発サポートがますます困難になったため、これらのバージョンのサポートを終了し、今後のリリースではリリースを中止することがアドバイスされます。したがって、x86 または mono を必要としないサポートされているオペレーティングシステムにアップグレードすることをお勧めします。また、必要に応じて Docker を使用することも検討できます。

#### FPcalc を更新する必要があります

{#fpcalc-upgrade}

- Lidarr は、トラックを識別するために chromaprint オーディオフィンガープリントを使用しています。これには外部バイナリ `fpcalc` が必要です。このバイナリは Lidarr v1 用に Windows、Linux、macOS で配布されていますが、freeBSD では独自に提供する必要があります。
- Lidarr にバンドルされている fpcalc バイナリが実行可能（755 のパーミッション）であることを確認してください。これは Lidarr のインストールディレクトリ（たとえば `/opt/Lidarr/fpcalc`）にあります。実行可能でない場合は、以下のコマンドでパーミッションを修正し、Lidarr を再起動してください。
  - 修正には `sudo` が必要な場合や、Lidarr のバイナリフォルダのパスが環境やセットアップによって異なる場合がありますので、注意してください。

```bash
chmod +x /opt/Lidarr/fpcalc
```

> 以下の情報は、旧バージョン v0.8.0 のみに適用されます。
{.is-info}

- ネイティブ Linux インスタンスでこれを修正するには、パッケージマネージャを使用して適切なパッケージをインストールし、fpcalc が PATH にあることを確認してください（which fpcalc を使用して確認し、正しい fpcalc の場所が返されるかどうかを確認します）。

| ディストリビューション |         パッケージ         |
| :-------------------: | :----------------------: |
|   Debian/Ubuntu       | libchromaprint-tools      |
|   Fedora/CentOS       | chromaprint-tools         |
|         Arch          | chromaprint               |
|       OpenSUSE        | chromaprint-fpcalc        |
|       Synology        | chromaprint               |

### ダウンロードクライアント

#### ダウンロードクライアントが利用できません

Lidarr がメディアをダウンロードするためには、適切に設定された有効なダウンロードクライアントが必要です。Lidarr はさまざまなダウンロードクライアントをサポートしているため、要件に最も適合するものを選択する必要があります。すでにダウンロードクライアントがインストールされている場合は、Lidarr でそれを使用し、カテゴリを作成する必要があります。`Settings=>Download Client` を参照してください。

#### ダウンロードクライアントとの通信ができません

Lidarr が設定されたダウンロードクライアントと通信できませんでした。ダウンロードクライアントが動作していることと、URL が正しいことを確認してください。これは認証エラーを示す場合もあります。
通常、これは正しく設定されていないダウンロードクライアントによるものです。通常、次のようなことを確認できます。
- ダウンロードクライアントの IP アドレス - すべてが同じベアメタルマシン上にある場合、これは通常 `127.0.0.1` です。
- ダウンロードクライアントが使用しているポート番号 - これらはデフォルトのポート番号で埋められていますが、変更した場合は Lidarr にも同じポート番号を入力する必要があります。
- Lidarr インスタンスとダウンロードクライアントがローカルネットワーク上で使用されている場合、SSL 暗号化がオンになっていないことを確認してください。詳細については、SSL の FAQ エントリを参照してください。

#### ダウンロードクライアントが失敗したため、ダウンロードクライアントは利用できません

ダウンロードクライアントのいずれかが Lidarr のリクエストに応答しなかったため、Lidarr は通常の 1 分ごとのサイクルでダウンロードクライアントにクエリを送信するのを一時停止しました。これは通常、アクティブなダウンロードを追跡し、完了したダウンロードをインポートするために使用されます。ただし、Lidarr は引き続きダウンロードをダウンロードクライアントに送信しようとしますが、おそらく失敗するでしょう。
失敗の理由については、`System=>Logs` を確認してください。
このダウンロードクライアントをもう使用しない場合は、Lidarr で無効にしてエラーを防ぐことができます。

#### 完了したダウンロードの処理を有効にする

Lidarr は、ダウンロードクライアントによってダウンロードされたファイルをインポートするために「完了したダウンロードの処理」が必要です。完了したダウンロードの処理を有効にすることをお勧めします（新しいユーザーの場合、デフォルトで有効になっています）。

#### Docker のリモートパスマッピングが正しくありません

このエラーは、ダウンロードクライアントまたは Lidarr の Docker パスが正しくない場合に通常発生します。

- 正しくない（一貫性のない）パスの例:
  - ダウンロードクライアント: `/mnt/user/downloads:/downloads`
  - Lidarr: `/mnt/user/downloads:/data`
- この例では、ダウンロードクライアントは `/downloads` にダウンロードを配置し、完了した本が `/downloads` にあると伝えます。Lidarr は `/downloads` にチェックを入れます。Lidarr は「OK、いいよ、`/downloads` をチェックしてみましょう」と言います。Lidarr は `/downloads` のパスを割り当てていないので、このエラーが発生します。
- これを修正する最も簡単な方法は、一貫性です。ダウンロードクライアントで1つのスキームを使用する場合は、すべての場所で同じスキームを使用します。

- Team Lidarr は、単に `/data` を使用することをお勧めします。

  - ダウンロードクライアント: `/mnt/user/data/downloads:/data/downloads`
  - Lidarr: `/mnt/user/data:/data`

- ダウンロードクライアント内で、ダウンロードをどこに置くかを指定できます。ダウンロードクライアントには、たとえば「はい、ダウンロードクライアント、ファイルを `/data/downloads/movies` に置いてください」と伝えることができます。Lidarr は、ダウンロードクライアントが完了したと伝えると、Lidarr は `/data` を持っており、`/data/downloads/movies` も見ることができます。すべてが正常です。
- 素晴らしいガイドがたくさんあります: 当社のウィキ [Docker ガイド](/docker-guide) と TRaSH の [ハードリンクとインスタントムーブ（アトミックムーブ）](https://trash-guides.info/hardlinks/)。これらのガイドはハードリンクとアトミックムーブに重点を置いていますが、コンテナとパスマッピングの概念がこれらの議論の中心です。
- オペレーティングシステムをまたいだ場合、またはネイティブと Docker を使い分ける場合は、リモートパスマップが必要です。詳細については、[TRaSH の Radarr のリモートパスガイド](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) と [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/) を参照してください。

#### ルートフォルダにダウンロードしています

{#downloads-in-root-folder}

アプリケーション内では、ルートフォルダは設定されたメディアライブラリフォルダと定義されます。これはマウントのルートフォルダではありません。ダウンロードクライアントが、ルート（ライブラリ）フォルダに不完全または完全なダウンロード（または完了したダウンロードを移動）を配置しています。
これは頻繁に問題を引き起こし、データの損失を含む場合があります。これを修正するには、ダウンロードクライアントを変更して、ルートフォルダにダウンロードを配置しないようにしてください。なお、'配置' には、ダウンロードクライアントのカテゴリがルートフォルダに設定されている場合や、NZBGet/SABnzbd がソートを有効にしてルートフォルダにソートしている場合も含まれます。
このチェックは、現在使用されているルートフォルダだけでなく、追加されたすべての定義済みのルートフォルダを調べます。つまり、ダウンロードクライアントがダウンロードを配置する場所、または完了したダウンロードを移動する場所は、*arr アプリケーションのルート/ライブラリ/最終メディアの宛先フォルダと同じであってはなりません。
設定されたルートフォルダ（ライブラリフォルダ）は、[Settings => Media Management => Root Folders](/lidarr/settings/#root-folders) で見つけることができます。
例えば、ダウンロードが `\data\downloads` に行く場合、ルートフォルダが `\data\downloads` と設定されているアルバムを見つけて、正しいルートフォルダに編集してください。
問題のアーティストを見つける最も簡単な方法は次のとおりです:

- アーティスト（ライブラリ）タブに移動します。
- 古いルートフォルダパスでカスタムフィルタを作成します。
- 上部バーの「一括編集」を選択し、ルートパスのドロップダウンからこれらのアーティストを移動する新しいルートパスを選択します。
- 次に、次のポップアップが表示されます。「アーティストフォルダを 'root path