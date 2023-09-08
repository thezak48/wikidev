---
title: Installation de Readarr sur FreeBSD
description: Guide d'installation de Readarr sur FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

L'équipe de Readarr ne fournit que des versions pour FreeBSD. Les plugins et les ports sont maintenus et créés par la communauté FreeBSD.

Les instructions d'installation pour FreeBSD sont également maintenues par la communauté FreeBSD et toute personne possédant un compte GitHub peut mettre à jour le wiki si nécessaire.

[Lien Freshports Readarr](https://www.freshports.org/net-p2p/readarr/)

## Configuration de la prison à l'aide de l'interface graphique TrueNAS

1. Depuis l'écran principal, sélectionnez "Prisons".

1. Cliquez sur "Ajouter".

1. Cliquez sur "Création avancée de prison".

1. Nom (n'importe quel nom fera l'affaire) : Readarr.

1. Type de prison : Par défaut (Clone Jail).

1. Version : 12.2-Release (ou plus récente).

1. Configurez les propriétés de base selon vos préférences.

1. Configurez les propriétés de la prison selon vos préférences, mais ajoutez

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` est utile pour le dépannage (par exemple, ping, traceroute), mais ce n'est pas une exigence. {.is-info}

1. Configurez les propriétés réseau selon vos préférences.

1. Configurez les propriétés personnalisées selon vos préférences.

1. Cliquez sur "Enregistrer".

1. Une fois la prison créée, elle démarrera automatiquement. Une autre propriété doit être définie pour que Readarr puisse voir l'espace de stockage de vos emplacements de médias montés. Ouvrez un shell root sur le serveur et entrez ces commandes :

```shell
iocage stop <nom_de_la_prison>
iocage set enforce_statfs=1 <nom_de_la_prison>
iocage start <nom_de_la_prison>
```

## Installation de Readarr

De retour dans la liste des prisons, recherchez la prison nouvellement créée pour `readarr` et cliquez sur "Shell".

Pour installer Readarr :

> \* Assurez-vous que votre référentiel pkg est configuré pour obtenir les paquets à partir de `/latest` et non de `/quarterly`
> \* Vérifiez `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Si cela n'existe pas, copiez `/etc/pkg/FreeBSD.conf` à cet emplacement, ouvrez-le et remplacez `quarterly` par `latest`
{.is-warning}

```shell
pkg install readarr
```

Ne fermez pas encore le shell, il nous reste encore quelques choses à faire !

## Configuration de Readarr

Maintenant que nous l'avons installé, quelques étapes supplémentaires sont nécessaires.

### Configuration du service

Il est temps d'activer le service, mais avant de le faire, une note :

La mise à jour automatique est désactivée par défaut. Le `pkg-message` donne des instructions sur la façon d'activer la mise à jour automatique, mais gardez à l'esprit que cela peut casser des choses comme `pkg check -s` et `pkg remove` pour Readarr lorsque le programme de mise à jour intégré remplace les fichiers.

Pour activer le service :

```shell
sysrc readarr_enable=TRUE
```

Si vous ne souhaitez pas utiliser l'utilisateur/groupe `readarr`, vous devrez indiquer au fichier de service sous quel utilisateur/groupe il doit s'exécuter

```shell
sysrc readarr_user="UTILISATEUR_SOUHAITÉ"
```

```shell
sysrc readarr_group="GROUPE_SOUHAITÉ"
```

`readarr` stocke ses données, sa configuration, ses journaux et ses fichiers PID dans `/usr/local/readarr` par défaut. Le fichier de service créera cela et en prendra possession SI ET SEULEMENT SI IL N'EXISTE PAS. Si vous souhaitez stocker ces fichiers à un autre endroit (par exemple, un ensemble de données monté dans la prison pour des instantanés plus faciles), vous devrez le modifier à l'aide de `sysrc`

```shell
sysrc readarr_data_dir="RÉPERTOIRE_SOUHAITÉ"
```

Rappel : Si vous utilisez un emplacement existant, vous devrez manuellement soit : changer la propriété en UID/GID utilisé par `readarr` ET/OU ajouter `readarr` à un GID qui a un accès en écriture.

Presque terminé, lançons le service :

```shell
service readarr start
```

Si tout s'est déroulé comme prévu, Readarr devrait être opérationnel sur l'adresse IP de la prison (port 8787) !

Vous pouvez maintenant fermer le shell en toute sécurité.

## Dépannage

- Le service semble fonctionner, mais l'interface utilisateur ne se charge pas ou la page met du temps à se charger
  - Vérifiez que `allow_mlock` est activé dans la prison.
  
- `System.NET.Sockets.SocketException (43) : Protocol not supported`
  - Assurez-vous que vous avez activé `VNET` pour votre prison, ip6=inherit ou ip6=new.

> Le script de service devrait maintenant contourner l'absence de VNET et/ou IP6, supprimant ainsi l'exigence de VNET ou ip6=inherit. {.is-info}