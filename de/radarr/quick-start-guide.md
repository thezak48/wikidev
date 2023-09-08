---
title: Radarr Schnellstart-Anleitung
description: 
published: true
date: 2023-08-27T22:14:05.687Z
tags: radarr, quickstart
editor: markdown
dateCreated: 2021-06-20T20:05:44.814Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Schnellstart-Setup-Anleitung](#schnellstart-setup-anleitung)
- [Starten](#starten)
- [Medienverwaltung](#medienverwaltung)
  - [Filmbenennung](#filmbenennung)
  - [Importieren](#importieren)
  - [Dateiverwaltung](#dateiverwaltung)
  - [Stammordner](#stammordner)
- [Profile](#profile)
- [Qualität](#qualität)
- [Indexer](#indexer)
- [Download-Clients](#download-clients)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [So importieren Sie Ihre vorhandene organisierte Medienbibliothek](#so-importieren-sie-ihre-vorhandene-organisierte-medienbibliothek)
  - [Filme importieren](#filme-importieren)
  - [Vorhandene Medien importieren](#vorhandene-medien-importieren)
    - [Keine Übereinstimmung gefunden](#keine-übereinstimmung-gefunden)
    - [Fehlerhafter Ordnername nach dem Import beheben](#fehlerhafter-ordnername-nach-dem-import-beheben)
  - [So fügen Sie einen Film hinzu](#so-fügen-sie-einen-film-hinzu)

# Schnellstart-Setup-Anleitung

> Diese Seite ist noch in Bearbeitung und nicht vollständig. Beiträge sind willkommen.

> Für eine detailliertere Erläuterung aller Einstellungen siehe [Radarr => Einstellungen](/radarr/settings)
{.is-info}

In dieser Anleitung erklären wir das grundlegende Setup, das Sie durchführen müssen, um mit Radarr zu starten. Wir werden einige Optionen überspringen, die Sie auf dem Bildschirm sehen können. Wenn Sie tiefer in diese Optionen eintauchen möchten, finden Sie eine ausführliche Erklärung auf der entsprechenden Seite in den FAQ und der Dokumentation.

> Bitte beachten Sie, dass in den Screenshots und GUI-Einstellungen in `orange` erweiterte Optionen enthalten sind. Sie müssen oben auf der Seite auf `Erweitert anzeigen` klicken, um sie sichtbar zu machen.
{.is-warning}

# Starten

Nach der Installation und dem Starten öffnen Sie einen Browser und gehen zu `http://{Ihre_IP_hier_einfügen}:7878`

![Radarr-start.png](/assets/radarr/Radarr-start.png)

# Medienverwaltung

Zuerst werfen wir einen Blick auf die Einstellungen für die `Medienverwaltung`, in denen wir unsere bevorzugten Benennungs- und Dateiverwaltungseinstellungen festlegen können.

`Einstellungen` => `Medienverwaltung`

![Radarr-settings-mm.png](/assets/radarr/Radarr-settings-mm.png)

## Filmbenennung

![Radarr-settings-mm-movie-naming.png](/assets/radarr/Radarr-settings-mm-movie-naming.png)

1. Aktivieren/Deaktivieren Sie die Umbenennung Ihrer Filme (anstatt die Namen beizubehalten, die sie derzeit haben oder als Sie sie heruntergeladen haben).
2. Wenn Sie illegale Zeichen ersetzen oder entfernen möchten (`\ / : * ? " < > | ~ # % & + { }`).
3. Diese Einstellung legt fest, wie Radarr Doppelpunkte in der Filmdatei behandelt.
4. Hier wählen Sie die Benennungskonvention für die eigentlichen Filmdateien aus.
5. *(Erweiterte Option) Hier legen Sie die Benennungskonvention für den Ordner fest, der die Videodatei enthält.*

> Wenn Sie eine empfohlene Benennungsschema und Beispiele wünschen, werfen Sie einen Blick auf [TRaSH's empfohlene Benennungsschemata](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/).
{.is-info}

## Importieren

![Radarr-settings-mm-importing.png](/assets/radarr/Radarr-settings-mm-importing.png)

1. *(Erweiterte Option) Aktivieren Sie `Hardlinks anstelle von Kopieren verwenden` für weitere Informationen und Beispiele siehe [TRaSH's Hardlinks-Anleitung](https://trash-guides.info/hardlinks).*
1. *(Erweiterte Option) Importieren Sie passende zusätzliche Dateien (Untertitel, nfo usw.) nach dem Importieren einer Datei.*

## Dateiverwaltung

![Radarr-settings-mm-fm.png](/assets/radarr/Radarr-settings-mm-fm.png)

1. Filme, die von der Festplatte gelöscht wurden, werden automatisch in Radarr nicht mehr überwacht.
    - Möglicherweise möchten Sie einen Film löschen, möchten jedoch nicht, dass Radarr den Film erneut herunterlädt. In diesem Fall verwenden Sie diese Option.
1. *(Erweiterte Option) Bestimmen Sie einen Speicherort, an den gelöschte Dateien verschoben werden sollen (falls Sie sie wiederherstellen möchten, bevor der Papierkorb geleert wird).*
1. *(Erweiterte Option) Dies gibt an, wie alt eine bestimmte Datei sein kann, bevor sie dauerhaft gelöscht wird.*

## Stammordner

![Radarr-settings-mm-root-folder.png](/assets/radarr/Radarr-settings-mm-root-folder.png)

Hier fügen wir den Stammordner hinzu, den Radarr zum Importieren Ihrer vorhandenen organisierten Medienbibliothek verwenden wird und wohin Radarr Ihre Medien nach dem Herunterladen durch Ihren Download-Client importieren wird (Kopieren/Hardlink/Verschieben).

> \* Nicht-Windows: Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
> \* Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.
{.is-warning}

> **Der Benutzer und die Gruppe, die Sie für die Ausführung von Radarr konfiguriert haben, müssen Lese- und Schreibzugriff auf diesen Speicherort haben.** {.is-info}

> Ihr Download-Client lädt in einen Download-Ordner herunter, und Radarr importiert ihn in Ihren Medienordner (endgültiges Ziel), den Ihr Medienserver verwendet.
{.is-info}

> **Ihr Download-Ordner und Ihr Medien- (Bibliotheks- / Stamm-) Ordner können nicht der gleiche Speicherort sein.**
{.is-danger}

Vergessen Sie nicht, Ihre Änderungen zu speichern.

# Profile

`Einstellungen` => `Profile`

![Radarr-settings-profiles.png](/assets/radarr/Radarr-settings-profiles.png)

Hier können Sie Profile konfigurieren, die für die Qualität, die bevorzugte Sprache und die benutzerdefinierte Formatbewertung eines Films, den Sie herunterladen möchten, verwendet werden können.

Wir empfehlen Ihnen, Ihre eigenen Profile zu erstellen und nur die gewünschten Qualitätsquellen und Sprachen auszuwählen.

Weitere Informationen zu fremdsprachigen Titeln und Sprachen finden Sie in [diesem FAQ-Eintrag](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles).

Viele Benutzer finden [TRaSH's Anleitung zur benutzerdefinierten Formatierung von Sprachen](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) hilfreich, um die gewünschten Sprachen für Filme festzulegen.

Profile ist auch der Ort, an dem benutzerdefinierte Formatbewertungen konfiguriert werden. Es wird dringend empfohlen, die folgenden benutzerdefinierten Formate aus [TRaSH's Anleitungen](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) hinzuzufügen, um unerwünschte Downloads zu vermeiden. Weitere Informationen finden Sie im verlinkten TRaSH Guide Custom Format-Artikel und in den drei zusätzlichen referenzierten TRaSH Custom Format Guides oben auf der Seite Collection of Custom Formats.

- [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) verhindert das Herunterladen von Veröffentlichungen mit Dolby Vision (DV), die einen grünen Farbstich aufweisen, wenn DV nicht unterstützt wird.
- [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) verhindert das Herunterladen von schlecht benannten BR-DISKs, die nicht der BR-DISK-Qualitätsparsing entsprechen.

> Weitere Informationen finden Sie unter [Einstellungen => Profile](/radarr/settings#profiles).
> Um den Unterschied zwischen den Qualitätsquellen zu sehen, werfen Sie einen Blick auf unsere [Qualitätsdefinitionen](/radarr/settings#qualities-defined).
{.is-info}

# Qualität

`Einstellungen` => `Qualität`

![Radarr-settings-quality.png](/assets/radarr/Radarr-settings-quality.png)

Hier können Sie die Mindest- und Maximalgröße Ihrer gewünschten Mediendateien ändern/feinabstimmen (bei Verwendung von Usenet sollten Sie die RAR/PAR2-Dateien beachten).

> Wenn Sie Hilfe bei den Einstellungen für die Qualität benötigen, werfen Sie einen Blick auf [TRaSH's Größenempfehlungen](https://trash-guides.info/Radarr/Radarr-Quality-Settings-File-Size/) für ein getestetes Beispiel.
{.is-info}

# Indexer

`Einstellungen` => `Indexer`

![Radarr-settings-indexers.png](/assets/radarr/Radarr-settings-indexers.png)

Hier fügen Sie den Indexer/Tracker hinzu, den Sie tatsächlich zum Herunterladen Ihrer Dateien verwenden möchten.

Nachdem Sie auf die Schaltfläche <kb>+</kb> geklickt haben, um einen neuen Indexer hinzuzufügen, wird ein neues Fenster mit vielen verschiedenen Optionen angezeigt. Für Radarr gelten sowohl Usenet-Indexer als auch Torrent-Tracker als "Indexer".

Es gibt zwei Abschnitte: Usenet und Torrents. Je nachdem, welchen Download-Client Sie verwenden, sollten Sie den Typ des Indexers auswählen.

Für Torrent-Tracker - fast alle erfordern die Verwendung von [Prowlarr](/prowlarr) oder [Jackett](https://github.com/Jackett/Jackett).

# Download-Clients

`Einstellungen` => `Download-Clients`

![Radarr-settings-download-clients.png](/assets/radarr/Radarr-settings-download-clients.png)

Das Herunterladen und Importieren ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss die Software in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Lese- und Schreibzugriff auf den Speicherort zu haben, an dem der Download-Client die heruntergeladenen Dateien meldet. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Setups. Das bedeutet, dass es zwar einige gemeinsame Setups gibt, aber kein einziges richtiges Setup und jedes Setup ein wenig anders sein kann. Es gibt jedoch viele falsche Setups.

> Weitere Informationen finden Sie auf der [Einstellungsseite](/radarr/settings#download-clients), auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#download-clients) für diesen Abschnitt und in [TRaSH's Download-Client-Anleitungen](https://trash-guides.info/Downloaders/) für weitere Informationen.
{.is-info}

## Download-Protokolle {.tabset}

### Usenet

{#usenet}

- Radarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Radarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Radarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich an einem separaten Ort von Ihrem Medienordner befindet und von Radarr zugänglich ist.
- Radarr durchsucht diesen abgeschlossenen Speicherort nach Dateien, die Radarr verwenden kann. Es analysiert den Dateinamen, um ihn mit dem angeforderten Medium abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie an den angegebenen Speicherort.
- Atomare Verschiebungen (sofortige Verschiebungen) sind standardmäßig aktiviert. Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die atomare Verschiebung fehlschlägt oder Ihr Setup keine Hardlinks und atomare Verschiebungen unterstützt, wird Radarr auf das Kopieren der Datei zurückgreifen und sie dann aus der Quelle löschen, was zu hohem IO-Aufwand führt.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Radarr aktiviert ist, werden übrig gebliebene Dateien aus dem Download über eine Anfrage an Ihren Client in den Papierkorb oder das Recycling verschoben.

### BitTorrent

{#bittorrent}

- Radarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Radarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
- Abgeschlossene Downloads, die noch seeden, verbleiben mit ihren Dateien an ihrem ursprünglichen Speicherort, damit Sie die Datei seeden können (Verhältnis oder Zeit kann im Download-Client oder innerhalb von Radarr unter dem spezifischen Download-Client angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, erstellt Radarr einen Hardlink zur Datei, sofern dies von Ihrem Setup unterstützt wird, oder kopiert sie, wenn keine Hardlinks unterstützt werden. Torrents, die pausiert und vollständig gesät sind, werden atomar verschoben, wenn Hardlinks unterstützt werden, oder kopiert und gelöscht, wenn sie nicht unterstützt werden.
- Hardlinks sind standardmäßig aktiviert. [Ein Hardlink erfordert keinen zusätzlichen Festplattenspeicher.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihr Setup keine Hardlinks unterstützt, wird Radarr auf das Kopieren der Datei zurückgreifen.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Radarr aktiviert ist, löscht Radarr den Torrent aus Ihrem Client und fordert den Client auf, die Torrent-Daten zu entfernen, jedoch nur, wenn der Client meldet, dass das Seeding abgeschlossen ist und der Torrent gestoppt ist (bei Abschluss pausiert).

# So importieren Sie Ihre vorhandene organisierte Medienbibliothek

> Beachten Sie, dass Radarr nicht regelmäßig nach Filmen sucht. Lesen Sie den FAQ-Eintrag [Wie funktioniert Radarr?](/radarr/faq#how-does-radarr-work), um zu verstehen, wie Radarr funktioniert.
{.is-info}

Nachdem Sie Ihre Profile/Qualitätsgrößen eingerichtet und Ihre Indexer und Download-Clients hinzugefügt haben, ist es Zeit, Ihre vorhandene organisierte Medienbibliothek zu importieren.

`Filme`

![Radarr-movies.png](/assets/radarr/Radarr-movies.png)

Wählen Sie `Vorhandene Filme importieren` oder wählen Sie `Importieren` in der Seitenleiste.

## Filme importieren

![Radarr-movies-import.png](/assets/radarr/Radarr-movies-import.png)

Wählen Sie den Stammordner aus, den Sie zuvor [im Abschnitt Stammordner](#stammordner) hinzugefügt haben.

## Vorhandene Medien importieren

![Radarr-importing-existing.png](/assets/radarr/Radarr-importing-existing.png)

Je nachdem, wie gut Ihre vorhandenen Filmordner benannt sind, wird Radarr versuchen, sie mit dem richtigen Film abzugleichen, wie in Nr. 5 zu sehen ist. Wenn sich alle Ihre Filme in einem einzigen Verzeichnis befinden, befolgen Sie diese [Anleitung](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

1. Der Name Ihres Filmordners.
1. Überwachung - Wie möchten Sie, dass der Film zu Radarr hinzugefügt wird.

- Keine - Den Film oder die Sammlung nicht auf neue Veröffentlichungen überwachen
- Nur Film - Nur den Film auf neue Veröffentlichungen überwachen
- Film & Sammlung - Sowohl den Film auf neue Veröffentlichungen überwachen als auch alle Filme in der Sammlung des Films hinzufügen und überwachen (falls vorhanden)

1. Verfügbarkeit - Wann Radarr einen Film als verfügbar betrachtet.

- **Angekündigt**: Radarr betrachtet Filme als verfügbar, sobald sie zu Radarr hinzugefügt werden. Diese Einstellung wird *empfohlen*, wenn Sie gute private Tracker haben, die keine Fälschungen enthalten.
- **Im Kino**: Radarr betrachtet Filme als verfügbar, sobald sie in die Kinos kommen. Diese Option wird *nicht empfohlen*.
- **Veröffentlicht**: Radarr betrachtet Filme als verfügbar, sobald die Blu-ray veröffentlicht wird. Diese Option wird *empfohlen*, wenn Ihre Indexer häufig Fälschungen enthalten.

1. Qualitätsprofil - Wählen Sie Ihr bevorzugtes Profil aus.
1. Film - Der Film, den Radarr als Übereinstimmung betrachtet. Es ist wichtig, dass Sie dies überprüfen und bei Bedarf die Übereinstimmung bearbeiten/suchen, wenn sie nicht korrekt ist. Falsche Übereinstimmungen werden oft durch schlecht benannte Ordner verursacht.
1. Massenauswahl des Überwachungsstatus.
1. Massenauswahl der Mindestverfügbarkeit.
1. Massenauswahl des Qualitätsprofils.
1. Starten Sie den Import Ihrer vorhandenen Medienbibliothek.

Sobald ein Film zu Radarr hinzugefügt wurde, durchsucht Radarr den Ordner des Films und versucht, eine Videodatei in dem Ordner mit dem Film abzugleichen. Die häufigste Ursache dafür, dass Radarr die Datei nicht abgleicht und der Film daher den Radarr-Status "Fehlt" hat, ist, dass der Dateiname das Jahr nicht enthält. Radarr erfordert das Jahr im Dateinamen, um es analysieren zu können.  

### Keine Übereinstimmung gefunden

Wenn Sie einen Fehler wie diesen erhalten

![Radarr-importing-existing-no-match.png](/assets/radarr/Radarr-importing-existing-no-match.png)

haben Sie wahrscheinlich einen Fehler bei der Benennung Ihres Filmordners gemacht.

Um dieses Problem zu beheben, können Sie Folgendes versuchen:

Erweitern Sie die Fehlermeldung

![Radarr-importing-existing-no-match-expand.png](/assets/radarr/Radarr-importing-existing-no-match-expand.png)

und überprüfen Sie auf [themoviedb](https://www.themoviedb.org/), ob das Jahr oder der Titel übereinstimmt. In diesem Beispiel werden Sie feststellen, dass das Jahr falsch ist, und Sie können es ändern, indem Sie das Jahr ändern und auf das Aktualisierungssymbol klicken.

![radarr-importing-existing-no-match-expand-refresh.png](/assets/radarr/radarr-importing-existing-no-match-expand-refresh.png)

Oder Sie können einfach die tmdb:id oder imdb:id verwenden (wenn tmdb mit imdb verknüpft ist) und dann den gefundenen Film auswählen, wenn er übereinstimmt.

![Radarr-importing-existing-no-match-expand-tmdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-tmdb.png)

![Radarr-importing-existing-no-match-expand-imdb.png](/assets/radarr/Radarr-importing-existing-no-match-expand-imdb.png)

### Beheben Sie den fehlerhaften Ordnername nach dem Import

![Radarr-wrong-folder-name.png](/assets/radarr/Radarr-wrong-folder-name.png)

Sie werden feststellen, dass der Ordnername nach der während des Imports vorgenommenen Korrektur immer noch das falsche Jahr enthält. Um dies zu beheben, werden wir einen kleinen Zaubertrick anwenden.

Gehen Sie zu Ihrer Filmübersicht

`Filme`

Klicken Sie oben auf `Film-Editor`

![Radarr-movie-editor.png](/assets/radarr/Radarr-movie-editor.png)

Nach der Aktivierung wählen Sie den/die Film(e) aus, bei dem/denen Sie den/die Ordner umbenennen möchten.

![Radarr-movie-editor-select.png](/assets/radarr/Radarr-movie-editor-select.png)

1. Wenn Sie möchten, dass alle Ihre Filmordner gemäß dem zuvor festgelegten Ordnerbenennungsschema umbenannt werden [Abschnitt zur Filmnamensgebung](#movie-naming).
2. Wählen Sie den/die Film(e) aus, bei dem/denen Sie den/die Ordner umbenennen möchten.
3. Wählen Sie denselben `Stammordner`

Es wird ein neues Popup-Fenster angezeigt

![Radarr-movie-editor-move-files-yes.png](/assets/radarr/Radarr-movie-editor-move-files-yes.png)

Wählen Sie `Ja, Dateien verschieben`

Dann Magie

![Radarr-correct-folder-name.png](/assets/radarr/Radarr-correct-folder-name.png)

Wie Sie sehen können, wurde der Ordner gemäß Ihrem Benennungsschema in das richtige Jahr umbenannt.

## Wie füge ich einen Film hinzu?

Nachdem Sie Ihre bereits gut organisierte Medienbibliothek importiert haben, ist es an der Zeit, die gewünschten Filme hinzuzufügen.

`Filme` => `Neu hinzufügen`

![Radarr-add-new.png](/assets/radarr/Radarr-add-new.png)

Geben Sie den gewünschten Film in das Feld ein oder verwenden Sie die tmdb:id oder imdb:id.

Wenn Sie den Filmtitel eingeben, werden Ihnen Ergebnisse angezeigt.

![Radarr-movie-search.png](/assets/radarr/Radarr-movie-search.png)

Wenn Sie den gewünschten Film sehen, klicken Sie darauf.

![Radarr-movie-add.png](/assets/radarr/Radarr-movie-add.png)

1. Stammordner - Radarr fügt den Film dem von Ihnen eingerichteten Stammordner hinzu [im Abschnitt zu den Stammordnern](#root-folders)
1. Überwachen - Wie der Film zu Radarr hinzugefügt werden soll.

- Nur Film = Radarr überwacht den RSS-Feed nach Filmen in Ihrer Bibliothek, die Sie noch nicht haben oder aktualisiert den vorhandenen Film auf eine bessere Qualität.
- Film & Sammlung = Radarr überwacht den RSS-Feed nach Filmen in Ihrer Bibliothek, die Sie noch nicht haben oder aktualisiert den vorhandenen Film auf eine bessere Qualität. Es fügt auch alle Filme in dieser Filmkollektion (falls vorhanden) mit Ihren ausgewählten Einstellungen hinzu.
- Keine = Radarr überwacht den RSS-Feed nicht, Upgrades oder neue Filme werden ignoriert und müssen manuell durchgeführt werden. Alle Suchen nach nicht überwachten Filmen müssen manuell ausgelöst oder interaktiv durchgeführt werden.

1. Verfügbarkeit - Wann Radarr einen Film als verfügbar betrachten soll.

> Weitere Informationen zu den Daten von TMDB, die die unten aufgeführten Verfügbarkeiten beeinflussen, finden Sie unter [Wie bestimmt Radarr das Jahr eines Films?](#how-does-radarr-determine-the-year-of-a-movie)
{.is-info}

- **Angekündigt**: Radarr betrachtet Filme als verfügbar, sobald sie zu Radarr hinzugefügt werden. Diese Einstellung wird empfohlen, wenn Sie gute private Tracker (oder wirklich gute öffentliche, z.B. rarbg.to) haben, die keine Fälschungen haben.
- **Im Kino**: Radarr betrachtet Filme als verfügbar, sobald sie in die Kinos kommen (Theatrical Date auf TMDb). Diese Option wird nicht empfohlen.
- **Veröffentlicht**: Radarr betrachtet Filme als verfügbar, sobald die Blu-Ray- oder Streaming-Version veröffentlicht wird (Digitale und physische Daten auf TMDb). Diese Option wird empfohlen und sollte wahrscheinlich mit einer Verfügbarkeitsverzögerung von `-14` oder `-21` Tagen kombiniert werden.
  - Wenn TMDb nicht mit einem Datum gefüllt ist, wird angenommen, dass der Film 90 Tage nach dem `Theatrical Date` (ältestes Datum im Kino) in Web- oder physischen Diensten verfügbar ist.

1. Qualitätsprofil - Wählen Sie Ihr Profil für diesen Film aus
1. Tags - Hier können Sie bestimmte Tags für erweiterte Verwendungszwecke hinzufügen.
1. Bei "Suche beim Hinzufügen" aktivieren, wenn Sie möchten, dass Radarr nach dem fehlenden Film sucht, wenn er zu Radarr hinzugefügt wird [weitere Informationen](/radarr/faq#how-does-radarr-find-movies)
1. Klicken Sie auf `Film hinzufügen`, um den Film zu Radarr hinzuzufügen.

- Wenn Sie einen Fehler "Pfad ist bereits konfiguriert" erhalten, [sehen Sie sich diesen FAQ-Eintrag an](/radarr/faq#path-is-already-configured-for-an-existing-movie)