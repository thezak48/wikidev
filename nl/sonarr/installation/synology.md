---
title: Sonarr Synology Installatie
description: Installatiehandleiding voor Sonarr op Synology
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [De SynoCommunity maakt, ondersteunt en onderhoudt een Synology NAS-pakket](https://synocommunity.com/package/nzbdrone)

> Het NAS-pakket wordt slecht onderhouden en is vaak verouderd. Als je NAS Docker ondersteunt, wordt het sterk aanbevolen om [Docker uit te voeren](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) in plaats daarvan. Je kunt Sonarr niet opnieuw installeren zonder je database handmatig te wissen, omdat het NAS-pakket verouderd is en niet is geconfigureerd om zichzelf bij het opstarten bij te werken. {.is-info}

- [SynoCommunity maakt ook het vereiste Mono-pakket, ondersteunt en onderhoudt het](https://synocommunity.com/package/mono)

## Synology Mono SSL-fouten

> Vanwege een bug in het slecht onderhouden Mono-pakket van SynoCommunity kan Sonarr geen verbinding maken na het bijwerken van Mono of na een nieuwe installatie. Dit kan worden opgelost door de instructies te volgen op [SynoCommunity Bug Report #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625). Houd er rekening mee dat DSM7-gebruikers op basis van [deze opmerking](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799) een extra stap hebben.
{.is-danger}

1. Schakel binnen DSM de SSH-service in via *Configuratiescherm => Terminal en SNMP* en klik op Toepassen.
1. Maak verbinding met de NAS via [Terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) (MacOS) met behulp van `ssh -l [beheerdersgebruikersnaam] [NAS-adres]` of via [Putty](https://www.putty.org/) (Windows) met het netwerkadres van je NAS.
1. Voer het vereiste beheerderswachtwoord in en druk op Enter.
1. Voer de juiste commando('s) in voor je DSM-versie zoals hieronder vermeld en druk op Enter.
1. Voer het vereiste beheerderswachtwoord in en druk op Enter. Wanneer het proces is voltooid, zou je de regel *Import process completed* moeten zien.
1. Verbreek de SSH-sessie door `exit` in te typen en op Enter te drukken.
1. Schakel binnen DSM de SSH-service uit via *Configuratiescherm => Terminal en SNMP* en klik op Toepassen.
1. De fouten in Sonarr zouden vanzelf moeten verdwijnen binnen enkele minuten.

### Commando voor het oplossen van Synology DSM6 Mono

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Commando voor het oplossen van Synology DSM7 Mono

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```