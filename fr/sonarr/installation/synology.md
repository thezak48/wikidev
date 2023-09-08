---
title: Installation de Sonarr sur Synology
description: Guide d'installation de Sonarr sur Synology
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [La communauté SynoCommunity crée, prend en charge et maintient un package Synology NAS](https://synocommunity.com/package/nzbdrone)

> Le package NAS est mal maintenu et souvent obsolète. Si votre NAS prend en charge Docker, il est fortement recommandé [d'exécuter Docker](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/) à la place. Vous ne pourrez pas réinstaller Sonarr sans effacer manuellement votre base de données en raison de l'obsolescence du package NAS et de l'absence de configuration pour les mises à jour automatiques au démarrage. {.is-info}

- [SynoCommunity crée également, prend en charge et maintient le package Mono requis](https://synocommunity.com/package/mono)

## Erreurs SSL Mono Synology

> En raison d'un bogue introduit par le package Mono mal maintenu de SynoCommunity, Sonarr échouera à se connecter après la mise à jour de Mono ou après une installation fraîche. Cela peut être résolu en suivant les instructions de [SynoCommunity Bug Report #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625). Notez que, selon [ce commentaire](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799), les utilisateurs de DSM7 ont une étape supplémentaire.
{.is-danger}

1. Dans DSM, activez le service SSH dans *Panneau de configuration => Terminal & SNMP* et cliquez sur Appliquer.
1. À l'aide de [Terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) (MacOS), connectez-vous au NAS en utilisant `ssh -l [nom d'utilisateur admin] [adresse NAS]` ou en utilisant [Putty](https://www.putty.org/) (Windows), connectez-vous à l'adresse réseau de votre NAS.
1. Entrez le mot de passe admin requis et appuyez sur Entrée.
1. Entrez la ou les commandes appropriées pour votre version de DSM indiquées ci-dessous et appuyez sur Entrée.
1. Entrez le mot de passe admin requis et appuyez sur Entrée. Lorsque vous avez terminé, vous devriez voir la ligne *Import process completed*.
1. Déconnectez la session SSH en tapant `exit` et appuyez sur Entrée.
1. Dans DSM, désactivez le service SSH dans *Panneau de configuration => Terminal & SNMP* et cliquez sur Appliquer.
1. Une fois terminé, les erreurs dans Sonarr devraient disparaître d'elles-mêmes en quelques minutes.

### Commande de correction Mono Synology DSM6

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Commande de correction Mono Synology DSM7

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```