---
title: Radarr Brugerdefinerede Scripts
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

Hvis du vil udløse et brugerdefineret script, kan du finde flere detaljer her. Scripts tilføjes til Radarr via [Forbindelsesindstillingerne](/radarr/settings#connections).

# Oversigt

Radarr kan udføre et brugerdefineret script, når film importeres eller omdøbes. Afhængigt af handlingen leveres forskellige parametre. Parametre sendes til scriptet via miljøvariabler.

## Radarr-logs

Bemærk, at følgende kun logges for brugerdefinerede scripts:

- Scriptets `stdout`-output logges som `Debug`
- Scriptets `stderr`-output logges som `Info`
- Udløseren af scriptet logges som `Trace`

# Miljøvariabler

## Ved hentning

| Miljøvariabel                      | Detaljer                                                                                      |
| --------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                | `Grab`                                                                                       |
| `radarr_download_client`          | Downloadklient (tom, hvis ukendt)                                                            |
| `radarr_download_id`              | Hash af torrent-/NZB-filen (bruges til at identificere downloaden unikt i downloadklienten) |
| `radarr_movie_id`                 | Intern ID for filmen                                                                         |
| `radarr_movie_imdbid`             | IMDb ID for filmen (tom, hvis ukendt)                                                        |
| `radarr_movie_in_cinemas_date`    | Biografpremieredato (tom, hvis ukendt)                                                       |
| `radarr_movie_physical_release_date` | Fysisk udgivelsesdato (tom, hvis ukendt)                                                     |
| `radarr_movie_title`              | Titel på filmen                                                                              |
| `radarr_movie_tmdbid`             | TMDb ID for filmen                                                                           |
| `radarr_movie_year`               | Udgivelsesår for filmen                                                                      |
| `radarr_release_indexer`          | Indexer, hvorfra udgivelsen blev hentet                                                      |
| `radarr_release_quality`          | Kvalitetsnavn på udgivelsen, som registreret af Radarr                                        |
| `radarr_release_qualityversion`   | `1` er standard, `2` er til korrekte udgivelser, og `3`+ kan bruges til anime-versioner     |
| `radarr_release_releasegroup`     | Udgivelsesgruppe (tom, hvis ukendt)                                                          |
| `radarr_release_size`             | Størrelse på udgivelsen, som rapporteret af indexeret                                        |
| `radarr_release_title`            | Torrent-/NZB-titel                                                                           |

## Ved import/ved opgradering

| Miljøvariabel                      | Detaljer                                                                                      |
| --------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                | `Download`                                                                                   |
| `radarr_download_id`              | Hash af torrent-/NZB-filen (bruges til at identificere downloaden unikt i downloadklienten) |
| `radarr_download_client`          | Downloadklient                                                                              |
| `radarr_isupgrade`                | `True`, når en eksisterende fil opgraderes, `False` ellers                                   |
| `radarr_movie_id`                 | Intern ID for filmen                                                                         |
| `radarr_movie_imdbid`             | IMDb ID for filmen (tom, hvis ukendt)                                                        |
| `radarr_movie_in_cinemas_date`    | Biografpremieredato (tom, hvis ukendt)                                                       |
| `radarr_movie_path`               | Fuld sti til filmen                                                                          |
| `radarr_movie_physical_release_date` | Fysisk udgivelsesdato (tom, hvis ukendt)                                                     |
| `radarr_movie_title`              | Titel på filmen                                                                              |
| `radarr_movie_tmdbid`             | TMDb ID for filmen                                                                           |
| `radarr_movie_year`               | Udgivelsesår for filmen                                                                      |
| `radarr_moviefile_id`             | Intern ID for filmfilen                                                                      |
| `radarr_moviefile_relativepath`   | Sti til filmfilen i forhold til filmstien                                                    |
| `radarr_moviefile_path`           | Fuld sti til filmfilen                                                                       |
| `radarr_moviefile_quality`        | Kvalitetsnavn på udgivelsen, som registreret af Radarr                                        |
| `radarr_moviefile_qualityversion` | `1` er standard, `2` er til korrekte udgivelser, og `3`+ kan bruges til anime-versioner     |
| `radarr_moviefile_releasegroup`   | Udgivelsesgruppe (tom, hvis ukendt)                                                          |
| `radarr_moviefile_scenename`      | Oprindeligt udgivelsesnavn (tom, hvis ukendt)                                                |
| `radarr_moviefile_sourcepath`     | Fuld sti til den importerede filmfil                                                         |
| `radarr_moviefile_sourcefolder`   | Fuld sti til mappen, hvorfra filmfilen blev importeret                                       |
| `radarr_deletedrelativepaths`     | `|`-afgrænset liste over filer, der blev slettet for at importere denne fil                   |
| `radarr_deletedpaths`             | `|`-afgrænset liste over fulde stier til filer, der blev slettet for at importere denne fil   |

## Ved omdøbning

| Miljøvariabel                     | Detaljer                                         |
| --------------------------------- | ------------------------------------------------ |
| `radarr_eventtype`                | `Rename`                                         |
| `radarr_movie_id`                 | Intern ID for filmen                            |
| `radarr_movie_title`              | Titel på filmen                                  |
| `radarr_movie_year`               | Udgivelsesår for filmen                          |
| `radarr_movie_path`               | Fuld sti til filmen                              |
| `radarr_movie_imdbid`             | IMDb ID for filmen (tom hvis ukendt)             |
| `radarr_movie_tmdbid`             | TMDb ID for filmen                               |
| `radarr_movie_in_cinemas_date`    | Biografpremieredato (tom hvis ukendt)            |
| `radarr_movie_physical_release_date` | Fysisk/webudgivelsesdato (tom hvis ukendt)    |
| `radarr_moviefile_ids`            | Liste over fil-ID'er adskilt med `,`             |
| `radarr_moviefile_relativepaths`  | Liste over relative stier adskilt med `|`       |
| `radarr_moviefile_paths`          | Liste over stier adskilt med `|`                 |
| `radarr_moviefile_previousrelativepaths` | Liste over tidligere relative stier adskilt med `|` |
| `radarr_moviefile_previouspaths`  | Liste over tidligere stier adskilt med `|`       |

## Om helbredscheck

| Miljøvariabel                   | Detaljer                                                        |
| ------------------------------ | -------------------------------------------------------------- |
| `radarr_eventtype`              | `HealthIssue`                                                   |
| `radarr_health_issue_level`     | Type af helbredsproblem (`Ok`, `Notice`, `Warning` eller `Error`) |
| `radarr_health_issue_message`   | Besked fra helbredsproblemet                                    |
| `radarr_health_issue_type`      | Område, der fejlede og udløste helbredsproblemet                 |
| `radarr_health_issue_wiki`      | Wiki-URL (tom hvis den ikke findes)                              |

## Om programopdatering

| Miljøvariabel                   | Detaljer                                  |
| ------------------------------ | ----------------------------------------- |
| `radarr_eventtype`              | `ApplicationUpdate`                       |
| `radarr_update_message`         | Besked fra opdateringen                   |
| `radarr_update_newversion`      | Version, som Radarr er opdateret til (streng) |
| `radarr_update_previousversion` | Version, som Radarr er opdateret fra (streng) |

## Om test

Når du tilføjer scriptet til Radarr og klikker på 'Test', vil scriptet blive kaldt med følgende parametre. Scriptet skal kunne ignorere eventtyper, der ikke understøttes.

| Miljøvariabel        | Detaljer |
| -------------------- | -------- |
| `radarr_eventtype`   | `Test`   |