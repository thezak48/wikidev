---
title: Prowlarr 快速入门指南
description: 
published: true
date: 2023-04-06T16:04:33.682Z
tags: 
editor: markdown
dateCreated: 2023-04-06T16:04:33.682Z
---

# 目录

- [目录](#目录)
- [索引器](#索引器)
- [应用程序](#应用程序)
  - [应用程序设置](#应用程序设置)
- [下载客户端](#下载客户端)
  - [Usenet 客户端设置](#usenet-客户端设置)
  - [Torrent 客户端设置](#torrent-客户端设置)
  - [测试下载客户端](#测试下载客户端)
- [设置完成](#设置完成)

> 此页面仍在制作中，尚未完成。

> 要获取更详细的设置说明，请查看 [Prowlarr => 设置](/prowlarr/settings)。

在本指南中，我们将尝试解释如何基本设置 Prowlarr 以开始使用。我们将跳过一些您在屏幕上可能看到的选项。如果您想深入了解这些选项，请参阅 FAQ 和文档中的相应页面以获取完整的说明。

> 请注意，在 `橙色` 的屏幕截图和 GUI 设置中是高级选项，因此您需要在页面顶部单击 `显示高级` 以使其可见。

# 索引器

在 Prowlarr 中首先要设置的是索引器。您将逐个将每个索引器添加到 Prowlarr 中。

点击 `索引器`，然后点击 + 添加新的索引器。

![addindexer.png](/assets/prowlarr/addindexer.png)

您可以添加的所有索引器（Usenet 和 Torrent）都列在其中，您可以输入以部分匹配任何现有条目。如果您要添加的索引器在列表中不存在，您可以添加 "Generic Newznab"（用于 Usenet）或 "Generic Torznab"（用于 Torrent）。

![addgeneric.png](/assets/prowlarr/addgeneric.png)

一些索引器有特殊设置，但大多数都是标准设置，如图所示。

![addnewindexer.png](/assets/prowlarr/addnewindexer.png)

- 名称 - 为此索引器选择一个名称。当它与您的应用程序同步时，它将在后面添加 `(Prowlarr)`。
- 启用 - 选中此复选框以启用此索引器。
- 重定向 - 如果需要重定向，请选中此复选框。只有少数索引器需要这样做以避免被禁止。如果启用，它将直接将抓取链接传递给应用程序，而不是通过 Prowlarr 代理。

> 通常只有少数非常特定的索引器需要重定向。

- 同步配置文件 - 在此处选择您的同步配置文件。您可以在 [`设置` => `应用程序`](/prowlarr/settings#applications) 中创建这些配置文件。标准默认配置文件已经存在，如下所示：

> 您可以通过创建多个索引器实例来为每个应用程序设置不同的设置。

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - 选择 Prowlarr 要使用的 URL。如果为空，则使用默认/第一个 URL。
- 下载链接 - 如果您正在添加 Torrent 索引器，您可能需要选择要使用的下载链接类型。
- （高级选项）API 路径 - 索引器的 API 路径。通常为 `/api`。
- 凭据 - 许多索引器和跟踪器需要您以某种方式进行身份验证/登录。您可能需要输入索引器的 API 密钥、RSS 密钥、会话 ID、Cookie 或其他凭据（通常在您的个人资料页面或安全性下找到），选择搜索顺序或其他特定索引器的选项。
  - API 密钥
  - RSS 密钥
  - 会话 ID
  - Cookie
  - 用户名/密码
  - 等等。
- （高级选项）其他参数 - 添加到此索引器请求的其他参数。
- VIP 过期 - 输入 ISO 格式的日期（yyyy-MM-DD），在过期前 1 周通知；否则留空。
- 标签 - 使用标签指定默认下载客户端、指定索引器代理、将索引器指定给应用程序或仅用于组织索引器。
- （高级选项）查询限制 - 如果您的索引器限制每天的 API 请求次数，您可以在此处输入该数字，以避免超过限制。
- （高级选项）抓取限制 - 如果您的索引器限制每天的抓取次数，您可以在此处输入该数字，以避免超过限制。一旦达到抓取限制，进一步的查询将触发 \*Arr 应用程序中的未处理异常。其他应用程序可能会有所不同。
- （高级选项）种子比率 - 仅适用于 Torrent 索引器：种子在停止之前应达到的比率，如果为空，则为应用程序的默认值。
- （高级选项）种子时间 - 仅适用于 Torrent 索引器：种子在停止之前应该持续的时间，如果为空，则为应用程序的默认值。
- （高级选项）索引器优先级 - 在此处选择索引器优先级，范围为 1-50（1 最高）。这些优先级将与您的应用程序同步。

测试您的输入。如果出现绿色的勾号，则可以保存您的输入，并根据需要为您希望 Prowlarr 使用的每个索引器重复此操作。如果失败，则需要检查日志以查找错误（URL、API 密钥等）。

# 应用程序

在添加索引器之后，我们将连接 Prowlarr 到其他应用程序。

点击 `设置` => `应用程序`，然后点击 + 添加支持的应用程序。

![addapps.png](/assets/prowlarr/addapps.png)

列出了您可以添加的所有程序。您只应添加您当前已安装的程序，如果您有多个实例，您必须分别添加每个实例。

> 当前支持的应用程序可以在此部分的 [更多信息（支持的应用程序）](/prowlarr/supported#applications) 页面找到。

添加应用程序时，您需要在弹出屏幕中输入值：

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> 注意：索引器是基于它们声称支持的功能/类别进行同步的。如果一个索引器仅支持 `tv` 类别，则它不会被同步到 Lidarr、Radarr 和 Readarr。它只会被同步到 Sonarr。可以在高级设置中选择 "支持的" 类别作为每个应用程序的高级设置。**还请注意，\*Arrs 仅接受测试查询返回包含至少一个配置的类别的索引器。**
{.is-warning}

## 应用程序设置

- 名称 - 输入此应用程序的名称。
- 同步级别 - 选择要使用的同步级别
  - `仅添加和删除` - 当索引器在 Prowlarr 中添加或删除时，它将更新此远程应用程序。如果索引器在同步时处于离线状态，它将在远程应用程序上被禁用。
  - `完全同步` - 完全同步将完全同步此应用程序的索引器。在 Prowlarr 中对索引器进行的更改将同步到此应用程序。在此应用程序中远程设置的更改将在下次同步时被 Prowlarr 覆盖。用于比较和确定是否应进行同步的因素列表可以在 [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) 中找到。
  - `禁用` - 将阻止索引器与程序同步。

> `完全同步` 意味着 Prowlarr 将覆盖大多数设置，包括在 Prowlarr 中可配置的用户选择的类别。但是，不受 Prowlarr 管理的设置不会被更改。但是，[几乎所有其他更改因素](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) 都会触发同步并覆盖 \*Arr 中的相应设置。
{.is-warning}

- 标签 - 如果您在设置过程中添加了标签到您的索引器，只有带有此标签的索引器才会用于此程序条目。
- Prowlarr 服务器 - 在此处输入 Prowlarr 服务器的 URL（包括 http、端口和基本 URL，如果需要）。
> 请注意，如果您使用的是反向代理，您需要将 URL 基本路径添加到此处！如果不添加，那么当索引器同步时，它们将无法正常工作，如果您选择了仅添加和删除，当您编辑它时，它将无法修复！
- 应用程序服务器 - 在此处输入您的程序的应用程序服务器 URL（包括 http、端口和基本 URL，如果需要）。如果使用了 URL 基本路径，请再次输入完整的 URL。
- API 密钥 - 在此处输入您的程序的 API 密钥。对于 \*Arrs，可以在 设置 => 通用 中找到此密钥。您可以从程序的 `设置` => `通用` 选项卡中获取此密钥，并将其复制/粘贴到此处。
- （高级设置）同步类别 - 选择要同步到此应用程序的类别。支持这些类别的索引器将被同步。
  - 索引器自定义类别将映射到标准的 Torznab/Newznab 类别，因此搜索标准化类别将包含所有底层自定义类别。如果您不想一次性全部使用它们，可以列出索引器自定义类别以进行微调。

> 保存后，它将同步您的索引器到应用程序。它们都将使用您为索引器选择的名称加上 (Prowlarr)。例如：`{索引器名称} (Prowlarr)`

![nzbgeek.png](/assets/prowlarr/nzbgeek.png)

然后，您应该进入您的程序，并禁用非 Prowlarr 版本的索引器。一切运行顺利后，您可以删除那些条目，只保留 (Prowlarr) 版本。

您可能希望进入您的程序并检查 Prowlarr 索引器的类别。默认类别将作为 Prowlarr 中应用程序的高级设置进行映射。

> **请注意，自定义/非标准索引器特定类别将映射到标准类别，因此搜索将包含所有标准类别。**

## 同步配置文件

为（一个）应用程序配置同步配置文件

- 名称 - 同步配置文件的唯一名称
- 启用 RSS - 对于具有此配置文件的索引器，启用 \*Arr 应用程序的 RSS 搜索/查询
- 启用交互式搜索 - 对于具有此配置文件的索引器，启用 \*Arr 应用程序的交互式（手动）搜索
- 启用自动搜索 - 对于具有此配置文件的索引器，启用 \*Arr 应用程序的自动搜索
- 最小种子数 - 对于具有此配置文件的索引器，\*Arr 抓取种子所需的最小种子数

# 下载客户端（Prowlarr 搜索）

> 如果您打算直接在 Prowlarr 中进行搜索，您需要添加下载客户端。否则，您不需要在此处添加它们。对于来自您的应用程序的搜索，将使用在那里配置的下载客户端。

> 下载客户端仅用于 Prowlarr 内部搜索，不会同步到应用程序。目前没有计划添加此类功能。

点击 `设置` => `下载客户端`，然后点击 + 添加新的下载客户端。您的下载客户端应已按照此指南进行配置。

![downloadclients.png](/assets/prowlarr/downloadclients.png)

> 当前支持的下载客户端可以在此部分的 [更多信息（支持的下载客户端）](/prowlarr/supported#downloadclient) 页面找到。

选择要添加的下载客户端，然后会出现一个弹出框以输入连接详细信息。这些详细信息对于大多数客户端来说是相似的。有些会要求输入用户名或密码，有些会要求选择是将新下载添加为暂停/开始状态，等等。
![nzbget.png](/assets/prowlarr/nzbget.png)

> 客户端优先级仅在添加了相同类型（usenet 或 torrent）的 2 个客户端时才有意义。1 是最高优先级，如果存在多个相同类型的客户端且具有相同的优先级，则 Prowlarr 将在它们之间轮流选择。

## Usenet 客户端设置

- 名称 - Prowlarr 中下载客户端的名称
- 启用 - 启用此下载客户端
- 主机 - 您的下载客户端的 URL
- 端口 - 您的下载客户端的端口
- 使用 SSL - 使用安全连接与您的下载客户端通信。请注意这个常见错误。
- URL 基本路径 - 向 URL 添加前缀；这通常用于反向代理。
- API 密钥 - 用于对客户端进行身份验证的 API 密钥
- 用户名 - 用于对客户端进行身份验证的用户名（通常不需要）
- 密码 - 用于对客户端进行身份验证的密码（通常不需要）
- 类别 - Prowlarr 将使用的下载客户端中的类别
- 优先级 - 添加项目的下载客户端优先级
- 客户端优先级 - Prowlarr 中下载客户端的优先级。对于具有相同优先级的相同类型的客户端，将使用轮流选择。

## Torrent 客户端设置

- 名称 - Prowlarr 中下载客户端的名称
- 启用 - 启用此下载客户端
- 主机 - 您的下载客户端的 URL
- 端口 - 您的下载客户端的端口
- 使用 SSL - 使用安全连接与您的下载客户端通信。请注意这个常见错误。
- URL 基本路径 - 向 URL 添加前缀；这通常用于反向代理。
- 用户名 - 用于对客户端进行身份验证的用户名
- 密码 - 用于对客户端进行身份验证的密码
- 类别 - Prowlarr 将使用的下载客户端中的类别
- 优先级 - 添加项目的下载客户端优先级
- 初始状态 - 种子的初始状态（仅适用于 Qbittorrent：强制绕过所有种子阈值）
- 客户端优先级 - Prowlarr 中下载客户端的优先级。对于具有相同优先级的相同类型的客户端，将使用轮流选择。

## 测试下载客户端

测试您的输入。如果出现绿色的勾号，则可以保存您的输入，并根据需要为您希望 Prowlarr 使用的每个下载客户端重复此操作。如果失败，则需要检查日志以查找错误（连接、凭据等）。

# 设置完成

这就是基本设置！您可以根据需要添加通知和其他更高级的设置选项。这些在完整的设置页面中有详细说明。