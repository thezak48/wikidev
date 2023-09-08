**Markdown Content to be translated:**

# User Documentation

Welcome to our user documentation! Here you will find all the information you need to get started with our product.

## Table of Contents

- [Getting Started](#getting-started)
- [Features](#features)
- [FAQ](#faq)
- [Contact Us](#contact-us)

## Getting Started

To get started with our product, follow these steps:

1. Sign up for an account [here](https://www.example.com/signup).
2. Download the latest version of our product from [this link](https://www.example.com/download).
3. Install the product on your device.
4. Launch the product and sign in with your account credentials.
5. You're ready to start using our product!

## Features

Our product offers the following features:

- Feature 1: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
- Feature 2: Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
- Feature 3: Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

## FAQ

Here are some frequently asked questions:

1. **Q:** How do I reset my password?
   **A:** To reset your password, go to the login page and click on the "Forgot Password" link. Follow the instructions to reset your password.

2. **Q:** Can I use the product on multiple devices?
   **A:** Yes, you can use the product on multiple devices. Simply sign in with your account credentials on each device.

3. **Q:** Is there a mobile app available?
   **A:** Yes, we have a mobile app available for both iOS and Android. You can download it from the App Store or Google Play Store.

## Contact Us

If you have any further questions or need assistance, please contact our support team at support@example.com.

---

# 사용자 문서

사용자 문서에 오신 것을 환영합니다! 여기에서는 제품을 시작하는 데 필요한 모든 정보를 찾을 수 있습니다.

## 목차

- [시작하기](#getting-started)
- [기능](#features)
- [자주 묻는 질문](#faq)
- [문의하기](#contact-us)

## 시작하기

제품을 시작하려면 다음 단계를 따르세요:

1. [여기](https://www.example.com/signup)에서 계정을 등록하세요.
2. [이 링크](https://www.example.com/download)에서 최신 버전의 제품을 다운로드하세요.
3. 제품을 기기에 설치하세요.
4. 제품을 실행하고 계정 자격 증명으로 로그인하세요.
5. 이제 제품을 사용할 준비가 되었습니다!

## 기능

저희 제품은 다음과 같은 기능을 제공합니다:

- 기능 1: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
- 기능 2: Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
- 기능 3: Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

## 자주 묻는 질문

다음은 자주 묻는 질문입니다:

1. **Q:** 비밀번호를 재설정하는 방법은 무엇인가요?
   **A:** 비밀번호를 재설정하려면 로그인 페이지로 이동하여 "비밀번호를 잊으셨나요?" 링크를 클릭하세요. 지침에 따라 비밀번호를 재설정하세요.

2. **Q:** 제품을 여러 기기에서 사용할 수 있나요?
   **A:** 네, 여러 기기에서 제품을 사용할 수 있습니다. 각 기기에서 계정 자격 증명으로 로그인하세요.

3. **Q:** 모바일 앱을 사용할 수 있나요?
   **A:** 네, iOS 및 Android용 모바일 앱을 사용할 수 있습니다. App Store 또는 Google Play Store에서 다운로드할 수 있습니다.

## 문의하기

추가 질문이 있거나 도움이 필요한 경우 support@example.com으로 지원팀에 문의하세요.

---
title: Lidarr 시스템
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, system
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# 목차

- [목차](#목차)
- [상태](#상태)
  - [건강 상태](#건강-상태)
    - [시스템 경고](#시스템-경고)
      - [브랜치가 유효한 릴리스 브랜치가 아닙니다](#브랜치가-유효한-릴리스-브랜치가-아닙니다)
      - [.NET 버전으로 업데이트](#net-버전으로-업데이트)
        - [도커 설치 수정](#도커-설치-수정)
        - [독립 설치 수정](#독립-설치-수정)
      - [현재 설치된 모노 버전이 오래되어 더 이상 지원되지 않습니다](#현재-설치된-모노-버전이-오래되어-더-이상-지원되지-않습니다)
      - [현재 설치된 SQLite 버전은 지원되지 않습니다](#현재-설치된-sqlite-버전은-지원되지-않습니다)
      - [새로운 업데이트가 있습니다](#새로운-업데이트가-있습니다)
      - [시작 폴더가 사용자에 의해 쓰기 가능하지 않아 업데이트를 설치할 수 없습니다](#시작-폴더가-사용자에-의해-쓰기-가능하지-않아-업데이트를-설치할-수-없습니다)
      - [업데이트를 방지하기 위해 AppData를 삭제하지 않도록 업데이트할 수 없습니다](#업데이트를-방지하기-위해-appdata를-삭제하지-않도록-업데이트할-수-없습니다)
      - [브랜치는 이전 버전을 위한 것입니다](#브랜치는-이전-버전을-위한-것입니다)
      - [signalR에 연결할 수 없습니다](#signalr에-연결할-수-없습니다)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [구성된 프록시 호스트의 IP 주소를 확인할 수 없습니다](#구성된-프록시-호스트의-ip-주소를-확인할-수-없습니다)
      - [프록시 테스트 실패](#프록시-테스트-실패)
      - [시스템 시간이 1일 이상 차이가 납니다](#시스템-시간이-1일-이상-차이가-납니다)
      - [Mono Legacy TLS가 활성화되었습니다](#mono-legacy-tls가-활성화되었습니다)
      - [Mono 및 x86 빌드가 종료됩니다](#mono-및-x86-빌드가-종료됩니다)
      - [FPcalc를 업데이트해야 합니다](#fpcalc를-업데이트해야-합니다)
    - [다운로드 클라이언트](#다운로드-클라이언트)
      - [사용 가능한 다운로드 클라이언트가 없습니다](#사용-가능한-다운로드-클라이언트가-없습니다)
      - [다운로드 클라이언트와 통신할 수 없습니다](#다운로드-클라이언트와-통신할-수-없습니다)
      - [다운로드 클라이언트를 사용할 수 없습니다](#다운로드-클라이언트를-사용할-수-없습니다)
      - [완료된 다운로드 처리 활성화](#완료된-다운로드-처리-활성화)
      - [Docker 잘못된 원격 경로 매핑](#docker-잘못된-원격-경로-매핑)
      - [루트 폴더로 다운로드](#루트-폴더로-다운로드)
      - [잘못된 다운로드 클라이언트 설정](#잘못된-다운로드-클라이언트-설정)
      - [잘못된 원격 경로 매핑](#잘못된-원격-경로-매핑)
      - [권한 오류](#권한-오류)
      - [원격 파일이 처리 중에 제거되었습니다](#원격-파일이-처리-중에-제거되었습니다)
      - [원격 경로 사용 및 가져오기 실패](#원격-경로-사용-및-가져오기-실패)
    - [완료/실패한 다운로드 처리](#완료실패한-다운로드-처리)
      - [완료된 다운로드 처리가 비활성화되었습니다](#완료된-다운로드-처리가-비활성화되었습니다)
    - [인덱서](#인덱서)
      - [자동 검색이 활성화된 인덱서가 없습니다. Lidarr는 자동 검색 결과를 제공하지 않습니다](#자동-검색이-활성화된-인덱서가-없습니다-lidarr는-자동-검색-결과를-제공하지-않습니다)
      - [RSS 동기화가 활성화된 인덱서가 없습니다. Lidarr는 새 릴리스를 자동으로 가져오지 않습니다](#rss-동기화가-활성화된-인덱서가-없습니다-lidarr는-새-릴리스를-자동으로-가져오지-않습니다)
      - [인덱서가 활성화되지 않았습니다](#인덱서가-활성화되지-않았습니다)
    - [활성화된 인덱서가 검색을 지원하지 않습니다](#활성화된-인덱서가-검색을-지원하지-않습니다)
      - [대화식 검색이 활성화된 인덱서가 없습니다](#대화식-검색이-활성화된-인덱서가-없습니다)
      - [인덱서가 실패로 인해 사용할 수 없습니다](#인덱서가-실패로-인해-사용할-수-없습니다)
      - [Jackett의 모든 엔드포인트가 사용되었습니다](#jackett의-모든-엔드포인트가-사용되었습니다)
        - [해결 방법](#해결-방법)
    - [아티스트 폴더](#아티스트-폴더)
      - [루트 폴더가 없습니다](#루트-폴더가-없습니다)
      - [목록이 실패로 인해 사용할 수 없습니다](#목록이-실패로-인해-사용할-수-없습니다)
  - [디스크 공간](#디스크-공간)
  - [정보](#정보)
  - [추가 정보](#추가-정보)
- [작업](#작업)
  - [스케줄된 작업](#스케줄된-작업)
  - [대기열](#대기열)
- [백업](#백업)
- [업데이트](#업데이트)
- [이벤트](#이벤트)
- [로그 파일](#로그-파일)

> 경고: 이 페이지는 작업 중인 초안이며 현재 Readarr을 기반으로 한 개략적인 초안입니다
{.is-danger}

# 상태

## 건강 상태

이 페이지에는 Lidarr에서 주기적으로 수행되는 건강 상태 확인 오류 목록이 포함되어 있습니다. 이 건강 상태 확인은 Lidarr에서 주기적으로 수행되며 특정 이벤트에서 수행됩니다. 결과적으로 발생한 경고 및 오류는 여기에 나열되어 해결 방법을 제공하기 위해 나열됩니다.

### 시스템 경고

#### 브랜치가 유효한 릴리스 브랜치가 아닙니다

설정한 브랜치가 유효한 릴리스 브랜치가 아닙니다. 업데이트를 받을 수 없습니다. [현재 릴리스 브랜치](/lidarr/faq#how-do-i-update-lidarr) 중 하나로 변경하십시오.

#### .NET 버전으로 업데이트

{#update-to-net-core-version}

- Lidarr의 최신 버전은 .NET6 이상을 대상으로 합니다. 1.0 이후로는 레거시 모노 빌드를 더 이상 제공하지 않을 예정입니다. 현재 사용 중인 플랫폼이 .NET을 지원하지만 이전 빌드 중 하나를 실행 중입니다.

##### 도커 설치 수정

- 컨테이너를 다시 가져옵니다.

##### 독립 설치 수정

- 다음 단계 이전에 기존 구성을 백업하십시오.
- 이 단계는 Linux 호스트에서만 발생해야 합니다. Microsoft의 .NET 런타임 또는 SDK를 설치하지 마십시오.
- 이를 해결하려면 아키텍처에 맞는 올바른 빌드를 다운로드하고 기존 이진 파일(응용 프로그램)을 교체해야 합니다.
- 간단히 말해서 기존 이진 파일(/opt/Lidarr의 내용 또는 폴더)을 삭제하고 방금 다운로드한 .tar.gz의 내용으로 대체해야 합니다.

> 기존 이진 파일 위에 다운로드를 바로 풀어 헤치지 마십시오.
> 먼저 이전 파일을 삭제해야 합니다.
{.is-warning}

- 아래는 모노 설치를 제거하고 .NET 설치로 대체하는 커뮤니티에서 개발한 스크립트입니다. 기여 및 수정은 환영합니다.
- 이 스크립트는 `master` Lidarr 브랜치에서 실행되는 것으로 가정합니다. 필요한 경우 변수를 업데이트하십시오.
- Lidarr가 `lidarr` 사용자로 실행되는 것으로 가정합니다. 필요한 경우 변수를 업데이트하십시오.
- Lidarr가 `/opt/Lidarr`에 설치되었다고 가정합니다. 필요한 경우 변수를 업데이트하십시오.

```bash
#!/bin/bash
## 사용자 변수
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /사용자 변수
app="lidarr"
ARCH=$(dpkg --print-architecture)
# \*arr 중지
sudo systemctl stop $app
# 아키텍처 가져오기
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "지원되지 않는 아키텍처입니다"
    exit 1
    ;;
esac
echo "다운로드 중..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "설치 파일 다운로드 및 추출 완료"
echo "기존 설치 이동 중"
sudo mv "$installdir/" "$installdir.old/"
echo "설치 중..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "앱 설치 완료"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### 현재 설치된 모노 버전이 오래되어 더 이상 지원되지 않습니다

- Lidarr은 .NET으로 작성되었으며 매우 오래된 ARM 프로세서에서 실행되기 위해 Mono가 필요합니다. Mono 빌드는 v1.0 이후로 더 이상 지원되지 않습니다.
- Lidarr의 최소 요구 버전은 Mono 5.20입니다.
- Mono의 업그레이드 절차는 플랫폼마다 다릅니다.

#### 현재 설치된 SQLite 버전은 지원되지 않습니다

- Lidarr은 데이터를 SQLite 데이터베이스에 저장합니다. 시스템에 설치된 SQLite3 라이브러리가 너무 오래되었습니다. Lidarr은 최소 3.9.0 버전 이상이 필요합니다. Lidarr은 SQLite3 업그레이드 패키지에 포함되어 있는 `libSQLite3.so`를 사용합니다.

#### 새로운 업데이트가 있습니다

- 개발자가 새로운 업데이트를 릴리스했습니다. 이는 일반적으로 멋진 새로운 기능과 버그 수정을 의미합니다 (맞나요?). 자동 업데이트가 활성화되어 있지 않으므로 업데이트하는 방법을 찾아야 합니다. 일반적으로 `시스템 => 업데이트` 페이지에서 설치 버튼을 누르는 것이 좋은 시작점입니다.

> 현재 버전이 14일 이내인 경우에는 이 경고가 표시되지 않습니다
{.is-info}

#### 시작 폴더가 사용자에 의해 쓰기 가능하지 않아 업데이트를 설치할 수 없습니다

- 이는 Lidarr가 자체 업데이트를 수행할 수 없음을 의미합니다. Lidarr을 수동으로 업데이트하거나 Lidarr의 시작 디렉토리(설치 디렉토리)의 권한을 설정하여 Lidarr이 자체 업데이트할 수 있도록 해야 합니다.

#### 업데이트를 방지하기 위해 AppData를 삭제하지 않도록 업데이트할 수 없습니다

- Lidarr는 운영 체제의 AppData 폴더가 Lidarr 이진 파일을 포함하는 디렉토리 내에 있는 것을 감지했습니다. 일반적으로 Windows의 경우 `C:\ProgramData`이고, Linux의 경우 `~/.config`입니다.

- 현재 상태에서 Lidarr은 데이터 손실의 위험 없이 자체 업데이트할 수 없습니다.
- Linux의 경우 Lidarr를 실행하는 사용자의 홈 디렉토리를 변경하고 `~/.config/Lidarr` 디렉토리의 현재 내용을 복사하여 데이터베이스를 보존해야 합니다.
- 현재 AppData 및 시작 디렉토리를 확인하려면 `시스템 => 정보`를 참조하십시오.
- 이로 인해 Lidarr은 데이터 손실의 위험 없이 자체 업데이트할 수 없습니다.
- Linux의 경우 Lidarr를 실행하는 사용자의 홈 디렉토리를 변경하고 `~/.config/Lidarr` 디렉토리의 현재 내용을 복사하여 데이터베이스를 보존해야 합니다.

#### 브랜치는 이전 버전을 위한 것입니다

- `설정 => 일반`에서 설정한 업데이트 브랜치는 이전 버전의 Lidarr을 위한 것이므로 `시스템 => 업데이트` 피드에서 올바른 업데이트 정보를 볼 수 없으며 새로운 업데이트를 받을 수 없을 수 있습니다.

#### signalR에 연결할 수 없습니다

- signalR은 동적 UI 업데이트를 제어합니다. 따라서 브라우저가 서버의 signalR에 연결할 수 없으면 UI에서 실시간 업데이트를 볼 수 없습니다.

- 가장 일반적인 경우는 리버스 프록시나 클라우드플레어를 사용하는 경우입니다.
- 클라우드플레어는 웹소켓을 활성화해야 합니다.

##### NGINX

- Nginx에서 앱의 위치 블록에 다음을 추가해야 합니다:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> nginx 문서에서 제안하는대로 `proxy_set_header Connection "Upgrade";`를 포함하지 마십시오. 이렇게 하면 작동하지 않습니다.
> <https://github.com/aspnet/AspNetCore/issues/17081> 참조
{.is-warning}

##### Apache

- Apache2 리버스 프록시를 위해 다음 모듈을 활성화해야 합니다: proxy, proxy_http 및 proxy_wstunnel. 그런 다음 다음 웹소켓 터널 지시문을 vhost 구성에 추가하십시오:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- Caddy (V1)의 경우 다음을 사용하십시오:
- 참고: lidarr 구성에 웹소켓 지시문을 추가해야 합니다.

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### 구성된 프록시 호스트의 IP 주소를 확인할 수 없습니다

- 프록시 설정을 검토하고 정확한지 확인하십시오.
- 프록시가 실행 중이고 작동 가능한지 확인하십시오.

#### 프록시 테스트 실패

- 구성된 프록시가 테스트에 실패했습니다. 제공된 HTTP 오류를 검토하거나 자세한 내용은 로그를 확인하십시오.

#### 시스템 시간이 1일 이상 차이가 납니다

- 시스템 시간이 1일 이상 차이가 납니다. 시스템 시간이 올바르게 수정되기 전까지 예약된 작업이 올바르게 실행되지 않을 수 있습니다.
- 시스템 시간을 검토하고 권위 있는 시간 서버와 동기화되고 정확한지 확인하십시오.

#### Mono Legacy TLS가 활성화되었습니다

- Mono 4.x tls 회피 방법이 아직 활성화되어 있습니다. `MONO_TLS_PROVIDER=legacy` 환경 옵션을 제거하는 것을 고려하십시오.

#### Mono 및 x86 빌드가 종료됩니다

- Mono 및 x86 빌드는 응용 프로그램의 다음 빌드에서 더 이상 지원되지 않을 예정입니다. 이 오류가 발생하면 응용 프로그램의 모노 버전 또는 x86 버전을 실행 중입니다. 이러한 레거시 버전의 개발 지원이 점점 어려워지기 때문에 이러한 버전의 지원을 중단하고 앞으로 이러한 버전에 대한 릴리스를 중단할 예정입니다. 따라서 x86 또는 모노를 필요로하지 않는 지원되는 운영 체제로 업그레이드하는 것이 좋습니다. 필요한 경우 Docker를 사용할 수도 있습니다.

#### FPcalc를 업데이트해야 합니다

{#fpcalc-upgrade}

- Lidarr은 음악 트랙을 식별하기 위해 chromaprint 오디오 지문을 사용합니다. 이는 Lidarr v1의 Windows, Linux 및 macOS용으로 제공되는 외부 이진 파일 `fpcalc`에 의존합니다. Lidarr의 설치 디렉토리(예: `/opt/Lidarr/fpcalc`)에 있는 Lidarr v1과 함께 제공되는 fpcalc 이진 파일이 실행 가능한지 확인하십시오. 실행 가능하지 않은 경우 아래 명령을 사용하여 권한을 수정한 다음 Lidarr을 다시 시작하십시오.
  - 참고: 이러한 수정에는 `sudo`가 필요할 수 있거나 환경 및 설정에 따라 Lidarr의 이진 파일 폴더 경로가 다를 수 있습니다.

```bash
chmod +x /opt/Lidarr/fpcalc
```

> 아래 정보는 레거시 v0.8.0 빌드 전용입니다.
{.is-info}

- 네이티브 Linux 인스턴스에서 이를 수정하려면 패키지 관리자를 사용하여 해당 패키지를 설치하고 fpcalc가 PATH에 있는지 확인하십시오(이는 `which fpcalc`을 사용하여 확인하고 올바른 fpcalc 위치가 반환되는지 확인할 수 있습니다):

| 배포판   |       패키지        |
| :------: | :-----------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### 다운로드 클라이언트

#### 사용 가능한 다운로드 클라이언트가 없습니다

- Lidarr이 미디어를 다운로드하려면 올바르게 구성된 활성화된 다운로드 클라이언트가 필요합니다. Lidarr은 다양한 다운로드 클라이언트를 지원하므로 요구 사항과 가장 일치하는 클라이언트를 결정해야 합니다. 이미 다운로드 클라이언트를 설치한 경우 Lidarr에서 사용하도록 구성하고 카테고리를 만들어야 합니다. `설정 => 다운로드 클라이언트`를 참조하십시오.

#### 다운로드 클라이언트와 통신할 수 없습니다

- Lidarr이 구성된 다운로드 클라이언트와 통신할 수 없습니다. 다운로드 클라이언트가 작동 중인지 확인하고 URL을 다시 확인하십시오. 이는 인증 오류일 수도 있습니다.
- 일반적으로 잘못 구성된 다운로드 클라이언트로 인한 문제입니다. 일반적으로 확인할 수 있는 사항:
  - 다운로드 클라이언트의 IP 주소 - 모두 동일한 기계에 있는 경우 일반적으로 `127.0.0.1`입니다.
  - 다운로드 클라이언트가 사용하는 포트 번호 - 기본 포트 번호로 채워져 있지만 변경한 경우 Lidarr에 동일한 포트 번호를 입력해야 합니다.
  - 로컬 네트워크(즉, 일반 HTTP로 Lidarr 인스턴스와 다운로드 클라이언트를 사용하는 경우)에서 Lidarr 인스턴스와 다운로드 클라이언트 모두 사용하는 경우 SSL 암호화가 비활성화되어 있는지 확인하십시오. 자세한 내용은 SSL FAQ 항목을 참조하십시오.

#### 다운로드 클라이언트를 사용할 수 없습니다

- 하나 이상의 다운로드 클라이언트가 Lidarr의 요청에 응답하지 않습니다. 따라서 Lidarr은 일반적으로 1분 주기로 다운로드 상태를 추적하고 완료된 다운로드를 가져오는 데 사용되는 작업을 일시적으로 중지합니다. 그러나 Lidarr은 계속해서 다운로드를 클라이언트에 전송하려고 시도하지만 아마도 실패할 것입니다.
- 실패 이유를 확인하려면 `시스템 => 로그`에서 이유를 확인하십시오.
- 더 이상 이 다운로드 클라이언트를 사용하지 않는 경우 Lidarr에서 비활성화하여 오류를 방지하십시오.

#### 완료된 다운로드 처리 활성화

- Lidarr은 다운로드 클라이언트에서 다운로드한 파일을 가져오기 위해 완료된 다운로드 처리를 사용해야 합니다. 완료된 다운로드 처리를 활성화하는 것이 좋습니다. (새로운 사용자의 경우 기본적으로 완료된 다운로드 처리가 활성화됩니다.)

#### Docker 잘못된 원격 경로 매핑

- 이 오류는 다운로드 클라이언트나 Lidarr의 잘못된 도커 경로와 관련됩니다.

- 잘못된(일관성 없는) 경로의 예는 다음과 같습니다:
  - 다운로드 클라이언트: `/mnt/user/downloads:/downloads`
  - Lidarr: `/mnt/user/downloads:/data`
- 이 예에서 다운로드 클라이언트는 다운로드를 `/downloads`에 위치시키고 완료된 책이 `/downloads`에 있다고 Lidarr에 알립니다. Lidarr은 "좋아요, `/downloads`를 확인해보겠습니다."라고 말합니다. 그러나 Lidarr 내부에서는 `/downloads` 경로를 할당하지 않았고 `/data` 경로를 할당했으므로 이 오류가 발생합니다.
- 이를 해결하는 가장 쉬운 방법은 일관성입니다. 다운로드 클라이언트에서 한 체계를 사용하는 경우 전체 체계에서 동일한 체계를 사용하십시오.

- Lidarr 팀은 `/data`를 사용하는 것을 권장합니다.

  - 다운로드 클라이언트: `/mnt/user/data/downloads:/data/downloads`
  - Lidarr: `/mnt/user/data:/data`

- 이제 다운로드 클라이언트에서 `/data`에 다운로드를 저장할 위치를 지정할 수 있습니다. 이는 클라이언트에 따라 다릅니다. "예, 다운로드 클라이언트야, 파일을 `/data/downloads/movies`에 저장해줘"라고 말할 수 있으며 Lidarr은 `/data`를 사용하므로 다운로드 클라이언트가 완료되었다고 알리면 Lidarr은 "좋아, `/data`가 있고 `/data/downloads/movies`도 볼 수 있으니까 모든 것이 올바르게 작동합니다."라고 말합니다.
- 많은 훌륭한 가이드가 있습니다: 우리의 위키 [Docker 가이드](/docker-guide) 및 TRaSH의 [Hardlinks 및 Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) 가이드입니다. 이 가이드는 하드링크 및 원자적 이동에 중점을 두지만 컨테이너와 경로 매핑이 작동하는 방식에 대한 개념이 이러한 토론의 핵심입니다.
- 운영 체제를 넘나드는 경우 또는 네이티브 및 도커를 넘나드는 경우 원격 경로 매핑이 필요합니다. 자세한 내용은 [TRaSH의 Radarr 원격 경로 가이드](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) 및 [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/)를 참조하십시오.

#### 루트 폴더로 다운로드

{#downloads-in-root-folder}

- 응용 프로그램에서 루트 폴더는 구성된 미디어 라이브러리 폴더로 정의됩니다. 이는 마운트의 루트 폴더가 아닙니다. 다운로드 클라이언트가 루트(라이브러리) 폴더로 불완전하거나 완료된 다운로드(또는 완료된 다운로드를 이동하는 경우)를 이동하고 있습니다.
- 이는 자주 문제를 일으키며 데이터 손실을 포함할 수 있으므로 수행해서는 안 됩니다. 이를 수정하려면 다운로드 클라이언트를 변경하여 루트 폴더에 다운로드하지 않도록 설정하십시오. '배치' 클라이언트의 경우 다운로드 클라이언트 카테고리가 루트 폴더로 설정되어 있거나 NZBGet/SABnzbd가 정렬을 사용하고 루트 폴더로 정렬하고 있는지 확인하십시오.
- 구성된 루트 폴더(라이브러리 폴더)는 [설정 => 미디어 관리 => 루트 폴더](/lidarr/settings/#root-folders)에서 찾을 수 있습니다.
- 예를 들어 다운로드가 `\data\downloads`로 이동하는 경우 루트 폴더가 `\data\downloads`로 설정되어 있습니다.
- 루트 폴더/라이브러리 폴더로 사용하는 폴더와 다운로드 클라이언트의 폴더는 분리되어야 합니다. \*Arr은 다운로드 클라이언트의 폴더에서 파일을 가져와 라이브러리로 가져옵니다. 다운로드 클라이언트는 라이브러리로 아무 것도 이동하거나 다운로드해서는 안 됩니다.
- 올바른 경로 설정에 대한 자세한 내용은 올바른 경로 설정에 대한 정보를 위해 [Docker 가이드](/docker-guide) 및 TRaSH의 [Hardlinks 및 Instant Moves (Atomic-Moves) 가이드](https://trash-guides.info/hardlinks/)를 검토하십시오. 도커 및 도커가 아닌 경우에도 개념이 적용됩니다.

> 다운로드 클라이언트가 다운로드를 배치하는 폴더와 루트/라이브러리 폴더는 반드시 분리되어야 합니다. \*Arr은 다운로드 클라이언트의 폴더에서 파일을 가져와 라이브러리로 가져옵니다. 다운로드 클라이언트는 라이브러리로 아무 것도 이동하거나 다운로드해서는 안 됩니다.
{.is-warning}

#### 잘못된 다운로드 클라이언트 설정

- 다운로드 클라이언트가 파일을 다운로드하는 위치가 문제를 일으키고 있습니다. 자세한 내용은 로그를 확인하십시오. 이는 권한 문제이거나 Windows에서 Linux로 또는 Linux에서 Windows로 이동하려고 하거나 원격 경로 매핑이 없는 경우일 수 있습니다.

#### 잘못된 원격 경로 매핑

- 다운로드 클라이언트가 파일을 다운로드하는 위치가 문제를 일으키고 있습니다. 자세한 내용은 로그를 확인하십시오. 이는 권한 문제이거나 Windows에서 Linux로 또는 Linux에서 Windows로 이동하려고 하거나 원격 경로 매핑이 없는 경우일 수 있습니다. 자세한 내용은 [TRaSH의 원격 경로 가이드](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)를 참조하십시오.

#### 권한 오류

- Lidarr(또는 lidarr이 실행 중인 사용자)가 다운로드 클라이언트가 파일을 다운로드하는 위치에 액세스할 수 없습니다. 일반적으로 권한 문제입니다.

#### 원