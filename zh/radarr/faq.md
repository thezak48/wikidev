## 所有电影文件可以存储在一个文件夹中吗？

- 是的，Radarr允许您将所有电影文件存储在一个文件夹中。要配置此设置，请按照以下步骤操作：

1. 在Radarr的Web界面中，导航到“设置”>“媒体管理”>“文件管理”。
2. 将“启用文件管理”选项设置为“是”。
3. 在“根文件夹路径”字段中，输入您想要存储所有电影文件的文件夹的路径。
4. 单击“保存”以保存更改。

请注意，如果您更改了根文件夹路径，Radarr将不会自动移动现有的电影文件。您需要手动将它们移动到新的文件夹中。此外，如果您使用的是Docker容器，请确保在容器设置中正确映射了文件夹路径。

- 不可以，原因是Radarr是[Sonarr](/sonarr)的一个分支，其中每个节目都有一个文件夹。这个限制是许多用户的痛点，也许会在将来的版本中解决。请注意，这不是一个简单的更改，实际上需要对后端进行完全重写。
- [自定义文件夹的GitHub问题](https://github.com/Radarr/Radarr/issues/153)在技术上涵盖了这个请求，但不能保证将在那个时候实现将所有电影文件放在一个文件夹中。
- 下面描述了一种稍微hack-ish的解决方案。请注意，您不能触发Radarr中的重新扫描，否则它将显示为丢失，而且无论如何电影都永远不会升级。
  - 使用自定义脚本
    - 脚本应在导入时触发
    - 它应该设计为在您想要的任何时候移动文件
    - 然后需要调用Radarr API并将电影更改为未监视。

如果您想将所有电影从一个文件夹移动到单独的文件夹，请查看[Tips and Tricks Section => Create a Folder for Each Movie](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)文章

## 我可以将我的所有电影放在一个文件夹中吗？

- 不可以，参见上面的回答。

## 如何更新Radarr？

- 进入设置，然后进入常规选项卡，并显示高级设置（使用保存按钮旁边的切换按钮）。

1. 在更新部分将分支名称更改为`master`或`develop`
1. 保存

*这不会立即安装该分支的组件，它将在下次更新时发生。*

- ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - （默认/稳定）：它已经由开发人员和夜间分支上的用户进行了测试，并且没有任何已知的重大问题。该版本将每月接收更新。在GitHub上，这是`master`分支。

- ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - （Beta）：这是测试边缘。在夜间测试后发布，以确保没有立即出现问题。新功能和错误修复将在夜间后首先在此发布。它可以被认为是半稳定的，但仍然是`beta`。该版本将每周或每两周更新一次，具体取决于开发情况。

> **警告：在切换到此分支后，您可能无法返回`master`。** 在GitHub上，这是`develop`分支。
{.is-warning}

- ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - （Alpha/不稳定）：这是最新的版本。只要提交的代码通过了所有自动化测试，就会立即发布。这个版本可能还没有被我们或其他用户使用过。不能保证在某些情况下它甚至能运行。这个分支只推荐给高级用户。在这个分支中，预计会出现问题和自我调查。***只有在您知道自己在做什么并愿意亲自解决更新失败的问题时，才使用此分支。***此版本会立即更新。

> **警告：在切换到此分支后，您可能无法返回`master`。** 在GitHub上，这是`develop`分支。
{.is-danger}

- 注意：如果您的安装是通过Docker进行的，请根据构建者的不同，在容器标签的末尾添加`:release`、`:latest`、`:testing`或`:develop`。

|                                                                    | ![Current Master/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### 我可以在Docker容器内更新Radarr吗？

- *从技术上讲，是可以的。* **但是你绝对不应该这样做。** 这是Docker的一个主要原则。如果您在内部升级到最新的`nightly`，但是然后更新Docker容器本身（可能降级到旧版本），可能会导致数据库问题。

### 安装更新版本

#### 本机

1. 进入系统，然后进入更新选项卡
1. 尚未安装的更新版本旁边会有一个更新按钮，点击该按钮将安装更新。

#### Docker

1. 重新拉取您的标签并更新容器

## 我可以从`nightly`切换回`develop`吗？

## 我可以在不同的分支之间切换吗？

- 如果版本相同，则可以切换，否则请与开发团队确认您是否可以从`nightly`切换到`master`；从`nightly`切换到`develop`；或从`develop`切换到`master`，具体取决于您的构建版本。
- 如果不按照这些说明操作，可能会导致您的Radarr无法使用或抛出错误。您已经被警告了。如果遇到以下错误，则表示您正在使用较新的数据库与较旧的\*Arr版本，这是不受支持的。将出现以下错误消息：
  - `Error parsing column 45 (Language=31 - Int64)`
  - `The DataMapper was unable to load the following field: 'Languages' value`
  - `ID does not match a known language Parameter name: id`
  - 其他类似的数据库错误，如缺少列或表。

## 如何备份/恢复Radarr？

### 备份Radarr

#### 使用内置备份

- 进入Radarr UI中的系统 => 备份
- 点击备份按钮
- 在备份创建后下载zip文件以备份

#### 直接使用文件系统

- 找到Radarr的AppData目录的位置
  - 通过Radarr UI进入系统 => 关于
  - [Radarr Appdata目录](/radarr/appdata-directory)
- 停止Radarr - 这将防止数据库损坏
- 将内容复制到安全位置

### 从备份中恢复

> 将备份还原到使用不同路径的操作系统上将无法工作（从Windows到Linux，从Linux到Windows，从Windows到OS X或从OS X到Windows），在OS X和Linux之间移动可能有效，因为两者都使用包含`/`而不是Windows使用的`\`的路径，但不受支持。您需要手动编辑数据库中的所有路径，或者使用[Toolbarr](https://github.com/Notifiarr/toolbarr)。
{.is-warning}

#### 使用zip备份

- 重新安装Radarr（如果适用/尚未安装）
- 运行Radarr
- 导航到系统 => 备份
- 选择还原备份
- 选择选择文件
- 选择您的备份zip文件
- 选择还原

#### 使用文件系统备份

- 重新安装Radarr（如果适用/尚未安装）
- 找到Radarr的AppData目录的位置
  - 运行Radarr一次，然后通过UI进入系统 => 关于
  - [Radarr Appdata目录](/radarr/appdata-directory)
- 停止Radarr
- 删除AppData目录的内容**（包括存在的.db-wal/.db-journal文件）**
- 从备份中恢复
- 启动Radarr
- 只要路径相同，一切都会继续进行

#### 在Synology NAS上进行文件系统还原

> 注意：在Synology上进行还原需要了解Linux和Root SSH访问Synology设备。
{.is-warning}

- 重新安装Radarr（如果适用/尚未安装）
- 找到Radarr的AppData目录的位置
  - 运行Radarr一次，然后通过UI进入系统 => 关于
  - [Radarr Appdata目录](/radarr/appdata-directory)
- 停止Radarr
- 通过SSH连接到Synology NAS并以root身份登录

> 在某些安装中，用户与下面的命令不同：`chown -R sc-Radarr:Radarr *` {.is-info}

- 执行以下命令：

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- 更新文件的权限：

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- 启动Radarr

# Radarr常见问题

## 任务被取消

- Radarr在100秒后未收到来自请求所在服务器的响应。
- 日志中将包含`System.Threading.Tasks.TaskCanceledException: A task was canceled.`。
- 这通常是由以下原因引起的：
  - VPN配置不正确或使用不当
  - 代理配置不正确或使用不当
  - 本地DNS问题 - 尝试更改为不同的DNS提供商
  - 本地IPv6问题 - *最常见* - 通常在主机系统上启用了IPv6，但无法正常工作
  - 使用Privoxy并且配置不正确
  - PiHole对请求进行[速率限制](https://docs.pi-hole.net/ftldns/configfile/#rate_limit)
- 您可以使用DNS `nslookup <来自跟踪日志的域名.tld>`和ipv6 `curl -sv -6 "<来自跟踪日志的URL>"` / 使用`curl -sv -4 "<来自跟踪日志的URL>"`来排除所有其他连接问题。

## 路径已配置为现有电影的路径

![existing-movie.png](/assets/radarr/existing-movie.png)

- 库导入显示“已存在”或者您收到“路径已配置为现有电影”的错误。
- 当尝试添加电影或编辑已存在电影的路径时，出现此问题，该路径已分配给其他电影。
- 可能是由于在用户导入库时未更正不匹配的电影引起的。
- 找到并更正已分配给该电影路径的电影。
  - 电影索引
  - 表视图
  - 选项 => 添加路径作为列
  - 排序并找到位于指定有问题路径的电影。
- 或者，从Radarr中删除使用现有路径的电影。

## 如何重命名我的电影文件夹？

{#rename-folders}

> 同样的过程也适用于移动/更改电影路径。如果您只是在Radarr中更新路径而不需要移动文件，请在第5步中不选择“是，移动文件”。
{.is-info}

1. 电影
1. 电影编辑器
1. 选择需要重命名其文件夹的电影
1. 将根文件夹更改为电影当前所在的根文件夹
1. 选择“是，移动文件”

> 如果您使用Plex，这将触发重新检测片头、缩略图、章节和预览元数据。
{.is-warning}

## 电影文件和文件夹命名

- 目前，Radarr要求每个电影都在一个文件夹中，其格式至少包含`电影标题（年份）/`，可选的分隔符有`_`或`.`。为了在导入过程中正确识别质量和分辨率，最好使用文件名格式如`电影标题（年份）[质量-分辨率].ext`，同样`_`或`.`也是有效的分隔符。

  - 一个有用的工具是[filebot](http://www.filebot.net/#download)，它在Apple和Windows商店中都有付费版本，但可以在他们的传统[SourceForge](https://sourceforge.net/projects/filebot/files/latest/download)网站上免费找到。它有GUI和CLI两种方式，所以您可以使用您熟悉的方式。对于上面的例子，`{ny}`会扩展为`Name (Year)`，`{vf}`会给出分辨率，如`1080p`。没有推断质量的方法，所以您可以使用`{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`来命名低于720p的任何内容为`[DVD-572p]`，而大于或等于720p的内容为`[Bluray-1080p]`。

- 有关更多详细信息，请参见[Tips and Tricks Section => Create a Folder for Each Movie](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie)。

## 电影文件夹命名不正确

- 电影文件夹的命名是基于添加电影时的元数据（名称/年份）。如果您在电影发布之前添加了电影，您可能需要使用上面提到的重命名文件夹技巧来更新电影文件夹的命名以反映新的当前数据。
- 即使您的电影已经在文件夹中，文件夹的命名也可能不正确。文件夹的名称应为`电影标题（年份）`，将标题和年份放在文件夹的名称中是非常重要的。

  - 可以正常工作的示例：
    - `/mnt/Movies/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Kid Movies/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - 可以正常工作，但需要手动管理的示例：
    - 按字母：`/mnt/Movies/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - 按评级：`/mnt/Movies/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - 按类型：`/mnt/Movies/Crime, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - 这些示例在添加电影时需要手动管理。每个示例都会有许多根目录，例如第一个字母示例中的`A-D`和`E-G`，评级示例中的`R`和`PG-13`，以及您可以猜测的各种类型文件夹。在添加新电影时，需要选择正确的基本文件夹才能使此格式正常工作。
  - 不起作用的示例：
    - 单个文件夹：`/mnt/Kid Movies/Frozen (2013) [Bluray-1080p].mkv`
      - 目前，电影必须只能放在以电影名称命名的文件夹中。在开发工作添加此功能之前，没有其他办法。
    - v0.2版本中的**电影**文件夹命名格式包括**文件**属性在**电影文件夹**名称中，例如``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}``在v3中不起作用。
      - 文件夹与电影相关，与文件无关。此外，这将与计划中的每个电影支持多个文件的功能冲突。
      - 删除此功能的另一个原因是它经常引起混淆、数据库损坏，并且通常只是一半的工作。
  - [Tips and Tricks Section => Create a Folder for Each Movie](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)是确保您的文件和文件夹结构正常工作的好资源。

## 我可以禁用刷新电影任务吗？

- 不可以，也不应该通过任何SQL黑客手段来禁用刷新电影任务。刷新电影任务会查询上游Servarr代理，并检查每部电影的元数据（ID、演员、摘要、评级、翻译、备用标题等）是否与Radarr中的当前数据不同。如果需要，它将更新适用的电影。
- 常见的抱怨是刷新任务会导致大量的I/O使用。
- 主要设置是“刷新后重新扫描电影文件夹”。如果在刷新过程中磁盘I/O使用量激增，则可以将重新扫描设置更改为`手动`。
  - 除非您的库中的所有更改（新电影、升级、删除等）都是通过Radarr完成的，否则不要将其更改为`从不`。
  - 如果您手动或通过Plex或其他第三方程序删除电影文件，请不要将其设置为`从不`。
- 可以更改的另一个设置是“分析视频文件”，如果您使用tdarr或以其他方式外部修改文件，则建议启用“分析视频文件”。如果您不这样做，可以安全地禁用“分析视频文件”以减少一些I/O。

## 如何为Radarr请求新功能？

- 这很简单，[点击这里](https://github.com/Radarr/Radarr/issues)

## 帮助，我的Mac显示Radarr无法打开，因为开发者无法验证

- 这很简单，请参阅此链接以获取更多信息[here](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Developer Cannot be verified](developer-cannot-be-verified.png "Developer Cannot be verified")
- 或者，您可能需要自签名Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## 帮助，我的Mac显示Radarr.app已损坏，无法打开

- 这可能是由于下载损坏，所以请再试一次或者[安全问题，请参阅此相关FAQ条目。](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## 我遇到了一个错误：数据库磁盘映像损坏

> \* 对于升级到v4.X版本的Radarr用户，如果您的数据库在任何地方之前出现过损坏（以前运行Radarr时可能无法检测到），迁移将失败。这将导致Radarr无法启动。很可能您的所有备份也都是损坏的，因此仅恢复这些备份可能无法解决问题。
> \* 如果迁移后的数据库无法打开或无法恢复，则从最近的备份中复制数据库文件，并对该文件应用数据库恢复过程，然后尝试使用恢复的备份文件启动Radarr。它应该能够无问题地进行迁移。
{.is-warning}

- **“创建日志数据库时出错”表示日志数据库存在问题**
  - 这可以通过重命名或删除数据库来快速解决。日志数据库包含有关命令历史记录、更新安装历史记录以及Info、Warn和Error条目的不重要信息。
- **“创建主数据库时出错”或一般的“数据库磁盘映像损坏”错误（没有指定数据库）表示radarr.db存在问题**
  - 继续执行下面的步骤
- 这意味着存储Radarr大部分信息的SQLite数据库已损坏。您的选择是尝试（一个）备份，尝试恢复现有数据库，尝试恢复备份，或者如果所有其他方法都失败，则从头开始使用全新的数据库。
- 如果此错误显示为数据库文件不可由用户/组\*Arr运行，写入。权限可能仅对新安装、迁移到新服务器的迁移安装、最近修改了appdata目录权限的情况，或者更改了\*Arr运行的用户和组时才会成为问题。
- 您的最佳和首选选项是[尝试从备份中恢复](#how-do-i-backuprestore-my-radarr)。然而，对于在升级到v4后收到此错误的用户来说，备份本身极有可能无法正常工作，您需要尝试其他提到的恢复方法。
- 您还可以尝试恢复数据库。这通常是此问题发生在更新后的唯一选择。尝试[sqlite3 `.recover`命令](/useful-tools#recovering-a-corrupt-db)
  - 如果您的sqlite没有`.recover`命令，或者您希望使用更友好的GUI（例如Windows），请按照[我们在此wiki上的说明](/useful-tools#recovering-a-corrupt-db-ui)进行操作。
- 数据库出现错误的另一个可能原因是您将数据库放在网络驱动器上（nfs或smb或其他不是本地的驱动器）。**SQLite是为数据和应用程序共存于同一台机器上的情况而设计的。**因此，您的\*Arr AppData文件夹（docker的/config挂载）必须位于本地存储上。[SQLite和网络驱动器不兼容，最终会导致数据库损坏](https://www.sqlite.org/draft/useovernet.html)。
- 如果您使用mergerFS，您需要删除`direct_io`，因为SQLite使用的是mmap，而`direct_io`不支持，如mergerFS的[文档中所解释的](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)。

## 我在Mac上使用Radarr，突然停止工作了。发生了什么？

- 最有可能的原因是MacOS的一个错误导致其中一个数据库损坏。
- 请参阅上面的数据库损坏条目。
- 然后尝试启动并查看是否正常工作。如果不起作用，您将需要进一步的支持。在我们的[Reddit /r/radarr](http://reddit.com/r/radarr)上发布或加入[我们的Discord](https://radarr.video/discord)寻求帮助。

## 为什么Radarr无法看到我在远程服务器上的文件？

- 对于所有操作系统，请确保您正在运行\*Arr的用户/组具有对挂载驱动器的读写访问权限。
- 对于Linux，请确保：
  - 如果您使用的是NFS挂载，请确保启用了`nolock`。
  - 如果您使用的是SMB挂载，请确保启用了`nobrl`。
- 对于Windows：简而言之，\*Arr正在运行的用户（如果是服务）或在其下运行的用户（如果是托盘应用程序）无法访问远程服务器上的文件路径。这可能是由于各种原因，但最常见的是\*Arr正在作为服务运行，这会导致下面描述的问题。

### Radarr默认在LocalService帐户下运行，该帐户无法访问受保护的远程文件共享

- 将Radarr服务运行为具有对该共享的访问权限的其他用户
- 在Windows服务器上打开“管理工具”\>“服务”窗口。
- 停止Radarr服务。
- 打开“属性”\>“登录”对话框。
- 将服务用户帐户更改为目标用户帐户。
- 使用启动文件夹运行Radarr.exe

### 您正在使用映射的网络驱动器（而不是UNC路径）

- 将路径更改为UNC路径（`\\server\share`）
- 通过启动文件夹运行Radarr.exe

## 如何从Windows服务更改为托盘应用程序？

1. 关闭Radarr
1. 运行Radarr目录中的serviceuninstall.exe
1. 以管理员身份运行一次`Radarr.exe`，以获得适当的权限并打开防火墙。完成后，您可以关闭它并正常运行。
1. （可选）在启动文件夹中放置一个.exe的快捷方式，以便在启动时自动启动。

## 帮助，我被锁定了

{#help-i-have-forgotten-my-password}

要禁用身份验证（以重置您忘记的用户名或密码），您需要编辑`config.xml`，该文件位于[Radarr Appdata目录](/radarr/appdata-directory)中

1. 用文本编辑器打开config.xml
1. 找到身份验证方法行，它将是
`<AuthenticationMethod>Basic</AuthenticationMethod>`或`<AuthenticationMethod>Forms</AuthenticationMethod>`
1. 将`AuthenticationMethod`行更改为`<AuthenticationMethod>None</AuthenticationMethod>`
1. 重新启动Radarr
1. 现在可以在没有密码的情况下访问Radarr，您应该在UI的“设置：常规”中设置您的用户名和密码

## 如何停止浏览器在启动时自动打开？

根据您的操作系统，有多种可能的方法。

- 在某些操作系统上，在“设置”=>“常规”中，有一个复选框可以在启动时打开浏览器。
- 在调用Radarr时，您可以在参数中添加`-nobrowser`（*nix）或`/nobrowser`（Windows）。
- 停止Radarr并编辑config.xml文件，将`<LaunchBrowser>True</LaunchBrowser>`更改为`<LaunchBrowser>False</LaunchBrowser>`。

## 奇怪的UI问题

- 如果您遇到任何奇怪的UI问题，比如库页面不显示任何内容或某个视图或排序不起作用，请尝试在Chrome的隐身窗口或Firefox的隐私窗口中查看。如果在那里正常工作，请清除特定IP/域的浏览器缓存和Cookie。有关更多信息，请参见[清除缓存、Cookie和本地存储](/useful-tools#clearing-cookies-and-local-storage)的wiki文章。

## 仅在Windows上以localhost加载Web界面

- 如果您只能在<http://localhost:7878/>或<http://127.0.0.1:7878/>上访问您的Web界面，您需要至少以管理员身份运行一次。

## 权限

- Radarr需要将文件从下载器放置的位置移动到最终位置，因此这意味着需要读写源目录和目标目录以及文件。
- 在Linux上，最佳实践是将服务作为其自己的用户运行，这可能意味着使用共享组并将文件夹权限设置为`775`，文件权限设置为`664`，无论是在下载器中还是在\*Arr中。在umask表示法中，这将是`002`。

## 系统和日志加载永远

- 这是由于Easy-privacy拦截列表引起的。它们基本上会阻止任何包含`/api/log?`的URL。请查看列表，告诉我您是否认为阻止该列表中的所有URL是明智的，其中有数十个URL可能会破坏网站。您在广告拦截器中选择了该选项。简单的解决方法是将Radarr运行的域名添加到白名单中。但我仍然建议检查列表。

## 解压缩种子

- 大多数种子客户端不会自动处理压缩的存档文件，就像它们的Usenet对应物一样。我们推荐使用[unpackerr](https://github.com/unpackerr/unpackerr)。

## uTorrent不再工作

- 确保Web UI已启用
- 确保Alt Listening Port（高级=> Web UI）与Listening Port（连接）不相同
- 我们建议更改Web UI Alt Listening Port，以避免干扰连接的任何端口转发。

## 我收到一个弹出窗口，说config.xml损坏了，现在怎么办？

- Radarr在启动时无法读取您的配置文件，因为它以某种方式损坏了。为了恢复在线状态，您需要删除您的[appdata-directory](/radarr/appdata-directory)中的`.xml`文件，一旦删除，启动并将在默认端口（7878）上启动，现在您应该重新配置在常规设置页面上配置的任何设置。

## 无效的证书和其他HTTPS或SSL问题

- 如果你的下载客户端停止工作，并且出现类似于“本地主机是无效证书”的错误？
  - Radarr会验证SSL证书。如果下载客户端中没有设置SSL证书，或者你正在使用未添加到本地证书存储中的自签名https证书，则会拒绝连接。你可以从[let's encrypt](https://letsencrypt.org/)获取免费的正确签名证书。
  - 如果你的下载客户端和Radarr在同一台机器上，没有理由使用HTTPS，所以最简单的解决方案是禁用连接的SSL。大多数人都同意，在本地网络上也不需要使用SSL。如果你想保持不安全的SSL设置，可以在高级设置中禁用证书验证。

## VPN、Jackett和\*ARRs

- 除非你在中国、澳大利亚或南非等压制言论的国家，否则你的种子客户端通常是唯一需要使用VPN的软件。因为VPN终端点被许多用户共享，你可能会遇到各种服务的速率限制、DDOS保护和IP封禁。
- 换句话说，将\*Arrs（Lidarr、Prowlarr、Radarr、Readarr和Lidarr）放在VPN后面可能会导致应用程序在某些情况下无法使用，因为这些服务无法访问。

> **需要明确的是，VPN会导致\*Arrs出现问题，而不是是否会出现问题：图像提供商会阻止你，而Cloudflare位于大多数\*Arr服务器（更新、元数据等）之前，也有可能阻止你**
{.is-warning}

- **许多私有跟踪器会禁止使用或访问它们（例如使用Jackett或Prowlarr）的VPN用户。**

### 使用VPN

- 如果需要使用VPN并且使用Docker，建议使用Hotio或Binhex的下载客户端+VPN容器。
- 如果需要使用VPN并且不使用Docker，你的VPN客户端***必须***支持分隔隧道，以便只有所需的（下载客户端）应用程序位于VPN后面。
- 使用Google或Cloudflare的DNS服务器可以解决访问跟踪器的许多问题，而不是使用ISP的DNS服务器。
- 在某些情况下（例如英国的ISP），你可能需要将种子下载客户端放在VPN后面，并按以下方式设置Jackett/Prowlarr：
  - 将Jackett放在VPN后面，并确保分隔隧道允许本地访问
  - 对于Prowlarr，配置你的VPN客户端提供代理，并在设置=>索引器中添加代理。给代理添加一个标签，需要使用它的任何索引器也使用相同的标签。
    - 如果绝对需要，而你的VPN没有提供创建代理的方法，你可以将Prowlarr放在VPN后面，并确保分隔隧道允许本地访问。

# Radarr搜索和下载常见问题

## 为什么我无法向Radarr添加新电影？

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarr使用[The Movie Database (TMDb)](http://themoviedb.org)提供电影信息和图片，如风景图、横幅和背景图。通常，你无法添加电影的原因有几个：
  - TMDb不喜欢在通过API（Radarr使用的）搜索电影时使用特殊字符，所以尝试使用翻译后的名称进行搜索，或者不使用特殊字符进行搜索。
  - 你也可以通过TMDb ID或者如果TMDb有的话，IMDb ID进行添加。
  - 该电影尚未添加到TMDb，请按照他们的[指南](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006)将其添加到TMDb。

## Jackett显示的结果比手动搜索的结果多

- 这通常是因为你在Jackett上进行的搜索方式与手动搜索不同。请参阅我们的[故障排除文章](/radarr/troubleshooting)获取更多信息。

## Radarr如何确定电影的年份？

- Radarr从[TMDb](https://www.themoviedb.org/)获取元数据。
- Radarr使用最早的**院线首映**日期和最早的**首映**日期进行匹配。
  - 请注意，如果不存在院线首映日期，则逻辑将回退到最早的实体或数字发布日期。
- 如果电影缺少数字、实体、院线或首映发布日期，则应更新TMDb。
- [TMDb的贡献指南](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013)中对其发布类型的说明如下：
  - **首映** - 首映放映可以是电影节放映（例如TIFF）或在大城市（例如洛杉矶、伦敦、多伦多）举行的与演员和剧组人员的首映活动。
  - **院线** - 可用于原始发布和任何后续官方发布。用于广泛或饱和发布。在美国，600-1,999个屏幕被认为是广泛发布，2000个以上被认为是饱和发布。
  - **院线（有限）** - 有限的院线发行是一种电影分发策略，即在一个国家的几个电影院中发布新电影，通常是在主要大都市市场。在美国，电影院的数量少于600个。
  - **实体** - 包括所有VHS、DVD和蓝光发布。
  - **数字** - 可以添加所有相关的发布，包括流媒体平台、VOD租赁或购买。数字放映包括在线电影节和虚拟影院发布也属于数字发布。

## Radarr如何处理外语电影或外语标题？

> [TRaSH的自定义格式语言指南](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats)可能对帮助你获取所需语言的电影有用。{.is-info}

> 从2023年2月12日开始，Radarr的元数据缓存将开始将电影的原始语言视为TMDb的口语语言，前提是该电影在TMDb上只有一种口语语言；否则将使用电影的原始TMDb语言。
{.is-warning}

## ID搜索

- **支持基于ID的索引器** - 在支持基于ID（TMDbId、IMDbId等）的搜索的索引器和跟踪器上进行搜索 - 例如许多Usenet索引器和许多私有Torrent跟踪器 - 如果基于ID的搜索返回结果，则不使用文本查询。如果你的索引器缺少结果，则是因为它们将发布与错误的电影ID相关联。
  - 发布的语言也可以从索引器或跟踪器的发布语言中获取，而不是从名称中解析

## 文本搜索

- **不支持基于ID的搜索或基于ID的搜索没有结果的索引器** - 搜索将使用电影的原始标题、英文标题和从[你在电影质量配置文件中首选的任何语言以及在质量配置文件中得分大于零的任何自定义格式](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/)中的翻译标题。
- 解析（即导入）将在所有翻译和替代标题中寻找匹配项。
  - 发布的语言也可以从索引器或跟踪器的发布语言中获取，而不是从名称中解析

## 获取外语电影

- 要获取外语电影，请将电影的质量配置文件语言设置为原始语言（电影的原始语言\*）、该配置文件的特定语言或`Any`，并创建得分大于0的[具有语言条件的自定义格式，以确定要获取的语言 - 详细信息请参见链接的TRaSH指南](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/)。
- 请注意，这不包括在索引器的设置中配置为`multi`的任何索引器语言。
  - 请注意，从[Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c)开始，Radarr不再默认将`multi`包括英语在内。
  - 用户可以根据索引器自定义其设置，以定义`multi`表示的语言是什么

## Radarr如何处理名称中的“multi”？

- 从Radarr v4.1+开始，Radarr假设`multi`只是电影的语言，**而不是**以前版本中的英语。
  - 用户可以根据索引器自定义其设置，以定义`multi`表示的语言是什么
- 请注意，`multi`定义仅适用于发布解析，而不适用于外语标题或电影搜索。

## 帮助，电影已添加，但未搜索

- Radarr不会自动*主动*搜索丢失的电影。相反，它会定期查询所有配置为RSS的索引器的新帖子。当该列表中出现所需的或未满足截止条件的电影时，它将被下载。这意味着在电影发布（或重新发布）之前，它不会被下载。
- 如果你添加的电影是你现在想要的，最好的选择是勾选“开始搜索丢失的电影”框，位于*添加电影*（**1**）按钮的左侧。你也可以转到你添加的电影的页面，点击放大镜“搜索”（**2**）按钮，或者使用Wanted视图搜索丢失的或未满足截止条件的电影。

  - 添加电影时添加并搜索电影
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - 搜索现有电影
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jackett的/all端点

{#jackett-all-endpoint}

- Jackett的`/all`端点很方便，但它只有这一个好处。其他一切都可能出现问题，因此需要单独添加每个跟踪器。或者，你可以考虑使用Jackett和NZBHydra2的替代方案[Prowlarr](/prowlarr)

- **2022年1月1日更新：由于只会引起问题，Jackett的`/all`端点已在4.0.0.5730版本中停止支持（例如会出现警告）。**

- Jackett的`/all`端点很方便，但它只有这一个好处。其他一切都可能出现问题，因此现在需要单独添加每个跟踪器。
- [即使Jackett的开发人员也表示应该避免使用`/all`端点，不应该使用它。](https://github.com/Jackett/Jackett#aggregate-indexers)
- 使用`/all`端点没有任何优势，只有劣势：
  - 你失去了对索引器特定设置（类别、搜索模式等）的控制
  - 混合使用搜索模式（IMDB、查询等）可能导致低质量的结果
  - 无法使用索引器特定的类别（\>= 100000）
  - 慢速索引器会降低整体结果的速度
  - 总结果限制为1000
  - 如果/all中的一个跟踪器返回错误，\*Arr将禁用它，你将无法获得任何结果。

### Jackett /All的解决方案

- 在\*Arr中手动将每个跟踪器添加为索引器
- 查看[Lidarr/Radarr/Readarr开发团队](/prowlarr)的[Prowlarr](/prowlarr)，它可以将索引器同步到\*Arr中。
- 查看[NZBHydra2](https://github.com/theotherp/nzbhydra2)，它可以将索引器同步到\*Arr中。但不要使用它们的单个聚合端点，而是使用`multi`（如果将使用同步）。

## 为什么会有两个文件？| 为什么下载文件夹中会有一个文件剩下？

这是正常现象。如果设置支持[硬链接](https://trash-guides.info/hardlinks)，则不会使用额外的空间。以下是种子处理的过程。

1. Radarr将下载请求发送到你的客户端，并将其与你在下载客户端设置中配置的标签或类别名称关联起来。例如：movies、tv、series、music等。
1. Radarr通过你的下载客户端的API监视使用该类别名称的活动下载。此监视通过你的下载客户端的API进行。
1. 完成的文件保留在其原始位置，以便你可以进行做种（可以在下载客户端或在特定下载客户端下进行调整上传比率或时间）。当文件导入到你的媒体文件夹时，如果你的设置支持硬链接，将创建硬链接；如果不支持硬链接，则进行复制。
1. 如果在Radarr的设置中启用了“完成下载处理 - 删除完成”选项，当下载客户端报告做种完成并且种子已停止（即暂停）时，Radarr将删除原始文件和种子。有关如何优化配置下载客户端的详细信息，请参阅[TRaSH的下载客户端指南](https://trash-guides.info/Downloaders/)。

> 硬链接默认已启用。[硬链接不会使用任何额外的磁盘空间。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)完成下载目录和媒体库的文件系统和挂载点必须相同。如果硬链接创建失败或者你的设置不支持硬链接，则会回退并复制文件。
{.is-info}

## 为什么Radarr无法在反向代理后工作

- 从v3开始，Radarr切换到了.NET和一个新的Web服务器。为了使SignalR工作、使UI按钮工作、使数据库更改生效以及其他项目，需要在Radarr的位置块中添加以下内容：

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- 确保**不要**包括nginx文档中建议的`proxy_set_header Connection "Upgrade";`。**这样不会起作用**
- [参见此ASP.NET Core问题](https://github.com/aspnet/AspNetCore/issues/17081)
- 如果你使用类似Cloudflare的CDN，请确保启用了Websockets以允许Websocket连接。
- 如果出现意外重定向，请确保已转发主机头。