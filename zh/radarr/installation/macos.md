---
title: Radarr MacOS 安装
description: Radarr 的 MacOS 安装指南
published: true
date: 2023-07-28T09:08:51.541Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:05.036Z
---

# MacOS (OSX)

{#OSX}

> 由于 .NET 不兼容性，Radarr 不支持低于 10.15（Catalina）版本的 OSX。
{.is-warning}

1. 根据您的系统，下载 [MacOS 应用程序](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) 或者 [MacOS M1 应用程序](https://radarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)。
1. 打开压缩文件并将 Radarr 图标拖到您的应用程序文件夹中。
1. 自签名 Radarr：`codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine /Applications/Radarr.app`
1. 在浏览器中访问 <http://localhost:7878> 开始使用 Radarr。

> Radarr 使用捆绑的 ffprobe 版本进行媒体文件分析，不需要在系统上安装 ffprobe 或 ffmpeg。如果 Radarr 提示找不到 Ffprobe，通常可以通过重新安装来解决。
{.is-info}