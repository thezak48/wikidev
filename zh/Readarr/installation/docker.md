---
title: Readarr Docker 安装
description: Readarr 的 Docker 安装指南
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Readarr 团队没有提供官方的 Docker 镜像。然而，许多第三方已经创建并维护了自己的镜像。

以下说明提供了通用的指导，适用于任何 Readarr Docker 镜像。

## Portainer

> **应避免使用 Portainer 来设置 Docker 容器** {.is-danger}

- Portainer 提供了一个漂亮的图形界面来管理容器，但它只适用于此。
- Portainer 只应用于查看 Docker 容器日志和容器状态。
- 强烈建议使用 Docker Compose，而不使用 Portainer。
- Portainer 存在许多问题，例如：
  - 挂载源和目标的顺序不正确
  - 大小写敏感性不一致
  - 没有为容器间通信自动创建自定义网络
  - 不同架构上的 Compose 实现不一致
  - 在不设置特定标签时，更新时会拉取所有标签
  - 某些功能被隐藏，而且在 ARM 平台上根本无法使用

请参阅此 [Docker 指南](/docker-guide) 和 [TRaSH 的 Docker 教程](https://trash-guides.info/hardlinks/)，了解如何设置 Docker Compose。

## 避免常见问题

### 卷和路径

Docker 卷存在两个常见问题：Readarr 和下载客户端容器之间路径不一致，以及路径导致快速移动和硬链接无法使用。

第一个问题是因为下载客户端会将下载的路径报告为 `/torrents/My.Movie.2018/`，但在 Readarr 容器中可能是 `/downloads/My.Movie.2018/`。第二个问题是性能问题，会导致种子的做种出现问题。这两个问题可以通过合理规划和保持一致的路径来解决。

大多数 Docker 镜像建议使用 `/books` 和 `/downloads` 等路径。这会导致移动速度变慢，并且无法使用硬链接，因为容器内被视为两个不同的文件系统。有些还建议下载客户端容器的路径与 Readarr 容器不同，例如 `/torrents`。

最佳解决方案是在容器内使用一个单一的共享卷，例如 `/data`。你的书籍可以放在 `/data/Books`，种子可以放在 `/data/downloads/torrents`，Usenet 下载可以放在 `/data/downloads/usenet`。

如果不遵循此建议，您可能需要在 Readarr 的 Web UI（设置 › 下载客户端）中配置远程路径映射。

### Calibre 集成

在创建根文件夹时，您可以选择是否使用 Calibre 集成。此选择只能在创建文件夹时进行，如果您选择不使用 Calibre，就无法后续添加。如果您目前使用 Calibre 管理图书库，应选择此选项。如果使用 Calibre，Calibre 将为您命名和组织图书文件。

如果您正在运行 Calibre，您必须首先启动 Calibre 内容服务器（首选项 / 网络共享），并设置用户和密码。这将需要重新启动 Calibre。

> 请注意，Calibre 内容服务器和 Calibre 不是 Calibre Web。Calibre Web 是一个与这两个程序无关的独立工具，Readarr 不需要也不使用它。
{.is-warning}

### 所有权和权限

文件的权限和所有权是 Readarr 用户最常见的问题之一，无论是在 Docker 内部还是在 Docker 外部。大多数镜像都有环境变量，可以用于覆盖默认的用户、组和 umask，您应该在设置所有容器之前决定这一点。建议为所有相关容器使用一个共享组，以便每个容器都可以使用共享组权限来读写挂载卷上的文件。
请记住，Readarr 需要对下载文件夹以及最终文件夹进行读写。

> 有关这些问题的更详细解释，请参阅 [最佳 Docker 设置和 Docker 指南](/docker-guide) 维基文章。
{.is-info}

## 安装 Readarr

要安装和使用这些 Docker 镜像，您需要在遵循其文档时牢记上述内容。管理 Docker 镜像和容器有许多方法，因此安装和维护取决于您选择的路径。

> 暂时，您需要使用 :nightly 或 :develop 标签与 Docker 镜像一起使用，因为没有主分支。[请参阅此 FAQ 条目了解分支的含义](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}