---
title: Installation de Readarr avec Docker
description: Guide d'installation de Readarr avec Docker
published: true
date: 2023-08-12T16:02:33.082Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:28.883Z
---

# Docker

L'équipe de Readarr ne propose pas d'image Docker officielle. Cependant, plusieurs tiers ont créé et maintiennent leurs propres images.

Les instructions suivantes fournissent des conseils génériques qui devraient s'appliquer à n'importe quelle image Docker de Readarr.

## Portainer

> **Portainer doit être évité pour la configuration des conteneurs Docker** {.is-danger}

- Portainer offre une interface graphique agréable pour gérer les conteneurs, mais c'est tout ce qu'il peut faire.
- Portainer ne devrait être utilisé que pour afficher les journaux des conteneurs Docker ou l'état des conteneurs.
- Il est fortement recommandé d'utiliser Docker Compose et de ne pas utiliser Portainer.
- Portainer présente de nombreux problèmes, tels que :
  - Ordre incorrect des sources et des cibles des montages
  - Sensibilité à la casse incohérente
  - Absence de création automatique de réseaux personnalisés pour la communication entre conteneurs
  - Implémentations de composition incohérentes sur différentes architectures
  - Télécharge toutes les balises lors de la mise à jour si aucune balise spécifique n'est définie
  - Certaines fonctionnalités sont masquées et certaines ne fonctionnent pas du tout sur les plates-formes ARM

Consultez ce [guide Docker](/docker-guide) et [le tutoriel Docker de TRaSH](https://trash-guides.info/hardlinks/) pour savoir comment configurer Docker Compose.

## Éviter les problèmes courants

### Volumes et chemins

Il existe deux problèmes courants avec les volumes Docker : les chemins qui diffèrent entre le conteneur Readarr et le conteneur du client de téléchargement, et les chemins qui empêchent les déplacements rapides et les liens physiques.

Le premier problème survient lorsque le client de téléchargement signale le chemin d'un téléchargement comme étant `/torrents/My.Movie.2018/`, mais dans le conteneur Readarr, il peut être situé à `/downloads/My.Movie.2018/`. Le deuxième problème est un problème de performance et cause des problèmes pour le partage des torrents. Les deux problèmes peuvent être résolus avec des chemins bien planifiés et cohérents.

La plupart des images Docker suggèrent des chemins tels que `/books` et `/downloads`. Cela entraîne des déplacements lents et n'autorise pas les liens physiques car ils sont considérés comme deux systèmes de fichiers différents à l'intérieur du conteneur. Certains recommandent également des chemins différents pour le conteneur du client de téléchargement par rapport au conteneur Readarr, comme `/torrents`.

La meilleure solution est d'utiliser un seul volume commun à l'intérieur des conteneurs, tel que `/data`. Vos livres seraient dans `/data/Books`, les torrents dans `/data/downloads/torrents` et/ou les téléchargements Usenet dans `/data/downloads/usenet`.

Si vous ne suivez pas ce conseil, vous devrez configurer une correspondance de chemin distant dans l'interface web de Readarr (Paramètres › Clients de téléchargement).

### Intégration de Calibre

Lors de la création d'un dossier racine, vous pouvez choisir d'utiliser ou non l'intégration de Calibre. Ce choix ne peut être fait qu'au moment de la création du dossier, et si vous choisissez de ne pas utiliser Calibre, vous ne pourrez pas l'ajouter ultérieurement. Si vous utilisez actuellement Calibre pour gérer votre bibliothèque de livres, vous devriez choisir cette option. Si vous l'utilisez, Calibre nommera et organisera vos fichiers de livres pour vous.

Si vous utilisez Calibre, vous devez d'abord démarrer le serveur de contenu Calibre (Préférences / Partage sur le net) et configurer un nom d'utilisateur et un mot de passe. Cela nécessitera un redémarrage de Calibre.

> Veuillez noter que Calibre Content Server et Calibre ne sont PAS Calibre Web. Calibre Web est un outil distinct sans rapport avec ces deux programmes, et n'est ni requis ni utilisé par Readarr de quelque manière que ce soit.
{.is-warning}

### Propriété et permissions

Les permissions et la propriété des fichiers sont l'un des problèmes les plus courants pour les utilisateurs de Readarr, à la fois à l'intérieur et à l'extérieur de Docker. La plupart des images ont des variables d'environnement qui peuvent être utilisées pour remplacer l'utilisateur, le groupe et l'umask par défaut. Vous devez décider de cela avant de configurer tous vos conteneurs. La recommandation est d'utiliser un groupe commun pour tous les conteneurs associés afin que chaque conteneur puisse utiliser les permissions de groupe partagées pour lire et écrire des fichiers sur les volumes montés.
Gardez à l'esprit que Readarr aura besoin de lire et d'écrire dans les dossiers de téléchargement ainsi que dans les dossiers finaux.

> Pour une explication plus détaillée de ces problèmes, consultez l'article wiki [The Best Docker Setup and Docker Guide](/docker-guide).
{.is-info}

## Installer Readarr

Pour installer et utiliser ces images Docker, vous devrez garder à l'esprit ce qui précède tout en suivant leur documentation. Il existe également de nombreuses façons de gérer les images et les conteneurs Docker, donc l'installation et la maintenance dépendront de la méthode que vous choisissez.

> Temporairement, vous devrez utiliser les balises :nightly ou :develop avec les images Docker, car il n'y a pas de branche principale. [Consultez cette entrée de FAQ pour connaître la signification des branches](/readarr/faq#how-do-i-update-readarr).
{.is-warning}

- [hotio/readarr](https://hotio.dev/containers/readarr/)
- [lscr.io/linuxserver/readarr](https://docs.linuxserver.io/images/docker-readarr)
{.links-list}