---
title: Lidarr Einstellungen
description: 
published: true
date: 2022-07-24T14:21:19.994Z
tags: lidarr, needs-love, settings
editor: markdown
dateCreated: 2021-06-14T21:36:07.513Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Einstellungen](#einstellungen)
- [Download-Clients](#download-clients)
  - [Übersicht](#übersicht)
  - [Download-Client-Prozesse](#download-client-prozesse)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Download-Clients](#download-clients-1)
    - [Unterstützte Download-Clients](#unterstützte-download-clients)
    - [Usenet-Client-Einstellungen](#usenet-client-einstellungen)
    - [Torrent-Client-Einstellungen](#torrent-client-einstellungen)
    - [Kompatibilität der Torrent-Client-Entfernung von Downloads](#kompatibilität-der-torrent-client-entfernung-von-downloads)
  - [Abschluss der Download-Verarbeitung](#abschluss-der-download-verarbeitung)
    - [Entfernen abgeschlossener Downloads](#entfernen-abgeschlossener-downloads)
    - [Behandlung fehlgeschlagener Downloads](#behandlung-fehlgeschlagener-downloads)
  - [Remote-Pfadzuordnungen](#remote-pfadzuordnungen)
- [Import-Listen](#import-listen)
  - [Import-Listen](#import-listen-1)
  - [Import-Listenausschlüsse](#import-listenausschlüsse)
  - [Hinzufügen einer Import-Liste](#hinzufügen-einer-import-liste)
- [Verbindungen](#verbindungen)
- [Tags](#tags)
- [Allgemein](#allgemein)
  - [Updates](#updates)

# Einstellungen

Diese Seite ist eine laufende Arbeit und Beiträge - basierend auf den anderen \*Arr-Seiten - sind sowohl willkommen als auch ausdrücklich erwünscht.

# Download-Clients

> Informationen zu unterstützten Download-Clients finden Sie auf der [Weitere Informationen (Unterstützt)](/lidarr/supported#download-clients)-Seite für diesen Abschnitt
{.is-info}

## Übersicht

- Das Herunterladen und Importieren ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss die Software in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch größere Vielfalt an Setups. Das bedeutet, dass es zwar einige gängige Setups gibt, aber kein einziges richtiges Setup und jedes Setup ein wenig anders sein kann. Es gibt jedoch viele falsche Setups.

## Download-Client-Prozesse

## Usenet

- Lidarr sendet eine Download-Anfrage an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Lidarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Lidarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich an einem separaten Ort von Ihrem Medienordner befindet und von Lidarr zugänglich ist.
- Lidarr durchsucht diesen abgeschlossenen Dateispeicherort nach Dateien, die Lidarr verwenden kann. Es analysiert den Dateinamen, um ihn mit den angeforderten Medien abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie an den angegebenen Medienort.
- Atomare Verschiebungen (sofortige Verschiebungen) sind standardmäßig aktiviert. Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die atomare Verschiebung fehlschlägt oder Ihre Konfiguration keine Hardlinks und atomare Verschiebungen unterstützt, wird Lidarr auf das Kopieren der Datei zurückgreifen und sie dann aus der Quelle löschen, was IO-intensiv ist.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Lidarr aktiviert ist, werden übrig gebliebene Dateien aus dem Download an Ihren Papierkorb oder Recycling-Bin gesendet, indem eine Anfrage an Ihren Client gesendet wird, um die Veröffentlichung zu löschen/entfernen.

## BitTorrent

- Lidarr sendet eine Download-Anfrage an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Lidarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
- Abgeschlossene Dateien werden an ihrem ursprünglichen Speicherort belassen, um Ihnen das Seeden der Datei zu ermöglichen (Verhältnis oder Zeit können im Download-Client oder innerhalb von Lidarr unter dem spezifischen Download-Client angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, erstellt Lidarr einen Hardlink zur Datei, sofern dies von Ihrer Konfiguration unterstützt wird, oder kopiert sie, wenn keine Hardlinks unterstützt werden.
- Hardlinks sind standardmäßig aktiviert. [Ein Hardlink benötigt keinen zusätzlichen Festplattenspeicher.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihre Konfiguration keine Hardlinks unterstützt, wird Lidarr auf das Kopieren der Datei zurückgreifen.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Lidarr aktiviert ist, löscht Lidarr den Torrent aus Ihrem Client und fordert den Client auf, die Torrent-Daten zu entfernen, jedoch nur, wenn der Client meldet, dass das Seeden abgeschlossen ist und der Torrent gestoppt ist (nach Abschluss pausiert).

## Download-Clients

Klicken Sie auf `Einstellungen => Download-Clients` und klicken Sie dann auf das <kb>+</kb>, um einen neuen Download-Client hinzuzufügen. Ihr Download-Client sollte bereits konfiguriert und ausgeführt werden.

### Unterstützte Download-Clients

- Eine Liste der unterstützten Download-Clients finden Sie auf der [Weitere Informationen (Unterstützt)](/lidarr/supported#downloadclient)-Seite für diesen Abschnitt

Wählen Sie den Download-Client aus, den Sie hinzufügen möchten, und es wird ein Popup-Fenster angezeigt, in dem Sie die Verbindungsdetails eingeben können. Diese Details sind für die meisten Clients ähnlich. Einige fragen nach einem Benutzernamen oder Passwort, andere fragen, ob neue Downloads im pausierten/Startzustand hinzugefügt werden sollen, usw.

### Usenet-Client-Einstellungen

- Name - Der Name des Download-Clients in Lidarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- (Erweiterte Option) URL-Basis - Ein Präfix zur URL hinzufügen; dies ist häufig für Reverse Proxies erforderlich.
- API-Schlüssel - Der API-Schlüssel zur Authentifizierung bei Ihrem Client
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Kategorie - Die Kategorie in Ihrem Download-Client, die von \*Arr verwendet wird. Um nicht verwandte Downloads in der Aktivität zu vermeiden, wird dringend empfohlen, eine Kategorie festzulegen.
- Aktuelle Priorität - Download-Client-Priorität für kürzlich veröffentlichte Medien
- Ältere Priorität - Download-Client-Priorität für nicht kürzlich veröffentlichte Medien
- (Erweiterte Option) Client-Priorität - Priorität des Download-Clients. Round-Robin wird für Clients desselben Typs (Torrent/Usenet) verwendet, die dieselbe Priorität haben. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität

### Torrent-Client-Einstellungen

- Name - Der Name des Download-Clients in Lidarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients; dies ist in der Regel der WebGUI-Port
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- (Erweiterte Option) URL-Basis - Ein Präfix zur URL hinzufügen; dies ist häufig für Reverse Proxies erforderlich.
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client
- Kategorie - Die Kategorie in Ihrem Download-Client, die von \*Arr verwendet wird. Um nicht verwandte Downloads in der Aktivität zu vermeiden, wird dringend empfohlen, eine Kategorie festzulegen.
- Nach dem Import Kategorie - Die Kategorie, die nach dem Herunterladen und Importieren der Veröffentlichung festgelegt werden soll. Bitte beachten Sie, dass dadurch die Entfernung der abgeschlossenen Download-Verarbeitung unterbrochen wird.
- Aktuelle Priorität - Download-Client-Priorität für kürzlich veröffentlichte Medien
- Ältere Priorität - Download-Client-Priorität für nicht kürzlich veröffentlichte Medien
- Anfangszustand - Anfangszustand für Torrents (nur Qbittorrent: Erzwingt das Umgehen aller Seed-Schwellenwerte)
- (Erweiterte Option) - Priorität des Download-Clients. Round-Robin wird für Clients desselben Typs (Torrent/Usenet) verwendet, die dieselbe Priorität haben. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität

### Kompatibilität der Torrent-Client-Entfernung von Downloads

Lidarr kann nur das Seed-Verhältnis/die Seed-Zeit bei Clients festlegen, die das Festlegen dieses Werts über ihre API beim Hinzufügen des Torrents unterstützen. Seed-Ziele können global im Client selbst oder pro Tracker in den \*Arr-Einstellungen für jeden Indexer festgelegt werden. In der unten stehenden Tabelle finden Sie Informationen zur Kompatibilität der Clients.

|      Client       |                                Verhältnis                                 |                                   Zeit                                   |
| :---------------: | :---------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|      Deluge       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
| Download Station  | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|       Flood       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
|     Hadouken      | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|    qBittorrent    |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
|     rTorrent      |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
| Torrent Blackhole | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|   Transmission    |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Unterstützt-Idle%20Limit*-blue) |
|     uTorrent      |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
|       Vuze        |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Unterstützt-Idle%20Limit*-blue) - Transmission hat intern eine Überprüfung der Leerlaufzeit, aber Lidarr vergleicht sie mit der Seeding-Zeit, wenn das Leerlauf-Limit für jeden Torrent festgelegt ist. Dies geschieht als Workaround für die API-Beschränkungen von Transmission.{.is-info}

## Abschluss der Download-Verarbeitung

- Die Abschluss der Download-Verarbeitung ist der Vorgang, bei dem Lidarr Medien von Ihrem Download-Client in Ihre Serienordner importiert.

- Aktivieren (Erweiterte globale Einstellung) - Abgeschlossene Downloads automatisch aus dem Download-Client importieren
- Entfernen (Einstellung pro Client) - Abgeschlossene Downloads entfernen, wenn sie abgeschlossen (Usenet) oder gestoppt/vollständig (Torrents) sind
  - Bei Torrents muss Ihr Download-Client beim Erreichen der Seed-Ziele pausieren. Es erfordert auch, dass die Seed-Ziele von Lidarr gemäß der obigen Tabelle unterstützt werden. Torrents müssen auch in derselben Kategorie bleiben.

### Entfernen abgeschlossener Downloads

- Lidarr sendet eine Download-Anfrage an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
- Lidarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Lidarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich an einem separaten Ort von Ihrem Medienordner befindet.
- Lidarr durchsucht diesen abgeschlossenen Dateispeicherort nach Videodateien. Es analysiert den Videodateinamen, um ihn mit einer Episode abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie an den zugewiesenen Bibliotheksordner.
- Übrig gebliebene Dateien aus dem Download werden in Ihren Papierkorb oder Recycling-Bin gesendet.

Wenn Sie einen BitTorrent-Client verwenden, ist der Vorgang etwas anders:

- Abgeschlossene Dateien werden an ihrem ursprünglichen Speicherort belassen, um Ihnen das Seeden zu ermöglichen. Wenn Dateien in Ihren zugewiesenen Bibliotheksordner importiert werden, versucht Lidarr, die Datei als Hardlink zu erstellen, oder greift auf das Kopieren zurück (verwendet doppelten Speicherplatz), wenn keine Hardlinks unterstützt werden.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen aktiviert ist, fordert Lidarr den Torrent-Client auf, die Originaldatei und den Torrent zu löschen, dies geschieht jedoch nur, wenn der Client meldet, dass das Seeden abgeschlossen ist, der Torrent sich in derselben Kategorie befindet (d. h. keine Verwendung einer Nach-import-Kategorie), das Seed-Ziel von Lidarr unterstützt wird und der Torrent pausiert (gestoppt) ist.

### Behandlung fehlgeschlagener Downloads

- Die Behandlung fehlgeschlagener Downloads ist nur mit SABnzbd und NZBGet kompatibel.
- Die Behandlung fehlgeschlagener Downloads gilt nicht für Torrents und es gibt keine Pläne, eine solche Funktionalität hinzuzufügen.

- Die Behandlung fehlgeschlagener Downloads besteht aus mehreren Komponenten:

- Überprüfung des Downloaders:
  - Warteschlange - Überprüfen Sie die Warteschlange Ihres Downloaders auf passwortgeschützte (verschlüsselte) Veröffentlichungen, die als fehlgeschlagen markiert sind
  - Verlauf - Überprüfen Sie den Verlauf Ihres Downloaders auf Fehler (z. B. nicht genügend Blöcke zur Reparatur oder Extraktion fehlgeschlagen)
- Wenn Lidarr einen fehlgeschlagenen Download findet, beginnt es mit der Verarbeitung und führt einige Aktionen aus:
  - Fügt ein fehlgeschlagenes Ereignis zum Verlauf von Lidarr hinzu
  - Entfernt den fehlgeschlagenen Download aus dem Download-Client, um Speicherplatz freizugeben und heruntergeladene Dateien zu löschen (optional)
  - Beginnt mit der Suche nach einer Ersatzdatei (optional)
  - Blocklisting (ehemals 'Blacklisting') ermöglicht das automatische Überspringen von NZBs, wenn sie fehlschlagen. Das bedeutet, dass dieses NZB von Lidarr nie automatisch heruntergeladen wird (Sie können den Download jedoch über eine manuelle Suche erzwingen).
  - Es gibt 2 erweiterte Optionen (auf der Seite "Download-Client"-Einstellungen), die das Verhalten der fehlgeschlagenen Downloads in Lidarr steuern. Derzeit sind sie alle standardmäßig aktiviert.

- Erneut herunterladen - Steuert, ob Lidarr nach einem Fehler nach derselben Datei sucht
- (Erweiterte Option) Entfernen - Ob der Download automatisch aus dem Download-Client entfernt werden soll, wenn der Fehler erkannt wird

## Remote-Pfadzuordnungen

- Remote-Pfadzuordnung fungiert als einfache Suche nach Remote-Pfad und Ersetzung durch lokalen Pfad. Dies wird hauptsächlich für zusammengeführte lokale/Remote-Setups mit MergerFS oder ähnlichem verwendet oder wenn die Anwendung und der Download-Client nicht auf demselben Server sind.
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht in diesem Ordner behandelt wird.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft, während \*Arr auf Windows oder umgekehrt läuft. Eine Remote-Pfadzuordnung ist auch möglicherweise erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine EINFACHE Suche/Ersetzung (wo der REMOTE-Wert gefunden wird, wird er durch den LOCAL-Wert für den angegebenen Host ersetzt).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie in TRaSH's Tutorial](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist es selten erforderlich, eine Remote-Pfadzuordnung vorzunehmen. Es wird empfohlen, den [Docker-Leitfaden](/docker-guide) zu überprüfen und/oder dem Tutorial von TRaSH zu folgen (https://trash-guides.info/hardlinks).
{.is-info}

# Import-Listen

> Informationen zu unterstützten Listenarten finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/lidarr/supported#lists) für diesen Abschnitt
{.is-info}

Import-Listen ermöglichen es Ihnen, Elemente von Spotify oder Last.fm zu Lidarr hinzuzufügen. Dies kann dazu führen, dass unerwartete Elemente in Ihrer Lidarr-Datenbank hinzugefügt werden, daher verwenden Sie es bitte mit Vorsicht.

<!-- ![importlists.png](/assets/readarr/importlists.png) -->

## Import-Listen

Hier sehen Sie die Listen, die Sie derzeit haben, und können neue Listen hinzufügen. Das Hinzufügen von Listen wird weiter unten detailliert erläutert.

## Import-Listen-Ausschlüsse

Alles, was hier aufgeführt ist, wurde von den Listen ausgeschlossen und wird niemals von einer Liste hinzugefügt. Sie können Elemente entfernen, indem Sie darauf klicken.

## Hinzufügen einer Import-Liste

Nach dem Klicken auf das <kb>+</kb> wählen Sie aus, welche Art von Liste Sie hinzufügen möchten:

<!-- ![addlist.png](/assets/readarr/addlist.png) -->

In diesem Fall fügen wir eine Spotify Saved Albums-Liste hinzu.

<!-- ![bookshelflist.png](/assets/readarr/bookshelflist.png) -->

- Name - Geben Sie einen Namen für diese Liste ein.
- Automatische Hinzufügung aktivieren - Wenn aktiviert, werden alle Elemente auf der Liste automatisch zu Lidarr hinzugefügt.

> Dadurch werden ALLE ALBEN dieses Künstlers zu Lidarr hinzugefügt!

- Überwachen - Wählen Sie Ihr Überwachungsniveau für hinzugefügte Elemente aus. Gültige Optionen sind `Keine`, `Bestimmtes Album` und `Alle Alben des Künstlers`. Alle Alben werden zu Lidarr hinzugefügt, aber je nach Auswahl überwacht oder nicht überwacht.
- Stammordner - Wählen Sie den Stammordner für Künstler aus, die von dieser Liste hinzugefügt werden
- Neue Alben überwachen - Wählen Sie aus, was Lidarr mit zukünftigen Alben des hinzugefügten Künstlers tun soll. Gültige Optionen sind `Alle Alben`, `Keine`, `Neue`.
- Qualitätsprofil - Wählen Sie Ihr Qualitätsprofil für Künstler aus, die von dieser Liste hinzugefügt werden
- Metadatenprofil - Wählen Sie Ihr Metadatenprofil für Künstler aus, die von dieser Liste hinzugefügt werden
- Lidarr-Tags - Wählen Sie aus, welche Tags für Künstler aus dieser Liste gelten

> Es wird dringend empfohlen, hier einen beschreibenden Tag hinzuzufügen. Andernfalls wissen Sie nicht, welche Liste diese Elemente zu Lidarr hinzugefügt hat, und sobald sie hinzugefügt sind, können Sie diese Informationen nie wieder abrufen! Diese Informationen werden nicht protokolliert!

Standardmäßig werden Listen alle 24 Stunden synchronisiert, können aber manuell von der Seite `System` => `Aufgaben` ausgelöst werden. Diesen Vorgang können Sie nicht schneller automatisieren.

# Verbindungen

> Informationen zu unterstützten Verbindungstypen finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/lidarr/supported#notifications) für diesen Abschnitt
{.is-info}

# Tags

- Der Tag-Bereich in Lidarr wird verwendet, um verschiedene Aspekte von Lidarr zu verknüpfen.
- Tags sind besonders nützlich für:

  - Verzögerungsprofile
  - Veröffentlichungsprofile
  - Indexer

- Tags können verwendet werden, um Verzögerungsprofile, Veröffentlichungsprofile, Indexer und Künstler/Alben miteinander zu verknüpfen.
- Zum Beispiel:
  - Sie möchten, dass ein bestimmter Künstler/ein bestimmtes Album nur einen bestimmten Indexer verwendet. Sie würden einen Tag erstellen und dem Künstler/Album und dem Indexer diesen Tag zuweisen.
  - Sie möchten, dass ein bestimmtes Veröffentlichungsprofil nur ein bestimmtes Verzögerungsprofil verwendet. Sie würden einen Tag erstellen und dem Veröffentlichungsprofil und dem Verzögerungsprofil diesen Tag zuweisen.

> Hinweis: Tags beeinflussen keine "Qualitätsprofile", "Metadatenprofile" oder andere nicht oben genannte Aspekte.
{.is-info}

# Allgemein

## Updates

- (Erweiterte Option) Branch - Dies ist der Branch von Lidarr, den Sie verwenden.
  - [Bitte lesen Sie diesen FAQ-Eintrag für weitere Informationen](/lidarr/faq#how-do-i-update-lidarr)
- Automatisch - Updates automatisch herunterladen und installieren. Sie können weiterhin über System: Updates installieren. Hinweis: Windows-Benutzer werden immer automatisch aktualisiert.
- Mechanismus - Verwenden Sie den integrierten Updater von Lidarr oder ein Skript
  - Integriert - Verwenden Sie den eigenen Updater von Lidarr
  - Skript - Lassen Sie Lidarr das Update-Skript ausführen
  - Docker - Aktualisieren Sie Lidarr nicht innerhalb des Docker, sondern ziehen Sie ein brandneues Image mit dem neuen Update
- Skript - Nur sichtbar, wenn der Mechanismus auf Skript eingestellt ist - Pfad zum Update-Skript
- Update-Prozess - Lidarr lädt die Update-Datei herunter, überprüft deren Integrität, extrahiert sie an einen temporären Speicherort und ruft die gewählte Methode auf. Der Update-Prozess wird unter demselben Benutzer ausgeführt, unter dem Lidarr ausgeführt wird. Er benötigt Berechtigungen, um die Lidarr-Dateien zu aktualisieren sowie Lidarr zu starten/stoppen.
- Integriert - Die integrierte Methode sichert Lidarr-Dateien und -Einstellungen, stoppt Lidarr, aktualisiert die Installation und startet Lidarr. Wenn Ihr System das Stoppen von Lidarr nicht verarbeiten kann und versucht, es automatisch neu zu starten, ist es möglicherweise besser, stattdessen ein Skript zu verwenden. Im Falle eines Fehlers wird die vorherige Version von Lidarr neu gestartet.
- Skript - Das Skript sollte dasselbe wie der integrierte Updater behandeln. Wenn Sie Dienste stoppen und starten müssen (upstart/launchd/etc), müssen Sie dies hier tun.