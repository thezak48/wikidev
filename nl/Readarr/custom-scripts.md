---
title: Readarr Aangepaste Scripts
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

Als je een aangepast script wilt activeren, kun je hier meer details vinden. Scripts worden aan Readarr toegevoegd via de [Connect Settings](/readarr/settings#connections).

# Overzicht

Readarr kan een aangepast script uitvoeren wanneer een boek nieuw wordt geïmporteerd of hernoemd. Afhankelijk van de actie worden verschillende parameters geleverd. Parameters worden aan het script doorgegeven via omgevingsvariabelen.

## Readarr Logs

Let op dat het volgende alleen wordt gelogd voor aangepaste scripts:

- Uitvoer van het script `stdout` wordt gelogd als `Debug`
- Uitvoer van het script `stderr` wordt gelogd als `Info`
- De trigger van het script wordt gelogd als `Trace`

# Omgevingsvariabelen

## Bij Grab

| Omgevingsvariabele                | Details                                        |
| --------------------------------- | ---------------------------------------------- |
| `readarr_eventtype`               | `Grab`                                         |
| `readarr_author_id`               | Interne ID van de auteur                        |
| `readarr_author_name`             | Naam van de auteur                              |
| `readarr_author_grid`             | Goodreads ID van de auteur                      |
| `readarr_release_bookcount`       | Aantal boeken in de release                     |
| `readarr_release_bookreleasedates`| Publicatiedatum van het boek                    |
| `readarr_release_booktitles`      | Boektitels van de release                       |
| `readarr_release_bookids`         | Boek-ID                                        |
| `readarr_release_grids`           | Goodreads-ID's van de release                   |
| `readarr_release_title`           | Titel van het boek                              |
| `readarr_release_indexer`         | Indexer waarvan de release is opgehaald         |
| `readarr_release_size`            | Grootte van de release                          |
| `readarr_release_quality`         | Kwaliteit van de release                        |
| `readarr_release_qualityVersion`  | Versie van de kwaliteit van de release          |
| `readarr_release_releasegroup`    | Releasegroep (leeg als onbekend)                |
| `readarr_download_client`         | Downloadclient die is gebruikt voor de release  |
| `readarr_download_id`             | Download-ID                                    |

## Bij Importeren/Upgraden

| Omgevingsvariabele      | Details                                        |
| -----------------------| ---------------------------------------------- |
| `readarr_eventtype`    | `Download`                                     |
| `readarr_author_id`    | Interne ID van de auteur                        |
| `readarr_author_name`  | Naam van de auteur                              |
| `readarr_author_path`  | Pad van de auteur                              |
| `readarr_author_grid`  | Goodreads ID van de auteur                      |
| `readarr_book_id`      | ID van het boek                                |
| `readarr_book_title`   | Titel van het boek                              |
| `readarr_book_grid`    | Goodreads ID van het boek                       |
| `readarr_book_releasedate` | Publicatiedatum van het boek                 |
| `readarr_download_client` | Downloadclient die is gebruikt voor de release |
| `readarr_download_id` | Download-ID |

## Bij Hernoemen

| Omgevingsvariabele   | Details                                      |
| -------------------- | -------------------------------------------- |
| `readarr_eventtype`  | `Rename`                                     |
| `readarr_author_id`  | Interne ID van de auteur                     |
| `readarr_author_name`| Naam van de auteur                           |
| `readarr_author_path`| Pad van de auteur                            |
| `readarr_author_grid`| Goodreads ID van de auteur                    |

## Bij Boek Retag

| Omgevingsvariabele              | Details                                      |
| ------------------------------- | -------------------------------------------- |
| `readarr_eventtype`             | `TrackRetag`                                 |
| `readarr_author_id`             | Interne ID van de auteur                     |
| `readarr_author_name`           | Naam van de auteur                           |
| `readarr_author_path`           | Pad van de auteur                            |
| `readarr_author_grid`           | Goodreads ID van de auteur                    |
| `readarr_book_id`               | ID van het boek                              |
| `readarr_book_title`            | Titel van het boek                           |
| `readarr_book_grid`             | Goodreads ID van het boek                    |
| `readarr_book_releasedate`      | Publicatiedatum van het boek                  |
| `readarr_bookfile_id`           | Bestands-ID van het boek                      |
| `readarr_bookfile_path`         | Pad naar het boek                            |
| `readarr_bookfile_quality`      | Kwaliteit van het boek                        |
| `readarr_bookfile_qualityversion` | Versie van de kwaliteit van het boek         |
| `readarr_bookfile_releasegroup` | Releasegroep van het boek                     |
| `readarr_bookfile_scenename`    | Scènenaam van het boek                        |
| `readarr_tags_diff`             | Verschillen in tags                           |
| `readarr_tags_scrubbed`         | Schoongemaakte tags                           |

## Bij Probleem met de Gezondheid

| Omgevingsvariabele          | Details                                                         |
| --------------------------- | --------------------------------------------------------------- |
| `readarr_eventtype`         | `HealthIssue`                                                   |
| `readarr_health_issue_level`| Type gezondheidsprobleem (`Ok`, `Notice`, `Warning` of `Error`)  |
| `readarr_health_issue_message` | Bericht van het gezondheidsprobleem                            |
| `readarr_health_issue_type` | Gebied dat is mislukt en het gezondheidsprobleem heeft geactiveerd |
| `readarr_health_issue_wiki` | Wiki-URL (leeg als deze niet bestaat)                            |

## Bij Test

Wanneer je het script aan Readarr toevoegt en op 'Test' klikt, wordt het script aangeroepen met de volgende parameters. Het script moet in staat zijn om op een goede manier om te gaan met elk niet-ondersteund gebeurtenistype.

| Omgevingsvariabele | Details |
| ------------------ | ------- |
| `readarr_eventtype`| `Test`  |