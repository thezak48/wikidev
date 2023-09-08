---
title: Prowlarr 常见问题解答
description: Prowlarr 常见问题解答
published: true
date: 2023-08-28T19:29:30.585Z
tags: prowlarr, faq
editor: markdown
dateCreated: 2021-11-03T03:01:18.079Z
---

# 目录

- [目录](#目录)
  - [强制身份验证](#强制身份验证)
  - [如何重置统计数据？](#如何重置统计数据)
  - [分类不可用或缺失](#分类不可用或缺失)
  - [我可以添加任何（通用的）Torznab或Newznab索引器吗？](#我可以添加任何通用的torznab或newznab索引器吗)
  - [我可以添加任何（通用的）Torrent RSS Feed 吗？](#我可以添加任何通用的torrent-rss-feed-吗)
  - [我可以使用 flaresolverr 索引器吗？](#我可以使用-flaresolverr-索引器吗)
  - [如何添加一个已经关闭或无法正常工作的索引器？](#如何添加一个已经关闭或无法正常工作的索引器)
  - [Prowlarr 无法与 Sonarr 同步](#prowlarr-无法与-sonarr-同步)
  - [Prowlarr 无法将 X 索引器同步到应用程序](#prowlarr-无法将-x-索引器同步到应用程序)
  - [哪些 \*Arr 索引器设置会用于应用程序的完全同步？](#哪些-arr-索引器设置会用于应用程序的完全同步)
  - [如何更新 Prowlarr？](#如何更新-prowlarr)
    - [我可以在 Docker 容器内更新 Prowlarr 吗？](#我可以在-docker-容器内更新-prowlarr-吗)
    - [安装更新版本](#安装更新版本)
      - [本地安装](#本地安装)
      - [Docker 安装](#docker-安装)
  - [我可以从 `nightly` 切换回 `develop` 吗？](#我可以从-nightly-切换回-develop-吗)
  - [我可以在不同分支之间切换吗？](#我可以在不同分支之间切换吗)
  - [帮助，我的 Mac 提示无法打开 Prowlarr，因为开发者无法验证](#帮助我的-mac-提示无法打开-prowlarr因为开发者无法验证)
  - [帮助，我的 Mac 提示 Prowlarr.app 已损坏，无法打开](#帮助我的-mac-提示-prowlarrapp-已损坏无法打开)
  - [如何请求 Prowlarr 的新功能？](#如何请求-prowlarr-的新功能)
  - [我遇到一个错误：数据库磁盘映像损坏](#我遇到一个错误数据库磁盘映像损坏)
  - [我在 Mac 上使用 Prowlarr，突然停止工作了。发生了什么？](#我在-mac-上使用-prowlarr突然停止工作了发生了什么)
  - [如何从 Windows 服务切换到托盘应用程序？](#如何从-windows-服务切换到托盘应用程序)
  - [如何备份/恢复 Prowlarr？](#如何备份恢复-prowlarr)
    - [备份 Prowlarr](#备份-prowlarr)
      - [使用内置备份](#使用内置备份)
      - [直接使用文件系统](#直接使用文件系统)
    - [从备份中恢复](#从备份中恢复)
      - [使用 zip 备份](#使用-zip-备份)
      - [使用文件系统备份](#使用文件系统备份)
      - [在 Synology NAS 上恢复文件系统](#在-synology-nas-上恢复文件系统)
  - [仅在 Windows 上以 localhost 加载 WebUI](#仅在-windows-上以-localhost-加载-webui)
  - [查找 Cookies](#查找-cookies)
  - [uTorrent 不再工作](#utorrent-不再工作)
  - [我收到一个弹窗，说 config.xml 损坏了，现在怎么办？](#我收到一个弹窗说-configxml-损坏了现在怎么办)
  - [无效的证书和其他 HTTPS 或 SSL 问题](#无效的证书和其他-https-或-ssl-问题)
  - [帮助，我被锁定了](#帮助我被锁定了)
  - [奇怪的用户界面问题](#奇怪的用户界面问题)
  - [VPN、Prowlarr 和 \*ARRs](#vpn-prowlarr-和-arrs)
  - [如何停止浏览器在启动时自动打开？](#如何停止浏览器在启动时自动打开)
  - [我可以一次性添加所有索引器吗？](#我可以一次性添加所有索引器吗)
  
## 强制身份验证

如果 Prowlarr 允许从本地网络外部访问其用户界面，则应启用某种形式的身份验证方法以访问用户界面。这也是 Tracker 和 Indexer 越来越多要求的。

从 Prowlarr v1 开始，身份验证是强制的。

### 身份验证方法

- `Basic`（浏览器弹窗）- 当访问 Prowlarr 时，此选项将显示一个小弹窗，允许您输入用户名和密码。
- `Forms`（登录页面）- 此选项将显示一个类似其他网站的登录界面，允许您登录到 Prowlarr。
- `External` - 仅可通过配置文件进行配置
  - 如果您使用**外部身份验证**，例如 Authelia、Authetik、NGINX 基本身份验证等，您可以通过关闭应用程序、在[配置文件](/prowlarr/appdata-directory)中设置 `<AuthenticationMethod>External</AuthenticationMethod>`，然后重新启动应用程序来避免双重身份验证。**请注意，配置文件中的多个 `AuthenticationMethod` 条目不受支持，只会使用顶部的值**

### 要求进行身份验证

- 如果您不将应用程序暴露在外部，或者不希望在本地（例如局域网）访问时需要进行身份验证，请在“设置”=>“常规安全性”=>“身份验证要求”中更改为 `禁用本地地址`
  - 配置文件中的等效设置是 `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`
  
## 如何重置统计数据？

- 要重置统计数据并清除历史记录，请按照以下步骤操作：

1. 进入“历史记录”=>“选项”
1. 将“历史记录清理”设置为 `1`。这将仅保留昨天的历史记录和统计数据
1. 导航到“系统”=>“任务”
1. 运行“清理历史记录”任务
1. 运行“Housekeeping”任务
1. 返回到“历史记录”=>“选项”
1. 将“历史记录清理”设置为您希望保留的历史记录和统计数据的保留期

## 分类不可用或缺失

- 请注意，自定义/非标准的索引器特定分类将映射到标准分类，因此搜索标准分类将包含所有自定义分类。请查看您特定索引器的分类映射定义以获取详细信息。

## 我可以添加任何（通用的）Torrent RSS Feed 吗？

可以。使用 "TorrentRSS"。

以下属性是必需的：

- guid
- title
- infohash
- enclosure 或 link

以下属性是可选的，但建议提供：

- size
- pubDate

## 我可以添加任何（通用的）Torznab 或 Newznab 索引器吗？

- 可以。
- 转到 `Indexers` => `Add Indexer`（<kb>+</kb>）=> `Generic Torznab` 或 `Generic Newznab`

## 我可以使用 flaresolverr 索引器吗？

- 可以。

1. 通过在 [设置 => 索引器](/prowlarr/settings#indexer-proxies) 中将其添加为代理来配置 flaresolverr 实例。
1. 为创建的 flaresovlerr 代理添加一个标签。
1. 将相同的标签添加到您的 [索引器](/prowlarr/indexers) 中。

> 标签必须匹配，并且必须检测到 Cloudflare 才能使用 Flaresolverr。如果未使用标签，则 Flaresolverr 代理将被禁用。
{.is-warning}

> [请参阅 TRaSH 的“如何设置 Flaresolverr”指南](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/)以获取更多详细信息
{.is-info}

## 如何添加一个已经关闭或无法正常工作的索引器？

- 按照标准步骤添加索引器，但注意以下更改。
- 取消选中（禁用）“启用”框
- 点击“保存”
- 再次点击“保存”以触发强制保存
- 编辑索引器（扳手图标）
- 选中（启用）“启用”框
- 点击“保存”
- 再次点击“保存”以触发强制保存

## Prowlarr 无法与 Sonarr 同步

- Prowlarr 仅支持 Sonarr v3+
- Prowlarr 不支持 Sonarr v2（以前称为 nzbdrone），也不受 Prowlarr 或一般支持，自 2021 年 3 月起已停止维护

## Prowlarr 无法将 X 索引器同步到应用程序

- Prowlarr 仅在应用程序启用“添加和删除”或“完全同步”时进行同步。
- 仅在应用程序和索引器具有匹配的标签或没有标签的情况下，索引器才会同步到应用程序。
- 索引器的同步基于其声称支持的功能/分类。
  - 如果索引器仅支持 TV 分类，则不会将其同步到 Lidarr、Radarr 和 Readarr。
- 仅当 Sonarr 可以选择“支持的”分类时，给定的索引器才会同步到 Sonarr。
- 如果索引器的空查询不返回包含任何配置的应用程序分类中的任何发布结果，则不会尝试同步索引器。
- 具体错误将是来自 \*Arr 的 HTTP 400，指示“查询成功，但从索引器未返回配置的分类中的任何结果。这可能是索引器或索引器分类设置的问题。”
  - 可能是该索引器无法与该 \*Arr 一起使用。这在尝试将公共 Tracker 或 Usenet 索引器与 Readarr 和 Lidarr 一起使用时很常见。
  - 调整 Prowlarr 中 \*Arr 应用程序的高级设置中同步的分类。
    - 请注意，某些 Tracker - 主要是“糟糕”的公共 Tracker - 需要选择并同步“8000 - 其他”分类。这通常在 Prowlarr 中的 Tracker 详细信息中说明，但并非总是如此。
  - 稍后再试
  - 如果问题仍然存在，可能是数据库损坏。检查日志以查看是否有“数据库磁盘映像损坏”或“创建主数据库时出错”的实例。有关可能的解决方案，请参阅[此标题](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)。

## 哪些 \*Arr 索引器设置会用于应用程序的完全同步？

- 应用程序/Prowlarr：索引器名称
- 应用程序/Prowlarr：启用/禁用 RSS
- 应用程序/Prowlarr：启用/禁用自动搜索
- 应用程序/Prowlarr：启用/禁用交互式搜索
- 应用程序/Prowlarr：索引器优先级
- 应用程序/Prowlarr：API 密钥
- 应用程序/Prowlarr：URL
- 应用程序/Prowlarr：基本 URL
- 应用程序/Prowlarr：端口
- 应用程序/Prowlarr：分类
- 应用程序/Prowlarr：种子比率和种子时间
- 应用程序/Prowlarr：最小种子数
- 应用程序/Prowlarr：*Prowlarr 中的其他任何可配置/可控制的设置*
- Prowlarr：实现（例如 YML 或 C#）

启用完全同步后，如果上述任何设置在 \*Arr 应用程序和 Prowlarr 之间发生更改，则索引器将在 \*Arr 中进行同步和更新。

## 如何更新 Prowlarr？

- 转到“设置”，然后进入“常规”选项卡，并显示高级设置（使用保存按钮旁边的切换）。

1. 在“更新”部分，将分支名称更改为 `master`、`develop` 或 `nightly`
1. 保存

*这不会立即安装该分支的组件，而是在下次更新时进行安装。*

- `master` - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    （默认/稳定）：已由开发者和用户在 develop 和 nightly 分支上进行测试，不知道是否存在任何重大问题。在 GitHub 上，这是 `master` 分支。

- `develop` - ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  （测试版）：这是测试边缘。在经过夜间测试以确保没有立即问题后发布。新功能和错误修复将在此之后首先在 beta 中发布。它可以被视为半稳定，但仍然是 `beta`。

> 在 GitHub 上，这是 `develop` 分支的特定时间点的快照。
{.is-warning}

- `nightly` - ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  （Alpha/不稳定）：这是最新的开发版本。只要提交的代码通过了所有自动化测试，就会立即发布此版本。此版本可能尚未被我们或其他用户使用过。不能保证在某些情况下它甚至能运行。此分支仅推荐给高级用户。在此分支中，预计会出现问题和自行解决问题。***仅在您知道自己在做什么并愿意在更新失败时进行手动恢复时使用此分支。*** 此版本会立即更新。

> **警告：在切换到此分支后，您可能无法返回到 `develop` 分支。** 在 GitHub 上，这是 `develop` 分支。
{.is-danger}

- 注意：如果您的安装是通过 Docker 进行的，请根据构建者的标签在容器标签的末尾添加 `:latest`、`:testing`、`:develop` 或 `:nightly`。



|                                                                      | `master` (稳定版) ![当前稳定版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (测试版) ![当前测试版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (不稳定版) ![当前不稳定版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### 我可以在 Docker 容器中更新 Prowlarr 吗？

- *从技术上讲，是可以的。* **但你绝对不应该这样做。** 这是 Docker 的主要理念。如果你在容器内升级到最新的 `nightly` 版本，然后更新 Docker 容器本身（可能降级到旧版本），可能会导致数据库问题。

### 安装新版本

#### 本地安装

1. 进入“System”然后点击“Updates”选项卡
1. 尚未安装的新版本旁边会有一个更新按钮，点击该按钮将安装更新。

#### Docker 安装

1. 重新拉取你的标签并更新容器

## 我可以从 `nightly` 切换回 `develop` 吗？

## 我可以在不同分支之间切换吗？

- 如果版本相同，你可以切换，否则请与开发团队确认是否可以从 `nightly` 切换到 `develop` 或从 `develop` 切换到 `nightly`。
- 如果不按照这些说明操作，可能导致你的 Prowlarr 无法使用或抛出错误。请注意
  - 最常见的错误是关于缺少列或表的数据库错误。

## 帮助，我的 Mac 提示无法打开 Prowlarr，因为开发者无法验证

- 这很简单，请查看此链接以获取更多信息 [here](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
- 或者，你可能需要自签名 Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## 帮助，我的 Mac 提示 Prowlarr.app 已损坏，无法打开

这可能是由于下载损坏（请重试）或安全问题引起的。

## 如何为 Prowlarr 提交功能请求？

要为 Prowlarr 提交功能请求，首先在 GitHub 上搜索以确保没有类似的请求，然后[点击此处](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=)添加你的请求。

## 我遇到一个错误：数据库磁盘映像损坏

- **“Error creating log database” 错误表示日志数据库存在问题**
  - 可以通过重命名或删除数据库来快速解决。日志数据库包含有关命令历史记录、更新安装历史记录以及 Info、Warn 和 Error 条目的不重要信息。
- **“Error creating main database” 或没有指定数据库的通用“database disk image is malformed” 错误表示 Prowlarr 的 SQLite 数据库存在问题**
  - 请继续执行下面的步骤
- 这意味着存储 Prowlarr 大部分信息的 SQLite 数据库已损坏。你可以尝试备份、恢复现有数据库、恢复备份，或者如果所有其他方法都失败，则从头开始使用全新的数据库。
- 如果数据库文件不可写，可能会导致此错误。权限问题可能只会影响新安装、迁移到新服务器的安装、最近修改了 appdata 目录权限的安装，或者更改了 \*Arr 运行的用户和组。
- 最好的选择是[尝试从备份中恢复](#how-do-i-backuprestore-my-prowlarr)
- 你还可以尝试恢复数据库。这通常是在更新后出现此问题时的唯一选择。尝试使用 [sqlite3 的 `.recover` 命令](/useful-tools#recovering-a-corrupt-db)
  - 如果你的 sqlite 没有 `.recover` 命令，或者你希望使用更友好的 GUI（例如 Windows），请按照[我们在此 wiki 上的说明](/useful-tools#recovering-a-corrupt-db-ui)操作。
- 数据库错误的另一个可能原因是将数据库放在网络驱动器上（nfs 或 smb 或其他非本地驱动器）。**SQLite 适用于数据和应用程序共存于同一台机器上的情况。**因此，你的 \*Arr AppData 文件夹（Docker 的 /config 挂载）必须位于本地存储上。[SQLite 和网络驱动器不兼容，最终会导致数据库损坏](https://www.sqlite.org/draft/useovernet.html)。
- 如果你使用的是 mergerFS，你需要删除 `direct_io`，因为 SQLite 使用的是 mmap，而 `direct_io` 不支持 mmap，详细信息请参阅 mergerFS 的[文档](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## 我在 Mac 上使用 Prowlarr，突然停止工作了。发生了什么？

最有可能是由于 MacOS 的一个错误导致 Prowlarr 数据库损坏。请查看恢复损坏数据库的 FAQ 条目。

## 如何从 Windows 服务切换到托盘应用？

- 关闭 Prowlarr
- 运行 Prowlarr 目录中的 serviceuninstall.exe
- 以管理员身份运行 Prowlarr.exe 一次，以赋予其适当的权限并打开防火墙。完成后，你可以关闭它并正常运行。
- （可选）将 Prowlarr.exe 的快捷方式放入启动文件夹，以在启动时自动启动。

## 如何备份/恢复 Prowlarr？

### 备份 Prowlarr

#### 使用内置备份

- 进入 Prowlarr UI 的“System”=>“Backup”
- 点击“Backup”按钮
- 在备份创建后下载 zip 文件以备份

#### 直接使用文件系统

- 找到 Prowlarr 的 AppData 目录的位置
  - 通过 Prowlarr UI 进入“System”=>“About”
  - [Prowlarr Appdata 目录](/prowlarr/appdata-directory)
- 停止 Prowlarr - 这将防止数据库损坏
- 将内容复制到安全位置

### 从备份中恢复

> 将备份还原到使用不同路径的操作系统上将无法正常工作（例如从 Windows 到 Linux，从 Linux 到 Windows，从 Windows 到 OS X 或从 OS X 到 Windows），在 OS X 和 Linux 之间移动可能有效，因为两者都使用包含 `/` 而不是 `\` 的路径，但不受支持。你需要手动编辑数据库中的所有路径。
{.is-warning}

#### 使用 zip 备份

- 重新安装 Prowlarr（如果适用/尚未安装）
- 运行 Prowlarr
- 导航到“System”=>“Backup”
- 选择“Restore Backup”
- 选择“Choose File”
- 选择你的备份 zip 文件
- 选择“Restore”

#### 使用文件系统备份

- 重新安装 Prowlarr（如果适用/尚未安装）
- 找到 Prowlarr 的 AppData 目录的位置
  - 运行 Prowlarr 一次，通过 UI 进入“System”=>“About”
  - [Prowlarr Appdata 目录](/prowlarr/appdata-directory)
- 停止 Prowlarr
- 删除 AppData 目录的内容 **（包括 .db-wal/.db-journal 文件，如果存在）**
- 从备份中恢复
- 启动 Prowlarr
- 只要路径相同，一切都会继续进行

#### 在 Synology NAS 上进行文件系统恢复

> 注意：在 Synology 上进行恢复需要了解 Linux 并具有根 SSH 访问 Synology 设备的权限。
{.is-warning}

- 重新安装 Prowlarr（如果适用/尚未安装）
- 找到 Prowlarr 的 AppData 目录的位置
  - 运行 Prowlarr 一次，通过 UI 进入“System”=>“About”
  - [Prowlarr Appdata 目录](/prowlarr/appdata-directory)
- 停止 Prowlarr
- 通过 SSH 连接到 Synology NAS 并以 root 身份登录

> 在某些安装中，用户与下面的命令不同：`chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- 执行以下命令：

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- 更新文件的权限：

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- 启动 Prowlarr

## 仅在 Windows 上的 localhost 加载 WebUI

如果你只能通过 `http://localhost:9696/` 或 `http://127.0.0.1:9696` 访问 Web 界面，则需要至少以管理员身份运行 Prowlarr 一次，甚至可能始终如此。

## 查找 Cookies

某些网站无法自动登录，需要你手动登录，然后将 Cookies 提供给 Prowlarr 以正常工作。[请参阅此文章了解详细信息。](/useful-tools#finding-cookies)

## uTorrent 不再工作

- 确保已启用 Web UI

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- 打开 Web UI

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- 确保“Alt Listening Port”（高级 => Web UI）与“Listening Port”（连接）不相同。我们建议更改 Web UI Alt Listening Port，以免影响连接的任何端口转发。

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## 我收到一个弹窗说config.xml文件损坏了，现在怎么办？

Prowlarr在启动时无法读取您的配置文件，因为它以某种方式损坏了。为了让Prowlarr恢复在线状态，您需要删除AppData文件夹中的`.xml`文件，删除后启动Prowlarr，它将在默认端口（9696）上启动，您现在应该重新配置在“常规设置”页面上配置的任何设置。

## 无效的证书和其他HTTPS或SSL问题

您的下载客户端停止工作，并且出现了类似“本地主机是无效证书”的错误？

Prowlarr验证SSL证书。如果下载客户端中没有设置SSL证书，或者您正在使用自签名的https证书而没有将CA证书添加到本地证书存储中，那么Prowlarr将拒绝连接。可以从Let's Encrypt获取免费的正确签名证书。

如果您的下载客户端和Prowlarr在同一台机器上，没有理由使用HTTPS，所以最简单的解决方案是禁用连接的SSL。大多数人都同意在本地网络上也不需要它。如果您想保持不安全的SSL设置，可以在高级设置中禁用证书验证。

## 帮助，我被锁在外面了

{#help-i-have-forgotten-my-password}

要禁用身份验证（以重置您忘记的用户名或密码），您需要编辑`config.xml`，它位于[Prowlarr Appdata目录](/prowlarr/appdata-directory)中

1. 用文本编辑器打开config.xml
2. 找到身份验证方法行，可能是`<AuthenticationMethod>Basic</AuthenticationMethod>`或`<AuthenticationMethod>Forms</AuthenticationMethod>`
3. 将`AuthenticationMethod`行更改为`<AuthenticationMethod>None</AuthenticationMethod>`
4. 重新启动Prowlarr
5. 现在可以无需密码访问Prowlarr，您应该在UI中的“设置：常规”中设置您的用户名和密码

## 奇怪的用户界面问题

- 如果您遇到任何奇怪的用户界面问题，或者某个视图或排序不起作用，请尝试在Chrome的隐身窗口或Firefox的隐私窗口中查看。如果在那里正常工作，请清除特定IP/域的浏览器缓存和cookie。有关更多信息，请参阅[清除缓存、Cookie和本地存储](/useful-tools#clearing-cookies-and-local-storage)维基文章。

## VPN、Jackett和\*ARRs

- 除非您在像中国、澳大利亚或南非这样的压制性国家，否则您的种子客户端通常是唯一需要在VPN后面的东西。由于VPN终点由许多用户共享，您可能会遇到各种服务的速率限制、DDOS保护和IP封禁。
- 换句话说，将\*Arrs（Lidarr、Prowlarr、Radarr、Readarr和Lidarr）放在VPN后面可能会导致应用程序在某些情况下无法使用，因为这些服务无法访问。

> **明确指出，VPN会导致\*Arrs出现问题，只是问题是什么时候出现：图像提供商会阻止您，Cloudflare也会在\*Arr服务器（更新、元数据等）之前阻止您**
{.is-warning}

- **许多私有跟踪器会禁止您使用或通过VPN访问它们（例如使用Jackett或Prowlarr）。**

### 使用VPN

- 如果需要VPN并且使用Docker，建议使用Hotio或Binhex的Download Client + VPN容器。
- 如果需要VPN并且不使用Docker，则您的VPN客户端***必须***支持分割隧道，以便只有所需的（下载客户端）应用程序在VPN后面。
- 使用Google或Cloudflare的DNS服务器代替您的ISP的DNS服务器，可以解决访问跟踪器的许多问题。
- 在某些情况下（例如英国的ISP），您可能需要将种子下载客户端放在VPN后面，并按以下方式配置Jackett/Prowlarr：
  - 将Jackett放在VPN后面，并确保分割隧道允许本地访问
  - 对于Prowlarr，配置您的VPN客户端提供代理，并在“设置”=>“索引器”中添加代理。给代理一个标签，需要使用它的任何索引器都使用相同的标签。
    - 如果绝对需要，如果您的VPN没有提供创建代理的方法，您可以将Prowlarr放在VPN后面，并确保分割隧道允许本地访问。

## 如何停止浏览器在启动时自动打开？

根据您的操作系统，有多种可能的方法。

- 在某些操作系统上，在“设置”=>“常规”中，有一个复选框可以在启动时打开浏览器。
- 在调用Prowlarr时，您可以在参数中添加`-nobrowser`（*nix）或`/nobrowser`（Windows）。
- 停止Prowlarr并编辑config.xml文件，将`<LaunchBrowser>True</LaunchBrowser>`更改为`<LaunchBrowser>False</LaunchBrowser>`。

## 我可以一次性添加所有索引器吗？

不可以。这样做不是一个好主意，也不会添加此功能。更好的做法是明智地选择您的索引器，注意统计信息，删除太慢或没有产生结果的索引器。正确修剪和维护您的索引器将在整体上产生更好的结果，并在应用程序搜索时更快地产生结果。