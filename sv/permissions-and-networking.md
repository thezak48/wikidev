---
title: Felsökning av nätverk och behörigheter
description: 
published: true
date: 2022-03-13T15:12:02.123Z
tags: felsökning
editor: markdown
dateCreated: 2021-11-13T21:09:50.099Z
---

# Felsökning av nätverk

- Generellt sett kommer `curl` att behövas för mycket av felsökningen
- För SSL kommer `openssl` att behövas för felsökning

## Problem med SSL

- curl validerar inte SSL-certifikat som \*Arrs gör, så openssl måste användas

- Testa anslutningen/webbplatsen med openssl för att se om certifikaten är giltiga

```bash
openssl s_client -showcerts -connect <url>:443
```

## IPv6 IP som inte kan anslutas

- Testa att ansluta med curl

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Kontrollera använda portar i Windows

- Använd netsh för att få en lista över använda portar och vad som använder dem

```bash
netstat -ab
```

## Kontrollera URL-reservationer i Windows

- Använd netsh för att få en lista över vilka portar och URL:er appar är bundna till och lyssnar på

```bash
netsh http show urlacl
```

## Skapa URL-reservationer i Windows

- Använd netsh för att skapa urlacl - nedanstående exempel är för radarr som använder port `7878`

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Kontrollera använda portar i Linux

- Använd netstat för att hitta använda portar / vilken port en app använder

```bash
sudo netstat -tnlp | grep <:port eller app>
```

### Exempel

- Port `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- App med namnet `Radarr`

```bash
sudo netstat -tnlp | grep 'Radarr'
```