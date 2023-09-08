---
title: Netzwerk- und Berechtigungsfehlerbehebung
description: 
published: true
date: 2022-03-13T15:12:02.123Z
tags: troubleshooting
editor: markdown
dateCreated: 2021-11-13T21:09:50.099Z
---

# Netzwerkfehlerbehebung

- In der Regel wird `curl` für die meisten Fehlerbehebungen benötigt.
- Für SSL ist `openssl` zur Fehlerbehebung erforderlich.

## SSL-Probleme

- Curl überprüft SSL-Zertifikate nicht wie \*Arrs, daher muss openssl verwendet werden.

- Testen Sie die Verbindung/Website mit openssl, um zu sehen, ob die Zertifikate gültig sind.

```bash
openssl s_client -showcerts -connect <url>:443
```

## Nicht erreichbare IPv6-IP

- Testen Sie die Verbindung mit curl.

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Überprüfen von Ports in Verwendung unter Windows

- Verwenden Sie netsh, um eine Liste der verwendeten Ports und deren Verwendung anzuzeigen.

```bash
netstat -ab
```

## Überprüfen von URL-Reservierungen unter Windows

- Verwenden Sie netsh, um eine Liste der Ports und URLs zu erhalten, an die Apps gebunden sind und auf die sie hören.

```bash
netsh http show urlacl
```

## Erstellen von URL-Reservierungen unter Windows

- Verwenden Sie netsh, um die URL-Reservierung zu erstellen. Das folgende Beispiel ist für Radarr, das den Port `7878` verwendet.

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Überprüfen von Ports in Verwendung unter Linux

- Verwenden Sie netstat, um verwendete Ports zu ermitteln bzw. den Port einer App zu finden.

```bash
sudo netstat -tnlp | grep <:port or app>
```

### Beispiele

- Port `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- App mit dem Namen `Radarr`

```bash
sudo netstat -tnlp | grep 'Radarr'
```