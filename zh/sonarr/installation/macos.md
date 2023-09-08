---
title: Sonarr MacOS 安装
description: Sonarr 的 MacOS 安装指南
published: true
date: 2023-07-28T11:15:29.588Z
tags: sonarr
editor: markdown
dateCreated: 2023-07-03T20:13:29.890Z
---

# MacOS (OSX)

{#OSX}

> 由于 .NET 不兼容性，Sonarr 最终将不再支持 OSX 版本低于 10.15（Catalina）的系统。
{.is-warning}

1. 下载 [MacOS 应用](https://services.sonarr.tv/v1/download/main/latest?version=3&os=macos&installer=true)
1. 打开压缩文件并将 Sonarr 图标拖动到应用程序文件夹中。
1. 自签名 Sonarr `codesign --force --deep -s - /Applications/Sonarr.app && xattr -rd com.apple.quarantine /Applications/Sonarr.app`
1. 在浏览器中访问 <http://localhost:8989> 开始使用 Sonarr