---
title: Sonarr快速入门指南
description: 
published: true
date: 2022-07-14T14:07:19.793Z
tags: sonarr, 需要关注
editor: markdown
dateCreated: 2021-09-03T19:14:22.283Z
---

# 目录

- [目录](#目录)
- [快速入门设置指南](#快速入门设置指南)
- [启动](#启动)
- [媒体管理](#媒体管理)
  - [剧集命名](#剧集命名)
  - [导入](#导入)
  - [根文件夹](#根文件夹)
- [配置文件](#配置文件)
- [索引器](#索引器)
- [下载客户端](#下载客户端)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
- [如何导入现有的组织好的媒体库](#如何导入现有的组织好的媒体库)
  - [导入剧集](#导入剧集)
    - [导入现有媒体](#导入现有媒体)
    - [未找到匹配项](#未找到匹配项)
    - [导入后修复错误的文件夹名称](#导入后修复错误的文件夹名称)
- [添加新剧集](#添加新剧集)

# 快速入门设置指南

> 此页面仍在编写中，尚未完成。欢迎贡献

> 要详细了解所有设置，请查看[Sonarr =>设置](/sonarr/settings)页面。
{.is-info}

在本指南中，我们将尝试解释使用Sonarr开始所需的基本设置。我们将跳过一些您在屏幕上可能看到的选项。如果您想深入了解这些选项，请参阅FAQ和文档中的相应页面以获取完整的解释。

> 请注意，在屏幕截图和GUI设置中，`橙色`表示高级选项，因此您需要在页面顶部单击`显示高级`以使其可见。
{.is-warning}

# 启动

安装并启动后，打开浏览器，访问`http://{your_ip_here}:8989`

![qs_startup.png](/assets/sonarr/qs_startup.png)

# 媒体管理

首先，我们将查看`媒体管理`设置，您可以在其中设置首选的命名和文件管理设置。

在左侧菜单中，单击`设置` => `媒体管理`。

## 剧集命名

![qs_episodenaming.png](/assets/sonarr/qs_episodenaming.png)

- 选中复选框以启用重命名剧集。
- 根据您的标准、每日和动画剧集命名约定进行决策。您应该查看推荐的命名约定[这里](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/)。

> 如果您选择不包括质量/分辨率或发布组，那么您将无法在以后重新获得这些信息。强烈建议您在命名方案中包括这些信息。
{.is-info}

## 导入

![mm_importing.png](/assets/sonarr/mm_importing.png)

- （高级选项）如果您希望立即导入TBA剧集，请将“Episode Title Required”更改为“Never”。
- （高级选项）启用`使用硬链接而不是复制`，了解更多信息和示例，请参见[TRaSH的硬链接指南](https://trash-guides.info/hardlinks)。
- 选中复选框以导入额外的文件，并将至少`.srt`添加到列表中。

## 根文件夹

在这里，我们将添加Sonarr将用于导入现有组织好的媒体库的根文件夹，并在下载客户端下载完成后将媒体导入（复制/硬链接/移动）到的位置。这是您的系列和剧集存储的文件夹，供媒体播放器播放。这不是您下载文件的位置！

> \* 非Windows用户：如果您使用NFS挂载，请确保启用了`nolock`。
> \* 如果您使用SMB挂载，请确保启用了`nobrl`。
{.is-warning}

> **您配置Sonarr运行的用户和组必须对此位置具有读写访问权限。**
{.is-info}

> **您的下载文件夹和媒体文件夹不能是同一个位置**
{.is-danger}

不要忘记保存更改！

# 配置文件

`设置` => `配置文件`

我们建议您创建自己的配置文件，并仅选择您实际需要的质量来源。但是，还提供了几个预填充的质量配置文件可供选择。如果您需要有关配置文件的更多信息，请参阅[适当的维基页面](/sonarr/settings#profiles)。

# 索引器

`设置` => `索引器`

在这里，您将添加实际下载任何文件的索引器/跟踪器。

单击<kb>+</kb>按钮添加新的索引器后，将显示一个新窗口，其中包含许多不同的选项。对于Sonarr来说，无论是Usenet索引器还是Torrent跟踪器都被视为“索引器”。

这里有两个部分：Usenet和Torrent。根据您将要使用的下载客户端，您将选择要使用的索引器类型。

大多数Usenet索引器需要API密钥，可以在索引器网站的个人资料页面中找到。

大多数Torrent跟踪器需要在Sonarr中使用[Prowlarr](/prowlarr)或Jackett

至少添加一个索引器，以使Sonarr正常工作。

> 有关更多信息，请参见[设置页面](/sonarr/settings#indexers)和[更多信息（支持的）](/sonarr/supported#indexers)页面的此部分。
{.is-info}

# 下载客户端

`设置` => `下载客户端`

大多数人在下载和导入过程中遇到问题。从高层次的角度来看，软件需要能够与您的下载客户端进行通信，并且可以访问其下载的文件。支持的下载客户端种类繁多，设置更是多种多样。这意味着虽然有一些常见的设置，但没有一个正确的设置，每个人的设置可能会有所不同。但是，有很多错误的设置。

> 有关更多信息，请参见[设置页面](/sonarr/settings#download-clients)、此部分的[更多信息（支持的）](/sonarr/supported#download-clients)页面，以及[TRaSH的下载客户端指南](https://trash-guides.info/Downloaders/)。
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Sonarr将向您的客户端发送下载请求，并将其与您在下载客户端设置中配置的标签或类别名称相关联。
  - 例如：电影、电视、剧集、音乐等。
- Sonarr将通过您的下载客户端的API监视使用该类别名称的活动下载。它通过您的下载客户端的API进行监视。
- 下载完成后，Sonarr将根据下载客户端报告的最终文件位置来确定文件的位置。该文件位置几乎可以是任何地方，只要它与您的媒体文件夹分开，并且Sonarr可以访问。
- Sonarr将扫描该完成的文件位置以查找Sonarr可以使用的文件。它将解析文件名以与请求的媒体进行匹配。如果可以匹配，它将根据您的规格对文件进行重命名，并将其移动到指定的媒体位置。
- 默认情况下启用原子移动（即瞬时移动）。完成下载目录和媒体库的文件系统和挂载点必须相同。如果原子移动失败或者您的设置不支持硬链接和原子移动，则Sonarr将退回并复制文件，然后从源文件中删除，这会增加IO负载。
- 如果在Sonarr的设置中启用了“完成下载处理 - 删除”选项，则会通过向客户端发送请求来将下载的剩余文件发送到垃圾箱或回收站以删除/移除发布。

### BitTorrent

{#bittorrent}

- Sonarr将向您的客户端发送下载请求，并将其与您在下载客户端设置中配置的标签或类别名称相关联。
  - 例如：电影、电视、剧集、音乐等。
- Sonarr将通过您的下载客户端的API监视使用该类别名称的活动下载。此监视通过您的下载客户端的API进行。
- 完成的文件保留在其原始位置，以便您可以进行文件的做种（可以在下载客户端或Sonarr中的特定下载客户端下调整比率或时间）。当文件导入到您的媒体文件夹时，如果您的设置支持硬链接，则Sonarr将创建硬链接；如果不支持硬链接，则进行复制。
- 默认情况下启用硬链接。[硬链接将不使用任何额外的磁盘空间。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)完成下载目录和媒体库的文件系统和挂载点必须相同。如果硬链接创建失败或者您的设置不支持硬链接，则Sonarr将退回并复制文件。
- 如果在Sonarr的设置中启用了“完成下载处理 - 删除”选项，则Sonarr将从您的客户端中删除种子，并要求客户端删除种子数据，但仅在客户端报告种子做种完成且种子已停止（完成后暂停）时。

# 如何导入现有的组织好的媒体库

> 请注意，Sonarr不会定期搜索剧集。请参阅FAQ条目以了解Sonarr的工作原理的详细信息。
[Sonarr如何找到剧集？](/sonarr/faq#how-does-sonarr-find-episodes)
{.is-info}

在设置配置文件/质量大小并添加索引器和下载客户端后，现在是时候导入您现有的组织好的媒体库了。

即将推出 - 欢迎贡献

## 导入现有媒体

根据现有剧集文件夹的命名情况，Sonarr将尝试将其与正确的剧集匹配。在导入之前，请仔细检查此列表。

仅在现有组织好的库上使用库导入，不要在下载文件夹上使用它来进行即时导入。

1. 导航到库导入
1. 阅读并理解库导入帮助文本
1. 选择或添加要从中导入剧集的根（库）文件夹
1. 检查Sonarr对剧集文件夹与TVDb剧集的映射/匹配
1. 根据需要设置监视设置和质量配置文件
1. 单击开始导入

### 未找到匹配项

1. 在系列选择框中搜索系列名称或TVDbId
1. 如果找不到系列，请参阅[此FAQ条目](/sonarr/faq#why-can-i-not-add-a-series)

### 导入后修复错误的文件夹名称

1. 从Sonarr中删除该系列
1. 库导入
1. 确保正确映射该系列

# 添加新剧集

[有关详细信息，请参阅库页面](/sonarr/library#add-new)

# 导入剧集

- 使用Wanted => Manual Import以按需将剧集文件导入其系列文件夹
- 在系列页面上使用Manage Episodes来重新映射或映射现有的剧集文件夹中的剧集文件