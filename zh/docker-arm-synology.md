---
title: 在 Synology ARM NAS 上安装 Docker
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# 介绍

Synology 仅在其基于 `x64` 的 NAS 上提供 Docker 软件包。使用此方法在 `aarch64` NAS 上安装 Docker 是完全不受支持/未经测试的，完全由您自己承担风险。这有可能会损坏您的 NAS。

> 再次强调，使用此方法在 `aarch64` NAS 上安装 Docker 是**完全不受支持/未经测试**的，完全由您自己承担风险。这有可能会损坏您的 NAS。{.is-danger}

# 概述

以下说明将：

1. 将 Docker 二进制文件放置在 `/usr/local/bin/` 中
1. 创建 Docker 配置文件 `/usr/local/etc/docker/docker.json`
1. 配置 Docker 将其数据保存到 `/volume1/docker/var`
1. 创建一个在启动时启动 Docker 的脚本 `/usr/local/etc/rc.d/docker.sh`
1. 创建一个 `docker` 用户组
1. 将一个 docker-compose 脚本放置在 `/usr/local/bin/` 中

# 安装

1. [通过 SSH 登录到 Synology 并提升为 `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

1. 执行以下命令：

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

如果一切顺利，您应该会看到以下消息：

```none
Done. Please add your user to the Docker group in the Synology GUI and reboot your NAS.
```

按照提示操作：

1. 使用 Synology GUI 将您的用户添加到新的 `docker` 用户组中
1. **重新启动**。

希望您现在可以使用 `docker` 和 `docker-compose` 命令，并且在以普通用户身份登录时可以正常工作。

# 注意事项

1. 似乎大多数 ARM Synology 不支持 seccomp，因此 Docker 容器对您的系统具有无限制的访问权限（比常规 Docker 更多）。
1. 再次提醒，由于 Synology 的限制，所有容器都需要使用 `--network=host`（或在 compose 中使用 `network_mode: host`），并且一切都可以直接从主机访问。没有端口映射。
1. 显然，您只能运行 aarch64 镜像，但大多数 hotio 和 linuxserver 镜像都提供 aarch64 版本。

# 设置 Docker GUI

如果您想要一个 GUI，可以使用以下示例 compose 运行 Portainer：

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

将其放置在名为 `docker-compose.yml` 的文件中，放置在一个空目录中。运行：

```shell
docker-compose up -d
```

访问 [`http://ip:9000`](http://ip:9000) 完成设置（其中 `ip` 是您 Synology 的 IP 地址）。

# 设置 Sonarr/Radarr/Lidarr/Readarr

有关设置 Sonarr/Radarr/Lidarr/Readarr 的指导，请参阅 [Docker 指南](/docker-guide)，并**记住上述注意事项 2**。