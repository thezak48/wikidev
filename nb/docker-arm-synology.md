---
title: Installere Docker på en Synology ARM NAS
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# Innledning

Synology tilbyr bare en Docker-pakke på deres `x64`-baserte NAS. Å bruke denne metoden for å installere Docker på en `aarch64` NAS er helt usupportert/ikke testet og helt på egen risiko. Det er fullt mulig at det kan ødelegge NAS-en din.

> Igjen, denne metoden for å installere Docker på en `aarch64` NAS er **helt usupportert/ikke testet** og helt på egen risiko. Det er fullt mulig at det kan ødelegge NAS-en din. {.is-danger}

# Oppsummering

Instruksjonene nedenfor vil:

1. Plassere Docker-binærene i `/usr/local/bin/`
1. Opprette en Docker-konfigurasjonsfil `/usr/local/etc/docker/docker.json`
1. Konfigurere Docker til å lagre dataene sine i `/volume1/docker/var`
1. Opprette et skript for å starte Docker ved oppstart i `/usr/local/etc/rc.d/docker.sh`
1. Opprette en `docker`-gruppe
1. Plassere et docker-compose-skript i `/usr/local/bin/`

# Installasjon

1. [Logg inn på Synology-en din via SSH og bytt til `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

1. Kjør følgende kommando:

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

Hvis alt går bra, skal du se meldingen:

```none
Done. Please add your user to the Docker group in the Synology GUI and reboot your NAS.
```

Gjør som det står:

1. Legg til brukeren din i den nye `docker`-gruppen ved hjelp av Synology GUI-en
1. **Start på nytt.**

Forhåpentligvis har du fungerende `docker`- og `docker-compose`-kommandoer, som skal fungere når du er logget inn som vanlig bruker.

# Begrensninger

1. Det virker som de fleste ARM Synology-enhetene ikke støtter seccomp, så Docker-containeren har uhindret tilgang til systemet ditt (enda mer enn med en vanlig Docker).
1. Igjen, på grunn av Synology-begrensninger, må alle containere bruke `--network=host` (eller `network_mode: host` i compose), og alt vil være direkte tilgjengelig fra vertsmaskinen. Det er ingen porter som er kartlagt.
1. Selvfølgelig kan du bare kjøre aarch64-bilder, men de fleste hotio- og linuxserver-bilder tilbyr en aarch64-versjon.

# Oppsett av et Docker-GUI

Hvis du vil ha et GUI, kan du kjøre Portainer ved hjelp av følgende eksempel-compose:

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

Plasser dette i en fil kalt `docker-compose.yml` i en ellers tom mappe. Kjør:

```shell
docker-compose up -d
```

Besøk [`http://ip:9000`](http://ip:9000) for å fullføre oppsettet (der `ip` er IP-adressen til Synology-en din).

# Oppsett av Sonarr/Radarr/Lidarr/Readarr

For veiledning om oppsett av Sonarr/Radarr/Lidarr/Readarr, se [Docker Guide](/docker-guide), og **husk begrensning 2 ovenfor.**