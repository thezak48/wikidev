---
title: Sonarr FreeBSD 安装
description: Sonarr 的 FreeBSD 安装指南
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Sonarr 团队仅为 FreeBSD 提供构建版本。插件和端口由 FreeBSD 社区维护和创建。

FreeBSD 安装说明也由 FreeBSD 社区维护，任何拥有 GitHub 账户的人都可以根据需要更新 Wiki。

[Freshports Sonarr 链接](https://www.freshports.org/net-p2p/sonarr/)

## 使用 TrueNAS GUI 设置 Jail

1. 从主屏幕选择 Jails

1. 点击 ADD

1. 点击 Advanced Jail Creation

1. 名称（任何名称都可以）：Sonarr

1. Jail 类型：默认（克隆 Jail）

1. 发行版：12.2-Release（或更新版本）

1. 根据您的喜好配置基本属性

1. 根据您的喜好配置 Jail 属性，但添加

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` 有助于故障排除（例如 ping、traceroute），但不是必需的。{.is-info}

1. 根据您的喜好配置网络属性

1. 根据您的喜好配置自定义属性

1. 点击 Save

1. 创建 Jail 后，它将自动启动。为了使 Sonarr 能够看到已挂载的媒体位置的存储空间，还需要设置一个属性。在服务器上打开 root shell 并输入以下命令：

```shell
iocage stop <jailname>
iocage set enforce_statfs=1 <jailname>
iocage start <jailname>
```

## 使用 CLI 设置 Jail

假设已安装并配置了 iocage（<https://iocage.readthedocs.io/en/latest/install.html>）
假设已配置了 iocage 网络桥（vnet）（<https://iocage.readthedocs.io/en/latest/networking.html>）

将 "10.0.0.100" 替换为您网络上的可用 IPV4 地址
将 "13.1-RELEASE" 替换为首选的 FreeBSD 版本
将 "sonarr" 替换为您首选的 jail 名称
如果不想自动配置 IPV6，请将 "accept_rtadv" 替换为 "remove ip6_addr" 或删除 ip6_addr

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Sonarr Mono 安装

返回到 jails 列表，找到您新创建的 `sonarr` jail，然后点击 "Shell"

要安装 Sonarr

> * 确保您的 pkg 仓库已配置为从 `/latest` 获取软件包，而不是 `/quarterly`
> * 检查 `/usr/local/etc/pkg/repos/FreeBSD.conf`
> * 如果不存在，请将 `/etc/pkg/FreeBSD.conf` 复制到该位置，打开它，并将 `quarterly` 替换为 `latest`{.is-warning}

```shell
pkg install sonarr
```

现在不要关闭 shell，我们还有一些事情要做！

## Sonarr .NET 安装

返回到 jails 列表，找到您新创建的 `sonarr` jail，然后点击 "Shell"

要安装 Sonarr

> * 确保您的 pkg 仓库已配置为从 `/latest` 获取软件包，而不是 `/quarterly`
> * 检查 `/usr/local/etc/pkg/repos/FreeBSD.conf`
> * 如果不存在，请将 `/etc/pkg/FreeBSD.conf` 复制到该位置，打开它，并将 `quarterly` 替换为 `latest`{.is-warning}

安装以下库以支持 Sonarr

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

创建 Sonarr 用户和组（如果不想使用用户/组 'sonarr'，可以根据喜好进行更改）

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

从 <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> 下载最新版本并设置其权限

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

在您选择的编辑器中创建一个 rc.subr 脚本，以将 Sonarr 作为守护进程运行（如果文件夹已存在，则可能可以跳过第 1 行），并使用下面的 sonarr rc.subr 的内容

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

现在不要关闭 shell，我们还有一些事情要做！

## 配置 Sonarr

现在我们已经安装好了，还需要进行一些额外的步骤。

### 服务设置

是时候启用服务了，但在此之前，请注意：

更新程序默认已禁用。`pkg-message` 中提供了启用更新程序的说明，但请注意：当内置更新程序替换文件时，这可能会破坏 Sonarr 的 `pkg check -s` 和 `pkg remove` 等功能。

要启用服务：

```shell
sysrc sonarr_enable=TRUE
```

如果您不想使用用户/组 `sonarr`，则需要告诉服务文件应在哪个用户/组下运行

```shell
sysrc sonarr_user="您想要的用户"
```

```shell
sysrc sonarr_group="您想要的组"
```

`sonarr` 默认将其数据、配置、日志和 PID 文件存储在 `/usr/local/sonarr` 中。服务文件将在**仅当该位置不存在时**创建此文件夹并拥有它。如果您想将这些文件存储在其他位置（例如，一个挂载到 jail 中以便更容易进行快照的数据集），则需要使用 `sysrc` 进行更改

```shell
sysrc sonarr_data_dir="您想要的目录"
```

提醒：如果您使用的是现有位置，则需要手动将所有权更改为 UID/GID `sonarr` 使用的值，并/或将 `sonarr` 添加到具有写访问权限的 GID。

几乎完成了，让我们启动服务：

```shell
service sonarr start
```

如果一切按计划进行，Sonarr 应该在 jail 的 IP 上（端口 8989）正常运行！

现在可以安全地关闭 shell

## 故障排除

- 服务似乎正在运行，但 UI 未加载或页面超时
  - 请再次检查 jail 中是否启用了 `allow_mlock`
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - 确保您的 jail 上已启用 `VNET`，ip6=inherit 或 ip6=new

> 服务脚本现在应该解决了缺少 VNET 和/或 IP6 的问题，因此不再需要 VNET 或 ip6=inherit 的要求。{.is-info}

### BSD Mono SSL 问题

- SSL 或其他证书问题（例如 `unable to verify SSL certificate`）
  - 请参阅[此 TrueNAS 论坛帖子，您需要更新和同步 mono 的证书](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)