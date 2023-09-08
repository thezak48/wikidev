---
title: Prowlarr 设置
description: 
published: true
date: 2023-03-30T14:07:39.851Z
tags: 
editor: markdown
dateCreated: 2021-06-06T15:04:48.057Z
---

# 目录

- [目录](#目录)
- [菜单选项](#菜单选项)
- [索引器代理](#索引器代理)
  - [代理设置](#代理设置)
  - [FlareSolverr 代理设置](#flaresolverr-代理设置)
  - [HTTP 代理设置](#http-代理设置)
  - [Socks4 代理设置](#socks4-代理设置)
  - [Socks5 代理设置](#socks5-代理设置)
- [应用程序](#应用程序)
  - [应用程序设置](#应用程序设置)
  - [测试应用程序](#测试应用程序)
- [下载客户端（Prowlarr 搜索）](#下载客户端-prowlarr-搜索)
  - [Usenet 客户端设置](#usenet-客户端设置)
  - [Torrent 客户端设置](#torrent-客户端设置)
  - [测试下载客户端](#测试下载客户端)
- [通知](#通知)
  - [连接](#连接)
  - [通知触发器](#通知触发器)
- [标签](#标签)
- [常规](#常规)
  - [主机](#主机)
  - [安全](#安全)
  - [代理](#代理)
  - [日志记录](#日志记录)
  - [分析](#分析)
  - [更新](#更新)
  - [备份](#备份)
- [用户界面](#用户界面)
  - [日期](#日期)
  - [样式](#样式)
  - [语言](#语言)
  
本页面将介绍 Prowlarr 中所有可用的设置及其工作原理。这不是一个全面的“如何设置 Prowlarr”的指南。如果您需要这样的指南，请使用[快速入门](/prowlarr/quick-start-guide)页面。

# 菜单选项

要进入设置页面，请从左侧菜单中选择“设置”。将提供以下子菜单选项：

![settings_1_menu.png](/assets/prowlarr/settings_1_menu.png)

此外，请注意，对于每个单独的设置页面，菜单顶部有一些选项：

![settings_2_topmenu.png](/assets/prowlarr/settings_2_topmenu.png)

- 隐藏/显示高级选项对于下面标记为“（高级选项）”的项目非常重要，否则它们将不会显示。这些菜单项在截图中以橙色显示。

- 在离开屏幕之前，您必须保存您的更改。通过点击磁盘图标来保存更改。如果您没有进行任何更改，它将显示“无更改”并变为灰色，如上所示。

# 索引器代理

> 有关支持的代理类型的信息，请参阅此部分的[更多信息（支持的）](/prowlarr/supported#indexer-proxies)页面
{.is-info}

在这里，您可以为那些需要代理或 Flaresolverr 配置的索引器添加代理。

导航到 `设置` => `索引器代理`，然后单击 <kb>+</kb> 添加代理。

![proxies.png](/assets/prowlarr/proxies.png)

## 代理设置
  
- 名称 - Prowlarr 中代理的名称
- 标签 - 此代理的标签。代理适用于所有匹配（相同标签）的索引器。如果为空，则此代理适用于所有索引器。

## FlareSolverr 代理设置

- 主机 - 您的 FlareSolverr 实例的完整主机路径（包括 http 和端口）
- （高级设置）请求超时（秒） - Prowlarr 用于 FlareSolverr 请求的[FlareSolver 请求的 `maxTimeout` 值](https://github.com/FlareSolverr/FlareSolverr#-requestget)。必须介于 `1` 秒和 `180` 秒之间（默认值：`60` 秒）

> \* 仅当 Prowlarr 检测到 Cloudflare 时，才会使用 FlareSolverr 代理进行请求
> \* 仅当代理和索引器具有匹配的标签时，才会使用 FlareSolverr 代理进行请求
> \* **如果 Flaresolverr 代理没有配置任何标签或没有具有匹配标签的索引器，则它将被禁用。**
{.is-info}

## HTTP 代理设置

- 主机 - 您的代理的主机地址
- 端口 - 您的代理的端口
- 用户名 - 您的代理的用户名
- 密码 - 您的代理的密码

## Socks4 代理设置

- 主机 - 您的代理的主机地址
- 端口 - 您的代理的端口
- 用户名 - 您的代理的用户名
- 密码 - 您的代理的密码

## Socks5 代理设置

- 主机 - 您的代理的主机地址
- 端口 - 您的代理的端口
- 用户名 - 您的代理的用户名
- 密码 - 您的代理的密码

# 应用程序

> 有关支持的应用程序的信息，请参阅此部分的[更多信息（支持的）](/prowlarr/supported#applications)页面
{.is-info}

在这里，您将添加使用 Prowlarr 的应用程序（如 Radarr、Sonarr、Lidarr、Readarr 等），以及它们如何与 Prowlarr 保持同步。

- 单击 `设置` => `应用程序`，然后单击 <kb>+</kb> 添加应用程序。
- 同步应用程序索引器 - 触发将所有索引器同步到所有应用程序
- 测试所有应用程序 - 触发测试所有应用程序
  
![addapps.png](/assets/prowlarr/addapps.png)

列出了您可以添加的所有程序。您只应添加您当前已安装的程序，如果您有多个实例，您应该分别添加每个实例。

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> 注意：索引器根据它们声称支持的功能/类别进行同步。如果一个索引器仅支持 `tv` 类别，它将不会被同步到 Lidarr、Radarr 和 Readarr。它只会被同步到 Sonarr。可以在每个应用程序的高级设置中选择“支持的”类别。**还要注意，\*Arrs 只接受测试查询返回包含至少一个配置的类别的索引器。**
{.is-info}

## 应用程序设置

- 名称 - 为此应用程序输入一个名称。
- 同步级别 - 选择要使用的同步级别
  - `仅添加和删除` - 当在 Prowlarr 中添加或删除索引器时，它将更新此远程应用程序。如果索引器在同步时处于离线状态，它将在下次同步时在远程应用程序上禁用。
  - `完全同步` - 完全同步将使此应用程序的索引器完全同步。对 Prowlarr 中索引器的更改将同步到此应用程序。在此应用程序中远程设置的 FAQ 上对这些索引器进行的任何更改都将在下次同步时被 Prowlarr 覆盖。有关用于比较和确定是否应进行同步的因素的列表，请参阅[FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `禁用` - 将阻止索引器与程序同步。

> `完全同步` 意味着 Prowlarr 将覆盖大多数设置，包括在 Prowlarr 中可配置的用户选择的类别。但是，不会触及非 Prowlarr 管理的设置。但是，[几乎所有其他更改因素](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)都会触发同步并覆盖 \*Arr 中相应的设置。
{.is-warning}

- 标签 - 如果您在设置过程中添加了标签到您的索引器，只有具有此标签的索引器才会用于此程序条目。
- Prowlarr 服务器 - 输入 Prowlarr 服务器的 URL（包括 http、端口和 baseurl，如果需要）作为应用程序在此处访问它。
> 请注意，如果您使用的是反向代理，您需要将 URL Base 添加到此处！如果不添加，那么当索引器同步时，它们将无法正常工作，如果您选择了仅添加和删除，那么在您编辑它时，它将无法修复！{.is-info}

- 应用程序服务器 - 输入您的程序的应用程序服务器 URL（包括 http、端口和 baseurl，如果需要）在此处。如果使用了完整的 URL Base，请再次输入。
- API 密钥 - 在此处输入您的程序的 API 密钥。对于 \*Arrs，可以在“设置”=>“常规”中找到。您可以从程序的“设置”=>“常规”选项卡中获取此信息，并将其复制/粘贴到此处。
- （高级设置）同步类别 - 选择要同步到此应用程序的类别。支持这些类别的索引器将被同步。
  - 索引器自定义类别将映射到标准的 Torznab/Newznab 类别，因此搜索标准化类别将包括所有底层自定义类别。如果您不想一次性使用它们，可以列出索引器自定义类别以进行精细调整。

## 测试应用程序

测试您的条目。如果出现绿色的勾号，您可以保存您的条目，并根据需要重复为每个您想要与 Prowlarr 同步的程序进行操作。如果失败，您需要检查日志以获取错误信息（URL、API 密钥等）。

## 同步配置文件

配置要用于（一个）应用程序的同步配置文件

> 您可以通过创建多个索引器实例来为每个应用程序设置不同的设置
{.is-info}

- 名称 - 同步配置文件的唯一名称
- 启用 RSS - 对于具有此配置文件的索引器，启用 RSS 搜索/查询 \*Arr 应用程序
- 启用交互式搜索 - 对于具有此配置文件的索引器，启用交互式（手动）搜索 \*Arr 应用程序
- 启用自动搜索 - 对于具有此配置文件的索引器，启用自动搜索 \*Arr 应用程序
- 最小种子数 - 对于具有此配置文件的索引器，\*Arr 抓取种子所需的最小种子数

# 下载客户端（Prowlarr 搜索）

{#download-clients}

> 有关支持的下载客户端的信息，请参阅此部分的[更多信息（支持的）](/prowlarr/supported#download-clients)页面
{.is-info}

如果您打算直接在 Prowlarr 中进行搜索，您需要添加下载客户端。否则，您不需要在此处添加它们。对于来自您的应用程序的搜索，将使用那里配置的下载客户端。

> Prowlarr 不会将下载客户端同步到应用程序。
{.is-info}

单击 `设置` => `下载客户端`，然后单击 <kb>+</kb> 添加新的下载客户端。您的下载客户端应已根据此指南进行配置。

![downloadclients.png](/assets/prowlarr/downloadclients.png)

选择要添加的下载客户端，然后会弹出一个框以输入连接详细信息。这些详细信息对于大多数客户端是相似的。有些会要求用户名或密码，有些会询问是否在暂停/开始状态下添加新下载等。

> 客户端优先级仅在添加了相同类型（usenet 或 torrent）的 2 个客户端时才有意义。1 是最高优先级，如果存在多个具有相同优先级的相同类型的客户端，则 Prowlarr 将在它们之间进行交替。
{.is-info}

## Usenet 客户端设置

- 名称 - Prowlarr 中下载客户端的名称
- 启用 - 启用此下载客户端
- 主机 - 您的下载客户端的 URL
- 端口 - 您的下载客户端的端口
- 使用 SSL - 使用安全连接与您的下载客户端通信。请注意这个常见错误。
- URL 基础 - 为 URL 添加前缀；这通常需要用于反向代理。
- API 密钥 - 用于对客户端进行身份验证的 API 密钥
- 用户名 - 用于对客户端进行身份验证的用户名（通常不需要）
- 密码 - 用于对客户端进行身份验证的密码（通常不需要）
- 类别 - Prowlarr 将使用的下载客户端中的类别
- 优先级 - 添加项目的下载客户端优先级
- 客户端优先级 - Prowlarr 中下载客户端的优先级。对于具有相同优先级的相同类型的客户端，将使用轮询。

## Torrent 客户端设置

- 名称 - Prowlarr 中下载客户端的名称
- 启用 - 启用此下载客户端
- 主机 - 您的下载客户端的 URL
- 端口 - 您的下载客户端的端口；这通常是 WebGUI 端口
- 使用 SSL - 使用安全连接与您的下载客户端通信。请注意这个常见错误。
- URL 基础 - 为 URL 添加前缀；这通常需要用于反向代理。
- 用户名 - 用于对客户端进行身份验证的用户名
- 密码 - 用于对客户端进行身份验证的密码
- 类别 - Prowlarr 将使用的下载客户端中的类别
- 优先级 - 添加项目的下载客户端优先级
- 初始状态 - 种子的初始状态（仅适用于 Qbittorrent：强制绕过所有种子阈值）
- 客户端优先级 - Prowlarr 中下载客户端的优先级。对于具有相同优先级的相同类型的客户端，将使用轮询。

## 测试下载客户端

测试您的条目。如果出现绿色的勾号，您可以保存您的条目，并根据需要重复为每个您希望 Prowlarr 使用的下载客户端进行操作。如果失败，您需要检查日志以获取错误信息（连接、凭据等）。

# 通知

> 有关支持的通知提供程序的信息，请参阅此部分的[更多信息（支持的）](/prowlarr/supported#notifications)页面
{.is-info}

## 连接

连接是您希望 Prowlarr 与外部世界进行通信的方式。

- 通过单击 <kb>+</kb> 按钮，您将看到一个新窗口，可以在其中配置许多不同的端点

- 支持的通知和连接的列表位于[更多信息（支持的）](/prowlarr/supported#notifications)中

## 通知触发器

- 在发布抓取时 - 在 Prowlarr 或 API 中发布抓取时收到通知
  - 包括手动抓取 - 在 Prowlarr UI 中手动触发的抓取时收到通知
- 在健康问题时 - 在健康检查失败时收到通知
  - 包括健康警告 - 除了错误外，还收到健康警告的通知。
- 在应用程序更新时 - 在 Prowlarr 更新到新版本时收到通知

# 标签

- Prowlarr 中的标签部分用于链接 Prowlarr 的不同方面。
- 标签特别适用于：
  - 为需要使用索引器的 Flaresolverr 代理启用；请注意，没有标签的 Flaresolverr 代理将被禁用
  - 为需要使用 HTTP 或 SOCKS 代理的索引器启用
  - 指定索引器到特定的应用程序

# 常规

在这里，您将更改常规应用程序设置，如端口和日志记录级别。

单击 `设置` => `常规`。

> 只有单击屏幕顶部的“显示高级”才能看到这里的许多选项。任何橙色的菜单项只有在启用显示高级时才会显示。
{.is-info}

## 主机

![general_host.png](/assets/prowlarr/general_host.png)

- （高级选项）绑定地址 - 除非您需要更改它，否则将其保留为 `*`。Prowlarr 将侦听的系统 IPv4 地址/主机。 （默认值：`*`）
  - 请注意，`*` 表示任何/所有地址
- 端口号 - Prowlarr 运行的端口。它必须是唯一的。 （默认值：9696）
- BaseUrl - 如果您使用反向代理，您需要在此处添加 URL 基础。 （需要重新启动）（默认值：空）
- （高级选项）实例名称 - 浏览器选项卡和 SysLog（如果已启用）使用的名称（需要重新启动）（默认值：Prowlarr）
- （高级选项）使用 SSL - 如果您使用 https 地址连接到 Prowlarr，请勾选此框。如果您使用 `localhost` 或 IP 地址，几乎永远不要勾选此框。 （默认值：false）
- 启动浏览器（仅限 Windows） - 如果您希望在 Prowlarr 启动时启动浏览器窗口，请勾选此框。 （默认值：是）

## 安全

![general_security.png](/assets/prowlarr/general_security.png)

- 认证 - 您希望如何进行身份验证以访问您的 Prowlarr 实例
  - 无 - 您没有身份验证来访问您的 Prowlarr。通常情况下，如果您是网络的唯一用户，没有任何人在您的网络上关心访问您的 Radarr，或者您的 Radarr 没有暴露在互联网上
  - 基本身份验证（浏览器弹窗）- 当访问您的 Prowlarr 时，将显示一个小弹窗，允许您输入用户名和密码
  - 表单身份验证（登录页面）- 此选项将显示一个类似其他网站的熟悉的登录界面，允许您登录到您的 Prowlarr

- API 密钥 - API 密钥用于外部应用程序访问 Prowlarr。这是秘密的，不应与任何人共享。如果它被共享了，您应该重新生成它并更新您的应用程序。

- 证书验证 - 更改 HTTPS 证书验证的严格程度
  - 已启用 - 验证所有 HTTPS 证书（推荐）
  - 对本地地址禁用 - 验证除本地主机和局域网之外的所有 HTTPS 证书
  - 已禁用 - 不验证任何 HTTPS 证书

## 代理

![general_proxy.png](/assets/prowlarr/general_proxy.png)

代理 - 此选项允许您通过代理运行 Prowlarr 拉取和搜索的信息。如果您所在的国家不允许下载 Torrent 文件，这可能会很有用。

- 使用代理 - 启用以使用代理
- 代理类型 - 选择代理类型（HTTPS、Socks4 或 Socks5）
- 主机名 - 输入代理主机名（不包括 http/https 或任何其他协议）
- 端口 - 输入代理端口
- 用户名 - 如果适用，请输入代理用户名
- 密码 - 如果适用，请输入代理密码
- 忽略的地址 - 输入一个逗号分隔的地址列表，绕过代理
- 对本地地址绕过代理 - 选中此框以绕过代理访问本地地址。

## 日志

![general_logging.png](/assets/prowlarr/general_logging.png)

默认日志级别为 `Info`。这是非常基本的日志记录。您可以在此处更改为更详细的日志记录。日志文件将进行轮转，因此不会占用太多空间。

- 日志级别 - 可能是最有用的故障排除工具之一
  - Info - 这是 Prowlarr 收集信息的最基本方式，其中包括日志中的非常少量信息。此日志文件包含致命、错误、警告和信息条目。
  - Debug - 调试将包括 Info 包含的所有信息以及更多有用的信息。此日志文件包含致命、错误、警告、信息和调试条目。
  - Trace - Prowlarr 上最先进和详细的日志记录，Trace 将包括 Info 和 Debug 收集的所有信息以及更多信息。这是在 Discord 或 Reddit 进行故障排除时最常要求的日志类型。如果您需要帮助，请选择 Trace 日志，并重新执行导致问题的任务以捕获日志。此日志文件包含致命、错误、警告、信息、调试和跟踪条目。

## 分析

![general_analytics.png](/assets/prowlarr/general_analytics.png)

- 分析 - 将匿名使用和错误信息发送到 Prowlarr 的服务器（Servarr）。这包括有关您的浏览器、您使用的 Prowlarr WebUI 页面、错误报告以及操作系统、运行时版本和相关信息的信息。我们将使用此信息来优先处理功能和错误修复。

## 更新

![general_updates.png](/assets/prowlarr/general_updates.png)

- （高级选项）分支 - 这是您正在运行的 Prowlarr 分支。
  - [请参阅此 FAQ 条目获取更多信息](/prowlarr/faq#how-do-i-update-prowlarr)
- 自动 - 自动下载并安装更新。您仍然可以从“系统：更新”安装。注意：Windows 用户始终会自动更新。
- 机制 - 使用 Prowlarr 内置的更新程序或脚本
  - 内置 - 使用 Prowlarr 自己的更新程序
  - 脚本 - 让 Prowlarr 运行更新脚本
  - Docker - 不要从 Docker 内部更新 Prowlarr，而是使用新的更新拉取全新的映像
- 脚本 - 仅当机制设置为脚本时可见 - 更新脚本的路径
- 更新过程 - Prowlarr 将下载更新文件，验证其完整性，并将其提取到临时位置，并调用所选的方法。更新过程将在与 Prowlarr 运行的相同用户下运行，它将需要权限来更新 Prowlarr 文件以及停止/启动 Prowlarr。
- 内置 - 内置方法将备份 Prowlarr 文件和设置，停止 Prowlarr，更新安装并启动 Prowlarr，如果您的系统无法处理停止 Prowlarr 并将尝试自动重新启动它，最好使用脚本。如果更新失败，将重新启动先前版本的 Prowlarr。
- 脚本 - 如果需要处理停止和启动服务（upstart/launchd 等），脚本应该处理与内置更新程序相同的操作，您需要在此处执行。

## 备份

![general_backups.png](/assets/prowlarr/general_backups.png)

- （高级选项）文件夹 - 这允许您选择备份位置。在 Docker 中，您将受到容器允许查看的限制。路径相对于 appdata 文件夹；如果需要，您可以设置绝对路径以备份到 appdata 文件夹之外。
- （高级选项）间隔 - 您希望 Prowlarr 多久进行一次备份
- （高级选项）保留期 - 您希望 Prowlarr 保留每个备份的时间长度。在创建新备份后，最旧的备份将被删除

> 手动备份将永久保留，存储在同一文件夹中，并以不同的名称命名。
{.is-info}

# 用户界面

## 日期

- 短日期格式 - 您希望 Prowlarr 如何显示短日期？
- 长日期格式 - 您希望 Prowlarr 如何显示长日期格式？
- 时间格式 - 您希望使用 12 小时制还是 24 小时制？
- 显示相对日期 - 您希望 Prowlarr 显示相对日期（今天/昨天/等等）还是绝对日期？

## 样式

- 主题 - 选择 Prowlarr 应使用的颜色主题，灵感来自 [Theme.Park](https://github.com/GilbN/theme.park)
- 启用色盲模式 - 修改样式以使色盲用户更好地区分颜色编码的信息

## 语言

- 用户界面语言 - 选择 Prowlarr 在应用程序界面中使用的语言