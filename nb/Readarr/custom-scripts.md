---
title: Readarr Egendefinerte Skript
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

Hvis du ønsker å utløse et egendefinert skript, kan du finne mer informasjon her. Skript legges til i Readarr via [Tilkoblingsinnstillinger](/readarr/settings#connections).

# Oversikt

Readarr kan kjøre et egendefinert skript når en bok er nyimportert eller omdøpt. Avhengig av handlingen, blir forskjellige parametere levert. Parametere sendes til skriptet gjennom miljøvariabler.

## Readarr-logger

Merk at følgende bare blir logget for egendefinerte skript:

- Skriptets `stdout`-utdata blir logget som `Debug`
- Skriptets `stderr`-utdata blir logget som `Info`
- Utløseren for skriptet blir logget som `Trace`

# Miljøvariabler

## Ved Henting

| Miljøvariabel                    | Detaljer                                         |
| -------------------------------- | ------------------------------------------------ |
| `readarr_eventtype`              | `Grab`                                           |
| `readarr_author_id`              | Intern ID for forfatteren                        |
| `readarr_author_name`            | Navn på forfatteren                              |
| `readarr_author_grid`            | Goodreads-ID for forfatteren                     |
| `readarr_release_bookcount`      | Antall bøker i utgivelsen                        |
| `readarr_release_bookreleasedates` | Utgivelsesdato for boken                       |
| `readarr_release_booktitles`     | Boktitler i utgivelsen                           |
| `readarr_release_bookids`        | Bok-ID                                         |
| `readarr_release_grids`          | Goodreads-ID-er for utgivelsen                   |
| `readarr_release_title`          | Tittel på boken                                  |
| `readarr_release_indexer`        | Indekseringsverktøy som ble brukt til utgivelsen |
| `readarr_release_size`           | Størrelse på utgivelsen                          |
| `readarr_release_quality`        | Kvalitet på utgivelsen                           |
| `readarr_release_qualityVersion` | Kvalitetsversjon for utgivelsen                  |
| `readarr_release_releasegroup`   | Utgivelsesgruppe (tom hvis ukjent)               |
| `readarr_download_client`        | Nedlastingsklient som ble brukt til utgivelsen   |
| `readarr_download_id`            | Nedlastings-ID                                   |

## Ved Import/Ved Oppgradering

| Miljøvariabel         | Detaljer                                         |
| --------------------- | ------------------------------------------------ |
| `readarr_eventtype`   | `Download`                                       |
| `readarr_author_id`   | Intern ID for forfatteren                        |
| `readarr_author_name` | Navn på forfatteren                              |
| `readarr_author_path` | Sti til forfatteren                              |
| `readarr_author_grid` | Goodreads-ID for forfatteren                     |
| `readarr_book_id`     | Bokens ID                                        |
| `readarr_book_title`  | Bokens tittel                                    |
| `readarr_book_grid`   | Goodreads-ID for boken                           |
| `readarr_book_releasedate` | Utgivelsesdato for boken                      |
| `readarr_download_client` | Nedlastingsklient som ble brukt til utgivelsen |
| `readarr_download_id` | Nedlastings-ID                                   |

## Ved Omdøping

| Miljøvariabel         | Detaljer                                         |
| --------------------- | ------------------------------------------------ |
| `readarr_eventtype`   | `Rename`                                         |
| `readarr_author_id`   | Intern ID for forfatteren                        |
| `readarr_author_name` | Navn på forfatteren                              |
| `readarr_author_path` | Sti til forfatteren                              |
| `readarr_author_grid` | Goodreads-ID for forfatteren                     |

## Ved Omtagging av Bok

| Miljøvariabel                 | Detaljer                                         |
| ---------------------------- | ------------------------------------------------ |
| `readarr_eventtype`          | `TrackRetag`                                     |
| `readarr_author_id`          | Intern ID for forfatteren                        |
| `readarr_author_name`        | Navn på forfatteren                              |
| `readarr_author_path`        | Sti til forfatteren                              |
| `readarr_author_grid`        | Goodreads-ID for forfatteren                     |
| `readarr_book_id`            | Bokens ID                                        |
| `readarr_book_title`         | Bokens tittel                                    |
| `readarr_book_grid`          | Goodreads-ID for boken                           |
| `readarr_book_releasedate`   | Utgivelsesdato for boken                         |
| `readarr_bookfile_id`        | Bokfilens ID                                     |
| `readarr_bookfile_path`      | Sti til boken                                    |
| `readarr_bookfile_quality`   | Kvalitet på bokfilen                             |
| `readarr_bookfile_qualityversion` | Kvalitetsversjon for bokfilen                |
| `readarr_bookfile_releasegroup` | Utgivelsesgruppe for boken                    |
| `readarr_bookfile_scenename` | Scene-navn for boken                             |
| `readarr_tags_diff`          | Forskjeller i koder                              |
| `readarr_tags_scrubbed`      | Rensede koder                                    |

## Ved Helseproblem

| Miljøvariabel                 | Detaljer                                         |
| ---------------------------- | ------------------------------------------------ |
| `readarr_eventtype`          | `HealthIssue`                                    |
| `readarr_health_issue_level` | Type helseproblem (`Ok`, `Notice`, `Warning` eller `Error`) |
| `readarr_health_issue_message` | Melding fra helseproblemet                      |
| `readarr_health_issue_type`  | Område som feilet og utløste helseproblemet      |
| `readarr_health_issue_wiki`  | Wiki-URL (tom hvis den ikke finnes)              |

## Test

Når du legger til skriptet i Readarr og klikker på 'Test', vil skriptet bli kalt med følgende parametere. Skriptet bør kunne ignorere eventuelle ikke-støttede hendelsestyper på en hensiktsmessig måte.

| Miljøvariabel         | Detaljer |
| -------------------- | ------- |
| `readarr_eventtype`  | `Test`  |