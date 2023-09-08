---
title: Sonarr Benutzerdefinierte Skripte
description: 
published: true
date: 2022-06-13T15:52:03.477Z
tags: sonarr, needs-love, benutzerdefinierte skripte
editor: markdown
dateCreated: 2021-06-16T15:55:53.999Z
---

Wenn Sie ein benutzerdefiniertes Skript auslösen möchten, finden Sie hier weitere Details. Skripte werden in Sonarr über die [Verbindungs-Einstellungen](/sonarr/settings#connections) hinzugefügt.

# Übersicht

Sonarr kann ein benutzerdefiniertes Skript ausführen, wenn eine Episode neu importiert oder umbenannt wird. Je nach Aktion werden unterschiedliche Parameter bereitgestellt. Die Parameter werden dem Skript über Umgebungsvariablen übergeben.

## Sonarr-Protokolle

Beachten Sie, dass das Folgende nur für benutzerdefinierte Skripte protokolliert wird:

- Die Ausgabe von Skript `stdout` wird als `Debug` protokolliert.
- Die Ausgabe von Skript `stderr` wird als `Info` protokolliert.
- Der Auslöser des Skripts wird als `Trace` protokolliert.

# Umgebungsvariablen

## Beim Abrufen

| Umgebungsvariable                       | Details                                                                                      |
| --------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `Grab`                                                                                       |
| `sonarr_series_id`                      | Interne ID der Serie                                                                         |
| `sonarr_series_title`                   | Titel der Serie                                                                              |
| `sonarr_series_tvdbid`                  | TVDB-ID für die Serie                                                                        |
| `sonarr_series_tvmazeid`                | TVMaze-ID für die Serie                                                                      |
| `sonarr_series_imdbid`                  | IMDB-ID für die Serie (leer, wenn unbekannt)                                                  |
| `sonarr_series_type`                    | Art der Serie (`Anime`, `Daily` oder `Standard`)                                             |
| `sonarr_release_episodecount`           | Anzahl der Episoden in der Veröffentlichung                                                   |
| `sonarr_release_seasonnumber`           | Staffelnummer der Veröffentlichung                                                           |
| `sonarr_release_episodenumbers`         | Komma-getrennte Liste der Episodennummern                                                    |
| `sonarr_release_absoluteepisodenumbers` | Komma-getrennte Liste der absoluten Episodennummern                                           |
| `sonarr_release_episodeairdates`        | Komma-getrennte Liste der Ausstrahlungsdaten vom Originalnetzwerk                             |
| `sonarr_release_episodeairdatesutc`     | Komma-getrennte Liste der Ausstrahlungsdaten in UTC                                           |
| `sonarr_release_episodetitles`          | Mit `|` getrennte Liste der Episodentitel                                                     |
| `sonarr_release_title`                  | Torrent-/NZB-Titel                                                                           |
| `sonarr_release_indexer`                | Indexer, von dem die Veröffentlichung abgerufen wurde                                         |
| `sonarr_release_size`                   | Größe der Veröffentlichung, wie vom Indexer gemeldet                                          |
| `sonarr_release_quality`                | Qualitätsname der Veröffentlichung, wie von Sonarr erkannt                                   |
| `sonarr_release_qualityversion`         | `1` ist der Standardwert, `2` steht für korrekt und `3`+ kann für Anime-Versionen verwendet werden |
| `sonarr_release_releasegroup`           | Release-Gruppe (leer, wenn unbekannt)                                                         |
| `sonarr_download_client`                | Download-Client                                                                             |
| `sonarr_download_id`                    | Hash der Torrent-/NZB-Datei (wird verwendet, um den Download im Download-Client eindeutig zu identifizieren) |

## Beim Importieren/Beim Aktualisieren

| Umgebungsvariable                     | Details                                                                                      |
| ------------------------------------- | -------------------------------------------------------------------------------------------- |
| `sonarr_eventtype`                    | `Download`                                                                                   |
| `sonarr_isupgrade`                    | `True`, wenn eine vorhandene Datei aktualisiert wird, `False` sonst                           |
| `sonarr_series_id`                    | Interne ID der Serie                                                                        |
| `sonarr_series_title`                 | Titel der Serie                                                                              |
| `sonarr_series_path`                  | Vollständiger Pfad zur Serie                                                                 |
| `sonarr_series_tvdbid`                | TVDB-ID für die Serie                                                                       |
| `sonarr_series_tvmazeid`              | TVMaze-ID für die Serie                                                                     |
| `sonarr_series_imdbid`                | IMDB-ID für die Serie (leer, wenn unbekannt)                                                 |
| `sonarr_series_type`                  | Art der Serie (`Anime`, `Daily` oder `Standard`)                                             |
| `sonarr_episodefile_id`               | Interne ID der Episodendatei                                                                |
| `sonarr_episodefile_episodecount`     | Anzahl der Episoden in der Datei                                                            |
| `sonarr_episodefile_relativepath`     | Pfad zur Episodendatei relativ zum Serienpfad                                               |
| `sonarr_episodefile_path`             | Vollständiger Pfad zur Episodendatei                                                        |
| `sonarr_episodefile_episodeids`       | Interne ID(s) der Episodendatei                                                             |
| `sonarr_episodefile_seasonnumber`     | Staffelnummer der Episodendatei                                                             |
| `sonarr_episodefile_episodenumbers`   | Komma-getrennte Liste der Episodennummern                                                   |
| `sonarr_episodefile_episodeairdates`  | Komma-getrennte Liste der Ausstrahlungsdaten vom Originalnetzwerk                            |
| `sonarr_episodefile_episodeairdatesutc` | Komma-getrennte Liste der Ausstrahlungsdaten in UTC                                        |
| `sonarr_episodefile_episodetitles`    | `\|`-getrennte Liste der Episodentitel                                                      |
| `sonarr_episodefile_quality`          | Qualitätsname der Episodendatei, wie von Sonarr erkannt                                     |
| `sonarr_episodefile_qualityversion`   | `1` ist der Standardwert, `2` steht für korrekt und `3`+ kann für Anime-Versionen verwendet werden |
| `sonarr_episodefile_releasegroup`     | Release-Gruppe (leer, wenn unbekannt)                                                       |
| `sonarr_episodefile_scenename`        | Originaler Veröffentlichungsname (leer, wenn unbekannt)                                     |
| `sonarr_episodefile_sourcepath`       | Vollständiger Pfad zur importierten Episodendatei                                           |
| `sonarr_episodefile_sourcefolder`     | Vollständiger Pfad zum Ordner, aus dem die Episodendatei importiert wurde                     |
| `sonarr_download_client`              | Download-Client                                                                             |
| `sonarr_download_id`                  | Hash der Torrent-/NZB-Datei (wird verwendet, um den Download im Download-Client eindeutig zu identifizieren) |
| `sonarr_deletedrelativepaths`         | `\|`-getrennte Liste der Dateien, die gelöscht wurden, um diese Datei zu importieren         |
| `sonarr_deletedpaths`                 | `\|`-getrennte Liste der vollständigen Pfade der Dateien, die gelöscht wurden, um diese Datei zu importieren |

## Bei Umbenennung

| Umgebungsvariable     | Details                                              |
| --------------------- | ---------------------------------------------------- |
| `sonarr_eventtype`    | `Rename`                                             |
| `sonarr_series_id`    | Interne ID der Serie                            |
| `sonarr_series_title` | Titel der Serie                                  |
| `sonarr_series_path`  | Vollständiger Pfad zur Serie                              |
| `sonarr_series_tvdbid`   | TVDB-ID für die Serie                               |
| `sonarr_series_tvmazeid` | TVMaze-ID für die Serie                             |
| `sonarr_series_imdbid`   | IMDB-ID für die Serie (leer, wenn unbekannt)            |
| `sonarr_series_type`     | Art der Serie (`Anime`, `Daily` oder `Standard`) |

## Bei Löschung der Episodendatei

| Umgebungsvariable                      | Details                                                                          |
| -------------------------------------- | -------------------------------------------------------------------------------- |
| `sonarr_eventtype`                      | `EpisodeFileDelete`                                                              |
| `sonarr_series_id`                      | Interne ID der Serie                                                            |
| `sonarr_series_title`                   | Titel der Serie                                                                  |
| `sonarr_series_path`                    | Vollständiger Pfad zur Serie                                                     |
| `sonarr_series_tvdbid`                  | TVDB-ID für die Serie                                                            |
| `sonarr_series_tvmazeid`                | TVMaze-ID für die Serie                                                          |
| `sonarr_series_imdbid`                  | IMDB-ID für die Serie (leer, wenn unbekannt)                                      |
| `sonarr_series_type`                    | Art der Serie (`Anime`, `Daily` oder `Standard`)                                 |
| `sonarr_episodefile_id`                 | Interne ID der Episodendatei                                                     |
| `sonarr_episodefile_episodecount`       | Anzahl der Episoden in der Datei                                                 |
| `sonarr_episodefile_relativepath`       | Pfad zur Episodendatei relativ zum Pfad der Serie                                 |
| `sonarr_episodefile_path`               | Vollständiger Pfad zur Episodendatei                                              |
| `sonarr_episodefile_episodeids`         | Interne ID(s) der Episodendatei                                                  |
| `sonarr_episodefile_seasonnumber`       | Staffelnummer der Episodendatei                                                  |
| `sonarr_episodefile_episodenumbers`     | Komma-getrennte Liste der Episodennummern                                        |
| `sonarr_episodefile_episodeairdates`    | Komma-getrennte Liste der Ausstrahlungsdaten des Originalnetzwerks                |
| `sonarr_episodefile_episodeairdatesutc` | Komma-getrennte Liste der Ausstrahlungsdaten in UTC                              |
| `sonarr_episodefile_episodetitles`      | Mit `|` getrennte Liste der Episodentitel                                        |
| `sonarr_episodefile_quality`            | Qualitätsname der Episodendatei, wie von Sonarr erkannt                           |
| `sonarr_episodefile_qualityversion`     | `1` ist der Standardwert, `2` steht für korrekt und `3`+ kann für Anime-Versionen verwendet werden |
| `sonarr_episodefile_releasegroup`       | Release-Gruppe (leer, wenn unbekannt)                                            |
| `sonarr_episodefile_scenename`          | Originaler Veröffentlichungsname (leer, wenn unbekannt)                           |

## Beim Löschen einer Serie

| Umgebungsvariable        | Details                                                      |
| ----------------------- | ------------------------------------------------------------ |
| `sonarr_eventtype`      | `SeriesDelete`                                               |
| `sonarr_series_id`      | Interne ID der Serie                                         |
| `sonarr_series_title`   | Titel der Serie                                              |
| `sonarr_series_path`    | Vollständiger Pfad zur Serie                                 |
| `sonarr_series_tvdbid`  | TVDB-ID für die Serie                                        |
| `sonarr_series_imdbid`  | IMDB-ID für die Serie (leer, wenn unbekannt)                  |
| `sonarr_series_type`    | Art der Serie (`Anime`, `Daily` oder `Standard`)             |
| `sonarr_series_deletedfiles` | `True`, wenn die Option zum Löschen von Dateien ausgewählt wurde, andernfalls `False` |

## Bei Problemen mit der Gesundheit

| Umgebungsvariable           | Details                                                      |
| -------------------------- | ------------------------------------------------------------ |
| `sonarr_eventtype`         | `HealthIssue`                                                |
| `sonarr_health_issue_level` | Art des Gesundheitsproblems (`Ok`, `Notice`, `Warning` oder `Error`) |
| `sonarr_health_issue_message` | Nachricht vom Gesundheitsproblem                            |
| `sonarr_health_issue_type` | Bereich, der fehlgeschlagen ist und das Gesundheitsproblem ausgelöst hat |
| `sonarr_health_issue_wiki` | Wiki-URL (leer, wenn nicht vorhanden)                        |

## Bei Anwendungsaktualisierung

| Umgebungsvariable                | Details                                   |
| ------------------------------- | ----------------------------------------- |
| `sonarr_eventtype`              | `ApplicationUpdate`                       |
| `sonarr_update_message`         | Nachricht von der Aktualisierung           |
| `sonarr_update_newversion`      | Version, zu der Sonarr aktualisiert wurde (Zeichenkette) |
| `sonarr_update_previousversion` | Version, von der Sonarr aktualisiert wurde (Zeichenkette) |

## Bei Test

Wenn das Skript zu Sonarr hinzugefügt und auf "Testen" geklickt wird, wird das Skript mit den folgenden Parametern aufgerufen. Das Skript sollte in der Lage sein, jeden nicht unterstützten Ereignistyp elegant zu ignorieren.

| Umgebungsvariable | Details |
| ----------------- | ------- |
| `sonarr_eventtype` | `Test`  |