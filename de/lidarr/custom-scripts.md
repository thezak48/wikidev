---
title: Lidarr Benutzerdefinierte Skripte
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, needs-love, benutzerdefinierte skripte
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

Wenn Sie ein benutzerdefiniertes Skript auslösen möchten, finden Sie weitere Details auf dieser Seite. Skripte werden in Lidarr über die [Verbindungs-Einstellungen](/lidarr/settings#connections) hinzugefügt.

# Übersicht

Lidarr kann ein benutzerdefiniertes Skript ausführen, wenn eine Episode neu importiert oder umbenannt wird. Je nach Aktion werden unterschiedliche Parameter übergeben. Die Parameter werden dem Skript über Umgebungsvariablen übergeben.

Ein benutzerdefiniertes Skript kann jede ausführbare Datei sein, auf die der Benutzer zugreifen kann, unter dem Lidarr ausgeführt wird.

## Lidarr-Protokolle

Beachten Sie, dass das Folgende nur für benutzerdefinierte Skripte protokolliert wird:

- Die Ausgabe von Skript `stdout` wird als `Debug` in config/logs/Lidarr.debug.txt protokolliert.
- Die Ausgabe von Skript `stderr` wird als `Info` in config/logs/Lidarr.txt protokolliert.
- Der Auslöser des Skripts wird als `Trace` in config/logs/Lidarr.trace.txt protokolliert.

# Umgebungsvariablen

Die Umgebungsvariablen variieren je nach Ereignistyp. Die folgenden Abschnitte geben die für jeden verfügbaren Variablen an.

> [Die folgenden Abschnitte müssen bereinigt, organisiert und verbessert werden. Hier finden Sie den Quellcode](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Grab

| Umgebungsvariable                  | Details                                                             |
| --------------------------------- | ------------------------------------------------------------------- |
| `lidarr_eventtype`                 | Grab                                                                 |
| `lidarr_artist_id`                 | `artist.Id`                                                         |
| `lidarr_artist_name`               | `artist.Metadata.Value.Name`                                        |
| `lidarr_artist_mbid`               | `artist.Metadata.Value.ForeignArtistId`                             |
| `lidarr_artist_type`               | `artist.Metadata.Value.Type`                                        |
| `lidarr_release_albumcount`        | `remoteAlbum.Albums.Count`                                          |
| `lidarr_release_albumreleasedates` | Durch Kommas getrennte Liste von Veröffentlichungsdaten der Alben   |
| `lidarr_release_albumtitles`       | Durch Pipe getrennte Liste von Albumtiteln                           |
| `lidarr_release_albummbids`        | Durch Pipe getrennte Liste von externen Dienst-IDs der Alben (z. B. MusicBrainz) |
| `lidarr_release_title`             | `remoteAlbum.Release.Title`                                         |
| `lidarr_release_indexer`           | `remoteAlbum.Release.Indexer`                                       |
| `lidarr_release_size`              | `remoteAlbum.Release.Size`                                          |
| `lidarr_release_quality`           | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                  |
| `lidarr_release_qualityversion`    | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`              |
| `lidarr_release_releasegroup`      | `releaseGroup`                                                      |
| `lidarr_download_client`           | `message.DownloadClient`                                            |
| `lidarr_download_id`               | `message.DownloadId`                                                |

## Beim Importieren / Beim Aktualisieren

| Umgebungsvariable       | Details                                  |
| ----------------------- | ---------------------------------------- |
| `lidarr_eventtype`      | AlbumDownload                            |
| `lidarr_artist_id`      | `artist.Id`                              |
| `lidarr_artist_name`    | `artist.Metadata.Value.Name`             |
| `lidarr_artist_path`    | `artist.Path`                            |
| `lidarr_artist_mbid`    | `artist.Metadata.Value.ForeignArtistId`  |
| `lidarr_artist_type`    | `artist.Metadata.Value.Type`             |
| `lidarr_album_id`       | `album.Id`                               |
| `lidarr_album_title`    | `album.Title`                            |
| `lidarr_album_mbid`     | `album.ForeignAlbumId`                   |
| `lidarr_albumrelease_mbid` | `release.ForeignReleaseId`               |
| `lidarr_album_releasedate` | `album.ReleaseDate`                      |
| `lidarr_download_client` | `message.DownloadClient`                 |
| `lidarr_download_id`    | `message.DownloadId`                     |
| `lidarr_addedtrackpaths` | Durch Pipe getrennte Liste der hinzugefügten Track-Pfade |
| `lidarr_deletedpaths`   | Durch Pipe getrennte Liste der gelöschten Dateien |

## Umbenennen

| Umgebungsvariable | Details                                 |
| ----------------- | --------------------------------------- |
| `lidarr_eventtype` | Rename                                  |
| `lidarr_artist_id` | `artist.Id`                             |
| `lidarr_artist_name` | `artist.Metadata.Value.Name`            |
| `lidarr_artist_path` | `artist.Path`                           |
| `lidarr_artist_mbid` | `artist.Metadata.Value.ForeignArtistId` |
| `lidarr_artist_type` | `artist.Metadata.Value.Type`            |

## Track Retag

| Umgebungsvariable              | Details                                 |
| ------------------------------ | --------------------------------------- |
| `lidarr_eventtype`             | TrackRetag                              |
| `lidarr_artist_id`             | `artist.Id`                             |
| `lidarr_artist_name`           | `artist.Metadata.Value.Name`            |
| `lidarr_artist_path`           | `artist.Path`                           |
| `lidarr_artist_mbid`           | `artist.Metadata.Value.ForeignArtistId` |
| `lidarr_artist_type`           | `artist.Metadata.Value.Type`            |
| `lidarr_album_id`              | `album.Id`                              |
| `lidarr_album_title`           | `album.Title`                           |
| `lidarr_album_mbid`            | `album.ForeignAlbumId`                  |
| `lidarr_albumrelease_mbid`     | `release.ForeignReleaseId`              |
| `lidarr_album_releasedate`     | `album.ReleaseDate`                     |
| `lidarr_trackfile_id`          | `trackFile.Id`                          |
| `lidarr_trackfile_trackcount`  | `trackFile.Tracks.Value.Count`          |
| `lidarr_trackfile_path`        | `trackFile.Path`                        |
| `lidarr_trackfile_tracknumbers` | Durch Kommas getrennte Liste von Track-Nummern |
| `lidarr_trackfile_tracktitles` | Durch Pipe getrennte Liste von Track-Titeln |
| `lidarr_trackfile_quality`     | `trackFile.Quality.Quality.Name`        |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`    |
| `lidarr_trackfile_releasegroup` | `trackFile.ReleaseGroup`                |
| `lidarr_trackfile_scenename`   | `trackFile.SceneName`                   |
| `lidarr_tags_diff`             | `message.Diff.ToJson()`                 |
| `lidarr_tags_scrubbed`         | `message.Scrubbed`                      |

## Gesundheitsproblem

| Umgebungsvariable           | Details                                 |
| --------------------------- | --------------------------------------- |
| `lidarr_eventtype`          | HealthIssue                             |
| `lidarr_health_issue_level` | `nameof(healthCheck.Type)`              |
| `lidarr_health_issue_message` | `healthCheck.Message`                   |
| `lidarr_health_issue_type`  | `healthCheck.Source.Name`               |
| `lidarr_health_issue_wiki`  | Wiki-URL für die Hilfeseite des Gesundheitsproblems |

## Beim Testen

Wenn Sie das Skript zu Lidarr hinzufügen und auf "Testen" klicken, wird das Skript mit den folgenden Parametern aufgerufen. Das Skript sollte in der Lage sein, jeden nicht unterstützten Ereignistyp zu ignorieren.

| Umgebungsvariable | Details |
| ----------------- | ------- |
| `lidarr_eventtype` | Test    |