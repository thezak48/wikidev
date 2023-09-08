---
title: Bibliothèque Sonarr
description: 
published: true
date: 2022-10-28T17:18:11.116Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-06-11T23:31:01.289Z
---

# Séries

La page des séries affiche l'ensemble de votre bibliothèque et vous permet de sélectionner des séries individuelles (cependant, la recherche peut être plus efficace dans les grandes bibliothèques) et de faire des recherches pour des séries spécifiques, ainsi que de pouvoir les modifier. Elle vous permet également de filtrer vos séries.

# Filtres

Les options de filtre vous permettent de restreindre vos séries et sont extrêmement utiles. Elles peuvent être utilisées pour voir les dates de sortie, les noms, le nombre d'épisodes, le nombre de disques, et bien plus encore, y compris des filtres personnalisés, pour répondre à tous vos besoins. Ils peuvent également être utilisés dans l'éditeur de masse.

# Ajouter une nouvelle série

La fonctionnalité d'ajout de nouvelle série vous permet d'ajouter une nouvelle série à surveiller et à télécharger pour Sonarr.

- Dossier racine - Le dossier [racine/bibliothèque](/sonarr/settings#root-folders) sélectionné dans Sonarr pour que cette série l'utilise
- Surveillance - Comment souhaitez-vous que la série soit surveillée initialement ?
  - Tous les épisodes - Surveiller tous les épisodes sauf les épisodes spéciaux
  - Épisodes futurs - Surveiller les épisodes qui n'ont pas encore été diffusés
  - Épisodes manquants - Surveiller les épisodes qui n'ont pas de fichiers ou qui n'ont pas encore été diffusés
  - Épisodes existants - Surveiller les épisodes qui ont des fichiers
  - Première saison - Surveiller tous les épisodes de la première saison ; toutes les autres saisons seront ignorées
  - Dernière saison - Surveiller tous les épisodes de la dernière saison et des saisons futures
  - Aucun - Aucun épisode ne sera surveillé
- Profil de qualité - Le [profil de qualité](/sonarr/settings#quality-profiles) à utiliser pour cette série
- Type de série - Quel type de série utiliser pour cette série ; cela modifie la façon dont les recherches sont effectuées [Voir l'entrée FAQ pour plus d'informations](/sonarr/faq#whats-the-different-series-types)
- Dossier de saison - Activer ou désactiver la création et l'utilisation de dossiers de saison pour cette série
- Tags - Utilisés pour attribuer des séries à des profils de publication, des profils de retard, des indexeurs, ou simplement pour organiser vos séries
- [ ] Lancer la recherche des épisodes manquants - en fonction de vos paramètres de surveillance sélectionnés, rechercher tous les épisodes manquants et surveillés dans cette série
- [ ] Lancer la recherche des épisodes non conformes à la limite - en fonction de vos paramètres de surveillance sélectionnés et uniquement si vous avez des fichiers existants pour vos épisodes dans le dossier de la série, rechercher tous les épisodes existants et surveillés dans cette série qui ne répondent pas ou ne dépassent pas la limite de votre profil de qualité

# Importation de la bibliothèque

L'importation de la bibliothèque vous permet d'importer des séries et des fichiers d'épisodes existants et organisés dans Sonarr via des fichiers existants dans le répertoire du chemin. Cela est particulièrement utile lorsque vous créez une nouvelle instance de Sonarr et que vous souhaitez conserver vos séries existantes.

- L'importation de la bibliothèque sert à ajouter et importer une bibliothèque organisée existante de séries dans Sonarr.

- L'importation de la bibliothèque ne peut pas être utilisée pour :
  - Importer des fichiers à partir d'un dossier de téléchargement
  - Ajouter ou importer un ou plusieurs fichiers qui ne sont pas correctement nommés et organisés dans leur propre dossier de série à l'intérieur de votre dossier racine ou d'un dossier que vous souhaitez ajouter en tant que dossier racine
  - Toutes autres utilisations qui ne consistent pas à ajouter une série ou un épisode à Sonarr et à importer la série et son(s) fichier(s) à partir du dossier racine (bibliothèque) qui a été entré dans l'importation de la bibliothèque

> \* Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

> **L'utilisateur et le groupe que vous avez configurés pour exécuter Sonarr doivent avoir un accès en lecture et en écriture à cet emplacement.** {.is-info}

> Votre client de téléchargement télécharge vers un dossier de téléchargement et Sonarr l'importe vers votre dossier multimédia (destination finale) que votre serveur multimédia utilise.
{.is-info}

> **Votre dossier de téléchargement et votre dossier multimédia ne peuvent pas être situés au même emplacement**
{.is-danger}

# Éditeur de masse

L'éditeur de masse vous permet de modifier des séries en masse. Vous pouvez modifier tous les paramètres précédents que vous avez définis lors de l'ajout de la série.

# Abonnement à la saison

Cela affiche des informations sur le nombre de saisons de chaque série et sur le nombre d'épisodes manquants dans chaque saison.