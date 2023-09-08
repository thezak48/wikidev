---
title: Prowlarr MacOS 安装
description: Prowlarr 的 MacOS 安装指南
published: true
date: 2023-07-28T11:17:40.904Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:30.382Z
---

# MacOS (OSX)

{#OSX}
  
> 由于 .NET 不兼容性，Prowlarr 不支持 OSX 版本低于 10.15（Catalina）。
{.is-warning}

1. 下载 [MacOS 应用程序](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=x64&installer=true) 或者 [MacOS M1 应用程序](https://prowlarr.servarr.com/v1/update/master/updatefile?os=osx&runtime=netcore&arch=arm64&installer=true)，根据你的系统选择。
1. 打开压缩文件，并将 Prowlarr 图标拖动到你的应用程序文件夹中。
1. 自签名 Prowlarr：`codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine /Applications/Prowlarr.app`
1. 在浏览器中访问 <http://localhost:9696> 开始使用 Prowlarr。