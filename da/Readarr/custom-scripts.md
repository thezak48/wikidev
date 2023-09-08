---
title: Readarr Brugerdefinerede Scripts
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

Hvis du vil udløse et brugerdefineret script, kan du finde flere detaljer her. Scripts tilføjes til Readarr via [Forbindelsesindstillingerne](/readarr/settings#connections).

# Oversigt

Readarr kan udføre et brugerdefineret script, når en bog er nyimporteret eller omdøbt. Afhængigt af handlingen leveres forskellige parametre. Parametre sendes til scriptet gennem miljøvariabler.

## Readarr-logfiler

Bemærk, at følgende kun bliver logget for brugerdefinerede scripts:

- Scriptets `stdout`-output logges som `Debug`
- Scriptets `stderr`-output logges som `Info`
- Udløseren af scriptet logges som `Trace`

# Miljøvariabler

## Ved hentning

| Miljøvariabel                  | Detaljer                                     |
| ------------------------------ | -------------------------------------------- |
| `readarr_eventtype`            | `Grab`                                       |
| `readarr_author_id`            | Intern ID for forfatteren                    |
| `readarr_author_name`          | Navn på forfatteren                          |
| `readarr_author_grid`          | Forfatterens Goodreads-id                    |
| `readarr_release_bookcount`    | Antal bøger i udgivelsen                      |
| `readarr_release_bookreleasedates` | Udgivelsesdato for bogen                 |
| `readarr_release_booktitles`   | Bogtitlerne i udgivelsen                     |
| `readarr_release_bookids`      | Bog-id                                      |
| `readarr_release_grids`        | Goodreads-id'er for udgivelsen               |
| `readarr_release_title`        | Bogens titel                                 |
| `readarr_release_indexer`      | Indekser, hvorfra udgivelsen blev hentet     |
| `readarr_release_size`         | Størrelsen på udgivelsen                     |
| `readarr_release_quality`      | Kvaliteten på udgivelsen                     |
| `readarr_release_qualityVersion` | Versionsnummeret for kvaliteten på udgivelsen |
| `readarr_release_releasegroup` | Udgivelsesgruppe (tom, hvis ukendt)           |
| `readarr_download_client`      | Downloadklienten, der blev brugt til at downloade udgivelsen |
| `readarr_download_id`          | Download-id                                  |

## Ved import/ved opgradering

| Miljøvariabel                | Detaljer                                     |
| ---------------------------- | -------------------------------------------- |
| `readarr_eventtype`          | `Download`                                   |
| `readarr_author_id`          | Intern ID for forfatteren                    |
| `readarr_author_name`        | Navn på forfatteren                          |
| `readarr_author_path`        | Sti til forfatteren                          |
| `readarr_author_grid`        | Forfatterens Goodreads-id                    |
| `readarr_book_id`            | Bogens id                                    |
| `readarr_book_title`         | Bogens titel                                 |
| `readarr_book_grid`          | Bogens Goodreads-id                          |
| `readarr_book_releasedate`   | Udgivelsesdato for bogen                     |
| `readarr_download_client`    | Downloadklienten, der blev brugt til at downloade udgivelsen |
| `readarr_download_id`        | Download-id                                  |

## Ved omdøbning

| Miljøvariabel               | Detaljer                   |
| --------------------------- | ------------------------- |
| `readarr_eventtype`         | `Rename`                  |
| `readarr_author_id`         | Intern ID for forfatteren |
| `readarr_author_name`       | Navn på forfatteren        |
| `readarr_author_path`       | Sti til forfatteren        |
| `readarr_author_grid`       | Forfatterens Goodreads-id  |

## Ved genmærkning af bog

| Miljøvariabel                  | Detaljer                   |
| ------------------------------ | ------------------------- |
| `readarr_eventtype`            | `TrackRetag`              |
| `readarr_author_id`            | Intern ID for forfatteren |
| `readarr_author_name`          | Navn på forfatteren        |
| `readarr_author_path`          | Sti til forfatteren        |
| `readarr_author_grid`          | Forfatterens Goodreads-id  |
| `readarr_book_id`              | Bogens id                 |
| `readarr_book_title`           | Bogens titel              |
| `readarr_book_grid`            | Bogens Goodreads-id       |
| `readarr_book_releasedate`     | Udgivelsesdato for bogen  |
| `readarr_bookfile_id`          | Bogfilens id              |
| `readarr_bookfile_path`        | Sti til bogen             |
| `readarr_bookfile_quality`     | Bogfilens kvalitet        |
| `readarr_bookfile_qualityversion` | Versionsnummeret for bogfilens kvalitet |
| `readarr_bookfile_releasegroup` | Udgivelsesgruppen for bogen |
| `readarr_bookfile_scenename`   | Scenenavnet for bogen     |
| `readarr_tags_diff`            | Forskelle i tags          |
| `readarr_tags_scrubbed`        | Rensede tags              |

## Ved sundhedsproblem

| Miljøvariabel                  | Detaljer                                                      |
| ------------------------------ | ------------------------------------------------------------ |
| `readarr_eventtype`            | `HealthIssue`                                                |
| `readarr_health_issue_level`   | Type af sundhedsproblem (`Ok`, `Notice`, `Warning` eller `Error`) |
| `readarr_health_issue_message` | Besked fra sundhedsproblemet                                |
| `readarr_health_issue_type`    | Område, der mislykkedes og udløste sundhedsproblemet          |
| `readarr_health_issue_wiki`    | Wiki-URL (tom, hvis den ikke findes)                           |

## Ved test

Når du tilføjer scriptet til Readarr og klikker på 'Test', vil scriptet blive kaldt med følgende parametre. Scriptet skal kunne ignorere eventuelle ikke-understøttede eventtyper.

| Miljøvariabel        | Detaljer |
| -------------------- | ------- |
| `readarr_eventtype`  | `Test`  |