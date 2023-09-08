---
title: Prowlarr Linux インストール
description: Prowlarr の Linux インストールガイド
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

Debian / Ubuntu / Raspbian の初心者の方には、Apt リポジトリや Deb パッケージはありません。

簡単な方法を希望する場合は、コミュニティが提供・維持している `Easy Install` スクリプトを使用して、Debian (Raspbian / Raspberry Pi OS) / Ubuntu のベースインストールを行ってください。

**公式の手順に従って 'ハンズオン' インストールを行いたい場合は、以下の [Debian / Ubuntu ハンズオンインストール](#debian-ubuntu-hands-on-install) の手順に進んでください。**

[\*Arr コミュニティのインストールスクリプトを参照してください](/install-script)

### Debian / Ubuntu ハンズオンインストール

以下のコマンドを使用してバイナリをインストールする必要があります。

> 以下の手順では、Prowlarr をダウンロードして `/opt` にインストールします。
> Prowlarr はユーザー `prowlarr` とグループ `prowlarr` の下で実行されます。
> Prowlarr の設定ファイルは `/var/lib/prowlarr` に保存されます。
{.is-warning}

- 必要な前提パッケージをインストールしてください:

```shell
sudo apt install curl sqlite3
```

> 警告: 以下の前提条件を無視すると、インストールに失敗し、アプリケーションが機能しなくなります。 {.is-warning}

> **インストールの前提条件**
> 以下の手順は、次の前提条件に基づいています。必要に応じて、特定の要件に合わせて手順を変更してください。
> \* ユーザー `prowlarr` が作成されていること
> \* ディレクトリ `/var/lib/prowlarr` が作成され、ユーザー `prowlarr` が読み書きの権限を持っていること
{.is-danger}

> 以下を続行することで、上記の要件を読み、満たしていることを認識します。 {.is-warning}

- アーキテクチャに応じた正しいバイナリをダウンロードします。
  - アーキテクチャは `dpkg --print-architecture` コマンドで確認できます。
    - AMD64 の場合は `arch=x64` を使用します。
    - ARM、armf、および armh の場合は `arch=arm` を使用します。
    - ARM64 の場合は `arch=arm64` を使用します。

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- ファイルを展開します:

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- ファイルを `/opt/` に移動します:

```shell
sudo mv Prowlarr/ /opt
```

> これは、ユーザーが作成され、ユーザー `prowlarr` とグループ `prowlarr` で実行されることを前提としています。必要に応じてこれを変更してください。
{.is-danger}

- バイナリディレクトリの所有権を確認します。

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- Prowlarr が起動時に自動起動できるように systemd を設定します。

> 以下の systemd 作成スクリプトは、データディレクトリとして `/var/lib/prowlarr` を使用します。存在しない場合は、必要に応じて変更してください。デフォルトのデータディレクトリ `/home/$USER/.config/Prowlarr` の場合は、`-data` 引数を削除してください。なお、`$USER` は Prowlarr が実行されるユーザーであり、以下で定義されています。
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/prowlarr.service > /dev/null
[Unit]
Description=Prowlarr Daemon
After=syslog.target network.target
[Service]
User=prowlarr
Group=prowlarr
Type=simple

ExecStart=/opt/Prowlarr/Prowlarr -nobrowser -data=/var/lib/prowlarr/
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

- Prowlarr サービスを有効にします:

```shell
sudo systemctl enable --now -q prowlarr
```

- (オプション) tar ボールを削除します:

```shell
rm Prowlarr*.linux*.tar.gz
```

通常、Prowlarr の Web GUI にアクセスするには、`http://{サーバーの IP アドレス}:9696` にアクセスします。

Prowlarr が起動しなかった場合は、サービスのステータスを確認してください:

```shell
sudo journalctl --since today -u prowlarr
```

---

### アンインストール

アンインストールと削除を行うには:
> 警告: これによりアプリケーションデータが破棄されます。 {.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

アンインストールしてアプリケーションデータを保持するには:

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```