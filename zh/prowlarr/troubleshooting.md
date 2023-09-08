---
title: Prowlarr故障排除
description: 
published: true
date: 2023-08-20T00:20:04.841Z
tags: prowlarr, 故障排除
editor: markdown
dateCreated: 2021-06-20T20:05:25.223Z
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
- [从更新失败中恢复](#从更新失败中恢复)
  - [确定问题](#确定问题)
    - [迁移问题](#迁移问题)
    - [权限问题](#权限问题)
  - [解决问题](#解决问题)
    - [权限问题](#权限问题)
    - [手动升级](#手动升级)
- [NGINX错误](#nginx错误)
- [索引器、应用程序和下载客户端问题](#索引器应用程序和下载客户端问题)
  - [无法确定帧大小或接收到损坏的帧](#无法确定帧大小或接收到损坏的帧)
  - [连接超时](#连接超时)
  - [Sonarr HTTP 404错误](#sonarr-http-404错误)
  - [\*Arr HTTP 400错误](#arr-http-400错误)
  - [503 HTTP服务不可用](#503-http服务不可用)
  - [无效的种子](#无效的种子)
  - [搜索和索引器](#搜索和索引器)

# 寻求帮助

需要帮助吗？没问题，每个人有时都需要帮助。您可以通过以下方式实时获得帮助：

- [<i class="fab fa-discord"></i>&emsp;Discord *官方Prowlarr Discord*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *官方Prowlarr Subreddit*](https://reddit.com/r/prowlarr)
{.links-list}

但在您去那里发布帖子之前，请确保您的求助请求尽可能完善。清楚地描述问题，并简要描述您的设置，包括操作系统/发行版、.NET版本、Prowlarr版本、下载客户端及其版本等信息。**如果您使用的是[Docker](https://www.docker.com/)，请先按照[Docker指南](/docker-guide)进行操作，因为这将解决常见和频繁的路径/权限问题。否则，请准备好[docker compose](/docker-guide#docker-compose)。[如何生成Docker Compose](https://trash-guides.info/compose)** 告诉我们您已经尝试过什么，查看了什么。使用[日志和日志文件](#日志和日志文件)部分将日志级别调整到跟踪，重现问题，将相关上下文粘贴到pastebin中，并在帖子中包含链接。甚至可以包含一些屏幕截图以突出显示问题。

我们了解得越多，就越容易帮助您。

# 日志和日志文件

还可以查看[索引器、应用程序和下载客户端常见问题](#索引器应用程序和下载客户端问题)。

> 如果要求提供索引器响应以进行开发或调试，请继续阅读此蓝色部分...否则，请继续下面的步骤。为了调试索引器响应，可能有助于在Prowlarr的`settings/development`（隐藏页面）中临时启用增强的索引器日志记录以记录索引器的响应。不应始终保持打开。
{.is-info}

如果要求提供调试日志，则您的日志将包含`debug`，如果要求提供跟踪日志，则您的日志将包含`trace`。如果您提供的日志不包含这两者，则它们不是所请求的日志。

- 除非要求，否则不要共享整个日志文件。
- 除非要求，不要直接上传日志到Discord或将其粘贴为文本墙。
- 不要将日志作为附件、zip存档或任何其他形式的非文本文件共享

为了提供好的和有用的共享日志：

> 确保没有运行垃圾任务，比如RSS刷新
{.is-warning}

1. [将日志级别调整到跟踪（设置 => 通用 => 日志级别或编辑配置文件）](#跟踪调试日志)
2. [清除日志（系统 => 日志 => 清除日志或删除日志文件夹中的所有日志）](#清除日志)
3. 重现问题（重新执行导致问题的操作）
4. [通过UI或文件系统上的日志文件（Lidarr.trace.txt）打开跟踪日志文件](#标准日志位置)，找到相关的上下文
5. 复制问题之前的大块内容、问题本身和问题之后的大块内容。
6. 使用[Gist](https://gist.github.com/)、[0bin（**确保禁用着色**）](https://0bin.net/)、[PrivateBin](https://privatebin.net/)、[Notifiarr PrivateBin](http://logs.notifiarr.com/)、[Hastebin](https://hastebin.com/)、[Ubuntu的Pastebin](https://pastebin.ubuntu.com/)或类似的网站（不包括下面要避免的网站）共享上述复制的日志

**警告：**
- **不要使用[pastebin.com](https://pastebin.com)，因为它们的过滤器往往会阻止日志。
- 不要使用[pastebin.pl](https://pastebin.pl)，因为他们的网站经常无法访问。
- 不要使用[JustPasteIt](https://justpaste.it/)，因为他们的网站不方便查看日志。
- 不要上传日志文件
- 不要通过Google Drive、Dropbox或任何其他未在上面提到的网站上传和共享日志。
- 不要归档（zip、tar（tarball）、7zip等）您的日志。
- 不要共享控制台输出、docker容器输出或除应用程序日志之外的任何内容

**重要提示：**
- 使用[0bin](https://0bin.net/)时，请确保禁用着色，并且阅后即焚。

- 或者，如果您要在旧的日志文件中查找特定条目，但不确定哪个文件，可以使用N++。您可以使用Notepad++的“在文件中查找”功能根据需要搜索旧的日志文件。
- **仅适用于Unix：** 或者，如果您要在旧的日志文件中查找特定条目，但不确定哪个文件，可以使用grep。例如，如果您想查找与电影/节目/书籍/歌曲/索引器“Shooter”相关的信息，可以运行以下命令`grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` 如果您的[Appdata目录](/prowlarr/appdata-directory)在您的主文件夹中，则运行：`grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * 标志的功能如下
    * -i：忽略大小写
    * -n：显示行号
    * -r：递归检查路径中的所有文件
    * -C：提供找到的行之前和之后的行数
    * -e：要搜索的模式

```

## 标准日志位置

日志文件位于Prowlarr的[Appdata目录](/prowlarr/appdata-directory)中的logs/文件夹中。您还可以通过UI在System => Logs => Files中访问日志文件。

> 注意：UI中的日志（"Events"表）与日志文件不同，也不太有用。如果要求提供日志，请从日志文件中复制/粘贴，而不是从表中复制/粘贴。
{.is-info}

## 更新日志位置

更新日志文件位于Prowlarr的[Appdata目录](/prowlarr/appdata-directory)中的UpdateLogs/文件夹中。

## 共享日志

日志可能很长，很难在论坛或Reddit帖子中阅读，而且在Discord中也会产生垃圾信息，因此请使用[Pastebin](https://pastebin.ubuntu.com/)、[Hastebin](https://hastebin.com/)、[Gist](https://gist.github.com)、[0bin](https://0bin.net)或任何其他类似的pastebin网站。通常不需要整个文件，只需要问题/错误之前和之后的一段合适的上下文即可。不要忘记等待垃圾任务（如RSS同步或库刷新）完成。

## 跟踪/调试日志

您可以在Settings => General => Logging中更改日志级别。更改日志级别后，无需重新启动Prowlarr即可生效。此更改仅影响日志文件，而不影响日志数据库。最新的调试/跟踪日志文件分别命名为`prowlarr.debug.txt`和`prowlarr.trace.txt`。

如果无法访问UI以设置日志级别，可以通过编辑AppData目录中的config.xml文件来进行设置。将LogLevel的值设置为Debug或Trace，而不是Info。

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## 清除日志

您可以直接从UI中清除日志文件和日志数据库，方法是在`System` => `Logs` => `Files`和`System` => `Logs` => `Delete`（垃圾桶图标）下进行操作。

# 多个日志文件

Prowlarr使用每个限制为1MB的滚动日志文件。当前日志文件始终为Prowlarr.txt，其他文件中Prowlarr.0.txt是下一个最新的（数字越大，表示越旧）。此日志文件包含`fatal`、`error`、`warn`和`info`条目。

启用调试日志级别时，还会存在额外的`prowlarr.debug.txt`滚动日志文件。此日志文件包含`fatal`、`error`、`warn`、`info`和`debug`条目。它通常覆盖了40小时的时间段。

启用跟踪日志级别时，还会存在额外的`prowlarr.trace.txt`滚动日志文件。此日志文件包含`fatal`、`error`、`warn`、`info`、`debug`和`trace`条目。由于跟踪详细程度较高，它只覆盖最多几个小时，有时甚至不到一分钟，如果您正在进行一些密集的操作。

# 从更新失败中恢复

我们尽力防止升级时出现问题，但如果确实出现问题，本文将指导您恢复安装。

## 确定问题

- 在更新后应用程序无法启动时，最好的方法是查看[更新日志](#更新日志位置)并查看更新是否成功完成。如果没有问题，则下一步是查看常规应用程序日志文件，在尝试重新启动之前，使用[日志记录](/prowlarr/settings#logging)和[日志文件](/prowlarr/system#log-files)找到它们并增加日志级别。
- 最常见的问题是应用程序所安装的系统在升级过程中干扰了`/tmp`目录并删除了关键的\*Arr文件，从而导致升级和回滚都失败。在这种情况下，只需在现有的破损安装上重新安装即可。

### 迁移问题

- 迁移错误不会完全相同，但以下是一个示例：

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### 权限问题

- 权限问题是由于应用程序无法访问相关的临时文件夹和/或应用程序二进制文件夹。修复权限，以使应用程序运行的用户/组具有适当的访问权限。

- Synology用户可能会遇到此Synology错误`Access to the path '/proc/{some number}/maps is denied`

- Synology用户还可能在某些NAS上的`/tmp`空间不足。您需要为应用程序指定不同的`/tmp`路径。有关此问题的帮助，请参阅SynoCommunity或其他Synology支持渠道。

## 解决问题

在迁移问题的情况下，您目前无法立即采取任何措施。如果问题是特定于您的情况（或尚无帖子），请在[我们的subreddit](https://reddit.com/r/prowlarr)上创建一个帖子，或者访问我们的[discord](https://prowlarr.com/discord)。如果有其他人遇到相同的问题，那么请放心，我们正在解决。

> 请确保您没有尝试在稳定版本上使用来自`nightly`的数据库。不建议频繁更换分支。{.is-info}

### 权限问题

- 修复权限，以确保应用程序运行的用户/组可以访问（读取和写入）`/tmp`和应用程序的安装目录。

- 对于在Synology上遇到`/proc/###/maps`问题的用户，停止Sonarr或其他\*Arr应用程序并进行更新应该可以解决此问题。这是SynoCommunity软件包的问题。

### 手动升级

从我们的网站上获取最新版本。

安装更新（.exe）或将内容解压缩（.zip）到现有安装上，并像往常一样重新运行Prowlarr。

# NGINX错误

在您的Prowlarr设置中，您将需要添加以下行：

`proxy_set_header Host $host;`

如果您有任何不同的`proxy_set_header`，您必须将其替换为上面的行。

# 索引器、应用程序和下载客户端问题

- 基本上，Prowlarr需要能够与您的索引器通信。
- 如果您使用应用程序同步，Prowlarr还需要能够与您的应用程序通信，并且应用程序需要能够与Prowlarr通信。
- 如果您在Prowlarr中有一个下载客户端用于手动下载，那么Prowlarr将需要能够与您的下载客户端通信。

> 请注意，查询索引器ID 0的日志：ID 0是一个通用的测试端点，允许我们测试\*Arr是否可以回调并连接到Prowlarr，而不实际依赖于工作的索引器。
{.is-info}

以下是一些常见原因

## 无法确定帧大小或接收到损坏的帧

`无法确定帧大小或接收到损坏的帧。`

Prowlarr在连接到站点时存在安全问题。

这通常是由以下原因引起的：

- 本地DNS问题-尝试更改为不同的DNS提供商

## 连接超时

`请求超时`

Prowlarr未收到客户端的响应。[请参阅我们的常规网络和权限故障排除指南](/permissions-and-networking)

这通常是由以下原因引起的：

- 配置不正确或使用了VPN
- 配置不正确或使用了代理
- 本地DNS问题-尝试更改为不同的DNS提供商
- 本地IPv6问题-通常启用了IPv6，但无法正常工作
- 使用Privoxy

## Sonarr HTTP 404错误

- 这通常是由于运行已终止生命周期（EOL）版本的Sonarr，该版本没有v3 API端点
- Prowlarr不支持Sonarr v2
- Prowlarr仅支持Sonarr v3

## \*Arr HTTP 400错误

- 请参阅此FAQ条目：[Prowlarr无法将X索引器同步到应用程序](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 HTTP服务不可用

- 这通常是由于您的跟踪器通过Cloudflare阻止您，并要求使用[FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)

## 无效的种子

- 尝试通过URL和Prowlarr使用的变量下载链接
- 尝试通过Prowlarr代理下载种子文件（即使用抓取文件的应用程序使用的Prowlarr链接）
- 确保您用于索引器的cookie或其他凭据未过期且有效
- 如果问题是由Prowlarr引起的，请提交错误报告。

## 搜索索引器和追踪器

- [Lidarr 搜索和索引器](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Radarr 搜索和索引器](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Readarr 搜索和索引器](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Sonarr 搜索和索引器](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}