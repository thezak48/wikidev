我将把后面粘贴的Markdown内容翻译成简体中文。您必须严格遵循以下规则： - 不要更改Markdown标记结构。不要添加或删除链接。不要更改任何URL。 - 即使代码块中似乎有错误，也不要更改代码块的内容。 - 始终保留原始换行符。不要添加或删除空行。 - 不要触碰标题末尾的永久链接，如`{/*examples*/}`。 - 不要触碰类似HTML的标签，如`<Notes>`。

---
title: Lidarr 系统
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, system
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# 目录

- [目录](#目录)
- [状态](#状态)
  - [健康状况](#健康状况)
    - [系统警告](#系统警告)
      - [分支不是有效的发布分支](#分支不是有效的发布分支)
      - [更新到 .NET 版本](#更新到-net-版本)
        - [修复 Docker 安装](#修复-docker-安装)
        - [修复独立安装](#修复独立安装)
      - [当前安装的 mono 版本过旧且不受支持](#当前安装的-mono-版本过旧且不受支持)
      - [当前安装的 SQLite 版本不受支持](#当前安装的-sqlite-版本不受支持)
      - [有新的更新可用](#有新的更新可用)
      - [无法安装更新，因为启动文件夹不可写](#无法安装更新因为启动文件夹不可写)
      - [更新将不可行以防止在更新时删除 AppData](#更新将不可行以防止在更新时删除-appdata)
      - [分支是旧版本的](#分支是旧版本的)
      - [无法连接到 signalR](#无法连接到-signalr)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [无法解析配置的代理主机的 IP 地址](#无法解析配置的代理主机的-ip-地址)
      - [代理测试失败](#代理测试失败)
      - [系统时间超过 1 天](#系统时间超过-1-天)
      - [启用了 Mono 旧版 TLS](#启用了-mono-旧版-tls)
      - [Mono 和 x86 构建即将结束](#mono-和-x86-构建即将结束)
      - [FPcalc 需要更新](#fpcalc-需要更新)
    - [下载客户端](#下载客户端)
      - [没有可用的下载客户端](#没有可用的下载客户端)
      - [无法与下载客户端通信](#无法与下载客户端通信)
      - [下载客户端不可用](#下载客户端不可用)
      - [启用完成的下载处理](#启用完成的下载处理)
      - [Docker 错误的远程路径映射](#docker-错误的远程路径映射)
      - [下载到根文件夹](#下载到根文件夹)
      - [错误的下载客户端设置](#错误的下载客户端设置)
      - [错误的远程路径映射](#错误的远程路径映射)
      - [权限错误](#权限错误)
      - [远程文件在处理过程中被删除](#远程文件在处理过程中被删除)
      - [使用远程路径并导入失败](#使用远程路径并导入失败)
    - [完成/失败的下载处理](#完成失败的下载处理)
      - [已禁用完成的下载处理](#已禁用完成的下载处理)
    - [索引器](#索引器)
      - [没有启用自动搜索的可用索引器，Lidarr 将不会提供任何自动搜索结果](#没有启用自动搜索的可用索引器lidarr-将不会提供任何自动搜索结果)
      - [没有启用 RSS 同步的可用索引器，Lidarr 将不会自动抓取新发布内容](#没有启用-rss-同步的可用索引器lidarr-将不会自动抓取新发布内容)
      - [没有启用索引器](#没有启用索引器)
    - [已启用的索引器不支持搜索](#已启用的索引器不支持搜索)
      - [没有启用交互式搜索的可用索引器](#没有启用交互式搜索的可用索引器)
      - [由于故障索引器不可用](#由于故障索引器不可用)
      - [使用了 Jackett 的全部终端节点](#使用了-jackett-的全部终端节点)
        - [解决方案](#解决方案)
    - [艺术家文件夹](#艺术家文件夹)
      - [缺少根文件夹](#缺少根文件夹)
      - [由于故障列表不可用](#由于故障列表不可用)
  - [磁盘空间](#磁盘空间)
  - [关于](#关于)
  - [更多信息](#更多信息)
- [任务](#任务)
  - [计划任务](#计划任务)
  - [队列](#队列)
- [备份](#备份)
- [更新](#更新)
- [事件](#事件)
- [日志文件](#日志文件)

> 警告：本页面正在进行中，目前是基于 Readarr 的初稿
{.is-danger}

# 状态

## 健康状况

此页面包含健康检查错误的列表。Lidarr 定期执行这些健康检查，并在某些事件发生时执行。在此处列出警告和错误，以提供解决问题的建议。

### 系统警告

#### 分支不是有效的发布分支

您设置的分支不是有效的发布分支。您将无法接收更新。请更改为[当前的发布分支](/lidarr/faq#how-do-i-update-lidarr)之一。

#### 更新到 .NET 版本

{#update-to-net-core-version}

- Lidarr 的较新版本针对 .NET6 或更新版本进行了优化。在 1.0 版本发布后，我们将不再提供旧版的 mono 构建。您正在运行其中一个旧版构建，但您的平台支持 .NET。

##### 修复 Docker 安装

- 重新拉取容器

##### 修复独立安装

- 在进行下一步之前备份现有配置。
- 这仅适用于 Linux 主机。不要从 Microsoft 安装 .NET 运行时或 SDK。
- 要解决此问题，请下载适用于您的架构的正确版本，并替换现有的二进制文件（应用程序）。
- 简而言之，您需要删除现有的二进制文件（/opt/Lidarr 的内容或文件夹），并用刚刚下载的 .tar.gz 的内容替换它们。

> 不要只是在现有的二进制文件上提取下载内容。
> 您必须首先删除旧的二进制文件。
{.is-warning}

- 以下是一个由社区开发的脚本，用于删除您的 mono 安装并将其替换为 .NET 安装。欢迎提供贡献和更正。
- 如果需要，请更新变量以适应您的环境
- 假设您正在 `master` Lidarr 分支上运行，请更新变量
- 假设 Lidarr 以 `lidarr` 用户运行，请更新变量
- 假设 Lidarr 安装在 `/opt/Lidarr`，请更新变量

```bash
#!/bin/bash
## User Variables
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /User Variables
app="lidarr"
ARCH=$(dpkg --print-architecture)
# Stop \*arr
sudo systemctl stop $app
# get arch
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arch not supported"
    exit 1
    ;;
esac
echo "Downloading..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installation files downloaded and extracted"
echo "Moving existing installation"
sudo mv "$installdir/" "$installdir.old/"
echo "Installing..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App Installed"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### 当前安装的 mono 版本过旧且不受支持

- Lidarr 是用 .NET 编写的，需要 Mono 在非常旧的 ARM 处理器上运行。请注意，v1.0 之后不再支持 Mono 构建。
- Lidarr 的绝对最低要求是 Mono 5.20。
- Mono 的升级过程因平台而异。

#### 当前安装的 SQLite 版本不受支持

- Lidarr 将其数据存储在 SQLite 数据库中。您系统上安装的 SQLite3 库版本太旧。Lidarr 至少需要 3.9.0 版本。请注意，Lidarr 使用的是 `libSQLite3.so`，该文件可能包含在 SQLite3 升级包中，也可能不包含在其中。

#### 有新的更新可用

- 恭喜，开发人员发布了新的更新。这通常意味着令人兴奋的新功能和修复了一堆错误（对吗？）。显然，您没有启用自动更新，因此您需要弄清楚如何在您的平台上进行更新。在“系统 => 更新”页面上点击“安装”按钮可能是一个好的起点。

> 如果您当前的版本距离现在不到 14 天，将不会显示此警告
{.is-info}

#### 无法安装更新因为启动文件夹不可写

- 这意味着 Lidarr 将无法更新自身。您将需要手动更新 Lidarr，或者将 Lidarr 的启动目录（安装目录）的权限设置为允许 Lidarr 更新自身。

#### 更新将不可行以防止在更新时删除 AppData

- Lidarr 检测到您的操作系统的 AppData 文件夹位于包含 Lidarr 二进制文件的目录中。通常情况下，Windows 的 AppData 文件夹是 `C:\ProgramData`，Linux 的 AppData 文件夹是 `~/.config`。

- 请查看“系统 => 信息”以查看当前的 AppData 和启动目录。
- 这意味着 Lidarr 将无法更新自身，以免出现数据丢失的风险。
- 如果您使用的是 Linux，则可能需要更改运行 Lidarr 的用户的主目录，并将 `~/.config/Lidarr` 目录的当前内容复制到以保留数据库。
- 有关正确设置和最佳路径设置的更多信息，请参阅我们的[容器指南](/docker-guide)和 TRaSH 的[硬链接和即时移动（原子移动）](https://trash-guides.info/hardlinks/)指南。现在，这些指南非常强调硬链接和原子移动，但是容器和路径映射的一般概念是这些讨论的核心。
- 如果您在不同的操作系统之间或本机和容器之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的[Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)和[Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。
- 如果您在不同的操作系统之间或本机和容器之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的[Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)和[Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。
- 如果您在不同的操作系统之间或本机和容器之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的[Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)和[Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。
- 如果您在不同的操作系统之间或本机和容器之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的[Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)和[Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。

#### 分支是旧版本的

- 在“设置 => 通用”中设置的更新分支是 Lidarr 的旧版本，因此该实例将无法在“系统 => 更新”中看到正确的更新信息，并且可能无法在发布时接收到新的更新。

#### 无法连接到 signalR

- signalR 用于动态 UI 更新，因此如果您的浏览器无法连接到服务器上的 signalR，则在 UI 中将无法看到任何实时更新。

- 最常见的情况是使用反向代理或 Cloudflare
- Cloudflare 需要启用 WebSockets。

##### NGINX

- Nginx 需要在应用程序的位置块中添加以下内容：

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> 请确保不要包含 nginx 文档中建议的 `proxy_set_header Connection "Upgrade";`。这样不起作用。
> 请参阅 <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- 对于 Apache2 反向代理，您需要启用以下模块：proxy、proxy_http 和 proxy_wstunnel。然后，在虚拟主机配置中添加此 WebSocket 隧道指令：

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- 对于 Caddy（V1），请使用以下配置：
- 注意：您还需要在 Lidarr 配置中添加 WebSocket 指令

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### 无法解析配置的代理主机的 IP 地址

- 检查代理设置并确保其准确无误
- 确保代理正在运行且可访问

#### 代理测试失败

- 配置的代理未能成功测试，请查看提供的 HTTP 错误，或检查日志以获取更多详细信息。

#### 系统时间超过 1 天

- 系统时间超过 1 天。在时间被纠正之前，计划任务可能无法正确运行。
- 检查系统时间并确保它与权威时间服务器同步并准确。

#### 启用了 Mono 旧版 TLS

- 仍然启用了 Mono 4.x 的 TLS 解决方法，请考虑删除 `MONO_TLS_PROVIDER=legacy` 环境选项

#### Mono 和 x86 构建即将结束

- Mono 和 x86 构建将不再受到应用程序的支持。如果您收到此错误消息，则表示您正在运行应用程序的 mono 版本或 x86 版本。很遗憾，由于在开发支持这些旧版的困难不断增加，我们将停止对它们的支持，并因此不再发布它们的版本。因此，建议您升级到不需要 x86 或 mono 的受支持操作系统。您还可以尝试使用 Docker。

#### FPcalc 需要更新

{#fpcalc-upgrade}

- Lidarr 使用 chromaprint 音频指纹技术来识别曲目。这取决于一个名为 `fpcalc` 的外部二进制文件，该文件在 Lidarr v1 的 Windows、Linux 和 macOS 版本中已经分发，但在 FreeBSD 上必须单独提供。
- 确保 Lidarr 捆绑的 fpcalc 二进制文件具有可执行权限（755 权限）。该文件位于 Lidarr 的安装目录中（例如 `/opt/Lidarr/fpcalc`）。如果该文件没有可执行权限，请使用以下命令更正其权限，然后重新启动 Lidarr。
  - 请注意，对于修复，可能需要使用 `sudo` 或根据您的环境和设置更改 Lidarr 的二进制文件夹路径。

```bash
chmod +x /opt/Lidarr/fpcalc
```

> 下面的信息仅适用于旧版 v0.8.0。
{.is-info}

- 要在本机 Linux 实例上修复此问题，请使用软件包管理器安装适当的软件包，并确保 fpcalc 在您的 PATH 中（可以使用 which fpcalc 检查，并验证返回的 fpcalc 的正确位置）：

| 发行版  |       软件包        |
| :-----: | :----------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### 下载客户端

#### 没有可用的下载客户端

- Lidarr 需要正确配置和启用的下载客户端才能下载媒体。由于 Lidarr 支持不同的下载客户端，您应该确定哪个最符合您的要求。如果您已经安装了下载客户端，请配置 Lidarr 使用它并创建一个类别。请参阅“设置=>下载客户端”。

#### 无法与下载客户端通信

- Lidarr 无法与配置的下载客户端通信。请验证下载客户端是否正常运行，并仔细检查 URL。这也可能表示身份验证错误。
- 这通常是由于下载客户端配置不正确引起的。您可以检查以下内容：
  - 您的下载客户端的 IP 地址 - 如果它们都在同一台物理机上，通常是 `127.0.0.1`
  - 您的下载客户端使用的端口号 - 这些默认填写了默认端口号，但如果您更改了端口号，您需要在 Lidarr 中输入相同的端口号。
  - 如果您在本地网络上同时使用 Lidarr 实例和下载客户端，请确保未启用 SSL 加密（即在纯 HTTP 上使用）。有关详细信息，请参阅 SSL 常见问题解答。

#### 下载客户端不可用

- 您的一个或多个下载客户端未响应 Lidarr 的请求。因此，Lidarr 决定在正常的 1 分钟周期内暂时停止查询下载客户端，该周期通常用于跟踪活动下载并导入已完成的下载。但是，Lidarr 仍将继续尝试将下载发送到客户端，但很可能会失败。
- 您应该检查“系统=>日志”以查看失败的原因。
- 如果您不再使用此下载客户端，请在 Lidarr 中禁用它以防止出现错误。

#### 启用完成的下载处理

- Lidarr 需要启用“完成的下载处理”才能导入由下载客户端下载的文件。建议启用“完成的下载处理”（新用户默认启用）。

#### Docker 错误的远程路径映射

- 此错误通常与下载客户端或 Lidarr 中的错误 Docker 路径相关

- 错误（不一致）路径的示例：
  - 下载客户端：`/mnt/user/downloads:/downloads`
  - Lidarr：`/mnt/user/downloads:/data`
- 在此示例中，下载客户端将其下载放在 `/downloads` 中，并在完成后告诉 Lidarr 完成的书籍在 `/downloads` 中。然后，Lidarr 来到这里并说：“好的，很好，让我在 `/downloads` 中检查。”嗯，在 Lidarr 中，您没有分配 `/downloads` 路径，而是分配了 `/data` 路径，因此它会抛出此错误。
- 修复此问题的最简单方法是保持一致性 - 如果您在下载客户端中使用一种方案，请在整个 Lidarr 中使用相同的方案。

- Lidarr 团队非常喜欢简单地使用 /data。

  - 下载客户端：`/mnt/user/data/downloads:/data/downloads`
  - Lidarr：`/mnt/user/data:/data`

- 现在，在下载客户端中，您可以指定将下载放在 `/data/downloads/movies` 中，由于您在 Lidarr 中使用了 `/data`，因此当下载客户端告诉 Lidarr 完成时，Lidarr 将来到这里并说：“太好了，我有一个 `/data`，我还可以看到 `/data/downloads/movies`，世界上一切都很好。”
- 有许多很好的文章：我们的 Wiki [Docker 指南](/docker-guide) 和 TRaSH 的 [硬链接和即时移动（原子移动）](https://trash-guides.info/hardlinks/)。现在，这些指南非常强调硬链接和原子移动，但是容器和路径映射的一般概念是这些讨论的核心。
- 如果您在操作系统之间或本机和 Docker 之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的 [Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) 和 [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。
- 如果您在操作系统之间或本机和 Docker 之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的 [Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) 和 [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。
- 如果您在操作系统之间或本机和 Docker 之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的 [Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) 和 [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。
- 如果您在操作系统之间或本机和 Docker 之间进行切换，则需要进行远程路径映射。有关更多信息，请参阅 TRaSH 的 [Radarr 的远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) 和 [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)。

#### 下载到根文件夹

{#downloads-in-root-folder}

- 在应用程序中，根文件夹定义为配置的媒体库文件夹。这不是挂载的根文件夹。您的下载客户端将不完整或已完成的下载（或正在移动已完成的下载）放在您的根（库）文件夹中。
- 这经常会引起问题，包括数据丢失，不应该这样做。要修复此问题，请更改下载客户端，使其不要将下载放在根文件夹中。请注意，“放置”还包括如果您的下载客户端类别设置为根文件夹，或者如果 NZBGet/SABnzbd 启用了排序并且正在对根文件夹进行排序。
- 请注意，此检查会查看添加的所有已定义/配置的根文件夹，而不仅仅是当前正在使用的根文件夹。换句话说，您的下载客户端下载或将已完成的下载移动到的文件夹不应与您在 *arr 应用程序中配置为根/库/最终媒体目标文件夹的文件夹相同。
- 可在 [设置 => 媒体管理 => 根文件夹](/lidarr/settings/#root-folders) 中找到已配置的根文件夹（也称为库文件夹）。
- 一个示例是，如果您的下载文件位于 `\data\downloads` 中，那么您设置了一个根文件夹为 `\data\downloads`。
- 建议将根文件夹/库文件夹使用类似 `\data\media\` 的路径，将下载文件夹使用类似 `\data\downloads\` 的路径。
- 有关正确和最佳路径设置的更多信息，请查看我们的[容器指南](/docker-guide)和 TRaSH 的[硬链接和即时移动（原子移动）指南](https://trash-guides.info/hardlinks/)。请注意，这些指南非常强调硬链接和原子移动，但是正确和最佳路径设置的概念是这些讨论的核心。

> 您的下载文件夹（下载客户端放置下载的位置）和根/库文件夹必须是分开的。\*Arr 将从下载客户端的文件夹导入文件到库中。下载客户端不应将任何文件移动或下载到库中。
{.is-warning}

#### 错误的下载客户端设置

- 下载客户端下载文件的位置导致问题。请检查日志以获取更多信息。这可能是权限问题，也可能是在 Windows 和 Linux 之间或 Linux 和 Windows 之间进行远程路径映射。

#### 错误的远程路径映射

- 下载客户端下载文件的位置导致问题。请检查日志以获取更多信息。这可能是权限问题，也可能是在 Windows 和 Linux 之间或 Linux 和 Windows 之间进行远程路径映射。有关更多信息，请参阅 TRaSH 的[远程路径指南](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)。

#### 权限错误

- Lidarr（或运行 Lidarr 的用户 lidarr）无法访问下载客户端下载文件的位置。这通常是权限问题。

#### 远程文件在处理过程中被删除

- 在通过远程路径映射访问的文件在处理完成之前似乎已被删除。

#### 使用远程路径并导入失败

- 请检查日志以获取更多信息。请参阅我们的[故障排除指南](/lidarr/troubleshooting)。

### 完成/失败的下载处理

#### 已禁用完成的下载处理

- Lidarr 需要启用“完成的下载处理”才能导入由下载客户端下载的文件。建议启用“完成的下载处理”（新用户默认启用）。

### 索引器

#### 没有启用自动搜索的可用索引器，Lidarr 将不会提供任何自动搜索结果

- 简而言之，您没有将任何索引器设置为允许自动搜索
- 进入“设置 => 索引器”，选择一个您想要允许自动搜索的索引器，然后点击保存。

#### 没有启用 RSS 同步的可用索引器，Lidarr 将不会自动抓取新发布内容

- Lidarr 使用 RSS 订阅来获取新发布的内容。有关详细信息，请参阅此处。
- 要纠正此问题，请转到“设置 => 索引器”，选择您拥有的索引器并启用 RSS 同步。

#### 没有启用索引器

- Lidarr 需要索引器才能发现新发布的内容。请阅读 Wiki 上的说明以了解如何添加索引器。

### 已启用的索引器不支持搜索

- 您已启用的索引器都不支持搜索。这意味着 Lidarr 只能通过 RSS 订阅找到新发布的内容。但是，搜索电影（自动搜索或手动搜索）将永远不会返回任何结果。显然，唯一的解决方法是添加另一个索引器。

#### 没有启用交互式搜索的可用索引器

- 您已启用的索引器都不支持交互式搜索。这意味着该应用程序只能通过 RSS 订阅或自动搜索找到新发布的内容。

#### 由于故障索引器不可用

- Lidarr 尝试使用其中一个索引器时发生错误。为了限制重试次数，Lidarr 将在一段逐渐增加的时间内（最多 24 小时）不再使用该索引器。
- 如果 Lidarr 无法从索引器获取响应（可能是由 DNS、代理/VPN 连接、身份验证或索引器问题引起的），或者无法从索引器获取 nzb/torrent 文件，则会触发此机制。
- 请检查日志以确定是什么类型的错误导致了问题。
- 您可以通过禁用受影响的索引器来防止警告。
- 运行索引器上的测试以强制 Lidarr 重新检查索引器，请注意，健康检查警告不会立即消失。

#### 使用了 Jackett 的全部终端节点

- Jackett 的 `/all` 终端节点很方便，但这是它的唯一好处。其他一切都是潜在的问题，因此现在需要单独添加每个跟踪器。
- [即使 Jackett 的开发人员也表示应避免使用它，不应使用它。](https://github.com/Jackett/Jackett#aggregate-indexers)
- 使用 `/all` 终端节点没有任何优势，只有劣势：
  - 您无法控制索引器特定的设置（类别、搜索模式等）
  - 混合搜索模式（IMDB、查询等）可能导致低质量的结果
  - 无法使用索引器特定的类别（>= 100000）
  - 慢速索引器会减慢整体结果
  - 总结果限制为 1000
  - 如果其中一个跟踪器返回错误，\*Arr 将禁用它，现在您将无法获得任何结果。

##### 解决方案

- 在 Jackett 中手动添加每个跟踪器作为索引器
- 查看 [Prowlarr](/prowlarr)，它可以将索引器同步到 \*Arr，由 Lidarr/Radarr/Readarr 开发团队开发。
- 查看 [NZBHydra2](https://github.com/theotherp/nzbhydra2)，它可以将索引器同步到 \*Arr。但是不要使用其单个聚合终端节点，而是使用 `multi`。

### 艺术家文件夹

#### 缺少根文件夹

- 如果艺术家正在寻找根文件夹，但该根文件夹不再可用，则会识别此错误。
- 如果列表仍然指向根文件夹，但该根文件夹不再可用，则也可能出现此错误。
- 如果要删除此警告，请找到仍在使用旧根文件夹的专辑，并将其编辑为正确的根文件夹。

- 查找问题艺术家的最简单方法是：

  - 转到艺术家（库）选项卡
  - 使用旧根文件夹路径创建自定义筛选器
  - 在顶部工具栏上选择批量编辑，并从根路径下拉菜单中选择要将这些艺术家移动到的新根路径。
  - 接下来，您将收到一个弹出窗口，询问是否要将艺术家文件夹移动到“根路径”？这还将指出这将根据设置中的艺术家文件夹格式重命名艺术家文件夹。如果您不希望 Lidarr 移动文件，请选择“否”
  - 在“系统 => 任务”中运行“检查健康”任务

#### 由于故障列表不可用

- 通常，这意味着 Lidarr 无法通过 API 或登录到您选择的列表提供程序进行通信。如果问题持续存在，您最好联系他们以排除问题，因为他们的系统可能会不时过载。
- 请查看“系统 => 事件”，按警告（警告和错误）筛选以查看历史故障，或检查日