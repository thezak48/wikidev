---
title: Scripts personnalisés Radarr
description: 
published: true
date: 2022-05-02T03:36:09.625Z
tags: radarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-16T15:55:44.765Z
---

Si vous souhaitez déclencher un script personnalisé, vous pouvez trouver plus de détails ici. Les scripts sont ajoutés à Radarr via les [Paramètres de connexion](/radarr/settings#connections).

# Aperçu

Radarr peut exécuter un script personnalisé lors de l'importation ou du renommage de films. Selon l'action, différents paramètres sont fournis. Les paramètres sont transmis au script via des variables d'environnement.

## Journaux Radarr

Notez que les éléments suivants ne seront enregistrés que pour les scripts personnalisés :

- La sortie `stdout` du script sera enregistrée en tant que `Debug`
- La sortie `stderr` du script sera enregistrée en tant que `Info`
- Le déclencheur du script sera enregistré en tant que `Trace`

# Variables d'environnement

## Sur la capture

| Variable d'environnement             | Détails                                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                   | `Grab`                                                                                       |
| `radarr_download_client`             | Client de téléchargement (vide si inconnu)                                                   |
| `radarr_download_id`                 | Hash du fichier torrent/NZB (utilisé pour identifier de manière unique le téléchargement dans le client de téléchargement) |
| `radarr_movie_id`                    | ID interne du film                                                                           |
| `radarr_movie_imdbid`                | ID IMDb du film (vide si inconnu)                                                            |
| `radarr_movie_in_cinemas_date`       | Date de sortie en salle (vide si inconnue)                                                   |
| `radarr_movie_physical_release_date` | Date de sortie physique (vide si inconnue)                                                   |
| `radarr_movie_title`                 | Titre du film                                                                                |
| `radarr_movie_tmdbid`                | ID TMDb du film                                                                              |
| `radarr_movie_year`                  | Année de sortie du film                                                                      |
| `radarr_release_indexer`             | Indexeur à partir duquel la version a été capturée                                           |
| `radarr_release_quality`             | Nom de la qualité de la version, détectée par Radarr                                         |
| `radarr_release_qualityversion`      | `1` est la valeur par défaut, `2` est utilisé pour les versions correctes et `3`+ peut être utilisé pour les versions d'anime |
| `radarr_release_releasegroup`        | Groupe de sortie (vide si inconnu)                                                           |
| `radarr_release_size`                | Taille de la version, telle que rapportée par l'indexeur                                      |
| `radarr_release_title`               | Titre du torrent/NZB                                                                         |

## Sur l'importation/la mise à niveau

| Variable d'environnement             | Détails                                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------------------- |
| `radarr_eventtype`                   | `Download`                                                                                   |
| `radarr_download_id`                 | Hash du fichier torrent/NZB (utilisé pour identifier de manière unique le téléchargement dans le client de téléchargement) |
| `radarr_download_client`             | Client de téléchargement                                                                     |
| `radarr_isupgrade`                   | `True` lorsque un fichier existant est mis à niveau, `False` sinon                            |
| `radarr_movie_id`                    | ID interne du film                                                                           |
| `radarr_movie_imdbid`                | ID IMDb du film (vide si inconnu)                                                            |
| `radarr_movie_in_cinemas_date`       | Date de sortie en salle (vide si inconnue)                                                   |
| `radarr_movie_path`                  | Chemin complet vers le film                                                                  |
| `radarr_movie_physical_release_date` | Date de sortie physique (vide si inconnue)                                                   |
| `radarr_movie_title`                 | Titre du film                                                                                |
| `radarr_movie_tmdbid`                | ID TMDb du film                                                                              |
| `radarr_movie_year`                  | Année de sortie du film                                                                      |
| `radarr_moviefile_id`                | ID interne du fichier du film                                                                |
| `radarr_moviefile_relativepath`      | Chemin d'accès au fichier du film, relatif au chemin du film                                 |
| `radarr_moviefile_path`              | Chemin complet vers le fichier du film                                                       |
| `radarr_moviefile_quality`           | Nom de la qualité de la version, détectée par Radarr                                         |
| `radarr_moviefile_qualityversion`    | `1` est la valeur par défaut, `2` est utilisé pour les versions correctes et `3`+ peut être utilisé pour les versions d'anime |
| `radarr_moviefile_releasegroup`      | Groupe de sortie (vide si inconnu)                                                           |
| `radarr_moviefile_scenename`         | Nom de sortie d'origine (vide si inconnu)                                                    |
| `radarr_moviefile_sourcepath`        | Chemin complet vers le fichier de film importé                                               |
| `radarr_moviefile_sourcefolder`      | Chemin complet vers le dossier à partir duquel le fichier de film a été importé               |
| `radarr_deletedrelativepaths`        | Liste de fichiers supprimés, séparés par `|`, qui ont été supprimés pour importer ce fichier |
| `radarr_deletedpaths`                | Liste complète des chemins d'accès aux fichiers supprimés pour importer ce fichier            |

## Sur le renommage

| Variable d'environnement                | Détails                                         |
| ---------------------------------------- | ----------------------------------------------- |
| `radarr_eventtype`                       | `Rename`                                        |
| `radarr_movie_id`                        | ID interne du film                             |
| `radarr_movie_title`                     | Titre du film                                   |
| `radarr_movie_year`                      | Année de sortie du film                         |
| `radarr_movie_path`                      | Chemin complet du film                          |
| `radarr_movie_imdbid`                    | ID IMDb du film (vide si inconnu)               |
| `radarr_movie_tmdbid`                    | ID TMDb du film                                 |
| `radarr_movie_in_cinemas_date`           | Date de sortie en salle (vide si inconnue)      |
| `radarr_movie_physical_release_date`     | Date de sortie physique/web (vide si inconnue) |
| `radarr_moviefile_ids`                   | Liste des ID de fichier séparés par des `,`     |
| `radarr_moviefile_relativepaths`         | Liste des chemins relatifs séparés par des `|`  |
| `radarr_moviefile_paths`                 | Liste des chemins absolus séparés par des `|`   |
| `radarr_moviefile_previousrelativepaths` | Liste des anciens chemins relatifs séparés par des `|` |
| `radarr_moviefile_previouspaths`         | Liste des anciens chemins absolus séparés par des `|`  |

## Sur la vérification de l'état de santé

| Variable d'environnement          | Détails                                                      |
| ----------------------------- | ------------------------------------------------------------ |
| `radarr_eventtype`            | `HealthIssue`                                                |
| `radarr_health_issue_level`   | Type de problème de santé (`Ok`, `Notice`, `Warning` ou `Error`) |
| `radarr_health_issue_message` | Message du problème de santé                                |
| `radarr_health_issue_type`    | Zone ayant échoué et déclenché le problème de santé              |
| `radarr_health_issue_wiki`    | URL du wiki (vide s'il n'existe pas)                           |

## Sur la mise à jour de l'application

| Variable d'environnement             | Détails                               |
|--------------------------------- |-------------------------------------- |
| `radarr_eventtype`               | `ApplicationUpdate`                   |
| `radarr_update_message`          | Message de la mise à jour                   |
| `radarr_update_newversion`       | Version à laquelle Radarr a été mise à jour (chaîne de caractères)    |
| `radarr_update_previousversion`  | Version de Radarr avant la mise à jour (chaîne de caractères)  |

## Sur le test

Lorsque vous ajoutez le script à Radarr et cliquez sur "Tester", le script sera invoqué avec les paramètres suivants. Le script doit être capable d'ignorer gracieusement tout type d'événement non pris en charge.

| Variable d'environnement | Détails |
| -------------------- | ------- |
| `radarr_eventtype`   | `Test`  |