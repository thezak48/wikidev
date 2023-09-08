# Markdown Cheatsheet

## Introduction

Markdown is a lightweight markup language that you can use to add formatting elements to plaintext documents. Created by John Gruber in 2004, Markdown is now one of the most popular markup languages used for writing documentation, creating web pages, and even formatting text messages.

This cheatsheet provides a quick reference guide for the most commonly used Markdown syntax. Use it as a handy reference whenever you need to quickly format text in Markdown.

## Headers

Headers in Markdown are created by using one to six hash symbols (`#`) at the beginning of a line. The number of hash symbols determines the level of the header.

### Example

```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

### Output

# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

## Emphasis

You can add emphasis to text in Markdown by using asterisks (`*`) or underscores (`_`). Use a single asterisk or underscore for *italic* text, and use double asterisks or underscores for **bold** text.

### Example

```markdown
*Italic text*
_Italic text_

**Bold text**
__Bold text__
```

### Output

*Italic text*
_Italic text_

**Bold text**
__Bold text__

## Lists

Markdown supports both ordered and unordered lists.

### Unordered Lists

Unordered lists can be created by using either asterisks (`*`), plus signs (`+`), or hyphens (`-`) at the beginning of a line.

### Example

```markdown
- Item 1
- Item 2
- Item 3
```

### Output

- Item 1
- Item 2
- Item 3

### Ordered Lists

Ordered lists are created by using numbers followed by periods at the beginning of a line.

### Example

```markdown
1. Item 1
2. Item 2
3. Item 3
```

### Output

1. Item 1
2. Item 2
3. Item 3

## Links

You can create links in Markdown by using square brackets (`[]`) for the link text and parentheses (`()`) for the link URL.

### Example

```markdown
[Google](https://www.google.com)
```

### Output

[Google](https://www.google.com)

## Images

Images can be added to Markdown documents using the same syntax as links, but with an exclamation mark (`!`) at the beginning.

### Example

```markdown
![Alt text](https://www.example.com/image.jpg)
```

### Output

![Alt text](https://www.example.com/image.jpg)

## Code Blocks

Code blocks can be created by indenting each line of the block by four spaces or one tab.

### Example

```markdown
    code block
```

### Output

    code block

## Horizontal Rules

Horizontal rules can be created by using three or more hyphens (`-`), asterisks (`*`), or underscores (`_`) on a line by themselves.

### Example

```markdown
---
```

### Output

---

## Conclusion

This cheatsheet covers the most commonly used Markdown syntax. For more advanced features and syntax, refer to the official [Markdown documentation](https://daringfireball.net/projects/markdown/).

---
title: Système Lidarr
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, système
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Statut](#statut)
  - [Santé](#santé)
    - [Avertissements système](#avertissements-système)
      - [La branche n'est pas une branche de version valide](#la-branche-nest-pas-une-branche-de-version-valide)
      - [Mise à jour de la version .NET](#mise-à-jour-de-la-version-net)
        - [Correction des installations Docker](#correction-des-installations-docker)
        - [Correction des installations autonomes](#correction-des-installations-autonomes)
      - [La version Mono actuellement installée est ancienne et non prise en charge](#la-version-mono-actuellement-installée-est-ancienne-et-non-prise-en-charge)
      - [La version SQLite actuellement installée n'est pas prise en charge](#la-version-sqlite-actuellement-installée-nest-pas-prise-en-charge)
      - [Une nouvelle mise à jour est disponible](#une-nouvelle-mise-à-jour-est-disponible)
      - [Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur](#impossible-dinstaller-la-mise-à-jour-car-le-dossier-de-démarrage-nest-pas-accessible-en-écriture-par-lutilisateur)
      - [La mise à jour ne sera pas possible pour éviter la suppression des données de l'application lors de la mise à jour](#la-mise-à-jour-ne-sera-pas-possible-pour-éviter-la-suppression-des-données-de-lapplication-lors-de-la-mise-à-jour)
      - [La branche est destinée à une version précédente](#la-branche-est-destinée-à-une-version-précédente)
      - [Impossible de se connecter à signalR](#impossible-de-se-connecter-à-signalr)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [Échec de la résolution de l'adresse IP pour l'hôte proxy configuré](#échec-de-la-résolution-de-ladresse-ip-pour-lhôte-proxy-configuré)
      - [Échec du test du proxy](#échec-du-test-du-proxy)
      - [L'heure système est décalée de plus d'un jour](#lheure-système-est-décalée-de-plus-dun-jour)
      - [Mono Legacy TLS activé](#mono-legacy-tls-activé)
      - [Mono et les versions x86 prennent fin](#mono-et-les-versions-x86-prennent-fin)
      - [FPcalc doit être mis à jour](#fpcalc-doit-être-mis-à-jour)
    - [Clients de téléchargement](#clients-de-téléchargement)
      - [Aucun client de téléchargement n'est disponible](#aucun-client-de-téléchargement-nest-disponible)
      - [Impossible de communiquer avec le client de téléchargement](#impossible-de-communiquer-avec-le-client-de-téléchargement)
      - [Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance](#les-clients-de-téléchargement-ne-sont-pas-disponibles-en-raison-dune-défaillance)
      - [Activer la gestion des téléchargements terminés](#activer-la-gestion-des-téléchargements-terminés)
      - [Mauvaise correspondance de chemin distant Docker](#mauvaise-correspondance-de-chemin-distant-docker)
      - [Téléchargement dans le dossier racine](#téléchargement-dans-le-dossier-racine)
      - [Mauvais paramètres du client de téléchargement](#mauvais-paramètres-du-client-de-téléchargement)
      - [Mauvaise correspondance de chemin distant](#mauvaise-correspondance-de-chemin-distant)
      - [Erreur d'autorisations](#erreur-dautorisations)
      - [Le fichier distant a été supprimé en cours de traitement](#le-fichier-distant-a-été-supprimé-en-cours-de-traitement)
      - [Le chemin distant est utilisé et l'importation a échoué](#le-chemin-distant-est-utilisé-et-limportation-a-échoué)
    - [Gestion des téléchargements terminés/échoués](#gestion-des-téléchargements-terminéséchoués)
      - [La gestion des téléchargements terminés est désactivée](#la-gestion-des-téléchargements-terminés-est-désactivée)
    - [Indexeurs](#indexeurs)
      - [Aucun indexeur disponible avec la recherche automatique activée, Lidarr ne fournira aucun résultat de recherche automatique](#aucun-indexeur-disponible-avec-la-recherche-automatique-activée-lidarr-ne-fournira-aucun-résultat-de-recherche-automatique)
      - [Aucun indexeur disponible avec la synchronisation RSS activée, Lidarr ne récupérera pas automatiquement les nouvelles versions](#aucun-indexeur-disponible-avec-la-synchronisation-rss-activée-lidarr-ne-récupérera-pas-automatiquement-les-nouvelles-versions)
      - [Aucun indexeur n'est activé](#aucun-indexeur-nest-activé)
    - [Les indexeurs activés ne prennent pas en charge la recherche](#les-indexeurs-activés-ne-prennent-pas-en-charge-la-recherche)
      - [Aucun indexeur disponible avec la recherche interactive activée](#aucun-indexeur-disponible-avec-la-recherche-interactive-activée)
      - [Les indexeurs ne sont pas disponibles en raison de défaillances](#les-indexeurs-ne-sont-pas-disponibles-en-raison-de-défaillances)
      - [Jackett utilise tous les points de terminaison](#jackett-utilise-tous-les-points-de-terminaison)
        - [Solutions](#solutions)
    - [Dossiers d'artistes](#dossiers-dartistes)
      - [Dossier racine manquant](#dossier-racine-manquant)
      - [Les listes ne sont pas disponibles en raison de défaillances](#les-listes-ne-sont-pas-disponibles-en-raison-de-défaillances)
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

> Avertissement : Cette page est en cours de rédaction et est actuellement un brouillon basé sur Readarr
{.is-danger}

# Statut

## Santé

Cette page contient une liste des erreurs de vérification de santé. Ces vérifications de santé sont effectuées périodiquement par Lidarr et lors de certains événements. Les avertissements et erreurs résultants sont répertoriés ici pour donner des conseils sur la façon de les résoudre.

### Avertissements système

#### La branche n'est pas une branche de version valide

La branche que vous avez définie n'est pas une branche de version valide. Vous ne recevrez pas de mises à jour. Veuillez changer pour l'une des [branches de version actuelles](/lidarr/faq#how-do-i-update-lidarr)

#### Mise à jour de la version .NET

{#update-to-net-core-version}

- Les versions plus récentes de Lidarr sont ciblées pour .NET6 ou une version ultérieure. Nous ne fournirons plus de versions mono héritées après la version 1.0. Vous utilisez l'une de ces versions héritées mais votre plateforme prend en charge .NET.

##### Correction des installations Docker

- Reprenez votre conteneur

##### Correction des installations autonomes

- Sauvegardez votre configuration existante avant l'étape suivante.
- Cela ne devrait se produire que sur les hôtes Linux. N'installez pas le runtime ou le SDK .NET de Microsoft.
- Pour remédier à cela, téléchargez la version correcte pour votre architecture et remplacez vos binaires existants (application)
- En bref, vous devrez supprimer vos binaires existants (contenu ou dossier de /opt/Lidarr) et les remplacer par le contenu du fichier .tar.gz que vous venez de télécharger.

> NE DÉCOMPRESSEZ PAS SIMPLEMENT LE TÉLÉCHARGEMENT PAR-DESSUS VOS ANCIENS BINAIRES.
> VOUS DEVEZ D'ABORD SUPPRIMER LES ANCIENS.
{.is-warning}

- Ce qui suit est un script développé par la communauté pour supprimer votre installation mono et la remplacer par l'installation .NET. Les contributions et les corrections sont les bienvenues.
- Cela suppose que vous êtes sur la branche Lidarr `master`, mettez à jour la variable si nécessaire
- Cela suppose que Lidarr s'exécute en tant qu'utilisateur `lidarr`, mettez à jour les variables si nécessaire
- Cela suppose que Lidarr est installé dans `/opt/Lidarr`, mettez à jour les variables si nécessaire

```bash
#!/bin/bash
## Variables utilisateur
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /Variables utilisateur
app="lidarr"
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

#### La version Mono actuellement installée est ancienne et non prise en charge

- Lidarr est écrit en .NET et nécessite Mono pour s'exécuter sur de très anciens processeurs ARM. Veuillez noter que les versions Mono ne sont plus prises en charge après la version 1.0
- Mono 5.20 est le minimum absolu pour Lidarr.
- La procédure de mise à niveau de Mono varie selon la plateforme.

#### La version SQLite actuellement installée n'est pas prise en charge

- Lidarr stocke ses données dans une base de données SQLite. La bibliothèque SQLite3 installée sur votre système est trop ancienne. Lidarr nécessite au moins la version 3.9.0. Notez que Lidarr utilise `libSQLite3.so` qui peut être ou non contenu dans un package de mise à niveau SQLite3.

#### Une nouvelle mise à jour est disponible

- Réjouissez-vous, les développeurs ont publié une nouvelle mise à jour. Cela signifie généralement de nouvelles fonctionnalités géniales et des tas de bogues corrigés (n'est-ce pas ?). Apparemment, vous n'avez pas activé la mise à jour automatique, vous devrez donc trouver comment mettre à jour sur votre plateforme. Appuyer sur le bouton Installer sur la page `Système => Mises à jour` est probablement un bon point de départ.

> Cet avertissement n'apparaîtra pas si votre version actuelle a moins de 14 jours
{.is-info}

#### Impossible d'installer la mise à jour car le dossier de démarrage n'est pas accessible en écriture par l'utilisateur

- Cela signifie que Lidarr ne pourra pas se mettre à jour automatiquement. Vous devrez mettre à jour Lidarr manuellement ou définir les autorisations sur le répertoire de démarrage de Lidarr (le répertoire d'installation) pour permettre à Lidarr de se mettre à jour.

#### La mise à jour ne sera pas possible pour éviter la suppression des données de l'application lors de la mise à jour

- Lidarr a détecté que le dossier AppData pour votre système d'exploitation est situé à l'intérieur du répertoire qui contient les binaires Lidarr. Normalement, il s'agirait de `C:\ProgramData` pour Windows et `~/.config` pour Linux.

- Veuillez consulter `Système => Informations` pour voir les répertoires AppData et de démarrage actuels.
- Cela signifie que Lidarr ne pourra pas se mettre à jour sans risquer de perdre des données.
- Si vous êtes sous Linux, vous devrez probablement changer le répertoire personnel de l'utilisateur qui exécute Lidarr et copier le contenu actuel du répertoire `~/.config/Lidarr` pour préserver votre base de données.

#### La branche est destinée à une version précédente

- La branche de mise à jour configurée dans `Paramètres => Général` est destinée à une version précédente de Lidarr, par conséquent, l'instance ne verra pas les informations de mise à jour correctes dans le flux `Système => Mises à jour` et peut ne pas recevoir de nouvelles mises à jour lorsqu'elles seront publiées.

#### Impossible de se connecter à signalR

- signalR permet les mises à jour dynamiques de l'interface utilisateur, donc si votre navigateur ne peut pas se connecter à signalR sur votre serveur, vous ne verrez aucune mise à jour en temps réel dans l'interface utilisateur.

- Le cas le plus courant est l'utilisation d'un proxy inverse ou de Cloudflare
- Cloudflare nécessite l'activation des websockets.

##### NGINX

- Nginx nécessite l'ajout suivant au bloc de localisation de l'application :

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Assurez-vous de ne pas inclure `proxy_set_header Connection "Upgrade";` comme suggéré par la documentation de nginx. CELA NE FONCTIONNERA PAS
> Voir <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- Pour un proxy inverse Apache2, vous devez activer les modules suivants : proxy, proxy_http et proxy_wstunnel. Ensuite, ajoutez cette directive de tunnel websocket à la configuration de votre hôte virtuel :

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- Pour Caddy (V1), utilisez ceci :
- Remarque : vous devrez également ajouter la directive websocket à votre configuration Lidarr

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### Échec de la résolution de l'adresse IP pour l'hôte proxy configuré

- Vérifiez vos paramètres de proxy et assurez-vous qu'ils sont corrects
- Assurez-vous que votre proxy est actif, en cours d'exécution et accessible

#### Échec du test du proxy

- Votre proxy configuré a échoué au test avec succès, vérifiez l'erreur HTTP fournie et/ou consultez les journaux pour plus de détails.

#### L'heure système est décalée de plus d'un jour

- L'heure système est décalée de plus d'un jour. Les tâches planifiées peuvent ne pas s'exécuter correctement tant que l'heure n'est pas corrigée
- Vérifiez l'heure système et assurez-vous qu'elle est synchronisée avec un serveur de temps fiable et précis

#### Mono Legacy TLS activé

- La solution de contournement Mono 4.x tls est toujours activée, envisagez de supprimer l'option d'environnement `MONO_TLS_PROVIDER=legacy`

#### Mono et les versions x86 prennent fin

- Les versions Mono et x86 ne seront plus prises en charge dans la prochaine version de l'application. Si vous recevez cette erreur, cela signifie que vous utilisez la version mono de l'application ou la version x86. Malheureusement, en raison de la difficulté croissante de la prise en charge du développement de ces versions héritées, nous cesserons de les prendre en charge et donc de les publier à l'avenir. Il est donc conseillé de passer à un système d'exploitation pris en charge qui ne nécessite ni x86 ni mono. Vous pouvez également envisager d'utiliser Docker pour vos besoins.

#### FPcalc doit être mis à jour

{#fpcalc-upgrade}

- Lidarr utilise la reconnaissance audio chromaprint pour identifier les pistes. Cela dépend d'un binaire externe `fpcalc`, qui est distribué avec Lidarr v1 pour Windows, Linux et macOS, mais doit être fourni indépendamment pour FreeBSD.
- Assurez-vous que le binaire fpcalc inclus avec Lidarr est exécutable (permissions 755). Il se trouve dans le répertoire d'installation de Lidarr (par exemple `/opt/Lidarr/fpcalc`). S'il n'est pas exécutable, corrigez ses autorisations avec la commande suivante, puis redémarrez Lidarr.
  - Notez que pour la correction, `sudo` peut être nécessaire ou votre chemin vers le dossier binaire de Lidarr peut être différent en fonction de votre environnement et de votre configuration.

```bash
chmod +x /opt/Lidarr/fpcalc
```

> Les informations ci-dessous concernent uniquement les versions héritées v0.8.0.
{.is-info}

- Pour résoudre ce problème sur une instance Linux native, installez le package approprié à l'aide de votre gestionnaire de paquets et assurez-vous que fpcalc est dans votre PATH (vous pouvez vérifier cela avec la commande `which fpcalc` et vérifier que l'emplacement correct de fpcalc est renvoyé) :

| Distribution  |       Package        |
| :-----------: | :------------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### Clients de téléchargement

#### Aucun client de téléchargement n'est disponible

- Un client de téléchargement correctement configuré et activé est requis pour que Lidarr puisse télécharger des médias. Lidarr prend en charge différents clients de téléchargement, vous devez donc déterminer celui qui correspond le mieux à vos besoins. Si vous avez déjà un client de téléchargement installé, vous devez le configurer pour qu'il soit utilisé par Lidarr et créer une catégorie. Voir `Paramètres => Client de téléchargement`.

#### Impossible de communiquer avec le client de téléchargement

- Lidarr n'a pas pu communiquer avec le client de téléchargement configuré. Veuillez vérifier que le client de téléchargement est opérationnel et vérifier à nouveau l'URL. Cela peut également indiquer une erreur d'authentification.
- Cela est généralement dû à un client de téléchargement mal configuré. Voici quelques éléments que vous pouvez vérifier :
  - L'adresse IP de votre client de téléchargement - si tout est sur la même machine physique, il s'agit généralement de `127.0.0.1`
  - Le numéro de port utilisé par votre client de téléchargement - ces champs sont remplis avec le numéro de port par défaut, mais si vous l'avez modifié, vous devrez entrer le même numéro dans Lidarr.
  - Assurez-vous que le chiffrement SSL n'est pas activé si vous utilisez à la fois votre instance Lidarr et votre client de téléchargement sur un réseau local (c'est-à-dire en HTTP simple). Consultez la FAQ SSL pour plus d'informations.

#### Les clients de téléchargement ne sont pas disponibles en raison d'une défaillance

- Un ou plusieurs de vos clients de téléchargement ne répondent pas aux demandes de Lidarr. Par conséquent, Lidarr a décidé d'arrêter temporairement les requêtes vers le client de téléchargement selon son cycle normal d'une minute, qui est normalement utilisé pour suivre les téléchargements en cours et importer les téléchargements terminés. Cependant, Lidarr continuera d'essayer d'envoyer des téléchargements au client, mais il est fort probable que cela échoue.
- Vous devez inspecter `Système => Journaux` pour connaître la raison des échecs.
- Si vous n'utilisez plus ce client de téléchargement, désactivez-le dans Lidarr pour éviter les erreurs.

#### Activer la gestion des téléchargements terminés

- Lidarr nécessite la gestion des téléchargements terminés pour pouvoir importer les fichiers téléchargés par le client de téléchargement. Il est recommandé d'activer la gestion des téléchargements terminés. (La gestion des téléchargements terminés est activée par défaut pour les nouveaux utilisateurs.)

#### Mauvaise correspondance de chemin distant Docker

- Cette erreur est généralement associée à des chemins Docker incorrects dans votre client de téléchargement ou Lidarr.

- Un exemple de mauvais chemins (incohérents) serait :
  - Client de téléchargement : `/mnt/user/downloads:/downloads`
  - Lidarr : `/mnt/user/downloads:/data`
- Dans cet exemple, le client de téléchargement place ses téléchargements dans `/downloads` et indique à Lidarr, une fois le téléchargement terminé, que le livre terminé se trouve dans `/downloads`. Lidarr vient ensuite et dit "D'accord, cool, je vais vérifier dans `/downloads`". Eh bien, à l'intérieur de Lidarr, vous n'avez pas alloué un chemin `/downloads`, vous avez alloué un chemin `/data`, donc il affiche cette erreur.
- La solution la plus simple consiste à être CONSISTANT - si vous utilisez un schéma dans votre client de téléchargement, utilisez-le partout.

- L'équipe Lidarr est très favorable à l'utilisation de /data.

  - Client de téléchargement : `/mnt/user/data/downloads:/data/downloads`
  - Lidarr : `/mnt/user/data:/data`

- Maintenant, dans le client de téléchargement, vous pouvez spécifier où dans `/data` vous souhaitez placer vos téléchargements, cela varie en fonction du client, mais vous devriez pouvoir lui dire "Oui, client de téléchargement, placez mes fichiers dans `/data/downloads/movies`" et comme vous avez utilisé `/data` dans Lidarr, lorsque le client de téléchargement dit à Lidarr que c'est terminé, Lidarr vérifiera `/data` et `/data/downloads/movies`, tout est bien dans le monde.
- Il existe de nombreux bons guides : notre wiki [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH. Ces guides mettent l'accent sur les liens physiques et les déplacements instantanés (déplacements atomiques), mais le concept général des conteneurs et du fonctionnement des chemins s'applique à ces discussions.
- Si vous passez d'un système d'exploitation à un autre ou d'un système natif à un système Docker, vous avez besoin d'une correspondance de chemin distant. Consultez le guide [TRaSH's Remote Path Guide for Radarr](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) et [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/) pour plus d'informations.

#### Téléchargement dans le dossier racine

{#downloads-in-root-folder}

- Dans l'application, un dossier racine est défini comme le dossier de bibliothèque multimédia configuré. Ce n'est pas le dossier racine d'un montage. Votre client de téléchargement a un dossier incomplet ou complet (ou déplace les téléchargements terminés) dans votre dossier racine (bibliothèque).
- Cela cause fréquemment des problèmes, y compris la perte de données, et ne doit pas être fait. Pour résoudre ce problème, modifiez votre client de téléchargement pour qu'il ne place pas les téléchargements dans votre dossier racine. Notez que 'placer' inclut également si la catégorie de votre client de téléchargement est définie sur votre dossier racine ou si NZBGet/SABnzbd a la fonction de tri activée et trie vers votre dossier racine.
- Veuillez noter que cette vérification examine tous les dossiers racines définis/configurés ajoutés, pas seulement les dossiers racines actuellement utilisés. En d'autres termes, le dossier dans lequel votre client de téléchargement télécharge ou déplace les téléchargements terminés ne doit pas être le même dossier que vous avez configuré comme dossier racine/bibliothèque/destination finale des médias dans l'application *arr.
- Les dossiers racines configurés (alias dossiers de bibliothèque) se trouvent dans [Paramètres => Gestion des médias => Dossiers racines](/lidarr/settings/#root-folders)
- Un exemple est si vos téléchargements vont dans `\data\downloads`, alors vous avez un dossier racine défini comme `\data\downloads`.
- Il est recommandé d'utiliser des chemins comme `\data\media\` pour votre dossier racine/bibliothèque et `\data\downloads\` pour vos téléchargements.
- Consultez notre [Guide Docker](/docker-guide) et le guide [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/) de TRaSH pour plus d'informations sur la configuration correcte et optimale des chemins. Notez que les concepts s'appliquent aux conteneurs et aux systèmes non-Docker.

> Votre dossier de téléchargement où votre client de téléchargement place les téléchargements et votre dossier racine/bibliothèque DOIVENT être séparés. \*Arr importera le(s) fichier(s) du dossier de votre client de téléchargement dans votre bibliothèque. Le client de téléchargement ne doit rien déplacer ni télécharger dans votre bibliothèque.
{.is-warning}

#### Mauvais paramètres du client de téléchargement

- L'emplacement où votre client de téléchargement télécharge les fichiers pose des problèmes. Vérifiez les journaux pour plus d'informations. Cela peut être dû à des autorisations ou à une tentative de passer de Windows à Linux ou de Linux à Windows sans correspondance de chemin distant.

#### Mauvaise correspondance de chemin distant

- L'emplacement où votre client de téléchargement télécharge les fichiers pose des problèmes. Vérifiez les journaux pour plus d'informations. Cela peut être dû à des autorisations ou à une tentative de passer de Windows à Linux ou de Linux à Windows sans correspondance de chemin distant. Consultez le guide [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) pour plus d'informations.

#### Erreur d'autorisations

- Lidarr (ou l'utilisateur sous lequel lidarr s'exécute) ne peut pas accéder à l'emplacement où votre client de téléchargement télécharge les fichiers. Il s'agit généralement d'un problème d'autorisations.

#### Le fichier distant a été supprimé en cours de traitement

- Un fichier accessible via une correspondance de chemin distant semble avoir été supprimé avant la fin du traitement.

#### Le chemin distant est utilisé et l'importation a échoué

- Vérifiez vos journaux pour plus d'informations. Consultez nos [Guides de dépannage](/lidarr/troubleshooting).

### Gestion des téléchargements terminés/échoués

#### La gestion des téléchargements terminés est désactivée

- Lidarr nécessite la `Gestion des téléchargements terminés` pour pouvoir importer les fichiers téléchargés par le client de téléchargement. Il est recommandé d'activer la `Gestion des téléchargements terminés`. (Elle est activée par défaut pour les nouveaux utilisateurs.)

### Indexeurs

#### Aucun indexeur disponible avec la recherche automatique activée, Lidarr ne fournira aucun résultat de recherche automatique

- En d'autres termes, vous n'avez aucun de vos indexeurs configurés pour autoriser les recherches automatiques
- Allez dans `Paramètres => Indexeurs`, sélectionnez un indexeur que vous souhaitez autoriser les recherches automatiques et cliquez sur Enregistrer.

#### Aucun indexeur disponible avec la synchronisation RSS activée, Lidarr ne récupérera pas automatiquement les nouvelles versions

- Lidarr utilise le flux RSS pour récupérer les nouvelles versions au fur et à mesure de leur sortie. Plus d'informations à ce sujet ici
- Pour corriger ce problème, allez dans `Paramètres => Indexeurs`, sélectionnez un indexeur que vous avez et activez la synchronisation RSS

#### Aucun indexeur n'est activé

- Lidarr nécessite des indexeurs pour pouvoir découvrir de nouvelles versions. Veuillez lire le wiki pour obtenir des instructions sur la façon d'ajouter des indexeurs.

#### Les indexeurs activés ne prennent pas en charge la recherche

- Aucun des indexeurs que vous avez activés ne prend en charge la recherche. Cela signifie que Lidarr ne pourra trouver de nouvelles versions que via les flux RSS. Mais la recherche de films (recherche automatique ou recherche manuelle) ne renverra jamais de résultats. La seule façon de remédier à cela est d'ajouter un autre indexeur.

#### Aucun indexeur disponible avec la recherche interactive activée

- Aucun des indexeurs que vous avez activés ne prend en charge la recherche interactive. Cela signifie que l'application ne pourra trouver de nouvelles versions que via les flux RSS ou une recherche automatique.

#### Les indexeurs ne sont pas disponibles en raison de défaillances

- Des erreurs se produisent lorsque Lidarr essaie d'utiliser l'un de vos indexeurs. Pour limiter les nouvelles tentatives, Lidarr n'utilisera pas l'indexeur pendant une durée de plus en plus longue (jusqu'à 24 heures).
- Ce mécanisme est déclenché si Lidarr n'a pas pu obtenir de réponse de l'indexeur (cela peut être dû à un problème DNS, à une connexion proxy/VPN, à une authentification ou à un problème d'indexeur) ou s'il n'a pas pu récupérer le fichier nzb/torrent de l'indexeur.
- Veuillez inspecter les journaux pour déterminer quel type d'erreur cause le problème.
- Vous pouvez éviter l'avertissement en désactivant l'indexeur concerné.
- Exécutez le test sur l'indexeur pour forcer Lidarr à vérifier à nouveau l'indexeur, veuillez noter que l'avertissement de vérification de santé ne disparaîtra pas toujours immédiatement.

#### Jackett utilise tous les points de terminaison

- L'endpoint `/all` de Jackett est pratique, mais c'est son seul avantage. Tout le reste peut poser des problèmes, il est donc maintenant nécessaire d'ajouter chaque tracker individuellement.
- [Même les développeurs de Jackett disent qu'il faut l'éviter et ne pas l'utiliser.](https://github.com/Jackett/Jackett#aggregate-indexers)
- L'utilisation de l'endpoint `/all` n'a aucun avantage, seulement des inconvénients :
  - vous perdez le contrôle sur les paramètres spécifiques de l'indexeur (catégories, modes de recherche, etc.)
  - la combinaison de modes de recherche (IMDB, requête, etc.) peut entraîner des résultats de faible qualité
  - les catégories spécifiques de l'indexeur (>= 100000) ne peuvent pas être utilisées.
  - les indexeurs lents ralentiront le résultat global
  - le nombre total de résultats est limité à 1000
  - si l'un des trackers renvoie une erreur, \*Arr le désactivera et vous n'obtiendrez plus aucun résultat.

##### Solutions

- Ajoutez chaque tracker dans Jackett manuellement en tant qu'indexeur dans \*Arr
- Consultez [Prowlarr](/prowlarr) qui peut synchroniser les indexeurs avec \*Arr et qui est développé par l'équipe de développement de Lidarr/Radarr/Readarr.
- Consultez [NZBHydra2](https://github.com/theotherp/nzbhydra2) qui peut synchroniser les indexeurs avec \*Arr. Mais n'utilisez pas leur endpoint d'agrégation unique et utilisez `multi` si la synchronisation est utilisée.

### Dossiers d'artistes

#### Dossier racine manquant

- Cette erreur est généralement identifiée si un artiste recherche un dossier racine mais que ce dossier racine n'est plus disponible.
- Cette erreur peut également se produire si une liste est toujours pointée vers un dossier racine mais que ce dossier racine n'est plus disponible.
- Si vous souhaitez supprimer cet avertissement, trouvez simplement l'album qui utilise toujours l'ancien dossier racine et modifiez-le pour le dossier racine correct.

- La manière la plus simple de trouver l'artiste posant problème est de :

  - Aller à l'onglet Artiste (Bibliothèque)
  - Créer un filtre personnalisé avec l'ancien chemin du dossier racine
  - Sélectionner la modification en masse dans la barre supérieure et dans le menu déroulant des chemins racine, sélectionner le nouveau chemin racine vers lequel vous souhaitez déplacer ces artistes.
  - Ensuite, vous recevrez une fenêtre contextuelle indiquant Voulez-vous déplacer les dossiers d'artistes vers 'chemin racine' ? Cela indiquera également Cela renommera également le dossier d'artiste selon le format de dossier d'artiste dans les paramètres. Sélectionnez simplement Non si vous ne voulez pas que Lidarr déplace vos fichiers.
  - Exécutez la tâche de vérification de santé dans Système => Tâches

## Espace disque

- Cette section vous montrera l'espace disque disponible
- Dans Docker, cela peut être délicat car il affiche généralement l'espace disponible dans votre image Docker

## À propos

- Cela vous donnera des informations sur votre installation actuelle de Lidarr

## Plus d'informations

- Page d'accueil : Page d'accueil de Lidarr
- Wiki : Vous êtes déjà ici
- Reddit : r/lidarr
- Discord : Rejoignez notre discord
- Dons : Si vous êtes généreux et que vous souhaitez faire un don, cliquez ici
- Dons à Sonarr : Si vous êtes généreux et que vous souhaitez faire un don au projet qui a tout commencé, cliquez ici
- Source : GitHub
- Demandes de fonctionnalités : Vous avez une excellente idée, déposez-la ici

# Tâches

## Planifiées

- Cette page répertorie toutes les tâches planifiées exécutées par Lidarr

  - Vérification de la mise à jour de l'application - Cela s'exécute à chaque fois selon le planning affiché dans l'interface utilisateur, vérifiant si Lidarr est à la version la plus récente, puis déclenche le script de mise à jour pour mettre à jour Lidarr. Paramètres => Mise à jour

  > Remarque : Si vous utilisez Docker, cela ne mettra pas à jour votre conteneur car une nouvelle image devra être téléchargée.
{.is-warning}

  - Sauvegarde - Cela exécute une sauvegarde de la base de données de votre Lidarr selon un planning défini. Plus de détails à ce sujet peuvent être trouvés ici. Plus d'informations sur les sauvegardes peuvent être trouvées dans Système => Sauvegardes.
  - Vérification de la santé - La vérification