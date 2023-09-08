- No, you cannot disable the refresh books task in Readarr. The refresh books task is responsible for updating the metadata and status of your books, ensuring that the information in Readarr is accurate and up to date. Disabling this task would result in outdated and incorrect information in your library.

- 不，也不应该通过任何SQL黑客手法来实现。刷新图书任务会查询上游的Servarr代理，并检查每本书的元数据（ID、演员、摘要、评分、翻译、替代标题等）是否与Readarr中的当前元数据有更新。如果有必要，它将更新相应的图书。
- 一个常见的问题是刷新任务会导致大量的I/O使用。可能会导致问题的一个设置是“刷新后重新扫描作者文件夹”。如果在刷新期间磁盘I/O使用量飙升，您可能需要将重新扫描设置更改为“手动”。除非您所有对图书馆的更改（新书、升级、删除等）都是通过Readarr进行的，否则不要将其更改为“从不”。如果您手动删除图书文件或使用第三方程序进行删除，请不要将其设置为“从不”。

## 我可以同时拥有同一本书的电子书和有声书版本吗？

- 不可以。在单个Readarr实例中，您只能拥有其中之一，而不能同时拥有两者。如果您想要同时拥有两者，您需要运行两个独立的Readarr实例（就像有些人运行两个Sonarr或Radarr实例一样，一个用于1080p版本，一个用于4K版本）。

## 我需要使用Calibre吗？

- 不需要。一般来说，Calibre提供了一些进一步的增强功能，比如自动将电子书转换为适合您的电子阅读器的另一种格式，并与该电子阅读器连接。但是，如果您在安装Readarr之前没有运行Calibre，那么安装它可能对您的益处有限，而且它是一个非常庞大的程序。

## 为什么Readarr无法看到我在远程服务器上的文件？

- 对于所有操作系统，请确保您正在运行\*Arr的用户/组具有对挂载驱动器的读写访问权限。
- 对于Linux，请确保：
  - 如果您使用的是NFS挂载，请确保为您的挂载启用了nolock。
  - 如果您使用的是SMB挂载，请确保为您的挂载启用了nobrl。
- 对于Windows：简而言之，\*Arr正在运行的用户（如果是服务）或正在其下运行的用户（如果是托盘应用程序）无法访问远程服务器上的文件路径。这可能是由于各种原因引起的，但最常见的是\*Arr正在作为服务运行，这会导致下面描述的问题。

### Readarr默认在LocalService帐户下运行，该帐户无法访问受保护的远程文件共享

- 将Readarr服务作为具有对该共享的访问权限的其他用户运行
- 在Windows服务器上打开“管理工具”>“服务”窗口。
- 停止Readarr服务。
- 打开“属性”>“登录”对话框。
- 将服务用户帐户更改为目标用户帐户。
- 使用启动文件夹运行Readarr.exe

### 您正在使用映射的网络驱动器（而不是UNC路径）

- 将您的路径更改为UNC路径（`\\server\share`）
- 通过启动文件夹运行Readarr.exe

## 帮助，我被锁在外面了

{#help-i-have-forgotten-my-password}

要禁用身份验证（以重置您忘记的用户名或密码），您需要编辑`config.xml`文件，该文件位于[Readarr应用数据目录](/readarr/appdata-directory)中。

1. 用文本编辑器打开config.xml文件
2. 找到身份验证方法行，它将是`<AuthenticationMethod>Basic</AuthenticationMethod>`或`<AuthenticationMethod>Forms</AuthenticationMethod>`
3. 将`AuthenticationMethod`行更改为`<AuthenticationMethod>None</AuthenticationMethod>`
4. 重新启动Readarr
5. 现在可以在没有密码的情况下访问Readarr，您应该在UI中的“设置：常规”中设置您的用户名和密码

## 如何停止浏览器在启动时自动打开？

根据您的操作系统，有多种可能的方法。

- 在某些操作系统上，在“设置”=>“常规”中，有一个复选框可以在启动时打开浏览器。
- 在调用Readarr时，您可以在参数中添加`-nobrowser`（*nix）或`/nobrowser`（Windows）。
- 停止Readarr并编辑config.xml文件，将`<LaunchBrowser>True</LaunchBrowser>`更改为`<LaunchBrowser>False</LaunchBrowser>`。

## 奇怪的用户界面问题

- 如果您遇到任何奇怪的用户界面问题，比如图书馆页面没有列出任何内容，或者某个视图或排序不起作用，请尝试在Chrome的隐身窗口或Firefox的隐私窗口中查看。如果在那里正常工作，请清除特定IP/域名的浏览器缓存和cookie。有关更多信息，请参阅[清除缓存、Cookie和本地存储](/useful-tools#clearing-cookies-and-local-storage)维基文章。

## VPN、Jackett和\*ARRs

- 除非您身处中国、澳大利亚或南非等压制性国家，否则通常只有您的种子客户端需要在VPN后面。由于VPN终点由许多用户共享，您可能会遇到各种服务使用的速率限制、DDOS保护和IP封禁问题。
- 换句话说，将\*Arrs（Lidarr、Prowlarr、Radarr、Readarr和Lidarr）放在VPN后面可能会导致应用程序在某些情况下无法使用，因为这些服务无法访问。

> **明确一点，VPN是否会对\*Arrs造成问题不是问题，而是何时会有问题：图像提供商会阻止您，而Cloudflare位于大多数\*Arr服务器（更新、元数据等）的前面，也有可能阻止您**
{.is-warning}

- **许多私有跟踪器会因使用或通过VPN访问它们（例如使用Jackett或Prowlarr）而封禁您。**

### 使用VPN

- 如果需要VPN并且使用Docker，则建议使用Hotio或Binhex的Download Client + VPN容器。
- 如果需要VPN并且不使用Docker，则您的VPN客户端***必须***支持分割隧道，以便只有所需的（下载客户端）应用程序位于VPN后面。
- 使用Google或Cloudflare的DNS服务器代替您的ISP的DNS服务器，可以解决访问跟踪器的许多问题。
- 在某些情况下（例如英国的ISP），您可能需要将种子下载客户端放在VPN后面，并按照以下方式设置Jackett/Prowlarr：
  - 将Jackett放在VPN后面，并确保分割隧道允许本地访问
  - 对于Prowlarr，请配置您的VPN客户端提供代理，并在“设置”=>“索引器”中添加代理。给代理添加一个标签，并将需要使用该代理的任何索引器添加相同的标签。
    - 如果绝对需要，且您的VPN没有提供创建代理的方法，您可以将Prowlarr放在VPN后面，并确保分割隧道允许本地访问。

## Jackett的/all端点

{#jackett-all-endpoint}

- Jackett的`/all`端点很方便，但这只是它的一个好处。其他一切都可能导致问题，因此需要单独添加每个跟踪器。或者，您可以考虑使用Jackett和NZBHydra2的替代方案[Prowlarr](/prowlarr)
- **2022年1月20日更新：Jackett的`/all`端点已在0.1.0.1188版本中停止支持（例如会出现警告），因为它只会引起问题。**
- Jackett的/all端点很方便，但这只是它的一个好处。其他一切都可能导致问题，因此现在需要单独添加每个跟踪器。
- [即使Jackett的开发人员也表示应避免使用/all端点，不应使用它。](https://github.com/Jackett/Jackett#aggregate-indexers)
- 使用/all端点没有任何优势，只有劣势：
  - 您失去了对索引器特定设置（类别、搜索模式等）的控制。
  - 混合使用搜索模式（IMDB、查询等）可能会导致低质量的结果。
  - 无法使用索引器特定的类别（>= 100000）。
  - 慢速索引器会减慢整体结果。
  - 总结果限制为1000。
  - 如果/all中的一个跟踪器返回错误，\*Arr将禁用它，您将无法获得任何结果。

### Jackett /All的解决方案

- 在Jackett中手动将每个跟踪器添加为索引器
- 查看[Prowlarr](/prowlarr)，它可以将索引器同步到\*Arr，并来自Lidarr/Radarr/Readarr开发团队。
- 查看[NZBHydra2](https://github.com/theotherp/nzbhydra2)，它可以将索引器同步到\*Arr。但不要使用它们的单个聚合端点，而是使用`multi`如果要使用同步。

## 为什么会有两个文件？| 为什么下载文件夹中会有一个文件剩下？

这是正常现象。如果设置支持[硬链接](https://trash-guides.info/hardlinks)，则不会使用双倍的空间。以下是种子处理的工作原理。

1. Readarr将向您的客户端发送下载请求，并将其与您在下载客户端设置中配置的标签或类别名称关联。例如：电影、电视、系列、音乐等。
2. Readarr将通过您的下载客户端的API监视使用该类别名称的活动下载。此监视通过您的下载客户端的API进行。
3. 完成的文件将保留在其原始位置，以便您可以继续做种（可以在下载客户端或在特定下载客户端下进行调整比率或时间）。当文件导入到您的媒体文件夹时，如果您的设置支持硬链接，将会创建硬链接，否则将会复制文件。
4. 如果在Readarr的设置中启用了“完成下载处理 - 删除已完成”选项，那么只有在下载客户端报告做种完成并停止种子时，Readarr才会删除原始文件和种子。

> 硬链接默认已启用。[硬链接不会使用任何额外的磁盘空间。](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/)完成下载目录和媒体库的文件系统和挂载点必须相同。如果硬链接创建失败或您的设置不支持硬链接，则会退回并复制文件。
{.is-info}

## Calibre显示“Calibre rejected duplicate book”，但实际上并不是重复的

如果您正在使用Calibre集成，Calibre偶尔会拒绝一本书，称其为重复的。实际上它可能并不是重复的。如果发生这种情况，Readarr无能为力，您需要取消监视该书籍，以防止Readarr继续尝试抓取并推送到Calibre。这只是Calibre集成的有趣缺点之一。