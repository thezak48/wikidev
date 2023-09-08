---
title: Guide Docker
description: Guide Docker Servarr - Présentation des concepts Docker, des concepts de liens physiques et des autorisations et permissions Linux
published: true
date: 2023-07-15T20:41:38.016Z
tags: 
editor: markdown
dateCreated: 2021-05-16T20:23:46.192Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [La meilleure configuration Docker](#la-meilleure-configuration-docker)
- [Portainer](#portainer)
- [Introduction](#introduction)
- [Utilisateurs multiples et groupe partagé](#utilisateurs-multiples-et-groupe-partagé)
  - [Autorisations](#autorisations)
  - [UMASK](#umask)
  - [PUID et PGID](#puid-et-pgid)
  - [Exemple](#exemple)
- [Utilisateur unique et groupe partagé facultatif](#utilisateur-unique-et-groupe-partagé-facultatif)
- [Propriété et autorisations de /config](#propriété-et-autorisations-de-config)
- [Chemins cohérents et bien planifiés](#chemins-cohérents-et-bien-planifiés)
  - [Exemples](#exemples)
    - [Torrents](#torrents)
    - [Usenet](#usenet)
    - [Serveur multimédia](#serveur-multimédia)
    - [Sonarr, Radarr et Lidarr](#sonarr-radarr-et-lidarr)
  - [Problèmes](#problèmes)
- [Exécution des conteneurs à l'aide de](#exécution-des-conteneurs-à-laide-de)
  - [Docker Compose](#docker-compose)
    - [Mise à jour de toutes les images et tous les conteneurs](#mise-à-jour-de-toutes-les-images-et-tous-les-conteneurs)
    - [Mise à jour d'une image et d'un conteneur individuels](#mise-à-jour-dune-image-et-dun-conteneur-individuels)
  - [docker run](#docker-run)
  - [Systemd](#systemd)
- [Commandes utiles](#commandes-utiles)
  - [Lister les conteneurs en cours d'exécution](#lister-les-conteneurs-en-cours-dexécution)
  - [Shell *à l'intérieur* d'un conteneur](#shell-à-lintérieur-dun-conteneur)
  - [Nettoyer Docker](#nettoyer-docker)
  - [Obtenir la commande docker run](#obtenir-la-commande-docker-run)
  - [Obtenir docker-compose](#obtenir-docker-compose)
  - [Résoudre les problèmes de réseau](#résoudre-les-problèmes-de-réseau)
  - [Changer récursivement le propriétaire et le groupe](#changer-récursivement-le-propriétaire-et-le-groupe)
  - [Changer récursivement les autorisations en 775/664](#changer-récursivement-les-autorisations-en-775664)
  - [Trouver l'UID/GID d'un utilisateur](#trouver-luidgid-dun-utilisateur)
  - [Examiner les fichiers pour les liens physiques](#examiner-les-fichiers-pour-les-liens-physiques)
- [Images Docker intéressantes](#images-docker-intéressantes)
  - [Solutions tout-en-un](#solutions-tout-en-un)
- [Réseau et DNS Docker personnalisés](#réseau-et-dns-docker-personnalisés)
- [Problèmes courants](#problèmes-courants)
  - [Chemins corrects à l'extérieur, chemins incorrects à l'intérieur](#chemins-corrects-à-lextérieur-chemins-incorrects-à-lintérieur)
  - [Exécution de conteneurs Docker en tant que root ou modification des utilisateurs](#exécution-de-conteneurs-docker-en-tant-que-root-ou-modification-des-utilisateurs)
  - [Exécution de conteneurs Docker avec umask 000](#exécution-de-conteneurs-docker-avec-umask-000)
- [Obtenir de l'aide](#obtenir-de-laide)
  - [Support par chat (Discord)](#support-par-chat-discord)
  - [Support par forum (Reddit)](#support-par-forum-reddit)

# La meilleure configuration Docker

**TL;DR**: Un utilisateur [éponyme](https://www.lexico.com/en/definition/eponymous) par démon et un groupe partagé avec un umask de `002`. Définitions de chemins cohérents entre *tous* les conteneurs qui maintiennent la structure des dossiers. L'utilisation d'un seul volume (afin que le dossier de téléchargement et le dossier de bibliothèque soient sur le même système de fichiers) permet d'utiliser des [liens physiques](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-hardlinks) et des [déplacements instantanés (déplacements atomiques)](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/#what-are-instant-moves-atomic-moves) pour Sonarr, Radarr, Lidarr et Readarr. Et surtout, ignorez *la plupart* de la documentation sur les chemins de l'image Docker !

> Remarque : Beaucoup de gens trouvent le [tutoriel sur les liens physiques de TRaSH](https://trash-guides.info/hardlinks/) utile et plus facile à comprendre que ce guide. Ce guide est plus conceptuel, tandis que le tutoriel de TRaSH vous guide à travers le processus.
{.is-info}

# Portainer

> **Portainer doit être évité pour la configuration des conteneurs Docker** {.is-danger}

- Portainer offre une interface graphique pratique pour gérer les conteneurs, mais il est uniquement utile à cette fin.
- Portainer ne doit être utilisé que pour afficher les journaux des conteneurs Docker/état des conteneurs.
- Il est fortement recommandé d'utiliser Docker Compose et de ne pas utiliser Portainer.
- Portainer présente de nombreux problèmes, tels que :
  - Ordre incorrect de la source et de la cible des montages
  - Sensibilité à la casse incohérente
  - Absence de création automatique de réseaux personnalisés pour la communication entre conteneurs
  - Implémentations de composition incohérentes sur différentes architectures
  - Extraction de toutes les balises lors de la mise à jour si aucune balise spécifique n'est définie
  - Certaines fonctionnalités sont masquées et certaines ne fonctionnent pas du tout sur les plates-formes ARM

Consultez ce [Guide Docker](/docker-guide) et [le tutoriel Docker de TRaSH](https://trash-guides.info/hardlinks/) pour savoir comment configurer Docker Compose.

# Introduction

Cet article ne vous montrera pas les détails de la meilleure configuration Docker, mais il décrit une vue d'ensemble que vous pouvez utiliser pour rendre votre propre configuration aussi bonne que possible. L'idée est d'exécuter chaque conteneur Docker en tant qu'utilisateur distinct, avec un groupe partagé et des volumes cohérents, de sorte que chaque conteneur voie la même structure de chemin. C'est facile à dire, mais pas si facile à comprendre et à expliquer.

> N'oubliez pas que beaucoup de gens trouvent le [tutoriel sur les liens physiques de TRaSH](https://trash-guides.info/hardlinks/) utile et plus facile à comprendre que ce guide. Ce guide est plus conceptuel, tandis que le tutoriel de TRaSH vous guide à travers le processus.
{.is-warning}

# Utilisateurs multiples et groupe partagé

## Autorisations

Idéalement, chaque logiciel s'exécute en tant qu'utilisateur distinct et ils font tous partie d'un groupe partagé avec des autorisations de dossier définies sur `775` (`drwxrwxr-x`) et des fichiers définis sur `664` (`-rw-rw-r--`), ce qui correspond à un umask de `002`. Une alternative raisonnable à cela est un seul utilisateur partagé, qui utiliserait `755` et `644`, ce qui correspond à un umask de `022`. Vous pouvez restreindre encore plus les autorisations en refusant la lecture à "autres", ce qui correspondrait à un umask de `007` pour un utilisateur par démon ou `077` pour un seul utilisateur partagé. Pour une explication plus détaillée, consultez les articles du wiki Arch Linux sur les [autorisations et attributs de fichier](https://wiki.archlinux.org/index.php/File_permissions_and_attributes) et [UMASK](https://wiki.archlinux.org/index.php/Umask).

## UMASK

De nombreuses images Docker acceptent `-e UMASK=002` en tant que variable d'environnement et certains logiciels peuvent être configurés avec un utilisateur, un groupe et un umask (NZBGet) ou des autorisations de dossier/fichier (Sonarr/Radarr), à l'intérieur du conteneur. Cela garantira que les fichiers et dossiers créés par *un* peuvent être lus et écrits par les autres. Si vous utilisez des dossiers et des fichiers existants, vous devrez également corriger leur propriété et leurs autorisations actuelles, mais à l'avenir, ils seront corrects car vous avez configuré chaque logiciel correctement.

## PUID et PGID

De nombreuses images Docker acceptent également `-e PUID=123` et `-e PGID=321` qui vous permettent de changer l'UID/GID utilisé à l'intérieur par celui d'un compte à l'extérieur. Si vous jetez un coup d'œil, vous constaterez que le nom d'utilisateur est quelque chose comme `abc`, `nobody` ou `hotio`, mais parce qu'il utilise l'UID/GID que vous passez, à l'extérieur, cela ressemble à l'utilisateur attendu. Si vous utilisez du stockage à partir d'un autre système via NFS ou CIFS, cela vous facilitera la vie si *ce* système a également des utilisateurs et des groupes correspondants. Vous pouvez laisser un système choisir les UID/GID, puis les réutiliser sur l'autre système, en supposant qu'ils ne sont pas en conflit.

## Exemple

Vous exécutez [Sonarr](https://github.com/Sonarr/Sonarr/releases) en utilisant [hotio/sonarr](https://github.com/hotio/docker-sonarr), vous avez créé un utilisateur `sonarr` avec l'UID `123` et un groupe partagé `media` avec le GID `321` dont l'utilisateur `sonarr` est membre. Vous configurez l'image Docker pour s'exécuter avec `-e PUID=123 -e PGID=321 -e UMASK=002`. Sonarr vous permet également de configurer l'utilisateur, le groupe ainsi que les autorisations de dossier et de fichier. Les paramètres précédents devraient annuler ceux-ci, mais vous pouvez les configurer si vous le souhaitez. Un umask de `002` donne `775` (`drwxrwxr-x`) pour les dossiers et `664` (`-rw-rw-r--`) pour les fichiers, et l'utilisateur/groupe est un peu délicat car *à l'intérieur* du conteneur, ils ont un nom différent. En général, ils sont `abc` ou `nobody`.

# Utilisateur unique et groupe partagé facultatif

Une autre option populaire et sans doute plus facile est un seul utilisateur partagé. Peut-être même *votre* utilisateur. Ce n'est pas aussi sécurisé et ne suit pas les meilleures pratiques, mais à la fin, c'est plus facile à comprendre et à mettre en œuvre. L'UMASK pour cela est `022`, ce qui donne `755` (`drwxr-xr-x`) pour les dossiers et `644` (`-rw-r--r--`) pour les fichiers. Le groupe n'a plus vraiment d'importance, vous utiliserez donc probablement le groupe portant le nom de l'utilisateur. Cela rend toutefois plus difficile le partage avec *d'autres* utilisateurs, vous pourriez donc finir par vouloir un UMASK de `002` même avec cette configuration.

# Propriété et autorisations de /config

N'oubliez pas que votre volume `/config` devra *également* avoir la propriété et les autorisations correctes, généralement l'utilisateur du démon et le groupe de cet utilisateur, comme `sonarr:sonarr` et un umask de `022` ou `077` afin que *seul* cet utilisateur ait accès. Dans une configuration à utilisateur unique, il s'agirait bien sûr de l'utilisateur que vous avez choisi.

# Chemins cohérents et bien planifiés

> Beaucoup de gens trouvent le [tutoriel sur les liens physiques de TRaSH](https://trash-guides.info/hardlinks) utile et plus facile à comprendre que ce guide. Ce guide est plus conceptuel, tandis que le tutoriel de TRaSH vous guide à travers le processus.
{.is-info}

Le détail le plus simple et le plus important est de créer des définitions de chemin unifiées pour tous les conteneurs.

Si vous vous demandez pourquoi les liens physiques ne fonctionnent pas ou pourquoi un simple déplacement prend beaucoup plus de temps que prévu, cette section l'explique. Les chemins que vous utilisez à l'*intérieur* sont importants. En raison du fonctionnement des volumes de Docker, en passant deux volumes tels que les chemins couramment suggérés `/tv`, `/movies` et `/downloads`, ils semblent être deux systèmes de fichiers différents, même s'ils sont un seul système de fichiers à l'extérieur du conteneur. Cela signifie que les liens physiques ne fonctionneront pas *et* au lieu d'un déplacement instantané/atomique, une copie+suppression plus lente et plus intensive en E/S est utilisée. Si vous avez plusieurs clients de téléchargement car vous utilisez des torrents et Usenet, avoir un seul chemin `/downloads` signifie qu'ils seront mélangés. Parce que le Radarr dans un conteneur demandera au NZBGet dans son propre conteneur où se trouvent les fichiers, en utilisant le même chemin dans les deux cas, cela fonctionnera simplement. Sinon, vous devrez le corriger avec une correspondance de chemin distant.

Choisissez donc une seule disposition de chemin et utilisez-la pour tous les conteneurs. Il est suggéré d'utiliser `/data`, mais il existe d'autres noms courants comme `/shared`, `/media` ou `/dvr`. En gardant cela identique à l'extérieur et à l'intérieur, votre configuration sera plus simple : un seul chemin à retenir ou si vous intégrez Docker et un logiciel natif. Par exemple, Synology pourrait utiliser `/Volume1/data` et unRAID pourrait utiliser `/mnt/user/data` à l'extérieur, mais `/data` à l'intérieur convient.

Il est également important de se rappeler que vous devrez configurer ou reconfigurer les chemins dans les logiciels s'exécutant *à l'intérieur* de ces conteneurs Docker. Si vous modifiez les chemins de votre client de téléchargement, vous devrez modifier ses paramètres pour les faire correspondre et probablement mettre à jour les torrents existants. Si vous modifiez le chemin de votre bibliothèque, vous devrez modifier ces paramètres dans Sonarr, Radarr, Lidarr, Plex, etc.

## Exemples

Ce qui importe ici, c'est la structure générale, pas les noms. Vous êtes libre de choisir des noms de dossiers qui vous semblent logiques. Et il existe d'autres façons d'organiser les choses également. Par exemple, il est peu probable que vous téléchargiez et rencontriez des conflits de versions identiques entre Usenet et les torrents, vous pouvez donc *mettre* les deux dans des dossiers `/data/downloads/{movies|books|music|tv}`. Les téléchargements n'ont même pas besoin d'être triés dans des sous-dossiers non plus, car les films, la musique et la télévision entreront rarement en conflit.

Ce dossier `data` d'exemple comporte des sous-dossiers pour les torrents et Usenet, et chacun de ces sous-dossiers comporte des sous-dossiers pour les téléchargements de télévision, de films et de musique afin de garder les choses bien rangées. Le dossier `media` comporte des sous-dossiers bien nommés pour la télévision, les films, les livres et la musique. Ce dossier `media` est votre bibliothèque et ce que vous transmettriez à Plex, Kodi, Emby, Jellyfin, etc.

Pour l'exemple ci-dessous, `data` est équivalent au chemin d'hôte `/host/data` et au chemin Docker `/data`

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    |  ├── books
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  ├── books
    │  └── tv
    └── media
        ├── movies
        ├── music
        ├── books
        └── tv
```

Le chemin pour chaque conteneur Docker peut être aussi spécifique que nécessaire tout en maintenant la structure correcte :

### Torrents

```none
    data
    └── torrents
        ├── movies
        ├── music
        ├── books
        └── tv
```

Torrents n'a besoin d'accéder qu'aux fichiers torrent, donc passez `-v /host/data/torrents:/data/torrents`. Dans les paramètres du logiciel de torrent, vous devrez reconfigurer les chemins et vous pouvez trier dans des sous-dossiers comme `/data/torrents/{tv|books|movies|music}`.

### Usenet

```none
    data
    └── usenet
        ├── movies
        ├── music
        └── tv
```

Usenet n'a besoin d'accéder qu'aux fichiers Usenet, donc passez `-v /host/data/usenet:/data/usenet`. Dans les paramètres du logiciel Usenet, vous devrez reconfigurer les chemins et vous pouvez trier dans des sous-dossiers comme `/data/usenet/{tv|movies|music}`.

### Serveur multimédia

```none
    data
    └── media
        ├── movies
        ├── music
        └── tv
```

Plex/Emby n'a besoin d'accéder qu'à votre bibliothèque multimédia, donc passez `-v /host/data/media:/data/media`, qui peut comporter un nombre quelconque de sous-dossiers comme `movies`, `kids movies`, `tv`, `documentary tv` et/ou `music`.

### Sonarr, Radarr et Lidarr

```none
    data
    ├── torrents
    │  ├── movies
    │  ├── music
    │  └── tv
    ├── usenet
    │  ├── movies
    │  ├── music
    │  └── tv
    └── media
        ├── movies
        ├── music
        └── tv
```

Sonarr, Radarr et Lidarr obtiennent tout en utilisant `-v /host/data:/data` car le dossier de *téléchargement* et le dossier de *média* ressembleront à un seul système de fichiers. Les liens physiques fonctionneront et les déplacements seront atomiques, au lieu de copier + supprimer.

## Problèmes

Il y a quelques problèmes mineurs si vous ne suivez pas les chemins suggérés de l'image Docker.

Le plus gros problème est que les volumes définis dans le `dockerfile` seront créés s'ils ne sont pas spécifiés, ce qui signifie qu'ils s'accumuleront lorsque vous supprimez et recréez les conteneurs. S'ils contiennent des données, ils peuvent consommer de l'espace de manière inattendue et probablement à un endroit inapproprié. Vous pouvez trouver une [commande de nettoyage](#prune-docker) dans la section des commandes utiles ci-dessous. Cela pourrait également être atténué en passant un dossier vide pour tous les volumes que vous ne souhaitez pas utiliser, comme `/data/empty:/movies` et `/data/empty:/downloads`. Vous pouvez même mettre un fichier nommé `NE PAS UTILISER CE DOSSIER` à l'intérieur, pour vous rappeler.

Un autre problème est que certaines images sont préconfigurées pour utiliser les volumes documentés, vous devrez donc modifier les paramètres du logiciel à l'intérieur du conteneur Docker. Heureusement, étant donné que la configuration persiste en dehors du conteneur, il s'agit d'un problème ponctuel. Vous pouvez également choisir un chemin comme `/data` ou `/media` que certaines images définissent déjà pour une utilisation spécifique. Cela ne devrait pas poser de problème, mais cela sera un peu plus confus lorsqu'il sera combiné avec les problèmes précédents. En fin de compte, cela en vaut la peine pour les liens durs et les déplacements rapides. La cohérence et la simplicité sont également des effets secondaires bienvenus.

Si vous utilisez la dernière version de [RadarrSync](https://github.com/Sperryfreak01/RadarrSync) abandonnée pour synchroniser deux instances de Radarr, cela *dépend* de la mise en correspondance du *même* chemin à l'intérieur vers un chemin différent à l'extérieur, par exemple `/movies` pour une instance pointerait vers `/data/media/movies` et l'autre vers `/data/media/movies4k`. Cela casse *tout* ce que vous avez lu ci-dessus. Il n'y a pas de bonne solution, vous pouvez utiliser l'ancienne version qui n'est pas aussi bonne, faire votre mise en correspondance d'une manière laide et casser les liens durs ou ne pas l'utiliser du tout.

# Exécution de conteneurs à l'aide de

## Docker Compose

C'est la meilleure option pour la plupart des utilisateurs, cela vous permet de contrôler et de configurer de nombreux conteneurs et leur interdépendance dans un seul fichier. Un bon point de départ est le [Guide de démarrage de Docker Compose](https://docs.docker.com/compose/gettingstarted/) de Docker lui-même. Vous pouvez utiliser [composerize](https://composerize.com) ou [ghcr.io/red5d/docker-autocompose](#get-docker-compose) pour convertir les commandes `docker run` en un seul fichier `docker-compose.yml`.

> Ce qui suit n'est *pas* un exemple complet et fonctionnel ! Les conteneurs n'ont que les PID, UID, UMASK et les chemins d'exemple définis pour simplifier.
{.is-warning}

```yml
    # sonarr
    Sonarr:
        image: cr.hotio.dev/hotio/sonarr
        volumes:
            - /path/to/config/sonarr:/config
            - /host/data:/data
        environment:
            - PUID=111
            - PGID=321
            - UMASK=002

    # deluge
    Deluge:
        image: binhex/arch-delugevpn
        volumes:
            - /path/to/config/deluge:/config
            - /host/data/torrents:/data/torrents
        environment:
            - PUID=222
            - PGID=321
            - UMASK=002

    # SABnzbd
    SABnzbd:
        image: cr.hotio.dev/hotio/sabnzbd
        volumes:
            - /path/to/config/sabnzbd:/config
            - /host/data/usenet:/data/usenet
        environment:
            - PUID=333
            - PGID=321
            - UMASK=002

    # plex
    Plex:
        image: cr.hotio.dev/hotio/plex
        volumes:
            - /path/to/config/plex:/config
            - /host/data/media:/data/media

        environment:
            - PUID=444
            - PGID=321
            - UMASK=002
```

### Mettre à jour toutes les images et les conteneurs

```shell
    docker-compose pull
    docker-compose up -d
```

### Mettre à jour une image et un conteneur individuellement

```shell
    docker-compose pull NOM
    docker-compose up -d NOM
```

## docker run

> Comme l'exemple Docker Compose ci-dessus, les commandes `docker run` suivantes sont réduites *uniquement* aux PUID, PGID, UMASK et volumes afin de servir d'exemple évident.
{.is-warning}

```shell
    # sonarr
    docker run -v /path/to/config/sonarr:/config \
               -v /host/data:/data \
               -e PUID=111 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sonarr

    # deluge
    docker run -v /path/to/config/deluge:/config \
               -v /host/data/torrents:/data/torrents \
               -e PUID=222 -e PGID=321 -e UMASK=002 \
               binhex/arch-delugevpn

    # SABnzbd
    docker run -v /path/to/config/sabnzbd:/config \
               -v /host/data/usenet:/data/usenet \
               -e PUID=333 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/sabnzbd

    # plex
    docker run -v /path/to/config/plex:/config \
               -v /host/data/media:/data/media \
               -e PUID=444 -e PGID=321 -e UMASK=002 \
               cr.hotio.dev/hotio/plex
```

## Systemd

Pour gérer quelques conteneurs Docker, l'utilisation de systemd est une option. Cela standardise le contrôle et simplifie les dépendances pour les services natifs et Docker. L'exemple générique ci-dessous peut être adapté à n'importe quel conteneur en ajustant ou en ajoutant les différentes valeurs et options.

```shell
    # /etc/systemd/system/thing.service
    [Unit]
    Description=Thing
    Requires=docker.service
    After=network.target docker.service

    [Service]
    ExecStart=/usr/bin/docker run --rm \
                              --name=thing \
                              -v /path/to/config/thing:/config \
                              -v /host/data:/data
                              -e PUID=111 -e PGID=321 -e UMASK=002 \
                              nobody/thing

    ExecStop=/usr/bin/docker stop -t 30 thing

    [Install]
    WantedBy=default.target
```

# Commandes utiles

## Liste des conteneurs en cours d'exécution

```shell
    docker ps
```

## Shell *à l'intérieur* d'un conteneur

L'exécution dans un conteneur vous connectera généralement en tant que root

```shell
    docker exec -it NOM_DU_CONTENEUR /bin/bash
```

Une fois à l'intérieur, vous pouvez changer d'utilisateur avec

```shell
    su - <nom_utilisateur>
```

Pour exécuter en tant qu'utilisateur spécifique, ajoutez `-u` en tant qu'argument et passez le nom d'utilisateur ou l'ID

```shell
    docker exec -u UTILISATEUR -it NOM_DU_CONTENEUR /bin/bash
```

### Exemples en tant qu'utilisateurs spécifiques

#### LSIO Radarr

```shell
    docker exec -u abc -it radarr bash
```

#### Hotio Sonarr

```shell
    docker exec -u hotio -it sonarr bash
```

Pour plus d'informations, consultez la documentation de [docker exec](https://docs.docker.com/engine/reference/commandline/exec/).

## Nettoyer Docker

```shell
    docker system prune --all --volumes
```

> Supprime les conteneurs, réseaux, volumes, images et cache de construction inutilisés. Comme l'avertissement donné par cette commande le dit, cela supprimera tous les éléments mentionnés précédemment pour tout ce qui n'est pas utilisé par un conteneur en cours d'exécution. Dans un environnement correctement configuré, cela ne pose pas de problème. Mais soyez conscient et procédez avec prudence la première fois. Consultez la documentation de [Docker system prune](https://docs.docker.com/engine/reference/commandline/system_prune/) pour plus de détails.
{.is-warning}

## Obtenir la commande docker run

Obtenir la commande `docker run` à partir de gestionnaires GUI peut être difficile, cette image Docker le rend facile pour un conteneur en cours d'exécution ([source](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container)).

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock assaflavie/runlike NOM_DU_CONTENEUR
```

## Obtenir docker-compose

> De plus, vous pouvez consulter [le guide TRaSH pour docker-compose](https://trash-guides.info/compose/)
{.is-info}

Il est possible d'obtenir un fichier `docker-compose.yml` à partir d'instances en cours d'exécution avec [docker-autocompose](https://github.com/Red5d/docker-autocompose), au cas où vous auriez déjà démarré vos conteneurs avec `docker run` ou `docker create` et que vous souhaitez passer à un style `docker-compose`. C'est également idéal pour partager vos paramètres avec d'autres personnes, car cela n'a pas d'importance quel logiciel de gestion vous utilisez. Le(s) dernier(s) argument(s) sont les noms de vos conteneurs et vous pouvez en passer autant que nécessaire en même temps. Le premier nom de conteneur est obligatoire, les autres sont facultatifs. Vous pouvez voir les noms de conteneur dans la colonne **NAMES** de `docker ps`, ils sont généralement définis par vous ou peuvent être générés en fonction de l'image comme `binhex-qbittorrent`. Ce n'est *pas* le nom de l'image, comme `binhex/arch-qbittorrentvpn`.

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $NOM_DU_CONTENEUR $AUTRE_NOM_DU_CONTENEUR ... $ENCORE_UN_AUTRE_NOM_DU_CONTENEUR
```

Pour certains utilisateurs, cela pourrait être :

```shell
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose lidarr prowlarr radarr readarr sonarr qbittorrent
```

## Dépanner le réseau

La plupart des images Docker ne contiennent pas beaucoup d'outils utiles pour le dépannage, mais vous pouvez [attacher une image de dépannage réseau](https://hub.docker.com/r/nicolaka/netshoot) à un conteneur existant pour vous aider.

```shell
    docker run -it --rm --network container:NOM_DU_CONTENEUR nicolaka/netshoot
```

## Changer récursivement le propriétaire et le groupe

```shell
    chown -R utilisateur:groupe /chemin/ici
```

## Changer récursivement les autorisations en 775/664

```shell
    chmod -R a=,a+rX,u+w,g+w /chemin/ici
              ^  ^    ^   ^ ajoute l'écriture au groupe
              |  |    | ajoute l'écriture à l'utilisateur
              |  | ajoute la lecture à tous et l'exécution à tous les dossiers (ce qui contrôle l'accès)
              | définit tout sur `000`
```

## Trouver l'UID/GID pour un utilisateur

```shell
    id <nom_utilisateur>
```

## Examiner les fichiers pour les liens durs

```shell
    ls -alhi
    42207934 -rw-r--r--  2 utilisateur groupe    0 11 sept. 11:55 # lié en dur
    42207936 -rw-r--r--  1 utilisateur groupe    0 11 sept. 11:55 # pas de liens durs
    42207934 -rw-r--r--  2 utilisateur groupe    0 11 sept. 11:55 # original

    stat original
      Fichier : original
      Taille : 0               Blocs : 0          Blocs d'E/S : 4096   fichier vide ordinaire
    Périphérique : 803h/2051d      Inœud : 42207934    Liens : 2
    Accès : (0644/-rw-r--r--)  Uid : ( 1000/ utilisateur)   Gid : ( 1001/ groupe)
    Accès : 2020-09-11 11:55:43.803327144 -0500
    Modification : 2020-09-11 11:55:43.803327144 -0500
    Changement : 2020-09-11 11:55:49.706660476 -0500
     Création : 2020-09-11 11:55:43.803327144 -0500
```

# Images Docker intéressantes

- [rasmunk/sshfs](https://github.com/rasmunk/docker-volume-sshfs)
{.links-list}
- [hotio’s](https://hotio.dev/) La documentation et le Dockerfile ne font aucune suggestion de mauvais chemin. Les images sont automatiquement mises à jour 2 fois par heure si des modifications sont trouvées en amont. Hotio construit également nos demandes de tirage (sauf Sonarr), ce qui peut être utile pour les tests.
  - [sonarr](https://hotio.dev/containers/sonarr)
  - [radarr](https://hotio.dev/containers/radarr)
  - [lidarr](https://hotio.dev/containers/lidarr)
  - [readarr](https://hotio.dev/containers/readarr)
  - [prowlarr](https://hotio.dev/containers/prowlarr) pour la recherche d'usenet et de trackers torrent
  - [qbittorrent](https://hotio.dev/containers/qbittorrent/)
  - [NZBGet](https://hotio.dev/containers/nzbget/)
  - [SABnzbd](https://hotio.dev/containers/sabnzbd/)
  - [qflood](https://hotio.dev/containers/qflood/)
  - [ombi](https://hotio.dev/containers/ombi) pour demander des médias
  - [overseerr](https://hotio.dev/containers/overseerr/) pour demander des médias
  - [jackett](https://hotio.dev/containers/jackett) pour la recherche de trackers torrent
  - [nzbhydra2](https://hotio.dev/containers/nzbhydra2) pour la recherche d'indexeurs usenet
  - [bazarr](https://hotio.dev/containers/bazarr) pour les sous-titres
  - [pullio](https://hotio.dev/pullio/) pour la mise à jour automatique des conteneurs
  - [unpackerr](https://hotio.dev/containers/unpackerr) est utile pour l'extraction de torrents empaquetés sur une variété de clients torrent où le déballage est insuffisant ou totalement absent.
{.links-list}
- Les images de [linuxserver.io](https://hub.docker.com/u/linuxserver) ont des images pour *beaucoup* de logiciels et elles sont bien entretenues. Cependant, évitez leurs chemins suggérés (facultatifs).
  - [SWAG Proxy](https://hub.docker.com/r/linuxserver/swag)
  - [qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/)
  - [deluge](https://hub.docker.com/r/linuxserver/deluge/)
  - [rtorrent](https://hub.docker.com/r/linuxserver/rutorrent/)
  - [SABnzbd](https://hub.docker.com/r/linuxserver/sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/linuxserver/nzbget/)
  - [sonarr](https://hub.docker.com/r/linuxserver/sonarr/)
  - [radarr](https://hub.docker.com/r/linuxserver/radarr/)
  - [lidarr](https://hub.docker.com/r/linuxserver/lidarr/)
- [binhex](https://hub.docker.com/u/binhex) un autre mainteneur populaire
  - [qbittorrent](https://hub.docker.com/r/binhex/arch-qbittorrentvpn/)
  - [deluge](https://hub.docker.com/r/binhex/arch-delugevpn/)
  - [rtorrent](https://hub.docker.com/r/binhex/arch-rtorrentvpn/)
  - [SABnzbd](https://hub.docker.com/r/binhex/arch-sabnzbd/)
  - [NZBGet](https://hub.docker.com/r/binhex/arch-nzbget/)
  - [sonarr](https://hub.docker.com/r/binhex/arch-sonarr/)
  - [radarr](https://hub.docker.com/r/binhex/arch-radarr/)
  - [lidarr](https://hub.docker.com/r/binhex/arch-lidarr/)
{.links-list}

### Solutions tout-en-un

- [Il s'agit d'un dépôt GitHub](https://github.com/Luctia/ezarr) destiné aux débutants qui souhaitent utiliser Docker pour leur pile Servarr. Il s'agit essentiellement d'une collection de fichiers prête à l'emploi et il vous suffit de lancer deux choses pour mettre en ligne l'ensemble. Cela élimine les tracas liés à la gestion des utilisateurs et des autorisations sur le périphérique hôte et propose d'autres applications telles que PleX.

# Réseau et DNS Docker personnalisés

Une fonctionnalité intéressante d'un [réseau Docker personnalisé](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks) est qu'il dispose de son propre serveur DNS. Si vous créez un réseau pont pour vos conteneurs, vous pouvez utiliser leurs noms d'hôte dans votre configuration. Par exemple, si vous exécutez `docker run --network=isolated --hostname=deluge binhex/arch-deluge` et `docker run --network=isolated --hostname=radarr binhex/arch-radarr`, vous pouvez ensuite configurer le client de téléchargement dans Radarr pour pointer uniquement vers `deluge` et cela fonctionnera *et* communiquera sur son propre réseau privé. Cela signifie que si vous voulez être encore plus sécurisé, vous pouvez *arrêter* de transférer ce port également. Si vous placez votre conteneur de proxy inverse sur le même réseau, vous pouvez même arrêter de transférer les ports de l'interface web et les rendre encore plus sécurisés.

# Problèmes courants

## Chemins corrects *à l'extérieur*, chemins incorrects *à l'intérieur*

Beaucoup de gens lisent cela et pensent comprendre, mais ils finissent par voir le chemin extérieur correctement vers quelque chose comme `/data/usenet`, mais ils passent à côté du point et définissent toujours le chemin *à l'intérieur* sur `/downloads`.

- Bon :
  - `/host/data/usenet:/data/usenet`
  - `/data/media:/data/media`
- Mauvais :
  - `/host/data:/downloads`
  - `/host/data:/media`
  - `/data/downloads:/data`

## Exécution des conteneurs Docker en tant que root ou modification des utilisateurs

Si vous vous retrouvez à exécuter vos conteneurs en tant que `root:root`, vous faites quelque chose de mal. Si vous ne transmettez pas un UID et un GID, vous utiliserez celui par défaut de l'image et *celui-ci* ne correspondra probablement pas à un utilisateur raisonnable sur votre système. Et si vous modifiez l'utilisateur et le groupe sous lesquels s'exécutent vos conteneurs Docker, vous risquez probablement de rencontrer des problèmes de permissions sur des dossiers tels que le dossier `/config` qui contiendra probablement des fichiers et des dossiers créés la première fois avec l'UID/GID que vous avez utilisé la première fois.

## Exécution des conteneurs Docker avec umask 000

Si vous vous retrouvez à définir un UMASK de `000` (qui est 777 pour les dossiers et 666 pour les fichiers), vous faites *également* quelque chose de mal. Cela laisse vos fichiers et dossiers en lecture/écriture pour *tout le monde*, ce qui est une mauvaise hygiène Linux.

# Obtenir de l'aide

## Support par chat (Discord)

- [Discord Sonarr](https://discord.sonarr.tv/)
- [Discord Radarr](https://radarr.video/discord)
{.links-list}

## Support par forum (Reddit)

- [/r/sonarr](http://reddit.com/r/sonarr)
- [/r/radarr](http://reddit.com/r/radarr)
{.links-list}