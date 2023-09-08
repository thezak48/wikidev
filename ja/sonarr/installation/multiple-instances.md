---
title: 複数のインスタンス
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# 複数のインスタンス

Sonarrの複数のインスタンスを実行することができます。これは、シリーズの4Kコピーと1080pコピーの両方を取得したい場合に通常行われます。
[注意：Sonarrをリストとして使用するために、2番目のSonarrを構成することもできます。これは、両方を同期させたい場合に便利です。](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

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
- Docker以外の場合、1つのインスタンスを除いて自動更新を無効にする必要があります。

## Windowsの複数のインスタンス

{#windows-multi}

このガイドでは、Windowsで複数のSonarrインスタンスを1つの基本インストールだけで実行する方法を示します。このガイドはWindows 10を使用して作成されました。Windowsの以前のバージョン（7、8など）を使用している場合は、いくつかの設定を調整する必要があるかもしれません。このガイドでは、Sonarrをデフォルトのディレクトリにインストールし、2番目のSonarrインスタンスをSonarr-4Kと呼ぶことを前提としています。自分のインストールに合わせて変更してください。

### サービス（Windows）

#### 前提条件（サービス）

- [Sonarrがすでにインストールされている必要があります](#windows)
- [NSSM（Non-Sucking Service Manager）](http://nssm.cc)がインストールされている必要があります。インストールするには、最新のリリース（執筆時点では2.24）をダウンロードし、32ビットまたは64ビットのnssm.exeファイルをC:/windows/system32にコピーします。
  - 32ビットまたは64ビットのシステムかどうかがわからない場合は、設定 => システム => 情報 => システムの種類を確認してください。

#### Sonarrサービスの設定

1. 管理者権限のあるコマンドプロンプトウィンドウを開きます（管理者として実行するには、コマンドプロンプトのアイコンを右クリックし、「管理者として実行する」を選択します）。
1. Sonarrが実行中の場合は、コマンドプロンプトで`nssm stop Sonarr`を実行してサービスを停止します。
1. これで、既存のSonarrインスタンスを明示的にデータディレクトリに指定するように編集する必要があります。デフォルトのコマンドは次のとおりです：`sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe -data=C:\ProgramData\Sonarr"`

このコマンドは、元のSonarrインスタンスがデータディレクトリとして`C:\ProgramData\Sonarr`を明示的に使用するように指示します。デフォルトのSonarrインストールを使用しなかった場合や、データフォルダが他の場所にある場合は、ここでパスを変更する必要があります。

#### Sonarr-4Kサービスの作成

1. Sonarr-4Kを配置する新しいフォルダを作成します。多くの場合、`C:\ProgramData\Sonarr-4K`などの類似した場所を使用します。
1. コマンドプロンプトに戻り、`nssm install Sonarr-4K`を使用して新しいSonarr-4Kサービスを作成します。ポップアップウィンドウが開き、新しいインスタンスのパラメータを入力できます。この例では、次の設定を使用します：
      - パス：`C:\ProgramData\Sonarr\bin\Sonarr.exe`
      - 起動ディレクトリ：`C:\ProgramData\Sonarr\bin`
      - 引数：`-data=C:\ProgramData\Sonarr-4K`

> **引数**は、ステップ1で作成した*新しい*フォルダを指しています。これは重要です。これにより、両方のインスタンスのデータファイルが別々の場所に保持されます。{.is-warning}

1. *サービスのインストール*をクリックします。ウィンドウが閉じられ、サービスが実行可能になります。
1. [Sonarr-4kの設定](#windows-multi-config-second)を続けます。

### トレイアプリ（Windows）

#### 前提条件（トレイアプリ）

- [Sonarrがすでにインストールされている必要があります](#windows)
- Sonarrは複数のインスタンスを許可するために`/data=`引数で構成されている必要があります
- 現在のユーザーのスタートアップフォルダ`%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`に移動し、必要に応じて既存のショートカットを編集します。

#### Sonarr-4Kトレイアプリの作成

- 右クリックして新しいショートカットを作成します
- パス：`C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- `Sonarr-4K`などの一意の名前を付けてウィザードを完了します。
- 新しいショートカットをダブルクリックして実行してテストします。
- [Sonarr-4kの設定](#windows-multi-config-second)を続けます。

### Sonarr-4kの設定 {#windows-multi-config-second}

- サービスメソッドまたはトレイアプリを使用したかに関係なく、両方のサービスとアプリを停止します
- Sonarr-4k（サービスまたはトレイアプリ）を起動します
- Sonarr-4kを開き、アプリ内で[設定 => 一般 => ホスト](/sonarr/settings/#host)に移動します
- `ポート番号`を`8989`から異なるポート（例：`7879`）に変更して、SonarrとSonarr4kが競合しないようにします
- これで両方のアプリを起動できるはずです
- [更新の処理](#dealing-with-updates)を続けます

### 更新の処理

- 1つのインスタンスで自動更新を無効にします
- 1つのSonarrインスタンスが更新されると、両方のインスタンスがシャットダウンされ、更新されたインスタンスのみが再起動します。これを修正するには、他のインスタンスを手動で起動する必要があります。または、以下のPowerShellスクリプトを使用することも検討できます。

#### Windowsポートチェッカーと再起動のPowerShellスクリプト

- 2つのSonarrインスタンスを使用し、1つのインスタンスが更新されると、すべてのインスタンスが終了します。更新中のインスタンスのみがオンラインに戻ります。
- 以下のPowerShellスクリプトは、スケジュールされたタスクとして構成する必要があります。
- ポートをチェックし、オンラインでない場合はSonarrを起動するスケジュールされたタスクを（再）開始します。

1. 以下のコードでSonarrInstancesChecker.ps1という新しいファイルを作成します。
1. スクリプトを実際のサービス名、IP、およびポートで編集します。
1. [スクリプトを繰り返しスケジュールで実行するためのスケジュールされたタスク](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler)を作成します。

- セキュリティオプション：`最高の特権で実行`を有効にする
  - そうしないと、スクリプトはサービスを操作できません
- トリガー：`起動時`
- タスクを繰り返す：`5`または`10`分ごと
- アクション：`プログラムの開始`
- プログラム/スクリプト：`powershell`
- 引数：`-File D:\SonarrInstancesChecker.ps1`
  - スクリプトの場所への完全なパスを使用してください

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### 複数のSonarrインスタンスを監視し、ポートがオンラインでない場合は再起動します          ###
### サポートにはSonarrのDiscordまたはRedditをご利用ください！                                ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### バージョン：1.1                                                                           ###
### 更新日：2020-10-22                                                                        ###
### 作者：reloxx13                                                                            ###
################################################################################################



### ここで設定を行います ###
# 適切なホストIPとポートを設定し、サービスまたはスケジュールされたタスクの名前を使用してください！

# (string) Sonarrの起動方法
# "Service"（デフォルト） サービスプロセスが使用されます
# "ScheduledTask" タスクスケジューラが使用されます
$startType = 'Service'

# (bool) ログをC:\Users\YOURUSERNAME\log.txtに書き込む場合はtrueに設定します
# $false（デフォルト）
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # インスタンス1
        Name = 'Sonarr-V3'; # (string) サービスまたはタスクの名前（デフォルト：Sonarr-V3）
        IP   = '192.168.178.12'; # (string) Sonarrが実行されているサーバーのIP（デフォルト：192.168.178.12）
        Port = '7873'; # (string) Sonarrが実行されているサーバーポート（デフォルト：7873）
    }
    [pscustomobject]@{   # インスタンス2
        Name = 'Sonarr-4K'; # (string) サービスまたはタスクの名前（デフォルト：Sonarr-4K）
        IP   = '192.168.178.12'; # (string) Sonarrが実行されているサーバーのIP（デフォルト：192.168.178.12）
        Port = '7874'; # (string) Sonarrが実行されているサーバーポート（デフォルト：7874）
    }
    # 必要に応じて以下の行のコメントを解除して、さらにインスタンスを追加できます
    # [pscustomobject]@{   # インスタンス3
    # Name='Sonarr-3D';    # (string) サービスまたはタスクの名前（デフォルト：Sonarr-3D）
    # IP='192.168.178.12'; # (string) Sonarrが実行されているサーバーのIP（デフォルト：192.168.178.12）
    # Port='7875';         # (string) Sonarrが実行されているサーバーポート（デフォルト：7875）
    # }
)


### 以下の行を変更しないでください ###


###
# この関数はログファイルまたはコンソール出力に書き込みます
###
function Write-Log
{
    # C:\Users\YOURUSERNAME\log.txtに書き込みます
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # コンソール出力
    Write-Output "[$(TS)]$Message"
    
    # ファイル出力
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

- [Swizzinユーザー](https://github.com/ComputerByte/sonarr4k)
- Swizzin以外のユーザー
  - 最初のインスタンスに`-data=`引数が渡されていることを確認します。
  - 一時的に最初のインスタンスを停止して、2番目のインスタンスのポートを変更します `systemctl stop sonarr`
  - Sonarrのインスタンスの1つで自動更新を無効にします

> 以下はSonarr4Kインスタンスを作成するための例のスクリプトです。以下のsystemd作成スクリプトは、データディレクトリとして`/var/lib/sonarr4k/`を使用します。ディレクトリが存在するか、必要に応じて変更してください。{.is-danger}

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

- systemdをリロードします：

```shell
sudo systemctl -q daemon-reload
```

- Sonarr4kサービスを有効にします：

```shell
sudo systemctl enable --now -q sonarr4k
```

## Dockerの複数のインスタンス

{#docker-multi}

- 上記の要件が満たされていることを確認し、異なる名前の2番目のDockerコンテナを起動します。