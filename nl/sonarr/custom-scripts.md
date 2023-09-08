---
title: Aangepaste scripts in Sonarr
description: 
published: true
date: 2022-06-13T15:52:03.477Z
tags: sonarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:53.999Z
---

Als je een aangepast script wilt activeren, kun je hier meer informatie vinden. Scripts worden aan Sonarr toegevoegd via de [Connect-instellingen](/sonarr/settings#connections).

# Overzicht

Sonarr kan een aangepast script uitvoeren wanneer een aflevering nieuw wordt geïmporteerd of hernoemd. Afhankelijk van de actie worden verschillende parameters meegegeven. Parameters worden aan het script doorgegeven via omgevingsvariabelen.

## Sonarr-logboeken

Houd er rekening mee dat het volgende alleen wordt gelogd voor aangepaste scripts:

- Uitvoer van het script `stdout` wordt gelogd als `Debug`
- Uitvoer van het script `stderr` wordt gelogd als `Info`
- De trigger van het script wordt gelogd als `Trace`

# Omgevingsvariabelen

## Bij downloaden

| Omgevingsvariabele                    | Details                                                                                      |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Grab`                                                                                       |
| `sonarr_series_id`                      | Interne ID van de serie                                                                    |
| `sonarr_series_title`                   | Titel van de serie                                                                          |
| `sonarr_series_tvdbid`                  | TVDB-ID voor de serie                                                                       |
| `sonarr_series_tvmazeid`                | TVMaze-ID voor de serie                                                                     |
| `sonarr_series_imdbid`                  | IMDB-ID voor de serie (leeg als onbekend)                                                    |
| `sonarr_series_type`                    | Type van de serie (`Anime`, `Daily` of `Standard`)                                         |
| `sonarr_release_episodecount`           | Aantal afleveringen in de release                                                            |
| `sonarr_release_seasonnumber`           | Seizoennummer van de release                                                                   |
| `sonarr_release_episodenumbers`         | Komma-gescheiden lijst van afleveringsnummers                                                      |
| `sonarr_release_absoluteepisodenumbers` | Komma-gescheiden lijst van absolute afleveringsnummers                                             |
| `sonarr_release_episodeairdates`        | Komma-gescheiden lijst van uitzenddata van het originele netwerk                                      |
| `sonarr_release_episodeairdatesutc`     | Komma-gescheiden lijst van uitzenddata in UTC                                                     |
| `sonarr_release_episodetitles`          | Lijst van afleveringstitels gescheiden door `\|`                                                        |
| `sonarr_release_title`                  | Torrent/NZB-titel                                                                            |
| `sonarr_release_indexer`                | Indexer waarvan de release is gedownload                                                   |
| `sonarr_release_size`                   | Grootte van de release, zoals gerapporteerd door de indexer                                              |
| `sonarr_release_quality`                | Kwaliteitsnaam van de release, zoals gedetecteerd door Sonarr                                           |
| `sonarr_release_qualityversion`         | `1` is de standaardwaarde, `2` is voor de juiste versie en `3`+ kan worden gebruikt voor animeversies             |
| `sonarr_release_releasegroup`           | Releasegroep (leeg als onbekend)                                                             |
| `sonarr_download_client`                | Downloadclient                                                                              |
| `sonarr_download_id`                    | Hash van het torrent/NZB-bestand (wordt gebruikt om de download uniek te identificeren in de downloadclient) |

## Bij importeren/bij upgraden

| Omgevingsvariabele                    | Details                                                                                      |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Download`                                                                                   |
| `sonarr_isupgrade`                      | `True` wanneer een bestaand bestand wordt geüpgraded, `False` anders                           |
| `sonarr_series_id`                      | Interne ID van de serie                                                                     |
| `sonarr_series_title`                   | Titel van de serie                                                                          |
| `sonarr_series_path`                    | Volledig pad naar de serie                                                                  |
| `sonarr_series_tvdbid`                  | TVDB ID voor de serie                                                                       |
| `sonarr_series_tvmazeid`                | TVMaze ID voor de serie                                                                     |
| `sonarr_series_imdbid`                  | IMDB ID voor de serie (leeg als onbekend)                                                    |
| `sonarr_series_type`                    | Type van de serie (`Anime`, `Daily` of `Standard`)                                          |
| `sonarr_episodefile_id`                 | Interne ID van het afleveringsbestand                                                       |
| `sonarr_episodefile_episodecount`       | Aantal afleveringen in het bestand                                                          |
| `sonarr_episodefile_relativepath`       | Pad naar het afleveringsbestand, relatief aan het seriepad                                  |
| `sonarr_episodefile_path`               | Volledig pad naar het afleveringsbestand                                                    |
| `sonarr_episodefile_episodeids`         | Interne ID('s) van het afleveringsbestand                                                   |
| `sonarr_episodefile_seasonnumber`       | Seizoensnummer van het afleveringsbestand                                                    |
| `sonarr_episodefile_episodenumbers`     | Komma-gescheiden lijst van afleveringsnummers                                                |
| `sonarr_episodefile_episodeairdates`    | Komma-gescheiden lijst van uitzenddata van het originele netwerk                             |
| `sonarr_episodefile_episodeairdatesutc` | Komma-gescheiden lijst van uitzenddata in UTC                                                |
| `sonarr_episodefile_episodetitles`      | Lijst van afleveringstitels gescheiden door `\|`                                             |
| `sonarr_episodefile_quality`            | Kwaliteitsnaam van het afleveringsbestand, zoals gedetecteerd door Sonarr                     |
| `sonarr_episodefile_qualityversion`     | `1` is de standaard, `2` is voor juiste versies en `3`+ kan worden gebruikt voor animeversies |
| `sonarr_episodefile_releasegroup`       | Releasegroep (leeg als onbekend)                                                             |
| `sonarr_episodefile_scenename`          | Oorspronkelijke releasenaam (leeg als onbekend)                                              |
| `sonarr_episodefile_sourcepath`         | Volledig pad naar het geïmporteerde afleveringsbestand                                       |
| `sonarr_episodefile_sourcefolder`       | Volledig pad naar de map waaruit het afleveringsbestand is geïmporteerd                      |
| `sonarr_download_client`                | Downloadclient                                                                              |
| `sonarr_download_id`                    | Hash van het torrent/NZB-bestand (wordt gebruikt om de download uniek te identificeren in de downloadclient) |
| `sonarr_deletedrelativepaths`           | Lijst van bestanden die zijn verwijderd om dit bestand te importeren, gescheiden door `\|`    |
| `sonarr_deletedpaths`                   | Lijst van volledige paden van bestanden die zijn verwijderd om dit bestand te importeren, gescheiden door `\|` |

## Bij hernoemen

| Omgevingsvariabele     | Details                                              |
| ------------------------ | ---------------------------------------------------- |
| `sonarr_eventtype`       | `Rename`                                             |
| `sonarr_series_id`       | Interne ID van de serie                            |
| `sonarr_series_title`    | Titel van de serie                                  |
| `sonarr_series_path`     | Volledig pad naar de serie                              |
| `sonarr_series_tvdbid`   | TVDB ID voor de serie                               |
| `sonarr_series_tvmazeid` | TVMaze ID voor de serie                             |
| `sonarr_series_imdbid`   | IMDB ID voor de serie (leeg als onbekend)            |
| `sonarr_series_type`     | Type van de serie (`Anime`, `Daily` of `Standard`) |

## Bij het verwijderen van een afleveringsbestand

| Omgevingsvariabele                    | Details                                                                          |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`                      | Interne ID van de serie                                                        |
| `sonarr_series_title`                   | Titel van de serie                                                              |
| `sonarr_series_path`                    | Volledig pad naar de serie                                                      |
| `sonarr_series_tvdbid`                  | TVDB ID voor de serie                                                           |
| `sonarr_series_tvmazeid`                | TVMaze ID voor de serie                                                         |
| `sonarr_series_imdbid`                  | IMDB ID voor de serie (leeg indien onbekend)                                     |
| `sonarr_series_type`                    | Type van de serie (`Anime`, `Daily` of `Standard`)                               |
| `sonarr_episodefile_id`                 | Interne ID van het afleveringsbestand                                           |
| `sonarr_episodefile_episodecount`       | Aantal afleveringen in het bestand                                              |
| `sonarr_episodefile_relativepath`       | Pad naar het afleveringsbestand, relatief aan het pad van de serie                |
| `sonarr_episodefile_path`               | Volledig pad naar het afleveringsbestand                                         |
| `sonarr_episodefile_episodeids`         | Interne ID('s) van het afleveringsbestand                                        |
| `sonarr_episodefile_seasonnumber`       | Seizoennummer van het afleveringsbestand                                         |
| `sonarr_episodefile_episodenumbers`     | Komma-gescheiden lijst van afleveringsnummers                                    |
| `sonarr_episodefile_episodeairdates`    | Komma-gescheiden lijst van uitzenddata van het originele netwerk                  |
| `sonarr_episodefile_episodeairdatesutc` | Komma-gescheiden lijst van uitzenddata in UTC                                    |
| `sonarr_episodefile_episodetitles`      | Lijst van afleveringstitels gescheiden door `\|`                                 |
| `sonarr_episodefile_quality`            | Kwaliteitsnaam van het afleveringsbestand, zoals gedetecteerd door Sonarr         |
| `sonarr_episodefile_qualityversion`     | `1` is de standaard, `2` is voor juiste versies en `3`+ kan worden gebruikt voor animeversies |
| `sonarr_episodefile_releasegroup`       | Releasegroep (leeg indien onbekend)                                              |
| `sonarr_episodefile_scenename`          | Oorspronkelijke releasenaam (leeg indien onbekend)                                |

## Bij het verwijderen van een serie

| Omgevingsvariabele         | Details                                                                  |
| ---------------------------- | ------------------------------------------------------------------------ |
| `sonarr_eventtype`           | `SeriesDelete`                                                           |
| `sonarr_series_id`           | Interne ID van de serie                                                |
| `sonarr_series_title`        | Titel van de serie                                                      |
| `sonarr_series_path`         | Volledig pad naar de serie                                                  |
| `sonarr_series_tvdbid`       | TVDB ID voor de serie                                                   |
| `sonarr_series_imdbid`       | IMDB ID voor de serie (leeg indien onbekend)                                |
| `sonarr_series_type`         | Type van de serie (`Anime`, `Daily` of `Standard`)                     |
| `sonarr_series_deletedfiles` | `True` wanneer de optie om bestanden te verwijderen is geselecteerd, anders `False` |

## Bij een probleem met de gezondheid

| Omgevingsvariabele          | Details                                                      |
| ----------------------------- | ------------------------------------------------------------ |
| `sonarr_eventtype`            | `HealthIssue`                                                |
| `sonarr_health_issue_level`   | Type gezondheidsprobleem (`Ok`, `Notice`, `Warning` of `Error`) |
| `sonarr_health_issue_message` | Bericht van het gezondheidsprobleem                                |
| `sonarr_health_issue_type`    | Gebied dat is mislukt en het gezondheidsprobleem heeft veroorzaakt              |
| `sonarr_health_issue_wiki`    | Wiki-URL (leeg indien niet beschikbaar)                           |

## Bij een applicatie-update

| Omgevingsvariabele             | Details                               |
|--------------------------------- |-------------------------------------- |
| `sonarr_eventtype`               | `ApplicationUpdate`                   |
| `sonarr_update_message`          | Bericht van de update                   |
| `sonarr_update_newversion`       | Versie waar Sonarr naar is bijgewerkt (string)    |
| `sonarr_update_previousversion`  | Versie waar Sonarr van is bijgewerkt (string)  |

## Bij een test

Wanneer het script aan Sonarr wordt toegevoegd en op 'Test' wordt geklikt, wordt het script aangeroepen met de volgende parameters. Het script moet in staat zijn om eventuele niet-ondersteunde gebeurtenistypen te negeren.

| Omgevingsvariabele | Details |
| -------------------- | ------- |
| `sonarr_eventtype`   | `Test`  |