---
title: Bibliothèque Readarr
description: 
published: true
date: 2021-11-30T01:41:54.243Z
tags: readarr, needs-love, library
editor: markdown
dateCreated: 2021-11-30T00:50:59.442Z
---

# Bibliothèque

Cette section permet de gérer votre bibliothèque d'[auteurs](#authors) et de [livres](#books).

# Auteurs

- Vue de la bibliothèque
  - Tout mettre à jour - Mettre à jour les métadonnées de tous les auteurs, rafraîchir les affiches, réanalyser les dossiers des auteurs et réanalyser les fichiers des livres (si activé)
  - Rafraîchir et analyser - Rafraîchir les métadonnées de l'auteur actuellement affiché et réanalyser son dossier
  - Synchronisation RSS - Rafraîchir le flux RSS de vos indexeurs et voir s'il y a quelque chose de nouveau à récupérer
  - Éditeur d'auteurs / Index des auteurs - Basculer entre le mode Éditeur de masse et le mode Index des auteurs (Bibliothèque)
  - Options - Modifier les options d'affichage
  - Vue - Basculer le type de vue
    - Tableau - Vue tabulaire (liste)
    - Affiches - Afficher les affiches (similaire à Plex)
    - Aperçu - Afficher les informations générales et l'affiche (vue détaillée)
  - Trier - Trier la vue actuelle
  - Filtrer - Filtrer la vue actuelle

# Livres

- Vue de la bibliothèque
  - Tout mettre à jour - Mettre à jour les métadonnées de tous les auteurs, rafraîchir les affiches, réanalyser les dossiers des auteurs et réanalyser les fichiers des livres (si activé)
  - Rafraîchir et analyser - Rafraîchir les métadonnées de l'auteur actuellement affiché et réanalyser son dossier
  - Synchronisation RSS - Rafraîchir le flux RSS de vos indexeurs et voir s'il y a quelque chose de nouveau à récupérer
  - Rechercher tout / Rechercher filtré / Rechercher sélectionné - Rechercher tous les livres ou les livres sélectionnés dans la vue actuelle
  - Éditeur de livres / Index des livres - Basculer entre le mode Éditeur de masse et le mode Index des livres (Bibliothèque)
  - Options - Modifier les options d'affichage
  - Vue - Basculer le type de vue
    - Tableau - Vue tabulaire (liste)
    - Affiches - Afficher les affiches (similaire à Plex)
    - Aperçu - Afficher les informations générales et l'affiche (vue détaillée)
  - Trier - Trier la vue actuelle
  - Filtrer - Filtrer la vue actuelle
  
# Ajouter un nouveau

![addnew.png](/assets/readarr/addnew.png)

- Vous pouvez ajouter de nouveaux auteurs ou des livres individuels en entrant le nom de l'auteur ou le titre du livre ici, puis en le sélectionnant dans la liste des résultats.
  - Vous trouverez comment faire dans notre [Guide de démarrage rapide](/readarr/quick-start-guide)
- Vous pouvez également ajouter des auteurs en utilisant leur identifiant GoodReads, leur ISBN ou leur ASIN, en utilisant le format indiqué.

![poe.png](/assets/readarr/poe.png)

- Cliquez sur le nom de l'auteur ou du livre pour l'ajouter à Readarr. Une boîte de dialogue s'affichera avec des options pour vous.

![addauthor.png](/assets/readarr/addauthor.png)

- Dossier racine - Sélectionnez ici le dossier racine. Ne le modifiez pas si vous utilisez Calibre Content Server.
- Surveillance - Sélectionnez l'état de surveillance de tous les livres de cet auteur.
- Profil de qualité - Sélectionnez le profil de qualité à utiliser lors de la recherche de livres pour cet auteur.
- (Livre uniquement) Profil de métadonnées - Sélectionnez le profil de métadonnées à utiliser pour ce livre.
- Étiquettes - Si vous souhaitez qu'une étiquette soit appliquée aux livres de cet auteur, saisissez-la ici.
- Lancer la recherche des livres manquants - Choisissez si vous souhaitez lancer immédiatement une recherche historique dans vos indexeurs pour tous les livres de cet auteur. Si vous ne le faites pas, seuls les livres nouvellement téléchargés seront récupérés à partir de ce moment-là.
- Ajouter {Nom de l'auteur} ou Ajouter {Nom du livre} - Cliquez sur le bouton Ajouter pour ajouter cet auteur à Readarr et commencer à récupérer les métadonnées de tous les livres de cet auteur. Ce processus peut prendre un certain temps, il est donc conseillé de ne pas ajouter trop d'auteurs trop rapidement.

> Si vous ajoutez un livre individuel et sélectionnez `Aucun`\* pour le [profil de métadonnées](/readarr/settings#metadata-profiles), seul ce livre apparaîtra sous l'auteur lorsqu'il sera ajouté. Si vous souhaitez ajouter d'autres livres de cet auteur, choisissez un profil de métadonnées approprié.
> \* **Notez que `Aucun` n'applique aucun filtre de métadonnées et vous pouvez obtenir des éditions étrangères indésirables. Pour contourner ce problème, [créez un profil de métadonnées comme indiqué dans la FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Fichiers non mappés

![unmappedfiles.png](/assets/readarr/unmappedfiles.png)

Si des livres sont répertoriés ici, cela signifie qu'ils ne sont pas reconnus par Readarr et ne sont pas répertoriés comme "existants" dans Readarr, mais ils se trouvent dans l'un des dossiers racines que vous avez définis.

Vous pouvez obtenir plus d'informations en cliquant sur l'icône *i* à droite.

Vous pouvez importer manuellement le livre en cliquant sur l'icône *personne* à droite.

Vous pouvez supprimer le fichier du livre en cliquant sur l'icône *corbeille* à droite.

Vous pouvez également cliquer sur *Ajouter les manquants* en haut pour essayer d'ajouter tous les livres à Readarr. Notez que cela peut prendre du temps si vous avez beaucoup de livres répertoriés ici.