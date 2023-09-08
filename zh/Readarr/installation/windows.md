---
title: Readarr Windows 安装
description: Readarr 的 Windows 安装指南
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr 在 Windows 上有原生支持。可以将 Readarr 安装在 Windows 上作为 Windows 服务或系统托盘应用程序。
> Windows 版本的支持仅限于 Microsoft 当前支持的版本，其他版本可能可以使用，但这是一个不受支持的配置
{.is-warning}

Windows 服务在用户未登录时也会运行，但需要特别注意，因为 Windows 服务[无法访问网络驱动器](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives)（X:\ 映射驱动器或 \\\server\share UNC 路径）而不进行特殊配置。

此外，Windows 服务以“本地服务”帐户运行，默认情况下，该帐户**没有权限访问用户的主目录，除非手动分配了权限**。这在使用配置为下载到主目录的下载客户端时尤为重要。

因此，如果用户可以保持登录状态，建议将 Readarr 安装为系统托盘应用程序。安装程序提供了这样的选项。

> 如果在安装后出现访问错误（例如访问路径 `C:\ProgramData\Readarr\config.xml` 被拒绝）或者使用了映射网络驱动器，则可能需要以“管理员”身份运行一次。这样可以给予 Readarr 所需的权限。您不应该每次都需要以管理员身份运行。
{.is-warning}

> 警告：如果您通过 [PmsService](https://github.com/cjmurph/PmsService) 将 Plex 作为服务运行，则需要将 PMsService 的端口从 `8787` 更改为 Readarr 在 `config.xml` 文件中运行的端口。
{.is-info}

1. 下载适用于您的架构的最新版本的 Readarr，链接如下。
1. 运行安装程序。
1. 浏览到 <http://localhost:8787> 开始使用 Readarr。

- [Windows x64 安装程序](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 安装程序](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> 也可以使用 [x64 .zip 下载](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64) 手动安装 Readarr。但在这种情况下，您必须手动处理依赖项、安装和权限。
{.is-info}