---
title: Sonarr Linux 安装
description: Sonarr 的 Linux 安装指南
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [请参考官方网站的指南](https://sonarr.tv/#downloads-v3-linux)
- 整理后的安装步骤如下：
  - [添加 Mono 仓库](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [添加 MediaInfo 仓库](https://mediaarea.net/en/Repos)
  - [安装 Sonarr](https://sonarr.tv/#downloads-v3-linux)
- 对于 Ubuntu 20.04，安装步骤如下：

```bash
# 添加 Mono 仓库 (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# 获取 MediaInfo
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# 添加 Sonarr 仓库
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# 更新 Apt
sudo apt update
# 安装 Sonarr
sudo apt install sonarr
```

## Mono SSL 问题

- 安装后，用户常常遇到与 SSL 证书验证相关的问题。可以通过同步 Mono 的证书来解决。

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```