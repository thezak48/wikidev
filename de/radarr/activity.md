---
title: Radarr Aktivität
description: 
published: true
date: 2022-02-06T09:07:15.520Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:28:36.350Z
---

# Aktivität

Im Aktivitäts-Tab können Sie vergangene und aktuelle Aktivitäten sehen, die von \*Arr durchgeführt wurden. Dazu gehören Importe, Löschungen, Upgrades, Downloads, Umbenennungen und Fehler.

# Warteschlange

Wenn etwas aktiv heruntergeladen wird und noch nicht in \*Arr importiert wurde, wird es auf der Warteschlangen-Seite angezeigt.

Die Warteschlange zeigt alle Elemente an, die die Anwendung in der angegebenen Kategorie des Download-Clients erkennen kann (Einstellungen => Download-Client => Kategorie). Um alle Veröffentlichungen anzuzeigen, wählen Sie Optionen => Unbekannte anzeigen. Die Warteschlange wird nicht in der Anwendung gespeichert, sondern über die API-Antworten Ihres Download-Clients aktualisiert.

> Für Usenet-Clients sucht \*Arr nur 60 Elemente tief in der Warteschlange nach potenziellen Importen! Es ist wichtig, diese Zahl nicht zu überschreiten, da Sie sonst manuelle Importe durchführen müssen, wenn Ihr System überlastet ist und Elemente verpasst werden!.
> Das Entfernen abgeschlossener Downloads sollte auch für Ihren Download-Client aktiviert sein. {.is-warning}

## Symbole für Warteschlangenaktionen

- X - Element aus der Warteschlange entfernen
  - Veröffentlichung aus dem Download-Client entfernen - Veröffentlichung aus dem Download-Client entfernen. Erforderlich für nicht übereinstimmende Veröffentlichungselemente
  - Veröffentlichung blockieren - Veröffentlichung zur Blockliste hinzufügen
- Menschliches Symbol - Manueller Import der Veröffentlichung
- Greif-Symbol - Veröffentlichung an Download-Client senden

## Warteschlangenstatus

> Beachten Sie, dass die folgende Tabelle unvollständig ist {.is-warning}

| Symbol      | Status                   | Beschreibung                                                                                     | Lösungsschritte                                          |
| ----------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| graue Uhr   | Veröffentlichung ausstehend          | Der Download wartet darauf, dass der Download-Client verfügbar ist oder dass die Veröffentlichung den Verzögerungsprofilregeln entspricht | N/A                                                      |
| gelb        | Warnung: Import nicht möglich | \*Arr konnte die Veröffentlichung nicht importieren. Lesen Sie den Tooltip für weitere Details                    | [Siehe den Fehlerbehebungsleitfaden](/radarr/troubleshooting) |
| lila        | Import wird durchgeführt       | Der Download wird importiert                                                                           | N/A                                                      |
|             |                          |                                                                                                 |                                                          |
|             |                          |                                                                                                 |                                                          |

# Verlauf

Der Verlauf-Tab zeigt alle Dinge an, die die Warteschlange durch das Beenden/Abschließen der Aufgabe verlassen haben. Dies umfasst Importe, Fehler, Downloads, Löschungen und Upgrades.

Das linke Symbol zeigt die durchgeführte Aktion an (die Liste der möglichen Aktionen wird unten angezeigt). Sie können diese Aktionen filtern, indem Sie auf das Filter-Symbol auf der rechten Seite klicken. Sie können auch weitere Spalten anzeigen, indem Sie auf Optionen klicken.

![history2.png](/assets/radarr/history2.png)

Bei `Heruntergeladen`-Status können Sie auf das `i`-Symbol auf der rechten Seite klicken, um weitere Details zum Download anzuzeigen (von welchem Indexer er stammt, die URL des Downloads, das Alter des Uploads usw.). Sie können auch dieses Element als fehlgeschlagen markieren, um eine Entfernung, Blockierung und erneute Suche des Elements zu initiieren.

![history4.png](/assets/radarr/history4.png)

# Blockliste

> Die Blockliste wurde früher als 'Blacklist' bezeichnet {.is-info}

Die Blockliste zeigt Ihnen Elemente an, die blockiert sind, damit sie nicht erneut heruntergeladen werden. Dies sind Fehler aus dem automatischen Prozess oder manuell als fehlgeschlagen markierte Elemente. Elemente bleiben für immer in der Blockliste, es sei denn, Sie entfernen sie manuell.

![blocklist1.png](/assets/radarr/blocklist1.png)

Wenn Sie auf das `i`-Symbol ganz rechts klicken, werden Ihnen weitere Details zum blockierten Eintrag angezeigt und ob er manuell als fehlgeschlagen markiert wurde oder während des Downloads automatisch fehlgeschlagen ist.

![blocklist2.png](/assets/radarr/blocklist2.png)

Wenn Sie auf das `x` ganz rechts klicken, wird das Element aus der Blockliste entfernt, sodass Sie es bei Bedarf erneut herunterladen können, falls es versehentlich hinzugefügt wurde.

## Häufige Gründe für die Blockierung

- Benutzer hat den Download manuell als fehlgeschlagen markiert
- Benutzer hat "Zur Blockliste hinzufügen" ausgewählt, als er es aus der Warteschlange entfernt hat
- Usenet-Download-Client hat einen Fehler beim Herunterladen der Veröffentlichung gemeldet