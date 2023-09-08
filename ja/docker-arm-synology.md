---
title: Synology ARM NAS に Docker をインストールする
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# はじめに

Synology は `x64` ベースの NAS にのみ Docker パッケージを提供しています。`aarch64` ベースの NAS に Docker をインストールする方法は、完全に非サポート/未テストであり、完全に自己責任です。NAS を破壊する可能性があります。

> もう一度言いますが、`aarch64` ベースの NAS に Docker をインストールする方法は、**完全に非サポート/未テスト**であり、完全に自己責任です。NAS を破壊する可能性があります。{.is-danger}

# 概要

以下の手順により、次のことが実行されます。

1. Docker バイナリを `/usr/local/bin/` に配置します。
1. Docker の設定ファイル `/usr/local/etc/docker/docker.json` を作成します。
1. Docker のデータを `/volume1/docker/var` に保存するように設定します。
1. `/usr/local/etc/rc.d/docker.sh` に Docker を起動するスクリプトを作成します。
1. `docker` グループを作成します。
1. `/usr/local/bin/` に docker-compose スクリプトを配置します。

# インストール

1. [Synology に SSH でログインし、`root` に昇格します](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)。

1. 次のコマンドを実行します。

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

すべてがうまくいけば、次のメッセージが表示されます。

```none
Done. Please add your user to the Docker group in the Synology GUI and reboot your NAS.
```

以下の手順に従ってください。

1. Synology GUI を使用して、新しい `docker` グループにユーザーを追加します。
1. **再起動します。**

おそらく、通常のユーザーとしてログインしたときに動作するはずの `docker` および `docker-compose` コマンドが使用できるようになっているはずです。

# 注意事項

1. ほとんどの ARM Synology では seccomp がサポートされていないようですので、Docker コンテナはシステムへの制約なしにアクセスできます（通常の Docker よりもさらに制約があります）。
1. Synology の制約により、すべてのコンテナは `--network=host`（または compose では `network_mode: host`）を使用する必要があり、すべてがホストから直接アクセス可能になります。ポートマップはありません。
1. 明らかに aarch64 イメージのみ実行できますが、ほとんどの hotio および linuxserver イメージには aarch64 バージョンが提供されています。

# Docker GUI の設定

GUI を使用する場合は、次の例のように Portainer を実行できます。

```yml
    version: '2'

    services:
      portainer:
        image: portainer/portainer
        restart: unless-stopped
        network_mode: host
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
          - portainer_data:/data

    volumes:
      portainer_data:
```

これを `docker-compose.yml` という名前のファイルに保存し、それ以外の空のディレクトリに配置します。次のコマンドを実行します。

```shell
docker-compose up -d
```

[`http://ip:9000`](http://ip:9000) にアクセスしてセットアップを完了します（`ip` は Synology の IP アドレスです）。

# Sonarr/Radarr/Lidarr/Readarr の設定

Sonarr/Radarr/Lidarr/Readarr の設定については、[Docker ガイド](/docker-guide)を参照してください。**上記の注意事項 2 を忘れないでください。**