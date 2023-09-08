---
title: Sonarr egendefinerte skript
description: 
published: true
date: 2022-06-13T15:52:03.477Z
tags: sonarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:53.999Z
---

Hvis du ønsker å utløse et egendefinert skript, kan du finne mer informasjon her. Skript legges til i Sonarr via [Tilkoblingsinnstillinger](/sonarr/settings#connections).

# Oversikt

Sonarr kan kjøre et egendefinert skript når en episode er nyimportert eller omdøpt. Avhengig av handlingen, blir forskjellige parametere levert. Parametere blir sendt til skriptet gjennom miljøvariabler.

## Sonarr-logger

Merk at følgende bare blir logget for egendefinerte skript:

- Skriptets `stdout`-utdata blir logget som `Debug`
- Skriptets `stderr`-utdata blir logget som `Info`
- Utløseren for skriptet blir logget som `Trace`

# Miljøvariabler

## Ved opptak

| Miljøvariabel                          | Detaljer                                                                                     |
| -------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                     | `Grab`                                                                                       |
| `sonarr_series_id`                     | Intern ID for serien                                                                        |
| `sonarr_series_title`                  | Tittel på serien                                                                             |
| `sonarr_series_tvdbid`                 | TVDB-ID for serien                                                                           |
| `sonarr_series_tvmazeid`               | TVMaze-ID for serien                                                                         |
| `sonarr_series_imdbid`                 | IMDB-ID for serien (tom hvis ukjent)                                                         |
| `sonarr_series_type`                   | Type serien (`Anime`, `Daily` eller `Standard`)                                              |
| `sonarr_release_episodecount`          | Antall episoder i utgivelsen                                                                |
| `sonarr_release_seasonnumber`          | Sesongnummer fra utgivelsen                                                                 |
| `sonarr_release_episodenumbers`        | Komma-separert liste over episodenumre                                                      |
| `sonarr_release_absoluteepisodenumbers`| Komma-separert liste over absolutte episodenumre                                             |
| `sonarr_release_episodeairdates`       | Komma-separert liste over sendingsdatoer fra originalnettverket                             |
| `sonarr_release_episodeairdatesutc`    | Komma-separert liste over sendingsdatoer i UTC                                               |
| `sonarr_release_episodetitles`         | `\|`-separert liste over episodetitler                                                      |
| `sonarr_release_title`                 | Torrent-/NZB-tittel                                                                          |
| `sonarr_release_indexer`               | Indekser fra hvilken utgivelsen ble hentet                                                  |
| `sonarr_release_size`                  | Størrelsen på utgivelsen, slik den er rapportert av indekseren                               |
| `sonarr_release_quality`               | Kvalitetsnavn på utgivelsen, slik det er oppdaget av Sonarr                                  |
| `sonarr_release_qualityversion`        | `1` er standard, `2` er for riktig, og `3`+ kan brukes for animeversjoner                   |
| `sonarr_release_releasegroup`          | Utgivelsesgruppe (tom hvis ukjent)                                                           |
| `sonarr_download_client`               | Nedlastingsklient                                                                            |
| `sonarr_download_id`                   | Hash for torrent-/NZB-filen (brukes til å identifisere nedlastingen unikt i nedlastingsklienten) |

## Ved import/oppgradering

| Miljøvariabel                        | Detaljer                                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                   | `Download`                                                                                   |
| `sonarr_isupgrade`                   | `True` når en eksisterende fil oppgraderes, `False` ellers                                    |
| `sonarr_series_id`                   | Intern ID for serien                                                                         |
| `sonarr_series_title`                | Tittel på serien                                                                             |
| `sonarr_series_path`                 | Full sti til serien                                                                          |
| `sonarr_series_tvdbid`               | TVDB-ID for serien                                                                           |
| `sonarr_series_tvmazeid`             | TVMaze-ID for serien                                                                         |
| `sonarr_series_imdbid`               | IMDB-ID for serien (tom hvis ukjent)                                                         |
| `sonarr_series_type`                 | Type serien (`Anime`, `Daily` eller `Standard`)                                              |
| `sonarr_episodefile_id`              | Intern ID for episodens fil                                                                 |
| `sonarr_episodefile_episodecount`    | Antall episoder i filen                                                                     |
| `sonarr_episodefile_relativepath`    | Sti til episodens fil, relativt til seriens sti                                              |
| `sonarr_episodefile_path`            | Full sti til episodens fil                                                                  |
| `sonarr_episodefile_episodeids`      | Intern ID(er) for episodens fil                                                             |
| `sonarr_episodefile_seasonnumber`    | Sesongnummer for episodens fil                                                              |
| `sonarr_episodefile_episodenumbers`  | Komma-separert liste over episodenumre                                                      |
| `sonarr_episodefile_episodeairdates` | Komma-separert liste over sendingsdatoer fra originalnettverket                              |
| `sonarr_episodefile_episodeairdatesutc` | Komma-separert liste over sendingsdatoer i UTC                                              |
| `sonarr_episodefile_episodetitles`   | `\|`-separert liste over episodetitler                                                      |
| `sonarr_episodefile_quality`         | Kvalitetsnavn på episodens fil, som oppdaget av Sonarr                                       |
| `sonarr_episodefile_qualityversion`  | `1` er standard, `2` er for riktig, og `3`+ kan brukes for animeversjoner                    |
| `sonarr_episodefile_releasegroup`    | Utgivelsesgruppe (tom hvis ukjent)                                                           |
| `sonarr_episodefile_scenename`       | Opprinnelig utgivelsesnavn (tom hvis ukjent)                                                 |
| `sonarr_episodefile_sourcepath`      | Full sti til den importerte episodens fil                                                   |
| `sonarr_episodefile_sourcefolder`    | Full sti til mappen episodens fil ble importert fra                                         |
| `sonarr_download_client`             | Nedlastingsklient                                                                           |
| `sonarr_download_id`                 | Hash for torrent-/NZB-filen (brukes til å identifisere nedlastingen i nedlastingsklienten)   |
| `sonarr_deletedrelativepaths`        | `\|`-separert liste over filer som ble slettet for å importere denne filen                    |
| `sonarr_deletedpaths`                | `\|`-separert liste over fullstendige stier til filer som ble slettet for å importere denne filen |

## Ved omdøping

| Miljøvariabel            | Detaljer                                              |
| ----------------------- | ---------------------------------------------------- |
| `sonarr_eventtype`      | `Rename`                                              |
| `sonarr_series_id`      | Intern ID for serien                                 |
| `sonarr_series_title`   | Tittel på serien                                      |
| `sonarr_series_path`    | Full sti til serien                                  |
| `sonarr_series_tvdbid`  | TVDB-ID for serien                                   |
| `sonarr_series_tvmazeid`| TVMaze-ID for serien                                 |
| `sonarr_series_imdbid`  | IMDB-ID for serien (tom hvis ukjent)                  |
| `sonarr_series_type`    | Type serien (`Anime`, `Daily` eller `Standard`)       |

## Ved sletting av episodens fil

| Miljøvariabel                          | Detaljer                                                                         |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`                      | Intern ID for serien                                                            |
| `sonarr_series_title`                   | Tittel på serien                                                                 |
| `sonarr_series_path`                    | Full sti til serien                                                              |
| `sonarr_series_tvdbid`                  | TVDB-ID for serien                                                               |
| `sonarr_series_tvmazeid`                | TVMaze-ID for serien                                                             |
| `sonarr_series_imdbid`                  | IMDB-ID for serien (tom hvis ukjent)                                             |
| `sonarr_series_type`                    | Type serie (`Anime`, `Daily` eller `Standard`)                                   |
| `sonarr_episodefile_id`                 | Intern ID for episodens fil                                                     |
| `sonarr_episodefile_episodecount`       | Antall episoder i filen                                                         |
| `sonarr_episodefile_relativepath`       | Sti til episodens fil, relativt til seriens sti                                  |
| `sonarr_episodefile_path`               | Full sti til episodens fil                                                      |
| `sonarr_episodefile_episodeids`         | Intern ID for episodens fil(er)                                                 |
| `sonarr_episodefile_seasonnumber`       | Sesongnummer for episodens fil                                                  |
| `sonarr_episodefile_episodenumbers`     | Komma-separert liste over episodenumre                                          |
| `sonarr_episodefile_episodeairdates`    | Komma-separert liste over sendingsdatoer fra originalnettverket                   |
| `sonarr_episodefile_episodeairdatesutc` | Komma-separert liste over sendingsdatoer i UTC                                   |
| `sonarr_episodefile_episodetitles`      | `\|`-separert liste over episodetitler                                           |
| `sonarr_episodefile_quality`            | Kvalitetsnavn på episodens fil, som detektert av Sonarr                           |
| `sonarr_episodefile_qualityversion`     | `1` er standard, `2` er for riktig, og `3`+ kan brukes for animeversjoner        |
| `sonarr_episodefile_releasegroup`       | Utgivelsesgruppe (tom hvis ukjent)                                               |
| `sonarr_episodefile_scenename`          | Originalt utgivelsesnavn (tom hvis ukjent)                                       |

## Ved sletting av serie

| Miljøvariabel               | Detaljer                                                                         |
| ---------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`           | `SeriesDelete`                                                                   |
| `sonarr_series_id`           | Intern ID for serien                                                            |
| `sonarr_series_title`        | Tittel på serien                                                                 |
| `sonarr_series_path`         | Full sti til serien                                                              |
| `sonarr_series_tvdbid`       | TVDB-ID for serien                                                               |
| `sonarr_series_imdbid`       | IMDB-ID for serien (tom hvis ukjent)                                             |
| `sonarr_series_type`         | Type serie (`Anime`, `Daily` eller `Standard`)                                   |
| `sonarr_series_deletedfiles` | `True` når alternativet for sletting av filer er valgt, ellers `False`            |

## Ved helseproblem

| Miljøvariabel                | Detaljer                                                                         |
| ----------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`            | `HealthIssue`                                                                    |
| `sonarr_health_issue_level`   | Type helseproblem (`Ok`, `Notice`, `Warning` eller `Error`)                       |
| `sonarr_health_issue_message` | Melding fra helseproblemet                                                       |
| `sonarr_health_issue_type`    | Område som feilet og utløste helseproblemet                                       |
| `sonarr_health_issue_wiki`    | Wiki-URL (tom hvis den ikke finnes)                                               |

## Ved oppdatering av applikasjonen

| Miljøvariabel                  | Detaljer                                                                         |
| ----------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`            | `ApplicationUpdate`                                                              |
| `sonarr_update_message`       | Melding fra oppdateringen                                                        |
| `sonarr_update_newversion`    | Versjon Sonarr ble oppdatert til (streng)                                         |
| `sonarr_update_previousversion` | Versjon Sonarr ble oppdatert fra (streng)                                       |

## Ved test

Når du legger til skriptet i Sonarr og klikker på 'Test', vil skriptet bli kalt med følgende parametere. Skriptet bør kunne ignorere eventuelle ikke-støttede hendelsestyper.

| Miljøvariabel                | Detaljer                                                                         |
| ---------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`           | `Test`                                                                           |