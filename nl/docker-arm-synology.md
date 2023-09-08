---
title: Docker installeren op een Synology ARM NAS
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# Inleiding

Synology biedt alleen een Docker-pakket aan voor hun `x64`-gebaseerde NAS. Het gebruik van deze methode om Docker te installeren op een `aarch64` NAS wordt volledig niet ondersteund/getest en is volledig op eigen risico. Het is heel goed mogelijk dat het uw NAS vernietigt.

> Nogmaals, deze methode om Docker te installeren op een `aarch64` NAS wordt **volledig niet ondersteund/getest** en is volledig op eigen risico. Het is heel goed mogelijk dat het uw NAS vernietigt. {.is-danger}

# Samenvatting

De onderstaande instructies zullen het volgende doen:

1. De Docker-binaries plaatsen in `/usr/local/bin/`
1. Een Docker-configuratiebestand `/usr/local/etc/docker/docker.json` maken
1. Docker configureren om zijn gegevens op te slaan in `/volume1/docker/var`
1. Een script maken om Docker bij het opstarten te starten op `/usr/local/etc/rc.d/docker.sh`
1. Een `docker`-groep maken
1. Een docker-compose-script plaatsen in `/usr/local/bin/`

# Installatie

1. [Log in op uw Synology via SSH en verhoog de rechten naar `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

1. Voer de volgende opdracht uit:

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

Als alles goed gaat, ziet u het bericht:

```none
Gereed. Voeg uw gebruiker toe aan de Docker-groep in de Synology GUI en start uw NAS opnieuw op.
```

Doe wat er staat:

1. Voeg uw gebruiker toe aan de nieuwe `docker`-groep met behulp van de Synology GUI
1. **Start opnieuw op.**

Hopelijk hebt u werkende `docker`- en `docker-compose`-opdrachten, die moeten werken wanneer u bent ingelogd als uw normale gebruiker.

# Kanttekeningen

1. Het lijkt erop dat de meeste ARM Synology-apparaten geen seccomp ondersteunen, dus de Docker-container heeft onbeperkte toegang tot uw systeem (nog meer dan bij een gewone Docker).
1. Nogmaals, vanwege de beperkingen van Synology moeten alle containers `--network=host` gebruiken (of `network_mode: host` in compose) en is alles rechtstreeks toegankelijk vanaf de host. Er zijn geen poorttoewijzingen.
1. U kunt uiteraard alleen aarch64-images uitvoeren, maar de meeste hotio- en linuxserver-images bieden een aarch64-versie.

# Het instellen van een Docker GUI

Als u een GUI wilt, kunt u Portainer uitvoeren met behulp van het volgende voorbeeldcompose-bestand:

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

Plaats dit in een bestand genaamd `docker-compose.yml` in een verder lege map. Voer uit:

```shell
docker-compose up -d
```

Ga naar [`http://ip:9000`](http://ip:9000) om de installatie te voltooien (waarbij `ip` het IP-adres van uw Synology is).

# Het instellen van Sonarr/Radarr/Lidarr/Readarr

Voor begeleiding bij het instellen van Sonarr/Radarr/Lidarr/Readarr, zie de [Docker-handleiding](/docker-guide), en **onthoud kanttekening 2 hierboven.**