---
title: Radarr Linux 安装
description: Radarr 的 Linux 安装指南
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> 注意：Raspberry Pi OS 和 Raspbian 都是 Debian 的变种 {.is-info}

### 简易安装

对于 Debian / Ubuntu / Raspbian 的初学者来说，没有 Apt 仓库或 Deb 包。

如果你想要简单的安装过程，请按照社区提供和维护的 `简易安装` 脚本来进行基本的 Debian (Raspbian / Raspberry Pi OS) / Ubuntu 安装。

**对于官方的“亲自动手”安装指南，请参考下面的 [Debian / Ubuntu 亲自动手安装](#debian-ubuntu-亲自动手安装) 步骤。**

[请参阅 \*Arr 社区安装脚本](/install-script)

> Radarr 使用捆绑版本的 ffprobe 进行媒体文件分析，不需要在系统上安装 ffprobe 或 ffmpeg。如果 Radarr 提示找不到 Ffprobe，通常可以通过重新安装来解决。
{.is-info}

### Debian / Ubuntu 亲自动手安装

你需要使用以下命令来安装二进制文件。

> 下面的步骤将下载 Radarr 并将其安装到 `/opt` 目录下
> Radarr 将在 `radarr` 用户和 `media` 组下运行；`media` 是常见的建议组，用于运行 \*Arrs、下载客户端和媒体服务器。
> Radarr 的配置文件将存储在 `/var/lib/radarr` 目录下
{.is-success}

- 确保你已经安装了所需的先决条件包：

```shell
sudo apt install curl sqlite3
```

> 警告：忽略以下先决条件将导致安装失败和应用程序无法正常工作。{.is-warning}

> **安装先决条件**
> 下面的说明基于以下先决条件。如果需要，根据你的具体需求更改说明。
> \* 创建了用户 `radarr`
> \* 用户 `radarr` 是 `media` 组的一部分
> \* 你的下载客户端和媒体服务器以及它们所在的组都是 `media` 组的一部分
> \* 你的下载客户端和媒体服务器使用的路径对 `media` 组是可访问的（读/写）
> \* 你创建了目录 `/var/lib/radarr` 并确保用户 `radarr` 对其具有读/写权限
{.is-danger}

> 继续下面的操作，表示你已经阅读并满足了上述要求。{.is-success}

- 下载适合你架构的二进制文件。
  - 你可以使用 `dpkg --print-architecture` 命令确定你的架构
    - AMD64 使用 `arch=x64`
    - ARM、armf 和 armh 使用 `arch=arm`
    - ARM64 使用 `arch=arm64`

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- 解压文件：

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- 将文件移动到 `/opt/` 目录下

```shell
sudo mv Radarr /opt/
```

> 注意：这假设你将以 `radarr` 用户和 `media` 组身份运行。你可以根据自己的情况进行更改。选择正确的用户和组对于避免媒体文件的权限问题非常重要。我们建议你至少在下载客户端和 Radarr 之间保持组名相同。
{.is-danger}

- 确保二进制文件目录的所有权。

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- 配置 systemd，以便 Radarr 可以在启动时自动启动。

> 下面的 systemd 创建脚本将使用数据目录 `/var/lib/radarr`。确保它存在或根据需要进行修改。对于默认的数据目录 `/home/$USER/.config/Radarr`，只需删除 `-data` 参数。注意：`$USER` 是 Radarr 运行的用户，并在下面定义。
{.is-danger}

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

- 重新加载 systemd：

```shell
sudo systemctl -q daemon-reload
```

- 启用 Radarr 服务：

```shell
sudo systemctl enable --now -q radarr
```

- （可选）删除压缩包：

```shell
rm Radarr*.linux*.tar.gz
```

通常，要访问 Radarr 的 Web GUI，请浏览 `http://{你的服务器 IP 地址}:7878`

> Radarr 使用捆绑版本的 ffprobe 进行媒体文件分析，不需要在系统上安装 ffprobe 或 ffmpeg。如果 Radarr 提示找不到 Ffprobe，通常可以通过重新安装来解决。
{.is-info}

如果 Radarr 似乎没有启动，请检查服务的状态：

```shell
sudo journalctl --since today -u radarr
```

---

### 卸载

要卸载并清除数据：
> 警告：这将销毁你的应用程序数据。{.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

要卸载并保留你的应用程序数据：

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```