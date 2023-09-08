---
title: Docker指南
description: Servarr Docker指南 - Docker概念、硬链接概念和Linux所有权和权限的概述
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# 目录

- [目录](#目录)
- [最佳Docker设置](#最佳docker设置)
- [Portainer](#portainer)
- [介绍](#介绍)
- [多个用户和共享组](#多个用户和共享组)
  - [权限](#权限)
  - [UMASK](#umask)
  - [PUID和PGID](#puid和pgid)
  - [示例](#示例)
- [单个用户和可选的共享组](#单个用户和可选的共享组)
- [/config的所有权和权限](#config的所有权和权限)
- [一致且良好规划的路径](#一致且良好规划的路径)
  - [示例](#示例)
    - [Torrents](#torrents)
    - [Usenet](#usenet)
    - [媒体服务器](#媒体服务器)
    - [Sonarr、Radarr和Lidarr](#sonarr-radarr和lidarr)
  - [问题](#问题)
- [使用以下方式运行容器](#使用以下方式运行容器)
  - [Docker Compose](#docker-compose)
    - [更新所有镜像和容器](#更新所有镜像和容器)
    - [更新单个镜像和容器](#更新单个镜像和容器)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [有用的命令](#有用的命令)
  - [列出正在运行的容器](#列出正在运行的容器)
  - [在容器内部运行Shell](#在容器内部运行shell)
  - [清理Docker](#清理docker)
  - [获取docker run命令](#获取docker-run命令)
  - [获取docker-compose](#获取docker-compose)
  - [网络故障排除](#网络故障排除)
  - [递归更改用户和组的所有权](#递归更改用户和组的所有权)
  - [递归更改权限为775/664](#递归更改权限为775664)
  - [查找用户的UID/GID](#查找用户的uidgid)
  - [检查硬链接的文件](#检查硬链接的文件)
- [有趣的Docker镜像](#有趣的docker镜像)
  - [一体化解决方案](#一体化解决方案)
- [自定义Docker网络和DNS](#自定义docker网络和dns)
- [常见问题](#常见问题)
  - [正确的“外部”路径，错误的“内部”路径](#正确的外部路径错误的内部路径)
  - [以root身份运行Docker容器或更改用户](#以root身份运行docker容器或更改用户)
  - [以umask 000运行Docker容器](#以umask-000运行docker容器)
- [获取帮助](#获取帮助)
  - [聊天支持（Discord）](#聊天支持discord)
  - [论坛支持（Reddit）](#论坛支持reddit)

# 最佳Docker设置

**TL;DR**: 每个守护程序使用一个[同名](https://www.lexico.com/en/definition/eponymous)用户和一个具有umask为`002`的共享组。在所有容器之间保持一致的路径定义，以保持文件夹结构。使用一个卷（因此下载文件夹和库文件夹位于同一个文件系统上）可以使Sonarr、Radarr、Lidarr和Readarr支持[硬链接](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-hardlinks)和[即时移动（原子移动）](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-instant-moves-atomic-moves)。最重要的是，忽略大部分Docker镜像的路径文档！

> 注意：与本指南相比，许多人发现[TRaSH的硬链接教程](https://trash-guides.info/hardlinks/)更有帮助且更易理解。本指南更多地是概念性的，而TRaSH的教程则会引导您完成整个过程。
{.is-info}

# Portainer

> **不建议使用Portainer设置Docker容器** {.is-danger}

- Portainer提供了一个漂亮的GUI来管理容器，但它只适用于这个目的。
- Portainer只应用于查看Docker容器日志/容器状态。
- 强烈建议使用Docker Compose，而不是使用Portainer。
- Portainer存在许多问题，例如：
  - 挂载源和目标的顺序不正确
  - 大小写敏感性不一致
  - 没有为容器间通信自动创建自定义网络
  - 不同架构上的Compose实现不一致
  - 在不设置特定标签的情况下，在更新时拉取每个标签
  - 在ARM平台上，某些功能被隐藏且无法正常工作

请参阅此[Docker指南](/docker-guide)和[TRaSH的Docker教程](https://trash-guides.info/hardlinks/)，了解如何设置Docker Compose。

# 介绍

本文不会向您展示有关最佳Docker设置的具体细节，但它描述了一个概述，您可以使用该概述使自己的设置达到最佳状态。这个想法是将每个Docker容器作为其自己的用户运行，使用共享组和一致的卷，以便每个容器都能看到相同的路径布局。这很容易说，但不容易理解和解释。

> 请记住，与本指南相比，许多人发现[TRaSH的硬链接教程](https://trash-guides.info/hardlinks/)更有帮助且更易理解。本指南更多地是概念性的，而TRaSH的教程则会引导您完成整个过程。
{.is-warning}

# 多个用户和共享组

## 权限

理想情况下，每个软件都以自己的用户身份运行，并且它们都是共享组的一部分，文件夹权限设置为`775`（`drwxrwxr-x`），文件设置为`664`（`-rw-rw-r--`），这是一个umask为`002`。这种设置的一个合理的替代方案是使用单个共享用户，它将使用`755`和`644`，这是一个umask为`022`。您还可以通过拒绝“其他”读取来进一步限制权限，这对于每个守护程序使用一个用户的umask为`007`，或者对于单个共享用户的umask为`077`。有关更深入的解释，请参阅Arch Linux维基百科文章[文件权限和属性](https://wiki.archlinux.org/index.php/File_permissions_and_attributes)和[UMASK](https://wiki.archlinux.org/index.php/Umask)。

## UMASK

许多Docker镜像接受`-e UMASK=002`作为环境变量，一些软件可以使用用户、组和umask（NZBGet）或文件夹/文件权限（Sonarr/Radarr）在容器内部进行配置。这将确保由*一个*创建的文件和文件夹可以被其他软件读取和写入。如果您正在使用现有的文件夹和文件，您还需要修复它们的当前所有权和权限，但是未来它们将是正确的，因为您正确设置了每个软件。

## PUID和PGID

许多Docker镜像还可以使用`-e PUID=123`和`-e PGID=321`，让您将内部使用的UID/GID更改为外部帐户的UID/GID。如果您窥视一下，您会发现用户名是`abc`、`nobody`或`hotio`之类的东西，但是因为它使用了您传递的UID/GID，在外部看起来就像预期的用户一样。如果您正在使用来自另一个系统的存储（通过NFS或CIFS），如果*该*系统也具有匹配的用户和组，那么这将使您的生活更轻松。也许让一个系统选择UID/GID，然后在另一个系统上重复使用它们，假设它们不冲突。

## 示例

您使用[hotio/sonarr](https://github.com/hotio/docker-sonarr)运行[Sonarr](https://github.com/Sonarr/Sonarr/releases)，您创建了一个具有UID为`123`的`sonarr`用户和一个具有GID为`321`的共享组`media`，`sonarr`用户是该共享组的成员。您配置Docker镜像以使用`-e PUID=123 -e PGID=321 -e UMASK=002`运行。Sonarr还允许您配置用户、组以及文件夹和文件权限。前面的设置应该会抵消这些设置，但是如果您愿意，您可以对其进行配置。umask为`002`会导致文件夹的权限为`775`（`drwxrwxr-x`），文件的权限为`664`（`-rw-rw-r--`），用户/组在*容器内部*有一个不同的名称，这有点棘手。通常它们是`abc`或`nobody`。

# 单个用户和可选的共享组

另一个流行且更容易的选择是使用单个共享用户，甚至可能是*您*的用户。这样做不太安全，也不符合最佳实践，但最终更容易理解和实施。这种情况下的UMASK为`022`，这将导致文件夹的权限为`755`（`drwxr-xr-x`），文件的权限为`644`（`-rw-r--r--`）。组不再真正重要，因此您可能只会使用以用户命名的组。这样做会使与*其他*用户共享变得更困难，因此即使在此设置中，您可能仍然希望使用UMASK为`002`。

# /config的所有权和权限

不要忘记您的`/config`卷也需要具有正确的所有权和权限，通常是守护程序的用户和该用户的组，例如`sonarr:sonarr`，以及umask为`022`或`077`，以便*只有*该用户可以访问。在单个用户设置中，这当然将是您选择的一个用户。

# 一致且良好规划的路径

> 与本指南相比，许多人发现[TRaSH的硬链接教程](https://trash-guides.info/hardlinks)更有帮助且更易理解。本指南更多地是概念性的，而TRaSH的教程则会引导您完成整个过程。
{.is-info}

最简单且最重要的细节是在所有容器中创建统一的路径定义。

如果您想知道为什么硬链接不起作用或为什么简单的移动所需的时间比预期的长得多，本节将对此进行解释。您在*内部*使用的路径很重要。由于Docker的卷是如何工作的，传递两个卷，例如常见建议的`/tv`、`/movies`和`/downloads`，即使它们是容器外部的单个文件系统，它们看起来也像是两个不同的文件系统。这意味着硬链接将无法工作，并且不会使用即时/原子移动，而是使用更慢且更需要IO的复制+删除。如果您有多个下载客户端，因为您同时使用种子和Usenet，那么只有一个`/downloads`路径意味着它们会混在一起。因为一个容器中的Radarr会询问其自己的容器中的NZBGet文件在哪里，所以在两者中使用相同的路径意味着它们将一切正常。如果没有这样做，您将需要使用远程路径映射来修复它。

因此，请选择*一个*路径布局，并在所有容器中使用它。建议使用`/data`，但也有其他常见名称，例如`/shared`、`/media`或`/dvr`。保持外部和内部的一致将使您的设置更简单：只需记住一个路径，或者如果集成Docker和本机软件。例如，Synology可能在外部使用`/Volume1/data`，而unRAID可能在外部使用`/mnt/user/data`，但在内部使用`/data`是可以的。

还要记住，您需要在运行*这些Docker容器内部*的软件中设置或重新配置路径。如果更改了下载客户端的路径，您需要编辑其设置以匹配，并且可能需要更新现有的种子。如果更改了库路径，您需要在Sonarr、Radarr、Lidarr、Plex等中更改这些设置。

## 示例

这里重要的是一般结构，而不是名称。您可以选择适合您的文件夹名称。还有其他排列方式。例如，您不太可能在Usenet和种子之间下载和运行相同版本的冲突，因此您*可以*将两者都放在`/data/downloads/{movies|books|music|tv}`文件夹中。下载甚至不需要排序到子文件夹中，因为电影、音乐和电视很少会发生冲突。

此示例`data`文件夹具有种子和Usenet的子文件夹，每个子文件夹都有用于电视、电影和音乐下载的子文件夹，以保持整洁。`media`文件夹具有良好命名的`tv`、`movies`、`books`和`music`子文件夹。这个`media`文件夹是您的库，您将将其传递给Plex、Kodi、Emby、Jellyfin等。

对于下面的示例，`data`等效于主机路径`/host/data`和Docker路径`/data`

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

每个Docker容器的路径可以根据需要具体到某个程度，同时仍然保持正确的结构：

### Torrents

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrents只需要访问种子文件，因此传递`-v /host/data/torrents:/data/torrents`。在种子软件的设置中，您需要重新配置路径，并且可以按照`/data/torrents/{tv|books|movies|music}`的方式进行排序。

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

Usenet只需要访问Usenet文件，因此传递`-v /host/data/usenet:/data/usenet`。在Usenet软件的设置中，您需要重新配置路径，并且可以按照`/data/usenet/{tv|movies|music}`的方式进行排序。

### 媒体服务器

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby只需要访问您的媒体库，因此传递`-v /host/data/media:/data/media`，其中可以有任意数量的子文件夹，例如`movies`、`kids movies`、`tv`、`documentary tv`和/或`music`。

### Sonarr、Radarr和Lidarr

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

Sonarr、Radarr和Lidarr使用`-v /host/data:/data`获取所有内容，因为*下载*文件夹和*媒体*文件夹看起来和*是*一个文件系统。硬链接将起作用，并且移动将是原子的，而不是复制+删除。

## 问题

有一些小问题没有遵循Docker镜像的建议路径。

最大的问题是，如果未指定`dockerfile`中定义的卷，它们将被创建，这意味着当您删除和重新创建容器时，它们将堆积起来。如果它们包含数据，它们可能会意外地占用空间，并且可能在不合适的位置。您可以在所有不想使用的卷上传入一个空文件夹，例如`/data/empty:/movies`和`/data/empty:/downloads`。甚至可以在里面放一个名为“DO NOT USE THIS FOLDER”的文件，以提醒自己。

另一个问题是，某些镜像预先配置为使用文档中的卷，因此您需要更改Docker容器内部的软件设置。幸运的是，由于配置在容器外部持久存在，这只是一个一次性的问题。您还可以选择像`/data`或`/media`这样的路径，这些路径已经为特定用途定义了一些镜像。这不应该是一个问题，但与前面的问题结合在一起可能会更加混乱。最终，这是为了获得工作中的硬链接和快速移动而值得的。一致性和简单性也是受欢迎的副作用。

如果您使用最新版本的已弃用的[RadarrSync](https://github.com/Sperryfreak01/RadarrSync)来同步两个Radarr实例，则*依赖于*将内部的*相同*路径映射到外部的不同路径，例如，一个实例的`/movies`将指向`/data/media/movies`，另一个实例将指向`/data/media/movies4k`。这将*破坏*您之前阅读的*所有内容*。没有好的解决方案，您可以使用旧版本，但效果不好，或者以一种丑陋并破坏硬链接的方式进行映射，或者根本不使用它。

# 使用运行容器

## Docker Compose

对于大多数用户来说，这是最好的选择，它允许您在一个文件中控制和配置多个容器及其相互依赖关系。一个很好的起点是Docker自己的[使用Docker Compose入门](https://docs.docker.com/compose/gettingstarted/)。您可以使用[composerize](https://composerize.com)或[ghcr.io/red5d/docker-autocompose](#get-docker-compose)将`docker run`命令转换为单个`docker-compose.yml`文件。

> 下面的示例*不是*一个完整的工作示例！容器只定义了PID、UID、UMASK和示例路径，以保持简单。
{.is-warning}

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

### 更新所有镜像和容器

```shell
    docker-compose pull
    docker-compose up -d
```

### 更新单个镜像和容器

```shell
    docker-compose pull NAME
    docker-compose up -d NAME
```

## docker run

> 与上面的Docker Compose示例一样，下面的`docker run`命令仅包含PUID、PGID、UMASK和卷，以作为明显的示例。
{.is-warning}

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

对于只使用systemd来维护几个Docker容器的情况，这是一个选择。它标准化了控制，并使本机和Docker服务的依赖关系更简单。下面的通用示例可以通过调整或添加各种值和选项来适应任何容器。

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

# 有用的命令

## 列出正在运行的容器

```shell
    docker ps
```

## 进入容器内部的Shell

进入容器通常会以root用户登录

```shell
    docker exec -it CONTAINER_NAME /bin/bash
```

进入后，您可以使用以下命令切换用户

```shell
    su - <username>
```

要作为特定用户执行，请添加`-u`作为参数，并传递用户名或ID

```shell
    docker exec -u USER -it CONTAINER_NAME /bin/bash
```

### 以特定用户的示例

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

有关更多信息，请参阅[docker exec](https://docs.docker.com/engine/reference/commandline/exec/)文档。

## 清理Docker

```shell
    docker system prune --all --volumes
```

> 删除未使用的容器、网络、卷、镜像和构建缓存。正如此命令给出的警告所说，这将删除所有先前提到的项目，这些项目不被正在运行的容器使用。在正确配置的环境中，这是可以的。但请注意，并谨慎操作第一次。有关更多详细信息，请参阅[Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/)文档。
{.is-warning}

## 获取docker run命令

从GUI管理器获取`docker run`命令可能很困难，但是这个Docker镜像使得从运行中的容器中获取它变得很容易（[来源](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)）。

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAME
```

## 获取docker-compose

> 此外，您可以查看[TRaSH的docker-compose指南](https://trash-guides.info/compose/)
{.is-info}

使用[docker-autocompose](https://github.com/Red5d/docker-autocompose)可以从运行的实例中获取`docker-compose.yml`，以便在已经使用`docker run`或`docker create`启动容器并希望切换到`docker-compose`样式时使用。它还非常适合与他人共享设置，因为不管您使用的是什么管理软件，都没有关系。最后一个参数（或多个参数）是您的容器名称，您可以同时传入尽可能多的容器名称。第一个容器名称是必需的，其他是可选的。您可以在`docker ps`的**NAMES**列中看到容器名称，它们通常由您设置，或者可能是基于镜像生成的，例如`binhex-qbittorrent`。它不是镜像名称，如`binhex/arch-qbittorrentvpn`。

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAME $ANOTHER_CONTAINER_NAME ... $ONE_MORE_CONTAINER_NAME
```

对于某些用户，可能是这样的：

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## 故障排除网络

大多数Docker镜像中没有太多有用的工具进行故障排除，但是您可以将一个[网络故障排除类型的镜像](https://hub.docker.com/r/nicolaka/netshoot)附加到现有容器中以帮助解决问题。

```shell
    docker run -it --rm --network container:CONTAINER_NAME nicolaka/netshoot
```

## 递归更改用户和组的所有权

```shell
    chown -R user:group /some/path/here
```

## 递归更改权限为775/664

```shell
    chmod -R a=,a+rX,u+w,g+w /some/path/here
              ^  ^    ^   ^ 添加组的写权限
              |  |    | 添加用户的写权限
              |  | 添加所有人的读权限和所有文件夹的执行权限（控制访问权限）
              | 将所有权限设置为`000`
```

## 查找用户的UID/GID

```shell
    id <username>
```

## 检查文件的硬链接

```shell
    ls -alhi
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # hardlinked
    42207936 -rw-r--r--  1 user group    0 Sep 11 11:55 # no hardlinks
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # original

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

# 有趣的Docker镜像

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio's](https://hotio.dev/) 文档和 Dockerfile 没有提供任何错误的路径建议。如果发现上游有更改，镜像将自动每小时更新2次。Hotio还会构建我们的Pull Requests（除了Sonarr），这对于测试可能很有用。
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) 用于搜索usenet和torrent tracker
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) 用于请求媒体
  - [overseerr](https://hotio.dev/containers/overseerr/) 用于请求媒体
  - [jackett](https://hotio.dev/containers/jackett) 用于搜索torrent tracker
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) 用于搜索usenet indexer
  - [bazarr](https://hotio.dev/containers/bazarr) 用于字幕
  - [pullio](https://hotio.dev/pullio/) 用于自动更新容器
  - [unpackerr](https://hotio.dev/containers/unpackerr) 用于在各种缺乏或完全缺失解压功能的torrent客户端中提取打包的torrent。
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) 的镜像提供了大量软件，并且维护得很好。但是，避免使用它们的“建议（可选）”路径。
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) 是另一个受欢迎的维护者
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### 一体化解决方案

- [这是一个GitHub仓库](https://github.com/Luctia/ezarr)，面向想要使用Docker构建Servarr堆栈的初学者。它基本上是一个准备就绪的文件集合，只需要运行两个命令即可将整个系统上线。它消除了主机设备上的用户管理和权限的麻烦，并提供了一些其他应用程序，如PleX。

# 自定义Docker网络和DNS

自定义Docker网络的一个有趣特性是它拥有自己的DNS服务器。如果为容器创建一个桥接网络，您可以在配置中使用它们的主机名。例如，如果您运行 `docker run --network=isolated --hostname=deluge binhex/arch-deluge` 和 `docker run --network=isolated --hostname=radarr binhex/arch-radarr`，然后您可以配置Radarr中的下载客户端指向 `deluge`，它将在自己的私有网络上工作并进行通信。这意味着，如果您想要更安全，您甚至可以停止转发该端口。如果将反向代理容器放在同一网络中，您甚至可以停止转发Web界面端口，使其更加安全。

# 常见问题

## 正确的*外部*路径，错误的*内部*路径

很多人阅读这篇文章后以为他们理解了，但他们最终会将外部路径设置为 `/data/usenet` 等正确的路径，但是他们忽略了将*内部*路径仍然设置为 `/downloads`。

- 正确的：
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- 错误的：
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## 以root身份运行Docker容器或更改用户

如果您发现自己以 `root:root` 身份运行容器，那么您肯定做错了什么。如果您没有传递UID和GID，您将使用镜像的默认值，而*那个*很可能与您系统上的合理用户不匹配。如果您更改了Docker容器运行的用户和组，您可能会在像 `/config` 文件夹上遇到权限问题，该文件夹可能包含使用第一次使用的UID/GID创建的文件和文件夹。

## 以umask 000运行Docker容器

如果您发现自己设置了UMASK为 `000`（文件夹为777，文件为666），那么您也做错了什么。这会使您的文件和文件夹对*所有人*都具有读写权限，这是不良的Linux卫生习惯。

# 获取帮助

## 聊天支持（Discord）

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## 论坛支持（Reddit）

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}