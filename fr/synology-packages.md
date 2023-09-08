---
title: Packages Synology de Servarr
description: Packages Synology de Servarr
published: true
date: 2022-06-23T19:58:34.255Z
tags: lidarr, prowlarr, synology, radarr,readarr,sonarr
editor: markdown
dateCreated: 2022-05-06T13:45:19.731Z
---

- [Packages Synology de Servarr](#packages-synology-de-servarr)
- [DSM 6.x](#dsm-6x)
- [DSM 7.x](#dsm-7x)
  - [Installation de Bubblewrap sur DSM 7.X](#installation-de-bubblewrap-sur-dsm-7x)
    - [Installation simple de Bubblewrap](#installation-simple-de-bubblewrap)
    - [Installation manuelle de Bubblewrap](#installation-manuelle-de-bubblewrap)

# Packages Synology de Servarr

> Ces packages peuvent être considérés comme "bêta"
{.is-danger}

- L'équipe de Servarr crée et maintient désormais les packages Synology.
- Les instructions d'installation sont indiquées ci-dessous pour les versions spécifiques de DSM.

> En général, les versions existantes de SynoCommunity ne sont pas compatibles avec les versions de Servarr sans quelques manipulations. Cela signifie qu'il serait nécessaire de supprimer l'ancien package après avoir effectué une [sauvegarde de votre base de données *le lien est pour un exemple avec Radarr, mais les instructions/concepts sont les mêmes*](/radarr/faq#how-do-i-backuprestore-radarr). Cela peut être fait via l'interface web de l'application \*Arr.
{.is-warning}

> SynoCommunity dispose d'une liste des [NAS par architecture](https://github.com/SynoCommunity/spksrc/wiki/Architecture-per-Synology-model) qui vous aidera à identifier le package correct.
{.is-info}

# DSM 6.x

- Les packages Lidarr-Official, Prowlarr-Official, Radarr-Official, Readarr-Official et Sonarr devraient *fonctionner simplement*.
- Notez que le package Mono autonome de SynoCommunity n'est plus nécessaire, il est actuellement inclus dans notre package.
- Téléchargez la version de l'application correspondant à l'architecture de votre NAS depuis [le référentiel GitHub des packages Synology de Servarr](https://github.com/Servarr/spksrc/releases) et [installez manuellement le package](https://kb.synology.com/fr-fr/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via le gestionnaire de packages.

# DSM 7.x

- Les packages Lidarr-Official, Prowlarr-Official, Radarr-Official et Readarr-Official devraient *fonctionner simplement* pour la plupart des architectures.
  - Notez qu'un NAS avec `comcerto2k` nécessite des étapes supplémentaires pour Lidarr, Prowlarr, Radarr et Readarr ; [consultez les instructions](#installation-de-bubblewrap-sur-dsm-7x).
- Notez que le package Sonarr nécessite des étapes supplémentaires pour **toutes** les architectures.
- Notez que le package Mono autonome de SynoCommunity n'est plus nécessaire, il est actuellement inclus dans notre package.

> Pour les NAS exécutant `comcerto2k` (*tous les packages*) et Sonarr (*toutes les architectures de NAS*), vous devrez installer le package Bubblewrap et effectuer les étapes manuelles indiquées. **Bubblewrap doit être installé avant de tenter d'installer les packages \*Arr**
{.is-warning}

- Téléchargez la version de Bubblewrap correspondant à l'architecture de votre NAS depuis [le référentiel GitHub des packages Synology de Servarr](https://github.com/Servarr/spksrc/releases) et [installez manuellement le package](https://kb.synology.com/fr-fr/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via le gestionnaire de packages.
- Effectuez les étapes d'installation de Bubblewrap ci-dessous pour DSM 7.X.
- Une fois Bubblewrap installé, vous pouvez télécharger la version de l'application correspondant à l'architecture de votre NAS depuis [le référentiel GitHub des packages Synology de Servarr](https://github.com/Servarr/spksrc/releases) et [installez manuellement le package](https://kb.synology.com/fr-fr/DSM/tutorial/How_to_install_applications_with_Package_Center#x_anchor_id6) via le gestionnaire de packages.

## Installation de Bubblewrap sur DSM 7.X

Bubblewrap nous permet d'exécuter des programmes dans un conteneur de base afin que nous puissions utiliser des bibliothèques suffisamment récentes pour exécuter .NET6.

> **En raison des restrictions de DSM 7.0+, une configuration manuelle est requise après l'installation.**
{.is-danger}

### Installation simple de Bubblewrap

1. Créez une tâche déclenchée dans DSM :

- Utilisateur : `root`
  - Événement : `Démarrage`

1. Pour la commande `Exécuter`, entrez :

```bash
chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```

1. Enregistrez la tâche déclenchée et exécutez-la une fois.

![triggered_task.png](/assets/synology/triggered_task.png)

![create_task1.png](/assets/synology/create_task1.png)

![create_task2.png](/assets/synology/create_task2.png)

![run_task.png](/assets/synology/run_task.png)

### Installation manuelle de Bubblewrap

1. [Connectez-vous à votre Synology via SSH et passez en mode `root`](https://kb.synology.com/fr-fr/DSM/tutorial/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet)
1. Exécutez les commandes suivantes :

```bash
sudo chown root:root /volume1/@appstore/bubblewrap/bin/bwrap
```

```bash
chmod u+s /volume1/@appstore/bubblewrap/bin/bwrap
```