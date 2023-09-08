---
title: Radarr Anpassade Skript
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, behöver-kärlek, anpassade skript
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

Om du vill utlösa ett anpassat skript kan du hitta mer information här. Skript läggs till i Radarr via [Anslutningsinställningar](/radarr/settings#connections).

# Översikt

Radarr kan köra ett anpassat skript när filmer importeras eller byter namn. Beroende på åtgärden tillhandahålls olika parametrar. Parametrar skickas till skriptet genom miljövariabler.

## Radarr-loggar

Observera att följande endast loggas för anpassade skript:

- Skriptets `stdout`-utdata loggas som `Debug`
- Skriptets `stderr`-utdata loggas som `Info`
- Utlösningen av skriptet loggas som `Trace`

# Miljövariabler

## Vid hämtning

| Miljövariabel                       | Detaljer                                                                                     |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                  | `Grab`                                                                                       |
| `radarr_download_client`            | Hämta klient (tom om okänd)                                                                  |
| `radarr_download_id`                | Hash av torrent-/NZB-filen (används för att unikt identifiera hämtningen i hämtaklienten)    |
| `radarr_movie_id`                   | Intern ID för filmen                                                                         |
| `radarr_movie_imdbid`               | IMDb-ID för filmen (tom om okänd)                                                            |
| `radarr_movie_in_cinemas_date`      | Datum för biopremiär (tom om okänd)                                                          |
| `radarr_movie_physical_release_date`| Datum för fysisk utgivning (tom om okänd)                                                    |
| `radarr_movie_title`                | Titel på filmen                                                                              |
| `radarr_movie_tmdbid`               | TMDb-ID för filmen                                                                           |
| `radarr_movie_year`                 | Utgivningsår för filmen                                                                      |
| `radarr_release_indexer`            | Indexer från vilken utgåvan hämtades                                                        |
| `radarr_release_quality`            | Kvalitetsnamn på utgåvan, som detekterats av Radarr                                           |
| `radarr_release_qualityversion`     | `1` är standard, `2` är för korrekt, och `3`+ kan användas för anime-versioner               |
| `radarr_release_releasegroup`       | Utgivargrupp (tom om okänd)                                                                  |
| `radarr_release_size`               | Storlek på utgåvan, enligt indexeringskällan                                                 |
| `radarr_release_title`              | Titel på torrent-/NZB-filen                                                                  |

## Vid import/uppgradering

| Miljövariabel                       | Detaljer                                                                                     |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                  | `Download`                                                                                   |
| `radarr_download_id`                | Hash av torrent-/NZB-filen (används för att unikt identifiera hämtningen i hämtaklienten)    |
| `radarr_download_client`            | Hämta klient                                                                                 |
| `radarr_isupgrade`                  | `True` när en befintlig fil uppgraderas, `False` annars                                      |
| `radarr_movie_id`                   | Intern ID för filmen                                                                         |
| `radarr_movie_imdbid`               | IMDb-ID för filmen (tom om okänd)                                                            |
| `radarr_movie_in_cinemas_date`      | Datum för biopremiär (tom om okänd)                                                          |
| `radarr_movie_path`                 | Full sökväg till filmen                                                                      |
| `radarr_movie_physical_release_date`| Datum för fysisk utgivning (tom om okänd)                                                    |
| `radarr_movie_title`                | Titel på filmen                                                                              |
| `radarr_movie_tmdbid`               | TMDb-ID för filmen                                                                           |
| `radarr_movie_year`                 | Utgivningsår för filmen                                                                      |
| `radarr_moviefile_id`               | Intern ID för filmfilen                                                                      |
| `radarr_moviefile_relativepath`     | Sökväg till filmfilen, relativt filmens sökväg                                               |
| `radarr_moviefile_path`             | Full sökväg till filmfilen                                                                   |
| `radarr_moviefile_quality`          | Kvalitetsnamn på utgåvan, som detekterats av Radarr                                           |
| `radarr_moviefile_qualityversion`   | `1` är standard, `2` är för korrekt, och `3`+ kan användas för anime-versioner               |
| `radarr_moviefile_releasegroup`     | Utgivargrupp (tom om okänd)                                                                  |
| `radarr_moviefile_scenename`        | Ursprungligt utgåvenamn (tom om okänd)                                                       |
| `radarr_moviefile_sourcepath`       | Full sökväg till den importerade filmfilen                                                   |
| `radarr_moviefile_sourcefolder`     | Full sökväg till mappen där filmfilen importerades från                                     |
| `radarr_deletedrelativepaths`       | `|`-avgränsad lista över filer som raderades för att importera denna fil                     |
| `radarr_deletedpaths`               | `|`-avgränsad lista över fullständiga sökvägar till filer som raderades för att importera denna fil |

## Vid namnbyte

| Miljövariabel                          | Detaljer                                        |
| -------------------------------------- | ----------------------------------------------- |
| `radarr_eventtype`                     | `Rename`                                        |
| `radarr_movie_id`                      | Intern ID för filmen                            |
| `radarr_movie_title`                   | Titel på filmen                                 |
| `radarr_movie_year`                    | Utgivningsår för filmen                         |
| `radarr_movie_path`                    | Full sökväg till filmen                         |
| `radarr_movie_imdbid`                  | IMDb ID för filmen (tom om okänd)               |
| `radarr_movie_tmdbid`                  | TMDb ID för filmen                              |
| `radarr_movie_in_cinemas_date`         | Datum för biopremiär (tom om okänd)             |
| `radarr_movie_physical_release_date`   | Datum för fysisk/webbutgåva (tom om okänd)      |
| `radarr_moviefile_ids`                 | Lista med fil-ID:n separerade med `,`           |
| `radarr_moviefile_relativepaths`       | Lista med relativa sökvägar separerade med `|`  |
| `radarr_moviefile_paths`               | Lista med sökvägar separerade med `|`           |
| `radarr_moviefile_previousrelativepaths` | Lista med tidigare relativa sökvägar separerade med `|` |
| `radarr_moviefile_previouspaths`       | Lista med tidigare sökvägar separerade med `|`  |

## Om hälsokontroll

| Miljövariabel                | Detaljer                                                      |
| --------------------------- | ------------------------------------------------------------ |
| `radarr_eventtype`          | `HealthIssue`                                                |
| `radarr_health_issue_level` | Typ av hälsoproblem (`Ok`, `Notice`, `Warning` eller `Error`) |
| `radarr_health_issue_message` | Meddelande från hälsoproblemet                              |
| `radarr_health_issue_type`    | Område som misslyckades och utlöste hälsoproblemet           |
| `radarr_health_issue_wiki`    | Wiki-URL (tom om den inte finns)                            |

## Om programuppdatering

| Miljövariabel                | Detaljer                               |
| --------------------------- | -------------------------------------- |
| `radarr_eventtype`          | `ApplicationUpdate`                   |
| `radarr_update_message`     | Meddelande från uppdateringen          |
| `radarr_update_newversion`  | Version som Radarr uppdaterades till (sträng) |
| `radarr_update_previousversion` | Version som Radarr uppdaterades från (sträng) |

## Om test

När du lägger till skriptet i Radarr och klickar på 'Test' kommer skriptet att köras med följande parametrar. Skriptet bör kunna ignorera eventtyper som inte stöds.

| Miljövariabel        | Detaljer |
| -------------------- | ------- |
| `radarr_eventtype`   | `Test`  |