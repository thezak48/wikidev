---
title: Sonarr-Bibliothek
description: 
published: true
date: 2022-10-28T17:18:11.116Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-06-11T23:31:01.289Z
---

# Serien

Die Serienseite zeigt Ihre gesamte Bibliothek an und ermöglicht es Ihnen, einzelne Serien auszuwählen (die Suche kann jedoch in großen Bibliotheken effizienter sein) und nach bestimmten Serien zu suchen. Sie können sie auch bearbeiten und Ihre Serien filtern.

# Filter

Die Filteroptionen ermöglichen es Ihnen, Ihre Serien einzugrenzen und sind äußerst hilfreich. Sie können verwendet werden, um Veröffentlichungsdaten, Namen, Episodenzahlen, Festplattengrößen und vieles mehr anzuzeigen, einschließlich benutzerdefinierter Filter, um Ihren Bedürfnissen gerecht zu werden. Diese können auch im Masseneditor verwendet werden.

# Neu hinzufügen

Die Funktion "Neu hinzufügen" ermöglicht es Ihnen, eine neue Serie hinzuzufügen, die von Sonarr überwacht und heruntergeladen werden soll.

- Stammordner - Der ausgewählte [Stamm-/Bibliotheksordner](/sonarr/settings#root-folders) in Sonarr, den diese Serie verwenden soll
- Überwachung - Wie soll die Serie anfangs überwacht werden?
  - Alle Episoden - Überwachen Sie alle Episoden außer Specials
  - Zukünftige Episoden - Überwachen Sie Episoden, die noch nicht ausgestrahlt wurden
  - Fehlende Episoden - Überwachen Sie Episoden, die keine Dateien haben oder noch nicht ausgestrahlt wurden
  - Vorhandene Episoden - Überwachen Sie Episoden, die Dateien haben
  - Erste Staffel - Überwachen Sie alle Episoden der ersten Staffel; alle anderen Staffeln werden ignoriert
  - Aktuelle Staffel - Überwachen Sie alle Episoden der aktuellen Staffel und zukünftiger Staffeln
  - Keine - Es werden keine Episoden überwacht
- Qualitätsprofil - Das [Qualitätsprofil](/sonarr/settings#quality-profiles), das für diese Serie verwendet werden soll
- Serientyp - Welchen Serientyp soll diese Serie verwenden? Dies ändert, wie die Suche durchgeführt wird [Weitere Informationen finden Sie in der FAQ](/sonarr/faq#whats-the-different-series-types)
- Staffelordner - Aktivieren oder deaktivieren Sie die Erstellung und Verwendung von Staffelordnern für diese Serie
- Tags - Verwendet, um Serien Release-Profilen, Verzögerungsprofilen, Indexern zuzuordnen oder einfach nur Ihre Serien zu organisieren
- [ ] Suche nach fehlenden Episoden starten - basierend auf Ihren ausgewählten Überwachungseinstellungen, suchen Sie nach allen fehlenden und überwachten Episoden in dieser Serie
- [ ] Suche nach nicht erfüllten Abschneideepisoden starten - basierend auf Ihren ausgewählten Überwachungseinstellungen und nur anwendbar, wenn Sie bereits Dateien für Ihre Episoden im Serienordner haben, suchen Sie nach allen vorhandenen und überwachten Episoden in dieser Serie, die Ihre Qualitätsprofil-Abschneidekriterien nicht erfüllen oder übertreffen

# Bibliothek importieren

Mit der Funktion "Bibliothek importieren" können Sie vorhandene, organisierte Serien- und Episodendateien über vorhandene Dateien im Pfadverzeichnis in Sonarr importieren. Dies ist besonders nützlich, wenn Sie eine neue Sonarr-Instanz erstellen und Ihre vorhandenen Serien beibehalten möchten.

- Die Bibliothek importieren dient dazu, eine vorhandene organisierte Bibliothek von Serien in Sonarr hinzuzufügen und zu importieren.

- Die Bibliothek importieren kann nicht für Folgendes verwendet werden:
  - Importieren von Dateien aus einem Download-Ordner
  - Hinzufügen oder Importieren von einer oder mehreren Dateien, die nicht ordnungsgemäß benannt und in ihrem eigenen Serienordner innerhalb Ihres Stammordners oder eines Ordners, den Sie als Stammordner hinzufügen möchten, organisiert sind
  - Jede andere Verwendung, die nicht das Hinzufügen einer Serie oder Episode zu Sonarr und das Importieren der Serie und ihrer Datei(en) aus dem (Bibliotheks-)Stammordner betrifft

> \* Nicht-Windows: Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
> \* Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.
{.is-warning}

> **Der Benutzer und die Gruppe, die Sie für Sonarr konfiguriert haben, müssen Lese- und Schreibzugriff auf diesen Speicherort haben.** {.is-info}

> Ihr Download-Client lädt in einen Download-Ordner herunter und Sonarr importiert ihn in Ihren Medienordner (endgültiges Ziel), den Ihr Medienserver verwendet.
{.is-info}

> **Ihr Download-Ordner und Ihr Medienordner können nicht der gleiche Speicherort sein**
{.is-danger}

# Masseneditor

Der Masseneditor ermöglicht es Ihnen, Serien massenhaft zu bearbeiten. Sie können alle zuvor vorgenommenen Einstellungen ändern, als Sie die Serie hinzugefügt haben.

# Staffelpass

Hier werden Informationen darüber angezeigt, wie viele Staffeln jede Serie hat und wie viele Episoden in jeder Staffel fehlen.