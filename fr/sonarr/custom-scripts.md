---
title: Scripts personnalisés Sonarr
description: 
published: true
date: 2022-06-13T15:52:03.477Z
tags: sonarr, needs-love, scripts personnalisés
editor: markdown
dateCreated: 2021-06-16T15:55:53.999Z
---

Si vous souhaitez déclencher un script personnalisé, vous pouvez trouver plus de détails ici. Les scripts sont ajoutés à Sonarr via les [paramètres de connexion](/sonarr/settings#connections).

# Aperçu

Sonarr peut exécuter un script personnalisé lorsqu'un épisode est nouvellement importé ou renommé. Selon l'action, différents paramètres sont fournis. Les paramètres sont transmis au script via des variables d'environnement.

## Journaux Sonarr

Notez que les éléments suivants ne seront enregistrés que pour les scripts personnalisés :

- La sortie `stdout` du script sera enregistrée en tant que `Debug`
- La sortie `stderr` du script sera enregistrée en tant que `Info`
- Le déclencheur du script sera enregistré dans `Trace`

# Variables d'environnement

## Sur la récupération

| Variable d'environnement               | Détails                                                                                      |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Grab`                                                                                       |
| `sonarr_series_id`                      | ID interne de la série                                                                    |
| `sonarr_series_title`                   | Titre de la série                                                                          |
| `sonarr_series_tvdbid`                  | ID TVDB de la série                                                                       |
| `sonarr_series_tvmazeid`                | ID TVMaze de la série                                                                     |
| `sonarr_series_imdbid`                  | ID IMDB de la série (vide si inconnu)                                                    |
| `sonarr_series_type`                    | Type de la série (`Anime`, `Daily` ou `Standard`)                                         |
| `sonarr_release_episodecount`           | Nombre d'épisodes dans la version                                                            |
| `sonarr_release_seasonnumber`           | Numéro de saison de la version                                                                   |
| `sonarr_release_episodenumbers`         | Liste des numéros d'épisode séparés par des virgules                                                      |
| `sonarr_release_absoluteepisodenumbers` | Liste des numéros d'épisode absolus séparés par des virgules                                             |
| `sonarr_release_episodeairdates`        | Liste des dates de diffusion d'origine séparées par des virgules                                      |
| `sonarr_release_episodeairdatesutc`     | Liste des dates de diffusion en UTC séparées par des virgules                                                     |
| `sonarr_release_episodetitles`          | Liste des titres d'épisode séparés par des `\|`                                                        |
| `sonarr_release_title`                  | Titre du torrent/NZB                                                                            |
| `sonarr_release_indexer`                | Indexeur à partir duquel la version a été récupérée                                                   |
| `sonarr_release_size`                   | Taille de la version, telle que rapportée par l'indexeur                                              |
| `sonarr_release_quality`                | Nom de la qualité de la version, telle que détectée par Sonarr                                           |
| `sonarr_release_qualityversion`         | `1` est la valeur par défaut, `2` est pour les versions correctes, et `3`+ peut être utilisé pour les versions d'anime             |
| `sonarr_release_releasegroup`           | Groupe de sortie (vide si inconnu)                                                             |
| `sonarr_download_client`                | Client de téléchargement                                                                              |
| `sonarr_download_id`                    | Hash du fichier torrent/NZB (utilisé pour identifier de manière unique le téléchargement dans le client de téléchargement) |

## Sur l'importation/la mise à niveau

| Variable d'environnement                | Détails                                                                                      |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Download`                                                                                   |
| `sonarr_isupgrade`                      | `True` lorsque un fichier existant est mis à jour, `False` sinon                              |
| `sonarr_series_id`                      | ID interne de la série                                                                      |
| `sonarr_series_title`                   | Titre de la série                                                                           |
| `sonarr_series_path`                    | Chemin complet de la série                                                                  |
| `sonarr_series_tvdbid`                  | ID TVDB de la série                                                                         |
| `sonarr_series_tvmazeid`                | ID TVMaze de la série                                                                       |
| `sonarr_series_imdbid`                  | ID IMDB de la série (vide si inconnu)                                                       |
| `sonarr_series_type`                    | Type de la série (`Anime`, `Daily` ou `Standard`)                                           |
| `sonarr_episodefile_id`                 | ID interne du fichier d'épisode                                                             |
| `sonarr_episodefile_episodecount`       | Nombre d'épisodes dans le fichier                                                           |
| `sonarr_episodefile_relativepath`       | Chemin du fichier d'épisode, relatif au chemin de la série                                   |
| `sonarr_episodefile_path`               | Chemin complet du fichier d'épisode                                                         |
| `sonarr_episodefile_episodeids`         | ID(s) interne(s) du fichier d'épisode                                                       |
| `sonarr_episodefile_seasonnumber`       | Numéro de saison du fichier d'épisode                                                       |
| `sonarr_episodefile_episodenumbers`     | Liste de numéros d'épisode séparés par des virgules                                         |
| `sonarr_episodefile_episodeairdates`    | Liste de dates de diffusion séparées par des virgules à partir du réseau d'origine           |
| `sonarr_episodefile_episodeairdatesutc` | Liste de dates de diffusion en UTC séparées par des virgules                                |
| `sonarr_episodefile_episodetitles`      | Liste de titres d'épisode séparés par des `\|`                                               |
| `sonarr_episodefile_quality`            | Nom de la qualité du fichier d'épisode, détectée par Sonarr                                 |
| `sonarr_episodefile_qualityversion`     | `1` est la valeur par défaut, `2` est utilisé pour les versions correctes et `3`+ pour les versions d'anime |
| `sonarr_episodefile_releasegroup`       | Groupe de sortie (vide si inconnu)                                                          |
| `sonarr_episodefile_scenename`          | Nom de sortie original (vide si inconnu)                                                    |
| `sonarr_episodefile_sourcepath`         | Chemin complet du fichier d'épisode importé                                                 |
| `sonarr_episodefile_sourcefolder`       | Chemin complet du dossier à partir duquel le fichier d'épisode a été importé                 |
| `sonarr_download_client`                | Client de téléchargement                                                                    |
| `sonarr_download_id`                    | Hash du fichier torrent/NZB (utilisé pour identifier de manière unique le téléchargement dans le client de téléchargement) |
| `sonarr_deletedrelativepaths`           | Liste de fichiers supprimés séparés par des `\|` qui ont été supprimés pour importer ce fichier |
| `sonarr_deletedpaths`                   | Liste de chemins complets de fichiers séparés par des `\|` qui ont été supprimés pour importer ce fichier |

## Sur le renommage

| Variable d'environnement     | Détails                                              |
| ------------------------ | ---------------------------------------------------- |
| `sonarr_eventtype`       | `Rename`                                             |
| `sonarr_series_id`       | ID interne de la série                            |
| `sonarr_series_title`    | Titre de la série                                  |
| `sonarr_series_path`     | Chemin complet de la série                              |
| `sonarr_series_tvdbid`   | ID TVDB de la série                               |
| `sonarr_series_tvmazeid` | ID TVMaze de la série                             |
| `sonarr_series_imdbid`   | ID IMDB de la série (vide si inconnu)            |
| `sonarr_series_type`     | Type de la série (`Anime`, `Daily` ou `Standard`) |

| Variable d'environnement                | Détails                                                                          |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`                      | ID interne de la série                                                           |
| `sonarr_series_title`                   | Titre de la série                                                                |
| `sonarr_series_path`                    | Chemin complet de la série                                                       |
| `sonarr_series_tvdbid`                  | ID TVDB de la série                                                              |
| `sonarr_series_tvmazeid`                | ID TVMaze de la série                                                            |
| `sonarr_series_imdbid`                  | ID IMDB de la série (vide si inconnu)                                            |
| `sonarr_series_type`                    | Type de la série (`Anime`, `Daily` ou `Standard`)                                |
| `sonarr_episodefile_id`                 | ID interne du fichier d'épisode                                                  |
| `sonarr_episodefile_episodecount`       | Nombre d'épisodes dans le fichier                                                |
| `sonarr_episodefile_relativepath`       | Chemin du fichier d'épisode, relatif au chemin de la série                        |
| `sonarr_episodefile_path`               | Chemin complet du fichier d'épisode                                              |
| `sonarr_episodefile_episodeids`         | ID(s) interne(s) du fichier d'épisode                                            |
| `sonarr_episodefile_seasonnumber`       | Numéro de saison du fichier d'épisode                                            |
| `sonarr_episodefile_episodenumbers`     | Liste des numéros d'épisode séparés par des virgules                              |
| `sonarr_episodefile_episodeairdates`    | Liste des dates de diffusion d'origine séparées par des virgules                  |
| `sonarr_episodefile_episodeairdatesutc` | Liste des dates de diffusion en UTC séparées par des virgules                     |
| `sonarr_episodefile_episodetitles`      | Liste des titres d'épisode séparés par des `\|`                                   |
| `sonarr_episodefile_quality`            | Nom de la qualité du fichier d'épisode, détectée par Sonarr                       |
| `sonarr_episodefile_qualityversion`     | `1` est la valeur par défaut, `2` est utilisé pour les versions correctes, et `3`+ peut être utilisé pour les versions d'anime |
| `sonarr_episodefile_releasegroup`       | Groupe de diffusion (vide si inconnu)                                            |
| `sonarr_episodefile_scenename`          | Nom de diffusion d'origine (vide si inconnu)                                      |

## Sur la suppression de série

| Variable d'environnement         | Détails                                                                  |
| ---------------------------- | ------------------------------------------------------------------------ |
| `sonarr_eventtype`           | `SeriesDelete`                                                           |
| `sonarr_series_id`           | ID interne de la série                                                |
| `sonarr_series_title`        | Titre de la série                                                      |
| `sonarr_series_path`         | Chemin complet de la série                                                  |
| `sonarr_series_tvdbid`       | ID TVDB de la série                                                   |
| `sonarr_series_imdbid`       | ID IMDB de la série (vide si inconnu)                                |
| `sonarr_series_type`         | Type de la série (`Anime`, `Daily` ou `Standard`)                     |
| `sonarr_series_deletedfiles` | `True` lorsque l'option de suppression des fichiers a été sélectionnée, sinon `False` |

## Sur les problèmes de santé

| Variable d'environnement          | Détails                                                      |
| ----------------------------- | ------------------------------------------------------------ |
| `sonarr_eventtype`            | `HealthIssue`                                                |
| `sonarr_health_issue_level`   | Type de problème de santé (`Ok`, `Notice`, `Warning` ou `Error`) |
| `sonarr_health_issue_message` | Message du problème de santé                                |
| `sonarr_health_issue_type`    | Zone ayant échoué et déclenché le problème de santé              |
| `sonarr_health_issue_wiki`    | URL du wiki (vide s'il n'existe pas)                           |

## Sur la mise à jour de l'application

| Variable d'environnement             | Détails                               |
|--------------------------------- |-------------------------------------- |
| `sonarr_eventtype`               | `ApplicationUpdate`                   |
| `sonarr_update_message`          | Message de la mise à jour                   |
| `sonarr_update_newversion`       | Version vers laquelle Sonarr a été mise à jour (chaîne de caractères)    |
| `sonarr_update_previousversion`  | Version à partir de laquelle Sonarr a été mise à jour (chaîne de caractères)  |

## Sur le test

Lorsque vous ajoutez le script à Sonarr et cliquez sur 'Test', le script sera invoqué avec les paramètres suivants. Le script doit être capable d'ignorer gracieusement tout type d'événement non pris en charge.

| Variable d'environnement | Détails |
| -------------------- | ------- |
| `sonarr_eventtype`   | `Test`  |