---
title: Radarr Windows 安装
description: Radarr 的 Windows 安装指南
published: true
date: 2023-07-04T15:22:03.589Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:19.928Z
---

# Windows

Radarr 在 Windows 上有原生支持。可以将 Radarr 安装为 Windows 服务或系统托盘应用程序。
> 仅支持当前由 Microsoft 支持的 Windows 版本，其他版本可能可以使用，但这是不受支持的配置。
{.is-warning}

Windows 服务即使用户未登录也会运行，但是需要特别注意，因为 Windows 服务在没有特殊配置的情况下**无法访问网络驱动器**（如 X:\ 映射驱动器或 \\\server\share UNC 路径）。

此外，Windows 服务是在“本地服务”帐户下运行的，默认情况下，**该帐户没有权限访问用户的主目录，除非手动分配了权限**。这在使用配置为下载到主目录的下载客户端时尤为重要。

因此，如果用户可以保持登录状态，建议将 Radarr 安装为系统托盘应用程序。安装程序提供了这样的选项。

> 如果在安装后出现访问错误（例如访问路径 `C:\ProgramData\Radarr\config.xml` 被拒绝）或者使用了映射网络驱动器，您可能需要以“管理员”身份运行一次。这样可以给予 Radarr 所需的权限。您不应该每次都需要以管理员身份运行。
{.is-warning}

1. 下载与您的架构相对应的最新版本的 Radarr，链接如下。
1. 运行安装程序。
1. 浏览到 <http://localhost:7878> 开始使用 Radarr。

- [Windows x64 安装程序](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 安装程序](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> 您也可以使用 [x64 .zip 下载](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64) 手动安装 Radarr。但在这种情况下，您必须手动处理依赖项、安装和权限。
{.is-info}