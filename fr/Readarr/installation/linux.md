---
title: Installation de Readarr sur Linux
description: Guide d'installation de Readarr sur Linux
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

**Pour les instructions d'installation officielles qui sont "pratiques", suivez les étapes [Debian / Ubuntu Hands on Install](#debian-ubuntu-hands-on-install) ci-dessous.**

[Veuillez consulter le script d'installation de la communauté \*Arr](/install-script)

### Installation pratique de Debian / Ubuntu

Vous devrez installer les binaires en utilisant les commandes ci-dessous.

> Les étapes ci-dessous téléchargeront Readarr et l'installeront dans `/opt`
> Readarr s'exécutera sous l'utilisateur `readarr` et le groupe `media`; `media` est le groupe couramment suggéré pour exécuter les \*Arrs, les clients de téléchargement et le serveur multimédia.
> Les fichiers de configuration de Readarr seront stockés dans `/var/lib/readarr`
{.is-warning}

- Assurez-vous d'avoir les paquets prérequis nécessaires :

```shell
sudo apt install curl sqlite3
```

> Attention : Ignorer les prérequis ci-dessous entraînera une installation échouée et une application non fonctionnelle. {.is-warning}

> **Prérequis d'installation**
> Les instructions ci-dessous sont basées sur les prérequis suivants. Modifiez les instructions si nécessaire pour répondre à vos besoins spécifiques.
> \* L'utilisateur `readarr` est créé
> \* L'utilisateur `readarr` fait partie du groupe `media`
> \* Vos clients de téléchargement et votre serveur multimédia s'exécutent en tant que membres du groupe `media`
> \* Les chemins utilisés par vos clients de téléchargement et votre serveur multimédia sont accessibles (lecture/écriture) par le groupe `media`
> \* Si Calibre est utilisé, Calibre s'exécute en tant que groupe `media` et la bibliothèque Calibre a des autorisations de lecture/écriture pour `media`
> \* Vous avez créé le répertoire `/var/lib/readarr` et vous avez vérifié que l'utilisateur `readarr` dispose des autorisations de lecture/écriture pour celui-ci
{.is-danger}

> En continuant ci-dessous, vous reconnaissez avoir lu et satisfait aux exigences ci-dessus. {.is-warning}

- Téléchargez les binaires corrects pour votre architecture.
  - Vous pouvez déterminer votre architecture avec `dpkg --print-architecture`
    - AMD64 utilisez `arch=x64`
    - ARM, armf et armh utilisez `arch=arm`
    - ARM64 utilisez `arch=arm64`

```shell
wget --content-disposition 'http://readarr.servarr.com/v1/update/develop/updatefile?os=linux&runtime=netcore&arch=x64'
```

- Décompressez les fichiers :

```shell
tar -xvzf Readarr*.linux*.tar.gz
```

- Déplacez les fichiers vers `/opt/`

```shell
sudo mv Readarr /opt/
```

> Remarque : Cela suppose que vous avez créé l'utilisateur et qu'il s'exécutera en tant qu'utilisateur `readarr` et groupe `media`. Vous pouvez modifier cela pour correspondre à votre cas d'utilisation. Il est important de choisir correctement ces paramètres pour éviter les problèmes de permissions avec vos fichiers multimédias. Nous vous suggérons de garder au moins le nom du groupe identique entre votre client de téléchargement(s) et Readarr. Veuillez noter que si vous souhaitez utiliser Calibre, Readarr aura besoin des autorisations pour ce répertoire.
{.is-danger}

- Assurez-vous que le répertoire binaire appartient à l'utilisateur.

```shell  
sudo chown readarr:readarr -R /opt/Readarr
```

- Configurez systemd pour que Readarr démarre automatiquement au démarrage.

> Le script de création systemd ci-dessous utilisera un répertoire de données `/var/lib/readarr`. Assurez-vous qu'il existe ou modifiez-le si nécessaire. Pour le répertoire de données par défaut `/home/$USER/.config/Readarr`, supprimez simplement l'argument `-data`. Notez que `$USER` est l'utilisateur sous lequel Readarr s'exécute et est défini ci-dessous.
{.is-danger}

```shell
cat << EOF | sudo tee /etc/systemd/system/readarr.service > /dev/null
[Unit]
Description=Démon Readarr
After=syslog.target network.target
[Service]
User=readarr
Group=media
Type=simple

ExecStart=/opt/Readarr/Readarr -nobrowser -data=/var/lib/readarr/
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

- Activez le service Readarr :

```shell
sudo systemctl enable --now -q readarr
```

- (Facultatif) Supprimez le fichier tarball :

```shell
rm Readarr*.linux*.tar.gz
```

Généralement, pour accéder à l'interface utilisateur Web de Readarr, accédez à `http://{Votre adresse IP du serveur}:8787`

Si Readarr ne semble pas avoir démarré, vérifiez l'état du service :

```shell
sudo journalctl --since today -u readarr
```

---

### Désinstallation

Pour désinstaller et purger :
> Attention : Cela détruira vos données d'application. {.is-danger}

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /var/lib/readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```

Pour désinstaller et conserver vos données d'application :

```bash
sudo systemctl stop readarr
sudo rm -rf /opt/Readarr
sudo rm -rf /etc/systemd/system/readarr.service
sudo systemctl -q daemon-reload
```