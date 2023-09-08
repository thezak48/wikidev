---
title: Installation de Lidarr avec Docker
description: Guide d'installation de Lidarr avec Docker
published: true
date: 2023-08-12T16:03:02.989Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:10:37.188Z
---

# Docker

L'équipe de Lidarr ne propose pas d'image Docker officielle. Cependant, plusieurs tiers ont créé et maintiennent leurs propres images.

Les instructions suivantes fournissent des conseils génériques qui devraient s'appliquer à n'importe quelle image Docker de Lidarr.

## Portainer

> **Portainer doit être évité pour la configuration des conteneurs Docker** {.is-danger}

- Portainer offre une interface graphique agréable pour gérer les conteneurs, mais c'est tout ce qu'il est utile de faire.
- Portainer ne devrait être utilisé que pour afficher les journaux des conteneurs Docker ou l'état des conteneurs.
- Il est fortement recommandé d'utiliser Docker Compose et de ne pas utiliser Portainer.
- Portainer présente de nombreux problèmes, tels que :
  - Ordre incorrect des sources et des cibles des montages
  - Sensibilité à la casse incohérente
  - Absence de création automatique de réseaux personnalisés pour la communication entre conteneurs
  - Implémentations de Docker Compose incohérentes sur différentes architectures
  - Télécharge toutes les balises lors de la mise à jour si aucune balise spécifique n'est définie
  - Certaines fonctionnalités sont masquées et certaines ne fonctionnent pas du tout sur les plates-formes ARM

Consultez ce [Guide Docker](/docker-guide) et [le Tutoriel Docker de TRaSH](https://trash-guides.info/hardlinks/) pour savoir comment configurer Docker Compose.

## Éviter les problèmes courants

### Volumes et chemins

Il existe deux problèmes courants avec les volumes Docker : les chemins qui diffèrent entre le conteneur Lidarr et le conteneur du client de téléchargement, et les chemins qui empêchent les déplacements rapides et les liens physiques.

Le premier problème est dû au fait que le client de téléchargement indiquera le chemin d'un téléchargement comme étant `/torrents/My.Music.2018/`, mais dans le conteneur Lidarr, cela pourrait être `/downloads/My.Music.2018/`. Le deuxième problème est un problème de performance et cause des problèmes pour le partage des torrents. Les deux problèmes peuvent être résolus avec des chemins bien planifiés et cohérents.

La plupart des images Docker suggèrent des chemins tels que `/music` et `/downloads`. Cela entraîne des déplacements lents et n'autorise pas les liens physiques car ils sont considérés comme deux systèmes de fichiers différents à l'intérieur du conteneur. Certains recommandent également des chemins différents pour le conteneur du client de téléchargement par rapport au conteneur Lidarr, comme `/torrents`.

La meilleure solution est d'utiliser un seul volume commun à l'intérieur des conteneurs, tel que `/data`. Votre musique serait dans `/data/Music`, les torrents dans `/data/downloads/torrents` et/ou les téléchargements Usenet dans `/data/downloads/usenet`.

Si vous ne suivez pas ce conseil, vous devrez configurer une correspondance de chemin distant dans l'interface web de Lidarr (Paramètres › Clients de téléchargement).

### Propriété et permissions

Les permissions et la propriété des fichiers sont l'un des problèmes les plus courants pour les utilisateurs de Lidarr, à la fois à l'intérieur et à l'extérieur de Docker. La plupart des images disposent de variables d'environnement qui peuvent être utilisées pour remplacer l'utilisateur, le groupe et l'umask par défaut. Vous devriez décider de cela avant de configurer tous vos conteneurs. La recommandation est d'utiliser un groupe commun pour tous les conteneurs associés afin que chaque conteneur puisse utiliser les permissions de groupe partagées pour lire et écrire des fichiers sur les volumes montés.
Gardez à l'esprit que Lidarr aura besoin de lire et d'écrire dans les dossiers de téléchargement ainsi que dans les dossiers finaux.

> Pour une explication plus détaillée de ces problèmes, consultez l'article wiki [The Best Docker Setup and Docker Guide](/docker-guide) (en anglais).
{.is-info}

## Installer Lidarr

Pour installer et utiliser ces images Docker, vous devrez garder à l'esprit ce qui précède tout en suivant leur documentation. Il existe de nombreuses façons de gérer les images et les conteneurs Docker, donc l'installation et la maintenance dépendront de la méthode que vous choisissez.

- [hotio/lidarr](https://hotio.dev/containers/lidarr/) (en anglais)
- [lscr.io/linuxserver/lidarr](https://docs.linuxserver.io/images/docker-lidarr) (en anglais)
{.links-list}