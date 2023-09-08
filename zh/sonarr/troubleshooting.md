---
title: Sonarr故障排除
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, 故障排除
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
---

# 目录

- [目录](#目录)
- [寻求帮助](#寻求帮助)
- [日志和日志文件](#日志和日志文件)
  - [标准日志位置](#标准日志位置)
  - [更新日志位置](#更新日志位置)
  - [共享日志](#共享日志)
  - [跟踪/调试日志](#跟踪调试日志)
  - [清除日志](#清除日志)
- [多个日志文件](#多个日志文件)
- [从失败的更新中恢复](#从失败的更新中恢复)
  - [确定问题](#确定问题)
    - [迁移问题](#迁移问题)
    - [权限问题](#权限问题)
  - [解决问题](#解决问题)
    - [权限问题](#权限问题)
    - [手动升级](#手动升级)
- [下载和导入](#下载和导入)
  - [测试下载客户端](#测试下载客户端)
  - [测试下载](#测试下载)
  - [测试导入](#测试导入)
  - [常见问题](#常见问题)
    - [预期导入的一个或多个剧集在发布中未导入或丢失](#预期导入的一个或多个剧集在发布中未导入或丢失)
    - [使用Sonarr v2](#使用sonarr-v2)
    - [下载客户端的WebUI未启用](#下载客户端的webui未启用)
    - [使用了错误配置的SSL](#使用了错误配置的ssl)
    - [无法在Windows上看到共享](#无法在windows上看到共享)
    - [映射的网络驱动器不可靠](#映射的网络驱动器不可靠)
    - [Docker和用户、组、所有权、权限和路径](#docker和用户组所有权权限和路径)
    - [远程路径映射](#远程路径映射)
      - [远程挂载或远程同步（Syncthing）](#远程挂载或远程同步syncthing)
    - [库文件夹的权限](#库文件夹的权限)
    - [下载文件夹的权限](#下载文件夹的权限)
    - [下载文件夹和库文件夹不是不同的文件夹](#下载文件夹和库文件夹不是不同的文件夹)
    - [错误的类别](#错误的类别)
    - [压缩的种子](#压缩的种子)
    - [重复下载](#重复下载)
    - [Usenet下载未导入](#usenet下载未导入)
    - [下载客户端清除项目](#下载客户端清除项目)
    - [无法将下载匹配到库项](#无法将下载匹配到库项)
      - [通过抓取历史找到匹配的系列，但系列是通过系列ID匹配的。无法自动导入](#通过抓取历史找到匹配的系列但系列是通过系列id匹配的无法自动导入)
    - [剧集名称为TBA](#剧集名称为tba)
    - [连接超时](#连接超时)
  - [未列出的问题](#未列出的问题)
- [搜索索引器和跟踪器](#搜索索引器和跟踪器)
  - [将日志级别调整到跟踪](#将日志级别调整到跟踪)
  - [测试索引器或跟踪器](#测试索引器或跟踪器)
  - [测试搜索](#测试搜索)
  - [常见问题](#常见问题-1)
    - [未搜索索引器](#未搜索索引器)
    - [命名不规范的发布](#命名不规范的发布)
    - [跟踪器需要RawSearch功能](#跟踪器需要rawsearch功能)
    - [系列需要别名](#系列需要别名)
    - [系列需要XEM映射](#系列需要xem映射)
    - [错误的系列类型](#错误的系列类型)
      - [每日](#每日)
      - [标准](#标准)
      - [动画](#动画)
    - [媒体未监视](#媒体未监视)
    - [查询成功-未返回结果](#查询成功-未返回结果)
    - [错误的类别](#错误的类别-1)
    - [错误的结果](#错误的结果)
    - [缺少结果](#缺少结果)
    - [证书验证](#证书验证)
    - [达到速率限制](#达到速率限制)
    - [IP封禁](#ip封禁)
    - [使用Jackett的/all端点](#使用jackett的all端点)
    - [将NZBHydra2用作单个入口](#将nzbhydra2用作单个入口)
    - [未搜索索引器](#未搜索索引器-1)
    - [Jackett手动搜索找到更多结果](#jackett手动搜索找到更多结果)
    - [未遵守发布配置文件](#未遵守发布配置文件)
    - [未列出的问题](#未列出的问题-1)
  - [错误](#错误)
    - [底层连接被关闭：发送时发生了意外错误](#底层连接被关闭发送时发生了意外错误)
    - [请求超时](#请求超时)
    - [未列出的问题](#未列出的问题-2)

# 寻求帮助

需要帮助吗？没关系，每个人有时都需要帮助。您可以通过以下方式实时获得帮助：

- [<i class="fab fa-discord"></i>&emsp;Discord *官方Sonarr Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *官方Sonarr Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

但在您前往那里并发布帖子之前，请确保您寻求帮助的请求是最好的。清楚地描述问题，并简要描述您的设置，包括操作系统/发行版、.net/Mono版本、Sonarr版本、下载客户端及其版本。**如果您使用的是[Docker](https://www.docker.com/)，请先运行[Docker指南](/docker-guide)，因为它可以解决常见且频繁的路径/权限问题。否则，请准备好[docker compose](/docker-guide#docker-compose)。[如何生成Docker Compose](https://trash-guides.info/compose)** 告诉我们您已经尝试过什么，您已经查看了什么。使用[日志和日志文件](#日志和日志文件)部分将日志级别调整到跟踪，重新创建问题，将相关上下文粘贴到pastebin，并在帖子中包含链接。甚至可以包含一些屏幕截图以突出显示问题。

我们了解得越多，就越容易帮助您。

# 日志和日志文件

还可以查看常见故障排除问题：
- [下载和导入常见问题](#常见问题)
- [搜索索引器和跟踪器常见问题](#常见问题-1)
{.links-list}

如果要求提供调试日志，则您的日志将包含`debug`，如果要求提供跟踪日志，则您的日志将包含`trace`。如果您提供的日志不包含这两者中的任何一个，则它们不是所请求的日志。

- 除非被要求，否则不要共享整个日志文件。
- 除非被要求，否则不要直接上传日志到Discord或将其粘贴为文本墙。
- 请勿将日志作为附件、zip压缩文件或任何其他形式的文件共享。

为了提供好的和有用的共享日志：

> 确保没有运行类似于RSS刷新的垃圾任务
{.is-warning}

1. [将日志级别调整到跟踪（设置 => 通用 => 日志级别或编辑配置文件）](#跟踪调试日志)
2. [清除日志（系统 => 日志 => 清除日志或删除日志文件夹中的所有日志）](#清除日志)
3. 重现问题（重新执行导致问题的操作）
4. [通过UI或文件系统中的日志文件（sonarr.trace.txt）打开跟踪日志文件](#标准日志位置)，找到相关上下文
5. 复制问题之前的大块内容、问题本身和问题之后的大块内容。
6. 使用[Gist](https://gist.github.com/)、[0bin（**确保禁用着色**）](https://0bin.net/)、[PrivateBin](https://privatebin.net/)、[Notifiarr PrivateBin](http://logs.notifiarr.com/)、[Hastebin](https://hastebin.com/)、[Ubuntu的Pastebin](https://pastebin.ubuntu.com/)或类似的网站（不包括下面要避免的网站）共享上述复制的日志

**警告：**
- **不要使用[pastebin.com](https://pastebin.com)，因为它们的过滤器往往会阻止日志。
- 不要使用[pastebin.pl](https://pastebin.pl)，因为他们的网站经常无法访问。
- 不要使用[JustPasteIt](https://justpaste.it/)，因为他们的网站不方便查看日志。
- 不要上传日志文件。
- 不要通过Google Drive、Dropbox或任何其他未在上面提到的网站上传和共享日志。
- 不要压缩（zip、tar（tarball）、7zip等）您的日志。
- 不要共享控制台输出、docker容器输出或除应用程序日志之外的任何内容。

**重要提示：**
- 使用[0bin](https://0bin.net/)时，请确保禁用着色，并在阅读后不要销毁。

- 或者，如果您正在查找旧日志文件中的特定条目，但不确定哪个文件，您可以使用Notepad++。您可以使用Notepad++的“在文件中查找”功能根据需要搜索旧日志文件。
- **仅适用于Unix：** 或者，如果您正在查找旧日志文件中的特定条目，但不确定哪个文件，您可以使用grep。例如，如果您想要查找有关电影/剧集/书籍/歌曲/索引器“Shooter”的信息，可以运行以下命令`grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` 如果您的[Appdata目录](/sonarr/appdata-directory)在您的主文件夹中，则运行：`grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * 这些标志的功能如下
    * -i：忽略大小写
    * -n：显示行号
    * -r：递归检查路径中的所有文件
    * -C：提供在找到的行之前和之后的行数
    * -e：要搜索的模式

```

## 标准日志位置

日志文件位于Sonarr的[Appdata目录](/sonarr/appdata-directory)中的logs/文件夹中。您还可以通过UI在System => Logs => Files中访问日志文件。

> 注意：UI中的日志（“Events”表）与日志文件不同，也不那么有用。如果要求提供日志，请从日志文件而不是表中复制/粘贴。
{.is-info}

## 更新日志位置

更新日志文件位于Sonarr的[Appdata目录](/sonarr/appdata-directory)中的UpdateLogs/文件夹中。

## 共享日志

日志可能很长，很难在论坛或Reddit帖子中阅读，并且在Discord中会产生垃圾信息，因此请使用[Pastebin](https://pastebin.ubuntu.com/)、[Hastebin](https://hastebin.com/)、[Gist](https://gist.github.com)、[0bin](https://0bin.net)或任何其他类似的pastebin网站。通常不需要整个文件，只需要问题/错误之前和之后的一大段上下文即可。不要忘记等待垃圾任务（如RSS同步或库刷新）完成。

## 跟踪/调试日志

您可以在设置 => 通用 => 日志记录中更改日志级别。更改后，Sonarr无需重新启动即可生效。此更改仅影响日志文件，而不影响日志数据库。最新的调试/跟踪日志文件分别命名为`sonarr.debug.txt`和`sonarr.trace.txt`。

如果无法访问UI以设置日志级别，则可以通过编辑AppData目录中的config.xml文件来进行设置。将LogLevel值设置为Debug或Trace，而不是Info。

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## 清除日志

您可以直接从UI中清除日志文件和日志数据库，方法是在System => Logs => Files和System => Logs => Delete（垃圾桶图标）下进行。

# 多个日志文件

Sonarr使用每个限制为1MB的滚动日志文件。当前日志文件始终是`sonarr.txt`，其他文件`sonarr.0.txt`是下一个最新的（数字越大，表示越旧）。此日志文件包含`fatal`、`error`、`warn`和`info`条目。

启用调试日志级别时，还会存在其他`sonarr.debug.txt`滚动日志文件。此日志文件包含`fatal`、`error`、`warn`、`info`和`debug`条目。它通常覆盖40小时的时间段。

启用跟踪日志级别时，还会存在其他`sonarr.trace.txt`滚动日志文件。此日志文件包含`fatal`、`error`、`warn`、`info`、`debug`和`trace`条目。由于跟踪详细程度很高，它通常只覆盖几个小时的时间。

# 从失败的更新中恢复

我们尽一切努力防止升级时出现问题，但如果确实出现问题，这将指导您恢复安装。

## 确定问题

在更新后应用程序无法启动时，最好的查找位置是查看[更新日志](#更新日志位置)，并查看更新是否成功完成。如果没有问题，则下一步是查看常规应用程序日志文件，在尝试重新启动之前，使用[日志记录](/sonarr/settings#logging)和[日志文件](/sonarr/system#log-files)找到它们并增加日志级别。

### 迁移问题

- 迁移错误不会完全相同，但这是一个示例：

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### 权限问题

- 权限问题是由于应用程序无法访问相关临时文件夹和/或应用程序二进制文件夹而导致的。修复权限，以便应用程序运行的用户/组具有适当的访问权限。

- Synology用户可能会遇到Synology的一个bug `Access to the path '/proc/{some number}/maps is denied`

- 在某些NAS上，Synology用户可能会遇到`/tmp`空间不足的问题。您需要为应用程序指定一个不同的`/tmp`路径。请参考SynoCommunity或其他Synology支持渠道寻求帮助。

## 解决问题

在迁移问题发生时，您目前没有太多可以立即做的事情，如果问题是特定于您的（或者还没有任何帖子），请在[我们的subreddit](https://reddit.com/r/sonarr)上创建一个帖子，或者加入我们的[discord](https://discord.sonarr.tv/)，如果有其他人遇到了相同的问题，那么请放心，我们正在解决这个问题。

> 请确保您没有尝试在稳定版本上使用`develop`的数据库。不建议频繁切换分支。{.is-info}

### 权限问题

- 修复权限，确保应用程序运行的用户/组可以访问（读写）`/tmp`和应用程序的安装目录。

- 对于在Synology上遇到`/proc/###/maps`问题的用户，停止Sonarr或其他\*Arr应用程序并进行更新应该可以解决此问题。这是SynoCommunity软件包的问题。

### 手动升级

从我们的网站上获取最新版本。

安装更新（.exe）或解压缩（.zip）内容到现有安装目录，并像往常一样重新运行Sonarr。

# 下载和导入

下载和导入是大多数人遇到问题的地方。从高层次的角度来看，Sonarr需要能够与您的下载客户端进行通信，并且可以访问其下载的文件。支持的下载客户端种类繁多，设置更是千差万别。这意味着虽然有一些常见的设置，但并没有一个“正确”的设置，每个人的设置可能都有所不同。

> **第一步是将日志级别调整为Trace，请参阅[日志和日志文件](#logging-and-log-files)以了解如何调整日志级别和搜索日志。然后，您将重现问题，并使用该时间段的跟踪级别日志来检查问题。**
> 如果有人正在帮助您，请将之前/之后的上下文放在[pastebin](https://0bin.net)、[Gist](https://gist.com)或类似的网站上以供他们查看。
> 它不需要整个文件，也不应该只是错误。您还应该在不运行会产生大量日志的任务的情况下重现问题。
{.is-danger}

当您寻求帮助时，请确保阅读[寻求帮助](#asking-for-help)以便提供我们所需的详细信息。

## 测试下载客户端

确保您的下载客户端正在运行。首先测试下载客户端，如果它无法工作，您将能够在跟踪级别日志中看到详细信息。您应该找到一个可以在浏览器中输入的URL，并查看它是否有效。可能是连接问题，可能表示IP、主机名、端口或防火墙阻止访问有误。也可能是明显的问题，比如用户名、密码或API密钥错误。

## 测试下载

现在我们来尝试下载，选择一个系列的一集并进行手动搜索。选择其中一个文件并尝试下载它。它是否被发送到下载客户端？它是否显示在活动中？在**检查已完成的下载**任务（刷新已监视的下载和处理已监视的下载任务）期间，它是否出现在跟踪级别日志中（大约每分钟运行一次）？它是否在该任务期间被正确解析？排队的下载是否有一个合理的名称？由于某些索引器/跟踪器是按ID搜索的，它可能会将一个具有无法识别的名称的文件排队。

## 测试导入

导入问题几乎总是表现为活动中的一个带有橙色图标的项目，您可以将鼠标悬停在上面以查看错误。如果它们没有显示在活动中，请首先解决此问题。大多数导入错误都是*权限*问题，请记住需要能够在下载文件夹中读取和写入。有时，库文件夹的权限也可能有问题，因此请确保检查两者。

路径错误也是可能的，尽管在正常设置中较少见。理解路径问题的关键是知道从下载客户端通过其API获取下载路径。这在更独特的用例中会成为问题，比如下载客户端在不同的系统上运行（甚至可能是不同的操作系统）。在Docker设置中，如果卷设置不正确，也可能发生此问题。如果您没有控制权，比如种子盒设置，那么远程路径映射是一个好的解决方案。在Docker设置中，修复路径是一个更好的选择。

## 常见问题

以下是一些常见问题。

### 预期的一个或多个剧集没有导入或丢失

- 如果所有剧集都已导入，则最常见的原因是下载了一个季度包，但其中不包含该季度的所有剧集。点击`X`以删除并忽略该发布。
- 对于其他所有问题，一个或多个剧集无法导入。请在UI中查看信息并检查其他常见问题。

### 使用Sonarr v2

Sonarr v2已经终止支持，自2021年3月起不再受支持。它与qBittorrent v4.3.0或更新版本不兼容。请升级到Sonarr v3。

### 下载客户端的WebUI未启用

Sonarr通过下载客户端的API与其进行通信，并通过客户端的WebUI访问它。您必须确保客户端的WebUI已启用，并且其使用的端口不与其他正在使用的客户端端口或系统上正在使用的端口冲突。

### 使用了错误的SSL配置

如果您在本地网络上同时使用实例和下载客户端，请确保未启用SSL加密。有关更多信息，请参见[SSL FAQ条目](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues)。

### 无法在Windows上看到共享

Windows服务的默认用户是`LocalService`，通常无法访问您的共享。编辑服务并将其设置为以您自己的用户身份运行，有关详细信息，请参见FAQ条目[为什么无法在远程服务器上看到我的文件](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server)。

### 映射的网络驱动器不可靠

虽然映射的网络驱动器（如`X:\`）很方便，但它们不如UNC路径（如`\\server\share`）可靠，而且在登录之前也无法使用。根据需要设置您的下载客户端，以便它们使用UNC路径。如果您的库位于共享上，您需要确保根文件夹使用UNC路径。如果您的下载客户端发送到共享文件夹，则需要配置UNC路径，因为获取下载路径是通过下载客户端完成的。您可以继续使用映射的网络驱动器供自己使用，但不要将其用于自动化。

### Docker和用户、组、所有权、权限和路径

Docker增加了另一层容易出错但仍然可以正常工作但存在各种问题的复杂性。不要在这里详细介绍它们，而是阅读这篇维基文章[关于这些自动化软件和Docker](/docker-guide)，它涵盖了用户、组、所有权、权限和路径。它不针对任何特定的Docker系统，而是以高层次的方式介绍这些内容，以便您可以在自己的环境中实施它们。

### 远程路径映射

如果您在Docker中使用Sonarr，而下载客户端在非Docker中（或反之亦然），或者将程序安装在不同的服务器上，则可能需要远程路径映射。

日志将如下所示

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

因此，在Sonarr的容器中，`/volume3/data`不存在或无法访问。

- [设置 => 下载客户端 => 远程路径映射](/sonarr/settings#remote-path-mappings)
- 当您的下载客户端报告已完成数据的路径位于另一台服务器上，或者以\*Arr不处理该文件夹的方式时，需要使用远程路径映射。
- 通常，只有在您的下载客户端在Linux上而\*Arr在Windows上（或反之亦然）时才需要远程路径映射。如果混合使用Docker和本机客户端，或者使用远程服务器，则可能还需要远程路径映射。
- 远程路径映射是一个简单的搜索/替换（它查找REMOTE值，并将其替换为指定主机的LOCAL值）。
- 如果关于错误路径的错误消息不包含REPLACED值，则路径映射未按预期工作。通常的解决方案是添加和删除映射。
- [有关远程路径映射的更多信息，请参见TRaSH的教程](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> 如果\*Arr和您的下载客户端都是Docker容器，很少需要远程路径映射。建议您[查看Docker指南](/docker-guide)和/或[按照TRaSH的教程操作](https://trash-guides.info/hardlinks)
{.is-info}

#### 远程挂载或远程同步（Syncthing）

- 您需要在下载的同时进行同步。并且您需要将本地同步目标设置为在\*Arr导入时可以进行硬链接的方式，这意味着它们需要是相同的文件系统并且看起来是相同的。
  - 在包含不完整和完整文件的较低级别常见文件夹中进行同步。
  - 将其同步到与您的库相同的本地文件系统上，并且看起来像它（Docker和网络共享容易配置错误）。
  - 您希望同步不完整和完整文件，以便当种子客户端执行移动操作时，本地也会反映出这一点，并且所有文件已经“存在”（即使它们仍在下载）。然后，您希望使用硬链接，因为即使在导入完成之前，它们也会完成。
  - 这样，在下载的整个过程中，它都在同步，然后种子客户端移动到tv子文件夹并同步反映出来。这样，下载在宣布完成时大部分都已经“存在”。即使它们还没有完全完成，有了硬链接的可能性，这也是可以的。
  - （可选 - 如果适用和/或需要（例如远程usenet客户端））配置自定义脚本，在导入/下载/升级时删除远程文件。
- 或者，与远程同步设置相比，远程挂载设置要简单得多，但通常速度较慢。
  - 使用sshfs或其他网络文件系统协议挂载远程存储。
  - 确保\*Arr配置为以其用户和组运行，并具有读取或写入访问权限。
  - 配置远程路径映射，以查找REMOTE路径并替换为LOCAL等效路径

### 库文件夹的权限

日志将如下所示

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

不要忘记检查*目标*的权限和所有权。很容易专注于下载的所有权和权限，通常这是与权限相关的问题的原因，但它也可能是目标的问题。检查目标文件夹是否存在。检查目标*文件*是否已经存在，或者无法删除或移动到回收站。检查所有权和权限是否允许复制、硬链接或移动下载的文件。运行Sonarr的用户或组需要能够读取和写入根文件夹。

- 对于Windows用户，这可能是由于运行为服务：
  - Windows服务默认使用“Local Service”帐户运行，默认情况下，此帐户无法访问您的用户主目录，除非手动分配了权限。当使用配置为下载到您的主目录的下载客户端时，这一点特别重要。
  - “Local Service”通常权限非常有限。因此，如果用户可以保持登录状态，建议将应用程序安装为系统托盘应用程序。安装程序提供了这样的选项。有关如何从服务转换为托盘应用程序的详细信息，请参见FAQ。

- 对于Synology用户，请参考[SynoCommunity的软件包权限文章](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- 非Windows：如果您使用的是NFS挂载，请确保启用了`nolock`。
- 如果您使用的是SMB挂载，请确保启用了`nobrl`。

### 下载文件夹的权限

您将看到类似以下的错误

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

或者

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

不要忘记检查*源*的权限和所有权。很容易专注于目标的所有权和权限，这是权限相关问题的*可能*原因，但通常是源的问题。检查源文件夹是否存在。检查所有权和权限是否允许复制/硬链接或复制+删除/移动下载的文件。运行Sonarr的用户或组需要能够读取和写入下载文件。

- 对于Windows用户，这可能是由于运行为服务：
  - Windows服务默认使用“Local Service”帐户运行，默认情况下，此帐户无法访问您的用户主目录，除非手动分配了权限。当使用配置为下载到您的主目录的下载客户端时，这一点特别重要。
  - “Local Service”通常权限非常有限。因此，如果用户可以保持登录状态，建议将应用程序安装为系统托盘应用程序。安装程序提供了这样的选项。有关如何从服务转换为托盘应用程序的详细信息，请参见FAQ。

- 对于Synology用户，请参考[SynoCommunity的软件包权限文章](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- 非Windows：如果您使用的是NFS挂载，请确保启用了`nolock`。
- 如果您使用的是SMB挂载，请确保启用了`nobrl`。

### 下载文件夹和库文件夹不是不同的文件夹

- 下载客户端应该下载到一个\*Arr可以访问的文件夹中，而不是您的根/库文件夹；应该从该单独的下载文件夹导入到您的库文件夹中。
- 您不应该直接下载到根文件夹中。您也不应该将根文件夹作为下载客户端的完成文件夹或不完整文件夹。
- [**这也会导致系统中的健康检查**](/sonarr/system#downloading-into-root-folder)
- 在应用程序中，根文件夹被定义为配置的媒体库文件夹。这不是挂载点的根文件夹。您的下载客户端将不完整或完整的下载文件（或正在移动已完成的下载文件）到您的根（库）文件夹中。这经常会导致问题，不建议这样做。要解决此问题，请更改下载客户端，使其不要将下载文件放在根文件夹中。请注意，“放置”还包括如果将下载客户端类别设置为根文件夹，或者如果NZBGet/SABnzbd启用了排序并将其排序到根文件夹。请注意，此检查会查看所有已定义/配置的根文件夹，而不仅仅是当前正在使用的根文件夹。换句话说，您的下载客户端下载到的文件夹或将已完成的下载移动到的文件夹不应该是您在\*Arr应用程序中配置为根/库/最终媒体目标文件夹的相同文件夹。
- 配置的根文件夹（也称为库文件夹）可以在[设置 => 媒体管理 => 根文件夹](/sonarr/settings/#root-folders)中找到。
- 一个例子是，如果您的下载文件放在`\data\downloads`中，那么您设置的根文件夹就是`\data\downloads`。
- 建议使用类似`\data\media\`的路径作为根文件夹/库文件夹，使用`\data\downloads\`作为下载文件夹。

> 您的下载文件夹和根/库文件夹必须是分开的
{.is-warning}

### 错误的类别

Sonarr应该设置使用类别，以便它只尝试处理自己的下载。虽然很少有情况下会添加没有正确类别的种子。如果您手动添加种子并希望处理它们，它们需要具有正确的类别。可以随时设置它，因为Sonarr每分钟都会尝试处理下载。

### 打包的种子

日志将显示以下错误：

```none
找不到适合导入的文件
```

如果您的种子被打包在`.rar`文件中，您需要设置解压。我们推荐使用[Unpackerr](https://github.com/unpackerr/unpackerr)，因为它可以正确解压：防止损坏的部分导入和在导入后清理解压后的文件。

如果文件夹中没有有效的媒体文件，也会出现此错误。

### 重复下载

重复下载的原因有很多，但其中一个与发布配置文件中的索引器限制有关。因为索引器*不会*存储数据，所以对于库中的媒体，任何“首选词”得分都为*零*，但在“RSS”和搜索中，它们将被应用。对于任何“必须包含”或“不能包含”的限制，仅适用于该索引器；其他任何内容都是合法的。这会导致您反复下载项目，因为它看起来像升级，然后不是，然后再次出现并看起来像升级，然后不是。不要将发布配置文件限制为一个索引器。

这也可能是由于下载实际上从未导入，然后从队列中消失，因此新的下载会不断被抓取并且永远不会导入。有关此问题的常见问题和故障排除步骤，请参阅其他各种常见问题。

### Usenet下载未导入

Sonarr只查看SABnzbd和NZBGet中最近的60个下载，因此如果您保留历史记录，这意味着在具有导入问题的大型队列中，下载可能会被静默地错过并且不会导入。避免这种情况的最佳方法是保持您的历史记录清晰，以便任何仍然出现的项目都需要进行调查。您可以通过启用“完成和失败的下载处理程序”下的“删除”来实现这一点。在NZBGet中，这将将项目移动到*隐藏*历史记录中，这非常好。不幸的是，SABnzbd没有类似的功能。在那里，您能做到的最好的是使用nzb备份文件夹。

### 下载客户端清除项目

下载客户端不应负责删除下载。Usenet客户端应该配置为不从历史记录中删除下载。Torrent客户端应该设置为在完成做种后不删除种子（而是暂停或停止）。这是因为Sonarr与下载客户端通信以了解要导入的内容，因此如果它们被*删除*，就没有要导入的内容，即使有一个文件夹里面有文件。

对于SABnzbd，可以使用历史记录保留设置来处理此问题。

### 无法将下载匹配到库项

由于各种原因，一旦抓取并发送到下载客户端，就无法解析发布。在\*Arr的下载客户端类别中，Activity => Options => Show Unknown（在最新版本中默认启用）将显示所有未被忽略/已导入的项目。这些通常需要手动映射和导入。

如果您的下载客户端中存在一个发布，但该媒体项（电影/剧集/书籍/歌曲）在应用程序中不存在，也会发生这种情况。

#### 通过抓取历史记录找到匹配的系列，但是系列是通过系列ID匹配的。无法自动导入

- 此导入错误与上述无法匹配的错误类似。
- Sonarr抓取了该发布，因为您的索引器或跟踪器报告该发布具有您想要的系列的TVDb ID（或IMDb ID）。
- 下载的文件的系列与报告的ID不匹配，因此Sonarr不会导入该文件。
- 根据系列标题和发布名称 - 假设发布与其关联的系列ID正确 - Sonarr可能需要添加一个别名，[此FAQ条目提供了一些更多信息](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) ，说明如何请求添加别名。
- 或者，该发布被错误地标记，不适用于报告的系列ID。应将此问题报告给您的索引器，以便他们采取纠正措施。
- 处理此错误的方法：
  1. 验证文件的系列
  1. 请求别名（如果适用）
  1. 从Activity => Queue手动导入文件（右侧的人形图标）或单击队列中的`X`以忽略客户端中的发布，并可选择将其加入黑名单/可选择从客户端中删除它

### 剧集名称为TBA

在TVDB上，当剧集名称未知时，它们将被命名为TBA，并且API上有一个24小时的缓存。通常，由于TVDB缓存、Skyhook缓存和系列刷新间隔，TVDB网站的更改需要24-48小时才能在Sonarr中生效。

Sonarr中的[Episode Title Required](/sonarr/settings#importing)设置控制当标题为TBA时的导入行为，但是在剧集的播出日期后24小时，即使标题仍为TBA，该发布也将被导入。此外，TBA标题的文件也不会自动进行重命名。

### 底层连接已关闭：发送时发生了意外错误

这是由索引器使用当前.NET版本不支持的SSL协议引起的，可以在[Sonarr => System => Status](/sonarr/system#status)中找到。

### 请求超时

Sonarr无法从客户端获取响应。

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

这也可能是由以下原因引起的：

- 错误配置或使用VPN
- 错误配置或使用代理
- 本地DNS问题 - 尝试更改为不同的DNS提供商
- 本地IPv6问题 - 通常启用了IPv6，但无法正常工作
- 使用Privoxy并且配置不正确

## 未列出的问题

您还可以在我们的指南中查看一些常见的权限和网络故障排除命令。否则，请在Discord上与支持团队讨论。如果这是一个常见问题，请建议将其添加到维基中。

# 搜索索引器和跟踪器

- [为什么Sonarr没有抓取我期望的剧集？](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) FAQ条目可能也有帮助。
- 如果您使用[Prowlarr](/prowlarr)，则可以查看Prowlarr接收到的所有查询的[历史记录](/prowlarr/history)以及它们如何发送到站点。确保在Prowlarr History => Options中启用了`Parameters`。 (i) 图标提供了额外的详细信息。
- 其他故障排除步骤如下

## 将日志级别调整为trace

> **第一步是将日志级别调整为Trace，请参阅[日志和日志文件](#logging-and-log-files)以了解如何调整日志级别和搜索日志。然后，您将重现问题，并使用该时间范围内的跟踪级别日志来检查问题。**如果有人正在帮助您，请将之前/之后的上下文放在[pastebin](https://0bin.net)、[Gist](https://gist.com)或类似的网站上展示给他们。它不需要整个文件，也不应该只是错误。您还应该在不运行会产生大量日志文件的任务的情况下重现问题。
{.is-danger}

## 测试索引器或跟踪器

在测试索引器或跟踪器时，在调试或跟踪日志中可以找到使用的URL。下面是一个成功测试的示例，您可以看到它使用特定的URL和参数查询索引器，然后是响应。您可以在浏览器中测试此URL，例如将`apikey=(removed)`替换为正确的apikey，如`apikey=123`。如果您从索引器获得错误或发现连接问题，可以尝试更改参数。在从自己的浏览器测试后，如果尚未测试过系统正在运行的系统，则应从该系统上进行测试。

## 测试搜索

与上面的索引器/跟踪器测试类似，当您触发搜索时，可以从调试或跟踪级别的日志中获取使用的URL。在测试过程中，最好使用尽可能狭窄的搜索。一个好的方法是手动（交互式）搜索单个剧集或季节，因为它是具体的，您可以在检查日志时在UI中看到结果。手动（交互式）搜索是通过转到一个系列并单击剧集或季节的人形图标来触发的。

在此测试中，您将寻找明显的错误并运行一些简单的测试。您可以看到搜索使用了URL `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1`，您可以在替换(removed)为该索引器的正确apikey后在浏览器中尝试它。它是否有效？您是否看到了预期的结果？是否适用于此FAQ条目？在该URL中，您可以看到它使用`cat=5030,5040,5045,5080`设置了特定的类别，因此如果您没有看到预期的结果，这是一个可能的原因。您还可以看到它使用`tvdbid=354629`按tvdbid进行搜索，因此如果该剧集在索引器上没有正确分类，就需要进行修复。您还可以看到它使用特定的季节和剧集进行搜索，如season=1和ep=1，因此如果索引器上的信息不正确，您将看不到这些结果。请参阅下面的手动搜索XML输出，以查看工作查询的输出示例。

- 手动搜索XML输出

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- 跟踪日志片段

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|正在为 [The Fix : S01E01] 搜索 1 个索引器
2021-03-20 13:15:23.6|Debug|Newznab|正在下载 Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|请求：[GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- 完整的搜索跟踪日志

```none
2022-04-24 20:14:26.7|Info|NzbSearchService|Searching 1 indexers for [Fairy Tail : S02E91 (91)]
2022-04-24 20:14:26.7|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'proxyenabled' defaultValue:'False'
2022-04-24 20:14:27.4|Trace|HttpClient|Res: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91: 200.OK (727 ms)
2022-04-24 20:14:27.4|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|NzbSearchService|Total of 2 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:27.4|Debug|NzbSearchService|Setting last search time to: 11/20/2019 20:14:27
2022-04-24 20:14:27.4|Info|DownloadDecisionMaker|Processing 2 releases
2022-04-24 20:14:27.4|Trace|DownloadDecisionMaker|Processing release 1/2
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.4|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.4|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.4|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.4|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:27.4|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.4|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.4|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.4|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.4|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.4|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.4|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:27.4|Trace|DownloadDecisionMaker|Processing release 2/2
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.4|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.4|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.4|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.4|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:27.4|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.4|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.4|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.4|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.4|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.4|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.4|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'autounmonitorpreviouslydownloadedepisodes' defaultValue:'False'
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'downloadpropersandrepacks' defaultValue:'PreferAndUpgrade'
2022-04-24 20:14:27.4|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (779 ms)
2022-04-24 20:14:27.4|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (779 ms)
```

- Logs will look like

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Searching indexers for [Fairy Tail : S02E91 (91)]. 0 active indexers
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Total of 0 reports were found for [Fairy Tail : S02E91 (91)] from 0 indexers
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|No results found
```

- Note that in the above case there are 0 indexers being searched. This number may very based on your specific setup. If the number is not the same as the number of indexers configured then the following are likely causes:
  - [Health Checks (System => Status)](/sonarr/system#health)
    - [No indexers available with automatic search enabled, Sonarr will not provide any automatic search results](/sonarr/system#no-indexers-available-with-automatic-search-enabled-sonarr-will-not-provide-any-automatic-search-results)
    - [No indexers are enabled](/sonarr/system#no-indexers-are-enabled)
    - [Enabled indexers do not support searching](/sonarr/system#enabled-indexers-do-not-support-searching)
    - [No indexers available with Interactive Search Enabled](/sonarr/system#no-indexers-available-with-interactive-search-enabled)
    - [Indexers are unavailable due to failures](/sonarr/system#indexers-are-unavailable-due-to-failures)
  - Searching a Series Type of Anime and no anime categories are configured for your tracker(s). Indexers have [two different configurable category types](/sonarr/settings#indexers).
  - Searching a Series Type of Daily or Standard are no standard (non-anime) categories are configured for your tracker(s)
    - Categories - Default categories will be used unless edited. It is likely these default categories are suboptimal. Upon editing this setting, Sonarr queries the indexer for its available categories and displays them in a selectable a list. The stale defaults will clear as soon as a category is toggled.
  - Anime Categories - The categories that Sonarr will use for Anime searches No categories will be used unless edited. Upon editing this setting, Sonarr queries the indexer for its available categories and displays them in a selectable a list. The stale defaults will clear as soon as a category is toggled.
  - The Indexer's Capabilities do not support the query type (e.g. Season/Episode, etc.):
    - Within Prowlarr, an indexer's capabilities can be located in the (I) icon for the indexer
    - Jackett does not display a tracker's capabilities within its UI.
  - Trace logs will display information as to why indexers are being ignored if a search is conducted after ***restarting Sonarr***.

### Poorly Named Releases

- Logs will look like

```none
2022-04-24 20:14:26.7|Info|NzbSearchService|Searching 1 indexers for [Fairy Tail : S02E91 (91)]
2022-04-24 20:14:26.7|Debug|Newznab|Downloading Feed https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|HttpClient|Req: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91
2022-04-24 20:14:26.7|Trace|ConfigService|Using default config value for 'proxyenabled' defaultValue:'False'
2022-04-24 20:14:27.4|Trace|HttpClient|Res: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=2&ep=91: 200.OK (727 ms)
2022-04-24 20:14:27.4|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Trace|NewznabRssParser|Parsed: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|NzbSearchService|Total of 2 reports were found for [Fairy Tail : S02E91 (91)] from 1 indexers
2022-04-24 20:14:27.4|Debug|NzbSearchService|Setting last search time to: 11/20/2019 20:14:27
2022-04-24 20:14:27.4|Info|DownloadDecisionMaker|Processing 2 releases
2022-04-24 20:14:27.4|Trace|DownloadDecisionMaker|Processing release 1/2
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.4|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.4|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.4|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.4|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|Parser|Quality parsed: WEBDL-1080p v1
2022-04-24 20:14:27.4|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.1080p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.4|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.4|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-1080p v1
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.1080p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.1080p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.4|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.4|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.4|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.4|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] WEBDL-1080p is not wanted in profile
2022-04-24 20:14:27.4|Trace|DownloadDecisionMaker|Processing release 2/2
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Processing release 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL' from 'NZBgeek'
2022-04-24 20:14:27.4|Debug|Parser|Parsing string 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|Parser|^(?<title>.+?)(?:(?:[-_\W](?<![()\[!]))+S?(?<season>(?<!\d+)(?:\d{1,2})(?!\d+))(?:[ex]|\W[ex]){1,2}(?<episode>\d{2,3}(?!\d+))(?:(?:\-|[ex]|\W[ex]|_){1,2}(?<episode>\d{2,3}(?!\d+)))*)\W?(?!\\)
2022-04-24 20:14:27.4|Debug|Parser|Episode Parsed. Fairy Tail - S02E91
2022-04-24 20:14:27.4|Debug|Parser|Language parsed: English
2022-04-24 20:14:27.4|Debug|QualityParser|Trying to parse quality for Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|Parser|Quality parsed: WEBDL-720p v1
2022-04-24 20:14:27.4|Debug|Parser|Release Group parsed:
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculating preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL'
2022-04-24 20:14:27.4|Trace|PreferredWordService|Calculated preferred word score for 'Fairy.Tail.S02E91.720p.AMZN.WEB-DL': 0
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Beginning size check for: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Possible double episode, doubling allowed size.
2022-04-24 20:14:27.4|Debug|AcceptableSizeSpecification|Item: Fairy.Tail.S02E91.720p.AMZN.WEB-DL, meets size constraints.
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Performing already imported check on report
2022-04-24 20:14:27.4|Debug|AlreadyImportedSpecification|Skipping already imported check for episode without file
2022-04-24 20:14:27.4|Debug|LanguageSpecification|Checking if report meets language requirements. English
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'maximumsize' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MaximumSizeSpecification|Maximum size is not set.
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'minimumage' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|MinimumAgeSpecification|Minimum age is not set.
2022-04-24 20:14:27.4|Debug|QualityAllowedByProfileSpecification|Checking if report meets quality requirements. WEBDL-720p v1
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|Checking if release meets restrictions: Fairy.Tail.S02E91.720p.AMZN.WEB-DL
2022-04-24 20:14:27.4|Debug|ReleaseRestrictionsSpecification|[Fairy.Tail.S02E91.720p.AMZN.WEB-DL] No restrictions apply, allowing
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'retention' defaultValue:'0'
2022-04-24 20:14:27.4|Debug|RetentionSpecification|Checking if report meets retention requirements. 245
2022-04-24 20:14:27.4|Debug|SeriesSpecification|Checking if series matches searched series
2022-04-24 20:14:27.4|Debug|DelaySpecification|Ignoring delay for user invoked search
2022-04-24 20:14:27.4|Debug|HistorySpecification|Skipping history check during search
2022-04-24 20:14:27.4|Debug|MonitoredEpisodeSpecification|Skipping monitored check during search
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'autounmonitorpreviouslydownloadedepisodes' defaultValue:'False'
2022-04-24 20:14:27.4|Debug|DownloadDecisionMaker|Release accepted
2022-04-24 20:14:27.4|Trace|ConfigService|Using default config value for 'downloadpropersandrepacks' defaultValue:'PreferAndUpgrade'
2022-04-24 20:14:27.4|Trace|Http|Res: 66 [GET] /api/v3/release?episodeId=1: 200.OK (779 ms)
2022-04-24 20:14:27.4|Debug|Api|[GET] /api/v3/release?episodeId=1: 200.OK (779 ms)
```

- This indicates that Sonarr is able to find releases for the episode, but they are not being processed because they do not match the naming pattern expected by Sonarr.
- To resolve this issue, you can try the following:
  - Check the [Series Type](/sonarr/series/#series-type) of the series in Sonarr. Make sure it is set correctly (e.g., Anime, Daily, Standard).
  - Check the [Series Editor](/sonarr/series/#series-editor) in Sonarr. Make sure the series is correctly mapped to the correct TVDB series ID.
  - Check the [Release Profile](/sonarr/settings/#profiles) in Sonarr. Make sure the quality and restrictions settings are configured correctly.
  - If the releases are consistently named in a different format, you can try adding a [Custom Format](/sonarr/settings/#custom-formats) in Sonarr to match the naming pattern of the releases.
  - If the releases are consistently named in a different language, you can try adding a [Language Profile](/sonarr/settings/#profiles) in Sonarr to match the language of the releases.
  - If the releases are consistently named in a different quality format, you can try adding a [Quality Profile](/sonarr/settings/#profiles) in Sonarr to match the quality of the releases.
  - If the releases are consistently named in a different release group format, you can try adding a [Release Profile](/sonarr/settings/#profiles) in Sonarr to match the release group of the releases.
  - If the releases are consistently named in a different season/episode format, you can try adding a [Season Pass](/sonarr/series/#season-pass) in Sonarr to match the season/episode of the releases.
  - If the releases are consistently named in a different language, quality, release group, or season/episode format, you may need to manually search for and add the releases to Sonarr.

- 不支持系列打包
- 不支持多季打包
- 在许多情况下，Sonarr无法将返回的结果与已知系列匹配。在这些情况下，您的日志将类似于下面的内容。这些需要手动获取并可能需要手动导入。在日志中查看的关键短语是`|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### 追踪器需要原始搜索功能

- Sonarr正在搜索`9 1 1`，但您的追踪器只有`9-1-1`或`John s Show`和`John's Show`的结果
- 这是因为您的追踪器不支持正常的标准化搜索。
- 解决方案是更新您的追踪器定义的搜索功能，指示它[需要并支持`RawSearch`](https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackett支持此标志，但需要根据每个索引器更新功能。为Jackett提出一个功能请求，以为您的索引器添加此功能。
- Prowlarr支持此标志，但需要根据每个索引器更新功能。为Prowlarr提出一个功能请求，以为您的索引器添加此功能。

### 系列需要别名

发布可能以`The Series Name`的形式上传，但TVDB将系列显示为`Series Name`或类似的命名差异。请参阅[此常见问题解答条目](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x)

### 系列需要XEM映射

发布可能以`Series Title S02E45`或`Other Series Title S2022E42`的形式上传，但TVDB将此剧集显示为`Series Title S03E01`或`Other Series Title S03E42`。请参阅[此常见问题解答条目](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

### 错误的系列类型

系列类型会影响Sonarr的搜索方式。应根据系列在索引器上的发布方式选择系列类型。
[有关更多详细信息，请参阅此常见问题解答条目](/sonarr/faq#whats-the-different-series-types)

> 如果使用**动画**系列类型 - 还可以使用标准类型搜索您的索引器。
{.is-info}

#### 每日

日志将显示`Searching indexers for [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### 标准

日志将显示`Searching indexers for [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### 动画

日志将显示`Searching indexers for [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### 媒体未监视

日志将显示类似以下内容

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

该系列/季/集未被监视。检查系列、季和集的监视状态。

> 只有在所有季的所有剧集都被监视并且季打包升级了所有现有剧集或所有剧集都丢失时，才会抓取季打包。
{.is-info}

### 查询成功 - 未返回结果

您收到类似于`Query successful, but no results were returned from your indexer. This may be an issue with the indexer or your indexer category settings.`的消息

这是由于您的索引器未返回与您为索引器配置的类别相符的任何结果引起的。

### 错误的类别

错误的类别可能是导致在索引器/追踪器的手动搜索中显示结果，但在\*Arr中没有显示的最常见原因。索引器/追踪器应在搜索结果中显示类别，这应该帮助您找出缺少的内容。如果您使用Jackett或Prowlarr，每个追踪器都有一个特定支持的类别列表。确保您在Sonarr中的条目编辑时在一个浏览器窗口中可见该列表。

> 请注意，如果您在索引器设置中将`Anime Categories`留空，则索引器将不会用于动画系列类型的搜索。
> 同样，如果您在索引器设置中将`Categories`留空，则索引器将不会用于标准或每日系列类型的搜索。
{.is-info}

### 错误的结果

有时索引器会返回完全不相关的结果；Sonarr会提供参数来限制搜索到一个系列。有时返回的结果完全不相关。或者有时，大部分相关但有少量错误的结果。第一种情况通常是索引器的问题，您可以从跟踪日志中确定是哪个索引器导致的。您可以禁用该索引器并报告问题。另一种情况通常是分类的发布，可以在索引器/追踪器上报告。

某些追踪器（如EZTV和其他公共追踪器）如果没有与查询的系列/季/集完全匹配的结果，会返回随机结果。这是无法解决的。

### 缺少结果

如果您在网站上找到的结果在Sonarr中没有显示，则您的问题可能是以下几种可能性之一：

- [类别不正确 - 请参见上文](#错误的类别)
- 基于ID（IMDbId、TVDBId等）的搜索正在进行，但索引器没有将发布正确映射到该ID。这是只有您的索引器可以解决的问题。他们需要确保将发布映射到正确的适用ID。
- 没有按照Sonarr的搜索方式进行搜索；很可能您在索引器上搜索的术语不是Sonarr的查询方式。您可以从跟踪日志中查看Sonarr的查询方式。文本查询通常以`q=words%20and%20things%20here`的格式出现，该字符串是经过HTTP编码的，可以使用任何在线的HTML解码/编码工具轻松解码。
- 错过了RSS Feed的新上传的块。日志将显示如下，并且会注意到警告事件。

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### 证书验证

您将通过https连接到大多数索引器/追踪器，因此您的系统需要正确工作。这意味着您的时区和时间都需要设置*正确*。这还意味着您的系统证书需要是最新的。

### 达到速率限制

如果您通过VPN或代理运行，您可能与数十个、数百个或数千个其他人竞争使用诸如、theXEM和/或您的索引器和追踪器等服务。速率限制和DDOS保护通常通过IP地址进行，而您的VPN/代理出口点是*一个*IP地址。除非您在中国、澳大利亚或南非等压制国家，否则您不需要使用VPN/代理。

Rarbg有时会在其API中有某种速率限制，并显示为不返回结果。

### IP封禁

与速率限制类似，某些追踪器（如Nyaa）可能会直接封禁IP地址。这通常是半永久性的，解决方法是从您的ISP或VPN提供商获取新的IP。

### 使用Jackett的/all端点

Jackett的`/all`端点很方便，但这是它的唯一好处。其他一切都可能会出现问题，因此需要单独添加每个追踪器。或者，您可以尝试使用Jackett和NZBHydra2的替代方案[Prowlarr](/prowlarr)

[Jackett甚至表示应避免使用/all，并且不应使用它。](https://github.com/Jackett/Jackett#aggregate-indexers)

使用all端点没有任何优势（除了减少管理开销），只有劣势：

- 您失去了对索引器特定设置（类别、搜索模式等）的控制
- 混合搜索模式（IMDB、查询等）可能会导致低质量的结果
- 无法使用索引器特定类别（\>= 100000）
- 慢速索引器会减慢整体结果
- 总结果限制为1000
- 不相关的结果
- 缺少结果

单独添加每个索引器允许根据每个索引器对类别进行精细调整，这在使用`/all`端点时可能会出现问题，如果使用错误的类别会在某些追踪器上导致错误。在Sonarr中，如果支持分页，则每个索引器的结果限制为1000个，如果不支持分页，则限制为100个，这意味着随着您向Jackett添加越来越多的追踪器，您越来越有可能截断结果。最后，如果`/all`中的*一个*追踪器返回错误，将禁用它，现在您将不会获得任何结果。

### 使用NZBHydra2作为单个条目

将NZBHydra2作为单个索引器条目使用（即在Sonarr中为NZBHydra2添加1个条目，而在NZBHydra2中为多个索引器添加多个条目）与Jackett的`/all`端点存在相同的问题。

### 未搜索到索引器

- 如果索引器似乎没有被搜索到，可能是因为索引器不支持查询类型。最常见的情况是Nyaa仅支持查询搜索，而不支持季/集搜索。跟踪日志在首次搜索后会指示索引器具有或不具有的功能。

### Jackett手动搜索找到更多结果

- [请参阅此常见问题解答条目](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### 未遵守发布配置文件

导致配置文件似乎被忽略的原因有几种。最常见的原因之一是与发布配置文件中的索引器限制相关。因为索引器*不*存储在数据中，所以对于库中的媒体，任何`preferred word`分数都为零，但在“RSS”和搜索期间，它们将被应用。同样，对于任何`must contain`或`must-not`包含的限制，只适用于该索引器；其他任何内容都是合法的。这可能导致发布配置文件似乎被忽略或导致升级循环发生。

### 问题未列出

您还可以在我们的指南中查看一些常见的权限和网络故障排除命令[/permissions-and-networking]。否则，请在Discord上与支持团队讨论。如果这是一个可能是常见问题的问题，请建议将其添加到维基中。

## 错误

这些是在添加索引器时可能遇到的一些常见错误

### 底层连接被关闭：发送时发生了意外错误

这是由索引器使用当前.NET版本不支持的SSL协议引起的，可以在[Sonarr => 系统 => 状态](/sonarr/system#status)中找到。

### 请求超时

Sonarr无法从索引器获取响应。

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

这也可能是由以下原因引起的：

- VPN的配置不正确或使用不正确
- 代理的配置不正确或使用不正确
- 本地DNS问题-尝试更改为不同的DNS提供商
- 本地IPv6问题-通常启用了IPv6，但无法正常工作
- 使用Privoxy并且配置不正确

### 问题未列出

您还可以在我们的指南中查看一些常见的权限和网络故障排除命令[/permissions-and-networking]。否则，请在Discord上与支持团队讨论。如果这是一个可能是常见问题的问题，请建议将其添加到维基中。