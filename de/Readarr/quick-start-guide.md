---
title: Readarr Schnellstart-Anleitung
description: 
published: true
date: 2022-09-07T23:19:05.590Z
tags: readarr
editor: markdown
dateCreated: 2021-12-11T19:42:31.825Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Schnellstart-Setup-Anleitung](#schnellstart-setup-anleitung)
- [Starten](#starten)
- [Medienverwaltung](#medienverwaltung)
- [Buchbenennung](#buchbenennung)
- [Ordner](#ordner)
- [Importieren](#importieren)
- [Dateiverwaltung](#dateiverwaltung)
- [Stammordner und Calibre-Integration](#stammordner-und-calibre-integration)
  - [Calibre Content Server (Optional)](#calibre-content-server-optional)
  - [Calibre-Integration](#calibre-integration)
- [Download-Clients](#download-clients)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [So importieren Sie Ihre vorhandene organisierte Medienbibliothek](#so-importieren-sie-ihre-vorhandene-organisierte-medienbibliothek)
  - [Importieren vorhandener Medien](#importieren-vorhandener-medien)
- [Neue Bücher hinzufügen](#neue-bücher-hinzufügen)

# Schnellstart-Setup-Anleitung

> Diese Seite ist noch in Bearbeitung und nicht vollständig. Beiträge sind willkommen.

> Für eine detailliertere Aufschlüsselung aller Einstellungen siehe [Readarr => Einstellungen](/readarr/settings)
{.is-info}

In dieser Anleitung erklären wir die grundlegende Einrichtung, die Sie vornehmen müssen, um mit Readarr zu beginnen. Wir werden einige Optionen überspringen, die Sie auf dem Bildschirm sehen können. Wenn Sie tiefer in diese Optionen eintauchen möchten, finden Sie eine ausführliche Erklärung auf der entsprechenden Seite in den FAQ und der Dokumentation.

> Bitte beachten Sie, dass in den Screenshots und GUI-Einstellungen in `orange` erweiterte Optionen angezeigt werden. Sie müssen oben auf der Seite auf `Erweitert anzeigen` klicken, um sie sichtbar zu machen.
{.is-warning}

# Starten

Nach der Installation und dem Starten öffnen Sie einen Browser und gehen zu `http://{your_ip_here}:8787`

![qs_startup.png](/assets/readarr/qs_startup.png)

# Medienverwaltung

Zuerst werfen wir einen Blick auf die Einstellungen für die `Medienverwaltung`, in denen wir unsere bevorzugten Benennungs- und Dateiverwaltungseinstellungen festlegen können.

`Einstellungen` => `Medienverwaltung`

![mediamanagement.png](/assets/readarr/mediamanagement.png)

# Buchbenennung

![booknaming.png](/assets/readarr/booknaming.png)

- Aktivieren/Deaktivieren Sie die Umbenennung Ihrer Bücher (anstatt die Namen beizubehalten, die sie derzeit haben oder als Sie sie heruntergeladen haben).
- Wenn Sie unzulässige Zeichen ersetzen oder entfernen möchten (`\ / : * ? " < > | ~ - % & + { }`).
- Hier wählen Sie die Benennungskonvention für die tatsächlichen Buchdateien aus. Beachten Sie, dass der Buchordnername hier ebenfalls definiert ist.
- `(Erweiterte Option) Hier legen Sie die Benennungskonvention für den Autorenordner fest.`

> Dies gilt nicht, wenn Calibre verwendet wird, da Calibre die Datei-/Ordnerbenennung mit seinem eigenen internen Schema behandelt.
{.is-info}

# Ordner

![folders.png](/assets/readarr/folders.png)

- (Erweiterte Option) Leere Autorenordner erstellen - Aktivieren Sie diese Option, um leere Autorenordner zu erstellen, wenn ein neuer Autor zu Readarr hinzugefügt wird.
- (Erweiterte Option) Leere Ordner löschen - Aktivieren Sie diese Option, um leere Autorenordner zu löschen, wenn keine Bücher mehr für diesen Autor vorhanden sind.

> Eine dieser Optionen kann ausgewählt werden, aber beide sollten NICHT ausgewählt sein.
{.is-warning}

> Dies gilt nicht, wenn Calibre verwendet wird, da Calibre die Datei-/Ordnerbenennung mit seinem eigenen internen Schema behandelt.
{.is-info}

# Importieren

![importing.png](/assets/readarr/importing.png)

- (Erweiterte Option) Überprüfung des freien Speicherplatzes überspringen - Wenn aktiviert, wird vor dem Importieren der freie Speicherplatz nicht überprüft.
- (Erweiterte Option) Mindestens freier Speicherplatz - Geben Sie den minimalen freien Speicherplatz für das Laufwerk ein, bevor der Importvorgang abgebrochen wird.
- (Erweiterte Option) Verwenden von Hardlinks anstelle von Kopien - Aktivieren Sie dieses Kontrollkästchen, um Hardlinks anstelle von Kopien zu verwenden (für Torrents). Beachten Sie, dass dies standardmäßig aktiviert ist.
  
> Sie sollten dies idealerweise immer verwenden. Damit Hardlinks verwendet werden können, müssen Quelle und Ziel auf demselben Dateisystem (Laufwerk, Partition) und den gleichen Einhängepunkten liegen. [Weitere Informationen finden Sie in TRaSH's Hardlink Guide](https://trash-guides.info/hardlinks/)
{.is-info}
  
- Zusätzliche Dateien importieren - Wenn aktiviert, werden angegebene zusätzliche Dateien importiert, die sich im Ordner des Buches befinden, wenn es importiert wird.
- (Erweiterte Option) Zusätzliche Dateien importieren - Wenn "Zusätzliche Dateien importieren" aktiviert ist, geben Sie eine durch Kommas getrennte Liste von Erweiterungen ein, die importiert werden sollen.

> Wenn Sie Readarr für Hörbücher verwenden, sollten Sie .cue zu dieser Liste hinzufügen, da es Ihre Kapitelinformationen enthält!
{.is-info}

# Dateiverwaltung

![filemanagement.png](/assets/readarr/filemanagement.png)

- Bücher, die von der Festplatte gelöscht wurden, werden automatisch in Readarr nicht mehr überwacht.

- Gelöschte Bücher ignorieren - Aktivieren Sie dieses Kontrollkästchen, um Bücher, die als gelöscht oder nicht zugänglich erkannt wurden, nicht mehr im Stammordner von Readarr zu überwachen.
- Richtiges Herunterladen & Repacks - Ob automatisch auf Richtiges/Repacks aktualisiert werden soll oder nicht. Verwenden Sie `Nicht bevorzugen`, um nach bevorzugten Wortbewertungen vor Repacks/Repacks zu sortieren.
  - Bevorzugen und Aktualisieren - Repacks und Propers höher bewerten als Nicht-Repacks und Nicht-Propers. Neue Repacks und Propers als Upgrade für aktuelle Veröffentlichungen behandeln.
  - Nicht automatisch aktualisieren - Repacks und Propers höher bewerten als Nicht-Repacks und Nicht-Propers. Neue Repacks und Propers nicht als Upgrade für aktuelle Veröffentlichungen behandeln.
  - Nicht bevorzugen - Repacks und Propers effektiv ignorieren. Sie müssen alle Präferenzen für diese mit [Bevorzugten Wörtern](#release-profiles) verwalten.

> \* `PROPER` - bedeutet, dass es ein Problem mit der vorherigen Veröffentlichung gab. Downloads, die als PROPER gekennzeichnet sind, zeigen an, dass die Probleme in dieser Veröffentlichung behoben wurden. Dies wird von einer Gruppe durchgeführt, die die Originalversion nicht veröffentlicht hat.
> \* `REPACK` - bedeutet, dass es ein Problem mit der vorherigen Veröffentlichung gab und dass es von der Originalgruppe behoben wurde. Downloads, die als REPACK gekennzeichnet sind, zeigen an, dass die Probleme in dieser Veröffentlichung behoben wurden. Dies wird von einer Gruppe durchgeführt, die die Originalversion veröffentlicht hat.
{.is-info}

- (Erweiterte Option) Stammordner auf Dateiänderungen überwachen - Aktivieren Sie dieses Kontrollkästchen, um einen erneuten Scan auszulösen, wenn festgestellt wird, dass sich im Stammordner Änderungen ergeben haben.
- (Erweiterte Option) Autorordner nach Aktualisierung erneut scannen - Wählen Sie aus, wann ein Autorordner nach Aktualisierung des Autors erneut gescannt werden soll.
  - Immer - Dies führt basierend auf dem Aufgabenplan einen erneuten Scan der Autorenordner durch.
  - Nach manueller Aktualisierung - Sie müssen den Datenträger manuell erneut scannen.
  - Nie - Wie der Name schon sagt, die Autorordner nie erneut scannen.
- (Erweiterte Option) Fingerprinting zulassen - Wählen Sie aus, wie Fingerprinting behandelt werden soll, um eine genauere Buchzuordnung zu ermöglichen, jedoch auf Kosten von CPU- und Festplattenzeit.
  - Immer - Fingerprinting immer verwenden, wenn möglich
  - Nur für neue Importe - Nur neu importierte Veröffentlichungen fingerprinten
  - Nie - Wie der Name schon sagt, Fingerprinting nie verwenden
- (Erweiterte Option) Dateidatum ändern - Dateidatum beim Importieren/Erneuten Scannen ändern
  - Keine - Readarr ändert das Datum nicht, das in Ihrem Dateibrowser angezeigt wird
  - Buchveröffentlichungsdatum - Das Datum, an dem das Buch veröffentlicht wurde.
- (Erweiterte Option) Papierkorb - Buchdateien werden hierhin verschoben, wenn sie gelöscht werden, anstatt dauerhaft gelöscht zu werden
- (Erweiterte Option) Papierkorb bereinigen - Wie alt eine bestimmte Datei sein kann, bevor sie dauerhaft gelöscht wird

> Es wird dringend empfohlen, einen Papierkorb zu verwenden. Es ist einfach, Dateien zu löschen, und wenn Sie den Papierkorb verwenden, ist die Wiederherstellung einfach.
{.is-warning}

# Stammordner und Calibre-Integration

![rootfolders1.png](/assets/readarr/rootfolders1.png)

Hier fügen wir den Stammordner hinzu, den Readarr zum Importieren Ihrer vorhandenen organisierten Medienbibliothek verwenden wird, und wohin Readarr Ihre Medien nach dem Herunterladen durch Ihren Download-Client importieren wird (Kopieren/Hardlink/Verschieben).

> **Der Benutzer und die Gruppe, die Sie für Readarr konfiguriert haben, müssen Lese- und Schreibzugriff auf diesen Speicherort haben.** {.is-info}

Sie können auch wählen, Calibre zur Verwaltung Ihrer Bibliothek auf diesem Bildschirm zu verwenden. Dazu müssen Sie den Calibre Content Server ausführen. Dies ist NICHT Calibre-Web.

> Benutzer von Nicht-Windows-Systemen:
> \* Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
> \* Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.
{.is-warning}

> Wenn Sie Calibre verwenden möchten, müssen die Bücher, die Sie von Readarr bei der ersten Bibliotheksimportierung erkennen lassen möchten, **bereits in Calibre vorhanden sein**. Bücher im Ordner, die nicht in Calibre sind, werden ignoriert. Hardlinks werden nicht verwendet, wenn Calibre-Integration hinzugefügt wird.
> **Beachten Sie, dass Sie Calibre-Integration nicht zu einem Stammordner hinzufügen können, nachdem er erstellt wurde.**
{.is-danger}

> Ihr Download-Client lädt in einen Download-Ordner herunter, und Readarr importiert ihn in Ihren Medienordner (endgültiges Ziel), den Ihr Medienserver verwendet. Ihr Download-Ordner und Ihr Medienordner können nicht der gleiche Speicherort sein!
{.is-warning}

Vergessen Sie nicht, Ihre Änderungen zu speichern.

## Calibre Content Server (Optional)

Wenn Sie Calibre zur Verwaltung Ihrer Bücher verwenden möchten, müssen Sie den Calibre Content Server einrichten. Auch hier handelt es sich nicht um Calibre-Web, sondern um einen Bestandteil von Calibre selbst. Sie müssen Calibre ausführen und den Content Server einrichten.

> Wenn Sie sich für die Verwendung von Calibre entscheiden, können Sie nichts in der Calibre-Datenbank ändern. Wenn Sie diese Warnung nicht beachten, müssen Sie Ihre Readarr-Datenbank löschen und von vorne beginnen.
{.is-danger}

Wenn Sie Docker verwenden, müssen Ihr Calibre-Buchverzeichnis und Ihr Readarr-Buchverzeichnis identisch sein.

> Bitte beachten Sie, dass während Readarr sich in der Beta-Phase befindet, wenn Sie Calibre verwenden, wird empfohlen, die Umbenennung in Readarr zu deaktivieren, nur für den Fall, dass ein unbeabsichtigter Fehler durchrutscht.
{.is-info}

Öffnen Sie dazu Calibre und klicken Sie auf `Einstellungen / Über das Netzwerk freigeben`

![calibreprefs.png](/assets/readarr/calibreprefs.png)

Fügen Sie zunächst ein Benutzerkonto hinzu. Das Konto benötigt Zugriff zum "Änderungen vornehmen".

![calibreacct.png](/assets/readarr/calibreacct.png)

Dann müssen Sie Calibre neu starten. Nach dem Neustart konfigurieren und starten Sie den Content Server. Es sollte Ihnen anzeigen, dass er läuft. Stellen Sie ihn so ein, dass er beim Start automatisch ausgeführt wird. Nach dem Speichern müssen Sie Calibre erneut neu starten. Stellen Sie sicher, dass der Server gestartet ist, wenn er wieder hochfährt, und gehen Sie dann zum nächsten Abschnitt über.

> Sie müssen "Benutzername und Passwort erforderlich, um auf den Content-Server zuzugreifen" auswählen, damit Readarr ordnungsgemäß funktioniert. Andernfalls erhalten Sie einen Fehler, der besagt "Anonyme Benutzer dürfen keine Änderungen vornehmen", wenn Readarr ein Buch importiert!
{.is-info}

![calibreserver.png](/assets/readarr/calibreserver.png)

## Calibre-Integration

![calibre1.png](/assets/readarr/calibre1.png)

Die folgenden Einstellungen sind spezifisch für Calibre und werden nur angezeigt, wenn `Calibre verwenden` aktiviert ist.

- Calibre verwenden - Aktivieren/Deaktivieren Sie die Verwendung des Calibre Content Server zur Verwaltung Ihres Stammordners.

> \* Beachten Sie, dass dies **nicht für einen vorhandenen Stammordner aktiviert werden kann**.
> \* Beachten Sie, dass dies **für einen vorhandenen Calibre-aktivierten Stammordner nicht deaktiviert werden kann**.
> \* Beachten Sie, dass hierfür der **Calibre Content Server** erforderlich ist und nicht mit Calibre Web oder Calibre funktioniert.
> \* Beachten Sie, dass Hardlinks mit Calibre-Integration nicht funktionieren.
> \* Beachten Sie, dass dies erfordert, dass in Calibre "Benutzername und Passwort erforderlich, um auf den Content-Server zuzugreifen" aktiviert ist.
> \* Wenn "Benutzername und Passwort erforderlich, um auf den Content-Server zuzugreifen" in Calibre nicht aktiviert ist, erhalten Sie einen Fehler "Anonyme Benutzer dürfen keine Änderungen vornehmen", wenn Readarr ein Buch importiert!
{.is-warning}

> Wenn Sie sich für die Verwendung von Calibre entscheiden, können Sie nichts in der Calibre-Datenbank ändern. Wenn Sie diese Warnung nicht beachten, müssen Sie Ihre Readarr-Datenbank löschen und von vorne beginnen.
{.is-danger}

- Calibre-Host - Die IP-/Domäne des Hosts des Calibre Content Server
- Calibre-Port - Der Port, auf dem der Calibre Content Server lauscht
- (Erweitert) Calibre-URL-Basis - Fügen Sie einen Präfix zur Calibre-URL hinzu, z.B. `http://[host]:[port]/[urlBase]`
- Calibre-Benutzername - Benutzername zum Zugriff auf den Calibre Content Server
- Calibre-Passwort - Passwort zum Zugriff auf den Calibre Content Server
- Calibre-Bibliothek - Name der Calibre Content Server-Bibliothek. Leer lassen für Standardwert
- In ein Format konvertieren - (Optional) Fordern Sie den Calibre Content Server auf, in andere Formate zu konvertieren, mit einer durch Kommas getrennten Liste.
  - Überprüfen Sie das (i)-Symbol in der App für eine aktuelle Liste der Optionen.
  - Optionen sind: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-Ausgabeprofil - Wählen Sie das Ausgabeprofil des Calibre Content Server aus, das verwendet werden soll
  - Das Ausgabeprofil gibt dem Konvertierungssystem des Calibre Content Server an, wie das erstellte Dokument für das angegebene Gerät optimiert werden soll (z.B. durch Anpassen der Bildgröße an die Bildschirmgröße des Geräts). In einigen Fällen kann ein Ausgabeprofil verwendet werden, um die Ausgabe für ein bestimmtes Gerät zu optimieren, dies ist jedoch selten erforderlich.
- SSL verwenden - Aktivieren oder Deaktivieren der Verwendung von SSL (HTTPS) für den Calibre Content Server

> Wenn Sie ein einzelnes Buch hinzufügen und für das [Metadatenprofil](/readarr/settings#metadata-profiles) `None`\* auswählen, wird nur dieses Buch unter dem Autor angezeigt, wenn es hinzugefügt wird. Wenn Sie andere Bücher für diesen Autor hinzufügen möchten, wählen Sie ein geeignetes Metadatenprofil aus.
> \* **Beachten Sie, dass `None` keine Metadatenfilter anwendet und Sie unerwünschte fremdsprachige Ausgaben erhalten können. Um dies zu umgehen, [erstellen Sie ein Metadatenprofil gemäß der FAQ](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Download-Clients

`Einstellungen` => `Download-Clients`

Das Herunterladen und Importieren ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss die Software in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Setups. Das bedeutet, dass es zwar einige gemeinsame Setups gibt, aber kein einziges richtiges Setup und jedes Setup ein wenig anders sein kann. Es gibt jedoch viele falsche Setups.

> Weitere Informationen finden Sie auf der [Einstellungsseite](/readarr/settings#download-clients), auf der Seite [Weitere Informationen (Unterstützt)](/readarr/supported#download-clients) für diesen Abschnitt und in [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/).
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Readarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder einer Kategorie zu, die Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Readarr überwacht die aktiven Downloads Ihres Download-Clients, die diese Kategorie verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Readarr den endgültigen Dateispeicherort, wie er von Ihrem Download-Client gemeldet wird. Dieser Dateispeicherort kann fast überall sein, solange er sich an einem separaten Ort von Ihrem Medienordner befindet und von Readarr zugänglich ist.
- Readarr durchsucht diesen abgeschlossenen Dateispeicherort nach Dateien, die Readarr verwenden kann. Es analysiert den Dateinamen, um ihn mit den angeforderten Medien abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie an den angegebenen Medienort.
- Atomare Verschiebungen (sofortige Verschiebungen) sind standardmäßig aktiviert. Das Dateisystem und die Einhängepunkte müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die atomare Verschiebung fehlschlägt oder Ihre Konfiguration keine Hardlinks und atomare Verschiebungen unterstützt, kopiert Readarr die Datei und löscht sie dann aus der Quelle, was eine hohe E/A-Last verursacht.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Readarr aktiviert ist, werden übrig gebliebene Dateien aus dem Download an Ihren Papierkorb oder Recycling weitergeleitet, indem eine Anfrage an Ihren Client gesendet wird, um die Veröffentlichung zu löschen/zu entfernen.

### BitTorrent

{#bittorrent}

- Readarr sendet eine Download-Anfrage an Ihren Client und ordnet sie einem von Ihnen in den Einstellungen des Download-Clients konfigurierten Label oder Kategorienamen zu.
  - Beispiele: Filme, TV, Serien, Musik, usw.
- Readarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
- Abgeschlossene Dateien werden an ihrem ursprünglichen Speicherort belassen, um das Teilen der Datei zu ermöglichen (Verhältnis oder Zeit können im Download-Client oder in Readarr unter dem spezifischen Download-Client angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, erstellt Readarr einen Hardlink zur Datei, sofern dies von Ihrer Konfiguration unterstützt wird, oder kopiert die Datei, wenn Hardlinks nicht unterstützt werden.
- Hardlinks sind standardmäßig aktiviert. [Ein Hardlink benötigt keinen zusätzlichen Speicherplatz.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihre Konfiguration keine Hardlinks unterstützt, wird Readarr auf die Kopie der Datei zurückgreifen.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Readarr aktiviert ist, löscht Readarr den Torrent aus Ihrem Client und fordert den Client auf, die Torrent-Daten zu entfernen, jedoch nur, wenn der Client meldet, dass das Teilen abgeschlossen ist und der Torrent gestoppt ist (bei Abschluss pausiert).

# Importieren Ihrer vorhandenen organisierten Medienbibliothek

> Beachten Sie, dass Readarr nicht regelmäßig nach Büchern sucht. Lesen Sie diese beiden FAQ-Einträge, um zu verstehen, wie Readarr funktioniert.
[Wie findet Readarr Bücher?](/readarr/faq#how-does-readarr-find-books) und [Wie funktioniert Readarr?](/readarr/faq#how-does-readarr-work)
{.is-info}

Nachdem Sie Ihre Profile/Qualitätsgrößen eingerichtet und Ihre Indexer und Download-Clients hinzugefügt haben, ist es an der Zeit, Ihre vorhandene organisierte Medienbibliothek zu importieren.

Demnächst verfügbar - Beiträge sind willkommen

## Importieren von vorhandenen Medien

Demnächst verfügbar - Beiträge sind willkommen

# Neue Bücher hinzufügen

[Weitere Informationen finden Sie auf der Bibliotheksseite](/readarr/library#add-new)