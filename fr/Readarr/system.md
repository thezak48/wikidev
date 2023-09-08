---
title: Système Readarr
description: 
published: true
date: 2022-05-05T12:52:16.242Z
tags: readarr, needs-love, système
editor: markdown
dateCreated: 2021-06-20T19:54:43.262Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Statut](#statut)
  - [Santé](#santé)
    - [Avertissements système](#avertissements-système)
      - [La branche n'est pas une branche de version valide](#la-branche-nest-pas-une-branche-de-version-valide)
      - [La version SQLite actuellement installée n'est pas prise en charge](#la-version-sqlite-actuellement-installée-nest-pas-prise-en-charge)
      - [Une nouvelle mise à jour est disponible](#une-nouvelle-mise-à-jour-est-disponible)
      - [Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur](#impossible-dinstaller-la-mise-à-jour-car-le-dossier-de-démarrage-nest-pas-accessible-en-écriture-par-lutilisateur)
      - [La mise à jour ne sera pas possible pour éviter la suppression des données de l'application lors de la mise à jour](#la-mise-à-jour-ne-sera-pas-possible-pour-éviter-la-suppression-des-données-de-lapplication-lors-de-la-mise-à-jour)
      - [La branche est destinée à une version précédente](#la-branche-est-destinée-à-une-version-précédente)
      - [Impossible de se connecter à signalR](#impossible-de-se-connecter-à-signalr)
        - [Nginx](#nginx)
      - [Échec de la résolution de l'adresse IP pour l'hôte proxy configuré](#échec-de-la-résolution-de-ladresse-ip-pour-lhôte-proxy-configuré)
      - [Échec du test du proxy](#échec-du-test-du-proxy)
      - [L'heure système est décalée de plus d'un jour](#lheure-système-est-décalée-de-plus-dun-jour)
    - [Clients de téléchargement](#clients-de-téléchargement)
      - [Aucun client de téléchargement n'est disponible](#aucun-client-de-téléchargement-nest-disponible)
      - [Impossible de communiquer avec le client de téléchargement](#impossible-de-communiquer-avec-le-client-de-téléchargement)
      - [Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance](#les-clients-de-téléchargement-ne-sont-pas-disponibles-en-raison-dune-défaillance)
      - [Activer la gestion des téléchargements terminés](#activer-la-gestion-des-téléchargements-terminés)
      - [Mauvaise correspondance de chemin distant Docker](#mauvaise-correspondance-de-chemin-distant-docker)
      - [Téléchargement dans le dossier racine](#téléchargement-dans-le-dossier-racine)
      - [Mauvais paramètres du client de téléchargement](#mauvais-paramètres-du-client-de-téléchargement)
      - [Mauvaise correspondance de chemin distant](#mauvaise-correspondance-de-chemin-distant)
      - [Erreur d'autorisation](#erreur-dautorisation)
      - [Le montage de l'auteur est en lecture seule](#le-montage-de-lauteur-est-en-lecture-seule)
      - [Le fichier distant a été supprimé en cours de traitement](#le-fichier-distant-a-été-supprimé-en-cours-de-traitement)
      - [Le chemin distant est utilisé et l'importation a échoué](#le-chemin-distant-est-utilisé-et-limportation-a-échoué)
    - [Gestion des téléchargements terminés/échoués](#gestion-des-téléchargements-terminéséchoués)
      - [La gestion des téléchargements terminés est désactivée](#la-gestion-des-téléchargements-terminés-est-désactivée)
    - [Indexeurs](#indexeurs)
      - [Aucun indexeur disponible avec la recherche automatique activée, Readarr ne fournira aucun résultat de recherche automatique](#aucun-indexeur-disponible-avec-la-recherche-automatique-activée-readarr-ne-fournira-aucun-résultat-de-recherche-automatique)
      - [Aucun indexeur disponible avec la synchronisation RSS activée, Readarr ne récupérera pas automatiquement les nouvelles versions](#aucun-indexeur-disponible-avec-la-synchronisation-rss-activée-readarr-ne-récupérera-pas-automatiquement-les-nouvelles-versions)
      - [Aucun indexeur n'est activé](#aucun-indexeur-nest-activé)
    - [Les indexeurs activés ne prennent pas en charge la recherche](#les-indexeurs-activés-ne-prennent-pas-en-charge-la-recherche)
      - [Aucun indexeur disponible avec la recherche interactive activée](#aucun-indexeur-disponible-avec-la-recherche-interactive-activée)
      - [Les indexeurs ne sont pas disponibles en raison de défaillances](#les-indexeurs-ne-sont-pas-disponibles-en-raison-de-défaillances)
      - [Jackett utilise tous les points de terminaison](#jackett-utilise-tous-les-points-de-terminaison)
        - [Solutions](#solutions)
    - [Dossiers de livres](#dossiers-de-livres)
      - [Dossier racine manquant](#dossier-racine-manquant)
    - [Listes d'importation](#listes-dimportation)
      - [Les listes d'importation ne sont pas disponibles en raison de défaillances](#les-listes-dimportation-ne-sont-pas-disponibles-en-raison-de-défaillances)
  - [Espace disque](#espace-disque)
  - [À propos](#à-propos)
  - [Plus d'informations](#plus-dinformations)
- [Tâches](#tâches)
  - [Planifiées](#planifiées)
  - [File d'attente](#file-dattente)
- [Sauvegarde](#sauvegarde)
- [Mises à jour](#mises-à-jour)
- [Événements](#événements)
- [Fichiers journaux](#fichiers-journaux)

# Statut

## Santé

- Cette page contient une liste des erreurs de vérification de santé. Ces vérifications de santé sont effectuées périodiquement par Readarr et lors de certains événements. Les avertissements et les erreurs résultants sont répertoriés ici pour donner des conseils sur la façon de les résoudre.

### Avertissements système

#### La branche n'est pas une branche de version valide

- La branche que vous avez définie n'est pas une branche de version valide. Vous ne recevrez pas de mises à jour. Veuillez changer pour l'une des [branches de version actuelles](/readarr/faq#how-do-i-update-readarr).

#### La version SQLite actuellement installée n'est pas prise en charge

- Readarr stocke ses données dans une base de données SQLite. La bibliothèque SQLite3 installée sur votre système est trop ancienne. Readarr nécessite au moins la version 3.9.0. Notez que Readarr utilise `libSQLite3.so` qui peut être ou non contenu dans un package de mise à niveau SQLite3.

> Notez que Readarr utilise `libSQLite3.so` qui peut être ou non contenu dans un package de mise à niveau SQLite3.
{.is-info}

#### Une nouvelle mise à jour est disponible

Réjouissez-vous, les développeurs ont publié une nouvelle mise à jour. Cela signifie généralement de nouvelles fonctionnalités géniales et des tas de bugs corrigés (n'est-ce pas ?). Apparemment, vous n'avez pas activé la mise à jour automatique, vous devrez donc trouver comment mettre à jour sur votre plateforme. Appuyer sur le bouton Installer sur la page Système => Mises à jour est probablement un bon point de départ.

> Cet avertissement n'apparaîtra pas si votre version actuelle a moins de 14 jours
{.is-info}

#### Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur

- Cela signifie que Readarr ne pourra pas se mettre à jour lui-même. Vous devrez mettre à jour Readarr manuellement ou définir les autorisations sur le répertoire de démarrage de Readarr (le répertoire d'installation) pour permettre à Readarr de se mettre à jour lui-même.

#### La mise à jour ne sera pas possible pour éviter la suppression des données de l'application lors de la mise à jour

- Readarr a détecté que le dossier AppData pour votre système d'exploitation est situé à l'intérieur du répertoire qui contient les binaires de Readarr. Normalement, il s'agirait de C:\ProgramData pour Windows et ~/.config pour Linux.

- Veuillez consulter Système => Informations pour voir les répertoires AppData et de démarrage actuels.
- Cela signifie que Readarr ne pourra pas se mettre à jour lui-même sans risquer de perdre des données.
- Si vous êtes sous Linux, vous devrez probablement modifier le répertoire personnel de l'utilisateur qui exécute Readarr et copier le contenu actuel du répertoire ~/.config/Readarr pour préserver votre base de données.

#### La branche est destinée à une version précédente

- La configuration de la branche de mise à jour dans Paramètres/Général est destinée à une version précédente de Readarr, par conséquent, l'instance ne verra pas les informations de mise à jour correctes dans le flux Système/Mises à jour et ne recevra peut-être pas les nouvelles mises à jour lorsqu'elles seront publiées.

#### Impossible de se connecter à signalR

- signalR permet les mises à jour dynamiques de l'interface utilisateur, donc si votre navigateur ne peut pas se connecter à signalR sur votre serveur, vous ne verrez aucune mise à jour en temps réel dans l'interface utilisateur.

- La situation la plus courante est l'utilisation d'un proxy inverse ou de Cloudflare.
- Cloudflare nécessite l'activation des websockets.

##### Nginx

- Nginx nécessite l'ajout suivant au bloc de localisation de l'application :

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Assurez-vous de ne pas inclure proxy_set_header Connection "Upgrade"; comme suggéré par la documentation de nginx. CELA NE FONCTIONNERA PAS
> Voir <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

Pour Apache2 en tant que proxy inverse, vous devez activer les modules suivants : proxy, proxy_http et proxy_wstunnel. Ensuite, ajoutez cette directive de tunnel websocket à la configuration de votre hôte virtuel :

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8787/$1 [P,L]
```

Pour Caddy (V1), utilisez ceci :
Note : vous devrez également ajouter la directive websocket à votre configuration Readarr

```none
 proxy /readarr 127.0.0.1:8787 {
     websocket
     transparent
 }
```

#### Échec de la résolution de l'adresse IP pour l'hôte proxy configuré

- Vérifiez vos paramètres de proxy et assurez-vous qu'ils sont corrects.
- Assurez-vous que votre proxy est actif, en cours d'exécution et accessible.

#### Échec du test du proxy

- Votre proxy configuré a échoué au test, vérifiez l'erreur HTTP fournie et/ou consultez les journaux pour plus de détails.

#### L'heure système est décalée de plus d'un jour

- L'heure système est décalée de plus d'un jour. Les tâches planifiées peuvent ne pas s'exécuter correctement tant que l'heure n'est pas corrigée.
- Vérifiez l'heure système et assurez-vous qu'elle est synchronisée avec un serveur de temps fiable et précis.

### Clients de téléchargement

#### Aucun client de téléchargement n'est disponible

- Un client de téléchargement correctement configuré et activé est requis pour que Readarr puisse télécharger des médias. Étant donné que Readarr prend en charge différents clients de téléchargement, vous devez déterminer celui qui correspond le mieux à vos besoins. Si vous avez déjà un client de téléchargement installé, vous devez le configurer pour l'utiliser avec Readarr et créer une catégorie. Voir Paramètres => Client de téléchargement.

#### Impossible de communiquer avec le client de téléchargement

- Readarr n'a pas pu communiquer avec le client de téléchargement configuré. Veuillez vérifier si le client de téléchargement est opérationnel et vérifier à nouveau l'URL. Cela peut également indiquer une erreur d'authentification.
- Cela est généralement dû à une mauvaise configuration du client de téléchargement. Voici quelques points que vous pouvez vérifier :
- L'adresse IP de vos clients de téléchargement, si elle est sur la même machine physique, il s'agit généralement de 127.0.0.1
- Le numéro de port que votre client de téléchargement utilise, ces champs sont remplis avec le numéro de port par défaut, mais si vous l'avez modifié, vous devrez entrer le même numéro dans Readarr.
- Assurez-vous que le chiffrement SSL n'est pas activé si vous utilisez à la fois votre instance Readarr et votre client de téléchargement sur un réseau local. Consultez la FAQ SSL pour plus d'informations.

#### Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance

{#download-clients-are-unavailable-due-to-failures}

- Un ou plusieurs de vos clients de téléchargement ne répondent pas aux demandes de Readarr. Par conséquent, Readarr a décidé d'arrêter temporairement l'interrogation du client de téléchargement selon son cycle normal d'une minute, qui est normalement utilisé pour suivre les téléchargements actifs et importer les téléchargements terminés. Cependant, Readarr continuera à essayer d'envoyer des téléchargements au client, mais il est fort probable que cela échoue.
- Vous devriez consulter Système=>Journaux pour voir la raison des échecs.
- Si vous n'utilisez plus ce client de téléchargement, désactivez-le dans Readarr pour éviter les erreurs.

#### Activer la gestion des téléchargements terminés

- Readarr nécessite la gestion des téléchargements terminés pour pouvoir importer les fichiers téléchargés par le client de téléchargement. Il est recommandé d'activer la gestion des téléchargements terminés.
- (La gestion des téléchargements terminés est activée par défaut pour les nouveaux utilisateurs.)

#### Mauvaise correspondance de chemin distant Docker

- Cette erreur est généralement associée à des chemins Docker incorrects dans votre client de téléchargement ou Readarr.

- Un exemple de cela serait :
  - Client de téléchargement : Chemin de téléchargement : /mnt/user/downloads:/downloads
  - Readarr : Chemin de téléchargement : /mnt/user/downloads:/data
- Dans cet exemple, le client de téléchargement place ses téléchargements dans /downloads et dit ensuite à Readarr, une fois qu'il a terminé, que le livre terminé se trouve dans /downloads. Readarr vient ensuite et dit "D'accord, cool, laisse-moi vérifier dans /downloads". Eh bien, à l'intérieur de Readarr, vous n'avez pas alloué un chemin /downloads, vous avez alloué un chemin /data, donc cela génère cette erreur.
- La solution la plus simple consiste à être CONSISTANT. Si vous utilisez un schéma dans votre client de téléchargement, utilisez-le partout.

- L'équipe Readarr est très favorable à l'utilisation de /data.
  - Client de téléchargement : /mnt/user/data/downloads:/data/downloads
  - Readarr : /mnt/user/data:/data

- Maintenant, dans le client de téléchargement, vous pouvez spécifier où placer vos téléchargements dans /data, cela varie en fonction du client, mais vous devriez pouvoir lui dire "Oui, client de téléchargement, placez mes fichiers dans." /data/torrents (ou usenet)/books et comme vous avez utilisé /data dans Readarr, lorsque le client de téléchargement dit à Readarr qu'il a terminé, Readarr viendra et dira "Super, j'ai un /data et je peux aussi voir /torrents (ou usenet)/books, tout va bien dans le monde."
- Il existe de nombreux bons articles : notre wiki [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH. Ces guides mettent l'accent sur les liens physiques et les déplacements instantanés (déplacements atomiques), mais le concept général des conteneurs et du fonctionnement de la correspondance des chemins est au cœur de ces discussions.

- Si vous passez d'un système d'exploitation à un autre ou d'un système natif à Docker, vous avez besoin d'une correspondance de chemin distant. Consultez le [Guide de correspondance de chemin distant de TRaSH pour Radarr](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) pour plus d'informations. Le concept est le même pour tous les \*Arrs.

- Si vous obtenez cette erreur avec Calibre, Redarr ne peut pas accéder à la bibliothèque de Calibre. La résolution est la même : corrigez les montages incohérents de vos conteneurs. Sinon, créez une correspondance de chemin distant pour mapper le chemin de la bibliothèque de Calibre au chemin accessible de Readarr. Une correspondance de chemin distant n'est nécessaire que si vous passez d'un système d'exploitation à un autre ou d'un serveur à un autre. Si tout est dans Docker, il est préférable de corriger vos montages.

#### Téléchargement dans le dossier racine

{#downloads-in-root-folder}

- Dans l'application, un dossier racine est défini comme le dossier de la bibliothèque multimédia configurée. Il ne s'agit pas du dossier racine d'un montage. Votre client de téléchargement télécharge des fichiers incomplets ou complets (ou déplace les téléchargements terminés) dans votre dossier racine (bibliothèque).
- Cela cause fréquemment des problèmes, y compris la perte de données, et ne doit pas être fait. Pour résoudre ce problème, modifiez votre client de téléchargement afin qu'il ne place pas les téléchargements dans votre dossier racine. Notez que "placer" inclut également si la catégorie de votre client de téléchargement est définie sur votre dossier racine ou si NZBGet/SABnzbd a le tri activé et trie vers votre dossier racine.
- Veuillez noter que cette vérification examine tous les dossiers racines définis/configurés, pas seulement les dossiers racines actuellement utilisés. En d'autres termes, le dossier dans lequel votre client de téléchargement télécharge ou déplace les téléchargements terminés ne doit pas être le même dossier que vous avez configuré comme dossier racine/bibliothèque/destination finale des médias dans l'application *arr.
- Les dossiers racines configurés (également appelés dossiers de bibliothèque) se trouvent dans [Paramètres => Gestion des médias => Dossiers racines](/readarr/settings/#root-folders)
- Un exemple est si vos téléchargements vont dans `\data\downloads`, alors vous avez un dossier racine défini comme `\data\downloads`.
- Il est recommandé d'utiliser des chemins comme `\data\media\` pour votre dossier racine/bibliothèque et `\data\downloads\` pour vos téléchargements.
- Consultez notre [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH pour plus d'informations sur la configuration correcte et optimale des chemins. Notez que les concepts s'appliquent à Docker et aux systèmes non-Docker.

> Votre dossier de téléchargement où votre client de téléchargement place les téléchargements et votre dossier racine/bibliothèque DOIVENT être séparés. \*Arr importera le(s) fichier(s) du dossier de votre client de téléchargement dans votre bibliothèque. Le client de téléchargement ne doit rien déplacer ni télécharger dans votre bibliothèque.
{.is-warning}

#### Mauvais paramètres du client de téléchargement

- L'emplacement vers lequel votre client de téléchargement télécharge les fichiers pose problème. Consultez les journaux pour plus d'informations. Cela peut être dû à des autorisations incorrectes ou à une tentative de passage de Windows à Linux ou de Linux à Windows sans correspondance de chemin distant.

#### Mauvaise correspondance de chemin distant

- L'emplacement vers lequel votre client de téléchargement télécharge les fichiers pose problème. Vérifiez les journaux pour obtenir plus d'informations. Cela peut être dû à des problèmes de permissions ou à une tentative de passer de Windows à Linux ou de Linux à Windows sans mappage de chemin distant. Consultez le [Guide de mappage de chemin distant de TRaSH](https://trash-guides.info/Readarr/Readarr-remote-path-mapping/) de TRaSH pour plus d'informations.

#### Erreur de permissions

- Readarr ou l'utilisateur readarr en cours d'exécution ne peut pas accéder à l'emplacement vers lequel votre client de téléchargement télécharge les fichiers. Il s'agit généralement d'un problème de permissions.

#### Le montage de l'auteur est en lecture seule

{#author-mount-ro}

- Le montage contenant un chemin d'auteur est monté en lecture seule. Vérifiez les paramètres de montage et les propriétés/permissions.

#### Le fichier distant a été supprimé en cours de traitement

- Un fichier accessible via une correspondance de chemin distant semble avoir été supprimé avant la fin du traitement.

#### Le chemin distant est utilisé et l'importation a échoué

- Vérifiez vos journaux pour plus d'informations ; consultez nos guides de dépannage.

### Gestion des téléchargements terminés/échoués

#### La gestion des téléchargements terminés est désactivée

- (Cet avertissement est généré uniquement pour les utilisateurs existants avant la mise en œuvre de la fonctionnalité de gestion des téléchargements terminés. Cette fonctionnalité est désactivée par défaut pour garantir que le système continue de fonctionner comme prévu pour les configurations actuelles.)
- Il est recommandé d'utiliser la gestion des téléchargements terminés car elle offre une meilleure compatibilité avec la logique de décompression et de post-traitement des différents clients de téléchargement. Avec cette fonctionnalité, Readarr n'importera un téléchargement que lorsque le client de téléchargement le signalera comme prêt.
- Si vous souhaitez activer la gestion des téléchargements terminés, vous devez vérifier ce qui suit : * Avertissement : La gestion des téléchargements terminés ne fonctionne correctement que si le client de téléchargement et Readarr sont sur la même machine, car il obtient le chemin à importer directement à partir du client de téléchargement, sinon une correspondance distante est nécessaire.

### Indexeurs

#### Aucun indexeur disponible avec la recherche automatique activée, Readarr ne fournira aucun résultat de recherche automatique

- En termes simples, vous n'avez aucun de vos indexeurs configurés pour autoriser les recherches automatiques.
- Allez dans Paramètres => Indexeurs, sélectionnez un indexeur que vous souhaitez autoriser les recherches automatiques, puis cliquez sur Enregistrer.

#### Aucun indexeur disponible avec la synchronisation RSS activée, Readarr ne récupérera pas automatiquement les nouvelles sorties

- Ainsi, Readarr utilise le flux RSS pour récupérer les nouvelles sorties au fur et à mesure qu'elles arrivent. Plus d'informations à ce sujet ici.
- Pour corriger ce problème, allez dans Paramètres => Indexeurs, sélectionnez un indexeur que vous avez et activez la synchronisation RSS.

#### Aucun indexeur n'est activé

- Readarr nécessite des indexeurs pour pouvoir découvrir de nouvelles sorties. Veuillez lire le wiki pour obtenir des instructions sur la façon d'ajouter des indexeurs.

### Les indexeurs activés ne prennent pas en charge la recherche

- Aucun des indexeurs que vous avez activés ne prend en charge la recherche. Cela signifie que Readarr ne pourra trouver de nouvelles sorties que via les flux RSS. Mais la recherche de livres (recherche automatique ou recherche manuelle) ne renverra jamais de résultats. Évidemment, la seule façon de remédier à cela est d'ajouter un autre indexeur.

#### Aucun indexeur disponible avec la recherche interactive activée

- Aucun des indexeurs que vous avez activés ne prend en charge la recherche interactive. Cela signifie que l'application ne pourra trouver de nouvelles sorties que via les flux RSS ou une recherche automatique.

#### Les indexeurs ne sont pas disponibles en raison d'échecs

- Des erreurs se produisent lorsque Readarr essaie d'utiliser l'un de vos indexeurs. Pour limiter les tentatives de répétition, Readarr n'utilisera pas l'indexeur pendant une durée de plus en plus longue (jusqu'à 24 heures).
- Ce mécanisme est déclenché si Readarr n'a pas pu obtenir de réponse de l'indexeur (cela peut être dû à un problème de DNS, de connexion proxy/VPN, d'authentification ou d'indexeur), ou s'il n'a pas pu récupérer le fichier NZB/torrent de l'indexeur. Veuillez consulter les journaux pour déterminer quel type d'erreur cause le problème.
- Vous pouvez éviter l'avertissement en désactivant l'indexeur concerné.
- Exécutez le test sur l'indexeur pour forcer Readarr à vérifier à nouveau l'indexeur, veuillez noter que l'avertissement de vérification de l'état de santé ne disparaîtra pas toujours immédiatement.

#### Tous les points de terminaison de Jackett sont utilisés

- Le point de terminaison /all de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc maintenant nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il faut l'éviter et ne pas l'utiliser.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation du point de terminaison /all n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
  - la combinaison de modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques de l'indexeur (\>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers dans /all renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez plus aucun résultat.

##### Solutions

- Ajoutez chaque tracker dans Jackett manuellement en tant qu'indexeur dans \*Arr
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui provient de l'équipe de développement de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur point de terminaison unique et utilisez `multi` si la synchronisation est utilisée.

### Dossiers de livres

#### Dossier racine manquant

- Cette erreur est généralement identifiée si un auteur recherche un dossier racine mais que ce dossier racine n'est plus disponible.
- Cette erreur peut également se produire si une liste est toujours pointée vers un dossier racine mais que ce dossier racine n'est plus disponible.
- Si vous souhaitez supprimer cet avertissement, il vous suffit de trouver l'album qui utilise toujours l'ancien dossier racine et de le modifier pour le dossier racine correct.

- La manière la plus simple de trouver l'auteur posant problème est la suivante :

  - Allez dans l'onglet Auteur (Bibliothèque)
  - Créez un filtre personnalisé avec l'ancien chemin du dossier racine
  - Sélectionnez l'édition en masse dans la barre supérieure et, dans la liste déroulante des chemins racine, sélectionnez le nouveau chemin racine vers lequel vous souhaitez déplacer ces auteurs.
  - Ensuite, vous recevrez une fenêtre contextuelle indiquant Souhaitez-vous déplacer les dossiers des auteurs vers 'chemin racine' ? Cela indiquera également Cela renommera également le dossier de l'auteur selon le format de dossier de l'auteur dans les paramètres. Sélectionnez simplement Non si vous ne souhaitez pas que Lidarr déplace vos fichiers.
  - Exécutez la tâche de vérification de l'état de santé dans Système => Tâches

### Importer des listes

#### Les listes d'importation ne sont pas disponibles en raison d'échecs

- En général, cela signifie simplement que Readarr n'est plus en mesure de communiquer via l'API ou en se connectant à votre fournisseur de listes choisi. Si le problème persiste, il est préférable de les contacter pour les exclure, car leurs systèmes peuvent être surchargés de temps en temps.

## Espace disque

- Cette section vous montrera l'espace disque disponible.
- Dans Docker, cela peut être délicat car il affiche généralement l'espace disponible dans votre image Docker.

## À propos

- Cela vous donnera des informations sur votre installation actuelle de Readarr.

## Plus d'informations

- Page d'accueil : Page d'accueil de Readarr
- Wiki : Vous êtes déjà ici
- Reddit : r/readarr
- Discord : Rejoignez notre discord
- Dons : Si vous vous sentez généreux et que vous souhaitez faire un don, cliquez ici
- Dons à Sonarr : Si vous vous sentez généreux et que vous souhaitez faire un don au projet qui a tout commencé, cliquez ici
- Source : GitHub
- Demandes de fonctionnalités : Vous avez une excellente idée, déposez-la ici

# Tâches

## Planifiées

- Cette section répertorie toutes les tâches planifiées exécutées par Readarr.

- Vérification de la mise à jour de l'application - Cette tâche s'exécute à l'heure indiquée dans l'interface utilisateur, vérifiant si Readarr est à la version la plus récente, puis déclenchant le script de mise à jour pour mettre à jour Readarr. Paramètres => Mise à jour

> Remarque : Si vous utilisez Docker, cela ne mettra pas à jour votre conteneur car une nouvelle image devra être téléchargée.
{.is-warning}

- Sauvegarde - Cette tâche effectuera une sauvegarde de la base de données de votre Readarr selon un calendrier défini. Vous trouverez plus de détails à ce sujet ici. Vous trouverez plus d'informations sur les sauvegardes dans Système => Sauvegardes.
- Vérification de l'état de santé - La vérification de l'état de santé s'exécute à l'heure indiquée dans l'interface utilisateur, vérifiant l'état de santé global de votre Readarr. Pour voir une liste des problèmes de santé possibles, consultez l'entrée du wiki sur les vérifications de l'état de santé.
- Entretien - À l'heure indiquée dans l'interface utilisateur, cela dépoussière les toiles d'araignée, balaye et aspire les sols, les lustre et même fait de jolies petites notes pliées bien rangées juste pour vous. Mais il ne sort pas les poubelles. Il n'est tout simplement pas assez payé pour ça.
- Synchronisation des listes d'importation - À l'heure indiquée dans l'interface utilisateur, cela exécutera vos listes et importera tous les nouveaux livres possibles. Plus d'informations sur les listes peuvent être trouvées dans Paramètres => Listes.
- Nettoyage des messages - À l'heure indiquée dans l'interface utilisateur, cela nettoie les messages qui apparaissent dans le coin inférieur gauche de Readarr.
- Actualiser l'auteur - Cela actualise tous les auteurs de votre bibliothèque.
- Actualiser les téléchargements surveillés - Cela actualise la file d'attente des téléchargements située sous Activité. Il s'agit essentiellement de vérifier si votre client de téléchargement a terminé les téléchargements.
- Analyser à nouveau les dossiers - Cela analyse tous les dossiers de livres pour vérifier si un livre existe ou non, et met à jour son statut en conséquence.
- Synchronisation RSS - Cela exécutera la synchronisation RSS. Cela peut être modifié dans Paramètres => Options. Vous trouverez plus d'informations sur la fonctionnalité RSS dans notre FAQ.

> Toutes ces tâches peuvent être exécutées manuellement en dehors de leurs horaires prévus en cliquant sur l'icône à l'extrême droite de chacune des tâches.
{.is-info}

## File d'attente

La file d'attente vous montrera les tâches en cours d'exécution et à venir, ainsi qu'un historique des tâches récemment exécutées et la durée de ces tâches.

# Sauvegarde

> Si vous recherchez comment sauvegarder/restaurer votre instance Readarr, cliquez [ici](/readarr/faq).
{.is-info}

- Dans la section Sauvegarde, vous verrez les sauvegardes précédentes (sauf si vous avez une nouvelle installation qui n'a pas effectué de sauvegardes).
  
- Sauvegarder maintenant - Cette option déclenchera une sauvegarde manuelle de la base de données de votre Readarr.
- Restaurer la sauvegarde - Cela ouvrira un nouvel écran pour restaurer à partir d'une sauvegarde précédente
  - En sélectionnant Choisir un fichier, cela demandera à votre navigateur d'ouvrir une boîte de dialogue pour restaurer à partir d'une sauvegarde Zip de Readarr
  
- Si vous avez des sauvegardes précédentes et que vous souhaitez les télécharger depuis Readarr pour les placer dans un emplacement non standard, vous pouvez simplement sélectionner l'un de ces fichiers pour les télécharger.
- À droite de chaque téléchargement précédent, vous avez deux options.
  - Restaurer (Icône d'horloge) - Pour restaurer à partir d'une sauvegarde précédente - Cela ouvrira une nouvelle fenêtre pour confirmer que vous souhaitez restaurer à partir de cette sauvegarde
  - Supprimer (Icône de corbeille) - Pour supprimer une sauvegarde précédente

# Mises à jour

- L'écran des mises à jour affichera les 5 dernières mises à jour effectuées ainsi que la version actuelle sur laquelle vous vous trouvez.
- Cette page affichera également les notes de mise à jour des développeurs vous indiquant ce qui a été corrigé ou ajouté à Readarr (Réjouissez-vous !)
  
> Une version de maintenance contient des corrections de bugs et diverses améliorations. Jetez un coup d'œil à l'historique des commits pour plus de détails.
{.is-info}

# Événements

- L'onglet Événements vous montrera ce qui s'est passé dans votre Readarr. Cela peut être utilisé pour diagnostiquer certains problèmes légers. Cependant, cela ne remplace pas les journaux de trace discutés dans la section Journalisation.

> Les événements sont l'équivalent des journaux INFO. {.is-info}

- Composants - Cette colonne vous indiquera quel composant de Readarr a été déclenché
- Message - Cette colonne vous indiquera quel message a été envoyé par le composant de la colonne précédente.
- Icône d'engrenage - Cette option vous permet de modifier le nombre de composants/messages affichés par page (la valeur par défaut est de 50)
- Options en haut de la page
  - Actualiser - Cette option actualisera la page actuelle, en récupérant un nouveau journal des événements
  - Effacer - Cela effacera le journal des événements actuel, vous permettant de repartir à zéro

# Fichiers journaux

- Cette page vous permet de télécharger et de voir les fichiers journaux actuels disponibles pour Readarr.

- Sur la première ligne, vous trouverez plusieurs options pour contrôler vos fichiers journaux.

- Sur la première ligne, tout à gauche, il y a une liste déroulante qui vous permet de passer des fichiers journaux aux fichiers journaux de mise à jour.
  - Fichiers journaux - L'essentiel de tout problème de support, vous trouverez plus d'informations sur les fichiers journaux ici.
  - Fichiers journaux de mise à jour - Cela affichera les fichiers journaux associés au script de mise à jour de Readarr

> Si vous utilisez Docker, cela sera vide car vous devriez mettre à jour en téléchargeant une nouvelle image Docker.
{.is-info}

- Actualiser - Cela actualisera la page actuelle et affichera tous les journaux nouvellement créés
- Supprimer - Cela effacera tous les journaux, vous permettant de repartir à zéro
- Nom du fichier - Cela affichera le nom du fichier associé au journal
- Dernière écriture - Il s'agit de l'heure locale à laquelle ce fichier journal particulier a été écrit.
  - Readarr utilise des fichiers journaux en rotation limités à 1 Mo chacun. Le fichier journal actuel est toujours readarr.txt, pour les autres fichiers, readarr.0.txt est le plus récent (plus le nombre est élevé, plus il est ancien) jusqu'à un total de 51 fichiers journaux. Ce fichier journal contient les entrées `fatal`, `error`, `warn` et `info`.
  - Lorsque le niveau de journalisation de débogage est activé, des fichiers journaux supplémentaires readarr.debug.txt en rotation seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info` et `debug`. Ils couvrent généralement une période d'environ 40 heures.
  - Lorsque le niveau de journalisation de trace est activé, des fichiers journaux supplémentaires readarr.trace.txt en rotation seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent les entrées `fatal`, `error`, `warn`, `info`, `debug` et `trace`. En raison de la verbosité de la trace, ils ne couvrent que quelques heures au maximum.