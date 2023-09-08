---
title: Lidarr Windows 安装
description: Lidarr 的 Windows 安装指南
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr 在 Windows 上有原生支持。Lidarr 可以作为 Windows 服务或系统托盘应用程序安装。
> Windows 版本的支持仅限于当前由 Microsoft 支持的版本，其他版本可能可以使用，但这是不受支持的配置。
{.is-warning}

Windows 服务在用户未登录时也可以运行，但是需要特别注意，因为 Windows 服务[无法访问网络驱动器](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives)（映射为 X:\ 的驱动器或 \\\server\share 的 UNC 路径）而不进行特殊配置。

此外，Windows 服务以“本地服务”帐户运行，默认情况下，该帐户**没有权限访问用户的主目录，除非手动分配了权限**。这在使用配置为下载到主目录的下载客户端时尤为重要。

因此，如果用户可以保持登录状态，建议将 Lidarr 安装为系统托盘应用程序。安装程序提供了这样的选项。

> 如果在托盘模式下安装后出现访问错误（例如拒绝访问路径 `C:\ProgramData\Lidarr\config.xml`），或者使用了映射的网络驱动器，则可能需要以“管理员”身份运行一次。这将给予 Lidarr 所需的权限。您不应该每次都需要以管理员身份运行。
{.is-warning}

1. 下载与您的架构相对应的最新版本的 Lidarr，链接如下。
1. 运行安装程序。
1. 在浏览器中打开 <http://localhost:8686>，开始使用 Lidarr。

- [Windows x64 安装程序](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 安装程序](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> 您也可以使用 [x64 .zip 下载](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64) 手动安装 Lidarr。但在这种情况下，您必须手动处理依赖项、安装和权限。
{.is-info}