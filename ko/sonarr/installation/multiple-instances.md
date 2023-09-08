---
title: 다중 인스턴스
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# 다중 인스턴스

Sonarr을 여러 개의 인스턴스로 실행할 수 있습니다. 이는 일련의 시리즈의 4K 및 1080p 복사본을 원할 때 일반적으로 수행됩니다.
[Sonarr을 두 번째 Sonarr로 구성하여 목록으로 사용할 수 있습니다. 두 인스턴스를 동기화하려는 경우에 유용합니다.](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Windows에서 다중 인스턴스](#windows-multi)
- [Linux에서 다중 인스턴스](#linux-multi)
- [Docker에서 다중 인스턴스](#docker-multi)
{.links-list}

다음 요구 사항을 유의해야 합니다:

- Docker가 아닌 경우, 동일한 이진 파일(프로그램 파일)을 사용해야 합니다.
- Docker가 아닌 경우, 모든 인스턴스에 `-data=` 또는 `/data=` 인수를 전달해야 합니다.
- Docker가 아닌 경우, 다른 포트를 사용해야 합니다.
  - Docker인 경우, 다른 외부 포트를 사용해야 합니다.
- 다른 다운로드 클라이언트 카테고리를 사용해야 합니다.
- 다른 루트 폴더를 사용해야 합니다.
- Docker가 아닌 경우, 1개의 인스턴스를 제외한 모든 인스턴스에서 자동 업데이트를 비활성화해야 합니다.

## Windows에서 다중 인스턴스

{#windows-multi}

이 가이드에서는 Windows에서 하나의 기본 설치만 사용하여 Sonarr의 여러 인스턴스를 실행하는 방법을 보여줍니다. 이 가이드는 Windows 10을 사용하여 작성되었으며, 이전 버전의 Windows(7, 8 등)을 사용하는 경우 일부 사항을 조정해야 할 수 있습니다. 이 가이드는 또한 Sonarr을 기본 디렉토리에 설치하고 두 번째 Sonarr 인스턴스를 Sonarr-4K라고 가정합니다. 필요에 따라 설치를 변경하여 자신의 설치에 맞게 변경하십시오.

### 서비스 (Windows)

#### 사전 요구 사항 (서비스)

- [Sonarr이 이미 설치되어 있어야 합니다](#windows)
- [NSSM (Non-Sucking Service Manager)](http://nssm.cc)이 설치되어 있어야 합니다. 설치하려면 최신 릴리스(글 작성 시점의 버전은 2.24)를 다운로드하고 32비트 또는 64비트 nssm.exe 파일을 C:/windows/system32에 복사하십시오.
  - 32비트 또는 64비트 시스템인지 확실하지 않은 경우 설정 => 시스템 => 정보 => 시스템 유형을 확인하십시오.

#### Sonarr 서비스 구성

1. 관리자 권한으로 명령 프롬프트 창을 엽니다. (관리자로 실행하려면 명령 프롬프트 아이콘을 마우스 오른쪽 단추로 클릭하고 "관리자로 실행"을 선택하십시오.)
1. Sonarr이 실행 중인 경우 명령 프롬프트에서 `nssm stop Sonarr`를 실행하여 서비스를 중지합니다.
1. 이제 기존의 Sonarr 인스턴스를 명시적으로 데이터 디렉토리를 가리키도록 편집해야 합니다. 기본 명령은 다음과 같습니다:
   `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe -data=C:\ProgramData\Sonarr"`

이 명령은 기존의 Sonarr 인스턴스가 데이터 디렉토리로 `C:\ProgramData\Sonarr`를 명시적으로 사용하도록 지시합니다. Sonarr 설치를 기본값으로 사용하지 않았거나 데이터 폴더가 다른 위치에 있는 경우 여기서 경로를 변경해야 할 수 있습니다.

#### Sonarr-4K 서비스 생성

1. Sonarr-4K가 위치할 새 폴더를 만듭니다. 대부분의 경우 `C:\ProgramData\Sonarr-4K`와 같은 유사한 위치를 사용합니다.
1. 명령 프롬프트로 돌아가서 `nssm install Sonarr-4K`를 사용하여 새로운 Sonarr-4K 서비스를 생성합니다. 팝업 창이 열리고 새 인스턴스에 대한 매개변수를 입력할 수 있습니다. 이 예제에서는 다음과 같이 사용합니다:
   - 경로: `C:\ProgramData\Sonarr\bin\Sonarr.exe`
   - 시작 디렉토리: `C:\ProgramData\Sonarr\bin`
   - 인수: `-data=C:\ProgramData\Sonarr-4K`

> **인수**는 1단계에서 생성한 *새* 폴더를 가리킵니다. 이는 두 인스턴스의 모든 데이터 파일을 별도의 위치에 유지하기 때문에 중요합니다. {.is-warning}

1. *서비스 설치*를 클릭합니다. 창이 닫히고 서비스가 실행 가능한 상태가 됩니다.
1. [Sonarr-4k 구성](#windows-multi-config-second)을 계속합니다.

### 트레이 앱 (Windows)

#### 사전 요구 사항 (트레이 앱)

- [Sonarr이 이미 설치되어 있어야 합니다](#windows)
- Sonarr은 `/data=` 인수로 구성되어야 하며, 다중 인스턴스를 허용해야 합니다.
- 현재 사용자의 시작 폴더 `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`로 이동하여 필요한 경우 기존 바로 가기를 편집합니다.

#### Sonarr-4K 트레이 앱 생성

- 마우스 오른쪽 단추로 클릭하여 새 바로 가기를 만듭니다.
- 경로: `C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- `Sonarr-4K`와 같은 고유한 이름을 지정하고 마법사를 완료합니다.
- 새 바로 가기를 두 번 클릭하여 실행하고 테스트합니다.
- [Sonarr-4k 구성](#windows-multi-config-second)을 계속합니다.

### Sonarr-4k 구성 {#windows-multi-config-second}

- 서비스 방법 또는 트레이 앱을 사용한 경우에 관계없이 두 서비스와 두 앱을 모두 중지합니다.
- Sonarr-4k(서비스 또는 트레이 앱)를 시작합니다.
- Sonarr-4k를 열고 앱 내에서 [설정 => 일반 => 호스트](/sonarr/settings/#host)로 이동합니다.
- `포트 번호`를 `8989`에서 다른 포트(예: `7879`)로 변경하여 Sonarr과 Sonarr4k가 충돌하지 않도록 합니다.
- 이제 두 앱을 모두 시작할 수 있어야 합니다.
- [업데이트 처리](#dealing-with-updates)를 계속합니다.

### 업데이트 처리

- 인스턴스 중 하나에서 자동 업데이트를 비활성화합니다.
- Sonarr 인스턴스 중 하나가 업데이트되면 두 인스턴스가 모두 종료되고 업데이트된 인스턴스만 다시 시작됩니다. 이 문제를 해결하려면 다른 인스턴스를 수동으로 시작해야 할 수도 있으며, 아래의 PowerShell 스크립트를 사용하여 문제를 해결할 수도 있습니다.

#### Windows 포트 확인 및 다시 시작 PowerShell 스크립트

- 두 개의 Sonarr 인스턴스를 사용하고 하나가 업데이트되면 모든 인스턴스가 종료됩니다. 업데이트 중인 인스턴스만 다시 온라인 상태가 됩니다.
- 아래의 PowerShell 스크립트는 예약된 작업으로 구성되어야 합니다.
- 포트를 확인하고 하나의 포트가 온라인 상태가 아니면 Sonarr을 시작하는 예약된 작업을 (다시) 시작합니다.

1. 아래 코드로 SonarrInstancesChecker.ps1이라는 새 파일을 만듭니다.
1. 스크립트를 실제 서비스 이름, IP 및 포트로 편집합니다.
1. [반복 일정](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler)에 스크립트를 실행하도록 예약된 작업을 만듭니다.

- 보안 옵션: `최고 권한으로 실행` 활성화
  - 그렇지 않으면 스크립트는 서비스를 조작할 수 없습니다.
- 트리거: `시작 시`
- 작업 반복: `5` 또는 `10`분
- 작업: `프로그램 시작`
- 프로그램/스크립트: `powershell`
- 인수: `-File D:\SonarrInstancesChecker.ps1`
  - 스크립트의 위치에 대한 전체 경로를 사용해야 합니다.

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### Keeps multiple Sonarr Instances up by checking the port                                  ###
### Please use Sonarr´s Discord or Reddit for support!                                       ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Updated: 2020-10-22                                                                      ###
### Author:  reloxx13                                                                        ###
################################################################################################



### SET YOUR CONFIGURATION HERE ###
# Set your host ip and port correctly and use your service or scheduledtask names!

# (string) The type how Sonarr is starting
# "Service" (default) Service process is used
# "ScheduledTask" Task Scheduler is used
$startType = 'Service'

# (bool) Writes the log to C:\Users\YOURUSERNAME\log.txt when enabled
# $false (default)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instance 1
        Name = 'Sonarr-V3'; # (string) Service or Task name (default: Sonarr-V3)
        IP   = '192.168.178.12'; # (string) Server IP where Sonarr runs (default: 192.168.178.12)
        Port = '7873'; # (string) Server Port where Sonarr runs (default: 7873)
    }
    [pscustomobject]@{   # Instance 2
        Name = 'Sonarr-4K'; # (string) Service or Task name (default: Sonarr-4K)
        IP   = '192.168.178.12'; # (string) Server IP where Sonarr runs (default: 192.168.178.12)
        Port = '7874'; # (string) Server Port where Sonarr runs (default: 7874)
    }
    # If needed you can add more instances here... by uncommenting out the below lines
    # [pscustomobject]@{   # Instance 3
    # Name='Sonarr-3D';    # (string) Service or Task name (default: Sonarr-3D)
    # IP='192.168.178.12'; # (string) Server IP where Sonarr runs (default: 192.168.178.12)
    # Port='7875';         # (string) Server Port where Sonarr runs (default: 7875)
    # }
)


### DONT CHANGE ANYTHING BELOW THIS LINE ###


###
# This function will write to a log file or in console output
###
function Write-Log
{
    #Will write to C:\Users\YOURUSERNAME\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    #Console output
    Write-Output "[$(TS)]$Message"
    
    #File Output
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'START ====================='


$instances | ForEach-Object {
    Write-Log "Check $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "Port $($_.Port) is closed, restart $($startType) $($_.Name)!"

        if ($startType -eq 'Service')
        {
            Get-Service -Name $_.Name | Stop-Service
            Get-Service -Name $_.Name | Start-Service
        }
        elseif ($startType -eq 'ScheduledTask')
        {
            Get-ScheduledTask -TaskName $_.Name | Stop-ScheduledTask
            Get-ScheduledTask -TaskName $_.Name | Start-ScheduledTask
        }
        else
        {
            Write-Log '[ERROR] STARTTYPE UNKNOWN! USE Service or ScheduledTask !'
        }
    }
    else
    {
        Write-Log "Port $($_.Port) is open!"
    }
}

Write-Log 'END ====================='
```

## Linux에서 다중 인스턴스

{#linux-multi}

- [Swizzin 사용자](https://github.com/ComputerByte/sonarr4k)
- Swizzin 사용자가 아닌 경우
  - 첫 번째 인스턴스에 `-data=` 인수가 전달되었는지 확인합니다.
  - 두 번째 인스턴스의 포트를 변경하려면 첫 번째 인스턴스를 일시적으로 중지합니다. `systemctl stop sonarr`
  - Sonarr 인스턴스 중 하나에서 자동 업데이트를 비활성화합니다.

> 아래는 Sonarr4K 인스턴스를 생성하는 예제 스크립트입니다. 아래의 systemd 생성 스크립트는 데이터 디렉토리로 `/var/lib/sonarr4k/`를 사용합니다. 디렉토리가 존재하거나 필요에 따라 수정하십시오.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/sonarr4k.service > /dev/null
[Unit]
Description=Sonarr4k Daemon
After=syslog.target network.target
[Service]
User=sonarr
Group=media
Type=simple

ExecStart=mono --debug /usr/lib/sonarr/bin/Sonarr.exe -nobrowser -data=/var/lib/sonarr4k/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- systemd 다시 로드:

```shell
sudo systemctl -q daemon-reload
```

- Sonarr4k 서비스 활성화:

```shell
sudo systemctl enable --now -q sonarr4k
```

## Docker에서 다중 인스턴스

{#docker-multi}

- 위의 요구 사항을 충족하는 다른 이름의 두 번째 Docker 컨테이너를 생성하기만 하면 됩니다.