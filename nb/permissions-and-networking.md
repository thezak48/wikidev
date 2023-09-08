---
title: Feilsøkingsguide for nettverk og tillatelser
description: 
published: true
date: 2022-03-13T15:12:02.123Z
tags: feilsøking
editor: markdown
dateCreated: 2021-11-13T21:09:50.099Z
---

# Feilsøking for nettverk

- Generelt vil `curl` være nødvendig for mye av feilsøkingen
- For SSL vil `openssl` være nødvendig for feilsøking

## SSL-problemer

- curl validerer ikke SSL-sertifikater som \*Arrs gjør, så openssl må brukes

- Test tilkoblingen/nettstedet ved å bruke openssl for å se om sertifikatene er gyldige

```bash
openssl s_client -showcerts -connect <url>:443
```

## Ikke-tilkoblingsbar IPv6-IP

- Test tilkobling med curl

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Sjekk porter i bruk på Windows

- Bruk netsh for å få en liste over porter i bruk og hva som bruker dem

```bash
netstat -ab
```

## Sjekk URL-reservasjoner på Windows

- Bruk netsh for å få en liste over hvilke porter og URL-er apper er bundet til og lytter på

```bash
netsh http show urlacl
```

## Opprett URL-reservasjoner på Windows

- Bruk netsh for å opprette urlacl - det følgende eksempelet er for radarr som bruker port `7878`

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Sjekk porter i bruk på Linux

- Bruk netstat for å finne porter i bruk / hvilken port en app er på

```bash
sudo netstat -tnlp | grep <:port or app>
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