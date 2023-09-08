---
title: Sonarr Linux Installation
description: Linux installationsguide för Sonarr
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [Se webbplatsen för instruktioner](https://sonarr.tv/#downloads-v3-linux)
- Sammanställ instruktionerna:
  - [Lägg till Mono Repository](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [Lägg till MediaInfo Repository](https://mediaarea.net/en/Repos)
  - [Installera Sonarr](https://sonarr.tv/#downloads-v3-linux)
- För Ubuntu 20.04 kommer det *förmodligen* se ut så här

```bash
# Lägg till Mono Repo (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# Hämta MediaInfo
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Lägg till Sonarr Repo
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Uppdatera Apt
sudo apt update
# Installera Sonarr
sudo apt install sonarr
```

## Mono SSL-problem

- Ett vanligt problem som användare upplever efter installationen är relaterat till SSL-certifikatvalideringsproblem. Detta kan åtgärdas genom att synkronisera monos certifikat

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```