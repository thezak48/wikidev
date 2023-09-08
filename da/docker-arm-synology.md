---
title: Installation af Docker på en Synology ARM NAS
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# Introduktion

Synology tilbyder kun en Docker-pakke til deres `x64`-baserede NAS. Brug af denne metode til at installere Docker på en `aarch64` NAS er helt uden support/ikke testet og helt på egen risiko. Det er fuldt ud muligt, at det vil ødelægge din NAS.

> Igen, denne metode til at installere Docker på en `aarch64` NAS er **helt uden support/ikke testet** og helt på egen risiko. Det er fuldt ud muligt, at det vil ødelægge din NAS. {.is-danger}

# Resumé

Nedenstående instruktioner vil:

1. Placere Docker-binærerne i `/usr/local/bin/`
1. Oprette en Docker-konfigurationsfil `/usr/local/etc/docker/docker.json`
1. Konfigurere Docker til at gemme sine data i `/volume1/docker/var`
1. Oprette et script til at starte Docker ved opstart i `/usr/local/etc/rc.d/docker.sh`
1. Oprette en `docker`-gruppe
1. Placere et docker-compose-script i `/usr/local/bin/`

# Installation

1. [Log ind på din Synology via SSH og skift til `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

1. Udfør følgende kommando:

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

Hvis alt går godt, skal du se følgende besked:

```none
Done. Please add your user to the Docker group in the Synology GUI and reboot your NAS.
```

Gør som der står:

1. Tilføj din bruger til den nye `docker`-gruppe ved hjælp af Synology GUI'en
1. **Genstart.**

Forhåbentlig har du fungerende `docker`- og `docker-compose`-kommandoer, som burde virke, når du er logget ind som din normale bruger.

# Begrænsninger

1. Det ser ud til, at de fleste ARM Synology-enheder ikke understøtter seccomp, så Docker-containeren har uhindret adgang til dit system (endnu mere end med en almindelig Docker).
1. Igen, på grund af Synology-begrænsninger, skal alle containere bruge `--network=host` (eller `network_mode: host` i compose), og alt vil være direkte tilgængeligt fra værten. Der er ingen portmappings.
1. Selvfølgelig kan du kun køre aarch64-billeder, men de fleste hotio- og linuxserver-billeder tilbyder en aarch64-version.

# Opsætning af et Docker-GUI

Hvis du vil have et GUI, kan du køre Portainer ved hjælp af følgende eksempel-compose:

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

Placer dette i en fil kaldet `docker-compose.yml` i en ellers tom mappe. Kør:

```shell
docker-compose up -d
```

Besøg [`http://ip:9000`](http://ip:9000) for at fuldføre opsætningen (hvor `ip` er IP-adressen på din Synology).

# Opsætning af Sonarr/Radarr/Lidarr/Readarr

For vejledning til opsætning af Sonarr/Radarr/Lidarr/Readarr, se [Docker Guide](/docker-guide), og **husk begrænsning 2 ovenfor.**