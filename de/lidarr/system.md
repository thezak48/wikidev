# Markdown-Syntax

Markdown ist eine einfache und intuitive Syntax zum Formatieren von Text. Es wurde entwickelt, um das Schreiben von Inhalten für das Web zu erleichtern. In diesem Dokument werden die grundlegenden Elemente der Markdown-Syntax erläutert.

## Überschriften

Sie können Überschriften mit einer oder mehreren `#`-Zeichen erstellen. Die Anzahl der `#`-Zeichen bestimmt die Ebene der Überschrift. Zum Beispiel:

```markdown
# Überschrift der Ebene 1
## Überschrift der Ebene 2
### Überschrift der Ebene 3
```

## Absätze

Absätze werden durch eine leere Zeile voneinander getrennt. Wenn Sie einen neuen Absatz erstellen möchten, fügen Sie einfach eine leere Zeile ein.

```markdown
Dies ist der erste Absatz.

Dies ist der zweite Absatz.
```

## Fett und kursiv

Sie können Text fett oder kursiv formatieren, indem Sie ihn mit Sternchen (`*`) oder Unterstrichen (`_`) umgeben.

```markdown
Dieser Text ist *fett*.
Dieser Text ist _kursiv_.
```

## Links

Sie können Links erstellen, indem Sie den Linktext in eckige Klammern (`[]`) und die URL in runde Klammern (`()`) setzen.

```markdown
Dies ist ein [Link](https://www.example.com).
```

## Listen

Sie können geordnete und ungeordnete Listen erstellen.

Ungeordnete Liste:

```markdown
- Element 1
- Element 2
- Element 3
```

Geordnete Liste:

```markdown
1. Element 1
2. Element 2
3. Element 3
```

## Codeblöcke

Sie können Codeblöcke erstellen, indem Sie den Code mit drei Backticks (\```) umgeben.

```markdown
```
function sayHello() {
    console.log("Hello, world!");
}
```
```

## Zitate

Sie können Zitate erstellen, indem Sie den Text mit einem `>`-Zeichen am Anfang jeder Zeile kennzeichnen.

```markdown
> Dies ist ein Zitat.
> Es kann aus mehreren Zeilen bestehen.
```

## Horizontale Linien

Sie können horizontale Linien erstellen, indem Sie drei oder mehr Bindestriche (`-`), Unterstriche (`_`) oder Sternchen (`*`) in einer Zeile verwenden.

```markdown
---
```

Das waren die grundlegenden Elemente der Markdown-Syntax. Sie können weitere fortgeschrittene Funktionen wie Tabellen, Bilder und mehr erkunden, indem Sie die offizielle Markdown-Dokumentation lesen.

---
title: Lidarr System
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, system
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Status](#status)
  - [Gesundheit](#gesundheit)
    - [Systemwarnungen](#systemwarnungen)
      - [Zweig ist kein gültiger Veröffentlichungszweig](#zweig-ist-kein-gültiger-veröffentlichungszweig)
      - [Aktualisierung auf .NET-Version](#aktualisierung-auf-net-version)
        - [Behebung von Docker-Installationen](#behebung-von-docker-installationen)
        - [Behebung von eigenständigen Installationen](#behebung-von-eigenständigen-installationen)
      - [Derzeit installierte Mono-Version ist veraltet und wird nicht unterstützt](#derzeit-installierte-mono-version-ist-veraltet-und-wird-nicht-unterstützt)
      - [Derzeit installierte SQLite-Version wird nicht unterstützt](#derzeit-installierte-sqlite-version-wird-nicht-unterstützt)
      - [Neues Update verfügbar](#neues-update-verfügbar)
      - [Update kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist](#update-kann-nicht-installiert-werden-da-der-startordner-vom-benutzer-nicht-beschreibbar-ist)
      - [Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern](#aktualisierung-ist-nicht-möglich-um-das-löschen-von-appdata-beim-update-zu-verhindern)
      - [Zweig ist für eine frühere Version](#zweig-ist-für-eine-frühere-version)
      - [Konnte keine Verbindung zu SignalR herstellen](#konnte-keine-verbindung-zu-signalr-herstellen)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [Konnte die IP-Adresse für den konfigurierten Proxy-Host nicht auflösen](#konnte-die-ip-adresse-für-den-konfigurierten-proxy-host-nicht-auflösen)
      - [Proxy-Test fehlgeschlagen](#proxy-test-fehlgeschlagen)
      - [Systemzeit weicht um mehr als 1 Tag ab](#systemzeit-weicht-um-mehr-als-1-tag-ab)
      - [Mono Legacy TLS aktiviert](#mono-legacy-tls-aktiviert)
      - [Mono- und x86-Builds werden eingestellt](#mono-und-x86-builds-werden-eingestellt)
      - [FPcalc muss aktualisiert werden](#fpcalc-muss-aktualisiert-werden)
    - [Download-Clients](#download-clients)
      - [Es ist kein Download-Client verfügbar](#es-ist-kein-download-client-verfügbar)
      - [Kommunikation mit dem Download-Client nicht möglich](#kommunikation-mit-dem-download-client-nicht-möglich)
      - [Download-Clients sind aufgrund eines Fehlers nicht verfügbar](#download-clients-sind-aufgrund-eines-fehlers-nicht-verfügbar)
      - [Abgeschlossene Download-Verarbeitung aktivieren](#abgeschlossene-download-verarbeitung-aktivieren)
      - [Docker schlechte Remote-Pfadzuordnung](#docker-schlechte-remote-pfadzuordnung)
      - [In Stammordner herunterladen](#in-stammordner-herunterladen)
      - [Fehlerhafte Download-Client-Einstellungen](#fehlerhafte-download-client-einstellungen)
      - [Fehlerhafte Remote-Pfadzuordnung](#fehlerhafte-remote-pfadzuordnung)
      - [Berechtigungsfehler](#berechtigungsfehler)
      - [Remote-Datei wurde während der Verarbeitung teilweise entfernt](#remote-datei-wurde-während-der-verarbeitung-teilweise-entfernt)
      - [Remote-Pfad wird verwendet und Import fehlgeschlagen](#remote-pfad-wird-verwendet-und-import-fehlgeschlagen)
    - [Abgeschlossene/fehlgeschlagene Download-Verarbeitung](#abgeschlossen-fehlgeschlagene-download-verarbeitung)
      - [Abgeschlossene Download-Verarbeitung ist deaktiviert](#abgeschlossene-download-verarbeitung-ist-deaktiviert)
    - [Indexer](#indexer)
      - [Keine Indexer verfügbar mit aktivierter automatischer Suche, Lidarr liefert keine automatischen Suchergebnisse](#keine-indexer-verfügbar-mit-aktivierter-automatischer-suche-lidarr-liefert-keine-automatischen-suchergebnisse)
      - [Keine Indexer verfügbar mit aktivierter RSS-Synchronisierung, Lidarr greift nicht automatisch auf neue Veröffentlichungen zu](#keine-indexer-verfügbar-mit-aktivierter-rss-synchronisierung-lidarr-greift-nicht-automatisch-auf-neue-veröffentlichungen-zu)
      - [Keine Indexer aktiviert](#keine-indexer-aktiviert)
    - [Aktivierte Indexer unterstützen keine Suche](#aktivierte-indexer-unterstützen-keine-suche)
      - [Keine Indexer verfügbar mit aktivierter interaktiver Suche](#keine-indexer-verfügbar-mit-aktivierter-interaktiver-suche)
      - [Indexer sind aufgrund von Fehlern nicht verfügbar](#indexer-sind-aufgrund-von-fehlern-nicht-verfügbar)
      - [Jackett Alle Endpunkte verwendet](#jackett-alle-endpunkte-verwendet)
        - [Lösungen](#lösungen)
    - [Künstlerordner](#künstlerordner)
      - [Fehlender Stammordner](#fehlender-stammordner)
      - [Listen sind aufgrund von Fehlern nicht verfügbar](#listen-sind-aufgrund-von-fehlern-nicht-verfügbar)
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

> Warnung: Diese Seite ist eine Arbeit in Bearbeitung und derzeit ein Entwurf basierend auf Readarr
{.is-danger}

# Status

## Gesundheit

Diese Seite enthält eine Liste von Fehlern bei der Gesundheitsprüfung. Diese Gesundheitsprüfungen werden regelmäßig von Lidarr durchgeführt und bei bestimmten Ereignissen durchgeführt. Die resultierenden Warnungen und Fehler werden hier aufgelistet, um Ratschläge zur Behebung zu geben.

### Systemwarnungen

#### Zweig ist kein gültiger Veröffentlichungszweig

Der von Ihnen festgelegte Zweig ist kein gültiger Veröffentlichungszweig. Sie erhalten keine Updates. Ändern Sie ihn bitte in einen der [aktuellen Veröffentlichungszweige](/lidarr/faq#how-do-i-update-lidarr)

#### Aktualisierung auf .NET-Version

{#update-to-net-core-version}

- Neuere Versionen von Lidarr sind für .NET6 oder neuer ausgelegt. Nach der Veröffentlichung von Version 1.0 werden keine Legacy-Mono-Builds mehr bereitgestellt. Sie verwenden eine dieser Legacy-Builds, aber Ihre Plattform unterstützt .NET.

##### Behebung von Docker-Installationen

- Ziehen Sie Ihren Container erneut

##### Behebung von eigenständigen Installationen

- Sichern Sie Ihre vorhandene Konfiguration vor dem nächsten Schritt.
- Dies sollte nur auf Linux-Hosts geschehen. Installieren Sie das .NET-Runtime oder den SDK nicht von Microsoft.
- Laden Sie zur Behebung die richtige Version für Ihre Architektur herunter und ersetzen Sie Ihre vorhandenen Binärdateien (Anwendung)
- Kurz gesagt müssen Sie Ihre vorhandenen Binärdateien (Inhalt oder Ordner von /opt/Lidarr) löschen und durch den Inhalt der gerade heruntergeladenen .tar.gz-Datei ersetzen.

> LÖSCHEN SIE NICHT EINFACH DEN DOWNLOAD ÜBER IHREN VORHANDENEN BINÄREN.
> SIE MÜSSEN ZUERST DIE ALTEN LÖSCHEN.
{.is-warning}

- Das folgende Skript wurde von der Community entwickelt, um Ihre Mono-Installation zu entfernen und durch die .NET-Installation zu ersetzen. Beiträge und Korrekturen sind willkommen.
- Dies setzt voraus, dass Sie sich auf dem `master` Lidarr-Zweig befinden, aktualisieren Sie die Variable bei Bedarf
- Dies setzt voraus, dass Lidarr als Benutzer `lidarr` ausgeführt wird, aktualisieren Sie die Variablen bei Bedarf
- Dies setzt voraus, dass Lidarr unter `/opt/Lidarr` installiert ist, aktualisieren Sie die Variablen bei Bedarf

```bash
#!/bin/bash
## Benutzervariablen
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /Benutzervariablen
app="lidarr"
ARCH=$(dpkg --print-architecture)
# Stop \*arr
sudo systemctl stop $app
# Architektur abrufen
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arch wird nicht unterstützt"
    exit 1
    ;;
esac
echo "Herunterladen..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installationsdateien heruntergeladen und extrahiert"
echo "Vorhandene Installation verschieben"
sudo mv "$installdir/" "$installdir.old/"
echo "Installieren..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App installiert"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### Derzeit installierte Mono-Version ist veraltet und wird nicht unterstützt

- Lidarr ist in .NET geschrieben und erfordert Mono, um auf sehr alten ARM-Prozessoren ausgeführt zu werden. Beachten Sie, dass Mono-Builds nach Version 1.0 nicht mehr unterstützt werden.
- Mono 5.20 ist das absolute Minimum für Lidarr.
- Das Upgrade-Verfahren für Mono variiert je nach Plattform.

#### Derzeit installierte SQLite-Version wird nicht unterstützt

- Lidarr speichert seine Daten in einer SQLite-Datenbank. Die auf Ihrem System installierte SQLite3-Bibliothek ist zu alt. Lidarr erfordert mindestens Version 3.9.0. Beachten Sie, dass Lidarr `libSQLite3.so` verwendet, die in einem SQLite3-Upgrade-Paket enthalten sein kann oder auch nicht.

#### Neues Update verfügbar

- Freuen Sie sich, die Entwickler haben ein neues Update veröffentlicht. Dies bedeutet in der Regel großartige neue Funktionen und behobene Fehler (richtig?). Offensichtlich haben Sie die automatische Aktualisierung nicht aktiviert, sodass Sie herausfinden müssen, wie Sie auf Ihrer Plattform aktualisieren können. Das Drücken der Schaltfläche "Installieren" auf der Seite `System => Updates` ist wahrscheinlich ein guter Ausgangspunkt.

> Diese Warnung wird nicht angezeigt, wenn Ihre aktuelle Version weniger als 14 Tage alt ist
{.is-info}

#### Update kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist

- Dies bedeutet, dass Lidarr sich nicht selbst aktualisieren kann. Sie müssen Lidarr manuell aktualisieren oder die Berechtigungen für das Startverzeichnis von Lidarr (das Installationsverzeichnis) so einstellen, dass Lidarr sich selbst aktualisieren kann.

#### Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern

- Lidarr hat erkannt, dass der AppData-Ordner für Ihr Betriebssystem im Verzeichnis liegt, das die Lidarr-Binärdateien enthält. Normalerweise wäre es `C:\ProgramData` für Windows und `~/.config` für Linux.

- Schauen Sie sich `System => Info` an, um die aktuellen AppData- und Startordner anzuzeigen.
- Dies bedeutet, dass Lidarr sich nicht selbst aktualisieren kann, ohne Datenverlust zu riskieren.
- Wenn Sie Linux verwenden, müssen Sie wahrscheinlich das Home-Verzeichnis für den Benutzer ändern, der Lidarr ausführt, und den aktuellen Inhalt des Verzeichnisses `~/.config/Lidarr` kopieren, um Ihre Datenbank zu erhalten.

#### Zweig ist für eine frühere Version

- Der in `Einstellungen => Allgemein` festgelegte Aktualisierungszweig ist für eine frühere Version von Lidarr bestimmt. Daher sieht die Instanz keine korrekten Aktualisierungsinformationen im `System => Updates`-Feed und erhält möglicherweise keine neuen Updates bei Veröffentlichung.

#### Konnte keine Verbindung zu SignalR herstellen

- SignalR steuert die dynamischen UI-Updates. Wenn Ihr Browser keine Verbindung zu SignalR auf Ihrem Server herstellen kann, sehen Sie keine Echtzeit-Updates in der Benutzeroberfläche.

- Das häufigste Auftreten davon ist die Verwendung eines Reverse-Proxys oder von Cloudflare
- Cloudflare benötigt aktiviertes Websockets.

##### NGINX

- Nginx erfordert die folgende Ergänzung zum Ortungsblock für die App:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Stellen Sie sicher, dass Sie `proxy_set_header Connection "Upgrade";` nicht wie in der nginx-Dokumentation vorgeschlagen einschließen. DAS FUNKTIONIERT NICHT
> Siehe <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- Für den Apache2-Reverse-Proxy müssen Sie die folgenden Module aktivieren: Proxy, Proxy_http und Proxy_wstunnel. Fügen Sie dann diese Websocket-Tunnelanweisung zu Ihrer Vhost-Konfiguration hinzu:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- Für Caddy (V1) verwenden Sie dies:
- Hinweis: Sie müssen auch die Websocket-Anweisung zu Ihrer Lidarr-Konfiguration hinzufügen

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### Konnte die IP-Adresse für den konfigurierten Proxy-Host nicht auflösen

- Überprüfen Sie Ihre Proxy-Einstellungen und stellen Sie sicher, dass sie korrekt sind
- Stellen Sie sicher, dass Ihr Proxy aktiv, ausgeführt und erreichbar ist

#### Proxy-Test fehlgeschlagen

- Ihr konfigurierter Proxy konnte nicht erfolgreich getestet werden. Überprüfen Sie den bereitgestellten HTTP-Fehler und/oder überprüfen Sie die Protokolle, um weitere Details zu erhalten.

#### Systemzeit weicht um mehr als 1 Tag ab

- Die Systemzeit weicht um mehr als 1 Tag ab. Geplante Aufgaben können möglicherweise nicht ordnungsgemäß ausgeführt werden, bis die Zeit korrigiert ist.
- Überprüfen Sie Ihre Systemzeit und stellen Sie sicher, dass sie mit einem autoritativen Zeitserver synchronisiert ist und korrekt ist.

#### Mono Legacy TLS aktiviert

- Mono 4.x TLS-Workaround ist immer noch aktiviert. Erwägen Sie das Entfernen der Umgebungsoption `MONO_TLS_PROVIDER=legacy`

#### Mono- und x86-Builds werden eingestellt

- Mono- und x86-Builds werden in der nächsten Version der Anwendung nicht mehr unterstützt. Wenn Sie diesen Fehler erhalten, verwenden Sie entweder die Mono-Version der Anwendung oder die x86-Version. Aufgrund der zunehmenden Schwierigkeiten bei der Entwicklung von Unterstützung für diese Legacy-Versionen werden wir ihre Unterstützung einstellen und somit auch ihre zukünftigen Veröffentlichungen. Es wird daher empfohlen, auf ein unterstütztes Betriebssystem zu aktualisieren, das weder x86 noch Mono erfordert. Möglicherweise können Sie auch Docker für Ihre Anforderungen verwenden.

#### FPcalc muss aktualisiert werden

{#fpcalc-upgrade}

- Lidarr verwendet die Chromaprint-Audiofingerprinting, um Tracks zu identifizieren. Dies hängt von einer externen Binärdatei `fpcalc` ab, die mit Lidarr v1 für Windows, Linux und macOS verteilt wird, aber auf FreeBSD unabhängig bereitgestellt werden muss.
- Stellen Sie sicher, dass die mit Lidarr gebündelte fpcalc-Binärdatei ausführbar ist (Berechtigungen 755). Diese befindet sich im Installationsverzeichnis von Lidarr (z. B. `/opt/Lidarr/fpcalc`). Wenn sie nicht ausführbar ist, korrigieren Sie die Berechtigungen mit dem folgenden Befehl und starten Sie dann Lidarr neu.
  - Beachten Sie, dass für die Korrektur möglicherweise `sudo` erforderlich ist oder Ihr Pfad zum Binärordner von Lidarr je nach Umgebung und Setup unterschiedlich sein kann.

```bash
chmod +x /opt/Lidarr/fpcalc
```

> Die folgenden Informationen gelten nur für Legacy-Builds von v0.8.0.
{.is-info}

- Um dies in einer nativen Linux-Instanz zu beheben, installieren Sie das entsprechende Paket mit Ihrem Paketmanager und stellen Sie sicher, dass fpcalc in Ihrem PATH enthalten ist (dies kann mit `which fpcalc` überprüft werden, um den richtigen Speicherort von fpcalc zurückzugeben):

| Distribution  |       Paket        |
| :-----------: | :------------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### Download-Clients

#### Es ist kein Download-Client verfügbar

- Ein ordnungsgemäß konfigurierter und aktivierter Download-Client ist erforderlich, damit Lidarr Medien herunterladen kann. Da Lidarr verschiedene Download-Clients unterstützt, sollten Sie herausfinden, welcher Ihren Anforderungen am besten entspricht. Wenn Sie bereits einen Download-Client installiert haben, sollten Sie Lidarr so konfigurieren, dass er ihn verwendet, und eine Kategorie erstellen. Siehe `Einstellungen => Download-Client`.

#### Kommunikation mit dem Download-Client nicht möglich

- Lidarr konnte nicht mit dem konfigurierten Download-Client kommunizieren. Überprüfen Sie, ob der Download-Client betriebsbereit ist, und überprüfen Sie die URL erneut. Dies kann auch auf einen Authentifizierungsfehler hinweisen.
- Dies liegt in der Regel an einem falsch konfigurierten Download-Client. Dinge, die Sie in der Regel überprüfen können:
  - IP-Adresse Ihres Download-Clients - Wenn alles auf derselben Bare-Metal-Maschine liegt, ist dies in der Regel `127.0.0.1`
  - Die Portnummer, die Ihr Download-Client verwendet - Diese sind mit der Standard-Portnummer ausgefüllt, aber wenn Sie sie geändert haben, müssen Sie dieselbe Nummer in Lidarr eingeben.
  - Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie Ihre Lidarr-Instanz und Ihren Download-Client in einem lokalen Netzwerk verwenden (d. H. Über einfaches HTTP). Weitere Informationen finden Sie in der SSL-FAQ.

#### Download-Clients sind aufgrund eines Fehlers nicht verfügbar

- Einer oder mehrere Ihrer Download-Clients reagieren nicht auf Anfragen von Lidarr. Daher hat Lidarr beschlossen, die Abfrage des Download-Clients in seinem normalen 1-Minuten-Zyklus vorübergehend zu stoppen, der normalerweise zum Verfolgen von aktiven Downloads und zum Importieren abgeschlossener Downloads verwendet wird. Lidarr wird jedoch weiterhin versuchen, Downloads an den Client zu senden, wird dies aber höchstwahrscheinlich nicht schaffen.
- Sie sollten `System=>Logs` überprüfen, um den Grund für die Fehler zu sehen.
- Wenn Sie diesen Download-Client nicht mehr verwenden, deaktivieren Sie ihn in Lidarr, um Fehler zu vermeiden.

#### Abgeschlossene Download-Verarbeitung aktivieren

- Lidarr erfordert die Aktivierung der abgeschlossenen Download-Verarbeitung, um Dateien importieren zu können, die vom Download-Client heruntergeladen wurden. Es wird empfohlen, die abgeschlossene Download-Verarbeitung zu aktivieren. (Die abgeschlossene Download-Verarbeitung ist standardmäßig für neue Benutzer aktiviert.)

#### Docker schlechte Remote-Pfadzuordnung

- Dieser Fehler ist in der Regel mit schlechten Docker-Pfaden in Ihrem Download-Client oder Lidarr verbunden

- Ein Beispiel für schlechte (inkonsistente) Pfade wäre:
  - Download-Client: `/mnt/user/downloads:/downloads`
  - Lidarr:   `/mnt/user/downloads:/data`
- In diesem Beispiel legt der Download-Client seine Downloads in `/downloads` ab und teilt Lidarr mit, dass das fertige Buch in `/downloads` ist, wenn es abgeschlossen ist. Lidarr kommt dann vorbei und sagt "Okay, cool, lass mich in `/downloads` nachsehen." Nun, in Lidarr haben Sie keinen `/downloads`-Pfad zugewiesen, sondern einen `/data`-Pfad zugewiesen, sodass dieser Fehler auftritt.
- Die einfachste Lösung dafür ist KONSISTENZ - wenn Sie ein Schema in Ihrem Download-Client verwenden, verwenden Sie es durchgehend.

- Team Lidarr ist ein großer Fan von einfach `/data` zu verwenden.

  - Download-Client: `/mnt/user/data/downloads:/data/downloads`
  - Lidarr: `/mnt/user/data:/data`

- Jetzt können Sie in Ihrem Download-Client angeben, wo Sie Ihre Downloads in `/data` platzieren möchten. Dies variiert je nach Client, aber Sie sollten ihm sagen können "Ja, Download-Client, platziere meine Dateien in `/data/downloads/movies`" und da Sie in Lidarr `/data` verwendet haben, wenn der Download-Client Lidarr mitteilt, dass er fertig ist, wird Lidarr kommen und sagen "Super, ich habe ein `/data` und ich kann auch `/data/downloads/movies` sehen, alles ist in Ordnung."
- Es gibt viele großartige Anleitungen: Unser Wiki [Docker Guide](/docker-guide) und TRaSH's [Hardlinks und Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). In diesen Anleitungen wird zwar der Schwerpunkt auf Hardlinks und Atomic-Moves gelegt, aber das allgemeine Konzept von Containern und der Funktionsweise der Pfadzuordnung ist der Kern dieser Diskussionen.
- Wenn Sie Betriebssysteme überschreiten oder nativ und Docker verwenden, benötigen Sie eine Remote-Pfadzuordnung. Weitere Informationen finden Sie in [TRaSH's Remote Path Guide für Radarr](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) und [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/).

#### In Stammordner herunterladen

{#downloads-in-root-folder}

- In der Anwendung wird ein Stammordner als der konfigurierte Medienbibliotheksordner definiert. Dies ist nicht der Stammordner eines Laufwerks. Ihr Download-Client lädt unvollständige oder abgeschlossene Downloads (oder verschiebt abgeschlossene Downloads) in Ihren Stamm (Bibliotheks-) Ordner.
- Dies führt häufig zu Problemen, einschließlich Datenverlust, und sollte nicht durchgeführt werden. Ändern Sie Ihren Download-Client so, dass er keine Downloads in Ihren Stammordner platziert. Beachten Sie, dass "Platzieren" auch bedeutet, dass Ihre Download-Client-Kategorie auf Ihren Stammordner eingestellt ist oder wenn NZBGet/SABnzbd sortiert ist und in Ihren Stammordner sortiert wird.
- Bitte beachten Sie, dass diese Überprüfung alle definierten/konfigurierten Stammordner umfasst, nicht nur die derzeit verwendeten Stammordner. Mit anderen Worten, der Ordner, in den Ihr Download-Client herunterlädt oder abgeschlossene Downloads verschiebt, sollte nicht derselbe Ordner sein, den Sie als Ihren Stamm-/Bibliotheks-/endgültigen Medienzielordner in der *arr-Anwendung konfiguriert haben.
- Konfigurierte Stammordner (auch als Bibliotheksordner bezeichnet) finden Sie unter [Einstellungen => Medienverwaltung => Stammordner](/lidarr/settings/#root-folders)
- Ein Beispiel ist, wenn Ihre Downloads in `\data\downloads` gehen, dann haben Sie einen Stammordner als `\data\downloads` festgelegt.
- Es wird vorgeschlagen, Pfade wie `\data\media\` für Ihren Stammordner/Bibliothek und `\data\downloads\` für Ihre Downloads zu verwenden.
- Lesen Sie unseren [Docker Guide](/docker-guide) und TRaSH's [Hardlinks und Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) für weitere Informationen zur korrekten und optimalen Pfadkonfiguration. Beachten Sie, dass die Konzepte für Docker und Nicht-Docker gelten

> Ihr Download-Ordner, in dem Ihr Download-Client die Downloads platziert, und Ihr Stamm-/Bibliotheksordner MÜSSEN getrennt sein. \*Arr importiert die Datei(en) aus dem Download-Ordner Ihres Download-Clients in Ihre Bibliothek. Der Download-Client sollte nichts verschieben oder herunterladen, das in Ihre Bibliothek gehört.
{.is-warning}

#### Fehlerhafte Download-Client-Einstellungen

- Der Speicherort, an dem Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne Remote-Pfadzuordnung zu wechseln, betreffen.

#### Fehlerhafte Remote-Pfadzuordnung

- Der Speicherort, an dem Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne Remote-Pfadzuordnung zu wechseln, betreffen. Weitere Informationen finden Sie in [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/).

#### Berechtigungsfehler

- Lidarr (oder der Benutzer, unter dem Lidarr ausgeführt wird) kann nicht auf den Speicherort zugreifen, an dem Ihr Download-Client Dateien herunterlädt. Dies ist in der Regel ein Berechtigungsproblem.

#### Remote-Datei wurde während der Verarbeitung teilweise entfernt

- Eine über einen Remote-Pfadzugriff erreichbare Datei scheint vor Abschluss der Verarbeitung entfernt worden zu sein.

#### Remote-Pfad wird verwendet und Import fehlgeschlagen

- Überprüfen Sie die Protokolle für weitere Informationen. Weitere Informationen finden Sie in unseren [Problembehandlungsanleitungen](/lidarr/troubleshooting).

### Abgeschlossene/fehlgeschlagene Download-Verarbeitung

#### Abgeschlossene Download-Verarbeitung ist deaktiviert

- Lidarr erfordert die Aktivierung der "Abgeschlossene Download-Verarbeitung", um Dateien importieren zu können, die vom Download-Client heruntergeladen wurden. Es wird empfohlen, die "Abgeschlossene Download-Verarbeitung" zu aktivieren. (Sie ist standardmäßig für neue Benutzer aktiviert.)

### Indexer

#### Keine Indexer verfügbar mit aktivierter automatischer Suche, Lidarr liefert keine automatischen Suchergebnisse

- Einfach ausgedrückt haben Sie keine Ihrer Indexer so eingestellt, dass automatische Suchen möglich sind
- Gehen Sie zu `Einstellungen => Indexer`, wählen Sie einen Indexer aus, für den Sie automatische Suchen zulassen möchten, und klicken Sie dann auf Speichern.

#### Keine Indexer verfügbar mit aktivierter RSS-Synchronisierung, Lidarr greift nicht automatisch auf neue Veröffentlichungen zu

- Lidarr verwendet den RSS-Feed, um neue Veröffentlichungen zu erfassen, wenn sie auftreten. Weitere Informationen dazu finden Sie hier
- Um dieses Problem zu beheben, gehen Sie zu `Einstellungen => Indexer`, wählen Sie einen Indexer aus, den Sie haben, und aktivieren Sie die RSS-Synchronisierung

#### Keine Indexer aktiviert

- Lidarr erfordert Indexer, um neue Veröffentlichungen entdecken zu können. Bitte lesen Sie das Wiki, um Anweisungen zum Hinzufügen von Indexern zu erhalten.

#### Aktivierte Indexer unterstützen keine Suche

- Keiner der von Ihnen aktivierten Indexer unterstützt die Suche. Dies bedeutet, dass Lidarr nur über die RSS-Feeds neue Veröffentlichungen finden kann. Das Suchen nach Filmen (entweder automatische Suche oder manuelle Suche) liefert niemals Ergebnisse. Die einzige Möglichkeit, dies zu beheben, besteht darin, einen weiteren Indexer hinzuzufügen.

#### Keine Indexer verfügbar mit aktivierter interaktiver Suche

- Keiner der von Ihnen aktivierten Indexer unterstützt die interaktive Suche. Dies bedeutet, dass die Anwendung nur über die RSS-Feeds oder eine automatische Suche neue Veröffentlichungen finden kann.

#### Indexer sind aufgrund von Fehlern nicht verfügbar

- Fehler treten auf, während Lidarr versucht, einen Ihrer Indexer zu verwenden. Um die Anzahl der Wiederholungsversuche zu begrenzen, verwendet Lidarr den Indexer für eine zunehmende Zeitspanne nicht (bis zu 24 Stunden).
- Dieser Mechanismus wird ausgelöst, wenn Lidarr keine Antwort vom Indexer erhalten konnte (kann durch DNS, Proxy/VPN-Verbindung, Authentifizierung oder ein Indexer-Problem verursacht werden) oder die NZB-/Torrent-Datei nicht vom Indexer abrufen konnte.
- Überprüfen Sie die Protokolle, um festzustellen, welche Art von Fehler das Problem verursacht.
- Sie können die Warnung verhindern, indem Sie den betroffenen Indexer deaktivieren.
- Führen Sie den Test auf dem Indexer aus, um Lidarr zum erneuten Überprüfen des Indexers zu zwingen. Beachten Sie, dass die Warnung der Gesundheitsprüfung nicht immer sofort verschwindet.

#### Jackett Alle Endpunkte verwendet

- Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere sind potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Selbst die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des `/all`-Endpunkts hat keine Vorteile, nur Nachteile:
  - Sie verlieren die Kontrolle über indexerspezifische Einstellungen (Kategorien, Suchmodi usw.)
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen
  - Indexerspezifische Kategorien (>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt
  - Wenn einer der Tracker einen Fehler zurückgibt, deaktiviert \*Arr ihn und Sie erhalten keine Ergebnisse mehr.

##### Lösungen

- Fügen Sie jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu
- Schauen Sie sich [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schauen Sie sich [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwenden Sie jedoch nicht ihren einzelnen aggregierten Endpunkt und verwenden Sie `multi`, wenn die Synchronisierung verwendet wird.

### Künstlerordner

#### Fehlender Stammordner

- Dieser Fehler wird in der Regel identifiziert, wenn ein Künstler nach einem Stammordner sucht, aber dieser Stammordner nicht mehr verfügbar ist.
- Dieser Fehler kann auch auftreten, wenn eine Liste immer noch auf einen Stammordner zeigt, dieser Stammordner jedoch nicht mehr verfügbar ist.
- Wenn Sie diese Warnung entfernen möchten, suchen Sie einfach das Album, das den alten Stammordner verwendet, und bearbeiten Sie es so, dass der richtige Stammordner verwendet wird.

- Der einfachste Weg, um den Problemkünstler zu finden, besteht darin:

  - Gehen Sie zum Künstler (Bibliothek) Tab
  - Erstellen Sie einen benutzerdefinierten Filter mit dem alten Stammordnerpfad
  - Wählen Sie Massenbearbeitung in der oberen Leiste aus und wählen Sie aus dem Dropdown-Menü "Stammordner" den neuen Stammordnerpfad aus, zu dem Sie diese Künstler verschieben möchten.
  - Als Nächstes erhalten Sie einen Popup, in dem steht: Möchten Sie die Künstlerordner in 'Stammordner' verschieben? Dies wird auch angeben: Dies wird auch den Künstlerordner gemäß dem Künstlerordnerformat in den Einstellungen umbenennen. Wählen Sie einfach Nein aus, wenn Sie nicht möchten, dass Lidarr Ihre Dateien verschiebt.
  - Führen Sie die Aufgabe "Gesundheitsprüfung überprüfen" in System => Aufgaben aus

## Festplattenspeicher

- In diesem Abschnitt wird der verfügbare Festplattenspeicher angezeigt
- In Docker kann dies schwierig sein, da in der Regel der verfügbare Speicherplatz in Ihrem Docker-Image angezeigt wird

## Über

- Hier erfahren Sie mehr über Ihre aktuelle Lidarr-Installation

## Weitere Informationen

- Startseite: Lidarr's Startseite
- Wiki: Sie sind bereits hier
- Reddit: r/lidarr
- Discord: Tritt unserem Discord bei
- Spenden: Wenn Sie großzügig sind und spenden möchten, klicken Sie hier
- Spenden an Sonarr: Wenn Sie großzügig sind und an das Projekt spenden möchten, das alles begonnen hat, klicken Sie hier
- Quelle: GitHub
- Funktionsanfragen: Haben Sie eine großartige Idee? Teilen Sie sie hier mit

# Aufgaben

## Geplant

- Diese Seite listet alle geplanten Aufgaben auf, die von Lidarr ausgeführt werden

  - Anwendung Aktualisierung überprüfen - Diese wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan ausgeführt und überprüft, ob Lidarr auf der neuesten Version ist, und löst dann das Aktualisierungsskript aus, um Lidarr zu aktualisieren. Einstellungen=> Update

  > Hinweis: Wenn Sie Docker verwenden, wird dies Ihren Container nicht aktualisieren, da ein neues Image heruntergeladen werden muss.
{.is-warning}

  - Sicherung - Dies führt gemäß dem in der Benutzeroberfläche angezeigten Zeitplan eine Sicherung der Lidarr-Datenbank durch. Weitere Informationen dazu finden Sie hier. Weitere Informationen zu Sicherungen finden Sie unter