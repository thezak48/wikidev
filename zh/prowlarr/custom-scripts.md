---
title: Prowlarr自定义脚本
description: 
published: true
date: 2021-12-20T16:40:47.702Z
tags: prowlarr, 需要关注, 自定义脚本
editor: markdown
dateCreated: 2021-06-23T06:40:30.916Z
---

如果您想要触发一个自定义脚本，您可以在这里找到更多详细信息。通过[连接设置](/prowlarr/settings#connections)，可以将脚本添加到Prowlarr中。

# 概述

当导入或重命名一个剧集时，Prowlarr可以执行一个自定义脚本。根据不同的操作，会提供不同的参数。参数通过环境变量传递给脚本。

## Prowlarr日志

请注意，以下内容仅适用于自定义脚本的日志记录：

- 脚本的`stdout`输出将被记录为`Debug`
- 脚本的`stderr`输出将被记录为`Info`
- 脚本的触发将被记录在`Trace`中

# 环境变量

环境变量根据事件类型而有所不同。详细信息即将推出^tm^

> [在此期间，您可以在此处查看代码。欢迎贡献Wiki](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## 测试时

当将脚本添加到Prowlarr并点击“测试”时，脚本将以以下参数调用。脚本应能够优雅地忽略任何不支持的事件类型。

| 环境变量 | 详情 |
| -------- | ---- |
| `prowlarr_eventtype` | `Test` |