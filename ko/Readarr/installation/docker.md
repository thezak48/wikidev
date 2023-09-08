---
title: Readarr Docker 설치
description: Readarr를 위한 Docker 설치 가이드
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

Readarr 팀은 공식 Docker 이미지를 제공하지 않습니다. 그러나 여러 제3자가 자체 Docker 이미지를 만들고 유지 관리하고 있습니다.

이 지침은 어떤 Readarr Docker 이미지에도 적용될 수 있는 일반적인 지침을 제공합니다.

## Portainer

> **Docker 컨테이너 설정에는 Portainer를 사용하지 마십시오** {.is-danger}

- Portainer는 컨테이너를 관리하기 위한 멋진 GUI를 제공하지만, 그 외에는 유용하지 않습니다.
- Portainer는 Docker 컨테이너 로그 및 컨테이너 상태를 보기 위해서만 사용해야 합니다.
- Docker Compose를 사용하고 Portainer를 사용하지 않는 것이 강력히 권장됩니다.
- Portainer에는 다음과 같은 여러 문제가 있습니다:
  - 마운트의 소스와 대상의 순서가 잘못됨
  - 대소문자 구분이 일관되지 않음
  - 컨테이너 간 통신을 위한 자동으로 생성되는 사용자 정의 네트워크가 없음
  - 다른 아키텍처에서 일관되지 않은 Compose 구현
  - 특정 태그를 설정하지 않으면 업데이트 시 모든 태그를 가져옴
  - 기능이 숨겨져 있고 일부 기능은 ARM 플랫폼에서 전혀 작동하지 않음

대신 [Docker 가이드](/docker-guide)와 [TRaSH의 Docker 튜토리얼](https://trash-guides.info/hardlinks/)을 참조하여 Docker Compose를 설정하는 방법을 알아보세요.

## 흔한 함정 피하기

### 볼륨과 경로

Docker 볼륨에는 두 가지 일반적인 문제가 있습니다: Readarr 및 다운로드 클라이언트 컨테이너 간에 다른 경로 및 빠른 이동과 하드 링크를 방지하는 경로입니다.

첫 번째 문제는 다운로드 클라이언트가 다운로드 경로를 `/torrents/My.Movie.2018/`로 보고하지만 Readarr 컨테이너에서는 `/downloads/My.Movie.2018/`에 있을 수 있다는 것입니다. 두 번째 문제는 성능 문제이며 토렌트 시딩에 문제를 일으킵니다. 이러한 문제는 계획적이고 일관된 경로로 해결할 수 있습니다.

대부분의 Docker 이미지는 `/books` 및 `/downloads`와 같은 경로를 제안합니다. 이로 인해 이동이 느려지고 하드 링크를 사용할 수 없습니다. 컨테이너 내에서 두 개의 다른 파일 시스템으로 간주되기 때문입니다. 일부 이미지는 Readarr 컨테이너와 다른 다운로드 클라이언트 컨테이너를 위한 경로를 `/torrents`와 같이 다르게 설정하도록 권장합니다.

가장 좋은 해결책은 `/data`와 같은 단일한 공통 볼륨을 사용하는 것입니다. 책은 `/data/Books`에, 토렌트는 `/data/downloads/torrents`에, 유즈넷 다운로드는 `/data/downloads/usenet`에 위치시킬 수 있습니다.

이 조언을 따르지 않으면 Readarr 웹 UI (설정 › 다운로드 클라이언트)에서 원격 경로 매핑을 구성해야 할 수도 있습니다.

### Calibre 통합

루트 폴더를 생성할 때 Calibre 통합을 사용할지 여부를 선택할 수 있습니다. 이 선택은 폴더 생성 중에만 가능하며, Calibre 통합을 사용하지 않도록 선택하면 나중에 추가할 수 없습니다. Calibre를 사용하여 도서 라이브러리를 관리하는 경우 이 옵션을 선택해야 합니다. Calibre를 사용하는 경우 Calibre가 도서 파일의 이름과 구성을 자동으로 처리합니다.

Calibre를 실행하는 경우 Calibre 콘텐츠 서버를 먼저 시작해야 합니다 (환경 설정 / 인터넷 공유) 그리고 사용자와 비밀번호를 설정해야 합니다. 이를 위해서는 Calibre를 다시 시작해야 합니다.

> Calibre 콘텐츠 서버와 Calibre는 Calibre 웹이 아닙니다. Calibre 웹은 이러한 프로그램과 관련이 없는 별도의 도구이며, Readarr에서는 필요하지 않고 사용되지 않습니다.
{.is-warning}

### 소유권과 권한

파일의 권한과 소유권은 Readarr 사용자들에게 가장 흔한 문제 중 하나입니다. Docker 내부 및 외부에서 모두 문제가 발생할 수 있습니다. 대부분의 이미지에는 기본 사용자, 그룹 및 umask를 재정의할 수 있는 환경 변수가 있습니다. 모든 컨테이너를 설정하기 전에 이를 결정해야 합니다. 권장 사항은 모든 관련 컨테이너에 대해 공통 그룹을 사용하여 각 컨테이너가 마운트된 볼륨에 대해 공유 그룹 권한을 사용하여 파일을 읽고 쓸 수 있도록 하는 것입니다.
Readarr는 다운로드 폴더뿐만 아니라 최종 폴더에 대한 읽기 및 쓰기 권한이 필요합니다.

> 이러한 문제에 대한 자세한 설명은 [The Best Docker Setup and Docker Guide](/docker-guide) 위키 문서를 참조하세요.
{.is-info}

## Readarr 설치

이 Docker 이미지를 설치하고 사용하려면 위의 내용을 기억하면서 해당 문서를 따라야 합니다. Docker 이미지와 컨테이너를 관리하는 여러 가지 방법이 있으므로 설치 및 유지 관리는 선택한 경로에 따라 다를 수 있습니다.

> 현재는 master 브랜치가 없으므로 docker 이미지에는 :nightly 또는 :develop 태그를 사용해야 합니다. [브랜치의 의미에 대한 FAQ 항목을 참조하세요](/readarr/faq#how-do-i-update-readarr)
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}