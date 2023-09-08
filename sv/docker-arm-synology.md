---
title: Installera Docker på en Synology ARM NAS
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# Introduktion

Synology erbjuder endast ett Docker-paket för sina NAS-enheter baserade på `x64`. Att använda denna metod för att installera Docker på en `aarch64` NAS är helt osupporterat/ointestat och helt på egen risk. Det är fullt möjligt att det kan förstöra din NAS.

> Återigen, denna metod för att installera Docker på en `aarch64` NAS är **helt osupporterad/ointestad** och helt på egen risk. Det är fullt möjligt att det kan förstöra din NAS. {.is-danger}

# Sammanfattning

Instruktionerna nedan kommer att:

1. Placera Docker-binärerna i `/usr/local/bin/`
1. Skapa en Docker-konfigurationsfil `/usr/local/etc/docker/docker.json`
1. Konfigurera Docker att spara sina data i `/volume1/docker/var`
1. Skapa ett skript för att starta Docker vid uppstart i `/usr/local/etc/rc.d/docker.sh`
1. Skapa en `docker`-grupp
1. Placera ett docker-compose-skript i `/usr/local/bin/`

# Installation

1. [Logga in på din Synology via SSH och höj till `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

1. Kör följande kommando:

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

Om allt går bra bör du se följande meddelande:

```none
Klart. Lägg till din användare i Docker-gruppen i Synology GUI och starta om din NAS.
```

Gör som det säger:

1. Lägg till din användare i den nya `docker`-gruppen med hjälp av Synology GUI
1. **Starta om.**

Förhoppningsvis har du fungerande `docker`- och `docker-compose`-kommandon, vilka bör fungera när du är inloggad som din vanliga användare.

# Förbehåll

1. Det verkar som att de flesta ARM-baserade Synology-enheter inte stöder seccomp, så Docker-kontainern har obegränsad åtkomst till ditt system (ännu mer än med en vanlig Docker).
1. Återigen, på grund av Synologys begränsningar måste alla kontainrar använda `--network=host` (eller `network_mode: host` i compose) och allt kommer att vara direkt åtkomligt från värden. Det finns inga portmappningar.
1. Självklart kan du bara köra aarch64-bilder, men de flesta hotio- och linuxserver-bilder erbjuder en aarch64-version.

# Konfigurera en Docker-GUI

Om du vill ha ett grafiskt gränssnitt kan du köra Portainer med följande exempelcompose:

```yml
    version: '2'

    services:
      portainer:
        image: portainer/portainer
        restart: unless-stopped
        network_mode: host
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
          - portainer_data:/data

    volumes:
      portainer_data:
```

Placera detta i en fil som heter `docker-compose.yml` i en annars tom katalog. Kör:

```shell
docker-compose up -d
```

Besök [`http://ip:9000`](http://ip:9000) för att slutföra installationen (där `ip` är IP-adressen för din Synology).

# Konfigurera Sonarr/Radarr/Lidarr/Readarr

För vägledning om hur du konfigurerar Sonarr/Radarr/Lidarr/Readarr, se [Docker Guide](/docker-guide), och **kom ihåg förbehåll 2 ovan.**