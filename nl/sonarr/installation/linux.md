---
title: Sonarr Linux-installatie
description: Installatiehandleiding voor Sonarr op Linux
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [Raadpleeg de website voor instructies](https://sonarr.tv/#downloads-v3-linux)
- De instructies moeten als volgt worden uitgevoerd:
  - [Voeg het Mono Repository toe](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [Voeg het MediaInfo Repository toe](https://mediaarea.net/en/Repos)
  - [Installeer Sonarr](https://sonarr.tv/#downloads-v3-linux)
- Voor Ubuntu 20.04 ziet dit er *waarschijnlijk* als volgt uit:

```bash
# Voeg Mono Repo toe (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# Haal MediaInfo op
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Voeg de Sonarr Repo toe
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Apt Update
sudo apt update
# Installeer Sonarr
sudo apt install sonarr
```

## Problemen met Mono SSL

- Een veelvoorkomend probleem dat gebruikers ervaren na de installatie heeft te maken met SSL-certificaatvalidatieproblemen. Dit kan worden opgelost door de certificaten van Mono te synchroniseren.

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```