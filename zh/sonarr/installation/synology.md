---
title: Sonarr Synology 安装
description: Sonarr 的 Synology 安装指南
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [SynoCommunity 创建、支持和维护 Synology NAS Package](https://synocommunity.com/package/nzbdrone)

> NAS package 维护较差，经常过时。如果您的 NAS 支持 Docker，强烈建议[使用 Docker 运行](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)。由于 NAS package 过时且未配置在启动时自动更新，因此您将无法重新安装 Sonarr，必须手动清除数据库。{.is-info}

- [SynoCommunity 还创建、支持和维护所需的 Mono Package](https://synocommunity.com/package/mono)

## Synology Mono SSL 错误

> 由于 SynoCommunity 维护不善的 Mono package 引入的错误，更新 Mono 或进行全新安装后，Sonarr 将无法连接。您可以按照 [SynoCommunity Bug Report #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625) 上的说明解决此问题。请注意，根据 [此评论](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799)，DSM7 用户需要额外的步骤。
{.is-danger}

1. 在 DSM 中，启用 *控制面板 => 终端和 SNMP* 中的 SSH 服务，并点击应用
1. 使用 [终端](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac)（MacOS）通过 `ssh -l [admin 用户名] [NAS 地址]` 连接到 NAS，或使用 [Putty](https://www.putty.org/)（Windows）连接到 NAS 的网络地址
1. 输入所需的管理员密码，然后按回车键
1. 输入下面适用于您的 DSM 版本的适当命令，并按回车键
1. 输入所需的管理员密码，然后按回车键。完成后，您应该看到 *导入过程已完成* 的行
1. 通过键入 `exit` 并按回车键断开 SSH 会话
1. 在 DSM 中，禁用 *控制面板 => 终端和 SNMP* 中的 SSH 服务，并点击应用
1. 完成后，Sonarr 中的错误应该会在几分钟内自行消失。

### Synology DSM6 Mono 修复命令

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Synology DSM7 Mono 修复命令

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```