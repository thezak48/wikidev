# 多个实例

可以运行多个 Readarr 实例。这通常在希望拥有一本书的有声书和电子书副本时使用。
请注意，您可以配置 Readarr 使用第二个 Readarr 作为列表。如果您希望保持两者同步，这将非常有帮助。

- [Windows 多个实例](#windows-multi)
- [Linux 多个实例](#linux-multi)
- [MacOS 多个实例](#macos-multi)
- [Docker 多个实例](#docker-multi)
{.links-list}

应注意以下要求：

- 如果不使用 Docker，则应使用相同的二进制文件（程序文件）
- 如果不使用 Docker，则所有实例*必须*传递一个 `-data=` 或 `/data=` 参数
- 如果不使用 Docker，则必须使用不同的端口
  - 如果使用 Docker，则必须使用不同的外部端口
- 必须使用不同的下载客户端类别
- 必须使用不同的根文件夹。
- 如果不使用 Docker，则应在除 1 个实例之外的所有实例上禁用自动更新。

## Windows 多个实例

{#windows-multi}

本指南将向您展示如何在 Windows 上运行多个 Readarr 实例，只使用一个基本安装。本指南是在使用 Windows 10 时编写的；如果您使用的是较早版本的 Windows（7、8 等），您可能需要调整一些内容。本指南还假设您已将 Readarr 安装到默认目录，并且您的第二个 Readarr 实例将被称为 Readarr-audiobooks。根据您自己的安装情况，随意更改这些内容。

### 服务（Windows）

#### 先决条件（服务）

- [您必须已经安装了 Readarr](#windows)
- 您必须安装 [NSSM（Non-Sucking Service Manager）](http://nssm.cc)。要安装，请下载最新版本（写作时为 2.24）并将 32 位或 64 位的 nssm.exe 文件复制到 C:/windows/system32。
  - 如果您不确定自己的系统是 32 位还是 64 位，请检查 设置 => 系统 => 关于 => 系统类型。

#### 配置 Readarr 服务

1. 打开一个以管理员身份运行的命令提示符窗口。（要以管理员身份运行，请右键单击命令提示符图标，然后选择“以管理员身份运行”。）
1. 如果 Readarr 正在运行，请在命令提示符中运行 `nssm stop Readarr` 停止服务。
1. 现在，我们必须编辑现有的 Readarr 实例，以明确指定其数据目录。默认命令如下：
   `sc config Readarr binpath= "C:\ProgramData\Readarr\bin\Readarr.exe -data=C:\ProgramData\Readarr"`

此命令告诉原始的 Readarr 实例明确使用 `C:\ProgramData\Readarr` 作为其数据目录。如果您没有使用默认的 Readarr 安装，或者如果您的数据文件夹在其他位置，您可能需要在此处更改路径。

#### 创建 Readarr-audiobooks 服务

1. 创建一个新文件夹，用于存放 Readarr-audiobooks。大多数人使用类似的位置，例如 `C:\ProgramData\Readarr-audiobooks`
1. 回到命令提示符，使用 `nssm install Readarr-audiobooks` 创建新的 Readarr-audiobooks 服务。将打开一个弹出窗口，您可以在其中输入新实例的参数。对于此示例，我们将使用以下内容：
   - 路径：`C:\ProgramData\Readarr\bin\Readarr.exe`
   - 启动目录：`C:\ProgramData\Readarr\bin`
   - 参数：`-data=C:\ProgramData\Readarr-audiobooks`

> 请注意，**参数**指向步骤 1 中创建的*新*文件夹。这非常重要，因为它将所有数据文件从两个实例分别保存在不同的位置。{.is-warning}

1. 单击 *Install service*。窗口应关闭，服务现在可用于运行。
1. 继续 [配置 Readarr-audiobooks](#windows-multi-config-second)

### 托盘应用（Windows）

#### 先决条件（托盘应用）

- [您必须已经安装了 Readarr](#windows)
- Readarr 必须配置了 `/data=` 参数以允许多个实例
- 转到当前用户的启动文件夹 `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`，并根据需要编辑现有的快捷方式。

#### 创建 Readarr-audiobooks 托盘应用

- 右键单击并创建新的快捷方式
- 路径：`C:\ProgramData\Readarr\bin\Readarr.exe /data=C:\ProgramData\Readarr-audiobooks`
- 为快捷方式指定一个唯一的名称，例如 `Readarr-audiobooks`，然后完成向导。
- 双击新的快捷方式以运行和测试。
- 继续 [配置 Readarr-audiobooks](#windows-multi-config-second)

### 配置 Readarr-audiobooks {#windows-multi-config-second}

- 无论您是使用服务方法还是托盘应用：停止两个服务和两个应用程序
- 启动 Readarr-audiobooks（服务或托盘应用）
- 打开 Readarr-audiobooks 并在应用程序内导航到 [设置 => 通用 => 主机](/readarr/settings/#host)
- 将 `端口号` 从 `8787` 更改为其他端口，例如 `8879`，以避免 Readarr 和 Readarr-audiobooks 冲突
- 现在应该能够启动两个应用程序
- 继续 [处理更新](#dealing-with-updates)

### 处理更新

- 在其中一个实例中禁用自动更新
- 如果更新了一个 Readarr 实例，两个实例都将关闭，只有更新的实例将重新启动。要解决此问题，您将需要手动启动另一个实例，或者您可能需要查看下面的 PowerShell 脚本来解决问题。

#### Windows 端口检查器和重启 PowerShell 脚本

{#win-portchecker}

- 当您使用两个 Readarr 实例并且其中一个正在更新时，它将关闭所有实例。只有正在更新的实例将重新上线。
- 下面的 PowerShell 脚本应配置为计划任务。
- 它会检查端口，如果有一个端口不在线，它将（重新）启动计划任务以启动 Readarr。

1. 创建一个名为 ReadarrInstancesChecker.ps1 的新文件，并使用以下代码填充。
1. 使用您的实际服务名称、IP 和端口编辑脚本。
1. [创建计划任务](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler)，以按重复的计划运行脚本。

- 安全选项：启用 `以最高权限运行`
  - 否则，脚本将无法操作服务
- 触发器：`启动时`
- 重复任务：每 `5` 或 `10` 分钟
- 操作：`启动程序`
- 程序/脚本：`powershell`
- 参数：`-File D:\ReadarrInstancesChecker.ps1`
  - 确保使用脚本位置的完整路径

```powershell
################################################################################################
### ReadarrInstancesChecker.ps1                                                               ###
################################################################################################
### 通过检查端口来保持多个 Readarr 实例在线                                                    ###
### 请使用 Readarr 的 Discord 或 Reddit 寻求支持！                                              ###
### https://wiki.servarr.com/readarr/installation#windows-multi                               ###
################################################################################################
### 版本：1.1                                                                                 ###
### 更新日期：2020-10-22                                                                      ###
### 作者：reloxx13                                                                           ###
################################################################################################



### 在此处设置您的配置 ###
# 设置正确的主机 IP 和端口，并使用您的服务或计划任务名称！

# (string) Readarr 启动方式
# "Service"（默认）使用服务进程
# "ScheduledTask" 使用任务计划程序
$startType = 'Service'

# (bool) 启用时将日志写入 C:\Users\YOURUSERNAME\log.txt
# $false（默认）
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # 实例 1
        Name = 'Readarr'; # (string) 服务或任务名称（默认：Readarr）
        IP   = '192.168.178.12'; # (string) Readarr 运行的服务器 IP（默认：192.168.178.12）
        Port = '8873'; # (string) Readarr 运行的服务器端口（默认：8873）
    }
    [pscustomobject]@{   # 实例 2
        Name = 'Readarr-audiobooks'; # (string) 服务或任务名称（默认：Readarr-audiobooks）
        IP   = '192.168.178.12'; # (string) Readarr 运行的服务器 IP（默认：192.168.178.12）
        Port = '8874'; # (string) Readarr 运行的服务器端口（默认：8874）
    }
    # 如果需要，您可以在此处添加更多实例... 取消下面的注释
    # [pscustomobject]@{   # 实例 3
    # Name='Readarr-3D';    # (string) 服务或任务名称（默认：Readarr-3D）
    # IP='192.168.178.12'; # (string) Readarr 运行的服务器 IP（默认：192.168.178.12）
    # Port='8875';         # (string) Readarr 运行的服务器端口（默认：7875）
    # }
)


### 请勿更改以下任何内容 ###


###
# 此函数将写入日志文件或控制台输出
###
function Write-Log
{
    # 将写入 C:\Users\YOURUSERNAME\log.txt
    
    Param(
        $Message,
        $Path = "$env:USERPROFILE\log.txt" 
    )

    function TS { Get-Date -Format 'hh:mm:ss' }
    
    # 控制台输出
    Write-Output "[$(TS)]$Message"
    
    # 文件输出
    if ($logToFile)
    {
        "[$(TS)]$Message" | Tee-Object -FilePath $Path -Append | Write-Verbose
    }
}


Write-Log 'START ====================='


$instances | ForEach-Object {
    Write-Log "检查 $($_.Name) $($_.IP):$($_.Port)"
    
    $PortOpen = ( Test-NetConnection $_.IP -Port $_.Port -WarningAction SilentlyContinue ).TcpTestSucceeded 
    
    if (!$PortOpen)
    {
        Write-Log "端口 $($_.Port) 已关闭，重新启动 $($startType) $($_.Name)！"

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
        Write-Log "端口 $($_.Port) 已打开！"
    }
}

Write-Log 'END ====================='
```

## Linux 多个实例

{#linux-multi}

- [Swizzin 用户](https://github.com/ComputerByte/readarr-audiobooks)
- 非 Swizzin 用户
  - 确保第一个实例已传递 `-data=` 参数。
  - 暂时停止第一个实例，以便您可以更改第二个实例的端口 `systemctl stop readarr`
  - 在其中一个 Readarr 实例上禁用自动更新

> 下面是一个示例脚本，用于创建 Readarr-audiobooks 实例。下面的 systemd 创建脚本将使用 `/var/lib/readarr-audiobooks/` 作为数据目录。确保目录存在，或根据需要进行修改。{.is-danger}

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

- 重新加载 systemd：

```shell
sudo systemctl -q daemon-reload
```

- 启用 Readarr-audiobooks 服务：

```shell
sudo systemctl enable --now -q readarr-audiobooks
```

## MacOS 多个实例

{#macos-multi}

本指南是在 macOS 13（Ventura）上制作和测试的，但应适用于 Readarr 支持的任何版本。

### 先决条件
- 必须在 `/Applications` 文件夹中安装 Readarr 应用程序
- 如果之前已经使用过 Readarr，则所有数据将丢失。将 `~/.config/Readarr` 移动到 `~/.config/readarr-books` 或 `~/.config/readarr-audiobooks` 以保留数据。

### 创建应用程序（轻松启动 Readarr）
您将创建两个新应用程序：“Readarr Books”和“Readarr Audiobooks”。

- 打开 Automator 应用程序
- 选择 `新建文稿`，然后选择 `应用程序`
- 在左上角的搜索框中搜索 `运行 Shell 脚本`，然后双击它
- 在打开的框中，粘贴以下内容：

```shell
# Readarr Books
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-books
```



- 将应用程序保存为`Readarr Books`
- 在菜单栏中选择`文件` > `复制`
- 用以下内容替换脚本的内容：

```shell
# Readarr Audiobooks
open -F -n -a Readarr --args -data="$HOME"/.config/readarr-audiobooks
```

- 将新的应用程序保存为`Readarr Audiobooks`
- 在Finder中查看应用程序，可选择更改它们的图标（通过`获取信息`窗口）。

### 配置实例
现在，您将为每个实例设置端口和名称。

- 为每个实例选择一个端口号。例如，默认的电子书端口为`8787`，有声书端口为`8789`。
- 如果其中一个实例使用默认的端口号，请先启动另一个实例。否则，先启动其中任意一个实例。
- 在Readarr中，转到`设置` > `常规`，并设置正确的端口。

> 可选：切换到高级选项并将`实例名称`设置为您喜欢的名称。
{.is-success}

- 启动另一个实例并执行相同的操作。

### 更新
当您更新一个实例时，更新程序会关闭两个实例，并只重新启动您更新的那个实例。为了解决这个问题，将创建一个端口检查的周期性任务（从[Windows指南](#win-portchecker)中适应但稍作修改）。

- 在其中一个实例中禁用自动更新，并确保永远不要更新它。
- 在您记得的地方创建一个名为`readarrportchecker.zsh`的新文件。
- 添加以下内容：

```shell
#!/bin/zsh

# 第一个实例的*应用程序名称*
name0="Readarr Books"
# 第一个实例的端口号
port0=8787

# 第二个实例的*应用程序名称*
name1="Readarr Audiobooks"
# 第二个实例的端口号
port1=8789

# 日志记录
LOGFILE="$HOME/.local/state/readarr.log"
test -d "$HOME/.local/state" || mkdir -p "$HOME/.local/state"

function checkport {
    lsof -i ":${1}" &>/dev/null
}

# 一个实例正在运行意味着两个实例都应该运行
if checkport "${port0}" && ! checkport "${port1}"; then
		open -a "${name1}"
    echo "Opened ${name1}" >> "$LOGFILE"
elif checkport "${port1}" && ! checkport "${port0}"; then
		open -a "${name0}"
    echo "Opened ${name0}" >> "$LOGFILE"
fi
```

- 使脚本可执行：

```shell
chmod +x readarrportchecker.zsh
```

- 定期运行脚本。在`~/Library/LaunchAgents`中创建一个名为`local.readarr.portchecker.plist`的新文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>local.readarr.portchecker</string>
    <key>Program</key>
    <!-- 通过右键单击，然后按住Option键并复制来查找路径 -->
    <string>/path/to/readarrportchecker.zsh</string>
    <key>StartInterval</key>
    <!-- 周期性间隔，以秒为单位。五分钟为300，十分钟为600。 -->
    <integer>300</integer>
  </dict>
</plist>
```

- 根据注释修改文件
- 重新登录或手动加载文件：

```shell
launchctl load ~/Library/LaunchAgents/local.readarr.portchecker.plist
```

> `TODO`：可能将此集成到更新过程的自定义脚本中，或者观察文件更改而不是每300秒运行一次。
{.is-info}

## Docker多实例

{#docker-multi}

- 只需使用不同的名称启动第二个Docker容器，确保满足上述要求。