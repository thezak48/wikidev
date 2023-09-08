---
title: Installation de Radarr sur Linux
description: Guide d'installation de Radarr sur Linux
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Note: Raspberry Pi OS et Raspbian sont tous deux des variantes de Debian {.is-info}

### Installation facile

Pour les débutants Debian / Ubuntu / Raspbian, il n'y a pas de référentiel Apt ou de paquet Deb.

Si vous voulez une installation facile, suivez ce script `Easy Install` fourni et maintenu par la communauté pour une installation de base de Debian (Raspbian / Raspberry Pi OS) / Ubuntu.

**Pour les instructions d'installation officielles qui sont "pratiques", suivez les étapes de [l'installation pratique Debian / Ubuntu](#debian-ubuntu-hands-on-install) ci-dessous.**

[Veuillez consulter le script d'installation de la communauté \*Arr](/install-script)

> Radarr utilise une version intégrée de ffprobe pour l'analyse des fichiers multimédias et n'a pas besoin que ffprobe ou ffmpeg soit installé sur le système. Si Radarr indique que Ffprobe n'est pas trouvé, cela peut généralement être corrigé avec une réinstallation.
{.is-info}

### Installation pratique Debian / Ubuntu

Vous devrez installer les binaires en utilisant les commandes ci-dessous.

> Les étapes ci-dessous téléchargeront Radarr et l'installeront dans `/opt`
> Radarr s'exécutera sous l'utilisateur `radarr` et le groupe `media`; `media` est le groupe couramment suggéré pour exécuter les \*Arrs, les clients de téléchargement et le serveur multimédia.
> Les fichiers de configuration de Radarr seront stockés dans `/var/lib/radarr`
{.is-success}

- Assurez-vous d'avoir les paquets prérequis nécessaires :

```shell
sudo apt install curl sqlite3
```

> Attention: Ignorer les prérequis ci-dessous entraînera une installation échouée et une application non fonctionnelle. {.is-warning}

> **Prérequis d'installation**
> Les instructions ci-dessous sont basées sur les prérequis suivants. Modifiez les instructions au besoin pour répondre à vos besoins spécifiques si nécessaire.
> \* L'utilisateur `radarr` est créé
> \* L'utilisateur `radarr` fait partie du groupe `media`
> \* Vos clients de téléchargement et votre serveur multimédia s'exécutent en tant que membres du groupe `media`
> \* Les chemins utilisés par vos clients de téléchargement et votre serveur multimédia sont accessibles (lecture/écriture) par le groupe `media`
> \* Vous avez créé le répertoire `/var/lib/radarr` et vous avez assuré que l'utilisateur `radarr` dispose des autorisations de lecture/écriture pour celui-ci
{.is-danger}

> En continuant ci-dessous, vous reconnaissez avoir lu et satisfait aux exigences ci-dessus. {.is-success}

- Téléchargez les binaires corrects pour votre architecture.
  - Vous pouvez déterminer votre architecture avec `dpkg --print-architecture`
    - AMD64 utilisez `arch=x64`
    - ARM, armf et armh utilisent `arch=arm`
    - ARM64 utilisez `arch=arm64`

```shell
wget --content-disposition 'http://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Décompressez les fichiers :

```shell
tar -xvzf Radarr*.linux*.tar.gz
```

- Déplacez les fichiers vers `/opt/`

```shell
sudo mv Radarr /opt/
```

> Remarque: Cela suppose que vous exécuterez l'utilisateur `radarr` et le groupe `media`. Vous pouvez modifier cela pour correspondre à votre cas d'utilisation. Il est important de choisir correctement ces paramètres pour éviter les problèmes de permission avec vos fichiers multimédias. Nous vous suggérons de garder au moins le nom du groupe identique entre votre client(s) de téléchargement et Radarr.
{.is-danger}

- Assurez-vous de posséder le répertoire binaire.

```shell  
sudo chown radarr:radarr -R /opt/Radarr
```

- Configurez systemd pour que Radarr démarre automatiquement au démarrage.

> Le script de création systemd ci-dessous utilisera un répertoire de données `/var/lib/radarr`. Assurez-vous qu'il existe ou modifiez-le si nécessaire. Pour le répertoire de données par défaut `/home/$USER/.config/Radarr`, supprimez simplement l'argument `-data`. Notez que `$USER` est l'utilisateur sous lequel Radarr s'exécute et est défini ci-dessous.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/radarr.service > /dev/null
[Unit]
Description=Radarr Daemon
After=syslog.target network.target
[Service]
User=radarr
Group=media
Type=simple

ExecStart=/opt/Radarr/Radarr -nobrowser -data=/var/lib/radarr/
TimeoutStopSec=20
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
```

- Rechargez systemd :

```shell
sudo systemctl -q daemon-reload
```

- Activez le service Radarr :

```shell
sudo systemctl enable --now -q radarr
```

- (Facultatif) Supprimez le fichier tarball :

```shell
rm Radarr*.linux*.tar.gz
```

Généralement, pour accéder à l'interface web de Radarr, accédez à `http://{Adresse IP de votre serveur}:7878`

> Radarr utilise une version intégrée de ffprobe pour l'analyse des fichiers multimédias et n'a pas besoin que ffprobe ou ffmpeg soit installé sur le système. Si Radarr indique que Ffprobe n'est pas trouvé, cela peut généralement être corrigé avec une réinstallation.
{.is-info}

Si Radarr ne semble pas avoir démarré, vérifiez l'état du service :

```shell
sudo journalctl --since today -u radarr
```

---

### Désinstallation

Pour désinstaller et purger :
> Attention: Cela détruira vos données d'application. {.is-danger}

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /var/lib/radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```

Pour désinstaller et conserver vos données d'application :

```bash
sudo systemctl stop radarr
sudo rm -rf /opt/Radarr
sudo rm -rf /etc/systemd/system/radarr.service
sudo systemctl -q daemon-reload
```