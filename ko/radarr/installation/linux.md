---
title: Radarr Linux 설치
description: Radarr를 위한 Linux 설치 가이드
published: true
date: 2023-09-07T20:43:01.533Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:59.391Z
---

# Linux

## Debian / Ubuntu

> 참고: Raspberry Pi OS와 Raspbian은 둘 다 Debian의 변형입니다. {.is-info}

### 쉬운 설치

Debian / Ubuntu / Raspbian 초보자를 위해 Apt 저장소나 Deb 패키지는 제공되지 않습니다.

쉬운 설치 스크립트를 사용하면 Debian (Raspbian / Raspberry Pi OS) / Ubuntu 기반 설치를 쉽게 할 수 있습니다. 이 스크립트는 커뮤니티에서 제공하며 유지 관리됩니다.

**'Hands on' 설치 지침을 따르려면 [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) 단계를 참조하세요.**

[\*Arr 커뮤니티 설치 스크립트를 확인하세요](/install-script)

> Radarr는 미디어 파일 분석을 위해 번들 버전의 ffprobe를 사용하며 시스템에 ffprobe 또는 ffmpeg를 설치할 필요가 없습니다. Radarr에서 Ffprobe를 찾을 수 없다는 메시지가 표시되면 재설치로 해결할 수 있습니다. {.is-info}

### Debian / Ubuntu Hands on Install

아래 명령을 사용하여 이진 파일을 설치해야 합니다.

> 아래 단계는 안정 버전 (`master` 릴리스 브랜치)의 Radarr을 다운로드하고 `/opt`에 설치합니다.
> Radarr은 사용자 `radarr`와 그룹 `media`에서 실행됩니다. `media`는 \*Arrs, 다운로드 클라이언트 및 미디어 서버를 실행하는 데 일반적으로 제안되는 그룹입니다.
> Radarr의 구성 파일은 `/var/lib/radarr`에 저장됩니다. {.is-success}

- 필요한 선행 패키지를 설치하세요:

```shell
sudo apt install curl sqlite3
```

> 경고: 아래 선행 조건을 무시하면 설치에 실패하고 애플리케이션이 작동하지 않을 수 있습니다. {.is-warning}

> **설치 전제 조건**
> 아래 지침은 다음 전제 조건을 기반으로 합니다. 필요한 경우 지침을 변경하여 특정 요구 사항에 맞게 수정하세요.
> \* 사용자 `radarr`가 생성되었습니다.
> \* 사용자 `radarr`가 그룹 `media`의 일부입니다.
> \* 다운로드 클라이언트 및 미디어 서버가 그룹 `media`로 실행되고 속해 있습니다.
> \* 다운로드 클라이언트 및 미디어 서버에서 사용하는 경로가 그룹 `media`에 대해 액세스 가능(읽기/쓰기)해야 합니다.
> \* `/var/lib/radarr` 디렉토리를 생성하고 사용자 `radarr`이 읽기/쓰기 권한을 갖도록 했습니다.
> \* 이전/기존 설치가 [FAQ](/radarr/faq)에서 지정한 `master` 릴리스 브랜치를 사용하거나 다운로드 URL에서 `master`를 업데이트했습니다. {.is-danger}

> 아래를 계속 진행하면 위의 요구 사항을 읽고 충족시켰다는 것을 인정하는 것입니다. {.is-success}

- 아키텍처에 맞는 바이너리를 다운로드하세요.
  - 아키텍처는 `dpkg --print-architecture` 명령으로 확인할 수 있습니다.
    - AMD64의 경우 `arch=x64`를 사용합니다.
    - ARM, armf, armh의 경우 `arch=arm`을 사용합니다.
    - ARM64의 경우 `arch=arm64`를 사용합니다.

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- 파일을 압축 해제하세요:

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- 파일을 `/opt/`로 이동하세요:

```shell
sudo mv Radarr /opt/
```

> 참고: 이는 사용자 `radarr`와 그룹 `media`에서 실행할 것으로 가정합니다. 필요에 따라 이를 변경할 수 있습니다. 미디어 파일의 권한 문제를 피하기 위해 적어도 그룹 이름을 다운로드 클라이언트와 Radarr 사이에서 동일하게 유지하는 것이 중요합니다. {.is-danger}

- 바이너리 디렉토리의 소유권을 확인하세요.

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- systemd를 구성하여 Radarr가 부팅 시 자동으로 시작되도록 합니다.

> 아래 systemd 생성 스크립트는 데이터 디렉토리로 `/var/lib/radarr`를 사용합니다. 디렉토리가 존재하거나 필요에 따라 수정하세요. 기본 데이터 디렉토리인 `/home/$USER/.config/Radarr`의 경우 `-data` 인수를 제거하세요. `$USER`는 Radarr이 실행되는 사용자로 아래에서 정의됩니다. {.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr.service > /dev/null
[Unit]
Description=Radarr Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr/
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

- Radarr 서비스를 활성화하세요:

```shell
sudo systemctl enable --now -q radarr
```

- (선택 사항) tarball을 제거하세요:

```shell
rm Radarr*.linux*.tar.gz
```

일반적으로 Radarr 웹 GUI에 액세스하려면 `http://{서버 IP 주소}:7878`로 이동하세요.

> Radarr는 미디어 파일 분석을 위해 번들 버전의 ffprobe를 사용하며 시스템에 ffprobe 또는 ffmpeg를 설치할 필요가 없습니다. Radarr에서 Ffprobe를 찾을 수 없다는 메시지가 표시되면 재설치로 해결할 수 있습니다. {.is-info}

Radarr가 시작되지 않은 경우 서비스 상태를 확인하세요:

```shell
sudo journalctl --since today -u radarr
```

---

### 제거

제거 및 완전 삭제하려면:
> 경고: 이렇게 하면 애플리케이션 데이터가 삭제됩니다. {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

애플리케이션 데이터를 유지한 채로 제거하려면:

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```