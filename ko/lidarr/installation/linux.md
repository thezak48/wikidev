---
title: Lidarr Linux 설치
description: Lidarr을 위한 Linux 설치 가이드
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> 참고: Raspberry Pi OS와 Raspbian은 모두 Debian의 변형입니다 {.is-info}

> Lidarr v0.8은 Ubuntu 22.04에서 호환되지 않으며 지원되지 않습니다. [자세한 내용은 FAQ 항목을 참조하세요](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### 쉬운 설치

Debian / Ubuntu / Raspbian 초보자를 위해 Apt 저장소나 Deb 패키지는 제공되지 않습니다.

쉬운 설치 스크립트를 사용하여 Debian (Raspbian / Raspberry Pi OS) / Ubuntu를 설치하려면 다음 커뮤니티 제공 및 유지 관리되는 `쉬운 설치` 스크립트를 따르세요.

**'Hands on'으로 진행하는 공식 설치 지침은 아래의 [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) 단계를 따르세요.**

[\*Arr 커뮤니티 설치 스크립트를 참조하세요](/install-script)

### Debian / Ubuntu Hands on Install

아래 명령을 사용하여 이진 파일을 설치해야 합니다.

> 아래 단계는 Lidarr을 다운로드하고 `/opt`에 설치합니다.
> Lidarr은 사용자 `lidarr`와 그룹 `media`로 실행됩니다.
> Lidarr의 구성 파일은 `/var/lib/lidarr`에 저장됩니다.
{.is-warning}

- 필요한 선행 패키지를 설치하세요:

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> 경고: 아래 선행 요구 사항을 무시하면 설치에 실패하고 기능이 작동하지 않는 애플리케이션이 됩니다. {.is-warning}

> **설치 선행 조건**
> 아래 지침은 다음의 선행 조건을 기반으로 합니다. 필요한 경우 지침을 변경하여 특정 요구 사항에 맞게 수정하세요.
> \* 사용자 `lidarr`가 생성되었습니다.
> \* 사용자 `lidarr`가 그룹 `media`의 일부입니다.
> \* 다운로드 클라이언트와 미디어 서버가 그룹 `media`로 실행되고 소속되어 있습니다.
> \* 다운로드 클라이언트와 미디어 서버에서 사용하는 경로가 그룹 `media`에게 액세스 가능(읽기/쓰기)해야 합니다.
> \* `/var/lib/lidarr` 디렉토리를 생성하고 사용자 `lidarr`이 읽기/쓰기 권한을 갖도록 했습니다.
{.is-danger}

> 아래를 계속 진행하면 위의 요구 사항을 읽고 충족시켰다는 것을 인정하는 것입니다. {.is-warning}

- 아키텍처에 맞는 올바른 이진 파일을 다운로드하세요.
  - 아키텍처는 `dpkg --print-architecture`로 확인할 수 있습니다.
    - AMD64의 경우 `arch=x64`를 사용합니다.
    - ARM, armf, armh의 경우 `arch=arm`을 사용합니다.
    - ARM64의 경우 `arch=arm64`를 사용합니다.

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- 파일을 압축 해제하세요:

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- 파일을 `/opt/`로 이동하세요.

```shell
sudo mv Lidarr/ /opt
```

> 이 가정은 사용자를 생성하고 사용자 `lidarr`와 그룹 `media`로 실행한다고 가정합니다. 이를 필요에 맞게 변경할 수 있습니다. 미디어 파일의 권한 문제를 피하기 위해 적절한 그룹 이름을 최소한으로 유지하는 것이 중요합니다. {.is-danger}

- 바이너리 디렉토리의 소유권을 확인하세요.

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Lidarr이 부팅 시 자동으로 시작할 수 있도록 systemd를 구성하세요.

> 아래 systemd 생성 스크립트는 `/var/lib/lidarr` 데이터 디렉토리를 사용합니다. 필요한 경우 디렉토리를 수정하거나 적절하게 변경하세요. `/home/$USER/.config/Lidarr`의 기본 데이터 디렉토리의 경우 `-data` 인수를 제거하세요. 참고: `$USER`는 Lidarr이 실행되는 사용자로 아래에서 정의됩니다.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/lidarr.service > /dev/null
[Unit]
Description=Lidarr Daemon
After=syslog.target network.target
[Service]
User=lidarr
Group=media
Type=simple

ExecStart=/opt/Lidarr/Lidarr -nobrowser -data=/var/lib/lidarr/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- systemd를 다시 로드하세요:

```shell
sudo systemctl -q daemon-reload
```

- Lidarr 서비스를 활성화하세요:

```shell
sudo systemctl enable --now -q lidarr
```

- (선택 사항) tarball을 제거하세요:

```shell
rm Lidarr*.linux*.tar.gz
```

일반적으로 Lidarr 웹 GUI에 액세스하려면 `http://{서버 IP 주소}:8686`로 이동하세요.

Lidarr이 시작되지 않은 경우 서비스 상태를 확인하세요:

```shell
sudo journalctl --since today -u lidarr
```

---

### 제거

제거하려면 다음을 실행하세요:
> 경고: 이렇게 하면 애플리케이션 데이터가 삭제됩니다. {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

애플리케이션 데이터를 유지하면서 제거하려면 다음을 실행하세요:

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```