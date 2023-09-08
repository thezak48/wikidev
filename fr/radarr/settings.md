---
title: Paramètres de Radarr
description: Description des menus de paramètres de Radarr
published: true
date: 2023-08-27T22:02:11.780Z
tags: radarr, needs-love, settings
editor: markdown
dateCreated: 2021-05-29T15:57:25.304Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Options de menu](#options-de-menu)
- [Gestion des médias](#gestion-des-médias)
  - [Suggestions de nom de la communauté](#suggestions-de-nom-de-la-communauté)
  - [Nom du film](#nom-du-film)
    - [Format standard du film](#format-standard-du-film)
    - [Nom du film](#nom-du-film-1)
    - [Identifiants du film](#identifiants-du-film)
    - [Qualité](#qualité)
    - [Informations sur les médias](#informations-sur-les-médias)
    - [Groupe de sortie](#groupe-de-sortie)
    - [Édition](#édition)
    - [Formats personnalisés (Nom)](#formats-personnalisés-nom)
    - [Original](#original)
  - [Format du dossier du film](#format-du-dossier-du-film)
    - [Nom du film](#nom-du-film-2)
    - [Identifiant du film](#identifiant-du-film)
  - [Dossiers](#dossiers)
  - [Importation](#importation)
  - [Gestion des fichiers](#gestion-des-fichiers)
  - [Autorisations](#autorisations)
  - [Dossiers racine](#dossiers-racine)
- [Profils](#profils)
  - [Profils de qualité](#profils-de-qualité)
  - [Profils de retard](#profils-de-retard)
    - [Utilisations](#utilisations)
    - [Fonctionnement des profils de retard](#fonctionnement-des-profils-de-retard)
      - [Exemples](#exemples)
        - [Exemple 1](#exemple-1)
        - [Exemple 2](#exemple-2)
        - [Exemple 3](#exemple-3)
- [Qualité](#qualité-1)
  - [Signification du tableau de qualité](#signification-du-tableau-de-qualité)
  - [Définition des qualités](#définition-des-qualités)
- [Formats personnalisés](#formats-personnalisés)
  - [Conditions de format personnalisé](#conditions-de-format-personnalisé)
    - [Modificateurs](#modificateurs)
    - [Conditions](#conditions)
    - [Paramètres de profilage et de classement](#paramètres-de-profilage-et-de-classement)
      - [Importation / Exportation de formats personnalisés](#importation-exportation-de-formats-personnalisés)
      - [Importation / Mise à jour de formats personnalisés existants](#importation-mise-à-jour-de-formats-personnalisés-existants)
    - [Collection de formats personnalisés](#collection-de-formats-personnalisés)
- [Indexeurs](#indexeurs)
  - [Indexeurs pris en charge](#indexeurs-pris-en-charge)
    - [Paramètres de l'indexeur](#paramètres-de-lindexeur)
    - [Configuration de l'indexeur Usenet](#configuration-de-lindexeur-usenet)
    - [Configuration du tracker torrent](#configuration-du-tracker-torrent)
      - [Indicateurs de l'indexeur](#indicateurs-de-lindexeur)
  - [Options](#options)
  - [Restrictions](#restrictions)
- [Clients de téléchargement](#clients-de-téléchargement)
  - [Aperçu](#aperçu)
  - [Processus du client de téléchargement](#processus-du-client-de-téléchargement)
    - [Processus Usenet](#processus-usenet)
    - [Processus Torrent](#processus-torrent)
  - [Clients de téléchargement](#clients-de-téléchargement-1)
    - [Clients de téléchargement pris en charge](#clients-de-téléchargement-pris-en-charge)
    - [Paramètres du client Usenet](#paramètres-du-client-usenet)
    - [Paramètres du client Torrent](#paramètres-du-client-torrent)
    - [Compatibilité de suppression de téléchargement du client Torrent](#compatibilité-de-suppression-de-téléchargement-du-client-torrent)
  - [Gestion des téléchargements terminés](#gestion-des-téléchargements-terminés)
    - [Supprimer les téléchargements terminés](#supprimer-les-téléchargements-terminés)
    - [Gestion des téléchargements échoués](#gestion-des-téléchargements-échoués)
  - [Mappings de chemin distant](#mappings-de-chemin-distant)
- [Listes d'importation](#listes-dimportation)
  - [Listes](#listes)
  - [Options de liste](#options-de-liste)
  - [Exclusions de liste](#exclusions-de-liste)
- [Connecter](#connecter)
  - [Connexions](#connexions)
  - [Déclencheurs de connexion](#déclencheurs-de-connexion)
- [Métadonnées](#métadonnées)
  - [Options](#options-1)
  - [Consommateurs de métadonnées](#consommateurs-de-métadonnées)
- [Tags](#tags)
- [Général](#général)
  - [Hôte](#hôte)
  - [Sécurité](#sécurité)
  - [Proxy](#proxy)
  - [Journalisation](#journalisation)
  - [Analytique](#analytique)
  - [Mises à jour](#mises-à-jour)
  - [Sauvegardes](#sauvegardes)
- [Interface utilisateur](#interface-utilisateur)
  - [Calendrier](#calendrier)
  - [Films](#films)
  - [Dates](#dates)
  - [Style](#style)
  - [Langue](#langue)

Cette page présente tous les paramètres disponibles dans Radarr et leur fonctionnement. Elle ne vise pas à être un guide complet sur la configuration de Radarr. Si vous souhaitez cela, veuillez consulter la page [Guide de démarrage rapide](/radarr/quick-start-guide) à la place.

# Options de menu

Pour accéder à la page des paramètres, choisissez Paramètres dans la barre latérale. Les options de sous-menu suivantes seront disponibles :

![settings_1_menu.png](/assets/radarr/settings_1_menu.png)

De plus, notez que pour chaque page de paramètres individuelle, il y a des options en haut du menu :

![settings_2_topmenu.png](/assets/radarr/settings_2_topmenu.png)

- Masquer/Afficher les options avancées est important pour tous les éléments marqués ci-dessous comme `(Option avancée)`, sinon ils n'apparaîtront pas. Ces éléments de menu sont affichés en orange dans les captures d'écran.

- Vous devez enregistrer vos modifications avant de quitter l'écran. Pour cela, cliquez sur l'icône du disque. Si vous n'avez apporté aucune modification, il affichera "Aucune modification" et sera grisé, comme indiqué ci-dessus.

# Gestion des médias

> Certains de ces paramètres ne sont visibles que via `Afficher les paramètres avancés` qui se trouve dans la barre supérieure sous la barre de recherche{.is-info}

## Suggestions de nom de la communauté

> Voici quelques suggestions de nom de la communauté provenant des [Guides de TRaSH](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/) {.is-info}

### Fichiers de film

- Radarr v4.2.2.6489 ou version ultérieure

`{Movie CleanTitle} {(Année de sortie)} {imdb-{ImdbId}} {edition-{Edition Tags}} {[Formats personnalisés]}{[Qualité complète]}{[MediaInfo 3D]}{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}]{MediaInfo AudioLanguages}[{Mediainfo VideoCodec}]{-Groupe de sortie}`

- Anciennes versions de Radarr

`{Movie CleanTitle} {(Année de sortie)} {Edition Tags} [imdb-{ImdbId}]{[Formats personnalisés]}{[Qualité complète]}{[MediaInfo 3D]}{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}][{Mediainfo VideoCodec}]{-Groupe de sortie}`

### Dossiers de film

`{Movie CleanTitle} ({Année de sortie})`

## Nom du film

- Renommer les films - Si décoché, Radarr utilisera le nom existant si le renommage est désactivé
  - Si décoché :
    - Importation du client de téléchargement
      - Le titre de sortie du client de téléchargement est utilisé
    - Importation manuelle (ad hoc) : Nom de fichier d'origine
- Remplacer les caractères illégaux - Si décoché, Radarr les supprimera à la place.

  - Les caractères sont : `:` `\` `/` `>` `<` `?` `*` `|` `"`
- Remplacement des deux-points (`:`) - Ce paramètre indique comment Radarr gère les deux-points dans le nom du fichier du film. Il est disponible uniquement lorsque la suppression des caractères illégaux est activée.
  - Supprimer - Auto-explicatif
    - Exemple : Film,Le.mkv => FilmLe.mkv
  - Remplacer par un tiret - Supprime les deux-points et ajoute un tiret à la place
    - Exemple : Film,Le.mkv => Film-Le.mkv
  - Remplacer par un espace - Supprime les deux-points et ajoute un espace à la place
    - Exemple : Film,Le.mkv => Film Le.mkv
  - Remplacer par un espace tiret espace - Auto-explicatif
    - Exemple : Film,Le.mkv => Film - Le.mkv

### Format standard du film

- Ici, vous sélectionnerez la convention de nommage de vos films

- Boîte déroulante (coin supérieur droit)
  - Boîte de gauche - Gestion des espaces
    Espace ( ) - Utiliser des espaces dans le nom (par défaut)
    Point (.) - Utiliser des points à la place des espaces dans le nom
    Souligné (_) - Utiliser des tirets bas à la place des espaces dans le nom
    Tiret (-) - Utiliser des tirets à la place des espaces dans le nom
  - Boîte de droite - Gestion de la casse
    Cas par défaut - Mettre le titre en majuscules et minuscules (~camel-case) (par défaut)
    Majuscules - Mettre le titre entièrement en majuscules
    Minuscules - Mettre le titre entièrement en minuscules

### Nom du film

- `{Movie Title}` = Le titre du film !
- `{Movie Title:DE}` = Titre du fichier
- `{Movie CleanTitle}` = Le titre du film !
- `{Movie TitleThe}` = Le titre du film, The
- `{Movie OriginalTitle}` = Τίτλος ταινίας
- `{Movie CleanOriginalTitle}` = Τίτλος ταινίας
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = La collection de films
- `{Movie Certification}` = R
- `{Release Year}` = 2009

`CleanTitle` [fait ce qui suit](https://github.com/Radarr/Radarr/blob/5948f564827eabb7afc1e89bf4a5987e3c71dc74/src/NzbDrone.Core/Organizer/FileNameBuilder.cs#L207) :

- Remplace `&` par `and`
- Remplace `/` et `\` par ` `
- Supprime `,`,`<`,`>`,`/`,`\`,`;`,`:`,`'`,`|`, `~`,`!`,`?`,`@`,`$`,`%`,`^`,`*`,`-`,`_`,`=` selon l'expression régulière suivante :

```regex
(?<=\s)(,|<|>|\/|\\|;|:|'|""|\||`|~|!|\?|@|$|%|^|\*|-|_|=){1}(?=\s)|('|:|\?|,)(?=(?:(?:s|m)\s)|\s|$)|(\(|\)|\[|\]|\{|\})
```

### Identifiants du film

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

> Les balises Imdb utilisées dans le format de nommage Plex seront masquées conditionnellement lorsque la valeur est vide `{imdb-{ImdbId}}` {.is-info}

### Qualité

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Informations sur les médias

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguages}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`, `AudioLanguages` et `SubtitleLanguages` ne prennent pas en charge actuellement un suffixe `:EN+DE` autorisé dans Sonarr pour filtrer les langues incluses dans le nom de fichier. Il existe un [problème](https://github.com/Radarr/Radarr/issues/4710) ouvert à ce sujet.
~~`MediaInfo Full`, `AudioLanguages` et `SubtitleLanguages` prennent en charge un suffixe `:EN+DE` vous permettant de filtrer les langues incluses dans le nom de fichier. Utilisez `-DE` pour exclure des langues spécifiques. L'ajout de <kb>+</kb> (par exemple : `:EN+`) affichera `[EN]`,`[EN+--]` ou `[--]` en fonction des langues exclues. Par exemple - `{MediaInfo Full:EN+DE}`.~~
{.is-info}

> `MediaInfo VideoDynamicRangeType` donnera les valeurs possibles suivantes : DV, DV HDR10, DV HLG, DV SDR, HDR10, HDR10Plus, HLG et PQ.
{.is-info}

### Groupe de sortie

- `{Release Group}` = Rls Grp

### Édition

- `{Edition Tags}` = IMAX

> À partir de la version 4.2.2.6489, les balises d'édition utilisées dans Radarr suivant le format de nommage de Plex `{edition-{Edition Tags}}` seront masquées conditionnellement comme le fait `{-Group}` lorsque la valeur des balises d'édition est vide
{.is-info}

### Formats personnalisés (Nom)

- `{Formats personnalisés}` = Son surround x264

> Les formats personnalisés seront le nom littéral du format personnalisé et nécessitent que le format personnalisé soit activé pour être inclus dans le renommage {.is-info}

### Original

- `{Original Title}` = Movie.Title.HDTV.x264-EVOLVE
- `{Original Filename}` = Movie.title.hdtv.x264-EVOLVE

> `Original Title` est le nom de sortie et il est recommandé de l'utiliser.
{.is-info}

>`Original Filename` n'est pas recommandé. Il s'agit du nom de fichier d'origine littéral et il peut être obscurci `t1i0p3s7i8yuti`.{.is-warning}

## Format du dossier du film

Ici, vous définirez la convention de nommage du dossier contenant les dossiers de saison ou les fichiers de film. Cliquez sur le `?` pour afficher la boîte de dialogue `Tokens de nom de dossier`.

### Nom du film

- `{Movie Title}` = Nom du film !
- `{Movie Title:DE}` = FileTitle
- `{Movie CleanTitle}` = Titre du film
- `{Movie TitleThe}` = Titre du film, The
- `{Movie OriginalTitle}` = Τίτλος ταινίας
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = La collection de films
- `{Movie Certification}` = R
- `{Release Year}` = 2009

### Identifiant du film

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

## Dossiers

- Créer des dossiers médias vides - Crée les dossiers de films manquants lors de l'analyse du disque
- Supprimer les dossiers vides - Supprime les dossiers de films vides lors de l'analyse du disque et lorsque les fichiers de films sont supprimés

## Importation

- Ignorer la vérification de l'espace libre - Utiliser lorsque Radarr ne parvient pas à détecter l'espace libre à partir du dossier racine de vos films
- Espace libre minimum - Activer cette option empêchera l'importation si cela laisserait moins de cet espace disque disponible
- Utiliser des liens durs au lieu de la copie - Utiliser des liens durs lors de la tentative de copie de fichiers à partir de torrents qui sont encore en cours de partage

  - Pour plus d'informations à ce sujet, cliquez [ici](https://trash-guides.info/hardlinks)

> Rarement - mais possible -, des verrous de fichiers peuvent empêcher le renommage de fichiers qui sont en cours de partage. Vous pouvez désactiver temporairement le partage et utiliser la fonction de renommage de Radarr comme solution de contournement.
{.is-warning}

- Importer des fichiers supplémentaires - Importer les fichiers supplémentaires correspondants (sous-titres, nfo, etc.) après l'importation d'un fichier

## Gestion des fichiers

- Ne plus surveiller les films supprimés - Les films supprimés du disque sont automatiquement désactivés dans Radarr.
- Télécharger les versions correctes et les repacks - Indique si vous souhaitez ou non mettre à niveau automatiquement vers les versions correctes/repacks. Utilisez `Ne pas préférer` pour trier en fonction du score de mots préférés plutôt que des versions correctes/repacks.

  - Préférer et mettre à niveau - Classez les repacks et les versions correctes plus haut que les versions non-repacks et non-correctes. Considérez les nouveaux repacks et les nouvelles versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas mettre à niveau automatiquement - Classez les repacks et les versions correctes plus haut que les versions non-repacks et non-correctes. Ne considérez pas les nouveaux repacks et les nouvelles versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas préférer - Cela ignore les repacks et les versions correctes. Vous devrez gérer les préférences pour ceux-ci avec [Formats personnalisés](#formats-personnalisés).

> \* `CORRECT` - signifie qu'il y avait un problème avec la version précédente. Les téléchargements marqués comme CORRECT indiquent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui n'a pas publié l'original.
> \* `REPACK` - signifie qu'il y avait un problème avec la version précédente et qu'il a été corrigé par le groupe original. Les téléchargements marqués comme REPACK indiquent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui a publié l'original.
{.is-info}

> [Utilisez des formats personnalisés pour les mises à niveau automatiques vers les versions correctes/repacks](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)
{.is-info}

- Analyser les fichiers vidéo - Extraire les informations du fichier telles que la résolution, la durée et les informations sur le codec. Cela nécessite que Radarr lise des parties du fichier, ce qui peut entraîner une activité disque ou réseau élevée lors des analyses.
- Analyser le dossier des films après actualisation
  - Toujours - Cela analysera les dossiers de films en fonction de la planification des tâches. C'est recommandé dans la plupart des cas, y compris si vous utilisez Bazarr.
  - Après actualisation manuelle - Vous devrez analyser manuellement le disque. C'est recommandé pour les utilisateurs de stockage cloud.
  - Jamais - Comme son nom l'indique, ne jamais analyser les dossiers de films. Ce n'est pas recommandé.
- Modifier la date du fichier - Modifier la date du fichier lors de l'importation/analyse
  - Aucune - Radarr ne modifiera pas la date affichée dans votre explorateur de fichiers.
  - Date de sortie en salle - La date de sortie du film en salle.
  - Date de sortie physique - La date de sortie du film sur disque (physique) ou sur le web.
- Corbeille de recyclage - Les fichiers de films seront placés ici lorsqu'ils sont supprimés au lieu d'être supprimés définitivement.
- Nettoyage de la corbeille de recyclage - C'est la durée pendant laquelle un fichier donné peut être avant d'être supprimé définitivement.

> Les fichiers dans la corbeille de recyclage plus anciens que le nombre de jours sélectionné seront automatiquement nettoyés. {.is-warning}

## Autorisations

- Définir les autorisations - Doit-on exécuter `chmod` lorsque les fichiers sont importés/renommés ?
  - Autorisations du dossier - Octal, appliqué lors de l'importation/du renommage des dossiers et fichiers multimédias (sans bits d'exécution)

> La liste déroulante propose une liste prédéfinie d'autorisations très couramment utilisées. Cependant, vous pouvez entrer manuellement un octal de dossier si vous le souhaitez. {.is-info}

> Cela ne fonctionne que si l'utilisateur exécutant `Radarr` est le propriétaire du fichier. Il est préférable de s'assurer que le client de téléchargement définit correctement les autorisations. {.is-warning}

- chown Groupe - Nom du groupe ou GID. Utilisez GID pour les systèmes de fichiers distants.

> Cela ne fonctionne que si l'utilisateur exécutant `Radarr` est le propriétaire du fichier. Il est préférable de s'assurer que le client de téléchargement définit correctement les autorisations. {.is-warning}

## Dossiers racine

- Chemin - Cela montre le chemin vers votre bibliothèque multimédia.
- Espace libre - C'est l'espace libre rapporté à Radarr par le système.
- Dossiers non mappés - Ce sont des dossiers qui ne sont pas associés à un film.

> Le `X` à la fin supprimera ce chemin racine. {.is-info}

- Ajouter un dossier racine - Cela vous permet de sélectionner un chemin racine pour placer les nouveaux téléchargements importés dans ce dossier ou permettre à Radarr de scanner les médias existants.

> Utilisateurs non Windows :
> \* Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

# Profils

## Profils de qualité

- Définissez les profils pour la qualité des films que vous souhaitez télécharger.

> Lorsque vous sélectionnez un profil existant ou ajoutez un profil supplémentaire, une nouvelle fenêtre apparaîtra. {.is-info}

> Remarque : La qualité qui a une case bleue est la qualité à laquelle tous les médias avec ce profil continueront d'être mis à niveau. {.is-info}

- Icône Plus (<kb>+</kb>) - Créez un nouveau profil de qualité.

- Nom - Sélectionnez un nom **UNIQUE** pour le profil de qualité que vous créez.
- Mises à niveau autorisées - Lorsque cette option est cochée et que vous demandez à Radarr de télécharger un `WEB 1080p` car c'est la première version d'un film spécifique, si quelqu'un peut ensuite télécharger un `Bluray-1080p`, Radarr mettra automatiquement à niveau vers une meilleure qualité ***si*** `Mise à niveau jusqu'à` a cette qualité sélectionnée.
- Mise à niveau jusqu'à - Une fois cette qualité atteinte, Radarr ne téléchargera plus de films.

> Remarque : Cela s'applique uniquement si vous avez `Bluray-1080p` supérieur à `WEB 1080p` dans la section `Qualités`. {.is-warning}

- Qualités - Les qualités les plus élevées dans la liste sont les plus préférées, même si elles ne sont pas cochées. Les qualités du même groupe sont équivalentes. Seules les qualités cochées sont souhaitées.
  - Modifier les groupes - Certaines qualités sont regroupées pour réduire la taille de la liste, ainsi que les regroupements de versions similaires. Un exemple typique est `WebDL` et `WebRip`, car ils sont très similaires et ont généralement des débits similaires. Lorsque vous modifiez les groupes, vous pouvez modifier la préférence au sein de chaque groupe. [Voir le guide de TRaSH sur la fusion des qualités](https://trash-guides.info/merge-quality)

  - [Voir les qualités](#qualités-définies)

> Par défaut, les qualités sont définies de la plus basse (en bas) à la plus élevée (en haut). {.is-info}

- Langue - Sélectionnez votre langue préférée.

- Format personnalisé - Radarr attribue un score à chaque version en utilisant la somme des scores correspondant aux formats personnalisés. Si une nouvelle version améliore le score, à la même qualité ou meilleure, Radarr la téléchargera.
Voir [Formats personnalisés](#formats-personnalisés) pour plus de détails.

## Profils de délai

- Les profils de délai vous permettent de réduire le nombre de versions téléchargées pour un film en ajoutant un délai pendant que Radarr continue de rechercher des versions correspondant mieux à vos préférences.
- Protocole préféré - Il s'agit soit de `Usenet`, soit de `Torrent`, en fonction du protocole de téléchargement que vous préférez.
- Délai Usenet - Défini par le nombre de minutes que vous souhaitez attendre avant le début du téléchargement.
- Délai Torrent - Défini par le nombre de minutes que vous souhaitez attendre avant le début du téléchargement.
- Contourner si meilleure qualité - Contourner le délai lorsque la version a le profil de qualité activé le plus élevé avec le protocole préféré.
- Tags - En attribuant un tag à ce profil de délai, vous pourrez appliquer ces règles à un film donné.
- Icône Clé à molette - Cela vous permet de modifier le profil de délai.
- Icône Plus (<kb>+</kb>) - Créez un nouveau profil de délai.

### Utilisations

Certains médias recevront une demi-douzaine de versions différentes de qualité variable dans les heures qui suivent leur sortie, et sans profils de délai, Radarr pourrait essayer de toutes les télécharger. Avec les profils de délai, Radarr peut être configuré pour ignorer les premières heures de versions.

Les profils de délai sont également utiles si vous souhaitez privilégier un protocole (Usenet ou BitTorrent) par rapport à l'autre. (Voir exemple 3)

### Fonctionnement des profils de délai

Le chronomètre démarre dès que Radarr détecte qu'un film dispose d'une version disponible. Cette version apparaîtra dans votre file d'attente avec une icône d'horloge pour indiquer qu'elle est soumise à un délai.

> L'horloge démarre à partir de l'heure de téléchargement des versions et non à partir du moment où Radarr les détecte. {.is-info}

Pendant la période de délai, toutes les nouvelles versions disponibles seront notées par Radarr. Lorsque le délai expire, Radarr téléchargera la seule version qui correspond le mieux à vos préférences de qualité.

La période du chronomètre peut être différente pour Usenet et les torrents. Chaque profil peut être associé à un ou plusieurs tags pour vous permettre de personnaliser les émissions qui ont ces profils. Un profil de délai sans tag est considéré comme le profil par défaut et s'applique à toutes les émissions qui n'ont pas de tag spécifique.

> Les profils de délai commencent à partir de l'heure à laquelle l'indexeur signale que la version a été téléchargée. Cela signifie que tout contenu plus ancien que le nombre de minutes que vous avez défini n'est pas impacté de quelque manière que ce soit par votre profil de délai et sera téléchargé immédiatement. De plus, **toutes les recherches manuelles** de contenu (recherches non basées sur les flux RSS) ignoreront les paramètres du profil de délai. {.is-warning}

#### Exemples

- Pour chaque exemple, supposons que l'utilisateur a le profil de qualité suivant actif : WebDL-720p et au-dessus sont autorisés, WebDL-1080p est la limite de qualité, et BluRay1080p est la qualité la mieux classée.

##### Exemple 1

- Dans cet exemple simple, le profil est défini avec un délai de 120 minutes (deux heures) pour Usenet et Torrent.

- À 23h00, la première version d'un film est détectée par Radarr et elle a été téléchargée à 22h50, le chronomètre de 120 minutes commence. À 00h50, Radarr évaluera toutes les versions trouvées au cours des deux dernières heures et téléchargera la meilleure, qui est WebDL 720p.

- À 03h00, une autre version est trouvée, qui est WebDL 720p et a été ajoutée à votre indexeur à 02h46. Un autre chronomètre de 120 minutes commence. À 04h46, la meilleure version disponible est téléchargée. Comme la limite de qualité est maintenant atteinte, le film ne peut plus être mis à niveau et Radarr cessera de rechercher de nouvelles versions.

- À tout moment, si une version WebDL 1080p est trouvée, elle sera téléchargée immédiatement car c'est la qualité la mieux classée. Si un chronomètre de délai est actuellement actif, il sera annulé.

##### Exemple 2

- Cet exemple a des chronomètres différents pour Usenet et les torrents. Supposons un chronomètre de 120 minutes pour Usenet et un chronomètre de 180 minutes pour BitTorrent.

- À 23h00, la première version d'un film est détectée par Radarr et les deux chronomètres commencent. La version a été ajoutée à l'indexeur à 22h15. À 00h15, Radarr évaluera toutes les versions et, s'il y a des versions Usenet acceptables, la meilleure sera téléchargée et les deux chronomètres prendront fin. Sinon, Radarr attendra jusqu'à 00h15 et téléchargera la meilleure version, quelle que soit sa source.

##### Exemple 3

- Une utilisation courante des profils de délai est de privilégier un protocole par rapport à un autre. Par exemple, vous ne voulez télécharger une version BitTorrent que si rien n'a été téléchargé sur Usenet après un certain laps de temps.

- Vous pourriez définir un chronomètre de 60 minutes pour BitTorrent et un chronomètre de 0 minute pour Usenet.

- Si la première version détectée provient d'Usenet, Radarr la téléchargera immédiatement.

- Si la première version provient de BitTorrent, Radarr définira un chronomètre de 60 minutes. Si une version Usenet admissible est détectée pendant ce délai, la version BitTorrent sera ignorée et la version Usenet sera téléchargée.

## Profils de versions

- Ici, vous pourrez définir des restrictions globales en fonction de plusieurs paramètres.
- Cliquez sur l'icône <kb>+</kb> et une nouvelle fenêtre s'ouvrira.
- Doit contenir - Dans ce champ, vous pouvez indiquer à Radarr que si une version ne contient pas une certaine chaîne de caractères, Radarr ne la téléchargera pas. Cela est insensible à la casse par défaut et les expressions régulières peuvent être utilisées.
- Ne doit pas contenir - Dans ce champ, vous pouvez indiquer à Radarr que si une version contient une certaine chaîne de caractères, Radarr ne la téléchargera pas. Cela est insensible à la casse par défaut et les expressions régulières peuvent être utilisées.
- Tags - Ici, vous pouvez appliquer ces paramètres aux films ayant au moins un des [tags](#tags) donnés.

# Qualité

## Signification de la table des qualités

- Qualité - Le nom de qualité de la scène (codé en dur)
- Titre - Le nom de la qualité dans l'interface utilisateur (configurable)
- Mégaoctets par minute - Auto-explicatif
- Limite de taille - Auto-explicatif
- Min - Le nombre minimum de mégaoctets par minute (Mo/min) qu'une qualité peut avoir.
- Préféré - Le nombre préféré de mégaoctets par minute (Mo/min) qu'une qualité peut avoir.
- Max - Le nombre maximum de mégaoctets par minute (Mo/min) qu'une qualité peut avoir.

## Qualités définies

- Inconnu - Auto-explicatif
- SDTV - Ripostes post-air à partir d'une source analogique (généralement la télévision par câble ou la télévision standard). La qualité de l'image est généralement bonne (pour la résolution) et elles sont généralement encodées en DivX/XviD ou MP4.
- WEBDL-480p - WEB-DL (P2P) fait référence à un fichier extrait sans perte à partir d'un service de streaming, tel que Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., ou téléchargé via un site de distribution en ligne tel que iTunes. La qualité est assez bonne, car elles ne sont pas réencodées. Les flux vidéo (H.264 ou H.265) et audio (AC3/AAC) sont généralement extraits d'iTunes ou d'Amazon Video et remuxés dans un conteneur MKV sans sacrifier la qualité. Un avantage de ces sorties est que, comme les BD/DVDRips, elles n'ont généralement pas de logos de réseau à l'écran. Elles sont presque aussi bonnes qu'une source Blu-ray, mais peuvent souffrir d'un décalage audio ou d'artefacts visuels dus au débit binaire adaptatif des services de streaming. Si la connexion Internet d'un ripper chute à un point où le débit binaire baisse, le débit binaire source peut changer dynamiquement, entraînant des variations de qualité d'image. La plupart des sorties qui souffrent d'une quantité extrême d'artefacts visuels sont NUKED et un PROPER est généralement publié pour corriger les variations sauvages du débit binaire adaptatif. Cela sera en qualité 480p (SD).
- WEBRip-480p - Dans un WEB-Rip (P2P), le fichier est souvent extrait à l'aide des protocoles HLS ou RTMP/E et remuxé à partir d'un conteneur TS, MP4 ou FLV en MKV. Cela sera en qualité 480p (SD).
- DVD - Une ré-encodage du DVD9 final sorti. Si possible, cela est publié avant la vente au détail. La qualité devrait être excellente (pour la résolution). Les DVDrips sont généralement publiés en DivX/XviD ou MP4.
- Bluray-480p - Un ré-encodage du Blu-ray final sorti, réduit à une résolution de 480p (720x480 @ 16:9, tout autre rapport d'aspect peut être une résolution différente). Si possible, cela est publié avant la vente au détail. La qualité devrait être excellente pour la résolution. Les débits binaires peuvent varier, mais ils sont généralement encodés en DivX, XviD ou AVC et offrent le compromis d'une légère réduction de qualité perçue par rapport à la source d'origine tout en réduisant considérablement la taille du fichier. Ils sont généralement au format MKV ou MP4, mais il existe également des fichiers DivX/XviD au format AVI.
- HDTV-720p - Un ré-encodage du Blu-ray final sorti, mais diffusé sur le câble HD ou par satellite (1280x720 @ 16:9, tout autre rapport d'aspect peut être une résolution différente). Il peut être modifié en fonction de la durée d'exécution ou du contenu en fonction du réseau d'où il provient. Cela est généralement publié plusieurs mois après une sortie en vente au détail, mais parfois des versions agrandies d'un film en définition standard sont diffusées sur des chaînes câblées telles que STARZ ou HBO, et elles sont les seules copies HD de ce film spécifique disponibles. Ils sont généralement au format MKV ou MP4.
- HDTV-1080p - Un ré-encodage du Blu-ray final sorti, mais diffusé sur le câble HD ou par satellite (1920x1080 @ 16:9, tout autre rapport d'aspect peut être une résolution différente). Il peut être modifié en fonction de la durée d'exécution ou du contenu en fonction du réseau d'où il provient. Cela est généralement publié plusieurs mois après une sortie en vente au détail, mais parfois des versions agrandies d'un film en définition standard sont diffusées sur des chaînes câblées telles que STARZ ou HBO, et elles sont les seules copies HD de ce film spécifique disponibles. Ils sont généralement au format MKV ou MP4.
- WEBRip-720p - Dans un WEB-Rip (P2P), le fichier est souvent extrait à l'aide des protocoles HLS ou RTMP/E et remuxé à partir d'un conteneur TS, MP4 ou FLV en MKV. Cela sera en qualité 720p.
- Bluray-720p - Un ré-encodage du Blu-ray final sorti, réduit à une résolution de 720p (1280x720 @ 16:9, tout autre rapport d'aspect peut être une résolution différente). Si possible, cela est publié avant la vente au détail. La qualité devrait être excellente pour la résolution. Les débits binaires peuvent varier, mais ils sont généralement encodés en AVC ou HEVC et offrent le compromis d'une légère réduction de qualité perçue par rapport à la source d'origine tout en réduisant considérablement la taille du fichier. Ils sont généralement au format MKV ou MP4.
- WEBDL-1080p - WEB-DL (P2P) fait référence à un fichier extrait sans perte à partir d'un service de streaming, tel que Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., ou téléchargé via un site de distribution en ligne tel que iTunes. La qualité est assez bonne, car elles ne sont pas réencodées. Les flux vidéo (H.264 ou H.265) et audio (AC3/AAC) sont généralement extraits d'iTunes ou d'Amazon Video et remuxés dans un conteneur MKV sans sacrifier la qualité. Un avantage de ces sorties est que, comme les BD/DVDRips, elles n'ont généralement pas de logos de réseau à l'écran. Elles sont presque aussi bonnes qu'une source Blu-ray, mais peuvent souffrir d'un décalage audio ou d'artefacts visuels dus au débit binaire adaptatif des services de streaming. Si la connexion Internet d'un ripper chute à un point où le débit binaire baisse, le débit binaire source peut changer dynamiquement, entraînant des variations de qualité d'image. La plupart des sorties qui souffrent d'une quantité extrême d'artefacts visuels sont NUKED et un PROPER est généralement publié pour corriger les variations sauvages du débit binaire adaptatif. Cela sera en qualité 1080p.
- WEBRip-1080p - Dans un WEB-Rip (P2P), le fichier est souvent extrait à l'aide des protocoles HLS ou RTMP/E et remuxé à partir d'un conteneur TS, MP4 ou FLV en MKV. Cela sera en qualité 1080p.
- Bluray-1080p - Un ré-encodage du Blu-ray final sorti, à sa résolution native de 1080p (1920x1080 @ 16:9, tout autre rapport d'aspect peut être une résolution différente). Si possible, cela est publié avant la vente au détail. La qualité devrait être excellente et la même résolution que la source. Les débits binaires peuvent varier, mais ils sont généralement encodés en AVC ou HEVC et offrent le compromis d'une légère réduction de qualité perçue par rapport à la source d'origine tout en réduisant légèrement la taille du fichier. Ils sont généralement au format MKV ou MP4.
- Remux-1080p - Un remux est une copie d'un disque Blu-ray ou HD DVD dans un autre format de conteneur ou simplement la suppression des menus et du matériel bonus du disque tout en conservant les contenus de ses flux audio et vidéo intacts (en conservant également les codecs actuels), garantissant la qualité exacte du film en 1:1 par rapport au disque d'origine. Cela est en qualité 1080p.
- HDTV-2160p - TVRip est une source de capture à partir d'une carte de capture. HDTV signifie source capturée à partir de la télévision HD. Avec une source HDTV, la qualité peut parfois même dépasser celle du DVD. Les films dans ce format commencent à gagner en popularité. Certaines publicités et bannières commerciales peuvent être visibles sur certaines sorties pendant la lecture. Cela est en qualité 2160p (4K).
- WEBDL-2160p - WEB-DL (P2P) fait référence à un fichier extrait sans perte à partir d'un service de streaming, tel que Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, etc., ou téléchargé via un site de distribution en ligne tel que iTunes. La qualité est assez bonne, car elles ne sont pas réencodées. Les flux vidéo (H.264 ou H.265) et audio (AC3/AAC) sont généralement extraits d'iTunes ou d'Amazon Video et remuxés dans un conteneur MKV sans sacrifier la qualité. Un avantage de ces sorties est que, comme les BD/DVDRips, elles n'ont généralement pas de logos de réseau à l'écran. Elles sont presque aussi bonnes qu'une source Blu-ray, mais peuvent souffrir d'un décalage audio ou d'artefacts visuels dus au débit binaire adaptatif des services de streaming. Si la connexion Internet d'un ripper chute à un point où le débit binaire baisse, le débit binaire source peut changer dynamiquement, entraînant des variations de qualité d'image. Cela sera en qualité 2160p (4K).
- WEBRip-2160p - Dans un WEB-Rip (P2P), le fichier est souvent extrait à l'aide des protocoles HLS ou RTMP/E et remuxé à partir d'un conteneur TS, MP4 ou FLV en MKV. Cela sera en qualité 2160p (4K).
- Bluray-2160p - Un ré-encodage du Blu-ray final sorti, à sa résolution native de 2160p (3840x2160 @ 16:9, tout autre rapport d'aspect peut être une résolution différente). Les versions 4K des films sont généralement encodées en codec HEVC et peuvent être soit en reproduction des couleurs 8 bits ou 10 bits, soit à partir d'une source HDR. Ils réduisent légèrement la taille du fichier. Ils sont généralement au format MKV ou MP4.
- Remux-2160p - Un remux est une copie d'un disque Blu-ray ou HD DVD dans un autre format de conteneur ou simplement la suppression des menus et du matériel bonus du disque tout en conservant les contenus de ses flux audio et vidéo intacts (en conservant également les codecs actuels), garantissant la qualité exacte du film en 1:1 par rapport au disque d'origine. Cela est en qualité 2160p (4K).

# Formats personnalisés

{#custom-formats-2}

- Assurez-vous d'obtenir la bonne version à chaque fois ! Les formats personnalisés permettent un contrôle précis de la priorisation et de la sélection des versions. Aussi simple qu'un seul mot préféré ou aussi complexe que vous le souhaitez avec plusieurs critères et expressions régulières.
- Les formats personnalisés sont calculés à la volée au lieu d'être stockés dans la base de données, ils se mettent donc à jour dès que vous modifiez les définitions.
- Les formats personnalisés sont utilisés dans vos profils de qualité pour déterminer le score de chaque format personnalisé. Dans chaque profil de qualité, vous pouvez définir un score minimum pour un format personnalisé afin de le télécharger et un score d'amélioration jusqu'à ce score également.
- Il est fortement recommandé d'ajouter les formats personnalisés suivants à partir des [Guides de TRaSH](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) pour éviter les téléchargements indésirables. Consultez l'article sur les formats personnalisés du guide TRaSH lié et les 3 autres guides de formats personnalisés TRaSH référencés en haut de la page Collection of Custom Formats pour plus d'informations.
  - [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) évitera de télécharger des versions avec Dolby Vision (DV) qui ont une teinte verte si DV n'est pas pris en charge.
  - [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) pour éviter de télécharger des BR-DISK mal nommés qui ne correspondent pas à l'analyse de qualité BR-DISK.

---

- Nom - Le nom du format personnalisé
- Inclure le format personnalisé lors du renommage - Inclure le nom du format personnalisé lors du renommage ?

> Les formats personnalisés n'influencent pas ce qui est recherché - seulement comment les résultats sont évalués. Il n'est pas non plus possible de modifier de quelque manière que ce soit la recherche utilisée par Radarr.
{.is-info}

Les profils sont l'endroit où les scores des formats personnalisés sont configurés.

## Conditions des formats personnalisés

### Modificateurs

- Nier - la correspondance est inversée, donc la condition est satisfaite si et seulement si la condition non niée n'est pas satisfaite
- Requis - s'applique uniquement aux formats avec plus d'une condition du même type et modifie les règles de correspondance pour les groupes de types. L'activation de cette option signifie que cette condition spécifique doit être satisfaite pour que le format personnalisé s'applique dans son ensemble, indépendamment du fait qu'une autre condition du même type satisferait autrement le groupe de types. **Remarque : Vous n'utilisez cela que si vous utilisez une condition plus d'une fois. En d'autres termes, si vous avez un format personnalisé avec 2 conditions de titre de sortie requises et 3 conditions de langue non requises, alors il DOIT satisfaire LES DEUX conditions de titre de sortie requises et il DOIT satisfaire UNE DES 3 conditions de langue.** De même, si vous avez un format personnalisé avec 4 conditions de titre de sortie et aucune n'est requise, alors le format personnalisé s'appliquera si l'une quelconque des conditions est satisfaite.

### Conditions

> **Différents types de conditions** agissent comme `et` dans le même format personnalisé. **Plusieurs conditions du même type** agissent comme `ou` sauf si Requis est utilisé.
{.is-info}

- **Toutes les conditions qui utilisent des expressions régulières ne sont pas sensibles à la casse**
- Notez les problèmes GitHub suivants
  - [Les formats personnalisés ne s'appliquent pas avant l'année du film dans les titres de sortie #4859](https://github.com/Radarr/Radarr/issues/4859)
  - [Le format personnalisé ne correspond pas au terme "xvid" à la fin du nom de sortie #6824](https://github.com/Radarr/Radarr/issues/6824)
- Titre de sortie - C'est une expression régulière correspondant au titre de sortie et, après le téléchargement, au nom de fichier sur le disque.
  - Remarque : Radarr ne considère que le texte après le titre du film et l'année, ce qui signifie que tout ce qui précède le titre est ignoré.
- Édition - Cette balise correspond à toutes les éditions que Radarr peut analyser. Vous pouvez mettre n'importe quelle valeur que Radarr essaiera de faire correspondre à ce qu'il a analysé (sans tenir compte de la casse).
- Langue - Cette langue correspond à toutes les langues que Radarr analyse. Toutes les langues précédemment sélectionnables dans les profils fonctionnent ici.
- [Indicateur d'indexeur](/radarr/settings#indexer-flags) - Cette balise correspond à tous les indicateurs d'indexeur que Radarr peut analyser.
- Source - La source à partir de laquelle une version a été extraite (par exemple BLURAY).
- Résolution - La résolution extraite soit du nom de la version, soit de mediainfo (si disponible).
- Modificateur de qualité - Le modificateur de qualité définit des choses comme Telescene, Telesync, Remux, Régional. Il dissocie une source donnée et une paire de résolution lorsqu'il existe plusieurs types de qualité (source) qui peuvent s'appliquer.
- Taille - Cela correspond à la taille de la version. La taille de la version est convertie en gigaoctets et comparée aux valeurs minimale et maximale.
- Groupe - Cela correspond au groupe que Radarr analyse en fonction de la logique de détection de groupe de Radarr.

### Paramètres de profilage et de classement

- Les formats personnalisés sont mis en œuvre dans les profils de qualité et leur impact est contrôlé par ceux-ci. Le score d'amélioration jusqu'à empêche la mise à niveau une fois qu'une version avec ce score souhaité a été téléchargée.
- Un score de 0 signifie que le format personnalisé est uniquement informatif et n'a aucun impact sur le classement des versions ni sur les langues recherchées.
- Le score minimum nécessite que le score cumulatif des formats personnalisés des versions atteigne ce seuil, sinon elles seront rejetées.
  - Les formats personnalisés correspondant à des attributs indésirables doivent se voir attribuer un score négatif pour réduire leur attrait.
  - Les rejets complets doivent se voir attribuer un score négatif suffisamment bas pour que même si tous les autres formats avec des scores positifs étaient ajoutés, le score serait toujours inférieur au minimum.
- [Veuillez consulter les guides de TRaSH pour savoir comment configurer et utiliser les formats personnalisés](https://trash-guides.info/Radarr/Radarr-setup-custom-formats/)

#### Importation / Exportation de formats personnalisés

- [Veuillez consulter les guides de TRaSH pour savoir comment importer/exporter des formats personnalisés.](https://trash-guides.info/Radarr/Radarr-import-custom-formats/) Cependant, il est possible d'importer et d'exporter des formats personnalisés.

#### Importation / Mise à jour des formats personnalisés existants

- [Veuillez consulter les guides de TRaSH pour savoir comment importer ou mettre à jour des formats personnalisés existants.](https://trash-guides.info/Radarr/Radarr-how-to-update-custom-formats/)

### Collection de formats personnalisés

- [TRaSH maintient une collection de formats personnalisés](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)

# Indexeurs

> Des informations sur les indexeurs pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/radarr/supported#indexers) de cette section
{.is-info}

## Indexeurs pris en charge

- Une liste des indexeurs pris en charge se trouve sur la page [Plus d'informations (Pris en charge)](/radarr/supported#indexers)

### Paramètres de l'indexeur

- Une fois que vous avez cliqué sur le bouton <kb>+</kb> pour ajouter un nouvel indexeur, une nouvelle fenêtre s'ouvre avec de nombreuses options différentes. Aux fins de ce wiki, Radarr considère à la fois les indexeurs Usenet et les trackers Torrent comme des "indexeurs".

- Il y a deux sections ici : Usenet et Torrents. En fonction du client de téléchargement que vous utiliserez, vous devrez sélectionner le type d'indexeur que vous utiliserez.

### Configuration de l'indexeur Usenet

- Newznab - Ici, vous trouverez des préréglages d'indexeurs Usenet populaires (préremplis, vous n'aurez besoin que de votre clé API fournie par l'indexeur Usenet de votre choix), ainsi que la possibilité de créer un indexeur personnalisé.
- Les logiciels qui fonctionnent avec Usenet et s'intègrent très bien avec Radarr sont [NZBHydra2](https://github.com/theotherp/nzbhydra2/) ou [Prowlarr](/prowlarr) qui s'intègrent à la fois à Usenet et aux torrents.
- Que vous choisissiez un indexeur prérempli ou une configuration d'indexeur personnalisée, une nouvelle fenêtre s'affichera pour saisir tous vos paramètres.
- Choisissez parmi les préréglages ou ajoutez un indexeur personnalisé (comme NZBHydra2 ou Prowlarr).
- Nom - Le nom de l'indexeur dans Radarr.
- Activer le flux RSS - Si activé, utilisez cet indexeur pour rechercher les fichiers manquants ou qui n'ont pas encore atteint leur limite.
- Activer la recherche automatique - Si activé, utilisez cet indexeur pour les recherches automatiques, y compris la recherche lors de l'ajout.
- Activer la recherche interactive - Si activé, utilisez cet indexeur pour les recherches interactives manuelles.
- URL - L'URL fournie par l'indexeur, telle que `https://api.nzbgeek.info`.
- Chemin de l'API - Le chemin de l'API fourni par l'indexeur. Il s'agit généralement de `/api`.
- Langues multiples - Définissez les langues `MULTI` pour cet indexeur.
- Clé API - La clé fournie par l'indexeur pour accéder à l'API.
- Catégories - Les catégories par défaut seront utilisées sauf si elles sont modifiées. Il est probable que ces catégories par défaut ne soient pas optimales. Lorsque vous modifiez ce paramètre, Radarr interroge l'indexeur pour obtenir ses catégories disponibles et les affiche dans une liste sélectionnable. Les catégories obsolètes seront effacées dès qu'une catégorie sera activée.
- (Option avancée) Paramètres supplémentaires - Paramètres Newznab supplémentaires à ajouter au lien de requête.
- Supprimer l'année de la chaîne de recherche - Pour les requêtes basées sur du texte, Radarr doit-il supprimer l'année après le titre du film lors de la recherche dans cet indexeur ?
- (Option avancée) Priorité de l'indexeur - Priorité de cet indexeur pour préférer un indexeur à un autre dans les scénarios d'égalité de sortie. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.
- (Option avancée) Client de téléchargement - Sélectionnez et spécifiez le client de téléchargement utilisé pour les téléchargements à partir de cet indexeur.
- Balises - Utilisez uniquement cet indexeur pour les films ayant au moins une balise correspondante. Laissez vide pour utiliser avec tous les films.

### Configuration du tracker Torrent

- Comme pour Usenet, il existe une variété d'informations préremplies sur les trackers Torrent. Si vous n'êtes membre d'aucun de ces trackers spécifiques, ils ne vous seront d'aucune utilité.
- L'une des meilleures et des plus simples façons d'utiliser des trackers Torrent qui ne sont pas nativement pris en charge par Radarr est d'utiliser un deuxième programme tel que [Prowlarr](/prowlarr) ou [Jackett](https://github.com/Jackett/Jackett). Ces logiciels s'intègrent bien avec Radarr en tant qu'indexeur de recherche qui regroupe toutes vos informations et les envoie à Radarr.
- Torznab - Cette option vous permettra de configurer un préréglage Jackett, si vous utilisez plusieurs trackers, vous devrez attribuer un nom unique à chaque entrée.
- Indexeur Torznab
- Choisissez parmi les préréglages ou ajoutez un indexeur personnalisé (comme Jackett).
- Nom - Le nom de l'indexeur dans Radarr.
- Activer le flux RSS - Si activé, utilisez cet indexeur pour rechercher les fichiers manquants ou qui n'ont pas encore atteint leur limite.
- Activer la recherche automatique - Si activé, utilisez cet indexeur pour les recherches automatiques, y compris la recherche lors de l'ajout.
- Activer la recherche interactive - Si activé, utilisez cet indexeur pour les recherches interactives manuelles.
- URL - L'URL fournie par l'indexeur, telle que `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- Chemin de l'API - Le chemin de l'API fourni par l'indexeur. Il s'agit généralement de `/api`.
- Clé API - La clé fournie par l'indexeur pour accéder à l'API.
- Langues multiples - Définissez les langues `MULTI` pour cet indexeur.
- Catégories - Les catégories par défaut seront utilisées sauf si elles sont modifiées. Il est probable que ces catégories par défaut ne soient pas optimales. Lorsque vous modifiez ce paramètre, Radarr interroge l'indexeur pour obtenir ses catégories disponibles et les affiche dans une liste sélectionnable. Les catégories obsolètes seront effacées dès qu'une catégorie sera activée.
- (Option avancée) Paramètres supplémentaires - Paramètres Torznab supplémentaires à ajouter au lien de requête.
- Supprimer l'année de la chaîne de recherche - Pour les requêtes basées sur du texte, Radarr doit-il supprimer l'année après le titre du film lors de la recherche dans cet indexeur ?
- Nombre minimum de sources - Le nombre minimum de sources requis pour qu'une sortie de ce tracker soit téléchargée.
- Ratio de partage - Si vide, utilisez la valeur par défaut du client de téléchargement. Sinon, le ratio de partage minimum requis pour que votre client de téléchargement réponde aux sorties de cet indexeur avant qu'il ne soit mis en pause par votre client et supprimé par Radarr (nécessite la gestion des téléchargements terminés - suppression activée).
- Durée de partage - Si vide, utilisez la valeur par défaut du client de téléchargement. Sinon, la durée de partage minimale en minutes requise pour que votre client de téléchargement réponde aux sorties de cet indexeur avant qu'il ne soit mis en pause par votre client et supprimé par Radarr (nécessite la gestion des téléchargements terminés - suppression activée).
- Drapeaux requis - Quels drapeaux de l'indexeur sont requis ?

#### Drapeaux de l'indexeur

| Drapeau          | Symbole | Description                                                                                                                                                                                                                     |
| ---------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `G_Freeleech`    | ⬇⬇      | Parfois, les sites de torrents définissent un torrent comme étant en téléchargement gratuit. Cela signifie que le téléchargement de ce torrent ne compte pas dans votre quota de téléchargement ou votre ratio. C'est très utile si vous n'avez pas encore établi un bon ratio. |
| `G_Halfleech`    | ⇩⇩      | Similaire à `G_Freeleech`, `G_Halfleech` signifie que seule la moitié de la taille de ce torrent compte dans votre quota de téléchargement ou votre ratio.                                                                               |
| `G_DoubleUpload` | ⬆       | Similaire à `G_Freeleech`, `G_DoubleUpload` signifie que toute quantité de données que vous téléchargez via le partage est comptée deux fois dans votre quota et votre ratio de téléchargement. C'est très utile si vous voulez constituer une réserve de ratio.      |
| `PTP_Golden`     | 🌟       | Sur PassThePopcorn, certains torrents reçoivent l'étiquette *Golden* lorsqu'ils répondent à certaines normes d'encodage. Ce sont généralement les meilleures encodages, avec une perte de qualité presque imperceptible. Vous pouvez en savoir plus sur leur page wiki. |
| `PTP_Approved`   | ✔       | Sur PassThePopcorn, certains torrents sont approuvés lorsqu'ils répondent aux normes minimales d'encodage (par exemple, pas de débits binaires faibles). Consultez leur wiki pour plus d'informations.                                                              |
| `HDB_Internal`   | 🚪       | Les sorties sur HDBits reçoivent cette étiquette lorsque la sortie a été téléchargée par l'un des groupes de sortie de HDBits eux-mêmes.                                                                                           |
| `G_Scene`        | ☠       | Similaire à `G_Freeleech`, `G_Freeleech75` signifie que seule 25% de la taille de ce torrent compte dans votre quota de téléchargement ou votre ratio.                                                                              |
| `G_Freeleech75`  | ⇩⬇      | Similaire à `G_Freeleech`, `G_Freeleech75` signifie que seule 25% de la taille de ce torrent compte dans votre quota de téléchargement ou votre ratio.                                                                              |
| `G_Freeleech25`  | ⇩       | Similaire à `G_Freeleech`, `G_Freeleech25` signifie que seule 75% de la taille de ce torrent compte dans votre quota de téléchargement ou votre ratio.                                                                              |

- (Option avancée) Priorité de l'indexeur - Priorité de cet indexeur pour préférer un indexeur à un autre dans les scénarios d'égalité de sortie. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.
- (Option avancée) Client de téléchargement - Sélectionnez et spécifiez le client de téléchargement utilisé pour les téléchargements à partir de cet indexeur.
- Balises - Utilisez uniquement cet indexeur pour les films ayant au moins une balise correspondante. Laissez vide pour utiliser avec tous les films.

## Options

- Âge minimum - Usenet uniquement : Âge minimum en minutes des NZB avant leur téléchargement. Utilisez cela pour donner aux nouvelles sorties le temps de se propager à votre fournisseur Usenet.
- Rétention - Usenet uniquement : Définissez la valeur sur zéro pour une rétention illimitée.
- Taille maximale - Taille maximale d'une sortie à télécharger en Mo. Définissez la valeur sur zéro pour une taille illimitée. Veuillez noter que cela s'applique globalement.
- Préférence des drapeaux de l'indexeur - Priorité aux sorties avec des drapeaux spéciaux. (Voir les drapeaux requis ci-dessus)
- Délai de disponibilité - Durée avant (-#) ou après (#) la date de disponibilité pour rechercher un film
  - Cela est utile pour retarder la recherche d'une sortie afin de laisser à la communauté le temps de réaliser les meilleurs encodages.
  - Généralement, une disponibilité du film "Sorti" avec un délai de "-21" ou "-14" est recommandée.
- Intervalle de synchronisation du flux RSS - Intervalle en minutes. Définissez la valeur sur zéro pour désactiver (cela arrêtera toutes les recherches automatiques de sorties). Minimum : 10 minutes Maximum : 120 minutes
  - Veuillez consulter [Comment Radarr trouve-t-il des films ?](/radarr/faq#how-does-radarr-find-movies) pour mieux comprendre comment la synchronisation du flux RSS peut vous aider.

> Si Radarr a été hors ligne pendant une période prolongée, Radarr essaiera de revenir en arrière pour trouver la dernière sortie qu'il a traitée afin d'éviter de manquer une sortie. Tant que votre indexeur prend en charge le retour en arrière et que cela n'a pas été trop long, Radarr pourra traiter les sorties qu'il aurait manquées et éviter que vous ayez besoin de rechercher les sorties manquées.{.is-info}

- Balises de sous-titres autorisées - Les balises saisies ici ne seront pas considérées comme des sous-titres intégrés.
- Autoriser les sous-titres intégrés - Si activé, autorisez le téléchargement automatique des sorties avec des sous-titres intégrés.

# Clients de téléchargement

> Des informations sur les clients de téléchargement pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/radarr/supported#download-clients) pour cette section
{.is-info}

## Aperçu

- Le téléchargement et l'importation sont les étapes où la plupart des utilisateurs rencontrent des problèmes. D'un point de vue général, le logiciel doit être capable de communiquer avec votre client de téléchargement et d'avoir accès aux fichiers qu'il télécharge. Il existe une grande variété de clients de téléchargement pris en charge et une variété encore plus grande de configurations. Cela signifie qu'il existe des configurations courantes, mais il n'y a pas de configuration unique et la configuration de chacun peut être légèrement différente. Mais il existe de nombreuses configurations incorrectes.

## Processus du client de téléchargement

### Processus Usenet

- Radarr enverra une demande de téléchargement à votre client et l'associera à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : films, séries TV, musique, etc.
- Radarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Radarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Radarr.
- Radarr analysera cet emplacement de fichier terminé pour trouver les fichiers que Radarr peut utiliser. Il analysera le nom du fichier pour le faire correspondre avec le média demandé. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens physiques et les déplacements atomiques, Radarr utilisera la copie du fichier, puis le supprimera de la source, ce qui est intensif en termes d'E/S.

### Processus Torrent

- Radarr enverra une demande de téléchargement à votre client et l'associera à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement. Exemples : films, séries TV, musique, etc.
- Radarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou la durée peuvent être ajustés dans le client de téléchargement ou depuis Radarr sous le client de téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, Radarr créera un lien physique vers le fichier s'il est pris en charge par votre configuration ou le copiera s'il n'est pas pris en charge par les liens physiques.
- Les liens physiques sont activés par défaut. [Un lien physique ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création de liens physiques échoue ou si votre configuration ne prend pas en charge les liens physiques, Radarr utilisera la copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Radarr, Radarr supprimera le fichier et le torrent d'origine de votre client, mais seulement si le client signale que le partage est terminé et que le torrent est arrêté (c'est-à-dire en pause).

## Clients de téléchargement

Cliquez sur `Paramètres => Clients de téléchargement`, puis cliquez sur le <kb>+</kb> pour ajouter un nouveau client de téléchargement. Votre client de téléchargement doit déjà être configuré et en cours d'exécution.

### Clients de téléchargement pris en charge

- Une liste des clients de téléchargement pris en charge se trouve sur la page [Plus d'informations (Pris en charge)](/radarr/supported#download-clients)

Sélectionnez le client de téléchargement que vous souhaitez ajouter, et une boîte de dialogue apparaîtra pour saisir les détails de connexion. Ces détails sont similaires pour la plupart des clients. Certains demanderont un nom d'utilisateur ou un mot de passe, d'autres demanderont s'il faut ajouter de nouveaux téléchargements en pause/démarrage, etc.

### Paramètres du client Usenet

- Nom - Le nom du client de téléchargement dans Radarr.
- Activer - Activer ce client de téléchargement.
- Hôte - L'URL de votre client de téléchargement.
- Port - Le port de votre client de téléchargement.
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base de l'URL - Ajouter un préfixe à l'URL ; cela est généralement nécessaire pour les serveurs proxy inverses.
- Clé API - La clé API pour s'authentifier auprès de votre client.
- Nom d'utilisateur - Le nom d'utilisateur pour s'authentifier auprès de votre client (généralement pas nécessaire).
- Mot de passe - Le mot de passe pour s'authentifier auprès de votre client (généralement pas nécessaire).
- Catégorie - La catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Priorité récente - priorité du client de téléchargement pour les médias récemment sortis
- Priorité plus ancienne - priorité du client de téléchargement pour les médias sortis il y a un certain temps
- (Option avancée) Priorité du client - Priorité du client de téléchargement. Le round-robin est utilisé pour les clients du même type (torrent/usenet) ayant la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse.
- Gestion des téléchargements terminés
  - Supprimer (Paramètre par client) - Supprimer les téléchargements terminés lorsque le téléchargement est terminé (Usenet) ou arrêté/terminé (torrents). Voir [Gestion des téléchargements terminés pour plus de détails](#completed-download-handling)

### Paramètres du client Torrent

- Nom - Le nom du client de téléchargement dans Radarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement ; il s'agit généralement du port webgui
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base d'URL - Ajouter un préfixe à l'URL ; cela est souvent nécessaire pour les serveurs proxy inverses.
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client
- Catégorie - la catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Catégorie après importation - la catégorie à définir après le téléchargement et l'importation de la version. Veuillez noter que cela rompt la suppression de la gestion des téléchargements terminés.
- Priorité récente - priorité du client de téléchargement pour les médias récemment publiés
- Priorité plus ancienne - priorité du client de téléchargement pour les médias publiés récemment
- État initial - État initial pour les torrents (uniquement Qbittorrent : forcer contourne tous les seuils de partage)
- (Option avancée) Priorité du client - Priorité du client de téléchargement. Le round-robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse
- Gestion des téléchargements terminés
  - Supprimer (paramètre par client) - Supprimer les téléchargements terminés lorsque terminé (usenet) ou arrêté/terminé (torrents). Voir [Gestion des téléchargements terminés pour plus de détails](#completed-download-handling)
    - Pour les torrents, cela nécessite que votre client de téléchargement fasse une pause lorsqu'il atteint les objectifs de partage. Cela nécessite également que les objectifs de partage soient pris en charge par Radarr selon le tableau ci-dessous. Les torrents doivent également rester dans la même catégorie.

### Compatibilité de suppression de téléchargement du client torrent

- Radarr est uniquement capable de définir le ratio de partage/temps sur les clients qui prennent en charge le réglage de cette valeur via leur API lors de l'ajout du torrent. Les objectifs de partage peuvent être définis globalement dans le client lui-même ou par tracker dans les paramètres \*Arr pour chaque indexeur. Consultez le tableau ci-dessous pour connaître la compatibilité du client.

|      Client       |                                Ratio                                 |                                    Temps                                    |
| :---------------: | :------------------------------------------------------------------: | :------------------------------------------------------------------------: |
|       Aria2       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |    ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)    |
|      Deluge       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |    ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)    |
| Download Station  | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |    ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)    |
|       Flood       |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |      ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)      |
|     Hadouken      | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |    ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)    |
|    qBittorrent    |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |      ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)      |
|     rTorrent      |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |      ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)      |
| Torrent Blackhole | ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical) |    ![Non pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Non-critical)    |
|   Transmission    |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   | ![Limite d'inactivité](https://img.shields.io/badge/Pris%20en%20charge-Limite%20d'inactivité*-blue)\* |
|     uTorrent      |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |      ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)      |
|       Vuze        |   ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)   |      ![Pris en charge](https://img.shields.io/badge/Pris%20en%20charge-Oui-success)      |

> ![Limite d'inactivité](https://img.shields.io/badge/Pris%20en%20charge-Limite%20d'inactivité*-blue) - Transmission a une vérification du temps d'inactivité en interne, mais Radarr la compare avec le temps de partage si la limite d'inactivité est définie pour chaque torrent. Cela est fait comme solution de contournement aux limitations de l'API de Transmission.{.is-info}

## Gestion des téléchargements terminés

- La gestion des téléchargements terminés est la façon dont Radarr importe les médias de votre client de téléchargement vers vos dossiers de séries. De nombreux problèmes courants sont liés à de mauvais chemins Docker et/ou à d'autres problèmes de permissions Docker.

- (Paramètre global avancé) Activer - Importer automatiquement les téléchargements terminés du client de téléchargement
- (Option avancée) Intervalle de vérification des téléchargements terminés - Définir la fréquence à laquelle interroger les files d'attente des clients de téléchargement et actualiser les téléchargements surveillés, minimum 1 minute
- (Paramètre par client) Supprimer - Supprimer les téléchargements terminés lorsque terminé (usenet) ou arrêté/terminé (torrents)
  - Pour les torrents, cela nécessite que votre client de téléchargement fasse une pause lorsqu'il atteint les objectifs de partage. Cela nécessite également que les objectifs de partage soient pris en charge par Radarr selon le tableau ci-dessus. Les torrents doivent également rester dans la même catégorie.

### Supprimer les téléchargements terminés

- Radarr envoie une demande de téléchargement à votre client et l'associe à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
- Radarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Radarr connaît l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier de médias.
- Radarr analyse cet emplacement de fichier terminé à la recherche de fichiers vidéo. Il analyse le nom du fichier vidéo pour le faire correspondre à un film. S'il peut le faire, il renomme le fichier selon vos spécifications et le déplace dans le dossier de bibliothèque assigné.
- Les fichiers restants du téléchargement sont envoyés à votre corbeille ou à votre recyclage.

Si vous téléchargez à l'aide d'un client BitTorrent, le processus est légèrement différent :

- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de les partager. Lorsque les fichiers sont importés dans votre dossier de bibliothèque assigné, Radarr tentera de créer un lien physique vers le fichier ou utilisera une copie (utilisez un double espace) si les liens physiques ne sont pas pris en charge.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres, Radarr demandera au client de torrent de supprimer le fichier et le torrent d'origine, mais cela ne se produira que si le client signale que le partage est terminé, que le torrent est dans la même catégorie (c'est-à-dire qu'il n'utilise pas de catégorie après importation), que l'objectif de partage atteint est pris en charge par Radarr et que le torrent est en pause (arrêté).

### Gestion des téléchargements échoués

- La gestion des téléchargements échoués n'est compatible qu'avec SABnzbd et NZBGet.
- La gestion des téléchargements échoués ne s'applique pas aux torrents et il n'est pas prévu d'ajouter une telle fonctionnalité.

- Il existe plusieurs composants qui composent le processus de gestion des téléchargements échoués :

- Vérification du téléchargeur :
  - File d'attente - Vérifiez la file d'attente de votre téléchargeur pour les versions protégées par mot de passe (cryptées) marquées comme échec
  - Historique - Vérifiez l'historique de votre téléchargeur pour les échecs (par exemple, pas assez pour réparer, ou extraction échouée)
- Lorsque Radarr trouve un téléchargement échoué, il commence à les traiter et fait quelques choses :
  - Ajoute un événement d'échec à l'historique de Radarr
  - Supprime le téléchargement échoué du client de téléchargement pour libérer de l'espace et effacer les fichiers téléchargés (facultatif)
  - Commence à rechercher un fichier de remplacement (facultatif)
  - La liste noire (anciennement "Blacklisting") permet de sauter automatiquement les nzbs lorsqu'ils échouent, cela signifie que le nzb ne sera jamais téléchargé automatiquement par Radarr (vous pouvez toujours forcer le téléchargement via une recherche manuelle).
  - Il existe 2 options avancées (sur la page des paramètres "Client de téléchargement") qui contrôlent le comportement des téléchargements échoués dans Radarr, à l'heure actuelle, elles sont toutes activées par défaut.

- Retélécharger - Contrôle si Radarr recherchera ou non le même fichier après un échec
- (Option avancée) Supprimer - Indique si le téléchargement doit être automatiquement supprimé du client de téléchargement lorsque l'échec est détecté

## Mappages de chemin distant

- Le mappage de chemin distant agit comme une recherche de chemin distant et le remplace par un chemin local. Cela est principalement utilisé pour les configurations locales/à distance fusionnées à l'aide de mergerfs ou similaires, ou est utilisé lorsque l'application et le client de téléchargement ne sont pas sur le même serveur.
- Un mappage de chemin distant est utilisé lorsque votre client de téléchargement signale un chemin pour les données terminées soit sur un autre serveur, soit d'une manière que \*Arr n'adresse pas ce dossier.
- Généralement, un mappage de chemin distant n'est nécessaire que si votre client de téléchargement est sur Linux lorsque \*Arr est sur Windows ou vice versa. Un mappage de chemin distant est également peut-être nécessaire si vous mélangez des clients Docker et natifs ou si vous utilisez un serveur distant.
- Un mappage de chemin distant est une recherche/remplacement STUPIDE (où il trouve la valeur DISTANTE, la remplace par la valeur LOCALE pour l'hôte spécifié).
- Si le message d'erreur concernant un mauvais chemin ne contient pas la valeur REMPLACÉE, alors le mappage de chemin ne fonctionne pas comme vous le souhaitez. La solution typique consiste à ajouter et supprimer le mappage.
- [Consultez le tutoriel de TRaSH pour plus d'informations sur le mappage de chemin distant](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Si à la fois \*Arr et votre client de téléchargement sont des conteneurs Docker, il est rare qu'un mappage de chemin distant soit nécessaire. Il est recommandé de [consulter le guide Docker](/docker-guide) et/ou de [suivre le tutoriel de TRaSH](https://trash-guides.info/hardlinks){.is-info}

# Importer des listes

> Des informations sur les types de listes pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/radarr/supported#lists) pour cette section
{.is-info}

## Listes

Les listes d'importation font partie de Radarr et vous permettent de suivre un créateur de liste donné. Disons que vous suivez un créateur de liste donné sur Trakt/TMDb et que vous aimez vraiment leur section "Collection ArrowVerse" et que vous voulez regarder chaque émission de leur liste. Vous regardez dans votre Radarr et réalisez que vous n'avez pas ces séries. Eh bien, au lieu de les rechercher une par une et de les ajouter, puis de rechercher vos indexeurs pour ces séries, vous pouvez le faire tout en une fois avec une liste. Les listes peuvent être configurées pour importer toutes les séries de la liste du conservateur ainsi que pour attribuer automatiquement un profil de qualité, ajouter automatiquement et surveiller automatiquement cette série.

- ATTENTION : Si les listes sont mal faites, elles vont absolument détruire votre bibliothèque avec une tonne de fichiers que vous n'avez aucune intention de regarder. Alors assurez-vous de ce que vous importez avant de cliquer sur Enregistrer. c'est-à-dire regardez physiquement la liste avant même d'aller dans Radarr.

- Ici, vous pouvez sélectionner le bouton <kb>+</kb> pour ouvrir une nouvelle fenêtre contextuelle
- Dans cette nouvelle fenêtre, vous avez plusieurs options différentes pour configurer votre liste à partir de nombreux fournisseurs de listes différents. Comme indiqué précédemment, soyez prudent lorsque vous utilisez des listes. Il est fortement recommandé de ne pas sélectionner le bouton Rechercher lors de l'ajout avant d'être absolument sûr que la liste que vous sélectionnez/configurez ajoute les séries que vous recherchez.
- Une fois que vous avez sélectionné le fournisseur de liste à partir duquel vous souhaitez extraire (comme IMDb ou Trakt), vous serez présenté avec une nouvelle fenêtre.
La plupart des paramètres de liste sont assez explicites, certaines listes nécessitent une authentification avec le fournisseur comme Trakt (ce qui nécessite un compte Trakt.tv)

## Options de liste

- (Option avancée) Intervalle de mise à jour de la liste - À quelle fréquence Radarr doit-il interroger la liste pour les mises à jour ? [Cela est d'au moins 6 heures.](/radarr/faq#why-are-lists-sync-times-so-long-and-can-i-change-it)
- (Option avancée) Niveau de nettoyage de la bibliothèque - Les films de la bibliothèque seront supprimés ou non surveillés s'ils ne sont pas dans votre/dans vos liste(s)
  - Désactivé - Ne pas nettoyer la bibliothèque (recommandé)
  - Journal uniquement - Seulement enregistrer les films qui ne sont pas dans la/les liste(s) et ne prendre aucune autre mesure
  - Conserver et désactiver le film - Conserver les films qui ne sont pas dans la/les liste(s), mais les désactiver dans Radarr.
  - Supprimer le film et conserver les fichiers - Supprimer les films qui ne sont pas dans la/les liste(s) de Radarr, mais ne pas supprimer leurs fichiers
  - Supprimer le film et supprimer les fichiers - Supprimer les films qui ne sont pas dans la/les liste(s) de Radarr et supprimer leurs fichiers

## Exclusions de liste

- Exclusion de liste d'importation - Cela vous permet de nettoyer votre liste de films que vous ne voulez plus voir. Un exemple de cela est si votre liste contient un film qui est dans une langue étrangère et qu'il est peu probable que vous trouviez ce film dans votre langue maternelle et que vous ne voulez pas le regarder avec des sous-titres. Vous pouvez exclure un film pour qu'il ne soit pas ajouté à l'avenir. Cependant, dans la section des exclusions de liste, vous pouvez le réintégrer dans la liste afin que lors de l'exécution de la liste, il soit lu dans votre bibliothèque.

# Connecter

> Des informations sur les types de connexion pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/radarr/supported#notifications) pour cette section
{.is-info}

## Connexions

Les connexions sont la façon dont vous souhaitez que Radarr communique avec le monde extérieur.

- En appuyant sur le bouton <kb>+</kb>, vous obtiendrez une nouvelle fenêtre qui vous permettra de configurer de nombreux points de terminaison différents

- Une liste de notifications et de connexions prises en charge se trouve sur la page [Plus d'informations (Pris en charge)](/radarr/supported#notifications)

## Déclencheurs de connexion

- À la récupération - Être notifié lorsque des films sont disponibles en téléchargement et ont été envoyés à un client de téléchargement
- À l'importation - Être notifié lorsque des films sont importés avec succès
- À la mise à niveau - Être notifié lorsque des films sont mis à niveau vers une meilleure qualité
- Au renommage - Être notifié lorsque des films sont renommés
- À l'ajout de film - Être notifié lorsque des films sont ajoutés à la bibliothèque de Radarr pour les gérer ou les surveiller
- À la suppression de film - Être notifié lorsque des films sont supprimés
- À la suppression de fichier de film - Être notifié lorsque des fichiers de films sont supprimés
- À la suppression de fichier de film pour mise à niveau - Être notifié lorsque des fichiers de films sont supprimés pour des mises à niveau
- En cas de problème de santé - Être notifié en cas d'échec de la vérification de santé
  - Inclure les avertissements de santé - Être notifié en cas d'avertissements de santé en plus des erreurs.
- À la mise à jour de l'application - Être notifié lorsque Radarr est mis à jour vers une nouvelle version

# Métadonnées

## Options

- Pays de certification - Sélectionnez le pays à utiliser pour les certifications de films (par exemple, R (US) ou 12A (UK))

## Consommateurs de métadonnées

> Des informations sur les consommateurs de métadonnées pris en charge peuvent être trouvées sur la page [Plus d'informations (Pris en charge)](/radarr/supported#metadata) pour cette section
{.is-info}

Ici, vous pouvez sélectionner le type de métadonnées qui sera utilisé par votre lecteur multimédia

Kodi sera l'une des options les plus couramment utilisées ici si c'est le logiciel utilisé. Cela permettra à Radarr de créer un fichier NFO ainsi que des affiches de film associées à être récupérées dans votre lecteur

# Étiquettes

- La section des étiquettes dans Radarr est utilisée pour lier différents aspects de Radarr. Elles sont également utiles pour suivre quels films proviennent de quelles listes.
- Les étiquettes sont particulièrement utiles pour :

  - Profils de retard
  - Restrictions
  - Indexeurs

- Les étiquettes peuvent être utilisées pour lier des profils de retard, des indexeurs, des restrictions et des films ensemble.
- Par exemple :
  - Vous voulez qu'un indexeur spécifique soit utilisé pour un film spécifique. Vous créez une étiquette et vous attribuez le film et l'indexeur à cette étiquette.
  - Vous voulez qu'une restriction spécifique s'applique uniquement à un film spécifique. Vous créez une étiquette et vous attribuez la restriction et le film à cette étiquette.
  - Ce processus est le même pour les profils de retard.

> Un film utilisera à la fois les indexeurs qui ont des étiquettes correspondantes et les indexeurs qui n'ont pas d'étiquettes.
{.is-warning}

> Remarque : Les étiquettes n'influencent pas les "Formats personnalisés", les "Profils de qualité" ou tout autre aspect non mentionné ci-dessus.
{.is-info}

# Général

## Hôte

- Adresse de liaison - Adresse IPv4 valide ou '*' pour toutes les interfaces
  - 0.0.0.0 ou `*` - toutes les adresses peuvent se connecter
  - 127.0.0.1 ou localhost - seules les applications en local peuvent se connecter
  - Toute autre IP (par exemple 1.2.3.4) - seule cette IP (1.2.3.4) peut se connecter
- Numéro de port - Le numéro de port que vous souhaitez utiliser pour accéder à l'interface web de Radarr

> Note : Si vous utilisez Docker, ne modifiez pas ce paramètre.
{.is-warning}

- URL de base - Pour la prise en charge d'un proxy inverse, la valeur par défaut est vide

> Note : Si vous utilisez un proxy inverse (par exemple : mondomaine.com/radarr), vous devez entrer '/radarr' pour l'URL de base.
{.is-info}

- Activer SSL - Si vous disposez de certificats SSL et souhaitez sécuriser les communications vers et depuis votre Radarr, activez cette option.

> Note : N'utilisez pas cette option à moins de savoir ce que vous faites.
{.is-warning}

## Sécurité

- Authentification - Comment souhaitez-vous vous authentifier pour accéder à votre instance Radarr
  - À partir de Radarr v5, l'authentification est désormais obligatoire. [Consultez la FAQ sur l'authentification obligatoire pour plus de détails.](/radarr/faq#forced-authentication)
  - ~~Aucune - Vous n'avez pas besoin d'authentification pour accéder à votre Radarr. Généralement, si vous êtes le seul utilisateur de votre réseau, si personne sur votre réseau ne souhaite accéder à votre Radarr ou si votre Radarr n'est pas exposé sur le web~~
  - Basique (fenêtre contextuelle du navigateur) - Cette option affiche une petite fenêtre contextuelle vous permettant de saisir un nom d'utilisateur et un mot de passe lorsque vous accédez à votre Radarr
  - Formulaire (page de connexion) - Cette option affiche une page de connexion familière, similaire à celle des autres sites web, vous permettant de vous connecter à votre Radarr
- Clé API - C'est ainsi que d'autres programmes peuvent communiquer avec Radarr ou faire communiquer Radarr avec d'autres programmes. Si cette clé est donnée à la mauvaise personne ayant accès, elle pourrait faire toutes sortes de choses sur votre bibliothèque. C'est pourquoi la clé API est masquée dans les journaux.
- Validation du certificat - Modifiez le niveau de validation des certificats HTTPS
  - Activée - Valider tous les certificats HTTPS (recommandé)
  - Désactivée pour les adresses locales - Ne pas valider les certificats HTTPS pour localhost et le réseau local
  - Désactivée - Ne pas valider les certificats HTTPS

## Proxy

Proxy - Cette option vous permet de faire passer les informations que Radarr récupère et recherche par un proxy. Cela peut être utile si vous vous trouvez dans un pays qui n'autorise pas le téléchargement de fichiers Torrent.

- Utiliser un proxy - Activer pour utiliser un proxy
- Type de proxy - Sélectionnez le type de proxy (HTTPS, Socks4 ou Socks5)
- Nom d'hôte - Entrez le nom d'hôte de votre proxy (ne pas inclure http/https ou tout autre protocole)
- Port - Entrez le port de votre proxy
- Nom d'utilisateur - Entrez le nom d'utilisateur de votre proxy, le cas échéant
- Mot de passe - Entrez le mot de passe de votre proxy, le cas échéant
- Adresses ignorées - Entrez une liste d'adresses séparées par des virgules qui contourneront le proxy
- Contourner le proxy pour les adresses locales - Cochez cette case pour contourner le proxy pour les adresses locales. Les requêtes locales sont identifiées par l'absence d'un point (.) dans l'URI, comme dans <http://serveurweb/>, ou pour accéder au serveur local, y compris <http://localhost>, <http://loopback> ou <http://127.0.0.1>. Lorsque cette option est désactivée, toutes les requêtes Internet passent par le serveur proxy.

## Journalisation

- Niveau de journalisation - L'un des outils de dépannage les plus utiles
  - Info - C'est la façon la plus basique dont Radarr collecte des informations, cela inclura un minimum d'informations dans les journaux. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement et d'information.
  - Débogage - Le débogage inclura toutes les informations incluses dans Info, ainsi que des informations supplémentaires pouvant être utiles. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement, d'information et de débogage.
  - Trace - La journalisation la plus avancée et détaillée sur Radarr, Trace inclura toutes les informations collectées par Info et Debug, et plus encore. C'est le type de journal le plus couramment demandé lors du dépannage sur Discord ou Reddit. Si vous avez besoin d'aide, veuillez sélectionner votre journal en mode Trace et refaire la tâche qui vous posait problème pour capturer le journal. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement, d'information, de débogage et de trace.

## Analyse

- Analyse - Envoyer des informations d'utilisation et d'erreurs anonymes aux serveurs de Radarr (Servarr). Cela inclut des informations sur votre navigateur, les pages de l'interface WebUI de Radarr que vous utilisez, les rapports d'erreurs ainsi que la version du système d'exploitation et d'exécution. Nous utiliserons ces informations pour hiérarchiser les fonctionnalités et les corrections de bugs.

## Mises à jour

- (Option avancée) Branche - Il s'agit de la branche de Radarr que vous utilisez.
  - [Veuillez consulter cette FAQ pour plus d'informations](/radarr/faq#how-do-i-update-radarr)
- Automatique - Télécharger et installer automatiquement les mises à jour. Vous pourrez toujours installer depuis Système : Mises à jour. Remarque : Les utilisateurs de Windows sont toujours mis à jour automatiquement.
- Mécanisme - Utiliser le système de mise à jour intégré de Radarr ou un script
  - Intégré - Utiliser le système de mise à jour intégré de Radarr
  - Script - Faire exécuter la mise à jour par Radarr
  - Docker - Ne pas mettre à jour Radarr depuis l'intérieur du conteneur Docker, mais plutôt tirer une nouvelle image avec la nouvelle mise à jour
- Script - Visible uniquement lorsque le mécanisme est défini sur Script - Chemin vers le script de mise à jour
- Processus de mise à jour - Radarr téléchargera le fichier de mise à jour, vérifiera son intégrité, l'extraiera dans un emplacement temporaire et appellera la méthode choisie. Le processus de mise à jour sera exécuté avec le même utilisateur que celui sous lequel Radarr est exécuté, il aura besoin des autorisations pour mettre à jour les fichiers de Radarr ainsi que pour arrêter/démarrer Radarr.
- Intégré - La méthode intégrée sauvegardera les fichiers et les paramètres de Radarr, arrêtera Radarr, mettra à jour l'installation et démarrera Radarr. Si votre système ne peut pas gérer l'arrêt de Radarr et tentera de le redémarrer automatiquement, il est peut-être préférable d'utiliser un script à la place. En cas d'échec, la version précédente de Radarr sera redémarrée.
- Script - Le script devrait gérer la même chose que le système de mise à jour intégré. Si vous devez gérer l'arrêt et le démarrage des services (upstart/launchd/etc), vous devrez le faire ici.

## Sauvegardes

- La section des sauvegardes vous permet de définir comment Radarr doit gérer les sauvegardes.

- (Option avancée) Dossier - Cela vous permet de sélectionner l'emplacement de sauvegarde. Dans Docker, vous serez limité à ce que vous autorisez le conteneur à voir. Les chemins sont relatifs au dossier appdata ; si nécessaire, vous pouvez définir un chemin absolu pour sauvegarder en dehors du dossier appdata.
- (Option avancée) Intervalle - À quelle fréquence souhaitez-vous que Radarr effectue une sauvegarde
- (Option avancée) Rétention - Combien de temps souhaitez-vous que Radarr conserve chaque sauvegarde. Après la création d'une nouvelle sauvegarde, la plus ancienne sera supprimée.

> Les sauvegardes manuelles sont conservées indéfiniment, stockées dans le même dossier et portent un nom différent.
{.is-info}

# Interface utilisateur

## Calendrier

- Premier jour de la semaine - Ici, vous pouvez sélectionner quel jour vous pensez être le premier jour de la semaine.
- En-tête de colonne de la semaine - Ici, vous pouvez sélectionner l'en-tête des colonnes.

## Films

- Format de durée - Sélectionnez comment formater les durées, en heures et minutes ou en minutes.

## Dates

- Format de date court - Comment souhaitez-vous que Radarr affiche les dates courtes ?
- Format de date long - Comment souhaitez-vous que Radarr affiche les dates au format long ?
- Format de l'heure - Souhaitez-vous un format 12 heures ou 24 heures ?
- Afficher les dates relatives - Souhaitez-vous que Radarr affiche des dates relatives (Aujourd'hui/Hier/etc) ou des dates absolues ?

## Style

- Activer le mode pour les personnes atteintes de daltonisme - Style modifié pour permettre aux personnes atteintes de daltonisme de mieux distinguer les informations codées par couleur.

## Langue

- Langue des informations sur les films - Sélectionnez la langue dans laquelle Radarr affiche les informations sur les films dans l'interface utilisateur.
- Langue de l'interface utilisateur - Sélectionnez la langue que Radarr utilise dans l'application.