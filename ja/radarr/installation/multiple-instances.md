---
title: 複数のインスタンス
description: 
published: true
date: 2023-09-01T05:05:47.102Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:10.189Z
---

# 複数のインスタンス

Radarrの複数のインスタンスを実行することができます。これは、映画の4Kと1080pのコピーを保持したい場合などに通常行われます。ただし、[TRaSHのガイドを確認して、2番目のRadarrをリストとして使用するようにRadarrを設定する](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)ことができます。これは、両方を同期させたい場合に役立ちます。

- [Windowsの複数のインスタンス](#windows-multi)
- [Linuxの複数のインスタンス](#linux-multi)
- [Dockerの複数のインスタンス](#docker-multi)
{.links-list}

以下の要件に注意してください：

- Docker以外の場合、同じバイナリ（プログラムファイル）を使用する必要があります
- Docker以外の場合、すべてのインスタンスには`-data=`または`/data=`引数が渡される必要があります
- Docker以外の場合、異なるポートを使用する必要があります
  - Dockerの場合、異なる外部ポートを使用する必要があります
- 異なるダウンロードクライアントのカテゴリを使用する必要があります
- 異なるルートフォルダを使用する必要があります。
- Docker以外の場合、1つのインスタンス以外の自動更新を無効にする必要があります。

## Windowsの複数のインスタンス

{#windows-multi}

このガイドでは、WindowsでRadarrの複数のインスタンスを1つの基本インストールのみで実行する方法を示します。このガイドはWindows 10を使用して作成されました。Windowsの以前のバージョン（7、8など）を使用している場合は、いくつかの設定を調整する必要があるかもしれません。このガイドでは、Radarrをデフォルトのディレクトリにインストールし、2番目のRadarrの名前をRadarr-4Kとします。必要に応じて、自分のインストールに合わせて変更してください。

> 注意：Radarrを**サービス**として実行するか、[トレイアプリ](#tray-app-windows)として実行するかのいずれかで実行する必要があります。アプリとサービスの両方を実行することは不要であり、問題の原因となる可能性があります。

### サービス（Windows）

#### 前提条件（サービス）

- [すでにRadarrがインストールされている必要があります](#windows)
- [NSSM（Non-Sucking Service Manager）](http://nssm.cc)がインストールされている必要があります。インストールするには、最新のリリース（執筆時点では2.24）をダウンロードし、32ビットまたは64ビットのnssm.exeファイルをC:/windows/system32にコピーします。
  - 32ビットまたは64ビットのシステムかどうかがわからない場合は、設定=>システム=>情報=>システムの種類を確認してください。

#### Radarrサービスの設定

1. 管理者権限のあるコマンドプロンプトウィンドウを開きます（管理者として実行するには、コマンドプロンプトのアイコンを右クリックし、「管理者として実行する」を選択します）。
1. Radarrが実行中の場合は、コマンドプロンプトで`nssm stop Radarr`を実行してサービスを停止します。
1. これで、既存のRadarrインスタンスを明示的にデータディレクトリに指定するように編集する必要があります。デフォルトのコマンドは次のとおりです：`sc config Radarr binpath= "C:\ProgramData\Radarr\bin\Radarr.exe -data=C:\ProgramData\Radarr"`

このコマンドは、元のRadarrインスタンスがデータディレクトリとして`C:\ProgramData\Radarr`を明示的に使用するように指示します。デフォルトのRadarrインストールを使用しなかった場合や、データフォルダが他の場所にある場合は、ここでパスを変更する必要があります。

#### Radarr-4Kサービスの作成

1. Radarr-4Kを配置する新しいフォルダを作成します。多くの場合、`C:\ProgramData\Radarr-4K`などの類似の場所を使用します。
1. コマンドプロンプトに戻り、`nssm install Radarr-4K`を使用して新しいRadarr-4Kサービスを作成します。ポップアップウィンドウが開き、新しいインスタンスのパラメータを入力できます。この例では、次の設定を使用します：
      - パス：`C:\ProgramData\Radarr\bin\Radarr.exe`
      - 起動ディレクトリ：`C:\ProgramData\Radarr\bin`
      - 引数：`-data=C:\ProgramData\Radarr-4K`
      - 終了アクションタブ
        - 再起動：アプリケーションの再起動
        - 遅延：120000ミリ秒（2分、更新が時間内に完了しない場合はより長くすることができます）

> **引数**は、ステップ1で作成した*新しい*フォルダを指しています。これは重要です。これにより、両方のインスタンスのデータファイルが別々の場所に保持されます。{.is-warning}

1. *サービスをインストール*をクリックします。ウィンドウが閉じられ、サービスが実行可能になります。
1. [Radarr-4kの設定](#windows-multi-config-second)を続けます。

### トレイアプリ（Windows）

#### 前提条件（トレイアプリ）

- [すでにRadarrがインストールされている必要があります](#windows)
- Radarrのショートカットには、複数のインスタンスを許可するために'target'フィールドに`/data=`引数が設定されている必要があります
- 現在のユーザーのスタートアップフォルダ`%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`に移動し、必要に応じて既存のショートカットを編集します。

#### Radarr-4Kトレイアプリの作成

- Radarr-4Kの設定ファイルのための新しいフォルダを作成します。多くの場合、`C:\ProgramData\Radarr-4K`などの類似の場所を使用します。
- 右クリックして新しいショートカットを作成します
- パス：`C:\ProgramData\Radarr\bin\Radarr.exe /data=C:\ProgramData\Radarr-4K`
- `Radarr-4K`などの一意の名前をショートカットに付け、ウィザードを完了します。
- 新しいショートカットをダブルクリックして実行してテストします。
- [Radarr-4kの設定](#windows-multi-config-second)を続けます。

### Radarr-4kの設定 {#windows-multi-config-second}

- サービスメソッドまたはトレイアプリを使用したかに関係なく、両方のサービスとアプリを停止します
- Radarr-4k（サービスまたはトレイアプリ）を起動します
- Radarr-4kを開き、アプリ内で[設定 => 一般 => ホスト](/radarr/settings/#host)に移動します
- `ポート番号`を`7878`から異なるポート（例：`7879`）に変更して、RadarrとRadarr4kが競合しないようにします
- これで両方のアプリを起動できるはずです
- [更新の処理](#dealing-with-updates)を続けます

### 更新の処理

> - 1つのインスタンスで自動更新を無効にします
  - config.xmlで更新ブランチを`<Branch>nonexistent</Branch>`に変更します
- 1つのRadarrインスタンスが更新されると、両方のインスタンスがシャットダウンされ、更新されたインスタンスのみが再起動します。これを修正するには、他のインスタンスを手動で起動する必要があります。または、以下のPowerShellスクリプトを使用することも検討できます。

> [NSSM Exit Action](#creating-radarr-4k-service)を正しく設定すると、追加のスクリプトなしでRadarrを更新して複数のインスタンスを再起動できます。
再起動の遅延がデフォルトで設定されていない場合、インスタンスはすぐに再起動されます。
これにより、更新が適用されなくなり、次のエラーが発生する可能性があります「外部プロセスによってRadarrが早期に再起動されました」。{.is-info}

#### Windowsポートチェッカーと再起動のPowerShellスクリプト

- 2つのRadarrインスタンスを使用し、1つが更新されるとすべてのインスタンスが終了します。更新中のインスタンスのみがオンラインに戻ります。
- 以下のPowerShellスクリプトは、スケジュールされたタスクとして設定する必要があります。
- ポートをチェックし、オンラインでない場合は、Radarrを起動するためにスケジュールされたタスクを（再）開始します。

1. 以下のコードを使用して、RadarrInstancesChecker.ps1という新しいファイルを作成します。
1. スクリプトを実際のサービス名、IP、およびポートで編集します。*トレイモードで実行している場合は、各Radarrインスタンスを起動するためのスケジュールされたタスクを作成し、以下のスクリプトでそのタスク名を使用する必要があります。*
1. [スクリプトを定期的に実行するスケジュールされたタスク](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler)を作成します。

- セキュリティオプション：`最高の特権で実行する`を有効にする
  - そうしないと、スクリプトはサービスを操作できません
- トリガー：`起動時`
- タスクを繰り返す：`5`または`10`分ごと
- アクション：`プログラムの開始`
- プログラム/スクリプト：`powershell`
- 引数：`-File D:\RadarrInstancesChecker.ps1`
  - スクリプトの場所への完全なパスを使用してください

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

## Linuxの複数のインスタンス

{#linux-multi}

- [Swizzinユーザー](https://github.com/ComputerByte/radarr4k)
- Swizzin以外のユーザー
  - 最初のインスタンスに`-data=`引数が渡されていることを確認します。
  - 一時的に最初のインスタンスを停止して、2番目のインスタンスのポートを変更します `systemctl stop radarr`
  - Radarrインスタンスの自動更新を無効にします

> 以下は、Radarr4Kインスタンスを作成するための例のスクリプトです。以下のsystemd作成スクリプトは、データディレクトリを`/var/lib/radarr4k/`として使用します。ディレクトリが存在するか、必要に応じて変更してください。{.is-danger}

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

- systemdをリロードします：

```shell
sudo systemctl -q daemon-reload
```

- Radarr4kサービスを有効にします：

```shell
sudo systemctl enable --now -q radarr4k
```

## Dockerの複数のインスタンス

{#docker-multi}

- 上記の要件を満たすように、異なる名前で2番目のDockerコンテナを起動してください。