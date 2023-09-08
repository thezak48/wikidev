---
title: Installation de Prowlarr sur FreeBSD
description: Guide d'installation de Prowlarr sur FreeBSD
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# FreeBSD

L'équipe de Prowlarr ne fournit des versions compilées que pour FreeBSD. Les plugins et les ports sont maintenus et créés par la communauté FreeBSD.

Les instructions d'installation pour FreeBSD sont également maintenues par la communauté FreeBSD et toute personne possédant un compte GitHub peut mettre à jour le wiki si nécessaire.

[Lien Freshports Prowlarr](https://www.freshports.org/net-p2p/prowlarr/)

## Configuration de la prison en utilisant l'interface graphique TrueNAS

1. Depuis l'écran principal, sélectionnez "Prisons".

1. Cliquez sur "Ajouter".

1. Cliquez sur "Création avancée de prison".

1. Nom (n'importe quel nom fera l'affaire) : Prowlarr.

1. Type de prison : Par défaut (Cloner la prison).

1. Version : 12.2-Release (ou plus récente).

1. Configurez les propriétés de base selon vos préférences.

1. Configurez les propriétés de la prison selon vos préférences, mais ajoutez

- [x] allow_mlock

- [x] allow_raw_sockets

> `allow_raw_sockets` est utile pour le dépannage (par exemple, ping, traceroute), mais ce n'est pas une exigence. {.is-info}

1. Configurez les propriétés réseau selon vos préférences.

1. Configurez les propriétés personnalisées selon vos préférences.

1. Cliquez sur "Enregistrer".

## Installation de Prowlarr

De retour dans la liste des prisons, recherchez la prison que vous venez de créer pour `prowlarr` et cliquez sur "Shell".

Pour installer Prowlarr :

> \* Assurez-vous que votre référentiel pkg est configuré pour obtenir les paquets à partir de `/latest` et non de `/quarterly`
> \* Vérifiez `/usr/local/etc/pkg/repos/FreeBSD.conf`
> \* Si cela n'existe pas, copiez `/etc/pkg/FreeBSD.conf` à cet emplacement, ouvrez-le et remplacez `quarterly` par `latest`
{.is-warning}

```shell
pkg install prowlarr
```

Ne fermez pas encore le shell, nous avons encore quelques étapes à suivre !

## Configuration de Prowlarr

Maintenant que nous l'avons installé, quelques étapes supplémentaires sont nécessaires.

### Configuration du service

Il est temps d'activer le service, mais avant de le faire, une note :

La mise à jour automatique est désactivée par défaut. Le `pkg-message` donne des instructions sur la façon d'activer la mise à jour automatique, mais gardez à l'esprit que cela peut casser des choses comme `pkg check -s` et `pkg remove` pour prowlarr lorsque le programme de mise à jour intégré remplace les fichiers.

Pour activer le service :

```shell
sysrc prowlarr_enable=TRUE
```

Si vous ne souhaitez pas utiliser l'utilisateur/groupe `prowlarr`, vous devrez indiquer au fichier de service sous quel utilisateur/groupe il doit s'exécuter

```shell
sysrc prowlarr_user="UTILISATEUR_DE_VOTRE_CHOIX"
```

```shell
sysrc prowlarr_group="GROUPE_DE_VOTRE_CHOIX"
```

`prowlarr` stocke ses données, sa configuration, ses journaux et ses fichiers PID dans `/usr/local/prowlarr` par défaut. Le fichier de service créera ce répertoire et en prendra possession SI ET SEULEMENT SI IL N'EXISTE PAS. Si vous souhaitez stocker ces fichiers dans un autre emplacement (par exemple, un ensemble de données monté dans la prison pour faciliter les instantanés), vous devrez le modifier à l'aide de `sysrc`

```shell
sysrc prowlarr_data_dir="RÉPERTOIRE_DE_VOTRE_CHOIX"
```

Rappel : Si vous utilisez un emplacement existant, vous devrez manuellement soit : changer la propriété en UID/GID utilisé par `prowlarr` ET/OU ajouter `prowlarr` à un GID qui a un accès en écriture.

Presque terminé, lançons le service :

```shell
service prowlarr start
```

Si tout s'est déroulé comme prévu, prowlarr devrait être en cours d'exécution sur l'adresse IP de la prison (port 9696) !

Vous pouvez maintenant fermer le shell en toute sécurité.

## Dépannage

- Le service semble être en cours d'exécution, mais l'interface utilisateur ne se charge pas ou la page dépasse le délai d'attente.
  - Vérifiez à nouveau que `allow_mlock` est activé dans la prison.
  
- `System.NET.Sockets.SocketException (43) : Protocole non pris en charge`
  - Assurez-vous que vous avez activé `VNET` pour votre prison, ip6=inherit ou ip6=new.

> Le script de service devrait maintenant contourner l'absence de VNET et/ou IP6, supprimant ainsi l'exigence de VNET ou ip6=inherit. {.is-info}