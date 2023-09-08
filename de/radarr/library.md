---
title: Radarr-Bibliothek
description: 
published: true
date: 2022-11-14T15:04:06.364Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:24:18.386Z
---

# Filme

## Bibliotheksansicht

- Alle aktualisieren - Metadaten für alle Filme aktualisieren, Poster aktualisieren, Filmordner erneut scannen und Filmdateien erneut scannen (falls aktiviert)
- Aktualisieren & Scannen - Metadaten des aktuell angezeigten Films aktualisieren und seinen Ordner erneut scannen
- RSS-Synchronisierung - RSS-Feed von Ihren Indexern aktualisieren und prüfen, ob etwas Neues zum Herunterladen verfügbar ist
- Alle suchen / Gefilterte suchen / Ausgewählte suchen - Alle Filme oder ausgewählte Filme in der aktuellen Ansicht suchen
- Manueller Import (Filmindex) - Manuell eine Filmdatei für einen Film importieren, den Sie zu Radarr hinzugefügt haben, aus einem beliebigen Ordner, auf den Radarr zugreifen kann
  - Automatisch verschieben - Versuchen Sie automatisch, eine Datei mit einem Film in Radarr abzugleichen und sie durch Verschieben zu importieren.
  - Interaktiver Import - Überprüfen Sie alle Dateien im Pfad und versuchen Sie, sie mit einem Film in Radarr abzugleichen, wobei der Benutzer die Ergebnisse überprüfen kann. Verschieben oder Kopieren/Hardlink ist eine auswählbare Option in der linken unteren Ecke.
- Manueller Import (Film) - Manuell eine Filmdatei für einen Film importieren, den Sie zu Radarr hinzugefügt haben, aus dem zugewiesenen Filmordner
  - Automatisch verschieben - Versuchen Sie automatisch, eine Datei mit einem Film in Radarr abzugleichen und sie durch Verschieben zu importieren.
  - Interaktiver Import - Überprüfen Sie alle Dateien im Pfad und versuchen Sie, sie mit einem Film in Radarr abzugleichen, wobei der Benutzer die Ergebnisse überprüfen kann. Verschieben oder Kopieren/Hardlink ist eine auswählbare Option in der linken unteren Ecke.
- Film-Editor / Filmindex - Zwischen dem Masseneditor-Modus und dem Filmindex (Bibliotheks-)Modus wechseln
- Optionen - Anzeigeoptionen ändern
- Ansicht - Ansichtstyp umschalten
  - Tabelle - Tabellarische Ansicht (Listenansicht)
  - Poster - Poster anzeigen (ähnlich wie Plex)
  - Übersicht - Übersichtsinformationen und Poster anzeigen (detaillierte Ansicht)
- Sortieren - Aktuelle Ansicht sortieren

### Filter

- Filter - Aktuelle Ansicht filtern
  - Nur überwachte - Titel, die auf Aktualisierungen überwacht werden.
  - Nicht überwacht - Titel, die nicht auf Aktualisierungen überwacht werden.
  - Fehlend - In der Datenbank überwacht, aber auf dem Dateisystem fehlend.
  - Gewünscht - In der Datenbank überwacht, fehlend, aber basierend auf den Verfügbarkeitseinstellungen verfügbar sein sollte
  - Unzureichende Abschneidung - Titel auf dem Dateisystem, aber weiterhin Überwachung auf gewünschte Qualität.
  - Benutzerdefinierte Filter
    - Überwacht (boolean)
    - Verfügbarkeit berücksichtigen (boolean)
    - Mindestverfügbarkeit (Enum)
      - Angekündigt
      - Im Kino
      - Veröffentlicht
    - Titel \[enthält\] (String)
    - Veröffentlichungsstatus (Enum)
      - TBA
      - Angekündigt
      - Im Kino
      - Veröffentlicht
      - Gelöscht
        - Von TMDb gelöscht
    - Studio (Enum Studios)
    - Sammlung (Enum Sammlungen)
    - Qualitätsprofil (Enum Qualitätsprofile)
    - Hinzugefügt (statisches DateTime, relative TimeDelta)
    - Jahr (Int)
    - Im Kino (statisches DateTime, relative TimeDelta)
    - Physische Veröffentlichung (statisches DateTime, relative TimeDelta)
    - Digitale Veröffentlichung (statisches DateTime, relative TimeDelta)
    - Laufzeit (Int)
    - Pfad \[enthält\] (String)
    - Größe auf der Festplatte (Int)
    - Genres \[enthält\] (Enum Genres)
    - TMDB-Bewertung (Float)
    - TMDB-Stimmen (Int)
    - IMDb-Bewertung
    - Tomato-Bewertung
    - IMDb-Stimmen
    - Zertifizierung (Enum Bewertung (PG-13, R, usw.))
    - Tags \[enthalten\] (Enum Tags)

# Neuen Film hinzufügen

![radarr-add-new-empty.png](/assets/radarr/radarr-add-new-empty.png)

- Wenn Sie einen neuen Film hinzufügen möchten, ist dies die Seite, auf der Sie dies tun können.
  - Die Anleitung finden Sie in unserem [Schnellstartleitfaden](/radarr/quick-start-guide).
- Unterhalb des Suchfelds finden Sie auch die Schaltfläche "Vorhandene Filme importieren". Wenn dies auf Sie zutrifft, finden Sie dazu auch großartige Informationen in unserem [Schnellstartleitfaden](/radarr/quick-start-guide).
- Wenn Sie den Fehler "Pfad ist bereits konfiguriert" erhalten, [sehen Sie sich diesen FAQ-Eintrag an](/radarr/faq#path-is-already-configured-for-an-existing-movie).

# Bibliothek importieren

Mit der Bibliothekimport-Funktion können Sie vorhandene organisierte Filme und die Dateien jedes Films über vorhandene Dateien im Pfadverzeichnis importieren. Dies ist besonders nützlich, wenn Sie eine neue Radarr-Instanz erstellen und Ihre vorhandenen Filme beibehalten möchten.

- Die Bibliothekimport-Funktion dient zum Hinzufügen und Importieren einer vorhandenen organisierten Filmbibliothek in Radarr.
- Die Bibliothekimport-Funktion kann nicht verwendet werden für:
  - Importieren von Dateien aus einem Download-Ordner
  - Hinzufügen oder Importieren von einer oder mehreren Dateien, die nicht ordnungsgemäß benannt und in ihrem eigenen Filmordner innerhalb Ihres Stammordners oder eines Ordners, den Sie als Stammordner hinzufügen möchten, organisiert sind
  - Alle anderen Verwendungen, die nicht das Hinzufügen eines Films zu Radarr und das Importieren des Films und seiner Datei aus dem (Bibliotheks-)Ordner, der in den Bibliothekimport eingegeben wurde, umfassen
- Wenn Sie den Fehler "Pfad ist bereits konfiguriert" erhalten, [sehen Sie sich diesen FAQ-Eintrag an](/radarr/faq#path-is-already-configured-for-an-existing-movie).
  
> Es ist erforderlich, dass Filmordner und -dateien das Jahr in ihrem Namen enthalten, um importiert und analysiert zu werden.{.is-warning}

> \* Nicht-Windows: Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
> \* Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.
{.is-warning}

> **Der Benutzer und die Gruppe, die Sie für die Ausführung von Radarr konfiguriert haben, müssen Lese- und Schreibzugriff auf diesen Speicherort haben.**
{.is-info}

> Ihr Download-Client lädt in einen Download-Ordner herunter und Radarr importiert ihn in Ihren Medienordner (endgültiges Ziel), den Ihr Medienserver verwendet.
{.is-info}

> **Ihr Download-Ordner und Ihr Medienordner können nicht der gleiche Speicherort sein**
{.is-danger}

# Sammlungen

Das Wiki wird von der Community entwickelt und gepflegt.
Dieser Abschnitt wurde nicht aktualisiert, um die Sammlungsseite in Radarr zu beschreiben.

# Entdecken

Entdecken zeigt empfohlene Filme an

- Wenn Sie keine Liste(n) haben, werden die 90 am meisten empfohlenen Filme basierend auf den von TMDb empfohlenen Filmen für die Filme in Ihrer Bibliothek sowie die 10 Empfehlungen Ihrer jüngsten Hinzufügungen angezeigt.

> Tipp: Sie können die von Radarr empfohlenen Filme deaktivieren und nur Filme von Ihren Listen anzeigen lassen in `Optionen`.
{.is-info}

- Wenn Sie Liste(n) haben, werden die oben genannten Empfehlungen angezeigt UND Einträge aus Ihren Liste(n).

> Tipp: Ändern Sie den `Filter` in `Neu Nicht ausgeschlossen`, um nur Filme anzuzeigen, die nicht in Ihrer Bibliothek enthalten sind.
{.is-info}

![radarr-discover-empty.png](/assets/radarr/radarr-discover-empty.png)

- Wahrscheinlich werden Ihre Entdeckungsempfehlungen spärlich sein, wenn Sie eine neue Installation mit wenigen oder keinen Filmen haben. Sie müssen Bibliotheksinhalte hinzufügen, um Empfehlungen zu erhalten. Sie haben mehrere Möglichkeiten:
  1. Klicken Sie auf die Schaltfläche [Neuen Film hinzufügen](/radarr/library#add-new), um Filme manuell hinzuzufügen.
  1. Klicken Sie auf die Schaltfläche [Vorhandene Bibliothek importieren](/radarr/library#library-import), um eine vorhandene Bibliothek zu importieren.
  1. Klicken Sie auf die Schaltfläche [Listen hinzufügen](/radarr/settings#lists), um eine Liste zu Radarr hinzuzufügen. Weitere Informationen zu Listen finden Sie auf der [Weitere Informationen (Unterstützt)](/radarr/faq#what-are-lists-and-what-can-they-do-for-me)-Seite für diesen Abschnitt.

![radarr-discover-add-new-movies.png](/assets/radarr/radarr-discover-add-new-movies.png)

- Sobald Sie einen Film auf eine der oben genannten drei Arten hinzugefügt haben, werden Ihnen verschiedene Filme zur Entdeckung angezeigt.
    1. Hier können Sie auswählen, welche Filme Sie Ihrer Bibliothek hinzufügen möchten
    1. Hier können Sie alle Filme auswählen, die auf dieser Liste stehen, wenn Sie besonders mutig sind
    1. Wählen Sie aus, in welchem Stammverzeichnis diese Filme nach dem Import landen sollen
    1. Wählen Sie aus, welche Verfügbarkeit der Film haben soll, bevor er heruntergeladen wird
    1. Wählen Sie alle bereits erstellten Qualitätsprofile aus ([Weitere Informationen](/radarr/settings#quality-profiles))
    1. Soll Radarr diesen Film auf Upgrades in der Qualität überwachen?
    1. Soll Radarr automatisch nach diesem Film suchen, nachdem Sie ihn hinzugefügt haben?
    1. Sollen diese Filme von allen importierten Listen ausgeschlossen werden? ([Weitere Informationen](/radarr/settings#list-exclusion))
    1. Fügen Sie den Film schließlich Ihrer Bibliothek hinzu.