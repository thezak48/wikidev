---
title: Sonarr Synology 설치
description: Sonarr을 위한 Synology 설치 안내서
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [SynoCommunity는 Synology NAS 패키지를 생성, 지원 및 유지 관리합니다](https://synocommunity.com/package/nzbdrone)

> NAS 패키지는 관리가 잘 되지 않으며 자주 업데이트되지 않습니다. NAS가 도커를 지원하는 경우 [도커를 실행하는 것이 강력히 권장됩니다](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/). NAS 패키지가 오래되어 자동으로 업데이트되지 않도록 구성되어 있으므로 Sonarr을 다시 설치하려면 데이터베이스를 수동으로 지워야 합니다. {.is-info}

- [SynoCommunity는 필요한 Mono 패키지도 생성, 지원 및 유지 관리합니다](https://synocommunity.com/package/mono)

## Synology Mono SSL 오류

> SynoCommunity의 관리가 잘 되지 않는 Mono 패키지 버그로 인해, Mono를 업데이트하거나 새로 설치한 후에 Sonarr이 연결에 실패할 수 있습니다. 이 문제는 [SynoCommunity 버그 보고서 #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625)의 지침을 따라 해결할 수 있습니다. [이 코멘트](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799)에 따르면 DSM7 사용자는 추가 단계가 필요합니다.
{.is-danger}

1. DSM에서 *제어판 => 터미널 및 SNMP*으로 이동하여 SSH 서비스를 활성화하고 적용을 클릭합니다.
1. [터미널](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac)을 사용하여 (MacOS) `ssh -l [관리자 사용자 이름] [NAS 주소]`를 입력하여 NAS에 연결하거나 [Putty](https://www.putty.org/) (Windows)를 사용하여 NAS의 네트워크 주소에 연결합니다.
1. 필요한 관리자 비밀번호를 입력하고 Enter 키를 누릅니다.
1. 아래에 표시된 DSM 버전에 해당하는 명령을 입력하고 Enter 키를 누릅니다.
1. 필요한 관리자 비밀번호를 입력하고 Enter 키를 누릅니다. 완료되면 *Import process completed*라는 줄이 표시됩니다.
1. `exit`를 입력하고 Enter 키를 눌러 SSH 세션을 종료합니다.
1. DSM에서 *제어판 => 터미널 및 SNMP*으로 이동하여 SSH 서비스를 비활성화하고 적용을 클릭합니다.
1. 완료되면 Sonarr의 오류가 몇 분 내에 자동으로 사라집니다.

### Synology DSM6 Mono 수정 명령

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Synology DSM7 Mono 수정 명령

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```