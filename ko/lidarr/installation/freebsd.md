---
title: Lidarr FreeBSD 설치
description: Lidarr을 위한 FreeBSD 설치 안내서
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

Lidarr 팀은 FreeBSD를 위한 빌드만 제공합니다. 플러그인과 포트는 FreeBSD 커뮤니티에서 유지 및 생성됩니다.

FreeBSD 설치에 대한 지침은 FreeBSD 커뮤니티에서도 유지되며 GitHub 계정을 가진 누구나 필요에 따라 위키를 업데이트할 수 있습니다.

[Freshports Lidarr 링크](https://www.freshports.org/net-p2p/lidarr/)

## TrueNAS GUI를 사용한 Jail 설정

1. 메인 화면에서 Jails를 선택합니다.

1. ADD를 클릭합니다.

1. Advanced Jail Creation을 클릭합니다.

1. 이름 (아무 이름이나 사용 가능): Lidarr

1. Jail 유형: Default (Clone Jail)

1. 릴리스: 12.2-Release (또는 그 이상)

1. 원하는대로 기본 속성을 구성합니다.

1. 원하는대로 Jail 속성을 구성하지만 다음을 추가합니다.

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets`는 문제 해결에 도움이 됩니다 (예: ping, traceroute) 하지만 필수 요구 사항은 아닙니다. {.is-info}

1. 원하는대로 네트워크 속성을 구성합니다.

1. 원하는대로 사용자 정의 속성을 구성합니다.

1. 저장을 클릭합니다.

1. Jail이 생성되면 자동으로 시작됩니다. Lidarr이 마운트된 미디어 위치의 저장 공간을 볼 수 있도록 하려면 추가로 하나의 속성을 설정해야 합니다. 서버에서 루트 쉘을 열고 다음 명령을 입력합니다:

```shell
iocage stop <jailname>
iocage set enforce_statfs=1 <jailname>
iocage start <jailname>
```

## Lidarr 설치

Jails 목록에서 `lidarr`을 위해 새로 생성한 Jail을 찾고 "Shell"을 클릭합니다.

Lidarr을 설치하려면

> \* pkg 저장소가 `/latest`에서 패키지를 가져오도록 구성되어 있는지 확인하세요.
> \* `/usr/local/etc/pkg/repos/FreeBSD.conf`를 확인하세요.
> \* 해당 위치에 없는 경우 `/etc/pkg/FreeBSD.conf`를 해당 위치로 복사하고 열어서 `quarterly`를 `latest`로 바꿉니다.
{.is-warning}

```shell
pkg install lidarr
```

아직 쉘을 닫지 마세요. 아직 몇 가지 할 일이 남아 있습니다!

## Lidarr 구성

이제 설치를 완료했으므로 몇 가지 추가 단계가 필요합니다.

### 서비스 설정

서비스를 활성화할 시간입니다. 하지만 먼저 알아두어야 할 사항이 있습니다.

업데이터는 기본적으로 비활성화되어 있습니다. `pkg-message`에서 업데이터를 활성화하는 방법에 대한 지침이 제공되지만 주의하세요: 내장 업데이터가 파일을 교체할 때 `pkg check -s` 및 `pkg remove`와 같은 작업이 손상될 수 있습니다.

서비스를 활성화하려면:

```shell
sysrc lidarr_enable=TRUE
```

사용자/그룹 `lidarr`을 사용하지 않으려면 서비스 파일에 어떤 사용자/그룹에서 실행되어야 하는지 알려야 합니다.

```shell
sysrc lidarr_user="USER_YOU_WANT"
```

```shell
sysrc lidarr_group="GROUP_YOU_WANT"
```

`lidarr`은 기본적으로 `/usr/local/lidarr`에 데이터, 구성, 로그 및 PID 파일을 저장합니다. 서비스 파일은 이를 생성하고 소유권을 가져갑니다. 그러나 해당 위치가 존재하지 않는 경우에만 해당됩니다. 이러한 파일을 다른 위치에 저장하려면 (예: 스냅샷을 더 쉽게 찍기 위해 Jail에 마운트된 데이터셋) `sysrc`를 사용하여 변경해야 합니다.

```shell
sysrc lidarr_data_dir="DIR_YOU_WANT"
```

알림: 기존 위치를 사용하는 경우 수동으로 소유권을 UID/GID `lidarr`이 사용하는 것으로 변경하거나 쓰기 액세스 권한이 있는 GID에 `lidarr`을 추가해야 합니다.

거의 끝났습니다. 서비스를 시작해 봅시다.

```shell
service lidarr start
```

모든 계획대로 진행되었다면 lidarr이 Jail의 IP (포트 8686)에서 실행 중일 것입니다!

이제 쉘을 안전하게 닫을 수 있습니다.

## 문제 해결

- 서비스가 실행 중인 것처럼 보이지만 UI가 로드되지 않거나 페이지가 시간 초과되는 경우
  - Jail에서 `allow_mlock`이 활성화되어 있는지 다시 확인하세요.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - Jail에 `VNET`이 켜져 있는지, ip6=inherit 또는 ip6=new인지 확인하세요.

> 서비스 스크립트는 이제 VNET 또는 IP6의 부재를 처리하므로 VNET 또는 ip6=inherit의 요구 사항이 제거되었습니다. {.is-info}