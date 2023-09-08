# 다중 인스턴스

Readarr을 여러 개의 인스턴스로 실행할 수 있습니다. 이는 보통 한 책의 오디오북과 전자책 복사본을 원할 때 사용됩니다.
Readarr을 두 번째 Readarr로 목록으로 사용하도록 구성할 수도 있습니다. 이렇게 하면 두 인스턴스를 동기화하는 데 도움이 됩니다.

- [Windows에서 다중 인스턴스 실행](#windows-multi)
- [Linux에서 다중 인스턴스 실행](#linux-multi)
- [MacOS에서 다중 인스턴스 실행](#macos-multi)
- [Docker에서 다중 인스턴스 실행](#docker-multi)
{.links-list}

다음 요구 사항을 유의해야 합니다:

- Docker가 아닌 경우, 동일한 이진 파일(프로그램 파일)을 사용해야 합니다.
- Docker가 아닌 경우, 모든 인스턴스에 `-data=` 또는 `/data=` 인수를 전달해야 합니다.
- Docker가 아닌 경우, 서로 다른 포트를 사용해야 합니다.
  - Docker인 경우, 서로 다른 외부 포트를 사용해야 합니다.
- 서로 다른 다운로드 클라이언트 카테고리를 사용해야 합니다.
- 서로 다른 루트 폴더를 사용해야 합니다.
- Docker가 아닌 경우, 1개의 인스턴스를 제외한 모든 인스턴스에서 자동 업데이트를 비활성화해야 합니다.

## Windows에서 다중 인스턴스 실행

{#windows-multi}

이 가이드는 Windows에서 하나의 기본 설치만 사용하여 Readarr의 여러 인스턴스를 실행하는 방법을 보여줍니다. 이 가이드는 Windows 10을 사용하여 작성되었으며, 이전 버전의 Windows(7, 8 등)을 사용하는 경우 일부 사항을 조정해야 할 수 있습니다. 이 가이드는 또한 Readarr을 기본 디렉토리에 설치하고 두 번째 Readarr 인스턴스를 Readarr-audiobooks라고 가정합니다. 필요에 따라 설치를 변경할 수 있습니다.

### 서비스 (Windows)

#### 전제 조건 (서비스)

- [이미 Readarr이 설치되어 있어야 합니다](#windows)
- [NSSM (Non-Sucking Service Manager)](http://nssm.cc)이 설치되어 있어야 합니다. 설치하려면 최신 릴리스(글 작성 시점의 버전은 2.24)를 다운로드하고 32비트 또는 64비트 nssm.exe 파일을 C:/windows/system32에 복사하면 됩니다.
  - 32비트 또는 64비트 시스템인지 확실하지 않은 경우 설정 => 시스템 => 정보 => 시스템 유형을 확인하세요.

#### Readarr 서비스 구성

1. 관리자 권한으로 명령 프롬프트 창을 엽니다. (관리자로 실행하려면 명령 프롬프트 아이콘을 마우스 오른쪽 버튼으로 클릭하고 "관리자로 실행"을 선택합니다.)
1. Readarr이 실행 중인 경우 명령 프롬프트에서 `nssm stop Readarr`를 실행하여 서비스를 중지합니다.
1. 이제 기존 Readarr 인스턴스를 명시적으로 데이터 디렉토리를 가리키도록 수정해야 합니다. 기본 명령은 다음과 같습니다:
   `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe -data=C:\ProgramData\Readarr"`

이 명령은 원래의 Readarr 인스턴스가 데이터 디렉토리로 `C:\ProgramData\Readarr`를 명시적으로 사용하도록 지정합니다. Readarr 설치를 기본값으로 사용하지 않았거나 데이터 폴더가 다른 위치에 있는 경우 여기서 경로를 변경해야 할 수 있습니다.

#### Readarr-audiobooks 서비스 생성

1. Readarr-audiobooks를 배치할 새 폴더를 만듭니다. 대부분 `C:\ProgramData\Readarr-audiobooks`와 같은 유사한 위치를 사용합니다.
1. 명령 프롬프트로 돌아가서 `nssm install Readarr-audiobooks`를 사용하여 새 Readarr-audiobooks 서비스를 생성합니다. 팝업 창이 열리고 새 인스턴스에 대한 매개변수를 입력할 수 있습니다. 이 예제에서는 다음과 같이 사용합니다:
   - 경로: `C:\ProgramData\Readarr\bin\Readarr.exe`
   - 시작 디렉토리: `C:\ProgramData\Readarr\bin`
   - 인수: `-data=C:\ProgramData\Readarr-audiobooks`

> **인수**는 1단계에서 생성한 *새* 폴더를 가리킵니다. 이는 두 인스턴스의 모든 데이터 파일을 별도의 위치에 유지하는 데 필수적입니다. {.is-warning}

1. *서비스 설치*를 클릭합니다. 창이 닫히고 서비스가 실행 가능한 상태가 됩니다.
1. [Readarr-audiobooks 구성](#windows-multi-config-second)을 계속합니다.

### 트레이 앱 (Windows)

#### 전제 조건 (트레이 앱)

- [이미 Readarr이 설치되어 있어야 합니다](#windows)
- Readarr은 여러 인스턴스를 허용하도록 `/data=` 인수로 구성되어 있어야 합니다.
- 현재 사용자의 시작 폴더 `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`로 이동하고 필요한 경우 기존 바로 가기를 편집합니다.

#### Readarr-audiobooks 트레이 앱 생성

- 마우스 오른쪽 버튼을 클릭하고 새 바로 가기를 만듭니다.
- 경로: `C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-audiobooks`
- `Readarr-audiobooks`와 같이 고유한 이름을 지정하고 마법사를 완료합니다.
- 새 바로 가기를 두 번 클릭하여 실행하고 테스트합니다.
- [Readarr-audiobooks 구성](#windows-multi-config-second)을 계속합니다.

### Readarr-audiobooks 구성 {#windows-multi-config-second}

- 서비스 방법 또는 트레이 앱을 사용했는지 여부에 관계없이 두 서비스와 두 앱을 모두 중지합니다.
- Readarr-audiobooks를 시작합니다(서비스 또는 트레이 앱).
- Readarr-audiobooks를 열고 앱 내에서 [설정 => 일반 => 호스트](/readarr/settings/#host)로 이동합니다.
- `포트 번호`를 `8787`에서 다른 포트(예: `8879`)로 변경하여 Readarr과 Readarr-audiobooks가 충돌하지 않도록 합니다.
- 이제 두 앱을 모두 시작할 수 있어야 합니다.
- [업데이트 처리](#dealing-with-updates)를 계속합니다.

### 업데이트 처리

- 인스턴스 중 하나에서 자동 업데이트를 비활성화합니다.
- Readarr 인스턴스 중 하나가 업데이트되면 두 인스턴스가 모두 종료되고 업데이트된 인스턴스만 다시 시작됩니다. 이 문제를 해결하려면 다른 인스턴스를 수동으로 시작해야 할 수도 있으며, 아래의 PowerShell 스크립트를 사용해 문제를 해결할 수도 있습니다.

#### Windows 포트 확인 및 재시작 PowerShell 스크립트

{#win-portchecker}

- 두 개의 Readarr 인스턴스를 사용하고 하나가 업데이트되면 모든 인스턴스가 종료됩니다. 업데이트 중인 인스턴스만 다시 온라인 상태가 됩니다.
- 아래의 PowerShell 스크립트는 예약된 작업으로 구성되어야 합니다.
- 포트를 확인하고 온라인 상태가 아닌 경우 Readarr을 시작하는 예약된 작업을 다시 시작합니다.

1. 아래 코드로 ReadarrInstancesChecker.ps1이라는 새 파일을 만듭니다.
1. 스크립트를 실제 서비스 이름, IP 및 포트로 편집합니다.
1. [예약된 작업을 만들어](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler) 스크립트를 반복적으로 실행하도록 설정합니다.

- 보안 옵션: `최고 권한으로 실행` 활성화
  - 그렇지 않으면 스크립트가 서비스를 조작할 수 없습니다.
- 트리거: `시작 시`
- 작업을 반복: `5` 또는 `10`분
- 작업: `프로그램 시작`
- 프로그램/스크립트: `powershell`
- 인수: `-File D:\ReadarrInstancesChecker.ps1`
  - 스크립트의 위치에 대한 전체 경로를 사용해야 합니다.

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### 포트를 확인하여 여러 Readarr 인스턴스를 유지합니다.                                  ###
### 지원을 받으려면 Readarr의 Discord 또는 Reddit를 사용하세요!                           ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### 버전: 1.1                                                                             ###
### 업데이트 날짜: 2020-10-22                                                                      ###
### 작성자:  reloxx13                                                                        ###
################################################################################################



### 여기에 구성을 설정하세요 ###
# 올바른 서비스 또는 예약된 작업 이름을 사용하여 호스트 IP 및 포트를 설정하세요!

# (문자열) Readarr을 시작하는 방법
# "Service" (기본값) 서비스 프로세스를 사용합니다.
# "ScheduledTask" 작업 스케줄러를 사용합니다.
$startType = 'Service'

# (부울) 로그를 C:\Users\YOURUSERNAME\log.txt에 기록합니다.
# $false (기본값)
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # 인스턴스 1
        Name = 'Readarr'; # (문자열) 서비스 또는 작업 이름 (기본값: Readarr)
        IP   = '192.168.178.12'; # (문자열) Readarr이 실행되는 서버 IP (기본값: 192.168.178.12)
        Port = '8873'; # (문자열) Readarr이 실행되는 서버 포트 (기본값: 8873)
    }
    [pscustomobject]@{   # 인스턴스 2
        Name = 'Readarr-audiobooks'; # (문자열) 서비스 또는 작업 이름 (기본값: Readarr-audiobooks)
        IP   = '192.168.178.12'; # (문자열) Readarr이 실행되는 서버 IP (기본값: 192.168.178.12)
        Port = '8874'; # (문자열) Readarr이 실행되는 서버 포트 (기본값: 8874)
    }
    # 필요한 경우 여기에 더 많은 인스턴스를 추가할 수 있습니다... 아래 줄의 주석을 제거하면 됩니다.
    # [pscustomobject]@{   # 인스턴스 3
    # Name='Readarr-3D';    # (문자열) 서비스 또는 작업 이름 (기본값: Readarr-3D)
    # IP='192.168.178.12'; # (문자열) Readarr이 실행되는 서버 IP (기본값: 192.168.178.12)
    # Port='8875';         # (문자열) Readarr이 실행되는 서버 포트 (기본값: 7875)
    # }
)


### 이 아래로는 아무것도 변경하지 마세요 ###


###
# 이 함수는 로그 파일이나 콘솔 출력에 기록합니다.
###
function Write-Log
{
    # C:\Users\YOURUSERNAME\log.txt에 기록됩니다.
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # 콘솔 출력
    Write-Output "[$(TS)]$Message"
    
    # 파일 출력
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

## Linux에서 다중 인스턴스 실행

{#linux-multi}

- [Swizzin 사용자](https://github.com/ComputerByte/readarr-audiobooks)
- Swizzin 사용자가 아닌 경우
  - 첫 번째 인스턴스에 `-data=` 인수가 전달되었는지 확인합니다.
  - 두 번째 인스턴스의 포트를 변경하려면 첫 번째 인스턴스를 일시적으로 중지합니다. `systemctl stop readarr`
  - Readarr 인스턴스 중 하나에서 자동 업데이트를 비활성화합니다.

> 아래는 Readarr-audiobooks 인스턴스를 생성하는 예제 스크립트입니다. 아래의 systemd 생성 스크립트는 데이터 디렉토리로 `/var/lib/readarr-audiobooks/`를 사용합니다. 디렉토리가 존재하는지 확인하거나 필요에 따라 수정하세요.{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr-audiobooks.service > /dev/null
[Unit]
Description=Readarr-audiobooks Daemon
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/Readarr-audiobooks/
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

- Readarr-audiobooks 서비스 활성화:

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## MacOS에서 다중 인스턴스 실행

{#macos-multi}

이 가이드는 macOS 13 (Ventura)에서 작성 및 테스트되었지만 Readarr이 지원하는 모든 버전에서 작동할 것입니다.

### 전제 조건
- Readarr 애플리케이션이 `/Applications` 폴더에 설치되어 있어야 합니다.
- Readarr을 이미 사용한 경우 모든 데이터가 손실됩니다. `~/.config/Readarr`를 `~/.config/readarr-books`로 이동하거나 `~/.config/readarr-audiobooks`로 이동하여 데이터를 유지하세요.

### 애플리케이션 생성 (Readarr 쉽게 시작)
"Readarr Books"와 "Readarr Audiobooks"라는 두 개의 새 애플리케이션을 생성합니다.

- Automator 앱을 엽니다.
- `새 문서`를 선택한 다음 `애플리케이션`을 선택합니다.
- 왼쪽 상단의 검색 상자를 사용하여 `Run Shell Script`를 찾고 두 번 클릭합니다.
- 열리는 상자에 다음 내용을 붙여넣습니다:

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- `Readarr Books`로 애플리케이션을 저장합니다.
- 메뉴 바에서 `File` > `Duplicate`로 이동합니다.
- 스크립트의 내용을 다음과 같이 바꿉니다:

```shell
# Readarr Audiobooks
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-audiobooks
```

- 새로운 애플리케이션을 `Readarr Audiobooks`로 저장합니다.
- Finder에서 애플리케이션을 확인하고, 원하는대로 아이콘을 변경할 수 있습니다 (`Get Info` 창을 통해).

### 인스턴스 구성
이제 각 인스턴스의 포트와 이름을 설정합니다.

- 각 인스턴스에 대해 포트 번호를 선택합니다. 예를 들어, 이북은 기본 `8787`이고 오디오북은 `8789`입니다.
- 인스턴스 중 하나가 기본 포트 번호를 사용하는 경우, 다른 인스턴스를 먼저 실행합니다. 그렇지 않으면 둘 중 아무거나 먼저 실행합니다.
- Readarr에서 `Settings` > `General`로 이동하고 올바른 포트를 설정합니다.

> 선택 사항: 고급 옵션을 전환하고 `Instance Name`을 원하는대로 설정합니다.
{.is-success}

- 다른 인스턴스를 실행하고 동일한 작업을 수행합니다.

### 업데이트
한 인스턴스를 업데이트하면 업데이터가 두 인스턴스를 모두 종료하고 업데이트한 인스턴스만 다시 시작합니다. 이를 해결하기 위해 포트 체커 주기적인 작업을 생성합니다 (Windows 가이드에서 적용하되 약간 변경).

- 인스턴스 중 하나에서 자동 업데이트를 비활성화하고, 절대로 업데이트하지 않도록 합니다.
- 기억하기 쉬운 장소에 `readarrportchecker.zsh`라는 새 파일을 만들고 다음 내용을 추가합니다:

```shell
#!/bin/zsh

# 첫 번째 인스턴스의 *애플리케이션 이름*
name0="Readarr Books"
# 첫 번째 인스턴스의 포트 번호
port0=8787

# 두 번째 인스턴스의 *애플리케이션 이름*
name1="Readarr Audiobooks"
# 두 번째 인스턴스의 포트 번호
port1=8789

# 로깅
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# 한 인스턴스가 실행 중인 경우 두 인스턴스 모두 실행
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Opened ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Opened ${name0}" >> "$LOGFILE"
fi
```

- 스크립트를 실행 가능하도록 설정합니다:

```shell
chmod +x readarrportchecker.zsh
```

- 스크립트를 주기적으로 실행하도록 예약합니다. `~/Library/LaunchAgents`에 `local.readarr.portchecker.plist`라는 새 파일을 만듭니다:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- 마우스 오른쪽 버튼을 클릭한 다음, Option을 누르고 복사하여 경로를 찾습니다 -->
    <string>/path/to/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- 주기적인 간격(초). 300은 5분, 600은 10분입니다. -->
    <integer>300</integer>
  </dict>
</plist>
```

- 주석에 따라 파일을 수정합니다.
- 로그인을 다시 하거나 파일을 수동으로 로드합니다:

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`: 업데이트 프로세스를 위해 이것을 사용자 정의 스크립트에 통합하거나 300초마다 실행하는 대신 파일 변경을 관찰합니다.
{.is-info}

## Docker 다중 인스턴스

{#docker-multi}

- 위의 요구 사항을 충족하는 다른 이름으로 두 번째 Docker 컨테이너를 생성합니다.