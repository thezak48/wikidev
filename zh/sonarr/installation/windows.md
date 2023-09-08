---
title: Sonarr Windows 安装
description: Sonarr 的 Windows 安装指南
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

Sonarr 在 Windows 上有原生支持。Sonarr 可以作为 Windows 服务或系统托盘应用程序安装。

> 仅支持当前由 Microsoft 支持的 Windows 版本，其他版本可能可以使用，但这是不受支持的配置。
{.is-warning}

Windows 服务在用户未登录时也会运行，但是需要特别注意，因为 Windows 服务在没有特殊配置的情况下**无法访问网络驱动器**（如 X:\ 映射的驱动器或 \\\server\share UNC 路径）。

此外，Windows 服务使用的是“本地服务”账户，**默认情况下该账户没有权限访问用户的主目录，除非手动分配了权限**。这在使用配置为下载到用户主目录的下载客户端时尤为重要。

因此，如果用户可以保持登录状态，建议将 Sonarr 安装为系统托盘应用程序。安装程序提供了这个选项。

> 如果在安装后出现访问错误（例如访问路径 `C:\ProgramData\Sonarr\config.xml` 被拒绝）或者使用了映射的网络驱动器，您可能需要以管理员身份运行一次。这将给予 Sonarr 所需的权限。您不应该每次都需要以管理员身份运行。
{.is-warning}

1. 下载与您的架构相对应的最新版本 Sonarr，链接如下。
1. 运行安装程序。
1. 在浏览器中打开 <http://localhost:8989>，开始使用 Sonarr。

- [Windows x32 安装程序](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> 您也可以使用 [x32 .zip 下载](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows) 手动安装 Sonarr。但在这种情况下，您必须手动处理依赖项、安装和权限。
{.is-info}