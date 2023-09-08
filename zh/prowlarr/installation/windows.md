---
title: Prowlarr Windows 安装
description: Prowlarr 的 Windows 安装指南
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr 在 Windows 上有原生支持。Prowlarr 可以作为 Windows 服务或系统托盘应用程序安装。
> 仅支持 Microsoft 当前支持的 Windows 版本，其他版本可能可以使用，但这是一个不受支持的配置
{.is-warning}

Windows 服务会在用户未登录时运行。
否则，如果用户可以保持登录状态，可以使用系统托盘应用程序。安装程序会提供此选项。

> 如果出现访问错误（例如拒绝访问路径 `C:\ProgramData\Prowlarr\config.xml`），您可能需要以管理员身份运行一次。这将授予 Prowlarr 所需的权限。您不应该每次都需要以管理员身份运行。
{.is-warning}

1. 下载与您的架构相对应的最新版本的 Prowlarr，链接如下。
1. 运行安装程序。
1. 浏览到 <http://localhost:9696> 开始使用 Prowlarr。

- [Windows x64 安装程序](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 安装程序](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> 您也可以使用 [x64 .zip 下载](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64) 手动安装 Prowlarr。但在这种情况下，您必须手动处理依赖项、安装和权限。
{.is-info}

> 如果您在同一台机器上使用 [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/) 来管理 IIS 的 LetsEncrypt 证书，并且正在安装 Prowlarr，则后台服务将使用端口 `9696`。您需要将 Prowlarr 的监听端口在 `config.xml` 中更改为其他端口，或者更改 Certify The Web 后台服务的端口。
{.is-info}