---
title: Scripts personnalisés Lidarr
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, needs-love, scripts personnalisés
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

Si vous souhaitez déclencher un script personnalisé, vous pouvez trouver plus de détails sur cette page. Les scripts sont ajoutés à Lidarr via les [paramètres de connexion](/lidarr/settings#connections).

# Aperçu

Lidarr peut exécuter un script personnalisé lorsqu'un épisode est nouvellement importé ou renommé. Selon l'action, différents paramètres sont fournis. Les paramètres sont transmis au script via des variables d'environnement.

Un script personnalisé peut être n'importe quel exécutable accessible par l'utilisateur sous lequel Lidarr s'exécute.

## Journaux Lidarr

Notez que les éléments suivants ne seront enregistrés que pour les scripts personnalisés :

- La sortie `stdout` du script sera enregistrée en tant que `Debug` dans config/logs/Lidarr.debug.txt
- La sortie `stderr` du script sera enregistrée en tant que `Info` dans config/logs/Lidarr.txt
- Le déclenchement du script sera enregistré en tant que `Trace` dans config/logs/Lidarr.trace.txt

# Variables d'environnement

Les variables d'environnement varient en fonction du type d'événement. Les sections ci-dessous indiquent les variables disponibles pour chaque type.

> [Les sections ci-dessous nécessitent un nettoyage, une organisation et des détails améliorés. Voir le code source ici](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Grab

| Variable d'environnement         | Détails                                                               |
| -------------------------------- | --------------------------------------------------------------------- |
| `lidarr_eventtype`               | Grab                                                                  |
| `lidarr_artist_id`               | `artist.Id`                                                           |
| `lidarr_artist_name`             | `artist.Metadata.Value.Name`                                          |
| `lidarr_artist_mbid`             | `artist.Metadata.Value.ForeignArtistId`                               |
| `lidarr_artist_type`             | `artist.Metadata.Value.Type`                                          |
| `lidarr_release_albumcount`      | `remoteAlbum.Albums.Count`                                            |
| `lidarr_release_albumreleasedates` | Liste des dates de sortie des albums séparées par des virgules         |
| `lidarr_release_albumtitles`     | Liste des titres d'album séparés par des barres verticales             |
| `lidarr_release_albummbids`      | Liste des identifiants de service externe des albums séparés par des barres verticales (par ex. MusicBrainz) |
| `lidarr_release_title`           | `remoteAlbum.Release.Title`                                           |
| `lidarr_release_indexer`         | `remoteAlbum.Release.Indexer`                                         |
| `lidarr_release_size`            | `remoteAlbum.Release.Size`                                            |
| `lidarr_release_quality`         | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                    |
| `lidarr_release_qualityversion`  | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`                |
| `lidarr_release_releasegroup`    | `releaseGroup`                                                        |
| `lidarr_download_client`         | `message.DownloadClient`                                              |
| `lidarr_download_id`             | `message.DownloadId`                                                  |

## À l'importation / À la mise à niveau

| Variable d'environnement | Détails                                   |
| ------------------------ | ----------------------------------------- |
| `lidarr_eventtype`       | AlbumDownload                             |
| `lidarr_artist_id`       | `artist.Id`                               |
| `lidarr_artist_name`     | `artist.Metadata.Value.Name`              |
| `lidarr_artist_path`     | `artist.Path`                             |
| `lidarr_artist_mbid`     | `artist.Metadata.Value.ForeignArtistId`   |
| `lidarr_artist_type`     | `artist.Metadata.Value.Type`              |
| `lidarr_album_id`        | `album.Id`                                |
| `lidarr_album_title`     | `album.Title`                             |
| `lidarr_album_mbid`      | `album.ForeignAlbumId`                    |
| `lidarr_albumrelease_mbid` | `release.ForeignReleaseId`                |
| `lidarr_album_releasedate` | `album.ReleaseDate`                       |
| `lidarr_download_client` | `message.DownloadClient`                  |
| `lidarr_download_id`     | `message.DownloadId`                      |
| `lidarr_addedtrackpaths` | Liste des chemins des pistes ajoutées séparés par des barres verticales |
| `lidarr_deletedpaths`    | Liste des fichiers supprimés séparés par des barres verticales      |

## Renommer

| Variable d'environnement | Détails                                   |
| ------------------------ | ----------------------------------------- |
| `lidarr_eventtype`       | Rename                                    |
| `lidarr_artist_id`       | `artist.Id`                               |
| `lidarr_artist_name`     | `artist.Metadata.Value.Name`              |
| `lidarr_artist_path`     | `artist.Path`                             |
| `lidarr_artist_mbid`     | `artist.Metadata.Value.ForeignArtistId`   |
| `lidarr_artist_type`     | `artist.Metadata.Value.Type`              |

## Retag des pistes

| Variable d'environnement        | Détails                                   |
| ------------------------------- | ----------------------------------------- |
| `lidarr_eventtype`              | TrackRetag                                |
| `lidarr_artist_id`              | `artist.Id`                               |
| `lidarr_artist_name`            | `artist.Metadata.Value.Name`              |
| `lidarr_artist_path`            | `artist.Path`                             |
| `lidarr_artist_mbid`            | `artist.Metadata.Value.ForeignArtistId`   |
| `lidarr_artist_type`            | `artist.Metadata.Value.Type`              |
| `lidarr_album_id`               | `album.Id`                                |
| `lidarr_album_title`            | `album.Title`                             |
| `lidarr_album_mbid`             | `album.ForeignAlbumId`                    |
| `lidarr_albumrelease_mbid`      | `release.ForeignReleaseId`                |
| `lidarr_album_releasedate`      | `album.ReleaseDate`                       |
| `lidarr_trackfile_id`           | `trackFile.Id`                            |
| `lidarr_trackfile_trackcount`   | `trackFile.Tracks.Value.Count`            |
| `lidarr_trackfile_path`         | `trackFile.Path`                          |
| `lidarr_trackfile_tracknumbers` | Liste des numéros de piste séparés par des virgules |
| `lidarr_trackfile_tracktitles`  | Liste des titres de piste séparés par des barres verticales |
| `lidarr_trackfile_quality`      | `trackFile.Quality.Quality.Name`          |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`      |
| `lidarr_trackfile_releasegroup` | `trackFile.ReleaseGroup`                  |
| `lidarr_trackfile_scenename`    | `trackFile.SceneName`                     |
| `lidarr_tags_diff`              | `message.Diff.ToJson()`                   |
| `lidarr_tags_scrubbed`          | `message.Scrubbed`                        |

## Problème de santé

| Variable d'environnement          | Détails                                   |
| --------------------------------- | ----------------------------------------- |
| `lidarr_eventtype`                | HealthIssue                               |
| `lidarr_health_issue_level`       | `nameof(healthCheck.Type)`                 |
| `lidarr_health_issue_message`     | `healthCheck.Message`                     |
| `lidarr_health_issue_type`        | `healthCheck.Source.Name`                 |
| `lidarr_health_issue_wiki`        | URL Wiki pour la page d'aide du problème de santé |

## Test

Lorsque vous ajoutez le script à Lidarr et cliquez sur 'Test', le script sera invoqué avec les paramètres suivants. Le script devrait être en mesure d'ignorer gracieusement tout type d'événement non pris en charge.

| Variable d'environnement | Détails |
| ----------------------- | ------- |
| `lidarr_eventtype`      | Test    |