---
title: Readarr Linux 安装
description: Readarr 的 Linux 安装指南
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

如果你想过上简单的生活，请按照社区提供和维护的 `简易安装` 脚本进行基本的 Debian (Raspbian / Raspberry Pi OS) / Ubuntu 安装。

**对于官方的“亲自动手”安装说明，请参阅下面的 [Debian / Ubuntu 亲自动手安装](#debian-ubuntu-亲自动手安装) 步骤。**

[请参阅 \*Arr 社区安装脚本](/install-script)

### Debian / Ubuntu 亲自动手安装

你需要使用以下命令安装二进制文件。

> 下面的步骤将下载 Readarr 并将其安装到 `/opt` 目录下
> Readarr 将在 `readarr` 用户和 `media` 组下运行；`media` 是常见的建议组，用于运行 \*Arrs、下载客户端和媒体服务器。
> Readarr 的配置文件将存储在 `/var/lib/readarr` 目录下
{.is-warning}

- 确保你安装了所需的前提软件包：

```shell
sudo apt install curl sqlite3
```

> 警告：忽略下面的前提条件将导致安装失败和应用程序无法正常工作。{.is-warning}

> **安装前提条件**
> 下面的说明基于以下前提条件。如果需要，根据你的特定需求更改说明。
> \* 创建了用户 `readarr`
> \* 用户 `readarr` 是 `media` 组的一部分
> \* 你的下载客户端和媒体服务器以及它们所在的组 `media` 运行
> \* 你的下载客户端和媒体服务器使用的路径对 `media` 组是可访问的（读/写）
> \* 如果将使用 Calibre，Calibre 以 `media` 组身份运行，并且 Calibre 图书馆对 `media` 具有读/写权限
> \* 你创建了目录 `/var/lib/readarr` 并确保用户 `readarr` 对其具有读/写权限
{.is-danger}

> 继续下面的操作，表示你已经阅读并满足了上述要求。{.is-warning}

- 下载适用于你的架构的正确二进制文件。
  - 你可以使用 `dpkg --print-architecture` 命令确定你的架构
    - AMD64 使用 `arch=x64`
    - ARM、armf 和 armh 使用 `arch=arm`
    - ARM64 使用 `arch=arm64`

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- 解压文件：

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- 将文件移动到 `/opt/` 目录下

```shell
sudo mv Readarr /opt/
```

> 注意：这里假设你已经创建了用户并将其作为 `readarr` 用户和 `media` 组运行。你可以根据你的用例进行更改。选择正确的用户和组名称非常重要，以避免在媒体文件上出现权限问题。我们建议你至少保持下载客户端和 Readarr 之间的组名相同。请注意，如果你希望使用 Calibre，Readarr 将需要该目录的权限。
{.is-danger}

- 确保二进制文件目录的所有权。

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- 配置 systemd，以便 Readarr 可以在启动时自动启动。

> 下面的 systemd 创建脚本将使用数据目录 `/var/lib/readarr`。确保它存在，或根据需要进行修改。对于默认的数据目录 `/home/$USER/.config/Readarr`，只需删除 `-data` 参数。注意：这里的 `$USER` 是 Readarr 运行的用户，并在下面定义。
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr.service > /dev/null
[Unit]
Description=Readarr Daemon
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/readarr/
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

- 启用 Readarr 服务：

```shell
sudo systemctl enable --now -q readarr
```

- （可选）删除 tar 压缩包：

```shell
rm Readarr*.linux*.tar.gz
```

通常，要访问 Readarr 的 Web GUI，请浏览 `http://{你的服务器 IP 地址}:8787`

如果 Readarr 似乎没有启动，请检查服务的状态：

```shell
sudo journalctl --since today -u readarr
```

---

### 卸载

要卸载并清除：
> 警告：这将销毁你的应用程序数据。{.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

要卸载并保留你的应用程序数据：

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```