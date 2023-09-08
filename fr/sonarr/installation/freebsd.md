---
title: Installation de Sonarr sur FreeBSD
description: Guide d'installation de Sonarr sur FreeBSD
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# FreeBSD

L'équipe Sonarr ne fournit des versions compilées que pour FreeBSD. Les plugins et les ports sont maintenus et créés par la communauté FreeBSD.

Les instructions d'installation pour FreeBSD sont également maintenues par la communauté FreeBSD et toute personne disposant d'un compte GitHub peut mettre à jour le wiki si nécessaire.

[Lien Freshports Sonarr](https://www.freshports.org/net-p2p/sonarr/)

## Configuration de la prison en utilisant l'interface graphique TrueNAS

1. Depuis l'écran principal, sélectionnez "Prisons".

1. Cliquez sur "Ajouter".

1. Cliquez sur "Création avancée de prison".

1. Nom (n'importe quel nom conviendra) : Sonarr.

1. Type de prison : Par défaut (clone de prison).

1. Version : 12.2-Release (ou plus récente).

1. Configurez les propriétés de base selon vos préférences.

1. Configurez les propriétés de la prison selon vos préférences, mais ajoutez

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` est utile pour le dépannage (par exemple, ping, traceroute), mais ce n'est pas une exigence. {.is-info}

1. Configurez les propriétés réseau selon vos préférences.

1. Configurez les propriétés personnalisées selon vos préférences.

1. Cliquez sur "Enregistrer".

1. Une fois la prison créée, elle démarrera automatiquement. Une autre propriété doit être définie pour que Sonarr puisse voir l'espace de stockage de vos emplacements de médias montés. Ouvrez un shell root sur le serveur et entrez ces commandes :

```shell
iocage stop <nom_de_la_prison>
iocage set enforce_statfs=1 <nom_de_la_prison>
iocage start <nom_de_la_prison>
```

## Configuration de la prison en utilisant l'interface de ligne de commande (CLI)

Suppose que iocage est installé et configuré (<https://iocage.readthedocs.io/en/latest/install.html>)
Suppose que le pont réseau iocage (vnet) est configuré (<https://iocage.readthedocs.io/en/latest/networking.html>)

Remplacez "10.0.0.100" par une adresse IPV4 libre sur votre réseau
Remplacez "13.1-RELEASE" par la version FreeBSD préférée
Remplacez "sonarr" par le nom de prison souhaité
Remplacez "accept_rtadv" ou supprimez ip6_addr si vous ne souhaitez pas configurer IPV6 automatiquement

```shell
iocage create -n "sonarr" -r 13.1-RELEASE ip4_addr="vnet0|10.0.0.100/24" vnet="on" allow_raw_sockets="1" boot="on" allow_mlock="1" ip6_addr="vnet0|accept_rtadv" enforce_statfs="1"
iocage console sonarr
```

## Installation de Sonarr Mono

De retour sur la liste des prisons, recherchez la prison nouvellement créée pour `sonarr` et cliquez sur "Shell".

Pour installer Sonarr :

> \* Assurez-vous que votre référentiel pkg est configuré pour obtenir les paquets à partir de `/latest` et non de `/quarterly`
> \* Vérifiez `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Si cela n'existe pas, copiez `/etc/pkg/FreeBSD.conf` à cet emplacement, ouvrez-le et remplacez `quarterly` par `latest`
{.is-warning}

```shell
pkg install sonarr
```

Ne fermez pas encore le shell, il nous reste encore quelques étapes !

## Installation de Sonarr .NET

De retour sur la liste des prisons, recherchez la prison nouvellement créée pour `sonarr` et cliquez sur "Shell".

Pour installer Sonarr :

> \* Assurez-vous que votre référentiel pkg est configuré pour obtenir les paquets à partir de `/latest` et non de `/quarterly`
> \* Vérifiez `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Si cela n'existe pas, copiez `/etc/pkg/FreeBSD.conf` à cet emplacement, ouvrez-le et remplacez `quarterly` par `latest`
{.is-warning}

Installez les bibliothèques suivantes pour prendre en charge Sonarr :

```shell
pkg install icu libunwind krb5 libnotify libinotify sqlite3
```

Créez l'utilisateur et le groupe Sonarr (Si vous ne souhaitez pas utiliser l'utilisateur/groupe 'sonarr', vous pouvez le modifier selon vos préférences) :

```shell
pw user add sonarr -c sonarr -u 351 -d /nonexistent -s /usr/bin/nologin
```

Téléchargez la dernière version depuis <https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64> et définissez ses autorisations :

```shell
curl -J -L "https://services.sonarr.tv/v1/download/develop/latest?version=4&os=freebsd&arch=x64" -o Sonarr.develop.freebsd-x64.tar.gz
tar -xvf Sonarr.develop.freebsd-x64.tar.gz -C /usr/local/share
chown -R sonarr:sonarr /usr/local/share/Sonarr
```

Créez un script rc.subr pour exécuter Sonarr en tant que démon dans un éditeur de votre choix (vous pouvez peut-être sauter la ligne 1 si le dossier existe déjà) et utilisez le contenu du fichier rc.subr de Sonarr ci-dessous :

```shell
mkdir -p /usr/local/etc/rc.d
vi /usr/local/etc/rc.d/sonarr
chmod +x /usr/local/etc/rc.d/sonarr
```

```shell
#!/bin/sh

# PROVIDE: sonarr
# REQUIRE: LOGIN
# KEYWORD: shutdown
#
# Ajoutez les lignes suivantes à /etc/rc.conf.local ou /etc/rc.conf
# pour activer ce service :
#
# sonarr_enable:   Défini sur yes pour activer le service Sonarr.
#                       Par défaut : no
# sonarr_user:     Le compte utilisateur utilisé pour exécuter le démon Sonarr.
#                       C'est facultatif, cependant ne le définissez pas spécifiquement sur une
#                       chaîne vide car cela fera fonctionner le démon en tant que root.
#                       Par défaut : sonarr
# sonarr_group:    Le groupe utilisé pour exécuter le démon Sonarr.
#                       C'est facultatif, cependant ne le définissez pas spécifiquement sur une
#                       chaîne vide car cela fera fonctionner le démon avec le groupe wheel.
#                       Par défaut : sonarr
# sonarr_data_dir: Répertoire où les données de configuration de Sonarr sont stockées.
#                       Par défaut : /var/db/sonarr
# sonarr_pid:      Nom du fichier PID.
#                       Par défaut : sonarr.pid
# sonarr_pid_dir:  Chemin du fichier PID.
#                       Par défaut : /var/run/sonarr

. /etc/rc.subr
name=sonarr
rcvar=${name}_enable
load_rc_config ${name}

: ${sonarr_enable:="no"}
: ${sonarr_user:="sonarr"}
: ${sonarr_group:="sonarr"}
: ${sonarr_data_dir:="/var/db/sonarr"}
: ${sonarr_pid:="sonarr.pid"}
: ${sonarr_pid_dir:="/var/run/sonarr"}

pidfile="${sonarr_pid_dir}/${sonarr_pid}"
command="/usr/sbin/daemon"
command_args="-r -f -P ${pidfile} /usr/local/share/Sonarr/Sonarr --debug --data=${sonarr_data_dir} --nobrowser"

start_precmd=sonarr_start_precmd
sonarr_start_precmd()
{
 [ -d ${sonarr_pid_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_pid_dir}
 [ -d ${sonarr_data_dir} ] || install -d -g ${sonarr_group} -o ${sonarr_user} ${sonarr_data_dir}

 # .NET 6+ utilise des sockets en mode double pour éviter la gestion séparée de AF.
 # désactivez l'utilisation de V6 par .NET si aucune ipv6 n'est configurée.
 # Voir https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=259194#c17
 ifconfig | grep -q inet6
 if [ $? == 1 ]; then
  export DOTNET_SYSTEM_NET_DISABLEIPV6=1
 fi
}

run_rc_command "$1"
```

Ne fermez pas encore le shell, il nous reste encore quelques étapes !

## Configuration de Sonarr

Maintenant que nous l'avons installé, quelques étapes supplémentaires sont nécessaires.

### Configuration du service

Il est temps d'activer le service, mais avant de le faire, une note :

La mise à jour automatique est désactivée par défaut. Le fichier `pkg-message` donne des instructions sur la façon d'activer la mise à jour automatique, mais gardez à l'esprit que cela peut casser des choses comme `pkg check -s` et `pkg remove` pour Sonarr lorsque le programme de mise à jour intégré remplace les fichiers.

Pour activer le service :

```shell
sysrc sonarr_enable=TRUE
```

Si vous ne souhaitez pas utiliser l'utilisateur/groupe `sonarr`, vous devrez indiquer au fichier de service l'utilisateur/groupe sous lequel il doit s'exécuter :

```shell
sysrc sonarr_user="UTILISATEUR_SOUHAITÉ"
```

```shell
sysrc sonarr_group="GROUPE_SOUHAITÉ"
```

`sonarr` stocke ses données, sa configuration, ses journaux et ses fichiers PID dans `/usr/local/sonarr` par défaut. Le fichier de service créera ce répertoire et en prendra possession SI ET SEULEMENT S'IL N'EXISTE PAS. Si vous souhaitez stocker ces fichiers dans un autre emplacement (par exemple, un ensemble de données monté dans la prison pour faciliter les instantanés), vous devrez le modifier à l'aide de `sysrc` :

```shell
sysrc sonarr_data_dir="RÉPERTOIRE_SOUHAITÉ"
```

Rappel : Si vous utilisez un emplacement existant, vous devrez manuellement : changer la propriété en UID/GID utilisé par `sonarr` ET/OU ajouter `sonarr` à un GID qui a un accès en écriture.

Presque terminé, lançons le service :

```shell
service sonarr start
```

Si tout s'est déroulé comme prévu, Sonarr devrait être opérationnel sur l'adresse IP de la prison (port 8989) !

Vous pouvez maintenant fermer le shell en toute sécurité.

## Dépannage

- Le service semble fonctionner mais l'interface utilisateur ne se charge pas ou la page met du temps à se charger
  - Vérifiez que `allow_mlock` est activé dans la prison.
  
- `System.NET.Sockets.SocketException (43) : Protocole non pris en charge`
  - Assurez-vous que vous avez activé `VNET` pour votre prison, ip6=inherit ou ip6=new

> Le script de service devrait maintenant contourner l'absence de VNET et/ou IP6, supprimant ainsi l'exigence de VNET ou ip6=inherit
{.is-info}

### Problèmes SSL de BSD Mono

- Problèmes SSL ou autres problèmes de certificat (par exemple, `unable to verify SSL certificate`)
  - Consultez [ce message du forum TrueNAS car vous devrez mettre à jour et synchroniser les certificats de mono](https://www.truenas.com/community/threads/sonarr-radarr-probably-other-arr-jails-unable-to-verify-ssl-certificates-after-latest-update.96008/)