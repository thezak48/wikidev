---
title: Activité de Radarr
description: 
published: true
date: 2022-02-06T09:07:15.520Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:28:36.350Z
---

# Activité

L'onglet Activité vous permet de voir les activités passées et présentes effectuées par \*Arr. Cela inclut les importations, les suppressions, les mises à niveau, les captures, les renommages et les échecs.

# File d'attente

Lorsqu'un téléchargement est en cours et n'a pas encore été importé dans \*Arr, il apparaît dans la page File d'attente.

La file d'attente affiche tous les éléments que l'application peut reconnaître dans la catégorie spécifiée du client de téléchargement (Paramètres => Client de téléchargement => Catégorie). Pour afficher toutes les versions, sélectionnez Options => Afficher les inconnues. La file d'attente n'est stockée nulle part dans l'application, mais elle est mise à jour via les réponses de l'API de votre client de téléchargement.

> Pour les clients Usenet, \*Arr ne vérifiera que les 60 premiers éléments de la file d'attente pour les importations potentielles ! Il est important de ne pas dépasser cette limite, sinon vous devrez effectuer des importations manuelles lorsque votre système sera surchargé et commencera à manquer des éléments !.
> La suppression des téléchargements terminés doit également être activée pour votre client de téléchargement. {.is-warning}

## Icônes d'action de la file d'attente

- X - Supprimer l'élément de la file d'attente
  - Supprimer la version du client de téléchargement - Supprimer la version du client de téléchargement. Obligatoire pour les éléments de version non correspondants
  - Ajouter la version à la liste noire - Ajouter la version à la liste noire
- Icône humaine - Importation manuelle de la version
- Icône de capture - Envoyer la version vers le client de téléchargement

## Statuts de la file d'attente

> Notez que ce qui suit est incomplet {.is-warning}

| Icône      | Statut                   | Description                                                                                     | Étapes de résolution                                     |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Horloge grise | Version en attente          | Le téléchargement attend que le client de téléchargement soit disponible ou que la version respecte les règles du profil de retard | N/A                                                      |
| Jaune     | Avertissement Impossible à importer | \*Arr n'a pas pu importer la version. Consultez l'info-bulle pour plus de détails                    | [Voir le guide de dépannage](/radarr/troubleshooting) |
| Violet     | Importation du téléchargement       | Le téléchargement est en cours d'importation                                                                           | N/A                                                      |
|            |                          |                                                                                                 |                                                          |
|            |                          |                                                                                                 |                                                          |

# Historique

L'onglet Historique affiche toutes les actions qui ont quitté la file d'attente car la tâche est terminée. Cela inclut les importations, les échecs, les captures, les suppressions et les mises à niveau.

L'icône de gauche représente l'action qui a été effectuée (la liste des actions possibles est indiquée ci-dessous). Vous pouvez filtrer ces actions en cliquant sur l'icône de filtre à droite. Vous pouvez également afficher plus de colonnes en cliquant sur Options.

![history2.png](/assets/radarr/history2.png)

Sur les statuts `Capturés`, vous pouvez cliquer sur l'icône `i` à droite pour voir plus de détails sur le téléchargement (à partir de quel indexeur il provient, l'URL de la capture, l'âge du téléchargement, etc.). Vous pouvez également marquer cet élément comme échec pour initier sa suppression, son ajout à la liste noire et sa recherche ultérieure.

![history4.png](/assets/radarr/history4.png)

# Liste noire

> La liste noire était auparavant appelée 'Blacklist' {.is-info}

La page de la liste noire vous montre les éléments qui sont placés sur liste noire afin qu'ils ne soient pas téléchargés à nouveau. Il s'agit d'échecs du processus automatique ou d'éléments marqués manuellement comme échecs. Les éléments restent sur la liste noire indéfiniment, sauf si vous les supprimez manuellement.

![blocklist1.png](/assets/radarr/blocklist1.png)

En cliquant sur l'icône `i` tout à droite, vous pouvez voir plus de détails sur l'entrée placée sur la liste noire, et savoir si elle a été marquée manuellement comme échec ou si elle a échoué automatiquement lors du téléchargement.

![blocklist2.png](/assets/radarr/blocklist2.png)

En cliquant sur le `x` tout à droite, vous pouvez supprimer l'élément de la liste noire, afin de pouvoir le télécharger à nouveau s'il a été ajouté par erreur.

## Raisons courantes pour placer des éléments sur la liste noire

- L'utilisateur a marqué le téléchargement comme échec manuellement
- L'utilisateur a sélectionné "Ajouter à la liste noire" lors de la suppression de la file d'attente
- Le client de téléchargement Usenet a signalé un échec de téléchargement de la version