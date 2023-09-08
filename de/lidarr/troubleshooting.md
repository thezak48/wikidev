---
title: Lidarr Fehlerbehebung
description: 
published: true
date: 2023-07-24T19:53:24.970Z
tags: lidarr, needs-love, troubleshooting
editor: markdown
dateCreated: 2021-06-14T21:36:46.193Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Hilfe anfordern](#hilfe-anfordern)
- [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien)
  - [Standard-Protokolldateien](#standard-protokolldateien)
  - [Update-Protokolldateien](#update-protokolldateien)
  - [Protokolle teilen](#protokolle-teilen)
  - [Trace-/Debug-Protokolle](#trace-debug-protokolle)
  - [Protokolle löschen](#protokolle-löschen)
- [Mehrere Protokolldateien](#mehrere-protokolldateien)
- [Wiederherstellung nach einem fehlgeschlagenen Update](#wiederherstellung-nach-einem-fehlgeschlagenen-update)
  - [Das Problem ermitteln](#das-problem-ermitteln)
    - [Migrationsproblem](#migrationsproblem)
    - [Berechtigungsproblem](#berechtigungsproblem)
  - [Das Problem beheben](#das-problem-beheben)
    - [Berechtigungsprobleme](#berechtigungsprobleme)
    - [Manuelles Upgrade](#manuelles-upgrade)
- [Downloads und Importieren](#downloads-und-importieren)
  - [Testen des Download-Clients](#testen-des-download-clients)
  - [Testen eines Downloads](#testen-eines-downloads)
  - [Testen eines Imports](#testen-eines-imports)
  - [Häufige Probleme](#häufige-probleme)
    - [WebUI des Download-Clients ist nicht aktiviert](#webui-des-download-clients-ist-nicht-aktiviert)
    - [Fehlerhafte SSL-Konfiguration](#fehlerhafte-ssl-konfiguration)
    - [Freigabe auf Windows nicht sichtbar](#freigabe-auf-windows-nicht-sichtbar)
    - [Zugriff auf Netzlaufwerke ist nicht zuverlässig](#zugriff-auf-netzlaufwerke-ist-nicht-zuverlässig)
    - [Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade](#docker-und-benutzer-gruppe-besitz-berechtigungen-und-pfade)
    - [Remote-Pfadzuordnung](#remote-pfadzuordnung)
      - [Remote-Mount oder Remote-Sync (Syncthing)](#remote-mount-oder-remote-sync-syncthing)
    - [Berechtigungen im Bibliotheksordner](#berechtigungen-im-bibliotheksordner)
    - [Berechtigungen im Download-Ordner](#berechtigungen-im-download-ordner)
    - [Download-Ordner und Bibliotheksordner sind nicht unterschiedliche Ordner](#download-ordner-und-bibliotheksordner-sind-nicht-unterschiedliche-ordner)
    - [Falsche Kategorie](#falsche-kategorie)
    - [Gepackte Torrents](#gepackte-torrents)
    - [Wiederholte Downloads](#wiederholte-downloads)
    - [Usenet-Download wird nicht importiert](#usenet-download-wird-nicht-importiert)
    - [Download-Client löscht Elemente](#download-client-löscht-elemente)
    - [Download kann keinem Bibliothekselement zugeordnet werden](#download-kann-keinem-bibliothekselement-zugeordnet-werden)
    - [Verbindungstimeout](#verbindungstimeout)
  - [Nicht aufgeführtes Problem](#nicht-aufgeführtes-problem)
- [Suchen, Indexer und Tracker](#suchen-indexer-und-tracker)
  - [Protokollierung erhöhen](#protokollierung-erhöhen)
  - [Indexer oder Tracker testen](#indexer-oder-tracker-testen)
  - [Suche testen](#suche-testen)
  - [Häufige Probleme](#häufige-probleme-1)
    - [Medien sind nicht überwacht](#medien-sind-nicht-überwacht)
    - [Tracker benötigt RawSearch Caps](#tracker-benötigt-rawsearch-caps)
    - [Falsche Kategorien](#falsche-kategorien)
    - [Falsche Ergebnisse](#falsche-ergebnisse)
    - [Erfolgreiche Abfrage - Keine Ergebnisse zurückgegeben](#erfolgreiche-abfrage-keine-ergebnisse-zurückgegeben)
    - [Fehlende Ergebnisse](#fehlende-ergebnisse)
    - [Zertifikatsvalidierung](#zertifikatsvalidierung)
    - [Rate Limits erreicht](#rate-limits-erreicht)
    - [IP-Sperre](#ip-sperre)
    - [Verwendung des Jackett /all-Endpunkts](#verwendung-des-jackett-all-endpunkts)
    - [Verwendung von NZBHydra2 als einzelner Eintrag](#verwendung-von-nzbhydra2-als-einzelner-eintrag)
    - [Nicht aufgeführtes Problem](#nicht-aufgeführtes-problem-1)
  - [Fehler](#fehler)
    - [Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist aufgetreten](#die-zugrunde-liegende-verbindung-wurde-geschlossen-ein-unerwarteter-fehler-ist-aufgetreten)
    - [Die Anforderung hat das Zeitlimit überschritten](#die-anforderung-hat-das-zeitlimit-überschritten)
    - [Nicht aufgeführtes Problem](#nicht-aufgeführtes-problem-2)

# Hilfe anfordern

Benötigen Sie Hilfe? Das ist in Ordnung, jeder braucht manchmal Hilfe. Sie können in Echtzeit Hilfe über den Chat erhalten auf

- [<i class="fab fa-discord"></i>&emsp;Discord *Offizieller Lidarr-Discord*](https://lidarr.audio/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offizieller Lidarr-Subreddit*](https://reddit.com/r/lidarr)
{.links-list}

Bevor Sie dorthin gehen und einen Beitrag veröffentlichen, stellen Sie sicher, dass Ihre Hilfsanfrage so gut wie möglich ist. Beschreiben Sie das Problem klar und geben Sie eine kurze Beschreibung Ihrer Konfiguration an, einschließlich Dingen wie Ihrem Betriebssystem/Verteilung, Version von .NET, Version von Lidarr, Download-Client und dessen Version. **Wenn Sie [Docker](https://www.docker.com/) verwenden, führen Sie bitte zuerst den [Docker-Leitfaden](/docker-guide) durch, da dies häufig auftretende Pfad-/Berechtigungsprobleme löst. Andernfalls halten Sie bitte ein [Docker Compose](/docker-guide#docker-compose) bereit. [So generieren Sie ein Docker Compose](https://trash-guides.info/compose)** Erzählen Sie uns, was Sie bereits versucht haben, wonach Sie gesucht haben. Verwenden Sie den Abschnitt [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien), um Ihre Protokollierung auf Trace-Niveau zu erhöhen, das Problem zu reproduzieren, den relevanten Kontext auf Pastebin hochzuladen und einen Link in Ihrem Beitrag anzugeben. Vielleicht fügen Sie sogar einige Screenshots hinzu, um das Problem zu verdeutlichen.

Je mehr wir wissen, desto einfacher ist es, Ihnen zu helfen.

# Protokollierung und Protokolldateien

Es ist wahrscheinlich sinnvoll, auch die häufigen Probleme bei der Fehlerbehebung zu überprüfen:
- [Häufige Probleme bei Downloads und Importieren](#häufige-probleme)
- [Häufige Probleme bei der Suche nach Indexern und Trackern](#häufige-probleme-1)
{.links-list}

Wenn Sie nach Debug-Protokollen gefragt werden, enthalten Ihre Protokolle `debug` und wenn Sie nach Trace-Protokollen gefragt werden, enthalten Ihre Protokolle `trace`. Wenn die von Ihnen bereitgestellten Protokolle dies nicht enthalten, handelt es sich nicht um die angeforderten Protokolle.

- Vermeiden Sie es, die gesamte Protokolldatei zu teilen, es sei denn, Sie werden dazu aufgefordert.
- Laden Sie Protokolle nicht direkt in Discord hoch oder fügen Sie sie als Textwände ein, es sei denn, Sie werden dazu aufgefordert.
- Teilen Sie die Protokolle nicht als Anhang, als Zip-Archiv oder in irgendeiner anderen Form als Text, der über die unten genannten Dienste geteilt wird.

Um gute und nützliche Protokolle für die Weitergabe bereitzustellen:

> Stellen Sie sicher, dass keine spammy Aufgabe ausgeführt wird, wie z.B. ein RSS-Refresh
{.is-warning}

1. [Erhöhen Sie die Protokollierung auf Trace-Niveau (Einstellungen => Allgemein => Protokollstufe oder Bearbeiten der Konfigurationsdatei)](#trace-debug-protokolle)
2. [Protokolle löschen (System => Protokolle => Protokolle löschen oder Löschen aller Protokolle im Protokollordner)](#protokolle-löschen)
3. Reproduzieren Sie das Problem (Wiederholen Sie, was die Dinge kaputt macht)
4. [Öffnen Sie die Trace-Protokolldatei (Lidarr.trace.txt) über die Benutzeroberfläche oder die Protokolldatei](#standard-protokolldateien) im Dateisystem und finden Sie den relevanten Kontext
5. Kopieren Sie einen großen Abschnitt vor dem Problem, das Problem selbst und einen großen Abschnitt nach dem Problem.
6. Verwenden Sie [Gist](https://gist.github.com/), [0bin (**Stellen Sie sicher, dass die Colorierung deaktiviert ist**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) oder ähnliche Websites - mit Ausnahme der unten angegebenen Websites - um die kopierten Protokolle von oben zu teilen

**Warnungen:**
- **Verwenden Sie nicht [pastebin.com](https://pastebin.com), da deren Filter dazu neigen, die Protokolle zu blockieren.
- Verwenden Sie nicht [pastebin.pl](https://pastebin.pl), da ihre Website häufig nicht erreichbar ist.
- Verwenden Sie nicht [JustPasteIt](https://justpaste.it/), da ihre Website das Überprüfen von Protokollen nicht erleichtert.
- Laden Sie Ihr Protokoll nicht als Datei hoch.
- Laden Sie Ihre Protokolle nicht über Google Drive, Dropbox oder eine andere nicht oben genannte Website hoch und teilen Sie sie.
- Archivieren Sie Ihre Protokolle nicht (zip, tar (tarball), 7zip usw.).
- Teilen Sie keine Konsolenausgabe, Docker-Container-Ausgabe oder etwas anderes als die angegebenen Anwendungsprotokolle

**Wichtiger Hinweis:**
- Wenn Sie [0bin](https://0bin.net/) verwenden, stellen Sie sicher, dass die Colorierung deaktiviert ist und brennen Sie nach dem Lesen nicht.

- Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie N++ verwenden. Sie können die Funktion "In Dateien suchen" von Notepad++ verwenden, um bei Bedarf in alten Protokolldateien zu suchen.
- **Nur Unix:** Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie grep verwenden. Wenn Sie beispielsweise Informationen über den Film/die Serie/das Buch/das Lied/den Indexer "Shooter" finden möchten, können Sie den folgenden Befehl ausführen: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Wenn Ihr [Appdata-Verzeichnis](/lidarr/appdata-directory) in Ihrem Home-Verzeichnis liegt, führen Sie Folgendes aus: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Die Flags haben folgende Funktionen
    * -i: Groß-/Kleinschreibung ignorieren
    * -n: Zeilennummer anzeigen
    *  -r: rekursiv alle Dateien im Pfad überprüfen
    * -C: Anzahl der Zeilen vor und nach der gefundenen Zeile angeben
    * -e: das zu suchende Muster

```

## Standard-Protokolldateien

Die Protokolldateien befinden sich im [Appdata-Verzeichnis](/lidarr/appdata-directory) von Lidarr, im Ordner logs/. Sie können auch über die Benutzeroberfläche unter System => Protokolle => Dateien auf die Protokolldateien zugreifen.

> Hinweis: Die Protokolltabelle ("Ereignisse") in der Benutzeroberfläche ist nicht dasselbe wie die Protokolldateien und nicht so nützlich. Wenn Sie nach Protokollen gefragt werden, kopieren Sie bitte aus den Protokolldateien und nicht aus der Tabelle.
{.is-info}

## Update-Protokolldateien

Die Update-Protokolldateien befinden sich im [Appdata-Verzeichnis](/lidarr/appdata-directory) von Lidarr, im Ordner UpdateLogs/.

## Protokolle teilen

Die Protokolle können in Foren- oder Reddit-Beiträgen lang und schwer lesbar sein und in Discord Spam verursachen. Verwenden Sie daher bitte [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) oder eine ähnliche Pastebin-Website. In der Regel ist nicht die gesamte Datei erforderlich, sondern nur ein guter Teil des Kontexts vor und nach dem Problem/Fehler. Vergessen Sie nicht, auf das Ende von spammy Aufgaben wie einer RSS-Synchronisierung oder Aktualisierung der Bibliothek zu warten.

## Trace-/Debug-Protokolle

Sie können die Protokollstufe unter Einstellungen => Allgemein => Protokollierung ändern. Lidarr muss nicht neu gestartet werden, damit die Änderung wirksam wird. Diese Änderung betrifft nur die Protokolldateien, nicht die Protokolldatenbank. Die neuesten Debug-/Trace-Protokolldateien haben die Namen `lidarr.debug.txt` bzw. `lidarr.trace.txt`.

Wenn Sie nicht auf die Benutzeroberfläche zugreifen können, um die Protokollierungsstufe festzulegen, können Sie dies tun, indem Sie die Datei config.xml im AppData-Verzeichnis bearbeiten und den Wert LogLevel auf Debug oder Trace anstelle von Info setzen.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Protokolle löschen

Sie können Protokolldateien und die Protokolldatenbank direkt über die Benutzeroberfläche unter System => Protokolle => Dateien und System => Protokolle => Löschen (Mülleimer-Symbol) löschen.

# Mehrere Protokolldateien

Lidarr verwendet rollende Protokolldateien, die auf jeweils 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer `lidarr.txt`, für die anderen Dateien ist `.0.txt` die nächstneuere (je höher die Zahl, desto älter ist sie). Diese Protokolldatei enthält Einträge für `fatal`, `error`, `warn` und `info`.

Wenn die Debug-Protokollierung aktiviert ist, sind zusätzliche rollende Protokolldateien `lidarr.debug.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info` und `debug`. Sie decken in der Regel einen Zeitraum von 40 Stunden ab.

Wenn die Trace-Protokollierung aktiviert ist, sind zusätzliche rollende Protokolldateien `lidarr.trace.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info`, `debug` und `trace`. Aufgrund der Trace-Verbosity decken sie in der Regel höchstens ein paar Stunden ab.

# Wiederherstellung nach einem fehlgeschlagenen Update

Wir tun alles, um Probleme bei der Aktualisierung zu vermeiden, aber wenn sie auftreten, führen Sie die folgenden Schritte aus, um Ihre Installation wiederherzustellen.

## Das Problem ermitteln

- Der beste Ort, um nachzusehen, wenn die Anwendung nach einem Update nicht startet, ist das Überprüfen der [Update-Protokolle](#update-protokolldateien), um festzustellen, ob das Update erfolgreich abgeschlossen wurde. Wenn diese keine Probleme aufweisen, ist der nächste Schritt das Überprüfen Ihrer regulären Anwendungsprotokolldateien. Erhöhen Sie vor dem erneuten Starten die Protokollierung mit [Protokollierung](/lidarr/settings#protokollierung) und [Protokolldateien](/lidarr/system#protokolldateien), um sie zu finden und die Protokollierungsstufe zu erhöhen.
- Das am häufigsten auftretende Problem ist, dass das System, auf dem die Anwendung installiert ist, das `/tmp`-Verzeichnis manipuliert und während des Upgrades kritische \*Arr-Dateien gelöscht hat, was sowohl das Upgrade als auch das Rollback zum Scheitern bringt. In diesem Fall installieren Sie einfach die Anwendung erneut über der vorhandenen fehlerhaften Installation.

### Migrationsproblem

- Migrationsfehler sind nicht identisch, aber hier ist ein Beispiel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Berechtigungsproblem

- Berechtigungsprobleme treten auf, wenn die Anwendung keinen Zugriff auf die relevanten temporären Ordner und/oder den Anwendungs-Binärordner hat. Beheben Sie die Berechtigungen, damit der Benutzer/die Gruppe, unter der die Anwendung ausgeführt wird, den entsprechenden Zugriff hat.

- Synology-Benutzer können auf diesen Synology-Bug stoßen: `Access to the path '/proc/{some number}/maps is denied`

- Synology-Benutzer können auch auf Platzmangel in `/tmp` auf bestimmten NAS-Geräten stoßen. Sie müssen einen anderen Pfad für `/tmp` für die Anwendung angeben. Wenden Sie sich an die SynoCommunity oder andere Synology-Supportkanäle, um Hilfe zu erhalten.

## Das Problem beheben

Bei einem Migrationsproblem können Sie zunächst nicht viel tun. Wenn das Problem spezifisch für Sie ist (oder es noch keine Beiträge dazu gibt), erstellen Sie bitte einen Beitrag in [unserem Subreddit](https://reddit.com/r/lidarr) oder kommen Sie in unserem [Discord](https://lidarr.audio/discord) vorbei. Wenn es andere mit dem gleichen Problem gibt, können Sie sicher sein, dass wir daran arbeiten.

> Bitte stellen Sie sicher, dass Sie nicht versucht haben, eine Datenbank von `nightly` in der stabilen Version zu verwenden. Das Wechseln zwischen Branches ist nicht ratsam.{.is-info}

### Berechtigungsprobleme

- Beheben Sie die Berechtigungen, um sicherzustellen, dass der Benutzer/die Gruppe, unter der die Anwendung ausgeführt wird, sowohl auf `/tmp` als auch auf das Installationsverzeichnis der Anwendung zugreifen kann (Lesen und Schreiben).

- Synology-Benutzer, die Probleme mit `/proc/###/maps` haben, können dies beheben, indem sie Lidarr oder die anderen \*Arr-Anwendungen anhalten und aktualisieren. Dies ist ein Problem mit dem SynoCommunity-Paket.

### Manuelles Upgrade

Laden Sie die neueste Version von unserer Website herunter.

Installieren Sie das Update (.exe) oder extrahieren Sie den Inhalt (.zip) über Ihre bestehende Installation und führen Sie Lidarr wie gewohnt erneut aus.

# Downloads und Import

Der Download und Import ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss Lidarr in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Setups. Das bedeutet, dass es zwar einige gängige Setups gibt, aber kein einziges richtiges Setup und jedes Setup ein wenig anders sein kann.

> **Der erste Schritt besteht darin, das Logging auf Trace-Ebene zu erhöhen. Weitere Informationen zum Anpassen des Loggings und zum Durchsuchen von Logs finden Sie unter [Logging und Log-Dateien](#logging-und-log-dateien). Wiederholen Sie dann das Problem und verwenden Sie die Trace-Level-Logs aus diesem Zeitraum, um das Problem zu untersuchen.** Wenn Ihnen jemand hilft, geben Sie den Kontext vor/nach dem Problem in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website an, um es ihnen zu zeigen. Es muss nicht die gesamte Datei sein und es sollte nicht *nur* der Fehler sein. Wiederholen Sie das Problem auch, während Aufgaben, die die Log-Datei mit Spam füllen, nicht ausgeführt werden.
{.is-danger}

Wenn Sie Hilfe suchen, lesen Sie unbedingt [asking for help](#asking-for-help), damit Sie uns die benötigten Details zur Verfügung stellen können.

## Testen des Download-Clients

Stellen Sie sicher, dass Ihr(e) Download-Client(s) ausgeführt wird/laufen. Beginnen Sie mit dem Test des Download-Clients. Wenn es nicht funktioniert, können Sie Details in den Trace-Level-Logs sehen. Sie sollten eine URL finden, die Sie in Ihren Browser eingeben und überprüfen können, ob sie funktioniert. Es könnte ein Verbindungsproblem sein, das auf eine falsche IP-Adresse, einen falschen Hostnamen, einen falschen Port oder sogar eine Firewall hinweisen könnte. Es könnte offensichtlich sein, wie ein Authentifizierungsproblem, bei dem Sie den Benutzernamen, das Passwort oder den API-Schlüssel falsch eingegeben haben.

## Testen eines Downloads

Nun werden wir einen Download ausprobieren. Wählen Sie einen Song aus und führen Sie eine manuelle Suche durch. Wählen Sie eine dieser Dateien aus und versuchen Sie, sie herunterzuladen. Wird sie an den Download-Client gesendet? Wird sie in der richtigen Kategorie angezeigt? Erscheint sie in der Aktivität? Erscheint sie in den Trace-Level-Logs während der Aufgaben "Überprüfung abgeschlossener Downloads" (Aktualisierung überwachter Downloads und Verarbeitung überwachter Downloads), die ungefähr alle Minute ausgeführt werden? Wird sie während dieser Aufgabe korrekt analysiert? Hat der heruntergeladene Download einen vernünftigen Namen? Da Suchvorgänge auf einigen Indexern/Trackern nach ID durchgeführt werden, kann es vorkommen, dass ein Download mit einem Namen in die Warteschlange gestellt wird, den er nicht erkennen kann.

## Testen eines Imports

Importprobleme sollten fast immer als Eintrag in der Aktivität mit einem orangefarbenen Symbol angezeigt werden, auf das Sie mit der Maus zeigen können, um den Fehler zu sehen. Wenn sie nicht in der Aktivität angezeigt werden, sollten Sie sich zuerst auf dieses Problem konzentrieren und es lösen. Die meisten Importfehler sind *Berechtigungsprobleme*. Denken Sie daran, dass Lidarr Lese- und Schreibzugriff auf den Download-Ordner benötigt. Manchmal können auch Berechtigungen im Bibliotheksordner schuld sein, also überprüfen Sie bitte beides.

Auch falsche Pfadprobleme sind möglich, aber in normalen Setups weniger häufig. Der Schlüssel zum Verständnis von Pfadproblemen besteht darin zu wissen, dass Lidarr den Pfad zum Download *vom* Download-Client über dessen API erhält. Dies wird zu einem Problem in einzigartigen Anwendungsfällen, wie z.B. wenn der Download-Client auf einem anderen System (vielleicht sogar einem anderen Betriebssystem) läuft. Es kann auch in einer Docker-Umgebung auftreten, wenn die Volumes nicht korrekt konfiguriert sind. Eine Remote-Pfadzuordnung ist eine gute Lösung, wenn Sie keine Kontrolle haben, z.B. bei einer Seedbox-Konfiguration. Bei einer Docker-Umgebung ist das Beheben der Pfade eine bessere Option.

## Häufige Probleme

Hier sind einige häufige Probleme aufgeführt.

### Die Web-Benutzeroberfläche des Download-Clients ist nicht aktiviert

Lidarr kommuniziert mit Ihrem Download-Client über dessen API und greift über die Web-Benutzeroberfläche des Clients darauf zu. Sie müssen sicherstellen, dass die Web-Benutzeroberfläche des Clients aktiviert ist und der verwendete Port nicht mit anderen Client-Ports in Verwendung oder mit Ports auf Ihrem System in Konflikt steht.

### SSL wird verwendet und falsch konfiguriert

Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie sowohl Ihre Instanz als auch Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in [der SSL-FAQ](/lidarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues).

### Freigabe unter Windows nicht sichtbar

Der Standardbenutzer für einen Windows-Dienst ist `LocalService`, der in der Regel keinen Zugriff auf Ihre Freigaben hat. Bearbeiten Sie den Dienst und richten Sie ihn so ein, dass er unter Ihrem eigenen Benutzerkonto ausgeführt wird. Weitere Informationen finden Sie in der FAQ [Warum kann ich meine Dateien auf einem Remote-Server nicht sehen?](/lidarr/faq#why-cant-see-my-files-on-a-remote-server).

### Netzwerklaufwerke sind nicht zuverlässig

Obwohl Netzwerklaufwerke wie `X:\` praktisch sind, sind sie nicht so zuverlässig wie UNC-Pfade wie `\\server\share` und sie sind auch nicht vor der Anmeldung verfügbar. Konfigurieren Sie Ihren Download-Client so, dass er bei Bedarf UNC-Pfade verwendet. Wenn Ihre Bibliothek auf einem Netzwerkfreigabe liegt, stellen Sie sicher, dass Ihre Stammordner UNC-Pfade verwenden. Wenn Ihr Download-Client auf eine Freigabe sendet, müssen Sie dort UNC-Pfade konfigurieren, da Lidarr den Download-Pfad vom Download-Client erhält. Es ist in Ordnung, Ihre Netzwerklaufwerke für sich selbst zu verwenden, verwenden Sie sie jedoch nicht für die Automatisierung.

### Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade

Docker fügt eine weitere Ebene von Komplexität hinzu, die leicht falsch konfiguriert werden kann, aber dennoch zu einer funktionierenden Einrichtung führt, die verschiedene Probleme aufweist. Anstatt sie hier zu erläutern, lesen Sie diesen Wiki-Artikel [für diese Automatisierungssoftware und Docker](/docker-guide), der sich mit Benutzer, Gruppe, Besitz, Berechtigungen und Pfaden befasst. Er ist nicht spezifisch für ein bestimmtes Docker-System, sondern behandelt die Dinge auf einer hohen Ebene, damit Sie sie in Ihrer eigenen Umgebung implementieren können.

### Remote-Pfadzuordnung

Wenn Sie Lidarr in Docker und den Download-Client in einem Nicht-Docker-Container (oder umgekehrt) haben oder die Programme auf verschiedenen Servern haben, benötigen Sie möglicherweise eine Remote-Pfadzuordnung.

Die Logs sehen wie folgt aus:

```none
2022-02-03 14:03:54.3|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /volume3/data/torrents/music/Five Finger Death Punch - F8 (2020) FLAC. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Daher existiert `/volume3/data` nicht in Lidarrs Container oder ist nicht zugänglich.

- [Einstellungen => Download-Clients => Remote-Pfadzuordnungen](/lidarr/settings#remote-path-mappings)
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht auf diesen Ordner verweist.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft, während \*Arr auf Windows oder umgekehrt läuft. Eine Remote-Pfadzuordnung ist auch möglicherweise erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine einfache Suchen/Ersetzen-Funktion (sie sucht nach dem REMOTE-Wert und ersetzt ihn durch den LOCAL-Wert für den angegebenen Host).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie in TRaSH's Tutorial](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist eine Remote-Pfadzuordnung selten erforderlich. Es wird empfohlen, [den Docker Guide](/docker-guide) zu überprüfen und/oder [TRaSH's Tutorial](https://trash-guides.info/hardlinks) zu befolgen.
{.is-info}

#### Remote-Mount oder Remote-Synchronisation (Syncthing)

- Sie müssen sicherstellen, dass es die ganze Zeit synchronisiert wird, während es herunterlädt. Und Sie müssen sicherstellen, dass das lokale Synchronisationsziel beim Import von \*Arr als Festplattenverknüpfungen verwendet werden kann, d.h. dass es dasselbe Dateisystem hat und so aussieht.
  - Synchronisieren Sie in einem niedrigeren, gemeinsamen Ordner, der sowohl unvollständige als auch vollständige Dateien enthält.
  - Synchronisieren Sie an einen Speicherort, der auf demselben Dateisystem lokal wie Ihre Bibliothek liegt und so aussieht (Docker und Netzwerkfreigaben machen es leicht, dies falsch zu konfigurieren).
  - Sie möchten die unvollständigen und vollständigen Dateien synchronisieren, damit, wenn der Torrent-Client den Verschiebevorgang durchführt, dies lokal reflektiert wird und alle Dateien bereits "dort" sind (auch wenn sie noch heruntergeladen werden). Dann möchten Sie Festplattenverknüpfungen verwenden, weil selbst wenn der Import vor Abschluss erfolgt, werden sie trotzdem fertiggestellt.
  - Auf diese Weise wird während des gesamten Herunterladens synchronisiert, dann verschiebt der Torrent-Client in den TV-Unterordner und die Synchronisierung spiegelt das wider. Auf diese Weise sind die Downloads größtenteils vorhanden, wenn sie als abgeschlossen deklariert werden. Und selbst wenn sie noch nicht ganz fertig sind, ist es in Ordnung, dass die Festplattenverknüpfung möglich ist.
  - (Optional - falls zutreffend und/oder erforderlich (z.B. bei Verwendung eines Remote-Usenet-Clients)) Konfigurieren Sie ein benutzerdefiniertes Skript, das beim Import/Download/Upgrade ausgeführt wird, um die Remote-Datei zu entfernen.
- Alternativ ist eine Remote-Mount-Einrichtung anstelle einer Remote-Synchronisation deutlich weniger kompliziert zu konfigurieren, aber in der Regel langsamer.
  - Mounten Sie Ihren Remote-Speicher mit sshfs oder einem anderen Netzdateisystemprotokoll.
  - Stellen Sie sicher, dass der Benutzer und die Gruppe, unter der \*Arr ausgeführt wird, Lese- oder Schreibzugriff haben.
  - Konfigurieren Sie eine Remote-Pfadzuordnung, um den REMOTE-Pfad zu finden und durch den entsprechenden LOCAL-Wert zu ersetzen.

### Berechtigungen auf dem Bibliotheksordner

Die Logs sehen wie folgt aus:

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/media/music/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Vergessen Sie nicht, die Berechtigungen und den Besitz des *Zielordners* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Downloads zu fixieren, und das ist *in der Regel* die Ursache für Berechtigungsprobleme, aber es *könnte* auch das Ziel sein. Überprüfen Sie, ob die Zielordner existieren. Überprüfen Sie, ob eine Ziel-*Datei* bereits vorhanden ist oder nicht gelöscht oder in den Papierkorb verschoben werden kann. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren, das Erstellen von Festplattenverknüpfungen oder das Verschieben der heruntergeladenen Datei zulassen. Der Benutzer oder die Gruppe, unter der \*Arr ausgeführt wird, muss in der Lage sein, den Stammordner zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies daran liegen, dass es als Dienst ausgeführt wird:
  - Der Windows-Dienst wird standardmäßig unter dem Konto "Local Service" ausgeführt. Dieses Konto hat standardmäßig keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Download-Clients verwendet werden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "Local Service" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die Anwendung als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten. Weitere Informationen finden Sie in der FAQ, wie Sie von einem Dienst zu einer Tray-Anwendung wechseln können.

- Für Synology-Benutzer siehe [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Berechtigungen auf dem Download-Ordner

Die Logs sehen wie folgt aus:

```none
2022-02-28 18:51:01.1|Error|DownloadedTracksImportService|Import failed, path does not exist or is not accessible by Lidarr: /data/downloads/music/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Lidarr has the correct permissions to access this file/folder
```

Vergessen Sie nicht, die Berechtigungen und den Besitz der *Quelle* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Ziels zu fixieren, und das ist eine *mögliche* Ursache für Berechtigungsprobleme, aber in der Regel liegt es an der Quelle. Überprüfen Sie, ob die Quellordner existieren. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren/Erstellen von Festplattenverknüpfungen oder das Kopieren+Löschen/Verschieben der Datei zulassen. Der Benutzer oder die Gruppe, unter der \*Arr ausgeführt wird, muss in der Lage sein, den Download-Ordner zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies daran liegen, dass es als Dienst ausgeführt wird:
  - Der Windows-Dienst wird standardmäßig unter dem Konto "Local Service" ausgeführt. Dieses Konto hat standardmäßig keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Download-Clients verwendet werden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "Local Service" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die Anwendung als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten. Weitere Informationen finden Sie in der FAQ, wie Sie von einem Dienst zu einer Tray-Anwendung wechseln können.

- Für Synology-Benutzer siehe [SynoCommunity's Permissions Article for their Packages](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Download-Ordner und Bibliotheksordner sind nicht unterschiedliche Ordner

Der Download-Client sollte in einen Ordner herunterladen, auf den \*Arr zugreifen kann, und dieser Ordner sollte nicht Ihr Stamm-/Bibliotheksordner sein. \*Arr sollte aus diesem separaten Download-Ordner in Ihren Bibliotheksordner importieren.

Sie sollten niemals direkt in Ihren Stammordner herunterladen. Sie sollten Ihren Stammordner auch nicht als den abgeschlossenen Ordner oder den unvollständigen Ordner des Download-Clients verwenden.

> Ihr Download-Ordner und Ihr Stamm-/Bibliotheksordner MÜSSEN getrennt sein.
{.is-warning}

### Falsche Kategorie

Lidarr sollte so eingerichtet sein, dass es eine Kategorie verwendet, damit es nur versucht, seine eigenen Downloads zu verarbeiten. Es ist selten, dass ein von hinzugefügter Torrent ohne die richtige Kategorie hinzugefügt wird, aber es kann vorkommen. Wenn Sie Torrents manuell hinzufügen und sie verarbeiten möchten, müssen sie die richtige Kategorie haben. Sie kann jederzeit festgelegt werden, da Lidarr versucht, Downloads alle Minute zu verarbeiten.

### Gepackte Torrents

Die Logs zeigen Fehler wie

```none
No files found are eligible for import
```

Wenn Ihr Torrent in `.rar`-Dateien gepackt ist, müssen Sie die Entpackung einrichten. Wir empfehlen [Unpackerr](https://github.com/unpackerr/unpackerr), da es die Entpackung richtig durchführt: Es verhindert beschädigte teilweise Importe und räumt die entpackten Dateien nach dem Import auf.

Der Fehler kann auch auftreten, wenn sich keine gültige Mediendatei im Ordner befindet.

### Wiederholte Downloads

Es gibt einige Ursachen für wiederholte Downloads, aber eine davon hängt mit der Indexer-Beschränkung in den Release-Profilen zusammen. Da der Indexer *nicht* mit den Daten gespeichert wird, sind alle bevorzugten Wortbewertungen für Medien in Ihrer Bibliothek *null*, aber während "RSS" und Suche werden sie angewendet. Dadurch geraten Sie in eine Schleife, in der Sie die Elemente immer wieder herunterladen, weil es wie ein Upgrade aussieht, dann keines ist, dann wieder auftaucht und wie ein Upgrade aussieht, dann keines ist. Beschränken Sie Ihr Release-Profil nicht auf einen Indexer.

Dies kann auch darauf zurückzuführen sein, dass der Download nie tatsächlich importiert wird und dann aus der Warteschlange verschwindet, sodass ein neuer Download ständig heruntergeladen und nie importiert wird. Bitte beachten Sie die verschiedenen anderen häufigen Probleme und Fehlerbehebungsschritte dafür.

### Usenet-Download wird nicht importiert

Lidarr betrachtet nur die 60 neuesten Downloads in SABnzbd und NZBGet. Wenn Sie Ihre Historie *behalten*, bedeutet dies, dass während großer Warteschlangen mit Importproblemen Downloads stillschweigend verpasst und nicht importiert werden können. Der beste Weg, dies zu vermeiden, besteht darin, Ihre Historie zu löschen, damit alle noch vorhandenen Elemente untersucht werden müssen. Sie können dies erreichen, indem Sie unter "Abgeschlossene und fehlgeschlagene Download-Handler" die Option "Entfernen" aktivieren. Bei NZBGet werden die Elemente dann in die *versteckte* Historie verschoben, was großartig ist. Leider verfügt SABnzbd nicht über eine ähnliche Funktion. Das Beste, was Sie dort erreichen können, ist die Verwendung des NZB-Backup-Ordners.

### Download-Client löscht Elemente



Der Download-Client sollte *nicht* für das Entfernen von Downloads verantwortlich sein. Usenet-Clients sollten so konfiguriert sein, dass sie Downloads nicht aus dem Verlauf entfernen. Torrent-Clients sollten so eingestellt sein, dass sie Torrents nicht entfernen, wenn sie mit dem Seeding fertig sind (stattdessen pausieren oder stoppen). Dies liegt daran, dass Lidarr mit dem Download-Client kommuniziert, um zu wissen, was importiert werden soll. Wenn die Downloads entfernt werden, gibt es nichts zu importieren... selbst wenn sich ein Ordner mit Dateien befindet.

Bei SABnzbd wird dies mit der Einstellung "History Retention" gehandhabt.

### Download kann keinem Bibliothekseintrag zugeordnet werden

Aus verschiedenen Gründen können Releases nach dem Herunterladen und Senden an den Download-Client nicht analysiert werden. Aktivität => Optionen => "Show Unknown" (dies ist in neueren Versionen standardmäßig aktiviert) zeigt alle Elemente an, die nicht anderweitig ignoriert/ bereits importiert wurden, innerhalb der Kategorie des Download-Clients von Lidarr. Diese müssen in der Regel manuell zugeordnet und importiert werden.

Dies kann auch auftreten, wenn Sie ein Release in Ihrem Download-Client haben, aber dieses Medienelement (Film/Folge/Buch/Song) nicht in der Anwendung existiert.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist bei einem Sendevorgang aufgetreten

Dies wird durch den Indexer verursacht, der ein von der aktuellen .NET-Version in [Lidarr => System => Status](/lidarr/system#status) nicht unterstütztes SSL-Protokoll verwendet.

### Die Anforderung hat das Zeitlimit überschritten

Lidarr erhält keine Antwort vom Indexer.

```none
System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten: ’https://example.org/api?t=caps&apikey=(entfernt) —> System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Verbindung zum Indexer nicht möglich

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen.
```

Dies kann auch durch folgende Ursachen verursacht werden:

- Falsche Konfiguration oder Verwendung eines VPNs
- Falsche Konfiguration oder Verwendung eines Proxys
- Lokale DNS-Probleme - Versuchen Sie, einen anderen DNS-Anbieter zu verwenden
- Lokale IPv6-Probleme - normalerweise ist IPv6 aktiviert, aber nicht funktionsfähig
- Die Verwendung von Privoxy und eine falsche Konfiguration davon

## Problem nicht aufgelistet

Sie können auch einige gängige Berechtigungs- und Netzwerkprobleme [in unserem Leitfaden](/permissions-and-networking) überprüfen. Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem sein könnte, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.

# Indexer und Tracker durchsuchen

- Wenn Sie [Prowlarr](/prowlarr) verwenden, können Sie die [History](/prowlarr/history) aller Abfragen anzeigen, die Prowlarr erhalten hat und wie sie an die Websites gesendet wurden. Stellen Sie sicher, dass in den Prowlarr-Einstellungen unter History => Options "Parameters" aktiviert ist. Das (i)-Symbol bietet zusätzliche Details.

## Protokollierung auf Trace-Niveau erhöhen

> **Der erste Schritt besteht darin, die Protokollierung auf Trace-Niveau zu erhöhen. Weitere Informationen zur Anpassung der Protokollierung und zum Durchsuchen von Protokollen finden Sie unter [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien). Wiederholen Sie dann das Problem und verwenden Sie die Protokolle auf Trace-Niveau aus diesem Zeitraum, um das Problem zu untersuchen.** Wenn Ihnen jemand hilft, geben Sie den Kontext vor/nach dem Problem in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website an, um es ihnen zu zeigen. Es muss nicht die gesamte Datei sein und es sollte nicht *nur* der Fehler sein. Sie sollten das Problem auch reproduzieren, während keine Aufgaben ausgeführt werden, die das Protokoll spammen.
{.is-danger}

## Testen eines Indexers oder Trackers

Wenn Sie einen Indexer oder Tracker testen, finden Sie in den Debug- oder Trace-Protokollen die verwendete URL. Ein Beispiel für einen erfolgreichen Test finden Sie unten. Sie können sehen, dass er den Indexer über eine bestimmte URL mit bestimmten Parametern abfragt und dann die Antwort erhält. Sie können diese URL in Ihrem Browser testen, indem Sie `apikey=(entfernt)` durch den richtigen API-Schlüssel wie `apikey=123` ersetzen. Sie können mit den Parametern experimentieren, wenn Sie einen Fehler vom Indexer erhalten oder überprüfen möchten, ob Sie Konnektivitätsprobleme haben, wenn es überhaupt nicht funktioniert. Nachdem Sie es in Ihrem eigenen Browser getestet haben, sollten Sie es auch von dem System aus testen, auf dem Lidarr ausgeführt wird, *wenn* Sie dies noch nicht getan haben.

## Testen einer Suche

Ähnlich wie beim oben beschriebenen Indexer/Tracker-Test können Sie bei der Auslösung einer Suche im Debug- oder Trace-Protokoll die verwendete URL aus den Protokolldateien erhalten. Beim Testen ist es am besten, eine so spezifische Suche wie möglich durchzuführen. Eine manuelle Suche ist gut, weil sie spezifisch ist und Sie die Ergebnisse in der Benutzeroberfläche sehen können, während Sie die Protokolle untersuchen.

Bei diesem Test suchen Sie nach offensichtlichen Fehlern und führen einige einfache Tests durch. Sie können sehen, dass die Suche die URL ***AKTUALISIERTE URL FÜR MUSIK BENÖTIGT - DIES IST EIN SONARR URL-BEISPIEL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(entfernt)&offset=0&limit=100&tvdbid=354629&season=1&ep=1` verwendet, die Sie selbst in einem Browser ausprobieren können, nachdem Sie (entfernt) durch Ihren API-Schlüssel für diesen Indexer ersetzt haben. Funktioniert es? Sehen Sie die erwarteten Ergebnisse? Gilt dieser FAQ-Eintrag? In dieser URL können Sie sehen, dass bestimmte Kategorien mit `cat=5030,5040,5045,5080` festgelegt wurden. Wenn Sie also nicht die erwarteten Ergebnisse sehen, ist dies ein wahrscheinlicher Grund. Sie können auch sehen, dass nach der tvdbid mit `tvdbid=354629` gesucht wurde. Wenn die Episode auf dem Indexer nicht richtig kategorisiert ist, muss dies behoben werden. Sie können auch sehen, dass nach einer bestimmten Staffel und Episode mit season=1 und ep=1 gesucht wird. Wenn dies auf dem Indexer nicht korrekt ist, sehen Sie diese Ergebnisse nicht. Schauen Sie sich das Beispiel für die XML-Ausgabe einer manuellen Suche unten an, um ein Beispiel für die Ausgabe einer funktionierenden Abfrage zu sehen.

- Beispiel für XML-Ausgabe einer manuellen Suche

```xml
BEISPIEL FÜR INDEXER-SUCHE AUSGABE ERFORDERLICH
```

***Bilder erforderlich***

![searches-indexers-and-trackers1.png](/assets/lidarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/lidarr/searches-indexers-and-trackers2.png)

- Ausschnitt aus dem Trace-Protokoll

```none
Ausschnitt aus dem Trace-Protokoll für eine manuelle Suche erforderlich
```

- Vollständiges Trace-Protokoll einer Suche

```none
Vollständiger Abschnitt des Trace-Protokolls für eine manuelle Suche erforderlich
```

## Häufige Probleme

Hier sind einige häufige Probleme aufgeführt.

### Medien sind nicht überwacht

Das/die Lied(er) wird/werden nicht überwacht.

### Tracker benötigt RawSearch-Fähigkeiten

- Lidarr sucht nach `Kikis Delivery Service`, aber Ihr Tracker hat nur Ergebnisse für `Kiki's Delivery Service`.
- Dies liegt daran, dass Ihr Tracker keine normalen standardisierten Suchen unterstützt.
- Die Lösung besteht darin, die Suchfähigkeiten der Definition Ihres Trackers zu aktualisieren, um anzuzeigen, dass er `RawSearch` erfordert und unterstützt.
- Jackett unterstützt diese Funktion, aber die Fähigkeiten müssen für jeden Indexer aktualisiert werden. Erstellen Sie eine Feature-Anfrage für Jackett, um diese Funktionalität für Ihren Indexer hinzuzufügen.
- Prowlarr unterstützt diese Funktion, aber die Fähigkeiten müssen für jeden Indexer aktualisiert werden. Erstellen Sie eine Feature-Anfrage für Prowlarr, um diese Funktionalität für Ihren Indexer hinzuzufügen.

### Falsche Kategorien

Falsche Kategorien sind wahrscheinlich die häufigste Ursache dafür, dass Ergebnisse in manuellen Suchen eines Indexers/Trackers angezeigt werden, aber nicht in Lidarr. Der Indexer/Tracker sollte die Kategorie in den Suchergebnissen anzeigen, was Ihnen helfen sollte, herauszufinden, was fehlt. Wenn Sie Jackett oder Prowlarr verwenden, hat jeder Tracker eine Liste der speziell unterstützten Kategorien. Stellen Sie sicher, dass Sie die richtigen Kategorien verwenden. Viele finden es hilfreich, die Liste in einem Browserfenster sichtbar zu haben, während sie den Eintrag bearbeiten.

### Falsche Ergebnisse

Manchmal liefert der Indexer völlig irrelevante Ergebnisse, obwohl Lidarr Parameter zur Begrenzung der Suche angibt. Oder manchmal sind die Ergebnisse größtenteils relevant, aber mit einigen falschen Ergebnissen. Das erste ist in der Regel ein Problem des Indexers, das Sie anhand der Trace-Protokolle erkennen können. Sie können diesen Indexer deaktivieren und das Problem melden. Das andere ist in der Regel kategorisierte Releases, die auf dem Indexer/Tracker gemeldet werden sollten.

### Abfrage erfolgreich - Keine Ergebnisse zurückgegeben

Sie erhalten eine Meldung ähnlich wie "Abfrage erfolgreich, aber es wurden keine Ergebnisse von Ihrem Indexer zurückgegeben. Dies kann ein Problem mit dem Indexer oder Ihren Indexer-Kategorieeinstellungen sein."

Dies wird verursacht, wenn Ihr Indexer keine Ergebnisse zurückgibt, die in den von Ihnen für den Indexer konfigurierten Kategorien liegen.

### Fehlende Ergebnisse

Wenn Sie Ergebnisse auf der Website finden, die in Lidarr nicht angezeigt werden, ist Ihr Problem wahrscheinlich eines der folgenden:

- [Falsche Kategorien - siehe oben](#falsche-kategorien)
- Es wird eine ID-basierte Suche durchgeführt und der Indexer hat die Releases nicht korrekt dieser ID zugeordnet. Dies ist etwas, das nur Ihr Indexer lösen kann. Er muss sicherstellen, dass das Release den richtigen zutreffenden IDs zugeordnet ist.
- Sie suchen nicht so, wie Lidarr sucht. Es ist sehr wahrscheinlich, dass die Begriffe, nach denen Sie auf dem Indexer suchen, nicht der Art und Weise entsprechen, wie Lidarr danach sucht. Sie können sehen, wie Lidarr in den Trace-Protokollen sucht. Textbasierte Abfragen haben in der Regel das Format `q=Wörter%20und%20Dinge%20hier`. Diese Zeichenkette ist HTTP-codiert und kann mit einem beliebigen Online-HTML-Codierungs/-Decodierungstool einfach decodiert werden.

### Zertifikatsvalidierung

Sie werden sich mit den meisten Indexern/Trackern über https verbinden, daher müssen Sie sicherstellen, dass dies auf Ihrem System ordnungsgemäß funktioniert. Das bedeutet, dass Ihre Zeitzone und Ihre Uhrzeit *korrekt* eingestellt sein müssen. Außerdem müssen Ihre Systemzertifikate auf dem neuesten Stand sein.

### Erreichen von Rate-Limits

Wenn Sie Ihren über ein VPN oder einen Proxy ausführen, konkurrieren Sie möglicherweise mit 10, 100 oder 1000 anderen Personen, die alle versuchen, Dienste wie , theXEM und/oder Ihre Indexer und Tracker zu nutzen. Rate-Limiting und DDOS-Schutz werden häufig anhand der IP-Adresse durchgeführt, und Ihr VPN/Proxy-Ausgangspunkt ist *eine* IP-Adresse. Wenn Sie sich nicht in einem repressiven Land wie China, Australien oder Südafrika befinden, müssen Sie kein VPN/Proxy verwenden.

Rarbg neigt dazu, irgendeine Art von Rate-Limiting in ihrer API zu haben und meldet sich als Antwort ohne Ergebnisse.

### IP-Sperre

Ähnlich wie bei Rate-Limits kann es vorkommen, dass bestimmte Indexer - wie Nyaa - eine IP-Adresse vollständig sperren. Dies ist in der Regel halbpermanent, und die Lösung besteht darin, eine neue IP-Adresse von Ihrem ISP oder VPN-Anbieter zu erhalten.

### Verwendung des Jackett /all-Endpunkts

Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere sind potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ können Sie sich die Alternative zu Jackett & NZBHydra2, [Prowlarr](/prowlarr), ansehen.

[Sogar Jackett sagt, dass /all vermieden werden sollte und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)

Die Verwendung des all-Endpunkts hat keine Vorteile (außer reduziertem Verwaltungsaufwand), nur Nachteile:

- Sie verlieren die Kontrolle über indexerspezifische Einstellungen (Kategorien, Suchmodi usw.)
- Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen
- Indexerspezifische Kategorien (\>= 100000) können nicht verwendet werden.
- Langsame Indexer verlangsamen das Gesamtergebnis
- Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt

Durch das Hinzufügen jedes Indexers einzeln können Sie die Kategorien für jeden Indexer individuell anpassen, was bei Verwendung des `/all`-Endpunkts zu Problemen führen kann, wenn die falsche Kategorie auf einigen Trackern Fehler verursacht. In ist jeder Indexer auf 1000 Ergebnisse begrenzt, wenn die Seitenumbruch unterstützt wird, oder auf 100, wenn dies nicht der Fall ist. Das bedeutet, dass Sie, je mehr Tracker Sie zu Jackett hinzufügen, umso wahrscheinlicher sind, dass Ergebnisse abgeschnitten werden. Schließlich, wenn *einer* der Tracker in `/all` einen Fehler zurückgibt, deaktiviert Lidarr ihn und Sie erhalten keine Ergebnisse mehr.

### Verwendung von NZBHydra2 als einzelner Eintrag

Die Verwendung von NZBHydra2 als einzelner Indexer-Eintrag (d.h. 1 NZBHydra2-Eintrag in Lidarr für viele Indexer in NZBHydra2) hat dieselben Probleme wie der `/all`-Endpunkt von Jackett.

### Problem nicht aufgelistet

Sie können auch einige gängige Berechtigungs- und Netzwerkprobleme [in unserem Leitfaden](/permissions-and-networking) überprüfen. Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem sein könnte, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.

## Fehler

Dies sind einige der häufigen Fehler, die beim Hinzufügen eines Indexers auftreten können.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist bei einem Sendevorgang aufgetreten

Dies wird durch den Indexer verursacht, der ein von der aktuellen .NET-Version in [Lidarr => System => Status](/lidarr/system#status) nicht unterstütztes SSL-Protokoll verwendet.

### Die Anforderung hat das Zeitlimit überschritten

Lidarr erhält keine Antwort vom Indexer.

```none
System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten: ’https://example.org/api?t=caps&apikey=(entfernt) —> System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Verbindung zum Indexer nicht möglich

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen.
```

Dies kann auch durch folgende Ursachen verursacht werden:

- Falsche Konfiguration oder Verwendung eines VPNs
- Falsche Konfiguration oder Verwendung eines Proxys
- Lokale DNS-Probleme - Versuchen Sie, einen anderen DNS-Anbieter zu verwenden
- Lokale IPv6-Probleme - normalerweise ist IPv6 aktiviert, aber nicht funktionsfähig
- Die Verwendung von Privoxy und eine falsche Konfiguration davon

### Problem nicht aufgelistet

Sie können auch einige gängige Berechtigungs- und Netzwerkprobleme [in unserem Leitfaden](/permissions-and-networking) überprüfen. Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem sein könnte, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.