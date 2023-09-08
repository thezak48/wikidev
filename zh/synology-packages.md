---
title: Synology套件
description: Servarr Synology套件
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Servarr Synology套件](#servarr-synology套件)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [在DSM 7.X上安装Bubblewrap](#在dsm-7x上安装bubblewrap)
    - [简单的Bubblewrap安装](#简单的bubblewrap安装)
    - [手动安装Bubblewrap](#手动安装bubblewrap)

# Servarr Synology套件

> 这些套件可以被视为“测试版”
{.is-danger}

- Servarr团队现在创建并维护Synology套件
- 安装说明如下，适用于特定的DSM版本

> 通常情况下，现有的SynoCommunity版本与Servarr版本不兼容，需要进行一些额外操作。这意味着在备份数据库之后需要删除旧的套件，具体操作可以参考[备份/恢复Radarr的说明](/radarr/faq#how-do-i-backuprestore-radarr)。可以通过\*Arr应用的Web界面进行操作。
{.is-warning}

> SynoCommunity有一个[按Synology型号分类的NAS列表](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model)，可以帮助您确定正确的套件。
{.is-info}

# DSM 6.x

- Lidarr-Official、Prowlarr-Official、Radarr-Official、Readarr-Official和Sonarr套件应该可以正常工作。
- 请注意，不再需要来自SynoCommunity的独立Mono套件，它已经包含在我们的套件中。
- 从[Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)下载适用于您NAS架构的应用程序版本，并通过套件管理器[手动安装套件](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)。

# DSM 7.x

- Lidarr-Official、Prowlarr-Official、Radarr-Official和Readarr-Official套件对大多数架构来说应该可以正常工作。
  - 请注意，使用`comcerto2k`的NAS需要额外的步骤来安装Lidarr、Prowlarr、Radarr和Readarr；[请参阅说明](#在dsm-7x上安装bubblewrap)。
- 请注意，Sonarr套件对**所有**架构都需要额外的步骤。
- 请注意，不再需要来自SynoCommunity的独立Mono套件，它已经包含在我们的套件中。

> 对于运行在`comcerto2k`上的NAS（*所有套件*）和Sonarr（*所有NAS架构*），您需要安装Bubblewrap套件并执行所述的手动步骤。**在尝试安装\*Arr套件之前，必须先安装Bubblewrap**
{.is-warning}

- 从[Servarr Synology Package GitHub](https://github.com/Servarr/spksrc/releases)下载适用于您NAS架构的Bubblewrap版本，并通过套件管理器[手动安装套件](https://kb.synology.com/en-us/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6)。

## 在DSM 7.X上安装Bubblewrap

Bubblewrap允许我们在基本容器中运行程序，以便我们可以使用足够新的库来运行.NET6。

> **由于DSM 7.0+的限制，安装后需要进行一些手动设置。**
{.is-danger}

### 简单的Bubblewrap安装

1. 在DSM中创建一个触发任务：

- 用户：`root`
  - 事件：`启动`

1. 在`运行命令`中输入：

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. 保存触发任务，并运行一次。

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### 手动安装Bubblewrap

1. [通过SSH登录到Synology并提升为`root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. 执行以下命令：

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```