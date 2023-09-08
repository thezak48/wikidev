---
title: Sonarr Brugerdefinerede Scripts
description: 
published: true
date: 2022-06-13T15:52:03.477Z
tags: sonarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:53.999Z
---

Hvis du vil udløse et brugerdefineret script, kan du finde flere detaljer her. Scripts tilføjes til Sonarr via [Forbindelsesindstillingerne](/sonarr/settings#connections).

# Oversigt

Sonarr kan udføre et brugerdefineret script, når en episode er nyimporteret eller omdøbt. Afhængigt af handlingen leveres forskellige parametre. Parametrene sendes til scriptet via miljøvariabler.

## Sonarr-logfiler

Bemærk, at følgende kun logges for brugerdefinerede scripts:

- Scriptets `stdout`-output logges som `Debug`
- Scriptets `stderr`-output logges som `Info`
- Udløseren af scriptet logges som `Trace`

# Miljøvariabler

## Ved Grab

| Miljøvariabel                           | Detaljer                                                                                     |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Grab`                                                                                       |
| `sonarr_series_id`                      | Intern ID for serien                                                                         |
| `sonarr_series_title`                   | Titel på serien                                                                              |
| `sonarr_series_tvdbid`                  | TVDB-ID for serien                                                                           |
| `sonarr_series_tvmazeid`                | TVMaze-ID for serien                                                                         |
| `sonarr_series_imdbid`                  | IMDB-ID for serien (tom, hvis ukendt)                                                        |
| `sonarr_series_type`                    | Type af serien (`Anime`, `Daily` eller `Standard`)                                           |
| `sonarr_release_episodecount`           | Antal episoder i udgivelsen                                                                 |
| `sonarr_release_seasonnumber`           | Sæsonnummer fra udgivelsen                                                                   |
| `sonarr_release_episodenumbers`         | Komma-separeret liste over episodenumre                                                     |
| `sonarr_release_absoluteepisodenumbers` | Komma-separeret liste over absolutte episodenumre                                            |
| `sonarr_release_episodeairdates`        | Komma-separeret liste over luftdatoer fra det oprindelige netværk                            |
| `sonarr_release_episodeairdatesutc`     | Komma-separeret liste over luftdatoer i UTC                                                  |
| `sonarr_release_episodetitles`          | `\|`-separeret liste over episodetitler                                                      |
| `sonarr_release_title`                  | Torrent/NZB-titel                                                                            |
| `sonarr_release_indexer`                | Indexer, hvorfra udgivelsen blev hentet                                                      |
| `sonarr_release_size`                   | Størrelsen på udgivelsen, som rapporteret af indexeret                                       |
| `sonarr_release_quality`                | Kvalitetsnavn på udgivelsen, som detekteret af Sonarr                                         |
| `sonarr_release_qualityversion`         | `1` er standard, `2` er til korrekt og `3`+ kan bruges til anime-versioner                  |
| `sonarr_release_releasegroup`           | Udgivelsesgruppe (tom, hvis ukendt)                                                          |
| `sonarr_download_client`                | Downloadklient                                                                              |
| `sonarr_download_id`                    | Hash for torrent-/NZB-filen (bruges til entydigt at identificere downloaden i downloadklienten) |

## Ved Import/Ved Opgradering

| Miljøvariabel                | Detaljer                                                                                     |
| ---------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`           | `Download`                                                                                   |
| `sonarr_isupgrade`           | `True`, når en eksisterende fil opgraderes, `False` ellers                                   |
| `sonarr_series_id`           | Intern ID for serien                                                                        |
| `sonarr_series_title`        | Titel på serien                                                                             |
| `sonarr_series_path`         | Fuld sti til serien                                                                         |
| `sonarr_series_tvdbid`       | TVDB ID for serien                                                                          |
| `sonarr_series_tvmazeid`     | TVMaze ID for serien                                                                        |
| `sonarr_series_imdbid`       | IMDB ID for serien (tom, hvis ukendt)                                                        |
| `sonarr_series_type`         | Type af serien (`Anime`, `Daily` eller `Standard`)                                           |
| `sonarr_episodefile_id`      | Intern ID for episodens fil                                                                |
| `sonarr_episodefile_episodecount` | Antal episoder i filen                                                                 |
| `sonarr_episodefile_relativepath` | Sti til episodens fil, relativ til seriestien                                         |
| `sonarr_episodefile_path`    | Fuld sti til episodens fil                                                                  |
| `sonarr_episodefile_episodeids` | Intern(e) ID(er) for episodens fil                                                      |
| `sonarr_episodefile_seasonnumber` | Sæsonnummer for episodens fil                                                          |
| `sonarr_episodefile_episodenumbers` | Komma-separeret liste over episodenumre                                              |
| `sonarr_episodefile_episodeairdates` | Komma-separeret liste over udsendelsesdatoer fra originalnetværket                   |
| `sonarr_episodefile_episodeairdatesutc` | Komma-separeret liste over udsendelsesdatoer i UTC                                  |
| `sonarr_episodefile_episodetitles` | `\|`-separeret liste over episodetitler                                               |
| `sonarr_episodefile_quality` | Kvalitetsnavn for episodens fil, som detekteret af Sonarr                                 |
| `sonarr_episodefile_qualityversion` | `1` er standard, `2` er til korrekte filer, og `3`+ kan bruges til animeversioner   |
| `sonarr_episodefile_releasegroup` | Udgivelsesgruppe (tom, hvis ukendt)                                                      |
| `sonarr_episodefile_scenename` | Oprindeligt udgivelsesnavn (tom, hvis ukendt)                                              |
| `sonarr_episodefile_sourcepath` | Fuld sti til den importerede episodens fil                                                |
| `sonarr_episodefile_sourcefolder` | Fuld sti til mappen, som episodens fil blev importeret fra                               |
| `sonarr_download_client`    | Downloadklient                                                                             |
| `sonarr_download_id`        | Hash for torrent-/NZB-filen (bruges til entydigt at identificere downloaden i downloadklienten) |
| `sonarr_deletedrelativepaths` | `\|`-separeret liste over filer, der blev slettet for at importere denne fil                |
| `sonarr_deletedpaths`       | `\|`-separeret liste over fulde stier til filer, der blev slettet for at importere denne fil |

## Ved omdøbning

| Miljøvariabel                | Detaljer                                              |
| ---------------------------- | ---------------------------------------------------- |
| `sonarr_eventtype`           | `Rename`                                             |
| `sonarr_series_id`           | Intern ID for serien                                 |
| `sonarr_series_title`        | Titel på serien                                      |
| `sonarr_series_path`         | Fuld sti til serien                                  |
| `sonarr_series_tvdbid`       | TVDB ID for serien                                   |
| `sonarr_series_tvmazeid`     | TVMaze ID for serien                                 |
| `sonarr_series_imdbid`       | IMDB ID for serien (tom, hvis ukendt)                 |
| `sonarr_series_type`         | Type af serien (`Anime`, `Daily` eller `Standard`)    |

## Ved sletning af episodens fil

| Miljøvariabel                    | Detaljer                                                                          |
| -------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`               | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`               | Intern ID for serien                                                            |
| `sonarr_series_title`            | Titel på serien                                                                  |
| `sonarr_series_path`             | Fuld sti til serien                                                              |
| `sonarr_series_tvdbid`           | TVDB ID for serien                                                               |
| `sonarr_series_tvmazeid`         | TVMaze ID for serien                                                             |
| `sonarr_series_imdbid`           | IMDB ID for serien (tom hvis ukendt)                                             |
| `sonarr_series_type`             | Type af serien (`Anime`, `Daily` eller `Standard`)                                |
| `sonarr_episodefile_id`          | Intern ID for episodens fil                                                     |
| `sonarr_episodefile_episodecount`| Antal episoder i filen                                                          |
| `sonarr_episodefile_relativepath`| Sti til episodens fil, relativ til seriens sti                                   |
| `sonarr_episodefile_path`        | Fuld sti til episodens fil                                                       |
| `sonarr_episodefile_episodeids`  | Intern(e) ID'er for episodens fil                                                |
| `sonarr_episodefile_seasonnumber`| Sæsonnummer for episodens fil                                                    |
| `sonarr_episodefile_episodenumbers`| Komma-separeret liste over episodenumre                                         |
| `sonarr_episodefile_episodeairdates`| Komma-separeret liste over luftdatoer fra originalt netværk                    |
| `sonarr_episodefile_episodeairdatesutc`| Komma-separeret liste over luftdatoer i UTC                                  |
| `sonarr_episodefile_episodetitles`| `\|`-separeret liste over episodetitler                                           |
| `sonarr_episodefile_quality`     | Kvalitetsnavn for episodens fil, som detekteret af Sonarr                         |
| `sonarr_episodefile_qualityversion`| `1` er standard, `2` er til korrekt, og `3`+ kan bruges til animeversioner    |
| `sonarr_episodefile_releasegroup`| Udgivelsesgruppe (tom hvis ukendt)                                               |
| `sonarr_episodefile_scenename`   | Oprindeligt udgivelsesnavn (tom hvis ukendt)                                     |

## Ved sletning af serie

| Miljøvariabel          | Detaljer                                                              |
| ----------------------| --------------------------------------------------------------------- |
| `sonarr_eventtype`    | `SeriesDelete`                                                        |
| `sonarr_series_id`    | Intern ID for serien                                                  |
| `sonarr_series_title` | Titel på serien                                                        |
| `sonarr_series_path`  | Fuld sti til serien                                                    |
| `sonarr_series_tvdbid`| TVDB ID for serien                                                     |
| `sonarr_series_imdbid`| IMDB ID for serien (tom hvis ukendt)                                  |
| `sonarr_series_type`  | Type af serien (`Anime`, `Daily` eller `Standard`)                     |
| `sonarr_series_deletedfiles`| `True`, når sletningsfilerne er valgt, ellers `False`                |

## Ved sundhedsproblem

| Miljøvariabel                | Detaljer                                                      |
| ---------------------------- | ------------------------------------------------------------- |
| `sonarr_eventtype`           | `HealthIssue`                                                 |
| `sonarr_health_issue_level`  | Type af sundhedsproblem (`Ok`, `Notice`, `Warning` eller `Error`) |
| `sonarr_health_issue_message`| Besked fra sundhedsproblemet                                  |
| `sonarr_health_issue_type`   | Område, der mislykkedes og udløste sundhedsproblemet            |
| `sonarr_health_issue_wiki`   | Wiki-URL (tom hvis den ikke findes)                            |

## Ved opdatering af applikation

| Miljøvariabel                    | Detaljer                                      |
| -------------------------------- | --------------------------------------------- |
| `sonarr_eventtype`               | `ApplicationUpdate`                           |
| `sonarr_update_message`          | Besked fra opdatering                         |
| `sonarr_update_newversion`       | Version, som Sonarr er opdateret til (streng)  |
| `sonarr_update_previousversion`  | Version, som Sonarr er opdateret fra (streng) |

## Ved test

Når du tilføjer scriptet til Sonarr og klikker på 'Test', vil scriptet blive kaldt med følgende parametre. Scriptet skal kunne ignorere eventuelle ikke-understøttede eventtyper.

| Miljøvariabel          | Detaljer |
| ----------------------| -------- |
| `sonarr_eventtype`    | `Test`   |