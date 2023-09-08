---
title: Prowlarr Benutzerdefinierte Skripte
description: 
published: true
date: 2021-12-20T16:40:47.702Z
tags: prowlarr, needs-love, benutzerdefinierte skripte
editor: markdown
dateCreated: 2021-06-23T06:40:30.916Z
---

Wenn Sie ein benutzerdefiniertes Skript auslösen möchten, finden Sie hier weitere Details. Skripte werden in Prowlarr über die [Verbindungseinstellungen](/prowlarr/settings#connections) hinzugefügt.

# Übersicht

Prowlarr kann ein benutzerdefiniertes Skript ausführen, wenn eine Episode neu importiert oder umbenannt wird. Je nach Aktion werden unterschiedliche Parameter übergeben. Die Parameter werden dem Skript über Umgebungsvariablen übergeben.

## Prowlarr-Protokolle

Beachten Sie, dass Folgendes nur für benutzerdefinierte Skripte protokolliert wird:

- Die Ausgabe von Skript `stdout` wird als `Debug` protokolliert.
- Die Ausgabe von Skript `stderr` wird als `Info` protokolliert.
- Der Auslöser des Skripts wird als `Trace` protokolliert.

# Umgebungsvariablen

Die Umgebungsvariablen variieren je nach Ereignistyp. Details folgen in Kürze^tm^

> [Der Code zur Überprüfung befindet sich vorübergehend hier. Wiki-Beiträge sind willkommen](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## Beim Testen

Wenn Sie das Skript zu Prowlarr hinzufügen und auf "Testen" klicken, wird das Skript mit den folgenden Parametern aufgerufen. Das Skript sollte in der Lage sein, jeden nicht unterstützten Ereignistyp elegant zu ignorieren.

| Umgebungsvariable   | Details |
| -------------------- | ------- |
| `prowlarr_eventtype` | `Test`  |