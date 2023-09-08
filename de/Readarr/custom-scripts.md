---
title: Readarr Benutzerdefinierte Skripte
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, needs-love, benutzerdefinierte skripte
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

Wenn Sie ein benutzerdefiniertes Skript auslösen möchten, finden Sie hier weitere Details. Skripte werden Readarr über die [Verbindungs-Einstellungen](/readarr/settings#connections) hinzugefügt.

# Übersicht

Readarr kann ein benutzerdefiniertes Skript ausführen, wenn ein Buch neu importiert oder umbenannt wird. Je nach Aktion werden unterschiedliche Parameter übergeben. Die Parameter werden dem Skript über Umgebungsvariablen übergeben.

## Readarr-Protokolle

Beachten Sie, dass das Folgende nur für benutzerdefinierte Skripte protokolliert wird:

- Die Ausgabe von Skript `stdout` wird als `Debug` protokolliert.
- Die Ausgabe von Skript `stderr` wird als `Info` protokolliert.
- Der Auslöser des Skripts wird als `Trace` protokolliert.

# Umgebungsvariablen

## Beim Erfassen

| Umgebungsvariable                | Details                                     |
| -------------------------------- | ------------------------------------------- |
| `readarr_eventtype`              | `Grab`                                      |
| `readarr_author_id`              | Interne ID des Autors                       |
| `readarr_author_name`            | Name des Autors                             |
| `readarr_author_grid`            | Goodreads-ID des Autors                     |
| `readarr_release_bookcount`      | Anzahl der Bücher in der Veröffentlichung   |
| `readarr_release_bookreleasedates` | Veröffentlichungsdatum des Buches          |
| `readarr_release_booktitles`     | Buchtitel der Veröffentlichung              |
| `readarr_release_bookids`        | Buch-ID                                     |
| `readarr_release_grids`          | Goodreads-IDs der Veröffentlichung          |
| `readarr_release_title`          | Titel des Buches                            |
| `readarr_release_indexer`        | Indexer, von dem die Veröffentlichung erfasst wurde |
| `readarr_release_size`           | Größe der Veröffentlichung                  |
| `readarr_release_quality`        | Qualität der Veröffentlichung               |
| `readarr_release_qualityVersion` | Versionsnummer der Qualität der Veröffentlichung |
| `readarr_release_releasegroup`   | Veröffentlichungsgruppe (leer, wenn unbekannt) |
| `readarr_download_client`        | Download-Client, der zum Herunterladen der Veröffentlichung verwendet wird |
| `readarr_download_id`            | Download-ID                                 |

## Beim Importieren/Beim Aktualisieren

| Umgebungsvariable       | Details                                     |
| ---------------------- | ------------------------------------------- |
| `readarr_eventtype`    | `Download`                                  |
| `readarr_author_id`    | Interne ID des Autors                       |
| `readarr_author_name`  | Name des Autors                             |
| `readarr_author_path`  | Pfad des Autors                             |
| `readarr_author_grid`  | Goodreads-ID des Autors                     |
| `readarr_book_id`      | ID des Buches                               |
| `readarr_book_title`   | Titel des Buches                            |
| `readarr_book_grid`    | Goodreads-ID des Buches                     |
| `readarr_book_releasedate` | Veröffentlichungsdatum des Buches          |
| `readarr_download_client` | Download-Client, der zum Herunterladen der Veröffentlichung verwendet wird |
| `readarr_download_id` | Download-ID                                 |

## Beim Umbenennen

| Umgebungsvariable   | Details                                     |
| ------------------  | ------------------------------------------- |
| `readarr_eventtype` | `Rename`                                    |
| `readarr_author_id` | Interne ID des Autors                       |
| `readarr_author_name` | Name des Autors                            |
| `readarr_author_path` | Pfad des Autors                            |
| `readarr_author_grid` | Goodreads-ID des Autors                     |

## Beim Neutagging des Buches

| Umgebungsvariable              | Details                                     |
| -----------------------------  | ------------------------------------------- |
| `readarr_eventtype`            | `TrackRetag`                                |
| `readarr_author_id`            | Interne ID des Autors                       |
| `readarr_author_name`          | Name des Autors                             |
| `readarr_author_path`          | Pfad des Autors                             |
| `readarr_author_grid`          | Goodreads-ID des Autors                     |
| `readarr_book_id`              | ID des Buches                               |
| `readarr_book_title`           | Titel des Buches                            |
| `readarr_book_grid`            | Goodreads-ID des Buches                     |
| `readarr_book_releasedate`     | Veröffentlichungsdatum des Buches           |
| `readarr_bookfile_id`          | Buchdatei-ID                                |
| `readarr_bookfile_path`        | Pfad zur Buchdatei                          |
| `readarr_bookfile_quality`     | Qualität der Buchdatei                      |
| `readarr_bookfile_qualityversion` | Versionsnummer der Qualität der Buchdatei |
| `readarr_bookfile_releasegroup` | Veröffentlichungsgruppe des Buches          |
| `readarr_bookfile_scenename`   | Szenenname des Buches                       |
| `readarr_tags_diff`            | Unterschiede in den Tags                    |
| `readarr_tags_scrubbed`        | Bereinigte Tags                             |

## Bei Problemen mit der Gesundheit

| Umgebungsvariable             | Details                                                      |
| ---------------------------- | ------------------------------------------------------------ |
| `readarr_eventtype`          | `HealthIssue`                                                |
| `readarr_health_issue_level` | Art des Gesundheitsproblems (`Ok`, `Notice`, `Warning` oder `Error`) |
| `readarr_health_issue_message` | Nachricht vom Gesundheitsproblem                             |
| `readarr_health_issue_type`  | Bereich, der fehlgeschlagen ist und das Gesundheitsproblem ausgelöst hat |
| `readarr_health_issue_wiki`  | Wiki-URL (leer, wenn nicht vorhanden)                        |

## Beim Testen

Wenn Sie das Skript zu Readarr hinzufügen und auf "Testen" klicken, wird das Skript mit den folgenden Parametern aufgerufen. Das Skript sollte in der Lage sein, jeden nicht unterstützten Ereignistyp elegant zu ignorieren.

| Umgebungsvariable | Details |
| ----------------- | ------- |
| `readarr_eventtype` | `Test`  |