---
title: Fejlfinding af netværk og tilladelser
description: 
published: true
date: 2022-03-13T15:12:02.123Z
tags: fejlfinding
editor: markdown
dateCreated: 2021-11-13T21:09:50.099Z
---

# Fejlfinding af netværk

- Generelt vil `curl` være nødvendig til meget af fejlfinding
- Til SSL vil `openssl` være nødvendig til fejlfinding

## SSL-problemer

- curl validerer ikke SSL-certifikater som \*Arrs gør, så openssl skal bruges

- Test forbindelsen/webstedet ved hjælp af openssl for at se, om certifikaterne er gyldige

```bash
openssl s_client -showcerts -connect <url>:443
```

## Ikke-forbindelig IPv6 IP

- Test forbindelsen med curl

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Kontrollerede porte i brug på Windows

- Brug netsh til at få en liste over porte i brug og hvad der bruger dem

```bash
netstat -ab
```

## Kontrollerede URL-reservationer på Windows

- Brug netsh til at få en liste over hvilke porte og URL'er apps er bundet til og lytter på

```bash
netsh http show urlacl
```

## Oprettelse af URL-reservationer på Windows

- Brug netsh til at oprette urlacl - nedenstående eksempel er for radarr, som bruger port `7878`

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Kontrollerede porte i brug på Linux

- Brug netstat til at finde porte i brug / hvilken port en app er på

```bash
sudo netstat -tnlp | grep <:port eller app>
```

### Eksempler

- Port `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- App med navnet `Radarr`

```bash
sudo netstat -tnlp | grep 'Radarr'
```