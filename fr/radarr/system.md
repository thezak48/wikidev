---
title: Système Radarr
description: 
published: true
date: 2022-10-19T22:59:06.531Z
tags: radarr, needs-love
editor: markdown
dateCreated: 2021-05-25T02:28:35.194Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Statut](#statut)
  - [Santé](#santé)
    - [Avertissements système](#avertissements-système)
      - [La branche n'est pas une branche de version valide](#la-branche-nest-pas-une-branche-de-version-valide)
      - [Mise à jour de la version .NET](#mise-à-jour-de-la-version-net)
        - [Correction des installations Docker](#correction-des-installations-docker)
        - [Correction des installations FreeBSD](#correction-des-installations-freebsd)
        - [Correction des installations autonomes](#correction-des-installations-autonomes)
      - [La version actuellement installée de Mono est ancienne et non prise en charge](#la-version-actuellement-installée-de-mono-est-ancienne-et-non-prise-en-charge)
      - [La version actuellement installée de SQLite n'est pas prise en charge](#la-version-actuellement-installée-de-sqlite-nest-pas-prise-en-charge)
      - [Échec de l'intégrité de la base de données](#échec-de-lintégrité-de-la-base-de-données)
      - [Une nouvelle mise à jour est disponible](#une-nouvelle-mise-à-jour-est-disponible)
      - [Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur](#impossible-dinstaller-la-mise-à-jour-car-le-dossier-de-démarrage-nest-pas-accessible-en-écriture-par-lutilisateur)
      - [La mise à jour ne sera pas possible pour éviter la suppression des données de l'application lors de la mise à jour](#la-mise-à-jour-ne-sera-pas-possible-pour-éviter-la-suppression-des-données-de-lapplication-lors-de-la-mise-à-jour)
      - [La branche est destinée à une version précédente](#la-branche-est-destinée-à-une-version-précédente)
      - [Impossible de se connecter à signalR](#impossible-de-se-connecter-à-signalr)
        - [Nginx](#nginx)
        - [Apache2](#apache2)
        - [Caddy](#caddy)
      - [Échec de la résolution de l'adresse IP pour l'hôte proxy configuré](#échec-de-la-résolution-de-ladresse-ip-pour-lhôte-proxy-configuré)
      - [Échec du test du proxy](#échec-du-test-du-proxy)
      - [L'heure système est décalée de plus d'un jour](#lheure-système-est-décalée-de-plus-dun-jour)
      - [Les paramètres de l'indexeur PTP sont obsolètes](#les-paramètres-de-lindexeur-ptp-sont-obsolètes)
      - [Les versions Mono et x86 prennent fin](#les-versions-mono-et-x86-prennent-fin)
    - [Clients de téléchargement](#clients-de-téléchargement)
      - [Aucun client de téléchargement n'est disponible](#aucun-client-de-téléchargement-nest-disponible)
      - [Impossible de communiquer avec le client de téléchargement](#impossible-de-communiquer-avec-le-client-de-téléchargement)
      - [Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance](#les-clients-de-téléchargement-ne-sont-pas-disponibles-en-raison-dune-défaillance)
      - [Activer la gestion des téléchargements terminés](#activer-la-gestion-des-téléchargements-terminés)
      - [Mauvaise correspondance du chemin distant Docker](#mauvaise-correspondance-du-chemin-distant-docker)
      - [Téléchargement dans le dossier racine](#téléchargement-dans-le-dossier-racine)
      - [Mauvais paramètres du client de téléchargement](#mauvais-paramètres-du-client-de-téléchargement)
      - [Mauvaise correspondance du chemin distant](#mauvaise-correspondance-du-chemin-distant)
      - [Erreur d'autorisations](#erreur-dautorisations)
      - [Le fichier distant a été supprimé en cours de traitement](#le-fichier-distant-a-été-supprimé-en-cours-de-traitement)
      - [Le chemin distant est utilisé et l'importation a échoué](#le-chemin-distant-est-utilisé-et-limportation-a-échoué)
    - [Gestion des téléchargements terminés/échoués](#gestion-des-téléchargements-terminéséchoués)
      - [La gestion des téléchargements terminés est désactivée](#la-gestion-des-téléchargements-terminés-est-désactivée)
    - [Indexeurs](#indexeurs)
      - [Aucun indexeur disponible avec la recherche automatique activée, Radarr ne fournira aucun résultat de recherche automatique](#aucun-indexeur-disponible-avec-la-recherche-automatique-activée-radarr-ne-fournira-aucun-résultat-de-recherche-automatique)
      - [Aucun indexeur disponible avec la synchronisation RSS activée, Radarr ne récupérera pas automatiquement les nouvelles versions](#aucun-indexeur-disponible-avec-la-synchronisation-rss-activée-radarr-ne-récupérera-pas-automatiquement-les-nouvelles-versions)
      - [Aucun indexeur n'est activé](#aucun-indexeur-nest-activé)
    - [Les indexeurs activés ne prennent pas en charge la recherche](#les-indexeurs-activés-ne-prennent-pas-en-charge-la-recherche)
      - [Aucun indexeur disponible avec la recherche interactive activée](#aucun-indexeur-disponible-avec-la-recherche-interactive-activée)
      - [Les indexeurs ne sont pas disponibles en raison de défaillances](#les-indexeurs-ne-sont-pas-disponibles-en-raison-de-défaillances)
      - [Jackett utilise tous les points de terminaison](#jackett-utilise-tous-les-points-de-terminaison)
        - [Solutions](#solutions)
    - [Dossiers de films](#dossiers-de-films)
      - [Dossier racine manquant](#dossier-racine-manquant)
    - [Films](#films)
      - [Le film a été supprimé de TMDb](#le-film-a-été-supprimé-de-tmdb)
      - [Les listes ne sont pas disponibles en raison de défaillances](#les-listes-ne-sont-pas-disponibles-en-raison-de-défaillances)
    - [Notifications](#notifications)
    - [Discord en tant que notification Slack](#discord-en-tant-que-notification-slack)
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

- Cette page contient une liste des erreurs de vérification de santé. Ces vérifications de santé sont effectuées périodiquement par Radarr et lors de certains événements. Les avertissements et erreurs résultants sont répertoriés ici pour donner des conseils sur la façon de les résoudre.

### Avertissements système

#### La branche n'est pas une branche de version valide

- La branche que vous avez définie n'est pas une branche de version valide. Vous ne recevrez pas de mises à jour. Veuillez changer pour l'une des [branches de version actuelles](/radarr/faq#how-do-i-update-radarr).

#### Mise à jour de la version .NET

{#update-to-net-core-version}

- Les versions plus récentes de Radarr sont ciblées pour .NET6 ou une version ultérieure. Les versions Mono ne sont pas fournies ni prises en charge à partir de la version 4. La version 3.2.2 est la dernière version de Radarr à prendre en charge les versions Mono héritées. Vous utilisez l'une de ces versions Mono héritées, mais votre plateforme prend en charge .NET.

Consultez les entrées ci-dessous pour savoir comment passer des versions Mono obsolètes et non prises en charge à .NET.

- [Correction des installations Docker](#fixing-docker-installs)
- [Correction des installations FreeBSD](#fixing-freebsd-installs)
- [Correction des installations autonomes](#fixing-standalone-installs)
{.links-list}

##### Correction des installations Docker

- Assurez-vous que votre branche est correcte pour votre mainteneur Docker et répétez votre conteneur

##### Correction des installations FreeBSD

- Mettez simplement à jour le port Radarr avec `pkg update && pkg upgrade`
- (Facultatif) Supprimez le package mono si vous le souhaitez

##### Correction des installations autonomes

Des erreurs telles que :

```none
Impossible d'ouvrir l'assembly '/opt/Radarr/Radarr' : Le fichier ne contient pas une image CIL valide
```

- Sauvegardez votre configuration existante avant l'étape suivante.
- Cela ne devrait se produire que sur les hôtes Linux. N'installez pas le runtime ou le SDK .NET de Microsoft.
- Pour remédier à cela, téléchargez la version correcte pour votre architecture et remplacez vos binaires existants (application)
- En bref, vous devrez supprimer vos binaires existants (contenu ou dossier de /opt/Radarr) et les remplacer par le contenu du .tar.gz que vous venez de télécharger, puis mettez à jour votre fichier de service pour ne pas utiliser mono.

> NE DÉCOMPRESSEZ PAS SIMPLEMENT LE TÉLÉCHARGEMENT PAR-DESSUS VOS ANCIENS BINAIRES.
> VOUS DEVEZ D'ABORD SUPPRIMER LES ANCIENS.
{.is-warning}

- Ce qui suit est un script développé par la communauté pour supprimer votre installation mono et la remplacer par l'installation .NET. Les contributions et les corrections sont les bienvenues.
- Cela suppose que vous êtes sur la branche Radarr `master`, donc mettez à jour la variable si nécessaire
- Cela suppose que Radarr s'exécute en tant qu'utilisateur `radarr`, donc mettez à jour les variables si nécessaire
- Cela suppose que Radarr est installé dans `/opt/Radarr`, donc mettez à jour les variables si nécessaire

```bash
#!/bin/bash
## Variables utilisateur
installdir="/opt/Radarr"
APPUSER="radarr"
branch="master"
## /Variables utilisateur
app="radarr"
ARCH=$(dpkg --print-architecture)
# Arrêter \*arr
sudo systemctl stop $app
# obtenir l'architecture
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Architecture non prise en charge"
    exit 1
    ;;
esac
echo "Téléchargement..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Téléchargement et extraction des fichiers d'installation"
echo "Déplacement de l'installation existante"
sudo mv "$installdir/" "$installdir.old/"
echo "Installation..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "Application installée"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### La version actuellement installée de Mono est ancienne et non prise en charge

- Radarr est écrit en .NET et nécessite Mono pour s'exécuter sur de très anciens processeurs ARM. Mono 5.20 est le minimum absolu pour Radarr.
- La procédure de mise à niveau de Mono varie selon la plateforme.

> Mono n'est plus pris en charge à partir de la version 4.0 de Radarr
{.is-warning}

#### La version actuellement installée de SQLite n'est pas prise en charge

- Radarr stocke ses données dans une base de données SQLite. La bibliothèque SQLite3 installée sur votre système est trop ancienne. Radarr nécessite au moins la version 3.9.0.

> Notez que Radarr utilise `libSQLite3.so` qui peut être contenue ou non dans un package de mise à niveau SQLite3.
{.is-info}

#### Échec de l'intégrité de la base de données

- Vos bases de données ont échoué à une [vérification d'intégrité de SQLite Pragma](https://www.sqlite.org/pragma.html#pragma_integrity_check) et présentent une certaine corruption.
- Si `Radarr.db` est corrompu, [veuillez consulter cette entrée de FAQ](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)
- Si `logs.db` est corrompu : Arrêtez Radarr, supprimez `logs.db` et tous les fichiers `logs.wal`.
- Si les deux sont corrompus, suivez les processus respectifs ci-dessus.

#### Une nouvelle mise à jour est disponible

- Réjouissez-vous, les développeurs ont publié une nouvelle mise à jour. Cela signifie généralement de nouvelles fonctionnalités géniales et une résolution de nombreux problèmes (n'est-ce pas ?). Apparemment, vous n'avez pas activé la mise à jour automatique, vous devrez donc trouver comment mettre à jour votre plateforme. Appuyer sur le bouton Installer sur la page Système => Mises à jour est probablement un bon point de départ.

> Cet avertissement n'apparaîtra pas si votre version actuelle a moins de 14 jours
{.is-info}

#### Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur

- Cela signifie que Radarr ne pourra pas se mettre à jour automatiquement. Vous devrez mettre à jour Radarr manuellement ou définir les autorisations sur le répertoire de démarrage de Radarr (le répertoire d'installation) pour permettre à Radarr de se mettre à jour lui-même.

#### La mise à jour ne sera pas possible pour éviter la suppression des données de l'application lors de la mise à jour

- Radarr a détecté que le dossier AppData pour votre système d'exploitation est situé à l'intérieur du répertoire qui contient les binaires de Radarr. Normalement, il devrait s'agir de C:\ProgramData pour Windows et ~/.config pour Linux.

- Veuillez consulter Système => Info pour voir les répertoires AppData et de démarrage actuels.
- Cela signifie que Radarr ne pourra pas se mettre à jour sans risquer de perdre des données.
- Si vous êtes sous Linux, vous devrez probablement modifier le répertoire personnel de l'utilisateur qui exécute Radarr et copier le contenu actuel du répertoire ~/.config/Radarr pour préserver votre base de données.

#### La branche est destinée à une version précédente

- La branche de mise à jour configurée dans Paramètres/Général est destinée à une version précédente de Radarr, par conséquent, l'instance ne verra pas les informations de mise à jour correctes dans le flux Mises à jour du système et risque de ne pas recevoir de nouvelles mises à jour lorsqu'elles seront publiées.

#### Impossible de se connecter à signalR

- signalR permet les mises à jour dynamiques de l'interface utilisateur. Si votre navigateur ne peut pas se connecter à signalR sur votre serveur, vous ne verrez aucune mise à jour en temps réel dans l'interface utilisateur.
- La cause la plus courante de ce problème est l'utilisation d'un proxy inverse ou de Cloudflare.
- Cloudflare nécessite l'activation des websockets.

##### Nginx

- Nginx nécessite l'ajout suivant au bloc de localisation de l'application :

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Assurez-vous de ne pas inclure proxy_set_header Connection "Upgrade"; comme suggéré par la documentation de nginx. CELA NE FONCTIONNERA PAS
> Voir <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache2

Pour le proxy inverse Apache2, vous devez activer les modules suivants : proxy, proxy_http et proxy_wstunnel. Ensuite, ajoutez cette directive de tunnel websocket à la configuration de votre hôte virtuel :

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:7878/$1 [P,L]
```

Si vous avez un proxy inverse dans un sous-répertoire, la RewriteRule doit inclure votre chemin de base, par exemple :

```none
RewriteRule /radarr/(.*) ws://127.0.0.1:7878/radarr/$1 [P,L]
```

Si Radarr ne s'exécute pas sur la même machine que votre proxy inverse, remplacez 127.0.0.1 par l'adresse IP/DNS appropriée de votre application Radarr.

##### Caddy

Pour Caddy (V1), utilisez ceci :
Remarque : vous devrez également ajouter la directive websocket à votre configuration Radarr

```none
 proxy /radarr 127.0.0.1:7878 {
     websocket
     transparent
 }
```

#### Échec de la résolution de l'adresse IP pour l'hôte proxy configuré

- Vérifiez vos paramètres de proxy et assurez-vous qu'ils sont corrects
- Vérifiez que votre proxy est actif, en cours d'exécution et accessible

#### Échec du test du proxy

- Votre proxy configuré a échoué lors du test, vérifiez l'erreur HTTP fournie et/ou consultez les journaux pour plus de détails.

#### L'heure système est décalée de plus d'un jour

- L'heure système est décalée de plus d'un jour. Les tâches planifiées peuvent ne pas s'exécuter correctement tant que l'heure n'est pas corrigée.
- Vérifiez l'heure système et assurez-vous qu'elle est synchronisée avec un serveur de temps fiable et précis.

#### Les paramètres de l'indexeur PTP sont obsolètes

- Les indexeurs PassThePopcorn suivants ont des paramètres obsolètes et doivent être mis à jour.

#### Les versions Mono et x86 prennent fin

- Les versions Mono et x86 ne sont plus prises en charge à partir de la version 4. Si vous recevez cette erreur, cela signifie que vous utilisez la version Mono de l'application ou la version x86. Malheureusement, en raison de la difficulté croissante de la prise en charge du développement de ces versions héritées, nous cesserons de les prendre en charge et, par conséquent, de les publier à l'avenir. Il est donc conseillé de passer à un système d'exploitation pris en charge qui ne nécessite ni x86 ni Mono. Vous pouvez également envisager d'utiliser Docker pour vos besoins.

### Clients de téléchargement

#### Aucun client de téléchargement n'est disponible

- Un client de téléchargement correctement configuré et activé est requis pour que Radarr puisse télécharger des médias. Étant donné que Radarr prend en charge différents clients de téléchargement, vous devez déterminer celui qui correspond le mieux à vos besoins. Si vous avez déjà un client de téléchargement installé, vous devez le configurer pour que Radarr l'utilise et créer une catégorie. Voir Paramètres => Client de téléchargement.

#### Impossible de communiquer avec le client de téléchargement

- Radarr n'a pas pu communiquer avec le client de téléchargement configuré. Veuillez vérifier si le client de téléchargement est opérationnel et vérifier à nouveau l'URL. Cela peut également indiquer une erreur d'authentification.
- Cela est généralement dû à une mauvaise configuration du client de téléchargement. Voici quelques points que vous pouvez vérifier :
  - L'adresse IP de votre client de téléchargement, si celui-ci est sur la même machine physique, il s'agit généralement de 127.0.0.1
  - Le numéro de port que votre client de téléchargement utilise, ces champs sont remplis avec le numéro de port par défaut, mais si vous l'avez modifié, vous devrez entrer le même numéro dans Radarr.
  - Assurez-vous que le chiffrement SSL n'est pas activé si vous utilisez à la fois votre instance Radarr et votre client de téléchargement sur un réseau local. Consultez la FAQ SSL pour plus d'informations.
  - Assurez-vous que l'IPv6 est désactivé sur le système s'il n'est pas fonctionnel.
  - Assurez-vous qu'un serveur DNS (par exemple, pihole) ne limite pas le nombre de requêtes.

#### Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance

- Un ou plusieurs de vos clients de téléchargement ne répondent pas aux demandes de Radarr. Par conséquent, Radarr a décidé d'arrêter temporairement les requêtes au client de téléchargement selon son cycle normal d'une minute, qui est normalement utilisé pour suivre les téléchargements en cours et importer les téléchargements terminés. Cependant, Radarr continuera à essayer d'envoyer des téléchargements au client, mais il échouera très probablement.
- Vous devez inspecter Système=>Journaux pour connaître la raison des échecs.
- Si vous n'utilisez plus ce client de téléchargement, désactivez-le dans Radarr pour éviter les erreurs.

#### Activer la gestion des téléchargements terminés

- Radarr nécessite la gestion des téléchargements terminés pour pouvoir importer les fichiers téléchargés par le client de téléchargement. Il est recommandé d'activer la gestion des téléchargements terminés. (La gestion des téléchargements terminés est activée par défaut pour les nouveaux utilisateurs.)

#### Mauvaise correspondance du chemin distant Docker

- Cette erreur est généralement associée à des chemins Docker incorrects dans votre client de téléchargement ou Radarr.

- Un exemple de cela serait :
  - Client de téléchargement : Chemin de téléchargement : /mnt/user/downloads:/downloads
  - Radarr : Chemin de téléchargement : /mnt/user/downloads:/data
- Dans cet exemple, le client de téléchargement place ses téléchargements dans /downloads et indique ensuite à Radarr, une fois le téléchargement terminé, que le film terminé se trouve dans /downloads. Radarr vient ensuite et dit "D'accord, cool, je vais vérifier dans /downloads". Eh bien, à l'intérieur de Radarr, vous n'avez pas alloué un chemin /downloads, vous avez alloué un chemin /data, donc il affiche cette erreur.
- La solution la plus simple consiste à être CONSISTANT. Si vous utilisez un schéma dans votre client de téléchargement, utilisez-le partout.

- L'équipe Radarr est un grand fan d'utiliser simplement /data.
  - Client de téléchargement : /mnt/user/data/downloads:/data/downloads
  - Radarr : /mnt/user/data:/data

- Maintenant, dans le client de téléchargement, vous pouvez spécifier où dans /data vous souhaitez placer vos téléchargements. Cela varie en fonction du client, mais vous devriez pouvoir lui dire "Oui, client de téléchargement, placez mes fichiers dans." /data/torrents (ou usenet)/movies et comme vous avez utilisé /data dans Radarr, lorsque le client de téléchargement dit à Radarr que c'est terminé, Radarr vient et dit "Super, j'ai un /data et je peux également voir /torrents (ou usenet)/movies, tout va bien dans le monde."
- Il existe de nombreux bons articles : notre wiki [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH. Ces guides mettent fortement l'accent sur les liens durs et les déplacements instantanés (mouvements atomiques), mais le concept général des conteneurs et du fonctionnement de la correspondance des chemins est au cœur de ces discussions.

- Consultez [le guide TRaSH sur la correspondance des chemins distants](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) pour plus d'informations.

#### Téléchargement dans le dossier racine

{#downloads-in-root-folder}

- Dans l'application, un dossier racine est défini comme le dossier de bibliothèque multimédia configuré. Il ne s'agit pas du dossier racine d'un montage. Votre client de téléchargement télécharge des fichiers incomplets ou complets (ou déplace des téléchargements terminés) dans votre dossier racine (bibliothèque).
- Cela cause fréquemment des problèmes, y compris la perte de données, et ne doit pas être fait. Pour résoudre ce problème, modifiez votre client de téléchargement pour qu'il ne place pas les téléchargements dans votre dossier racine. Notez que « placer » inclut également si la catégorie de votre client de téléchargement est définie sur votre dossier racine ou si NZBGet/SABnzbd a la fonction de tri activée et trie vers votre dossier racine.
- Veuillez noter que cette vérification examine tous les dossiers racines définis/configurés, pas seulement les dossiers racines actuellement utilisés. En d'autres termes, le dossier dans lequel votre client de téléchargement télécharge ou déplace les téléchargements terminés ne doit pas être le même dossier que vous avez configuré comme dossier racine/bibliothèque/destination finale des médias dans l'application *arr.
- Les dossiers racines configurés (alias dossiers de bibliothèque) se trouvent dans [Paramètres => Gestion des médias => Dossiers racines](/radarr/settings/#root-folders)
- Un exemple est si vos téléchargements vont dans `\data\downloads`, alors vous avez un dossier racine défini comme `\data\downloads`.
- Il est recommandé d'utiliser des chemins comme `\data\media\` pour votre dossier racine/bibliothèque et `\data\downloads\` pour vos téléchargements.
- Consultez notre [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH pour plus d'informations sur la configuration correcte et optimale des chemins. Notez que les concepts s'appliquent aux conteneurs et aux non-conteneurs.

> Votre dossier de téléchargement où votre client de téléchargement place les téléchargements et votre dossier racine/bibliothèque DOIVENT être séparés. \*Arr importera le(s) fichier(s) depuis le dossier de votre client de téléchargement dans votre bibliothèque. Le client de téléchargement ne doit rien déplacer ni télécharger dans votre bibliothèque.
{.is-warning}

#### Mauvais paramètres du client de téléchargement

- L'emplacement où votre client de téléchargement télécharge les fichiers pose des problèmes. Vérifiez les journaux pour plus d'informations. Cela peut être dû à des autorisations ou à une tentative de passage de Windows à Linux ou de Linux à Windows sans correspondance de chemin distant.

#### Mauvaise correspondance du chemin distant

- L'emplacement où votre client de téléchargement télécharge les fichiers pose des problèmes. Vérifiez les journaux pour plus d'informations. Cela peut être dû à des autorisations ou à une tentative de passage de Windows à Linux ou de Linux à Windows sans correspondance de chemin distant. Consultez [le guide TRaSH sur la correspondance des chemins distants](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) pour plus d'informations.

#### Erreur d'autorisations

- Radarr ou l'utilisateur radarr qui l'exécute ne peut pas accéder à l'emplacement où votre client de téléchargement télécharge les fichiers. Il s'agit généralement d'un problème d'autorisations.

#### Le fichier distant a été supprimé en cours de traitement

- Un fichier accessible via une correspondance de chemin distant semble avoir été supprimé avant la fin du traitement.

#### Le chemin distant est utilisé et l'importation a échoué

- Vérifiez vos journaux pour plus d'informations ; consultez nos guides de dépannage

### Gestion des téléchargements terminés/échoués

#### La gestion des téléchargements terminés est désactivée

- (Cet avertissement n'est généré que pour les utilisateurs existants avant la mise en œuvre de la fonctionnalité de gestion des téléchargements terminés. Cette fonctionnalité est désactivée par défaut pour garantir que le système continue de fonctionner comme prévu pour les configurations actuelles.)
- Il est recommandé d'utiliser la gestion des téléchargements terminés car elle offre une meilleure compatibilité avec la logique de décompression et de post-traitement des différents clients de téléchargement. Avec elle, Radarr n'importera un téléchargement que lorsque le client de téléchargement le signalera comme prêt.
- Si vous souhaitez activer la gestion des téléchargements terminés, vous devez vérifier ce qui suit : * Avertissement : la gestion des téléchargements terminés ne fonctionne correctement que si le client de téléchargement et Radarr sont sur la même machine, car il obtient le chemin à importer directement à partir du client de téléchargement, sinon une correspondance distante est nécessaire.

### Indexeurs

#### Aucun indexeur disponible avec la recherche automatique activée, Radarr ne fournira aucun résultat de recherche automatique

- En termes simples, vous n'avez aucun de vos indexeurs configurés pour autoriser les recherches automatiques
- Allez dans Paramètres => Indexeurs, sélectionnez un indexeur que vous souhaitez autoriser les recherches automatiques, puis cliquez sur Enregistrer.

#### Aucun indexeur disponible avec la synchronisation RSS activée, Radarr ne récupérera pas automatiquement les nouvelles versions

- Radarr utilise le flux RSS pour récupérer les nouvelles versions au fur et à mesure de leur sortie. Plus d'informations à ce sujet ici
- Pour corriger ce problème, allez dans Paramètres => Indexeurs, sélectionnez un indexeur que vous avez et activez la synchronisation RSS

#### Aucun indexeur n'est activé

- Radarr nécessite des indexeurs pour pouvoir découvrir de nouvelles versions. Veuillez lire le wiki pour savoir comment ajouter des indexeurs.

#### Les indexeurs activés ne prennent pas en charge la recherche

- Aucun des indexeurs que vous avez activés ne prend en charge la recherche. Cela signifie que Radarr ne pourra trouver de nouvelles versions que via les flux RSS. Mais la recherche de films (recherche automatique ou recherche manuelle) ne renverra jamais de résultats. La seule façon de remédier à cela est d'ajouter un autre indexeur.

#### Aucun indexeur disponible avec la recherche interactive activée

- Aucun des indexeurs que vous avez activés ne prend en charge la recherche interactive. Cela signifie que l'application ne pourra trouver de nouvelles versions que via les flux RSS ou une recherche automatique.

#### Les indexeurs ne sont pas disponibles en raison de défaillances

- Des erreurs se produisent lorsque Radarr essaie d'utiliser l'un de vos indexeurs. Pour limiter les nouvelles tentatives, Radarr n'utilisera pas l'indexeur pendant une durée de plus en plus longue (jusqu'à 24 heures).
- Ce mécanisme est déclenché si Radarr n'a pas pu obtenir de réponse de l'indexeur (cela peut être dû à un problème DNS, de connexion proxy/VPN, d'authentification ou d'indexeur) ou s'il n'a pas pu récupérer le fichier nzb/torrent de l'indexeur. Veuillez inspecter les journaux pour déterminer quel type d'erreur a causé le problème.
- Vous pouvez éviter l'avertissement en désactivant l'indexeur concerné.
- Exécutez le test sur l'indexeur pour forcer Radarr à vérifier à nouveau l'indexeur, veuillez noter que l'avertissement de vérification de santé ne disparaîtra pas toujours immédiatement.

#### Jackett utilise tous les points de terminaison

- L'endpoint /all de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc maintenant nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il faut l'éviter et ne pas l'utiliser.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation de l'endpoint /all n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
  - mélanger les modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques de l'indexeur (\>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers dans /all renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez plus aucun résultat.

##### Solutions

- Ajoutez chaque tracker dans Jackett manuellement en tant qu'indexeur dans \*Arr
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui est développé par l'équipe de développement de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur endpoint d'agrégation unique et utilisez `multi` si la synchronisation est utilisée.

### Dossiers de films

#### Dossier racine manquant

{#movie-collection-missing-root-folder}

- Cette erreur est généralement identifiée si un film ou une collection est attribué à un dossier racine qui n'est plus disponible.
- Cette erreur peut également se produire si une liste est toujours liée à un dossier racine qui n'est plus disponible.
- Si vous souhaitez supprimer cet avertissement, trouvez simplement le(s) film(s) ou la/les collection(s) qui utilisent toujours l'ancien dossier racine et modifiez-le(s) pour le(s) dossier(s) racine correct(s).

##### Affichage du tableau des films

1. Accédez à l'onglet Films (Bibliothèque)
1. Affichez le tableau et activez la colonne Chemin, puis triez par chemin

##### Filtre personnalisé des films

1. Créez un filtre personnalisé avec l'ancien chemin du dossier racine
1. Sélectionnez la modification en masse dans la barre supérieure et dans la liste déroulante Chemins racines, sélectionnez le nouveau chemin racine dans lequel vous souhaitez que ces films soient déplacés.
1. Ensuite, vous recevrez une fenêtre contextuelle indiquant "Voulez-vous déplacer les dossiers de films vers 'chemin racine' ?" Cela indiquera également que cela renommera également le dossier de film selon le format de dossier de film dans les paramètres. Sélectionnez simplement Non si vous ne voulez pas que Radarr déplace vos fichiers.
1. Exécutez la tâche de vérification de santé dans Système => Tâches

#### Filtre personnalisé des collections

1. Créez un filtre personnalisé dans Collections avec l'ancien chemin du dossier racine
1. Sélectionnez les collections et dans la liste déroulante Chemins racines, sélectionnez le nouveau chemin racine dans lequel vous souhaitez que les futurs films de ces collections soient attribués.
1. Exécutez la tâche de vérification de santé dans Système => Tâches

### Films

#### Le film a été supprimé de TMDb

- Le film est lié à un ID TMDb qui a été supprimé de TMDb, généralement parce qu'il s'agissait d'un doublon, qu'il ne s'agissait pas d'un film ou que l'ID a été modifié pour une autre raison. Les films supprimés ne recevront aucune mise à jour et doivent être corrigés par l'utilisateur pour assurer une fonctionnalité continue. Supprimez le film de Radarr sans supprimer les fichiers, puis essayez de le réajouter. S'il n'apparaît pas dans une recherche, vérifiez Sonarr car il pourrait s'agir d'une mini-série télévisée comme Ça de Stephen King.

- Vous pouvez trouver et modifier les films supprimés en créant un filtre personnalisé en suivant les étapes suivantes :

  1. Cliquez sur Films dans le menu de gauche
  1. Cliquez sur la liste déroulante Filtre et sélectionnez "Filtre personnalisé"
  1. Entrez un libellé, par exemple "Films supprimés"
  1. Créez le filtre comme suit : `Statut de sortie` est `Supprimé`
  1. Cliquez sur Enregistrer et sélectionnez le filtre nouvellement créé dans le menu déroulant du filtre

#### Les listes ne sont pas disponibles en raison de défaillances

- En général, cela signifie simplement que Radarr n'est plus en mesure de communiquer via l'API ou en se connectant à votre fournisseur de listes choisi. Si le problème persiste, il est préférable de les contacter pour les exclure, car leurs systèmes peuvent être surchargés de temps en temps.
- Consultez

## File d'attente

- La file d'attente vous montrera les tâches en cours d'exécution et à venir, ainsi qu'un historique des tâches récemment exécutées et la durée de ces tâches.

# Sauvegarde

> Si vous recherchez comment sauvegarder/restaurer votre instance Radarr, cliquez [ici](/radarr/faq).
{.is-info}

- Dans la section Sauvegarde, vous verrez les sauvegardes précédentes (sauf si vous avez une nouvelle installation qui n'a effectué aucune sauvegarde).
  
- Sauvegarder maintenant - Cette option déclenchera une sauvegarde manuelle de la base de données de votre Radarr.
- Restaurer une sauvegarde - Cela ouvrira un nouvel écran pour restaurer à partir d'une sauvegarde précédente.
  - En sélectionnant Choisir un fichier, cela incitera votre navigateur à ouvrir une boîte de dialogue pour restaurer à partir d'une sauvegarde Zip de Radarr.
  
- Si vous avez des sauvegardes précédentes et que vous souhaitez les télécharger depuis Radarr pour les placer dans un emplacement non standard, vous pouvez simplement sélectionner l'un de ces fichiers pour les télécharger.
- À droite de chaque téléchargement précédent, vous avez deux options.
  - Restaurer (Icône de l'horloge) - Pour restaurer à partir d'une sauvegarde précédente - Cela ouvrira une nouvelle fenêtre pour confirmer que vous souhaitez restaurer à partir de cette sauvegarde.
  - Supprimer (Icône de la corbeille) - Pour supprimer une sauvegarde précédente.

# Mises à jour

- L'écran des mises à jour affichera les 5 dernières mises à jour effectuées ainsi que la version actuelle que vous utilisez.
- Cette page affichera également les notes de mise à jour des développeurs vous indiquant ce qui a été corrigé ou ajouté à Radarr (Réjouissez-vous !)
  
> Une version de maintenance contient des corrections de bugs et diverses améliorations. Consultez l'historique des modifications pour plus de détails.
{.is-info}

# Événements

- L'onglet Événements vous montrera ce qui s'est passé dans votre Radarr. Cela peut être utilisé pour diagnostiquer certains problèmes légers. Cependant, cela ne remplace pas les journaux de trace discutés dans la section Journalisation.

> Les événements sont l'équivalent des journaux INFO. {.is-info}

- Composants - Cette colonne vous indiquera quel composant de Radarr a été déclenché.
- Message - Cette colonne vous indiquera quel message a été envoyé par le composant de la colonne précédente.
- Icône d'engrenage - Cette option vous permettra de modifier le nombre de composants/messages affichés par page (la valeur par défaut est de 50).
- Options en haut de la page
  - Actualiser - Cette option actualisera la page actuelle, en récupérant un nouveau journal des événements.
  - Effacer - Cela effacera le journal des événements actuel, vous permettant de repartir à zéro.

# Fichiers journaux

- Cette page vous permettra de télécharger et de voir quels fichiers journaux sont disponibles pour Radarr.

- Sur la première ligne, vous trouverez plusieurs options pour vous permettre de contrôler vos fichiers journaux.

- Sur la première ligne tout à gauche, il y a une liste déroulante qui vous permettra de passer des fichiers journaux aux fichiers journaux de mise à jour.
  - Fichiers journaux - L'essentiel de tout problème de support peut être trouvé ici.
  - Fichiers journaux de mise à jour - Cela affichera les fichiers journaux associés au script de mise à jour de Radarr.

> Si vous utilisez Docker, cette section sera vide car vous devriez effectuer la mise à jour en téléchargeant une nouvelle image Docker.
{.is-info}

- Actualiser - Cela actualisera la page actuelle et affichera tous les journaux récemment créés.
- Supprimer - Cela effacera tous les journaux, vous permettant de repartir à zéro.
- Nom du fichier - Cela affichera le nom du fichier associé au journal.
- Dernière écriture - Il s'agit de l'heure locale à laquelle ce fichier journal particulier a été écrit.
  - Radarr utilise des fichiers journaux roulants limités à 1 Mo chacun. Le fichier journal actuel est toujours radarr.txt, pour les autres fichiers, radarr.0.txt est le plus récent (plus le nombre est élevé, plus il est ancien) jusqu'à un total de 51 fichiers journaux. Ce fichier journal contient des entrées `fatal`, `error`, `warn` et `info`.
  - Lorsque le niveau de journalisation de débogage est activé, des fichiers journaux roulants supplémentaires radarr.debug.txt seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent des entrées `fatal`, `error`, `warn`, `info` et `debug`. Ils couvrent généralement une période d'environ 40 heures.
  - Lorsque le niveau de journalisation de trace est activé, des fichiers journaux roulants supplémentaires radarr.trace.txt seront présents, jusqu'à 51 fichiers. Ces fichiers journaux contiennent des entrées `fatal`, `error`, `warn`, `info`, `debug` et `trace`. En raison de la verbosité de la trace, ils ne couvrent que quelques heures au maximum.