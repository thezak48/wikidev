---
title: Radarr Egendefinerte Skript
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

Hvis du ønsker å utløse et egendefinert skript, kan du finne mer informasjon her. Skript legges til i Radarr via [Tilkoblingsinnstillinger](/radarr/settings#connections).

# Oversikt

Radarr kan kjøre et egendefinert skript når filmer importeres eller får nytt navn. Avhengig av handlingen, blir forskjellige parametere levert. Parametere sendes til skriptet gjennom miljøvariabler.

## Radarr-logger

Merk at følgende bare blir logget for egendefinerte skript:

- Skriptets `stdout`-utdata blir logget som `Debug`
- Skriptets `stderr`-utdata blir logget som `Info`
- Utløseren av skriptet blir logget som `Trace`

# Miljøvariabler

## Ved opptak

| Miljøvariabel                       | Detaljer                                                                                     |
| ---------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                 | `Grab`                                                                                       |
| `radarr_download_client`           | Nedlastingsklient (tom hvis ukjent)                                                          |
| `radarr_download_id`               | Hash av torrent-/NZB-filen (brukes til å identifisere nedlastingen unikt i nedlastingsklienten) |
| `radarr_movie_id`                  | Intern ID for filmen                                                                         |
| `radarr_movie_imdbid`              | IMDb-ID for filmen (tom hvis ukjent)                                                          |
| `radarr_movie_in_cinemas_date`     | Kinopremieredato (tom hvis ukjent)                                                           |
| `radarr_movie_physical_release_date` | Fysisk utgivelsesdato (tom hvis ukjent)                                                     |
| `radarr_movie_title`               | Tittel på filmen                                                                             |
| `radarr_movie_tmdbid`              | TMDb-ID for filmen                                                                           |
| `radarr_movie_year`                | Utgivelsesår for filmen                                                                      |
| `radarr_release_indexer`           | Indekseringskilde som utgivelsen ble hentet fra                                              |
| `radarr_release_quality`           | Kvalitetsnavn på utgivelsen, som oppdaget av Radarr                                          |
| `radarr_release_qualityversion`    | `1` er standard, `2` er for riktig, og `3`+ kan brukes for anime-versjoner                   |
| `radarr_release_releasegroup`      | Utgivelsesgruppe (tom hvis ukjent)                                                           |
| `radarr_release_size`              | Størrelse på utgivelsen, som rapportert av indekseren                                        |
| `radarr_release_title`             | Tittel på torrent-/NZB-filen                                                                 |

## Ved import/oppgradering

| Miljøvariabel                       | Detaljer                                                                                     |
| ---------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                 | `Download`                                                                                   |
| `radarr_download_id`               | Hash av torrent-/NZB-filen (brukes til å identifisere nedlastingen unikt i nedlastingsklienten) |
| `radarr_download_client`           | Nedlastingsklient                                                                            |
| `radarr_isupgrade`                 | `True` når en eksisterende fil oppgraderes, `False` ellers                                   |
| `radarr_movie_id`                  | Intern ID for filmen                                                                         |
| `radarr_movie_imdbid`              | IMDb-ID for filmen (tom hvis ukjent)                                                          |
| `radarr_movie_in_cinemas_date`     | Kinopremieredato (tom hvis ukjent)                                                           |
| `radarr_movie_path`                | Full sti til filmen                                                                          |
| `radarr_movie_physical_release_date` | Fysisk utgivelsesdato (tom hvis ukjent)                                                     |
| `radarr_movie_title`               | Tittel på filmen                                                                             |
| `radarr_movie_tmdbid`              | TMDb-ID for filmen                                                                           |
| `radarr_movie_year`                | Utgivelsesår for filmen                                                                      |
| `radarr_moviefile_id`              | Intern ID for filmfilen                                                                      |
| `radarr_moviefile_relativepath`    | Sti til filmfilen, relativ til filmstien                                                     |
| `radarr_moviefile_path`            | Full sti til filmfilen                                                                       |
| `radarr_moviefile_quality`         | Kvalitetsnavn på utgivelsen, som oppdaget av Radarr                                          |
| `radarr_moviefile_qualityversion`  | `1` er standard, `2` er for riktig, og `3`+ kan brukes for anime-versjoner                   |
| `radarr_moviefile_releasegroup`    | Utgivelsesgruppe (tom hvis ukjent)                                                           |
| `radarr_moviefile_scenename`       | Opprinnelig utgivelsesnavn (tom hvis ukjent)                                                 |
| `radarr_moviefile_sourcepath`      | Full sti til den importerte filmfilen                                                        |
| `radarr_moviefile_sourcefolder`    | Full sti til mappen filmfilen ble importert fra                                              |
| `radarr_deletedrelativepaths`      | `|`-delt liste over filer som ble slettet for å importere denne filen                         |
| `radarr_deletedpaths`              | `|`-delt liste over full sti til filer som ble slettet for å importere denne filen            |

## Ved omdøping

| Miljøvariabel                          | Detaljer                                        |
| -------------------------------------- | ----------------------------------------------- |
| `radarr_eventtype`                     | `Rename`                                        |
| `radarr_movie_id`                      | Intern ID for filmen                           |
| `radarr_movie_title`                   | Tittel på filmen                                |
| `radarr_movie_year`                    | Utgivelsesår for filmen                        |
| `radarr_movie_path`                    | Full sti til filmen                            |
| `radarr_movie_imdbid`                  | IMDb-ID for filmen (tom hvis ukjent)            |
| `radarr_movie_tmdbid`                  | TMDb-ID for filmen                             |
| `radarr_movie_in_cinemas_date`         | Kinoutgivelsesdato (tom hvis ukjent)            |
| `radarr_movie_physical_release_date`   | Fysisk/nettutgivelsesdato (tom hvis ukjent)    |
| `radarr_moviefile_ids`                 | Liste med fil-ID(er) separert med `,`          |
| `radarr_moviefile_relativepaths`       | Liste med relative stier separert med `|`      |
| `radarr_moviefile_paths`               | Liste med stier separert med `|`               |
| `radarr_moviefile_previousrelativepaths` | Liste med tidligere relative stier separert med `|` |
| `radarr_moviefile_previouspaths`       | Liste med tidligere stier separert med `|`      |

## Ved helsesjekk

| Miljøvariabel                | Detaljer                                                       |
| --------------------------- | -------------------------------------------------------------- |
| `radarr_eventtype`          | `HealthIssue`                                                  |
| `radarr_health_issue_level` | Type helseproblem (`Ok`, `Notice`, `Warning` eller `Error`)     |
| `radarr_health_issue_message` | Melding fra helseproblemet                                    |
| `radarr_health_issue_type`  | Område som feilet og utløste helseproblemet                     |
| `radarr_health_issue_wiki`  | Wiki-URL (tom hvis den ikke finnes)                             |

## Ved oppdatering av applikasjonen

| Miljøvariabel                 | Detaljer                                      |
| ---------------------------- | --------------------------------------------- |
| `radarr_eventtype`           | `ApplicationUpdate`                           |
| `radarr_update_message`      | Melding fra oppdateringen                     |
| `radarr_update_newversion`   | Versjon Radarr ble oppdatert til (streng)     |
| `radarr_update_previousversion` | Versjon Radarr ble oppdatert fra (streng)   |

## Ved test

Når du legger til skriptet i Radarr og klikker på 'Test', vil skriptet bli kalt med følgende parametere. Skriptet bør kunne ignorere event-typer som ikke støttes.

| Miljøvariabel          | Detaljer |
| --------------------- | -------- |
| `radarr_eventtype`    | `Test`   |