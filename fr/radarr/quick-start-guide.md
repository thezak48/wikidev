---
title: Guide de démarrage rapide de Radarr
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, démarrage rapide
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Guide de configuration rapide](#guide-de-configuration-rapide)
- [Démarrage](#démarrage)
- [Gestion des médias](#gestion-des-médias)
  - [Nom des films](#nom-des-films)
  - [Importation](#importation)
  - [Gestion des fichiers](#gestion-des-fichiers)
  - [Dossiers racine](#dossiers-racine)
- [Profils](#profils)
- [Qualité](#qualité)
- [Indexeurs](#indexeurs)
- [Clients de téléchargement](#clients-de-téléchargement)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Comment importer votre bibliothèque multimédia organisée existante](#comment-importer-votre-bibliothèque-multimédia-organisée-existante)
  - [Importer des films](#importer-des-films)
  - [Importation de médias existants](#importation-de-médias-existants)
    - [Aucune correspondance trouvée](#aucune-correspondance-trouvée)
    - [Corriger le nom de dossier défectueux après l'importation](#corriger-le-nom-de-dossier-défectueux-après-limportation)
  - [Comment ajouter un film](#comment-ajouter-un-film)

# Guide de configuration rapide

> Cette page est encore en cours de réalisation et n'est pas complète. Les contributions sont les bienvenues.

> Pour une description plus détaillée de tous les paramètres, consultez [Radarr => Paramètres](/radarr/settings).
{.is-info}

Dans ce guide, nous allons essayer d'expliquer la configuration de base que vous devez effectuer pour commencer avec Radarr. Nous allons passer en revue certaines options que vous pouvez voir à l'écran. Si vous souhaitez approfondir ces options, veuillez consulter la page appropriée dans la FAQ et la documentation pour une explication complète.

> Veuillez noter que dans les captures d'écran et les paramètres de l'interface utilisateur en `orange`, il s'agit d'options avancées. Vous devrez cliquer sur `Afficher les options avancées` en haut de la page pour les rendre visibles.
{.is-warning}

# Démarrage

Après l'installation et le démarrage, ouvrez un navigateur et accédez à `http://{votre_ip_ici}:7878`

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# Gestion des médias

Tout d'abord, nous allons jeter un coup d'œil aux paramètres de `Gestion des médias` où nous pouvons configurer nos préférences de nommage et de gestion des fichiers.

`Paramètres` => `Gestion des médias`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## Nom des films

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. Activer/Désactiver le renommage de vos films (au lieu de laisser les noms tels qu'ils sont actuellement ou tels qu'ils étaient lors de leur téléchargement).
2. Si vous souhaitez remplacer ou supprimer les caractères illégaux (`\ / : * ? " < > | ~ # % & + { }`).
3. Ce paramètre indique comment Radarr gère les deux-points dans le nom du film.
4. Vous sélectionnerez ici la convention de nommage pour les fichiers de film réels.
5. *(Option avancée) C'est ici que vous définirez la convention de nommage pour le dossier contenant le fichier vidéo.*

> Si vous souhaitez une convention de nommage recommandée et des exemples, consultez [Schémas de nommage recommandés de TRaSH](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/).
{.is-info}

## Importation

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(Option avancée) Activer `Utiliser des liens durs au lieu de la copie` pour plus d'informations sur la manière et la raison d'utiliser des liens durs, consultez [Guide des liens durs de TRaSH](https://trash-guides.info/hardlinks).
1. *(Option avancée) Importer les fichiers supplémentaires correspondants (sous-titres, nfo, etc.) après l'importation d'un fichier.*

## Gestion des fichiers

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. Les films supprimés du disque sont automatiquement désactivés dans Radarr.
    - Vous voudrez peut-être supprimer un film mais ne pas vouloir que Radarr le télécharge à nouveau. Vous utiliserez cette option.
1. *(Option avancée) Désignez un emplacement où les fichiers supprimés doivent être stockés (au cas où vous voudriez les récupérer avant que la corbeille ne soit vidée).*
1. *(Option avancée) Il s'agit de l'ancienneté d'un fichier donné avant qu'il ne soit supprimé définitivement.*

## Dossiers racine

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

Ici, nous ajouterons le dossier racine que Radarr utilisera pour importer votre bibliothèque multimédia organisée existante et où Radarr importera (copie/liens durs/déplacement) vos médias après que votre client de téléchargement les ait téléchargés.

> \* Non-Windows : Si vous utilisez un montage NFS, assurez-vous que `nolock` est activé.
> \* Si vous utilisez un montage SMB, assurez-vous que `nobrl` est activé.
{.is-warning}

> **L'utilisateur et le groupe que vous avez configurés pour exécuter Radarr doivent avoir un accès en lecture et en écriture à cet emplacement.** {.is-info}

> Votre client de téléchargement télécharge dans un dossier de téléchargement et Radarr l'importe dans votre dossier multimédia (destination finale) que votre serveur multimédia utilise.
{.is-info}

> **Votre dossier de téléchargement et votre dossier de médias (bibliothèque / racine) ne peuvent pas être situés au même endroit.** {.is-danger}

N'oubliez pas d'enregistrer vos modifications.

# Profils

`Paramètres` => `Profils`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

Ici, vous pourrez configurer des profils pour la qualité, la langue préférée et le score de format personnalisé d'un film que vous souhaitez télécharger.

Nous vous recommandons de créer vos propres profils et de sélectionner uniquement les sources de qualité et les langues que vous souhaitez réellement.

Pour plus d'informations sur les titres et les langues étrangères, consultez [cette entrée de FAQ](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles).

De nombreux utilisateurs trouvent [le guide des formats personnalisés de TRaSH](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) utile pour spécifier les langues des films qu'ils souhaitent.

Les profils sont également l'endroit où les scores de format personnalisés sont configurés. Il est fortement recommandé d'ajouter les formats personnalisés suivants à partir des [Guides de TRaSH](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) pour éviter les téléchargements indésirables. Consultez l'article sur les formats personnalisés du guide TRaSH lié et les 3 autres guides de formats personnalisés TRaSH référencés en haut de la page Collection of Custom Formats pour plus d'informations.

- [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) évitera de télécharger des versions avec Dolby Vision (DV) qui ont une teinte verte si DV n'est pas pris en charge.
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) évitera de télécharger des BR-DISK mal nommés qui ne correspondent pas à l'analyse de qualité BR-DISK.

> Plus d'informations sur [Paramètres => Profils](/radarr/settings#profiles).
> Pour voir la différence entre les sources de qualité, consultez [nos définitions de qualité](/radarr/settings#qualities-defined).
{.is-info}

# Qualité

`Paramètres` => `Qualité`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

Ici, vous pouvez modifier/affiner la taille minimale et maximale de vos fichiers multimédias souhaités (lorsque vous utilisez Usenet, gardez à l'esprit les fichiers RAR/PAR2).

> Si vous avez besoin d'aide pour définir les paramètres de qualité, consultez [les recommandations de taille de TRaSH](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/) pour un exemple testé.
{.is-info}

# Indexeurs

`Paramètres` => `Indexeurs`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

Ici, vous ajouterez l'indexeur/le tracker que vous utiliserez pour télécharger vos fichiers.

Une fois que vous avez cliqué sur le bouton <kb>+</kb> pour ajouter un nouvel indexeur, une nouvelle fenêtre s'ouvrira avec de nombreuses options différentes. Aux fins de ce wiki, Radarr considère à la fois les indexeurs Usenet et les trackers Torrent comme des "indexeurs".

Il y a deux sections ici : Usenet et Torrents. En fonction du client de téléchargement que vous utiliserez, vous devrez sélectionner le type d'indexeur que vous utiliserez.

Pour les trackers Torrent, la plupart nécessitent l'utilisation de [Prowlarr](/prowlarr) ou [Jackett](https://github.com/Jackett/Jackett).

# Clients de téléchargement

`Paramètres` => `Clients de téléchargement`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

Le téléchargement et l'importation sont les étapes où la plupart des utilisateurs rencontrent des problèmes. D'un point de vue général, le logiciel doit être capable de communiquer avec votre client de téléchargement et d'avoir un accès en lecture et en écriture à l'emplacement où le client de téléchargement signale les fichiers téléchargés. Il existe une grande variété de clients de téléchargement pris en charge et une variété encore plus grande de configurations. Cela signifie qu'il n'y a pas de configuration unique et qu'il peut y avoir des différences entre les configurations de chacun. Mais il y a aussi de nombreuses configurations incorrectes.

> Consultez la [page des paramètres](/radarr/settings#download-clients), la page [Plus d'informations (Pris en charge)](/radarr/supported#download-clients) pour cette section, et [les guides des clients de téléchargement de TRaSH](https://trash-guides.info/Downloaders/) pour plus d'informations.
{.is-info}

## Protocoles de téléchargement {.tabset}

### Usenet

{#usenet}

- Radarr envoie une demande de téléchargement à votre client et l'associe à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Radarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Il surveille cela via l'API de votre client de téléchargement.
- Lorsque le téléchargement est terminé, Radarr connaît l'emplacement final du fichier tel que rapporté par votre client de téléchargement. Cet emplacement de fichier peut être presque n'importe où, tant qu'il est séparé de votre dossier multimédia et accessible par Radarr.
- Radarr analyse cet emplacement de fichier terminé pour trouver des fichiers que Radarr peut utiliser. Il analyse le nom du fichier pour le faire correspondre avec le média demandé. S'il peut le faire, il renomme le fichier selon vos spécifications et le déplace vers l'emplacement multimédia spécifié.
- Les déplacements atomiques (déplacements instantanés) sont activés par défaut. Le système de fichiers et les montages doivent être les mêmes pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si le déplacement atomique échoue ou si votre configuration ne prend pas en charge les liens durs et les déplacements atomiques, Radarr effectuera une copie du fichier, puis le supprimera de la source, ce qui est intensif en termes d'E/S.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Radarr, les fichiers restants du téléchargement seront envoyés à la corbeille ou au recyclage via une demande à votre client pour supprimer le téléchargement.

### BitTorrent

{#bittorrent}

- Radarr envoie une demande de téléchargement à votre client et l'associe à un label ou à un nom de catégorie que vous avez configuré dans les paramètres du client de téléchargement.
  - Exemples : films, séries TV, musique, etc.
- Radarr surveille les téléchargements actifs de votre client de téléchargement qui utilisent ce nom de catégorie. Cette surveillance se fait via l'API de votre client de téléchargement.
- Les téléchargements terminés qui sont toujours en partage de fichiers sont laissés à leur emplacement d'origine pour vous permettre de partager le fichier (le ratio ou le temps peut être ajusté dans le client de téléchargement ou depuis Radarr sous le client de téléchargement spécifique). Lorsque les fichiers sont importés dans votre dossier multimédia, Radarr crée un lien dur vers le fichier s'il est pris en charge par votre configuration, sinon il effectue une copie si les liens durs ne sont pas pris en charge. Les torrents en pause et ayant terminé le partage seront déplacés de manière atomique s'ils sont pris en charge par les liens durs, sinon ils seront copiés et supprimés.
- Les liens durs sont activés par défaut. [Un lien dur ne nécessite pas d'espace disque supplémentaire.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Le système de fichiers et les montages doivent être les mêmes pour votre répertoire de téléchargement terminé et votre bibliothèque multimédia. Si la création du lien dur échoue ou si votre configuration ne prend pas en charge les liens durs, Radarr effectuera une copie du fichier.
- Si l'option "Gestion des téléchargements terminés - Supprimer" est activée dans les paramètres de Radarr, Radarr supprimera le torrent de votre client et demandera au client de supprimer les données du torrent, mais seulement si le client signale que le partage est terminé et que le torrent est arrêté (en pause à la fin).

# Comment importer votre bibliothèque multimédia organisée existante

> Notez que Radarr ne recherche pas régulièrement les films. Consultez l'entrée de FAQ [Comment fonctionne Radarr ?](/radarr/faq#how-does-radarr-work) pour comprendre comment Radarr fonctionne.
{.is-info}

Après avoir configuré vos profils/tailles de qualité et ajouté vos indexeurs et client(s) de téléchargement, il est temps d'importer votre bibliothèque multimédia organisée existante.

`Films`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

Sélectionnez `Importer des films existants` ou sélectionnez `Importer` dans la barre latérale.

## Importer des films

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

Sélectionnez le chemin racine que vous avez ajouté précédemment [dans la section des dossiers racine.](#dossiers-racine)

## Importation de médias existants

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

En fonction de la qualité de vos noms de dossiers de films existants, Radarr essaiera de les faire correspondre au film correct, comme indiqué au numéro 5. Si tous vos films se trouvent dans un seul répertoire, suivez ce [guide](/radarr/tips-and-tricks#creating-a-folder-for-each-movie).

1. Le nom de votre dossier de film.
1. Surveillance - Comment vous souhaitez que le film soit ajouté à Radarr.

- Aucun - Ne surveille pas le film ni la collection pour les nouvelles sorties.
- Film uniquement - Surveille uniquement le film pour les nouvelles sorties.
- Film et collection - Surveille à la fois le film pour les nouvelles sorties et ajoute et surveille tous les films de la collection du film (s'il en existe).

1. Disponibilité - Quand Radarr considère qu'un film est disponible.

- **Annoncé** : Radarr considère les films disponibles dès qu'ils sont ajoutés à Radarr. Ce paramètre est *recommandé* si vous avez de bons trackers privés qui n'ont pas de faux.
- **En salle** : Radarr considère les films disponibles dès qu'ils sortent en salle. Cette option n'est *pas recommandée*.
- **Sorti** : Radarr considère les films disponibles dès que le Blu-ray est sorti. Cette option est *recommandée* si vos indexeurs contiennent souvent des faux.

1. Profil de qualité - Sélectionnez votre profil préféré à utiliser.
1. Film - Ce que Radarr pense être le film correspondant. Il est impératif de vérifier cela et de modifier/rechercher si la correspondance n'est pas correcte. Les incohérences sont souvent causées par des dossiers mal nommés.
1. Sélection de masse de l'état de surveillance.
1. Sélection de masse de la disponibilité minimale.
1. Sélection de masse du profil de qualité.
1. Commencez à importer votre bibliothèque multimédia existante.

Une fois qu'un film est ajouté à Radarr, Radarr analyse le dossier du film et tente de faire correspondre un fichier vidéo dans le dossier au film. La cause la plus courante de non-correspondance du fichier et du film, ce qui entraîne un statut Radarr "Manquant", est l'absence de l'année dans le nom du fichier. Radarr exige que l'année soit présente dans le nom du fichier pour qu'il puisse être analysé.

### Aucune correspondance trouvée

Si vous obtenez une erreur comme celle-ci

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

Alors vous avez probablement fait une erreur dans le nom de votre dossier de film.

Pour résoudre ce problème, vous pouvez essayer ce qui suit :

Développez le message d'erreur

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

et vérifiez sur [themoviedb](https://www.themoviedb.org/) si l'année ou le titre correspond. Dans cet exemple, vous remarquerez que l'année est incorrecte et vous pouvez la corriger en modifiant l'année et en cliquant sur l'icône de rafraîchissement.

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

Ou vous pouvez simplement utiliser l'identifiant tmdb ou imdb (si tmdb est lié à imdb) et ensuite sélectionner le film trouvé s'il correspond.

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### Correction du nom de dossier erroné après l'importation

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

Vous remarquerez après la correction que nous avons effectuée lors de l'importation que le nom du dossier contient toujours la mauvaise année. Pour corriger cela, nous allons faire un petit tour de magie.

Accédez à l'aperçu de votre film

`Films`

En haut, cliquez sur `Éditeur de films`

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

Après l'avoir activé, sélectionnez le(s) film(s) à partir duquel vous souhaitez renommer le(s) dossier(s).

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. Si vous souhaitez que tous les dossiers de vos films soient renommés selon le schéma de nommage que vous avez défini précédemment [section de nommage des films](#movie-naming).
2. Sélectionnez le(s) film(s) à partir duquel vous souhaitez renommer le(s) dossier(s).
3. Choisissez le même `Dossier racine`

Une nouvelle fenêtre contextuelle s'affiche

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

Sélectionnez `Oui, déplacer les fichiers`

Ensuite, magie

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

Comme vous pouvez le voir, le dossier a été renommé avec l'année correcte selon votre schéma de nommage.

## Comment ajouter un film

Après avoir importé votre bibliothèque multimédia bien organisée, il est temps d'ajouter les films que vous souhaitez.

`Films` => `Ajouter un nouveau`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

Tapez dans la boîte le film que vous souhaitez ou utilisez l'identifiant tmdb ou imdb.

Lorsque vous saisissez le nom du film, vous verrez qu'il commence à afficher des résultats.

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

Lorsque vous voyez le film que vous souhaitez, cliquez dessus.

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. Dossier racine - Radarr ajoutera le film au dossier racine que vous avez configuré [dans la section des dossiers racines](#root-folders)
1. Surveiller - Comment vous souhaitez que le film soit ajouté à Radarr.

- Film uniquement = Radarr surveillera le flux RSS pour le film de votre bibliothèque que vous n'avez pas encore ou améliorera le film existant avec une meilleure qualité.
- Film et collection = Radarr surveillera le flux RSS pour le film de votre bibliothèque que vous n'avez pas encore ou améliorera le film existant avec une meilleure qualité. Il ajoutera également tous les films de la collection de ce film (s'il y en a) avec vos paramètres sélectionnés.
- Aucun = Radarr ne surveillera pas le flux RSS, toutes les mises à niveau ou les nouveaux films seront ignorés et devront être effectués manuellement. Toutes les recherches de films non surveillés doivent être des recherches déclenchées manuellement ou des recherches interactives.

1. Disponibilité - Quand Radarr considère qu'un film est disponible.

> Pour plus d'informations sur les dates de TMDB qui influencent les disponibilités ci-dessous, voir [Comment Radarr détermine-t-il l'année du film](#how-does-radarr-determine-the-year-of-a-movie)
{.is-info}

- **Annoncé** : Radarr considérera les films disponibles dès qu'ils seront ajoutés à Radarr. Ce paramètre est recommandé si vous avez de bons trackers privés (ou de très bons trackers publics, par exemple rarbg.to) qui n'ont pas de faux fichiers.
- **En salles** : Radarr considérera les films disponibles dès qu'ils sortiront en salles (date de sortie en salle sur TMDb). Cette option n'est pas recommandée.
- **Sorti** : Radarr considérera les films disponibles dès que la version Blu-Ray ou en streaming sera disponible (dates numériques et physiques sur TMDb). Cette option est recommandée et devrait probablement être combinée avec un délai de disponibilité de `-14` ou `-21` jours.
  - Si TMDb n'est pas renseigné avec une date, on suppose que 90 jours après la `date de sortie en salle` (la plus ancienne), le film est disponible sur le web ou en version physique.

1. Profil de qualité - Sélectionnez votre profil à utiliser pour ce film
1. Tags - Ici, vous pouvez ajouter certaines balises pour une utilisation avancée.
1. Recherche lors de l'ajout - Assurez-vous d'activer cette option si vous souhaitez que Radarr recherche le film manquant lorsqu'il est ajouté à Radarr [plus d'informations](/radarr/faq#how-does-radarr-find-movies)
1. Cliquez sur `Ajouter le film` pour ajouter le film à Radarr.

- Si vous obtenez une erreur "le chemin est déjà configuré" [consultez cette entrée FAQ](/radarr/faq#path-is-already-configured-for-an-existing-movie)