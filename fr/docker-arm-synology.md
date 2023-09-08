---
title: Installation de Docker sur un NAS Synology ARM
description: 
published: true
date: 2022-05-18T15:47:17.201Z
tags: docker, synology
editor: markdown
dateCreated: 2021-07-12T20:22:05.719Z
---

# Introduction

Synology ne propose qu'un package Docker sur leurs NAS basés sur `x64`. Utiliser cette méthode pour installer Docker sur un NAS `aarch64` est totalement non pris en charge/non testé et se fait entièrement à vos propres risques. Il est tout à fait possible que cela endommage votre NAS.

> Encore une fois, cette méthode pour installer Docker sur un NAS `aarch64` est **totalement non prise en charge/non testée** et se fait entièrement à vos propres risques. Il est tout à fait possible que cela endommage votre NAS. {.is-danger}

# Résumé

Les instructions ci-dessous vont :

1. Placer les binaires Docker dans `/usr/local/bin/`
1. Créer un fichier de configuration Docker `/usr/local/etc/docker/docker.json`
1. Configurer Docker pour enregistrer ses données dans `/volume1/docker/var`
1. Créer un script pour démarrer Docker au démarrage dans `/usr/local/etc/rc.d/docker.sh`
1. Créer un groupe `docker`
1. Placer un script docker-compose dans `/usr/local/bin/`

# Installation

1. [Connectez-vous à votre Synology via SSH et passez en tant que `root`](https://kb.synology.com/en-global/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)

1. Exécutez la commande suivante :

```bash
curl https://gist.githubusercontent.com/ta264/2b7fb6e6466b109b9bf9b0a1d91ebedc/raw/b76a28d25d0abd0d27a0c9afaefa0d499eb87d3d/get-docker.sh | sh
```

Si tout se passe bien, vous devriez voir le message :

```none
Done. Please add your user to the Docker group in the Synology GUI and reboot your NAS.
```

Faites ce qu'il dit :

1. Ajoutez votre utilisateur au nouveau groupe `docker` en utilisant l'interface graphique Synology
1. **Redémarrez.**

Espérons que vous disposez des commandes `docker` et `docker-compose` fonctionnelles, qui devraient fonctionner lorsque vous êtes connecté en tant qu'utilisateur normal.

# Limitations

1. Il semble que la plupart des Synology ARM ne prennent pas en charge seccomp, donc le conteneur Docker a un accès illimité à votre système (encore plus qu'avec un docker classique).
1. Encore une fois, en raison des contraintes de Synology, tous les conteneurs doivent utiliser `--network=host` (ou `network_mode: host` dans compose) et tout sera directement accessible depuis l'hôte. Il n'y a pas de mappages de ports.
1. Évidemment, vous ne pouvez exécuter que des images aarch64, mais la plupart des images hotio et linuxserver proposent une version aarch64.

# Configuration d'une interface graphique Docker

Si vous souhaitez une interface graphique, vous pouvez exécuter Portainer en utilisant l'exemple de composition suivant :

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

Placez cela dans un fichier appelé `docker-compose.yml` dans un répertoire vide. Exécutez :

```shell
docker-compose up -d
```

Rendez-vous sur [`http://ip:9000`](http://ip:9000) pour terminer la configuration (où `ip` est l'adresse IP de votre Synology).

# Configuration de Sonarr/Radarr/Lidarr/Readarr

Pour des instructions sur la configuration de Sonarr/Radarr/Lidarr/Readarr, consultez le [Guide Docker](/docker-guide), et **n'oubliez pas la limitation 2 ci-dessus.**