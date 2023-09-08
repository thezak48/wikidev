---
title: Installation de Prowlarr sur Linux
description: Guide d'installation de Prowlarr sur Linux
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

Si vous voulez une installation facile, suivez ce script d'installation fourni et maintenu par la communauté pour une installation de base de Debian (Raspbian / Raspberry Pi OS) / Ubuntu.

**Pour les instructions d'installation officielles qui sont "pratiques", suivez les étapes d'installation de [Debian / Ubuntu Hands on](#debian-ubuntu-hands-on-install) ci-dessous.**

[Veuillez consulter le script d'installation de la communauté \*Arr](/install-script)

### Installation pratique de Debian / Ubuntu

Vous devrez installer les binaires en utilisant les commandes ci-dessous.

> Les étapes ci-dessous téléchargeront Prowlarr et l'installeront dans `/opt`
> Prowlarr s'exécutera sous l'utilisateur `prowlarr` et le groupe `prowlarr`
> Les fichiers de configuration de Prowlarr seront stockés dans `/var/lib/prowlarr`
{.is-warning}

- Assurez-vous d'avoir les paquets prérequis nécessaires :

```shell
sudo apt install curl sqlite3
```

> Attention : Ignorer les prérequis ci-dessous entraînera une installation échouée et une application non fonctionnelle. {.is-warning}

> **Prérequis d'installation**
> Les instructions ci-dessous sont basées sur les prérequis suivants. Modifiez les instructions si nécessaire pour répondre à vos besoins spécifiques.
> \* L'utilisateur `prowlarr` est créé
> \* Vous avez créé le répertoire `/var/lib/prowlarr` et vous avez assuré que l'utilisateur `prowlarr` a les permissions de lecture/écriture pour celui-ci
{.is-danger}

> En continuant ci-dessous, vous reconnaissez avoir lu et satisfait aux exigences ci-dessus. {.is-warning}

- Téléchargez les binaires corrects pour votre architecture.
  - Vous pouvez déterminer votre architecture avec `dpkg --print-architecture`
    - AMD64 utilisez `arch=x64`
    - ARM, armf et armh utilisez `arch=arm`
    - ARM64 utilisez `arch=arm64`

```shell
wget --content-disposition 'http://prowlarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Décompressez les fichiers :

```shell
tar -xvzf Prowlarr*.linux*.tar.gz
```

- Déplacez les fichiers vers `/opt/`

```shell
sudo mv Prowlarr/ /opt
```

> Cela suppose que vous avez créé l'utilisateur et qu'il s'exécutera en tant qu'utilisateur `prowlarr` et groupe `prowlarr`. Vous pouvez modifier cela en fonction de votre cas d'utilisation.
{.is-danger}

- Assurez-vous de posséder le répertoire binaire.

```shell  
sudo chown prowlarr:prowlarr -R /opt/Prowlarr
```

- Configurez systemd pour que Prowlarr démarre automatiquement au démarrage.

> Le script de création systemd ci-dessous utilisera un répertoire de données `/var/lib/prowlarr`. Assurez-vous qu'il existe ou modifiez-le si nécessaire. Pour le répertoire de données par défaut `/home/$USER/.config/Prowlarr`, supprimez simplement l'argument `-data`. Notez que `$USER` est l'utilisateur sous lequel Prowlarr s'exécute et est défini ci-dessous.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/prowlarr.service > /dev/null
[Unit]
Description=Démon Prowlarr
After=syslog.target network.target
[Service]
User=prowlarr
Group=prowlarr
Type=simple

ExecStart=/opt/Prowlarr/Prowlarr -nobrowser -data=/var/lib/prowlarr/
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

- Activez le service Prowlarr :

```shell
sudo systemctl enable --now -q prowlarr
```

- (Facultatif) Supprimez le fichier tarball :

```shell
rm Prowlarr*.linux*.tar.gz
```

Généralement, pour accéder à l'interface web de Prowlarr, accédez à `http://{Votre adresse IP du serveur}:9696`

Si Prowlarr ne semble pas avoir démarré, vérifiez l'état du service :

```shell
sudo journalctl --since today -u prowlarr
```

---

### Désinstallation

Pour désinstaller et purger :
> Attention : Cela détruira vos données d'application. {.is-danger}

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /var/lib/prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```

Pour désinstaller et conserver vos données d'application :

```bash
sudo systemctl stop prowlarr
sudo rm -rf /opt/Prowlarr
sudo rm -rf /etc/systemd/system/prowlarr.service
sudo systemctl -q daemon-reload
```