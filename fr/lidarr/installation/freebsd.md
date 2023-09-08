---
title: Installation de Lidarr sur FreeBSD
description: Guide d'installation de Lidarr sur FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

L'équipe de Lidarr ne fournit des versions compilées que pour FreeBSD. Les plugins et les ports sont maintenus et créés par la communauté FreeBSD.

Les instructions d'installation pour FreeBSD sont également maintenues par la communauté FreeBSD et toute personne possédant un compte GitHub peut mettre à jour le wiki si nécessaire.

[Lien Freshports Lidarr](https://www.freshports.org/net-p2p/lidarr/)

## Configuration de la prison en utilisant l'interface graphique TrueNAS

1. Depuis l'écran principal, sélectionnez "Prisons".

1. Cliquez sur "Ajouter".

1. Cliquez sur "Création avancée de prison".

1. Nom (n'importe quel nom fera l'affaire) : Lidarr.

1. Type de prison : Par défaut (Clone de prison).

1. Version : 12.2-Release (ou plus récente).

1. Configurez les propriétés de base selon vos préférences.

1. Configurez les propriétés de la prison selon vos préférences, mais ajoutez

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` est utile pour le dépannage (par exemple, ping, traceroute), mais ce n'est pas une exigence. {.is-info}

1. Configurez les propriétés réseau selon vos préférences.

1. Configurez les propriétés personnalisées selon vos préférences.

1. Cliquez sur "Enregistrer".

1. Une fois la prison créée, elle démarrera automatiquement. Une autre propriété doit être définie pour que Lidarr puisse voir l'espace de stockage de vos emplacements de médias montés. Ouvrez un shell root sur le serveur et entrez ces commandes :

```shell
iocage stop <nom_de_la_prison>
iocage set enforce_statfs=1 <nom_de_la_prison>
iocage start <nom_de_la_prison>
```

## Installation de Lidarr

De retour sur la liste des prisons, recherchez la prison nouvellement créée pour `lidarr` et cliquez sur "Shell".

Pour installer Lidarr

> \* Assurez-vous que votre référentiel pkg est configuré pour obtenir les paquets à partir de `/latest` et non de `/quarterly`
> \* Vérifiez `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Si cela n'existe pas, copiez `/etc/pkg/FreeBSD.conf` à cet emplacement, ouvrez-le et remplacez `quarterly` par `latest`
{.is-warning}

```shell
pkg install lidarr
```

Ne fermez pas encore le shell, il nous reste encore quelques choses à faire !

## Configuration de Lidarr

Maintenant que nous l'avons installé, quelques étapes supplémentaires sont nécessaires.

### Configuration du service

Il est temps d'activer le service, mais avant de le faire, une note :

La mise à jour automatique est désactivée par défaut. Le `pkg-message` donne des instructions sur la façon d'activer la mise à jour automatique, mais gardez à l'esprit que cela peut casser des choses comme `pkg check -s` et `pkg remove` pour Lidarr lorsque le programme de mise à jour intégré remplace des fichiers.

Pour activer le service :

```shell
sysrc lidarr_enable=TRUE
```

Si vous ne souhaitez pas utiliser l'utilisateur/groupe `lidarr`, vous devrez indiquer au fichier de service sous quel utilisateur/groupe il doit s'exécuter

```shell
sysrc lidarr_user="UTILISATEUR_SOUHAITÉ"
```

```shell
sysrc lidarr_group="GROUPE_SOUHAITÉ"
```

`lidarr` stocke ses données, sa configuration, ses journaux et ses fichiers PID dans `/usr/local/lidarr` par défaut. Le fichier de service créera cela et en prendra possession SI ET SEULEMENT SI IL N'EXISTE PAS. Si vous souhaitez stocker ces fichiers dans un autre emplacement (par exemple, un ensemble de données monté dans la prison pour des instantanés plus faciles), vous devrez le modifier à l'aide de `sysrc`

```shell
sysrc lidarr_data_dir="EMPLACEMENT_SOUHAITÉ"
```

Rappel : Si vous utilisez un emplacement existant, vous devrez manuellement soit : changer la propriété en UID/GID utilisé par `lidarr` ET/OU ajouter `lidarr` à un GID qui a un accès en écriture.

Presque terminé, lançons le service :

```shell
service lidarr start
```

Si tout s'est déroulé comme prévu, Lidarr devrait être opérationnel sur l'adresse IP de la prison (port 8686) !

Vous pouvez maintenant fermer le shell en toute sécurité.

## Dépannage

- Le service semble fonctionner, mais l'interface utilisateur ne se charge pas ou la page dépasse le délai d'attente
  - Vérifiez à nouveau que `allow_mlock` est activé dans la prison.
  
- `System.NET.Sockets.SocketException (43) : Protocole non pris en charge`
  - Assurez-vous que vous avez activé `VNET` pour votre prison, ip6=inherit ou ip6=new

> Le script de service devrait maintenant contourner l'absence de VNET et/ou IP6, supprimant ainsi l'exigence de VNET ou ip6=inherit
{.is-info}