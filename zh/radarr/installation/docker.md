---
title: Radarr Docker 安装
description: Radarr 的 Docker 安装指南
published: true
date: 2023-08-12T16:02:10.602Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:47.674Z
---

# Docker

Radarr 团队没有提供官方的 Docker 镜像。然而，许多第三方已经创建并维护了自己的镜像。

以下说明提供了通用的指导，适用于任何 Radarr Docker 镜像。

Synology 用户可以参考 [TRaSH 的 Synology Docker 指南](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **不建议使用 Portainer 来设置 Docker 容器** {.is-danger}

- Portainer 提供了一个漂亮的图形界面来管理容器，但它只是一个有用的工具而已。
- Portainer 只应用于查看 Docker 容器的日志和状态。
- 强烈建议使用 Docker Compose，而不要使用 Portainer。
- Portainer 存在许多问题，例如：
  - 挂载点的源和目标顺序不正确
  - 大小写敏感性不一致
  - 没有为容器间通信自动创建自定义网络
  - 不同架构上的 Compose 实现不一致
  - 在更新时拉取所有标签，如果不设置特定标签
  - 功能被隐藏，某些功能在 ARM 平台上根本无法使用

请参考这个 [Docker 指南](/docker-guide) 和 [TRaSH 的 Docker 教程](https://trash-guides.info/hardlinks/)，了解如何设置 Docker Compose。

## 避免常见问题

### 卷和路径

Docker 卷存在两个常见问题：Radarr 和下载客户端容器之间的路径不同，以及路径阻止了快速移动和硬链接。

第一个问题是因为下载客户端会将下载的路径报告为 `/torrents/My.Movie.2018/`，但在 Radarr 容器中可能是 `/downloads/My.Movie.2018/`。第二个问题是性能问题，会导致种子的做种出现问题。这两个问题可以通过良好规划和一致的路径来解决。

大多数 Docker 镜像建议使用 `/movies` 和 `/downloads` 等路径。这会导致移动速度慢，并且不允许使用硬链接，因为它们在容器内被视为两个不同的文件系统。有些还建议下载客户端容器的路径与 Radarr 容器不同，例如 `/torrents`。

最佳解决方案是在容器内使用一个共享的公共卷，例如 `/data`。你的电影可以放在 `/data/Movies`，种子可以放在 `/data/downloads/torrents`，Usenet 下载可以放在 `/data/downloads/usenet`。

如果不遵循这个建议，你可能需要在 Radarr 的 Web UI（设置 › 下载客户端）中配置远程路径映射。

### 权限和所有权

文件的权限和所有权是 Radarr 用户最常见的问题之一，无论是在 Docker 内部还是在外部。大多数镜像都有环境变量，可以用来覆盖默认的用户、组和 umask，你应该在设置所有容器之前决定这些值。建议为所有相关容器使用一个共享的组，以便每个容器都可以使用共享组权限来读写挂载卷上的文件。
请记住，Radarr 需要对下载文件夹和最终文件夹具有读写权限。

> 更详细的解释，请参考 [最佳 Docker 设置和 Docker 指南](/docker-guide) 维基文章。
{.is-info}

## 安装 Radarr

要安装和使用这些 Docker 镜像，你需要在遵循它们的文档时记住上述内容。管理 Docker 镜像和容器有很多方法，因此它们的安装和维护取决于你选择的路径。

- [hotio/radarr](https://hotio.dev/containers/radarr/)
- [lscr.io/linuxserver/radarr](https://docs.linuxserver.io/images/docker-radarr)
{.links-list}