---
title: Paramètres Lidarr
description: 
published: true
date: 2022-07-24T14:21:19.994Z
tags: lidarr, needs-love, settings
editor: markdown
dateCreated: 2021-06-14T21:36:07.513Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Paramètres](#paramètres)
- [Clients de téléchargement](#clients-de-téléchargement)
  - [Aperçu](#aperçu)
  - [Processus du client de téléchargement](#processus-du-client-de-téléchargement)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Clients de téléchargement](#clients-de-téléchargement-1)
    - [Clients de téléchargement pris en charge](#clients-de-téléchargement-pris-en-charge)
    - [Paramètres du client Usenet](#paramètres-du-client-usenet)
    - [Paramètres du client BitTorrent](#paramètres-du-client-bittorrent)
    - [Compatibilité de suppression de téléchargement du client BitTorrent](#compatibilité-de-suppression-de-téléchargement-du-client-bittorrent)
  - [Gestion des téléchargements terminés](#gestion-des-téléchargements-terminés)
    - [Supprimer les téléchargements terminés](#supprimer-les-téléchargements-terminés)
    - [Gestion des échecs de téléchargement](#gestion-des-échecs-de-téléchargement)
  - [Correspondances de chemin distant](#correspondances-de-chemin-distant)
- [Listes d'importation](#listes-dimportation)
  - [Listes d'importation](#listes-dimportation-1)
  - [Exclusions de liste d'importation](#exclusions-de-liste-dimportation)
  - [Ajouter une liste d'importation](#ajouter-une-liste-dimportation)
- [Connexions](#connexions)
- [Balises](#balises)
- [Général](#général)
  - [Mises à jour](#mises-à-jour)

# Paramètres

Cette page est en cours de réalisation et les contributions - basées sur les autres pages \*Arr - sont les bienvenues et fortement encouragées.

# Clients de téléchargement

> Des informations sur les clients de téléchargement pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/lidarr/supported#download-clients) de cette section
{.is-info}

## Aperçu

- Le téléchargement et l'importation sont les étapes où la plupart des utilisateurs rencontrent des problèmes. D'un point de vue global, le logiciel doit être capable de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une encore plus grande variété de configurations. Cela signifie qu'il n'y a pas de configuration unique et correcte, et que la configuration de chacun peut être légèrement différente. Mais il existe de nombreuses configurations incorrectes.

## Processus du client de téléchargement

## Usenet

- Lidarr enverra une demande de téléchargement à votre client et l'associera à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Lidarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Lidarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Lidarr.
- Lidarr analysera cet emplacement de fichier terminé à la recherche de fichiers que Lidarr peut utiliser. Il analysera le nom du fichier pour le faire correspondre avec le média demandé. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens physiques et les déplacements atomiques, Lidarr recourra à la copie du fichier, puis le supprimera de la source, ce qui est intensif en termes d'E/S.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Lidarr, les fichiers restants du téléchargement seront envoyés à la corbeille ou au recyclage via une demande à votre client pour supprimer le téléchargement.

## BitTorrent

- Lidarr enverra une demande de téléchargement à votre client et l'associera à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Lidarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de les partager. Lorsque les fichiers sont importés dans votre dossier multimédia, Lidarr créera un lien physique vers le fichier s'il est pris en charge par votre configuration, sinon il le copiera.
- Les liens physiques sont activés par défaut. [Un lien physique ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, Lidarr recourra à la copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Lidarr, Lidarr supprimera le torrent de votre client et demandera au client de supprimer les données du torrent, mais cela ne se produira que si le client signale que le partage est terminé et que le torrent est arrêté (en pause à la fin).

## Clients de téléchargement

Cliquez sur `Paramètres => Clients de téléchargement`, puis cliquez sur le <kb>+</kb> pour ajouter un nouveau client de téléchargement. Votre client de téléchargement doit déjà être configuré et en cours d'exécution.

### Clients de téléchargement pris en charge

- Une liste des clients de téléchargement pris en charge se trouve sur la page [Plus d'informations (Pris en charge)](/lidarr/supported#downloadclient) de cette section

Sélectionnez le client de téléchargement que vous souhaitez ajouter, et une boîte contextuelle s'affichera pour entrer les détails de connexion. Ces détails sont similaires pour la plupart des clients. Certains vous demanderont un nom d'utilisateur ou un mot de passe, d'autres vous demanderont si vous souhaitez ajouter de nouveaux téléchargements en pause ou en cours, etc.

### Paramètres du client Usenet

- Nom - Le nom du client de téléchargement dans Lidarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base d'URL - Ajouter un préfixe à l'URL ; cela est généralement nécessaire pour les serveurs proxy inverses.
- Clé API - la clé API pour s'authentifier auprès de votre client
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Catégorie - la catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Priorité récente - priorité du client de téléchargement pour les médias récemment publiés
- Priorité plus ancienne - priorité du client de téléchargement pour les médias publiés il y a longtemps
- (Option avancée) Priorité du client - Priorité du client de téléchargement. Le round-robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse

### Paramètres du client BitTorrent

- Nom - Le nom du client de téléchargement dans Lidarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement ; il s'agit généralement du port de l'interface web
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base d'URL - Ajouter un préfixe à l'URL ; cela est généralement nécessaire pour les serveurs proxy inverses.
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client
- Catégorie - la catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Catégorie après importation - la catégorie à définir après le téléchargement et l'importation de la version. Veuillez noter que cela désactive la suppression des téléchargements terminés.
- Priorité récente - priorité du client de téléchargement pour les médias récemment publiés
- Priorité plus ancienne - priorité du client de téléchargement pour les médias publiés il y a longtemps
- État initial - État initial des torrents (uniquement pour Qbittorrent : la force contourne tous les seuils de partage)
- (Option avancée) - Priorité du client de téléchargement. Le round-robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse

### Compatibilité de suppression de téléchargement du client BitTorrent

- Lidarr est uniquement capable de définir le ratio/temps de partage sur les clients qui prennent en charge le réglage de cette valeur via leur API lors de l'ajout du torrent. Les objectifs de partage peuvent être définis globalement dans le client lui-même ou par tracker dans les paramètres de \*Arr pour chaque indexeur. Consultez le tableau ci-dessous pour connaître la compatibilité du client.

|      Client       |                                Ratio                                 |                                   Temps                                   |
| :---------------: | :------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|      Deluge       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
| Download Station  | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|       Flood       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
|     Hadouken      | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|    qBittorrent    |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
|     rTorrent      |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
| Torrent Blackhole | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |   ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)   |
|   Transmission    |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   | ![Limite d'inactivité](https://img.shields.io/badge/Pris%20en%20charge-Limite%20d'inactivité*-blue) |
|     uTorrent      |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |
|       Vuze        |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |     ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)     |

> ![Limite d'inactivité](https://img.shields.io/badge/Pris%20en%20charge-Limite%20d'inactivité*-blue) - Transmission dispose d'une vérification du temps d'inactivité en interne, mais Lidarr la compare avec le temps de partage si la limite d'inactivité est définie pour chaque torrent. Cela est fait comme contournement des limitations de l'API de Transmission.{.is-info}

## Gestion des téléchargements terminés

- La gestion des téléchargements terminés est la façon dont Lidarr importe les médias depuis votre client de téléchargement vers vos dossiers de séries.

- Activer (Paramètre global avancé) - Importer automatiquement les téléchargements terminés depuis le client de téléchargement
- Supprimer (Paramètre par client) - Supprimer les téléchargements terminés lorsqu'ils sont terminés (usenet) ou arrêtés/terminés (torrents)
  - Pour les torrents, cela nécessite que votre client de téléchargement mette en pause lorsque les objectifs de partage sont atteints. Cela nécessite également que les objectifs de partage soient pris en charge par Lidarr selon le tableau ci-dessus. Les torrents doivent également rester dans la même catégorie.

### Supprimer les téléchargements terminés

- Lidarr enverra une demande de téléchargement à votre client et l'associera à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
- Lidarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Lidarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia.
- Lidarr analysera cet emplacement de fichier terminé à la recherche de fichiers vidéo. Il analysera le nom du fichier vidéo pour le faire correspondre à un épisode. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers le dossier de bibliothèque assigné.
- Les fichiers restants du téléchargement seront envoyés à la corbeille ou au recyclage.

Si vous téléchargez à l'aide d'un client BitTorrent, le processus est légèrement différent :

- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de les partager. Lorsque les fichiers sont importés dans votre dossier de bibliothèque assigné, Lidarr tentera de créer un lien physique vers le fichier ou le copiera (utilisant ainsi un double espace) s'il ne prend pas en charge les liens physiques.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres, Lidarr demandera au client de torrent de supprimer le fichier et le torrent d'origine, mais cela ne se produira que si le client signale que le partage est terminé, que le torrent est dans la même catégorie (c'est-à-dire qu'il n'utilise pas de catégorie après importation), que l'objectif de partage atteint est pris en charge par Lidarr et que le torrent est en pause (arrêté).

### Gestion des échecs de téléchargement

- La gestion des échecs de téléchargement est uniquement compatible avec SABnzbd et NZBGet.
- La gestion des échecs de téléchargement ne s'applique pas aux torrents et il n'est pas prévu d'ajouter une telle fonctionnalité.

- Plusieurs composants composent le processus de gestion des échecs de téléchargement :

- Vérification du téléchargeur :
  - File d'attente - Vérifiez la file d'attente de votre téléchargeur pour les versions protégées par mot de passe (cryptées) marquées comme échec
  - Historique - Vérifiez l'historique de votre téléchargeur pour les échecs (par exemple, pas assez de blocs pour réparer ou échec de l'extraction)
- Lorsque Lidarr trouve un téléchargement en échec, il commence à les traiter et fait quelques actions :
  - Ajoute un événement d'échec à l'historique de Lidarr
  - Supprime le téléchargement en échec du client de téléchargement pour libérer de l'espace et effacer les fichiers téléchargés (facultatif)
  - Commence à rechercher un fichier de remplacement (facultatif)
  - La liste de blocage (anciennement appelée "liste noire") permet de sauter automatiquement les fichiers NZB en cas d'échec, ce qui signifie que cet NZB ne sera jamais téléchargé automatiquement par Lidarr (vous pouvez toujours forcer le téléchargement via une recherche manuelle).
  - Il existe 2 options avancées (sur la page des paramètres du "Client de téléchargement") qui contrôlent le comportement des échecs de téléchargement dans Lidarr, à l'heure actuelle, elles sont toutes activées par défaut.

- Redownload - Contrôle si Lidarr recherchera ou non le même fichier après un échec
- (Option avancée) Remove - Indique si le téléchargement doit être automatiquement supprimé du client de téléchargement lorsque l'échec est détecté

## Correspondances de chemin distant

- La correspondance de chemin distant agit comme une recherche et un remplacement de chemin distant par un chemin local. Cela est principalement utilisé pour les configurations locales/à distance fusionnées utilisant mergerfs ou similaire, ou est utilisé lorsque l'application et le client de téléchargement ne sont pas sur le même serveur.
- Une correspondance de chemin distant est utilisée lorsque votre client de téléchargement signale un chemin pour les données terminées soit sur un autre serveur, soit d'une manière que \*Arr n'adresse pas ce dossier.
- En général, une correspondance de chemin distant n'est nécessaire que si votre client de téléchargement est sur Linux lorsque \*Arr est sur Windows ou vice versa. Une correspondance de chemin distant est également peut-être nécessaire si vous mélangez des clients Docker et natifs ou si vous utilisez un serveur distant.
- Une correspondance de chemin distant est une recherche/remplacement DUMB (où elle trouve la valeur DISTANTE, la remplace par la valeur LOCALE pour l'Hôte spécifié).
- Si le message d'erreur concernant un mauvais chemin ne contient pas la valeur REMPLACÉE, alors la correspondance de chemin n'est pas utilisée comme vous le souhaitez. La solution typique consiste à ajouter et supprimer la correspondance.
- [Consultez le tutoriel de TRaSH pour plus d'informations sur la correspondance de chemin distant](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Si à la fois \*Arr et votre client de téléchargement sont des conteneurs Docker, il est rare qu'une correspondance de chemin distant soit nécessaire. Il est recommandé de [consulter le guide Docker](/docker-guide) et/ou de [suivre le tutoriel de TRaSH](https://trash-guides.info/hardlinks)
{.is-info}

# Importer des listes

> Des informations sur les types de listes pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/lidarr/supported#lists) de cette section
{.is-info}

Les listes d'importation vous permettent d'ajouter des éléments à Lidarr à partir de Spotify ou Last.fm. Cela peut potentiellement ajouter beaucoup d'éléments inattendus à votre base de données Lidarr, veuillez donc l'utiliser avec précaution.

<!-- ![importlists.png](/assets/readarr/importlists.png) -->

## Listes d'importation

Cela vous montre les listes que vous avez actuellement et vous permet d'ajouter de nouvelles listes. L'ajout de listes est expliqué plus en détail ci-dessous.

## Exclusions de listes d'importation

Tout ce qui se trouve ici a été exclu de l'ajout par les listes et ne sera jamais ajouté à partir d'une liste quelconque. Vous pouvez supprimer des éléments de cette liste en cliquant dessus.

## Ajouter une liste d'importation

Après avoir cliqué sur le <kb>+</kb>, choisissez le type de liste que vous souhaitez ajouter :

<!-- ![addlist.png](/assets/readarr/addlist.png) -->

Dans cet exemple, nous allons ajouter une liste d'albums enregistrés sur Spotify.

<!-- ![bookshelflist.png](/assets/readarr/bookshelflist.png) -->

- Nom - Entrez un nom pour cette liste.
- Activer l'ajout automatique - Si activé, tout ce qui se trouve sur la liste sera automatiquement ajouté à Lidarr.

> Cela va ajouter TOUS LES ALBUMS de cet artiste à Lidarr !

- Surveillance - Sélectionnez votre niveau de surveillance pour les éléments ajoutés. Les options valides sont `Aucun`, `Album spécifique` et `Tous les albums de l'artiste`. Tous les albums sont ajoutés à Lidarr, mais ils seront surveillés ou non en fonction de cette sélection.
- Dossier racine - Choisissez le dossier racine pour les artistes ajoutés à partir de cette liste.
- Surveiller les nouveaux albums - Choisissez ce que Lidarr doit faire avec les futurs albums de l'artiste ajouté. Les options valides sont `Tous les albums`, `Aucun`, `Nouveaux`.
- Profil de qualité - Choisissez votre profil de qualité pour les artistes ajoutés à partir de cette liste.
- Profil de métadonnées - Choisissez votre profil de métadonnées pour les artistes ajoutés à partir de cette liste.
- Tags Lidarr - Choisissez les tags qui s'appliquent aux artistes ajoutés à partir de cette liste.

> Il est fortement recommandé d'ajouter un tag descriptif ici. Sinon, vous ne saurez pas quelle liste a ajouté ces éléments à Lidarr, et une fois qu'ils sont ajoutés, vous ne pourrez plus obtenir cette information ! Ces informations ne sont pas enregistrées !

Les listes se synchronisent par défaut toutes les 24 heures, mais peuvent être déclenchées manuellement depuis la page `Système` => `Tâches`. Vous ne pouvez pas automatiser ce processus plus rapidement que cela.

# Connexions

> Des informations sur les types de connexion pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/lidarr/supported#notifications) de cette section
{.is-info}

# Tags

- La section des tags dans Lidarr est utilisée pour lier différents aspects de Lidarr.
- Les tags sont particulièrement utiles pour :

  - Les profils de retard
  - Les profils de sortie
  - Les indexeurs

- Les tags peuvent être utilisés pour lier des profils de retard, des profils de sortie, des indexeurs et des artistes/albums ensemble.
- Par exemple :
  - Vous voulez qu'un artiste/album spécifique utilise uniquement un indexeur spécifique. Vous créez un tag et assignez l'artiste/album et l'indexeur à ce tag.
  - Vous voulez qu'un profil de sortie spécifique utilise uniquement un profil de retard spécifique. Vous créez un tag et assignez le profil de sortie et le profil de retard à ce tag.

> Note : Les tags n'influencent pas les "Profils de qualité", les "Profils de métadonnées" ou tout autre aspect non mentionné ci-dessus.
{.is-info}

# Général

## Mises à jour

- (Option avancée) Branche - Il s'agit de la branche de Lidarr que vous utilisez.
  - [Veuillez consulter cette entrée de FAQ pour plus d'informations](/lidarr/faq#how-do-i-update-lidarr)
- Automatique - Téléchargez et installez automatiquement les mises à jour. Vous pourrez toujours installer depuis Système : Mises à jour. Note : Les utilisateurs de Windows sont toujours mis à jour automatiquement.
- Mécanisme - Utilisez le programme de mise à jour intégré de Lidarr ou un script
  - Intégré - Utilisez le programme de mise à jour intégré de Lidarr
  - Script - Faites exécuter le script de mise à jour par Lidarr
  - Docker - Ne mettez pas à jour Lidarr depuis l'intérieur du Docker, mais téléchargez une nouvelle image avec la nouvelle mise à jour
- Script - Visible uniquement lorsque le mécanisme est défini sur Script - Chemin vers le script de mise à jour
- Processus de mise à jour - Lidarr téléchargera le fichier de mise à jour, vérifiera son intégrité, l'extraiera dans un emplacement temporaire et appellera la méthode choisie. Le processus de mise à jour sera exécuté sous le même utilisateur que celui sous lequel Lidarr est exécuté, il aura besoin des autorisations pour mettre à jour les fichiers Lidarr ainsi que pour arrêter/démarrer Lidarr.
- Intégré - La méthode intégrée sauvegardera les fichiers et les paramètres de Lidarr, arrêtera Lidarr, mettra à jour l'installation et démarrera Lidarr. Si votre système ne gère pas l'arrêt de Lidarr et tente de le redémarrer automatiquement, il est préférable d'utiliser un script à la place. En cas d'échec, la version précédente de Lidarr sera redémarrée.
- Script - Le script devrait gérer la même chose que le programme de mise à jour intégré. Si vous devez gérer l'arrêt et le démarrage des services (upstart/launchd/etc), vous devrez le faire ici.