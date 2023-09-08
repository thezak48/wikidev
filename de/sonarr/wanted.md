---
title: Sonarr Wanted
description: 
published: true
date: 2021-11-29T22:12:55.806Z
tags: sonarr, needs-love, wanted
editor: markdown
dateCreated: 2021-06-10T01:40:02.329Z
---

# Gesucht

Der Abschnitt "Gesucht => Fehlend" enthält eine Liste der Episoden, die du markiert hast, um sie zu überwachen, aber die auf deiner Festplatte fehlen (noch nicht heruntergeladen wurden).

> Hier werden nur Episoden aufgelistet, die vollständig auf deiner Festplatte fehlen, nicht Episoden, die auf der Festplatte vorhanden sind, aber deren Abschneideprofil nicht erfüllt ist.
{.is-info}

- "Ausgewählte suchen" - Hier kannst du bestimmte Episoden auswählen, um nach ihnen in deinen Indexern zu suchen.

- "Ausgewählte nicht überwachen" - Hier kannst du bestimmte Episoden auswählen und die Überwachung beenden, wenn du nicht mehr interessiert bist.

- "Alle suchen" - Wenn du hier auswählst, wird eine Suche nach allen fehlenden Episoden bei allen deinen Indexern gestartet. Nachdem du auf die Schaltfläche gedrückt hast, wird ein Dialogfeld angezeigt, das dich warnt und dir mitteilt, wie viele Episoden gesucht werden. Dies ist besonders hilfreich, um zu wissen, ob deine Indexer deine API-Aufrufe begrenzen.

> Dieser Suchvorgang kann nicht abgebrochen werden, sobald er gestartet wurde, ohne Sonarr neu zu starten.
{.is-info}

Oben auf der Seite befindet sich "Manueller Import", mit dem du Mediendateien aus beliebigen Ordnern, auf die Sonarr zugreifen kann, für bereits in Sonarr vorhandene Serien willkürlich importieren kannst.

- "Automatisch verschieben" versucht, die Dateien automatisch den Serien/Episoden in Sonarr zuzuordnen und verschiebt sie - nicht kopiert oder hardlinkt - in deinen Bibliotheksordner.
- "Interaktiver Import" ermöglicht es dir, die Übereinstimmungen zu überprüfen und verschiedene Spezifikationen bei Bedarf anzupassen. Es bietet die Option (unten links), deine Dateien "Verschieben" oder "Kopieren/Hardlink" zu lassen. Stelle sicher, dass du die richtige Option für deine Bedürfnisse auswählst.
  
  > Wenn ein Verzeichnis mehr als 100 Dateien enthält, durchsucht Sonarr das Verzeichnis nicht rekursiv und versucht nicht, die Dateien zu analysieren und zuzuordnen. {.is-info}

# Abschneideprofil nicht erfüllt

Der Abschnitt "Gesucht => Abschneideprofil nicht erfüllt" enthält eine Liste der Episoden, die noch nicht ihren Abschneidepunkt erreicht haben. Der Abschneidepunkt wird in deinen Profilen festgelegt.

Der Abschneidepunkt ist der Punkt, an dem du Sonarr praktisch mitteilst, dass die Qualität der Videodatei für dich ausreichend ist und du nicht mehr möchtest, dass Sonarr nach einer besseren Qualität sucht.

Auf dieser Seite stehen dir einige Optionen zur Verfügung.
![wanted-cut-off-unmet.png](/assets/sonarr/wanted-cut-off-unmet.png)

1. "Ausgewählte suchen" - Durch Auswahl von Episoden in deiner Liste kannst du eine automatische Suche durchführen, um zu sehen, ob es Upgrades für deine vorhandenen Dateien gibt.
1. "Ausgewählte nicht überwachen" - Durch Auswahl bestimmter Episoden in deiner Liste kannst du Sonarr mitteilen, dass nach Upgrades für diese Episode nicht mehr gesucht werden soll, indem du die Überwachung beendest.
1. "Alle suchen" - Dies kann gefährlich sein (abhängig von der Größe deiner Liste), da du Sonarr damit beauftragst, nach jeder Datei zu suchen, die den Abschneidepunkt nicht erreicht hat. Dies kann nützlich sein, wenn du keine riesige Liste hast.
1. "Filter" - Damit kannst du deine Ergebnisse filtern. Dies ist nützlich, wenn du nach einer bestimmten Gruppe von Episoden oder Serien suchen möchtest.