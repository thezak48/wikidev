---
title: Lidarr Brugerdefinerede Scripts
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, needs-love, brugerdefinerede scripts
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

Hvis du vil udløse et brugerdefineret script, kan du finde flere detaljer på denne side. Scripts tilføjes til Lidarr via [Forbindelsesindstillingerne](/lidarr/settings#connections).

# Oversigt

Lidarr kan udføre et brugerdefineret script, når en episode er nyimporteret eller omdøbt. Afhængigt af handlingen leveres forskellige parametre. Parametrene sendes til scriptet gennem miljøvariabler.

Et brugerdefineret script kan være et hvilket som helst eksekverbart script, der er tilgængeligt for den bruger, som Lidarr kører som.

## Lidarr-logs

Bemærk, at følgende kun bliver logget for brugerdefinerede scripts:

- Scriptets `stdout`-output logges som `Debug` i config/logs/Lidarr.debug.txt
- Scriptets `stderr`-output logges som `Info` i config/logs/Lidarr.txt
- Udløseren af scriptet logges som `Trace` i config/logs/Lidarr.trace.txt

# Miljøvariabler

Miljøvariabler varierer afhængigt af begivenhedstypen. Afsnittene nedenfor angiver de tilgængelige variabler for hver begivenhedstype.

> [Afsnittene nedenfor har brug for oprydning, organisering og forbedring af detaljer. Se kildekoden her](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Grab

| Miljøvariabel                   | Detaljer                                                                 |
| ------------------------------ | ------------------------------------------------------------------------ |
| `lidarr_eventtype`              | Grab                                                                     |
| `lidarr_artist_id`              | `artist.Id`                                                              |
| `lidarr_artist_name`            | `artist.Metadata.Value.Name`                                             |
| `lidarr_artist_mbid`            | `artist.Metadata.Value.ForeignArtistId`                                  |
| `lidarr_artist_type`            | `artist.Metadata.Value.Type`                                             |
| `lidarr_release_albumcount`     | `remoteAlbum.Albums.Count`                                               |
| `lidarr_release_albumreleasedates` | Komma-separeret liste over albumudgivelsesdatoer                       |
| `lidarr_release_albumtitles`    | Pipe-separeret liste over albumtitler                                    |
| `lidarr_release_albummbids`     | Pipe-separeret liste over album-eksterne tjeneste-ID'er (f.eks. MusicBrainz) |
| `lidarr_release_title`          | `remoteAlbum.Release.Title`                                              |
| `lidarr_release_indexer`        | `remoteAlbum.Release.Indexer`                                            |
| `lidarr_release_size`           | `remoteAlbum.Release.Size`                                               |
| `lidarr_release_quality`        | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                       |
| `lidarr_release_qualityversion` | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`                   |
| `lidarr_release_releasegroup`   | `releaseGroup`                                                           |
| `lidarr_download_client`        | `message.DownloadClient`                                                 |
| `lidarr_download_id`            | `message.DownloadId`                                                     |

## Ved import / Ved opgradering

| Miljøvariabel             | Detaljer                                        |
| ------------------------ | ----------------------------------------------- |
| `lidarr_eventtype`       | AlbumDownload                                   |
| `lidarr_artist_id`       | `artist.Id`                                     |
| `lidarr_artist_name`     | `artist.Metadata.Value.Name`                    |
| `lidarr_artist_path`     | `artist.Path`                                   |
| `lidarr_artist_mbid`     | `artist.Metadata.Value.ForeignArtistId`         |
| `lidarr_artist_type`     | `artist.Metadata.Value.Type`                    |
| `lidarr_album_id`        | `album.Id`                                      |
| `lidarr_album_title`     | `album.Title`                                   |
| `lidarr_album_mbid`      | `album.ForeignAlbumId`                          |
| `lidarr_albumrelease_mbid` | `release.ForeignReleaseId`                      |
| `lidarr_album_releasedate` | `album.ReleaseDate`                             |
| `lidarr_download_client` | `message.DownloadClient`                        |
| `lidarr_download_id`     | `message.DownloadId`                            |
| `lidarr_addedtrackpaths` | Pipe-separeret liste over tilføjede sporstier |
| `lidarr_deletedpaths`    | Pipe-separeret liste over slettede filer        |

## Omdøb

| Miljøvariabel     | Detaljer                                       |
| ----------------- | ---------------------------------------------- |
| `lidarr_eventtype` | Rename                                         |
| `lidarr_artist_id` | `artist.Id`                                    |
| `lidarr_artist_name` | `artist.Metadata.Value.Name`                   |
| `lidarr_artist_path` | `artist.Path`                                  |
| `lidarr_artist_mbid` | `artist.Metadata.Value.ForeignArtistId`        |
| `lidarr_artist_type` | `artist.Metadata.Value.Type`                   |

## Track Retag

| Miljøvariabel                   | Detaljer                                       |
| ------------------------------ | ---------------------------------------------- |
| `lidarr_eventtype`              | TrackRetag                                     |
| `lidarr_artist_id`              | `artist.Id`                                    |
| `lidarr_artist_name`            | `artist.Metadata.Value.Name`                   |
| `lidarr_artist_path`            | `artist.Path`                                  |
| `lidarr_artist_mbid`            | `artist.Metadata.Value.ForeignArtistId`        |
| `lidarr_artist_type`            | `artist.Metadata.Value.Type`                   |
| `lidarr_album_id`               | `album.Id`                                     |
| `lidarr_album_title`            | `album.Title`                                  |
| `lidarr_album_mbid`             | `album.ForeignAlbumId`                         |
| `lidarr_albumrelease_mbid`      | `release.ForeignReleaseId`                     |
| `lidarr_album_releasedate`      | `album.ReleaseDate`                            |
| `lidarr_trackfile_id`           | `trackFile.Id`                                 |
| `lidarr_trackfile_trackcount`   | `trackFile.Tracks.Value.Count`                 |
| `lidarr_trackfile_path`         | `trackFile.Path`                               |
| `lidarr_trackfile_tracknumbers` | Komma-separeret liste over spornumre           |
| `lidarr_trackfile_tracktitles`  | Pipe-separeret liste over spor-titler          |
| `lidarr_trackfile_quality`      | `trackFile.Quality.Quality.Name`               |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`           |
| `lidarr_trackfile_releasegroup` | `trackFile.ReleaseGroup`                       |
| `lidarr_trackfile_scenename`    | `trackFile.SceneName`                          |
| `lidarr_tags_diff`              | `message.Diff.ToJson()`                        |
| `lidarr_tags_scrubbed`          | `message.Scrubbed`                             |

## Helbredsproblem

| Miljøvariabel                | Detaljer                                       |
| --------------------------- | ---------------------------------------------- |
| `lidarr_eventtype`          | HealthIssue                                    |
| `lidarr_health_issue_level` | `nameof(healthCheck.Type)`                      |
| `lidarr_health_issue_message` | `healthCheck.Message`                          |
| `lidarr_health_issue_type`  | `healthCheck.Source.Name`                      |
| `lidarr_health_issue_wiki`  | Wiki-URL til hjælpesiden for helbredsproblemet |

## Ved test

Når du tilføjer scriptet til Lidarr og klikker på 'Test', vil scriptet blive kaldt med følgende parametre. Scriptet skal kunne ignorere eventuelle ikke-understøttede begivenhedstyper på en hensigtsmæssig måde.

| Miljøvariabel      | Detaljer |
| ------------------ | -------- |
| `lidarr_eventtype` | Test     |