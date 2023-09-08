---
title: Radarr Linux インストール
description: Radarr の Linux インストールガイド
published: true
date: 2023-09-07T20:43:01.533Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:59.391Z
---

# Linux

## Debian / Ubuntu

> 注意: Raspberry Pi OS と Raspbian はいずれも Debian の派生版です {.is-info}

### 簡単なインストール

Debian / Ubuntu / Raspbian の初心者のために、Apt リポジトリや Deb パッケージはありません。

簡単な方法をお求めの場合は、コミュニティが提供し、メンテナンスされている `Easy Install` スクリプトを使用して、Debian (Raspbian / Raspberry Pi OS) / Ubuntu のベースインストールを行ってください。

**公式の手順に従ってインストールする場合は、以下の [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) の手順を参照してください。**

[\*Arr コミュニティのインストールスクリプトを参照してください](/install-script)

> Radarr はメディアファイルの解析にバンドルされた ffprobe のバージョンを使用しており、システムに ffprobe や ffmpeg のインストールは必要ありません。もし Radarr が Ffprobe が見つからないと言っている場合は、再インストールで問題が解決することが一般的です。
{.is-info}

### Debian / Ubuntu Hands on Install

以下のコマンドを使用してバイナリをインストールする必要があります。

> 以下の手順では、安定版 (`master` リリースブランチ) の Radarr をダウンロードし、`/opt` にインストールします。
> Radarr はユーザー `radarr` とグループ `media` の下で実行されます。`media` は、\*Arrs、ダウンロードクライアント、メディアサーバーを実行するために一般的に推奨されるグループです。
> Radarr の設定ファイルは `/var/lib/radarr` に保存されます。
{.is-success}

- 必要な前提パッケージをインストールしてください:

```shell
sudo apt install curl sqlite3
```

> 警告: 以下の前提条件を無視すると、インストールに失敗し、アプリケーションが機能しなくなります。 {.is-warning}

> **インストールの前提条件**
> 以下の手順は、次の前提条件に基づいています。必要に応じて、自分の特定のニーズに合わせて手順を変更してください。
> \* ユーザー `radarr` が作成されている
> \* ユーザー `radarr` がグループ `media` の一部である
> \* ダウンロードクライアントとメディアサーバーがグループ `media` の一部として実行されている
> \* ダウンロードクライアントとメディアサーバーで使用されるパスがグループ `media` によってアクセス可能 (読み書き可能) である
> \* ディレクトリ `/var/lib/radarr` を作成し、ユーザー `radarr` がそれに対して読み書きの権限を持っていることを確認してください
> \* 以前のインストールは、[FAQ](/radarr/faq) で注記されている `master` リリースブランチを使用しているか、ダウンロード URL で `master` を更新しています
{.is-danger}

> 以下を続行することで、上記の要件を読み、満たしていることを認識しています。 {.is-success}

- アーキテクチャに応じた正しいバイナリをダウンロードしてください。
  - アーキテクチャは `dpkg --print-architecture` で確認できます
    - AMD64 の場合は `arch=x64` を使用します
    - ARM、armf、および armh の場合は `arch=arm` を使用します
    - ARM64 の場合は `arch=arm64` を使用します

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- ファイルを展開してください:

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- ファイルを `/opt/` に移動してください:

```shell
sudo mv Radarr /opt/
```

> 注意: これはユーザー `radarr` とグループ `media` の下で実行することを前提としています。必要に応じてこれを変更して自分のユースケースに合わせてください。メディアファイルのパーミッションの問題を回避するために、少なくともグループ名をダウンロードクライアントと Radarr の間で同じにすることをおすすめします。
{.is-danger}

- バイナリディレクトリの所有権を確認してください。

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- systemd を設定して、Radarr が起動時に自動的に起動するようにしてください。

> 以下の systemd の作成スクリプトは、データディレクトリとして `/var/lib/radarr` を使用します。存在しない場合は、必要に応じて修正してください。デフォルトのデータディレクトリ `/home/$USER/.config/Radarr` の場合は、`-data` 引数を削除してください。なお、`$USER` は Radarr が実行されるユーザーであり、以下で定義されています。
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr.service > /dev/null
[Unit]
Description=Radarr Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- systemd をリロードしてください:

```shell
sudo systemctl -q daemon-reload
```

- Radarr サービスを有効にしてください:

```shell
sudo systemctl enable --now -q radarr
```

- (オプション) tar ボールを削除してください:

```shell
rm Radarr*.linux*.tar.gz
```

通常、Radarr の Web GUI にアクセスするには、`http://{サーバーの IP アドレス}:7878` にアクセスしてください。

> Radarr はメディアファイルの解析にバンドルされた ffprobe のバージョンを使用しており、システムに ffprobe や ffmpeg のインストールは必要ありません。もし Radarr が Ffprobe が見つからないと言っている場合は、再インストールで問題が解決することが一般的です。
{.is-info}

もし Radarr が起動しないようであれば、サービスのステータスを確認してください:

```shell
sudo journalctl --since today -u radarr
```

---

### アンインストール

アンインストールとパージ:

> 警告: これによりアプリケーションデータが破壊されます。 {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

アンインストールしてアプリケーションデータを保持する場合:

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```