---
title: Paramètres Sonarr
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, needs-love, settings
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Options de menu](#options-de-menu)
- [Gestion des médias](#gestion-des-médias)
  - [Suggestions de nom de la communauté](#suggestions-de-nom-de-la-communauté)
  - [Nom des épisodes](#nom-des-épisodes)
    - [Format standard des épisodes](#format-standard-des-épisodes)
    - [Nom de la série](#nom-de-la-série)
    - [Identifiants de la série](#identifiants-de-la-série)
    - [Saisons](#saisons)
    - [Épisodes](#épisodes)
    - [Date de diffusion](#date-de-diffusion)
    - [Titre de l'épisode](#titre-de-lépisode)
    - [Qualité](#qualité)
    - [Informations sur les médias](#informations-sur-les-médias)
    - [Autres](#autres)
    - [Original](#original)
  - [Format quotidien des épisodes](#format-quotidien-des-épisodes)
  - [Format des épisodes d'anime](#format-des-épisodes-danime)
    - [Numéro d'épisode absolu](#numéro-dépisode-absolu)
  - [Format du dossier de la série](#format-du-dossier-de-la-série)
    - [Nom de la série](#nom-de-la-série-1)
    - [Identifiants de la série](#identifiants-de-la-série-1)
  - [Format du dossier de la saison](#format-du-dossier-de-la-saison)
    - [Saisons](#saisons-1)
  - [Format du dossier de la saison](#format-du-dossier-de-la-saison-1)
    - [Épisodes spéciaux](#épisodes-spéciaux)
  - [Style multi-épisode](#style-multi-épisode)
  - [Dossiers](#dossiers)
  - [Importation](#importation)
  - [Gestion des fichiers](#gestion-des-fichiers)
  - [Autorisations](#autorisations)
  - [Dossiers racine](#dossiers-racine)
- [Profils](#profils)
  - [Profils de qualité](#profils-de-qualité)
  - [Profils de langue](#profils-de-langue)
  - [Profils de retard](#profils-de-retard)
    - [Utilisations](#utilisations)
    - [Fonctionnement des profils de retard](#fonctionnement-des-profils-de-retard)
      - [Exemples](#exemples)
        - [Exemple 1](#exemple-1)
        - [Exemple 2](#exemple-2)
        - [Exemple 3](#exemple-3)
  - [Profils de publication](#profils-de-publication)
- [Qualité](#qualité)
  - [Signification du tableau de qualité](#signification-du-tableau-de-qualité)
  - [Définition des qualités](#définition-des-qualités)
- [Indexeurs](#indexeurs)
  - [Indexeurs pris en charge](#indexeurs-pris-en-charge)
    - [Paramètres de l'indexeur](#paramètres-de-lindexeur)
    - [Configuration de l'indexeur Usenet](#configuration-de-lindexeur-usenet)
    - [Configuration du tracker torrent](#configuration-du-tracker-torrent)
  - [Options](#options)
- [Clients de téléchargement](#clients-de-téléchargement)
  - [Aperçu](#aperçu)
  - [Processus du client de téléchargement](#processus-du-client-de-téléchargement)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Clients de téléchargement](#clients-de-téléchargement-1)
    - [Clients de téléchargement pris en charge](#clients-de-téléchargement-pris-en-charge)
    - [Paramètres du client Usenet](#paramètres-du-client-usenet)
    - [Paramètres du client torrent](#paramètres-du-client-torrent)
    - [Compatibilité de suppression de téléchargement du client torrent](#compatibilité-de-suppression-de-téléchargement-du-client-torrent)
  - [Gestion des téléchargements terminés](#gestion-des-téléchargements-terminés)
    - [Supprimer les téléchargements terminés](#supprimer-les-téléchargements-terminés)
    - [Gestion des échecs de téléchargement](#gestion-des-échecs-de-téléchargement)
  - [Mappings de chemin distant](#mappings-de-chemin-distant)
- [Listes d'importation](#listes-dimportation)
  - [Listes](#listes)
  - [Exclusions de liste](#exclusions-de-liste)
- [Connecter](#connecter)
  - [Connexions](#connexions)
  - [Déclencheurs de connexion](#déclencheurs-de-connexion)
- [Métadonnées](#métadonnées)
  - [Métadonnées](#métadonnées-1)
- [Tags](#tags)
- [Général](#général)
  - [Hôte](#hôte)
  - [Sécurité](#sécurité)
  - [Proxy](#proxy)
  - [Journalisation](#journalisation)
  - [Analyse](#analyse)
  - [Mises à jour](#mises-à-jour)
  - [Sauvegardes](#sauvegardes)
- [Interface utilisateur](#interface-utilisateur)
  - [Calendrier](#calendrier)
  - [Dates](#dates)
  - [Style](#style)
  
Cette page présente tous les paramètres disponibles dans Sonarr et leur fonctionnement. Elle ne vise pas à être un guide complet sur la configuration de Sonarr. Consultez plutôt la page [Guide de démarrage rapide](/sonarr/quick-start-guide).

# Options de menu

Pour accéder à la page des paramètres, sélectionnez Paramètres dans le menu de gauche. Les options de sous-menu suivantes seront disponibles :

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

Notez également que pour chaque page de paramètres individuelle, il y a des options en haut du menu :

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- Masquer/Afficher les options avancées est important pour tous les éléments marqués ci-dessous comme `(Option avancée)`, sinon ils n'apparaîtront pas. Ces éléments de menu sont affichés en orange dans les captures d'écran.

- Vous devez enregistrer vos modifications avant de quitter l'écran. Pour cela, cliquez sur l'icône du disque. Si vous n'avez apporté aucune modification, il affichera "Aucune modification" et sera grisé, comme indiqué ci-dessus.

# Gestion des médias

> Certains de ces paramètres ne sont visibles que via `Afficher les paramètres avancés` qui se trouve dans la barre supérieure sous la barre de recherche{.is-info}

## Suggestions de nom de la communauté

> Voici quelques suggestions de nom de la communauté provenant des [Guides de TRaSH](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) {.is-info}

> Avertissement : À partir de la version 3.0.6.1431, Sonarr prend désormais en charge la reconnaissance des types Dolby Vision (DV) et High Dynamic Range (HDR). Si vous utilisez une version inférieure, remplacez : `{[MediaInfo VideoDynamicRangeType]}` par `{[MediaInfoVideoDynamicRange]}` {.is-warning}

- Série standard : `{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Série quotidienne : `{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Série d'anime : `{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- Dossiers de saison : `Saison {season:00}`

- Style multi-épisode : `Scene`

- Dossiers de série : `{Series TitleYear} [imdb-{ImdbId}]`

## Nom des épisodes

- Renommer les épisodes - Cochez pour permettre à Sonarr de renommer les fichiers
  - Si non coché :
    - Importation du client de téléchargement
      - Pack non saisonnier : le titre de sortie du client de téléchargement est utilisé
      - Pack saisonnier : Nom de fichier d'origine
    - Importation manuelle (ad hoc) : Nom de fichier d'origine

- Remplacer les caractères illégaux - Si non coché, Sonarr les supprimera à la place.
  - Les caractères sont : `:` `\` `/` `>` `<` `?` `*` `|` `"`

### Format standard des épisodes

Format standard des épisodes - Définissez la convention de nommage pour vos épisodes de type série standard. Cliquez sur l'icône `?` pour ouvrir la boîte de dialogue `Jeton de nom de fichier`.

- Boîte déroulante (coin supérieur droit)
  - Boîte de gauche - Gestion des espaces
  - Espace ( ) - Utiliser des espaces dans le nommage (par défaut)
  - Point (.) - Utiliser des points à la place des espaces dans le nommage
  - Tiret bas (_) - Utiliser des tirets bas à la place des espaces dans le nommage
  - Tiret (-) - Utiliser des tirets à la place des espaces dans le nommage
  - Boîte de droite - Gestion de la casse
  - Cas par défaut - Mettre en majuscules et minuscules (~camel-case) (par défaut)
  - Majuscules - Mettre tout en majuscules
  - Minuscules - Mettre tout en minuscules

### Nom de la série

- `{Series Title}` = Le titre de la série !
- `{Series CleanTitleYear}` = Le titre de la série ! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Le titre de la série !
- `{Series TitleThe}` = Le titre de la série, The
- `{Series TitleYear}` = Le titre de la série (2010)
- `{Series Year}` = (2010)

### Identifiants de la série

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### Saisons

- `{season:0}` = 1
- `{season:00}` =  01

### Épisodes

- `{episode:0}` = 1
- `{episode:00}` = 01

### Date de diffusion

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### Titre de l'épisode

- `{Episode Title}` = Titre de l'épisode
- `{Episode CleanTitle}` =  Titre de l'épisode

### Qualité

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Informations sur les médias

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguagesAll}` = \[DE\]
- `{MediaInfo AudioLanguagesAll}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`, `AudioLanguages` et `SubtitleLanguages` prennent en charge un suffixe `:EN+DE` qui vous permet de filtrer les langues incluses dans le nom du fichier. Utilisez `-DE` pour exclure des langues spécifiques. L'ajout de <kb>+</kb> (par exemple : `:EN+`) affichera `[EN]`, `[EN+--]` ou `[--]` en fonction des langues exclues. Par exemple, `{MediaInfo Full:EN+DE}`.
{.is-info}

> `AudioLanguages` n'affichera pas de langue pour l'audio s'il n'existe qu'une seule langue et qu'elle est EN (anglais). Pour obtenir le comportement souhaité et, par exemple, afficher l'allemand et l'anglais, utilisez {MediaInfo AudioLanguagesAll:DE+EN} à la place.
{.is-info}

> `MediaInfo VideoDynamicRangeType` donnera les valeurs possibles : DV, DV HDR10, HDR10, HDR10Plus, HLG, PQ et HDR
{.is-info}

### Autres

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL ou NF

> \* Les mots préférés seront le mot ou les mots qui correspondent littéralement à tous les mots préférés que vous avez. L'exemple ci-dessus serait un mot préféré `iNTERNAL` ou de manière similaire un mot préféré `/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i` renverrait `AMZN` ou `Amazon`
\* `{Preferred Words:<Nom du profil de publication>}` est une option supplémentaire pour utiliser des correspondances provenant de profils de publication spécifiques
{.is-info}

### Original

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> `Original Title` est le nom de la version et c'est ce qui est suggéré d'utiliser.
{.is-info}

>`Original Filename` n'est pas recommandé. C'est le nom de fichier d'origine littéral et peut être obscurci `t1i0p3s7i8yu7ti`.
{.is-warning}

## Format quotidien des épisodes

Format quotidien des épisodes - Définissez la convention de nommage pour vos épisodes de type série quotidienne. Cliquez sur l'icône `?` pour ouvrir la boîte de dialogue `Jeton de nom de fichier`.

Voir [Format standard des épisodes](/sonarr/settings#standard-episode-format) pour plus d'informations sur cette boîte de dialogue.

## Format des épisodes d'anime

Format des épisodes d'anime - Définissez la convention de nommage pour vos épisodes de type série anime. Cliquez sur l'icône `?` pour ouvrir la boîte de dialogue `Jeton de nom de fichier`.

Voir [Format standard des épisodes](/sonarr/settings#standard-episode-format) pour plus d'informations sur cette boîte de dialogue.

### Numéro d'épisode absolu

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## Format du dossier de la série

(Option avancée) - Dossier de la série - Définissez la convention de nommage pour le dossier. Cliquez sur l'icône `?` pour ouvrir la boîte de dialogue `Jeton de nom de fichier`.

### Nom de la série

- `{Series Title}` = Nom de la série !
- `{Series CleanTitleYear}` = Titre de la série 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Titre de la série
- `{Series TitleThe}` = Titre de la série, The
- `{Series TitleYear}` = Titre de la série (2010)
- `{Series Year}` = (2010)

### Identifiants de la série

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## Format du dossier de la saison

### Saisons

- `{season:0}` = 1
- `{season:00}` = 01

## Format du dossier de la saison

### Épisodes spéciaux

Nom du dossier `Épisodes spéciaux` (Saison)

- `Épisodes spéciaux`

> Il est recommandé d'utiliser `Épisodes spéciaux`
{.is-info}

## Style multi-épisode

- `Étendre` = `S01E01-02-03`
- `Dupliquer` = `S01E01.S01E01`
- `Répéter` = `S01E01E02E03`
- `Scène` = `S01E01-E02-E03`
- `Plage` = `S01E01-03`
- `Plage préfixée` = `S01E01-E03`

> Il est recommandé d'utiliser `Scène`
{.is-info}

## Dossiers

- Créer des dossiers médias vides - Créez les dossiers de séries manquants lors de l'analyse du disque
- Supprimer les dossiers vides - Supprimez les dossiers de séries et de saisons vides lors de l'analyse du disque et lorsque les fichiers d'épisodes sont supprimés

## Importation



- Titre de l'épisode requis - Empêche l'importation pendant 48 heures à partir de l'heure de diffusion des épisodes [UTC](https://fr.wikipedia.org/wiki/Temps_universel_coordonn%C3%A9) si le titre de l'épisode est au format de nommage et que le titre de l'épisode est TBA (à déterminer). Après 48 heures, la sortie sera importée même si le titre est toujours TBA.
  - Toujours - Attendez toujours jusqu'à 48 heures pour un titre avant d'importer si l'épisode est TBA.
  - Uniquement pour les sorties en masse de saison - Attendez jusqu'à 48 heures pour un titre avant d'importer si l'épisode est TBA, uniquement si un pack de saison ou une sortie en masse est trouvé. <- C'est recommandé.
  - Jamais - N'attendez pas pour importer si l'épisode est TBA.
- Ignorer la vérification de l'espace libre - Utilisez lorsque Sonarr ne parvient pas à détecter l'espace libre à partir du dossier racine de votre série.
- Espace libre minimum - En activant cette option, l'importation sera empêchée si elle laisse moins que cette quantité d'espace disque disponible.
- Utiliser des liens durs au lieu de la copie - Utilisez des liens durs lors de la tentative de copie de fichiers à partir de torrents qui sont encore en cours de partage.
  - Pour plus d'informations à ce sujet, cliquez [ici](https://trash-guides.info/hardlinks)

 > Rarement - mais éventuellement -, les verrous de fichiers peuvent empêcher le renommage des fichiers qui sont en cours de partage. Vous pouvez désactiver temporairement le partage et utiliser la fonction de renommage de Sonarr comme solution de contournement.
{.is-warning}

- Importer des fichiers supplémentaires - Importer des fichiers supplémentaires correspondants (sous-titres, nfo, etc.) après l'importation d'un fichier.
  Si le nom du fichier de sous-titres contient des balises supplémentaires telles que `cc` ou `forced`, elles seront conservées tant qu'elles sont reconnues (actuellement dans la version de développement).

## Gestion des fichiers

- Désactiver la surveillance des épisodes supprimés - Les épisodes supprimés du disque sont automatiquement désactivés dans Sonarr.
- Télécharger les versions correctes et les repacks - Permet ou non de mettre automatiquement à niveau vers les versions correctes/repacks. Utilisez `Ne pas préférer` pour trier selon le score des mots préférés plutôt que les versions correctes/repacks.
  - Préférer et mettre à niveau - Classez les repacks et les versions correctes plus haut que les versions non-repacks et non-correctes. Considérez les nouveaux repacks et les nouvelles versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas mettre à niveau automatiquement - Classez les repacks et les versions correctes plus haut que les versions non-repacks et non-correctes. Ne considérez pas les nouveaux repacks et les nouvelles versions correctes comme une mise à niveau des versions actuelles.
  - Ne pas préférer - Ignorez les repacks et les versions correctes. Vous devrez gérer toute préférence pour ceux-ci avec les [Profils de sortie (Mots préférés)](#profils-de-sortie).

> `PROPER` - signifie qu'il y avait un problème avec la version précédente. Les téléchargements marqués comme PROPER montrent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui n'a pas publié l'original.
> `REPACK` - signifie qu'il y avait un problème avec la version précédente et qu'il a été corrigé par le groupe original. Les téléchargements marqués comme REPACK montrent que les problèmes ont été résolus dans cette version. Cela est fait par un groupe qui a publié l'original.
{.is-info}

> [Utilisez des mots préférés pour les mises à niveau automatiques vers les versions correctes/repacks](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#propers-and-repacks)
{.is-info}

- Analyser les fichiers vidéo - Extraire les informations du fichier telles que la résolution, la durée et les informations sur le codec à partir des fichiers. Cela nécessite que Sonarr lise des parties du fichier, ce qui peut entraîner une activité disque ou réseau élevée pendant les analyses.
- Analyser à nouveau le dossier de la série après actualisation - Analyser à nouveau le dossier de la série après l'actualisation de la série
  - Toujours - Cela permet de scanner à nouveau le dossier de la série en fonction de la planification des tâches.
  - Après actualisation manuelle - Vous devrez scanner manuellement le disque.
  - Jamais - Comme son nom l'indique, ne jamais scanner à nouveau le dossier de la série.
- Modifier la date du fichier - Modifier la date du fichier lors de l'importation/analyse
  - Aucun - Sonarr ne modifiera pas la date qui s'affiche dans votre explorateur de fichiers.
  - Date de sortie locale - La date à laquelle la vidéo a été diffusée localement.
  - Date de sortie UTC - La date à laquelle la vidéo a été diffusée en fonction de l'UTC.
- Corbeille de recyclage - Les fichiers d'épisodes seront placés ici lorsqu'ils seront supprimés au lieu d'être supprimés définitivement.
- Nettoyage de la corbeille de recyclage - C'est l'ancienneté d'un fichier donné avant qu'il ne soit supprimé définitivement.

> Les fichiers de la corbeille de recyclage plus anciens que le nombre de jours sélectionné seront automatiquement nettoyés. {.is-warning}

## Autorisations

- Définir les autorisations - Doit-on exécuter `chmod` lors de l'importation/du renommage des fichiers ?
  - Dossier chmod - Octal, appliqué lors de l'importation/du renommage aux dossiers et fichiers multimédias (sans bits d'exécution)

> La liste déroulante propose une liste prédéfinie d'autorisations très couramment utilisées. Cependant, vous pouvez entrer manuellement un octal de dossier si vous le souhaitez.
{.is-info}

> Cela ne fonctionne que si l'utilisateur exécutant `Sonarr` est le propriétaire du fichier. Il est préférable de s'assurer que le client de téléchargement définit correctement les autorisations.
{.is-warning}

- chown Group - Nom du groupe ou GID. Utilisez GID pour les systèmes de fichiers distants.

> Cela ne fonctionne que si l'utilisateur exécutant `Sonarr` est le propriétaire du fichier. Il est préférable de s'assurer que le client de téléchargement définit correctement les autorisations.
{.is-warning}

## Dossiers racine

- Chemin - Cela montre le chemin vers votre bibliothèque multimédia.
- Espace libre - C'est l'espace libre rapporté à Sonarr par le système.
- Dossiers non mappés - Ce sont des dossiers qui ne sont associés à aucune série.

> Le `X` à la fin supprimera ce chemin racine.
{.is-info}

- Ajouter un dossier racine - Cela vous permet de sélectionner un chemin racine pour placer les nouveaux téléchargements importés dans ce dossier ou pour permettre à Sonarr de scanner les médias existants.

> Utilisateurs non Windows :
> \* Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

# Profils

## Profils de qualité

- Définissez des profils pour la qualité des séries que vous souhaitez télécharger.

> Lorsque vous sélectionnez un profil existant ou ajoutez un profil supplémentaire, une nouvelle fenêtre apparaîtra.
{.is-info}

> Remarque : La qualité qui a une case bleue est la qualité à laquelle tout média avec ce profil sera continuellement mis à niveau.
{.is-info}

- Nom - Sélectionnez un nom **UNIQUE** pour le profil de qualité que vous créez.
- Mises à niveau autorisées - Lorsque cette option est cochée et que vous demandez à Sonarr de télécharger un `WEB 1080p` car c'est la première sortie d'un épisode spécifique, puis plus tard quelqu'un peut télécharger un `Bluray-1080p`, Sonarr se mettra automatiquement à niveau vers une meilleure qualité ***si*** `Mise à niveau jusqu'à` a cette qualité sélectionnée.
- Mise à niveau jusqu'à - Une fois cette qualité atteinte, Sonarr ne téléchargera plus les épisodes.

> Remarque : Cela s'applique uniquement si vous avez `Bluray-1080p` supérieur à `WEB 1080p` dans la section `Qualités`.
{.is-warning}

- Qualités - Les qualités les plus élevées dans la liste sont les plus préférées, même si elles ne sont pas cochées. Les qualités du même groupe sont équivalentes. Seules les qualités cochées sont souhaitées.
- Modifier les groupes - Certaines qualités sont regroupées pour réduire la taille de la liste ainsi que pour regrouper les versions similaires. Un exemple typique est `WebDL` et `WebRip`, car ils sont très similaires et ont généralement des débits similaires. Lorsque vous modifiez les groupes, vous pouvez modifier la préférence au sein de chaque groupe. [Voir le guide de TRaSh sur la fusion des qualités](https://trash-guides.info/merge-quality)
  - [Voir les qualités](#qualités-définies)

> Par défaut, les qualités sont définies du plus bas (en bas) au plus élevé (en haut).
{.is-info}

## Profils de langue

- Définissez des profils pour la langue des séries que vous souhaitez télécharger.

> Veuillez noter que la priorité / l'ordre a de l'importance même si la langue n'est pas souhaitée (sélectionnée).
{.is-info}

- Nom - Sélectionnez un nom **UNIQUE** pour le profil de langue que vous créez.
- Mises à niveau autorisées - Si non cochée (désactivée), les langues ne seront pas mises à niveau. Par exemple, si vous demandez à Sonarr de télécharger une version chinoise car c'est la première sortie d'une série spécifique, puis plus tard quelqu'un peut télécharger une version anglaise, avec cette option sélectionnée, Sonarr se mettra automatiquement à niveau vers une meilleure qualité.

> Cela n'est valable que si l'anglais est plus haut dans la liste des langues que le chinois et que les deux sont sélectionnés.
{.is-warning}

- Langues - Les langues les plus élevées dans la liste sont les plus préférées. Seules les langues cochées sont souhaitées.

## Profils de retard

- Les profils de retard vous permettent de réduire le nombre de versions qui seront téléchargées pour un épisode en ajoutant un délai pendant que Sonarr continue de rechercher des versions qui correspondent mieux à vos préférences.
- Protocole préféré - Il s'agit soit de `Usenet`, soit de `Torrent`, en fonction du protocole de téléchargement que vous préférez.
- Délai Usenet - Défini par le nombre de minutes que vous souhaitez attendre avant que le téléchargement ne commence.
- Délai Torrent - Défini par le nombre de minutes que vous souhaitez attendre avant que le téléchargement ne commence.
- Contourner si qualité supérieure - Contourner le délai lorsque la version a le profil de qualité le plus élevé activé avec le protocole préféré.
- Balises - En attribuant une balise à ce profil de retard, vous pourrez attribuer cette règle à une série donnée.
- Icône de clé à molette - Cela vous permet de modifier le profil de retard.
- Icône plus (<kb>+</kb>) - Créez un nouveau profil de retard

### Utilisations

Certains médias recevront une demi-douzaine de versions différentes de qualité variable dans les heures qui suivent leur sortie, et sans les profils de retard, Sonarr pourrait essayer de toutes les télécharger. Avec les profils de retard, Sonarr peut être configuré pour ignorer les premières heures de sortie.

Les profils de retard sont également utiles si vous souhaitez privilégier un protocole (Usenet ou BitTorrent) par rapport à l'autre. (Voir [Exemple 3](/sonarr/settings/#example-3))

### Fonctionnement des profils de retard

Le minuteur commence dès que Sonarr détecte qu'un épisode a une version disponible. Cette version apparaîtra dans votre file d'attente avec une icône d'horloge pour indiquer qu'elle est en attente de retard.

> L'horloge démarre à partir de l'heure de téléchargement des versions et non à partir du moment où Sonarr les voit.
{.is-info}

Pendant la période de retard, toutes les nouvelles versions disponibles seront notées par Sonarr. Lorsque le minuteur de retard expire, Sonarr téléchargera la seule version qui correspond le mieux à vos préférences de qualité.

La durée du minuteur peut être différente pour Usenet et les torrents. Chaque profil peut être associé à une ou plusieurs balises pour vous permettre de personnaliser les émissions qui ont quel profil. Un profil de retard sans balise est considéré comme le profil par défaut et s'applique à toutes les émissions qui n'ont pas de balise spécifique.

> Les profils de retard commencent à partir de l'heure à laquelle l'indexeur signale que la version a été téléchargée. Cela signifie que tout contenu plus ancien que le nombre de minutes que vous avez défini n'est pas impacté de quelque manière que ce soit par votre profil de retard et sera téléchargé immédiatement. De plus, **toutes les recherches manuelles** de contenu (recherches autres que les flux RSS) ignoreront les paramètres du profil de retard.
{.is-warning}

#### Exemples

- Pour chaque exemple, supposons que l'utilisateur a le profil de qualité suivant actif : HDTV 720p et supérieur sont autorisés, WebDL 720p est la limite de qualité, WebDL 1080p est la qualité la mieux classée.

##### Exemple 1

- Dans cet exemple simple, le profil est défini avec un délai de 120 minutes (deux heures) pour Usenet et Torrent.

- À 23h00, la première version d'un épisode est détectée par Sonarr et elle a été téléchargée à 22h50, le minuteur de 120 minutes commence. À 00h50, Sonarr évaluera toutes les versions qu'il a trouvées au cours des deux dernières heures et téléchargera la meilleure, qui est WebDL 720p.

- À 03h00, une autre version est trouvée, qui est WebDL 720p et a été ajoutée à votre indexeur à 02h46. Un autre minuteur de 120 minutes commence. À 04h46, la meilleure version disponible est téléchargée. Comme la limite de qualité est maintenant atteinte, l'épisode ne peut plus être amélioré et Sonarr cessera de rechercher de nouvelles versions.

- À tout moment, si une version WebDL 1080p est trouvée, elle sera téléchargée immédiatement car c'est la qualité la mieux classée. Si un minuteur de retard est actuellement actif, il sera annulé.

##### Exemple 2

- Cet exemple a des minuteurs différents pour Usenet et les torrents. Supposons un minuteur de 120 minutes pour Usenet et un minuteur de 180 minutes pour BitTorrent.

- À 23h00, la première version d'un épisode est détectée par Sonarr et les deux minuteurs commencent. La version a été ajoutée à l'indexeur à 22h15. À 00h15, Sonarr évaluera toutes les versions et, s'il y a des versions acceptables de Usenet, la meilleure sera téléchargée et les deux minuteurs prendront fin. Sinon, Sonarr attendra jusqu'à 00h15 et téléchargera la meilleure version, quelle que soit sa source.

##### Exemple 3

- Une utilisation courante des profils de retard est de privilégier un protocole par rapport à un autre. Par exemple, vous ne voudrez peut-être télécharger une version BitTorrent que si rien n'a été téléchargé sur Usenet après un certain laps de temps.

- Vous pourriez définir un minuteur de 60 minutes pour BitTorrent et un minuteur de 0 minute pour Usenet.

- Si la première version détectée provient d'Usenet, Sonarr la téléchargera immédiatement.

- Si la première version provient de BitTorrent, Sonarr définira un minuteur de 60 minutes. Si une version de Usenet admissible est détectée pendant ce minuteur, la version BitTorrent sera ignorée et la version Usenet sera téléchargée.

## Profils de sortie

- Toutes les versions ne sont pas créées égales, chaque groupe de versions a sa propre façon d'emballer et d'encoder son matériel. Ici, vous pourrez sélectionner les versions préférées que vous recherchez.

> Vous pouvez utiliser des expressions régulières (sensible à la casse par défaut) dans les valeurs des mots `Doit contenir`, `Ne doit pas contenir` et `Préféré`. Les expressions régulières doivent être de la forme `/expression-régulière-ici/i`
{.is-info}

- Nom - Sélectionnez un nom **UNIQUE** pour le profil de sortie que vous créez.
- Activer le profil - Activez ou désactivez ce profil donné.
- Doit contenir - La version doit contenir au moins un de ces termes (insensible à la casse).
- Ne doit pas contenir - La version sera rejetée si elle contient un ou plusieurs des termes (insensible à la casse).
- Préféré - Ici, vous pouvez sélectionner un terme donné et lui attribuer un score.
  - Disons que vous recherchez des versions avec un regroupement spécifique de mots. Disons que vous voulez dire à Sonarr que vous voulez des Repacks ou des Propers plutôt que des versions régulières. Ici, vous mettrez le mot Repack dans l'un des champs et lui donnerez une valeur (disons 100), mais vous recherchez également une audio DTS-HD, vous le mettrez également et lui donnerez également un score (disons encore 100). Lorsque Sonarr parcourt toutes les versions du flux RSS et qu'il trouve une version qui contient à la fois Repack et DTS-HD, cela lui donnera un score de 200. Ce qui est beaucoup plus élevé que toutes les autres versions qui n'ont aucun de ces mots. Cela indique à Sonarr que cette version a un score plus élevé et elle sera la première à être choisie pour le téléchargement.
- Inclure les préférences lors du renommage - Lors de l'utilisation de la balise {Preferred Words} dans le schéma de nommage.
- Indexeur - Spécifiez à quel indexeur le profil s'applique.

> Cela est utile si vous ne souhaitez que des versions spécifiques d'un indexeur/traqueur donné.
{.is-info}

- Balises - En attribuant une balise à ce profil de sortie, vous pourrez attribuer cette règle à une série donnée. Si vous laissez ce champ vide, ces règles s'appliqueront à toutes les séries.

- [TRaSH maintient une liste des profils de sortie WEB-DL](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/)
- [Profils d'anime TRaSH](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx-Anime/)

# Qualité

## Signification de la table de qualité

- Qualité - Le nom de qualité de la scène (codé en dur)
- Titre - Le nom de la qualité dans l'interface utilisateur (configurable)
- Mégaoctets par heure - Auto-explicatif
- Limite de taille - Auto-explicatif
- Min - Le nombre minimum de mégaoctets par minute (Mo/min) qu'une qualité peut avoir.
- Max - Le nombre maximum de mégaoctets par minute (Mo/min) qu'une qualité peut avoir.

## Qualités définies

- In order to use Sonarr with Usenet, you will need a Usenet provider and a Usenet client software. Sonarr supports various Usenet clients such as SABnzbd, NZBGet, and nzb360.
- After setting up your Usenet client, you will need to configure it in Sonarr. Go to Settings > Download Clients and click on the "+" button to add a new client.
- Select your Usenet client from the list and enter the required information such as the host, port, API key, and category. You can find these details in your Usenet client settings.
- Once you have added your Usenet client, Sonarr will be able to send download requests to it and import the downloaded files into your media library.

## Torrents

- To use Sonarr with torrents, you will need a torrent client software such as qBittorrent, Deluge, or Transmission. Sonarr also supports remote torrent clients like rTorrent and ruTorrent.
- After setting up your torrent client, you will need to configure it in Sonarr. Go to Settings > Download Clients and click on the "+" button to add a new client.
- Select your torrent client from the list and enter the required information such as the host, port, username, password, and category. You can find these details in your torrent client settings.
- Once you have added your torrent client, Sonarr will be able to send download requests to it and import the downloaded files into your media library.

## Completed Download Handling

- Sonarr can automatically handle completed downloads by moving or copying them to the appropriate location in your media library.
- To enable completed download handling, go to Settings > Download Clients and click on the wrench icon next to your download client.
- In the settings, enable the "Completed Download Handling" option and configure the options according to your preferences. You can choose to move or copy the files, set the destination folder, and specify actions to be taken after the import.
- Sonarr will monitor the download client for completed downloads and automatically import them into your media library.

## Failed Download Handling

- Sonarr can handle failed downloads by automatically searching for alternative releases and re-downloading them.
- To enable failed download handling, go to Settings > Download Clients and click on the wrench icon next to your download client.
- In the settings, enable the "Failed Download Handling" option and configure the options according to your preferences. You can choose to search for alternative releases, set the maximum number of retries, and specify the delay between retries.
- Sonarr will automatically search for alternative releases and re-download them if the initial download fails.

## Blackhole

- Sonarr also supports a "Blackhole" download method, which allows you to manually download files and place them in a specific folder monitored by Sonarr.
- To use the Blackhole method, go to Settings > Download Clients and click on the "+" button to add a new client.
- Select "Blackhole" from the list and enter the path to the folder where you want to place the downloaded files.
- Once you have added the Blackhole client, you can manually download files and place them in the specified folder. Sonarr will detect the files and import them into your media library.

## Multiple Download Clients

- Sonarr supports multiple download clients, allowing you to use different clients for different purposes.
- To add multiple download clients, go to Settings > Download Clients and click on the "+" button to add a new client.
- Configure each download client with the required information and specify the priority for each client.
- Sonarr will use the highest priority download client that is available for each download request.

## Testing Download Clients

- Sonarr provides a built-in test feature that allows you to test the connection to your download clients.
- To test a download client, go to Settings > Download Clients and click on the wrench icon next to the client you want to test.
- In the settings, click on the "Test" button to test the connection.
- Sonarr will attempt to connect to the download client and display the test results.

## Download Client Priority

- Sonarr allows you to set the priority of your download clients, which determines the order in which they are used for download requests.
- To set the download client priority, go to Settings > Download Clients and click on the wrench icon next to each client.
- In the settings, enter a number for the priority, where a lower number indicates a higher priority.
- Sonarr will use the download client with the highest priority that is available for each download request.

## Download Client Settings

- Each download client has its own specific settings that can be configured in Sonarr.
- To configure the settings for a download client, go to Settings > Download Clients and click on the wrench icon next to the client.
- In the settings, you can configure options such as the host, port, username, password, and other client-specific settings.
- Make sure to enter the correct settings for your download client to ensure proper communication with Sonarr.

## More Information

- For more information on supported download clients and their specific settings, refer to the [Supported Download Clients](/sonarr/supported#download-clients) page.

- Sonarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configurée dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Sonarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il effectue cette surveillance via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Sonarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Sonarr.
- Sonarr analysera cet emplacement de fichier terminé à la recherche de fichiers que Sonarr peut utiliser. Il analysera le nom du fichier pour le faire correspondre au média demandé. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens physiques et les déplacements atomiques, Sonarr effectuera une copie du fichier, puis le supprimera de la source, ce qui est intensif en termes d'E/S.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Sonarr, les fichiers restants du téléchargement seront envoyés à la corbeille ou au recyclage via une demande à votre client pour supprimer le fichier.

## BitTorrent

- Sonarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configurée dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Sonarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de les partager. Lorsque les fichiers sont importés dans votre dossier multimédia, Sonarr tentera de créer un lien physique vers le fichier s'il est pris en charge par votre configuration, sinon il effectuera une copie (utilisant un double espace) si les liens physiques ne sont pas pris en charge.
- Les liens physiques sont activés par défaut. [Un lien physique ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être identiques pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien physique échoue ou si votre configuration ne prend pas en charge les liens physiques, Sonarr effectuera une copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres, Sonarr demandera au client torrent de supprimer le fichier et le torrent d'origine, mais cela ne se produira que si le client signale que le partage est terminé, que le torrent est dans la même catégorie (c'est-à-dire qu'il n'utilise pas de catégorie après l'importation), que l'objectif de partage atteint est pris en charge par Sonarr et que le torrent est en pause (arrêté).

## Clients de téléchargement

Cliquez sur `Paramètres` => `Clients de téléchargement`, puis cliquez sur le bouton <kb>+</kb> pour ajouter un nouveau client de téléchargement. Votre client de téléchargement doit déjà être configuré et en cours d'exécution.

### Clients de téléchargement pris en charge

- Une liste des clients de téléchargement pris en charge se trouve à la page [Informations supplémentaires (Pris en charge)](/sonarr/supported#download-clients)

Sélectionnez le client de téléchargement que vous souhaitez ajouter, et une boîte contextuelle s'ouvrira pour saisir les détails de connexion. Ces détails sont similaires pour la plupart des clients. Certains vous demanderont un nom d'utilisateur ou un mot de passe, d'autres vous demanderont si vous souhaitez ajouter de nouveaux téléchargements en pause ou en démarrage, etc.

### Paramètres du client Usenet

- Nom - Le nom du client de téléchargement dans Sonarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement ; il s'agit généralement du port de l'interface web
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base de l'URL - Ajouter un préfixe à l'URL ; cela est généralement nécessaire pour les serveurs proxy inverses.
- Clé API - la clé API pour s'authentifier auprès de votre client
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client (généralement pas nécessaire)
- Catégorie - la catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Priorité récente - priorité du client de téléchargement pour les médias récemment publiés
- Priorité plus ancienne - priorité du client de téléchargement pour les médias publiés il y a longtemps
- (Option avancée) Priorité du client - Priorité du client de téléchargement. Round-Robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse
- Gestion des téléchargements terminés
  - Supprimer (Paramètre par client) - Supprimer les téléchargements terminés lorsque ceux-ci sont terminés (usenet) ou arrêtés/terminés (torrents). Voir [Gestion des téléchargements terminés pour plus de détails](#completed-download-handling)

### Paramètres du client Torrent

- Nom - Le nom du client de téléchargement dans Sonarr
- Activer - Activer ce client de téléchargement
- Hôte - L'URL de votre client de téléchargement
- Port - Le port de votre client de téléchargement
- Utiliser SSL - Utiliser une connexion sécurisée avec votre client de téléchargement. Veuillez noter cette erreur courante.
- (Option avancée) Base de l'URL - Ajouter un préfixe à l'URL ; cela est généralement nécessaire pour les serveurs proxy inverses.
- Nom d'utilisateur - le nom d'utilisateur pour s'authentifier auprès de votre client
- Mot de passe - le mot de passe pour s'authentifier auprès de votre client
- Catégorie - la catégorie dans votre client de téléchargement que \*Arr utilisera. Pour éviter que des téléchargements non liés n'apparaissent dans l'activité, il est fortement recommandé de définir une catégorie.
- Catégorie après importation - la catégorie à définir après le téléchargement et l'importation de la version. Veuillez noter que cela désactive la suppression des téléchargements terminés.
- Priorité récente - priorité du client de téléchargement pour les médias récemment publiés
- Priorité plus ancienne - priorité du client de téléchargement pour les médias publiés il y a longtemps
- État initial - État initial des torrents (uniquement pour Qbittorrent : la mise en contournement forcée contourne tous les seuils de partage)
- (Option avancée) Priorité du client - Priorité du client de téléchargement. Round-Robin est utilisé pour les clients du même type (torrent/usenet) qui ont la même priorité. 1 est la priorité la plus élevée et 50 est la priorité la plus basse
- Gestion des téléchargements terminés
  - Supprimer (Paramètre par client) - Supprimer les téléchargements terminés lorsque ceux-ci sont terminés (usenet) ou arrêtés/terminés (torrents). Voir [Gestion des téléchargements terminés pour plus de détails](#completed-download-handling)
    - Pour les torrents, cela nécessite que votre client de téléchargement se mette en pause une fois les objectifs de partage atteints. Cela nécessite également que les objectifs de partage soient pris en charge par Sonarr, comme indiqué dans le tableau ci-dessous. Les torrents doivent également rester dans la même catégorie.

### Compatibilité de suppression des téléchargements terminés du client Torrent

- Sonarr est uniquement capable de définir le ratio de partage/temps sur les clients qui prennent en charge le réglage de cette valeur via leur API lors de l'ajout du torrent. Les objectifs de partage peuvent être définis globalement dans le client lui-même ou par tracker dans les paramètres de \*Arr pour chaque indexeur. Consultez le tableau ci-dessous pour connaître la compatibilité du client.

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

> ![Limite d'inactivité](https://img.shields.io/badge/Pris%20en%20charge-Limite%20d'inactivité*-blue) - Transmission dispose d'une vérification du temps d'inactivité en interne, mais Sonarr la compare avec le temps de partage si la limite d'inactivité est définie pour chaque torrent. Cela est fait en contournement des limitations de l'API de Transmission.{.is-info}

## Gestion des téléchargements terminés

- La gestion des téléchargements terminés est la façon dont Sonarr importe les médias de votre client de téléchargement vers vos dossiers de séries. De nombreux problèmes courants sont liés à de mauvais chemins Docker et/ou à d'autres problèmes de permissions Docker.

- (Paramètre global avancé) Activer - Importer automatiquement les téléchargements terminés du client de téléchargement
- (Paramètre par client) Supprimer - Supprimer les téléchargements terminés lorsque ceux-ci sont terminés (usenet) ou arrêtés/terminés (torrents)
  - Pour les torrents, cela nécessite que votre client de téléchargement se mette en pause une fois les objectifs de partage atteints. Cela nécessite également que les objectifs de partage soient pris en charge par Sonarr, comme indiqué dans le tableau ci-dessus. Les torrents doivent également rester dans la même catégorie.

### Supprimer les téléchargements terminés

- Sonarr enverra une demande de téléchargement à votre client et l'associera à un label ou à une catégorie que vous avez configurée dans les paramètres du client de téléchargement.
- Sonarr surveillera les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il effectue cette surveillance via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Sonarr connaîtra l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia.
- Sonarr analysera cet emplacement de fichier terminé à la recherche de fichiers vidéo. Il analysera le nom du fichier vidéo pour le faire correspondre à un épisode. S'il peut le faire, il renommera le fichier selon vos spécifications et le déplacera vers le dossier de bibliothèque assigné.
- Les fichiers restants du téléchargement seront envoyés à la corbeille ou au recyclage.

Si vous téléchargez à l'aide d'un client BitTorrent, le processus est légèrement différent :

- Les fichiers terminés sont laissés à leur emplacement d'origine pour vous permettre de les partager. Lorsque les fichiers sont importés dans votre dossier de bibliothèque assigné, Sonarr tentera de créer un lien physique vers le fichier ou effectuera une copie (utilisant un double espace) en cas d'absence de prise en charge des liens physiques.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres, Sonarr demandera au client torrent de supprimer le fichier et le torrent d'origine, mais cela ne se produira que si le client signale que le partage est terminé, que le torrent est dans la même catégorie (c'est-à-dire qu'il n'utilise pas de catégorie après l'importation), que l'objectif de partage atteint est pris en charge par Sonarr et que le torrent est en pause (arrêté).

### Gestion des téléchargements échoués

- La gestion des téléchargements échoués est uniquement compatible avec SABnzbd et NZBGet.
- La gestion des téléchargements échoués ne s'applique pas aux torrents et il n'est pas prévu d'ajouter une telle fonctionnalité.

- Plusieurs composants composent le processus de gestion des téléchargements échoués :

- Vérification du téléchargeur :
  - File d'attente - Vérifiez la file d'attente de votre téléchargeur pour les versions protégées par mot de passe (cryptées) marquées comme échec
  - Historique - Vérifiez l'historique de votre téléchargeur pour les échecs (par exemple, pas assez de blocs pour réparer ou échec de l'extraction)
- Lorsque Sonarr trouve un téléchargement échoué, il commence à les traiter et fait quelques choses :
  - Ajoute un événement d'échec à l'historique de Sonarr
  - Supprime le téléchargement échoué du client de téléchargement pour libérer de l'espace et effacer les fichiers téléchargés (facultatif)
  - Commence à rechercher un fichier de remplacement (facultatif)
  - La liste de blocage (anciennement appelée "liste noire") permet de sauter automatiquement les fichiers NZB lorsqu'ils échouent, ce qui signifie que l'NZB ne sera jamais téléchargé automatiquement par Sonarr (vous pouvez toujours forcer le téléchargement via une recherche manuelle).
  - Il existe 2 options avancées (sur la page des paramètres du "Client de téléchargement") qui contrôlent le comportement des téléchargements échoués dans Sonarr, à l'heure actuelle, elles sont toutes activées par défaut.

- Redownload - Contrôle si Sonarr recherchera ou non le même fichier après un échec
- (Option avancée) Supprimer - Indique si le téléchargement doit être automatiquement supprimé du client de téléchargement lorsque l'échec est détecté

## Mappages de chemin distant

- Le mappage de chemin distant agit comme une recherche/remplacement de chemin distant par chemin local. Cela est principalement utilisé pour les configurations locales/à distance fusionnées utilisant mergerfs ou similaires, ou est utilisé lorsque l'application et le client de téléchargement ne sont pas sur le même serveur.
- Un mappage de chemin distant est utilisé lorsque votre client de téléchargement signale un chemin pour les données terminées soit sur un autre serveur, soit d'une manière que \*Arr n'adresse pas ce dossier.
- Généralement, un mappage de chemin distant n'est nécessaire que si votre client de téléchargement est sur Linux lorsque \*Arr est sur Windows ou vice versa. Un mappage de chemin distant peut également être nécessaire si vous mélangez des clients Docker et natifs ou si vous utilisez un serveur distant.
- Un mappage de chemin distant est une recherche/remplacement DUMB (où il trouve la valeur DISTANTE, la remplace par la valeur LOCALE pour l'hôte spécifié).
- Si le message d'erreur concernant un mauvais chemin ne contient pas la valeur REMPLACÉE, alors le mappage de chemin ne fonctionne pas comme vous le souhaitez. La solution typique consiste à ajouter et supprimer le mappage.
- [Consultez le tutoriel de TRaSH pour plus d'informations sur le mappage de chemin distant](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Si \*Arr et votre client de téléchargement sont tous deux des conteneurs Docker, il est rare qu'un mappage de chemin distant soit nécessaire. Il est recommandé de [consulter le guide Docker](/docker-guide) et/ou de [suivre le tutoriel de TRaSH](https://trash-guides.info/hardlinks){.is-info}

# Listes d'importation

> Des informations sur les types de listes pris en charge peuvent être trouvées sur la page [Informations supplémentaires (Pris en charge)](/sonarr/supported#lists) pour cette section
{.is-info}

## Listes

- Les listes d'importation font partie de Sonarr et vous permettent de suivre un créateur de liste donné. Disons que vous suivez un créateur de liste donné sur Trakt/TMDb et que vous aimez vraiment leur section ArrowVerse Collection et que vous voulez regarder toutes les émissions de leur liste. Vous regardez dans votre Sonarr et réalisez que vous n'avez pas ces séries. Eh bien, au lieu de les rechercher une par une et de les ajouter, puis de rechercher ces éléments dans vos indexeurs. Vous pouvez le faire tout en une fois avec une liste. Les listes peuvent être configurées pour importer toutes les séries de la liste du conservateur ainsi que pour attribuer automatiquement un profil de qualité, ajouter automatiquement et surveiller automatiquement cette série.

- ATTENTION : Si les listes sont mal faites, elles vont absolument détruire votre bibliothèque avec une tonne de contenu que vous n'avez aucune intention de regarder. Alors assurez-vous de ce que vous importez avant de cliquer sur Enregistrer. C'est-à-dire, regardez physiquement la liste avant même d'aller dans Sonarr.

- Ici, vous pouvez sélectionner le bouton <kb>+</kb> pour ouvrir une nouvelle fenêtre contextuelle
- Dans cette nouvelle fenêtre, vous avez plusieurs options différentes pour configurer votre liste à partir de nombreux fournisseurs de listes différents. Comme indiqué précédemment, soyez prudent lorsque vous utilisez des listes. Il est fortement recommandé de ne pas sélectionner le bouton Rechercher lors de l'ajout avant d'être absolument sûr que la liste que vous sélectionnez/configurez ajoute les séries que vous recherchez.
- Une fois que vous avez sélectionné le fournisseur de liste à partir duquel vous souhaitez extraire (comme IMDb ou Trakt), une nouvelle fenêtre s'ouvre.
La plupart des paramètres de liste sont assez explicites, certaines listes vous demandent de vous authentifier auprès du fournisseur, comme Trakt (ce qui nécessite d'avoir un compte sur Trakt.tv)

- Importation de la liste d'exclusion - Cela vous permet de nettoyer votre liste de séries que vous ne souhaitez plus voir. Par exemple, si votre liste contient une série dans une langue étrangère et qu'il est peu probable que vous la trouviez un jour dans votre langue maternelle et que vous ne souhaitez pas la regarder avec des sous-titres, vous pouvez exclure cette série pour qu'elle ne soit pas ajoutée à l'avenir. Cependant, dans la section d'exclusion de la liste, vous pouvez la réintégrer pour qu'elle soit lue dans votre bibliothèque lorsque la liste est exécutée à nouveau.

# Connexion

> Vous trouverez des informations sur les types de connexion pris en charge sur la page [Plus d'informations (Pris en charge)](/sonarr/supported#notifications) de cette section
{.is-info}

## Connexions

- Les connexions déterminent comment Sonarr communique avec le monde extérieur.

- En appuyant sur le bouton <kb>+</kb>, une nouvelle fenêtre s'ouvrira vous permettant de configurer de nombreux points de terminaison différents.

- Une liste des notifications et connexions prises en charge est disponible sur la page [Plus d'informations (Pris en charge)](/sonarr/supported#notifications)

## Déclencheurs de connexion

- Sur Capture - Recevez une notification lorsque des épisodes sont disponibles en téléchargement et ont été envoyés à un client de téléchargement.
- Sur Importation - {Anciennement appelé Sur Téléchargement} Recevez une notification lorsque les épisodes sont importés avec succès.
- Sur Mise à niveau - Recevez une notification lorsque les épisodes sont améliorés en termes de qualité.
- Sur Renommage - Recevez une notification lorsque les épisodes sont renommés.
- Sur Suppression de série - Recevez une notification lorsque des séries sont supprimées.
- Sur Suppression de fichier d'épisode - Recevez une notification lorsque des fichiers d'épisodes sont supprimés.
- Sur Suppression de fichier d'épisode pour mise à niveau - Recevez une notification lorsque des fichiers d'épisodes sont supprimés pour une mise à niveau.
- Sur Problème de santé - Recevez une notification en cas d'échec de la vérification de santé.
  - Inclure les avertissements de santé - Recevez une notification en cas d'avertissements de santé en plus des erreurs.
- Sur Mise à jour de l'application - Recevez une notification lorsque Sonarr est mis à jour vers une nouvelle version.

# Métadonnées

## Métadonnées

> Vous trouverez des informations sur les consommateurs de métadonnées pris en charge sur la page [Plus d'informations (Pris en charge)](/sonarr/supported#metadata) de cette section
{.is-info}

- Ici, vous pouvez sélectionner le type de métadonnées qui sera utilisé par votre lecteur multimédia.

- Kodi sera l'une des options les plus couramment utilisées ici si c'est le logiciel que vous utilisez. Cela permettra à Sonarr de créer un fichier NFO ainsi que des affiches de films associées à être récupérées dans votre lecteur.

# Étiquettes

- La section des étiquettes dans Sonarr est utilisée pour lier différents aspects de Sonarr.
- Les étiquettes sont particulièrement utiles pour :
  - Les profils de retard
  - Les profils de publication
  - Les indexeurs
- Les étiquettes peuvent être utilisées pour lier des profils de retard, des profils de publication, des indexeurs et des séries entre eux.
- Par exemple :
  - Vous voulez qu'un indexeur spécifique soit utilisé pour une série spécifique. Vous créeriez une étiquette et assigneriez la série et l'indexeur à cette étiquette.
  - Vous voulez qu'un profil de publication spécifique n'utilise qu'un profil de retard spécifique. Vous créeriez une étiquette et assigneriez le profil de publication et le profil de retard à cette étiquette.

> Une série utilisera à la fois les indexeurs ayant des étiquettes correspondantes et les indexeurs n'ayant aucune étiquette.
{.is-warning}

> Remarque : Les étiquettes n'influencent pas les mots "Doit contenir", "Ne doit pas contenir", les mots "Préféré" ou tout autre aspect non mentionné ci-dessus.
{.is-info}

# Général

## Hôte

- Adresse de liaison - Adresse IP4 valide ou '*' pour toutes les interfaces
  - 0.0.0.0 ou `*` - toutes les adresses peuvent se connecter
  - 127.0.0.1 ou localhost - seules les applications en local peuvent se connecter
  - Toute autre IP (par exemple 1.2.3.4) - seule cette IP (1.2.3.4) peut se connecter
- Numéro de port - Le numéro de port que vous souhaitez utiliser pour accéder à l'interface web de Sonarr

> Remarque : Si vous utilisez Docker, ne modifiez pas ce paramètre.
{.is-warning}

- Base de l'URL - Pour prendre en charge un proxy inverse, la valeur par défaut est vide

> Remarque : Si vous utilisez un proxy inverse (par exemple : mondomaine.com/sonarr), vous devez entrer '/sonarr' pour la base de l'URL.
{.is-info}

- Nom de l'instance - Nom de l'instance dans l'onglet et pour le nom de l'application Syslog

> Si vous exécutez plusieurs instances, cela ajoutera le nom de l'instance au nom de l'onglet du navigateur web. {.is-info}

- Activer SSL - Si vous disposez de certificats SSL et que vous souhaitez sécuriser les communications vers et depuis votre Sonarr, activez cette option.

> Remarque : N'utilisez pas cette option à moins de savoir ce que vous faites.
{.is-warning}

## Sécurité

- Authentification - Comment souhaitez-vous vous authentifier pour accéder à votre instance Sonarr
  - Aucune - Vous n'avez pas besoin d'authentification pour accéder à votre Sonarr. Cela s'applique généralement si vous êtes le seul utilisateur de votre réseau, si personne sur votre réseau ne souhaite accéder à votre Sonarr ou si votre Sonarr n'est pas exposé sur le web.
  - Basique (fenêtre contextuelle du navigateur) - Cette option affiche une petite fenêtre contextuelle vous permettant de saisir un nom d'utilisateur et un mot de passe lorsque vous accédez à votre Sonarr.
  - Formulaire (page de connexion) - Cette option affiche une page de connexion familière, similaire à celles des autres sites web, vous permettant de vous connecter à votre Sonarr.
- Clé API - C'est ainsi que d'autres programmes peuvent communiquer avec Sonarr ou faire communiquer Sonarr avec d'autres programmes. Si cette clé est donnée à la mauvaise personne ayant accès, elle pourrait faire toutes sortes de choses avec votre bibliothèque. C'est pourquoi la clé API est masquée dans les journaux.
- Validation du certificat - Modifiez le niveau de validation du certificat HTTPS
  - Activé - Valider tous les certificats HTTPS (recommandé)
  - Désactivé pour les adresses locales - Ne pas valider les certificats HTTPS pour localhost et le réseau local (LAN)
  - Désactivé - Ne pas valider les certificats HTTPS

## Proxy

- Proxy - Cette option vous permet de faire passer les informations que Sonarr récupère et recherche par un proxy. Cela peut être utile si vous vous trouvez dans un pays qui n'autorise pas le téléchargement de fichiers Torrent.

- Utiliser un proxy - Activer pour utiliser un proxy
- Type de proxy - Sélectionnez votre type de proxy (HTTPS, Socks4 ou Socks5)
- Nom d'hôte - Entrez le nom d'hôte de votre proxy (ne pas inclure http/https ou tout autre protocole)
- Port - Entrez le port de votre proxy
- Nom d'utilisateur - Entrez le nom d'utilisateur de votre proxy, le cas échéant
- Mot de passe - Entrez le mot de passe de votre proxy, le cas échéant
- Adresses ignorées - Entrez une liste d'adresses séparées par des virgules qui contourneront le proxy
- Ignorer le proxy pour les adresses locales - Cochez cette case pour contourner le proxy pour les adresses locales. Les requêtes locales sont identifiées par l'absence d'un point (.) dans l'URI, comme <http://serveurweb/>, ou pour accéder au serveur local, y compris <http://localhost>, <http://loopback> ou <http://127.0.0.1>. Lorsque cette option n'est pas cochée, toutes les requêtes Internet sont effectuées via le serveur proxy.

## Journalisation

- Niveau de journalisation - L'un des outils de dépannage les plus utiles
  - Info - C'est la façon la plus basique dont Sonarr collecte des informations, cela inclura un minimum d'informations dans les journaux. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement et d'information.
  - Débogage - Le débogage inclura toutes les informations incluses dans Info ainsi que des informations supplémentaires qui peuvent être utiles. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement, d'information et de débogage.
  - Trace - La journalisation la plus avancée et détaillée de Sonarr, Trace inclura toutes les informations collectées par Info et Debug, et plus encore. C'est le type de journal le plus couramment demandé lors du dépannage sur Discord ou Reddit. Si vous avez besoin d'aide, veuillez sélectionner votre journal en mode Trace et refaire la tâche qui vous posait problème pour capturer le journal. Ce fichier journal contient des entrées fatales, d'erreur, d'avertissement, d'information, de débogage et de trace.

## Analyse

- Analyse - Envoyer des informations d'utilisation et d'erreurs anonymes aux serveurs de Sonarr (SkyHook). Cela inclut des informations sur votre navigateur, les pages de l'interface web de Sonarr que vous utilisez, les rapports d'erreurs ainsi que la version du système d'exploitation et d'exécution. Nous utiliserons ces informations pour hiérarchiser les fonctionnalités et les corrections de bugs.

## Mises à jour

- (Option avancée) Branche - Il s'agit de la branche de Sonarr que vous utilisez.
  - [Veuillez consulter cette entrée de FAQ pour plus d'informations](/sonarr/faq#how-do-i-update-sonarr)
- Automatique - Téléchargez et installez automatiquement les mises à jour. Vous pourrez toujours installer depuis Système : Mises à jour. Remarque : Les utilisateurs de Windows sont toujours mis à jour automatiquement.
- Mécanisme - Utilisez le programme de mise à jour intégré de Sonarr ou un script
  - Intégré - Utilisez le programme de mise à jour intégré de Sonarr
  - Script - Demandez à Sonarr d'exécuter le script de mise à jour
  - Docker - Ne mettez pas à jour Sonarr depuis l'intérieur du Docker, mais téléchargez une nouvelle image avec la nouvelle mise à jour
  - Apt - Défini par le paquet Debian/Ubuntu lorsque la mise à jour est gérée exclusivement via Apt
- Script - Visible uniquement lorsque le mécanisme est défini sur Script - Chemin vers le script de mise à jour
- Processus de mise à jour - Sonarr téléchargera le fichier de mise à jour, vérifiera son intégrité, l'extrairea dans un emplacement temporaire et appellera la méthode choisie. Le processus de mise à jour sera exécuté avec le même utilisateur que celui utilisé pour exécuter Sonarr, il aura besoin des autorisations pour mettre à jour les fichiers de Sonarr ainsi que pour arrêter/démarrer Sonarr.
- Intégré - La méthode intégrée sauvegardera les fichiers et les paramètres de Sonarr, arrêtera Sonarr, mettra à jour l'installation et démarrera Sonarr. Si votre système ne peut pas gérer l'arrêt de Sonarr et tentera de le redémarrer automatiquement, il est préférable d'utiliser un script. En cas d'échec, la version précédente de Sonarr sera redémarrée.
- Script - Le script doit gérer la même chose que le programme de mise à jour intégré. Si vous devez gérer l'arrêt et le démarrage des services (upstart/launchd/etc), vous devrez le faire ici.

## Sauvegardes

- La section des sauvegardes vous permet de définir comment Sonarr doit gérer les sauvegardes.

- Dossier - Cela vous permet de sélectionner l'emplacement de sauvegarde. Dans Docker, vous serez limité à ce que vous autorisez le conteneur à voir. Les chemins sont relatifs au dossier appdata ; si nécessaire, vous pouvez définir un chemin absolu pour sauvegarder en dehors du dossier appdata.
- Intervalle - À quelle fréquence souhaitez-vous que Sonarr effectue une sauvegarde ?
- Rétention - Combien de temps souhaitez-vous que Sonarr conserve chaque sauvegarde ? Après la création d'une nouvelle sauvegarde, la plus ancienne sera supprimée.

# Interface utilisateur

## Calendrier

- Premier jour de la semaine - Ici, vous pouvez sélectionner quel jour vous pensez être le premier jour de la semaine.
- En-tête de colonne de la semaine - Ici, vous pouvez sélectionner l'en-tête des colonnes.

## Dates

- Format de date court - Comment souhaitez-vous que Sonarr affiche les dates courtes ?
- Format de date long - Comment souhaitez-vous que Sonarr affiche les dates au format long ?
- Format de l'heure - Souhaitez-vous un format 12h ou 24h ?
- Afficher les dates relatives - Souhaitez-vous que Sonarr affiche des dates relatives (Aujourd'hui/Hier/etc) ou des dates absolues ?

## Style

- Activer le mode pour les personnes atteintes de daltonisme - Style modifié pour permettre aux personnes atteintes de daltonisme de mieux distinguer les informations codées par couleur.