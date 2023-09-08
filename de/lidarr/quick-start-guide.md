---
title: Lidarr Schnellstart
description: 
published: true
date: 2022-07-14T14:10:13.343Z
tags: 
editor: markdown
dateCreated: 2021-06-13T06:14:53.615Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Schnellstart-Setup-Anleitung](#schnellstart-setup-anleitung)
- [Einschränkungen](#einschränkungen)
- [Konzept](#konzept)
  - [Veröffentlichungen (Metadaten)](#veröffentlichungen-metadaten)
  - [Künstler (Metadaten)](#künstler-metadaten)
- [Erster Start](#erster-start)
- [Einstellungen](#einstellungen)
  - [Medienverwaltung](#medienverwaltung)
  - [Profile](#profile)
  - [Qualität](#qualität)
  - [Indexer](#indexer)
  - [Download-Clients](#download-clients)
    - [{.tabset}](#tabset)
      - [Usenet](#usenet)
      - [BitTorrent](#bittorrent)
- [Erster Künstler](#erster-künstler)
- [Erster Download/Import](#erster-downloadimport)
- [Schnellstart - Erweitert](#schnellstart-erweitert)
  - [Lidarr-Anwendungsfälle](#lidarr-anwendungsfälle)
    - [Lose Dateien](#lose-dateien)
    - [Spezialbibliotheken](#spezialbibliotheken)
  - [Importieren einer vorhandenen Bibliothek oder von Dateien](#importieren-einer-vorhandenen-bibliothek-oder-von-dateien)
    - [Vorbereitung Ihrer vorhandenen Dateien](#vorbereitung-ihrer-vorhandenen-dateien)
      - [Ordnerstruktur](#ordnerstruktur)
      - [Tagging](#tagging)
    - [Vor dem Import zu beachtende Punkte](#vor-dem-import-zu-beachtende-punkte)
    - [Import starten](#import-starten)

# Schnellstart-Setup-Anleitung

> Diese Seite ist noch in Bearbeitung und nicht vollständig. Beiträge sind willkommen.

> Für eine detailliertere Aufschlüsselung aller Einstellungen siehe [Lidarr => Einstellungen](/lidarr/settings)
{.is-info}

In dieser Anleitung werden wir versuchen, die grundlegende Einrichtung zu erklären, die Sie vornehmen müssen, um mit Lidarr zu beginnen. Wir werden einige Optionen überspringen, die Sie auf dem Bildschirm sehen können. Wenn Sie tiefer in diese Optionen eintauchen möchten, finden Sie auf der entsprechenden Seite in den FAQ und der Dokumentation eine vollständige Erklärung.

> Bitte beachten Sie, dass auf den Screenshots und in den GUI-Einstellungen in `orange` erweiterte Optionen angezeigt werden. Sie müssen daher oben auf der Seite auf `Erweitert anzeigen` klicken, um sie sichtbar zu machen.
{.is-warning}

# Einschränkungen

In dieser Anleitung werden die grundlegenden Schritte erläutert, um mit Lidarr zu arbeiten. Diese Anleitung setzt voraus, dass Sie die Anwendung bereits installiert haben. Installationsanweisungen finden Sie auf der folgenden Seite [Installation](/lidarr/installation). Wir konzentrieren uns auf die Minimaleinrichtung/-optionen, um eine funktionierende Konfiguration zu erhalten. Es gibt zusätzliche Einrichtung und Überlegungen, wenn eine der folgenden Situationen zutrifft:

- Vorhandene Bibliothek oder Dateien
- Falscher Anwendungsfall
- Falsche Ordnerstruktur
- Falsches oder extrem kompliziertes Tagging
- Lose Dateisammlung
- Spezialbasierte Musikbibliotheken: Klassik, Singles, Elektronik

Wenn eine der oben genannten Situationen zutrifft, lesen Sie bitte den Abschnitt Schnellstart - Erweitert.

Diese Anleitung ist in Abschnitte unterteilt. Es wird empfohlen, die gesamte Anleitung zu lesen, um ein vollständiges Verständnis zu haben, aber Sie können zu bestimmten Abschnitten springen, wenn Sie sofortige Fragen haben. Verwenden Sie das Inhaltsverzeichnis links, um schnell zu springen.

# Konzept

Um Lidarr ordnungsgemäß zu verwenden, müssen die zugrunde liegenden Konzepte verstanden werden. Auf einer hohen Ebene folgt es den Prinzipien der anderen Arr-Anwendungen. Lidarr fungiert als Musikbibliotheksverwaltungssystem, Datenaggregator und Automatisierungsplattform zum Auffinden und Herunterladen von Medien.

Von dort abweichend ist der Unterschied ziemlich groß. Die Verwaltung einer Musikbibliothek ist ein sehr komplizierter Prozess, da es viele konkurrierende Variablen gibt, die den Prozess behindern. Im Gegensatz zur Verwaltung von Filmen oder TV-Shows gibt es keine einheitlichen Standards für das Tagging, die Benennung oder die Speicherung von Musik. Dies wurde durch die sich ändernden Methoden der Musikverteilung von physischen Medien zu elektronischen Medien weiter kompliziert. Schließlich sind die Meinungen darüber, wie diese Verwaltung gehandhabt werden soll, weit verbreitet und vielfältig.

Lidarr verwendet Informationen von Datenaggregationsdiensten, um die Musikbibliothek ordnungsgemäß zu taggen und zu verwalten. Diese Daten von Drittanbietern repräsentieren Medien in definierten Kategorien und Typen.

> Wenn die Daten nicht in den Drittanbieterdiensten vorhanden sind, können sie NICHT von Lidarr verwaltet werden.
Weitere Informationen zur Teilnahme und Beitrag finden Sie unten.
{.is-warning}

Der Hauptdienst, der genutzt wird, ist [MusicBrainz](https://musicbrainz.org/). Dies ist ein kostenloser Dienst, der von der Community getragen wird und letztendlich von Ihren Beiträgen und Ihrer Teilnahme abhängt und überlebt. Die Erstellung und Beitrag von Veröffentlichungen ist nicht Gegenstand dieser Anleitung. Anweisungen finden Sie hier: [Wie man beiträgt](https://musicbrainz.org/doc/How_to_Contribute)

Letztendlich wird die Datenqualität durch die Standards der Drittanbieterdaten definiert. Wenn die Standards nicht mit Ihrem Anwendungsfall übereinstimmen, ist **Lidarr möglicherweise nicht die richtige Lösung**. Andere Anwendungen zur Verwaltung Ihrer Medien können Folgendes umfassen:

[Beets Media Management](https://beets.io/)
[MusicBrainz Picard](https://picard.musicbrainz.org/)
[Music Bee](https://getmusicbee.com/)

Diese Implementierungen können zusammen mit Lidarr verwendet werden, dies fällt jedoch nicht in den Rahmen dieser Anleitung.

## Veröffentlichungen (Metadaten)

Lidarr hat den Standard `Veröffentlichung` für die Verwaltung von Musikmedien ausgewählt. Das bedeutet, dass für das System ordnungsgemäß funktioniert, müssen alle vom System verarbeiteten Medien eine `Veröffentlichung` sein.

Beispiele für Veröffentlichungen:

- Album
- EP
- Single
- Rundfunk

Jedes zu verwaltende Element muss eine entsprechende `Veröffentlichung` im Drittanbieterdatendienst haben.

> `Veröffentlichungen` müssen in den Drittanbieterdiensten vorhanden sein, um von Lidarr verwaltet zu werden.

## Künstler (Metadaten)

Künstler sind genau das, was man als `Veröffentlichungskünstler` erwarten würde. Leider haben Namensgebung, Stiländerungen im Laufe der Zeit, Benutzervorlieben und andere Gründe verwirrt, was diesen `Veröffentlichungskünstler` ausmacht.

Beispiele für korrekte und inkorrekte "Künstler":

- Bob Dylan
- BOB DYLAN
- The Bob Dylan
- Bob Dylan, The
- Bob Dylan & the Band
- Bob Dylan feat. The Band
- The Band featuring Bob Dylan
- ...

Diese Liste könnte endlos fortgesetzt werden. Nochmals, alle `Veröffentlichungen` sind mit einem `Künstler` korreliert. Sie müssen den richtigen `Künstler` finden (Schritte später in dieser Anleitung) und verwenden, um eine `Veröffentlichung` herunterzuladen.

> `Veröffentlichungskünstler` müssen in den Drittanbieterdiensten vorhanden sein, um von Lidarr verwaltet zu werden.

# Erster Start

Nach der Installation und dem Starten von Lidarr greifen Sie darauf zu, indem Sie einen Browser öffnen und zu `http://{Ihre_IP_hier}:8686` gehen

![lidarr_qs_startup.png](/assets/lidarr/quick-start-guide/lidarr_qs_startup.png)

Auf dem Startbildschirm werden zwei Optionen angezeigt, die wir jedoch zunächst nicht verwenden werden.

# Einstellungen

Wir werden die Standardeinstellungen verwenden, um Lidarr zu konfigurieren. Dadurch werden die vorhandenen Profile, Qualitäten, Tags usw. verwendet.

> Für eine detailliertere Aufschlüsselung aller Einstellungen siehe [Lidarr > Einstellungen](/lidarr/settings)
{.is-info}

## Medienverwaltung

Zuerst werfen wir einen Blick auf die `Medienverwaltung`, wo wir den `Stammordner` festlegen werden. Dies ist der Speicherort, an dem die Mediendateien gespeichert werden.

> Speichern Sie Lidarr-Medien nicht bei einem Cloud-Speicheranbieter! Aufgrund der Art und Weise, wie Lidarr Tags verwendet, werden dadurch alle API-Limits überschritten und es treten Probleme auf. Bewahren Sie Ihre Bibliothek in Ihrem Netzwerk auf.
{.is-warning}

Klicken Sie auf `Einstellungen` > `Medienverwaltung` im linken Menü.

![lidarr_qs_mediamanagement.png](/assets/lidarr/quick-start-guide/lidarr_qs_mediamanagement.png)

Klicken Sie auf `Hinzufügen (+)` der `Stammordner`.

Es wird ein neues Fenster angezeigt:

![lidarr_qs_rootfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_rootfolder.png)

- **Name** - Dies ist der `Freundliche Name` des Speicherorts.
- **Pfad** - Dies ist der tatsächliche `Pfad` zum Speicherort der Daten. Das System/der Benutzer muss die entsprechenden Berechtigungen für diesen Speicherpfad haben. Dieser Ordner darf nicht Ihr Download-Speicherort sein!

Lassen Sie die anderen Optionen auf ihren Standardwerten.

> Wenn Sie einen `Stammordner` mit vorhandenen Dateien verwenden. Lesen Sie den Abschnitt Schnellstart - Erweitert für weitere Überlegungen.
{.is-warning}

> \* Nicht-Windows: Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
> \* Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.
{.is-warning}

> **Der Benutzer und die Gruppe, für die Sie Lidarr konfiguriert haben, müssen Lese- und Schreibzugriff auf diesen Speicherort haben.** {.is-info}

> Ihr Download-Client lädt in einen Download-Ordner herunter und Lidarr importiert ihn in Ihren Medienordner (Zielort), den Ihr Medienserver verwendet.
{.is-info}

> **Ihr Download-Ordner und Ihr Medienordner können nicht der gleiche Speicherort sein**
{.is-danger}

## Profile

`Einstellungen` > `Profile`

Die Profileinstellungen bleiben auf ihren Standardwerten.

## Qualität

`Einstellungen` > `Qualität`

Die Qualitätseinstellungen bleiben auf ihren Standardwerten.

## Indexer

`Einstellungen` > `Indexer`

In diesem Abschnitt werden die Indexer/Tracker festgelegt, die Sie zum Auffinden von herunterladbaren Mediendateien verwenden werden.

Klicken Sie auf `Hinzufügen (+)` von `Indexer`. Es wird ein neues Fenster mit vielen verschiedenen Optionen angezeigt. Lidarr betrachtet sowohl Usenet-Indexer als auch BitTorrent-Tracker als `Indexer`.

Fügen Sie mindestens einen `Indexer` hinzu, damit Lidarr verfügbare Dateien ordnungsgemäß finden kann.

Das Verständnis der Konfiguration/Konzepte hinter `Indexern` liegt außerhalb des Rahmens dieser Anleitung. Das Internet bietet eine Fülle von Informationen zu diesem Thema.

## Download-Clients

`Einstellungen` => `Download-Clients`

![Lidarr-settings-download-clients.png](/assets/lidarr/Lidarr-settings-download-clients.png)

Das Herunterladen und Importieren ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss die Software in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Setups. Das bedeutet, dass es zwar einige gemeinsame Setups gibt, aber kein einziges richtiges Setup und jedes Setup ein wenig anders sein kann. Es gibt jedoch viele falsche Setups.

> Weitere Informationen finden Sie auf der [Einstellungsseite](/lidarr/settings#download-clients), auf der Seite [Weitere Informationen (Unterstützt)](/lidarr/supported#download-clients) für diesen Abschnitt und in [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/).
{.is-info}

### {.tabset}

#### Usenet

{#usenet}

- Lidarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Lidarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Lidarr den endgültigen Dateispeicherort, wie er von Ihrem Download-Client gemeldet wird. Dieser Dateispeicherort kann sich fast überall befinden, solange er sich an einem separaten Ort von Ihrem Medienordner befindet und von Lidarr zugänglich ist.
- Lidarr durchsucht diesen abgeschlossenen Dateispeicherort nach Dateien, die Lidarr verwenden kann. Es analysiert den Dateinamen, um ihn mit den angeforderten Medien abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie an den angegebenen Medienort.
- Atomare Verschiebungen (sofortige Verschiebungen) sind standardmäßig aktiviert. Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die atomare Verschiebung fehlschlägt oder Ihr Setup keine Hardlinks und atomare Verschiebungen unterstützt, wird Lidarr auf die Kopie der Datei zurückgreifen und sie dann aus der Quelle löschen, was eine hohe IO-Auslastung verursacht.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Lidarr-Einstellungen aktiviert ist, werden übrig gebliebene Dateien aus dem Download über eine Anforderung an Ihren Client in den Papierkorb oder das Recycling verschoben/gelöscht.

#### BitTorrent

{#bittorrent}

- Lidarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Lidarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
- Abgeschlossene Dateien bleiben an ihrem ursprünglichen Speicherort, damit Sie die Datei seeden können (Verhältnis oder Zeit kann im Download-Client oder innerhalb von Lidarr unter dem spezifischen Download-Client angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, erstellt Lidarr einen Hardlink zur Datei, sofern von Ihrem Setup unterstützt, oder kopiert sie, wenn keine Hardlinks unterstützt werden.
- Hardlinks sind standardmäßig aktiviert. [Ein Hardlink erfordert keinen zusätzlichen Festplattenspeicher.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihr Setup keine Hardlinks unterstützt, wird Lidarr auf die Kopie der Datei zurückgreifen.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Lidarr-Einstellungen aktiviert ist, löscht Lidarr den Torrent aus Ihrem Client und bittet den Client, die Torrent-Daten zu entfernen, aber nur, wenn der Client meldet, dass das Seeding abgeschlossen ist und der Torrent gestoppt ist (nach Abschluss pausiert).

# Erster Künstler

Wenn Sie dieser Anleitung folgen und Ihr `Stammordner` keine Mediendateien enthält, müssen Sie einen `Künstler` hinzufügen.

`Bibliothek` > `Neu hinzufügen`

![lidarr_qs_addnew.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnew.png)

Dies führt zu dem Suchbildschirm, um einen Künstler zu finden. Suchen und wählen Sie den `Künstler` aus, den Sie hinzufügen möchten. Dadurch wird das Fenster "Neuen Künstler hinzufügen" geöffnet.

![lidarr_qs_addnewdylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_addnewdylan.png)

Wir werden die Standardeinstellungen verwenden. Diese sollten Folgendes beinhalten:

- Stammordner - Der von Ihnen erstellte Ordner
- Überwachung - Keine
- Qualitätsprofil - Beliebig
- Tags - (leer)
- Suche nach fehlenden Alben starten - Nicht aktiviert

Dies startet den Download der `Künstler`-Metadaten. Dies dauert je nach Menge der zu sammelnden Daten einige Zeit. Denken Sie daran, dass diese Informationen von Drittanbieterquellen stammen und nur so vollständig sind wie das, was die Community beigetragen hat.

Klicken Sie auf den neu hinzugefügten `Künstler`. (In diesem Beispiel Bob Dylan)

> Das Standard-Metadatenprofil wird verwendet, es werden nur `Veröffentlichungen` des Typs `Studioalben` angezeigt.

![lidarr_qs_dylan.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylan.png)

> Gefällt Ihnen die heruntergeladene Metadaten nicht? - Tragen Sie dazu bei, sie zu verbessern!
{.is-info}

# Erster Download/Import

Endlich ist es Zeit, Ihre erste `Veröffentlichung` herunterzuladen/importieren!

Finden Sie die `Veröffentlichung`, die Sie Ihrer Bibliothek hinzufügen möchten. Wählen Sie das Symbol für die manuelle Suche (menschliches Symbol) neben der Veröffentlichung aus.

![lidarr_qs_dylanrelease.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanrelease.png)

Dies öffnet das Fenster zur Auswahl der `Veröffentlichung`. In diesem Fenster werden die Ergebnisse der `Indexer`-Abfrage oder einfach gesagt die Suchergebnisse für verfügbare Downloads angezeigt.

> Das Standard-Qualitätsprofil erlaubt jeden Dateityp. Das Standard-Veröffentlichungsprofil erlaubt alle Downloads. Für eine detaillierte Aufschlüsselung dieser erweiterten Einstellungen siehe [Lidarr > Einstellungen](/lidarr/settings)

![lidarr_qs_dylandownload.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylandownload.png)

Überprüfen Sie das Download-Fenster auf die verschiedenen bereitgestellten Informationen:

1. Titel - Dies ist der Name des Downloads, wie er vom `Indexer` zurückgegeben wird.
1. Qualität - Dies ist die Qualität, wie sie von Lidarr anhand des Titels bestimmt wird.
1. Die Warnhinweise geben eine Beschreibung, warum der Download die Lidarr-Prüfungen nicht bestanden hat. Im Beispiel wurde "Falsches Album" angezeigt.

Wenn Sie dies überprüft haben, wählen Sie das Download-Symbol (Nummer 4), um die verfügbare `Veröffentlichung` herunterzuladen.

Wenn alles richtig konfiguriert ist, wird der Download an Ihren `Download-Client` gesendet.

Der Download wird zur `Warteschlange` hinzugefügt und durchläuft die verschiedenen Zustände Ihres Download-Clients.

Schließlich wird der Download in Ihren `Stammordner` importiert. Wenn alles erfolgreich ist, sollte er wie unten angezeigt erscheinen.

![lidarr_qs_dylansucess.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylansuccess.png)

Sie finden Ihre heruntergeladenen Dateien in Ihrem `Stammordner` und können sie mit Ihrem bevorzugten Media Player wiedergeben.

![lidarr_qs_dylanfolder.png](/assets/lidarr/quick-start-guide/lidarr_qs_dylanfolder.png)

# Schnellstart - Fortgeschritten

Dieser fortgeschrittene Abschnitt richtet sich an Setups, die möglicherweise besondere Überlegungen erfordern. Überprüfen Sie, ob diese auf Ihre Konfiguration zutreffen, und sparen Sie möglicherweise einige Kopfschmerzen.

> Die folgenden Abschnitte helfen bei häufig auftretenden Problemen und Schwierigkeiten.
{.is-warning}

## Verwendungszweck von Lidarr

Wie bereits im Abschnitt Konzept erwähnt, sollte Lidarr nicht verwendet werden, wenn Ihr beabsichtigter Verwendungszweck nicht mit dem Verwaltungssystem von Lidarr für `Releases` übereinstimmt. Lidarr funktioniert NICHT mit den folgenden Verwendungszwecken:

- Lose Sammlung von Dateien - Dateien von verschiedenen Künstlern (keine Zusammenstellungen) oder mehreren `Releases`
- Spezialisierte Musikbibliotheken: Klassik, Singles, Elektronik

### Lose Dateien

Eine geringe bis keine Kuration von losen Dateien funktioniert nicht mit Lidarr. Es ist am besten, diese Dateien nicht mit Lidarr zu verwenden.

### Spezialisierte Bibliotheken

Spezialisierte Bibliotheken stellen für jedes Verwaltungssystem einzigartige Probleme dar. Diese Situationen können mit Lidarr funktionieren, erfordern jedoch möglicherweise umfangreiche Arbeit Ihrerseits und verzichten weitgehend auf die integrierten Automatisierungen. Zum Beispiel:

- **Klassische Musik** - Erfordert normalerweise umfangreiche Tagging-Anforderungen oder -Wünsche. Metadaten zu `Releases` werden wahrscheinlich nicht vorhanden sein oder falsch sein.
- **Singles** - Singles sind möglicherweise keine tatsächlichen `Releases`. Daten von Drittanbieter-Diensten liefern keine Metadaten. Sie werden nicht automatisiert und Lidarr kann keine Verwaltung anwenden.
- **Elektronik** - Dies gilt NICHT für `Releases` im Genre Elektronik. Dies bezieht sich auf Bibliotheken von Mixes, Beats, Samples usw. (Beatport). Datenquellen von Drittanbietern erkennen diese nicht als `Releases` an. Sie werden nicht automatisiert und Lidarr kann keine Verwaltung anwenden.

## Importieren einer vorhandenen Bibliothek oder von Dateien

> Beachten Sie, dass Lidarr nicht regelmäßig nach `Releases` sucht. Lesen Sie diese beiden FAQ-Einträge, um zu verstehen, wie Lidarr funktioniert.
[Wie findet Lidarr `Releases`?](/lidarr/faq#how-does-lidarr-find-releases) und [Wie funktioniert Lidarr?](/lidarr/faq#how-does-lidarr-work)
{.is-info}

> Der automatisierte Import ist ein geplanter Vorgang und kann nicht gestoppt werden.
Fügen Sie KEIN `Root-Verzeichnis` mit vorhandenen Dateien hinzu, bis Sie diesen Abschnitt vollständig durchgelesen haben.
{.is-warning}

Lidarr verwendet ein automatisiertes System zum Hinzufügen von `Release Artists` und `Releases`, die sich in Ihrem `Root-Verzeichnis` befinden.

Wenn der Verwendungszweck von Lidarr übereinstimmt und Sie keine einzigartigen oder spezialisierten Bibliotheken haben, können Sie mit dem Importieren Ihrer vorhandenen Bibliothek fortfahren.

Es ist wichtig, dass Ihre vorhandenen Bibliotheksdateien strukturiert sind und dem Verwaltungssystem von Lidarr für `Releases` folgen. Dies bedeutet, dass Folgendes nicht funktioniert:

- Falsche Ordnerstruktur - Dateien befinden sich in einem einzigen Ordner - Beachten Sie den Abschnitt Vorbereitung>Ordnerstruktur
- Falsches oder extrem kompliziertes Tagging - Beachten Sie den Abschnitt Vorbereitung>Tagging

### Vorbereitung Ihrer vorhandenen Dateien

Damit der automatisierte Prozess funktioniert, müssen Ihre Dateien vorbereitet werden, um sicherzustellen, dass dies effizient oder überhaupt funktioniert.

#### Ordnerstruktur

Es wird empfohlen, der Standardordnerstruktur zu folgen:

\Root-Verzeichnis\Release Artist\Release\XX - Track

In Kombination mit den richtigen Tags ermöglicht dies eine Erkennung von fast 95% oder mehr durch Media-Player.

#### Tagging

Das Tagging kann ein komplizierter Vorgang sein. Die Anzahl der Dateien und wie sie derzeit getaggt sind, bestimmen den Aufwand, der erforderlich ist.

Die empfohlenen Methoden zum Taggen Ihrer Dateien sind:

- MusicBrainz Picard
- Beets
- MusicBee, MediaMonkey, JRiver

Die Verwendung dieser Anwendungen fällt nicht in den Rahmen dieses Leitfadens, aber es ist ratsam, MusicBrainz Release ID's als Teil des Tagging-Prozesses zu verwenden.

> Die meisten Tagging-Software kann Ordnerstruktur und Umbenennung durchführen und dabei Dateien ordnungsgemäß taggen.
{.is-info}

### Vor dem Import zu beachtende Punkte

Sobald die Dateien ordnungsgemäß getaggt und benannt sind, sollten die folgenden Punkte überprüft werden, um sicherzustellen, dass der Importvorgang erfolgreich abgeschlossen wird:

- **Systemarchitektur** - Empfohlen x64 / 64 Bit - Der Import großer Bibliotheken erfordert, dass das System auf große Mengen an RAM zugreift und effizienter berechnet. x86 / 32 Bit wird unterstützt, ist jedoch nicht so effizient und dauert wesentlich länger.
- **Systemanforderungen für den Arbeitsspeicher (RAM)** - Mindestens 4 GB, empfohlen 8 GB - Der Importprozess erfordert viel Arbeitsspeicher, und wenn Lidarr importiert und ein Browser geöffnet ist, wird eine erhebliche Menge an RAM verwendet.
- **Grenzen für `Release`-Discs/Tracks** - `Releases`, die eine große Anzahl von Tracks oder Discs haben, sollten aus dem Importprozess entfernt werden. Sie können manuell importiert werden, indem Sie die integrierten Verfahren verwenden. Es gibt keine genaue Grenze, aber um sicher zu gehen, sollten Releases mit mehr als 25 Discs oder 250 Tracks entfernt werden.
- **`Release Artist` mit vielen `Releases`** - Der automatisierte Prozess von Lidarr vergleicht `Releases` mit Ihren Dateien. Obwohl es unwahrscheinlich ist, dass dies fehlschlägt, führt das Durchlaufen dieser Dateien durch das automatisierte Verfahren zu einer erheblichen Verlängerung der Importzeit. Es gibt einzelne Künstler mit Tausenden von `Releases`.
- **Zeit** - Der automatisierte Importvorgang dauert seine Zeit. Eine vernünftige Schätzung wäre 1 Stunde für 500 ordnungsgemäß getaggte `Releases`. Dies ist stark variabel abhängig von Ihrem Speicher, Ihrer Internetgeschwindigkeit und der Systemleistung.

### Import starten

//

Demnächst verfügbar

- Überwachen * - Hiermit wird die Standardüberwachungsoption (`Releases`) für das `Root-Verzeichnis` festgelegt.
- Qualitätsprofil * - Hiermit wird die Standardqualitätsoption für das `Root-Verzeichnis` festgelegt.
- Metadatenprofil * - Hiermit wird die Standardmetadatenoption für das `Root-Verzeichnis` festgelegt.