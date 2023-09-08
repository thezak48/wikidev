---
title: 有用的工具
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: useful-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# 目录

- [目录](#目录)
- [恢复损坏的数据库](#恢复损坏的数据库)
  - [恢复损坏的数据库（UI）（Windows）](#恢复损坏的数据库uiwindows)
  - [命令行数据库恢复](#命令行数据库恢复)
- [查找 Cookies](#查找-cookies)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [清除 Cookies 和本地存储](#清除-cookies-和本地存储)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
{.links-list}
- [其他项目和程序 - 请求应用 *Arrs](#其他项目和程序-请求应用-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
{.links-list}
- [其他项目和程序 - *Arr 相关](#其他项目和程序-arr-相关)
  - [远程控制](#远程控制)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Android 应用](#radarr-sonarr-companion-android-应用)
    - [nzb360 - Android 应用](#nzb360-android-应用)
{.links-list}
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [字幕](#字幕)
    - [Bazarr](#bazarr)
- [其他项目和程序 - Torrents/下载](#其他项目和程序-torrents下载)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit 管理](#qbit-管理)
- [其他项目和程序](#其他项目和程序)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
{.links-list}
- [Twitter 连接说明](#twitter-连接说明)

以下应用程序是与 \*Arr 应用套件或媒体收藏相关的伴侣应用程序。它们不由 \*Arr 开发团队维护、开发或支持。请将任何具体的支持问题直接向相应的应用程序开发团队提问。

# 恢复损坏的数据库

请注意，应用程序的数据库可以在下面链接的应用数据目录中找到。该目录也可以作为 datadir 参数传递。

- [Lidarr 应用数据目录](/lidarr/appdata-directory)
- [Prowlarr 应用数据目录](/prowlarr/appdata-directory)
- [Radarr 应用数据目录](/radarr/appdata-directory)
- [Readarr 应用数据目录](/readarr/appdata-directory)
- [Sonarr 应用数据目录](/sonarr/appdata-directory)
{.links-list}

> 有两种恢复数据库的选项，如下所示。{.is-info}

- [使用 DB Browser for SQLite 和使用 UI](#恢复损坏的数据库-ui)
- [使用 Sqlite 的 `.recover` 函数](#命令行数据库恢复)
{.links-list}

## 恢复损坏的数据库（UI）（Windows）

{#windows}
{#恢复损坏的数据库-ui}

> 请注意，这与 `.recover` 命令相同，需要 Sqlite v3.29 | [请参阅 Sqlite 文档以获取有关 `.recover` 命令的更多详细信息](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database)。下面链接的步骤中介绍了如何执行此操作。{.is-info}

> [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/) 是一个高质量、可视化、开源的工具，用于创建、设计和编辑与 SQLite 兼容的数据库文件。DB4S 适用于希望创建、搜索和编辑数据库的用户和开发人员。DB4S 使用一种熟悉的类似电子表格的界面，不需要学习复杂的 SQL 命令。
{.is-info}

1. 停止应用程序
1. 复制损坏的数据库（`.db`）并将其与任何 `.shm` 和 `.wal` 文件一起复制
1. 在 [DB Browser for SQLite (DB4S)](https://SQLitebrowser.org/) 中打开损坏的数据库
1. 文件 => 导出 => 导出数据库到 SQL 文件
1. 选择所有表
1. 勾选/启用“在 INSERT INTO 中保留列名”
1. 导出全部内容
1. 覆盖旧模式
1. 保存
1. 关闭数据库
1. 新建数据库 => 文件 => 导入 => 导入前一步骤的文件
1. 如果有导入错误或约束问题，尽可能清理有问题的插入语句或删除它们
1. 执行以下 SQL `VACUUM;`
1. 提示时保存数据库。
1. 工具 => 完整性检查；结果应显示为 OK
1. 关闭数据库
1. 从配置文件夹中删除所有 `wal`、`shm` 和 `db` 文件
1. 将新数据库保存（或复制，如果 \*Arr 不在与 DB4S 相同的系统上）到配置文件夹，并将应用程序指向它。所有 \*Arrs 将其数据库命名为 `<appname>.db`，例如 `radarr.db`
1. 如有需要，为恢复的数据库设置正确的权限。所有者应为用户和组，与 \*Arr 配置为运行的用户和组相同。
1. 启动应用程序

请注意，gif 动画不包括 `VACUUM;` 命令

![dbrecover.gif](/dbrecover.gif)

## 命令行数据库恢复

{#nix}

以下说明适用于 \*Nix 操作系统，但在 Windows 命令行上的概念类似。

> 这使用了 [sqlite3 的 `.recover` 命令](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database)，是理想的方法。请注意，它需要 Sqlite 3.29+。
{.is-info}

> 由于 \*Arrs 需要 sqlite3，因此假设您已在系统上安装了 sqlite3。{.is-info}

1. 停止应用程序
1. SSH 进入您的主机或以其他方式启动 shell
1. 输入 `sqlite3 <损坏数据库的路径> ".recover" | sqlite3 <恢复数据库的输出路径>`
1. 如有需要，为恢复的数据库设置正确的权限。所有者应为用户和组，与 \*Arr 配置为运行的用户和组相同。
1. 删除或移动/重命名文件夹中的旧损坏数据库和任何 `wal` 或 `shm` 文件
1. 重命名恢复的数据库。所有 \*Arrs 将其数据库命名为 `<appname>.db`，例如 `radarr.db`
1. 启动应用程序

# 查找 Cookies

- 有些网站无法自动登录，需要您手动登录，然后提供 cookies 才能正常工作。下面的页面描述了如何执行此操作。

## 通用说明

1. 使用浏览器登录到您选择的 Prowlarr 索引器配置中使用的网站链接地址
1. 按 F12 打开 DevTools 面板
1. 选择 Network 选项卡
1. 单击 Doc 按钮（Chrome 浏览器）或 HTML 按钮（Firefox 浏览器）
1. 按 F5 刷新页面
1. 单击第一行条目
1. 在右侧面板上选择 Headers 选项卡
1. 在请求标头部分查找 'cookie:'。有关详细信息，请参阅您的跟踪器的 UI 中的帮助文本
1. 选择并复制整个 cookie 字符串（在 cookie: 之后的所有内容）
1. 删除 Prowlarr 索引器配置 cookie 框中已有的任何内容
1. 将复制的 cookie 字符串粘贴到该框中
1. 单击保存

> 如果您的跟踪器需要用户代理，则可以在请求标头中找到它。{.is-info}

### 注意事项

- 请确保使用与运行 Prowlarr 的计算机相同的浏览器，因为从其他平台很少能够使用 cookies。
- 在网站的登录页面上，请不要勾选任何限制您的会话仅限于一个 IP 地址或在短时间后注销的选项。如果有“记住我”的选项，请使用它。
- 确保在获取 cookie 之前，您可以访问站点的种子搜索页面，因为站点为了防止此操作（警报、未读通知或未读私信，或低比率警告）将阻止 Prowlarr 在使用 cookie 后成功进行测试。

## Chrome

- 转到种子跟踪器网站并登录。

- 按 F12

- 在顶部的 Application 选项卡下，左侧将有 "Storage"。您将看到一个 "Cookies" 子部分，在其中您将看到您的跟踪器的 URL。单击该 URL。

- 单击该选项卡上的 "Pass" 或类似条目，将弹出一个框，其中显示一个大约 25-30 个字符长的字符串。将其复制并粘贴到需要它的应用程序中。

  - 如果字符串看起来类似于 `cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser`，则应使用整个条目。

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- 您还可以参考 Chrome 的文档 [Chrome cookies](https://developer.chrome.com/docs/devtools/storage/cookies/)

## Firefox

- [请参阅 Mozilla 的文档](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# 清除 Cookies 和本地存储

## Chrome

1. 导航到 `chrome://settings/siteData`
1. 输入要清除的站点（或应用）名称
1. 单击该站点的垃圾桶图标

## Firefox

- 请参阅 [Mozilla 的帮助文章](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox)

## Microsoft Edge (Chromium)

1. 导航到 `edge://settings/siteData`
1. 输入要清除的站点（或应用）名称
1. 单击该站点的箭头
1. 单击该站点的垃圾桶图标

# 其他项目和程序 - 请求应用 *Arrs

## Notifiarr（前身为 Discord Notifier）

[Notifiarr](https://notifiarr.com/) 是由 \*Arr 开发人员之一创建的工具，旨在通过更详细的 Discord 通知提供更深入的功能。它提供了一种可配置的方式，根据您选择的触发器添加通知（包括反应）。网站提供了一个 UI，用于选择在通知中显示的内容。除了其他功能外，还支持抓取、导入、升级、健康和失败通知。

[Wiki](https://notifiarr.wiki/)

亮点

- 应用程序状态
- 请求和批准（\~Ombi）
- 可自定义的 *ARR 应用程序通知
- 带批准的请求系统
- 用户监视系列或电影并通过 @ 提及进行通知的关注系统
- 服务器状态
- 经常更新的新功能

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/) 允许用户请求电影、电视节目（系列、季节或单集）和音乐专辑。

## Overseerr

[Overseerr](https://overseerr.dev/) 是一个请求管理和媒体发现工具，可与您现有的 Plex 生态系统配合使用。

## Petio

[Petio](https://petio.tv/) 是一个第三方伴侣应用程序，可供 Plex 服务器所有者使用，让他们的用户请求、审核和发现内容。

该应用程序旨在即时熟悉和直观，即使对于最不懂技术的用户也是如此。Petio 将帮助您管理用户的请求，连接到其他第三方应用程序，如 Sonarr 和 Radarr，当内容可用时通知用户，并跟踪请求的进度。Petio 还允许用户在您的服务器上和服务器外发现媒体，快速轻松地找到相关内容，并留下他们对其他用户的意见。

# 其他项目和程序 - *Arr 相关

## 远程控制

### LunaSea

[LunaSea](https://www.lunasea.app/) 是一个功能齐全的开源自托管控制器！专注于为您的自托管媒体软件提供无缝体验。

### Radarr & Sonarr Companion - Android 应用

使用手机轻松地向您的系统添加新电影/电视节目。应用程序可在 [Google Play](https://play.google.com/store/apps/details?id=easy.radarr) 上获取。

### nzb360 - Android 应用

nzb360 提供 Sonarr、Radarr、Lidarr、torrent、usenet 和其他服务的管理。应用程序可在 [Google Play](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360) 上获取。有关更多信息，请访问 [官方网站](https://nzb360.com/)。

## Lidarr

### AMD

[Automated Music Downloader](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd 是一个 Lidarr 的伴侣脚本，用于自动下载 Lidarr 的音乐。

### AMVD

[Automated Music Video Downloader](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd 是一个 Lidarr 的伴侣脚本，用于自动下载和标记用于其他视频应用程序（plex/kodi/jellyfin/emby）的音乐视频。

## Radarr

## AMTD

[Automated Movie Trailer Downloader](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd 是一个 Radarr 的伴侣脚本，用于自动下载用于其他视频应用程序（plex/kodi/jellyfin/emby）的电影预告片和额外内容。

## 字幕

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr) 是一个与 Sonarr 和 Radarr 配合使用的伴侣应用程序，根据您的要求管理和下载字幕。

# 其他项目和程序 - Torrents/下载

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed) 是一个旨在帮助您下载可以基于现有种子进行交叉种子的种子的应用程序。它旨在保守匹配，以最小化手动干预。目前支持 Jackett 和 Qbittorrent/rTorrent。

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr) 提供了一套用于修复 Starr 应用程序问题的实用程序。Toolbarr 允许您对 Starr 应用程序及其 SQLite3 数据库执行各种操作。

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr) 此应用程序作为守护程序在您的下载主机上运行。它会检查已完成的下载并提取它们，以便 \*Arr 可以导入它们。

有一些选项可用于在客户端下载文件后提取和删除文件。Captain 不喜欢其中任何一个，所以他自己写了一个。他想要一个小巧的单一二进制文件，具有合理的日志记录功能，可以提取已下载的存档文件，并在导入后清理它们。

## qBit 管理

[qBit 管理，也称为 "qbit_manage"](https://github.com/StuffAnThings/qbit_manage) 是一个用于管理 qBittorrent 实例的程序，例如：



- 根据Tracker URL为种子打标签（仅为没有标签的种子打标签）
- 根据保存目录更新分类
- 删除未注册的种子（删除数据和种子，如果它没有被交叉种子，否则只会删除种子）
- 自动将交叉种子的种子添加到暂停状态（与[cross-seed脚本](#cross-seed)一起使用）
- 按最低大小重新检查暂停的种子，并在完成后恢复
- 从根目录中删除未被qBittorrent引用的孤立文件
- 为没有硬链接的任何种子打标签，并允许根据最大比率和/或播种时间进行可选清理以删除这些种子和内容

# 其他项目和程序

## Filebot

[FileBot](https://www.filebot.net/) 是一个用于组织和重命名电影、电视剧和动漫的终极工具，还可以获取字幕和艺术品。它智能且易于使用。

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes) 是一个用于识别和处理重复文件的程序。

> TRaSH [也有一份指南](https://trash-guides.info/jdupes) {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= 这将检查重复文件并打印结果的摘要

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= 这将重新创建它们作为硬链接，从而减少重复空间的使用

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md) 是一个 PowerShell 脚本，用于在 Radarr/Sonarr 媒体库中手动搜索未标记特定标签的 n 个项目。n 是此脚本将搜索的项目数量，这样做的好处是您不会频繁使用索引器并被禁止使用 :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager) 是一个用于更新电影、电视剧和集合的元数据信息的 Python 脚本，还可以自动构建集合。

## Tautulli

[Tautulli](https://tautulli.com/) 是一个第三方应用程序，您可以在 Plex 媒体服务器旁边运行它，以监视活动并跟踪各种统计数据。最重要的是，这些统计数据包括已观看的内容、观看者、观看时间和地点以及观看方式。唯一缺少的是“为什么他们观看”，但我不是质疑您观看《冰雪奇缘》42次的人。所有统计数据都以漂亮干净的界面呈现，包括许多表格和图表，这使得向其他人炫耀您的服务器变得容易。

## Tdarr

[Tdarr](https://tdarr.io) 是一个闭源的自托管 Web 应用程序，用于自动化媒体库转码/重编管理，并确保您的文件在编解码器/流/容器等方面完全符合您的需求。设计用于与[Sonarr](/sonarr)/[Radarr](/radarr)一起工作，并以模块化、并行化和可扩展性为目标，您添加的每个库都有自己的转码设置、过滤器和计划。工作进程可以根据需要启动和关闭，并分为3种类型-“通用”、“转码”和“健康检查”。工作进程限制可以由调度程序以及手动管理。

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform) 是一个用于 Sonarr 和 Radarr 的自定义脚本，用于通知 Tdarr 新文件/更改/删除文件，而无需依赖文件系统事件或频繁的磁盘扫描。

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr) 是一个用于从 Plex/Sonarr/Radarr 中删除过时和非活动媒体的工具。当您允许用户通过 Overseerr/Ombi 请求节目，但又不想手动监视可用磁盘空间时，它有助于管理有限的空间。它可配置为仅删除符合您定义的条件的媒体。

## Twitter Connect

在<https://apps.twitter.com/>上创建一个 Twitter 应用程序（如果尚未创建）。

填写强制字段以及回调 URL，将其设置为公开可用的 URL（不是 localhost），它不需要存在，但需要设置，使用<https://sonarr.tv/twitter>或<https://radarr.video>即可。