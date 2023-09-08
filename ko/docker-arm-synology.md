---
title: Synology ARM NAS에 Docker 설치하기
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# 소개

Synology는 `x64` 기반 NAS에만 Docker 패키지를 제공합니다. `aarch64` NAS에 Docker를 설치하는 방법은 완전히 지원되지 않으며 테스트되지 않았으며 완전히 사용자의 책임입니다. 이 방법은 NAS를 손상시킬 수 있습니다.

> 다시 말하지만, `aarch64` NAS에 Docker를 설치하는 이 방법은 **완전히 지원되지 않으며 테스트되지 않았으며** 완전히 사용자의 책임입니다. 이 방법은 NAS를 손상시킬 수 있습니다. {.is-danger}

# 요약

아래 지침은 다음을 수행합니다:

1. Docker 바이너리를 `/usr/local/bin/`에 배치합니다.
1. Docker 구성 파일 `/usr/local/etc/docker/docker.json`을 생성합니다.
1. Docker를 `/volume1/docker/var`에 데이터를 저장하도록 구성합니다.
1. 부팅 시 Docker를 시작하는 스크립트를 `/usr/local/etc/rc.d/docker.sh`에 생성합니다.
1. `docker` 그룹을 생성합니다.
1. `docker-compose` 스크립트를 `/usr/local/bin/`에 배치합니다.

# 설치

1. [Synology에 SSH로 로그인하고 `root`로 승격합니다](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet).

1. 다음 명령을 실행합니다:

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

모두 잘 진행되면 다음 메시지가 표시됩니다:

```none
Done. Please add your user to the Docker group in the Synology GUI and reboot your NAS.
```

다음을 수행하세요:

1. Synology GUI를 사용하여 새로운 `docker` 그룹에 사용자를 추가합니다.
1. **재부팅**합니다.

이제 일반 사용자로 로그인할 때 작동하는 `docker` 및 `docker-compose` 명령이 제대로 작동하는지 확인할 수 있습니다.

# 주의 사항

1. 대부분의 ARM Synology에서 seccomp를 지원하지 않는 것으로 보입니다. 따라서 Docker 컨테이너는 시스템에 제한 없이 액세스할 수 있습니다(일반 Docker보다 더 많은 권한).
1. 다시 한번 Synology의 제약으로 인해 모든 컨테이너는 `--network=host`(또는 compose에서 `network_mode: host`)를 사용해야 하며 모든 것이 호스트에서 직접 액세스할 수 있습니다. 포트 매핑은 지원되지 않습니다.
1. 당연히 aarch64 이미지만 실행할 수 있지만, 대부분의 hotio 및 linuxserver 이미지는 aarch64 버전을 제공합니다.

# Docker GUI 설정

GUI를 원한다면 다음 예제 compose를 사용하여 Portainer를 실행할 수 있습니다:

```yml
    version: '2'

    services:
      portainer:
        image: portainer/portainer
        restart: unless-stopped
        network_mode: host
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
          - portainer_data:/data

    volumes:
      portainer_data:
```

이를 `docker-compose.yml`이라는 파일에 빈 디렉토리에 저장하세요. 다음을 실행하세요:

```shell
docker-compose up -d
```

[`http://ip:9000`](http://ip:9000)을 방문하여 설정을 완료하세요(`ip`는 Synology의 IP 주소입니다).

# Sonarr/Radarr/Lidarr/Readarr 설정하기

Sonarr/Radarr/Lidarr/Readarr 설정에 대한 안내는 [Docker 가이드](/docker-guide)를 참조하세요. **위의 주의 사항 2를 기억하세요.**