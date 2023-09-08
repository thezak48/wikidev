---
title: Probleemoplossingsgids voor netwerken en machtigingen
description: 
published: true
date: 2022-03-13T15:12:02.123Z
tags: troubleshooting
editor: markdown
dateCreated: 2021-11-13T21:09:50.099Z
---

# Probleemoplossing voor netwerken

- Over het algemeen is `curl` nodig voor veel probleemoplossingen.
- Voor SSL is `openssl` nodig voor probleemoplossing.

## SSL-problemen

- Curl valideert SSL-certificaten niet zoals browsers dat doen, dus openssl moet worden gebruikt.

- Test de verbinding/site met openssl om te zien of de certificaten geldig zijn.

```bash
openssl s_client -showcerts -connect <url>:443
```

## Niet bereikbaar IPv6 IP-adres

- Test de verbinding met curl.

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Controleren van poorten in gebruik op Windows

- Gebruik netsh om een lijst te krijgen van poorten in gebruik en wat ze gebruikt.

```bash
netstat -ab
```

## Controleren van URL-reserveringen op Windows

- Gebruik netsh om een lijst te krijgen van welke poorten en URL's apps gebonden zijn en naar luisteren.

```bash
netsh http show urlacl
```

## Maken van URL-reserveringen op Windows

- Gebruik netsh om de urlacl te maken - het onderstaande voorbeeld is voor radarr dat poort `7878` gebruikt.

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Controleren van poorten in gebruik op Linux

- Gebruik netstat om poorten in gebruik te vinden / op welke poort een app draait.

```bash
sudo netstat -tnlp | grep <:port of app>
```

### Voorbeelden

- Poort `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- App met de naam `Radarr`

```bash
sudo netstat -tnlp | grep 'Radarr'
```