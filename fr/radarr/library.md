---
title: Bibliothèque Radarr
description: 
published: true
date: 2022-11-14T15:04:06.364Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:24:18.386Z
---

# Films

## Vue de la bibliothèque

- Tout mettre à jour - Mettre à jour les métadonnées de tous les films, rafraîchir les affiches, réanalyser les dossiers de films et réanalyser les fichiers de films (si activé)
- Rafraîchir et analyser - Rafraîchir les métadonnées du film actuellement affiché et réanalyser son dossier
- Synchronisation RSS - Rafraîchir le flux RSS de vos indexeurs et voir si de nouveaux éléments ont été publiés pour être récupérés
- Rechercher tout / Rechercher filtré / Rechercher sélectionné - Rechercher tous les films ou les films sélectionnés dans la vue actuelle
- Importation manuelle (Index des films) - Importer manuellement un fichier de film pour un film que vous avez ajouté à Radarr à partir de n'importe quel dossier accessible par Radarr
  - Déplacer automatiquement - Essayer automatiquement de faire correspondre un fichier à un film dans Radarr et l'importer en le déplaçant.
  - Importation interactive - Examiner tous les fichiers dans le chemin et essayer de les faire correspondre à un film dans Radarr en permettant à l'utilisateur de vérifier les résultats. Le déplacement ou la copie/liage dur est une option sélectionnable dans le coin inférieur gauche.
- Importation manuelle (Film) - Importer manuellement un fichier de film pour un film que vous avez ajouté à Radarr à partir du dossier du film assigné
  - Déplacer automatiquement - Essayer automatiquement de faire correspondre un fichier à un film dans Radarr et l'importer en le déplaçant.
  - Importation interactive - Examiner tous les fichiers dans le chemin et essayer de les faire correspondre à un film dans Radarr en permettant à l'utilisateur de vérifier les résultats. Le déplacement ou la copie/liage dur est une option sélectionnable dans le coin inférieur gauche.
- Éditeur de films / Index des films - Basculer entre le mode Éditeur de masse et le mode Index des films (Bibliothèque)
- Options - Modifier les options d'affichage
- Vue - Basculer le type de vue
  - Tableau - Vue tabulaire (liste)
  - Affiches - Afficher les affiches (similaire à Plex)
  - Aperçu - Afficher les informations générales et l'affiche (vue détaillée)
- Trier - Trier la vue actuelle

### Filtres

- Filtre - Filtrer la vue actuelle
  - Uniquement surveillés - Titres surveillés pour les mises à jour.
  - Non surveillés - Titres NON surveillés pour les mises à jour.
  - Manquants - Dans la base de données, surveillés, mais manquants du système de fichiers.
  - Recherchés - Dans la base de données, surveillés, manquants, mais devraient être disponibles en fonction des paramètres de disponibilité
  - Coupure non atteinte - Titre sur le système de fichiers, mais toujours en surveillance pour une qualité recherchée.
  - Filtres personnalisés
    - Surveillé (booléen)
    - Considéré comme disponible (booléen)
    - Disponibilité minimale (Enum)
      - Annoncé
      - En salle
      - Sorti
    - Titre \[contient\] (Chaîne)
    - Statut de sortie (Enum)
      - À venir
      - Annoncé
      - En salle
      - Sorti
      - Supprimé
        - Supprimé de TMDb
    - Studio (Enum Studios)
    - Collection (Enum Collections)
    - Profil de qualité (Enum QualityProfiles)
    - Ajouté (DateTime statique, TimeDelta relatif)
    - Année (Int)
    - En salle (DateTime statique, TimeDelta relatif)
    - Sortie physique (DateTime statique, TimeDelta relatif)
    - Sortie numérique (DateTime statique, TimeDelta relatif)
    - Durée (Int)
    - Chemin \[contient\] (Chaîne)
    - Taille sur le disque (Int)
    - Genres \[contient\] (Enum Genres)
    - Note TMDB (Float)
    - Votes TMDB (Int)
    - Note IMDb
    - Note Tomate
    - Votes IMDb
    - Certification (Enum Rating (PG-13, R, etc))
    - Tags \[contient\] (Enum Tags)

# Ajouter un nouveau

![radarr-add-new-empty.png](/assets/radarr/radarr-add-new-empty.png)

- Si vous souhaitez ajouter un nouveau film, c'est la page sur laquelle vous voudrez le faire.
  - Vous trouverez comment faire dans notre [Guide de démarrage rapide](/radarr/quick-start-guide).
- Sous le champ de recherche, vous pouvez également trouver le bouton Importer des films existants. Si c'est votre cas, vous pouvez trouver de nombreuses informations à ce sujet également dans notre [Guide de démarrage rapide](/radarr/quick-start-guide).
- Si vous obtenez une erreur "le chemin est déjà configuré", [consultez cette entrée de FAQ](/radarr/faq#path-is-already-configured-for-an-existing-movie).

# Importation de la bibliothèque

L'importation de la bibliothèque vous permet d'importer des films organisés existants et les fichiers de chaque film via des fichiers existants dans le répertoire du chemin. Cela est particulièrement utile lorsque vous créez une nouvelle instance de Radarr et que vous souhaitez conserver vos films existants.

- L'importation de la bibliothèque permet d'ajouter et d'importer une bibliothèque de films organisée existante dans Radarr.
- L'importation de la bibliothèque ne peut pas être utilisée pour :
  - Importer des fichiers à partir d'un dossier de téléchargement
  - Ajouter ou importer un ou plusieurs fichiers qui ne sont pas correctement nommés et organisés dans leur propre dossier de film à l'intérieur de votre dossier racine ou d'un dossier que vous souhaitez ajouter en tant que dossier racine
  - Toutes les autres utilisations qui ne consistent pas à ajouter un film à Radarr et à importer le film et son fichier à partir du dossier racine (bibliothèque) qui a été entré dans l'importation de la bibliothèque
- Si vous obtenez une erreur "le chemin est déjà configuré", [consultez cette entrée de FAQ](/radarr/faq#path-is-already-configured-for-an-existing-movie).
  
> Il est nécessaire que les dossiers et les fichiers de films contiennent l'année dans leur nom pour être importés et analysés.{.is-warning}

> \* Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

> **L'utilisateur et le groupe que vous avez configurés pour exécuter Radarr doivent avoir un accès en lecture et en écriture à cet emplacement.**
{.is-info}

> Votre client de téléchargement télécharge dans un dossier de téléchargement et Radarr l'importe dans votre dossier multimédia (destination finale) que votre serveur multimédia utilise.
{.is-info}

> **Votre dossier de téléchargement et votre dossier multimédia ne peuvent pas être situés au même emplacement**
{.is-danger}

# Collections

Le wiki est développé et maintenu par la communauté.
Cette section n'a pas fait l'objet de contributions pour refléter et décrire la page des collections dans Radarr.

# Découvrir

Découvrir montre des films recommandés

- Si vous n'avez pas de liste(s), il affichera les 90 films les plus recommandés en fonction des films recommandés par TMDb pour les films de votre bibliothèque, ainsi que les 10 recommandations de vos ajouts les plus récents.

> Astuce : Vous pouvez désactiver les films recommandés par Radarr et afficher uniquement les films de vos listes dans `Options`.
{.is-info}

- Si vous avez des liste(s), il affichera les recommandations mentionnées ci-dessus ET les entrées de vos liste(s).

> Astuce : Changez le `Filtre` en `Nouveaux non exclus` pour afficher uniquement les films qui ne sont pas dans votre bibliothèque.
{.is-info}

![radarr-discover-empty.png](/assets/radarr/radarr-discover-empty.png)

- Il est probable que vos recommandations de Découverte soient rares si vous avez une nouvelle installation avec peu ou pas de films. Vous devrez ajouter du contenu à la bibliothèque pour alimenter les recommandations. Vous avez plusieurs options :
  1. Cliquez sur le bouton [Ajouter un nouveau film](/radarr/library#add-new) pour ajouter des films manuellement.
  1. Cliquez sur le bouton [Importer une bibliothèque existante](/radarr/library#library-import) pour importer une bibliothèque existante.
  1. Cliquez sur le bouton [Ajouter des listes](/radarr/settings#lists) pour ajouter une liste à Radarr. Vous trouverez des informations supplémentaires sur les listes sur la page [Plus d'informations (Pris en charge)](/radarr/faq#what-are-lists-and-what-can-they-do-for-me) de cette section.

![radarr-discover-add-new-movies.png](/assets/radarr/radarr-discover-add-new-movies.png)

- Une fois que vous avez ajouté un film par l'une des trois options énumérées ci-dessus, vous verrez différents films à découvrir.
    1. Ici, vous pouvez sélectionner les films que vous souhaitez ajouter à votre bibliothèque
    1. Ici, vous pouvez sélectionner tous les films de cette liste si vous vous sentez particulièrement fou
    1. Sélectionnez le chemin racine dans lequel vous souhaitez que ces films soient importés une fois qu'ils sont ajoutés
    1. Sélectionnez la disponibilité que vous souhaitez que le film ait avant d'être récupéré
    1. Sélectionnez les profils de qualité que vous avez déjà créés ([Plus d'informations](/radarr/settings#quality-profiles))
    1. Voulez-vous que Radarr surveille ce film pour toute amélioration de la qualité ?
    1. Souhaitez-vous que Radarr recherche automatiquement ce film après l'avoir ajouté ?
    1. Voulez-vous exclure ces films de toutes les listes qui seraient importées ? ([Plus d'informations](/radarr/settings#list-exclusion))
    1. Enfin, ajoutez le film à votre bibliothèque.