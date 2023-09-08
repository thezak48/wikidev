# ドッカーガイド

**TL;DR**: デーモンごとに1つのユーザーと共有グループを使用し、umaskが`002`の設定を行います。すべてのコンテナで一貫したパスの定義を維持します。ダウンロードフォルダとライブラリフォルダが同じファイルシステム上にあるため、Sonarr、Radarr、Lidarr、Readarrでハードリンクとインスタントムーブ（アトミックムーブ）が可能になります。そして何よりも、Dockerイメージのパスのドキュメントのほとんどを無視してください！

> 注意: このガイドよりも、多くの人々が[TRaSHのハードリンクチュートリアル](https://trash-guides.info/hardlinks/)を理解しやすく、役立つと感じています。このガイドは概念的な性質があり、TRaSHのチュートリアルは手順を説明しています。
{.is-info}

# Portainer

> **Dockerコンテナの設定にはPortainerを使用しないでください** {.is-danger}

- Portainerはコンテナを管理するための見栄えの良いGUIを提供しますが、それ以外の用途には役立ちません。
- Portainerは、Dockerコンテナのログやコンテナのステータスを表示するためにのみ使用するべきです。
- Docker Composeを使用し、Portainerを使用しないことを強くお勧めします。
- Portainerには次のような問題があります。
  - マウントのソースとターゲットの順序が正しくない
  - 大文字と小文字の区別が一貫していない
  - コンテナ間通信のためのカスタムネットワークが自動的に作成されない
  - 異なるアーキテクチャでの一貫したComposeの実装がない
  - 特定のタグを設定しない場合、更新時にすべてのタグを取得する
  - ARMプラットフォームでは、一部の機能が非表示になり、動作しないものもあります

Docker Composeの設定方法については、[Dockerガイド](/docker-guide)と[TRaSHのDockerチュートリアル](https://trash-guides.info/hardlinks/)を参照してください。

# はじめに

この記事では、最適なDockerのセットアップについて具体的な内容を示すものではありませんが、自分自身のセットアップを最適なものにするための概要を説明します。アイデアは、各Dockerコンテナを独自のユーザーとして実行し、共有グループと一貫したボリュームを使用して、すべてのコンテナが同じパスレイアウトを見ることです。これは簡単に言えることですが、理解と説明はそれほど簡単ではありません。

> TRaSHのハードリンクチュートリアルの方が、多くの人々にとってこのガイドよりも理解しやすく役立つと感じることを忘れないでください。このガイドは概念的な性質があり、TRaSHのチュートリアルは手順を説明しています。
{.is-warning}

# 複数のユーザーと共有グループ

## パーミッション

理想的には、各ソフトウェアは独自のユーザーとして実行され、すべてのユーザーが共有グループの一部であり、フォルダのパーミッションが`775`（`drwxrwxr-x`）に設定され、ファイルが`664`（`-rw-rw-r--`）に設定されている状態が望ましいです。これは、umaskが`002`であることを意味します。これに対する合理的な代替策は、単一の共有ユーザーであり、`755`と`644`を使用することです。これはumaskが`022`であることを意味します。さらに、"other"からの読み取りを拒否することで、パーミッションをさらに制限することもできます。これは、デーモンごとのユーザーの場合はumaskが`007`であり、単一の共有ユーザーの場合はumaskが`077`になります。詳細な説明については、Arch LinuxのWiki記事である[ファイルのパーミッションと属性](https://wiki.archlinux.org/index.php/File_permissions_and_attributes)と[UMASK](https://wiki.archlinux.org/index.php/Umask)を参照してください。

## UMASK

多くのDockerイメージは、環境変数として`-e UMASK=002`を受け入れ、一部のソフトウェアはコンテナ内でユーザー、グループ、およびumask（NZBGet）またはフォルダ/ファイルのパーミッション（Sonarr/Radarr）を設定できます。これにより、1つのソフトウェアによって作成されたファイルとフォルダを他のソフトウェアが読み書きできるようにすることができます。既存のフォルダとファイルを使用している場合は、現在の所有権とパーミッションも修正する必要がありますが、それ以降は正しい設定になります。

## PUIDとPGID

多くのDockerイメージは、`-e PUID=123`および`-e PGID=321`を受け入れ、内部で使用されるUID/GIDを外部のアカウントのUID/GIDに変更することができます。中を覗いてみると、ユーザー名は`abc`、`nobody`、`hotio`などのようになっているかもしれませんが、渡したUID/GIDを使用しているため、外部では期待されるユーザーのように見えます。NFSやCIFSを介して他のシステムからストレージを使用している場合は、そのシステムも一致するユーザーとグループを持っていると便利です。1つのシステムでUID/GIDを選択し、他のシステムでもそれらを再利用することができます（競合しない場合）。

## 例

[hotio/sonarr](https://github.com/hotio/docker-sonarr)を使用して[Sonarr](https://github.com/Sonarr/Sonarr/releases)を実行しているとします。`sonarr`ユーザーを作成し、uidが`123`で、`media`という共有グループを作成し、gidが`321`で、`sonarr`ユーザーがそのメンバーであるとします。Dockerイメージを`-e PUID=123 -e PGID=321 -e UMASK=002`で実行するように構成します。Sonarrはユーザー、グループ、フォルダ、ファイルのパーミッションも設定できますが、前述の設定はこれらを無効にするはずです。ただし、必要に応じてこれらを設定することもできます。UMASKが`002`の場合、フォルダのパーミッションは`775`（`drwxrwxr-x`）で、ファイルのパーミッションは`664`（`-rw-rw-r--`）になります。ユーザー/グループは少しトリッキーですが、コンテナの*内部*では異なる名前になります。通常、`abc`または`nobody`などです。

# 単一のユーザーとオプションの共有グループ

もう1つの人気のあるオプションは、単一の共有ユーザーです。おそらく、*あなた自身*のユーザーです。これは安全ではなく、ベストプラクティスに従いませんが、最終的には理解しやすく実装しやすいです。これに対するUMASKは`022`で、フォルダのパーミッションは`755`（`drwxr-xr-x`）で、ファイルのパーミッションは`644`（`-rw-r--r--`）になります。グループはもはや重要ではなく、おそらくユーザーの名前に基づいたグループを使用するでしょう。これにより、他のユーザーと共有するのが難しくなるため、このセットアップでもUMASKが`002`が必要になる場合があります。

# /configの所有権とパーミッション

自分の`/config`ボリュームも正しい所有権とパーミッションを持つ必要があることを忘れないでください。通常、デーモンのユーザーとそのユーザーのグループ（例：`sonarr:sonarr`）とumaskが`022`または`077`であるように設定します。単一のユーザーセットアップの場合、これはもちろん選択した1つのユーザーになります。

# 一貫性のある計画されたパス

> 多くの人々が[TRaSHのハードリンクチュートリアル](https://trash-guides.info/hardlinks)の方が理解しやすく役立つと感じることを忘れないでください。このガイドは概念的な性質があり、TRaSHのチュートリアルは手順を説明しています。
{.is-info}

最も重要な詳細は、すべてのコンテナで統一されたパスの定義を作成することです。

ハードリンクが機能しない理由や、シンプルな移動が予想よりもはるかに長い時間がかかる理由について疑問に思っている場合、このセクションで説明します。*内部*で使用するパスが重要です。Dockerのボリュームの動作方法により、`/tv`、`/movies`、`/downloads`などといった一般的に提案される2つのボリュームを渡すと、それらは1つのファイルシステムのように見えますが、コンテナの外部では1つのファイルシステムです。これは、ハードリンクが機能せず、インスタント/アトミックな移動の代わりに、より遅く、よりIO集中的なコピー+削除が使用されることを意味します。トレントとUsenetの両方を使用しているために複数のダウンロードクライアントがある場合、単一の`/downloads`パスを使用すると、それらが混在することになります。1つのコンテナのRadarrが、自分自身のコンテナ内のNZBGetにファイルの場所を尋ねるため、両方で同じパスを使用すると、すべてがうまく動作します。そうでない場合は、リモートパスマップで修正する必要があります。

したがって、*1つの*パスレイアウトを選択し、それをすべてのコンテナで使用することが重要です。`/data`を使用することをお勧めしますが、`/shared`、`/media`、または`/dvr`などの一般的な名前もあります。これにより、外部と内部の両方で同じものが保持され、セットアップが簡単になります。覚えるべきパスは1つだけです。または、Dockerとネイティブのソフトウェアを統合する場合。たとえば、Synologyでは外部では`/Volume1/data`、unRAIDでは外部では`/mnt/user/data`を使用するかもしれませんが、内部では`/data`を使用します。

また、これらのDockerコンテナ内で実行されているソフトウェアのパスを設定または再構成する必要があることも覚えておくことが重要です。ダウンロードクライアントのパスを変更する場合は、その設定を編集し、おそらく既存のトレントを更新する必要があります。ライブラリパスを変更する場合は、Sonarr、Radarr、Lidarr、Plexなどの設定を変更する必要があります。

## 例

ここで重要なのは、一般的な構造であり、名前ではありません。自分に意味のあるフォルダ名を選ぶことができます。他の配置方法もあります。たとえば、usenetとtorrentの間で同一のリリースの競合が起こることはまれですので、`/data/downloads/{movies|books|music|tv}`フォルダに両方を配置することができます。ダウンロードはサブフォルダに分類する必要もありません。なぜなら、映画、音楽、テレビはほとんど競合しないからです。

この例の`data`フォルダには、整理された状態を保つために、torrentsとusenetのサブフォルダがあります。`media`フォルダには、きれいに名前が付けられた`tv`、`movies`、`books`、`music`のサブフォルダがあります。この`media`フォルダはライブラリであり、Plex、Kodi、Emby、Jellyfinなどに渡すものです。

以下の例では、`data`はホストパス`/host/data`とDockerパス`/data`と同等です。

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    |  ├── books
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  ├── books
    │  └── tv
    └── media
        ├── movies
        ├── music
        ├── books
        └── tv
```

各Dockerコンテナのパスは、必要に応じて具体的になる場合がありますが、正しい構造を維持します。

### Torrents

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrentsはトレントファイルにのみアクセスする必要があるため、`-v /host/data/torrents:/data/torrents`を渡します。トレントソフトウェアの設定を再構成する必要があり、`/data/torrents/{tv|books|movies|music}`のようにサブフォルダに分類することができます。

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

UsenetはUsenetファイルにのみアクセスする必要があるため、`-v /host/data/usenet:/data/usenet`を渡します。Usenetソフトウェアの設定を再構成する必要があり、`/data/usenet/{tv|movies|music}`のようにサブフォルダに分類することができます。

### メディアサーバー

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Embyはメディアライブラリにのみアクセスする必要があるため、`-v /host/data/media:/data/media`を渡します。`movies`、`kids movies`、`tv`、`documentary tv`および/または`music`などのサブフォルダを持つことができます。

### Sonarr、Radarr、Lidarr

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  └── tv
    └── media
        ├── movies
        ├── music
        └── tv
```

Sonarr、Radarr、Lidarrは、ハードリンクが機能し、移動がアトミックに行われるため、`-v /host/data:/data`を使用してすべてを取得します。

## 問題点

Dockerイメージの提案されたパスに従わない場合、いくつかの細かい問題が発生します。

最も大きな問題は、`dockerfile`で定義されたボリュームが指定されていない場合に作成されることです。これは、コンテナを削除して再作成するたびにボリュームが積み重なることを意味します。それらにデータが含まれている場合、予期せずにスペースを消費し、適切でない場所にデータが保存される可能性があります。[クリーンアップコマンド](#prune-docker)を使用して、不要なボリュームを削除できます。また、使用しないすべてのボリュームに対して空のフォルダを渡すことで、この問題を緩和することもできます。たとえば、`/data/empty:/movies`や`/data/empty:/downloads`のようなパスを指定することができます。また、自分自身に思い出させるために、内部に`DO NOT USE THIS FOLDER`という名前のファイルを配置することもできます。

もう1つの問題は、一部のイメージがドキュメント化されたボリュームを使用するように事前に設定されているため、Dockerコンテナ内のソフトウェアの設定を変更する必要があることです。幸いなことに、設定はコンテナの外部に永続化されるため、これは一度だけの問題です。また、一部のイメージが特定の用途に対してすでに定義している`/data`や`/media`などのパスを選択することもできます。これは問題にはなりませんが、前述の問題と組み合わせると少し混乱するかもしれません。最終的には、ハードリンクと高速な移動のために価値があります。一貫性とシンプルさも歓迎される副作用です。

もし、2つのRadarrインスタンスを同期するために廃止された最新バージョンの[RadarrSync](https://github.com/Sperryfreak01/RadarrSync)を使用する場合、内部で*同じ*パスを異なるパスにマッピングする必要があります。たとえば、一方のインスタンスの`/movies`は`/data/media/movies`を指し、もう一方のインスタンスは`/data/media/movies4k`を指します。これは、上記で読んだすべての内容を壊します。良い解決策はありません。古いバージョンを使用するか、見た目が悪くハードリンクを壊すようなマッピング方法を使用するか、それとも使用しないかのいずれかです。

# Docker Composeを使用してコンテナを実行する

## Docker Compose

これはほとんどのユーザーにとって最適なオプションであり、1つのファイルで多くのコンテナとその相互依存関係を制御および設定できます。Docker自体の[Get started with Docker Compose](https://docs.docker.com/compose/gettingstarted/)が良い出発点です。[composerize](https://composerize.com)または[ghcr.io/red5d/docker-autocompose](#get-docker-compose)を使用して、`docker run`コマンドを単一の`docker-compose.yml`ファイルに変換できます。

> 以下は*完全な動作する例ではありません*！コンテナにはPID、UID、UMASK、および例のパスのみが定義されています。{.is-warning}

```yml
    # sonarr
    Sonarr:
        image: cr.hotio.dev/hotio/sonarr
        volumes:
            - /path/to/config/sonarr:/config
            - /host/data:/data
        environment:
            - PUID=111
            - PGID=321
            - UMASK=002

    # deluge
    Deluge:
        image: binhex/arch-delugevpn
        volumes:
            - /path/to/config/deluge:/config
            - /host/data/torrents:/data/torrents
        environment:
            - PUID=222
            - PGID=321
            - UMASK=002

    # SABnzbd
    SABnzbd:
        image: cr.hotio.dev/hotio/sabnzbd
        volumes:
            - /path/to/config/sabnzbd:/config
            - /host/data/usenet:/data/usenet
        environment:
            - PUID=333
            - PGID=321
            - UMASK=002

    # plex
    Plex:
        image: cr.hotio.dev/hotio/plex
        volumes:
            - /path/to/config/plex:/config
            - /host/data/media:/data/media

        environment:
            - PUID=444
            - PGID=321
            - UMASK=002
```

### すべてのイメージとコンテナを更新する

```shell
    docker-compose pull
    docker-compose up -d
```

### 個別のイメージとコンテナを更新する

```shell
    docker-compose pull NAME
    docker-compose up -d NAME
```

## docker run

> 上記のDocker Composeの例と同様に、以下の`docker run`コマンドは、明らかな例として、PUID、PGID、UMASK、およびボリュームのみが削除されています。{.is-warning}

```shell
    # sonarr
    docker run -v /path/to/config/sonarr:/config \
               -v /host/data:/data \
               -e PUID=111 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sonarr

    # deluge
    docker run -v /path/to/config/deluge:/config \
               -v /host/data/torrents:/data/torrents \
               -e PUID=222 -e PGID=321 -e UMASK=002 \
               binhex/arch-delugevpn

    # SABnzbd
    docker run -v /path/to/config/sabnzbd:/config \
               -v /host/data/usenet:/data/usenet \
               -e PUID=333 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sabnzbd

    # plex
    docker run -v /path/to/config/plex:/config \
               -v /host/data/media:/data/media \
               -e PUID=444 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/plex
```

## Systemd

数個のDockerコンテナを管理するために、systemdを使用することもできます。これにより、ネイティブおよびDockerサービスの制御が標準化され、依存関係が単純化されます。以下の一般的な例は、さまざまな値とオプションを調整または追加することで、任意のコンテナに適応できます。

```shell
    # /etc/systemd/system/thing.service
    [Unit]
    Description=Thing
    Requires=docker.service
    After=network.target docker.service

    [Service]
    ExecStart=/usr/bin/docker run --rm \
                              --name=thing \
                              -v /path/to/config/thing:/config \
                              -v /host/data:/data
                              -e PUID=111 -e PGID=321 -e UMASK=002 \
                              nobody/thing

    ExecStop=/usr/bin/docker stop -t 30 thing

    [Install]
    WantedBy=default.target
```

# 便利なコマンド

## 実行中のコンテナの一覧を表示する

```shell
    docker ps
```

## コンテナ内のシェルに入る

コンテナにエグゼクトすると、通常はrootとしてログインします。

```shell
    docker exec -it CONTAINER_NAME /bin/bash
```

内部に入ったら、次のコマンドでユーザーを切り替えることができます。

```shell
    su - <username>
```

特定のユーザーとしてエグゼクトするには、引数として`-u`を追加し、ユーザー名またはIDを渡します。

```shell
    docker exec -u USER -it CONTAINER_NAME /bin/bash
```

### 特定のユーザーとしての例

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

詳細については、[docker exec](https://docs.docker.com/engine/reference/commandline/exec/)のドキュメントを参照してください。

## Dockerのクリーンアップ

```shell
    docker system prune --all --volumes
```

> 未使用のコンテナ、ネットワーク、ボリューム、イメージ、およびビルドキャッシュを削除します。このコマンドが警告するように、実行中のコンテナで使用されていないすべてのアイテムに対して、以前に言及したアイテムがすべて削除されます。正しく構成された環境では、これは問題ありません。ただし、最初の実行時に注意して進めてください。詳細については、[Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/)のドキュメントを参照してください。{.is-warning}

## docker runコマンドの取得

GUIマネージャから`docker run`コマンドを取得するのは難しい場合がありますが、このDockerイメージを使用すると、実行中のコンテナから簡単に取得できます（[ソース](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)）。

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAME
```

## docker-composeの取得

> さらに、[TRaSH's Guide for docker-compose](https://trash-guides.info/compose/)も参照してください。{.is-info}

実行中のインスタンスから`docker-compose.yml`を取得することは、[docker-autocompose](https://github.com/Red5d/docker-autocompose)を使用することで可能です。すでに`docker run`または`docker create`でコンテナを起動していて、`docker-compose`スタイルに変更したい場合に使用できます。また、これは他の人と設定を共有するためにも非常に便利です。使用している管理ソフトウェアに関係なく、設定を共有できます。最後の引数はコンテナ名であり、必要な数だけ同時に渡すことができます。最初のコンテナ名は必須で、それ以降はオプションです。コンテナ名は`docker ps`の**NAMES**列に表示されます。通常は自分で設定するか、イメージに基づいて生成される場合があります（例：`binhex-qbittorrent`）。イメージ名ではありません（例：`binhex/arch-qbittorrentvpn`）。

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAME $ANOTHER_CONTAINER_NAME ... $ONE_MORE_CONTAINER_NAME
```

一部のユーザーにとっては、次のようになるかもしれません。

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## ネットワーキングのトラブルシューティング

ほとんどのDockerイメージにはトラブルシューティングに役立つツールがほとんど含まれていませんが、既存のコンテナにネットワークトラブルシューティングタイプのイメージをアタッチすることで、トラブルシューティングを補助することができます。

```shell
    docker run -it --rm --network container:CONTAINER_NAME nicolaka/netshoot
```

## ユーザーとグループの再帰的なchown

```shell
    chown -R user:group /some/path/here
```

## 再帰的なchmod 775/664

```shell
    chmod -R a=,a+rX,u+w,g+w /some/path/here
              ^  ^    ^   ^ グループに書き込みを追加
              |  |    | ユーザーに書き込みを追加
              |  | 全員に読み取りを追加し、すべてのフォルダに実行を追加（アクセスを制御）
              | すべてを`000`に設定
```

## ユーザーのUID/GIDを検索する

```shell
    id <username>
```

## ハードリンクのファイルを調べる

```shell
    ls -alhi
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # ハードリンクあり
    42207936 -rw-r--r--  1 user group    0 Sep 11 11:55 # ハードリンクなし
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # オリジナル

    stat original
      File: original
      Size: 0               Blocks: 0          IO Block: 4096   regular empty file
    Device: 803h/2051d      Inode: 42207934    Links: 2
    Access: (0644/-rw-r--r--)  Uid: ( 1000/ user)   Gid: ( 1001/ group)
    Access: 2020-09-11 11:55:43.803327144 -0500
    Modify: 2020-09-11 11:55:43.803327144 -0500
    Change: 2020-09-11 11:55:49.706660476 -0500
     Birth: 2020-09-11 11:55:43.803327144 -0500
```

# おもしろいDockerイメージ

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio’s](https://hotio.dev/) ドキュメントとDockerfileは、パスの提案が不適切ではありません。イメージは、アップストリームの変更が見つかった場合に1時間に2回自動的に更新されます。HotioはPull Request（Sonarrを除く）もビルドしてくれるため、テストに役立つかもしれません。
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) - Usenetおよびトレントトラッカーの検索に使用します。
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) - メディアのリクエストに使用します。
  - [overseerr](https://hotio.dev/containers/overseerr/) - メディアのリクエストに使用します。
  - [jackett](https://hotio.dev/containers/jackett) - トレントトラッカーの検索に使用します。
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) - Usenetインデクサーの検索に使用します。
  - [bazarr](https://hotio.dev/containers/bazarr) - 字幕に使用します。
  - [pullio](https://hotio.dev/pullio/) - コンテナの自動更新に使用します。
  - [unpackerr](https://hotio.dev/containers/unpackerr) - 様々なトレントクライアントで不足しているまたは完全に欠落しているパックされたトレントの抽出に便利です。
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) イメージは、*たくさん*のソフトウェアに対応しており、メンテナンスも行き届いています。ただし、'suggested (optional)'パスは避けてください。
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) はもう一人の人気のあるメンテナーです。
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### オールインワンソリューション

- [これはGitHubリポジトリ](https://github.com/Luctia/ezarr)で、ServarrスタックのDockerを使用したい初心者を対象にしています。基本的には使用準備が整ったファイルのコレクションであり、オンラインにするために実行するだけのものです。ホストデバイス上のユーザー管理とパーミッションの手間を省き、PleXなどの他のアプリケーションも備えています。

# カスタムDockerネットワークとDNS

[カスタムDockerネットワーク](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks)の興味深い機能の1つは、独自のDNSサーバーを持っていることです。コンテナ用のブリッジネットワークを作成すると、設定でホスト名を使用できます。たとえば、`docker run --network=isolated --hostname=deluge binhex/arch-deluge`と`docker run --network=isolated --hostname=radarr binhex/arch-radarr`を実行すると、Radarrのダウンロードクライアントを`deluge`に設定することができ、それ自体のプライベートネットワークで動作および通信することができます。つまり、さらにセキュリティを強化するために、そのポートの転送を*停止*することもできます。リバースプロキシコンテナを同じネットワークに配置すると、Webインターフェースポートの転送も停止し、さらにセキュリティを強化することができます。

# よくある問題

## 正しい*外部*パス、間違った*内部*パス

多くの人がこれを読んで理解したつもりになりますが、外部パスを`/data/usenet`などのように正しく設定しても、まだポイントを見逃して内部パスを`/downloads`のままに設定してしまいます。

- 良い例:
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- 悪い例:
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Dockerコンテナをrootとして実行するか、ユーザーを変更する

コンテナを`root:root`として実行している場合、何か間違ったことをしています。UIDとGIDを渡していない場合、イメージのデフォルトが使用され、それはおそらくシステム上の合理的なユーザーと一致しないでしょう。また、Dockerコンテナが実行されるユーザーとグループを変更している場合、最初に使用したUID/GIDで作成された`/config`フォルダなどのフォルダにはおそらくパーミッションの問題が発生します。

## umask 000でDockerコンテナを実行する

UMASKを`000`（フォルダに対しては777、ファイルに対しては666）に設定している場合、それも間違っています。これにより、ファイルとフォルダが*誰にでも*読み書き可能になり、Linuxのハイジーンが悪くなります。

# ヘルプの取得

## チャットサポート（Discord）

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## フォーラムサポート（Reddit）

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}