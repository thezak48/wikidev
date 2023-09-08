---
title: Sonarr FreeBSD インストール
description: Sonarr の FreeBSD インストールガイド
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Sonarr チームは FreeBSD 向けのビルドのみ提供しています。プラグインとポートは FreeBSD コミュニティによってメンテナンスおよび作成されています。

FreeBSD のインストール手順は FreeBSD コミュニティによってメンテナンスされており、GitHub アカウントを持つ誰でも必要に応じて wiki を更新できます。

[Freshports Sonarr リンク](https://www.freshports.org/net-p2p/sonarr/)

## TrueNAS GUI を使用した Jail のセットアップ

1. メイン画面から Jail を選択します。

1. ADD をクリックします。

1. Advanced Jail Creation をクリックします。

1. 名前（任意の名前で構いません）: Sonarr

1. Jail Type: Default (Clone Jail)

1. Release: 12.2-Release (またはそれ以降)

1. 好みに応じて基本プロパティを設定します。

1. 好みに応じて Jail プロパティを設定しますが、以下を追加します。

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` はトラブルシューティング（ping、traceroute など）に役立ちますが、必須ではありません。{.is-info}

1. 好みに応じてネットワークプロパティを設定します。

1. 好みに応じてカスタムプロパティを設定します。

1. Save をクリックします。

1. Jail が作成されると、自動的に開始されます。Sonarr がマウントされたメディアのストレージスペースを認識するためには、もう1つのプロパティを設定する必要があります。サーバーでルートシェルを開き、次のコマンドを入力します。

```shell
iocage stop <jailname>
iocage set enforce_statfs=1 <jailname>
iocage start <jailname>
```

## CLI を使用した Jail のセットアップ

iocage がインストールおよび設定されていることを前提とします（<https://iocage.readthedocs.io/en/latest/install.html>）
iocage ネットワークブリッジ（vnet）が設定されていることを前提とします（<https://iocage.readthedocs.io/en/latest/networking.html>）

ネットワーク上の空いている IPV4 アドレスで "10.0.0.100" を置き換えてください
好みの FreeBSD バージョンで "13.1-RELEASE" を置き換えてください
好みの jail 名で "sonarr" を置き換えてください
自動構成 IPV6 を使用しない場合は "accept_rtadv" を置き換えるか、ip6_addr を削除してください

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Sonarr Mono のインストール

Jails リストで `sonarr` の新しく作成された jail を見つけ、"Shell" をクリックします。

Sonarr をインストールするには

> \* pkg リポジトリが `/latest` からパッケージを取得するように設定されていることを確認してください
> \* `/usr/local/etc/pkg/repos/FreeBSD.conf` を確認してください
> \* それが存在しない場合は、`/etc/pkg/FreeBSD.conf` をその場所にコピーし、`quarterly` を `latest` に置き換えて開きます
{.is-warning}

```shell
pkg install sonarr
```

シェルをまだ閉じないで、もう少しやることがあります！

## Sonarr .NET のインストール

Jails リストで `sonarr` の新しく作成された jail を見つけ、"Shell" をクリックします。

Sonarr をインストールするには

> \* pkg リポジトリが `/latest` からパッケージを取得するように設定されていることを確認してください
> \* `/usr/local/etc/pkg/repos/FreeBSD.conf` を確認してください
> \* それが存在しない場合は、`/etc/pkg/FreeBSD.conf` をその場所にコピーし、`quarterly` を `latest` に置き換えて開きます
{.is-warning}

Sonarr をサポートするために次のライブラリをインストールします

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Sonarr ユーザーとグループを作成します（ユーザー/グループ 'sonarr' を使用したくない場合は、好みに応じて変更できます）

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

最新バージョンを <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> からダウンロードし、その権限を設定します

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

エディターで rc.subr スクリプトを作成して Sonarr をデーモンとして実行するためのものです（既にフォルダが存在する場合は 1 行目をスキップできるかもしれません）。以下の sonarr rc.subr の内容を使用します

```shell
mkdir -p /usr/local/etc/rc.d
vi /usr/local/etc/rc.d/sonarr
chmod +x /usr/local/etc/rc.d/sonarr
```

```shell
#!/bin/sh

# PROVIDE: sonarr
# REQUIRE: LOGIN
# KEYWORD: shutdown
#
# Add the following lines to /etc/rc.conf.local or /etc/rc.conf
# to enable this service:
#
# sonarr_enable:   Set to yes to enable the sonarr service.
#                       Default: no
# sonarr_user:     The user account used to run the sonarr daemon.
#                       This is optional, however do not specifically set this to an
#                       empty string as this will cause the daemon to run as root.
#                       Default: sonarr
# sonarr_group:    The group account used to run the sonarr daemon.
#                       This is optional, however do not specifically set this to an
#                       empty string as this will cause the daemon to run with group wheel.
#                       Default: sonarr
# sonarr_data_dir: Directory where sonarr configuration data is stored.
#                       Default: /var/db/sonarr
# sonarr_pid:      Name of the pid file.
#                       Default: sonarr.pid
# sonarr_pid_dir:  Path of the pid file.
#                       Default: /var/run/sonarr

. /etc/rc.subr
name=sonarr
rcvar=${name}_enable
load_rc_config ${name}

: ${sonarr_enable:="no"}
: ${sonarr_user:="sonarr"}
: ${sonarr_group:="sonarr"}
: ${sonarr_data_dir:="/var/db/sonarr"}
: ${sonarr_pid:="sonarr.pid"}
: ${sonarr_pid_dir:="/var/run/sonarr"}

pidfile="${sonarr_pid_dir}/${sonarr_pid}"
command="/usr/sbin/daemon"
command_args="-r -f -P ${pidfile} /usr/local/share/Sonarr/Sonarr --debug --data=${sonarr_data_dir} --nobrowser"

start_precmd=sonarr_start_precmd
sonarr_start_precmd()
{
 [ -d ${sonarr_pid_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_pid_dir}
 [ -d ${sonarr_data_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_data_dir}

 # .NET 6+ uses dual mode sockets to avoid the separate AF handling.
 # disable .NET use of V6 if no ipv6 is configured.
 # See https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

シェルをまだ閉じないで、もう少しやることがあります！

## Sonarr の設定

インストールが完了したので、もう少し手順が必要です。

### サービスの設定

サービスを有効にする時間ですが、注意が必要です。

アップデーターはデフォルトで無効になっています。`pkg check -s` や `pkg remove` などの Sonarr のビルトインアップデーターがファイルを置き換えると、これらが壊れる可能性があることに注意してください。

サービスを有効にするには:

```shell
sysrc sonarr_enable=TRUE
```

ユーザー/グループ `sonarr` を使用したくない場合は、サービスファイルに実行するユーザー/グループを指定する必要があります

```shell
sysrc sonarr_user="USER_YOU_WANT"
```

```shell
sysrc sonarr_group="GROUP_YOU_WANT"
```

`sonarr` はデフォルトで `/usr/local/sonarr` にデータ、設定、ログ、PID ファイルを保存します。サービスファイルはこれを作成し、所有権を取得しますが、それが存在しない場合に限ります。これらのファイルを別の場所に保存したい場合（例：スナップショットを容易にするために jail にマウントされたデータセット）、`sysrc` を使用して変更する必要があります

```shell
sysrc sonarr_data_dir="DIR_YOU_WANT"
```

注意: 既存の場所を使用している場合は、所有権を UID/GID `sonarr` に変更するか、書き込みアクセス権を持つ GID に `sonarr` を追加する必要があります。

ほぼ完了です。サービスを開始しましょう:

```shell
service sonarr start
```

すべてが計画どおりに進んだ場合、Sonarr は jail の IP（ポート 8989）で正常に動作しているはずです！

シェルを安全に閉じることができます

## トラブルシューティング

- サービスは実行されているようですが、UI が読み込まれないか、ページがタイムアウトしています
  - Jail で `allow_mlock` が有効になっていることを再確認してください
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Jail の VNET がオンになっていること、ip6=inherit または ip6=new であることを確認してください

> サービススクリプトは現在、VNET または ip6=inherit の必要性を取り除くために VNET および/または IP6 の不足を回避するはずです。{.is-info}

### BSD Mono SSL の問題

- SSL またはその他の証明書の問題（たとえば `unable to verify SSL certificate`）
  - [この TrueNAS フォーラムの投稿を参照して、mono の証明書を更新および同期する必要があります](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)