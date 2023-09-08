---
title: Readarr快速入门指南
description: 
published: true
date: 2022-09-07T23:19:05.590Z
tags: readarr
editor: markdown
dateCreated: 2021-12-11T19:42:31.825Z
---

# 目录

- [目录](#目录)
- [快速入门设置指南](#快速入门设置指南)
- [启动](#启动)
- [媒体管理](#媒体管理)
- [图书命名](#图书命名)
- [文件夹](#文件夹)
- [导入](#导入)
- [文件管理](#文件管理)
- [根文件夹和Calibre集成](#根文件夹和calibre集成)
  - [Calibre内容服务器（可选）](#calibre内容服务器可选)
  - [Calibre集成](#calibre集成)
- [下载客户端](#下载客户端)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [如何导入现有的组织良好的媒体库](#如何导入现有的组织良好的媒体库)
  - [导入现有媒体](#导入现有媒体)
- [添加新书](#添加新书)

# 快速入门设置指南

> 此页面仍在制作中，尚未完成。欢迎贡献。

> 要获取所有设置的更详细说明，请参阅[Readarr =>设置](/readarr/settings)。
{.is-info}

在本指南中，我们将尝试解释开始使用Readarr所需的基本设置。我们将跳过屏幕上可能看到的一些选项。如果您想深入了解这些选项，请参阅FAQ和文档中的相应页面以获取完整的解释。

> 请注意，在`橙色`的屏幕截图和GUI设置中，是高级选项，因此您需要在页面顶部单击“显示高级”以使其可见。
{.is-warning}

# 启动

安装并启动后，打开浏览器，然后转到`http://{your_ip_here}:8787`

![qs_startup.png](/assets/readarr/qs_startup.png)

# 媒体管理

首先，我们将查看“媒体管理”设置，我们可以在其中设置首选的命名和文件管理设置。

`设置` => `媒体管理`

![mediamanagement.png](/assets/readarr/mediamanagement.png)

# 图书命名

![booknaming.png](/assets/readarr/booknaming.png)

- 启用/禁用对图书进行重命名（与保留当前名称或下载时的名称相反）。
- 如果要替换或删除非法字符（`\ / : * ? " < > | ~ - % & + { }`）。
- 在此处，您将选择实际图书文件的命名约定。请注意，图书文件夹名称也在此处定义。
- （高级选项）这是您将为作者文件夹设置命名约定的地方。

> 如果使用Calibre，则不适用，因为Calibre使用其自己的内部模式处理文件/文件夹命名。
{.is-info}

# 文件夹

![folders.png](/assets/readarr/folders.png)

- （高级选项）创建空作者文件夹-在向Readarr添加新作者时启用以创建空作者文件夹。
- （高级选项）删除空文件夹-在没有该作者的剩余图书时启用以删除空作者文件夹。

> 可以选择其中一个复选框，但不应同时选中两个复选框。
{.is-warning}

> 如果使用Calibre，则不适用，因为Calibre使用其自己的内部模式处理文件/文件夹命名。
{.is-info}

# 导入

![importing.png](/assets/readarr/importing.png)

- （高级选项）跳过空闲空间检查-如果启用，则在导入之前跳过空闲空间检查。
- （高级选项）最小空闲空间-输入导入停止之前驱动器所需的最小空闲空间。
- （高级选项）使用硬链接而不是复制-选中此复选框以使用硬链接而不是复制（用于Torrent）。请注意，这是默认启用的。

> 在可能的情况下，您应该尽量使用硬链接。要使用硬链接，您必须将源/目标放在同一文件系统（驱动器、分区）和挂载点上。[请参阅TRaSH的硬链接指南以获取更多信息](https://trash-guides.info/hardlinks/)
{.is-info}

- 导入额外文件-如果启用，则在导入时导入书籍文件夹中指定的额外文件。
- （高级选项）导入额外文件-如果启用“导入额外文件”，请输入要导入的扩展名的逗号分隔列表。

> 如果您使用Readarr来处理有声读物，应将.cue添加到此列表中，因为它包含您的章节信息！
{.is-info}

# 文件管理

![filemanagement.png](/assets/readarr/filemanagement.png)

- 从磁盘中删除的图书将自动在Readarr中取消监视。

- 忽略已删除的图书-选中此复选框以取消监视在Readarr的根文件夹中检测到的已删除或无法访问的图书。
- 下载正确和修复版本-是否自动升级为正确版本/修复版本。使用“不首选”按首选词得分对其进行排序，而不是按正确版本/修复版本排序。
  - 首选并升级-将修复版本和正确版本排在非修复版本和非正确版本之上。将新的修复版本和正确版本视为对当前版本的升级。
  - 不自动升级-将修复版本和正确版本排在非修复版本和非正确版本之上。不将新的修复版本和正确版本视为对当前版本的升级。
  - 不首选-实际上忽略修复版本和正确版本。您需要使用[首选词](#发布配置文件)来管理对它们的任何偏好。

> \* `PROPER`-表示以前的版本存在问题。标记为PROPER的下载表示该问题已在该版本中修复。这是由未发布原始版本的组织完成的。
> \* `REPACK`-表示以前的版本存在问题，并由原始组织进行了修复。标记为REPACK的下载表示该问题已在该版本中修复。这是由发布原始版本的组织完成的。
{.is-info}

- （高级选项）监视根文件夹的文件更改-选中此复选框以在检测到根文件夹更改时触发重新扫描。
- （高级选项）刷新后重新扫描作者文件夹-选择何时在刷新作者后重新扫描作者文件夹。
  - 始终-这将根据任务计划重新扫描作者文件夹
  - 手动刷新后-您必须手动重新扫描磁盘
  - 从不-就像它所说的那样，从不重新扫描作者文件夹。
- （高级选项）允许指纹识别-选择如何处理指纹识别，它可以提高图书匹配的准确性，但会增加CPU/磁盘时间的消耗。
  - 始终-如果可能，始终使用指纹识别
  - 仅对新导入的发布-仅对新导入的发布使用指纹识别
  - 从不-就像它所说的那样，从不使用指纹识别
- （高级选项）更改文件日期-在导入/重新扫描时更改文件日期
  - 无-Readarr不会更改在给定文件浏览器中显示的日期
  - 图书发布日期-图书发布的日期。
- （高级选项）回收站-删除的图书文件将放在这里，而不是永久删除

> 强烈建议使用回收站。删除文件很容易，如果使用回收站，恢复文件也很容易。
{.is-warning}

# 根文件夹和Calibre集成

![rootfolders1.png](/assets/readarr/rootfolders1.png)

在这里，我们将添加Readarr将用于导入现有组织良好的媒体库的根文件夹，并在下载客户端下载完成后将媒体导入（复制/硬链接/移动）到的位置。

> **您配置Readarr运行的用户和组必须对此位置具有读写访问权限。** {.is-info}

您还可以选择在此屏幕上使用Calibre来管理您的图书馆。这将要求您运行Calibre内容服务器。这不是Calibre-Web。

> 非Windows用户：
> \* 如果您使用的是NFS挂载，请确保启用了`nolock`。
> \* 如果您使用的是SMB挂载，请确保启用了`nobrl`。
{.is-warning}

> 如果要使用Calibre，则您希望在初始库导入时，Readarr要识别的图书**必须已经在Calibre中**。文件夹中的图书而不在Calibre中将被忽略。添加Calibre集成时不使用硬链接。
> **请注意，您无法在创建根文件夹后添加Calibre集成。**
{.is-danger}

> 您的下载客户端将下载到下载文件夹，然后Readarr将其导入到媒体文件夹（最终目标），您的媒体服务器将使用该文件夹。下载文件夹和媒体文件夹不能是同一个位置！
{.is-warning}

不要忘记保存更改。

## Calibre内容服务器（可选）

如果您要使用Calibre管理图书，您需要设置Calibre内容服务器。再次强调，这不是Calibre-Web，而是Calibre本身的一部分。您必须运行Calibre，并设置内容服务器。

> 如果您选择使用Calibre-您不能更改Calibre数据库中的任何内容。不遵守此警告将导致您需要删除Readarr数据库并重新开始。
{.is-danger}

如果您使用的是docker，您的Calibre挂载的图书目录和Readarr挂载的图书目录必须相同。

> 请注意，虽然Readarr处于测试版；如果您使用Calibre，建议在Readarr中禁用重命名，以防意外的错误。
{.is-info}

要执行此操作，请打开Calibre，然后单击“首选项/通过网络共享”

![calibreprefs.png](/assets/readarr/calibreprefs.png)

首先，添加一个用户帐户。该帐户需要具有“进行更改”访问权限。

![calibreacct.png](/assets/readarr/calibreacct.png)

然后，您需要重新启动Calibre。重新启动后，配置并启动内容服务器。它应该显示正在运行。将其设置为在启动时自动运行。保存后，您需要再次重新启动Calibre。确保服务器在重新启动后启动，然后您可以转到下一节。

> 为了使Readarr正常工作，您必须选择“要求用户名和密码以访问内容服务器”。如果不这样做，当Readarr导入一本书时，您将收到一个错误，显示“不允许匿名用户进行更改”！
{.is-info}

![calibreserver.png](/assets/readarr/calibreserver.png)

## Calibre集成

![calibre1.png](/assets/readarr/calibre1.png)

以下是Calibre特定设置，仅在启用“使用Calibre”时显示

- 使用Calibre-启用/禁用使用Calibre内容服务器来管理您的根文件夹。

> \* 请注意，**无法在现有根文件夹上启用此选项**。
> \* 请注意，**无法在已启用Calibre的现有根文件夹上禁用此选项**。
> \* 请注意，这需要**Calibre内容服务器**，而不适用于Calibre Web或Calibre。
> \* 请注意，硬链接在Calibre集成中不起作用。
> \* 请注意，这要求Calibre的“要求用户名和密码以访问内容服务器”选项已启用。
> \* 如果在Calibre中未启用“要求用户名和密码以访问内容服务器”，将出现“不允许匿名用户进行更改”的错误。
{.is-warning}

> 如果选择使用Calibre-您不能更改Calibre数据库中的任何内容。不遵守此警告将导致您需要删除Readarr数据库并重新开始。
{.is-danger}

- Calibre主机-Calibre内容服务器的主机的IP/域名
- Calibre端口-Calibre内容服务器侦听的端口
- （高级）Calibre URL基础-为Calibre URL添加前缀，例如`http://[host]:[port]/[urlBase]`
- Calibre用户名-用于访问Calibre内容服务器的用户名
- Calibre密码-用于访问Calibre内容服务器的密码
- Calibre库-Calibre内容服务器库名称。保留为空白以使用默认值
- 转换为格式-（可选）要求Calibre内容服务器将其转换为其他格式的逗号分隔列表。
  - 请查看应用程序中的（i）图标以获取当前选项列表。
  - 选项包括：MOBI、EPUB、AZW3、DOCX、FB2、HTMLZ、LIT、LRF、PDB、PDF、PMLZ、RB、RTF、SNB、TCR、TXT、TXTZ、ZIP
- Calibre输出配置文件-选择要使用的Calibre内容服务器输出配置文件
  - 输出配置文件告诉Calibre内容服务器转换系统如何为指定设备优化创建的文档（例如，通过调整图像大小以适应设备屏幕尺寸）。在某些情况下，可以使用输出配置文件来优化输出以适应特定设备，但这很少需要。
- 使用SSL-启用或禁用Calibre内容服务器的SSL（HTTPS）使用

> 如果添加单个图书，并为[元数据配置文件](/readarr/settings#metadata-profiles)选择了`None`\*，则仅在添加时该图书将显示在作者下。如果要添加该作者的其他图书，请选择适当的元数据配置文件。
> \* **请注意，“None”不应用任何元数据过滤器，您可能会获得不需要的外国版本。要解决此问题，请[按照FAQ中的说明创建元数据配置文件](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# 下载客户端

`设置` => `下载客户端`

下载和导入是大多数人遇到问题的地方。从高层次的角度来看，软件需要能够与您的下载客户端进行通信，并访问其下载的文件。有许多支持的下载客户端和更多各种各样的设置。这意味着虽然有一些常见的设置，但没有一个正确的设置，每个人的设置都可能有所不同。但是有很多错误的设置。

> 有关更多信息，请参阅[设置页面](/readarr/settings#download-clients)，在[更多信息（支持）](/readarr/supported#download-clients)页面中查看此部分，并参阅[TRaSH的下载客户端指南](https://trash-guides.info/Downloaders/)。
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Readarr将向您的客户端发送下载请求，并将其与您在下载客户端设置中配置的标签或类别名称关联起来。
  - 例如：电影、电视、系列、音乐等。
- Readarr将通过您的下载客户端的API监视使用该类别名称的活动下载。
- 下载完成后，Readarr将根据您的要求解析文件名以将其与请求的媒体匹配。如果可以匹配，它将根据您的规格重命名文件，并将其移动到指定的媒体位置。
- 默认情况下启用原子移动（即瞬时移动）。已完成的下载目录和媒体库的文件系统和挂载点必须相同。如果原子移动失败或您的设置不支持硬链接和原子移动，则Readarr将退回并复制文件，然后从源中删除文件，这会产生IO开销。
- 如果在Readarr的设置中启用了“完成的下载处理-删除”选项，则会通过向客户端发送删除/删除发布的请求，将下载的剩余文件发送到垃圾箱或回收站。

### BitTorrent

{#bittorrent}

- Readarr会向您的下载客户端发送下载请求，并将其与您在下载客户端设置中配置的标签或类别名称关联起来。
  - 示例：电影、电视、系列、音乐等。
- Readarr将监视使用该类别名称的下载客户端的活动下载。此监视通过您的下载客户端的API进行。
- 完成的文件将保留在其原始位置，以便您可以做种文件（比率或时间可以在下载客户端或在Readarr中的特定下载客户端下进行调整）。当文件被导入到您的媒体文件夹时，如果您的设置支持硬链接，Readarr将会创建硬链接；如果不支持硬链接，则会复制文件。
- 硬链接默认为启用状态。[硬链接将不使用任何额外的磁盘空间。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)您完成下载的目录和媒体库的文件系统和挂载点必须相同。如果硬链接创建失败或您的设置不支持硬链接，则Readarr将退回并复制文件。
- 如果在Readarr的设置中启用了“完成下载处理 - 删除”选项，Readarr将从您的客户端中删除种子，并要求客户端删除种子数据，但仅在客户端报告种子做种已完成且种子已停止（完成后暂停）时才会执行此操作。

# 如何导入现有的组织好的媒体库

> 请注意，Readarr不会定期搜索图书。请参阅以下两个常见问题解答条目，了解Readarr的工作原理的详细信息。
[Readarr如何找到图书？](/readarr/faq#how-does-readarr-find-books) 和 [Readarr如何工作？](/readarr/faq#how-does-readarr-work)
{.is-info}

在设置完您的配置文件/质量大小并添加了索引器和下载客户端之后，现在是时候导入您现有的组织好的媒体库了。

即将推出 - 欢迎贡献

## 导入现有媒体

即将推出 - 欢迎贡献

# 添加新图书

[有关更多信息，请参阅图书馆页面](/readarr/library#add-new)