---
title: Readarr Bibliothek
description: 
published: true
date: 2021-11-30T01:41:54.243Z
tags: readarr, needs-love, library
editor: markdown
dateCreated: 2021-11-30T00:50:59.442Z
---

# Bibliothek

Dieser Abschnitt dient der Verwaltung Ihrer Bibliothek von [Autoren](#autoren) und [Büchern](#bücher).

# Autoren

- Bibliotheksansicht
  - Alle aktualisieren - Metadaten für alle Autoren aktualisieren, Poster aktualisieren, Autorenordner erneut scannen und Buchdateien erneut scannen (falls aktiviert)
  - Aktualisieren & Scannen - Metadaten des aktuell angezeigten Autors aktualisieren und dessen Ordner erneut scannen
  - RSS-Synchronisierung - Den RSS-Feed von Ihren Indexern aktualisieren und prüfen, ob etwas Neues zum Abrufen veröffentlicht wurde
  - Autoren-Editor / Autoren-Index - Zwischen dem Masseneditor-Modus und dem Autoren-Index (Bibliothek) wechseln
  - Optionen - Anzeigeoptionen ändern
  - Ansicht - Ansichtstyp umschalten
    - Tabelle - Tabellarische Ansicht (Listenansicht)
    - Poster - Poster anzeigen (ähnlich wie Plex)
    - Übersicht - Übersichtsinformationen und das Poster anzeigen (detaillierte Ansicht)
  - Sortieren - Die aktuelle Ansicht sortieren
  - Filtern - Die aktuelle Ansicht filtern

# Bücher

- Bibliotheksansicht
  - Alle aktualisieren - Metadaten für alle Autoren aktualisieren, Poster aktualisieren, Autorenordner erneut scannen und Buchdateien erneut scannen (falls aktiviert)
  - Aktualisieren & Scannen - Metadaten des aktuell angezeigten Autors aktualisieren und dessen Ordner erneut scannen
  - RSS-Synchronisierung - Den RSS-Feed von Ihren Indexern aktualisieren und prüfen, ob etwas Neues zum Abrufen veröffentlicht wurde
  - Alle durchsuchen / Gefilterte durchsuchen / Ausgewählte durchsuchen - Alle Bücher oder ausgewählte Bücher in der aktuellen Ansicht durchsuchen
  - Buch-Editor / Buch-Index - Zwischen dem Masseneditor-Modus und dem Buch-Index (Bibliothek) wechseln
  - Optionen - Anzeigeoptionen ändern
  - Ansicht - Ansichtstyp umschalten
    - Tabelle - Tabellarische Ansicht (Listenansicht)
    - Poster - Poster anzeigen (ähnlich wie Plex)
    - Übersicht - Übersichtsinformationen und das Poster anzeigen (detaillierte Ansicht)
  - Sortieren - Die aktuelle Ansicht sortieren
  - Filtern - Die aktuelle Ansicht filtern
  
# Neu hinzufügen

![addnew.png](/assets/readarr/addnew.png)

- Sie können neue Autoren oder einzelne Bücher hinzufügen, indem Sie den Namen des Autors oder den Buchtitel hier eingeben und ihn aus der Ergebnisliste auswählen.
  - Eine Anleitung dazu finden Sie in unserem [Schnellstartleitfaden](/readarr/quick-start-guide).
- Sie können auch Autoren nach GoodReads-ID, ISBN oder ASIN hinzufügen, falls erforderlich, und das angegebene Format verwenden.

![poe.png](/assets/readarr/poe.png)

- Klicken Sie auf den Namen des Autors oder des Buches, um ihn zu Readarr hinzuzufügen. Es wird ein Dialogfeld mit Optionen angezeigt.

![addauthor.png](/assets/readarr/addauthor.png)

- Stammordner - Wählen Sie hier den Stammordner aus. Ändern Sie dies nicht, wenn Sie den Calibre Content Server verwenden.
- Überwachen - Wählen Sie den Überwachungsstatus aller Bücher dieses Autors aus.
- Qualitätsprofil - Wählen Sie das Qualitätsprofil aus, das beim Suchen nach Büchern dieses Autors verwendet werden soll.
- (Nur Buch) Metadatenprofil - Wählen Sie das Metadatenprofil für dieses Buch aus.
- Tags - Wenn Sie möchten, dass diesem Autor Bücher mit einem Tag versehen werden, geben Sie ihn hier ein.
- Suche nach fehlenden Büchern starten - Wählen Sie aus, ob sofort eine historische Suche in Ihren Indexern nach allen Büchern dieses Autors gestartet werden soll. Wenn Sie dies nicht tun, werden nur NEU hochgeladene Bücher ab diesem Zeitpunkt abgerufen.
- {Autorname} hinzufügen oder {Buchname} hinzufügen - Klicken Sie auf die Schaltfläche "Hinzufügen", um diesen Autor zu Readarr hinzuzufügen und Metadaten für alle Bücher dieses Autors abzurufen. Dieser Vorgang kann einige Zeit dauern, daher ist es ratsam, nicht zu viele Autoren zu schnell hinzuzufügen.

> Wenn Sie ein einzelnes Buch hinzufügen und `None`\* für das [Metadatenprofil](/readarr/settings#metadata-profiles) auswählen, wird nur dieses Buch unter dem Autor angezeigt, wenn es hinzugefügt wird. Wenn Sie weitere Bücher für diesen Autor hinzufügen möchten, wählen Sie ein geeignetes Metadatenprofil aus.
> \* **Beachten Sie, dass `None` keine Metadatenfilter anwendet und Sie unerwünschte fremdsprachige Ausgaben erhalten können. Um dies zu umgehen, [erstellen Sie ein Metadatenprofil gemäß der FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Nicht zugeordnete Dateien

![unmappedfiles.png](/assets/readarr/unmappedfiles.png)

Wenn hier Bücher aufgelistet sind, werden sie von Readarr nicht erkannt und nicht als "vorhanden" in Readarr aufgeführt, befinden sich jedoch in einem der von Ihnen definierten Stammordner.

Weitere Informationen erhalten Sie, indem Sie auf das *i*-Symbol rechts klicken.

Sie können das Buch manuell importieren, indem Sie auf das *Person*-Symbol rechts klicken.

Sie können die Buchdatei löschen, indem Sie auf das *Mülleimer*-Symbol rechts klicken.

Sie können auch oben auf *Fehlende hinzufügen* klicken, um zu versuchen, alle Bücher zu Readarr hinzuzufügen. Beachten Sie, dass dies zeitaufwändig sein kann, wenn Sie hier viele Bücher aufgelistet haben.