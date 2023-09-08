---
title: Recherche dans Prowlarr
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

Cette page vous montrera comment effectuer une recherche depuis Prowlarr. En général, vos recherches se feraient via l'application, mais il est également possible de les faire directement dans Prowlarr.

# Effectuer une recherche

Pour lancer une recherche, cliquez sur `Recherche` dans le menu de gauche. Vous verrez une page principalement vide avec quelques options en bas de l'écran.

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- Requête - Entrez vos termes de recherche dans le champ Requête.
  - Cliquez sur la loupe pour changer le type de recherche, les options disponibles sont :
    - Recherche basique - Requête de texte basique
    - Recherche TV - Recherche en utilisant les paramètres TV tels qu'affichés dans l'interface utilisateur, y compris les recherches basées sur les ID (TVDbId, IMDbId, TMDbID, etc.) et les recherches par saison/épisode
    - Recherche de film - Recherche en utilisant les paramètres de film tels qu'affichés dans l'interface utilisateur, y compris les recherches basées sur les ID (TMDbId, IMDbId, Genre, etc.)
    - Recherche audio - Recherche en utilisant les paramètres de musique tels qu'affichés dans l'interface utilisateur, y compris Artiste, Album, Label, Genre, etc.
    - Recherche de livre - Recherche en utilisant les paramètres de livre tels qu'affichés dans l'interface utilisateur, y compris l'auteur, le titre, etc.

> Ces formats sont généralement `{NomVariable:ValeurRecherche}` par exemple, pour une recherche TV des Simpson saison 32, l'entrée de recherche serait `{TvdbId:71663} {Season:32}`
{.is-info}

> Notez que tous les indexeurs ne prennent pas en charge tous les types de requêtes {.is-info}

- Indexeurs - Choisissez vos indexeurs dans la liste déroulante Indexeurs. Vous pouvez cocher "Usenet" ou "Torrents" pour sélectionner automatiquement tous les indexeurs de ces catégories, ou vous pouvez sélectionner des indexeurs spécifiques pour votre recherche dans l'un ou l'autre groupe.
- Catégorie - Choisissez les catégories sur lesquelles vous souhaitez effectuer votre recherche dans les indexeurs à partir de la liste déroulante. Vous pouvez sélectionner des catégories de premier niveau (TV, Films, etc.) pour sélectionner automatiquement toutes les sous-catégories, ou vous pouvez sélectionner des catégories spécifiques dans l'un des groupes.

Ensuite, cliquez sur le bouton `Recherche`. Vos résultats peuvent prendre quelques secondes pour apparaître. Une fois qu'ils sont là, vous pouvez ajouter ou supprimer des colonnes en utilisant le bouton `Options`, et vous pouvez trier et filtrer vos résultats en cliquant sur les en-têtes de colonne ou en utilisant le bouton `Filtrer`.

Vous pouvez télécharger le résultat en cliquant sur l'icône de téléchargement à droite du résultat. Cela l'enverra au client de téléchargement approprié que vous avez configuré.

Vous pouvez également récupérer plusieurs résultats à la fois en cochant les cases de sélection sur le côté gauche et en cliquant sur le bouton `Récupérer les publications`.

> Tout ce qui est téléchargé aura l'assignation de catégorie que vous avez définie dans Prowlarr. Cela peut nécessiter une importation manuelle dans votre programme d'application à partir d'un répertoire non standard ! {.is-info}

# Points d'accès de l'API

## Flux compatible RSS - Indexeur unique

- Point d'accès/paramètres compatibles avec Newznab/Torznab standard. Vous pouvez ajuster les requêtes en fonction de vos besoins selon les normes définies.

> Un point d'accès multi-indexeur agrégé ne sera pas ajouté en raison des inconvénients significatifs de cette fonctionnalité {.is-info}

### Clé API dans la requête

- `http://{hôte_prowlarr}:{port_prowlarr}/{baseurl}/{id_indexeur}/api?t=search&q={terme}&apikey={votre_clé}&cat={liste séparée par des virgules}`
  - par exemple `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={votre_clé}&cat=5000,2000`

### Clé API dans l'en-tête

> Assurez-vous de passer `X-Api-Key` avec la clé API en tant qu'en-tête {.is-info}

- `http://{hôte_prowlarr}:{port_prowlarr}/{baseurl}/{id_indexeur}/api?t=search&q={terme}&apikey={votre_clé}&cat={liste séparée par des virgules}`
  - par exemple `http://192.168.1.100:9696/{id_indexeur}/api?t=search&q=mike&cat=5000,2000`

## Flux de recherche

- `http://{hôte_prowlarr}:{port_prowlarr}/{baseurl}/api/v1/search?query={terme_encodé}&indexerIds={liste séparée par des virgules}&categories={liste séparée par des virgules}&type={type_recherche}`
  - par exemple `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - par exemple `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

Paramètres

- `query` - Chaîne de recherche encodée en URL
- `indexerIds` - liste séparée par des virgules des ID des indexeurs
  - Laissez le paramètre hors de l'URL pour tous les indexeurs
  - `-2` représente tous les torrents
  - `-1` représente tous les Usenet
  - ID des indexeurs
- `categories` - liste séparée par des virgules des catégories à utiliser
  - laissez le paramètre hors de l'URL pour toutes les catégories
- `type` - le type de recherche à effectuer
  - `search` - Requête de texte basique
  - `tvsearch` - Requête TV - Prend en charge les paramètres TV
  - `moviesearch` - Requête de film - Prend en charge les paramètres de film
  - `audiosearch` - Requête audio/musique - Prend en charge les paramètres de musique
  - `booksearch` - Requête de livre - Prend en charge les paramètres de livre