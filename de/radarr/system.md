---
title: Radarr System
description: 
published: true
date: 2022-10-19T22:59:06.531Z
tags: radarr, needs-love
editor: markdown
dateCreated: 2021-05-25T02:28:35.194Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Status](#status)
  - [Gesundheit](#gesundheit)
    - [Systemwarnungen](#systemwarnungen)
      - [Zweig ist kein gültiger Release-Zweig](#zweig-ist-kein-gültiger-release-zweig)
      - [Aktualisierung auf .NET-Version](#aktualisierung-auf-net-version)
        - [Behebung von Docker-Installationen](#behebung-von-docker-installationen)
        - [Behebung von FreeBSD-Installationen](#behebung-von-freebsd-installationen)
        - [Behebung von eigenständigen Installationen](#behebung-von-eigenständigen-installationen)
      - [Derzeit installierte Mono-Version ist veraltet und wird nicht unterstützt](#derzeit-installierte-mono-version-ist-veraltet-und-wird-nicht-unterstützt)
      - [Derzeit installierte SQLite-Version wird nicht unterstützt](#derzeit-installierte-sqlite-version-wird-nicht-unterstützt)
      - [Datenbank-Integritätsprüfung fehlgeschlagen](#datenbank-integritätsprüfung-fehlgeschlagen)
      - [Neues Update verfügbar](#neues-update-verfügbar)
      - [Aktualisierung kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist](#aktualisierung-kann-nicht-installiert-werden-da-der-startordner-vom-benutzer-nicht-beschreibbar-ist)
      - [Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern](#aktualisierung-ist-nicht-möglich-um-das-löschen-von-appdata-beim-update-zu-verhindern)
      - [Zweig ist für eine frühere Version](#zweig-ist-für-eine-frühere-version)
      - [Konnte keine Verbindung zu SignalR herstellen](#konnte-keine-verbindung-zu-signalr-herstellen)
        - [Nginx](#nginx)
        - [Apache2](#apache2)
        - [Caddy](#caddy)
      - [Fehler beim Auflösen der IP-Adresse für den konfigurierten Proxy-Host](#fehler-beim-auflösen-der-ip-adresse-für-den-konfigurierten-proxy-host)
      - [Proxy-Test fehlgeschlagen](#proxy-test-fehlgeschlagen)
      - [Systemzeit weicht um mehr als 1 Tag ab](#systemzeit-weicht-um-mehr-als-1-tag-ab)
      - [PTP-Indexer-Einstellungen veraltet](#ptp-indexer-einstellungen-veraltet)
      - [Mono- und x86-Builds werden eingestellt](#mono-und-x86-builds-werden-eingestellt)
    - [Download-Clients](#download-clients)
      - [Es ist kein Download-Client verfügbar](#es-ist-kein-download-client-verfügbar)
      - [Kommunikation mit dem Download-Client nicht möglich](#kommunikation-mit-dem-download-client-nicht-möglich)
      - [Download-Clients sind aufgrund eines Fehlers nicht verfügbar](#download-clients-sind-aufgrund-eines-fehlers-nicht-verfügbar)
      - [Abgeschlossene Download-Verarbeitung aktivieren](#abgeschlossene-download-verarbeitung-aktivieren)
      - [Fehlerhafte Remote-Pfadzuordnung in Docker](#fehlerhafte-remote-pfadzuordnung-in-docker)
      - [Herunterladen in das Stammverzeichnis](#herunterladen-in-das-stammverzeichnis)
      - [Fehlerhafte Download-Client-Einstellungen](#fehlerhafte-download-client-einstellungen)
      - [Fehlerhafte Remote-Pfadzuordnung](#fehlerhafte-remote-pfadzuordnung)
      - [Berechtigungsfehler](#berechtigungsfehler)
      - [Remote-Datei wurde während der Verarbeitung teilweise entfernt](#remote-datei-wurde-während-der-verarbeitung-teilweise-entfernt)
      - [Remote-Pfad wird verwendet und Import fehlgeschlagen](#remote-pfad-wird-verwendet-und-import-fehlgeschlagen)
    - [Abgeschlossene/fehlgeschlagene Download-Verarbeitung](#abgeschlossenefehlgeschlagene-download-verarbeitung)
      - [Abgeschlossene Download-Verarbeitung ist deaktiviert](#abgeschlossene-download-verarbeitung-ist-deaktiviert)
    - [Indexer](#indexer)
      - [Keine Indexer verfügbar mit aktivierter automatischer Suche, Radarr liefert keine automatischen Suchergebnisse](#keine-indexer-verfügbar-mit-aktivierter-automatischer-suche-radarr-liefert-keine-automatischen-suchergebnisse)
      - [Keine Indexer verfügbar mit aktivierter RSS-Synchronisierung, Radarr lädt keine neuen Veröffentlichungen automatisch herunter](#keine-indexer-verfügbar-mit-aktivierter-rss-synchronisierung-radarr-lädt-keine-neuen-veröffentlichungen-automatisch-herunter)
      - [Keine Indexer aktiviert](#keine-indexer-aktiviert)
    - [Aktivierte Indexer unterstützen keine Suche](#aktivierte-indexer-unterstützen-keine-suche)
      - [Keine Indexer verfügbar mit aktivierter interaktiver Suche](#keine-indexer-verfügbar-mit-aktivierter-interaktiver-suche)
      - [Indexer sind aufgrund von Fehlern nicht verfügbar](#indexer-sind-aufgrund-von-fehlern-nicht-verfügbar)
      - [Jackett All-Endpunkt verwendet](#jackett-all-endpunkt-verwendet)
        - [Lösungen](#lösungen)
    - [Filmordner](#filmordner)
      - [Fehlender Stammordner](#fehlender-stammordner)
    - [Filme](#filme)
      - [Film wurde von TMDb entfernt](#film-wurde-von-tmdb-entfernt)
      - [Listen sind aufgrund von Fehlern nicht verfügbar](#listen-sind-aufgrund-von-fehlern-nicht-verfügbar)
    - [Benachrichtigungen](#benachrichtigungen)
    - [Discord als Slack-Benachrichtigung](#discord-als-slack-benachrichtigung)
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

- Diese Seite enthält eine Liste von Fehlern bei der Gesundheitsprüfung. Diese Gesundheitsprüfungen werden regelmäßig von Radarr durchgeführt und bei bestimmten Ereignissen. Die resultierenden Warnungen und Fehler werden hier aufgelistet, um Ratschläge zur Behebung zu geben.

### Systemwarnungen

#### Zweig ist kein gültiger Release-Zweig

- Der von Ihnen festgelegte Zweig ist kein gültiger Release-Zweig. Sie erhalten keine Updates. Bitte ändern Sie zu einem der [aktuellen Release-Zweige](/radarr/faq#how-do-i-update-radarr).

#### Aktualisierung auf .NET-Version

{#update-to-net-core-version}

- Neuere Versionen von Radarr sind für .NET6 oder neuer ausgelegt. Mono-Builds werden ab Version 4 nicht mehr bereitgestellt oder unterstützt. Version 3.2.2 ist die letzte Version von Radarr, die Legacy-Mono-Builds unterstützt. Sie verwenden eine dieser Legacy-Mono-Builds, aber Ihre Plattform unterstützt .NET.

Siehe die folgenden Einträge, wie Sie von nicht unterstützten, veralteten Mono-Versionen zu dotnet wechseln können.

- [Behebung von Docker-Installationen](#behebung-von-docker-installationen)
- [Behebung von FreeBSD-Installationen](#behebung-von-freebsd-installationen)
- [Behebung von eigenständigen Installationen](#behebung-von-eigenständigen-installationen)
{.links-list}

##### Behebung von Docker-Installationen

- Stellen Sie sicher, dass Ihr Zweig für Ihren Docker-Maintainer korrekt ist, und ziehen Sie Ihren Container erneut.

##### Behebung von FreeBSD-Installationen

- Aktualisieren Sie einfach den Radarr-Port mit `pkg update && pkg upgrade`
- (Optional) Entfernen Sie das Mono-Paket, wenn Sie möchten

##### Behebung von eigenständigen Installationen

Fehler wie:

```none
Cannot open assembly '/opt/Radarr/Radarr': File does not contain a valid CIL image
```

- Sichern Sie Ihre vorhandene Konfiguration vor dem nächsten Schritt.
- Dies sollte nur auf Linux-Hosts auftreten. Installieren Sie kein .NET-Runtime oder SDK von Microsoft.
- Um dies zu beheben, laden Sie den richtigen Build für Ihre Architektur herunter und ersetzen Sie Ihre vorhandenen Binärdateien (Anwendung)
- Kurz gesagt müssen Sie Ihre vorhandenen Binärdateien (Inhalt oder Ordner von /opt/Radarr) löschen und durch den Inhalt der gerade heruntergeladenen .tar.gz ersetzen und dann Ihre Dienstdatei aktualisieren, um kein Mono zu verwenden.

> LÖSCHEN SIE NICHT EINFACH DEN DOWNLOAD ÜBER IHREN VORHANDENEN BINÄREN.
> SIE MÜSSEN ZUERST DIE ALTEN LÖSCHEN.
{.is-warning}

- Das Folgende ist ein von der Community entwickeltes Skript, um Ihre Mono-Installation zu entfernen und durch die .NET-Installation zu ersetzen. Beiträge und Korrekturen sind willkommen.
- Dies setzt voraus, dass Sie sich im `master`-Radarr-Zweig befinden. Aktualisieren Sie die Variable bei Bedarf.
- Dies setzt voraus, dass Radarr als Benutzer `radarr` ausgeführt wird. Aktualisieren Sie die Variablen bei Bedarf.
- Dies setzt voraus, dass Radarr unter `/opt/Radarr` installiert ist. Aktualisieren Sie die Variablen bei Bedarf.

```bash
#!/bin/bash
## Benutzervariablen
installdir="/opt/Radarr"
APPUSER="radarr"
branch="master"
## /Benutzervariablen
app="radarr"
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
    echo_error "Arch not supported"
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

- Radarr ist in .NET geschrieben und erfordert Mono, um auf sehr alten ARM-Prozessoren ausgeführt zu werden. Mono 5.20 ist das absolute Minimum für Radarr.
- Das Upgrade-Verfahren für Mono variiert je nach Plattform.

> Mono wird ab Radarr Version 4.0 nicht mehr unterstützt
{.is-warning}

#### Derzeit installierte SQLite-Version wird nicht unterstützt

- Radarr speichert seine Daten in einer SQLite-Datenbank. Die auf Ihrem System installierte SQLite3-Bibliothek ist zu alt. Radarr erfordert mindestens Version 3.9.0.

> Beachten Sie, dass Radarr `libSQLite3.so` verwendet, die möglicherweise in einem SQLite3-Upgrade-Paket enthalten ist oder nicht.
{.is-info}

#### Datenbank-Integritätsprüfung fehlgeschlagen

- Ihre Datenbank(en) haben eine [SQLite Pragma Integrity Check](https://www.sqlite.org/pragma.html#pragma_integrity_check) nicht bestanden und weisen einige Korruptionen auf.
- Wenn `Radarr.db` beschädigt ist, [lesen Sie bitte diesen FAQ-Eintrag](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)
- Wenn `logs.db` beschädigt ist: Stoppen Sie Radarr, löschen Sie `logs.db` und alle `logs.wal`-Dateien.
- Wenn beide beschädigt sind, überprüfen Sie die entsprechenden Vorgänge oben.

#### Neues Update verfügbar

- Freuen Sie sich, die Entwickler haben ein neues Update veröffentlicht. Dies bedeutet in der Regel großartige neue Funktionen und behobene Fehler (oder?). Offensichtlich haben Sie die automatische Aktualisierung nicht aktiviert, daher müssen Sie herausfinden, wie Sie auf Ihrer Plattform aktualisieren können. Das Drücken der Schaltfläche "Installieren" auf der Seite System => Updates ist wahrscheinlich ein guter Ausgangspunkt.

> Diese Warnung wird nicht angezeigt, wenn Ihre aktuelle Version weniger als 14 Tage alt ist
{.is-info}

#### Aktualisierung kann nicht installiert werden, da der Startordner vom Benutzer nicht beschreibbar ist

- Dies bedeutet, dass Radarr sich nicht selbst aktualisieren kann. Sie müssen Radarr manuell aktualisieren oder die Berechtigungen für das Startverzeichnis von Radarr (das Installationsverzeichnis) so einstellen, dass Radarr sich selbst aktualisieren kann.

#### Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern

- Radarr hat erkannt, dass der AppData-Ordner für Ihr Betriebssystem im Verzeichnis liegt, das die Radarr-Binärdateien enthält. Normalerweise wäre dies C:\ProgramData für Windows und ~/.config für Linux.

- Bitte schauen Sie sich System => Info an, um die aktuellen AppData- und Startverzeichnisse anzuzeigen.
- Dies bedeutet, dass Radarr sich selbst nicht aktualisieren kann, ohne Datenverlust zu riskieren.
- Wenn Sie Linux verwenden, müssen Sie wahrscheinlich das Home-Verzeichnis für den Benutzer ändern, der Radarr ausführt, und den aktuellen Inhalt des Verzeichnisses ~/.config/Radarr kopieren, um Ihre Datenbank zu erhalten.

#### Zweig ist für eine frühere Version

- Der in den Einstellungen/Allgemein festgelegte Aktualisierungszweig ist für eine frühere Version von Radarr. Daher wird die Instanz keine korrekten Aktualisierungsinformationen im System/Updates-Feed sehen und möglicherweise keine neuen Updates erhalten, wenn sie veröffentlicht werden.

#### Konnte keine Verbindung zu SignalR herstellen

- SignalR steuert die dynamischen UI-Updates. Wenn Ihr Browser keine Verbindung zu SignalR auf Ihrem Server herstellen kann, sehen Sie keine Echtzeit-Updates in der Benutzeroberfläche.
- Das häufigste Auftreten davon ist die Verwendung eines Reverse-Proxys oder von Cloudflare.
- Cloudflare benötigt aktiviertes Websockets.

##### Nginx

- Nginx erfordert die folgende Ergänzung zum Location-Block für die App:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Stellen Sie sicher, dass Sie `proxy_set_header Connection "Upgrade";` nicht wie in der nginx-Dokumentation vorgeschlagen einfügen. DAS FUNKTIONIERT NICHT
> Siehe <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache2

Für den Apache2-Reverse-Proxy müssen Sie die folgenden Module aktivieren: proxy, proxy_http und proxy_wstunnel. Fügen Sie dann diese Websocket-Tunnelanweisung zu Ihrer Vhost-Konfiguration hinzu:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:7878/$1 [P,L]
```

Wenn Sie einen Reverse-Proxy unter einem Unterverzeichnis haben, sollte die RewriteRule Ihren Basispfad enthalten, z.B.

```none
RewriteRule /radarr/(.*) ws://127.0.0.1:7878/radarr/$1 [P,L]
```

Wenn Radarr nicht auf demselben Computer wie Ihr Reverse-Proxy ausgeführt wird, ersetzen Sie 127.0.0.1 durch die entsprechende IP-Adresse/DNS-Namen Ihrer Radarr-App.

##### Caddy

Für Caddy (V1) verwenden Sie dies:
Hinweis: Sie müssen auch die Websocket-Anweisung zu Ihrer Radarr-Konfiguration hinzufügen

```none
 proxy /radarr 127.0.0.1:7878 {
     websocket
     transparent
 }
```

#### Fehler beim Auflösen der IP-Adresse für den konfigurierten Proxy-Host

- Überprüfen Sie Ihre Proxy-Einstellungen und stellen Sie sicher, dass sie korrekt sind
- Stellen Sie sicher, dass Ihr Proxy aktiv, ausgeführt und erreichbar ist

#### Proxy-Test fehlgeschlagen

- Ihr konfigurierter Proxy hat den Test nicht erfolgreich bestanden. Überprüfen Sie den bereitgestellten HTTP-Fehler und/oder überprüfen Sie die Protokolle für weitere Details.

#### Systemzeit weicht um mehr als 1 Tag ab

- Die Systemzeit weicht um mehr als 1 Tag ab. Geplante Aufgaben können erst korrekt ausgeführt werden, wenn die Zeit korrigiert ist.
- Überprüfen Sie Ihre Systemzeit und stellen Sie sicher, dass sie mit einem autoritativen Zeitserver synchronisiert ist und korrekt ist.

#### PTP-Indexer-Einstellungen veraltet

- Die folgenden PassThePopcorn-Indexer haben veraltete Einstellungen und sollten aktualisiert werden.

#### Mono- und x86-Builds werden eingestellt

- Mono- und x86-Builds werden ab Version 4 nicht mehr unterstützt. Wenn Sie diese Fehlermeldung erhalten, verwenden Sie entweder die Mono-Version der Anwendung oder die x86-Version. Aufgrund der zunehmenden Schwierigkeiten bei der Entwicklung und Unterstützung dieser Legacy-Versionen werden wir ihre Unterstützung einstellen und sie daher in Zukunft nicht mehr veröffentlichen. Es wird daher empfohlen, auf ein unterstütztes Betriebssystem zu aktualisieren, das weder x86 noch Mono erfordert. Möglicherweise können Sie auch Docker für Ihre Anforderungen verwenden.

### Download-Clients

#### Es ist kein Download-Client verfügbar

- Ein ordnungsgemäß konfigurierter und aktivierter Download-Client ist erforderlich, damit Radarr Medien herunterladen kann. Da Radarr verschiedene Download-Clients unterstützt, sollten Sie feststellen, welcher Ihren Anforderungen am besten entspricht. Wenn Sie bereits einen Download-Client installiert haben, sollten Sie Radarr so konfigurieren, dass er ihn verwendet und eine Kategorie erstellt. Siehe Einstellungen => Download-Client.

#### Kommunikation mit dem Download-Client nicht möglich

- Radarr konnte nicht mit dem konfigurierten Download-Client kommunizieren. Überprüfen Sie, ob der Download-Client betriebsbereit ist, und überprüfen Sie die URL erneut. Dies kann auch auf einen Authentifizierungsfehler hinweisen.
- Dies liegt in der Regel an einem falsch konfigurierten Download-Client. Dinge, die Sie in der Regel überprüfen können:
  - Die IP-Adresse Ihres Download-Clients, wenn er auf demselben Bare-Metal-Computer liegt, ist dies in der Regel 127.0.0.1
  - Die Portnummer, die Ihr Download-Client verwendet, diese sind mit der Standardportnummer ausgefüllt, aber wenn Sie sie geändert haben, müssen Sie dieselbe Nummer in Radarr eingeben.
  - Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie Ihre Radarr-Instanz und Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in der SSL-FAQ.
  - Stellen Sie sicher, dass IPv6 auf dem System deaktiviert ist, wenn es nicht funktioniert
  - Stellen Sie sicher, dass ein DNS-Server (z.B. pihole) keine Abfragen mit Rate Limiting beschränkt

#### Download-Clients sind aufgrund eines Fehlers nicht verfügbar

- Einer oder mehrere Ihrer Download-Clients reagieren nicht auf Anfragen von Radarr. Daher hat Radarr beschlossen, die Abfrage des Download-Clients in seinem normalen 1-Minuten-Zyklus vorübergehend zu stoppen, der normalerweise verwendet wird, um aktive Downloads zu verfolgen und abgeschlossene Downloads zu importieren. Radarr wird jedoch weiterhin versuchen, Downloads an den Client zu senden, wird jedoch höchstwahrscheinlich scheitern.
- Sie sollten System=>Logs überprüfen, um den Grund für die Fehler zu sehen.
- Wenn Sie diesen Download-Client nicht mehr verwenden, deaktivieren Sie ihn in Radarr, um die Fehler zu vermeiden.

#### Abgeschlossene Download-Verarbeitung aktivieren

- Radarr erfordert die Aktivierung der abgeschlossenen Download-Verarbeitung, um Dateien importieren zu können, die vom Download-Client heruntergeladen wurden. Es wird empfohlen, die abgeschlossene Download-Verarbeitung zu aktivieren. (Die abgeschlossene Download-Verarbeitung ist standardmäßig für neue Benutzer aktiviert.)

#### Fehlerhafte Remote-Pfadzuordnung in Docker

- Dieser Fehler tritt in der Regel bei fehlerhaften Docker-Pfaden in Ihrem Download-Client oder Radarr auf.

- Ein Beispiel dafür wäre:
  - Download-Client: Download-Pfad: /mnt/user/downloads:/downloads
  - Radarr: Download-Pfad: /mnt/user/downloads:/data
- In diesem Beispiel legt der Download-Client seine Downloads in /downloads ab und teilt Radarr dann mit, dass der fertige Film in /downloads ist. Radarr kommt dann und sagt "Okay, cool, lass mich in /downloads nachsehen" Nun, innerhalb von Radarr haben Sie keinen /downloads-Pfad zugewiesen, sondern einen /data-Pfad, daher wird dieser Fehler angezeigt.
- Die einfachste Lösung dafür ist KONSISTENZ. Wenn Sie ein Schema in Ihrem Download-Client verwenden, verwenden Sie es in allen Bereichen.

- Team Radarr ist ein großer Fan von einfach /data zu verwenden.
  - Download-Client: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Jetzt können Sie in Ihrem Download-Client angeben, wo Sie Ihre Downloads in /data platzieren möchten. Dies variiert je nach Client, aber Sie sollten ihm sagen können "Ja, Download-Client platziere meine Dateien in." /data/torrents (oder usenet)/movies und da Sie in Radarr /data verwendet haben, wenn der Download-Client Radarr mitteilt, dass er fertig ist, wird Radarr kommen und sagen "Super, ich habe ein /data und ich kann auch /torrents (oder usenet)/movies sehen, alles ist in Ordnung."
- Es gibt viele großartige Anleitungen: unser Wiki [Docker Guide](/docker-guide) und TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Diese Anleitungen legen zwar großen Wert auf Hardlinks und Atomic-Moves, aber das allgemeine Konzept von Containern und der Funktionsweise der Pfadzuordnung ist der Kern dieser Diskussionen.

- Weitere Informationen finden Sie in [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/).

#### Herunterladen in das Stammverzeichnis

{#downloads-in-root-folder}

- In der Anwendung wird ein Stammverzeichnis als das konfigurierte Medienbibliotheksverzeichnis definiert. Dies ist nicht das Stammverzeichnis eines Laufwerks. Ihr Download-Client lädt eine unvollständige oder vollständige Datei (oder verschiebt abgeschlossene Downloads) in Ihr Stammverzeichnis (Bibliothek).
- Dies führt häufig zu Problemen, einschließlich Datenverlust, und sollte nicht durchgeführt werden. Ändern Sie dies, indem Sie Ihren Download-Client so konfigurieren, dass er keine Downloads in Ihr Stammverzeichnis platziert. Beachten Sie, dass "Platzieren" auch bedeutet, dass Ihre Download-Client-Kategorie auf Ihr Stammverzeichnis festgelegt ist oder dass NZBGet/SABnzbd sortiert ist und in Ihr Stammverzeichnis sortiert.
- Bitte beachten Sie, dass diese Überprüfung alle definierten/konfigurierten Stammverzeichnisse umfasst, nicht nur die derzeit verwendeten Stammverzeichnisse. Mit anderen Worten, der Ordner, in den Ihr Download-Client herunterlädt oder abgeschlossene Downloads verschiebt, sollte nicht derselbe Ordner sein, den Sie als Ihr Stamm-/Bibliotheks-/endgültiges Medienzielverzeichnis in der *arr-Anwendung konfiguriert haben.
- Konfigurierte Stammverzeichnisse (auch Bibliotheksverzeichnisse genannt) finden Sie in [Einstellungen => Medienverwaltung => Stammverzeichnisse](/radarr/settings/#root-folders)
- Ein Beispiel ist, wenn Ihre Downloads in `\data\downloads` gehen, dann haben Sie ein Stammverzeichnis als `\data\downloads` festgelegt.
- Es wird empfohlen, Pfade wie `\data\media\` für Ihr Stammverzeichnis/Bibliothek und `\data\downloads\` für Ihre Downloads zu verwenden.
- Lesen Sie unseren [Docker Guide](/docker-guide) und TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) für weitere Informationen zur korrekten und optimalen Pfadkonfiguration. Beachten Sie, dass die Konzepte für Docker und Nicht-Docker gelten.

> Ihr Download-Ordner, in dem Ihr Download-Client die Downloads platziert, und Ihr Stamm-/Bibliotheksordner MÜSSEN getrennt sein. \*Arr importiert die Datei(en) aus dem Download-Ordner Ihres Download-Clients in Ihre Bibliothek. Der Download-Client sollte nichts verschieben oder herunterladen, das in Ihre Bibliothek gehört.
{.is-warning}

#### Fehlerhafte Download-Client-Einstellungen

- Der Speicherort, an dem Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne Remote-Pfadzuordnung zu wechseln, betreffen.

#### Fehlerhafte Remote-Pfadzuordnung

- Der Speicherort, an dem Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne Remote-Pfadzuordnung zu wechseln, betreffen. Weitere Informationen finden Sie in [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/).

#### Berechtigungsfehler

- Radarr oder der Benutzer radarr, unter dem Radarr ausgeführt wird, kann nicht auf den Speicherort zugreifen, an dem Ihr Download-Client Dateien herunterlädt. Dies ist in der Regel ein Berechtigungsproblem.

#### Remote-Datei wurde während der Verarbeitung teilweise entfernt

- Eine über eine Remote-Pfadzuordnung zugängliche Datei scheint vor Abschluss der Verarbeitung entfernt worden zu sein.

#### Remote-Pfad wird verwendet und Import fehlgeschlagen

- Überprüfen Sie die Protokolle für weitere Informationen. Weitere Informationen finden Sie in unseren Fehlerbehebungshandbüchern.

### Abgeschlossene/fehlgeschlagene Download-Verarbeitung

#### Abgeschlossene Download-Verarbeitung ist deaktiviert

- (Diese Warnung wird nur für bestehende Benutzer generiert, bevor die Funktion zur abgeschlossenen Download-Verarbeitung implementiert wurde. Diese Funktion ist standardmäßig deaktiviert, um sicherzustellen, dass das System für aktuelle Konfigurationen wie erwartet funktioniert.)
- Es wird empfohlen, die abgeschlossene Download-Verarbeitung zu verwenden, da sie eine bessere Kompatibilität für die Entpackungs- und Nachverarbeitungslogik verschiedener Download-Clients bietet. Mit ihr importiert Radarr einen Download erst, wenn der Download-Client ihn als bereit meldet.
- Wenn Sie die abgeschlossene Download-Verarbeitung aktivieren möchten, sollten Sie Folgendes überprüfen: * Warnung: Die abgeschlossene Download-Verarbeitung funktioniert nur ordnungsgemäß, wenn der Download-Client und Radarr auf demselben Computer ausgeführt werden, da er den zu importierenden Pfad direkt vom Download-Client erhält. Andernfalls ist eine Remote-Zuordnung erforderlich.

### Indexer

#### Keine Indexer verfügbar mit aktivierter automatischer Suche, Radarr liefert keine automatischen Suchergebnisse

- Einfach ausgedrückt haben Sie keine Ihrer Indexer so eingestellt, dass automatische Suchen möglich sind.
- Gehen Sie zu Einstellungen => Indexer, wählen Sie einen Indexer aus, den Sie für automatische Suchen zulassen möchten, und klicken Sie dann auf Speichern.

#### Keine Indexer verfügbar mit aktivierter RSS-Synchronisierung, Radarr lädt keine neuen Veröffentlichungen automatisch herunter

- Radarr verwendet den RSS-Feed, um neue Veröffentlichungen zu erfassen, wenn sie auftreten. Weitere Informationen dazu finden Sie hier
- Um dieses Problem zu beheben, gehen Sie zu Einstellungen => Indexer, wählen Sie einen Indexer aus, den Sie haben, und aktivieren Sie die RSS-Synchronisierung

#### Keine Indexer aktiviert

- Radarr erfordert Indexer, um neue Veröffentlichungen entdecken zu können. Bitte lesen Sie das Wiki, um Anweisungen zum Hinzufügen von Indexern zu erhalten.

#### Aktivierte Indexer unterstützen keine Suche

- Keiner der von Ihnen aktivierten Indexer unterstützt die Suche. Dies bedeutet, dass Radarr nur über die RSS-Feeds neue Veröffentlichungen finden kann. Die Suche nach Filmen (entweder automatische Suche oder manuelle Suche) liefert niemals Ergebnisse. Die einzige Möglichkeit, dies zu beheben, besteht darin, einen weiteren Indexer hinzuzufügen.

#### Keine Indexer verfügbar mit aktivierter interaktiver Suche

- Keiner der von Ihnen aktivierten Indexer unterstützt die interaktive Suche. Dies bedeutet, dass die Anwendung nur über die RSS-Feeds oder eine automatische Suche neue Veröffentlichungen finden kann.

#### Indexer sind aufgrund von Fehlern nicht verfügbar

- Fehler treten auf, wenn Radarr versucht, einen Ihrer Indexer zu verwenden. Um die Anzahl der Wiederholungsversuche zu begrenzen, verwendet Radarr den Indexer für eine zunehmende Zeit nicht mehr (bis zu 24 Stunden).
- Dieser Mechanismus wird ausgelöst, wenn Radarr keine Antwort vom Indexer erhalten konnte (kann durch DNS, Proxy/VPN-Verbindung, Authentifizierung oder ein Indexer-Problem verursacht werden) oder die nzb/torrent-Datei nicht vom Indexer abrufen konnte. Bitte überprüfen Sie die Protokolle, um festzustellen, welche Art von Fehler das Problem verursacht hat.
- Sie können die Warnung verhindern, indem Sie den betroffenen Indexer deaktivieren.
- Führen Sie den Test auf dem Indexer aus, um Radarr zum erneuten Überprüfen des Indexers zu zwingen. Beachten Sie, dass die Warnung der Gesundheitsprüfung nicht immer sofort verschwindet.

#### Jackett All-Endpunkt verwendet

- Der Jackett /all-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere sind potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Selbst die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des /all-Endpunkts hat keine Vorteile, nur Nachteile:
  - Sie verlieren die Kontrolle über indexerspezifische Einstellungen (Kategorien, Suchmodi usw.)
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen
  - Indexerspezifische Kategorien (\>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt
  - Wenn einer der Tracker in /all einen Fehler zurückgibt, deaktiviert \*Arr ihn und Sie erhalten keine Ergebnisse mehr.

##### Lösungen

- Fügen Sie jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu
- Schauen Sie sich [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schauen Sie sich [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwenden Sie jedoch nicht deren einzelnen Aggregat-Endpunkt und verwenden Sie `multi`, wenn die Synchronisierung verwendet wird.

### Filmordner

#### Fehlender Stammordner

{#movie-collection-missing-root-folder}

- Dieser Fehler wird in der Regel erkannt, wenn einem Film oder einer Sammlung ein Stammordner zugewiesen ist, der nicht mehr verfügbar ist.
- Dieser Fehler kann auch auftreten, wenn eine Liste immer noch auf einen Stammordner zeigt und dieser Stammordner nicht mehr verfügbar ist.
- Wenn Sie diese Warnung entfernen möchten, suchen Sie einfach den/die Film(e) oder die Sammlung(en), die immer noch den alten Stammordner verwenden, und bearbeiten Sie sie so, dass der richtige Stammordner verwendet wird.

##### Tabellenansicht der Filme

1. Gehen Sie zum Tab "Filme" (Bibliothek)
1. Tabellenansicht aktivieren und die Spalte "Pfad" aktivieren, dann nach Pfad sortieren

##### Benutzerdefinierter Filter für Filme

1. Erstellen Sie einen benutzerdefinierten Filter mit dem alten Stammordnerpfad
1. Wählen Sie die Filme aus und wählen Sie im Dropdown-Menü "Stammordner" den neuen Stammordner aus, dem diese Filme zugewiesen werden sollen.
1. Als Nächstes erhalten Sie einen Pop-up, in dem steht "Möchten Sie die Filmordner in 'Stammordner' verschieben?" Es wird auch angegeben, dass dabei der Filmordner gemäß dem Filmordnerformat in den Einstellungen umbenannt wird. Wählen Sie einfach Nein aus, wenn Sie nicht möchten, dass Radarr Ihre Dateien verschiebt.
1. Führen Sie die Aufgabe "Gesundheitsprüfung überprüfen" in System => Aufgaben aus

#### Benutzerdefinierter Filter für Sammlungen

1. Erstellen Sie einen benutzerdefinierten Filter in Sammlungen mit dem alten Stammordnerpfad
1. Wählen Sie die Sammlungen aus und wählen Sie im Dropdown-Menü "Stammordner" den neuen Stammordner aus, dem die zukünftigen Filme dieser Sammlungen zugewiesen werden sollen.
1. Führen Sie die Aufgabe "Gesundheitsprüfung überprüfen" in System => Aufgaben aus

### Filme

#### Film wurde von TMDb entfernt

- Der Film ist mit einer TMDb-ID verknüpft, die von TMDb gelöscht wurde, normalerweise weil es sich um ein Duplikat handelte, kein Film war oder aus einem anderen Grund die ID geändert wurde. Gelöschte Filme erhalten keine Updates und sollten vom Benutzer korrigiert werden, um die Funktionalität sicherzustellen. Entfernen Sie den Film aus Radarr, ohne die Dateien zu löschen, und versuchen Sie, ihn erneut hinzuzufügen. Wenn er bei einer Suche nicht angezeigt wird, überprüfen Sie Sonarr, da es sich möglicherweise um eine TV-Miniserie wie Stephen Kings Es handelt.

- Sie können gelöschte Filme finden und bearbeiten, indem Sie einen benutzerdefinierten Filter mit den folgenden Schritten erstellen:

  1. Klicken Sie auf Filme im linken Menü
  1. Klicken Sie auf das Dropdown-Menü Filter und wählen Sie "Benutzerdefinierter Filter"
  1. Geben Sie ein Label ein, z.B. "Gelöschte Filme"
  1. Erstellen Sie den Filter wie folgt: `Veröffentlichungsstatus` ist `Gelöscht`
  1. Klicken Sie auf Speichern und wählen Sie den neu erstellten Filter aus dem Dropdown-Menü Filter

#### Listen sind aufgrund von Fehlern nicht verfügbar

- In der Regel bedeutet dies einfach, dass Radarr nicht mehr über die API oder durch Anmeldung bei Ihrem gewählten Listenanbieter kommunizieren kann. Wenn das Problem weiterhin besteht, sollten Sie am besten Kontakt mit ihnen aufnehmen, um sie auszuschließen, da ihre Systeme von Zeit zu Zeit überlastet sein können.
- Überprüfen Sie System => Ereignisse, gefiltert nach Warnung (Warnung & Fehler), um die historischen Fehler oder Protokolle für Details anzuzeigen.

### Benachrichtigungen

## Warteschlange

- Die Warteschlange zeigt Ihnen laufende und zukünftige Aufgaben sowie einen Verlauf kürzlich ausgeführter Aufgaben und deren Dauer.

# Backup

> Wenn Sie wissen möchten, wie Sie Ihre Radarr-Instanz sichern/wiederherstellen können, klicken Sie [hier](/radarr/faq).
{.is-info}

- Im Backup-Bereich werden Ihnen frühere Backups angezeigt (sofern Sie keine frische Installation haben, die noch keine Backups erstellt hat).
  
- Jetzt sichern - Diese Option löst eine manuelle Sicherung der Radarr-Datenbank aus.
- Backup wiederherstellen - Dadurch wird ein neuer Bildschirm geöffnet, um aus einem früheren Backup wiederherzustellen.
  - Durch Auswahl von Datei auswählen wird Ihr Browser aufgefordert, einen Dialog zum Wiederherstellen aus einem Radarr-Zip-Backup zu öffnen.
  
- Wenn Sie frühere Backups haben und diese von Radarr herunterladen möchten, um sie an einem anderen Ort zu speichern, können Sie einfach eine dieser Dateien auswählen, um sie herunterzuladen.
- Rechts neben jedem der vorherigen Downloads haben Sie zwei Optionen.
  - Wiederherstellen (Uhr-Symbol) - Zur Wiederherstellung aus einem früheren Backup - Dadurch wird ein neues Fenster geöffnet, um zu bestätigen, dass Sie aus diesem Backup wiederherstellen möchten.
  - Löschen (Mülleimer) - Zum Löschen eines früheren Backups

# Updates

- Der Update-Bildschirm zeigt die letzten 5 Updates sowie die aktuelle Version an, auf der Sie sich befinden.
- Auf dieser Seite werden auch die Update-Hinweise der Entwickler angezeigt, in denen steht, was in Radarr behoben oder hinzugefügt wurde (Freude!)

> Ein Wartungs-Release enthält Fehlerbehebungen und verschiedene Verbesserungen. Schauen Sie sich die Commit-History für Details an.
{.is-info}

# Ereignisse

- Der Ereignisse-Tab zeigt Ihnen, was in Ihrem Radarr passiert ist. Dies kann zur Diagnose von leichten Problemen verwendet werden. Dies ersetzt jedoch nicht die in Logging besprochenen Trace-Logs.

> Ereignisse entsprechen den INFO-Protokollen. {.is-info}

- Komponenten - Diese Spalte zeigt an, welche Komponente in Radarr ausgelöst wurde.
- Nachricht - Diese Spalte zeigt an, welche Nachricht von der Komponente aus der vorherigen Spalte gesendet wurde.
- Zahnrad-Symbol - Diese Option ermöglicht es Ihnen, festzulegen, wie viele Komponenten/Nachrichten pro Seite angezeigt werden (Standardwert ist 50).
- Optionen oben auf der Seite
  - Aktualisieren - Diese Option aktualisiert die aktuelle Seite und ruft ein neues Ereignisprotokoll ab.
  - Löschen - Dadurch wird das aktuelle Ereignisprotokoll gelöscht und Sie können von vorne beginnen.

# Protokolldateien

- Auf dieser Seite können Sie die aktuellen Protokolldateien für Radarr herunterladen und anzeigen.

- In der obersten Zeile gibt es mehrere Optionen, mit denen Sie Ihre Protokolldateien steuern können.

- In der obersten Zeile ganz links befindet sich ein Dropdown-Menü, mit dem Sie zwischen Protokolldateien und Updater-Protokolldateien wechseln können.
  - Protokolldateien - Das A und O bei jedem Support-Fall finden Sie hier weitere Informationen zu Protokolldateien.
  - Updater-Protokolldateien - Hier werden die Protokolldateien des Radarr-Updater-Skripts angezeigt.

> Wenn Sie Docker verwenden, ist dies leer, da Sie ein Update durch Herunterladen eines neuen Docker-Images durchführen sollten.
{.is-info}

- Aktualisieren - Dadurch wird die aktuelle Seite aktualisiert und alle neu erstellten Protokolle angezeigt.
- Löschen - Dadurch werden alle Protokolle gelöscht und Sie können von vorne beginnen.
- Dateiname - Hier wird der Dateiname angezeigt, der mit dem Protokoll verknüpft ist.
- Zuletzt geschrieben - Dies ist die lokale Zeit, zu der diese bestimmte Protokolldatei geschrieben wurde.
  - Radarr verwendet rollende Protokolldateien, die jeweils auf 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer radarr.txt, für die anderen Dateien ist radarr.0.txt die nächstneueste (je höher die Zahl, desto älter ist sie) bis zu insgesamt 51 Protokolldateien. Diese Protokolldatei enthält `fatal`, `error`, `warn` und `info` Einträge.
  - Wenn der Debug-Protokollpegel aktiviert ist, sind zusätzliche rollende Protokolldateien radarr.debug.txt vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten `fatal`, `error`, `warn`, `info` und `debug` Einträge. Sie decken normalerweise einen Zeitraum von ca. 40 Stunden ab.
  - Wenn der Trace-Protokollpegel aktiviert ist, sind zusätzliche rollende Protokolldateien radarr.trace.txt vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten `fatal`, `error`, `warn`, `info`, `debug` und `trace` Einträge. Aufgrund der umfangreichen Trace-Informationen deckt es normalerweise höchstens ein paar Stunden ab.