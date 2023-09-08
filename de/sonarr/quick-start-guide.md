---
title: Sonarr Schnellstart-Anleitung
description: 
published: true
date: 2022-07-14T14:07:19.793Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-09-03T19:14:22.283Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Schnellstart-Setup-Anleitung](#schnellstart-setup-anleitung)
- [Starten](#starten)
- [Medienverwaltung](#medienverwaltung)
  - [Episodenbenennung](#episodenbenennung)
  - [Importieren](#importieren)
  - [Stammordner](#stammordner)
- [Profile](#profile)
- [Indexer](#indexer)
- [Download-Clients](#download-clients)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
- [Wie importiere ich Ihre vorhandene organisierte Medienbibliothek?](#wie-importiere-ich-ihre-vorhandene-organisierte-medienbibliothek)
  - [Episoden importieren](#episoden-importieren)
    - [Vorhandene Medien importieren](#vorhandene-medien-importieren)
    - [Keine Übereinstimmung gefunden](#keine-übereinstimmung-gefunden)
    - [Fehlerhaften Ordnername nach dem Import beheben](#fehlerhaften-ordnername-nach-dem-import-beheben)
- [Neue Serie hinzufügen](#neue-serie-hinzufügen)

# Schnellstart-Setup-Anleitung

> Diese Seite ist noch in Bearbeitung und nicht vollständig. Beiträge sind willkommen.

> Für eine detailliertere Erklärung aller Einstellungen siehe [Sonarr => Einstellungen](/sonarr/settings)
{.is-info}

In dieser Anleitung erklären wir die grundlegende Einrichtung, die Sie vornehmen müssen, um mit Sonarr zu starten. Wir werden einige Optionen überspringen, die Sie auf dem Bildschirm sehen können. Wenn Sie tiefer in diese Optionen eintauchen möchten, finden Sie eine ausführliche Erklärung auf der entsprechenden Seite in den FAQ und der Dokumentation.

> Bitte beachten Sie, dass in den Screenshots und GUI-Einstellungen in `orange` erweiterte Optionen enthalten sind. Sie müssen oben auf der Seite auf `Erweitert anzeigen` klicken, um sie sichtbar zu machen.
{.is-warning}

# Starten

Nach der Installation und dem Starten öffnen Sie einen Browser und gehen zu `http://{your_ip_here}:8989`

![qs_startup.png](/assets/sonarr/qs_startup.png)

# Medienverwaltung

Zuerst schauen wir uns die Einstellungen für die `Medienverwaltung` an, wo wir unsere bevorzugten Benennungs- und Dateiverwaltungseinstellungen einrichten können.

Klicken Sie auf `Einstellungen` => `Medienverwaltung` im linken Menü.

## Episodenbenennung

![qs_episodenaming.png](/assets/sonarr/qs_episodenaming.png)

- Aktivieren Sie das Kontrollkästchen, um Episoden umzubenennen.
- Entscheiden Sie sich für Ihre Standard-, Tages- und Anime-Episodenbenennungskonventionen. Sie sollten die empfohlenen Benennungskonventionen [hier](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) überprüfen.

> Wenn Sie sich dafür entscheiden, keine Qualitäts-/Auflösungs- oder Release-Gruppe einzuschließen, handelt es sich um Informationen, die Sie später nicht wiederherstellen können. Es wird dringend empfohlen, diese in Ihr Benennungsschema aufzunehmen.
{.is-info}

## Importieren

![mm_importing.png](/assets/sonarr/mm_importing.png)

- (Erweiterte Option) Wenn Sie möchten, dass TBA-Episoden sofort importiert werden, ändern Sie "Erforderlicher Episodentitel" in "Nie".
- (Erweiterte Option) Aktivieren Sie `Verwenden Sie Hardlinks anstelle von Kopieren` für weitere Informationen, wie und warum mit Beispielen [TRaSH's Hardlinks Guide](https://trash-guides.info/hardlinks).
- Aktivieren Sie das Kontrollkästchen, um zusätzliche Dateien zu importieren, und fügen Sie mindestens `.srt` zur Liste hinzu.

## Stammordner

Hier fügen wir den Stammordner hinzu, den Sonarr verwenden wird, um Ihre vorhandene organisierte Medienbibliothek zu importieren, und wohin Sonarr Ihre Medien nach dem Herunterladen durch Ihren Download-Client importieren wird (Kopieren/Hardlink/Verschieben). Dies ist der Ordner, in dem Ihre Serien und Episoden gespeichert sind, damit Ihr Mediaplayer sie abspielen kann. Es ist NICHT der Ort, an dem Sie Dateien herunterladen!

> \* Benutzer von Nicht-Windows: Wenn Sie einen NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
> \* Wenn Sie einen SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.
{.is-warning}

> **Der Benutzer und die Gruppe, die Sie für die Ausführung von Sonarr konfiguriert haben, müssen Lese- und Schreibzugriff auf diesen Speicherort haben.**
{.is-info}

> **Ihr Download-Ordner und Ihr Medienordner können nicht der gleiche Speicherort sein**
{.is-danger}

Vergessen Sie nicht, Ihre Änderungen zu speichern!

# Profile

`Einstellungen` => `Profile`

Wir empfehlen Ihnen, Ihre eigenen Profile zu erstellen und nur die gewünschten Qualitätsquellen auszuwählen. Es gibt jedoch auch mehrere vorausgefüllte Qualitätsprofile zur Auswahl, wenn eines davon passt. Wenn Sie weitere Informationen zu Profilen benötigen, lesen Sie bitte die [entsprechende Wiki-Seite](/sonarr/settings#profiles) für diesen Abschnitt.

# Indexer

`Einstellungen` => `Indexer`

Hier fügen Sie die Indexer/Tracker hinzu, die Sie tatsächlich zum Herunterladen Ihrer Dateien verwenden werden.

Nachdem Sie auf die Schaltfläche <kb>+</kb> geklickt haben, um einen neuen Indexer hinzuzufügen, wird ein neues Fenster mit vielen verschiedenen Optionen angezeigt. Für Sonarr gelten sowohl Usenet-Indexer als auch Torrent-Tracker als "Indexer".

Es gibt zwei Abschnitte: Usenet und Torrents. Je nachdem, welchen Download-Client Sie verwenden, wählen Sie den Typ des Indexers aus.

Die meisten Usenet-Indexer erfordern einen API-Schlüssel, der auf der Profilseite auf der Website des Indexers gefunden werden kann.

Die meisten Torrent-Tracker erfordern [Prowlarr](/prowlarr) oder Jackett, um in Sonarr verwendet zu werden.

Fügen Sie mindestens einen Indexer hinzu, damit Sonarr ordnungsgemäß funktioniert.

> Weitere Informationen finden Sie auf der [Einstellungsseite](/sonarr/settings#indexers) und auf der [Weitere Informationen (Unterstützt)](/sonarr/supported#indexers)-Seite für diesen Abschnitt.
{.is-info}

# Download-Clients

`Einstellungen` => `Download-Clients`

Das Herunterladen und Importieren ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss die Software in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Konfigurationen. Das bedeutet, dass es zwar einige gemeinsame Konfigurationen gibt, aber keine einheitliche Konfiguration und die Konfiguration jedes Benutzers etwas anders sein kann. Es gibt jedoch viele falsche Konfigurationen.

> Weitere Informationen finden Sie auf der [Einstellungsseite](/sonarr/settings#download-clients), auf der [Weitere Informationen (Unterstützt)](/sonarr/supported#download-clients)-Seite für diesen Abschnitt und in [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/).
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Sonarr sendet eine Download-Anfrage an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Sonarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Sonarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich an einem separaten Ort von Ihrem Medienordner befindet und von Sonarr zugänglich ist.
- Sonarr durchsucht diesen abgeschlossenen Speicherort nach Dateien, die Sonarr verwenden kann. Es analysiert den Dateinamen, um ihn mit den angeforderten Medien abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie an den angegebenen Speicherort.
- Atomare Verschiebungen (sofortige Verschiebungen) sind standardmäßig aktiviert. Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die atomare Verschiebung fehlschlägt oder Ihre Konfiguration keine Hardlinks und atomare Verschiebungen unterstützt, wird Sonarr auf die Datei zurückgreifen, sie kopieren und dann aus der Quelle löschen, was zu einer hohen E/A-Auslastung führt.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Sonarr aktiviert ist, werden übrig gebliebene Dateien aus dem Download anhand einer Anfrage an Ihren Client in den Papierkorb oder das Recycling verschoben/gelöscht.

### BitTorrent

{#bittorrent}

- Sonarr sendet eine Download-Anfrage an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Sonarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
- Abgeschlossene Dateien verbleiben an ihrem ursprünglichen Speicherort, damit Sie die Datei weiterverteilen können (Verhältnis oder Zeit kann im Download-Client oder innerhalb von Sonarr unter dem spezifischen Download-Client angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, erstellt Sonarr einen Hardlink zur Datei, sofern dies von Ihrer Konfiguration unterstützt wird, oder kopiert sie, wenn keine Hardlinks unterstützt werden.
- Hardlinks sind standardmäßig aktiviert. [Ein Hardlink erfordert keinen zusätzlichen Festplattenspeicher.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihre Konfiguration keine Hardlinks unterstützt, wird Sonarr auf die Datei zurückgreifen und sie kopieren.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Sonarr aktiviert ist, löscht Sonarr den Torrent aus Ihrem Client und fordert den Client auf, die Torrent-Daten zu entfernen, aber nur, wenn der Client meldet, dass das Seeden abgeschlossen ist und der Torrent gestoppt ist (nach Abschluss pausiert).

# Wie importiere ich Ihre vorhandene organisierte Medienbibliothek?

> Beachten Sie, dass Sonarr nicht regelmäßig nach Episoden sucht. Weitere Informationen finden Sie in der FAQ-Eintrag, um zu verstehen, wie Sonarr funktioniert.
[Wie findet Sonarr Episoden?](/sonarr/faq#how-does-sonarr-find-episodes)
{.is-info}

Nachdem Sie Ihre Profile/Qualitätsgrößen eingerichtet und Ihre Indexer und Download-Clients hinzugefügt haben, ist es Zeit, Ihre vorhandene organisierte Medienbibliothek zu importieren.

Demnächst verfügbar - Beiträge sind willkommen

## Vorhandene Medien importieren

Je nachdem, wie gut Ihre vorhandenen Serienordner benannt sind, wird Sonarr versuchen, sie mit der richtigen Serie abzugleichen. Überprüfen Sie diese Liste sorgfältig, bevor Sie importieren.

Die Bibliotheksimporthilfe sollte nur für eine vorhandene organisierte Bibliothek verwendet werden und nicht für einen Download-Ordner oder den ad-hoc-Import von Medien.

1. Navigieren Sie zu "Bibliothek importieren"
1. Lesen und verstehen Sie den Hilfetext zum Bibliotheksimport
1. Wählen Sie den Stammordner (Bibliothek) aus, aus dem Serien importiert werden sollen, oder fügen Sie ihn hinzu
1. Überprüfen Sie die Zuordnung/Übereinstimmung von Serienordnern in Sonarr mit TVDb-Serien
1. Legen Sie Ihre Überwachungseinstellungen und Qualitätsprofile entsprechend fest
1. Klicken Sie auf "Import starten"

### Keine Übereinstimmung gefunden

1. Suchen Sie den Seriennamen oder die TVDbId in der Serienauswahlbox
1. Sehen Sie [diesen FAQ-Eintrag](/sonarr/faq#why-can-i-not-add-a-series), wenn die Serie nicht gefunden werden kann

### Fehlerhaften Ordnername nach dem Import beheben

1. Entfernen Sie die Serie aus Sonarr
1. Bibliothek importieren
1. Stellen Sie sicher, dass die Serie korrekt zugeordnet ist

# Neue Serie hinzufügen

[Weitere Informationen finden Sie auf der Bibliotheksseite](/sonarr/library#add-new)

# Episoden importieren

- Verwenden Sie "Gewünscht" => "Manueller Import", um Episodendateien ad hoc in ihre Serienordner zu importieren
- Verwenden Sie "Episoden verwalten" auf der Seite einer Serie, um vorhandene Episodendateien in einem Serienordner neu zuzuordnen oder zuzuordnen