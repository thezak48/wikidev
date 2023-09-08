---
title: Prowlarr System
description: 
published: true
date: 2023-05-31T11:54:59.064Z
tags: prowlarr, system
editor: markdown
dateCreated: 2021-08-03T21:21:08.969Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Status](#status)
  - [Gesundheit](#gesundheit)
    - [Systemwarnungen](#systemwarnungen)
      - [Zweig ist kein gültiger Veröffentlichungszweig](#zweig-ist-kein-gültiger-veröffentlichungszweig)
      - [Derzeit installierte SQLite-Version wird nicht unterstützt](#derzeit-installierte-sqlite-version-wird-nicht-unterstützt)
      - [Neues Update verfügbar](#neues-update-verfügbar)
      - [Update kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist](#update-kann-nicht-installiert-werden-da-der-startordner-vom-benutzer-nicht-beschreibbar-ist)
      - [Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern](#aktualisierung-ist-nicht-möglich-um-das-löschen-von-appdata-beim-update-zu-verhindern)
      - [Zweig ist für eine frühere Version](#zweig-ist-für-eine-frühere-version)
      - [Konnte keine Verbindung zu SignalR herstellen](#konnte-keine-verbindung-zu-signalr-herstellen)
      - [Fehler beim Auflösen der IP-Adresse für den konfigurierten Proxy-Host](#fehler-beim-auflösen-der-ip-adresse-für-den-konfigurierten-proxy-host)
      - [Proxy-Test fehlgeschlagen](#proxy-test-fehlgeschlagen)
      - [Systemzeit weicht um mehr als 1 Tag ab](#systemzeit-weicht-um-mehr-als-1-tag-ab)
    - [Download-Clients](#download-clients)
      - [Es ist kein Download-Client verfügbar](#es-ist-kein-download-client-verfügbar)
      - [Kommunikation mit dem Download-Client nicht möglich](#kommunikation-mit-dem-download-client-nicht-möglich)
      - [Download-Clients sind aufgrund eines Fehlers nicht verfügbar](#download-clients-sind-aufgrund-eines-fehlers-nicht-verfügbar)
      - [Schlechte Download-Client-Einstellungen](#schlechte-download-client-einstellungen)
    - [Indexer](#indexer)
      - [Indexer haben keine Definition](#indexer-haben-keine-definition)
      - [Indexer sind veraltet](#indexer-sind-veraltet)
        - [Veraltet aufgrund von Code-Änderungen](#veraltet-aufgrund-von-code-änderungen)
        - [Veraltet aufgrund von Site-Entfernungen](#veraltet-aufgrund-von-site-entfernungen)
      - [Es sind keine Indexer aktiviert](#es-sind-keine-indexer-aktiviert)
      - [Indexer sind aufgrund von Fehlern nicht verfügbar](#indexer-sind-aufgrund-von-fehlern-nicht-verfügbar)
      - [Indexer VIP läuft ab](#indexer-vip-läuft-ab)
      - [Indexer VIP abgelaufen](#indexer-vip-abgelaufen)
    - [Anwendungen](#anwendungen)
      - [Anwendungen sind aufgrund von Fehlern nicht verfügbar](#anwendungen-sind-aufgrund-von-fehlern-nicht-verfügbar)
  - [Festplattenspeicher](#festplattenspeicher)
  - [Über](#über)
  - [Weitere Informationen](#weitere-informationen)
- [Aufgaben](#aufgaben)
  - [Geplant](#geplant)
  - [Warteschlange](#warteschlange)
- [Sicherung](#sicherung)
- [Updates](#updates)
- [Ereignisse](#ereignisse)
- [Protokolldateien](#protokolldateien)

# Status

## Gesundheit

Diese Seite enthält eine Liste von Fehlern bei der Gesundheitsprüfung. Diese Gesundheitsprüfungen werden regelmäßig von Prowlarr durchgeführt und bei bestimmten Ereignissen durchgeführt. Die resultierenden Warnungen und Fehler werden hier aufgelistet, um Ratschläge zur Behebung zu geben.

### Systemwarnungen

#### Zweig ist kein gültiger Veröffentlichungszweig

- Der von Ihnen festgelegte Zweig ist kein gültiger Veröffentlichungszweig. Sie erhalten keine Updates. Ändern Sie ihn bitte in einen der [aktuellen Veröffentlichungszweige](/prowlarr/faq#how-do-i-update-prowlarr).

#### Derzeit installierte SQLite-Version wird nicht unterstützt

- Prowlarr speichert seine Daten in einer SQLite-Datenbank. Die auf Ihrem System installierte SQLite3-Bibliothek ist zu alt. Prowlarr erfordert mindestens Version 3.9.0. Beachten Sie, dass Prowlarr `libSQLite3.so` verwendet, die in einem SQLite3-Upgrade-Paket enthalten sein kann oder auch nicht.

#### Neues Update verfügbar

- Freuen Sie sich, die Entwickler haben ein neues Update veröffentlicht. Dies bedeutet in der Regel großartige neue Funktionen und behobene Fehler (oder?). Offensichtlich haben Sie die automatische Aktualisierung nicht aktiviert, daher müssen Sie herausfinden, wie Sie auf Ihrer Plattform aktualisieren können. Das Drücken der Schaltfläche "Installieren" auf der Seite System => Updates ist wahrscheinlich ein guter Ausgangspunkt.

> Diese Warnung wird nicht angezeigt, wenn Ihre aktuelle Version weniger als 14 Tage alt ist
{.is-info}

#### Update kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist

- Dies bedeutet, dass Prowlarr sich nicht selbst aktualisieren kann. Sie müssen Prowlarr manuell aktualisieren oder die Berechtigungen für das Startverzeichnis von Prowlarr (das Installationsverzeichnis) so einstellen, dass Prowlarr sich selbst aktualisieren kann.

#### Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern

- Prowlarr hat erkannt, dass der AppData-Ordner für Ihr Betriebssystem innerhalb des Verzeichnisses liegt, das die Prowlarr-Binärdateien enthält. Normalerweise wäre dies C:\ProgramData für Windows und ~/.config für Linux.

- Schauen Sie sich bitte unter System => Info an, um die aktuellen AppData- und Startverzeichnisse zu sehen.
- Dies bedeutet, dass Prowlarr sich nicht selbst aktualisieren kann, ohne Datenverlust zu riskieren.
- Wenn Sie Linux verwenden, müssen Sie wahrscheinlich das Home-Verzeichnis für den Benutzer ändern, der Prowlarr ausführt, und den aktuellen Inhalt des Verzeichnisses ~/.config/Prowlarr kopieren, um Ihre Datenbank zu erhalten.

#### Zweig ist für eine frühere Version

- Der in den Einstellungen/Allgemein festgelegte Aktualisierungszweig ist für eine frühere Version von Prowlarr bestimmt. Daher wird die Instanz keine korrekten Aktualisierungsinformationen im System/Updates-Feed sehen und möglicherweise keine neuen Updates erhalten, wenn sie veröffentlicht werden.

#### Konnte keine Verbindung zu SignalR herstellen

- SignalR steuert die dynamischen UI-Updates. Wenn Ihr Browser keine Verbindung zu SignalR auf Ihrem Server herstellen kann, sehen Sie keine Echtzeit-Updates in der Benutzeroberfläche.

- Das häufigste Auftreten davon ist die Verwendung eines Reverse-Proxys oder von Cloudflare
  - Cloudflare benötigt aktiviertes Websockets.
  - Nginx erfordert die folgende Ergänzung zum Location-Block für die App:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Stellen Sie sicher, dass Sie nicht proxy_set_header Connection "Upgrade"; wie in der nginx-Dokumentation vorgeschlagen, einschließen. DAS FUNKTIONIERT NICHT
> Siehe <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

- Für den Apache2-Reverse-Proxy müssen Sie die folgenden Module aktivieren: Proxy, Proxy_http und Proxy_wstunnel. Fügen Sie dann diese Websocket-Tunnel-Direktive zu Ihrer Vhost-Konfiguration hinzu:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:9696/$1 [P,L]
```

Wenn Sie einen Reverse-Proxy unter einem Unterverzeichnis haben, sollte die RewriteRule Ihren Basispfad enthalten, z.B.

```none
RewriteRule /prowlarr/(.*) ws://127.0.0.1:9696/prowlarr/$1 [P,L]
```

Wenn Prowlarr nicht auf demselben Computer wie Ihr Reverse-Proxy läuft, ersetzen Sie 127.0.0.1 durch die entsprechende IP-Adresse/DNS-Namen Ihrer Prowlarr-App.

- Für Caddy (V1) verwenden Sie dies:

> Hinweis: Sie müssen auch die Websocket-Direktive zu Ihrer Prowlarr-Konfiguration hinzufügen{.is-info}

```none
 proxy /prowlarr 127.0.0.1:9696 {
     websocket
     transparent
 }
```

#### Fehler beim Auflösen der IP-Adresse für den konfigurierten Proxy-Host

- Überprüfen Sie Ihre Proxy-Einstellungen und stellen Sie sicher, dass sie korrekt sind.
- Stellen Sie sicher, dass Ihr Proxy aktiv, ausgeführt und erreichbar ist.

#### Proxy-Test fehlgeschlagen

- Ihr konfigurierter Proxy konnte nicht erfolgreich getestet werden. Überprüfen Sie den bereitgestellten HTTP-Fehler und/oder überprüfen Sie die Protokolle für weitere Details.

#### Systemzeit weicht um mehr als 1 Tag ab

- Die Systemzeit weicht um mehr als 1 Tag ab. Geplante Aufgaben können erst korrekt ausgeführt werden, wenn die Zeit korrigiert ist.
- Überprüfen Sie Ihre Systemzeit und stellen Sie sicher, dass sie mit einem autoritativen Zeitserver synchronisiert ist und korrekt ist.

### Download-Clients

#### Es ist kein Download-Client verfügbar

- Für Prowlarr ist ein ordnungsgemäß konfigurierter und aktivierter Download-Client erforderlich, um Medien herunterladen zu können. Da Prowlarr verschiedene Download-Clients unterstützt, sollten Sie feststellen, welcher Ihren Anforderungen am besten entspricht. Wenn Sie bereits einen Download-Client installiert haben, sollten Sie Prowlarr so konfigurieren, dass er ihn verwendet und eine Kategorie erstellt. Siehe Einstellungen => Download-Client.

#### Kommunikation mit dem Download-Client nicht möglich

- Prowlarr konnte nicht mit dem konfigurierten Download-Client kommunizieren. Überprüfen Sie, ob der Download-Client betriebsbereit ist, und überprüfen Sie die URL erneut. Dies kann auch auf einen Authentifizierungsfehler hinweisen.
- Dies liegt in der Regel an einem falsch konfigurierten Download-Client. Dinge, die Sie in der Regel überprüfen können:
- Die IP-Adresse Ihrer Download-Clients, wenn sie auf derselben Bare-Metal-Maschine sind, ist dies in der Regel 127.0.0.1
- Die Portnummer, die Ihr Download-Client verwendet, diese sind mit der Standard-Portnummer ausgefüllt, aber wenn Sie sie geändert haben, müssen Sie dieselbe Nummer in Prowlarr eingeben.
- Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie Ihre Prowlarr-Instanz und Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in der SSL-FAQ.
- Die Verwendung von rutorrent erfordert spezielle Einstellungsänderungen, da es https erfordert.

#### Download-Clients sind aufgrund eines Fehlers nicht verfügbar

- Einer oder mehrere Ihrer Download-Clients reagieren nicht auf Anfragen von Prowlarr. Daher hat Prowlarr beschlossen, die Abfrage des Download-Clients in seinem normalen 1-Minuten-Zyklus vorübergehend zu stoppen, der normalerweise zum Verfolgen von aktiven Downloads und zum Importieren abgeschlossener Downloads verwendet wird. Prowlarr wird jedoch weiterhin versuchen, Downloads an den Client zu senden, wird jedoch höchstwahrscheinlich fehlschlagen.
- Sie sollten System=>Logs überprüfen, um den Grund für die Fehler zu sehen.
- Wenn Sie diesen Download-Client nicht mehr verwenden, deaktivieren Sie ihn in Prowlarr, um Fehler zu vermeiden.

#### Schlechte Download-Client-Einstellungen

- Der Speicherort, an dem Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne Remote-Pfadzuordnung zu wechseln, betreffen.

### Indexer

#### Indexer haben keine Definition

- Ihre Indexer haben keine vorhandene Definition (Datei). Dies liegt in der Regel daran, dass Ihr Indexer nicht mehr unterstützt und entfernt wurde oder die Cardigann-YML-Definition nicht mehr zugänglich ist.

#### Indexer sind veraltet

- Die Definition Ihres Indexers ist veraltet und veraltet. Dies hat zwei Ursachen, die unten angegeben sind.

##### Veraltet aufgrund von Code-Änderungen

- Aufgrund von Code-Änderungen ist der/die Indexer, die/die angegeben ist/sind, veraltet, wie derzeit konfiguriert. Entfernen Sie den Indexer aus Prowlarr und fügen Sie ihn erneut hinzu, um das Problem zu beheben.
- Dies wird in der Regel durch die Konvertierung von APIs oder von YML nach C# oder umgekehrt verursacht.

##### Veraltet aufgrund von Site-Entfernungen

- Bestimmte Websites können darum gebeten werden, aus Prowlarr oder Jackett entfernt zu werden. Diese können dann als veraltet markiert werden.
  - [TVVault](https://github.com/Prowlarr/Prowlarr/issues/573) in [Prowlarr #700](https://github.com/Prowlarr/Prowlarr/pull/700)
  - Audiobookbay hat darum gebeten, dass Prowlarr nicht auf ihre API zugreift
  - Ebookbay hat darum gebeten, dass Prowlarr nicht auf ihre API zugreift
  - Rarbg hat [am 2023-05-31 den Betrieb eingestellt](https://torrentfreak.com/iconic-torrent-site-rarbg-shuts-down-all-content-releases-stop-230531/)

#### Es sind keine Indexer aktiviert

- Prowlarr erfordert Indexer, um neue Veröffentlichungen entdecken zu können. Bitte lesen Sie die Anweisungen im Wiki, wie Sie Indexer hinzufügen können.

#### Indexer sind aufgrund von Fehlern nicht verfügbar

- Bei der Verwendung eines Ihrer Indexer ist ein Fehler aufgetreten. Um die Anzahl der Wiederholungsversuche zu begrenzen, verwendet Prowlarr den Indexer für eine zunehmende Zeitdauer nicht (bis zu 24 Stunden).
- Überprüfen Sie Ereignisse und filtern Sie nach Warnungen, um eine schnelle Vorstellung davon zu bekommen, welche Probleme historisch aufgetreten sind.
- Dieser Mechanismus wird ausgelöst, wenn Prowlarr keine Antwort vom Indexer erhalten konnte (kann durch DNS, Proxy/VPN-Verbindung, Authentifizierung oder ein Indexer-Problem verursacht werden) oder die NZB-/Torrent-Datei nicht vom Indexer abrufen konnte. Bitte überprüfen Sie die Protokolle, um festzustellen, welche Art von Fehler das Problem verursacht.
- Sie können die Warnung verhindern, indem Sie den betroffenen Indexer deaktivieren.
- Führen Sie den Test auf dem Indexer aus, um Prowlarr zu zwingen, den Indexer erneut zu überprüfen. Beachten Sie jedoch, dass die Warnung der Gesundheitsprüfung nicht immer sofort verschwindet.

#### Indexer VIP läuft ab

- Ihr VIP-Abonnement oder Ihre Vorteile für Ihren Indexer laufen innerhalb der nächsten 7 Tage oder weniger ab, basierend auf dem von Ihnen in Prowlarr konfigurierten Ablaufdatum.

#### Indexer VIP abgelaufen

- Ihr VIP-Abonnement oder Ihre Vorteile für Ihren Indexer sind abgelaufen, basierend auf dem von Ihnen in Prowlarr konfigurierten Ablaufdatum.

### Anwendungen

#### Anwendungen sind aufgrund von Fehlern nicht verfügbar

- Bei der Verwendung einer Ihrer Anwendungen ist ein Fehler aufgetreten. Um die Anzahl der Wiederholungsversuche zu begrenzen, verwendet Prowlarr die Anwendung für eine zunehmende Zeitdauer nicht (bis zu 24 Stunden).
- Dieser Mechanismus wird ausgelöst, wenn Prowlarr keine Antwort von der Anwendung erhalten konnte (kann durch DNS, Verbindung, Authentifizierung oder Anwendungsproblem verursacht werden). Bitte überprüfen Sie die Protokolle, um festzustellen, welche Art von Fehler das Problem verursacht.
- Überprüfen Sie Ereignisse und filtern Sie nach Warnungen, um eine schnelle Vorstellung davon zu bekommen, welche Probleme historisch aufgetreten sind.
- Prowlarr kann sich nicht mit der Anwendung synchronisieren, und es ist wahrscheinlich, dass die Anwendung die Indexer von Prowlarr nicht verwenden kann.
- Sie können die Warnung verhindern, indem Sie die betroffene Anwendung deaktivieren.
- Führen Sie den Test auf der Anwendung aus, um Prowlarr zu zwingen, die Anwendung erneut zu überprüfen. Beachten Sie jedoch, dass die Warnung der Gesundheitsprüfung nicht immer sofort verschwindet.

## Festplattenspeicher

In diesem Abschnitt wird der verfügbare Festplattenspeicher angezeigt. In Docker kann dies schwierig sein, da in der Regel der verfügbare Speicherplatz in Ihrem Docker-Image angezeigt wird.

## Über

Hier erfahren Sie mehr über Ihre aktuelle Prowlarr-Installation.

## Weitere Informationen

Home Page: Prowlarr's Homepage
Wiki: Sie sind bereits hier
Reddit: r/prowlarr
Discord: Treten Sie unserem Discord bei
Spenden: Wenn Sie großzügig sind und spenden möchten, klicken Sie hier
Spenden an Sonarr: Wenn Sie großzügig sind und an das Projekt spenden möchten, das alles begonnen hat, klicken Sie hier
Quelle: GitHub
Feature-Anfragen: Haben Sie eine großartige Idee? Teilen Sie sie hier mit.

# Aufgaben

## Geplant

Diese Seite listet alle geplanten Aufgaben auf, die Prowlarr ausführt.

- Anwendungsupdate überprüfen - Dies wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan ausgeführt und überprüft, ob Prowlarr auf der neuesten Version ist. Anschließend wird das Aktualisierungsskript ausgeführt, um Prowlarr zu aktualisieren. Einstellungen => Update

> Hinweis: Wenn Sie Docker verwenden, wird dies Ihren Container nicht aktualisieren, da ein neues Image heruntergeladen werden muss.
{.is-warning}

- Sicherung - Dies führt gemäß einem festgelegten Zeitplan eine Sicherung der Prowlarr-Datenbank durch. Weitere Informationen finden Sie hier. Weitere Informationen zu Sicherungen finden Sie unter System => Backups.
- Gesundheitsprüfung - Die Gesundheitsprüfung wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan durchgeführt und überprüft die allgemeine Gesundheit von Prowlarr. Eine Liste möglicher gesundheitsbezogener Probleme finden Sie im Wiki-Eintrag zu den Gesundheitsprüfungen.
- Hausputz - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan wird dies alle Spinnweben entfernen, die Böden kehren und staubsaugen, wischen, glänzen und sogar schöne, ordentlich gefaltete Notizen nur für Sie machen. Aber den Müll nimmt es nicht mit. Dafür wurde es einfach nicht genug bezahlt.
- Bereinigung der Nachrichten - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan werden diese Nachrichten bereinigt, die in der unteren linken Ecke von Prowlarr angezeigt werden.

> Alle diese Aufgaben können außerhalb ihrer geplanten Zeiten manuell ausgeführt werden, indem Sie auf das Symbol ganz rechts jeder Aufgabe klicken.
{.is-info}

## Warteschlange

Die Warteschlange zeigt Ihnen bevorstehende Aufgaben sowie eine Historie der kürzlich ausgeführten Aufgaben und deren Dauer an.

# Sicherung

> Dieser Abschnitt wird speziell auf die Schaltflächen und den Gesamtpunkt der Seite zugeschnitten sein.
> Wenn Sie jedoch Informationen zur Sicherung/Wiederherstellung Ihrer Prowlarr-Instanz suchen, [sehen Sie sich unsere FAQ an](/prowlarr/faq).
{.is-info}

Im Bereich "Sicherung" werden Ihnen frühere Sicherungen angezeigt (sofern Sie keine frische Installation haben, die noch keine Sicherungen erstellt hat).

Hier haben Sie oben auf dem Bildschirm zwei Optionen:

- Jetzt sichern - Diese Option löst eine manuelle Sicherung der Prowlarr-Datenbank aus.
- Sicherung wiederherstellen - Dadurch wird ein neuer Bildschirm geöffnet, um eine frühere Sicherung wiederherzustellen.
Wenn Sie "Datei auswählen" auswählen, wird Ihr Browser aufgefordert, einen Dialog zur Wiederherstellung aus einer Prowlarr-Zip-Sicherung zu öffnen.

Schließlich können Sie, wenn Sie frühere Sicherungen haben und diese von Prowlarr herunterladen möchten, um sie an einem anderen Ort zu speichern, einfach eine dieser Dateien auswählen, um sie herunterzuladen.
Rechts neben jedem vorherigen Download haben Sie zwei Optionen.

- Eins - Zur Wiederherstellung aus einer früheren Sicherung - Dadurch wird ein neues Fenster geöffnet, um zu bestätigen, dass Sie aus dieser Sicherung wiederherstellen möchten.
- Zwei - Um eine frühere Sicherung zu löschen

# Updates

Auf dem Update-Bildschirm werden die letzten 5 Updates angezeigt, die durchgeführt wurden, sowie die aktuelle Version, die Sie verwenden.
Auf dieser Seite werden auch die Update-Notizen der Entwickler angezeigt, in denen beschrieben wird, was an Prowlarr behoben oder hinzugefügt wurde (Freut euch!)

> Ein Wartungs-Release enthält Fehlerbehebungen und verschiedene Verbesserungen. Werfen Sie einen Blick auf den Commit-Verlauf für Details.
{.is-info}

# Ereignisse

Der Ereignis-Tab zeigt Ihnen, was in Ihrem Prowlarr passiert ist. Dies kann zur Diagnose von leichten Problemen verwendet werden. Dies ersetzt jedoch nicht die in Logging besprochenen Trace-Logs. Ereignisse entsprechen den INFO-Logs.

- Komponenten - Diese Spalte zeigt an, welche Komponente in Prowlarr ausgelöst wurde.
- Nachricht - Diese Spalte zeigt an, welche Nachricht von der Komponente aus der vorherigen Spalte gesendet wurde.
- Zahnrad-Symbol - Diese Option ermöglicht es Ihnen, festzulegen, wie viele Komponenten/Nachrichten pro Seite angezeigt werden (Standardmäßig sind es 50).
- Optionen oben auf der Seite
  - Aktualisieren - Diese Option aktualisiert die aktuelle Seite und lädt ein neues Ereignisprotokoll.
  - Löschen - Dadurch wird das aktuelle Ereignisprotokoll gelöscht und Sie können von vorne beginnen.

# Protokolldateien

Auf dieser Seite können Sie die aktuellen Protokolldateien für Prowlarr herunterladen und anzeigen.

In der obersten Zeile gibt es mehrere Optionen, mit denen Sie Ihre Protokolldateien steuern können.

- In der obersten Zeile ganz links befindet sich ein Dropdown-Menü, mit dem Sie zwischen Protokolldateien und Updater-Protokolldateien wechseln können.
  - Protokolldateien - Das A und O bei jedem Support-Problem, weitere Informationen zu Protokolldateien finden Sie hier.
  - Updater-Protokolldateien - Hier werden die Protokolldateien des Prowlarr-Updater-Skripts angezeigt.

> Wenn Sie Docker verwenden, ist dies leer, da Sie ein Update durch Herunterladen eines neuen Docker-Images durchführen sollten.
{.is-info}

- Aktualisieren - Dadurch wird die aktuelle Seite aktualisiert und alle neu erstellten Protokolle angezeigt.
- Löschen - Dadurch werden alle Protokolle gelöscht und Sie können von vorne beginnen.
- Dateiname - Hier wird der Dateiname des Protokolls angezeigt.
- Zuletzt geschrieben - Dies ist die lokale Zeit, zu der diese bestimmte Protokolldatei geschrieben wurde.
  - Prowlarr verwendet rollende Protokolldateien, die auf jeweils 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer prowlarr.txt, für die anderen Dateien ist prowlarr.0.txt die nächstneuere (je höher die Zahl, desto älter ist sie) bis zu insgesamt 51 Protokolldateien. Diese Protokolldatei enthält Einträge für `fatal`, `error`, `warn` und `info`.
  - Wenn der Debug-Protokollierungspegel aktiviert ist, sind zusätzliche rollende Protokolldateien prowlarr.debug.txt vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info` und `debug`. Sie decken normalerweise einen Zeitraum von ca. 40 Stunden ab.
  - Wenn der Trace-Protokollierungspegel aktiviert ist, sind zusätzliche rollende Protokolldateien prowlarr.trace.txt vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info`, `debug` und `trace`. Aufgrund der ausführlichen Protokollierung deckt es normalerweise höchstens ein paar Stunden ab.