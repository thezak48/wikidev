---
title: Lidarr Linux インストール
description: Lidarr の Linux インストールガイド
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> 注意: Raspberry Pi OS と Raspbian は Debian のフレーバーです {.is-info}

> Lidarr v0.8 は Ubuntu 22.04 と互換性がなく、サポートされていません [詳細はこちらの FAQ エントリを参照してください](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### 簡単なインストール

Debian / Ubuntu / Raspbian の初心者の方には、Apt リポジトリや Deb パッケージはありません。

簡単な方法を希望する場合は、コミュニティが提供し、メンテナンスされている `Easy Install` スクリプトに従って、Debian (Raspbian / Raspberry Pi OS) / Ubuntu のベースインストールを行ってください。

**詳しい手順については、[Debian / Ubuntu ハンズオンインストール](#debian-ubuntu-hands-on-install) の公式インストール手順を参照してください。**

[\*Arr コミュニティインストールスクリプトをご覧ください](/install-script)

### Debian / Ubuntu ハンズオンインストール

以下のコマンドを使用してバイナリをインストールする必要があります。

> 以下の手順では、Lidarr をダウンロードして `/opt` にインストールします
> Lidarr はユーザー `lidarr` とグループ `media` の下で実行されます
> Lidarr の設定ファイルは `/var/lib/lidarr` に保存されます
{.is-warning}

- 必要な前提パッケージをインストールしてください:

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> 警告: 以下の前提条件を無視すると、インストールに失敗し、アプリケーションが機能しなくなります。 {.is-warning}

> **インストールの前提条件**
> 以下の手順は、次の前提条件に基づいています。必要に応じて、自分の特定のニーズに合わせて手順を変更してください。
> \* ユーザー `lidarr` が作成されている
> \* ユーザー `lidarr` がグループ `media` の一部である
> \* ダウンロードクライアントとメディアサーバーがグループ `media` の一部であり、ユーザー `lidarr` として実行されます
> \* ダウンロードクライアントとメディアサーバーで使用するパスがグループ `media` にアクセス可能（読み書き可能）である
> \* ディレクトリ `/var/lib/lidarr` を作成し、ユーザー `lidarr` がそれに対して読み書きの権限を持つことを確認しました
{.is-danger}

> 以下を続行することで、上記の要件を読み、満たしたことを認識します。 {.is-warning}

- アーキテクチャに応じた正しいバイナリをダウンロードします。
  - アーキテクチャは `dpkg --print-architecture` で確認できます
    - AMD64 の場合は `arch=x64` を使用します
    - ARM、armf、および armh の場合は `arch=arm` を使用します
    - ARM64 の場合は `arch=arm64` を使用します

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- ファイルを展開します:

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- ファイルを `/opt/` に移動します

```shell
sudo mv Lidarr/ /opt
```

> これは、ユーザーを作成し、ユーザー `lidarr` とグループ `media` として実行することを前提としています。これを適切に選択して、メディアファイルの権限の問題を回避するためにこれらを正しく選択することが重要です。ダウンロードクライアントと Lidarr の間で少なくともグループ名が同じであることをお勧めします。
{.is-danger}

- バイナリディレクトリの所有権を確認します。

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Lidarr が起動時に自動的に起動できるように systemd を設定します。

> 以下の systemd 作成スクリプトは、データディレクトリとして `/var/lib/lidarr` を使用します。存在しない場合は、必要に応じて変更してください。デフォルトのデータディレクトリ `/home/$USER/.config/Lidarr` の場合は、`-data` 引数を削除してください。なお、`$USER` は Lidarr が実行されるユーザーであり、以下で定義されています。
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/lidarr.service > /dev/null
[Unit]
Description=Lidarr Daemon
After=syslog.target network.target
[Service]
User=lidarr
Group=media
Type=simple

ExecStart=/opt/Lidarr/Lidarr -nobrowser -data=/var/lib/lidarr/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- systemd をリロードします:

```shell
sudo systemctl -q daemon-reload
```

- Lidarr サービスを有効にします:

```shell
sudo systemctl enable --now -q lidarr
```

- (オプション) tar ボールを削除します:

```shell
rm Lidarr*.linux*.tar.gz
```

通常、Lidarr の Web GUI にアクセスするには、`http://{サーバーの IP アドレス}:8686` にアクセスします

Lidarr が起動しなかった場合は、サービスのステータスを確認してください:

```shell
sudo journalctl --since today -u lidarr
```

---

### アンインストール

アンインストールおよびパージ:

> 警告: これにより、アプリケーションデータが破壊されます。 {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

アンインストールしてアプリケーションデータを保持する場合:

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```