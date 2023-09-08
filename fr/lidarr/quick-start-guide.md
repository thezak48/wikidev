---
title: Guide de démarrage rapide de Lidarr
description: 
published: true
date: 2022-07-14T14:10:13.343Z
tags: 
editor: markdown
dateCreated: 2021-06-13T06:14:53.615Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Guide de configuration rapide](#guide-de-configuration-rapide)
- [Limitations](#limitations)
- [Concept](#concept)
  - [Sorties (Métadonnées)](#sorties-métadonnées)
  - [Artiste (Métadonnées)](#artiste-métadonnées)
- [Premier démarrage](#premier-démarrage)
- [Paramètres](#paramètres)
  - [Gestion des médias](#gestion-des-médias)
  - [Profils](#profils)
  - [Qualité](#qualité)
  - [Indexeurs](#indexeurs)
  - [Clients de téléchargement](#clients-de-téléchargement)
    - [{.tabset}](#tabset)
      - [Usenet](#usenet)
      - [BitTorrent](#bittorrent)
- [Premier artiste](#premier-artiste)
- [Premier téléchargement/importation](#premier-téléchargementimportation)
- [Guide de démarrage rapide - Avancé](#guide-de-démarrage-rapide---avancé)
  - [Cas d'utilisation de Lidarr](#cas-dutilisation-de-lidarr)
    - [Fichiers individuels](#fichiers-individuels)
    - [Bibliothèques spécialisées](#bibliothèques-spécialisées)
  - [Importation d'une bibliothèque ou de fichiers existants](#importation-dune-bibliothèque-ou-de-fichiers-existants)
    - [Préparation de vos fichiers existants](#préparation-de-vos-fichiers-existants)
      - [Structure des dossiers](#structure-des-dossiers)
      - [Balisage](#balisage)
    - [Considérations avant l'importation](#considérations-avant-limportation)
    - [Commencer l'importation](#commencer-limportation)

# Guide de configuration rapide

> Cette page est encore en cours de rédaction et n'est pas complète. Les contributions sont les bienvenues.

> Pour une description plus détaillée de tous les paramètres, consultez [Lidarr => Paramètres](/lidarr/settings)
{.is-info}

Dans ce guide, nous essaierons d'expliquer la configuration de base que vous devez effectuer pour commencer avec Lidarr. Nous allons passer en revue certaines options que vous pouvez voir à l'écran. Si vous souhaitez approfondir ces options, veuillez consulter la page appropriée dans la FAQ et la documentation pour une explication complète.

> Veuillez noter que dans les captures d'écran et les paramètres de l'interface utilisateur en `orange`, il s'agit d'options avancées. Vous devrez cliquer sur `Afficher les options avancées` en haut de la page pour les rendre visibles.
{.is-warning}

# Limitations

Dans ce guide, nous expliquerons les étapes de base pour commencer à utiliser Lidarr. Ce guide suppose que vous avez déjà installé l'application. Les instructions d'installation se trouvent à la page suivante [installation](/lidarr/installation). Nous nous concentrerons sur la configuration/options minimales pour obtenir une configuration fonctionnelle. Il existe des configurations et des considérations supplémentaires si l'une des situations suivantes s'applique :

- Bibliothèque ou fichiers existants
- Cas d'utilisation incorrect
- Structure de dossier incorrecte
- Balisage incorrect ou extrêmement compliqué
- Collection de fichiers non structurée
- Bibliothèques de musique spécialisées : Classique, Singles, Électronique

Si l'une des situations ci-dessus s'applique, veuillez vous référer à la section Guide de démarrage rapide - Avancé.

Ce guide est divisé en sections. Il est recommandé de lire l'ensemble du guide pour une compréhension complète, mais vous pouvez passer à des sections spécifiques pour des préoccupations immédiates. Utilisez le plan à gauche pour passer rapidement.

# Concept

Pour utiliser correctement Lidarr, il est nécessaire de comprendre les concepts sous-jacents. Dans les grandes lignes, il suit les principes des autres applications Arr. Lidarr agit comme un système de gestion de bibliothèque musicale, un agrégateur de données et une plateforme d'automatisation pour trouver et télécharger des médias.

Ensuite, la déviation est assez importante. La gestion d'une bibliothèque musicale est un processus très complexe car il existe de nombreuses variables concurrentes qui entravent le processus. Contrairement à la gestion de films ou de séries télévisées, il n'existe pas d'ensemble cohérent de normes pour le balisage, le nommage ou le stockage de la musique. Cela a été encore compliqué par les méthodes changeantes de distribution de la musique, passant des supports physiques à l'électronique. Enfin, les opinions sur la manière de gérer cette gestion sont nombreuses et variées.

Lidarr utilise des informations provenant de services d'agrégation de données pour baliser et gérer correctement la bibliothèque musicale. Ces données tierces représentent des médias dans des catégories et des types définis.

> Si les données n'existent pas dans les services tiers, elles NE PEUVENT PAS être gérées par Lidarr.
Les détails sont ci-dessous pour participer et contribuer.
{.is-warning}

Le principal service utilisé est [MusicBrainz](https://musicbrainz.org/). Il s'agit d'un service gratuit, piloté par la communauté, qui existe et survit grâce à vos contributions et votre participation. La création et la contribution de sorties dépassent le cadre de ce guide. Les instructions peuvent être trouvées ici : [Comment contribuer](https://musicbrainz.org/doc/How_to_Contribute)

En fin de compte, les données sont définies par les normes de données tierces. Si les normes ne correspondent pas à votre cas d'utilisation, **Lidarr peut ne pas être la solution appropriée**. D'autres applications pour la gestion de vos médias peuvent inclure :

[Gestion des médias Beets](https://beets.io/)
[MusicBrainz Picard](https://picard.musicbrainz.org/)
[Music Bee](https://getmusicbee.com/)

Ces implémentations peuvent être utilisées conjointement avec Lidarr, mais cela dépasse le cadre de ce guide.

## Sorties (Métadonnées)

Lidarr a choisi la norme `Sortie` pour la gestion des médias musicaux. Cela signifie que pour que le système fonctionne correctement, tous les médias traités par le système doivent être une `Sortie`.

Exemples de sorties :

- Album
- EP
- Single
- Diffusion

Chaque élément à gérer doit avoir une `Sortie` correspondante dans le service de données tiers.

> Les `Sorties` doivent exister dans les services tiers pour être gérées dans Lidarr.

## Artiste (Métadonnées)

Les artistes sont exactement ce à quoi on peut s'attendre de l'`Artiste de la Sortie`. Malheureusement, le nom des artistes, leur style, les changements au fil du temps, les préférences des utilisateurs et d'autres raisons ont compliqué ce qui constitue cet `Artiste de la Sortie`.

Exemples d'artistes corrects et incorrects :

- Bob Dylan
- BOB DYLAN
- The Bob Dylan
- Bob Dylan, The
- Bob Dylan & the Band
- Bob Dylan feat. The Band
- The Band featuring Bob Dylan
- ...

La liste pourrait continuer ainsi de suite. Encore une fois, toutes les `Sorties` sont corrélées à un `Artiste`. Vous devez trouver (étapes ultérieures de ce guide) et utiliser le `Artiste` approprié pour télécharger une `Sortie`.

> Les `Artistes de Sortie` doivent exister dans les services tiers pour être gérés dans Lidarr.

# Premier démarrage

Après l'installation et le démarrage de Lidarr, vous y accédez en ouvrant un navigateur et en allant à `http://{votre_ip_ici}:8686`

![lidarr_qs_startup.png](/assets/lidarr/quick-start-guide/lidarr_qs_startup.png)

Il y a deux options affichées à l'écran de démarrage, mais nous ne les utiliserons pas initialement.

# Paramètres

Nous utiliserons la configuration par défaut des paramètres pour configurer Lidarr. Cela utilisera les profils, la qualité, les balises, etc. existants.

> Pour une description plus détaillée de tous les paramètres, consultez [Lidarr > Paramètres](/lidarr/settings)
{.is-info}

## Gestion des médias

Tout d'abord, nous allons jeter un coup d'œil à la `Gestion des médias` où nous allons définir le `Dossier racine`. Cela sera l'emplacement où les fichiers multimédias seront stockés.

> Ne stockez pas les médias Lidarr sur un fournisseur de stockage cloud ! En raison de la manière dont Lidarr utilise les balises, cela tuera toutes les limites de l'API et causera des problèmes. Conservez votre bibliothèque sur votre réseau.
{.is-warning}

Cliquez sur `Paramètres` > `Gestion des médias` dans le menu de gauche.

![lidarr_qs_mediamanagement.png](/assets/lidarr/quick-start-guide/lidarr_qs_mediamanagement.png)

Cliquez sur `Ajouter (+)` des `Dossiers racines`.

Vous serez présenté avec la fenêtre suivante :

![lidarr_qs_rootfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_rootfolder.png)

- **Nom** - Il s'agit du `Nom convivial` de l'emplacement de stockage.
- **Chemin** - Il s'agit du `Chemin` réel de l'emplacement de stockage des données. Le système/l'utilisateur doit disposer des autorisations appropriées pour ce chemin de stockage. Ce dossier ne peut pas être votre emplacement de téléchargement !

Laissez les autres options par défaut.

> Si vous utilisez un `Dossier racine` avec des fichiers existants, consultez la section Guide de démarrage rapide - Avancé pour des considérations.
{.is-warning}

> \* Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

> **L'utilisateur et le groupe que vous avez configurés pour exécuter Lidarr doivent avoir un accès en lecture et en écriture à cet emplacement.** {.is-info}

> Votre client de téléchargement télécharge dans un dossier de téléchargement et Lidarr l'importe dans votre dossier multimédia (destination finale) que votre serveur multimédia utilise.
{.is-info}

> **Votre dossier de téléchargement et votre dossier multimédia ne peuvent pas être le même emplacement**
{.is-danger}

## Profils

`Paramètres` > `Profils`

Les paramètres de profil resteront à leurs valeurs par défaut.

## Qualité

`Paramètres` > `Qualité`

Les paramètres de qualité resteront à leurs valeurs par défaut.

## Indexeurs

`Paramètres` > `Indexeurs`

Cette section définit les indexeurs/trackers que vous utiliserez pour trouver des fichiers multimédias téléchargeables.

Cliquez sur `Ajouter (+)` des `Indexeurs`. Vous serez présenté avec une nouvelle fenêtre contenant de nombreuses options différentes. Lidarr considère à la fois les indexeurs Usenet et les trackers BitTorrent comme des `Indexeurs`.

Ajoutez au moins un `Indexeur` pour que Lidarr puisse trouver correctement les fichiers disponibles.

La configuration et les concepts des `Indexeurs` dépassent le cadre de ce guide. Internet regorge d'informations sur le sujet.

## Clients de téléchargement

`Paramètres` => `Clients de téléchargement`

![Lidarr-settings-download-clients.png](/assets/lidarr/Lidarr-settings-download-clients.png)

Le téléchargement et l'importation sont les étapes où la plupart des personnes rencontrent des problèmes. D'un point de vue général, le logiciel doit être capable de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une variété encore plus grande de configurations. Cela signifie qu'il existe quelques configurations courantes, mais il n'y a pas de configuration unique et la configuration de chacun peut être légèrement différente. Mais il existe de nombreuses configurations incorrectes.

> Consultez la [page des paramètres](/lidarr/settings#download-clients), la page [Plus d'informations (Pris en charge)](/lidarr/supported#download-clients) pour cette section, et [Guides des clients de téléchargement de TRaSH](https://trash-guides.info/Downloaders/) pour plus d'informations.
{.is-info}

### {.tabset}

#### Usenet

{#usenet}

- Lidarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Lidarr surveillera les téléchargements actifs de vos clients de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Lidarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Lidarr.
- Lidarr analysera cet emplacement de fichier terminé pour trouver des fichiers que Lidarr peut utiliser. Il analysera le nom du fichier pour le faire correspondre à la demande de média. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être les mêmes pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens physiques et les déplacements atomiques, Lidarr effectuera une copie du fichier, puis le supprimera de la source, ce qui est intensif en E/S.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Lidarr, les fichiers restants du téléchargement seront envoyés à votre corbeille ou à votre recyclage via une demande à votre client pour supprimer la sortie.

#### BitTorrent

{#bittorrent}

- Lidarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Lidarr surveillera les téléchargements actifs de vos clients de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou le temps peut être ajusté dans le client de téléchargement ou depuis Lidarr sous le client de téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, Lidarr créera un lien physique vers le fichier s'il est pris en charge par votre configuration, sinon il le copiera si les liens physiques ne sont pas pris en charge.
- Les liens physiques sont activés par défaut. [Un lien physique ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être les mêmes pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, Lidarr effectuera une copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Lidarr, Lidarr supprimera le torrent de votre client et demandera au client de supprimer les données du torrent, mais seulement si le client signale que le partage est terminé et que le torrent est arrêté (en pause à la fin).

# Premier artiste

Si vous suivez ce guide et que votre `Dossier racine` ne contient aucun fichier multimédia, vous devrez ajouter un `Artiste`.

`Bibliothèque` > `Ajouter un nouvel artiste`

![lidarr_qs_addnew.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnew.png)

Cela vous mènera à l'écran de recherche pour trouver un artiste. Recherchez et sélectionnez l'`Artiste` que vous souhaitez ajouter. Cela ouvrira la fenêtre "Ajouter un nouvel artiste".

![lidarr_qs_addnewdylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnewdylan.png)

Nous utiliserons les sélections par défaut. Celles-ci devraient inclure :

- Dossier racine - Le dossier que vous avez créé
- Surveillance - Aucune
- Profil de qualité - Tout
- Balises - (vide)
- Démarrer la recherche des albums manquants - Non cochée

Cela lancera le téléchargement des métadonnées de l'`Artiste`. Cela prendra du temps en fonction de la quantité de données à collecter. Rappelez-vous que ces informations proviennent de sources tierces et ne sont aussi complètes que ce que la communauté a contribué.

Cliquez sur le nouvel `Artiste` ajouté. (Bob Dylan dans cet exemple)

> Le `Profil de métadonnées` par défaut est utilisé, seules les `Sorties` de type `Albums studio` seront affichées.

![lidarr_qs_dylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylan.png)

> Vous n'aimez pas les métadonnées téléchargées ? - Contribuez pour les améliorer !
{.is-info}

# Premier téléchargement/importation

Enfin, il est temps de télécharger/importer votre première `Sortie` !

Trouvez la `Sortie` que vous souhaitez ajouter à votre bibliothèque. Sélectionnez l'icône de recherche manuelle (humaine) à côté de la sortie.

![lidarr_qs_dylanrelease.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanrelease.png)

Cela ouvrira la fenêtre de sélection de la `Sortie`. Cette fenêtre affichera les résultats de la requête de l'`Indexeur` ou simplement les résultats de recherche des téléchargements disponibles.

> Le `Profil de qualité` par défaut autorise tous les types de fichiers. Le `Profil de sortie` par défaut autorise tous les téléchargements. Pour une description détaillée de ces paramètres avancés, consultez [Lidarr > Paramètres](/lidarr/settings)

![lidarr_qs_dylandownload.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylandownload.png)

Examinez la fenêtre de téléchargement pour les différentes informations fournies :

1. Titre - Il s'agit du nom du téléchargement tel qu'il est renvoyé par l'`Indexeur`.
1. Qualité - Il s'agit de la qualité déterminée par Lidarr en utilisant le titre.
1. Les indicateurs d'avertissement donneront une description de la raison pour laquelle le téléchargement a échoué aux vérifications de Lidarr. Dans l'exemple, la recherche a renvoyé "Mauvais album".

Lorsque vous avez examiné, sélectionnez l'icône de téléchargement (numéro 4) pour télécharger la `Sortie` disponible.

Si la configuration est correcte, le téléchargement sera envoyé à votre `Client de téléchargement`.

Le téléchargement sera ajouté à la `File d'attente` et passera par les différents états de votre type de `Client de téléchargement`.

Enfin, le téléchargement sera importé dans votre `Dossier racine`. Si tout se passe bien, il devrait apparaître comme ci-dessous.

![lidarr_qs_dylansucess.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylansuccess.png)

Vous pouvez trouver vos fichiers téléchargés dans votre `Dossier racine` et les lire avec le lecteur multimédia de votre choix.

![lidarr_qs_dylanfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanfolder.png)

# Démarrage rapide - Avancé

Cette section avancée est destinée aux configurations qui peuvent nécessiter des considérations spéciales. Veuillez les examiner si elles s'appliquent à votre configuration et vous pourriez ainsi éviter quelques problèmes.

> Les sections suivantes vous aideront à éviter les problèmes courants.
{.is-warning}

## Cas d'utilisation de Lidarr

Comme indiqué précédemment dans la section Concept. Lidarr ne doit pas être utilisé si votre utilisation prévue ne correspond pas au système de gestion des `Releases` de Lidarr. Lidarr NE fonctionnera PAS avec les cas d'utilisation suivants :

- Collection de fichiers non organisée - Fichiers provenant de plusieurs artistes (non compilations) ou de plusieurs `Releases`
- Bibliothèques de musique spécialisées : Classique, Singles, Électronique

### Fichiers non organisés

Une faible ou aucune organisation des fichiers non organisés ne fonctionnera pas avec Lidarr. Il vaut mieux ne pas essayer d'utiliser ces fichiers avec Lidarr.

### Bibliothèques spécialisées

Les bibliothèques spécialisées posent des problèmes uniques à tout système de gestion. Ces situations peuvent fonctionner avec Lidarr, mais cela peut nécessiter un travail important de votre part, en renonçant pratiquement aux automatisations intégrées. Par exemple :

- **Musique classique** - Elle nécessite généralement des exigences ou des souhaits de balisage étendus. Les métadonnées des `Releases` risquent de ne pas exister ou d'être incorrectes.
- **Singles** - Les singles peuvent ne pas être de véritables `Releases`. Les services de données tiers ne renverront aucune métadonnée. Ils ne seront pas automatisés et Lidarr ne pourra pas les gérer.
- **Électronique** - Cela NE s'applique pas aux `Releases` du genre Électronique. Cela concerne les bibliothèques de mixes, de beats, d'échantillons, etc. (Beatport). Les sources de données tierces ne reconnaissent pas ces éléments comme des `Releases`. Ils ne seront pas automatisés et Lidarr ne pourra pas les gérer.

## Importation d'une bibliothèque ou de fichiers existants

> Notez que Lidarr ne recherche pas régulièrement de `Releases`. Consultez ces deux entrées de FAQ pour comprendre comment Lidarr fonctionne.
[Comment Lidarr trouve-t-il des `Releases` ?](/lidarr/faq#how-does-lidarr-find-releases) et [Comment Lidarr fonctionne-t-il ?](/lidarr/faq#how-does-lidarr-work)
{.is-info}

> L'importation automatisée est un processus planifié et ne peut pas être arrêtée une fois lancée.
NE PAS ajouter un `Dossier racine` avec des fichiers existants avant d'avoir lu cette section en entier.
{.is-warning}

Lidarr utilise un système automatisé pour ajouter les `Release Artists` et les `Releases` situés dans votre `Dossier racine`.

Si le cas d'utilisation de Lidarr correspond et que vous n'avez pas de bibliothèques uniques ou spécialisées. Vous pouvez procéder à l'importation de votre bibliothèque existante.

Il est impératif que les fichiers de votre bibliothèque existante soient structurés et suivent le système de gestion des `Releases` de Lidarr. Cela signifie que les éléments suivants ne fonctionneront pas :

- Structure de dossier incorrecte - Fichiers situés dans un seul dossier - Reportez-vous à la section Préparation>Structure des dossiers
- Balisage incorrect ou extrêmement compliqué - Reportez-vous à la section Préparation>Balisage

### Préparation de vos fichiers existants

Pour que le processus automatisé fonctionne, vos fichiers doivent être préparés pour que cela se déroule efficacement ou fonctionne du tout.

#### Structure des dossiers

Il est recommandé de suivre la structure de dossier standard :

\Dossier racine\Artiste de la `Release`\`Release`\XX - Piste

Cela, combiné à des balises appropriées, permettra une reconnaissance par les lecteurs multimédias d'environ 95% ou plus.

#### Balisage

Le balisage peut être une procédure compliquée. Le nombre de fichiers et la façon dont ils sont actuellement balisés détermineront l'effort nécessaire.

Les méthodes recommandées pour baliser vos fichiers sont les suivantes :

- MusicBrainz Picard
- Beets
- MusicBee, MediaMonkey, JRiver

L'utilisation de ces applications dépasse le cadre de ce guide, mais il est préférable d'associer les identifiants de `Release` de MusicBrainz dans le processus de balisage.

> La plupart des logiciels de balisage sont capables de structurer et de renommer les dossiers tout en balisant correctement les fichiers.
{.is-info}

### Considérations avant l'importation

Une fois que les fichiers sont correctement balisés et nommés, les éléments suivants doivent être vérifiés pour s'assurer que le processus se terminera avec succès :

- **Architecture du système** - Recommandée x64 / 64 bits - L'importation de grandes bibliothèques nécessite que le système accède à de grandes quantités de RAM et calcule de manière plus efficace. x86 / 32 bits est pris en charge, mais il sera moins efficace et prendra beaucoup plus de temps.
- **Exigences de mémoire système (RAM)** - Minimum 4 Go, recommandé 8 Go - Le processus d'importation nécessite beaucoup de mémoire et avoir Lidarr en cours d'importation et un navigateur ouvert entraînera une utilisation substantielle de la RAM.
- **Limites de disque/piste des `Releases`** - Les `Releases` qui comportent un grand nombre de pistes ou de disques doivent être exclus du processus d'importation. Ils peuvent être importés manuellement en utilisant les procédures intégrées. Il n'y a pas de limite exacte, mais pour être prudent, les `Releases` comportant plus de 25 disques ou 250 pistes doivent être exclus.
- **`Release Artist` avec de nombreuses `Releases`** - Le processus automatisé de Lidarr compare les `Releases` à vos fichiers. Bien que peu probable d'échouer, le fait de faire passer ces fichiers par la procédure automatisée entraînera une augmentation substantielle du temps d'importation. Il existe des artistes uniques avec des milliers de `Releases`.
- **Temps** - La procédure d'importation automatisée prend du temps. Une estimation raisonnable serait de 1 heure pour 500 `Releases` correctement balisées. Cela varie considérablement en fonction de votre stockage, de la vitesse de votre connexion Internet et des performances de votre système.

### Commencer l'importation

//

Bientôt disponible

- Monitor * - Cela définit l'option de surveillance par défaut (`Releases`) pour le `Dossier racine`.
- Profil de qualité * - Cela définit l'option de qualité par défaut pour le `Dossier racine`.
- Profil de métadonnées * - Cela définit l'option de métadonnées par défaut pour le `Dossier racine`.