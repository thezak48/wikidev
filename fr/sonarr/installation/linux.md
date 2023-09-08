---
title: Installation de Sonarr sur Linux
description: Guide d'installation de Sonarr sur Linux
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [Veuillez consulter le site Web pour obtenir les instructions](https://sonarr.tv/#downloads-v3-linux)
- Les instructions complètes sont les suivantes :
  - [Ajouter le référentiel Mono](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [Ajouter le référentiel MediaInfo](https://mediaarea.net/en/Repos)
  - [Installer Sonarr](https://sonarr.tv/#downloads-v3-linux)
- Pour Ubuntu 20.04, cela ressemblera *probablement* à ceci :

```bash
# Ajouter le référentiel Mono (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# Obtenir MediaInfo
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Ajouter le référentiel Sonarr
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Mise à jour d'Apt
sudo apt update
# Installer Sonarr
sudo apt install sonarr
```

## Problèmes de SSL avec Mono

- Un problème courant rencontré par les utilisateurs après l'installation est lié aux problèmes de validation du certificat SSL. Cela peut être résolu en synchronisant les certificats de Mono.

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```