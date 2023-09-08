---
title: Aangepaste scripts in Radarr
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

Als je een aangepast script wilt activeren, kun je hier meer informatie vinden. Scripts worden aan Radarr toegevoegd via de [Verbindingsinstellingen](/radarr/settings#connections).

# Overzicht

Radarr kan een aangepast script uitvoeren wanneer films worden geïmporteerd of hernoemd. Afhankelijk van de actie worden verschillende parameters meegegeven. Parameters worden aan het script doorgegeven via omgevingsvariabelen.

## Radarr-logboeken

Houd er rekening mee dat het volgende alleen wordt gelogd voor aangepaste scripts:

- Uitvoer van het script `stdout` wordt gelogd als `Debug`
- Uitvoer van het script `stderr` wordt gelogd als `Info`
- De trigger van het script wordt gelogd als `Trace`

# Omgevingsvariabelen

## Bij het downloaden

| Omgevingsvariabele                  | Details                                                                                      |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                  | `Grab`                                                                                       |
| `radarr_download_client`            | Downloadclient (leeg als onbekend)                                                           |
| `radarr_download_id`                | Hash van het torrent-/NZB-bestand (wordt gebruikt om de download uniek te identificeren in de downloadclient) |
| `radarr_movie_id`                   | Interne ID van de film                                                                      |
| `radarr_movie_imdbid`               | IMDb ID van de film (leeg als onbekend)                                                      |
| `radarr_movie_in_cinemas_date`      | Releasedatum in de bioscoop (leeg als onbekend)                                              |
| `radarr_movie_physical_release_date`| Fysieke releasedatum (leeg als onbekend)                                                     |
| `radarr_movie_title`                | Titel van de film                                                                            |
| `radarr_movie_tmdbid`               | TMDb ID van de film                                                                          |
| `radarr_movie_year`                 | Jaar van uitgave van de film                                                                 |
| `radarr_release_indexer`            | Indexer waarvan de release is gedownload                                                     |
| `radarr_release_quality`            | Kwaliteitsnaam van de release, zoals gedetecteerd door Radarr                                 |
| `radarr_release_qualityversion`     | `1` is de standaardwaarde, `2` is voor de juiste versie en `3`+ kan worden gebruikt voor animeversies |
| `radarr_release_releasegroup`       | Releasegroep (leeg als onbekend)                                                             |
| `radarr_release_size`               | Grootte van de release, zoals gerapporteerd door de indexer                                  |
| `radarr_release_title`              | Titel van de torrent-/NZB-bestand                                                            |

## Bij importeren/bij upgraden

| Omgevingsvariabele                  | Details                                                                                      |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                  | `Download`                                                                                   |
| `radarr_download_id`                | Hash van het torrent-/NZB-bestand (wordt gebruikt om de download uniek te identificeren in de downloadclient) |
| `radarr_download_client`            | Downloadclient                                                                              |
| `radarr_isupgrade`                  | `True` als een bestaand bestand wordt geüpgraded, `False` anders                              |
| `radarr_movie_id`                   | Interne ID van de film                                                                      |
| `radarr_movie_imdbid`               | IMDb ID van de film (leeg als onbekend)                                                      |
| `radarr_movie_in_cinemas_date`      | Releasedatum in de bioscoop (leeg als onbekend)                                              |
| `radarr_movie_path`                 | Volledig pad naar de film                                                                    |
| `radarr_movie_physical_release_date`| Fysieke releasedatum (leeg als onbekend)                                                     |
| `radarr_movie_title`                | Titel van de film                                                                            |
| `radarr_movie_tmdbid`               | TMDb ID van de film                                                                          |
| `radarr_movie_year`                 | Jaar van uitgave van de film                                                                 |
| `radarr_moviefile_id`               | Interne ID van het filmbestand                                                               |
| `radarr_moviefile_relativepath`     | Pad naar het filmbestand, relatief aan het filmpad                                           |
| `radarr_moviefile_path`             | Volledig pad naar het filmbestand                                                            |
| `radarr_moviefile_quality`          | Kwaliteitsnaam van de release, zoals gedetecteerd door Radarr                                 |
| `radarr_moviefile_qualityversion`   | `1` is de standaardwaarde, `2` is voor de juiste versie en `3`+ kan worden gebruikt voor animeversies |
| `radarr_moviefile_releasegroup`     | Releasegroep (leeg als onbekend)                                                             |
| `radarr_moviefile_scenename`        | Oorspronkelijke releasenaam (leeg als onbekend)                                              |
| `radarr_moviefile_sourcepath`       | Volledig pad naar het geïmporteerde filmbestand                                              |
| `radarr_moviefile_sourcefolder`     | Volledig pad naar de map waaruit het filmbestand is geïmporteerd                             |
| `radarr_deletedrelativepaths`       | Lijst van bestanden die zijn verwijderd om dit bestand te importeren, gescheiden door `|`     |
| `radarr_deletedpaths`               | Lijst van volledige paden naar bestanden die zijn verwijderd om dit bestand te importeren, gescheiden door `|` |

## Bij hernoemen

| Omgevingsvariabele                      | Details                                          |
| --------------------------------------- | ------------------------------------------------ |
| `radarr_eventtype`                      | `Rename`                                         |
| `radarr_movie_id`                       | Interne ID van de film                           |
| `radarr_movie_title`                    | Titel van de film                                |
| `radarr_movie_year`                     | Uitgavejaar van de film                          |
| `radarr_movie_path`                     | Volledig pad naar de film                        |
| `radarr_movie_imdbid`                   | IMDb ID van de film (leeg als onbekend)          |
| `radarr_movie_tmdbid`                   | TMDb ID van de film                              |
| `radarr_movie_in_cinemas_date`          | Releasedatum in de bioscoop (leeg als onbekend) |
| `radarr_movie_physical_release_date`    | Fysieke/web release datum (leeg als onbekend)   |
| `radarr_moviefile_ids`                  | Door `,` gescheiden lijst van bestands-ID('s)    |
| `radarr_moviefile_relativepaths`        | Door `|` gescheiden lijst van relatieve pad(en)  |
| `radarr_moviefile_paths`                | Door `|` gescheiden lijst van pad(en)            |
| `radarr_moviefile_previousrelativepaths`| Door `|` gescheiden lijst van vorige relatieve pad(en) |
| `radarr_moviefile_previouspaths`        | Door `|` gescheiden lijst van vorige pad(en)     |

## Over Gezondheidscontrole

| Omgevingsvariabele           | Details                                                      |
| ---------------------------- | ------------------------------------------------------------ |
| `radarr_eventtype`           | `HealthIssue`                                                |
| `radarr_health_issue_level`  | Type gezondheidsprobleem (`Ok`, `Notice`, `Warning` of `Error`) |
| `radarr_health_issue_message`| Bericht van het gezondheidsprobleem                          |
| `radarr_health_issue_type`   | Gebied dat is mislukt en het gezondheidsprobleem heeft veroorzaakt |
| `radarr_health_issue_wiki`   | Wiki-URL (leeg als deze niet bestaat)                        |

## Over Applicatie-update

| Omgevingsvariabele             | Details                              |
| ------------------------------ | ------------------------------------ |
| `radarr_eventtype`             | `ApplicationUpdate`                  |
| `radarr_update_message`        | Bericht van de update                |
| `radarr_update_newversion`     | Versie waar Radarr naar is bijgewerkt (string) |
| `radarr_update_previousversion`| Versie waar Radarr van is bijgewerkt (string) |

## Over Test

Wanneer het script aan Radarr wordt toegevoegd en op 'Test' wordt geklikt, wordt het script aangeroepen met de volgende parameters. Het script moet in staat zijn om eventuele niet-ondersteunde gebeurtenistypen op een goede manier te negeren.

| Omgevingsvariabele | Details |
| ------------------ | ------- |
| `radarr_eventtype` | `Test`  |