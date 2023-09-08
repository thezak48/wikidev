---
title: Prowlarr Linux 安装
description: Prowlarr 的 Linux 安装指南
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

如果你想简化安装过程，请按照社区提供和维护的 `简易安装` 脚本来进行基本的 Debian (Raspbian / Raspberry Pi OS) / Ubuntu 安装。

**对于官方的“亲自动手”安装说明，请参考下面的 [Debian / Ubuntu 亲自动手安装](#debian-ubuntu-亲自动手安装) 步骤。**

[请查看 \*Arr 社区的安装脚本](/install-script)

### Debian / Ubuntu 亲自动手安装

你需要使用以下命令来安装二进制文件。

> 下面的步骤将下载 Prowlarr 并将其安装到 `/opt` 目录下
> Prowlarr 将在 `prowlarr` 用户和 `prowlarr` 组下运行
> Prowlarr 的配置文件将存储在 `/var/lib/prowlarr` 目录下
{.is-warning}

- 确保你已安装所需的先决条件包：

```shell
sudo apt install curl sqlite3
```

> 警告：忽略下面的先决条件将导致安装失败和应用程序无法正常运行。{.is-warning}

> **安装先决条件**
> 下面的说明基于以下先决条件。如有需要，请根据你的具体需求更改说明。
> \* 创建了用户 `prowlarr`
> \* 创建了目录 `/var/lib/prowlarr` 并确保用户 `prowlarr` 对其具有读写权限
{.is-danger}

> 继续下面的操作，即表示你已阅读并满足了上述要求。{.is-warning}

- 下载适用于你的架构的正确二进制文件。
  - 你可以使用 `dpkg --print-architecture` 命令确定你的架构
    - AMD64 使用 `arch=x64`
    - ARM、armf 和 armh 使用 `arch=arm`
    - ARM64 使用 `arch=arm64`

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- 解压文件：

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- 将文件移动到 `/opt/` 目录下

```shell
sudo mv Prowlarr/ /opt
```

> 这假设你已创建了用户，并将其作为 `prowlarr` 用户和 `prowlarr` 组运行。你可以根据你的用例进行更改。
{.is-danger}

- 确保二进制文件目录的所有权。

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- 配置 systemd，以便 Prowlarr 可以在启动时自动启动。

> 下面的 systemd 创建脚本将使用数据目录 `/var/lib/prowlarr`。确保它存在，或根据需要进行修改。对于默认数据目录 `/home/$USER/.config/Prowlarr`，只需删除 `-data` 参数。注意：`$USER` 是 Prowlarr 运行的用户，并在下面定义。
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/prowlarr.service > /dev/null
[Unit]
Description=Prowlarr Daemon
After=syslog.target network.target
[Service]
User=prowlarr
Group=prowlarr
Type=simple

ExecStart=/opt/Prowlarr/Prowlarr -nobrowser -data=/var/lib/prowlarr/
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

- 启用 Prowlarr 服务：

```shell
sudo systemctl enable --now -q prowlarr
```

- （可选）删除 tar 压缩包：

```shell
rm Prowlarr*.linux*.tar.gz
```

通常，要访问 Prowlarr 的 Web GUI，请浏览 `http://{你的服务器 IP 地址}:9696`

如果 Prowlarr 似乎没有启动，请检查服务的状态：

```shell
sudo journalctl --since today -u prowlarr
```

---

### 卸载

要卸载并清除数据：
> 警告：这将销毁你的应用程序数据。{.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

要卸载并保留你的应用程序数据：

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```