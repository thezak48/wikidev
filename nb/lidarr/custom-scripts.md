---
title: Lidarr Tilpassede Skript
description: 
published: true
date: 2023-04-09T23:23:38.475Z
tags: lidarr, needs-love, tilpassede skript
editor: markdown
dateCreated: 2021-11-24T19:22:09.331Z
---

Hvis du ønsker å utløse et tilpasset skript, kan du finne mer informasjon på denne siden. Skript legges til i Lidarr via [Tilkoblingsinnstillinger](/lidarr/settings#connections).

# Oversikt

Lidarr kan kjøre et tilpasset skript når en episode er nyimportert eller omdøpt. Avhengig av handlingen, blir forskjellige parametere levert. Parametere sendes til skriptet gjennom miljøvariabler.

Et tilpasset skript kan være hvilken som helst kjørbar fil som er tilgjengelig for brukeren som Lidarr kjører som.

## Lidarr-logger

Merk at følgende kun blir logget for tilpassede skript:

- Skriptets `stdout`-utdata blir logget som `Debug` i config/logs/Lidarr.debug.txt
- Skriptets `stderr`-utdata blir logget som `Info` i config/logs/Lidarr.txt
- Utløseren for skriptet blir logget som `Trace` i config/logs/Lidarr.trace.txt

# Miljøvariabler

Miljøvariabler varierer basert på hendelsestypen. Seksjonene nedenfor viser hvilke variabler som er tilgjengelige for hver hendelsestype.

> [Seksjonene nedenfor trenger opprydding, organisering og forbedret detaljer. Se kildekoden her](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Henting

| Miljøvariabel                    | Detaljer                                                              |
| -------------------------------- | --------------------------------------------------------------------- |
| `lidarr_eventtype`               | Henting                                                               |
| `lidarr_artist_id`               | `artist.Id`                                                           |
| `lidarr_artist_name`             | `artist.Metadata.Value.Name`                                          |
| `lidarr_artist_mbid`             | `artist.Metadata.Value.ForeignArtistId`                               |
| `lidarr_artist_type`             | `artist.Metadata.Value.Type`                                          |
| `lidarr_release_albumcount`      | `remoteAlbum.Albums.Count`                                            |
| `lidarr_release_albumreleasedates` | Komma-separert liste over albumutgivelsesdatoer                      |
| `lidarr_release_albumtitles`     | Pipe-separert liste over albumtitler                                  |
| `lidarr_release_albummbids`      | Pipe-separert liste over album-ID-er for eksterne tjenester (f.eks. MusicBrainz) |
| `lidarr_release_title`           | `remoteAlbum.Release.Title`                                           |
| `lidarr_release_indexer`         | `remoteAlbum.Release.Indexer`                                         |
| `lidarr_release_size`            | `remoteAlbum.Release.Size`                                            |
| `lidarr_release_quality`         | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                    |
| `lidarr_release_qualityversion`  | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`                |
| `lidarr_release_releasegroup`    | `releaseGroup`                                                        |
| `lidarr_download_client`         | `message.DownloadClient`                                              |
| `lidarr_download_id`             | `message.DownloadId`                                                  |

## Ved import / Ved oppgradering

| Miljøvariabel         | Detaljer                                  |
| --------------------- | ---------------------------------------- |
| `lidarr_eventtype`    | Albumnedlasting                           |
| `lidarr_artist_id`    | `artist.Id`                              |
| `lidarr_artist_name`  | `artist.Metadata.Value.Name`             |
| `lidarr_artist_path`  | `artist.Path`                            |
| `lidarr_artist_mbid`  | `artist.Metadata.Value.ForeignArtistId`  |
| `lidarr_artist_type`  | `artist.Metadata.Value.Type`             |
| `lidarr_album_id`     | `album.Id`                               |
| `lidarr_album_title`  | `album.Title`                            |
| `lidarr_album_mbid`   | `album.ForeignAlbumId`                   |
| `lidarr_albumrelease_mbid` | `release.ForeignReleaseId`               |
| `lidarr_album_releasedate` | `album.ReleaseDate`                      |
| `lidarr_download_client` | `message.DownloadClient`                 |
| `lidarr_download_id` | `message.DownloadId`                     |
| `lidarr_addedtrackpaths` | Pipe-separert liste over tilføyde sporbaner |
| `lidarr_deletedpaths` | Pipe-separert liste over slettede filer     |

## Omdøping

| Miljøvariabel       | Detaljer                                 |
| ------------------- | ---------------------------------------- |
| `lidarr_eventtype`  | Omdøping                                |
| `lidarr_artist_id`  | `artist.Id`                             |
| `lidarr_artist_name` | `artist.Metadata.Value.Name`            |
| `lidarr_artist_path` | `artist.Path`                           |
| `lidarr_artist_mbid` | `artist.Metadata.Value.ForeignArtistId` |

## Endre merking av spor

| Miljøvariabel                     | Detaljer                                 |
| -------------------------------- | ---------------------------------------- |
| `lidarr_eventtype`                | EndreMerkingAvSpor                       |
| `lidarr_artist_id`                | `artist.Id`                              |
| `lidarr_artist_name`              | `artist.Metadata.Value.Name`             |
| `lidarr_artist_path`              | `artist.Path`                            |
| `lidarr_artist_mbid`              | `artist.Metadata.Value.ForeignArtistId`  |
| `lidarr_artist_type`              | `artist.Metadata.Value.Type`             |
| `lidarr_album_id`                 | `album.Id`                               |
| `lidarr_album_title`              | `album.Title`                            |
| `lidarr_album_mbid`               | `album.ForeignAlbumId`                   |
| `lidarr_albumrelease_mbid`        | `release.ForeignReleaseId`               |
| `lidarr_album_releasedate`        | `album.ReleaseDate`                      |
| `lidarr_trackfile_id`             | `trackFile.Id`                           |
| `lidarr_trackfile_trackcount`     | `trackFile.Tracks.Value.Count`           |
| `lidarr_trackfile_path`           | `trackFile.Path`                         |
| `lidarr_trackfile_tracknumbers`   | Komma-separert liste over spornumre      |
| `lidarr_trackfile_tracktitles`    | Pipe-separert liste over spornavn        |
| `lidarr_trackfile_quality`        | `trackFile.Quality.Quality.Name`         |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`     |
| `lidarr_trackfile_releasegroup`   | `trackFile.ReleaseGroup`                 |
| `lidarr_trackfile_scenename`      | `trackFile.SceneName`                    |
| `lidarr_tags_diff`                | `message.Diff.ToJson()`                  |
| `lidarr_tags_scrubbed`            | `message.Scrubbed`                       |

## Helseproblem

| Miljøvariabel                 | Detaljer                                 |
| ---------------------------- | ---------------------------------------- |
| `lidarr_eventtype`           | Helseproblem                             |
| `lidarr_health_issue_level`  | `nameof(healthCheck.Type)`               |
| `lidarr_health_issue_message` | `healthCheck.Message`                    |
| `lidarr_health_issue_type`   | `healthCheck.Source.Name`                |
| `lidarr_health_issue_wiki`   | Wiki-URL for hjelpesiden for helseproblemet |

## Test

Når du legger til skriptet i Lidarr og klikker på 'Test', vil skriptet bli kalt med følgende parametere. Skriptet bør kunne ignorere eventuelle ikke-støttede hendelsestyper på en hensiktsmessig måte.

| Miljøvariabel     | Detaljer |
| ----------------- | -------- |
| `lidarr_eventtype` | Test     |