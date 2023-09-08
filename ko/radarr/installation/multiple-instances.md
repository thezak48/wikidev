# 다중 인스턴스

Radarr을 여러 개의 인스턴스로 실행할 수 있습니다. 이는 한 영화에 4K 및 1080p 복사본을 원하는 경우에 일반적으로 수행됩니다. 두 개의 Radarr을 동기화하여 사용하려면 [TRaSH의 가이드를 검토하고 두 번째 Radarr을 목록으로 사용하도록 구성](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)하는 것이 좋습니다. 이렇게하면 두 인스턴스를 동기화하여 유지할 수 있습니다.

- [Windows에서 다중 인스턴스](#windows-multi)
- [Linux에서 다중 인스턴스](#linux-multi)
- [Docker에서 다중 인스턴스](#docker-multi)
{.links-list}

다음 요구 사항을 유의해야 합니다.

- 비 도커의 경우 동일한 이진 파일(프로그램 파일)을 사용해야 합니다.
- 비 도커의 경우 모든 인스턴스에 `-data=` 또는 `/data=` 인수를 전달해야 합니다.
- 비 도커의 경우 다른 포트를 사용해야 합니다.
  - 도커의 경우 다른 외부 포트를 사용해야 합니다.
- 다른 다운로드 클라이언트 카테고리를 사용해야 합니다.
- 다른 루트 폴더를 사용해야 합니다.
- 비 도커의 경우 1개의 인스턴스를 제외한 모든 인스턴스에서 자동 업데이트를 비활성화해야 합니다.

## Windows에서 다중 인스턴스

{#windows-multi}

이 가이드에서는 Windows에서 하나의 기본 설치만 사용하여 Radarr의 여러 인스턴스를 실행하는 방법을 보여줍니다. 이 가이드는 Windows 10을 사용하여 작성되었으며, 이전 버전의 Windows(7, 8 등)을 사용하는 경우 일부 사항을 조정해야 할 수 있습니다. 이 가이드는 또한 Radarr을 기본 디렉토리에 설치하고 두 번째 Radarr 인스턴스를 Radarr-4K로 지칭할 것으로 가정합니다. 필요에 따라 설치를 맞추기 위해 변경할 수 있습니다.

> 참고: Radarr을 **서비스**로 실행하거나 [트레이 앱](#tray-app-windows)으로 실행해야 합니다. 앱과 서비스를 모두 실행하는 것은 불필요하며 문제가 발생할 수 있습니다.

### 서비스 (Windows)

#### 전제 조건 (서비스)

- [이미 Radarr이 설치되어 있어야 합니다](#windows)
- [NSSM (Non-Sucking Service Manager)](http://nssm.cc)이 설치되어 있어야 합니다. 설치하려면 최신 릴리스(작성 시점에서 2.24)를 다운로드하고 32비트 또는 64비트 nssm.exe 파일을 C:/windows/system32에 복사하십시오.
  - 32비트 또는 64비트 시스템인지 확실하지 않은 경우 설정 => 시스템 => 정보 => 시스템 유형을 확인하십시오.

#### Radarr 서비스 구성

1. 관리자 권한으로 명령 프롬프트 창을 엽니다. (관리자로 실행하려면 명령 프롬프트 아이콘을 마우스 오른쪽 단추로 클릭하고 "관리자로 실행"을 선택하십시오.)
1. Radarr이 실행 중인 경우 명령 프롬프트에서 `nssm stop Radarr`를 실행하여 서비스를 중지합니다.
1. 이제 기존의 Radarr 인스턴스를 명시적으로 데이터 디렉토리를 가리키도록 편집해야 합니다. 기본 명령은 다음과 같습니다.
   `sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe -data=C:\ProgramData\Radarr"`

이 명령은 원래의 Radarr 인스턴스가 데이터 디렉토리로 `C:\ProgramData\Radarr`를 명시적으로 사용하도록 지정합니다. Radarr 설치를 기본값으로 사용하지 않았거나 데이터 폴더가 다른 위치에 있는 경우 여기서 경로를 변경해야 할 수 있습니다.

#### Radarr-4K 서비스 생성

1. Radarr-4K가 위치할 새 폴더를 만듭니다. 대부분의 경우 `C:\ProgramData\Radarr-4K`와 같은 유사한 위치를 사용합니다.
1. 명령 프롬프트로 돌아가 `nssm install Radarr-4K`를 사용하여 새로운 Radarr-4K 서비스를 생성합니다. 팝업 창이 열리고 새 인스턴스에 대한 매개변수를 입력할 수 있습니다. 이 예제에서는 다음과 같이 사용합니다.
   - 경로: `C:\ProgramData\Radarr\bin\Radarr.exe`
   - 시작 디렉토리: `C:\ProgramData\Radarr\bin`
   - 인수: `-data=C:\ProgramData\Radarr-4K`
   - 종료 작업 탭
     - 다시 시작: 응용 프로그램 다시 시작
     - 지연: 120000 ms
       (2분, 업데이트가 제 시간에 완료되지 못하는 경우 더 길게 설정할 수 있음)

> **인수**는 1단계에서 생성한 *새* 폴더를 가리켜야 합니다. 이는 두 인스턴스의 모든 데이터 파일을 별도의 위치에 유지하기 때문에 중요합니다. {.is-warning}

1. *서비스 설치*를 클릭합니다. 창이 닫히고 서비스가 실행 가능한 상태가 됩니다.
1. [Radarr-4k 구성](#windows-multi-config-second)을 계속합니다.

### 트레이 앱 (Windows)

#### 전제 조건 (트레이 앱)

- [이미 Radarr이 설치되어 있어야 합니다](#windows)
- Radarr의 바로 가기에는 여러 인스턴스를 허용하기 위해 '대상' 필드에 `/data=` 인수가 구성되어 있어야 합니다.
- 현재 사용자의 시작 메뉴 폴더 `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`로 이동하여 필요한 경우 기존 바로 가기를 편집합니다.

#### Radarr-4K 트레이 앱 생성

- Radarr-4K의 구성 파일을 위한 새 폴더를 만듭니다. 대부분의 경우 `C:\ProgramData\Radarr-4K`와 같은 유사한 위치를 사용합니다.
- 마우스 오른쪽 단추로 클릭하고 새 바로 가기를 만듭니다.
- 경로: `C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- `Radarr-4K`와 같은 고유한 이름을 지정하고 마법사를 완료합니다.
- 새 바로 가기를 두 번 클릭하여 실행하고 테스트합니다.
- [Radarr-4k 구성](#windows-multi-config-second)을 계속합니다.

### Radarr-4k 구성 {#windows-multi-config-second}

- 서비스 방법 또는 트레이 앱을 사용한 경우에 관계없이 두 서비스와 두 앱을 모두 중지합니다.
- Radarr-4k(서비스 또는 트레이 앱)를 시작합니다.
- Radarr-4k를 열고 앱 내에서 [설정 => 일반 => 호스트](/radarr/settings/#host)로 이동합니다.
- `포트 번호`를 `7878`에서 다른 포트(예: `7879`)로 변경하여 Radarr과 Radarr4k가 충돌하지 않도록 합니다.
- 이제 두 앱을 모두 시작할 수 있어야 합니다.
- [업데이트 처리](#dealing-with-updates)를 계속합니다.

### 업데이트 처리

> - 인스턴스 중 하나에서 자동 업데이트를 비활성화합니다.
  - config.xml에서 업데이트 브랜치를 `<Branch>nonexistent</Branch>`로 변경합니다.
- 하나의 Radarr 인스턴스가 업데이트되면 두 인스턴스가 모두 종료되고 업데이트된 인스턴스만 다시 시작됩니다. 이 문제를 해결하려면 다른 인스턴스를 수동으로 시작해야 할 수도 있으며, 아래의 PowerShell 스크립트를 사용해 문제를 해결할 수도 있습니다.

> [NSSM 종료 작업](#creating-radarr-4k-service)을 올바르게 구성하면 Radarr을 업데이트하고 여러 인스턴스를 다시 시작할 수 있습니다.
재시작 지연이 기본적으로 구성되지 않은 경우 인스턴스가 즉시 다시 시작됩니다.
이로 인해 업데이트가 적용되지 않을 수 있으며 다음 오류가 발생할 수 있습니다. `Radarr was restarted prematurely by external process.` {.is-info}

#### Windows 포트 확인 및 다시 시작 PowerShell 스크립트

- 두 개의 Radarr 인스턴스를 사용하고 하나는 업데이트하는 경우 모든 인스턴스가 종료됩니다. 업데이트 중인 인스턴스만 다시 온라인으로 돌아옵니다.
- 아래의 PowerShell 스크립트는 예약된 작업으로 구성되어야 합니다.
- 포트를 확인하고 온라인이 아닌 경우 예약된 작업을 (다시) 시작하여 Radarr을 실행합니다.

1. 아래 코드로 RadarrInstancesChecker.ps1이라는 새 파일을 만듭니다.
1. 스크립트를 실제 서비스 이름, IP 및 포트로 편집합니다. *트레이 모드에서 실행 중인 경우 각 Radarr 인스턴스를 시작하는 예약된 작업을 만들고 스크립트에서 해당 작업 이름을 사용해야 합니다.*
1. [반복 일정](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler)에 스크립트를 반복적으로 실행할 예약된 작업을 만듭니다.

- 보안 옵션: `최고 권한으로 실행`
  - 그렇지 않으면 스크립트가 서비스를 조작할 수 없습니다.
- 트리거: `시작 시`
- 작업 반복: `5` 또는 `10`분
- 작업: `프로그램 시작`
- 프로그램/스크립트: `powershell`
- 인수: `-File D:\RadarrInstancesChecker.ps1`
  - 스크립트의 위치에 대한 전체 경로를 사용해야 합니다.

```powershell
################################################################################################
### RadarrInstancesChecker.ps1                                                               ###
################################################################################################
### Keeps multiple Radarr Instances up by checking the port                                  ###
### Please use Radarr´s Discord or Reddit for support!                                       ###
### https://wiki.servarr.com/radarr/installation#windows-multi                               ###
################################################################################################
### Version: 1.1                                                                             ###
### Updated: 2020-10-22                                                                      ###
### Author:  reloxx13                                                                        ###
################################################################################################



### SET YOUR CONFIGURATION HERE ###
# Set your host ip and port correctly and use your service or scheduledtask names!

# (string) The type how Radarr is starting
# "Service" (default) Service process is used
# "ScheduledTask" Task Scheduler is used
$startType = 'Service'

# (bool) Writes the log to C:\Users\YOURUSERNAME\log.txt when enabled
# $false (default)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # Instance 1
        Name = 'Radarr-V3'; # (string) Service or Task name (default: Radarr-V3)
        IP   = '192.168.178.12'; # (string) Server IP where Radarr runs (default: 192.168.178.12)
        Port = '7873'; # (string) Server Port where Radarr runs (default: 7873)
    }
    [pscustomobject]@{   # Instance 2
        Name = 'Radarr-4K'; # (string) Service or Task name (default: Radarr-4K)
        IP   = '192.168.178.12'; # (string) Server IP where Radarr runs (default: 192.168.178.12)
        Port = '7874'; # (string) Server Port where Radarr runs (default: 7874)
    }
    # If needed you can add more instances here... by uncommenting out the below lines
    # [pscustomobject]@{   # Instance 3
    # Name='Radarr-3D';    # (string) Service or Task name (default: Radarr-3D)
    # IP='192.168.178.12'; # (string) Server IP where Radarr runs (default: 192.168.178.12)
    # Port='7875';         # (string) Server Port where Radarr runs (default: 7875)
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

- [Swizzin 사용자](https://github.com/ComputerByte/radarr4k)
- Swizzin 사용자가 아닌 경우
  - 첫 번째 인스턴스에 `-data=` 인수가 전달되었는지 확인합니다.
  - 두 번째 인스턴스의 포트를 변경하려면 첫 번째 인스턴스를 일시적으로 중지합니다. `systemctl stop radarr`
  - Radarr 인스턴스 중 하나에서 자동 업데이트를 비활성화합니다.

> 아래는 Radarr4K 인스턴스를 만드는 예입니다. 아래의 systemd 생성 스크립트는 데이터 디렉토리를 `/var/lib/radarr4k/`로 사용합니다. 디렉토리가 존재하거나 필요한 경우 수정하십시오.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr4k.service > /dev/null
[Unit]
Description=Radarr4k Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr4k/
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

- Radarr4k 서비스를 활성화합니다:

```shell
sudo systemctl enable --now -q radarr4k
```

## 도커 다중 인스턴스

{#docker-multi}

- 위의 요구 사항을 충족하는 다른 이름을 가진 두 번째 도커 컨테이너를 시작합니다.