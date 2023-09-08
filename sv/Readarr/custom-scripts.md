---
title: Readarr Anpassade Skript
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, behöver-kärlek, anpassade skript
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

Om du vill utlösa ett anpassat skript kan du hitta mer information här. Skript läggs till i Readarr via [Anslutningsinställningar](/readarr/settings#connections).

# Översikt

Readarr kan köra ett anpassat skript när en bok importeras eller byter namn. Beroende på åtgärden tillhandahålls olika parametrar. Parametrar skickas till skriptet genom miljövariabler.

## Readarr-loggar

Observera att följande endast loggas för anpassade skript:

- Skriptets `stdout`-utdata loggas som `Debug`
- Skriptets `stderr`-utdata loggas som `Info`
- Triggern för skriptet loggas som `Trace`

# Miljövariabler

## Vid hämtning

| Miljövariabel                   | Detaljer                                    |
| ------------------------------ | ------------------------------------------- |
| `readarr_eventtype`            | `Grab`                                      |
| `readarr_author_id`            | Intern ID för författaren                   |
| `readarr_author_name`          | Namn på författaren                         |
| `readarr_author_grid`          | Författarens Goodreads-id                   |
| `readarr_release_bookcount`    | Antal böcker i utgåvan                      |
| `readarr_release_bookreleasedates` | Utgivningsdatum för boken               |
| `readarr_release_booktitles`   | Boktitlar i utgåvan                         |
| `readarr_release_bookids`      | Bok-ID                                      |
| `readarr_release_grids`        | Goodreads-id för utgåvan                    |
| `readarr_release_title`        | Bokens titel                                |
| `readarr_release_indexer`      | Indexer från vilken utgåvan hämtades        |
| `readarr_release_size`         | Utgåvans storlek                            |
| `readarr_release_quality`      | Utgåvans kvalitet                           |
| `readarr_release_qualityVersion` | Utgåvans kvalitetsversion                |
| `readarr_release_releasegroup` | Utgivningsgrupp (tom om okänd)              |
| `readarr_download_client`      | Nedladdningsklient som användes för utgåvan |
| `readarr_download_id`          | Nedladdnings-ID                             |

## Vid import/uppgradering

| Miljövariabel         | Detaljer                                    |
| --------------------- | ------------------------------------------- |
| `readarr_eventtype`  | `Download`                                  |
| `readarr_author_id`  | Intern ID för författaren                   |
| `readarr_author_name` | Namn på författaren                         |
| `readarr_author_path` | Sökväg till författaren                     |
| `readarr_author_grid` | Författarens Goodreads-id                   |
| `readarr_book_id`     | Bokens ID                                   |
| `readarr_book_title`  | Bokens titel                                |
| `readarr_book_grid`   | Bokens Goodreads-id                         |
| `readarr_book_releasedate` | Utgivningsdatum för boken               |
| `readarr_download_client` | Nedladdningsklient som användes för utgåvan |
| `readarr_download_id` | Nedladdnings-ID                             |

## Vid namnbyte

| Miljövariabel     | Detaljer                   |
| ----------------- | ------------------------- |
| `readarr_eventtype` | `Rename`                  |
| `readarr_author_id` | Intern ID för författaren |
| `readarr_author_name` | Namn på författaren        |
| `readarr_author_path` | Sökväg till författaren    |
| `readarr_author_grid` | Författarens Goodreads-id  |

## Vid omtaggning av bok

| Miljövariabel                | Detaljer                   |
| --------------------------- | ------------------------- |
| `readarr_eventtype`         | `TrackRetag`              |
| `readarr_author_id`         | Intern ID för författaren |
| `readarr_author_name`       | Namn på författaren        |
| `readarr_author_path`       | Sökväg till författaren    |
| `readarr_author_grid`       | Författarens Goodreads-id  |
| `readarr_book_id`           | Bokens ID                 |
| `readarr_book_title`        | Bokens titel              |
| `readarr_book_grid`         | Bokens Goodreads-id       |
| `readarr_book_releasedate`  | Utgivningsdatum för boken |
| `readarr_bookfile_id`       | Bokfilens ID              |
| `readarr_bookfile_path`     | Sökväg till boken         |
| `readarr_bookfile_quality`  | Bokfilens kvalitet        |
| `readarr_bookfile_qualityversion` | Bokfilens kvalitetsversion |
| `readarr_bookfile_releasegroup` | Utgivningsgrupp för boken |
| `readarr_bookfile_scenename` | Scenenamn för boken       |
| `readarr_tags_diff`         | Skillnader i taggar       |
| `readarr_tags_scrubbed`     | Rensade taggar            |

## Vid hälsoproblem

| Miljövariabel                | Detaljer                                                      |
| --------------------------- | ------------------------------------------------------------ |
| `readarr_eventtype`         | `HealthIssue`                                                |
| `readarr_health_issue_level` | Typ av hälsoproblem (`Ok`, `Notice`, `Warning` eller `Error`) |
| `readarr_health_issue_message` | Meddelande från hälsoproblemet                              |
| `readarr_health_issue_type` | Område som misslyckades och utlöste hälsoproblemet            |
| `readarr_health_issue_wiki` | Wiki-URL (tom om den inte finns)                             |

## Test

När du lägger till skriptet i Readarr och klickar på "Testa" kommer skriptet att köras med följande parametrar. Skriptet bör kunna ignorera eventtyper som inte stöds.

| Miljövariabel | Detaljer |
| -------------------- | ------- |
| `readarr_eventtype`  | `Test`  |