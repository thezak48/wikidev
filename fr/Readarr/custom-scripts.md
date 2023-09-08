---
title: Scripts personnalisés Readarr
description: 
published: true
date: 2022-05-02T03:36:38.595Z
tags: readarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:41:11.792Z
---

Si vous souhaitez déclencher un script personnalisé, vous pouvez trouver plus de détails ici. Les scripts sont ajoutés à Readarr via les [paramètres de connexion](/readarr/settings#connections).

# Aperçu

Readarr peut exécuter un script personnalisé lorsqu'un livre est nouvellement importé ou renommé. Selon l'action, différents paramètres sont fournis. Les paramètres sont transmis au script via des variables d'environnement.

## Journaux Readarr

Notez que les éléments suivants ne seront enregistrés que pour les scripts personnalisés :

- La sortie `stdout` du script sera enregistrée en tant que `Debug`
- La sortie `stderr` du script sera enregistrée en tant que `Info`
- Le déclencheur du script sera enregistré dans `Trace`

# Variables d'environnement

## Sur Grab

| Variable d'environnement          | Détails                                     |
| --------------------------------- | ------------------------------------------- |
| `readarr_eventtype`               | `Grab`                                      |
| `readarr_author_id`               | ID interne de l'auteur                      |
| `readarr_author_name`             | Nom de l'auteur                             |
| `readarr_author_grid`             | ID Goodreads de l'auteur                     |
| `readarr_release_bookcount`       | Nombre de livres dans la publication        |
| `readarr_release_bookreleasedates`| Date de publication du livre                |
| `readarr_release_booktitles`      | Titres des livres de la publication         |
| `readarr_release_bookids`         | ID du livre                                 |
| `readarr_release_grids`           | IDs Goodreads de la publication             |
| `readarr_release_title`           | Titre du livre                              |
| `readarr_release_indexer`         | Indexeur à partir duquel la publication a été récupérée |
| `readarr_release_size`            | Taille de la publication                    |
| `readarr_release_quality`         | Qualité de la publication                   |
| `readarr_release_qualityVersion`  | Version de la qualité de la publication     |
| `readarr_release_releasegroup`    | Groupe de publication (vide si inconnu)     |
| `readarr_download_client`         | Client de téléchargement utilisé pour télécharger la publication |
| `readarr_download_id`             | ID de téléchargement                        |

## Sur Import/Upgrade

| Variable d'environnement | Détails                                     |
| ------------------------ | ------------------------------------------- |
| `readarr_eventtype`      | `Download`                                  |
| `readarr_author_id`      | ID interne de l'auteur                      |
| `readarr_author_name`    | Nom de l'auteur                             |
| `readarr_author_path`    | Chemin de l'auteur                          |
| `readarr_author_grid`    | ID Goodreads de l'auteur                     |
| `readarr_book_id`        | ID du livre                                 |
| `readarr_book_title`     | Titre du livre                              |
| `readarr_book_grid`      | ID Goodreads du livre                       |
| `readarr_book_releasedate`| Date de publication du livre                |
| `readarr_download_client`| Client de téléchargement utilisé pour télécharger la publication |
| `readarr_download_id`    | ID de téléchargement                        |

## Sur Renommer

| Variable d'environnement | Détails                   |
| ------------------------ | ------------------------- |
| `readarr_eventtype`      | `Rename`                  |
| `readarr_author_id`      | ID interne de l'auteur    |
| `readarr_author_name`    | Nom de l'auteur           |
| `readarr_author_path`    | Chemin de l'auteur        |
| `readarr_author_grid`    | ID Goodreads de l'auteur   |

## Sur Retag de livre

| Variable d'environnement          | Détails                   |
| --------------------------------- | ------------------------- |
| `readarr_eventtype`               | `TrackRetag`              |
| `readarr_author_id`               | ID interne de l'auteur    |
| `readarr_author_name`             | Nom de l'auteur           |
| `readarr_author_path`             | Chemin de l'auteur        |
| `readarr_author_grid`             | ID Goodreads de l'auteur   |
| `readarr_book_id`                 | ID du livre               |
| `readarr_book_title`              | Titre du livre            |
| `readarr_book_grid`               | ID Goodreads du livre     |
| `readarr_book_releasedate`        | Date de publication du livre |
| `readarr_bookfile_id`             | ID du fichier du livre    |
| `readarr_bookfile_path`           | Chemin du livre           |
| `readarr_bookfile_quality`        | Qualité du fichier du livre |
| `readarr_bookfile_qualityversion` | Version de la qualité du fichier du livre |
| `readarr_bookfile_releasegroup`   | Groupe de publication du livre |
| `readarr_bookfile_scenename`      | Nom de scène du livre     |
| `readarr_tags_diff`               | Différences de tags       |
| `readarr_tags_scrubbed`           | Tags nettoyés             |

## Sur Problème de santé

| Variable d'environnement           | Détails                                                      |
| ---------------------------------- | ------------------------------------------------------------ |
| `readarr_eventtype`                | `HealthIssue`                                                |
| `readarr_health_issue_level`       | Type de problème de santé (`Ok`, `Notice`, `Warning` ou `Error`) |
| `readarr_health_issue_message`     | Message du problème de santé                                |
| `readarr_health_issue_type`        | Zone qui a échoué et a déclenché le problème de santé        |
| `readarr_health_issue_wiki`        | URL du wiki (vide s'il n'existe pas)                           |

## Sur Test

Lorsque vous ajoutez le script à Readarr et cliquez sur "Test", le script sera invoqué avec les paramètres suivants. Le script doit être capable d'ignorer gracieusement tout type d'événement non pris en charge.

| Variable d'environnement | Détails |
| ----------------------- | ------- |
| `readarr_eventtype`     | `Test`  |