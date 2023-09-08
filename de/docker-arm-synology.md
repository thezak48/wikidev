---
title: Docker auf einem Synology ARM NAS installieren
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# Einführung

Synology bietet das Docker-Paket nur für ihre `x64`-basierten NAS-Geräte an. Die Verwendung dieser Methode zur Installation von Docker auf einem `aarch64`-basierten NAS ist völlig unsupportet/ungetestet und erfolgt vollständig auf eigenes Risiko. Es ist durchaus möglich, dass dadurch Ihr NAS zerstört wird.

> Nochmals, diese Methode zur Installation von Docker auf einem `aarch64`-basierten NAS ist **völlig unsupportet/ungetestet** und erfolgt vollständig auf eigenes Risiko. Es ist durchaus möglich, dass dadurch Ihr NAS zerstört wird. {.is-danger}

# Zusammenfassung

Die folgenden Anweisungen werden:

1. Die Docker-Binärdateien in `/usr/local/bin/` platzieren
1. Eine Docker-Konfigurationsdatei `/usr/local/etc/docker/docker.json` erstellen
1. Docker so konfigurieren, dass seine Daten in `/volume1/docker/var` gespeichert werden
1. Ein Skript zum Starten von Docker beim Booten unter `/usr/local/etc/rc.d/docker.sh` erstellen
1. Eine `docker`-Gruppe erstellen
1. Ein docker-compose-Skript in `/usr/local/bin/` platzieren

# Installation

1. [Melden Sie sich über SSH bei Ihrem Synology an und wechseln Sie zu `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

1. Führen Sie den folgenden Befehl aus:

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

Wenn alles gut geht, sollte die Meldung angezeigt werden:

```none
Done. Please add your user to the Docker group in the Synology GUI and reboot your NAS.
```

Tun Sie, wie es sagt:

1. Fügen Sie Ihren Benutzer zur neuen `docker`-Gruppe über die Synology GUI hinzu
1. **Starten Sie den NAS neu.**

Hoffentlich haben Sie funktionierende `docker`- und `docker-compose`-Befehle, die funktionieren, wenn Sie als normaler Benutzer angemeldet sind.

# Einschränkungen

1. Es scheint, dass die meisten ARM Synology-Geräte seccomp nicht unterstützen, sodass der Docker-Container uneingeschränkten Zugriff auf Ihr System hat (noch mehr als bei einem regulären Docker).
1. Aufgrund von Synology-Beschränkungen müssen alle Container erneut `--network=host` verwenden (oder `network_mode: host` in compose), und alles ist direkt vom Host aus erreichbar. Es gibt keine Portzuordnungen.
1. Offensichtlich können Sie nur aarch64-Images ausführen, aber die meisten hotio- und linuxserver-Images bieten eine aarch64-Version an.

# Einrichten einer Docker-GUI

Wenn Sie eine GUI möchten, können Sie Portainer mit dem folgenden Beispiel-Compose ausführen:

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

Platzieren Sie dies in einer Datei namens `docker-compose.yml` in einem ansonsten leeren Verzeichnis. Führen Sie aus:

```shell
docker-compose up -d
```

Besuchen Sie [`http://ip:9000`](http://ip:9000), um die Einrichtung abzuschließen (wobei `ip` die IP-Adresse Ihres Synology-Geräts ist).

# Einrichten von Sonarr/Radarr/Lidarr/Readarr

Für Anleitungen zur Einrichtung von Sonarr/Radarr/Lidarr/Readarr siehe den [Docker Guide](/docker-guide) und **beachten Sie die oben genannte Einschränkung 2.**