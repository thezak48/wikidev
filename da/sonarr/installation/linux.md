---
title: Sonarr Linux Installation
description: Linux installationsguide til Sonarr
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [Se venligst websitet for instruktioner](https://sonarr.tv/#downloads-v3-linux)
- Samlet set skal instruktionerne være:
  - [Tilføj Mono Repository](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [Tilføj MediaInfo Repository](https://mediaarea.net/en/Repos)
  - [Installer Sonarr](https://sonarr.tv/#downloads-v3-linux)
- For Ubuntu 20.04 vil det *sandsynligvis* se sådan ud

```bash
# Tilføj Mono Repo (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# Hent MediaInfo
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Tilføj Sonarr Repo
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Apt Update
sudo apt update
# Installer Sonarr
sudo apt install sonarr
```

## Mono SSL-problemer

- Et almindeligt problem, som brugere oplever efter installation, er relateret til SSL-certifikatvalideringsproblemer. Dette kan løses ved at synkronisere mono's certifikater

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```