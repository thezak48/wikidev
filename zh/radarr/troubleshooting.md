---
title: Radarr故障排除
description: Radarr故障排除，包括获取日志文件、搜索故障排除和常见问题，以及下载/导入故障排除和常见问题
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, 故障排除
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
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
    - [数据库磁盘映像损坏](#数据库磁盘映像损坏)
    - [迁移问题](#迁移问题)
    - [UI迁移问题](#ui迁移问题)
    - [权限问题](#权限问题)
  - [解决问题](#解决问题)
    - [迁移问题](#迁移问题)
    - [权限问题](#权限问题)
    - [手动升级](#手动升级)
- [下载和导入](#下载和导入)
  - [测试下载客户端](#测试下载客户端)
  - [测试下载](#测试下载)
  - [测试导入](#测试导入)
  - [常见问题](#常见问题)
    - [下载客户端的WebUI未启用](#下载客户端的webui未启用)
    - [使用的SSL配置不正确](#使用的ssl配置不正确)
    - [在Windows上无法看到共享](#在windows上无法看到共享)
    - [映射的网络驱动器不可靠](#映射的网络驱动器不可靠)
    - [Docker和用户、组、所有权、权限和路径](#docker和用户组所有权权限和路径)
    - [远程路径映射](#远程路径映射)
      - [远程挂载或远程同步（Syncthing）](#远程挂载或远程同步syncthing)
    - [库文件夹的权限](#库文件夹的权限)
    - [下载文件夹的权限](#下载文件夹的权限)
    - [下载文件夹和库文件夹不是不同的文件夹](#下载文件夹和库文件夹不是不同的文件夹)
    - [类别不正确](#类别不正确)
    - [打包的种子](#打包的种子)
    - [重复下载](#重复下载)
    - [Usenet下载未导入](#usenet下载未导入)
    - [下载客户端清除项目](#下载客户端清除项目)
    - [下载无法匹配到库项目](#下载无法匹配到库项目)
    - [连接超时](#连接超时)
  - [未列出的问题](#未列出的问题)
- [搜索索引器和跟踪器](#搜索索引器和跟踪器)
  - [将日志级别调高到跟踪](#将日志级别调高到跟踪)
  - [测试索引器或跟踪器](#测试索引器或跟踪器)
  - [测试搜索](#测试搜索)
  - [常见问题](#常见问题-1)
    - [跟踪器需要RawSearch权限](#跟踪器需要rawsearch权限)
    - [媒体未监视](#媒体未监视)
    - [错误的类别](#错误的类别)
    - [查询成功-没有返回结果](#查询成功-没有返回结果)
    - [错误的结果](#错误的结果)
    - [缺失的结果](#缺失的结果)
    - [证书验证](#证书验证)
    - [达到速率限制](#达到速率限制)
    - [IP被封禁](#ip被封禁)
    - [年份不匹配](#年份不匹配)
    - [缺失的年份](#缺失的年份)
    - [使用Jackett的/all端点](#使用jackett的all端点)
    - [使用NZBHydra2作为单个入口](#使用nzbhydra2作为单个入口)
    - [未列出的问题](#未列出的问题-1)
  - [错误](#错误)
    - [底层连接被关闭：发送时发生了意外错误](#底层连接被关闭发送时发生了意外错误)
    - [请求超时](#请求超时)
    - [未列出的问题](#未列出的问题-2)

# 寻求帮助

需要帮助吗？没关系，每个人有时都需要帮助。您可以通过以下方式实时获取帮助：

- [<i class="fab fa-discord"></i>&emsp;Discord *官方Radarr Discord*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *官方Radarr Subreddit*](https://reddit.com/r/radarr)
{.links-list}

但在您前往那里并发布帖子之前，请确保您的求助请求尽可能完善。清楚地描述问题，并简要描述您的设置，包括操作系统/发行版、.NET版本、Radarr版本、下载客户端及其版本。**如果您使用的是[Docker](https://www.docker.com/)，请先按照[Docker指南](/docker-guide)解决常见和频繁的路径/权限问题。否则，请准备好[docker compose](/docker-guide#docker-compose)。[如何生成Docker Compose](https://trash-guides.info/compose)** 告诉我们您已经尝试过什么，您已经查看了什么。使用[日志和日志文件](#日志和日志文件)部分将日志级别调高到跟踪，重现问题，将相关上下文粘贴到pastebin，并在帖子中包含链接。甚至可以包含一些屏幕截图以突出显示问题。

我们了解得越多，就越容易帮助您。

# 日志和日志文件

还可以查看常见的故障排除问题：
- [下载和导入常见问题](#常见问题)
- [搜索索引器和跟踪器常见问题](#常见问题-1)
{.links-list}

如果要求提供调试日志，则您的日志将包含`debug`，如果要求提供跟踪日志，则您的日志将包含`trace`。如果您提供的日志中没有包含这两者，则它们不是所要求的日志。

- 除非要求，否则不要共享整个日志文件。
- 除非要求，不要直接上传日志到Discord或将其粘贴为文本墙。
- 请勿将日志作为附件、zip归档文件或任何其他形式的文件共享，只能通过下面提到的服务共享文本。

为了提供好的和有用的共享日志：

> 确保没有运行类似于RSS刷新的垃圾任务
{.is-warning}

1. [将日志级别调高到跟踪（设置 => 通用 => 日志级别或编辑配置文件）](#跟踪调试日志)
2. [清除日志（系统 => 日志 => 清除日志或删除日志文件夹中的所有日志）](#清除日志)
3. 重现问题（重新执行导致问题的操作）
4. [通过UI或文件系统中的日志文件（radarr.trace.txt）打开跟踪日志文件](#标准日志位置)，找到相关的上下文
5. 复制问题之前的大块内容、问题本身和问题之后的大块内容。
6. 使用[Gist](https://gist.github.com/)、[0bin（**确保禁用着色**）](https://0bin.net/)、[PrivateBin](https://privatebin.net/)、[Notifiarr PrivateBin](http://logs.notifiarr.com/)、[Hastebin](https://hastebin.com/)、[Ubuntu的Pastebin](https://pastebin.ubuntu.com/)或类似的网站（请勿使用下面提到的网站）共享上述复制的日志

**警告：**
- **不要使用[pastebin.com](https://pastebin.com)，因为它们的过滤器往往会阻止日志。
- 不要使用[pastebin.pl](https://pastebin.pl)，因为他们的网站经常无法访问。
- 不要使用[JustPasteIt](https://justpaste.it/)，因为他们的网站不方便查看日志。
- 不要上传日志文件。
- 不要通过Google Drive、Dropbox或任何其他未在上面提到的网站上传和共享日志。
- 不要归档（zip、tar（tarball）、7zip等）您的日志。
- 不要共享控制台输出、Docker容器输出或除应用程序日志之外的任何内容

**重要提示：**
- 使用[0bin](https://0bin.net/)时，请确保禁用着色，并在阅读后不要销毁。

- 或者，如果您正在查找旧日志文件中的特定条目，但不确定哪个文件，您可以使用Notepad++。您可以使用Notepad++的“在文件中查找”功能按需搜索旧日志文件。
- **仅适用于Unix：** 或者，如果您正在查找旧日志文件中的特定条目，但不确定哪个文件，您可以使用grep。例如，如果您想要查找有关电影/节目/书籍/歌曲/索引器“Shooter”的信息，可以运行以下命令`grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` 如果您的[Appdata目录](/radarr/appdata-directory)在您的主文件夹中，则运行：`grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * 标志的功能如下
    * -i：忽略大小写
    * -n：显示行号
    * -r：递归检查路径中的所有文件
    * -C：提供找到的行之前和之后的行数
    * -e：要搜索的模式

```

## 标准日志位置

日志文件位于Radarr的[Appdata目录](/radarr/appdata-directory)中的logs/文件夹中。您还可以通过UI访问日志文件，路径为System => Logs => Files。

> 注意：UI中的日志（"Events"）表格与日志文件不同，也不那么有用。如果要求提供日志，请从日志文件而不是表格中复制/粘贴。
{.is-info}

## 更新日志位置

更新日志文件位于Radarr的[Appdata目录](/radarr/appdata-directory)中的UpdateLogs/文件夹中。

## 共享日志

日志可能很长，很难在论坛或Reddit帖子中阅读，并且在Discord中它们会产生垃圾信息，因此请使用[Pastebin](https://pastebin.ubuntu.com/)、[Hastebin](https://hastebin.com/)、[Gist](https://gist.github.com)、[0bin](https://0bin.net)或任何其他类似的pastebin网站。通常不需要整个文件，只需要问题/错误之前和之后的一段合适的上下文即可。不要忘记等待垃圾任务（如RSS同步或库刷新）完成。

## 跟踪/调试日志

您可以在设置 => 通用 => 日志记录中更改日志级别。更改日志级别后，无需重新启动Radarr即可生效。最新的调试/跟踪日志文件分别命名为`radarr.debug.txt`和`radarr.trace.txt`。

如果无法访问UI以设置日志级别，则可以通过编辑AppData目录中的config.xml文件来进行设置。将LogLevel的值设置为Debug或Trace，而不是Info。

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## 清除日志

您可以直接从UI中清除日志文件和日志数据库，路径为System => Logs => Files和System => Logs => Delete（垃圾桶图标）

# 多个日志文件

Radarr使用每个限制为1MB的滚动日志文件。当前日志文件始终为`radarr.txt`，其他文件`radarr.0.txt`是下一个最新的（数字越大，表示越旧）。此日志文件包含`fatal`、`error`、`warn`和`info`条目。

启用调试日志级别时，还会出现额外的`radarr.debug.txt`滚动日志文件。此日志文件包含`fatal`、`error`、`warn`、`info`和`debug`条目。它通常覆盖了40小时的时间段。

启用跟踪日志级别时，还会出现额外的`radarr.trace.txt`滚动日志文件。此日志文件包含`fatal`、`error`、`warn`、`info`、`debug`和`trace`条目。由于跟踪详细程度较高，它通常只覆盖几个小时。

# 从失败的更新中恢复

- 我们尽一切努力防止升级时出现问题，但如果确实出现问题，本节将指导您恢复安装。
- 本节还涵盖了常见的更新后问题。

## 确定问题

- 在更新后应用程序无法启动时，最好的查找位置是查看[更新日志](#更新日志位置)，看看更新是否成功完成。如果没有问题，那么下一步是查看常规应用程序日志文件，在尝试重新启动之前，使用[日志记录](/radarr/settings#logging)和[日志文件](/radarr/system#log-files)找到它们并增加日志级别。
- 最常见的问题是安装应用程序的系统在升级过程中干扰了`/tmp`目录并删除了关键的\*Arr文件，从而导致升级和回滚都失败。在这种情况下，只需在现有的损坏安装上重新安装即可。

### 数据库磁盘映像损坏

- 请参阅我们的[常见问题解答](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)

### 迁移问题

- 迁移错误不会完全相同，但以下是一个示例：

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### UI迁移问题

- 如果在[不受支持的版本/分支](/radarr/faq#can-i-switch-between-branches)之间切换，则可能会遇到类似下面的迁移问题。解决方法是[返回到之前的分支或更高版本](/radarr/faq#how-do-i-update-radarr)，或者为当前版本[恢复备份](/radarr/faq#how-do-i-backuprestore-radarr)。

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### 权限问题

- 权限问题是由于应用程序无法访问相关的临时文件夹和/或应用程序二进制文件夹而导致的。修复权限，以便应用程序运行的用户/组具有适当的访问权限。

- Synology用户可能会遇到Synology的一个bug`访问路径'/proc/{一些数字}/maps被拒绝'`

- Synology用户在某些NAS上可能会遇到`/tmp`空间不足的问题。您需要为应用程序指定一个不同的`/tmp`路径。请参考SynoCommunity或其他Synology支持渠道寻求帮助。

## 解决问题

### 迁移问题

在迁移问题发生时，您目前无法立即采取任何措施。如果问题是特定于您的（或者还没有任何帖子），请在[我们的subreddit](https://reddit.com/r/radarr)上创建一个帖子，或者加入我们的[discord](https://radarr.video/discord)。如果有其他人遇到相同的问题，那么请放心，我们正在解决这个问题。

> 请确保您没有尝试在稳定版本上使用`nightly`的数据库。不建议在不同分支之间切换。{.is-info}

### 权限问题

- 修复权限，确保应用程序运行的用户/组可以访问（读取和写入）`/tmp`和应用程序的安装目录。

- 对于在Synology上遇到`/proc/###/maps`问题的用户，停止Sonarr或其他\*Arr应用程序并进行更新应该可以解决此问题。这是SynoCommunity软件包的问题。

### 手动升级

从我们的网站上获取最新版本。

安装更新（.exe）或将内容（.zip）提取到现有安装上，并像往常一样重新运行Radarr。

# 下载和导入

下载和导入是大多数人遇到问题的地方。从高层次的角度来看，Radarr需要能够与您的下载客户端进行通信，并且可以访问其下载的文件。支持的下载客户端种类繁多，设置更是多种多样。这意味着虽然有一些常见的设置，但并没有一个“正确”的设置，每个人的设置可能都有所不同。

> **第一步是将日志级别调整为Trace，请参阅[日志和日志文件](#logging-and-log-files)以了解如何调整日志级别和搜索日志。然后，您将重现问题，并使用该时间段的跟踪级别日志来检查问题。**如果有人在帮助您，请将上下文从之前/之后的内容放在[pastebin](https://0bin.net)、[Gist](https://gist.com)或类似的网站上展示给他们。不需要整个文件，也不应该只是错误信息。您还应该在不运行会产生大量日志的任务的情况下重现问题。
{.is-danger}

当您寻求帮助时，请确保阅读[寻求帮助](#asking-for-help)，以便为我们提供所需的详细信息。

## 测试下载客户端

确保您的下载客户端正在运行。首先测试下载客户端，如果它无法工作，您将能够在跟踪级别日志中看到详细信息。您应该找到一个可以在浏览器中输入的URL，并查看它是否有效。可能是连接问题，这可能表示IP、主机名、端口或防火墙阻止访问的问题。也可能是明显的问题，比如身份验证问题，您可能输入了错误的用户名、密码或API密钥。请注意，某些种子盒需要使用https、端口443和URL基本路径（高级选项），而不是您的下载客户端的实际端口。

## 测试下载

现在我们来尝试下载，选择一部电影并进行手动搜索。选择其中一个文件并尝试下载它。它是否被发送到下载客户端？它是否显示正确的类别？它是否出现在活动中？它是否在**检查已完成的下载**任务（刷新已监视的下载和处理已监视的下载任务）期间的跟踪级别日志中出现，该任务大约每分钟运行一次？它是否在该任务期间被正确解析？排队的下载是否有一个合理的名称？由于某些索引器/跟踪器是按ID搜索的，它可能会使用无法识别的名称排队。

## 测试导入

导入问题几乎总是表现为活动中的一个带有橙色图标的项目，您可以将鼠标悬停在上面以查看错误。如果它们没有显示在活动中，则需要首先解决此问题，请返回并找出原因。大多数导入错误都是*权限*问题，请记住，需要能够在下载文件夹中读取和写入。有时，库文件夹的权限也可能有问题，因此请务必检查两者。

路径错误也是可能的，尽管在正常设置中较少见。理解路径问题的关键是知道从下载客户端通过其API获取下载路径。这在更独特的用例中会成为问题，比如下载客户端在不同的系统上运行（甚至可能是不同的操作系统）。在Docker设置中，如果卷设置不正确，也可能会出现此问题。在您无法控制的情况下，例如种子盒设置，远程路径映射是一个很好的解决方案。在Docker设置中，修复路径是更好的选择。

## 常见问题

以下是一些常见问题。

### 下载客户端的WebUI未启用

Radarr通过下载客户端的API与其进行通信，并通过客户端的WebUI访问它。您必须确保客户端的WebUI已启用，并且其使用的端口与其他正在使用的客户端端口或系统上正在使用的端口不冲突。

### 使用错误配置的SSL

如果您的实例和下载客户端都在本地网络上使用，并且启用了SSL加密，请确保未启用SSL加密。有关更多信息，请参见[SSL FAQ条目](/radarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues)。

### 无法在Windows上看到共享

Windows服务的默认用户是`LocalService`，通常无法访问您的共享。编辑服务并将其设置为以您自己的用户身份运行，有关详细信息，请参见FAQ条目[为什么无法在远程服务器上看到我的文件](/radarr/faq#why-cant-i-see-my-files-on-a-remote-server)。

### 映射的网络驱动器不可靠

虽然像`X:\`这样的映射的网络驱动器很方便，但它们不像`\\server\share`这样的UNC路径可靠，而且在登录之前也无法使用。根据需要设置和配置下载客户端，以便它们使用UNC路径。如果您的库位于共享上，您需要确保您的根文件夹使用UNC路径。如果您的下载客户端发送到共享，那么您将需要配置UNC路径，因为从下载客户端获取下载路径。您可以将映射的网络驱动器保留供您自己使用，但不要将其用于自动化。

### Docker和用户、组、所有权、权限和路径

Docker增加了另一层容易出错但仍然可以正常工作但存在各种问题的复杂性。不在这里详细介绍它们，而是阅读这篇维基文章[关于这些自动化软件和Docker](/docker-guide)，它涵盖了用户、组、所有权、权限和路径。它不特定于任何Docker系统，而是以高层次的方式介绍这些内容，以便您可以在自己的环境中实施它们。

### 远程路径映射

如果您在Docker中使用Radarr，而下载客户端在非Docker中（或反之亦然），或者将程序安装在不同的服务器上，则可能需要进行远程路径映射。

日志将显示类似于以下内容。

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

因此，在Radarr的容器中，`/volume3/data`不存在或无法访问。

- [设置 => 下载客户端 => 远程路径映射](/radarr/settings#remote-path-mappings)
- 当您的下载客户端报告已完成数据的路径位于另一台服务器上，或者以\*Arr不处理该文件夹的方式时，需要使用远程路径映射。
- 通常，只有在下载客户端在Linux上，而\*Arr在Windows上，或者反之亦然时，才需要远程路径映射。如果混合使用Docker和本机客户端，或者使用远程服务器，则可能还需要远程路径映射。
- 远程路径映射是一个简单的搜索/替换（它查找REMOTE值，并将其替换为指定主机的LOCAL值）。
- 如果关于错误路径的错误消息不包含REPLACED值，则路径映射未按预期工作。通常的解决方法是添加和删除映射。
- [有关远程路径映射的更多信息，请参见TRaSH的教程](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> 如果\*Arr和您的下载客户端都是Docker容器，很少需要远程路径映射。建议您[查看Docker指南](/docker-guide)和/或[按照TRaSH的教程操作](https://trash-guides.info/hardlinks)
{.is-info}

#### 远程挂载或远程同步（Syncthing）

- 您需要在下载的同时进行同步。您需要将本地同步目标设置为在\*Arr导入时可以进行硬链接的位置，这意味着它们需要是相同的文件系统并且看起来是相同的。
  - 在包含不完整和完整内容的较低、公共文件夹中进行同步。
  - 将同步到与您的库相同的本地文件系统上的位置，并且看起来像它（Docker和网络共享易于配置错误）。
  - 您希望同步不完整和完整的内容，以便当种子客户端进行移动时，本地反映了这一点，并且所有文件已经“存在”（即使它们仍在下载）。然后，您希望使用硬链接，因为即使在导入之前完成，它们仍然会完成。
  - 这样，整个下载过程中，它都在同步，然后种子客户端移动到电视子文件夹并同步反映这一点。这样，下载在宣布完成时大部分都已经“存在”。即使它们还没有完全完成，有了硬链接的可能性也是可以的，这仍然是可以的。
  - （可选 - 如果适用和/或需要（例如远程usenet客户端））配置一个自定义脚本，在导入/下载/升级时删除远程文件。
- 或者，与远程同步相比，远程挂载设置要简单得多，但通常速度较慢。
  - 使用sshfs或其他网络文件系统协议挂载远程存储。
  - 确保\*Arr配置为以具有读取或写入访问权限的用户和组运行。
  - 配置远程路径映射，以查找REMOTE路径并替换为LOCAL等效路径

### 库文件夹的权限

日志将显示如下内容

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

不要忘记检查*目标*的权限和所有权。很容易过于关注下载的所有权和权限，通常这是与权限相关的问题的原因，但它也可能是目标的问题。检查目标文件夹是否存在。检查目标*文件*是否已经存在，或者无法删除或移动到回收站。检查所有权和权限是否允许复制、硬链接或移动下载的文件。运行的用户或组需要能够读取和写入根文件夹。

- 对于Windows用户，这可能是由于运行为服务：
  - Windows服务默认在“Local Service”帐户下运行，默认情况下，此帐户无法访问您的用户主目录，除非手动分配了权限。当使用配置为下载到您的主目录的下载客户端时，这一点特别重要。
  - “Local Service”通常具有非常有限的权限。因此，如果用户可以保持登录状态，建议将应用程序安装为系统托盘应用程序。安装程序提供了这样的选项。有关如何从服务转换为托盘应用程序的详细信息，请参见FAQ。

- 对于Synology用户，请参考[SynoCommunity的权限文章](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- 非Windows：如果您使用的是NFS挂载，请确保启用了`nolock`。
- 如果您使用的是SMB挂载，请确保启用了`nobrl`。

### 下载文件夹的权限

日志将显示如下内容

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

不要忘记检查*源*的权限和所有权。很容易过于关注目标的所有权和权限，这是与权限相关的问题的*可能*原因，但通常是源的问题。检查源文件夹是否存在。检查所有权和权限是否允许复制/硬链接或复制+删除/移动下载的文件。运行的用户或组需要能够读取和写入下载文件夹。

- 对于Windows用户，这可能是由于运行为服务：
  - Windows服务默认在“Local Service”帐户下运行，默认情况下，此帐户无法访问您的用户主目录，除非手动分配了权限。当使用配置为下载到您的主目录的下载客户端时，这一点特别重要。
  - “Local Service”通常具有非常有限的权限。因此，如果用户可以保持登录状态，建议将应用程序安装为系统托盘应用程序。安装程序提供了这样的选项。有关如何从服务转换为托盘应用程序的详细信息，请参见FAQ。

- 对于Synology用户，请参考[SynoCommunity的权限文章](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- 非Windows：如果您使用的是NFS挂载，请确保启用了`nolock`。
- 如果您使用的是SMB挂载，请确保启用了`nobrl`。

### 下载文件夹和库文件夹不是不同的文件夹

- 下载客户端应该下载到一个\*Arr可以访问的文件夹，并且不是您的根/库文件夹；应该从该单独的下载文件夹导入到您的库文件夹中。
- 您不应该直接下载到根文件夹。您也不应该将根文件夹用作下载客户端的完成文件夹或不完整文件夹。
- [**这也会导致系统中的健康检查问题**](/radarr/system#downloading-into-root-folder)
- 在应用程序中，根文件夹被定义为配置的媒体库文件夹。这不是挂载的根文件夹。您的下载客户端具有不完整或完整的文件夹（或正在移动已完成的下载到根（库）文件夹）。这经常导致问题，不建议这样做。要解决此问题，请更改下载客户端，使其不将下载放在根文件夹中。请注意，“放置”还包括如果将下载客户端类别设置为根文件夹，或者如果NZBGet/SABnzbd启用了排序并且正在对根文件夹进行排序。请注意，此检查会查看所有已定义/配置的根文件夹，而不仅仅是当前正在使用的根文件夹。换句话说，您的下载客户端下载到的文件夹或将已完成的下载移动到的文件夹不应该是您在\*Arr应用程序中配置的根/库/最终媒体目标文件夹。
- 配置的根文件夹（也称为库文件夹）可以在[设置 => 媒体管理 => 根文件夹](/radarr/settings/#root-folders)中找到
- 一个例子是，如果您的下载存储在`\data\downloads`中，那么您设置了一个根文件夹为`\data\downloads`。

> 您的下载文件夹和根/库文件夹必须是分开的
{.is-warning}

### 类别错误

Radarr应该设置使用一个类别，以便它只尝试处理自己的下载。很少情况下，通过会添加没有正确类别的种子，但这可能会发生。如果您手动添加种子并希望处理它们，它们需要具有正确的类别。可以随时设置它，因为会尝试每分钟处理下载。

### 打包的种子

日志将显示类似于以下错误

```none
No files found are eligible for import
```

如果您的种子被打包在`.rar`文件中，您将需要设置解压。我们推荐使用[Unpackerr](https://github.com/unpackerr/unpackerr)，因为它可以正确地解压：防止损坏的部分导入和在导入后清理解压后的文件。

如果文件夹中没有有效的媒体文件，也会出现此错误。

### 重复下载

有几个原因会导致重复下载，其中之一与自定义格式有关。可能是发布名称与自定义格式匹配，但下载文件不匹配。这会导致你陷入一个循环中，因为它看起来像是一个升级，然后不是，然后再次出现并看起来像是一个升级，然后又不是。根据你的自定义格式，你可以通过在重命名模式中包含自定义格式来解决这个问题。（启用可以在重命名中包含自定义格式，然后将自定义格式添加到你的重命名模式中）

这也可能是由于下载实际上从未导入，然后从队列中消失，因此会不断抓取新的下载并且永远不会导入。请参阅其他常见问题和故障排除步骤。

### Usenet下载未导入

Radarr只查看SABnzbd和NZBGet中最近的60个下载，因此如果你保留下载历史记录，这意味着在具有导入问题的大型队列中，下载可能会被静默地错过并且不会导入。避免这种情况的最佳方法是保持你的历史记录清晰，以便任何仍然出现的项目都需要进行调查。你可以通过启用“已完成”和“已失败的下载处理程序”下的“删除”来实现这一点。在NZBGet中，这将将项目移动到*隐藏*历史记录中，这非常好。不幸的是，SABnzbd没有类似的功能。在那里，你可以使用nzb备份文件夹来实现最佳效果。

### 下载客户端清除项目

下载客户端不应负责删除下载。Usenet客户端应该配置为*不*从历史记录中删除下载。Torrent客户端应该设置为在完成种子后*不*删除种子（而是暂停或停止）。这是因为Radarr与下载客户端通信以了解要导入的内容，因此如果它们被*删除*，就没有要导入的内容...即使有一个文件夹里面有文件。

对于SABnzbd，可以通过“历史保留”设置来处理此问题。

### 无法将下载匹配到库项

由于各种原因，一旦抓取并发送到下载客户端，就无法解析发布。在“活动”=>“选项”=>“显示未知”（最近的版本中默认启用）中，将显示所有未被忽略/已导入的\*Arr下载客户端类别中的项目。这些通常需要手动映射和导入。

原因包括：
- 电影名称在TMDb上有一个`:`，而TMDb没有带有`-`或用`:`替换的替代标题
- 文件名缺少必需的年份
- AKA或奇怪的多个名称；Radarr对这些的支持有限
- 文件名与多部电影匹配
- 来自索引器的发布名称或发布ID与文件名不匹配

如果你的下载客户端中有一个发布，但该媒体项（电影/剧集/书籍/歌曲）在应用程序中不存在，也会出现此问题。

### 底层连接已关闭：发送时发生了意外错误

这是由索引器使用当前.NET版本中不支持的SSL协议引起的，可以在[Radarr => 系统 => 状态](/radarr/system#status)中找到。

### 请求超时

Radarr无法从客户端获取响应。

```none
    System.NET.WebException: 请求超时：’https://example.org/api?t=caps&apikey=(已删除) —> System.NET.WebException: 请求超时
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|无法连接到索引器

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: 任务已取消。
```

这也可能是由以下原因引起的：

- 错误配置或使用VPN
- 错误配置或使用代理
- 本地DNS问题-尝试更改为不同的DNS提供商
- 本地IPv6问题-通常启用了IPv6，但无法正常工作
- 使用Privoxy并且配置不正确

## 未列出的问题

你还可以查看一些常见的权限和网络故障排除命令[在我们的指南中](/permissions-and-networking)。否则，请在Discord上与支持团队讨论。如果这是一个可能的常见问题，请建议将其添加到维基中。

# 搜索索引器和跟踪器

- 如果你使用[Prowlarr](/prowlarr)，那么你可以查看Prowlarr接收到的所有查询的[历史记录](/prowlarr/history)以及它们如何发送到站点。确保在Prowlarr History => Options中启用了`Parameters`。 (i) 图标提供了额外的详细信息。

## 将日志级别调整为跟踪

> **第一步是将日志级别调整为跟踪，请参阅[日志和日志文件](#logging-and-log-files)以了解如何调整日志级别和搜索日志。然后，你将重现问题并使用该时间段的跟踪级别日志来检查问题。**如果有人在帮助你，请将前后的上下文放在[pastebin](https://0bin.net)、[Gist](https://gist.com)或类似的网站上展示给他们。它不需要整个文件，也不应该*只*是错误。你还应该在不运行会产生大量日志文件的任务的情况下重现问题。
{.is-danger}

## 测试索引器或跟踪器

当你测试索引器或跟踪器时，在调试或跟踪日志中可以找到使用的URL。下面是一个成功测试的示例，你可以看到它通过特定的URL和特定的参数查询索引器，然后得到响应。你可以在浏览器中测试这个URL，将`apikey=(已删除)`替换为正确的apikey，例如`apikey=123`。如果你从索引器获得错误，你可以尝试更改参数，或者如果根本不起作用，你可以查看是否存在连接问题。在你自己的浏览器中测试后，如果你还没有测试系统正在运行的地方，你应该从该系统上进行测试。

## 测试搜索

与上面的索引器/跟踪器测试类似，当你在调试或跟踪级别日志中触发搜索时，你可以从日志文件中获取使用的URL。在测试过程中，最好使用尽可能狭窄的搜索。手动搜索很好，因为它是具体的，你可以在检查日志时在UI中看到结果。

在这个测试中，你将寻找明显的错误并运行一些简单的测试。你可以看到搜索使用了URL `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(已删除)&q=O+Brother+Where+Art+Thou`，你可以在替换`(已删除)`为该索引器的apikey后在浏览器中尝试。它工作吗？你是否看到了预期的结果？在该URL中，你可以看到它设置了特定的类别2000，所以如果你没有看到预期的结果，这是一个可能的原因。如果电影在索引器上没有正确分类，就需要修复它。查看下面的手动搜索XML输出，以查看工作查询的输出示例。

- 手动搜索XML输出

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(已删除)&q=O+Brother+Where+Art+Thou" rel="self" type="application/rss+xml"/>
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
<newznab:response offset="0" total="17"/>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=e83b7ae75bca71e92367fab29b036731&apikey=(已删除)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(已删除)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=e83b7ae75bca71e92367fab29b036731</comments>
<pubDate>Sat, 10 Jul 2021 08:33:22 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(已删除)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="e83b7ae75bca71e92367fab29b036731"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=c00a92567863801ab1a4901458ae31ba&apikey=(已删除)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(已删除)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=c00a92567863801ab1a4901458ae31ba</comments>
<pubDate>Sun, 28 Mar 2021 10:50:38 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(已删除)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="c00a92567863801ab1a4901458ae31ba"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=75f5be8b4cd573c2359b638350689f73&apikey=(已删除)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(已删除)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=75f5be8b4cd573c2359b638350689f73</comments>
<pubDate>Sun, 28 Jul 2019 00:46:00 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(已删除)" length="936738000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="936738000"/>
<newznab:attr name="guid" value="75f5be8b4cd573c2359b638350689f73"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(已删除)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(已删除)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=a0fe801d9ba0a703db7d2164e996aa1f</comments>
<pubDate>Mon, 14 Aug 2017 15:34:36 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(已删除)" length="9746182000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="9746182000"/>
<newznab:attr name="guid" value="a0fe801d9ba0a703db7d2164e996aa1f"/>
</item>
</channel>
</rss>
```

***需要图片***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- 跟踪日志片段

```none
需要手动搜索的跟踪日志片段
```

- 搜索的完整跟踪日志

```none
需要手动搜索的完整跟踪日志部分
```

## 常见问题

以下是一些常见问题。

### 跟踪器需要RawSearch Caps

- Radarr正在搜索`Kikis Delivery Service`，但你的跟踪器只有`Kiki's Delivery Service`的结果
- 这是因为你的跟踪器不支持正常的标准化搜索。
- 解决方法是更新你的跟踪器定义的搜索功能，指示它[需要和支持`RawSearch`](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905)
- Jackett支持此标志，但需要在每个索引器上更新功能。为Jackett添加此功能的索引器，请提出一个功能请求。
- Prowlarr支持此标志，但需要在每个索引器上更新功能。为Prowlarr添加此功能的索引器，请提出一个功能请求。

### 媒体未监视

电影（们）未被监视。

### 错误的类别

错误的分类可能是索引器/追踪器手动搜索结果显示的最常见原因，但在Radarr中没有显示。索引器/追踪器应该在搜索结果中显示分类，这应该帮助您找出缺失的内容。如果您使用的是Jackett或Prowlarr，每个追踪器都有一个特定支持的分类列表。确保您在Categories中使用的是正确的分类。许多人发现在编辑条目时，在一个浏览器窗口中可见列表会很有帮助。

### 查询成功 - 没有返回结果

您收到类似于“查询成功，但您的索引器没有返回任何结果。这可能是索引器或索引器分类设置的问题。”的消息。

这是由于您的索引器未返回任何符合您为索引器配置的分类的结果引起的。

### 错误的结果

有时索引器会返回完全无关的结果，Radarr会提供参数来限制搜索，但返回的结果完全无关。或者有时，大部分相关但有少量错误结果。第一种情况通常是索引器的问题，您可以从跟踪日志中看出是哪个索引器引起的。您可以禁用该索引器并报告问题。另一种情况通常是错误分类的发布，可以在索引器/追踪器上报告。

### 缺失的结果

如果您在网站上找到的结果在Radarr中没有显示，则您的问题可能是以下几种可能性之一：

- [分类不正确 - 请参见上文](#wrong-categories)
- 基于ID（IMDbId、TMDbId等）进行的搜索，并且索引器没有正确地将发布与该ID映射。这是只有您的索引器可以解决的问题。他们需要确保将发布映射到正确的适用ID。
- 搜索方式与Radarr的搜索方式不一致；您在索引器上搜索的术语很可能不是Radarr的查询方式。您可以从跟踪日志中查看Radarr的查询方式。文本查询通常以`q=words%20and%20things%20here`的格式显示，该字符串是经过HTTP编码的，可以使用任何在线的HTML解码/编码工具进行解码。
- [有关Radarr如何处理外语电影或外语标题的详细信息，请参见常见问题解答](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### 证书验证

您将通过https连接到大多数索引器/追踪器，因此您的系统需要正确地工作。这意味着您的时区和时间都需要设置正确。这还意味着您的系统证书需要保持最新。

### 达到速率限制

如果您通过VPN或代理运行，您可能与数十个、数百个或数千个其他人竞争使用服务，如、theXEM和/或您的索引器和追踪器。速率限制和DDOS保护通常是通过IP地址进行的，而您的VPN/代理出口点是*一个*IP地址。除非您在像中国、澳大利亚或南非这样的专制国家，否则您不需要使用VPN/代理。

Rarbg在其API中有一种限制速率的倾向，并显示为没有结果返回。

### IP封禁

与速率限制类似，某些索引器（如Nyaa）可能会直接封禁IP地址。这通常是半永久性的，解决方法是从您的ISP或VPN提供商获取新的IP。

### 年份不匹配

- [请参阅此常见问题解答条目](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr从TMDb获取元数据
  - Radarr使用最早的**院线发行**日期和最早的**首映**日期进行匹配
- 在某些情况下，电影可能被推迟或改变，发布组使用的年份与最早的首映日期年份和最早的院线发行日期年份都不匹配。在这种情况下，您必须手动获取和导入。

### 缺失的年份

如果发布名称不包含年份，Radarr将不会获取该发布。这是一个错误的发布，只能手动获取。这是在尝试弄清为什么电影没有按预期抓取时经常忽视的一个常见问题。

### 使用Jackett的/all端点

Jackett的`/all`端点很方便，但除此之外都存在潜在问题，因此需要单独添加每个追踪器。或者，您可以考虑使用Jackett和NZBHydra2的替代方案[Prowlarr](/prowlarr)。

[Jackett甚至表示应避免使用/all端点](https://github.com/Jackett/Jackett#aggregate-indexers)

使用all端点没有任何优势（除了减少管理开销），只有劣势：

- 您失去了对索引器特定设置（分类、搜索模式等）的控制
- 混合使用搜索模式（IMDB、查询等）可能导致质量低下的结果
- 无法使用索引器特定的分类（\>= 100000）
- 缓慢的索引器会减慢整体结果
- 总结果限制为1000个

单独添加每个索引器允许对每个索引器的分类进行精细调整，如果在/all端点上使用错误的分类会在某些追踪器上引发错误。

### 将NZBHydra2作为单个条目使用

将NZBHydra2作为单个索引器条目使用（即在Radarr中为NZBHydra2添加1个条目，该条目包含NZBHydra2中的多个索引器），而不是多个条目（即在Radarr中为NZBHydra2添加多个条目，每个条目包含NZBHydra2中的多个索引器）会导致与Jackett的`/all`端点相同的问题。

### 未列出的问题

您还可以查看我们的指南中的一些常见权限和网络故障排除命令。否则，请在Discord上与支持团队讨论。如果这是一个可能是常见问题的问题，请建议将其添加到Wiki中。

## 错误

这些是您在添加索引器时可能遇到的一些常见错误。

### 底层连接被关闭：发送时发生了意外错误

这是由索引器使用的SSL协议不受当前.NET版本支持引起的，可以在[Radarr => System => Status](/radarr/system#status)中找到。

### 请求超时

Radarr无法从索引器获取响应。

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

这也可能是由以下原因引起的：

- VPN配置不正确或使用不当
- 代理配置不正确或使用不当
- 本地DNS问题 - 尝试更改为不同的DNS提供商
- 本地IPv6问题 - 通常启用了IPv6，但无法正常工作
- 使用Privoxy并且配置不正确

### 未列出的问题

您还可以查看我们的指南中的一些常见权限和网络故障排除命令。否则，请在Discord上与支持团队讨论。如果这是一个可能是常见问题的问题，请建议将其添加到Wiki中。