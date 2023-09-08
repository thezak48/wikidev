---
title: Synology 패키지
description: Servarr Synology 패키지
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synology 패키지](#servarr-synology-packages)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [DSM 7.X에서 Bubblewrap 설치](#bubblewrap-installation-on-dsm-7x)
    - [간단한 Bubblewrap 설치](#simple-bubblewrap-installation)
    - [수동 Bubblewrap 설치](#manual-bubblewrap-installation)

# Servarr Synology 패키지

> 이 패키지들은 "베타"로 간주될 수 있습니다.
{.is-danger}

- Servarr 팀이 Synology 패키지를 생성하고 유지 관리합니다.
- 설치 지침은 특정 DSM 버전에 대해 아래에 기재되어 있습니다.

> 일반적으로 Servarr 버전과 호환되지 않는 SynoCommunity 버전은 일부 추가 작업이 필요합니다. 이는 [데이터베이스 백업 *링크는 Radarr 예제를 위한 것이지만, 지침/개념은 동일합니다*](/radarr/faq#how-do-i-backuprestore-radarr)을 수행한 후 이전 패키지를 삭제해야 함을 의미합니다. 이는 \*Arr 앱의 웹 인터페이스를 통해 수행할 수 있습니다.
{.is-warning}

> SynoCommunity는 [NAS별 아키텍처 목록](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model)을 제공하여 올바른 패키지를 식별하는 데 도움이 됩니다.
{.is-info}

# DSM 6.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official, Readarr-Official 및 Sonarr 패키지는 *정상 작동*해야 합니다.
- SynoCommunity의 독립 Mono 패키지는 더 이상 필요하지 않으며, 현재 우리 패키지에 번들되어 있습니다.
- [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)에서 NAS 아키텍처에 해당하는 응용 프로그램 릴리스를 다운로드하고 [패키지 관리자를 통해 패키지를 수동으로 설치](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)합니다.

# DSM 7.x

- Lidarr-Official, Prowlarr-Official, Radarr-Official 및 Readarr-Official 패키지는 대부분의 아키텍처에서 *정상 작동*해야 합니다.
  - `comcerto2k`를 사용하는 NAS의 경우 Lidarr, Prowlarr, Radarr 및 Readarr에 대해 추가 단계가 필요합니다. [지침을 참조하세요](#bubblewrap-installation-on-dsm-7x).
- Sonarr 패키지는 **모든** 아키텍처에 대해 추가 단계가 필요합니다.
- SynoCommunity의 독립 Mono 패키지는 더 이상 필요하지 않으며, 현재 우리 패키지에 번들되어 있습니다.

> `comcerto2k`를 사용하는 NAS (*모든 패키지*) 및 Sonarr (*모든 NAS 아키텍처*)의 경우 Bubblewrap 패키지를 설치하고 수동 단계를 수행해야 합니다. **\*Arr 패키지를 설치하기 전에 Bubblewrap를 설치해야 합니다.**
{.is-warning}

- [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)에서 NAS 아키텍처에 해당하는 Bubblewrap 릴리스를 다운로드하고 [패키지 관리자를 통해 패키지를 수동으로 설치](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)합니다.
- DSM 7.X에서 아래 Bubblewrap 설치 단계를 완료합니다.
- Bubblewrap이 설치되면 [Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)에서 NAS 아키텍처에 해당하는 응용 프로그램 릴리스를 다운로드하고 [패키지 관리자를 통해 패키지를 수동으로 설치](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)합니다.

## DSM 7.X에서 Bubblewrap 설치

Bubblewrap을 사용하여 .NET6를 실행하기 위해 기본 컨테이너에서 프로그램을 실행할 수 있습니다.

> **DSM 7.0+의 제한 사항으로 인해 설치 후 일부 수동 설정이 필요합니다.**
{.is-danger}

### 간단한 Bubblewrap 설치

1. DSM 내에서 트리거된 작업을 생성합니다:

- 사용자: `root`
  - 이벤트: `부팅`

1. `실행 명령`에 다음을 입력합니다:

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. 트리거된 작업을 저장하고 한 번 실행합니다.

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### 수동 Bubblewrap 설치

1. [SSH를 통해 Synology에 로그인하고 `root`로 승격](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)합니다.
1. 다음 명령을 실행합니다:

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```