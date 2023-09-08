---
title: 多实例
description: 
published: true
date: 2023-08-20T02:23:13.676Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:35.847Z
---

# 多实例

可以运行多个 Sonarr 实例。这通常在用户想要一个系列的 4K 和 1080p 副本时使用。
[请注意，您可以配置 Sonarr 使用第二个 Sonarr 作为列表。这对于希望保持两者同步非常有帮助。](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)

- [Windows 多实例](#windows-multi)
- [Linux 多实例](#linux-multi)
- [Docker 多实例](#docker-multi)
{.links-list}

应注意以下要求：

- 如果不是使用 Docker，应使用相同的二进制文件（程序文件）
- 如果不是使用 Docker，所有实例*必须*传递一个 `-data=` 或 `/data=` 参数
- 如果不是使用 Docker，必须使用不同的端口
  - 如果使用 Docker，则必须使用不同的外部端口
- 必须使用不同的下载客户端类别
- 必须使用不同的根文件夹
- 如果不是使用 Docker，在除 1 个实例外，禁用自动更新。

## Windows 多实例

{#windows-multi}

本指南将向您展示如何在 Windows 上使用一个基本安装运行多个 Sonarr 实例。本指南是在 Windows 10 上编写的；如果您使用的是以前的 Windows 版本（7、8 等），您可能需要进行一些调整。本指南还假设您已将 Sonarr 安装到默认目录，并且您的第二个 Sonarr 实例将被称为 Sonarr-4K。请随意更改以适应您自己的安装。

### 服务（Windows）

#### 先决条件（服务）

- [您必须已经安装了 Sonarr](#windows)
- 您必须安装 [NSSM（Non-Sucking Service Manager）](http://nssm.cc)。要安装，请下载最新版本（写作时为 2.24）并将 32 位或 64 位的 nssm.exe 文件复制到 C:/windows/system32。
  - 如果您不确定自己的系统是 32 位还是 64 位，请检查 设置 => 系统 => 关于 => 系统类型。

#### 配置 Sonarr 服务

1. 打开以管理员身份运行的命令提示符窗口。（要以管理员身份运行，请右键单击命令提示符图标，然后选择“以管理员身份运行”。）
1. 如果 Sonarr 正在运行，请在命令提示符中运行 `nssm stop Sonarr` 停止服务。
1. 现在，我们必须编辑现有的 Sonarr 实例，以明确指定其数据目录。默认命令如下：
   `sc config Sonarr binpath= "C:\ProgramData\Sonarr\bin\Sonarr.exe -data=C:\ProgramData\Sonarr"`

此命令告诉 Sonarr 的原始实例明确使用 `C:\ProgramData\Sonarr` 作为其数据目录。如果您没有使用默认的 Sonarr 安装，或者如果您的数据文件夹在其他位置，您可能需要在此处更改路径。

#### 创建 Sonarr-4K 服务

1. 创建一个新文件夹，用于存放 Sonarr-4K。大多数人使用类似的位置，例如 `C:\ProgramData\Sonarr-4K`。
1. 回到命令提示符，使用 `nssm install Sonarr-4K` 创建新的 Sonarr-4K 服务。将打开一个弹出窗口，您可以在其中输入新实例的参数。对于此示例，我们将使用以下内容：
   - 路径：`C:\ProgramData\Sonarr\bin\Sonarr.exe`
   - 启动目录：`C:\ProgramData\Sonarr\bin`
   - 参数：`-data=C:\ProgramData\Sonarr-4K`

> 请注意，**参数**指向步骤 1 中创建的*新*文件夹。这一点非常重要，因为它将所有数据文件从两个实例分别保存在不同的位置。{.is-warning}

1. 单击“安装服务”。窗口应关闭，服务现在可用于运行。
1. 继续 [配置 Sonarr-4k](#windows-multi-config-second)

### 托盘应用程序（Windows）

#### 先决条件（托盘应用程序）

- [您必须已经安装了 Sonarr](#windows)
- Sonarr 必须配置了 `/data=` 参数以允许多个实例
- 转到当前用户的启动文件夹 `%appdata%\Microsoft\Windows\Start Menu\Programs\Startup`，如果需要，编辑现有的快捷方式。

#### 创建 Sonarr-4K 托盘应用程序

- 右键单击并创建新快捷方式
- 路径：`C:\ProgramData\Sonarr\bin\Sonarr.exe /data=C:\ProgramData\Sonarr-4K`
- 为快捷方式指定一个唯一的名称，例如 `Sonarr-4K`，然后完成向导。
- 双击新的快捷方式以运行和测试。
- 继续 [配置 Sonarr-4k](#windows-multi-config-second)

### 配置 Sonarr-4k {#windows-multi-config-second}

- 无论您是使用服务方法还是托盘应用程序：停止两个服务和两个应用程序
- 启动 Sonarr-4k（服务或托盘应用程序）
- 打开 Sonarr-4k，并在应用程序内导航到 [设置 => 通用 => 主机](/sonarr/settings/#host)
- 将 `端口号` 从 `8989` 更改为不同的端口，例如 `7879`，以避免 Sonarr 和 Sonarr4k 冲突
- 现在应该能够启动两个应用程序
- 继续 [处理更新](#dealing-with-updates)

### 处理更新

- 在其中一个实例中禁用自动更新
- 如果更新了一个 Sonarr 实例，两个实例都将关闭，只有更新的实例将重新启动。要解决此问题，您将需要手动启动另一个实例，或者您可能需要查看以下 PowerShell 脚本来解决问题。

#### Windows 端口检查器和重启 PowerShell 脚本

- 当您使用两个 Sonarr 实例并且其中一个正在更新时，它将关闭所有实例。只有正在更新的实例将重新上线。
- 下面的 PowerShell 脚本应配置为计划任务。
- 它会检查端口，如果一个端口不在线，它将（重新）启动计划任务以启动 Sonarr。

1. 创建一个名为 SonarrInstancesChecker.ps1 的新文件，并使用下面的代码填充。
1. 使用实际的服务名称、IP 和端口编辑脚本。
1. [创建计划任务](https://www.thewindowsclub.com/schedule-task-in-windows-7-task-scheduler)，以按重复计划运行脚本。

- 安全选项：启用 `以最高权限运行`
  - 否则，脚本将无法操作服务
- 触发器：`在启动时`
- 重复任务：每 `5` 或 `10` 分钟
- 操作：`启动程序`
- 程序/脚本：`powershell`
- 参数：`-File D:\SonarrInstancesChecker.ps1`
  - 确保使用脚本位置的完整路径

```powershell
################################################################################################
### SonarrInstancesChecker.ps1                                                               ###
################################################################################################
### 通过检查端口来保持多个 Sonarr 实例在线                                                     ###
### 请使用 Sonarr 的 Discord 或 Reddit 寻求支持！                                              ###
### https://wiki.servarr.com/sonarr/installation#windows-multi                               ###
################################################################################################
### 版本：1.1                                                                                 ###
### 更新日期：2020-10-22                                                                      ###
### 作者：reloxx13                                                                           ###
################################################################################################



### 在此处设置您的配置 ###
# 设置正确的主机 IP 和端口，并使用您的服务或计划任务名称！

# (string) Sonarr 启动方式
# "Service"（默认）使用服务进程
# "ScheduledTask" 使用任务计划程序
$startType = 'Service'

# (bool) 启用时，将日志写入 C:\Users\YOURUSERNAME\log.txt
# $false（默认）
# $true
$logToFile = $false


$instances = @(
    [pscustomobject]@{   # 实例 1
        Name = 'Sonarr-V3'; # (string) 服务或任务名称（默认：Sonarr-V3）
        IP   = '192.168.178.12'; # (string) Sonarr 运行的服务器 IP（默认：192.168.178.12）
        Port = '7873'; # (string) Sonarr 运行的服务器端口（默认：7873）
    }
    [pscustomobject]@{   # 实例 2
        Name = 'Sonarr-4K'; # (string) 服务或任务名称（默认：Sonarr-4K）
        IP   = '192.168.178.12'; # (string) Sonarr 运行的服务器 IP（默认：192.168.178.12）
        Port = '7874'; # (string) Sonarr 运行的服务器端口（默认：7874）
    }
    # 如果需要，您可以在此处添加更多实例... 取消下面的注释
    # [pscustomobject]@{   # 实例 3
    # Name='Sonarr-3D';    # (string) 服务或任务名称（默认：Sonarr-3D）
    # IP='192.168.178.12'; # (string) Sonarr 运行的服务器 IP（默认：192.168.178.12）
    # Port='7875';         # (string) Sonarr 运行的服务器端口（默认：7875）
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
        Write-Log "端口 $($_.Port) 已关闭，正在重新启动 $($startType) $($_.Name)！"

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

## Linux 多实例

{#linux-multi}

- [Swizzin 用户](https://github.com/ComputerByte/sonarr4k)
- 非 Swizzin 用户
  - 确保第一个实例已传递 `-data=` 参数。
  - 暂时停止第一个实例，以便您可以更改第二个实例的端口 `systemctl stop sonarr`
  - 在其中一个 Sonarr 实例上禁用自动更新

> 下面是一个创建 Sonarr4K 实例的示例脚本。下面的 systemd 创建脚本将使用数据目录 `/var/lib/sonarr4k/`。确保目录存在，或根据需要进行修改。{.is-danger}

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

- 重新加载 systemd：

```shell
sudo systemctl -q daemon-reload
```

- 启用 Sonarr4k 服务：

```shell
sudo systemctl enable --now -q sonarr4k
```

## Docker 多实例

{#docker-multi}

- 只需使用不同的名称启动第二个 Docker 容器，确保满足上述要求。