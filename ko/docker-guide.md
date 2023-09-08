---
title: Docker 가이드
description: Servarr Docker 가이드 - Docker 개념, 하드링크 개념 및 Linux 소유권 및 권한 개요
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# 목차

- [목차](#목차)
- [최상의 Docker 설정](#최상의-docker-설정)
- [Portainer](#portainer)
- [소개](#소개)
- [다중 사용자 및 공유 그룹](#다중-사용자-및-공유-그룹)
  - [권한](#권한)
  - [UMASK](#umask)
  - [PUID 및 PGID](#puid-및-pgid)
  - [예시](#예시)
- [단일 사용자 및 선택적 공유 그룹](#단일-사용자-및-선택적-공유-그룹)
- [/config의 소유권과 권한](#config의-소유권과-권한)
- [일관되고 잘 계획된 경로](#일관되고-잘-계획된-경로)
  - [예시](#예시)
    - [토렌트](#토렌트)
    - [Usenet](#usenet)
    - [미디어 서버](#미디어-서버)
    - [Sonarr, Radarr 및 Lidarr](#sonarr-radarr-및-lidarr)
  - [문제점](#문제점)
- [Docker를 사용하여 컨테이너 실행](#docker를-사용하여-컨테이너-실행)
  - [Docker Compose](#docker-compose)
    - [모든 이미지 및 컨테이너 업데이트](#모든-이미지-및-컨테이너-업데이트)
    - [개별 이미지 및 컨테이너 업데이트](#개별-이미지-및-컨테이너-업데이트)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [유용한 명령어](#유용한-명령어)
  - [실행 중인 컨테이너 목록](#실행-중인-컨테이너-목록)
  - [컨테이너 내부에서 쉘 실행](#컨테이너-내부에서-쉘-실행)
  - [Docker 정리](#docker-정리)
  - [docker run 명령어 가져오기](#docker-run-명령어-가져오기)
  - [docker-compose 가져오기](#docker-compose-가져오기)
  - [네트워킹 문제 해결](#네트워킹-문제-해결)
  - [사용자 및 그룹에 대한 재귀적인 chown](#사용자-및-그룹에-대한-재귀적인-chown)
  - [재귀적으로 775/664로 chmod 설정](#재귀적으로-775664로-chmod-설정)
  - [사용자의 UID/GID 찾기](#사용자의-uidgid-찾기)
  - [하드링크를 위한 파일 검사](#하드링크를-위한-파일-검사)
- [흥미로운 Docker 이미지](#흥미로운-docker-이미지)
  - [올인원 솔루션](#올인원-솔루션)
- [사용자 정의 Docker 네트워크 및 DNS](#사용자-정의-docker-네트워크-및-dns)
- [일반적인 문제점](#일반적인-문제점)
  - [올바른 *외부* 경로, 잘못된 *내부* 경로](#올바른-외부-경로-잘못된-내부-경로)
  - [루트로 Docker 컨테이너 실행 또는 사용자 변경](#루트로-docker-컨테이너-실행-또는-사용자-변경)
  - [umask 000으로 Docker 컨테이너 실행](#umask-000으로-docker-컨테이너-실행)
- [도움 받기](#도움-받기)
  - [채팅 지원 (Discord)](#채팅-지원-discord)
  - [포럼 지원 (Reddit)](#포럼-지원-reddit)

# 최상의 Docker 설정

**TL;DR**: 데몬 당 [고유한](https://www.lexico.com/en/definition/eponymous) 사용자 및 umask가 `002`인 공유 그룹. 모든 컨테이너 간에 일관된 폴더 구조를 유지하는 하나의 볼륨 사용(다운로드 폴더와 라이브러리 폴더가 동일한 파일 시스템에 있음)은 Sonarr, Radarr, Lidarr 및 Readarr에서 [하드링크](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-hardlinks)와 [즉시 이동(원자적 이동)](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-instant-moves-atomic-moves)를 가능하게 합니다. 그리고 무엇보다도, 대부분의 Docker 이미지 경로 문서를 무시하세요!

> 참고: 많은 사람들이 [TRaSH의 하드링크 튜토리얼](https://trash-guides.info/hardlinks/)이 이 가이드보다 이해하기 쉽고 도움이 된다고 생각합니다. 이 가이드는 개념적인 내용이며 TRaSH의 튜토리얼은 과정을 안내합니다.
{.is-info}

# Portainer

> **Docker 컨테이너 설정에는 Portainer를 사용하지 마세요** {.is-danger}

- Portainer는 컨테이너 관리를 위한 멋진 GUI를 제공하지만, 그것이 유용한 모든 기능입니다.
- Portainer는 Docker 컨테이너 로그/상태만 볼 수 있도록 사용하는 것이 좋습니다.
- Docker Compose를 사용하고 Portainer를 사용하지 않는 것이 강력히 권장됩니다.
- Portainer에는 다음과 같은 여러 문제점이 있습니다:
  - 마운트의 소스와 대상의 순서가 잘못됨
  - 대소문자 구분이 일관되지 않음
  - 컨테이너 간 통신을 위한 사용자 정의 네트워크가 자동으로 생성되지 않음
  - 다른 아키텍처에서 일관된 Compose 구현이 없음
  - 특정 태그를 설정하지 않으면 업데이트 시 모든 태그를 가져옴
  - 기능이 숨겨져 있고 일부는 ARM 플랫폼에서 전혀 작동하지 않음

Docker Compose 설정 방법에 대해서는 [Docker 가이드](/docker-guide)와 [TRaSH의 Docker 튜토리얼](https://trash-guides.info/hardlinks/)을 참조하세요.

# 소개

이 문서는 최상의 Docker 설정에 대한 구체적인 내용을 보여주지는 않지만, 여러분이 자체 설정을 최상의 상태로 만들기 위해 사용할 수 있는 개요를 설명합니다. 아이디어는 각 Docker 컨테이너를 고유한 사용자로 실행하고 공유 그룹 및 일관된 볼륨을 사용하여 모든 컨테이너가 동일한 경로 레이아웃을 볼 수 있도록 하는 것입니다. 이것은 말하기는 쉽지만 이해하고 설명하기는 그렇게 쉽지 않습니다.

> 많은 사람들이 [TRaSH의 하드링크 튜토리얼](https://trash-guides.info/hardlinks/)이 이 가이드보다 이해하기 쉽고 도움이 된다고 생각합니다. 이 가이드는 개념적인 내용이며 TRaSH의 튜토리얼은 과정을 안내합니다.
{.is-warning}

# 다중 사용자 및 공유 그룹

## 권한

이상적으로 각 소프트웨어는 고유한 사용자로 실행되며 폴더 권한이 `775` (`drwxrwxr-x`)이고 파일 권한이 `664` (`-rw-rw-r--`)인 공유 그룹의 일부입니다. 이는 umask가 `002`인 것입니다. 이에 대한 합리적인 대안은 단일 공유 사용자입니다. 이 경우 폴더 권한은 `755`이고 파일 권한은 `644`이며 umask는 `022`입니다. "다른"에서 읽기를 거부하여 권한을 더 제한할 수 있습니다. 이 경우 데몬 당 사용자의 경우 umask는 `007`이고 단일 공유 사용자의 경우 umask는 `077`가 됩니다. 더 자세한 설명은 Arch Linux 위키 문서인 [파일 권한 및 속성](https://wiki.archlinux.org/index.php/File_permissions_and_attributes) 및 [UMASK](https://wiki.archlinux.org/index.php/Umask)를 참조하세요.

## UMASK

많은 Docker 이미지는 환경 변수로 `-e UMASK=002`를 허용하며 일부 소프트웨어는 컨테이너 내부에서 사용자, 그룹 및 umask(NZBGet) 또는 폴더/파일 권한(Sonarr/Radarr)을 구성할 수 있습니다. 이렇게 하면 *하나*에서 생성된 파일 및 폴더를 *다른*에서 읽고 쓸 수 있습니다. 기존 폴더와 파일을 사용하는 경우 현재 소유권과 권한을 수정해야 하지만, 앞으로는 각 소프트웨어를 올바르게 설정했기 때문에 올바르게 될 것입니다.

## PUID 및 PGID

많은 Docker 이미지는 `-e PUID=123` 및 `-e PGID=321`을 사용하여 컨테이너 내부에서 사용되는 UID/GID를 외부 계정의 UID/GID로 변경할 수 있습니다. 컨테이너 내부를 살펴보면 사용자 이름이 `abc`, `nobody` 또는 `hotio`와 같은 것을 찾을 수 있지만, 전달한 UID/GID를 사용하기 때문에 외부에서는 예상한 사용자처럼 보입니다. NFS 또는 CIFS를 통해 다른 시스템의 저장소를 사용하는 경우 해당 시스템에도 일치하는 사용자와 그룹이 있는 것이 좋습니다. 한 시스템에서 UID/GID를 선택한 다음 다른 시스템에서 그것을 재사용할 수 있습니다(충돌하지 않는 경우).

## 예시

[hotio/sonarr](https://github.com/hotio/docker-sonarr)를 사용하여 [Sonarr](https://github.com/Sonarr/Sonarr/releases)를 실행하고 uid가 `123`인 `sonarr` 사용자와 gid가 `321`인 `media` 공유 그룹(sonarr 사용자가 속한 그룹)을 생성했습니다. Docker 이미지를 `-e PUID=123 -e PGID=321 -e UMASK=002`로 실행하도록 구성했습니다. Sonarr는 사용자, 그룹 및 폴더 및 파일 권한도 구성할 수 있습니다. 이전 설정은 이러한 설정을 무효화하지만 원한다면 이러한 설정을 구성할 수 있습니다. `002`의 UMASK는 폴더에 대해 `775` (`drwxrwxr-x`)이고 파일에 대해 `664` (`-rw-rw-r--`)입니다. 사용자/그룹은 컨테이너 내부에서는 약간 복잡합니다. 일반적으로 `abc` 또는 `nobody`입니다.

# 단일 사용자 및 선택적 공유 그룹

다른 인기있는 방법은 단일 공유 사용자입니다. 아마도 *당신* 사용자일 수도 있습니다. 이 방법은 안전하지 않으며 최상의 방법을 따르지 않지만, 최종적으로 이해하기 쉽고 구현하기 쉽습니다. 이 경우 UMASK는 `022`이며 폴더에 대해 `755` (`drwxr-xr-x`)이고 파일에 대해 `644` (`-rw-r--r--`)입니다. 그룹은 더 이상 실제로 중요하지 않으므로 사용자 이름과 동일한 그룹을 사용할 것입니다. 그러나 다른 사용자와 공유하는 것이 어려워질 수 있으므로 이러한 설정을 사용하는 경우에도 여전히 UMASK가 `002`가 필요할 수 있습니다.

# /config의 소유권과 권한

/config 볼륨도 올바른 소유권과 권한을 가져야 합니다. 일반적으로 데몬의 사용자와 해당 사용자의 그룹(예: `sonarr:sonarr`) 및 umask(`022` 또는 `077`)로 설정합니다. 단일 사용자 설정의 경우 선택한 사용자 하나가 됩니다.

# 일관되고 잘 계획된 경로

> 많은 사람들이 [TRaSH의 하드링크 튜토리얼](https://trash-guides.info/hardlinks)이 이 가이드보다 이해하기 쉽고 도움이 된다고 생각합니다. 이 가이드는 개념적인 내용이며 TRaSH의 튜토리얼은 과정을 안내합니다.
{.is-info}

가장 쉽고 중요한 세부 사항은 모든 컨테이너에서 통일된 경로 정의를 만드는 것입니다.

하드링크가 작동하지 않거나 간단한 이동이 예상보다 훨씬 오래 걸리는 이유를 궁금해하는 경우, 이 섹션에서 설명합니다. *내부*에서 사용하는 경로가 중요합니다. Docker의 볼륨 작동 방식 때문에 `/tv`, `/movies` 및 `/downloads`와 같이 두 볼륨을 전달하면 하나의 파일 시스템 외부에서도 하나의 파일 시스템처럼 보이지만, 실제로는 두 개의 다른 파일 시스템으로 보입니다. 이는 하드링크가 작동하지 않고, 즉시/원자적인 이동 대신 더 느리고 더 많은 IO를 사용하는 복사+삭제가 사용됩니다. 토렌트와 유즈넷을 사용하기 때문에 여러 다운로드 클라이언트가 있는 경우 단일 `/downloads` 경로를 사용하면 혼합될 수 있습니다. 하나의 컨테이너에서 실행되는 Radarr은 해당 컨테이너의 NZBGet에 파일의 위치를 묻기 때문에 두 컨테이너에서 동일한 경로를 사용하면 모두 정상적으로 작동합니다. 그렇지 않은 경우 원격 경로 매핑으로 수정해야 합니다.

하나의 경로 레이아웃을 선택하고 모든 컨테이너에서 해당 경로를 사용하세요. `/data`를 사용하는 것이 좋습니다. 그러나 `/shared`, `/media` 또는 `/dvr`와 같은 일반적인 이름도 있습니다. 이렇게 하면 외부와 내부에서 동일한 경로를 유지하거나 Docker와 네이티브 소프트웨어를 통합하는 경우에도 설정을 간단하게 유지할 수 있습니다. 예를 들어, Synology는 외부에서 `/Volume1/data`를 사용하고 unRAID는 외부에서 `/mnt/user/data`를 사용할 수 있지만, 내부에서는 `/data`를 사용합니다.

또한 컨테이너 내에서 실행되는 소프트웨어의 경로를 설정하거나 다시 구성해야 함을 기억해야 합니다. 다운로드 클라이언트의 경로를 변경하면 해당 설정을 편집하고 기존 토렌트를 업데이트해야 합니다. 라이브러리 경로를 변경하면 Sonarr, Radarr, Lidarr, Plex 등에서 해당 설정을 변경해야 합니다.

## 예시

여기서 중요한 것은 이름이 아니라 일반적인 구조입니다. 의미 있는 폴더 이름을 선택할 수 있습니다. 또한 다른 배열 방법도 있습니다. 예를 들어, 유즈넷과 토렌트 사이에서 동일한 릴리스 간 충돌이 발생할 가능성이 거의 없으므로 `/data/downloads/{movies|books|music|tv}` 폴더에 모두 넣을 수 있습니다. 다운로드를 하위 폴더로 정렬할 필요도 없습니다. 영화, 음악 및 TV는 충돌이 거의 없을 것입니다.

이 예제 `data` 폴더에는 토렌트 및 유즈넷을 위한 하위 폴더가 있으며, 각각에는 TV, 영화 및 음악 다운로드를 위한 하위 폴더가 있습니다. `media` 폴더에는 잘 정리된 `tv`, `movies`, `books` 및 `music` 하위 폴더가 있습니다. 이 `media` 폴더는 라이브러리이며 Plex, Kodi, Emby, Jellyfin 등에 전달할 수 있습니다.

아래 예제에서 `data`는 호스트 경로 `/host/data`와 Docker 경로 `/data`와 동일합니다.

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    |  ├── books
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  ├── books
    │  └── tv
    └── media
        ├── movies
        ├── music
        ├── books
        └── tv
```

각 Docker 컨테이너의 경로는 필요에 따라 구체적일 수 있지만 올바른 구조를 유지합니다:

### 토렌트

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

토렌트는 토렌트 파일에만 액세스해야 하므로 `-v /host/data/torrents:/data/torrents`를 전달합니다. 토렌트 소프트웨어 설정에서 경로를 다시 구성해야 하며 `/data/torrents/{tv|books|movies|music}`와 같이 하위 폴더로 정렬할 수 있습니다.

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

유즈넷은 유즈넷 파일에만 액세스해야 하므로 `-v /host/data/usenet:/data/usenet`를 전달합니다. 유즈넷 소프트웨어 설정에서 경로를 다시 구성해야 하며 `/data/usenet/{tv|movies|music}`와 같이 하위 폴더로 정렬할 수 있습니다.

### 미디어 서버

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby는 미디어 라이브러리에만 액세스해야 하므로 `-v /host/data/media:/data/media`를 전달합니다. `movies`, `kids movies`, `tv`, `documentary tv` 및/또는 `music`과 같은 하위 폴더를 가질 수 있습니다.

### Sonarr, Radarr 및 Lidarr

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  └── tv
    └── media
        ├── movies
        ├── music
        └── tv
```

Sonarr, Radarr 및 Lidarr는 `-v /host/data:/data`를 사용하여 *다운로드* 폴더와 *미디어* 폴더가 하나의 파일 시스템처럼 보이고 *됨*을 의미합니다. 하드링크가 작동하고 이동이 원자적으로 이루어집니다. 복사 + 삭제 대신.

Docker 이미지의 제안된 경로를 따르지 않는 경우 몇 가지 작은 문제가 있습니다.

가장 큰 문제는 `dockerfile`에서 정의된 볼륨이 지정되지 않으면 생성된다는 것입니다. 이는 컨테이너를 삭제하고 다시 생성할 때 볼륨이 쌓이게 됨을 의미합니다. 이러한 볼륨에 데이터가 포함되어 있으면 예상치 못한 공간을 소비하고 적절하지 않은 위치에 저장될 수 있습니다. [유용한 명령](#prune-docker) 섹션에서 정리 명령을 찾을 수 있습니다. 이는 `/data/empty:/movies` 및 `/data/empty:/downloads`와 같이 사용하지 않을 모든 볼륨에 빈 폴더를 전달하여 완화할 수도 있습니다. 아마도 내부에 `DO NOT USE THIS FOLDER`라는 이름의 파일을 넣어서 자신에게 상기시킬 수도 있습니다.

다른 문제는 일부 이미지가 문서화된 볼륨을 사용하도록 미리 구성되어 있으므로 Docker 컨테이너 내부의 소프트웨어 설정을 변경해야 한다는 것입니다. 다행히 구성은 컨테이너 외부에서 유지되므로 이는 일회성 문제입니다. `/data` 또는 `/media`와 같은 경로를 선택할 수도 있으며, 일부 이미지에서 이미 특정 용도로 정의되어 있을 수 있습니다. 이는 문제가 되지 않을 것이지만 이전 문제와 결합되면 약간 더 혼란스러울 수 있습니다. 결국, 작동하는 하드 링크와 빠른 이동을 위해서는 이러한 문제를 감수해야 합니다. 일관성과 간단함은 환영받는 부수적인 효과입니다.

최신 버전의 [RadarrSync](https://github.com/Sperryfreak01/RadarrSync)를 사용하여 두 개의 Radarr 인스턴스를 동기화하는 경우, 내부에서 *동일한* 경로를 외부의 다른 경로로 매핑해야 합니다. 예를 들어, 한 인스턴스의 `/movies`는 `/data/media/movies`를 가리키고 다른 인스턴스는 `/data/media/movies4k`를 가리킵니다. 이는 위에서 읽은 모든 것을 *손상*시킵니다. 좋은 해결책은 없습니다. 좋지 않은 버전을 사용하거나, 매핑을 더러운 방식으로 수행하고 하드 링크를 깨뜨리거나 아예 사용하지 않는 것입니다.

# Docker Compose를 사용하여 컨테이너 실행하기

## Docker Compose

대부분의 사용자에게 가장 좋은 옵션입니다. 하나의 파일에서 여러 컨테이너와 그들의 상호 의존성을 제어하고 구성할 수 있습니다. Docker의 공식 [Docker Compose 시작하기](https://docs.docker.com/compose/gettingstarted/)를 참조하는 것이 좋은 시작점입니다. `docker run` 명령을 단일 `docker-compose.yml` 파일로 변환하기 위해 [composerize](https://composerize.com) 또는 [ghcr.io/red5d/docker-autocompose](#get-docker-compose)를 사용할 수 있습니다.

> 아래는 *완전한 작동 예제가 아닙니다!* 컨테이너에는 PID, UID, UMASK 및 예제 경로만 정의되어 있어 간단하게 유지되었습니다.
{.is-warning}

```yml
    # sonarr
    Sonarr:
        image: cr.hotio.dev/hotio/sonarr
        volumes:
            - /path/to/config/sonarr:/config
            - /host/data:/data
        environment:
            - PUID=111
            - PGID=321
            - UMASK=002

    # deluge
    Deluge:
        image: binhex/arch-delugevpn
        volumes:
            - /path/to/config/deluge:/config
            - /host/data/torrents:/data/torrents
        environment:
            - PUID=222
            - PGID=321
            - UMASK=002

    # SABnzbd
    SABnzbd:
        image: cr.hotio.dev/hotio/sabnzbd
        volumes:
            - /path/to/config/sabnzbd:/config
            - /host/data/usenet:/data/usenet
        environment:
            - PUID=333
            - PGID=321
            - UMASK=002

    # plex
    Plex:
        image: cr.hotio.dev/hotio/plex
        volumes:
            - /path/to/config/plex:/config
            - /host/data/media:/data/media

        environment:
            - PUID=444
            - PGID=321
            - UMASK=002
```

### 모든 이미지 및 컨테이너 업데이트

```shell
    docker-compose pull
    docker-compose up -d
```

### 개별 이미지 및 컨테이너 업데이트

```shell
    docker-compose pull NAME
    docker-compose up -d NAME
```

## docker run

> 위의 Docker Compose 예제와 마찬가지로, 다음 `docker run` 명령은 명확한 예제로 작성되었습니다. PUID, PGID, UMASK 및 볼륨만 포함되어 있습니다.
{.is-warning}

```shell
    # sonarr
    docker run -v /path/to/config/sonarr:/config \
               -v /host/data:/data \
               -e PUID=111 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sonarr

    # deluge
    docker run -v /path/to/config/deluge:/config \
               -v /host/data/torrents:/data/torrents \
               -e PUID=222 -e PGID=321 -e UMASK=002 \
               binhex/arch-delugevpn

    # SABnzbd
    docker run -v /path/to/config/sabnzbd:/config \
               -v /host/data/usenet:/data/usenet \
               -e PUID=333 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sabnzbd

    # plex
    docker run -v /path/to/config/plex:/config \
               -v /host/data/media:/data/media \
               -e PUID=444 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/plex
```

## Systemd

일부 Docker 컨테이너를 유지 관리하기 위해 systemd만 사용하는 것도 옵션입니다. 이는 네이티브 및 Docker 서비스 모두에 대해 제어를 표준화하고 종속성을 간단하게 만듭니다. 아래의 일반적인 예제는 다양한 값과 옵션을 조정하거나 추가함으로써 어떤 컨테이너에든지 적용할 수 있습니다.

```shell
    # /etc/systemd/system/thing.service
    [Unit]
    Description=Thing
    Requires=docker.service
    After=network.target docker.service

    [Service]
    ExecStart=/usr/bin/docker run --rm \
                              --name=thing \
                              -v /path/to/config/thing:/config \
                              -v /host/data:/data
                              -e PUID=111 -e PGID=321 -e UMASK=002 \
                              nobody/thing

    ExecStop=/usr/bin/docker stop -t 30 thing

    [Install]
    WantedBy=default.target
```

# 유용한 명령어

## 실행 중인 컨테이너 목록

```shell
    docker ps
```

## 컨테이너 내부의 쉘 실행

컨테이너에 대한 exec은 일반적으로 root로 로그인합니다.

```shell
    docker exec -it CONTAINER_NAME /bin/bash
```

내부에서는 다음과 같이 사용자를 전환할 수 있습니다.

```shell
    su - <username>
```

특정 사용자로 exec하려면 `-u`를 인수로 추가하고 사용자 이름 또는 ID를 전달하십시오.

```shell
    docker exec -u USER -it CONTAINER_NAME /bin/bash
```

### 특정 사용자로 예제 실행

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

자세한 내용은 [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) 문서를 참조하십시오.

## Docker 정리

```shell
    docker system prune --all --volumes
```

> 사용되지 않는 컨테이너, 네트워크, 볼륨, 이미지 및 빌드 캐시를 제거합니다. 이 명령이 제공하는 경고와 같이, 이 명령은 실행 중인 컨테이너에서 사용되지 않는 모든 항목을 제거합니다. 올바르게 구성된 환경에서는 괜찮지만, 처음 사용할 때는 주의하고 조심스럽게 진행하십시오. 자세한 내용은 [Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/) 문서를 참조하십시오.
{.is-warning}

## docker run 명령 가져오기

GUI 관리자에서 `docker run` 명령을 가져오는 것은 어려울 수 있습니다. 이 Docker 이미지를 사용하면 실행 중인 컨테이너에서 쉽게 가져올 수 있습니다 ([출처](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)).

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike CONTAINER_NAME
```

## docker-compose 가져오기

> 또한 [TRaSH의 docker-compose 가이드](https://trash-guides.info/compose/)를 확인할 수 있습니다.
{.is-info}

실행 중인 인스턴스에서 `docker-compose.yml`을 가져올 수 있습니다. 이미 `docker run` 또는 `docker create`로 컨테이너를 시작했고 `docker-compose` 스타일로 변경하려는 경우 [docker-autocompose](https://github.com/Red5d/docker-autocompose)를 사용할 수 있습니다. 또한 관리 소프트웨어에 관계없이 설정을 공유하는 데도 좋습니다. 마지막 인수(들)은 컨테이너 이름이며 필요한 만큼 동시에 전달할 수 있습니다. 첫 번째 컨테이너 이름은 필수이며, 나머지는 선택적입니다. 컨테이너 이름은 `docker ps`의 **NAMES** 열에 표시되며, 일반적으로 사용자가 설정하거나 이미지에 기반하여 생성됩니다(예: `binhex-qbittorrent`와 같이). 이미지 이름(`binhex/arch-qbittorrentvpn`와 같은)이 아닙니다.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $CONTAINER_NAME $ANOTHER_CONTAINER_NAME ... $ONE_MORE_CONTAINER_NAME
```

일부 사용자에게는 다음과 같을 수 있습니다.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## 네트워킹 문제 해결

대부분의 Docker 이미지에는 문제 해결에 유용한 도구가 많이 포함되어 있지 않지만, 기존 컨테이너에 [네트워크 문제 해결 유형 이미지](https://hub.docker.com/r/nicolaka/netshoot)를 연결하여 도움을 받을 수 있습니다.

```shell
    docker run -it --rm --network container:CONTAINER_NAME nicolaka/netshoot
```

## 사용자 및 그룹에 대한 재귀적인 chown

```shell
    chown -R user:group /some/path/here
```

## 775/664로 재귀적으로 chmod

```shell
    chmod -R a=,a+rX,u+w,g+w /some/path/here
              ^  ^    ^   ^ 그룹에 쓰기 추가
              |  |    | 사용자에 쓰기 추가
              |  | 모든 사람에게 읽기 및 모든 폴더에 대한 실행 추가(액세스 제어)
              | 모두를 `000`으로 설정
```

## 사용자의 UID/GID 찾기

```shell
    id <username>
```

## 하드 링크를 위한 파일 검사

```shell
    ls -alhi
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # hardlinked
    42207936 -rw-r--r--  1 user group    0 Sep 11 11:55 # no hardlinks
    42207934 -rw-r--r--  2 user group    0 Sep 11 11:55 # original

    stat original
      File: original
      Size: 0               Blocks: 0          IO Block: 4096   regular empty file
    Device: 803h/2051d      Inode: 42207934    Links: 2
    Access: (0644/-rw-r--r--)  Uid: ( 1000/ user)   Gid: ( 1001/ group)
    Access: 2020-09-11 11:55:43.803327144 -0500
    Modify: 2020-09-11 11:55:43.803327144 -0500
    Change: 2020-09-11 11:55:49.706660476 -0500
     Birth: 2020-09-11 11:55:43.803327144 -0500
```

# 흥미로운 Docker 이미지

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio’s](https://hotio.dev/) 문서와 Dockerfile은 나쁜 경로 제안을 하지 않습니다. 이미지는 upstream 변경 사항이 발견되면 1시간에 2번 자동으로 업데이트됩니다. Hotio는 우리의 Pull Requests(단 Sonarr은 제외)도 빌드하므로 테스트에 유용할 수 있습니다.
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) - 유즈넷 및 토렌트 트래커 검색용
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) - 미디어 요청용
  - [overseerr](https://hotio.dev/containers/overseerr/) - 미디어 요청용
  - [jackett](https://hotio.dev/containers/jackett) - 토렌트 트래커 검색용
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) - 유즈넷 인덱서 검색용
  - [bazarr](https://hotio.dev/containers/bazarr) - 자막용
  - [pullio](https://hotio.dev/pullio/) - 컨테이너 자동 업데이트용
  - [unpackerr](https://hotio.dev/containers/unpackerr) - 토렌트 클라이언트 간에 압축 해제를 위한 유용한 도구
{.links-list}
- [linuxserver.io](https://hub.docker.com/u/linuxserver) 이미지는 *많은* 소프트웨어에 대한 이미지를 가지고 있으며 잘 관리됩니다. 그러나 '제안된 (선택 사항)' 경로는 피하세요.
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) 또 다른 인기있는 유지 관리자
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### All-in-One 솔루션

- [이것은 GitHub 저장소](https://github.com/Luctia/ezarr)로 Docker를 사용하여 Servarr 스택을 사용하려는 초보자를 위한 것입니다. 이것은 기본적으로 준비된 파일의 모음이며, 전체를 온라인으로 가져오기 위해 두 가지만 실행하면 됩니다. 이것은 호스트 장치에서 사용자 관리 및 권한에 대한 번거로움을 제거하고 PleX와 같은 다른 애플리케이션도 제공합니다.

# 사용자 정의 Docker 네트워크 및 DNS

[사용자 정의 Docker 네트워크](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks)의 흥미로운 기능 중 하나는 해당 네트워크에 고유한 DNS 서버가 있다는 것입니다. 컨테이너를 위해 브리지 네트워크를 생성하면 구성에서 해당 컨테이너의 호스트 이름을 사용할 수 있습니다. 예를 들어, `docker run --network=isolated --hostname=deluge binhex/arch-deluge`와 `docker run --network=isolated --hostname=radarr binhex/arch-radarr`를 실행하면 Radarr의 다운로드 클라이언트를 `deluge`로 설정하고 독립된 개인 네트워크에서 작동합니다. 이는 더욱 안전하게 하려면 해당 포트 전달도 *중지*할 수 있다는 것을 의미합니다. 리버스 프록시 컨테이너를 동일한 네트워크에 배치하면 웹 인터페이스 포트 전달도 중지하고 더욱 안전하게 만들 수 있습니다.

# 일반적인 문제점

## 올바른 *외부* 경로, 잘못된 *내부* 경로

많은 사람들이 이것을 읽고 이해했다고 생각하지만, 그들은 외부 경로를 `/data/usenet`와 같이 올바르게 보지만, 여전히 *내부* 경로를 `/downloads`로 설정하는 등 핵심을 놓치게 됩니다.

- 좋음:
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- 나쁨:
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Docker 컨테이너를 root로 실행하거나 사용자 변경

컨테이너를 `root:root`로 실행하고 있다면, 무언가 잘못하고 있습니다. UID와 GID를 전달하지 않는다면, 이미지의 기본값을 사용하게 되고, 이는 시스템의 합리적인 사용자와 일치하지 않을 가능성이 높습니다. 또한 Docker 컨테이너가 실행되는 사용자와 그룹을 변경하면, 첫 번째 사용 시에 사용한 UID/GID로 생성된 `/config` 폴더와 같은 폴더에서 권한 문제가 발생할 수 있습니다.

## umask 000으로 Docker 컨테이너 실행

UMASK를 `000`으로 설정하고 있다면(폴더에 대해 777, 파일에 대해 666), 또한 잘못하고 있습니다. 이는 파일과 폴더를 *모두* 모든 사용자에게 읽기/쓰기 권한을 부여하므로, 이는 좋지 않은 Linux 관리 방식입니다.

# 도움 받기

## 채팅 지원 (Discord)

- [Sonarr Discord](https://discord.sonarr.tv/)
- [Radarr Discord](https://radarr.video/discord)
{.links-list}

## 포럼 지원 (Reddit)

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}