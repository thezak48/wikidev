---
title: Prowlarr FreeBSD 安装
description: Prowlarr 的 FreeBSD 安装指南
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Prowlarr 团队仅为 FreeBSD 提供构建。插件和端口由 FreeBSD 社区维护和创建。

FreeBSD 安装指南也由 FreeBSD 社区维护，任何拥有 GitHub 账户的人都可以根据需要更新 wiki。

[Freshports Prowlarr 链接](https://www.freshports.org/net-p2p/prowlarr/)

## 使用 TrueNAS GUI 设置 Jail

1. 从主屏幕选择 Jails

1. 点击 ADD

1. 点击 Advanced Jail Creation

1. 名称（任何名称都可以）：Prowlarr

1. Jail 类型：默认（克隆 Jail）

1. 发行版：12.2-Release（或更新版本）

1. 根据您的喜好配置基本属性

1. 根据您的喜好配置 Jail 属性，但添加

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` 对于故障排除（例如 ping、traceroute）很有帮助，但不是必需的。{.is-info}

1. 根据您的喜好配置网络属性

1. 根据您的喜好配置自定义属性

1. 点击 Save

## Prowlarr 安装

回到 jails 列表，找到您新创建的 `prowlarr` jail，然后点击 "Shell"

要安装 Prowlarr

> \* 确保您的 pkg 仓库已配置为从 `/latest` 而不是 `/quarterly` 获取软件包
> \* 检查 `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* 如果不存在，请将 `/etc/pkg/FreeBSD.conf` 复制到该位置，打开它，并将 `quarterly` 替换为 `latest`{.is-warning}

```shell
pkg install prowlarr
```

现在还不能关闭 shell，我们还有一些事情要做！

## 配置 Prowlarr

现在我们已经安装了它，还需要进行一些额外的步骤。

### 服务设置

是时候启用服务了，但在启用之前，有一个注意事项：

更新程序默认处于禁用状态。`pkg-message` 提供了如何启用更新程序的说明，但请记住：当内置更新程序替换文件时，这可能会破坏 prowlarr 的 `pkg check -s` 和 `pkg remove` 等功能。

要启用服务：

```shell
sysrc prowlarr_enable=TRUE
```

如果您不想使用用户/组 `prowlarr`，则需要告诉服务文件应在哪个用户/组下运行

```shell
sysrc prowlarr_user="USER_YOU_WANT"
```

```shell
sysrc prowlarr_group="GROUP_YOU_WANT"
```

`prowlarr` 默认将其数据、配置、日志和 PID 文件存储在 `/usr/local/prowlarr` 中。服务文件将在此处创建并拥有该目录，但仅当该目录不存在时。如果您想将这些文件存储在其他位置（例如，挂载到 jail 中以便更轻松地进行快照的数据集），则需要使用 `sysrc` 进行更改

```shell
sysrc prowlarr_data_dir="DIR_YOU_WANT"
```

提醒：如果您使用的是现有位置，则需要手动将所有权更改为 `prowlarr` 使用的 UID/GID，并/或将 `prowlarr` 添加到具有写访问权限的 GID。

几乎完成了，让我们启动服务：

```shell
service prowlarr start
```

如果一切按计划进行，prowlarr 应该在 jail 的 IP 上（端口 9696）上运行！

现在可以安全地关闭 shell 了

## 故障排除

- 服务似乎正在运行，但 UI 未加载或页面超时
  - 请再次检查 jail 中是否启用了 `allow_mlock`
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - 确保您的 jail 已启用 `VNET`，ip6=inherit 或 ip6=new

> 服务脚本现在应该解决了缺少 VNET 和/或 IP6 的问题，从而消除了对 VNET 或 ip6=inherit 的要求。{.is-info}