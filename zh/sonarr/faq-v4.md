---
title: Sonarr v4 Beta 常见问题解答
description: Sonarr v4 Beta 常见问题解答
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# Sonarr v4 Beta 常见问题解答

> Sonarr v4 目前处于测试版阶段，因此可能会出现错误和问题。请使用我们的支持渠道来提问、报告问题或提供 v4 beta 的反馈意见。如果需要，您可能会被要求在 Github 上开启一个问题，如果被要求在 [Github](https://github.com/Sonarr/Sonarr) 上开启一个问题，请提供原始讨论的链接以及所有其他请求的信息。{.is-warning}

## 有什么变化？

有关更多信息，请参阅 [v4 beta 公告](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)。

以下是一些亮点和更显著的变化：

- [强制身份验证](#强制身份验证)
- Mono => Dotnet（更快速；不再使用 mono）。由于此更改，可能需要更新反向代理配置：
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Preferred Words 已删除](#preferred-words-to-custom-formats-migration)，并替换为 Custom Formats
- [语言配置文件已删除](#where-have-language-profiles-gone)，并替换为 Custom Formats
- 暗黑/明亮主题
- SysLog 和实例名称支持
- 将 Mass Editor 合并到 [Series Overview](#where-has-the-mass-editor-gone)
- 还有更多更多

## 强制身份验证

如果 Sonarr 被暴露以便可以从本地网络外部访问其用户界面，则应启用某种形式的身份验证方法以便访问用户界面。这也越来越多地被 Tracker 和 Indexer 所要求。

从 Sonarr v4 开始，身份验证是强制的。

### 身份验证方法

- `Basic`（浏览器弹出窗口）- 当访问 Sonarr 时，此选项将显示一个小弹出窗口，允许您输入用户名和密码。
- `Forms`（登录页面）- 此选项将显示一个类似其他网站的熟悉的登录界面，允许您登录到 Sonarr。
- `External` - 仅可通过配置文件进行配置
  - 如果您使用**外部身份验证**，例如 Authelia、Authetik、NGINX 基本身份验证等，您可以通过关闭应用程序、在 [配置文件](/sonarr/appdata-directory) 中设置 `<AuthenticationMethod>External</AuthenticationMethod>`，然后重新启动应用程序来避免需要双重身份验证。**请注意，文件中的多个 `AuthenticationMethod` 条目不受支持，只会使用最顶部的值**

### 要求进行身份验证

- 如果您不公开应用程序并/或者不希望在本地（例如局域网）访问时需要进行身份验证，则在“设置”=>“常规安全性”=>“身份验证要求”中更改为 `Disabled For Local Addresses`
  - 配置文件中的等效设置是 `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Preferred Words 到 Custom Formats 的迁移

Preferred Words 系统已被 Custom Formats 系统取代。这样可以使 Sonarr 在决策上具有更细粒度的控制。而 Preferred Words 适用于所有质量配置文件，Custom Formats 可以为每个质量配置文件赋予不同的重要性级别。

Custom Formats 还可以设置截止等级，以便在达到所需的优先级水平后停止升级，而旧的 Preferred Words 系统则始终会在找到更好的发布时进行升级。

### 必须（不）包含

在发布配置文件设置中，"必须包含"和"必须不包含"仍然存在，就像在 v3 中一样。

### 文件命名标记

`{Preferred Words}` 命名标记使用文件命名中的正则表达式条目匹配的术语。
`{Custom Formats}` 命名标记使用 Custom Format 名称进行文件命名。

> 建议在升级之前截屏或删除您的 Preferred Words 发布配置文件。每个 Preferred Word 行将在迁移后成为自己的 Custom Format。{.is-warning}

## 语言配置文件去哪了？

在 Sonarr v4 中，语言的处理方式有所不同。它们不再通过旧的语言配置文件系统进行管理，而是现在是 Custom Formats 的一部分。您需要为您想要抓取的语言创建自定义格式，并将这些自定义格式添加到具有适当评分的质量配置文件中以强制抓取该语言。

> 请参阅 TRaSH Guide 的 [如何设置语言自定义格式](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/) 以获取更多信息。{.is-info}

### 仅英语

**来自 [TRaSH => 语言：仅英语](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

如果您只想抓取英语发布，您可以使用以下自定义格式。导入此自定义格式，然后将其分配给每个质量配置文件，并将评分设置为 -10000。假设您的最低自定义格式评分为 0，则这将拒绝所有未解析为英语的发布。

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "语言：仅英语",
  "name": "语言：非英语",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "非英语语言",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 1
      }
    }
  ]
}
```

### 仅原版

**来自 [TRaSH => 语言：仅原版](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

如果您只想抓取以剧集的 TVDb 原始语言发布，您可以使用以下自定义格式。导入此自定义格式，然后将其分配给每个质量配置文件，并将评分设置为 -10000。假设您的最低自定义格式评分为 0，则这将拒绝所有未解析为剧集的 TVDb 原始语言的发布。

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "语言：仅原版",
  "name": "语言：非原版",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "非原版语言",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": -2
      }
    }
  ]
}
```

## 我的反向代理不再工作？

由于 Sonarr 后端的更改（从 mono 到 donnet 的迁移），您的反向代理可能不再起作用。

### Nginx

您的 Nginx 配置文件需要更改。将此行替换为：

```nginx
   proxy_set_header   Host $host;
```

### Apache

您的 Apache 虚拟主机配置文件需要更改。添加此行：

```apache2
  ProxyPreserveHost On
```

## 这个新的“*覆盖并添加到下载队列*”按钮是什么？

在进行交互式搜索时，添加了一个名为“覆盖并添加到下载队列”的第二个下载按钮。此按钮使您可以执行两个操作：

- 选择将下载发送到哪个下载客户端。这在您拥有同一协议的多个下载客户端的情况下非常有用（例如多个种子客户端实例），而不是让 Sonarr 决定使用哪个客户端。
- 覆盖 Sonarr 对发布标题的解析，以防 Sonarr 解析错误或无法解析，但您仍然希望抓取该发布。以下解析字段可以被覆盖：
  - 系列
  - 季数
  - 剧集
  - 质量
  - 语言

## Mass Editor 去哪了？

Mass Editor 独立页面已被删除，其功能已合并到系列概览页面中。要批量编辑节目，请首先单击系列概览页面顶部的“选择系列”按钮，然后选择要编辑的节目。

Season Pass 页面也已被删除。部分功能仍在系列概览编辑器中，选择表格视图并按下“选择系列”。进入选择模式后，将鼠标悬停在季数列中的数字上，以访问该节目的 Season Pass 弹出窗口。

## 剧集的剧集时长显示为 0

v4 使用 TVDb 的每集时长。如果剧集的时长为 0，则会尝试回退到剧集的总时长。
如果剧集的总时长也为 0，则 Sonarr 会将在首个剧集播出后的 24 小时内播出的任何剧集的时长设置为 45。