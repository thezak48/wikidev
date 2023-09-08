---
title: Sonarr Linux 설치
description: Sonarr을 위한 Linux 설치 가이드
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Linux

- [지침은 웹사이트에서 확인하세요](https://sonarr.tv/#downloads-v3-linux)
- 아래는 설치 과정을 요약한 내용입니다:
  - [Mono 저장소 추가](https://www.mono-project.com/download/stable/#download-lin-ubuntu)
  - [MediaInfo 저장소 추가](https://mediaarea.net/en/Repos)
  - [Sonarr 설치](https://sonarr.tv/#downloads-v3-linux)
- Ubuntu 20.04에서는 아래와 같을 것입니다.

```bash
# Mono 저장소 추가 (20.04)
sudo apt install gnupg ca-certificates
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
# MediaInfo 가져오기
wget https://mediaarea.net/repo/deb/repo-mediaarea_1.0-19_all.deb && sudo dpkg -i repo-mediaarea_1.0-19_all.deb
# Sonarr 저장소 추가
sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/sonarr-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 2009837CBFFD68F45BC180471F4F90DE2A9B4BF8
echo "deb [signed-by=/usr/share/keyrings/sonarr-keyring.gpg] https://apt.sonarr.tv/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/sonarr.list

# Apt 업데이트
sudo apt update
# Sonarr 설치
sudo apt install sonarr
```

## Mono SSL 문제

- 설치 후 사용자가 자주 겪는 문제 중 하나는 SSL 인증서 유효성 검사 문제입니다. 이는 mono의 인증서를 동기화하여 해결할 수 있습니다.

```bash
sudo cert-sync /etc/ssl/certs/ca-certificates.crt
```