---
title: Radarr Benutzerdefinierte Skripte
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, needs-love, benutzerdefinierte skripte
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

Wenn Sie ein benutzerdefiniertes Skript auslösen möchten, finden Sie hier weitere Details. Skripte werden in Radarr über die [Verbindungs-Einstellungen](/radarr/settings#connections) hinzugefügt.

# Übersicht

Radarr kann ein benutzerdefiniertes Skript ausführen, wenn Filme importiert oder umbenannt werden. Je nach Aktion werden unterschiedliche Parameter bereitgestellt. Die Parameter werden dem Skript über Umgebungsvariablen übergeben.

## Radarr-Protokolle

Beachten Sie, dass Folgendes nur für benutzerdefinierte Skripte protokolliert wird:

- Die Ausgabe von Skript-`stdout` wird als `Debug` protokolliert.
- Die Ausgabe von Skript-`stderr` wird als `Info` protokolliert.
- Der Auslöser des Skripts wird als `Trace` protokolliert.

# Umgebungsvariablen

## Beim Herunterladen

| Umgebungsvariable                 | Details                                                                                      |
| --------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                | `Grab`                                                                                       |
| `radarr_download_client`          | Download-Client (leer, wenn unbekannt)                                                       |
| `radarr_download_id`              | Hash der Torrent-/NZB-Datei (wird verwendet, um den Download eindeutig im Download-Client zu identifizieren) |
| `radarr_movie_id`                 | Interne ID des Films                                                                         |
| `radarr_movie_imdbid`             | IMDb-ID für den Film (leer, wenn unbekannt)                                                   |
| `radarr_movie_in_cinemas_date`    | Kinoveröffentlichungsdatum (leer, wenn unbekannt)                                            |
| `radarr_movie_physical_release_date` | Physisches Veröffentlichungsdatum (leer, wenn unbekannt)                                   |
| `radarr_movie_title`              | Titel des Films                                                                              |
| `radarr_movie_tmdbid`             | TMDb-ID für den Film                                                                         |
| `radarr_movie_year`               | Veröffentlichungsjahr des Films                                                              |
| `radarr_release_indexer`          | Indexer, von dem die Veröffentlichung heruntergeladen wurde                                  |
| `radarr_release_quality`          | Qualitätsname der Veröffentlichung, wie von Radarr erkannt                                   |
| `radarr_release_qualityversion`   | `1` ist der Standardwert, `2` steht für korrekt, und `3`+ kann für Anime-Versionen verwendet werden |
| `radarr_release_releasegroup`     | Veröffentlichungsgruppe (leer, wenn unbekannt)                                               |
| `radarr_release_size`             | Größe der Veröffentlichung, wie vom Indexer gemeldet                                        |
| `radarr_release_title`            | Titel des Torrents/NZB                                                                      |

## Beim Importieren/Beim Aktualisieren

| Umgebungsvariable                 | Details                                                                                      |
| --------------------------------- | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                | `Download`                                                                                   |
| `radarr_download_id`              | Hash der Torrent-/NZB-Datei (wird verwendet, um den Download eindeutig im Download-Client zu identifizieren) |
| `radarr_download_client`          | Download-Client                                                                              |
| `radarr_isupgrade`                | `True`, wenn eine vorhandene Datei aktualisiert wird, `False` sonst                           |
| `radarr_movie_id`                 | Interne ID des Films                                                                         |
| `radarr_movie_imdbid`             | IMDb-ID für den Film (leer, wenn unbekannt)                                                   |
| `radarr_movie_in_cinemas_date`    | Kinoveröffentlichungsdatum (leer, wenn unbekannt)                                            |
| `radarr_movie_path`               | Vollständiger Pfad zum Film                                                                  |
| `radarr_movie_physical_release_date` | Physisches Veröffentlichungsdatum (leer, wenn unbekannt)                                   |
| `radarr_movie_title`              | Titel des Films                                                                              |
| `radarr_movie_tmdbid`             | TMDb-ID für den Film                                                                         |
| `radarr_movie_year`               | Veröffentlichungsjahr des Films                                                              |
| `radarr_moviefile_id`             | Interne ID der Filmdatei                                                                     |
| `radarr_moviefile_relativepath`   | Pfad zur Filmdatei relativ zum Film-Pfad                                                     |
| `radarr_moviefile_path`           | Vollständiger Pfad zur Filmdatei                                                             |
| `radarr_moviefile_quality`        | Qualitätsname der Veröffentlichung, wie von Radarr erkannt                                   |
| `radarr_moviefile_qualityversion` | `1` ist der Standardwert, `2` steht für korrekt, und `3`+ kann für Anime-Versionen verwendet werden |
| `radarr_moviefile_releasegroup`   | Veröffentlichungsgruppe (leer, wenn unbekannt)                                               |
| `radarr_moviefile_scenename`      | Originaler Veröffentlichungsname (leer, wenn unbekannt)                                      |
| `radarr_moviefile_sourcepath`     | Vollständiger Pfad zur importierten Filmdatei                                                |
| `radarr_moviefile_sourcefolder`   | Vollständiger Pfad zum Ordner, aus dem die Filmdatei importiert wurde                         |
| `radarr_deletedrelativepaths`     | `|`-getrennte Liste der Dateien, die gelöscht wurden, um diese Datei zu importieren           |
| `radarr_deletedpaths`             | `|`-getrennte Liste der vollständigen Pfade zu den Dateien, die gelöscht wurden, um diese Datei zu importieren |

| Umgebungsvariable                     | Details                                         |
| ---------------------------------------- | ----------------------------------------------- |
| `radarr_eventtype`                       | `Rename`                                        |
| `radarr_movie_id`                        | Interne ID des Films                        |
| `radarr_movie_title`                     | Titel des Films                              |
| `radarr_movie_year`                      | Erscheinungsjahr des Films                       |
| `radarr_movie_path`                      | Vollständiger Pfad zum Film                          |
| `radarr_movie_imdbid`                    | IMDb-ID des Films (leer, wenn unbekannt)        |
| `radarr_movie_tmdbid`                    | TMDb-ID des Films                           |
| `radarr_movie_in_cinemas_date`           | Kinoveröffentlichungsdatum (leer, wenn unbekannt)          |
| `radarr_movie_physical_release_date`     | Physisches/Web-Veröffentlichungsdatum (leer, wenn unbekannt)    |
| `radarr_moviefile_ids`                   | Durch `,` getrennte Liste von Datei-IDs                |
| `radarr_moviefile_relativepaths`         | Durch `|` getrennte Liste von relativen Pfaden          |
| `radarr_moviefile_paths`                 | Durch `|` getrennte Liste von Pfaden                   |
| `radarr_moviefile_previousrelativepaths` | Durch `|` getrennte Liste von vorherigen relativen Pfaden |
| `radarr_moviefile_previouspaths`         | Durch `|` getrennte Liste von vorherigen Pfaden          |

## Über die Gesundheitsprüfung

| Umgebungsvariable          | Details                                                      |
| ----------------------------- | ------------------------------------------------------------ |
| `radarr_eventtype`            | `HealthIssue`                                                |
| `radarr_health_issue_level`   | Art des Gesundheitsproblems (`Ok`, `Notice`, `Warning` oder `Error`) |
| `radarr_health_issue_message` | Nachricht vom Gesundheitsproblem                                |
| `radarr_health_issue_type`    | Bereich, der fehlgeschlagen ist und das Gesundheitsproblem ausgelöst hat              |
| `radarr_health_issue_wiki`    | Wiki-URL (leer, wenn nicht vorhanden)                           |

## Über das Anwendungsupdate

| Umgebungsvariable             | Details                               |
|--------------------------------- |-------------------------------------- |
| `radarr_eventtype`               | `ApplicationUpdate`                   |
| `radarr_update_message`          | Nachricht vom Update                   |
| `radarr_update_newversion`       | Version, zu der Radarr aktualisiert wurde (Zeichenkette)    |
| `radarr_update_previousversion`  | Version, von der Radarr aktualisiert wurde (Zeichenkette)  |

## Über den Test

Wenn das Skript zu Radarr hinzugefügt und auf "Testen" geklickt wird, wird das Skript mit den folgenden Parametern aufgerufen. Das Skript sollte in der Lage sein, jeden nicht unterstützten Ereignistyp zu ignorieren.

| Umgebungsvariable | Details |
| -------------------- | ------- |
| `radarr_eventtype`   | `Test`  |