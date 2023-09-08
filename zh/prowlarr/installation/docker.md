---
title: Prowlarr Docker 安装
description: Prowlarr 的 Docker 安装指南
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Prowlarr 团队没有提供官方的 Docker 镜像。然而，许多第三方已经创建并维护了自己的镜像。

> 有关 Docker 的更详细解释和建议的实践，请参阅 [The Best Docker Setup and Docker Guide](/docker-guide) wiki 文章。
{.is-info}

Synology 用户可以查看 [TRaSH 的 Synology Docker 指南](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)

## Portainer

> **应避免使用 Portainer 来设置 Docker 容器** {.is-danger}

- Portainer 提供了一个漂亮的图形界面来管理容器，但它只有这个用途。
- Portainer 只应用于查看 Docker 容器日志和容器状态。
- 强烈建议使用 Docker Compose，而不是使用 Portainer。
- Portainer 存在许多问题，例如：
  - 挂载的源和目标的顺序不正确
  - 大小写敏感性不一致
  - 没有为容器间通信自动创建自定义网络
  - 不同架构上的不一致的 compose 实现
  - 在更新时拉取所有标签，如果不设置特定标签
  - 功能被隐藏，某些功能在 ARM 平台上根本无法使用

请参阅此 [Docker 指南](/docker-guide) 和 [TRaSH 的 Docker 教程](https://trash-guides.info/hardlinks/)，了解如何设置 Docker Compose。

## 安装 Prowlarr

要安装和使用这些 Docker 镜像，您需要在遵循其文档时牢记上述内容。管理 Docker 镜像和容器有很多方法，因此安装和维护它们将取决于您选择的路径。

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}