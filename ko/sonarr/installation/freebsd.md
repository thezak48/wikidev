---
title: Sonarr FreeBSD 설치
description: Sonarr을 위한 FreeBSD 설치 가이드
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

Sonarr 팀은 FreeBSD를 위한 빌드만 제공합니다. 플러그인과 포트는 FreeBSD 커뮤니티에 의해 유지되고 생성됩니다.

FreeBSD 설치 지침은 FreeBSD 커뮤니티에 의해 유지되며 GitHub 계정을 가진 누구나 필요에 따라 위키를 업데이트할 수 있습니다.

[Freshports Sonarr 링크](https://www.freshports.org/net-p2p/sonarr/)

## TrueNAS GUI를 사용한 Jail 설정

1. 메인 화면에서 Jails를 선택합니다.

1. ADD를 클릭합니다.

1. Advanced Jail Creation을 클릭합니다.

1. 이름 (아무 이름이나 사용 가능): Sonarr

1. Jail 유형: Default (Clone Jail)

1. 릴리스: 12.2-Release (또는 그 이상)

1. Basic Properties를 원하는 대로 구성합니다.

1. Jail Properties를 원하는 대로 구성하지만 다음을 추가합니다.

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets`는 문제 해결에 도움이 됩니다 (예: ping, traceroute) 하지만 필수 요구 사항은 아닙니다. {.is-info}

1. Network Properties를 원하는 대로 구성합니다.

1. Custom Properties를 원하는 대로 구성합니다.

1. Save를 클릭합니다.

1. Jail이 생성되면 자동으로 시작됩니다. Sonarr이 마운트된 미디어 위치의 저장 공간을 볼 수 있도록 하려면 추가로 한 가지 속성을 설정해야 합니다. 서버에서 루트 쉘을 열고 다음 명령을 입력합니다:

```shell
iocage stop <jailname>
iocage set enforce_statfs=1 <jailname>
iocage start <jailname>
```

## CLI를 사용한 Jail 설정

iocage가 설치되어 있고 구성되어 있다고 가정합니다 (<https://iocage.readthedocs.io/en/latest/install.html>)
iocage 네트워크 브리지 (vnet)가 구성되어 있다고 가정합니다 (<https://iocage.readthedocs.io/en/latest/networking.html>)

"10.0.0.100"을 네트워크에서 사용 가능한 열린 IPV4 주소로 대체합니다.
"13.1-RELEASE"을 선호하는 FreeBSD 버전으로 대체합니다.
"sonarr"을 선호하는 jail 이름으로 대체합니다.
자동으로 IPV6를 구성하지 않으려면 "accept_rtadv"를 제거하거나 ip6_addr를 제거합니다.

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Sonarr Mono 설치

jails 목록에서 새로 생성한 `sonarr` jail을 찾고 "Shell"을 클릭합니다.

Sonarr을 설치하려면

> \* pkg 저장소가 `/latest`에서 패키지를 가져오도록 구성되어 있는지 확인합니다.
> \* `/usr/local/etc/pkg/repos/FreeBSD.conf`를 확인합니다.
> \* 해당 파일이 없는 경우 `/etc/pkg/FreeBSD.conf`를 해당 위치로 복사하고 열어서 `quarterly`를 `latest`로 바꿉니다.
{.is-warning}

```shell
pkg install sonarr
```

아직 쉘을 닫지 마세요. 아직 몇 가지 작업이 남아 있습니다!

## Sonarr .NET 설치

jails 목록에서 새로 생성한 `sonarr` jail을 찾고 "Shell"을 클릭합니다.

Sonarr을 설치하려면

> \* pkg 저장소가 `/latest`에서 패키지를 가져오도록 구성되어 있는지 확인합니다.
> \* `/usr/local/etc/pkg/repos/FreeBSD.conf`를 확인합니다.
> \* 해당 파일이 없는 경우 `/etc/pkg/FreeBSD.conf`를 해당 위치로 복사하고 열어서 `quarterly`를 `latest`로 바꿉니다.
{.is-warning}

Sonarr을 지원하기 위해 다음 라이브러리를 설치합니다.

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Sonarr 사용자와 그룹을 생성합니다 (사용자/그룹 'sonarr'을 사용하지 않으려면 기호에 따라 변경할 수 있습니다).

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

<https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64>에서 최신 버전을 다운로드하고 권한을 설정합니다.

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

선호하는 편집기에서 rc.subr 스크립트를 만들어 Sonarr을 데몬으로 실행하도록 설정합니다 (폴더가 이미 있는 경우 1번 라인을 건너뛸 수 있습니다) 아래의 sonarr rc.subr 내용을 사용합니다.

```shell
mkdir -p /usr/local/etc/rc.d
vi /usr/local/etc/rc.d/sonarr
chmod +x /usr/local/etc/rc.d/sonarr
```

```shell
#!/bin/sh

# PROVIDE: sonarr
# REQUIRE: LOGIN
# KEYWORD: shutdown
#
# Add the following lines to /etc/rc.conf.local or /etc/rc.conf
# to enable this service:
#
# sonarr_enable:   Set to yes to enable the sonarr service.
#                       Default: no
# sonarr_user:     The user account used to run the sonarr daemon.
#                       This is optional, however do not specifically set this to an
#                       empty string as this will cause the daemon to run as root.
#                       Default: sonarr
# sonarr_group:    The group account used to run the sonarr daemon.
#                       This is optional, however do not specifically set this to an
#                       empty string as this will cause the daemon to run with group wheel.
#                       Default: sonarr
# sonarr_data_dir: Directory where sonarr configuration data is stored.
#                       Default: /var/db/sonarr
# sonarr_pid:      Name of the pid file.
#                       Default: sonarr.pid
# sonarr_pid_dir:  Path of the pid file.
#                       Default: /var/run/sonarr

. /etc/rc.subr
name=sonarr
rcvar=${name}_enable
load_rc_config ${name}

: ${sonarr_enable:="no"}
: ${sonarr_user:="sonarr"}
: ${sonarr_group:="sonarr"}
: ${sonarr_data_dir:="/var/db/sonarr"}
: ${sonarr_pid:="sonarr.pid"}
: ${sonarr_pid_dir:="/var/run/sonarr"}

pidfile="${sonarr_pid_dir}/${sonarr_pid}"
command="/usr/sbin/daemon"
command_args="-r -f -P ${pidfile} /usr/local/share/Sonarr/Sonarr --debug --data=${sonarr_data_dir} --nobrowser"

start_precmd=sonarr_start_precmd
sonarr_start_precmd()
{
 [ -d ${sonarr_pid_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_pid_dir}
 [ -d ${sonarr_data_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_data_dir}

 # .NET 6+ uses dual mode sockets to avoid the separate AF handling.
 # disable .NET use of V6 if no ipv6 is configured.
 # See https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

아직 쉘을 닫지 마세요. 아직 몇 가지 작업이 남아 있습니다!

## Sonarr 구성

이제 설치가 완료되었으므로 몇 가지 추가 단계가 필요합니다.

### 서비스 설정

서비스를 활성화할 시간입니다. 그러나 이전에 주의할 점이 있습니다.

업데이터는 기본적으로 비활성화되어 있습니다. `pkg check -s` 및 `pkg remove`와 같은 작업을 Sonarr에 대해 내장된 업데이터가 파일을 교체하면 작동하지 않을 수 있음을 염두에 두세요.

서비스를 활성화하려면:

```shell
sysrc sonarr_enable=TRUE
```

사용자/그룹 `sonarr`을 사용하지 않으려면 서비스 파일에 어떤 사용자/그룹에서 실행되어야 하는지 알려야 합니다.

```shell
sysrc sonarr_user="사용자_이름"
```

```shell
sysrc sonarr_group="그룹_이름"
```

`sonarr`은 기본적으로 `/usr/local/sonarr`에 데이터, 구성, 로그 및 PID 파일을 저장합니다. 서비스 파일은 이를 생성하고 소유권을 가져갑니다. 그러나 해당 위치가 이미 존재하지 않는 경우에만 이를 수행합니다. 이러한 파일을 다른 위치에 저장하려면 (`jail`에 쉽게 스냅숏을 찍기 위해 마운트된 데이터셋 등) `sysrc`를 사용하여 변경해야 합니다.

```shell
sysrc sonarr_data_dir="원하는_디렉토리"
```

알림: 기존 위치를 사용하는 경우 수동으로 소유권을 UID/GID `sonarr`이 사용하는 것으로 변경하거나 쓰기 액세스 권한이 있는 GID에 `sonarr`을 추가해야 합니다.

거의 끝났습니다. 서비스를 시작해 봅시다.

```shell
service sonarr start
```

모든 것이 계획대로 진행되었다면 sonarr이 jail의 IP (포트 8989)에서 정상적으로 실행됩니다!

이제 쉘을 안전하게 닫을 수 있습니다.

## 문제 해결

- 서비스가 실행 중인 것처럼 보이지만 UI가 로드되지 않거나 페이지가 시간 초과되는 경우
  - jail에서 `allow_mlock`이 활성화되어 있는지 다시 확인하세요.
  
- `System.NET.Sockets.SocketException (43): Protocol not supported`
  - jail에 `VNET`이 켜져 있는지, ip6=inherit 또는 ip6=new인지 확인하세요.

> 서비스 스크립트는 이제 VNET 또는 IP6에 대한 요구 사항을 제거하므로 VNET 또는 ip6=inherit이 필요하지 않습니다. {.is-info}

### BSD Mono SSL 문제

- SSL 또는 기타 인증서 문제 (예: `unable to verify SSL certificate`)
  - [이 TrueNAS 포럼 게시물을 참조하여 mono의 인증서를 업데이트하고 동기화해야 합니다](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)