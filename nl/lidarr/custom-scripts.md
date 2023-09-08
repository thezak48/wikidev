---
title: Lidarr Aangepaste Scripts
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, needs-love, aangepaste scripts
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

Als je een aangepast script wilt activeren, vind je meer details op deze pagina. Scripts worden aan Lidarr toegevoegd via de [Connectie-instellingen](/lidarr/settings#connections).

# Overzicht

Lidarr kan een aangepast script uitvoeren wanneer een aflevering nieuw wordt geïmporteerd of hernoemd. Afhankelijk van de actie worden verschillende parameters meegegeven. Parameters worden aan het script doorgegeven via omgevingsvariabelen.

Een aangepast script kan elk uitvoerbaar bestand zijn dat toegankelijk is voor de gebruiker waarop Lidarr wordt uitgevoerd.

## Lidarr Logboeken

Merk op dat het volgende alleen wordt gelogd voor aangepaste scripts:

- Uitvoer van het script `stdout` wordt gelogd als `Debug` in config/logs/Lidarr.debug.txt
- Uitvoer van het script `stderr` wordt gelogd als `Info` in config/logs/Lidarr.txt
- De trigger van het script wordt gelogd als `Trace` in config/logs/Lidarr.trace.txt

# Omgevingsvariabelen

Omgevingsvariabelen variëren afhankelijk van het type gebeurtenis. De onderstaande secties geven de beschikbare variabelen aan voor elk type.

> [De onderstaande secties moeten worden opgeschoond, georganiseerd en verbeterd. Bekijk hier de broncode](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Grab

| Omgevingsvariabele                | Details                                                              |
| --------------------------------- | -------------------------------------------------------------------- |
| `lidarr_eventtype`                | Grab                                                                 |
| `lidarr_artist_id`                | `artist.Id`                                                          |
| `lidarr_artist_name`              | `artist.Metadata.Value.Name`                                         |
| `lidarr_artist_mbid`              | `artist.Metadata.Value.ForeignArtistId`                              |
| `lidarr_artist_type`              | `artist.Metadata.Value.Type`                                         |
| `lidarr_release_albumcount`       | `remoteAlbum.Albums.Count`                                           |
| `lidarr_release_albumreleasedates`| Door komma's gescheiden lijst van albumrelease-datums                |
| `lidarr_release_albumtitles`      | Door pipes gescheiden lijst van albumtitels                          |
| `lidarr_release_albummbids`       | Door pipes gescheiden lijst van externe service-ID's van albums (bijv. MusicBrainz) |
| `lidarr_release_title`            | `remoteAlbum.Release.Title`                                          |
| `lidarr_release_indexer`          | `remoteAlbum.Release.Indexer`                                        |
| `lidarr_release_size`             | `remoteAlbum.Release.Size`                                           |
| `lidarr_release_quality`          | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                   |
| `lidarr_release_qualityversion`   | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`               |
| `lidarr_release_releasegroup`     | `releaseGroup`                                                       |
| `lidarr_download_client`          | `message.DownloadClient`                                             |
| `lidarr_download_id`              | `message.DownloadId`                                                 |

## Bij importeren / bij upgraden

| Omgevingsvariabele      | Details                                  |
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
| `lidarr_addedtrackpaths`| Door pipes gescheiden lijst van toegevoegde nummerpaden |
| `lidarr_deletedpaths`   | Door pipes gescheiden lijst van verwijderde bestanden     |

## Hernoemen

| Omgevingsvariabele | Details                                 |
| ------------------ | --------------------------------------- |
| `lidarr_eventtype` | Rename                                  |
| `lidarr_artist_id` | `artist.Id`                             |
| `lidarr_artist_name` | `artist.Metadata.Value.Name`            |
| `lidarr_artist_path` | `artist.Path`                           |
| `lidarr_artist_mbid` | `artist.Metadata.Value.ForeignArtistId` |
| `lidarr_artist_type` | `artist.Metadata.Value.Type`            |

## Track Retag

| Omgevingsvariabele               | Details                                 |
| --------------------------------- | --------------------------------------- |
| `lidarr_eventtype`                | TrackRetag                              |
| `lidarr_artist_id`                | `artist.Id`                             |
| `lidarr_artist_name`              | `artist.Metadata.Value.Name`            |
| `lidarr_artist_path`              | `artist.Path`                           |
| `lidarr_artist_mbid`              | `artist.Metadata.Value.ForeignArtistId` |
| `lidarr_artist_type`              | `artist.Metadata.Value.Type`            |
| `lidarr_album_id`                 | `album.Id`                              |
| `lidarr_album_title`              | `album.Title`                           |
| `lidarr_album_mbid`               | `album.ForeignAlbumId`                  |
| `lidarr_albumrelease_mbid`        | `release.ForeignReleaseId`              |
| `lidarr_album_releasedate`        | `album.ReleaseDate`                     |
| `lidarr_trackfile_id`             | `trackFile.Id`                          |
| `lidarr_trackfile_trackcount`     | `trackFile.Tracks.Value.Count`          |
| `lidarr_trackfile_path`           | `trackFile.Path`                        |
| `lidarr_trackfile_tracknumbers`   | Door komma's gescheiden lijst van nummers |
| `lidarr_trackfile_tracktitles`    | Door pipes gescheiden lijst van nummertitels |
| `lidarr_trackfile_quality`        | `trackFile.Quality.Quality.Name`        |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`    |
| `lidarr_trackfile_releasegroup`   | `trackFile.ReleaseGroup`                |
| `lidarr_trackfile_scenename`      | `trackFile.SceneName`                   |
| `lidarr_tags_diff`                | `message.Diff.ToJson()`                 |
| `lidarr_tags_scrubbed`            | `message.Scrubbed`                      |

## Probleem met de gezondheid

| Omgevingsvariabele          | Details                                 |
| --------------------------- | --------------------------------------- |
| `lidarr_eventtype`          | HealthIssue                             |
| `lidarr_health_issue_level` | `nameof(healthCheck.Type)`              |
| `lidarr_health_issue_message` | `healthCheck.Message`                   |
| `lidarr_health_issue_type`  | `healthCheck.Source.Name`               |
| `lidarr_health_issue_wiki`  | URL van de wiki voor de help-pagina van het gezondheidsprobleem |

## Bij testen

Bij het toevoegen van het script aan Lidarr en het klikken op 'Testen', wordt het script aangeroepen met de volgende parameters. Het script moet in staat zijn om eventuele niet-ondersteunde gebeurtenistypen op een goede manier te negeren.

| Omgevingsvariabele   | Details |
| -------------------- | ------- |
| `lidarr_eventtype`   | Test    |