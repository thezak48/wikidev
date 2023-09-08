---
title: Sonarr Synology Installation
description: Installationsguide för Sonarr på Synology
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [SynoCommunity skapar, stöder och underhåller en Synology NAS-paket](https://synocommunity.com/package/nzbdrone)

> NAS-paketet är dåligt underhållet och blir ofta föråldrat. Om din NAS stöder Docker rekommenderas det starkt [att köra Docker](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) istället. Du kommer inte att kunna installera om Sonarr utan att manuellt rensa din databas på grund av att NAS-paketet är föråldrat och inte är konfigurerat att uppdatera sig vid uppstart. {.is-info}

- [SynoCommunity skapar också, stöder och underhåller det nödvändiga Mono-paketet](https://synocommunity.com/package/mono)

## Synology Mono SSL-fel

> På grund av en bugg som infördes av SynoCommunitys dåligt underhållna Mono-paket kommer Sonarr att misslyckas med att ansluta efter att Mono har uppdaterats eller efter en ny installation. Detta kan åtgärdas genom att följa instruktionerna på [SynoCommunity Buggrapport #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625). Observera att baserat på [den här kommentaren](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799) har DSM7-användare ett extra steg.
{.is-danger}

1. Inom DSM, aktivera SSH-tjänsten i *Kontrollpanelen => Terminal & SNMP* och klicka på Tillämpa
1. Anslut till NAS:en med hjälp av [Terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) (MacOS) genom att använda `ssh -l [admin användarnamn] [NAS-adress]` eller använd [Putty](https://www.putty.org/) (Windows) för att ansluta till nätverksadressen för din NAS
1. Ange det nödvändiga administratörslösenordet och tryck på Enter
1. Ange lämplig kommando för din DSM-version som anges nedan och tryck på Enter
1. Ange det nödvändiga administratörslösenordet och tryck på Enter. När processen är klar bör du se raden *Import process completed*
1. Avsluta SSH-sessionen genom att skriva `exit` och tryck på Enter
1. Inom DSM, inaktivera SSH-tjänsten i *Kontrollpanelen => Terminal & SNMP* och klicka på Tillämpa
1. När processen är klar bör felen i Sonarr försvinna av sig själva inom några minuter.

### Kommando för att fixa Synology DSM6 Mono

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Kommando för att fixa Synology DSM7 Mono

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```