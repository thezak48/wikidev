---
title: Installation de Lidarr sur Linux
description: Guide d'installation de Lidarr sur Linux
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Linux

## Debian / Ubuntu

> Note: Raspberry Pi OS et Raspbian sont tous deux des variantes de Debian {.is-info}

> Lidarr v0.8 n'est pas compatible ni pris en charge sur Ubuntu 22.04 [Voir cette entrée FAQ pour plus de détails](/lidarr/faq#lidarr-stopped-working-after-updating-to-ubuntu-2204)
{.is-warning}

### Installation facile

Pour les débutants Debian / Ubuntu / Raspbian, il n'y a pas de référentiel Apt ou de paquet Deb.

Si vous voulez une installation facile, suivez ce script d'installation fourni et maintenu par la communauté pour une installation de base de Debian (Raspbian / Raspberry Pi OS) / Ubuntu.

**Pour les instructions d'installation officielles qui sont "pratiques", suivez les étapes d'installation de Debian / Ubuntu ci-dessous.**

[Veuillez consulter le script d'installation de la communauté \*Arr](/install-script)

### Installation pratique de Debian / Ubuntu

Vous devrez installer les binaires en utilisant les commandes ci-dessous.

> Les étapes ci-dessous téléchargeront Lidarr et l'installeront dans `/opt`
> Lidarr s'exécutera sous l'utilisateur `lidarr` et le groupe `media`
> Les fichiers de configuration de Lidarr seront stockés dans `/var/lib/lidarr`
{.is-warning}

- Assurez-vous d'avoir les paquets prérequis nécessaires :

```shell
sudo apt install curl mediainfo sqlite3 libchromaprint-tools
```

> Attention : Ignorer les prérequis ci-dessous entraînera une installation échouée et une application non fonctionnelle. {.is-warning}

> **Prérequis d'installation**
> Les instructions ci-dessous sont basées sur les prérequis suivants. Modifiez les instructions au besoin pour répondre à vos besoins spécifiques si nécessaire.
> \* L'utilisateur `lidarr` est créé
> \* L'utilisateur `lidarr` fait partie du groupe `media`
> \* Vos clients de téléchargement et votre serveur multimédia s'exécutent en tant que membres du groupe `media`
> \* Vos chemins utilisés par vos clients de téléchargement et votre serveur multimédia sont accessibles (lecture/écriture) au groupe `media`
> \* Vous avez créé le répertoire `/var/lib/lidarr` et vous avez assuré que l'utilisateur `lidarr` dispose des autorisations de lecture/écriture pour celui-ci
{.is-danger}

> En continuant ci-dessous, vous reconnaissez avoir lu et satisfait aux exigences ci-dessus. {.is-warning}

- Téléchargez les binaires corrects pour votre architecture.
  - Vous pouvez déterminer votre architecture avec `dpkg --print-architecture`
    - AMD64 utilisez `arch=x64`
    - ARM, armf et armh utilisent `arch=arm`
    - ARM64 utilisez `arch=arm64`

```shell
wget --content-disposition 'http://lidarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Décompressez les fichiers :

```shell
tar -xvzf Lidarr*.linux*.tar.gz
```

- Déplacez les fichiers vers `/opt/`

```shell
sudo mv Lidarr/ /opt
```

> Cela suppose que vous avez créé l'utilisateur et qu'il s'exécutera en tant qu'utilisateur `lidarr` et groupe `media`. Vous pouvez modifier cela pour correspondre à votre cas d'utilisation. Il est important de choisir correctement ces valeurs pour éviter les problèmes de permission avec vos fichiers multimédias. Nous vous suggérons de garder au moins le nom du groupe identique entre votre/des client(s) de téléchargement et Lidarr.
{.is-danger}

- Assurez-vous que le répertoire binaire appartient à l'utilisateur.

```shell
sudo chown -R lidarr:media /opt/Lidarr
```

- Configurez systemd pour que Lidarr démarre automatiquement au démarrage.

> Le script de création systemd ci-dessous utilisera un répertoire de données `/var/lib/lidarr`. Assurez-vous qu'il existe ou modifiez-le si nécessaire. Pour le répertoire de données par défaut `/home/$USER/.config/Lidarr`, supprimez simplement l'argument `-data`. Notez que `$USER` est l'utilisateur sous lequel Lidarr s'exécute et est défini ci-dessous.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/lidarr.service > /dev/null
[Unit]
Description=Démon Lidarr
After=syslog.target network.target
[Service]
User=lidarr
Group=media
Type=simple

ExecStart=/opt/Lidarr/Lidarr -nobrowser -data=/var/lib/lidarr/
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

- Activez le service Lidarr :

```shell
sudo systemctl enable --now -q lidarr
```

- (Facultatif) Supprimez le fichier tarball :

```shell
rm Lidarr*.linux*.tar.gz
```

Généralement, pour accéder à l'interface web de Lidarr, accédez à `http://{Adresse IP de votre serveur}:8686`

Si Lidarr ne semble pas avoir démarré, vérifiez l'état du service :

```shell
sudo journalctl --since today -u lidarr
```

---

### Désinstallation

Pour désinstaller et purger :
> Attention : Cela détruira vos données d'application. {.is-danger}

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /var/lib/lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```

Pour désinstaller et conserver vos données d'application :

```bash
sudo systemctl stop lidarr
sudo rm -rf /opt/Lidarr
sudo rm -rf /etc/systemd/system/lidarr.service
sudo systemctl -q daemon-reload
```