---
title: Prowlarr索引器
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

本页面将介绍如何在Prowlarr中添加和配置索引器。

# 添加索引器

要添加索引器，首先点击左侧的`索引器`，然后在页面顶部点击<kb>+</kb> `添加索引器`。

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

从列表中选择您的索引器，或在框中输入部分名称以找到您的索引器。如果您的索引器未列出，您可以尝试使用"通用Newznab"（用于Usenet）或"通用Torznab"（用于种子）。否则，请访问我们的[索引器请求网站](https://requests.prowlarr.com/)。

> 使用`通用Newznab`或`通用Torznab`假定您的索引器支持标准化的*znab格式。如果不支持，则无法正常工作。
{.is-info}

> 注意：几乎每个Usenet站点都与通用Newznab兼容。
{.is-warning}

> 如果您的追踪器或索引器未列出，并且不在我们的[支持的索引器](/prowlarr/supported-indexers)页面上，您可以通过我们的[索引器请求网站](https://requests.prowlarr.com)请求添加。
{.is-info}

# 编辑索引器

要编辑索引器，首先点击左侧的`索引器`，然后点击要编辑的索引器右侧的扳手图标。

# 查看索引器ID或URL

要查看有关索引器的详细信息，首先点击左侧的`索引器`，然后点击索引器名称列中的索引器链接。（以前是右侧的(i)图标）

可用的详细信息可能包括：

- Prowlarr中的ID
- 描述
- 编码
- 语言
- 网站
- Newznab/Torznab Prowlarr URL
- 网站功能

# 索引器设置

选择索引器后，将弹出一个包含您需要配置的进一步信息的窗口。请注意，每个索引器的具体设置会因其所需字段和您配置的索引器类型而略有不同。

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- 名称 - 为此索引器选择一个名称。当它与您的应用程序同步时，它将在名称后面添加“(Prowlarr)”。
- 启用 - 选中此索引器的复选框以启用它。
- 重定向 - 如果需要重定向，选中此复选框。只有少数索引器需要此功能以避免被禁止。如果启用，它将直接将抓取链接传递给应用程序，而不是通过Prowlarr代理。

> 重定向通常只需要用于少数非常特定的索引器。
{.is-info}

- 同步配置文件 - 在此处选择您的同步配置文件。这些可以在[`设置` => `应用程序`](/prowlarr/settings#applications)中创建。标准默认配置文件已经存在，如下所示：

> 您可以通过创建多个索引器实例为每个应用程序设置不同的设置。
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - 选择Prowlarr要使用的URL。如果为空，将使用默认/第一个URL。
- 下载链接 - 如果您添加的是种子索引器，您可能需要选择要使用的下载链接类型。
- （高级选项）API路径 - 索引器的API路径。通常为`/api`。
- 凭据 - 许多索引器和追踪器需要您以某种方式进行身份验证/登录。您可能需要输入API密钥、RSS密钥、会话ID、Cookie或其他来自索引器的凭据（通常在个人资料页面或安全性下找到），选择搜索顺序或其他特定索引器的选项。
  - API密钥
  - RSS密钥
  - 会话ID
  - Cookie
  - 用户名/密码
  - 等等。
- （高级选项）其他参数 - 添加到此索引器请求的其他参数。
- VIP到期时间 - 输入ISO格式的日期（yyyy-MM-DD），在到期前1周收到通知；否则留空。
- 标签 - 使用标签指定默认下载客户端，指定索引器代理，将索引器指定给应用程序或仅用于组织索引器。
- （高级选项）查询限制 - 如果您的索引器限制每天的API请求次数，您可以在此处输入该数字以避免超过限制。
- （高级选项）抓取限制 - 如果您的索引器限制每天的抓取次数，您可以在此处输入该数字以避免超过限制。一旦达到抓取限制，进一步的查询将触发\*Arr应用程序中的未处理异常。其他应用程序可能会有所不同。
- （高级选项）种子比率 - 仅适用于种子索引器：种子在停止之前应达到的比率，留空为应用程序的默认值。
- （高级选项）种子时间 - 仅适用于种子索引器：种子在停止之前应该保种的时间，留空为应用程序的默认值。值以分钟为单位。
- （高级选项）索引器优先级 - 在发布决定方面优先考虑一个索引器而不是另一个的优先级。1是最高优先级，50是最低优先级。这些优先级将与\*Arr应用程序同步。

- 测试您的索引器，如果出现绿色的勾号，表示您可以保存它。保存后，根据您的同步设置，它将自动添加到您的应用程序中。

## 添加自定义YML定义

- 请注意，yml定义会被缓存一段时间，如果您出于开发目的进行更改，则需要等待缓存过期或重新启动Prowlarr。
- 如果您希望为不受支持的索引器添加自定义的Cardigann兼容的YML定义文件，或者测试对现有定义的更改：
  - 导航到[Prowlarr的应用数据文件夹](/prowlarr/appdata-directory)的`Definitions`文件夹中名为`Custom`的自定义索引器定义文件夹（如果不存在，请创建）
    - 示例路径：
      - Windows：`C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux：`/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX：`/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - 将[Cardigann兼容的YML文件](/prowlarr/cardigann-yml-definition)保存到该文件夹中，并确保Prowlarr具有访问权限。

> 定义中的文件名和ID必须是唯一的，并且不能与任何其他现有定义冲突。强烈建议定义中的名称也是唯一的。
{.is-info}

# 支持的索引器

- [请参阅此维基页面，了解最新夜间版本支持的索引器列表。](/prowlarr/supported-indexers/)