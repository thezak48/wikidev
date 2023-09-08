---
title: Readarr Linux インストール
description: Readarr の Linux インストールガイド
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> 注意: Raspberry Pi OS と Raspbian は Debian のフレーバーです {.is-info}

### 簡単なインストール

Debian / Ubuntu / Raspbian の初心者のために、Apt リポジトリや Deb パッケージはありません。

簡単な方法を希望する場合は、コミュニティが提供し、メンテナンスされている `Easy Install` スクリプトに従って、Debian (Raspbian / Raspberry Pi OS) / Ubuntu の基本的なインストールを行ってください。

**「ハンズオン」な公式のインストール手順に従いたい場合は、以下の [Debian / Ubuntu ハンズオンインストール](#debian-ubuntu-hands-on-install) の手順を進めてください。**

[\*Arr コミュニティのインストールスクリプトを参照してください](/install-script)

### Debian / Ubuntu ハンズオンインストール

以下のコマンドを使用してバイナリをインストールする必要があります。

> 以下の手順では、Readarr をダウンロードして `/opt` にインストールします。
> Readarr はユーザー `readarr` とグループ `media` の下で実行されます。`media` は、\*Arrs、ダウンロードクライアント、メディアサーバーを実行するために一般的に推奨されるグループです。
> Readarr の設定ファイルは `/var/lib/readarr` に保存されます。
{.is-warning}

- 必要な前提パッケージをインストールしてください。

```shell
sudo apt install curl sqlite3
```

> 警告: 以下の前提条件を無視すると、インストールに失敗し、アプリケーションが機能しなくなります。 {.is-warning}

> **インストールの前提条件**
> 以下の手順は、次の前提条件に基づいています。必要に応じて、特定の要件に合わせて手順を変更してください。
> \* ユーザー `readarr` が作成されている
> \* ユーザー `readarr` がグループ `media` の一部である
> \* ダウンロードクライアントとメディアサーバーがグループ `media` として実行され、その一部である
> \* ダウンロードクライアントとメディアサーバーで使用するパスがグループ `media` にアクセス可能（読み取り/書き込み）である
> \* Calibre を使用する場合、Calibre はグループ `media` として実行され、Calibre ライブラリには `media` の読み取り/書き込み権限があります
> \* ディレクトリ `/var/lib/readarr` を作成し、ユーザー `readarr` がそれに対して読み取り/書き込み権限を持つことを確認しました
{.is-danger}

> 以下を続行することで、上記の要件を読み、満たしたことを認識しています。 {.is-warning}

- アーキテクチャに応じた正しいバイナリをダウンロードします。
  - `dpkg --print-architecture` コマンドでアーキテクチャを確認できます
    - AMD64 の場合は `arch=x64` を使用します
    - ARM、armf、および armh の場合は `arch=arm` を使用します
    - ARM64 の場合は `arch=arm64` を使用します

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- ファイルを展開します。

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- ファイルを `/opt/` に移動します。

```shell
sudo mv Readarr /opt/
```

> 注意: これは、ユーザー `readarr` とグループ `media` として作成し、実行することを前提としています。必要に応じてこれを変更して、使用状況に合わせて選択することが重要です。メディアファイルの許可問題を回避するために、少なくともグループ名をダウンロードクライアントと Readarr の間で同じにすることをお勧めします。Calibre を使用する場合は、Readarr がそのディレクトリに対して権限を持つ必要があることに注意してください。
{.is-danger}

- バイナリディレクトリの所有権を確認します。

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- systemd を設定して、Readarr が起動時に自動的に起動するようにします。

> 以下の systemd 作成スクリプトは、データディレクトリとして `/var/lib/readarr` を使用します。存在しない場合は、必要に応じて変更してください。デフォルトのデータディレクトリ `/home/$USER/.config/Readarr` の場合は、`-data` 引数を削除してください。なお、`$USER` は Readarr が実行されるユーザーであり、以下で定義されています。
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr.service > /dev/null
[Unit]
Description=Readarr Daemon
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/readarr/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- systemd をリロードします。

```shell
sudo systemctl -q daemon-reload
```

- Readarr サービスを有効にします。

```shell
sudo systemctl enable --now -q readarr
```

- (オプション) tar ボールを削除します。

```shell
rm Readarr*.linux*.tar.gz
```

通常、Readarr の Web GUI にアクセスするには、`http://{サーバーの IP アドレス}:8787` にアクセスします。

Readarr が起動しなかった場合は、サービスのステータスを確認してください。

```shell
sudo journalctl --since today -u readarr
```

---

### アンインストール

アンインストールして削除するには:
> 警告: これにより、アプリケーションデータが破棄されます。 {.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

アンインストールしてアプリケーションデータを保持するには:

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```