---
title: Radarr Docker 설치
description: Radarr를 위한 Docker 설치 가이드
published: true
date: 2023-08-12T16:02:10.602Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:47.674Z
---

# Docker

Radarr 팀은 공식 Docker 이미지를 제공하지 않습니다. 그러나 일부 제3자가 자체 Docker 이미지를 만들고 유지 관리하고 있습니다.

이 지침은 어떤 Radarr Docker 이미지에도 적용될 수 있는 일반적인 지침을 제공합니다.

Synology 사용자는 [TRaSH의 Synology Docker 가이드](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)를 참조하십시오.

## Portainer

> **Docker 컨테이너 설정에는 Portainer를 사용하지 마십시오** {.is-danger}

- Portainer는 컨테이너를 관리하기 위한 멋진 GUI를 제공하지만, 그것이 유용한 모든 것입니다.
- Portainer는 Docker 컨테이너 로그/컨테이너 상태를 보기 위해서만 사용해야 합니다.
- Docker Compose를 사용하고 Portainer를 사용하지 않는 것이 강력히 권장됩니다.
- Portainer에는 다음과 같은 여러 문제가 있습니다:
  - 마운트의 소스와 대상의 잘못된 순서
  - 일관되지 않은 대소문자 구분
  - 컨테이너 간 통신을 위한 자동으로 생성되는 사용자 정의 네트워크가 없음
  - 다른 아키텍처에서 일관되지 않은 Compose 구현
  - 특정 태그를 설정하지 않으면 업데이트 시 모든 태그를 가져옴
  - 기능이 숨겨져 있고 ARM 플랫폼에서 일부 기능이 전혀 작동하지 않음

대신 Docker Compose를 설정하는 방법에 대해서는 [Docker 가이드](/docker-guide)와 [TRaSH의 Docker 튜토리얼](https://trash-guides.info/hardlinks/)을 참조하십시오.

## 흔한 실수 피하기

### 볼륨과 경로

Docker 볼륨에는 두 가지 일반적인 문제가 있습니다: Radarr 및 다운로드 클라이언트 컨테이너 간에 다른 경로 및 빠른 이동 및 하드 링크를 방지하는 경로입니다.

첫 번째 문제는 다운로드 클라이언트가 다운로드 경로를 `/torrents/My.Movie.2018/`로 보고하지만 Radarr 컨테이너에서는 `/downloads/My.Movie.2018/`에 있을 수 있다는 것입니다. 두 번째 문제는 성능 문제이며 토렌트 시딩에 문제를 일으킵니다. 이러한 문제는 잘 계획된 일관된 경로로 해결할 수 있습니다.

대부분의 Docker 이미지는 `/movies` 및 `/downloads`와 같은 경로를 제안합니다. 이로 인해 이동이 느려지고 하드 링크를 사용할 수 없습니다. 또한 다운로드 클라이언트 컨테이너에는 Radarr 컨테이너와 다른 경로(예: /torrents)를 사용하도록 권장하는 경우도 있습니다.

가장 좋은 해결책은 `/data`와 같은 단일한 공통 볼륨을 컨테이너 내부에 사용하는 것입니다. 영화는 `/data/Movies`에, 토렌트는 `/data/downloads/torrents`에, 유즈넷 다운로드는 `/data/downloads/usenet`에 위치시킬 수 있습니다.

이 권고사항을 따르지 않으면 Radarr 웹 UI(설정 › 다운로드 클라이언트)에서 원격 경로 매핑을 구성해야 할 수도 있습니다.

### 소유권과 권한

파일의 권한과 소유권은 Radarr 사용자의 가장 흔한 문제 중 하나입니다. Docker 내부 및 외부에서 모두 발생할 수 있습니다. 대부분의 이미지에는 기본 사용자, 그룹 및 umask를 재정의할 수 있는 환경 변수가 있습니다. 모든 관련 컨테이너에 대해 공통 그룹을 사용하여 각 컨테이너가 마운트된 볼륨에 대해 공유 그룹 권한을 사용하여 파일을 읽고 쓸 수 있도록 설정하는 것이 권장됩니다.
Radarr는 다운로드 폴더뿐만 아니라 최종 폴더에 대한 읽기 및 쓰기 권한이 필요합니다.

> 이러한 문제에 대한 자세한 설명은 [The Best Docker Setup and Docker Guide](/docker-guide) 위키 문서를 참조하십시오.
{.is-info}

## Radarr 설치

이 Docker 이미지를 설치하고 사용하려면 위의 내용을 기억하면서 해당 문서를 따라야 합니다. Docker 이미지와 컨테이너를 관리하는 다양한 방법이 있으므로 설치 및 유지 관리는 선택한 경로에 따라 달라질 것입니다.

- [hotio/radarr](https://hotio.dev/containers/radarr/)
- [lscr.io/linuxserver/radarr](https://docs.linuxserver.io/images/docker-radarr)
{.links-list}