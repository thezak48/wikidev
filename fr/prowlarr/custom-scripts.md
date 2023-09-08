---
title: Scripts personnalisés Prowlarr
description: 
published: true
date: 2021-12-20T16:40:47.702Z
tags: prowlarr, needs-love, scripts personnalisés
editor: markdown
dateCreated: 2021-06-23T06:40:30.916Z
---

Si vous souhaitez déclencher un script personnalisé, vous pouvez trouver plus de détails ici. Les scripts sont ajoutés à Prowlarr via les [paramètres de connexion](/prowlarr/settings#connections).

# Aperçu

Prowlarr peut exécuter un script personnalisé lorsqu'un épisode est nouvellement importé ou renommé. Selon l'action, différents paramètres sont fournis. Les paramètres sont transmis au script via des variables d'environnement.

## Journaux Prowlarr

Notez que les éléments suivants ne seront enregistrés que pour les scripts personnalisés :

- La sortie `stdout` du script sera enregistrée en tant que `Debug`
- La sortie `stderr` du script sera enregistrée en tant que `Info`
- Le déclencheur du script sera enregistré dans `Trace`

# Variables d'environnement

Les variables d'environnement varient en fonction du type d'événement. Plus de détails à venir^tm^

> [Le code à examiner est disponible ici en attendant. Les contributions au wiki sont les bienvenues](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Test

Lorsque vous ajoutez le script à Prowlarr et cliquez sur 'Test', le script sera invoqué avec les paramètres suivants. Le script devrait pouvoir ignorer gracieusement tout type d'événement non pris en charge.

| Variable d'environnement | Détails |
| ----------------------- | ------- |
| `prowlarr_eventtype`    | `Test`  |