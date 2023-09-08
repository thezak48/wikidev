---
title: Lidarr常见问题解答
description: 
published: true
date: 2023-08-31T19:08:18.905Z
tags: lidarr, needs-love, faq
editor: markdown
dateCreated: 2021-06-14T14:33:41.344Z
---

# 目录

- [目录](#目录)
  - [Lidarr是如何工作的？](#lidarr是如何工作的)
  - [Lidarr如何找到发布的内容？](#lidarr如何找到发布的内容)
  - [强制身份验证](#强制身份验证)
  - [如何比较可能的下载选项？](#如何比较可能的下载选项)
  - [更新到Ubuntu 22.04后，Lidarr停止工作](#更新到ubuntu-2204后lidarr停止工作)
  - [为什么无法向Lidarr添加新的发布或艺术家？](#为什么无法向lidarr添加新的发布或艺术家)
  - [为什么无法添加各种艺术家专辑？](#为什么无法添加各种艺术家专辑)
  - [为什么Lidarr只显示录音室专辑？如何找到单曲或EP？](#为什么lidarr只显示录音室专辑如何找到单曲或ep)
  - [我可以只添加一个专辑吗？](#我可以只添加一个专辑吗)
  - [我可以下载单个音轨吗？](#我可以下载单个音轨吗)
  - [为什么艺术家X在搜索中找不到？](#为什么艺术家x在搜索中找不到)
  - [Lidarr匹配了一个包含太多音轨的专辑。如何将专辑更改为正确的发布版本？](#lidarr匹配了一个包含太多音轨的专辑如何将专辑更改为正确的发布版本)
  - [我在Lidarr中找不到一个发布，但它在MusicBrainz上。](#我在lidarr中找不到一个发布但它在musicbrainz上)
  - [Lidarr和MusicBrainz数据库多久同步一次？](#lidarr和musicbrainz数据库多久同步一次)
  - [如何添加缺失的艺术家图片？](#如何添加缺失的艺术家图片)
  - [如何获取缺失的专辑图片？（封面艺术）](#如何获取缺失的专辑图片封面艺术)
  - [我在导入我的艺术家时遇到问题，可能是什么原因？](#我在导入我的艺术家时遇到问题可能是什么原因)
  - [如何重命名我的艺术家文件夹？](#如何重命名我的艺术家文件夹)
  - [如何批量从想要的列表中删除艺术家？](#如何批量从想要的列表中删除艺术家)
  - [为什么Lidarr不能在反向代理后工作？](#为什么lidarr不能在反向代理后工作)
  - [如何更新Lidarr？](#如何更新lidarr)
    - [我可以在Docker容器内更新Lidarr吗？](#我可以在docker容器内更新lidarr吗)
    - [安装新版本](#安装新版本)
      - [本地安装](#本地安装)
      - [Docker安装](#docker安装)
  - [我可以从“nightly”切换回“develop”吗？](#我可以从nightly切换回develop吗)
  - [我可以在不同分支之间切换吗？](#我可以在不同分支之间切换吗)
  - [我遇到一个错误：数据库磁盘映像损坏](#我遇到一个错误数据库磁盘映像损坏)
  - [如何备份/恢复我的Lidarr？](#如何备份恢复我的lidarr)
    - [备份Lidarr](#备份lidarr)
      - [使用内置备份](#使用内置备份)
      - [直接使用文件系统](#直接使用文件系统)
    - [从备份中恢复](#从备份中恢复)
      - [使用zip备份](#使用zip备份)
      - [使用文件系统备份](#使用文件系统备份)
      - [在Synology NAS上恢复文件系统](#在synology-nas上恢复文件系统)
  - [我在Mac上使用Lidarr，突然停止工作了。发生了什么？](#我在mac上使用lidarr突然停止工作了发生了什么)
  - [我正在使用Pi和Raspbian，Lidarr无法启动](#我正在使用pi和raspbianlidarr无法启动)
  - [为什么列表同步时间如此长，我可以更改吗？](#为什么列表同步时间如此长我可以更改吗)
  - [我可以禁用刷新发布任务吗？](#我可以禁用刷新发布任务吗)
  - [为什么Lidarr无法在远程服务器上看到我的文件？](#为什么lidarr无法在远程服务器上看到我的文件)
    - [Lidarr默认使用LocalService帐户运行，该帐户无法访问受保护的远程文件共享](#lidarr默认使用localservice帐户运行该帐户无法访问受保护的远程文件共享)
    - [您正在使用映射的网络驱动器（而不是UNC路径）](#您正在使用映射的网络驱动器而不是unc路径)
  - [帮助！我被锁在外面了](#帮助我被锁在外面了)
  - [如何停止浏览器在启动时自动打开？](#如何停止浏览器在启动时自动打开)
  - [奇怪的用户界面问题](#奇怪的用户界面问题)
  - [VPN、Jackett和\*ARRs](#vpnjackett和arrs)
  - [Jackett的/all端点](#jackett的all端点)
    - [Jackett /All解决方案](#jackett-all解决方案)
  - [为什么会有两个文件？|为什么下载后还有一个文件留在下载目录中？](#为什么会有两个文件为什么下载后还有一个文件留在下载目录中)
  - [我一直收到关于云存储API限制的警告](#我一直收到关于云存储api限制的警告)

## Lidarr是如何工作的？

- Lidarr依赖于RSS订阅来自动抓取发布的内容，包括新发布的内容以及重新发布的以前发布的内容。RSS订阅是来自网站的最新发布内容，通常包含50到100个发布，尽管有些网站提供更多，有些提供更少。RSS订阅包括最近可用的所有发布，包括您不关注的请求媒体的发布，如果查看调试日志，您将看到这些发布正在被处理，这是完全正常的。
- Lidarr强制执行RSS同步间隔的最低值为10分钟，最高值为2小时。大多数索引器建议的最低值为15分钟，尽管有些索引器允许更低的间隔，2小时可以确保Lidarr检查的频率足够频繁，以免错过发布（即使它可以在许多索引器上翻页浏览RSS订阅以帮助解决这个问题）。一些索引器允许客户端执行比10分钟更频繁的RSS同步，在这种情况下，我们建议使用Lidarr的Release-Push API端点以及一个IRC通知频道将发布推送到Lidarr进行处理，这样可以实现几乎实时的处理，并减少索引器和Lidarr的负担，因为Lidarr不需要过于频繁地请求和处理相同的发布。

## Lidarr如何找到发布的内容？

- Lidarr**不会**定期搜索缺失的专辑文件或未达到质量目标的专辑文件。相反，它会频繁查询您的索引器和追踪器以获取**所有**最新发布的内容，然后将其与缺失或需要升级的发布列表进行比较。任何匹配的内容都会被下载。这使得Lidarr可以使用每天仅需24-100个查询（15-60分钟的RSS间隔）来处理**任何大小**的音乐库。如果您理解了这一点，您将意识到它只涵盖了**未来**的内容。
- 那么如何处理现在和过去的内容呢？当您添加一个专辑时，您需要设置正确的路径、配置文件和监视状态，然后使用“开始搜索缺失的专辑”复选框。如果专辑尚未发布，您无需发起搜索。
- 换句话说，Lidarr只会找到新上传到您的索引器的发布。它不会主动寻找您想要的过去上传的发布。
- 如果您已经添加了专辑，但现在想要搜索它，您有几个选择。您可以转到专辑页面并使用搜索按钮，它会执行搜索然后自动选择一个结果。您可以使用搜索选项卡查看**所有**结果，并手动选择您想要的结果。或者您可以使用“缺失”、“想要”或“未达到截止日期”的筛选器。
- 如果Lidarr长时间离线，它将尝试翻页查找它处理的最后一个发布，以避免错过发布。只要您的索引器支持翻页并且时间不太长，Lidarr就能够处理它可能错过的发布，并避免您需要搜索错过的发布。

## 强制身份验证

如果Lidarr暴露出来，以便可以从本地网络外部访问UI，则应启用某种形式的身份验证方法以访问UI。这也越来越多地被Tracker和Indexer要求。

从Lidarr v2开始，身份验证是强制性的。

### 身份验证方法

- `Basic`（浏览器弹出窗口）- 当访问Lidarr时，此选项将显示一个小弹出窗口，允许您输入用户名和密码
- `Forms`（登录页面）- 此选项将显示一个类似其他网站的登录屏幕，允许您登录到Lidarr
- `External` - 仅通过配置文件进行配置
  - 如果您使用**外部身份验证**，例如Authelia、Authetik、NGINX基本身份验证等，您可以通过关闭应用程序、在[配置文件](/lidarr/appdata-directory)中设置`<AuthenticationMethod>External</AuthenticationMethod>`，然后重新启动应用程序来避免需要双重身份验证。**请注意，文件中不支持多个`AuthenticationMethod`条目，只会使用最顶部的值**

### 要求进行身份验证

- 如果您不将应用程序暴露在外部和/或不希望在本地（例如LAN）访问时需要进行身份验证，则在设置=>常规安全性=>需要身份验证的地方更改为`对本地地址禁用`
  - 配置文件中的等效设置为`<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## 如何比较可能的下载选项？

> 通常，质量优先。如果您希望质量不是主要优先级-您可以合并您的质量。[请参阅TRaSH的指南](https://trash-guides.info/merge-quality)***
{.is-info}

- 当前的逻辑[可以在这里找到](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs)。

- 截至2022-01-23，逻辑如下：

1. 质量
1. 首选词得分
1. 协议（根据相关延迟配置文件）
1. 索引器优先级
1. 种子/同行（如果是Torrent）
1. 专辑计数
1. 年龄（如果是Usenet）
1. 大小

## 更新到Ubuntu 22.04后，Lidarr停止工作

- Lidarr v0.8不兼容也不支持Ubuntu 22.04
- 只有Lidarr v1支持Ubuntu 22.04
- [有关分支和版本的信息，请参见此FAQ条目](#如何更新lidarr)

## 为什么无法向Lidarr添加新的发布或艺术家？

- 发布可能在MusicBrainz上是“未知”类型

## 为什么无法添加各种艺术家专辑？

- Musicbrainz上的Various Artists和其他元艺术家是由于它们提供的条目数量。

## 为什么Lidarr只显示录音室专辑？如何找到单曲或EP？

- Lidarr默认只获取每位艺术家的录音室专辑。但是，您可以通过使用元数据配置文件来扩展艺术家的专辑类型，或者扩展整个库的专辑类型。

## 我可以只添加一个专辑吗？

- 目前不支持。

## 我可以下载单个音轨吗？

- Lidarr通过搜索和下载完整的发布来工作，因此除非艺术家发布了单曲，否则无法下载单个音轨。

## 为什么艺术家X在搜索中找不到？

- 搜索仍然在进行中。未显示在搜索结果中的艺术家可以通过搜索`lidarr:mbid`来添加，其中`mbid`是艺术家的Musicbrainz ID。

## Lidarr匹配了一个包含太多音轨的专辑。如何将专辑更改为正确的发布版本？

- 打开专辑详细信息页面，选择顶部导航栏中的编辑图标。在那里，您可以找到与该专辑相关的所有发布的下拉列表。

## 我在Lidarr中找不到一个发布，但它在MusicBrainz上。

- 这可能是由于发布具有“未知”的发布状态。请更新MusicBrainz。

## Lidarr和MusicBrainz数据库多久同步一次？

- 每小时的5分钟

## 如何添加缺失的艺术家图片？

- 在fanart.tv上添加艺术品，并等待大约7天以上以清除缓存。然后刷新元数据。

## 如何获取缺失的专辑图片？（封面艺术）

- 在musicbrainz上添加封面艺术，并等待大约1小时以上以清除缓存。然后刷新元数据。

## 我在导入我的艺术家时遇到问题，可能是什么原因？

- 艺术家导入过程只导入艺术家名称和路径位置，这些信息存储在数据库中，以便可以检索元数据，并且将来可以将下载的内容放在相同的位置。为此，Lidarr运行的用户帐户需要对数据目录具有读写权限。

## 如何重命名我的艺术家文件夹？

{#rename-folders}

> 对于移动/更改艺术家路径，相同的过程也适用。
{.is-info}

1. 资源库
1. 批量编辑器
1. 选择需要重命名文件夹的艺术家
1. 将根文件夹更改为艺术家当前所在的相同根文件夹
1. 选择“是，移动文件”

## 如何批量从想要的列表中删除艺术家？

- 使用批量编辑器=>选择要删除的艺术家=>删除

## 为什么Lidarr不能在反向代理后工作

- Lidarr使用.NET和一个新的Web服务器。为了使SignalR工作，使UI按钮工作，使数据库更改生效以及其他项目。需要在Lidarr的位置块中添加以下内容：
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- 确保**不要**包括nginx文档中建议的`proxy_set_header Connection "Upgrade";`。**这不会起作用**
- [请参阅此ASP.NET Core问题](https://github.com/aspnet/AspNetCore/issues/17081)
- 如果您使用类似Cloudflare的CDN，请确保启用了Websockets以允许Websocket连接。

## 如何更新Lidarr？

- 转到设置，然后选择常规选项卡，显示高级设置（使用保存按钮旁边的切换）。

1. 在更新部分，将分支名称更改为`master`或`develop`
1. 保存

*这不会立即安装该分支的版本，它将在下次更新时进行。*

- `master` - ![当前主分支/稳定版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=主分支&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (默认/稳定版): 它已经由开发和夜间分支的用户测试过，没有任何已知的重大问题。该版本将每月接收更新。在 GitHub 上，这是 `master` 分支。

- `develop` - ![当前开发分支/测试版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=开发分支&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (测试版): 这是测试的边缘版本。在夜间版本测试通过后发布，以确保没有立即出现的问题。新功能和错误修复首先在此版本中发布。它可以被认为是半稳定的，但仍然是 `beta` 版本。该版本将每周或每两周接收更新，具体取决于开发进度。

> **警告：切换到此分支后，您可能无法返回到 `master` 分支。** 在 GitHub 上，这是 `develop` 分支的特定时间点的快照。
{.is-warning}

- `nightly` - ![当前夜间版本/不稳定版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=夜间版本&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (Alpha/不稳定版): 这是最新的版本。只要提交的代码通过了所有自动化测试，就会立即发布。这个版本可能还没有被我们或其他用户使用过。不能保证在某些情况下它甚至能运行。此分支仅推荐给高级用户。在此分支中，预计会出现问题和自我调查。***只有在您知道自己在做什么并愿意亲自解决更新失败的问题时才使用此分支。*** 此版本会立即更新。

> **警告：切换到此分支后，您可能无法返回到 `master` 分支。** 在 GitHub 上，这是 `develop` 分支。
{.is-danger}

- 注意：如果您的安装是通过 Docker，请根据构建者的不同，在容器标签的末尾添加 `:release`、`:latest`、`:testing` 或 `:develop`。请注意，意图上的分支 `nightly` 在下面故意没有列出。

|                                                                    | `master` (稳定版) ![当前主分支/最新版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=主分支&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (测试版) ![当前开发分支/测试版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=开发分支&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (不稳定版) ![当前夜间版本/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=夜间版本&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### 我可以在 Docker 容器中更新 Lidarr 吗？

- *从技术上讲，是可以的。* **但是你绝对不应该这样做。** 这是 Docker 的主要理念。如果你在容器内升级到最新的 `nightly` 版本，然后更新 Docker 容器本身（可能降级到旧版本），可能会导致数据库问题。

### 安装更新版本

#### 本机

1. 进入“系统”，然后点击“更新”选项卡
1. 尚未安装的更新版本旁边会有一个更新按钮，点击该按钮将安装更新。

#### Docker

1. 重新拉取标签并更新容器

## 我可以从 `nightly` 切换回 `develop` 吗？

## 我可以在不同分支之间切换吗？

- 如果版本相同，您可以切换，否则请与开发团队核实是否可以从 `nightly` 切换到 `master`；从 `nightly` 切换到 `develop`；或从 `develop` 切换到 `master`，具体取决于您所使用的构建版本。
- 如果不按照这些说明操作，可能导致 Lidarr 无法使用或抛出错误。您已经被警告过了。
  - 最常见的错误是类似于 `Error parsing column 45 (Language=31 - Int64)` 或其他类似的数据库错误，涉及缺少列或表。

## 我遇到了一个错误：Database disk image is malformed

- **`Error creating log database` 错误表示日志数据库存在问题**
  - 这可以通过重命名或删除数据库来快速解决。日志数据库包含有关命令历史记录、更新安装历史记录以及 Info、Warn 和 Error 条目的不重要信息。
- **`Error creating main database` 或没有指定数据库的一般性 `database disk image is malformed` 错误表示 lidarr.db 存在问题**
  - 请继续执行下面的步骤
- 这意味着存储 Lidarr 大部分信息的 SQLite 数据库已损坏。您可以尝试备份、恢复现有数据库、恢复备份，或者如果所有其他方法都失败，则重新开始使用全新的数据库。
- 如果数据库文件不可写，可能会出现此错误。权限问题可能只会影响新安装、迁移到新服务器的安装、最近修改了 appdata 目录权限或更改了 \*Arr 运行的用户和组。
- 您的最佳和首选选项是[尝试从备份中恢复](#如何备份/恢复我的 Lidarr)。
- 您还可以尝试恢复数据库。这通常是在更新后出现此问题时的唯一选择。尝试使用 [sqlite3 的 `.recover` 命令](/useful-tools#recovering-a-corrupt-db)
  - 如果您的 sqlite 没有 `.recover` 命令，或者您希望使用更友好的 GUI（例如 Windows），请按照[我们在此 wiki 上的说明](/useful-tools#recovering-a-corrupt-db-ui)进行操作。
- 您的数据库出现错误的另一个可能原因是将数据库放在网络驱动器上（nfs 或 smb 或其他非本地驱动器）。**SQLite 是为数据和应用程序共存于同一台机器的情况设计的。**因此，您的 \*Arr AppData 文件夹（Docker 的 /config 挂载点）必须位于本地存储上。[SQLite 和网络驱动器不兼容，会导致数据库损坏](https://www.sqlite.org/draft/useovernet.html)。
- 如果您使用的是 mergerFS，您需要删除 `direct_io`，因为 SQLite 使用 mmap，而 `direct_io` 不支持，详细信息请参阅 mergerFS 的[文档](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)。

## 如何备份/恢复我的 Lidarr？

### 备份 Lidarr

#### 使用内置备份

- 进入 Lidarr UI 的“系统” => “备份”
- 点击“备份”按钮
- 在备份创建完成后下载 zip 文件并妥善保存

#### 直接使用文件系统

- 找到 Lidarr 的 AppData 目录的位置
  - 通过 Lidarr UI 进入“系统” => “关于”
  - [Lidarr Appdata 目录](/lidarr/appdata-directory)
- 停止 Lidarr - 这将防止数据库损坏
- 将内容复制到安全位置

### 从备份中恢复

> 将备份还原到使用不同路径的操作系统上将无法正常工作（Windows 到 Linux，Linux 到 Windows，Windows 到 OS X 或 OS X 到 Windows），在 OS X 和 Linux 之间移动可能有效，因为两者都使用包含 `/` 而不是 Windows 使用的 `\` 的路径，但不受支持。您需要手动编辑数据库中的所有路径。
{.is-warning}

#### 使用 zip 备份

- 重新安装 Lidarr（如果适用/尚未安装）
- 运行 Lidarr
- 导航到“系统” => “备份”
- 选择“还原备份”
- 选择“选择文件”
- 选择您的备份 zip 文件
- 选择“还原”

#### 使用文件系统备份

- 重新安装 Lidarr（如果适用/尚未安装）
- 找到 Lidarr 的 AppData 目录的位置
  - 运行 Lidarr 一次，然后通过 UI 进入“系统” => “关于”
  - [Lidarr Appdata 目录](/lidarr/appdata-directory)
- 停止 Lidarr
- 删除 AppData 目录的内容 **（包括 .db-wal/.db-journal 文件，如果存在）**
- 从备份中恢复
- 启动 Lidarr
- 只要路径相同，一切都会继续进行

#### 在 Synology NAS 上的文件系统还原

> 注意：在 Synology 上进行还原需要了解 Linux，并具备对 Synology 设备的 Root SSH 访问权限。
{.is-warning}

- 重新安装 Lidarr（如果适用/尚未安装）
- 找到 Lidarr 的 AppData 目录的位置
  - 运行 Lidarr 一次，然后通过 UI 进入“系统” => “关于”
  - [Lidarr Appdata 目录](/lidarr/appdata-directory)
- 停止 Lidarr
- 通过 SSH 连接到 Synology NAS 并以 root 身份登录

> 在某些安装中，用户与下面的命令不同：`chown -R sc-Lidarr:Lidarr *` {.is-info}

- 执行以下命令：

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- 更新文件的权限：

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- 启动 Lidarr

## 我在 Mac 上使用 Lidarr，突然无法工作了。发生了什么？

- 最有可能是由于 MacOS 的一个错误导致其中一个数据库损坏。

- 请参阅上面的“数据库损坏”条目。

- 然后尝试启动并查看是否正常工作。如果仍然无法工作，您需要进一步的支持。在我们的 [subreddit /r/lidarr](http://reddit.com/r/lidarr) 上发布问题或加入[我们的 Discord](https://lidarr.audio/discord) 寻求帮助。

## 我在使用 Pi 和 Raspbian，Lidarr 无法启动



Raspbian的libseccomp2版本过旧，无法支持基于Ubuntu 20.04的Docker容器，而hotio和LinuxServer都使用Ubuntu 20.04作为基础。您可以使用`--privileged`选项，更新Ubuntu的libseccomp2版本，或者选择更好的操作系统（我们推荐使用Ubuntu 20.04 arm64）。

**可能的解决方案：**

通过从Debian仓库安装后端修复了此问题。通常不建议在全面升级模式下使用后端。安装单个软件包可能没有问题，但也可能引发问题。因此，您需要了解自己在做什么。

修复步骤：

首先确保您正在运行Raspbian buster，例如使用`lsb_release -a`命令。

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- 如果您正在使用buster：
  - 运行以下命令将后端添加到您的源中

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - 安装libseccomp2的后端

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## 为什么列表同步时间如此长，我可以更改吗？

列表从来都不是“立即添加”的工具，而是“嘿，我想要这个，请最终添加”工具。

您可以手动触发列表刷新，通过API脚本触发它，或直接将发布添加到Lidarr中。

这个改变是因为我们的服务器不希望被每10分钟更新列表的人拖垮。

## 我可以禁用刷新发布任务吗？

不可以，也不应该通过任何SQL操作来禁用它。刷新发布任务会查询上游的Servarr代理，检查每个发布的元数据（ID、演员、摘要、评分、翻译、替代标题等）是否与Lidarr中的当前元数据有更新。如果有必要，它将更新适用的发布。

常见的抱怨是刷新任务会导致大量的I/O使用。可能会导致问题的一个设置是“刷新后重新扫描艺术家文件夹”。如果在刷新过程中磁盘I/O使用量激增，您可能需要将重新扫描设置更改为“手动”。除非您所有对库的更改（新发布、升级、删除等）都是通过Lidarr完成的，否则不要将其更改为“从不”。如果您手动删除发布文件或使用第三方程序进行删除，请不要将其设置为“从不”。

## 为什么Lidarr无法看到我在远程服务器上的文件？

- 对于所有操作系统，请确保您以\*Arr运行的用户/组具有对挂载驱动器的读写权限。
- 对于Linux，请确保：
  - 如果您使用的是NFS挂载，请确保启用了`nolock`。
  - 如果您使用的是SMB挂载，请确保启用了`nobrl`。
- 对于Windows：简而言之，\*Arr正在运行的用户（如果是服务）或者在其下运行的用户（如果是托盘应用程序）无法访问远程服务器上的文件路径。这可能是由于各种原因，但最常见的是\*Arr正在以服务的身份运行，这会导致下面描述的问题。

### Lidarr默认在LocalService帐户下运行，该帐户无法访问受保护的远程文件共享

- 将Lidarr的服务更改为具有访问该共享的目标用户帐户。
- 在Windows服务器上打开“管理工具”\>“服务”窗口。
- 停止Lidarr服务。
- 打开“属性”\>“登录”对话框。
- 将服务用户帐户更改为目标用户帐户。
- 使用启动文件夹运行Lidarr.exe

### 您正在使用映射的网络驱动器（而不是UNC路径）

- 将路径更改为UNC路径（`\\server\share`）
- 通过启动文件夹运行Lidarr.exe

## 帮助，我被锁定了

{#help-i-have-forgotten-my-password}

要禁用身份验证（以重置您忘记的用户名或密码），您需要编辑`config.xml`文件，该文件位于[Lidarr应用数据目录](/lidarr/appdata-directory)中。

1. 用文本编辑器打开config.xml文件。
2. 找到身份验证方法行，可能是`<AuthenticationMethod>Basic</AuthenticationMethod>`或`<AuthenticationMethod>Forms</AuthenticationMethod>`。
3. 将`AuthenticationMethod`行更改为`<AuthenticationMethod>None</AuthenticationMethod>`。
4. 重新启动Lidarr。
5. 现在可以在没有密码的情况下访问Lidarr，您应该在UI的“设置：常规”中设置您的用户名和密码。

## 如何停止浏览器在启动时自动打开？

根据您的操作系统，有多种可能的方法。

- 在某些操作系统的“设置”=>“常规”中，有一个复选框可以在启动时打开浏览器。
- 在调用Lidarr时，您可以在参数中添加`-nobrowser`（*nix）或`/nobrowser`（Windows）。
- 停止Lidarr并编辑config.xml文件，将`<LaunchBrowser>True</LaunchBrowser>`更改为`<LaunchBrowser>False</LaunchBrowser>`。

## 奇怪的用户界面问题

- 如果您遇到任何奇怪的用户界面问题，比如库页面不显示任何内容，或者某个视图或排序不起作用，请尝试在Chrome的隐身窗口或Firefox的隐私窗口中查看。如果在那里正常工作，请清除特定IP/域名的浏览器缓存和Cookie。有关更多信息，请参阅[清除缓存、Cookie和本地存储](/useful-tools#clearing-cookies-and-local-storage)维基文章。

## VPN、Jackett和\*ARRs

- 除非您在中国、澳大利亚或南非等压制性国家，否则通常只有您的种子客户端需要在VPN后面。由于VPN终点由许多用户共享，您可能会遇到各种服务的速率限制、DDOS保护和IP封禁问题。
- 换句话说，将\*Arrs（Lidarr、Prowlarr、Radarr、Readarr和Lidarr）放在VPN后面可能会导致这些应用程序在某些情况下无法使用，因为无法访问这些服务。

> **明确一点，问题不在于VPN是否会对\*Arrs造成问题，而在于何时会造成问题：图像提供商会封锁您，而Cloudflare也会在\*Arr服务器（更新、元数据等）之前进行封锁**
{.is-warning}

- **许多私有跟踪器会因使用或通过VPN访问它们（例如使用Jackett或Prowlarr）而封禁您。**

### 使用VPN

- 如果需要VPN并且使用Docker，建议使用Hotio或Binhex的Download Client + VPN容器。
- 如果需要VPN并且不使用Docker，则您的VPN客户端***必须***支持分流，以便只有所需的（下载客户端）应用程序在VPN后面。
- 使用Google或Cloudflare的DNS服务器而不是您的ISP的DNS服务器，可以解决访问跟踪器的许多问题。
- 在某些情况下（例如英国的ISP），您可能需要将种子下载客户端放在VPN后面，并按以下方式设置Jackett/Prowlarr：
  - 将Jackett放在VPN后面，并确保分流允许本地访问。
  - 对于Prowlarr，请配置您的VPN客户端提供代理，并在“设置”=>“索引器”中添加代理。给代理添加一个标签，将需要使用该代理的索引器添加相同的标签。
    - 如果绝对需要，并且您的VPN没有提供创建代理的方法，您可以将Prowlarr放在VPN后面，并确保分流允许本地访问。

## Jackett的/all端点

{#jackett-all-endpoint}

- Jackett的`/all`端点很方便，但除此之外没有其他好处。其他一切都可能引发问题，因此需要逐个添加每个跟踪器。或者，您可以尝试使用Jackett和NZBHydra2的替代方案[Prowlarr](/prowlarr)。
- **2022年4月更新：由于Jackett的`/all`端点只会引发问题，\*Arr对其的支持已被移除。**
- Jackett的`/all`端点很方便，但除此之外没有其他好处。其他一切都可能引发问题，因此现在需要逐个添加每个跟踪器。
- [即使Jackett的开发人员也表示应避免使用`/all`端点](https://github.com/Jackett/Jackett#aggregate-indexers)。
- 使用/all端点没有任何优势，只有劣势：
  - 您失去了对索引器特定设置（类别、搜索模式等）的控制。
  - 混合使用搜索模式（IMDB、查询等）可能会导致低质量的结果。
  - 无法使用索引器特定的类别（>= 100000）。
  - 慢速索引器会降低整体结果的速度。
  - 总结果限制为1000个。
  - 如果/all中的一个跟踪器返回错误，\*Arr将禁用它，现在您将无法获得任何结果。

### Jackett /All的解决方案

- 在Jackett中手动将每个跟踪器添加为索引器。
- 查看[Lidarr/Radarr/Readarr开发团队](/prowlarr)的[Prowlarr](/prowlarr)，它可以将索引器同步到\*Arr。
- 查看[NZBHydra2](https://github.com/theotherp/nzbhydra2)，它可以将索引器同步到\*Arr。但不要使用它们的单个聚合端点，而是使用`multi`选项进行同步。

## 为什么会有两个文件？| 为什么下载文件夹中会有一个文件剩下？

这是正常现象。如果设置支持[硬链接](https://trash-guides.info/hardlinks)，则不会使用双倍的空间。以下是种子处理的工作原理。

1. Lidarr将下载请求发送到您的客户端，并将其与您在下载客户端设置中配置的标签或类别名称关联。例如：电影、电视、系列、音乐等。
2. Lidarr通过您的下载客户端的API监视使用该类别名称的活动下载。此监视通过您的下载客户端的API进行。
3. 完成的文件保留在其原始位置，以便您可以进行文件的做种（可以在下载客户端或在特定下载客户端下进行比率或时间的调整）。当文件导入到媒体文件夹时，如果您的设置支持硬链接，将会创建硬链接；如果不支持硬链接，则会复制文件。
4. 如果在Lidarr的设置中启用了“完成下载处理 - 删除完成”选项，只有当下载客户端报告做种完成并且种子已停止（即暂停）时，Lidarr才会删除原始文件和种子。有关如何优化配置下载客户端的详细信息，请参阅[TRaSH的下载客户端指南](https://trash-guides.info/Downloaders/)。

> 硬链接默认是启用的。[硬链接不会使用任何额外的磁盘空间。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)完成下载目录和媒体库的文件系统和挂载点必须相同。如果硬链接创建失败或者您的设置不支持硬链接，则会回退并复制文件。
{.is-info}

## 我一直收到来自云存储的API限制警告

Lidarr与其他Arrs不同。它使用标签而不是文件名进行操作。如果您将Lidarr文件保存在云存储上，它必须下载文件以读取标签。这将非常快速地消耗您在存储提供商上的任何API限制。我们非常不建议您将Lidarr库保存在云存储提供商上，您可能遇到的任何问题都可能是由于此设置引起的。