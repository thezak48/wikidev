# 複数のインスタンス

Readarrの複数のインスタンスを実行することができます。これは、同じ本のオーディオブックと電子書籍のコピーを持ちたい場合に通常行われます。
Readarrを2番目のReadarrとしてリストとして使用するように構成することもできます。これは、両方を同期させたい場合に役立ちます。

- [Windowsの複数のインスタンス](#windows-multi)
- [Linuxの複数のインスタンス](#linux-multi)
- [MacOSの複数のインスタンス](#macos-multi)
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

このガイドでは、Windowsで複数のReadarrインスタンスを1つの基本インストールだけで実行する方法を示します。このガイドはWindows 10を使用して作成されました。Windowsの以前のバージョン（7、8など）を使用している場合は、いくつかの設定を調整する必要があるかもしれません。このガイドでは、Readarrをデフォルトのディレクトリにインストールし、2番目のReadarrインスタンスをReadarr-audiobooksと呼ぶことを前提としています。ただし、自分のインストールに合わせて変更してください。

### サービス（Windows）

#### 前提条件（サービス）

- [すでにReadarrがインストールされている必要があります](#windows)
- [NSSM（Non-Sucking Service Manager）](http://nssm.cc)がインストールされている必要があります。インストールするには、最新のリリース（執筆時点でのバージョン2.24）をダウンロードし、32ビットまたは64ビットのnssm.exeファイルをC:/windows/system32にコピーします。
  - 32ビットまたは64ビットのシステムかどうかがわからない場合は、設定=>システム=>情報=>システムの種類を確認してください。

#### Readarrサービスの設定

1. 管理者権限のあるコマンドプロンプトウィンドウを開きます（管理者として実行するには、コマンドプロンプトのアイコンを右クリックし、「管理者として実行する」を選択します）。
1. Readarrが実行中の場合は、コマンドプロンプトで`nssm stop Readarr`を実行してサービスを停止します。
1. これで、既存のReadarrインスタンスを明示的にデータディレクトリにポイントするように編集する必要があります。デフォルトのコマンドは次のとおりです：`sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe -data=C:\ProgramData\Readarr"`

このコマンドは、元のReadarrインスタンスがデータディレクトリとして`C:\ProgramData\Readarr`を明示的に使用するように指示します。デフォルトのReadarrインストールを使用しなかった場合や、データフォルダが他の場所にある場合は、ここでパスを変更する必要があります。

#### Readarr-audiobooksサービスの作成

1. Readarr-audiobooksを配置する新しいフォルダを作成します。ほとんどの場合、`C:\ProgramData\Readarr-audiobooks`などの類似した場所を使用します。
1. コマンドプロンプトに戻り、次のコマンドを使用して新しいReadarr-audiobooksサービスを作成します：`nssm install Readarr-audiobooks`。ポップアップウィンドウが開き、新しいインスタンスのパラメータを入力できます。この例では、次のようにします：
   - パス：`C:\ProgramData\Readarr\bin\Readarr.exe`
   - 起動ディレクトリ：`C:\ProgramData\Readarr\bin`
   - 引数：`-data=C:\ProgramData\Readarr-audiobooks`

> **引数**は、ステップ1で作成した*新しい*フォルダを指しています。これは重要です。これにより、両方のインスタンスのデータファイルが別々の場所に保持されます。{.is-warning}

1. *サービスのインストール*をクリックします。ウィンドウが閉じられ、サービスが実行可能になります。
1. [Readarr-audiobooksの設定](#windows-multi-config-second)を続けます。

### トレイアプリ（Windows）

#### 前提条件（トレイアプリ）

- [すでにReadarrがインストールされている必要があります](#windows)
- Readarrは複数のインスタンスを許可するために`/data=`引数で構成する必要があります
- 現在のユーザーのスタートアップフォルダ`%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`に移動し、必要に応じて既存のショートカットを編集します。

#### Readarr-audiobooksトレイアプリの作成

- 右クリックして新しいショートカットを作成します
- パス：`C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-audiobooks`
- `Readarr-audiobooks`などの一意の名前を付けてウィザードを完了します。
- 新しいショートカットをダブルクリックして実行してテストします。
- [Readarr-audiobooksの設定](#windows-multi-config-second)を続けます。

### Readarr-audiobooksの設定 {#windows-multi-config-second}

- サービスメソッドまたはトレイアプリを使用したかどうかに関係なく、両方のサービスとアプリを停止します
- Readarr-audiobooks（サービスまたはトレイアプリ）を起動します
- Readarr-audiobooksを開き、アプリ内で[設定 => 一般 => ホスト](/readarr/settings/#host)に移動します
- `ポート番号`を`8787`から異なるポート（例：`8879`）に変更して、ReadarrとReadarr-audiobooksが競合しないようにします
- これで両方のアプリを起動できるはずです
- [更新の処理](#dealing-with-updates)を続けます

### 更新の処理

- 1つのインスタンスで自動更新を無効にします
- 1つのReadarrインスタンスが更新されると、両方のインスタンスがシャットダウンされ、更新されたインスタンスのみが再起動します。これを修正するには、他のインスタンスを手動で起動する必要があります。または、以下のPowerShellスクリプトを使用して問題を解決することもできます。

#### WindowsポートチェッカーとリスタートのPowerShellスクリプト

{#win-portchecker}

- 2つのReadarrインスタンスを使用し、1つのインスタンスが更新されると、すべてのインスタンスが終了します。更新中のインスタンスのみがオンラインに戻ります。
- 以下のPowerShellスクリプトは、スケジュールされたタスクとして構成する必要があります。
- ポートをチェックし、オンラインでない場合は、Readarrを起動するためにスケジュールされたタスクを（再）開始します。

1. 以下のコードで新しいファイルを作成し、ReadarrInstancesChecker.ps1という名前を付けます。
1. スクリプトを実際のサービス名、IP、およびポートで編集します。
1. [スケジュールされたタスクを作成](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler)して、スクリプトを繰り返し実行するようにします。

- セキュリティオプション：`最高の特権で実行`を有効にする
  - そうしないと、スクリプトはサービスを操作できません
- トリガー：`起動時`
- タスクを繰り返す：`5`または`10`分ごと
- アクション：`プログラムの開始`
- プログラム/スクリプト：`powershell`
- 引数：`-File D:\ReadarrInstancesChecker.ps1`
  - スクリプトの場所への完全なパスを使用してください

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### ポートをチェックして複数のReadarrインスタンスを起動し続けます                            ###
### サポートにはReadarrのDiscordまたはRedditをご利用ください！                                 ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### バージョン：1.1                                                                           ###
### 更新日：2020-10-22                                                                        ###
### 作者：reloxx13                                                                            ###
################################################################################################



### ここで設定を行います ###
# 適切なホストIPとポートを設定し、サービスまたはスケジュールされたタスク名を使用してください！

# (string) Readarrの起動方法
# "Service"（デフォルト）：サービスプロセスが使用されます
# "ScheduledTask"：タスクスケジューラが使用されます
$startType = 'Service'

# (bool) ログを有効にすると、ログはC:\Users\YOURUSERNAME\log.txtに書き込まれます
# $false（デフォルト）
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # インスタンス1
        Name = 'Readarr'; # (string) サービスまたはタスク名（デフォルト：Readarr）
        IP   = '192.168.178.12'; # (string) Readarrが実行されているサーバーのIP（デフォルト：192.168.178.12）
        Port = '8873'; # (string) Readarrが実行されているサーバーポート（デフォルト：8873）
    }
    [pscustomobject]@{   # インスタンス2
        Name = 'Readarr-audiobooks'; # (string) サービスまたはタスク名（デフォルト：Readarr-audiobooks）
        IP   = '192.168.178.12'; # (string) Readarrが実行されているサーバーのIP（デフォルト：192.168.178.12）
        Port = '8874'; # (string) Readarrが実行されているサーバーポート（デフォルト：8874）
    }
    # 必要に応じて、以下の行のコメントを解除して他のインスタンスを追加できます...
    # [pscustomobject]@{   # インスタンス3
    # Name='Readarr-3D';    # (string) サービスまたはタスク名（デフォルト：Readarr-3D）
    # IP='192.168.178.12'; # (string) Readarrが実行されているサーバーのIP（デフォルト：192.168.178.12）
    # Port='8875';         # (string) Readarrが実行されているサーバーポート（デフォルト：7875）
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
    
    #コンソール出力
    Write-Output "[$(TS)]$Message"
    
    #ファイル出力
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

- [Swizzinユーザー](https://github.com/ComputerByte/readarr-audiobooks)
- Swizzin以外のユーザー
  - 最初のインスタンスに`-data=`引数が渡されていることを確認します。
  - 2番目のインスタンスのポートを変更するために一時的に最初のインスタンスを停止します `systemctl stop readarr`
  - Readarrのインスタンスの自動更新を無効にします

> 以下は、Readarr-audiobooksインスタンスを作成するための例のスクリプトです。以下のsystemd作成スクリプトは、データディレクトリを`/var/lib/readarr-audiobooks/`として使用します。ディレクトリが存在するか、必要に応じて変更してください。{.is-danger}

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

- systemdをリロードします：

```shell
sudo systemctl -q daemon-reload
```

- Readarr-audiobooksサービスを有効にします：

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## MacOSの複数のインスタンス

{#macos-multi}

このガイドはmacOS 13（Ventura）で作成およびテストされましたが、Readarrがサポートするバージョンならどのバージョンでも動作するはずです。

### 前提条件
- Readarrアプリケーションが`/Applications`フォルダにインストールされている必要があります
- すでにReadarrを使用している場合、すべてのデータが失われます。`~/.config/Readarr`を`~/.config/readarr-books`または`~/.config/readarr-audiobooks`に移動してデータを保持してください。

### アプリケーションの作成（Readarrを簡単に起動する）
「Readarr Books」と「Readarr Audiobooks」という2つの新しいアプリケーションを作成します。

- Automatorアプリを開きます
- `新規ドキュメント`、`アプリケーション`を選択します
- 左上の検索ボックスを使用して`シェルスクリプトを実行`を検索し、ダブルクリックします
- 開くボックスに、次の内容を貼り付けます：

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- `Readarr Books`という名前でアプリケーションを保存します。
- メニューバーで`File` > `Duplicate`に移動します。
- スクリプトの内容を以下のように置き換えます：

```shell
# Readarr Audiobooks
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-audiobooks
```

- 新しいアプリケーションを`Readarr Audiobooks`として保存します。
- Finderでアプリケーションを表示し、必要に応じてアイコンを変更します（`Get Info`ウィンドウを使用）。

### インスタンスの設定
次に、各インスタンスのポートと名前を設定します。

- 各インスタンスにポート番号を割り当てます。例えば、e-booksのデフォルトポート番号は`8787`、audiobooksのデフォルトポート番号は`8789`です。
- インスタンスのうち1つがデフォルトのポート番号を使用している場合は、他のインスタンスを先に起動します。それ以外の場合は、どちらかのインスタンスを起動します。
- Readarrで`Settings` > `General`に移動し、正しいポートを設定します。

> オプション：詳細オプションを切り替えて、`Instance Name`を好みの名前に設定します。
{.is-success}

- 他のインスタンスを起動し、同じ設定を行います。

### アップデート
1つのインスタンスをアップデートすると、アップデータは両方をシャットダウンし、アップデートしたインスタンスのみを再起動します。これを回避するために、ポートチェッカーの定期タスクを作成します（[Windowsガイド](#win-portchecker)から適応させていくつか変更します）。

- 1つのインスタンスで自動アップデートを無効にし、決してアップデートしないようにします。
- 覚えておく場所に新しいファイルを作成し、`readarrportchecker.zsh`という名前を付けます。
- 以下の内容を追加します：

```shell
#!/bin/zsh

# First instance's *application name*
name0="Readarr Books"
# First instance's port number
port0=8787

# Second instance's *application name*
name1="Readarr Audiobooks"
# Second instance's port number
port1=8789

# Logging
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# One instance running means both should be
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Opened ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Opened ${name0}" >> "$LOGFILE"
fi
```

- スクリプトを実行可能にします：

```shell
chmod +x readarrportchecker.zsh
```

- スクリプトを定期的に実行するようにスケジュールします。`~/Library/LaunchAgents`に`local.readarr.portchecker.plist`という名前の新しいファイルを作成します：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- パスは右クリックして、Optionキーを押しながらコピーして取得します -->
    <string>/path/to/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- 定期的な間隔（秒単位）。5分の場合は300、10分の場合は600です。 -->
    <integer>300</integer>
  </dict>
</plist>
```

- コメントに従ってファイルを修正します
- 再ログインするか、次のコマンドを実行してファイルを手動でロードします：

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`: これをアップデートプロセスのカスタムスクリプトに統合するか、300秒ごとに実行する代わりにファイルの変更を監視するなど、カスタマイズする余地があります。
{.is-info}

## Dockerで複数のインスタンスを使用する

{#docker-multi}

- 上記の要件を満たすように、異なる名前で2番目のDockerコンテナを起動します。