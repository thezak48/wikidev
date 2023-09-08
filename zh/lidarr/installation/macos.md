---
title: Lidarr MacOS 安装
description: Lidarr 的 MacOS 安装指南
published: true
date: 2023-07-28T11:16:00.388Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:53.957Z
---

# MacOS (OSX)

{#OSX}

> 由于 .NET 不兼容性，Lidarr 不支持低于 10.15（Catalina）版本的 OSX。
{.is-warning}

1. 下载 [MacOS 应用程序](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) 或者 [MacOS M1 应用程序](https://lidarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)，根据你的系统选择。
1. 打开压缩文件，并将 Lidarr 图标拖动到你的应用程序文件夹中。
1. 自签名 Lidarr：`codesign --force --deep -s - /Applications/Lidarr.app && xattr -rd com.apple.quarantine /Applications/Lidarr.app`
1. 在浏览器中访问 <http://localhost:8686> 开始使用 Lidarr。