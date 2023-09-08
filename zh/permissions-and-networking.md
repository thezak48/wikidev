---
title: 网络和权限故障排除指南
description: 
published: true
date: 2022-03-13T15:12:02.123Z
tags: 故障排除
editor: markdown
dateCreated: 2021-11-13T21:09:50.099Z
---

# 网络故障排除

- 通常需要使用 `curl` 进行大部分故障排除
- 对于 SSL 问题，需要使用 `openssl` 进行故障排除

## SSL 问题

- `curl` 不像 \*Arrs 那样验证 SSL 证书，因此需要使用 openssl 进行验证

- 使用 openssl 测试连接/站点，查看证书是否有效

```bash
openssl s_client -showcerts -connect <url>:443
```

## 无法连接的 IPv6 IP

- 使用 curl 进行连接测试

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Windows 检查正在使用的端口

- 使用 netsh 获取正在使用的端口及其使用者的列表

```bash
netstat -ab
```

## Windows 检查 URL 预留

- 使用 netsh 获取应用程序绑定和监听的端口和 URL 列表

```bash
netsh http show urlacl
```

## Windows 创建 URL 预留

- 使用 netsh 创建 urlacl - 下面的示例是为使用端口 `7878` 的 radarr 创建的

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Linux 检查正在使用的端口

- 使用 netstat 查找正在使用的端口/应用程序所在的端口

```bash
sudo netstat -tnlp | grep <:port or app>
```

### 示例

- 端口 `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- 名为 `Radarr` 的应用程序

```bash
sudo netstat -tnlp | grep 'Radarr'
```
