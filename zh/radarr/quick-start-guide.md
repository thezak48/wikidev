---
title: Radarr快速入门指南
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, quickstart
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# 目录

- [目录](#目录)
- [快速入门设置指南](#快速入门设置指南)
- [启动](#启动)
- [媒体管理](#媒体管理)
  - [电影命名](#电影命名)
  - [导入](#导入)
  - [文件管理](#文件管理)
  - [根文件夹](#根文件夹)
- [配置文件](#配置文件)
- [质量](#质量)
- [索引器](#索引器)
- [下载客户端](#下载客户端)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [如何导入现有的组织好的媒体库](#如何导入现有的组织好的媒体库)
  - [导入电影](#导入电影)
  - [导入现有媒体](#导入现有媒体)
    - [未找到匹配项](#未找到匹配项)
    - [导入后修复错误的文件夹名称](#导入后修复错误的文件夹名称)
  - [如何添加电影](#如何添加电影)

# 快速入门设置指南

> 此页面仍在制作中，尚未完成。欢迎贡献。

> 要获取更详细的设置说明，请查看[Radarr =>设置](/radarr/settings)页面。
{.is-info}

在本指南中，我们将尝试解释您开始使用Radarr所需的基本设置。我们将跳过屏幕上可能看到的一些选项。如果您想深入了解这些选项，请参阅FAQ和文档中的相应页面以获取完整的解释。

> 请注意，在屏幕截图和GUI设置中，`橙色`表示高级选项，因此您需要在页面顶部单击`显示高级`以使其可见。
{.is-warning}

# 启动

安装并启动后，打开浏览器，转到 `http://{your_ip_here}:7878`

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# 媒体管理

首先，我们将查看`媒体管理`设置，您可以在其中设置首选的命名和文件管理设置。

`设置` => `媒体管理`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## 电影命名

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. 启用/禁用对电影进行重命名（与下载时的名称相同或保留当前名称）。
2. 如果您希望替换或删除非法字符（`\ / : * ? " < > | ~ # % & + { }`）。
3. 此设置将决定Radarr如何处理电影文件中的冒号。
4. 在此处，您将选择实际电影文件的命名约定。
5. *(高级选项) 这是您将设置包含视频文件的文件夹的命名约定。*

> 如果您想要推荐的命名方案和示例，请参阅[TRaSH的推荐命名方案](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/)。
{.is-info}

## 导入

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(高级选项) 启用`使用硬链接而不是复制`，了解更多信息和示例，请参阅[TRaSH的硬链接指南](https://trash-guides.info/hardlinks)。
2. *(高级选项) 导入匹配的附加文件（字幕、nfo等）后导入文件。

## 文件管理

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. 从磁盘中删除的电影将自动在Radarr中取消监视。
    - 您可能想要删除电影，但不希望Radarr重新下载电影。您可以使用此选项。
1. *(高级选项) 指定删除文件的位置（以防您在删除之前想要检索它们）。
1. *(高级选项) 文件在被永久删除之前可以存在的时间。

## 根文件夹

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

在这里，我们将添加Radarr将用于导入现有组织好的媒体库的根文件夹，并在下载客户端下载完成后将媒体导入（复制/硬链接/移动）到该位置。

> \* 非Windows：如果您使用NFS挂载，请确保启用了`nolock`。
> \* 如果您使用SMB挂载，请确保启用了`nobrl`。
{.is-warning}

> **您配置Radarr运行的用户和组必须对此位置具有读写访问权限。** {.is-info}

> 您的下载客户端将下载到下载文件夹，然后Radarr将其导入到您的媒体文件夹（最终目标），您的媒体服务器将使用该文件夹。
{.is-info}

> **您的下载文件夹和媒体（库/根）文件夹不能是同一个位置**。
{.is-danger}

不要忘记保存更改。

# 配置文件

`设置` => `配置文件`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

在这里，您可以配置质量、首选语言和电影下载的自定义格式评分的配置文件。

我们建议您创建自己的配置文件，并仅选择您实际需要的质量来源和语言。

有关外语标题和语言的更多信息，请参阅[此FAQ条目](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)。

许多用户发现[TRaSH的自定义格式语言指南](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats)对于指定他们想要的电影语言非常有帮助。

配置文件还是自定义格式评分的配置位置。强烈建议从[TRaSH的指南](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)中添加以下自定义格式，以避免不必要的下载。有关更多信息，请参阅链接的TRaSH指南自定义格式文章以及集合自定义格式页面顶部引用的其他3个TRaSH自定义格式指南。

- [DV（WEB-DL）](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl)将避免抓取不支持Dolby Vision（DV）的具有绿色色调的发布。
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk)将避免抓取命名不规范的BR-DISK，这些BR-DISK与BR-DISK质量解析不匹配。

> 有关更多信息，请参阅[设置 => 配置文件](/radarr/settings#profiles)。
> 要了解质量来源之间的区别，请查看我们的[质量定义](/radarr/settings#qualities-defined)。
{.is-info}

# 质量

`设置` => `质量`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

在这里，您可以更改/微调所需媒体文件的最小和最大大小（使用Usenet时，请记住RAR/PAR2文件）。

> 如果您需要有关质量设置的帮助，请查看[TRaSH的大小建议](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/)以获取经过测试的示例。
{.is-info}

# 索引器

`设置` => `索引器`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

在这里，您将添加要用于实际下载任何文件的索引器/跟踪器。

单击<kb>+</kb>按钮添加新索引器后，将显示一个新窗口，其中包含许多不同的选项。对于Radarr而言，无论是Usenet索引器还是Torrent跟踪器都被视为“索引器”。

这里有两个部分：Usenet和Torrent。根据您将要使用的下载客户端，您将选择要使用的索引器类型。

对于Torrent跟踪器-几乎所有都需要使用[Prowlarr](/prowlarr)或[Jackett](https://github.com/Jackett/Jackett)。

# 下载客户端

`设置` => `下载客户端`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

下载和导入是大多数人遇到问题的地方。从高层次的角度来看，软件需要能够与您的下载客户端进行通信，并且对下载客户端报告的文件位置具有读写访问权限。支持的下载客户端种类繁多，设置更是千差万别。这意味着虽然有一些常见的设置，但没有一个正确的设置，每个人的设置都可能有所不同。但是，错误的设置却有很多。

> 有关更多信息，请参阅[设置页面](/radarr/settings#download-clients)，[更多信息（支持的）](/radarr/supported#download-clients)页面中的此部分，以及[TRaSH的下载客户端指南](https://trash-guides.info/Downloaders/)。
{.is-info}

## 下载协议 {.tabset}

### Usenet

{#usenet}

- Radarr将向您的客户端发送下载请求，并将其与您在下载客户端设置中配置的标签或类别名称关联起来。
  - 例如：电影、电视、系列、音乐等。
- Radarr将通过您的下载客户端的API监视使用该类别名称的活动下载。
- 下载完成后，Radarr将根据下载客户端报告的最终文件位置来了解该文件的位置。只要该位置与您的媒体文件夹分开且Radarr可以访问，该位置几乎可以是任何地方。
- Radarr将扫描该完成的文件位置以查找Radarr可以使用的文件。它将解析文件名以与请求的媒体进行匹配。如果可以匹配，它将根据您的规范对文件进行重命名，并将其移动到指定的媒体位置。
- 默认情况下启用原子移动（即瞬时移动）。完成下载目录和媒体库的文件系统和挂载点必须相同。如果原子移动失败或者您的设置不支持硬链接和原子移动，则Radarr将退回并复制文件，然后从源文件中删除，这将导致IO密集型操作。
- 如果在Radarr的设置中启用了“完成下载处理 - 删除”选项，则会通过向客户端发送请求来将下载的剩余文件发送到垃圾箱或回收站以删除/移除发布。

### BitTorrent

{#bittorrent}

- Radarr将向您的客户端发送下载请求，并将其与您在下载客户端设置中配置的标签或类别名称关联起来。
  - 例如：电影、电视、系列、音乐等。
- Radarr将通过您的下载客户端的API监视使用该类别名称的活动下载。
- 仍在做种的已完成下载将保留其原始位置，以便您可以继续做种（下载客户端或在Radarr中的特定下载客户端中可以调整比率或时间）。当文件导入到您的媒体文件夹时，如果您的设置支持硬链接，则Radarr将创建硬链接，否则将复制文件。已暂停并完成做种的种子将进行原子移动（如果支持硬链接）或复制+删除（如果不支持硬链接）。
- 默认情况下启用硬链接。[硬链接将不使用任何额外的磁盘空间。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)完成下载目录和媒体库的文件系统和挂载点必须相同。如果硬链接创建失败或者您的设置不支持硬链接，则Radarr将退回并复制文件。
- 如果在Radarr的设置中启用了“完成下载处理 - 删除”选项，则Radarr将从您的客户端中删除种子，并要求客户端删除种子数据，但仅在客户端报告种子做种已完成且种子已停止（完成后暂停）时。

# 如何导入现有的组织好的媒体库

> 请注意，Radarr不会定期搜索电影。有关Radarr工作原理的详细信息，请参阅[Radarr是如何工作的？](/radarr/faq#how-does-radarr-work)FAQ条目。
{.is-info}

在设置配置文件/质量大小并添加索引器和下载客户端后，现在是时候导入您现有的组织好的媒体库了。

`电影`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

选择 `导入现有电影` 或从侧边栏选择 `导入`。

## 导入电影

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

选择您之前在[根文件夹部分](#根文件夹)中添加的根路径。

## 导入现有媒体

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

根据您现有的电影文件夹命名情况，Radarr将尝试将其与正确的电影匹配，如第5点所示。如果您的所有电影都在一个目录中，请按照此[指南](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)操作。

1. 您的电影文件夹名称。
1. 监视 - 您希望如何将电影添加到Radarr中。

- 无 - 不监视电影或集合以获取新发布
- 仅电影 - 仅监视电影以获取新发布
- 电影和集合 - 同时监视电影以获取新发布，并添加和监视电影的集合中的任何电影（如果存在）

1. 可用性 - Radarr何时认为电影可用。

- **已公布**：Radarr将电影视为一旦添加到Radarr即可用。如果您有良好的私人跟踪器且没有伪造品，则*推荐*使用此设置。
- **正在上映**：Radarr将电影视为一旦电影上映即可用。*不推荐*使用此选项。
- **已发布**：Radarr将电影视为一旦蓝光发行即可用。如果您的索引器经常包含伪造品，则*推荐*使用此选项。

1. 质量配置文件 - 选择您首选的配置文件。
1. 电影 - Radarr认为匹配的电影。您必须仔细检查并编辑/搜索以确保匹配正确。匹配不正确通常是由于文件夹命名不规范引起的。
1. 批量选择监视状态。
1. 批量选择最低可用性。
1. 批量选择质量配置文件。
1. 开始导入您的现有媒体库。

一旦电影添加到Radarr中，Radarr将扫描电影文件夹，并尝试将文件夹中的视频文件与电影匹配。Radarr无法匹配文件和电影的最常见原因是文件名中没有年份。Radarr要求文件名中包含年份以进行解析。

### 未找到匹配项

如果您遇到以下错误

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

那么您可能在电影文件夹命名方面犯了错误。

要解决此问题，您可以尝试以下操作

展开错误消息

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

并在[themoviedb](https://www.themoviedb.org/)上检查年份或标题是否匹配。在此示例中，您将注意到年份是错误的，您可以通过更改年份并单击刷新图标来修复它。

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

或者你可以使用tmdb:id或imdb:id（如果tmdb与imdb链接）然后选择找到的电影进行匹配。

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### 导入后修复错误的文件夹名称

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

你会注意到在导入过程中我们进行的修复后，文件夹名称仍然有错误的年份。为了修复这个问题，我们将进行一些魔术操作。

前往电影概览

`电影`

在顶部点击`电影编辑器`

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

激活后，选择你想要重命名文件夹的电影。

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. 如果你想要将所有电影文件夹重命名为之前设置的文件夹命名方案，请设置好之前的[电影命名部分](#电影命名)。
2. 选择你想要重命名文件夹的电影。
3. 选择相同的`根文件夹`

将会显示一个新的弹出窗口

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

选择`是的，移动文件`

然后进行魔术操作

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

如你所见，文件夹已经根据你的命名方案被重命名为正确的年份。

## 如何添加电影

在导入现有的良好组织的媒体库之后，现在是时候添加你想要的电影了。

`电影` => `添加新电影`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

在文本框中输入你想要的电影名称，或者使用tmdb:id或imdb:id。

当输入电影名称时，你会看到它开始显示结果。

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

当你看到你想要的电影时，点击它。

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. 根文件夹 - Radarr将把电影添加到你之前设置的根文件夹中[在根文件夹部分](#根文件夹)
2. 监视 - 你希望如何将电影添加到Radarr中。

- 仅电影 = Radarr将监视RSS订阅源，查找你库中尚未拥有的电影，或将现有电影升级为更高质量的版本。
- 电影和系列 = Radarr将监视RSS订阅源，查找你库中尚未拥有的电影，或将现有电影升级为更高质量的版本。它还将根据你选择的设置添加该电影系列中的所有电影（如果有）。
- 无 = Radarr将不会监视RSS订阅源，任何升级或新电影都将被忽略，必须手动完成。所有未监视电影的搜索必须手动触发搜索或交互式搜索。

1. 可用性 - Radarr何时认为电影可用。

> 有关影响下面可用性的TMDB日期的更多信息，请参阅[Radarr如何确定电影的年份](#radarr如何确定电影的年份)
{.is-info}

- **已宣布**：Radarr将在电影被添加到Radarr后立即认为电影可用。如果你有良好的私人跟踪器（或非常好的公共跟踪器，例如rarbg.to），建议使用此设置，因为它们不会有虚假的电影。
- **上映中**：Radarr将在电影上映后立即认为电影可用（TMDb上的上映日期）。不建议使用此选项。
- **已发布**：Radarr将在蓝光或流媒体版本发布后立即认为电影可用（TMDb上的数字和实体日期）。建议使用此选项，并且可能应与延迟可用性结合使用，例如`-14`或`-21`天。
  - 如果TMDb上没有填写日期，则假定在`上映日期`（最早的上映日期）之后90天，电影将在网络或实体服务中可用。

1. 质量配置文件 - 选择要为此电影使用的配置文件
1. 标签 - 在这里可以添加某些标签以进行高级使用。
1. 添加时搜索 - 如果你希望Radarr在添加到Radarr时搜索缺失的电影，请确保启用此选项[更多信息](/radarr/faq#radarr如何找到电影)
1. 点击`添加电影`将电影添加到Radarr中。

- 如果出现“路径已配置”错误，请参阅[此FAQ条目](/radarr/faq#为现有电影配置的路径已经存在)