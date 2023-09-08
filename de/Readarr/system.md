---
title: Readarr System
description: 
published: true
date: 2022-05-05T12:52:16.242Z
tags: readarr, needs-love, system
editor: markdown
dateCreated: 2021-06-20T19:54:43.262Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Status](#status)
  - [Gesundheit](#gesundheit)
    - [Systemwarnungen](#systemwarnungen)
      - [Zweig ist kein gültiger Release-Zweig](#zweig-ist-kein-gültiger-release-zweig)
      - [Derzeit installierte SQLite-Version wird nicht unterstützt](#derzeit-installierte-sqlite-version-wird-nicht-unterstützt)
      - [Neues Update verfügbar](#neues-update-verfügbar)
      - [Update kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist](#update-kann-nicht-installiert-werden-da-der-startordner-vom-benutzer-nicht-beschreibbar-ist)
      - [Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern](#aktualisierung-ist-nicht-möglich-um-das-löschen-von-appdata-beim-update-zu-verhindern)
      - [Zweig ist für eine frühere Version](#zweig-ist-für-eine-frühere-version)
      - [Verbindung mit SignalR konnte nicht hergestellt werden](#verbindung-mit-signalr-konnte-nicht-hergestellt-werden)
        - [Nginx](#nginx)
      - [IP-Adresse für den konfigurierten Proxy-Host konnte nicht aufgelöst werden](#ip-adresse-für-den-konfigurierten-proxy-host-konnte-nicht-aufgelöst-werden)
      - [Proxy-Test fehlgeschlagen](#proxy-test-fehlgeschlagen)
      - [Systemzeit weicht um mehr als 1 Tag ab](#systemzeit-weicht-um-mehr-als-1-tag-ab)
    - [Download-Clients](#download-clients)
      - [Es ist kein Download-Client verfügbar](#es-ist-kein-download-client-verfügbar)
      - [Kommunikation mit dem Download-Client nicht möglich](#kommunikation-mit-dem-download-client-nicht-möglich)
      - [Download-Clients sind aufgrund eines Fehlers nicht verfügbar](#download-clients-sind-aufgrund-eines-fehlers-nicht-verfügbar)
      - [Abgeschlossene Download-Verarbeitung aktivieren](#abgeschlossene-download-verarbeitung-aktivieren)
      - [Docker-Fehler bei der Zuordnung des Remote-Pfads](#docker-fehler-bei-der-zuordnung-des-remote-pfads)
      - [In das Stammverzeichnis herunterladen](#in-das-stammverzeichnis-herunterladen)
      - [Fehlerhafte Download-Client-Einstellungen](#fehlerhafte-download-client-einstellungen)
      - [Fehlerhafte Remote-Pfad-Zuordnung](#fehlerhafte-remote-pfad-zuordnung)
      - [Berechtigungsfehler](#berechtigungsfehler)
      - [Autor-Mount ist schreibgeschützt](#autor-mount-ist-schreibgeschützt)
      - [Remote-Datei wurde während der Verarbeitung teilweise entfernt](#remote-datei-wurde-während-der-verarbeitung-teilweise-entfernt)
      - [Remote-Pfad wird verwendet und Import fehlgeschlagen](#remote-pfad-wird-verwendet-und-import-fehlgeschlagen)
    - [Abgeschlossene/fehlgeschlagene Download-Verarbeitung](#abgeschlossenefehlgeschlagene-download-verarbeitung)
      - [Abgeschlossene Download-Verarbeitung ist deaktiviert](#abgeschlossene-download-verarbeitung-ist-deaktiviert)
    - [Indexer](#indexer)
      - [Keine Indexer verfügbar mit aktivierter automatischer Suche, Readarr liefert keine automatischen Suchergebnisse](#keine-indexer-verfügbar-mit-aktivierter-automatischer-suche-readarr-liefert-keine-automatischen-suchergebnisse)
      - [Keine Indexer verfügbar mit aktivierter RSS-Synchronisierung, Readarr wird keine neuen Veröffentlichungen automatisch abrufen](#keine-indexer-verfügbar-mit-aktivierter-rss-synchronisierung-readarr-wird-keine-neuen-veröffentlichungen-automatisch-abrufen)
      - [Keine Indexer aktiviert](#keine-indexer-aktiviert)
    - [Aktivierte Indexer unterstützen keine Suche](#aktivierte-indexer-unterstützen-keine-suche)
      - [Keine Indexer verfügbar mit aktivierter interaktiver Suche](#keine-indexer-verfügbar-mit-aktivierter-interaktiver-suche)
      - [Indexer sind aufgrund von Fehlern nicht verfügbar](#indexer-sind-aufgrund-von-fehlern-nicht-verfügbar)
      - [Jackett All Endpoint verwendet](#jackett-all-endpoint-verwendet)
        - [Lösungen](#lösungen)
    - [Buchordner](#buchordner)
      - [Fehlender Stammordner](#fehlender-stammordner)
    - [Import-Listen](#import-listen)
      - [Import-Listen sind aufgrund von Fehlern nicht verfügbar](#import-listen-sind-aufgrund-von-fehlern-nicht-verfügbar)
  - [Festplattenspeicher](#festplattenspeicher)
  - [Über](#über)
  - [Weitere Informationen](#weitere-informationen)
- [Aufgaben](#aufgaben)
  - [Geplant](#geplant)
  - [Warteschlange](#warteschlange)
- [Sicherung](#sicherung)
- [Aktualisierungen](#aktualisierungen)
- [Ereignisse](#ereignisse)
- [Protokolldateien](#protokolldateien)

# Status

## Gesundheit

- Diese Seite enthält eine Liste von Fehlern bei der Gesundheitsprüfung. Diese Gesundheitsprüfungen werden regelmäßig von Readarr durchgeführt und bei bestimmten Ereignissen durchgeführt. Die resultierenden Warnungen und Fehler werden hier aufgelistet, um Ratschläge zur Behebung zu geben.

### Systemwarnungen

#### Zweig ist kein gültiger Release-Zweig

- Der von Ihnen festgelegte Zweig ist kein gültiger Release-Zweig. Sie erhalten keine Updates. Bitte ändern Sie zu einem der [aktuellen Release-Zweige](/readarr/faq#how-do-i-update-readarr).

#### Derzeit installierte SQLite-Version wird nicht unterstützt

- Readarr speichert seine Daten in einer SQLite-Datenbank. Die auf Ihrem System installierte SQLite3-Bibliothek ist zu alt. Readarr erfordert mindestens Version 3.9.0. Beachten Sie, dass Readarr `libSQLite3.so` verwendet, die in einem SQLite3-Upgrade-Paket enthalten sein kann oder auch nicht.

> Beachten Sie, dass Readarr `libSQLite3.so` verwendet, die in einem SQLite3-Upgrade-Paket enthalten sein kann oder auch nicht.
{.is-info}

#### Neues Update verfügbar

Freue dich, die Entwickler haben ein neues Update veröffentlicht. Dies bedeutet in der Regel großartige neue Funktionen und behobene Fehler (richtig?). Offensichtlich haben Sie die automatische Aktualisierung nicht aktiviert, daher müssen Sie herausfinden, wie Sie auf Ihrer Plattform aktualisieren können. Das Drücken der Schaltfläche "Installieren" auf der Seite System => Updates ist wahrscheinlich ein guter Ausgangspunkt.

> Diese Warnung wird nicht angezeigt, wenn Ihre aktuelle Version weniger als 14 Tage alt ist.
{.is-info}

#### Update kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist

- Dies bedeutet, dass Readarr sich nicht selbst aktualisieren kann. Sie müssen Readarr manuell aktualisieren oder die Berechtigungen für das Startverzeichnis von Readarr (das Installationsverzeichnis) so einstellen, dass Readarr sich selbst aktualisieren kann.

#### Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern

- Readarr hat erkannt, dass der AppData-Ordner für Ihr Betriebssystem im Verzeichnis liegt, das die Readarr-Binärdateien enthält. Normalerweise wäre dies C:\ProgramData für Windows und ~/.config für Linux.

- Bitte schauen Sie sich System => Info an, um die aktuellen AppData- und Startverzeichnisse zu sehen.
- Dies bedeutet, dass Readarr sich selbst nicht aktualisieren kann, ohne Datenverlust zu riskieren.
- Wenn Sie Linux verwenden, müssen Sie wahrscheinlich das Home-Verzeichnis für den Benutzer ändern, unter dem Readarr ausgeführt wird, und den aktuellen Inhalt des Verzeichnisses ~/.config/Readarr kopieren, um Ihre Datenbank zu erhalten.

#### Zweig ist für eine frühere Version

- Der in den Einstellungen/Allgemein festgelegte Aktualisierungszweig ist für eine frühere Version von Readarr bestimmt. Daher sieht die Instanz keine korrekten Aktualisierungsinformationen im System/Updates-Feed und erhält möglicherweise keine neuen Updates bei Veröffentlichung.

#### Verbindung mit SignalR konnte nicht hergestellt werden

- SignalR steuert die dynamischen UI-Updates. Wenn Ihr Browser keine Verbindung mit SignalR auf Ihrem Server herstellen kann, sehen Sie keine Echtzeit-Updates in der Benutzeroberfläche.

- Das häufigste Auftreten davon ist die Verwendung eines Reverse-Proxys oder von Cloudflare.
- Cloudflare benötigt aktiviertes Websockets.

##### Nginx

- Nginx erfordert die folgende Ergänzung zum location-Block für die App:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Stellen Sie sicher, dass Sie proxy_set_header Connection "Upgrade"; nicht wie in der nginx-Dokumentation vorgeschlagen einschließen. DAS FUNKTIONIERT NICHT
> Siehe <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

Für Apache2-Reverse-Proxy müssen Sie die folgenden Module aktivieren: proxy, proxy_http und proxy_wstunnel. Fügen Sie dann diese Websocket-Tunnel-Direktive zu Ihrer Vhost-Konfiguration hinzu:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8787/$1 [P,L]
```

Für Caddy (V1) verwenden Sie dies:
Hinweis: Sie müssen auch die Websocket-Direktive zu Ihrer Readarr-Konfiguration hinzufügen

```none
 proxy /readarr 127.0.0.1:8787 {
     websocket
     transparent
 }
```

#### IP-Adresse für den konfigurierten Proxy-Host konnte nicht aufgelöst werden

- Überprüfen Sie Ihre Proxy-Einstellungen und stellen Sie sicher, dass sie korrekt sind.
- Stellen Sie sicher, dass Ihr Proxy aktiv, ausgeführt und erreichbar ist.

#### Proxy-Test fehlgeschlagen

- Ihr konfigurierter Proxy konnte nicht erfolgreich getestet werden. Überprüfen Sie den bereitgestellten HTTP-Fehler und/oder überprüfen Sie die Protokolle für weitere Details.

#### Systemzeit weicht um mehr als 1 Tag ab

- Die Systemzeit weicht um mehr als 1 Tag ab. Geplante Aufgaben können erst korrekt ausgeführt werden, wenn die Zeit korrigiert ist.
- Überprüfen Sie Ihre Systemzeit und stellen Sie sicher, dass sie mit einem autoritativen Zeitserver synchronisiert ist und korrekt ist.

### Download-Clients

#### Es ist kein Download-Client verfügbar

- Für Readarr ist ein ordnungsgemäß konfigurierter und aktivierter Download-Client erforderlich, um Medien herunterladen zu können. Da Readarr verschiedene Download-Clients unterstützt, sollten Sie ermitteln, welcher Ihren Anforderungen am besten entspricht. Wenn Sie bereits einen Download-Client installiert haben, sollten Sie Readarr so konfigurieren, dass es ihn verwendet, und eine Kategorie erstellen. Siehe Einstellungen => Download-Client.

#### Kommunikation mit dem Download-Client nicht möglich

- Readarr konnte nicht mit dem konfigurierten Download-Client kommunizieren. Überprüfen Sie, ob der Download-Client betriebsbereit ist, und überprüfen Sie die URL erneut. Dies kann auch auf einen Authentifizierungsfehler hinweisen.
- Dies liegt in der Regel an einem falsch konfigurierten Download-Client. Dinge, die Sie in der Regel überprüfen können:
- Die IP-Adresse Ihres Download-Clients, wenn er auf demselben Bare-Metal-Computer ausgeführt wird, ist dies in der Regel 127.0.0.1.
- Die Portnummer, die Ihr Download-Client verwendet, diese sind mit der Standard-Portnummer ausgefüllt, aber wenn Sie sie geändert haben, müssen Sie dieselbe Nummer in Readarr eingeben.
- Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie sowohl Ihre Readarr-Instanz als auch Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in der SSL-FAQ.

#### Download-Clients sind aufgrund eines Fehlers nicht verfügbar

{#download-clients-are-unavailable-due-to-failures}

- Einer oder mehrere Ihrer Download-Clients reagieren nicht auf Anfragen von Readarr. Daher hat Readarr beschlossen, die Abfrage des Download-Clients auf seinem normalen 1-Minuten-Zyklus vorübergehend zu stoppen, der normalerweise verwendet wird, um aktive Downloads zu verfolgen und abgeschlossene Downloads zu importieren. Readarr wird jedoch weiterhin versuchen, Downloads an den Client zu senden, wird aber höchstwahrscheinlich scheitern.
- Sie sollten System=>Protokolle überprüfen, um den Grund für die Fehler zu sehen.
- Wenn Sie diesen Download-Client nicht mehr verwenden, deaktivieren Sie ihn in Readarr, um die Fehler zu verhindern.

#### Abgeschlossene Download-Verarbeitung aktivieren

- Readarr erfordert die Aktivierung der abgeschlossenen Download-Verarbeitung, um Dateien importieren zu können, die vom Download-Client heruntergeladen wurden. Es wird empfohlen, die abgeschlossene Download-Verarbeitung zu aktivieren.
- (Die abgeschlossene Download-Verarbeitung ist standardmäßig für neue Benutzer aktiviert.)

#### Docker-Fehler bei der Zuordnung des Remote-Pfads

- Dieser Fehler ist in der Regel mit fehlerhaften Docker-Pfaden in Ihrem Download-Client oder Readarr verbunden.

- Ein Beispiel dafür wäre:
  - Download-Client: Download-Pfad: /mnt/user/downloads:/downloads
  - Readarr: Download-Pfad: /mnt/user/downloads:/data
- In diesem Beispiel legt der Download-Client seine Downloads in /downloads ab und teilt Readarr dann mit, dass das fertige Buch in /downloads ist. Readarr kommt dann und sagt "Okay, cool, lass mich in /downloads nachsehen" Nun, innerhalb von Readarr haben Sie keinen /downloads-Pfad zugewiesen, sondern einen /data-Pfad, daher wird dieser Fehler angezeigt.
- Die einfachste Lösung dafür ist KONSISTENZ. Wenn Sie ein Schema in Ihrem Download-Client verwenden, verwenden Sie es überall.

- Team Readarr ist ein großer Fan von einfach /data zu verwenden.
  - Download-Client: /mnt/user/data/downloads:/data/downloads
  - Readarr: /mnt/user/data:/data

- Jetzt können Sie im Download-Client angeben, wo Sie Ihre Downloads in /data platzieren möchten. Dies variiert je nach Client, aber Sie sollten ihm sagen können "Ja, Download-Client, platziere meine Dateien in." /data/torrents (oder usenet)/books und da Sie in Readarr /data verwendet haben, wenn der Download-Client Readarr mitteilt, dass er fertig ist, wird Readarr kommen und sagen "Super, ich habe ein /data und ich kann auch /torrents (oder usenet)/books sehen, alles ist in Ordnung auf der Welt."
- Es gibt viele großartige Anleitungen: unser Wiki [Docker-Anleitung](/docker-guide) und TRaSH's [Hardlinks und Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Diese Anleitungen legen zwar großen Wert auf Hardlinks und Atomic-Moves, aber das allgemeine Konzept von Containern und der Funktionsweise der Pfadzuordnung ist der Kern dieser Diskussionen.

- Wenn Sie Betriebssysteme oder nativ und Docker überschreiten, benötigen Sie eine Remote-Pfad-Zuordnung. Siehe [TRaSH's Remote Path Guide für Radarr, aber das Konzept ist für alle \*Arrs gleich](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) für weitere Informationen.

- Wenn Sie diesen Fehler bei Calibre erhalten, kann Redarr nicht auf die Calibre-Bibliothek zugreifen. Die Lösung ist dieselbe - korrigieren Sie die inkonsistenten Mounts für Ihre Container. Alternativ können Sie eine Remote-Pfad-Zuordnung erstellen, um den Pfad der Calibre-Bibliothek auf den für Readarr zugänglichen Pfad abzubilden. Eine Remote-Pfad-Zuordnung ist nur erforderlich, wenn Betriebssysteme oder Server überschritten werden. Wenn alles in Docker ist, ist es besser, Ihre Mounts zu korrigieren.

#### In das Stammverzeichnis herunterladen

{#downloads-in-root-folder}

- In der Anwendung wird ein Stammverzeichnis als das konfigurierte Medienbibliotheksverzeichnis definiert. Dies ist nicht das Stammverzeichnis eines Mounts. Ihr Download-Client lädt unvollständige oder abgeschlossene Downloads (oder verschiebt abgeschlossene Downloads) in Ihr Stamm (Bibliotheks-)Verzeichnis.
- Dies führt häufig zu Problemen - einschließlich Datenverlust - und sollte nicht durchgeführt werden. Ändern Sie Ihren Download-Client so, dass er Downloads nicht in Ihrem Stammverzeichnis ablegt. Beachten Sie, dass "ablegen" auch bedeutet, dass Ihre Download-Client-Kategorie auf Ihr Stammverzeichnis festgelegt ist oder wenn NZBGet/SABnzbd die Sortierung aktiviert haben und in Ihr Stammverzeichnis sortieren.
- Bitte beachten Sie, dass diese Überprüfung alle definierten/konfigurierten Stammverzeichnisse betrachtet, nicht nur die derzeit verwendeten Stammverzeichnisse. Mit anderen Worten, der Ordner, in den Ihr Download-Client herunterlädt oder abgeschlossene Downloads verschiebt, sollte nicht derselbe Ordner sein, den Sie als Ihr Stamm-/Bibliotheks-/endgültiges Medienzielverzeichnis in der *Arr-Anwendung konfiguriert haben.
- Konfigurierte Stammverzeichnisse (auch Bibliotheksverzeichnisse genannt) finden Sie in [Einstellungen => Medienverwaltung => Stammverzeichnisse](/readarr/settings/#root-folders)
- Ein Beispiel ist, wenn Ihre Downloads in `\data\downloads` gehen, dann haben Sie ein Stammverzeichnis als `\data\downloads` festgelegt.
- Es wird empfohlen, Pfade wie `\data\media\` für Ihr Stammverzeichnis/Bibliothek und `\data\downloads\` für Ihre Downloads zu verwenden.
- Lesen Sie unsere [Docker-Anleitung](/docker-guide) und TRaSH's [Hardlinks und Instant Moves (Atomic-Moves) Anleitung](https://trash-guides.info/hardlinks/) für weitere Informationen zur korrekten und optimalen Pfadkonfiguration. Beachten Sie, dass die Konzepte für Docker und Nicht-Docker gelten.

> Ihr Download-Ordner, in dem Ihr Download-Client die Downloads platziert, und Ihr Stamm-/Bibliotheksordner MÜSSEN getrennt sein. \*Arr importiert die Datei(en) aus dem Download-Ordner Ihres Download-Clients in Ihre Bibliothek. Der Download-Client sollte nichts verschieben oder etwas in Ihre Bibliothek herunterladen.
{.is-warning}

#### Fehlerhafte Download-Client-Einstellungen

- Der Speicherort, an dem Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne Remote-Pfad-Zuordnung zu wechseln, betreffen.

#### Fehlerhafte Remote-Pfad-Zuordnung

- Der Speicherort, an den Ihr Download-Client die Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann an Berechtigungen liegen oder daran, dass Sie von Windows zu Linux oder von Linux zu Windows wechseln, ohne eine Remote-Pfadzuordnung zu haben. Weitere Informationen finden Sie in [TRaSH's Remote Path Guide](https://trash-guides.info/Readarr/Readarr-remote-path-mapping/).

#### Berechtigungsfehler

- Readarr oder der Benutzer, unter dem Readarr läuft, kann nicht auf den Speicherort zugreifen, an den Ihr Download-Client die Dateien herunterlädt. Dies ist in der Regel ein Berechtigungsproblem.

#### Autor-Mount ist schreibgeschützt

{#author-mount-ro}

- Das Mounten eines Autoren-Pfads ist schreibgeschützt. Überprüfen Sie Ihre Mount-Einstellungen sowie Besitz und Berechtigungen.

#### Remote-Datei wurde während der Verarbeitung entfernt

- Eine über eine Remote-Pfadzuordnung zugängliche Datei scheint vor Abschluss der Verarbeitung entfernt worden zu sein.

#### Remote-Pfad wird verwendet und Import ist fehlgeschlagen

- Überprüfen Sie Ihre Protokolle für weitere Informationen. Siehe unsere Fehlerbehebungshandbücher.

### Behandlung abgeschlossener/fehlgeschlagener Downloads

#### Behandlung abgeschlossener Downloads ist deaktiviert

- (Diese Warnung wird nur für bestehende Benutzer generiert, bevor die Funktion zur Behandlung abgeschlossener Downloads implementiert wurde. Diese Funktion ist standardmäßig deaktiviert, um sicherzustellen, dass das System für aktuelle Konfigurationen wie erwartet funktioniert.)
- Es wird empfohlen, die Behandlung abgeschlossener Downloads zu verwenden, da sie eine bessere Kompatibilität für die Entpackungs- und Nachverarbeitungslogik verschiedener Download-Clients bietet. Mit dieser Funktion importiert Readarr einen Download erst, wenn der Download-Client ihn als bereit meldet.
- Wenn Sie die Behandlung abgeschlossener Downloads aktivieren möchten, sollten Sie Folgendes überprüfen: * Warnung: Die Behandlung abgeschlossener Downloads funktioniert nur ordnungsgemäß, wenn der Download-Client und Readarr auf demselben Computer ausgeführt werden, da er den Pfad, der importiert werden soll, direkt vom Download-Client erhält. Andernfalls ist eine Remote-Zuordnung erforderlich.

### Indexer

#### Keine Indexer verfügbar mit aktivierter automatischer Suche, Readarr liefert keine automatischen Suchergebnisse

- Einfach ausgedrückt haben Sie keine Indexer festgelegt, die automatische Suchen zulassen.
- Gehen Sie zu Einstellungen => Indexer, wählen Sie einen Indexer aus, für den Sie automatische Suchen zulassen möchten, und klicken Sie dann auf Speichern.

#### Keine Indexer verfügbar mit aktivierter RSS-Synchronisierung, Readarr lädt keine neuen Veröffentlichungen automatisch herunter

- Readarr verwendet den RSS-Feed, um neue Veröffentlichungen zu erfassen, während sie auftreten. Weitere Informationen dazu finden Sie hier.
- Um dieses Problem zu beheben, gehen Sie zu Einstellungen => Indexer, wählen Sie einen Indexer aus, den Sie haben, und aktivieren Sie die RSS-Synchronisierung.

#### Keine Indexer aktiviert

- Readarr benötigt Indexer, um neue Veröffentlichungen entdecken zu können. Bitte lesen Sie das Wiki, um Anweisungen zum Hinzufügen von Indexern zu erhalten.

### Aktivierte Indexer unterstützen keine Suche

- Keiner der von Ihnen aktivierten Indexer unterstützt die Suche. Das bedeutet, dass Readarr nur neue Veröffentlichungen über die RSS-Feeds finden kann. Bei der Suche nach Büchern (entweder automatische Suche oder manuelle Suche) werden niemals Ergebnisse zurückgegeben. Die einzige Möglichkeit, dies zu beheben, besteht darin, einen weiteren Indexer hinzuzufügen.

#### Keine Indexer verfügbar mit aktivierter interaktiver Suche

- Keiner der von Ihnen aktivierten Indexer unterstützt die interaktive Suche. Das bedeutet, dass die Anwendung nur neue Veröffentlichungen über die RSS-Feeds oder eine automatische Suche finden kann.

#### Indexer sind aufgrund von Fehlern nicht verfügbar

- Fehler sind aufgetreten, als Readarr versuchte, einen Ihrer Indexer zu verwenden. Um die Anzahl der Wiederholungsversuche zu begrenzen, wird Readarr den Indexer für eine zunehmende Zeitdauer nicht verwenden (bis zu 24 Stunden).
- Dieser Mechanismus wird ausgelöst, wenn Readarr keine Antwort vom Indexer erhalten konnte (könnte durch DNS, Proxy/VPN-Verbindung, Authentifizierung oder ein Indexer-Problem verursacht werden) oder die NZB-/Torrent-Datei nicht vom Indexer abrufen konnte. Bitte überprüfen Sie die Protokolle, um festzustellen, welche Art von Fehler das Problem verursacht.
- Sie können die Warnung verhindern, indem Sie den betroffenen Indexer deaktivieren.
- Führen Sie den Test auf dem Indexer aus, um Readarr dazu zu zwingen, den Indexer erneut zu überprüfen. Beachten Sie jedoch, dass die Warnung der Gesundheitsprüfung nicht immer sofort verschwindet.

#### Jackett All-Endpunkt verwendet

- Der Jackett /all-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere sind potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Selbst die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des /all-Endpunkts hat keine Vorteile, nur Nachteile:
  - Sie verlieren die Kontrolle über indexerspezifische Einstellungen (Kategorien, Suchmodi usw.).
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen.
  - Indexerspezifische Kategorien (\>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis.
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt.
  - Wenn einer der Tracker in /all einen Fehler zurückgibt, deaktiviert \*Arr ihn und Sie erhalten keine Ergebnisse mehr.

##### Lösungen

- Fügen Sie jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu.
- Schauen Sie sich [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schauen Sie sich [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwenden Sie jedoch nicht ihren einzelnen Aggregat-Endpunkt und verwenden Sie `multi`, wenn die Synchronisierung verwendet wird.

### Buchordner

#### Fehlender Stammordner

- Dieser Fehler wird in der Regel identifiziert, wenn ein Autor nach einem Stammordner sucht, der nicht mehr verfügbar ist.
- Dieser Fehler kann auch auftreten, wenn eine Liste immer noch auf einen Stammordner zeigt, der nicht mehr verfügbar ist.
- Wenn Sie diese Warnung entfernen möchten, suchen Sie einfach das Album, das den alten Stammordner verwendet, und bearbeiten Sie es so, dass der richtige Stammordner verwendet wird.

- Der einfachste Weg, den problematischen Autor zu finden, besteht darin:

  - Gehen Sie zum Autor (Bibliothek) Tab
  - Erstellen Sie einen benutzerdefinierten Filter mit dem alten Stammordnerpfad
  - Wählen Sie Massenbearbeitung in der oberen Leiste aus und wählen Sie aus dem Dropdown-Menü Root Paths den neuen Stammordnerpfad aus, zu dem Sie diese Autoren verschieben möchten.
  - Als nächstes erhalten Sie einen Pop-up, in dem steht: Möchten Sie die Autorenordner nach 'Stammordner' verschieben? Es wird auch angegeben, dass der Autorenordner gemäß dem Autorenordnerformat in den Einstellungen umbenannt wird. Wählen Sie einfach Nein aus, wenn Sie nicht möchten, dass Lidarr Ihre Dateien verschiebt.
  - Führen Sie die Check Health-Aufgabe in System => Aufgaben aus

### Import-Listen

#### Import-Listen sind aufgrund von Fehlern nicht verfügbar

- In der Regel bedeutet dies einfach, dass Readarr nicht mehr über die API oder durch Anmeldung bei Ihrem ausgewählten Listenanbieter kommunizieren kann. Wenn das Problem weiterhin besteht, sollten Sie sie kontaktieren, um sie auszuschließen, da ihre Systeme von Zeit zu Zeit überlastet sein können.

## Festplattenspeicher

- In diesem Abschnitt wird Ihnen der verfügbare Festplattenspeicher angezeigt.
- In Docker kann dies schwierig sein, da Ihnen in der Regel der verfügbare Speicherplatz innerhalb Ihres Docker-Images angezeigt wird.

## Über

- Hier erfahren Sie mehr über Ihre aktuelle Installation von Readarr.

## Weitere Informationen

- Startseite: Readarr's Startseite
- Wiki: Sie sind bereits hier
- Reddit: r/readarr
- Discord: Treten Sie unserem Discord bei
- Spenden: Wenn Sie großzügig sind und spenden möchten, klicken Sie hier
- Spenden an Sonarr: Wenn Sie großzügig sind und an das Projekt spenden möchten, das alles begonnen hat, klicken Sie hier
- Quellcode: GitHub
- Funktionsanfragen: Haben Sie eine großartige Idee? Teilen Sie sie hier mit

# Aufgaben

## Geplant

- In diesem Abschnitt werden alle geplanten Aufgaben aufgelistet, die Readarr ausführt.

- Anwendungs-Update überprüfen - Dies wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan ausgeführt und überprüft, ob Readarr auf der neuesten Version läuft, und löst dann das Aktualisierungsskript aus, um Readarr zu aktualisieren. Einstellungen => Update

> Hinweis: Wenn Sie Docker verwenden, wird dadurch Ihr Container nicht aktualisiert, da ein neues Image heruntergeladen werden muss.
{.is-warning}

- Backup - Dies führt gemäß einem festgelegten Zeitplan ein Backup der Datenbank von Readarr durch. Weitere Informationen dazu finden Sie hier. Weitere Informationen zu Backups finden Sie unter System => Backups.
- Gesundheitsprüfung - Die Gesundheitsprüfung wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan durchgeführt und überprüft den allgemeinen Zustand von Readarr. Eine Liste möglicher gesundheitsbezogener Probleme finden Sie im Wiki-Eintrag zu Gesundheitsprüfungen.
- Aufräumen - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan werden alle Spinnweben entfernt, die Böden gekehrt und gesaugt, gewischt und sogar schöne ordentliche kleine gefaltete Notizen nur für Sie gemacht. Aber den Müll nimmt es nicht mit. Dafür wurde es einfach nicht genug bezahlt.
- Import-Listen-Synchronisierung - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan werden Ihre Listen ausgeführt und möglicherweise neue Bücher importiert. Weitere Informationen zu Listen finden Sie unter Einstellungen => Listen.
- Bereinigung von Nachrichten - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan werden die Nachrichten bereinigt, die in der unteren linken Ecke von Readarr angezeigt werden.
- Autor aktualisieren - Dadurch werden alle Autoren in Ihrer Bibliothek aktualisiert.
- Überwachte Downloads aktualisieren - Dadurch werden die Warteschlange für Downloads aktualisiert, die sich unter Aktivität befindet. Es wird im Wesentlichen Ihr Download-Client abgefragt, um abgeschlossene Downloads zu überprüfen.
- Ordner erneut scannen - Dadurch werden alle Buchordner gescannt, um festzustellen, ob ein Buch vorhanden ist oder nicht, und der Status entsprechend aktualisiert.
- RSS-Synchronisierung - Dadurch wird die RSS-Synchronisierung ausgeführt. Dies kann in den Einstellungen => Optionen geändert werden. Weitere Informationen zur RSS-Funktion finden Sie in unseren FAQ.

> Alle diese Aufgaben können außerhalb ihrer geplanten Zeiten manuell ausgeführt werden, indem Sie auf das Symbol ganz rechts neben jeder Aufgabe klicken.
{.is-info}

## Warteschlange

Die Warteschlange zeigt Ihnen laufende und bevorstehende Aufgaben sowie eine Historie der kürzlich ausgeführten Aufgaben und deren Dauer an.

# Backup

> Wenn Sie wissen möchten, wie Sie Ihre Readarr-Instanz sichern/wiederherstellen können, klicken Sie [hier](/readarr/faq).
{.is-info}

- In der Backup-Sektion werden Ihnen frühere Backups angezeigt (sofern Sie keine frische Installation haben, die noch keine Backups erstellt hat).
  
- Jetzt sichern - Diese Option löst eine manuelle Sicherung der Datenbank von Readarr aus.
- Backup wiederherstellen - Dadurch wird ein neuer Bildschirm geöffnet, um aus einem früheren Backup wiederherzustellen.
  - Durch Auswahl von Datei auswählen wird Ihr Browser aufgefordert, einen Dialog zum Wiederherstellen aus einem Readarr-Zip-Backup zu öffnen.
  
- Wenn Sie frühere Backups haben und diese von Readarr herunterladen möchten, um sie an einem anderen Ort zu speichern, können Sie einfach eine dieser Dateien auswählen, um sie herunterzuladen.
- Rechts neben jedem der vorherigen Downloads haben Sie zwei Optionen.
  - Wiederherstellen (Uhr-Symbol) - Um aus einem früheren Backup wiederherzustellen - Dadurch wird ein neues Fenster geöffnet, um zu bestätigen, dass Sie aus diesem Backup wiederherstellen möchten.
  - Löschen (Mülleimer) - Um ein früheres Backup zu löschen

# Updates

- Der Update-Bildschirm zeigt die letzten 5 Updates an, die durchgeführt wurden, sowie die aktuelle Version, die Sie verwenden.
- Auf dieser Seite werden auch die Update-Notizen der Entwickler angezeigt, in denen steht, was in Readarr behoben oder hinzugefügt wurde (Freude!)
  
> Ein Wartungs-Release enthält Fehlerbehebungen und verschiedene Verbesserungen. Weitere Informationen finden Sie im Commit-Verlauf.
{.is-info}

# Ereignisse

- Der Ereignis-Tab zeigt Ihnen, was in Ihrem Readarr passiert ist. Dies kann zur Diagnose von leichten Problemen verwendet werden. Es ersetzt jedoch nicht die Protokolle zur Fehlerbehebung, die in Logging besprochen werden.

> Ereignisse entsprechen den INFO-Protokollen. {.is-info}

- Komponenten - Diese Spalte zeigt an, welche Komponente in Readarr ausgelöst wurde.
- Nachricht - Diese Spalte zeigt an, welche Nachricht von der Komponente aus der vorherigen Spalte gesendet wurde.
- Zahnrad-Symbol - Diese Option ermöglicht es Ihnen, die Anzahl der angezeigten Komponenten/Nachrichten pro Seite zu ändern (Standardmäßig sind es 50).
- Optionen oben auf der Seite
  - Aktualisieren - Diese Option aktualisiert die aktuelle Seite und ruft ein neues Ereignisprotokoll ab.
  - Löschen - Dadurch wird das aktuelle Ereignisprotokoll gelöscht und Sie können von vorne beginnen.

# Protokolldateien

- Auf dieser Seite können Sie die aktuellen Protokolldateien für Readarr herunterladen und anzeigen.

- In der obersten Zeile gibt es mehrere Optionen, mit denen Sie Ihre Protokolldateien steuern können.

- In der obersten Zeile ganz links befindet sich ein Dropdown-Menü, mit dem Sie zwischen Protokolldateien und Updater-Protokolldateien wechseln können.
  - Protokolldateien - Das A und O bei jedem Support-Fall. Weitere Informationen zu Protokolldateien finden Sie hier.
  - Updater-Protokolldateien - Hier werden die Protokolldateien des Updater-Skripts von Readarr angezeigt.

> Wenn Sie Docker verwenden, ist dies leer, da Sie ein neues Docker-Image herunterladen sollten, um ein Update durchzuführen.
{.is-info}

- Aktualisieren - Dadurch wird die aktuelle Seite aktualisiert und alle neu erstellten Protokolldateien angezeigt.
- Löschen - Dadurch werden alle Protokolle gelöscht und Sie können von vorne beginnen.
- Dateiname - Dadurch wird der Dateiname angezeigt, der mit dem Protokoll verknüpft ist.
- Zuletzt geschrieben - Dies ist die lokale Zeit, zu der diese bestimmte Protokolldatei geschrieben wurde.
  - Readarr verwendet rollende Protokolldateien, die jeweils auf 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer readarr.txt, für die anderen Dateien ist readarr.0.txt die nächstneueste (je höher die Zahl, desto älter ist sie) bis zu insgesamt 51 Protokolldateien. Diese Protokolldatei enthält Einträge für `fatal`, `error`, `warn` und `info`.
  - Wenn das Debug-Protokollierungsniveau aktiviert ist, sind zusätzliche rollende Protokolldateien readarr.debug.txt vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info` und `debug`. Sie decken normalerweise einen Zeitraum von etwa 40 Stunden ab.
  - Wenn das Trace-Protokollierungsniveau aktiviert ist, sind zusätzliche rollende Protokolldateien readarr.trace.txt vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info`, `debug` und `trace`. Aufgrund der Trace-Genauigkeit deckt es normalerweise höchstens ein paar Stunden ab.