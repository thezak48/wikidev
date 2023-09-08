---
title: Prowlarr Suche
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

Diese Seite zeigt Ihnen, wie Sie eine Suche innerhalb von Prowlarr durchführen können. Normalerweise würden Sie Ihre Suchen über die App durchführen, aber es ist auch möglich, sie direkt in Prowlarr zu machen.

# Eine Suche durchführen

Um eine Suche zu starten, klicken Sie auf `Suche` im linken Menü. Es wird eine weitgehend leere Seite mit einigen Optionen am unteren Bildschirmrand angezeigt.

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- Abfrage - Geben Sie Ihre Suchbegriffe in das Abfragefeld ein.
  - Klicken Sie auf das Vergrößerungsglas, um den Suchtyp zu ändern. Die verfügbaren Optionen sind:
    - Grundlegende Suche - Grundlegende Textabfrage
    - TV-Suche - Suche mit TV-Parametern, wie sie in der Benutzeroberfläche angezeigt werden, einschließlich ID-basierter (TVDbId, IMDbId, TMDbID usw.) und Staffel-/Episodensuchen
    - Film-Suche - Suche mit Film-Parametern, wie sie in der Benutzeroberfläche angezeigt werden, einschließlich ID-basierter (TMDbId, IMDbId, Genre usw.)
    - Audio-Suche - Suche mit Musik-Parametern, wie sie in der Benutzeroberfläche angezeigt werden, einschließlich Künstler, Album, Label, Genre usw.
    - Buch-Suche - Suche mit Buch-Parametern, wie sie in der Benutzeroberfläche angezeigt werden, einschließlich Autor, Titel usw.

> Diese werden in der Regel als `{Variablenname:Suchwert}` formatiert, z.B. für eine TV-Suche von The Simpsons Staffel 32 wäre die Sucheingabe `{TvdbId:71663} {Season:32}`
{.is-info}

> Beachten Sie, dass nicht alle Indexer alle Abfragetypen unterstützen {.is-info}

- Indexer - Wählen Sie Ihre Indexer im Dropdown-Menü "Indexer" aus. Sie können "Usenet" oder "Torrents" auswählen, um automatisch alle Indexer in diesen Kategorien auszuwählen, oder Sie können spezifische Indexer für Ihre Suche aus beiden Gruppen auswählen.
- Kategorie - Wählen Sie die Kategorien aus, nach denen Sie auf Ihren Indexern suchen möchten, aus dem Dropdown-Menü. Sie können übergeordnete Kategorien (TV, Filme usw.) auswählen, um automatisch alle Unterkategorien auszuwählen, oder Sie können spezifische Kategorien aus einer der Gruppen auswählen.

Klicken Sie dann auf die Schaltfläche `Suche`. Ihre Ergebnisse können einige Sekunden dauern, um angezeigt zu werden. Sobald sie angezeigt werden, können Sie Spalten hinzufügen oder entfernen, indem Sie die Schaltfläche `Optionen` verwenden, und Sie können Ihre Ergebnisse sortieren und filtern, indem Sie entweder auf die Spaltenüberschriften klicken oder die Schaltfläche `Filter` verwenden.

Sie können das Ergebnis herunterladen, indem Sie auf das Download-Symbol rechts neben dem Ergebnis klicken. Dadurch wird es an den richtigen Download-Client gesendet, den Sie konfiguriert haben.

Sie können Ergebnisse auch auf einmal herunterladen, indem Sie die Auswahlfelder auf der linken Seite aktivieren und die Schaltfläche `Freigaben abrufen` klicken.

> Alles, was heruntergeladen wird, hat die Kategoriezuweisung, die Sie in Prowlarr festgelegt haben. Dies erfordert möglicherweise einen manuellen Import in Ihrem App-Programm aus einem nicht standardmäßigen Verzeichnis! {.is-info}

# API-Endpunkte

## RSS-kompatibler - Einzelner Indexer-Feed

- Standard Newznab/Torznab-kompatibler Endpunkt/Parameter. Sie können die Abfragen entsprechend Ihren Bedürfnissen gemäß den definierten Standards anpassen.

> Ein aggregierter Multi-Indexer-Endpunkt wird aufgrund der erheblichen Nachteile dieser Funktion nicht hinzugefügt werden {.is-info}

### API-Schlüssel in der Abfrage

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - z.B. `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={yourkey}&cat=5000,2000`

### API-Schlüssel im Header

> Stellen Sie sicher, dass Sie `X-Api-Key` als Header mit dem API-Schlüssel übergeben {.is-info}

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - z.B. `http://192.168.1.100:9696/{indexerid}/api?t=search&q=mike&cat=5000,2000`

## Such-Feed

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/api/v1/search?query={encoded term}&indexerIds={comma separated list}&categories={comma separated list}&type={searchtype}`
  - z.B. `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - z.B. `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

Parameter

- `query` - URL-codierte Suchzeichenkette
- `indexerIds` - kommagetrennte Liste von Indexer-IDs
  - Lassen Sie den Parameter in der URL weg, um alle Indexer auszuwählen
  - `-2` sind alle Torrents
  - `-1` sind alle Usenet-Indexer
  - Indexer-IDs
- `categories` - kommagetrennte Liste von zu verwendenden Kategorien
  - Lassen Sie den Parameter weg, um alle auszuwählen
- `type` - der auszuführende Suchtyp
  - `search` - Grundlegende Textabfrage
  - `tvsearch` - TV-Abfrage - Unterstützt TV-Parameter
  - `moviesearch` - Filmabfrage - Unterstützt Film-Parameter
  - `audiosearch` - Audio/Musik-Abfrage - Unterstützt Musik-Parameter
  - `booksearch` - Buchabfrage - Unterstützt Buch-Parameter