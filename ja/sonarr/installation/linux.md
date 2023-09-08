---
title: Sonarr Linux インストール
description: Sonarr の Linux インストールガイド
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [手順についてはウェブサイトを参照してください](https://sonarr.tv/#downloads-v3-linux)
- インストール手順は以下の通りです:
  - [Mono リポジトリを追加](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [MediaInfo リポジトリを追加](https://mediaarea.net/en/Repos)
  - [Sonarr をインストール](https://sonarr.tv/#downloads-v3-linux)
- Ubuntu 20.04 の場合、おそらく以下のようになります

```bash
# Mono リポジトリを追加 (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# MediaInfo を取得
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Sonarr リポジトリを追加
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Apt アップデート
sudo apt update
# Sonarr をインストール
sudo apt install sonarr
```

## Mono SSL の問題

- インストール後にユーザーがよく遭遇する問題の一つは、SSL 証明書の検証に関連しています。これは mono の証明書を同期することで解決できます。

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```