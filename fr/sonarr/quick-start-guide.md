---
title: Guide de démarrage rapide de Sonarr
description: 
published: true
date: 2022-07-14T14:07:19.793Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-09-03T19:14:22.283Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Guide de configuration rapide](#guide-de-configuration-rapide)
- [Démarrage](#démarrage)
- [Gestion des médias](#gestion-des-médias)
  - [Nom des épisodes](#nom-des-épisodes)
  - [Importation](#importation)
  - [Dossiers racine](#dossiers-racine)
- [Profils](#profils)
- [Indexeurs](#indexeurs)
- [Clients de téléchargement](#clients-de-téléchargement)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
- [Comment importer votre bibliothèque multimédia organisée existante](#comment-importer-votre-bibliothèque-multimédia-organisée-existante)
  - [Importer des épisodes](#importer-des-épisodes)
    - [Importation de médias existants](#importation-de-médias-existants)
    - [Aucune correspondance trouvée](#aucune-correspondance-trouvée)
    - [Corriger le nom de dossier défectueux après l'importation](#corriger-le-nom-de-dossier-défectueux-après-limportation)
- [Ajouter une nouvelle série](#ajouter-une-nouvelle-série)

# Guide de configuration rapide

> Cette page est encore en cours de réalisation et n'est pas complète. Les contributions sont les bienvenues.

> Pour une description plus détaillée de tous les paramètres, consultez [Sonarr => Paramètres](/sonarr/settings)
{.is-info}

Dans ce guide, nous allons essayer d'expliquer la configuration de base que vous devez effectuer pour commencer avec Sonarr. Nous allons passer en revue certaines options que vous pouvez voir à l'écran. Si vous souhaitez approfondir ces options, veuillez consulter la page appropriée dans la FAQ et la documentation pour une explication complète.

> Veuillez noter que dans les captures d'écran et les paramètres de l'interface utilisateur en `orange`, il s'agit d'options avancées. Vous devrez cliquer sur `Afficher les options avancées` en haut de la page pour les rendre visibles.
{.is-warning}

# Démarrage

Après l'installation et le démarrage, ouvrez un navigateur et allez à `http://{votre_ip_ici}:8989`

![qs_startup.png](/assets/sonarr/qs_startup.png)

# Gestion des médias

Tout d'abord, nous allons jeter un coup d'œil aux paramètres de `Gestion des médias` où nous pouvons configurer nos préférences de nommage et de gestion des fichiers.

Cliquez sur `Paramètres` => `Gestion des médias` dans le menu de gauche.

## Nom des épisodes

![qs_episodenaming.png](/assets/sonarr/qs_episodenaming.png)

- Cochez la case pour activer le renommage des épisodes.
- Déterminez vos conventions de nommage des épisodes standard, quotidiens et d'anime. Vous devriez consulter les conventions de nommage recommandées [ici](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/).

> Si vous choisissez de ne pas inclure la qualité/résolution ou le groupe de sortie, ces informations seront perdues par la suite. Il est fortement recommandé de les inclure dans votre schéma de nommage.
{.is-info}

## Importation

![mm_importing.png](/assets/sonarr/mm_importing.png)

- (Option avancée) Si vous souhaitez que les épisodes à venir soient importés immédiatement, modifiez "Titre de l'épisode requis" en "Jamais".
- (Option avancée) Activez `Utiliser des liens durs au lieu de la copie` pour plus d'informations sur la manière et la raison avec des exemples [Guide des liens durs de TRaSH](https://trash-guides.info/hardlinks).
- Cochez la case pour importer des fichiers supplémentaires et ajoutez au moins `.srt` à la liste.

## Dossiers racine

Ici, nous allons ajouter le dossier racine que Sonarr utilisera pour importer votre bibliothèque multimédia organisée existante et où Sonarr importera (copie/liens durs/déplacement) vos médias après que votre client de téléchargement les a téléchargés. Il s'agit du dossier où vos séries et épisodes sont stockés pour que votre lecteur multimédia puisse les lire. Ce n'est pas l'endroit où vous téléchargez les fichiers !

> \* Utilisateurs non Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

> **L'utilisateur et le groupe que vous avez configurés pour exécuter Sonarr doivent avoir un accès en lecture et en écriture à cet emplacement.**
{.is-info}

> **Votre dossier de téléchargement et votre dossier multimédia ne peuvent pas être situés au même endroit.**
{.is-danger}

N'oubliez pas d'enregistrer vos modifications !

# Profils

`Paramètres` => `Profils`

Nous vous recommandons de créer vos propres profils et de ne sélectionner que les sources de qualité dont vous avez réellement besoin. Cependant, plusieurs profils de qualité préremplis sont également disponibles, si l'un d'entre eux convient. Si vous avez besoin de plus d'informations sur les profils, veuillez consulter la [page wiki appropriée](/sonarr/settings#profiles) pour cette section.

# Indexeurs

`Paramètres` => `Indexeurs`

Ici, vous allez ajouter les indexeurs/trackers que vous allez utiliser pour télécharger vos fichiers.

Une fois que vous avez cliqué sur le bouton <kb>+</kb> pour ajouter un nouvel indexeur, une nouvelle fenêtre s'ouvre avec de nombreuses options différentes. Aux fins de cette documentation, Sonarr considère à la fois les indexeurs Usenet et les trackers BitTorrent comme des "indexeurs".

Il y a deux sections ici : Usenet et Torrents. En fonction du client de téléchargement que vous allez utiliser, vous devrez sélectionner le type d'indexeur que vous allez utiliser.

La plupart des indexeurs Usenet nécessitent une clé API, qui peut être trouvée sur la page de votre profil sur le site de l'indexeur.

La plupart des trackers BitTorrent nécessitent [Prowlarr](/prowlarr) ou Jackett pour être utilisés dans Sonarr.

Ajoutez au moins un indexeur pour que Sonarr fonctionne correctement.

> Consultez la [page des paramètres](/sonarr/settings#indexers) et la page [Plus d'informations (Pris en charge)](/sonarr/supported#indexers) pour cette section pour plus d'informations.
{.is-info}

# Clients de téléchargement

`Paramètres` => `Clients de téléchargement`

Le téléchargement et l'importation sont les étapes où la plupart des utilisateurs rencontrent des problèmes. D'un point de vue général, le logiciel doit être capable de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une variété encore plus grande de configurations. Cela signifie qu'il n'y a pas de configuration unique qui convienne à tous, mais il y a de nombreuses configurations incorrectes.

> Consultez la [page des paramètres](/sonarr/settings#download-clients), la page [Plus d'informations (Pris en charge)](/sonarr/supported#download-clients) pour cette section, et les [Guides des clients de téléchargement de TRaSH](https://trash-guides.info/Downloaders/) pour plus d'informations.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Sonarr enverra une demande de téléchargement à votre client et l'associera à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Sonarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Sonarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Sonarr.
- Sonarr analysera cet emplacement de fichier terminé à la recherche de fichiers que Sonarr peut utiliser. Il analysera le nom du fichier pour le faire correspondre avec le média demandé. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être les mêmes pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens durs et les déplacements atomiques, Sonarr effectuera une copie du fichier, puis le supprimera de la source, ce qui est intensif en termes d'E/S.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Sonarr, les fichiers restants du téléchargement seront envoyés à la corbeille ou au recyclage via une demande à votre client pour supprimer le téléchargement.

### BitTorrent

{#bittorrent}

- Sonarr enverra une demande de téléchargement à votre client et l'associera à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Sonarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou la durée peuvent être ajustés dans le client de téléchargement ou depuis Sonarr sous le client de téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, Sonarr créera un lien dur vers le fichier s'il est pris en charge par votre configuration, sinon il le copiera si les liens durs ne sont pas pris en charge.
- Les liens durs sont activés par défaut. [Un lien dur ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être les mêmes pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien dur échoue ou si votre configuration ne prend pas en charge les liens durs, Sonarr effectuera une copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Sonarr, Sonarr supprimera le torrent de votre client et demandera au client de supprimer les données du torrent, mais seulement si le client signale que le partage est terminé et que le torrent est arrêté (en pause à la fin).

# Comment importer votre bibliothèque multimédia organisée existante

> Notez que Sonarr ne recherche pas régulièrement les épisodes. Consultez l'entrée de la FAQ pour comprendre comment Sonarr fonctionne.
[Comment Sonarr trouve-t-il les épisodes ?](/sonarr/faq#how-does-sonarr-find-episodes)
{.is-info}

Après avoir configuré vos profils/tailles de qualité et ajouté vos indexeurs et client(s) de téléchargement, il est temps d'importer votre bibliothèque multimédia organisée existante.

À venir - Contributions bienvenues

## Importation de médias existants

Selon la qualité des noms de vos dossiers de séries existants, Sonarr essaiera de les faire correspondre à la série correcte. Vous devriez examiner attentivement cette liste avant d'importer.

L'importation de la bibliothèque ne doit être utilisée que sur une bibliothèque organisée existante et ne doit pas être utilisée sur un dossier de téléchargement ou pour importer des médias de manière ad hoc.

1. Accédez à l'importation de la bibliothèque.
1. Lisez et comprenez le texte d'aide de l'importation de la bibliothèque.
1. Sélectionnez ou ajoutez le dossier racine (bibliothèque) à partir duquel importer les séries.
1. Vérifiez la correspondance des dossiers de séries de Sonarr avec les séries TVDb.
1. Configurez vos paramètres de surveillance et votre profil de qualité selon vos besoins.
1. Cliquez sur Démarrer l'importation.

### Aucune correspondance trouvée

1. Recherchez le nom de la série ou l'ID TVDb dans la boîte de sélection des séries.
1. Consultez [cette entrée de la FAQ](/sonarr/faq#why-can-i-not-add-a-series) si la série ne peut pas être trouvée.

### Corriger le nom de dossier défectueux après l'importation

1. Supprimez la série de Sonarr.
1. Importation de la bibliothèque.
1. Assurez-vous que la série est correctement mappée.

# Ajouter une nouvelle série

[Référez-vous à la page de la bibliothèque pour plus d'informations](/sonarr/library#add-new)

# Importer des épisodes

- Utilisez "Wanted => Importation manuelle" pour importer des fichiers d'épisodes dans leurs dossiers de séries de manière ad hoc.
- Utilisez "Gérer les épisodes" sur la page d'une série pour remapper ou mapper des fichiers d'épisodes existants dans un dossier de série.