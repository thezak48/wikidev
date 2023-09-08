# Lidarr Anpassade Skript

Om du vill utlösa ett anpassat skript kan du hitta mer information på den här sidan. Skript läggs till i Lidarr via [Anslutningsinställningar](/lidarr/settings#connections).

## Översikt

Lidarr kan köra ett anpassat skript när en episod är nyimporterad eller omdöpt. Beroende på åtgärden tillhandahålls olika parametrar. Parametrar skickas till skriptet genom miljövariabler.

Ett anpassat skript kan vara vilket exekverbart som helst som användaren Lidarr körs som har åtkomst till det.

## Lidarr-loggar

Observera att följande endast loggas för anpassade skript:

- Skriptets `stdout`-utdata loggas som `Debug` i config/logs/Lidarr.debug.txt
- Skriptets `stderr`-utdata loggas som `Info` i config/logs/Lidarr.txt
- Utlösningen av skriptet loggas som `Trace` i config/logs/Lidarr.trace.txt

## Miljövariabler

Miljövariabler varierar beroende på händelsetypen. Avsnitten nedan visar vilka variabler som är tillgängliga för varje händelse.

> [Avsnitten nedan behöver rensas upp, organiseras och förbättras med detaljer. Visa källkoden här](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Hämta

| Miljövariabel                    | Detaljer                                                              |
| -------------------------------- | --------------------------------------------------------------------- |
| `lidarr_eventtype`               | Hämta                                                                 |
| `lidarr_artist_id`               | `artist.Id`                                                           |
| `lidarr_artist_name`             | `artist.Metadata.Value.Name`                                          |
| `lidarr_artist_mbid`             | `artist.Metadata.Value.ForeignArtistId`                               |
| `lidarr_artist_type`             | `artist.Metadata.Value.Type`                                          |
| `lidarr_release_albumcount`      | `remoteAlbum.Albums.Count`                                            |
| `lidarr_release_albumreleasedates` | Kommaavgränsad lista över albumutgivningsdatum                        |
| `lidarr_release_albumtitles`     | Pipavgränsad lista över albumtitlar                                   |
| `lidarr_release_albummbids`      | Pipavgränsad lista över albumets externa tjänst-ID (t.ex. MusicBrainz) |
| `lidarr_release_title`           | `remoteAlbum.Release.Title`                                           |
| `lidarr_release_indexer`         | `remoteAlbum.Release.Indexer`                                         |
| `lidarr_release_size`            | `remoteAlbum.Release.Size`                                            |
| `lidarr_release_quality`         | `remoteAlbum.ParsedAlbumInfo.Quality.Quality.Name`                    |
| `lidarr_release_qualityversion`  | `remoteAlbum.ParsedAlbumInfo.Quality.Revision.Version`                |
| `lidarr_release_releasegroup`    | `releaseGroup`                                                        |
| `lidarr_download_client`         | `message.DownloadClient`                                              |
| `lidarr_download_id`             | `message.DownloadId`                                                  |

## Vid import / vid uppgradering

| Miljövariabel           | Detaljer                                  |
| ----------------------- | ----------------------------------------- |
| `lidarr_eventtype`      | AlbumDownload                             |
| `lidarr_artist_id`      | `artist.Id`                               |
| `lidarr_artist_name`    | `artist.Metadata.Value.Name`              |
| `lidarr_artist_path`    | `artist.Path`                             |
| `lidarr_artist_mbid`    | `artist.Metadata.Value.ForeignArtistId`   |
| `lidarr_artist_type`    | `artist.Metadata.Value.Type`              |
| `lidarr_album_id`       | `album.Id`                                |
| `lidarr_album_title`    | `album.Title`                             |
| `lidarr_album_mbid`     | `album.ForeignAlbumId`                    |
| `lidarr_albumrelease_mbid` | `release.ForeignReleaseId`                |
| `lidarr_album_releasedate` | `album.ReleaseDate`                       |
| `lidarr_download_client` | `message.DownloadClient`                  |
| `lidarr_download_id`    | `message.DownloadId`                      |
| `lidarr_addedtrackpaths` | Pipavgränsad lista över tillagda spårbanor |
| `lidarr_deletedpaths`   | Pipavgränsad lista över raderade filer     |

## Omdöpa

| Miljövariabel         | Detaljer                                    |
| --------------------- | ------------------------------------------- |
| `lidarr_eventtype`    | Omdöpa                                      |
| `lidarr_artist_id`    | `artist.Id`                                 |
| `lidarr_artist_name`  | `artist.Metadata.Value.Name`                |
| `lidarr_artist_path`  | `artist.Path`                               |
| `lidarr_artist_mbid`  | `artist.Metadata.Value.ForeignArtistId`     |
| `lidarr_artist_type`  | `artist.Metadata.Value.Type`                |

## Retaggning av spår

| Miljövariabel                   | Detaljer                                    |
| ------------------------------ | ------------------------------------------- |
| `lidarr_eventtype`             | TrackRetag                                  |
| `lidarr_artist_id`             | `artist.Id`                                 |
| `lidarr_artist_name`           | `artist.Metadata.Value.Name`                |
| `lidarr_artist_path`           | `artist.Path`                               |
| `lidarr_artist_mbid`           | `artist.Metadata.Value.ForeignArtistId`     |
| `lidarr_artist_type`           | `artist.Metadata.Value.Type`                |
| `lidarr_album_id`              | `album.Id`                                  |
| `lidarr_album_title`           | `album.Title`                               |
| `lidarr_album_mbid`            | `album.ForeignAlbumId`                      |
| `lidarr_albumrelease_mbid`     | `release.ForeignReleaseId`                  |
| `lidarr_album_releasedate`     | `album.ReleaseDate`                         |
| `lidarr_trackfile_id`          | `trackFile.Id`                              |
| `lidarr_trackfile_trackcount`  | `trackFile.Tracks.Value.Count`              |
| `lidarr_trackfile_path`        | `trackFile.Path`                            |
| `lidarr_trackfile_tracknumbers` | Kommaavgränsad lista över spårnummer        |
| `lidarr_trackfile_tracktitles`  | Pipavgränsad lista över spårtitlar          |
| `lidarr_trackfile_quality`     | `trackFile.Quality.Quality.Name`            |
| `lidarr_trackfile_qualityversion` | `trackFile.Quality.Revision.Version`        |
| `lidarr_trackfile_releasegroup` | `trackFile.ReleaseGroup`                    |
| `lidarr_trackfile_scenename`    | `trackFile.SceneName`                       |
| `lidarr_tags_diff`              | `message.Diff.ToJson()`                     |
| `lidarr_tags_scrubbed`          | `message.Scrubbed`                          |

## Hälsoproblem

| Miljövariabel                | Detaljer                                    |
| --------------------------- | ------------------------------------------- |
| `lidarr_eventtype`          | HealthIssue                                 |
| `lidarr_health_issue_level` | `nameof(healthCheck.Type)`                   |
| `lidarr_health_issue_message` | `healthCheck.Message`                       |
| `lidarr_health_issue_type`  | `healthCheck.Source.Name`                   |
| `lidarr_health_issue_wiki`  | Wiki-URL för hjälpsidan för hälsoproblem     |

## Test

När du lägger till skriptet i Lidarr och klickar på "Test" kommer skriptet att köras med följande parametrar. Skriptet bör kunna ignorera eventtyper som inte stöds på ett korrekt sätt.

| Miljövariabel       | Detaljer |
| ------------------- | -------- |
| `lidarr_eventtype`  | Test     |