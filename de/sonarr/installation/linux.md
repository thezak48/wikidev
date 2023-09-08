---
title: Sonarr Linux Installation
description: Linux-Installationsanleitung für Sonarr
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [Bitte besuchen Sie die Website für Anweisungen](https://sonarr.tv/#downloads-v3-linux)
- Die Anweisungen sollten wie folgt zusammengestellt werden:
  - [Fügen Sie das Mono-Repository hinzu](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [Fügen Sie das MediaInfo-Repository hinzu](https://mediaarea.net/en/Repos)
  - [Installieren Sie Sonarr](https://sonarr.tv/#downloads-v3-linux)
- Für Ubuntu 20.04 sieht dies *wahrscheinlich* wie folgt aus:

```bash
# Mono-Repo hinzufügen (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# MediaInfo holen
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Sonarr-Repo hinzufügen
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Apt-Update
sudo apt update
# Sonarr installieren
sudo apt install sonarr
```

## Mono SSL-Probleme

- Ein häufiges Problem, das Benutzer nach der Installation erleben, hängt mit Problemen bei der SSL-Zertifikatsvalidierung von Mono zusammen. Dies kann durch Synchronisieren der Zertifikate von Mono behoben werden.

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```