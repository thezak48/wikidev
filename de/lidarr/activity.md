---
title: Lidarr Aktivität
description: 
published: true
date: 2022-02-06T09:06:39.366Z
tags: lidarr, needs-love, activity
editor: markdown
dateCreated: 2021-06-14T21:35:25.390Z
---

# Aktivität

Im Aktivitäts-Tab kannst du vergangene und aktuelle Aktivitäten von \*Arr sehen. Dazu gehören Importe, Löschungen, Upgrades, Grabs, Umbenennungen und Fehler.

# Warteschlange

Wenn etwas aktiv heruntergeladen wird und noch nicht in \*Arr importiert wurde, wird es in der Warteschlange angezeigt.

Die Warteschlange zeigt alle Elemente an, die die Anwendung in der angegebenen Kategorie des Download-Clients erkennen kann (Einstellungen => Download-Client => Kategorie). Um alle Veröffentlichungen anzuzeigen, gehe zu Optionen => Unbekannte anzeigen. Die Warteschlange wird nicht in der Anwendung gespeichert, sondern über die API-Antworten deines Download-Clients aktualisiert.

> Für Usenet-Clients sucht \*Arr nur 60 Elemente tief in der Warteschlange nach potenziellen Importen! Es ist wichtig, diese Zahl nicht zu überschreiten, da du sonst manuelle Importe durchführen musst, wenn dein System überlastet ist und Elemente vermisst werden!.
> Entferne abgeschlossene Downloads sollte auch für deinen Download-Client aktiviert sein. {.is-warning}

## Symbole für Warteschlangenaktionen

- X - Element aus der Warteschlange entfernen
  - Veröffentlichung aus dem Download-Client entfernen - Veröffentlichung aus dem Download-Client entfernen. Erforderlich für nicht übereinstimmende Veröffentlichungselemente
  - Veröffentlichung auf Blockliste setzen - Veröffentlichung zur Blockliste hinzufügen
- Menschliches Symbol - Manueller Import der Veröffentlichung
- Grab-Symbol - Veröffentlichung an den Download-Client senden

## Warteschlangenstatus

> Beachte, dass die folgende Liste unvollständig ist {.is-warning}

| Symbol       | Status                   | Beschreibung                                                                                     | Lösungsschritte                                         |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| graue Uhr | Veröffentlichung ausstehend          | Der Download wartet darauf, dass der Download-Client verfügbar ist oder dass die Veröffentlichung den Verzögerungsprofilregeln entspricht | N/A                                                      |
| gelb     | Warnung: Import nicht möglich | \*Arr konnte die Veröffentlichung nicht importieren. Weitere Details findest du im Tooltip                    | [Siehe den Fehlerbehebungsleitfaden](/lidarr/troubleshooting) |
| lila     | Import wird durchgeführt       | Der Download wird importiert                                                                           | N/A                                                      |
|            |                          |                                                                                                 |                                                          |
|            |                          |                                                                                                 |                                                          |

# Verlauf

Der Verlauf-Tab zeigt alle Elemente an, die die Warteschlange durch das Beenden der Aufgabe verlassen haben. Dazu gehören Importe, Fehler, Grabs, Löschungen und Upgrades.

Das linke Symbol zeigt die durchgeführte Aktion an (die Liste der möglichen Aktionen wird unten angezeigt). Du kannst diese durch Klicken auf das Filter-Symbol auf der rechten Seite filtern. Du kannst auch mehr Spalten anzeigen lassen, indem du auf Optionen klickst.

![history2.png](/assets/lidarr/history2.png)

Bei `Grabs`-Status kannst du auf das `i`-Symbol auf der rechten Seite klicken, um weitere Details zum Download anzuzeigen (von welchem Indexer er stammt, die URL des Grabs, das Alter des Uploads usw.). Du kannst auch dieses Element als fehlgeschlagen markieren, um eine Entfernung, Blockierung und erneute Suche des Elements zu initiieren.

![history4.png](/assets/lidarr/history4.png)

# Blockliste

> Die Blockliste wurde früher als 'Blacklist' bezeichnet {.is-info}

Die Blockliste zeigt dir Elemente an, die blockiert sind und daher nicht erneut heruntergeladen werden. Diese sind Fehler des automatischen Prozesses oder manuell als fehlgeschlagen markierte Elemente. Elemente bleiben für immer in der Blockliste, es sei denn, du entfernst sie manuell.

![blocklist1.png](/assets/lidarr/blocklist1.png)

Wenn du auf das `i`-Symbol ganz rechts klickst, werden dir weitere Details zum blockierten Eintrag angezeigt und ob er manuell als fehlgeschlagen markiert wurde oder während des Downloads automatisch fehlgeschlagen ist.

![blocklist2.png](/assets/lidarr/blocklist2.png)

Wenn du auf das `x` ganz rechts klickst, wird das Element aus der Blockliste entfernt, sodass du es bei Bedarf erneut herunterladen kannst, falls es versehentlich hinzugefügt wurde.

## Häufige Gründe für die Blockierung

- Benutzer hat den Download manuell als fehlgeschlagen markiert
- Benutzer hat "Zur Blockliste hinzufügen" ausgewählt, als er aus der Warteschlange entfernt wurde
- Usenet-Download-Client hat einen Fehler beim Herunterladen der Veröffentlichung gemeldet