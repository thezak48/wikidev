---
title: Sonarr Linux-installasjon
description: Linux-installasjonsveiledning for Sonarr
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [Se nettsiden for instruksjoner](https://sonarr.tv/#downloads-v3-linux)
- Instruksjonene bør settes sammen slik:
  - [Legg til Mono Repository](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [Legg til MediaInfo Repository](https://mediaarea.net/en/Repos)
  - [Installer Sonarr](https://sonarr.tv/#downloads-v3-linux)
- For Ubuntu 20.04 vil dette *sannsynligvis* se slik ut

```bash
# Legg til Mono Repo (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# Hent MediaInfo
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Legg til Sonarr Repo
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Oppdater Apt
sudo apt update
# Installer Sonarr
sudo apt install sonarr
```

## Mono SSL-problemer

- Et vanlig problem som brukere opplever etter installasjonen, er relatert til SSL-sertifikatvalideringsproblemer. Dette kan løses ved å synkronisere mono-sertifikatene

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```