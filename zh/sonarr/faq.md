## Sonarr基础知识

### Sonarr如何找到剧集？

- Sonarr不会定期搜索缺失的剧集文件或未达到质量目标的剧集。相反，它会频繁查询您的索引器和追踪器，以获取所有新发布的剧集/新上传的发布，然后将其与缺失或需要升级的剧集列表进行比较。任何匹配的剧集都会被下载。这样，Sonarr只需每天进行24-100次查询（15-60分钟的RSS间隔）就可以覆盖任何大小的库。如果您理解这一点，您将意识到它只涵盖了“未来”。

- 那么如何处理现在和过去的剧集呢？当您添加一个剧集时，您需要设置正确的路径、配置文件和监视状态，然后使用“开始搜索缺失”复选框。如果该剧集还没有任何剧集，并且尚未发布，您不需要启动搜索。

- 换句话说，Sonarr只会找到新上传到您的索引器的发布。它不会主动尝试找到过去上传的发布。

- 如果您已经添加了剧集，但现在想要搜索它，您有几个选择。您可以转到剧集页面并使用搜索按钮，它会进行搜索，然后自动选择剧集。您可以自动或手动搜索单个剧集或季节。或者您可以转到[Wanted](/sonarr/wanted)选项卡并从那里进行搜索。

- 如果Sonarr离线时间过长，Sonarr将尝试翻页以找到其处理的最后一个发布，以避免错过发布。只要您的索引器支持翻页并且时间不长，Sonarr就能够处理它可能错过的发布，并避免您需要执行搜索来查找错过的剧集。

### 自动搜索发生的情况

自动搜索（通过索引器的API）仅在以下情况下进行。请注意，与正常情况一样，适用相同的规则：剧集+剧集必须被监视，没有播出日期的剧集将被跳过。

- 触发的自动或手动搜索
  - 用户或API触发的搜索。通常通过单击特定剧集、季节或剧集的自动或手动搜索按钮执行。
- 使用“添加并搜索”按钮添加剧集
- 使用Wanted => Missing或Wanted => Cutoff Unmet进行一次或多次搜索
- 最近播出的剧集在播出后添加
  - 如果Sonarr中添加了一个新剧集，该剧集在过去14天内播出或在未来1天内播出（以覆盖那些可能稍早发布的剧集），Sonarr将在重新扫描剧集文件夹后为这些剧集进行搜索（以捕获在Sonarr之外导入的内容）。

### 如何比较可能的下载选项？

> 通常，质量优先。如果您希望质量不是主要优先级-您可以合并您的质量。[请参阅TRaSH的指南](https://trash-guides.info/merge-quality)
{.is-info}

- 当前的逻辑[可以在这里找到](https://github.com/Sonarr/Sonarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs#L31-L40s)。

- 截至2022-01-23，逻辑如下：

1. 质量
2. 语言
3. 首选词得分\*
4. 协议（根据相关延迟配置文件中的配置）
5. 剧集数\*
6. 剧集编号
7. 索引器优先级
8. 种子/下载者（如果是Torrent）
9. 年龄（如果是Usenet）
10. 大小

> REPACKS和PROPER是质量的v2版本，因此在质量相同的情况下排名高于非REPACK版本。[在媒体管理=>文件管理`下载Proper和Repacks`中设置为“不偏好”](/sonarr/settings#file-management)，并使用TRaSH的指南中建议的正向得分为`/\b(repack|proper)\b/i`的首选词正则表达式
{.is-warning}

> \*首选词始终升级发布，即使已满足质量和/或语言截止时间。这包括如果配置文件禁用了升级。

> \*首选词覆盖标准季度包首选项。这是[Sonarr Github问题＃3562](https://github.com/Sonarr/Sonarr/issues/3562)。要在使用首选词时优先使用季度包，您需要[添加一个季度包首选项](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

## 首选词常见问题解答

- 对于磁盘上的文件得分：将评估文件的现有名称和发布的“原始场景名称”以获取首选词。将取两者中的较高得分。

- 首选词如何包含在重命名中？

  - 对于Sonarr，您可以在重命名方案中使用`{Preferred Words}`标记，并在发布配置文件中启用`在重命名时包含首选词`。请参阅TRaSH的推荐命名方案的[示例](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/)以获取Sonarr的推荐命名方案示例。在重命名方案中使用标记可以帮助解决下载循环问题。

- 从v3.0.7开始，您现在还可以根据发布配置文件包含首选词`{Preferred Words:<Release Profile Name>}`

- 首选词始终升级发布，即使已满足质量和/或语言截止时间。这包括如果配置文件禁用了升级。

> 首选词覆盖标准季度包首选项。这是[Sonarr Github问题＃3562](https://github.com/Sonarr/Sonarr/issues/3562)。要在使用首选词时优先使用季度包，您需要[添加一个季度包首选项](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

- 标签可用于控制发布配置文件适用于哪些剧集；有关更多信息，请参阅发布配置文件的设置条目

- 有关首选词和发布配置文件的其他信息，请参阅设置页面[/sonarr/settings#release-profiles](/sonarr/settings#release-profiles)

## 如何从Windows服务更改为托盘应用程序？

1. 关闭 Sonarr。
1. 在 Sonarr 目录中运行 serviceuninstall.exe。
1. 以管理员身份运行 Sonarr.exe 一次，以赋予它适当的权限并打开防火墙。完成后，关闭它并正常运行。
1. （可选）将 Sonarr.exe 的快捷方式放入启动文件夹，以在启动时自动启动。

## 如何备份/恢复 Sonarr？

### 备份 Sonarr

#### 使用内置备份

- 在 Sonarr 用户界面中转到 System => Backup。
- 点击 Backup 按钮。
- 在备份创建后下载 zip 文件以备份。

#### 直接使用文件系统备份

- 找到 Sonarr 的 AppData 目录的位置。
  - 通过 Sonarr 用户界面转到 System => About。
  - [Sonarr Appdata 目录](/sonarr/appdata-directory)
- 停止 Sonarr - 这将防止数据库损坏。
- 将内容复制到安全位置。

### 从备份中恢复

> 将备份恢复到使用不同路径的操作系统上将无法正常工作（例如，从 Windows 到 Linux，从 Linux 到 Windows，从 Windows 到 macOS，或从 macOS 到 Windows），在 macOS 和 Linux 之间迁移可能有效，因为两者都使用包含 `/` 而不是 Windows 使用的 `\` 的路径，但不受支持。您需要手动编辑数据库中的所有路径或使用 [Toolbarr](https://github.com/Notifiarr/toolbarr)。
{.is-warning}

#### 使用 zip 备份

- 重新安装 Sonarr（如果适用/尚未安装）。
- 运行 Sonarr。
- 导航到 System => Backup。
- 选择 Restore Backup。
- 选择 Choose File。
- 选择备份的 zip 文件。
- 选择 Restore。

#### 使用文件系统备份

- 重新安装 Sonarr（如果适用/尚未安装）。
- 找到 Sonarr 的 AppData 目录的位置。
  - 运行 Sonarr 一次并通过用户界面转到 System => About。
  - [Sonarr Appdata 目录](/sonarr/appdata-directory)
- 停止 Sonarr。
- 删除 AppData 目录的内容 **（包括 .db-wal/.db-journal 文件，如果存在）**。
- 从备份中恢复。
- 启动 Sonarr。
- 只要路径相同，一切都会继续进行。

#### 在 Synology NAS 上进行文件系统恢复

> 注意：在 Synology 上进行恢复需要了解 Linux 和 Root SSH 访问 Synology 设备。
{.is-warning}

- 重新安装 Sonarr（如果适用/尚未安装）。
- 找到 Sonarr 的 AppData 目录的位置。
  - 运行 Sonarr 一次并通过用户界面转到 System => About。
  - [Sonarr Appdata 目录](/sonarr/appdata-directory)
- 停止 Sonarr。
- 通过 SSH 连接到 Synology NAS 并以 root 身份登录。

> 在某些安装中，用户与下面的命令不同：`chown -R sc-Sonarr:Sonarr *` {.is-info}

- 执行以下命令：

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- 更新文件的权限：

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- 启动 Sonarr

## 我忘记了密码，怎么办？

{#help-i-have-forgotten-my-password}

> 如果您使用的是 Sonarr 的 v4 版本，则 `AuthenticationMethod` 类型 `None` 不再有效 - 请参阅此 [FAQ](/sonarr/faq-v4) {.is-info}

要禁用身份验证（以重置忘记的用户名或密码），您需要编辑 `config.xml` 文件，该文件位于 [Sonarr Appdata 目录](/sonarr/appdata-directory) 中。

1. 用文本编辑器打开 config.xml 文件。
1. 找到身份验证方法行，它将是 `<AuthenticationMethod>Basic</AuthenticationMethod>` 或 `<AuthenticationMethod>Forms</AuthenticationMethod>`。
1. 将 `AuthenticationMethod` 行更改为 `<AuthenticationMethod>None</AuthenticationMethod>`。
1. 重新启动 Sonarr。
1. 现在可以无需密码访问 Sonarr，您应该在用户界面的 `Settings: General` 中设置用户名和密码。

## 为什么会有两个文件？ \| 为什么下载文件夹中还有一个文件？

这是正常现象。如果设置支持 [硬链接](https://trash-guides.info/hardlinks)，则不会使用双倍的空间。以下是 Torrent 进程的工作原理。

1. Sonarr 将下载请求发送到您的客户端，并将其与您在下载客户端设置中配置的标签或类别名称关联。例如：movies、tv、series、music 等。
1. Sonarr 通过下载客户端的 API 监视使用该类别名称的活动下载。此监视通过下载客户端的 API 进行。
1. 已完成的文件保留在其原始位置，以便您可以进行文件的做种（可以在下载客户端或特定下载客户端下进行比率或时间的调整）。当文件导入到媒体文件夹时，如果您的设置支持硬链接，则会创建硬链接，否则将复制文件。
1. 如果在 Sonarr 的设置中启用了“已完成下载处理 - 删除已完成”选项，则 Sonarr 将从下载客户端中删除原始文件和种子，但仅当下载客户端报告做种已完成且种子已停止（即暂停）。有关如何优化下载客户端的配置，请参阅 [TRaSH 的下载客户端指南](https://trash-guides.info/Downloaders/)。

> 硬链接默认启用。[硬链接不会使用任何额外的磁盘空间](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)。已完成下载目录和媒体库的文件系统和挂载点必须相同。如果硬链接创建失败或您的设置不支持硬链接，则会退回并复制文件。{.is-info}

## 我看到 feature/bug X 已修复，为什么我看不到？

Sonarr 由两个主要的代码分支组成，即 `main` 和 `develop`。

- `main` 定期发布，当 `develop` 分支稳定时。
- `develop` 用于预发布测试和愿意冒险的用户。当一个功能被标记为 `develop` 时，它只对运行 `develop` 分支的用户可用，一旦它被移动到正式版本（在 `main` 中），它就正式发布了。

## 剧集进度是如何计算的？

- 剧集计数有两个部分，一个是剧集数（Episode Count），另一个是带有文件的剧集数（Episode File Count），每个部分使用稍微不同的逻辑来给出系列或季度的整体进度。

  - 剧集数 => 剧集已经播出并且正在监视，或者 - 剧集有文件
  - 剧集文件数 => 剧集有文件

- 如果一部剧集有 10 集已经播出，但您没有任何文件，那么您将有 0/10 集；如果您取消监视该系列的所有剧集，您将有 0/0 集；如果您获取了该系列的所有剧集，无论剧集是否被监视，您将有 10/10 集。

## 如何从其他计算机访问 Sonarr？

- 默认情况下，Sonarr 不会接受来自所有系统的请求（当不以管理员身份运行时），它只会在本地监听，这是由于 Sonarr 使用的 Web 服务器与 Windows 集成的方式（当前的替代方案也适用）。如果以管理员身份运行 Sonarr，它将正确地在 Windows 中注册自身，并打开防火墙端口，以便其他系统在您的网络上访问它。只需要以管理员身份运行一次（如果更改了端口，则需要重新运行）。

## 为什么 Sonarr 频繁刷新剧集信息？

- Sonarr 每隔 12 小时刷新剧集和剧集信息，同时重新扫描磁盘以查找文件。这可能看起来很频繁，但这是一个非常重要的过程。从我们的 TVDb 代理刷新数据很重要，因为会同步新的剧集信息，如上映日期、剧集数、状态（连载/完结）。即使不在播出的节目也会更新新信息。
- 磁盘扫描不是很重要，但用于检查未由 Sonarr 排序的新文件并检测已删除的文件。
- 最耗时的部分是信息刷新（假设磁盘访问速度合理），较大的节目需要更长的时间来处理剧集数。

> 无法禁用此任务。如果此任务运行的时间足够长，您认为它是问题的原因，那么说明还有其他问题需要解决，而不是停止此任务。{.is-warning}

## 为什么活动旁边会有一个数字？

- 此数字显示您的下载客户端队列中的剧集数以及其历史记录中最后 60 个尚未导入的项目。如果数字是蓝色的，则表示正常运行，应在剧集完成后导入剧集。黄色表示其中一个剧集有警告。红色表示发生错误。在黄色（警告）和红色（错误）的情况下，您需要查看活动下的队列，以查看问题所在（将鼠标悬停在图标上以获取更多详细信息）。
- 您需要从下载客户端的队列或历史记录中删除项目，以将它们从 Sonarr 的队列中删除。

## 不同的剧集类型有什么区别？

- 剧集类型影响 Sonarr 的搜索方式。剧集类型基于剧集在索引器上的发布方式，不一定是剧集的真实“类型”。
- 大多数节目应该选择 `Standard`。对于通常以日期发布的每日节目，应该选择 `Daily`。最后，有动画片，使用 `Anime` *通常* 是正确的选择，但有时使用 `Standard` 可能效果更好，因此如果遇到问题，请尝试*另一个*选项。
- 请注意，如果将剧集类型设置为动画，并且您启用的索引器没有配置任何动画类别，则它将跳过该索引器，可能会导致无法搜索。
- 请注意，动画类型没有任何季度或季节的概念，并且会导致单独搜索每一集。
- 请注意，并非所有索引器都支持季度/剧集（标准）搜索。
- 可以从批量编辑器或在查看剧集时从“编辑”中修改剧集类型。请注意，可以在导入时选择剧集类型。

- 如果使用 **Anime** 剧集类型 - 还可以使用标准类型搜索您的索引器。[/sonarr/settings#indexers]

### 剧集类型

- **Anime** - 使用绝对剧集编号发布的剧集
- **Daily** - 每天或更少频繁发布的剧集，使用年-月-日（2017-05-25）
- **Standard** - 使用 SxxEyy 模式发布的剧集

### 剧集类型示例

以下是每种剧集类型的一些示例发布名称。特定的区别部分以粗体字标出。

> 如果使用 **Anime** 剧集类型 - 还可以使用标准类型搜索您的索引器。[/sonarr/settings#indexers]
{.is-info}

#### Daily

日志将显示 `Searching indexers for [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

日志将显示 `Searching indexers for [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

日志将显示 `Searching indexers for [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## 如何重命名我的剧集文件夹？

{#rename-folders}

> 对于移动/更改剧集路径，相同的过程也适用{.is-info}

如果在 Sonarr 创建一些剧集文件夹后调整了剧集名称格式，Sonarr 将不会自动重命名现有文件夹。为了触发对这些文件夹的重命名，应执行以下步骤：

1. 剧集
1. 批量编辑器
1. 选择需要重命名文件夹的剧集
1. 将根文件夹更改为与剧集当前所在的根文件夹相同
1. 选择 "Yes move files" 以进行文件移动

> 如果您使用 Plex 或 Emby，则这将触发重新检测片头、缩略图、章节和预览元数据。
{.is-warning}

## 如何更新 Sonarr？

- 转到设置，然后转到常规选项卡，并显示高级设置（使用保存按钮旁边的切换）。

1. 在更新部分将分支名称更改为 `main` 或 `develop`。
1. 保存

*这不会立即安装该分支的组件，它将在下次更新时发生。*

- main - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - （默认/稳定）：已由用户在夜间（`develop`）分支上测试，并且不知道是否存在任何重大问题。大多数用户应该使用此分支。在 GitHub 上，这是 `main` 分支。
- develop - ![Current Develop/Nightly](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - （Alpha/不稳定）：对于预发布测试和愿意冒险的用户。当一个功能被标记为 `develop` 时，它只对运行 `develop` 分支的用户可用，一旦它被移动到正式版本（在 `main` 中），它就正式发布了。

> ~~**警告：切换到此分支后，您可能无法返回到 `main`。** 在 GitHub 上，这是 `develop` 分支。~~
{.is-danger}

- v4 develop - ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - （Alpha/不稳定）：**对于非 Docker 用户，分支是 `develop`，一旦安装了 v4，对于 Docker 用户，这可能是 `develop` 标签** 这是 Sonarr v4 Beta 的最新版本。它会在提交代码并通过所有自动化测试后立即发布。这个版本可能还没有被我们或其他用户使用过。无法保证它在某些情况下甚至能运行。只建议高级用户使用此分支。在 GitHub 上，这是 `develop` 分支。

> **警告：在切换到 v4 分支后，您将无法返回（v3）`main` 或（v3）`develop`，除非重新安装并找到 v3 的备份。** 在 GitHub 上，这是 `develop` 分支。
{.is-danger}

> v3 **非 Docker** 安装无法直接升级到 v4，需要安装 Sonarr v4
{.is-info}

- 注意：如果您的安装是通过 Docker 进行的，请在容器标签的末尾添加 `:release`、`:latest`、`:nightly` 或 `:develop`，具体取决于构建者。



|                                                                    | `main` (稳定版) ![当前主要/最新版本](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=主要&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (测试版) ![当前v3开发/测试版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=开发&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4测试版) ![当前v4测试版](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4预览&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### 安装更新版本

#### 本地安装

1. 进入“系统”，然后点击“更新”选项卡。
2. 尚未安装的更新版本旁边会有一个更新按钮，点击该按钮即可安装更新。

> v3 无法更新到 v4 测试版，需要手动安装。请参考 [v4 测试版公告](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)
{.is-info}

#### Docker 安装

1. 重新拉取标签并更新容器。

## 我可以从 `develop` 切换回 `main` 吗？

- 请参考下面的条目。

## 我可以在不同分支之间切换吗？

> 你（几乎）总是可以增加风险。{.is-info}

- `main` 可以切换到 `develop`。
- 请参考下面的条目，或者与开发团队核实是否可以从 `develop` 切换到 `main`。
- 如果不按照这些说明操作，可能导致 Sonarr 无法使用或抛出错误。请注意，如果遇到以下错误，则表示您正在使用较新的数据库与较旧的 \*Arr 版本，这是不受支持的。请将 \*Arr 升级到之前或更新的版本。
  - 示例错误消息：
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - 其他类似的数据库错误，如缺少列或表。
- **2022年8月7日更新**
  - `3.0.9.1549` 已发布为主要/稳定版本
  - 对于那些仍在 `develop` 上且仍在 `3.0.9.1549` 或更低版本的用户，可以安全地降级到主要版本
  - 如果您使用的是更新版本，则可能会被困在夜间/开发版本，直到发布新的稳定版本。如果您有在升级到上述版本之前的备份，可以重新安装并恢复备份。请与开发团队核实是否可以安全降级。

# Sonarr 和剧集问题 + 元数据

## Sonarr 如何处理剧集编号问题（美国老爸等）？

### Sonarr 如何处理剧集编号问题

- Sonarr 依赖于 [TheXEM](http://thexem.info/)，这是一个由社区驱动的网站，允许用户创建显示剧集编号的映射，其中“场景”（发布文件的人）和 TheTVDb（通常遵循网络的编号）之间存在差异。已经有许多剧集在上面了，但是添加另一个剧集非常容易，通常在几天内就会被接受（如果它们是正确的）。TheXEM 用于纠正剧集编号的差异（关于某一集是否是特别节目的争议）以及季数差异，例如某一集以 S10E01 的形式发布，但 TheTVDb 将同一集列为 S2017E01。

> 某些索引器或发布组可能会遵循 TVDb 而不是 `Scene`（即 XEM）。如果观察到这种情况，请通过场景映射表单提交它们。
{.is-info}

- [已请求的映射服务 *请查看并确保别名和发布尚未被请求或添加*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [场景映射请求表单 *为别名提交新请求。请确保完整填写表单*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### 问题剧集

> 这绝不是所有存在场景映射问题的剧集的完整列表；然而，这些是一些常见的剧集。
{.is-info}

- 这是已知存在问题的剧集的不完整列表：
- 《美国老爸》 {#problemshow-americandad}
  - 由于网络季节更改，美国老爸在发布和 TVDb 之间通常相差一个季度。有关详细信息，请参考 XEM 映射。
  - [美国老爸](https://thexem.info/xem/show/4948) 当前基于 TVDb 是 S19 或基于场景是 S18。因此，在 Sonarr 中搜索第 19 季将**仅**返回第 18 季的结果，这是由于 XEM 映射。
  - 如果您有带有第 19 季剧集的索引器/发布组，请通过场景映射表单提交它们，并确保它们尚未被请求。
    - [已请求的映射服务 *请查看并确保别名和发布尚未被请求或添加*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [场景映射请求表单 *为别名提交新请求。请确保完整填写表单*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- 《汪汪队立大功》 {#problemshow-pawpatrol}
  - 双集文件与单集 TVDb 不匹配，而且并非所有剧集都是双集，因此映射可能会出错，指向哪些是单集和双集。
- 《宠物小精灵》 {#problemshow-pokemon}
  - 在 TheXEM 上，[宠物小精灵](http://thexem.info/xem/show/4638) 跟踪的是“配音”剧集。因此，如果您想要字幕剧集，可能就没戏了。如果某些发布组遵循 TVDb 而不是 XEM 映射，请通过场景映射表单提交它们，并确保它们尚未被请求。
    - [已请求的映射服务 *请查看并确保别名和发布尚未被请求或添加*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [场景映射请求表单 *为别名提交新请求。请确保完整填写表单*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- 《纸钞屋》 {#problemshow-moneyheist}
  - TVDb 拥有来自西班牙网络的原始播放顺序，但 Netflix 购买了版权，并将该系列重新剪辑成了不同的集数。这导致“第 5 季”被导入现有的“第 3 季”剧集之上。关于此问题的更多信息，请参阅 Reddit 帖子 [此处](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- 《假面骑士》 {#problemshow-kamenrider}
  - 应在 Sonarr 中使用编目条目（[TVDb ID 74096](https://thetvdb.com/series/kamen-rider)）进行自动化，因为该剧集既有一个编目条目（收集所有季度），又有单独的季度条目在 TVDb 上列出。由于编目条目在 [TheXEM](https://thexem.info/xem/show/5376) 上具有单独的季度名称映射，因此无法在 Sonarr 中添加单独的季度条目，除非手动下载和导入发布。
- 《死神 千年血战篇》 {#problemshow-bleach}
  - 死神 千年血战篇的最新季度以各种不同的命名方案发布，这使得自动化变得困难，并有可能覆盖您现有的某些剧集。只有在以下情况下才能自动化：
    - 将剧集发布为 S17Exx 编号，或者
    - 使用正确的第 2 季系列标题（在此处找到 <https://thexem.info/xem/show/5476>），并从绝对集数 1 开始此新篇章。
- 《伟大的亚洲铁路之旅》 {#problemshow-greatasianrail}
  - 《伟大的亚洲铁路之旅》首先以 20 个较小的剧集播出，但后来以 10 个较长的剧集重新播出。这些较长的合并剧集被添加为特别剧集，并应相应命名。（S00E01 等，...）
- 《地平线》 {#problemshow-horizon}
  - 这是一部从 1964 年开始不定期播出的剧集。这使得映射特别困难，如您在 [TheXEM](https://thexem.info/xem/show/5495) 上所见。有兴趣的人可以在 Sonarr Discord 上找到有关此问题的原始讨论 [此处](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312)。
- 《万花筒》（2023） {#problemshow-kaleidoscope}
  - 《万花筒》（2023）在 Netflix 上作为非线性剧集发布，这意味着每个用户观看该剧集时都会获得不同的顺序。这导致 Sonarr 出现问题，因为发布组对该剧集具有不同的剧集顺序。为了防止剧集映射错误，Sonarr 不会自动获取剧集，您需要手动获取和导入剧集。您可以根据剧集标题进行匹配，或者通过预览前几秒钟并查看与标题匹配的剧集“颜色”来进行匹配。

其他常见出现问题的节目示例，其中大部分问题可能通过TheXEM映射解决，包括：《逮捕令》、《厨房噩梦（美国版）》、《神奇实验室》、《当铺之星》。

## 为什么Sonarr无法导入系列X的剧集文件？/ 为什么Sonarr找不到系列X的发布版本？

Sonarr无法找到或导入特定系列的剧集可能有多个原因。

> Sonarr不使用TVDb的别名或翻译（即任何外语标题）。
{.is-warning}

> **对于支持基于ID搜索的索引器**，将使用系列的TVDbID或IMDbID进行搜索。仅当基于ID的搜索没有结果时，才使用系列标题和任何别名。
{.is-info}

- Sonarr依赖于能够匹配标题，通常上传者使用不同的标题命名剧集，例如`CSI:犯罪现场调查`只发布为`CSI`，因此Sonarr无法在没有帮助的情况下匹配这些名称。这些问题由Sonarr团队维护的Scene Mapping处理。
- 您还可以查看[常见问题解答：有问题的节目和发布组与TVDb编号问题](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

> **对于所有日本动画，需要将别名添加到[thexem.info](https://thexem.info)**，对于其他系列，如果要请求新的映射，请参阅下面的步骤。有关更多信息，请参阅Sonarr Discord上的#XEM频道。
{.is-danger}

- [服务请求映射*请查看并确保别名和发布版本尚未被请求或添加*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [服务场景映射请求表格*为别名提出新请求。请确保完整填写表格*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> 通常，服务请求将在1-5天内添加
{.is-info}

> 不要为日本动画请求映射；请使用XEM。有关更多信息，请参阅[Sonarr Discord上的#XEM频道](https://discord.gg/Z3D6u5hBJb)
{.is-danger}

> 如果非日本系列需要季节映射（例如以S25E26发布，但TVDB是S26E2），则需要进行XEM映射。这无法通过服务映射完成。
{.is-info}

> 系列“Helt Perfekt”的TVDb ID为`343189`和`252077`，由于TVDb为这两个节目使用相同的名称，违反了TVDb自己的规则，因此很难自动化。系列的第一个条目将获得名称。该系列的任何后续条目必须在系列名称中包含年份。但是，已添加了一个场景异常以映射包含`NORWEGIAN`的Helt Perfekt发布- > `252077`和包含`SWEDISH`的发布- > `343189`
{.is-info}

## TVDb已更新，为什么Sonarr没有更新？

{#tvdb}

- TVDb在其API上有24小时的缓存。
- TVDb的API然后需要通过其CDN缓存填充，这需要几个小时的时间。
- Sonarr的Skyhook在此基础上还有几个小时的较小缓存。
- 此外，Sonarr仅在每12小时运行一次“刷新系列”任务。可以从系统=>任务中手动运行此任务；在系列索引中选择“全部更新”，或者在特定系列的页面上手动运行此任务。

- 因此，要使TVDb上的更改自动进入Sonarr，通常需要36至48小时（24 + ~3 + ~3 + 12）。

- 如果在TVDb上缺少系列或剧集，则它们将在添加后的36至48小时内从TVDb中添加到您的Sonarr实例中。

{#missing-episodes}

- 如果您知道TVDb更新是在48小时前进行的，请在我们的[Discord](https://discord.sonarr.tv/)上讨论。

## 为什么我无法添加系列？

{#why-can-i-not-add-a-new-series}

- 如果TheTVDb不可用，Sonarr无法获取搜索结果，您将无法通过搜索添加任何新系列。如果您知道TVDb ID，可以通过TVDb ID添加新系列，UI会解释如何添加。
- Sonarr无法添加任何没有英语标题的系列。如果尝试通过TVDb ID添加没有英语标题的系列，则无法找到该系列。如果TheTVDb上没有该系列的英语标题，则需要添加该系列，然后[需要等待TVDb的缓存清除](#tvdb)。
- 该节目必须是电视系列，而不是电影。它必须存在于TVDb上。如果它在IMDB、TMDB或其他任何地方都有，但在TVDb上没有，您无法添加该节目。
- 该系列必须存在于TVDb上。
- 某些系列实际上可能被视为其主要系列的延续和季节。
  - 已知的一些系列/季节有：
  - [《Dexter新血脉》是第9季](https://thetvdb.com/series/dexter/seasons/official/9)，但现在是[它自己的系列](https://thetvdb.com/series/dexter-new-blood)

## 我知道TVDb ID，为什么无法添加系列？

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr无法添加任何没有英语标题的系列。如果尝试通过TVDb ID添加没有英语标题的系列，则无法找到该系列。如果TheTVDb上没有该系列的英语标题，则需要添加该系列（如果可用）。
- 检查URL/系列- Sonarr不支持电影；请使用[Radarr](/radarr)来处理电影

## 标题 Slug 已使用

- 这个错误有两个主要原因，如下所示。

## 重复名称没有年份

- 当两个系列在TheTVDB上具有相同的标题时，通常会出现此错误，如果是这种情况，则应将年份附加到第二个系列的系列标题。
  - 系列A
  - 系列A（2021）
- 要纠正此问题，请等待有人最终（可能）更新TVDb或自己更新TVDb。一旦更正**并经过TVDb的审核员批准**，由于[TVDb的API问题](#tvdb-is-updated-why-isnt-sonarr)，一旦更新完成，您需要等待30多个小时，然后才能在Sonarr中使用更正后的标题。

## 重复名称标点符号

- 当两个名称相似的系列只有标点符号不同时，将发生此错误，请在[Sonarr Discord](https://discord.sonarr.tv/)上报告此问题。
  - Joe's Show（2022）
  - Joes Show（2022）

## 剧集没有绝对编号

- TVDb上的剧集没有分配绝对编号。如果需要，请更新TVDb上的系列，然后等待36-48小时，以便更新清除TVDb的内部缓存并加载到Sonarr中。

## 剧集播出时间

- 在Sonarr中，浏览器中显示的剧集播出日期和时间基于客户端的时间/时区，所有时间都以UTC时间（ISO-8601格式）从Sonarr发送到浏览器
- TVDb规定-除了流媒体服务外-播出时间和日期基于主要播出网络在该国最受欢迎的城市的当地时间。[有关详细信息，请参阅TVDb的常见问题解答](https://support.thetvdb.com/kb/faq.php?id=29)
- TVDb上的剧集播出日期和播出时间转换为UTC，并使用Sonarr团队在Skyhook中映射的Sonarr时区，用于该系列的Network TVDb。
  - 在罕见的情况下，如果没有映射网络，则假定TVDb中的时间为美国东部标准时间（UTC-5）。
  - 如果在将播出时间从播出网络的当地时区转换为浏览器的时区时，时间似乎不对齐，则很可能是网络需要在Skyhook中进行映射。[联系开发团队的Discord](https://discord.sonarr.tv/)以获取有关更新网络时区的支持。

# Sonarr常见问题

## 路径已配置为现有系列

- 库导入显示“已存在”，或者出现“路径已配置为现有系列”的错误
- 当尝试添加系列或编辑已存在系列的路径时，如果该路径已分配给其他系列，则会出现此问题。
- 这很可能是由于用户导入库时未纠正不匹配的系列引起的。
- 找到并纠正已分配给该系列路径的电影。
  - 系列索引
  - 表格视图
  - 选项=>添加路径作为列
  - 排序并找到指定问题路径上的电影。
- 或者，使用现有路径从Sonarr中删除该系列

## 系统和日志加载时间过长

- 这是由于easy-privacy blocklist引起的。它们基本上会阻止任何包含`/api/log?`的URL。请查看列表，并告诉我您是否认为阻止该列表中的所有URL是明智的，该列表中有数十个潜在破坏站点的URL。您在广告拦截器中选择了该选项。简单的解决方法是将Sonarr运行的域名添加到白名单中。但我仍建议检查该列表。

## 奇怪的UI问题

- 如果您遇到任何奇怪的UI问题，比如库页面不显示任何内容，或者某个视图或排序不起作用，请尝试在Chrome的隐身窗口或Firefox的隐私窗口中查看。如果在那里正常工作，请清除特定IP/域名的浏览器缓存和Cookie。有关更多信息，请参阅[清除缓存、Cookie和本地存储](/useful-tools#clearing-cookies-and-local-storage)维基文章。

## 仅在Windows上的localhost加载Web界面

- 如果您只能在<http://localhost:8989/>或<http://127.0.0.1:8989>上访问Web界面，则需要至少以管理员身份运行Sonarr一次。

## 我收到一个弹窗，说config.xml损坏，现在怎么办？

- Sonarr在启动时无法读取配置文件，因为它以某种方式损坏。为了使Sonarr恢复在线状态，您需要删除[AppData文件夹](/sonarr/appdata-directory)中的`.xml`，删除后启动Sonarr，它将在默认端口（8989）上启动，现在您应该重新配置在常规设置页面上配置的任何设置。

## 无效的证书和其他HTTPS或SSL问题

- 如果您使用的是非Windows系统，很可能是因为您的mono证书已过期，需要进行同步。[有关详细信息，请参阅安装文章中关于mono ssl的部分](/sonarr/installation#mono-ssl-issues)
- 您的下载客户端停止工作，并出现错误，例如“本地主机是无效的证书”？
  - Sonarr现在验证SSL证书。如果下载客户端中没有设置SSL证书，或者您正在使用自签名的https证书而没有将CA证书添加到本地证书存储中，则Sonarr将拒绝连接。您可以从[let's encrypt](https://letsencrypt.org/)获取免费的正确签名证书。
  - 如果您的下载客户端和Sonarr位于同一台机器上，则没有理由使用HTTPS，因此最简单的解决方案是禁用连接的SSL。大多数人都同意在本地网络上也不需要它。如果要保持不安全的SSL设置，可以在高级设置中禁用证书验证。

## 如何阻止浏览器在启动时自动打开？

根据您的操作系统，有多种可能的方法。

- 在某些操作系统上，在“设置”=>“常规”中，有一个复选框可以在启动时打开浏览器。
- 在调用Sonarr时，可以在参数中添加`-nobrowser`（*nix）或`/nobrowser`（Windows）。
- 停止Sonarr并编辑config.xml文件，将`<LaunchBrowser>True</LaunchBrowser>`更改为`<LaunchBrowser>False</LaunchBrowser>`。

## VPN、Jackett和\*ARRs

- 除非您身处像中国、澳大利亚或南非这样的压制国家，否则您的种子客户端通常是唯一需要在VPN后面的软件。由于VPN终端点由许多用户共享，您可能会遇到来自各种软件使用的各种服务的速率限制、DDOS保护和IP封禁。

> **明确指出，VPN是否会对\*Arrs造成问题，而不是何时：图像提供商将封锁您，而Cloudflare位于大多数\*Arr服务器（更新、元数据等）之前，也有可能封锁您**
{.is-warning}

- **许多私有跟踪器会因使用或通过VPN访问它们（例如使用Jackett或Prowlarr）而封禁您。**

### 使用VPN

- 如果需要VPN并且使用Docker，则建议使用Hotio或Binhex的Download Client + VPN容器。
- 如果需要VPN并且不使用Docker，则您的VPN客户端***必须***支持分割隧道，以便只有所需的（下载客户端）应用程序位于VPN后面。
- 使用Google或Cloudflare的DNS服务器而不是您的ISP的DNS服务器，可以解决访问跟踪器的许多问题。
- 在某些情况下（例如英国的ISP），您可能需要将种子下载客户端放在VPN后面，并按以下方式设置Jackett/Prowlarr：
  - 将Jackett放在VPN后面，并确保分割隧道允许本地访问
  - 对于Prowlarr，请配置您的VPN客户端提供代理，并在设置=>索引器中添加代理。给代理添加一个标签，并将需要使用它的任何索引器添加相同的标签。
    - 如果绝对需要，如果您的VPN没有提供创建代理的方法，您可以将Prowlarr放在VPN后面，并确保分割隧道允许本地访问。

## 我看到与我没有/不想要的节目相关的日志消息

- 这些消息是完全正常的，来自Sonarr检查以查看是否有您想要的剧集的RSS源，通常只会在调试/跟踪日志中出现，但如果处理项目时出现问题，可能会看到警告或错误。可以安全地忽略警告/错误，因为它们是针对您不想要的节目的，如果是您想要的节目，请在论坛上开启支持主题。

## 种子继续做种，但不会自动删除

- 当导入仍在做种的种子时，它会被复制或硬链接（如果启用且*可能*），以便种子客户端可以继续做种。在理想的设置中，种子下载文件夹和库文件夹将位于同一文件系统上并且*看起来像是*（Docker和网络共享很容易搞错），这样可以实现硬链接并最小化浪费的空间。
- 另外，您可以在Sonarr或下载客户端中配置种子的做种时间/比率目标，将下载客户端设置为在达到这些目标时*暂停*或*停止*，并启用“已完成”和“失败的下载处理程序”下的“删除”选项。这样，完成做种的种子将被Sonarr从下载客户端中删除。

## 帮助，我的Mac显示Sonarr无法打开，因为开发者无法验证

- 这很简单，请参阅此链接以获取更多信息[here](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
[![Developer Cannot be verified](/assets/general/faq_1_mac.png)]

## 帮助，我的Mac显示Sonarr.app已损坏，无法打开

- 这可能是由于下载损坏，因此请重试，或者[安全问题，请参阅相关的常见问题解答条目。](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## 我收到一个错误：数据库磁盘映像损坏

> 在将sqlite3升级到3.41后，您可能会收到此错误。Sonarr v3.0.9不支持sqlite3 3.41，因为默认更改会导致破坏。[有关该问题的详细信息，请参阅Sonarr GHI＃5464](https://github.com/Sonarr/Sonarr/issues/5464)
> 这在Sonarr v3.0.10中得到解决，用户应相应地升级Sonarr。
{.is-warning}

- **`Error creating log database`错误表示日志数据库（logs.db）存在问题**
  - 可以通过重命名或删除数据库来快速解决。日志数据库包含有关命令历史、更新安装历史以及信息、警告和错误条目的不重要信息。
- **`Error creating main database`或通用的`database disk image is malformed`错误（没有指定数据库）表示sonarr.db存在问题**
  - 请按照下面的步骤继续操作
- 这意味着存储Sonarr大部分信息的SQLite数据库已损坏。您可以尝试备份、恢复现有数据库、恢复备份，或者如果所有其他方法都失败了，从头开始使用全新的数据库。
- 如果数据库文件不可写，可能会出现此错误。权限问题通常只会影响新安装、迁移到新服务器的安装、最近修改了appdata目录权限或更改了\*Arr运行的用户和组。
- 恢复备份是您的最佳和首选选项。[尝试从备份恢复](#how-do-i-backuprestore-my-sonarr)
- 您还可以尝试恢复数据库。这通常是在更新后出现此问题时的唯一选项。尝试使用[sqlite3的`.recover`命令](/useful-tools#recovering-a-corrupt-db)
  - 如果您的sqlite没有`.recover`命令，或者您希望使用更友好的图形界面（例如Windows），请按照[我们在此wiki上的说明](/useful-tools#recovering-a-corrupt-db-ui)操作。
- 数据库出现错误的另一个可能原因是将数据库放在网络驱动器（nfs或smb或其他非本地驱动器）上。**SQLite设计用于数据和应用程序共存于同一台机器的情况。**因此，您的\*Arr AppData文件夹（Docker的/config挂载点）必须位于本地存储上。[SQLite和网络驱动器不兼容，最终会导致数据库损坏](https://www.sqlite.org/draft/useovernet.html)。
- 如果您使用的是mergerFS，您需要删除`direct_io`，因为SQLite使用的是mmap，而`direct_io`不支持，具体请参阅mergerFS的[文档](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## 我在Mac上使用Sonarr，突然停止工作了。发生了什么？

- 最有可能的原因是MacOS的一个错误导致其中一个Sonarr数据库损坏。
- [按照以下步骤解决问题](#i-am-getting-an-error-database-disk-image-is-malformed)
- 然后尝试启动Sonarr，看看是否正常工作。如果仍然无法正常工作，您需要进一步获得支持。在我们的[Reddit](http://reddit.com/r/Sonarr)上发布问题，或者在[Discord](https://discord.sonarr.tv/)上寻求帮助。

## 为什么Sonarr无法看到我在远程服务器上的文件？

- 对于所有操作系统，请确保您以\*Arr运行的用户/组具有挂载驱动器的读写权限。
- 对于Linux，请确保：
  - 如果您使用的是NFS挂载，请确保启用了`nolock`。
  - 如果您使用的是SMB挂载，请确保启用了`nobrl`。
- 对于Windows：简而言之，\*Arr运行的用户（如果是服务）或所在的用户组无法访问远程服务器上的文件路径。这可能是由于各种原因引起的，但最常见的原因是\*Arr作为服务运行，导致下面描述的问题。

### Sonarr默认在LocalService帐户下运行，该帐户无法访问受保护的远程文件共享

- 将Sonarr服务运行为具有访问该共享的权限的其他用户
- 在Windows服务器上打开“管理工具”\>“服务”窗口。
- 停止Sonarr服务。
- 打开“属性”\>“登录”对话框。
- 将服务用户帐户更改为目标用户帐户。
- 使用启动文件夹运行Sonarr.exe

### 您正在使用映射的网络驱动器（而不是UNC路径）

- 将路径更改为UNC路径（`\\server\share`）
- 通过启动文件夹运行Sonarr.exe

## 映射的网络驱动器与UNC路径

- 使用映射的网络驱动器通常效果不佳，特别是当Sonarr配置为作为服务运行时。设置共享的更好方法是使用UNC路径。因此，不要使用`X:\TV`，而是使用`\\Server\TV`。

- 需要记住的一个关键点是，Sonarr从下载器获取路径信息，因此您还需要设置NZBGet、SABNzbd或任何其他下载器使用UNC路径。

## Sonarr在Big Sur上无法工作

运行以下命令：

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## 升级到v2后，我的自定义脚本停止工作了

- 您可能在连接中传递了参数，这是不受支持的。
- 要纠正这个问题：
  1. 将参数更改为路径。
  2. 确保脚本中的shebang映射到您的pwsh路径（如果在其中没有shebang定义，请添加）。
  3. 确保pwsh脚本可执行。

# Sonarr搜索和下载常见问题

## 查询成功 - 未返回结果

- [请参阅此故障排除条目](/sonarr/troubleshooting#query-successful-no-results-returned)

## 为什么Sonarr没有抓取我期望的剧集？

首先，请确保您已阅读并理解上面的“Sonarr如何查找剧集”部分。其次，请确保您的索引器中至少有一个包含您期望抓取的剧集。

1. 在Sonarr中，单击剧集列表旁边的“手动搜索”图标。是否有任何结果？如果没有，则表示Sonarr与您的索引器通信有问题，或者您的索引器没有该剧集，或者该剧集在索引器上的命名/分类不正确。
2. **如果步骤1中有结果**，请检查结果旁边是否有红色感叹号图标。将鼠标悬停在图标上，查看为什么该发布不符合自动下载的条件。如果每个结果都有该图标，则不会进行自动下载。
3. **如果步骤2中至少有一个有效的手动搜索结果**，则应该自动下载。如果没有自动下载，最可能的原因是临时通信问题导致RSS同步与索引器之间断开连接。建议设置多个索引器以获得最佳结果。
4. **如果在节目中没有手动结果，但您可以在索引器的网站上找到该节目** - 这可能是由多种原因引起的，例如在索引器上未正确标记该发布，导致它在自动搜索中未返回给Sonarr。这个[故障排除条目](/sonarr/troubleshooting#searches-indexers-and-trackers)提供了一些确定原因的提示。通过使用多个索引器，可以提供更多相同内容的来源，从而解决此问题。

## 在抓取历史中找到匹配的剧集，但是通过ID匹配到系列。无法自动导入

- 请参阅[此故障排除条目](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- 在TVDb上，当剧集名称未知时，它们将被命名为TBA，并且TVDb API有一个24小时的缓存。通常，由于TVDb缓存（24小时）、skyhook缓存（几小时）和系列刷新间隔（每12小时一次），从TVDb网站更改到Sonarr需要24-48小时。[Episode Title Required设置](/sonarr/settings#importing)在剧集标题为TBA时控制导入行为，但是在系列播出后48小时，即使标题仍为TBA，也将导入该发布。此外，不会自动重新命名TBA标题的文件。请注意，TBA计时器是根据剧集的播出日期和时间计算的，而不是根据您抓取或上传时间计算。

## Sonarr在搜索或导入时显示未知系列

- 请参阅[为什么Sonarr无法为系列X导入剧集文件？/ 为什么Sonarr无法为系列X找到发布？](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)条目

## Jackett的/all端点

{#jackett-all-endpoint}

- Jackett的`/all`端点很方便，但除此之外没有其他好处。其他都可能导致问题，因此需要单独添加每个跟踪器。或者，您可以尝试使用Jackett和NZBHydra2的替代方案[Prowlarr](/prowlarr)

- **2022年2月5日更新：由于仅会引起问题，因此自v3.0.6.1457起，\*Arr不再支持Jackett的`/all`端点。不再支持Jackett的/all端点（例如，会出现警告）。**

- Jackett的`/all`端点很方便，但除此之外没有其他好处。其他都可能导致问题，因此现在需要单独添加每个跟踪器。
- [即使Jackett的开发人员也表示应避免使用/all端点，不应使用它。](https://github.com/Jackett/Jackett#aggregate-indexers)
- 使用/all端点没有任何优势，只有劣势：
  - 您无法控制特定索引器的设置（类别、搜索模式等）。
  - 混合使用搜索模式（IMDB、查询等）可能会导致低质量的结果。
  - 无法使用特定索引器的类别（\>= 100000）。
  - 缓慢的索引器会降低整体结果的速度。
  - 总结果限制为1000个。
  - 如果/all中的一个跟踪器返回错误，\*Arr将禁用它，您将无法获得任何结果。

### Jackett /All解决方案

- 在\*Arr中手动将每个跟踪器作为索引器添加到Jackett中
- 查看[Lidarr/Radarr/Readarr开发团队](/prowlarr)开发的[Prowlarr](/prowlarr)
- 查看[NZBHydra2](https://github.com/theotherp/nzbhydra2)，它可以将索引器同步到\*Arr。但不要使用它们的单个聚合端点，而是使用`multi`如果要使用同步。

## 在手动搜索时，Jackett显示的结果比Sonarr多

- 检查Sonarr中配置的跟踪器的类别
- 这通常是由于Sonarr与您的搜索方式不同。[请参阅此故障排除文章以获取更多信息](/sonarr/troubleshooting#searches-indexers-and-trackers)。

## 查找Cookies

- 有些网站无法自动登录，需要您手动登录，然后将Cookies提供给Sonarr以使其正常工作。[请参阅此文章获取详细信息。](/useful-tools#finding-cookies)

## 解压Torrent

- 大多数Torrent客户端不像Usenet客户端那样自动处理压缩的存档文件。我们推荐使用[unpackerr](https://github.com/unpackerr/unpackerr)。

## 权限

- Sonarr需要将文件从下载器放置的位置移动到最终位置，因此这意味着Sonarr需要读写源目录和目标目录及文件。
- 在Linux上，最佳实践是将服务作为其自己的用户运行，这可能意味着在您的下载器和Sonarr中使用共享组，并将文件夹权限设置为`775`，文件权限设置为`664`。以umask表示，即为`002`。

## 强制身份验证

- 在Sonarr v4（beta版）中，身份验证是强制性的。有关详细信息，请参阅[Sonarr v4 FAQ - Forced Authentication](/sonarr/faq-v4#forced-authentication)。