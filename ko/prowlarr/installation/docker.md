---
title: Prowlarr Docker 설치
description: Prowlarr을 위한 Docker 설치 가이드
published: true
date: 2023-08-12T16:03:43.190Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:13.937Z
---

# Docker

Prowlarr 팀은 공식 Docker 이미지를 제공하지 않습니다. 그러나 여러 제3자가 자체 이미지를 만들고 유지 관리하고 있습니다.

> Docker에 대한 자세한 설명과 권장 사항은 [The Best Docker Setup and Docker Guide](/docker-guide) 위키 문서를 참조하세요.
{.is-info}

Synology 사용자는 [TRaSH의 Synology Docker 가이드](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)를 참조할 수 있습니다.

## Portainer

> **Docker 컨테이너 설정에는 Portainer를 사용하지 마세요** {.is-danger}

- Portainer는 컨테이너를 관리하기 위한 멋진 GUI를 제공하지만, 그 외에는 유용하지 않습니다.
- Portainer는 Docker 컨테이너 로그 및 상태를 보기 위해서만 사용해야 합니다.
- Docker Compose를 사용하고 Portainer를 사용하지 않는 것이 강력히 권장됩니다.
- Portainer에는 다음과 같은 여러 문제가 있습니다:
  - 마운트의 소스와 대상의 순서가 잘못됨
  - 대소문자 구분이 일관되지 않음
  - 컨테이너 간 통신을 위한 사용자 정의 네트워크가 자동으로 생성되지 않음
  - 다른 아키텍처에서 일관된 Compose 구현이 없음
  - 특정 태그를 설정하지 않으면 업데이트 시 모든 태그를 가져옴
  - 기능이 숨겨져 있고 ARM 플랫폼에서 일부 기능이 전혀 작동하지 않음

대신 Docker Compose를 설정하는 방법에 대해서는 [Docker 가이드](/docker-guide)와 [TRaSH의 Docker 튜토리얼](https://trash-guides.info/hardlinks/)을 참조하세요.

## Prowlarr 설치

이러한 Docker 이미지를 설치하고 사용하려면, 위에서 언급한 사항을 염두에 두고 해당 문서를 따라야 합니다. Docker 이미지와 컨테이너를 관리하는 다양한 방법이 있으므로, 설치 및 유지 관리는 선택한 경로에 따라 달라질 것입니다.

- [hotio/prowlarr](https://hotio.dev/containers/prowlarr/)
- [lscr.io/linuxserver/prowlarr](https://docs.linuxserver.io/images/docker-prowlarr)
{.links-list}