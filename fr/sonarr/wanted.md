---
title: Sonarr Wanted
description: 
published: true
date: 2021-11-29T22:12:55.806Z
tags: sonarr, needs-love, wanted
editor: markdown
dateCreated: 2021-06-10T01:40:02.329Z
---

# Recherché

La section Recherché => Manquant contient une liste des épisodes que vous avez marqués pour les surveiller et qui sont manquants sur votre disque (n'ont pas encore été téléchargés).

> Cela inclura uniquement les épisodes totalement manquants sur votre disque, pas les épisodes qui existent sur le disque mais dont le profil de coupure n'est pas respecté.
{.is-info}

- "Rechercher la sélection" - Ici, vous pouvez sélectionner certains épisodes si vous souhaitez les rechercher avec vos indexeurs.

- "Ne plus surveiller la sélection" - Ici, vous pouvez sélectionner certains épisodes et les retirer de la surveillance si vous n'êtes plus intéressé par eux.

- "Rechercher tous" - En sélectionnant cette option, une recherche sera envoyée à tous vos indexeurs pour tous les épisodes manquants actuels. Une fois que vous appuyez sur le bouton, une boîte de dialogue s'affiche avec un avertissement vous indiquant combien d'épisodes seront recherchés ; cela est particulièrement utile si vos indexeurs limitent vos appels API.

> Ce processus de recherche ne peut pas être annulé une fois qu'il a été lancé sans redémarrer Sonarr.
{.is-info}

En haut de la page se trouve `Importation manuelle`, qui vous permet d'importer arbitrairement des fichiers multimédias depuis n'importe quelle destination accessible par Sonarr pour les séries déjà présentes dans Sonarr.

- "Déplacer automatiquement" tentera de faire correspondre automatiquement les fichiers aux séries/épisodes dans Sonarr et les déplacera - sans les copier ni créer de lien physique - vers votre dossier de bibliothèque.
- "Importation interactive" vous permettra de vérifier les correspondances et d'ajuster diverses spécifications si nécessaire. Il vous permet de choisir l'option (coin inférieur gauche) `Déplacer` ou `Copier/Créer un lien physique` vos fichiers. Assurez-vous de choisir l'option correcte en fonction de vos besoins.

  > Si un répertoire contient plus de 100 fichiers, Sonarr ne recherchera pas récursivement le répertoire ni n'essaiera d'analyser et de faire correspondre les fichiers.
{.is-info}

# Coupure non respectée

La section Recherché => Coupure non respectée contient une liste des épisodes qui n'ont pas encore atteint leur coupure. La coupure est définie dans vos profils.

La coupure est l'endroit où vous indiquez essentiellement à Sonarr que la qualité du fichier vidéo est suffisamment bonne pour vous et que vous ne souhaitez plus que Sonarr continue à rechercher une meilleure qualité.

Plusieurs options sont disponibles sur cette page
![wanted-cut-off-unmet.png](/assets/sonarr/wanted-cut-off-unmet.png)

1. Rechercher la sélection - En sélectionnant des épisodes dans votre liste, vous pouvez effectuer une recherche automatique pour voir s'il existe des mises à niveau pour vos fichiers existants.
1. Ne plus surveiller la sélection - En sélectionnant certains épisodes dans votre liste, vous pouvez indiquer à Sonarr de ne plus rechercher de mises à niveau en retirant ces épisodes de la surveillance.
1. Rechercher tous - Cela peut être dangereux (selon la taille de votre liste) car vous indiquez à Sonarr de rechercher chaque fichier qui n'a pas atteint la coupure. Cela peut être utile si vous n'avez pas une liste massive.
1. Filtrer - Cela vous permettra de filtrer vos résultats. C'est utile si vous souhaitez rechercher un ensemble spécifique d'épisodes ou de séries.