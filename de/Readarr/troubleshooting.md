---
title: Readarr Fehlerbehebung
description: 
published: true
date: 2023-07-24T19:54:33.343Z
tags: readarr, fehlerbehebung
editor: markdown
dateCreated: 2021-06-20T20:06:25.552Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Hilfe anfordern](#hilfe-anfordern)
- [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien)
  - [Standardmäßiger Protokollspeicherort](#standardmäßiger-protokollspeicherort)
  - [Aktualisierungsprotokollspeicherort](#aktualisierungsprotokollspeicherort)
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
    - [Sie bevorzugen ein Format, aber es wurde stattdessen ein anderes Format importiert](#sie-bevorzugen-ein-format-aber-es-wurde-statt-eines-anderen-formats-importiert)
    - [Die WebUI des Download-Clients ist nicht aktiviert](#die-webui-des-download-clients-ist-nicht-aktiviert)
    - [SSL wird verwendet und falsch konfiguriert](#ssl-wird-verwendet-und-falsch-konfiguriert)
    - [Freigabe unter Windows nicht sichtbar](#freigabe-unter-windows-nicht-sichtbar)
    - [Zugriff auf Netzwerklaufwerke ist nicht zuverlässig](#zugriff-auf-netzwerklaufwerke-ist-nicht-zuverlässig)
    - [Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade](#docker-und-benutzer-gruppe-besitz-berechtigungen-und-pfade)
    - [Remote-Pfadzuordnung](#remote-pfadzuordnung)
      - [Remote-Mount oder Remote-Sync (Syncthing)](#remote-mount-oder-remote-sync-syncthing)
    - [Berechtigungen für den Bibliotheksordner](#berechtigungen-für-den-bibliotheksordner)
    - [Berechtigungen für den Download-Ordner](#berechtigungen-für-den-download-ordner)
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
  - [Testen eines Indexers oder Trackers](#testen-eines-indexers-oder-trackers)
  - [Testen einer Suche](#testen-einer-suche)
  - [Häufige Probleme](#häufige-probleme-1)
    - [Medien sind nicht überwacht](#medien-sind-nicht-überwacht)
    - [Falsche Kategorien](#falsche-kategorien)
    - [Falsche Ergebnisse](#falsche-ergebnisse)
    - [Erfolgreiche Abfrage - Keine Ergebnisse zurückgegeben](#erfolgreiche-abfrage-keine-ergebnisse-zurückgegeben)
    - [Fehlende Ergebnisse](#fehlende-ergebnisse)
    - [Zertifikatsvalidierung](#zertifikatsvalidierung)
    - [Rate-Limits erreicht](#rate-limits-erreicht)
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

- [<i class="fab fa-discord"></i>&emsp;Discord *Offizieller Readarr-Discord*](https://readarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offizieller Readarr-Subreddit*](https://reddit.com/r/readarr)
{.links-list}

Bevor Sie jedoch dorthin gehen und einen Beitrag veröffentlichen, stellen Sie sicher, dass Ihre Hilfsanfrage so gut wie möglich ist. Beschreiben Sie das Problem klar und geben Sie eine kurze Beschreibung Ihrer Konfiguration an, einschließlich Dingen wie Ihrem Betriebssystem/Verteilung, Version von .NET, Version von Readarr, Download-Client und dessen Version. **Wenn Sie [Docker](https://www.docker.com/) verwenden, führen Sie bitte zuerst den [Docker-Leitfaden](/docker-guide) durch, da dies häufig auftretende Pfad-/Berechtigungsprobleme löst. Andernfalls halten Sie bitte ein [Docker Compose](/docker-guide#docker-compose) bereit. [So generieren Sie ein Docker Compose](https://trash-guides.info/compose)**. Erzählen Sie uns, was Sie bereits versucht haben, wonach Sie gesucht haben. Verwenden Sie den Abschnitt [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien), um Ihre Protokollierung auf Trace zu erhöhen, das Problem neu zu erstellen, den relevanten Kontext auf Pastebin hochzuladen und einen Link dazu in Ihrem Beitrag einzufügen. Vielleicht fügen Sie sogar einige Screenshots hinzu, um das Problem zu verdeutlichen.

Je mehr wir wissen, desto einfacher ist es, Ihnen zu helfen.

# Protokollierung und Protokolldateien

Es ist wahrscheinlich sinnvoll, auch die häufigen Probleme bei der Fehlerbehebung zu überprüfen:
- [Häufige Probleme bei Downloads und Importieren](#häufige-probleme)
- [Häufige Probleme bei der Suche nach Indexern und Trackern](#häufige-probleme-1)
{.links-list}

Wenn Sie nach Debug-Protokollen gefragt werden, enthalten Ihre Protokolle `debug` und wenn Sie nach Trace-Protokollen gefragt werden, enthalten Ihre Protokolle `trace`. Wenn die von Ihnen bereitgestellten Protokolle dies nicht enthalten, handelt es sich nicht um die angeforderten Protokolle.

- Vermeiden Sie es, die gesamte Protokolldatei zu teilen, es sei denn, Sie werden darum gebeten.
- Laden Sie Protokolle nicht direkt in Discord hoch oder fügen Sie sie als Textwände ein, es sei denn, Sie werden darum gebeten.
- Teilen Sie die Protokolle nicht als Anhang, als Zip-Archiv oder in einem anderen Format als Text, der über die unten aufgeführten Dienste geteilt wird.

Um gute und nützliche Protokolle für den Austausch bereitzustellen:

> Stellen Sie sicher, dass kein spammy Task ausgeführt wird, wie z.B. ein RSS-Refresh
{.is-warning}

1. [Erhöhen Sie die Protokollierung auf Trace (Einstellungen => Allgemein => Protokollstufe oder Bearbeiten der Konfigurationsdatei)](#trace-debug-protokolle)
2. [Protokolle löschen (System => Protokolle => Protokolle löschen oder Löschen aller Protokolle im Protokollordner)](#protokolle-löschen)
3. Reproduzieren Sie das Problem (Wiederholen Sie, was das Problem verursacht)
4. [Öffnen Sie die Trace-Protokolldatei (readarr.trace.txt) über die Benutzeroberfläche oder die Protokolldatei](#standardmäßiger-protokollspeicherort) im Dateisystem und finden Sie den relevanten Kontext
5. Kopieren Sie einen großen Abschnitt vor dem Problem, das Problem selbst und einen großen Abschnitt nach dem Problem.
6. Verwenden Sie [Gist](https://gist.github.com/), [0bin (**Stellen Sie sicher, dass die Colorierung deaktiviert ist**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) oder ähnliche Websites - mit Ausnahme der unten aufgeführten Websites - um die kopierten Protokolle von oben zu teilen

**Warnungen:**
- **Verwenden Sie nicht [pastebin.com](https://pastebin.com), da deren Filter dazu neigen, die Protokolle zu blockieren.
- Verwenden Sie nicht [pastebin.pl](https://pastebin.pl), da ihre Website häufig nicht erreichbar ist.
- Verwenden Sie nicht [JustPasteIt](https://justpaste.it/), da ihre Website das Überprüfen von Protokollen nicht ermöglicht.
- Laden Sie Ihr Protokoll nicht als Datei hoch.
- Laden Sie Ihre Protokolle nicht über Google Drive, Dropbox oder eine andere nicht oben genannte Website hoch und teilen Sie sie.
- Archivieren Sie Ihre Protokolle nicht (zip, tar (tarball), 7zip usw.).
- Teilen Sie keine Konsolenausgabe, Docker-Container-Ausgabe oder etwas anderes als die angegebenen Anwendungsprotokolle.

**Wichtiger Hinweis:**
- Wenn Sie [0bin](https://0bin.net/) verwenden, stellen Sie sicher, dass die Colorierung deaktiviert ist und brennen Sie die Protokolle nach dem Lesen nicht.
- Alternativ, wenn Sie in einer alten Protokolldatei nach einem bestimmten Eintrag suchen, aber nicht sicher sind, welche, können Sie N++ verwenden. Sie können die Funktion "In Dateien suchen" von Notepad++ verwenden, um bei Bedarf in alten Protokolldateien zu suchen.
- **Nur Unix:** Alternativ, wenn Sie in einer alten Protokolldatei nach einem bestimmten Eintrag suchen, aber nicht sicher sind, welche, können Sie grep verwenden. Wenn Sie beispielsweise Informationen über den Film/Die Show/Das Buch/Das Lied/Den Indexer "Shooter" finden möchten, können Sie den folgenden Befehl ausführen: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Wenn Ihr [Appdata-Verzeichnis](/readarr/appdata-directory) in Ihrem Home-Ordner liegt, führen Sie Folgendes aus: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Die Flags haben folgende Funktionen
    * -i: Groß-/Kleinschreibung ignorieren
    * -n: Zeilennummer anzeigen
    *  -r: rekursiv alle Dateien im Pfad überprüfen
    * -C: Anzahl der Zeilen vor und nach der gefundenen Zeile angeben
    * -e: das zu suchende Muster

```

## Standardmäßiger Protokollspeicherort

Die Protokolldateien befinden sich im [Appdata-Verzeichnis](/readarr/appdata-directory) von Readarr, im Ordner logs/. Sie können auch über die Benutzeroberfläche unter System => Protokolle => Dateien auf die Protokolldateien zugreifen.

> Hinweis: Die Protokolltabelle ("Ereignisse") in der Benutzeroberfläche ist nicht dasselbe wie die Protokolldateien und nicht so nützlich. Wenn Sie nach Protokollen gefragt werden, kopieren Sie bitte aus den Protokolldateien und nicht aus der Tabelle.
{.is-info}

## Aktualisierungsprotokollspeicherort

Die Aktualisierungsprotokolldateien befinden sich im [Appdata-Verzeichnis](/readarr/appdata-directory) von Readarr, im Ordner UpdateLogs/.

## Protokolle teilen

Die Protokolle können in Foren- oder Reddit-Beiträgen lang und schwer lesbar sein und in Discord Spam verursachen. Verwenden Sie daher bitte [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) oder eine ähnliche Pastebin-Website. In der Regel ist nicht die gesamte Datei erforderlich, sondern nur ein guter Teil des Kontexts vor und nach dem Problem/Fehler. Vergessen Sie nicht, auf das Ende von spammy Tasks wie einer RSS-Synchronisierung oder einer Bibliotheksaktualisierung zu warten.

## Trace-/Debug-Protokolle

Sie können die Protokollstufe unter Einstellungen => Allgemein => Protokollierung ändern. Readarr muss nicht neu gestartet werden, damit die Änderung wirksam wird. Diese Änderung betrifft nur die Protokolldateien, nicht die Protokollierungsdatenbank. Die neuesten Debug-/Trace-Protokolldateien haben die Namen `readarr.debug.txt` bzw. `readarr.trace.txt`.

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

Readarr verwendet rollende Protokolldateien, die auf jeweils 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer `readarr.txt`, für die anderen Dateien ist `readarr.0.txt` die nächstneuere (je höher die Zahl, desto älter ist sie). Diese Protokolldatei enthält Einträge für `fatal`, `error`, `warn` und `info`.

Wenn der Debug-Protokollmodus aktiviert ist, sind zusätzliche rollende Protokolldateien `readarr.debug.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info` und `debug`. Sie decken in der Regel einen Zeitraum von 40 Stunden ab.

Wenn der Trace-Protokollmodus aktiviert ist, sind zusätzliche rollende Protokolldateien `readarr.trace.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info`, `debug` und `trace`. Aufgrund der Trace-Verbosity decken sie nur einen Zeitraum von maximal einigen Stunden ab.

# Wiederherstellung nach einem fehlgeschlagenen Update

Wir tun alles, um Probleme bei der Aktualisierung zu vermeiden, aber wenn sie auftreten, führen Sie die folgenden Schritte aus, um Ihre Installation wiederherzustellen.

## Das Problem ermitteln

- Der beste Ort, um nachzusehen, wenn die Anwendung nach einem Update nicht startet, ist das Überprüfen der [Aktualisierungsprotokolle](#aktualisierungsprotokollspeicherort), um festzustellen, ob das Update erfolgreich abgeschlossen wurde. Wenn es keine Probleme gibt, schauen Sie sich als nächstes Ihre regulären Anwendungsprotokolldateien an. Erhöhen Sie vor dem erneuten Starten die Protokollierung mit [Protokollierung](/readarr/settings#logging) und [Protokolldateien](/readarr/system#log-files), um sie zu finden und die Protokollierungsstufe zu erhöhen.
- Das am häufigsten auftretende Problem ist, dass das System, auf dem die App installiert ist, das `/tmp`-Verzeichnis manipuliert und während des Upgrades kritische \*Arr-Dateien gelöscht hat, was sowohl das Upgrade als auch das Rollback scheitern lässt. In diesem Fall installieren Sie einfach die Anwendung über der vorhandenen fehlerhaften Installation.

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

- Synology-Benutzer können auch auf Platzmangel in `/tmp` auf bestimmten NAS-Geräten stoßen. Sie müssen einen anderen Pfad für `/tmp` für die Anwendung angeben. Wenden Sie sich an die SynoCommunity oder andere Synology-Supportkanäle, um Hilfe bei diesem Problem zu erhalten.

## Das Problem beheben

Bei einem Migrationsproblem können Sie zunächst nicht viel tun. Wenn das Problem spezifisch für Sie ist (oder es noch keine Beiträge dazu gibt), erstellen Sie bitte einen Beitrag in [unserem Subreddit](https://reddit.com/r/readarr) oder besuchen Sie unseren [Discord](https://readarr.com/discord). Wenn es andere mit dem gleichen Problem gibt, können Sie sicher sein, dass wir daran arbeiten.

> Bitte stellen Sie sicher, dass Sie nicht versucht haben, eine Datenbank von `nightly` in der stabilen Version zu verwenden. Das Wechseln zwischen Branches ist nicht ratsam.{.is-info}

### Berechtigungsprobleme

- Beheben Sie die Berechtigungen, um sicherzustellen, dass der Benutzer/die Gruppe, unter der die Anwendung ausgeführt wird, sowohl auf `/tmp` als auch auf das Installationsverzeichnis der Anwendung zugreifen kann (Lesen und Schreiben).

- Für Synology-Benutzer, die Probleme mit `/proc/###/maps` haben, sollte das Beenden von Sonarr oder den anderen \*Arr-Anwendungen und ein Update dieses Problems beheben. Dies ist ein Problem mit dem SynoCommunity-Paket.

### Manuelles Upgrade

Laden Sie die neueste Version von unserer Website herunter.

Installieren Sie das Update (.exe) oder extrahieren Sie den Inhalt (.zip) über Ihre bestehende Installation und führen Sie Readarr wie gewohnt erneut aus.

# Downloads und Import

Der Download und Import ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive betrachtet muss Readarr in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Setups. Das bedeutet, dass es zwar einige gängige Setups gibt, aber kein einziges richtiges Setup und jedes Setup ein wenig anders sein kann.

> **Der erste Schritt besteht darin, das Protokollierungsniveau auf Trace zu erhöhen. Weitere Informationen zum Anpassen der Protokollierung und zum Durchsuchen von Protokollen finden Sie unter [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien). Wiederholen Sie dann das Problem und verwenden Sie die Protokolle auf Trace-Ebene aus diesem Zeitraum, um das Problem zu untersuchen.** Wenn Ihnen jemand hilft, geben Sie den Kontext vor/nach dem Problem in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website an, um ihn anzuzeigen. Es muss nicht die gesamte Datei sein und es sollte nicht *nur* der Fehler sein. Sie sollten das Problem auch reproduzieren, während keine Aufgaben ausgeführt werden, die das Protokoll spammen.
{.is-danger}

Wenn Sie Hilfe suchen, lesen Sie unbedingt [Hilfe anfordern](#hilfe-anfordern), damit Sie uns die benötigten Details zur Verfügung stellen können.

## Testen des Download-Clients

Stellen Sie sicher, dass Ihr(e) Download-Client(s) ausgeführt wird/laufen. Beginnen Sie mit dem Test des Download-Clients. Wenn es nicht funktioniert, können Sie Details in den Protokollen auf Trace-Ebene sehen. Sie sollten eine URL finden, die Sie in Ihren Browser eingeben und überprüfen können, ob sie funktioniert. Es könnte ein Verbindungsproblem sein, das auf eine falsche IP-Adresse, einen falschen Hostnamen, einen falschen Port oder sogar eine Firewall hinweisen könnte. Es könnte offensichtlich sein, wie z.B. ein Authentifizierungsproblem, bei dem Sie den Benutzernamen, das Passwort oder den API-Schlüssel falsch eingegeben haben.

## Testen eines Downloads

Nun werden wir einen Download ausprobieren. Wählen Sie ein Buch aus und führen Sie eine manuelle Suche durch. Wählen Sie eine dieser Dateien aus und versuchen Sie, sie herunterzuladen. Wird sie an den Download-Client gesendet? Wird sie mit der richtigen Kategorie angezeigt? Erscheint sie in der Aktivität? Erscheint sie in den Protokollen auf Trace-Ebene während der Aufgabe "Überprüfen auf abgeschlossenen Download", die etwa alle Minute ausgeführt wird? Wird sie während dieser Aufgabe korrekt analysiert? Hat der heruntergeladene Download einen vernünftigen Namen? Da Suchen nach IDs auf einigen Indexern/Trackern erfolgen, kann es vorkommen, dass ein Download mit einem Namen in die Warteschlange gestellt wird, den er nicht erkennen kann.

## Testen eines Imports

Importprobleme sollten fast immer als Element in der Aktivität mit einem orangefarbenen Symbol angezeigt werden, über das Sie den Fehler anzeigen können. Wenn sie nicht in der Aktivität angezeigt werden, sollten Sie sich zuerst auf dieses Problem konzentrieren und es herausfinden. Die meisten Importfehler sind *Berechtigungsprobleme*. Denken Sie daran, dass Readarr Lese- und Schreibzugriff auf den Download-Ordner benötigt. Manchmal können auch Berechtigungen im Bibliotheksordner schuld sein, also überprüfen Sie beide.

Falsche Pfadprobleme sind ebenfalls möglich, treten aber in normalen Setups weniger häufig auf. Der Schlüssel zum Verständnis von Pfadproblemen besteht darin zu wissen, dass Readarr den Pfad zum Download *vom* Download-Client über dessen API erhält. Dies wird zu einem Problem in einzigartigeren Anwendungsfällen, wie z.B. wenn der Download-Client auf einem anderen System (vielleicht sogar einem anderen Betriebssystem) läuft. Es kann auch in einer Docker-Umgebung auftreten, wenn die Volumes nicht richtig eingerichtet sind. Eine Remote-Pfadzuordnung ist eine gute Lösung, wenn Sie keine Kontrolle haben, z.B. bei einer Seedbox-Einrichtung. Bei einer Docker-Umgebung ist es besser, die Pfade zu korrigieren.

## Häufige Probleme

Nachfolgend sind einige häufige Probleme aufgeführt.

### Sie bevorzugen ein Format, aber es wurde ein anderes Format importiert

Wenn Readarr importiert, erfolgt der Import in der Reihenfolge Ihrer Prioritäten in Ihrem Qualitätsprofil, unabhängig davon, ob sie aktiviert sind oder nicht. Um dieses Problem zu lösen, müssen Sie die aktivierten Formate an die Spitze der Qualitätsliste ziehen. In dem unten stehenden Beispiel werden trotz der gewünschten EPUB-Datei, wenn der Download eine AZW3-Datei zusammen mit der EPUB-Datei enthält, die Formate mit höherer Priorität als die EPUB-Datei importiert, was dazu führt, dass unerwünschte Formate importiert werden.

![qualities.png](/assets/readarr/qualities.png)

### Die WebUI des Download-Clients ist nicht aktiviert

Readarr kommuniziert mit Ihrem Download-Client über dessen API und greift über die WebUI des Clients darauf zu. Sie müssen sicherstellen, dass die WebUI des Clients aktiviert ist und der verwendete Port nicht mit anderen Client-Ports in Verwendung oder mit Ports auf Ihrem System in Konflikt steht.

### Falsche Konfiguration von SSL

Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie Ihre Instanz und Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in [der SSL-FAQ](/readarr/faq#ungültiges-zertifikat-und-andere-https-oder-ssl-probleme).

### Freigabe unter Windows nicht sichtbar

Der Standardbenutzer für einen Windows-Dienst ist `LocalService`, der in der Regel keinen Zugriff auf Ihre Freigaben hat. Bearbeiten Sie den Dienst und richten Sie ihn so ein, dass er unter Ihrem eigenen Benutzerkonto ausgeführt wird. Weitere Informationen finden Sie in der FAQ [Warum kann ich meine Dateien auf einem Remote-Server nicht sehen?](/readarr/faq#warum-kann-ich-meine-dateien-auf-einem-remote-server-nicht-sehen).

### Gemappte Netzlaufwerke sind nicht zuverlässig

Obwohl gemappte Netzlaufwerke wie `X:\` praktisch sind, sind sie nicht so zuverlässig wie UNC-Pfade wie `\\server\share` und sie sind auch vor dem Anmelden nicht verfügbar. Konfigurieren Sie Ihren Download-Client so, dass er bei Bedarf UNC-Pfade verwendet. Wenn sich Ihre Bibliothek auf einer Freigabe befindet, stellen Sie sicher, dass Ihre Stammordner UNC-Pfade verwenden. Wenn Ihr Download-Client an eine Freigabe sendet, müssen Sie dort UNC-Pfade konfigurieren, da Readarr den Download-Pfad vom Download-Client erhält. Es ist in Ordnung, Ihre gemappten Netzlaufwerke für sich selbst zu verwenden, verwenden Sie sie jedoch nicht für die Automatisierung.

### Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade

Docker fügt eine weitere Ebene der Komplexität hinzu, die leicht falsch gemacht werden kann, aber dennoch zu einer funktionierenden Einrichtung führt, die verschiedene Probleme aufweist. Anstatt sie hier zu behandeln, lesen Sie diesen Wiki-Artikel [für diese Automatisierungssoftware und Docker](/docker-guide), der sich mit Benutzer, Gruppe, Besitz, Berechtigungen und Pfaden befasst. Er ist nicht spezifisch für ein bestimmtes Docker-System, sondern behandelt die Dinge auf einer hohen Ebene, damit Sie sie in Ihrer eigenen Umgebung implementieren können.

### Remote-Pfadzuordnung

Wenn Sie Readarr in Docker und den Download-Client in einer Nicht-Docker-Umgebung (oder umgekehrt) haben oder die Programme auf verschiedenen Servern haben, benötigen Sie möglicherweise eine Remote-Pfadzuordnung.

Die Protokolle sehen wie folgt aus:

```none
2022-02-03 14:03:54.3|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /volume3/data/torrents/audiobooks/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Daher existiert `/volume3/data` nicht in Readarrs Container oder ist nicht zugänglich.

- [Einstellungen => Download-Clients => Remote-Pfadzuordnungen](/readarr/settings#remote-path-mappings)
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht in diesem Ordner adressiert wird.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft, während \*Arr auf Windows läuft oder umgekehrt. Eine Remote-Pfadzuordnung ist auch möglicherweise erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine einfache Suchen/Ersetzen-Funktion (sie sucht nach dem REMOTE-Wert und ersetzt ihn durch den LOCAL-Wert für den angegebenen Host).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie in TRaSHs Tutorial](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist eine Remote-Pfadzuordnung selten erforderlich. Es wird empfohlen, [den Docker-Leitfaden](/docker-guide) zu überprüfen und/oder [TRaSHs Tutorial](https://trash-guides.info/hardlinks) zu befolgen.
{.is-info}

#### Remote-Mount oder Remote-Synchronisation (Syncthing)

- Sie müssen sicherstellen, dass es die ganze Zeit synchronisiert wird, während es herunterlädt. Und Sie müssen das lokale Synchronisationsziel so einrichten, dass es beim Import von \*Arr als Hardlinks verwendet werden kann, d.h. es muss dasselbe Dateisystem haben und so aussehen.
  - Synchronisieren Sie in einem niedrigeren, gemeinsamen Ordner, der sowohl unvollständige als auch vollständige Dateien enthält.
  - Synchronisieren Sie an einen Speicherort, der auf demselben Dateisystem lokal wie Ihre Bibliothek liegt und so aussieht (Docker und Netzwerkfreigaben machen es leicht, dies falsch zu konfigurieren).
  - Sie möchten die unvollständigen und vollständigen Dateien synchronisieren, damit, wenn der Torrent-Client den Verschiebevorgang durchführt, dies lokal reflektiert wird und alle Dateien bereits "dort" sind (auch wenn sie noch heruntergeladen werden). Dann möchten Sie Hardlinks verwenden, denn selbst wenn der Import vor Abschluss erfolgt, werden sie trotzdem fertiggestellt.
  - Auf diese Weise wird während des gesamten Downloads synchronisiert, dann verschiebt der Torrent-Client in den Unterordner "tv" und die Synchronisierung spiegelt das wider. Auf diese Weise sind die Downloads größtenteils vorhanden, wenn sie als abgeschlossen deklariert werden. Und selbst wenn sie noch nicht ganz fertig sind, ist es in Ordnung, dass der Hardlink möglich ist.
  - (Optional - falls zutreffend und/oder erforderlich (z.B. Remote-Usenet-Client)) Konfigurieren Sie ein benutzerdefiniertes Skript, das beim Import/Download/Upgrade ausgeführt wird, um die Remote-Datei zu entfernen.
- Alternativ ist eine Remote-Mount-Einrichtung anstelle einer Remote-Synchronisations-Einrichtung deutlich weniger kompliziert zu konfigurieren, aber in der Regel langsamer.
  - Mounten Sie Ihren Remote-Speicher mit sshfs oder einem anderen Netzdateisystemprotokoll.
  - Stellen Sie sicher, dass der Benutzer und die Gruppe, unter der \*Arr ausgeführt wird, Lese- oder Schreibzugriff haben.
  - Konfigurieren Sie eine Remote-Pfadzuordnung, um den REMOTE-Pfad zu finden und durch den entsprechenden LOCAL-Wert zu ersetzen.

### Berechtigungen auf dem Bibliotheksordner

Die Protokolle sehen wie folgt aus:

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/media/books/Jasmine Guillory/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Vergessen Sie nicht, die Berechtigungen und den Besitz des *Zielordners* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Downloads zu fixieren, und das ist *in der Regel* die Ursache für Berechtigungsprobleme, aber es *könnte* auch das Ziel sein. Überprüfen Sie, ob die Zielordner existieren. Überprüfen Sie, ob eine Ziel-*Datei* bereits vorhanden ist oder nicht gelöscht oder in den Papierkorb verschoben werden kann. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren, Hardlinken oder Verschieben der heruntergeladenen Datei zulassen. Der Benutzer oder die Gruppe, unter der \*Arr ausgeführt wird, muss in der Lage sein, den Stammordner zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies daran liegen, dass der Dienst als Dienst ausgeführt wird:
  - Der Windows-Dienst wird standardmäßig unter dem Konto "Lokaler Dienst" ausgeführt. Dieses Konto hat standardmäßig keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Download-Clients verwendet werden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "Lokaler Dienst" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die Anwendung als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten. Informationen dazu, wie Sie von einem Dienst zu einer Tray-Anwendung wechseln, finden Sie in der FAQ.

- Für Synology-Benutzer siehe [SynoCommunitys Artikel zu Berechtigungen für ihre Pakete](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Berechtigungen auf dem Download-Ordner

Die Protokolle sehen wie folgt aus:

```none
2022-02-28 18:51:01.1|Error|DownloadedBooksImportService|Import failed, path does not exist or is not accessible by Readarr: /data/torrents/books/Party of Two - Jasmine Guillory.mp3. Ensure the path exists and the user running Readarr has the correct permissions to access this file/folder
```

Vergessen Sie nicht, die Berechtigungen und den Besitz der *Quelle* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Ziels zu fixieren, und das ist eine *mögliche* Ursache für Berechtigungsprobleme, aber in der Regel ist es die Quelle. Überprüfen Sie, ob die Quellordner existieren. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren/Hardlinken oder Kopieren+Löschen/Verschieben der heruntergeladenen Datei zulassen. Der Benutzer oder die Gruppe, unter der \*Arr ausgeführt wird, muss in der Lage sein, den Download-Ordner zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies daran liegen, dass der Dienst als Dienst ausgeführt wird:
  - Der Windows-Dienst wird standardmäßig unter dem Konto "Lokaler Dienst" ausgeführt. Dieses Konto hat standardmäßig keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Download-Clients verwendet werden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "Lokaler Dienst" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die Anwendung als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten. Informationen dazu, wie Sie von einem Dienst zu einer Tray-Anwendung wechseln, finden Sie in der FAQ.

- Für Synology-Benutzer siehe [SynoCommunitys Artikel zu Berechtigungen für ihre Pakete](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Download-Ordner und Bibliotheksordner sind nicht unterschiedliche Ordner

Der Download-Client sollte in einen Ordner herunterladen, auf den \*Arr zugreifen kann, und dieser Ordner sollte nicht Ihr Stamm-/Bibliotheksordner sein. \*Arr sollte aus diesem separaten Download-Ordner in Ihren Bibliotheksordner importieren.

Sie sollten niemals direkt in Ihren Stammordner herunterladen. Sie sollten Ihren Stammordner auch nicht als den abgeschlossenen Ordner oder den unvollständigen Ordner des Download-Clients verwenden.

> Ihr Download-Ordner und Ihr Stamm-/Bibliotheksordner MÜSSEN getrennt sein.
{.is-warning}

### Falsche Kategorie

Readarr sollte so eingerichtet sein, dass es eine Kategorie verwendet, damit es nur versucht, seine eigenen Downloads zu verarbeiten. Es ist selten, dass ein von hinzugefügter Torrent ohne die richtige Kategorie hinzugefügt wird, aber es kann vorkommen. Wenn Sie Torrents manuell hinzufügen und sie verarbeiten möchten, müssen sie die richtige Kategorie haben. Sie kann jederzeit festgelegt werden, da versucht, Downloads alle Minute zu verarbeiten.

### Gepackte Torrents

Die Protokolle zeigen Fehler wie

```none
No files found are eligible for import
```

Wenn Ihr Torrent in `.rar`-Dateien gepackt ist, müssen Sie die Entpackung einrichten. Wir empfehlen [Unpackerr](https://github.com/unpackerr/unpackerr), da es die Entpackung richtig durchführt: Es verhindert korrupte teilweise Importe und räumt die entpackten Dateien nach dem Import auf.

Der Fehler kann auch auftreten, wenn sich kein gültiges Mediendatei im Ordner befindet.

### Wiederholte Downloads

Es gibt einige Ursachen für wiederholte Downloads, aber eine davon hängt mit der Indexer-Beschränkung in den Release-Profilen zusammen. Da der Indexer *nicht* mit den Daten gespeichert wird, sind alle bevorzugten Wortbewertungen für Medien in Ihrer Bibliothek *null*, aber während "RSS" und Suche werden sie angewendet. Dadurch geraten Sie in eine Schleife, in der Sie die Elemente immer wieder herunterladen, weil es wie ein Upgrade aussieht, dann keines ist, dann wieder auftaucht und wie ein Upgrade aussieht, dann keines ist. Beschränken Sie Ihr Release-Profil nicht auf einen Indexer.

Dies kann auch darauf zurückzuführen sein, dass der Download nie tatsächlich importiert wird und dann aus der Warteschlange fehlt, sodass ein neuer Download immer wieder heruntergeladen und nie importiert wird. Bitte beachten Sie die verschiedenen anderen häufigen Probleme und Fehlerbehebungsschritte dafür.

### Usenet-Download wird nicht importiert

Readarr betrachtet nur die 60 neuesten Downloads in SABnzbd und NZBGet. Wenn du deinen Verlauf behältst, bedeutet das, dass während großer Warteschlangen mit Importproblemen Downloads stillschweigend verpasst und nicht importiert werden können. Der beste Weg, dies zu vermeiden, besteht darin, deinen Verlauf sauber zu halten, damit alle noch angezeigten Elemente untersucht werden können. Du kannst dies erreichen, indem du "Entfernen" unter "Abgeschlossene und fehlgeschlagene Download-Handler" aktivierst. Bei NZBGet werden die Elemente dann in den *versteckten* Verlauf verschoben, was großartig ist. Leider verfügt SABnzbd nicht über eine ähnliche Funktion. Das Beste, was du dort erreichen kannst, ist die Verwendung des NZB-Backup-Ordners.

### Löschen von Elementen des Download-Clients

Der Download-Client sollte *nicht* dafür verantwortlich sein, Downloads zu entfernen. Usenet-Clients sollten so konfiguriert sein, dass sie Downloads nicht aus dem Verlauf entfernen. Torrent-Clients sollten so eingestellt sein, dass sie Torrents nicht entfernen, wenn sie fertig sind (pausieren oder stoppen statt löschen). Dies liegt daran, dass Readarr mit dem Download-Client kommuniziert, um zu wissen, was importiert werden soll. Wenn die Downloads *entfernt* werden, gibt es nichts zu importieren... selbst wenn sich ein Ordner mit Dateien befindet.

Bei SABnzbd wird dies mit der Einstellung "Verlauf beibehalten" behandelt.

### Download kann keinem Bibliothekselement zugeordnet werden

Aus verschiedenen Gründen können Releases nach dem Herunterladen und Senden an den Download-Client nicht analysiert werden. "Aktivität" => "Optionen" => "Unbekannte anzeigen" (dies ist in aktuellen Versionen standardmäßig aktiviert) zeigt alle Elemente an, die nicht anderweitig ignoriert oder bereits in der Download-Client-Kategorie von \*Arr importiert wurden. Diese müssen in der Regel manuell zugeordnet und importiert werden.

Dies kann auch auftreten, wenn du ein Release in deinem Download-Client hast, aber dieses Medienelement (Film/Folge/Buch/Song) nicht in der Anwendung existiert.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist beim Senden aufgetreten

Dies wird durch den Indexer verursacht, der ein von der aktuellen .NET-Version in [Readarr => System => Status](/readarr/system#status) nicht unterstütztes SSL-Protokoll verwendet.

### Die Anforderung hat das Zeitlimit überschritten

Readarr erhält keine Antwort vom Client.

```none
    System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten: ’https://example.org/api?t=caps&apikey=(entfernt) —> System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Verbindung zum Indexer nicht möglich

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen.
```

Dies kann auch durch Folgendes verursacht werden:

- falsch konfigurierte oder Verwendung eines VPNs
- falsch konfigurierte oder Verwendung eines Proxys
- lokale DNS-Probleme
- lokale IPv6-Probleme - normalerweise ist IPv6 aktiviert, aber nicht funktionsfähig
- die Verwendung von Privoxy und eine falsche Konfiguration davon

## Problem nicht aufgelistet

Du kannst auch einige gängige Berechtigungs- und Netzwerkprobleme in unserem Leitfaden überprüfen (/permissions-and-networking). Andernfalls bespreche das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem ist, schlage bitte vor, es dem Wiki hinzuzufügen.

# Suchen von Indexern und Trackern

- Wenn du [Prowlarr](/prowlarr) verwendest, kannst du dir die [Verlauf](/prowlarr/history) aller Abfragen anzeigen lassen, die Prowlarr erhalten hat und wie sie an die Websites gesendet wurden. Stelle sicher, dass "Parameter" in den Prowlarr-Verlaufsoptionen aktiviert ist. Das (i)-Symbol bietet zusätzliche Details.

## Protokollierung auf Trace-Niveau erhöhen

> **Der erste Schritt besteht darin, die Protokollierung auf Trace-Niveau zu erhöhen. Informationen zum Anpassen der Protokollierung und zum Durchsuchen von Protokollen findest du unter [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien). Du wiederholst dann das Problem und verwendest die Protokolle auf Trace-Niveau aus diesem Zeitraum, um das Problem zu untersuchen.** Wenn dir jemand hilft, stelle den Kontext vorher/nachher in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website zur Verfügung, um ihn anzuzeigen. Es muss nicht die gesamte Datei sein und es sollte nicht *nur* der Fehler sein. Du solltest das Problem auch reproduzieren, während Aufgaben, die das Protokoll spammen, nicht ausgeführt werden.
{.is-danger}

## Testen eines Indexers oder Trackers

Wenn du einen Indexer oder Tracker testest, findest du in den Debug- oder Trace-Protokollen die verwendete URL. Ein Beispiel für einen erfolgreichen Test findest du unten. Du kannst sehen, dass er den Indexer über eine bestimmte URL mit bestimmten Parametern abfragt und dann die Antwort erhält. Du kannst diese URL in deinem Browser testen, indem du `apikey=(entfernt)` durch den richtigen API-Schlüssel wie `apikey=123` ersetzt. Du kannst mit den Parametern experimentieren, wenn du einen Fehler vom Indexer erhältst, oder überprüfen, ob du Konnektivitätsprobleme hast, wenn es überhaupt nicht funktioniert. Nachdem du es in deinem eigenen Browser getestet hast, solltest du es auch von dem System aus testen, auf dem es ausgeführt wird, *wenn* du es noch nicht getan hast.

## Testen einer Suche

Ähnlich wie beim oben beschriebenen Indexer/Tracker-Test kannst du bei Debug- oder Trace-Level-Protokollierung die verwendete URL aus den Protokolldateien abrufen, wenn du eine Suche auslöst. Beim Testen ist es am besten, eine so spezifische Suche wie möglich durchzuführen. Eine manuelle Suche ist gut, weil sie spezifisch ist und du die Ergebnisse in der Benutzeroberfläche sehen kannst, während du die Protokolle untersuchst.

Bei diesem Test suchst du nach offensichtlichen Fehlern und führst einige einfache Tests durch. Du kannst sehen, dass die Suche die URL ***AKTUALISIERTE URL FÜR BÜCHER ERFORDERLICH - DIES IST EIN SONARR URL-BEISPIEL*** `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(entfernt)&offset=0&limit=100&tvdbid=354629&season=1&ep=1` verwendet, die du selbst in einem Browser ausprobieren kannst, nachdem du (entfernt) durch deinen API-Schlüssel für diesen Indexer ersetzt hast. Funktioniert es? Siehst du die erwarteten Ergebnisse? Gilt dieser FAQ-Eintrag? In dieser URL kannst du sehen, dass bestimmte Kategorien mit `cat=5030,5040,5045,5080` festgelegt sind. Wenn du also nicht die erwarteten Ergebnisse siehst, ist dies ein wahrscheinlicher Grund. Du kannst auch sehen, dass nach tvdbid mit `tvdbid=354629` gesucht wird. Wenn die Episode auf dem Indexer nicht richtig kategorisiert ist, muss dies behoben werden. Du kannst auch sehen, dass nach einer bestimmten Staffel und Episode mit season=1 und ep=1 gesucht wird. Wenn dies auf dem Indexer nicht korrekt ist, siehst du diese Ergebnisse nicht. Sieh dir unten das Beispiel für die XML-Ausgabe der manuellen Suche an, um zu sehen, wie eine funktionierende Abfrage aussieht.

- XML-Ausgabe der manuellen Suche

```xml
BEISPIEL FÜR INDEXER-SUCHE ERWARTET
```

***Bilder erforderlich***

![searches-indexers-and-trackers1.png](/assets/readarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/readarr/searches-indexers-and-trackers2.png)

- Ausschnitt aus dem Trace-Protokoll

```none
Ausschnitt aus dem Trace-Protokoll für eine manuelle Suche erforderlich
```

- Vollständiges Trace-Protokoll einer Suche

```none
Vollständiger Abschnitt des Trace-Protokolls für eine manuelle Suche erforderlich
```

## Häufige Probleme

Hier sind einige häufige Probleme.

### Medien sind nicht überwacht

Das/die Buch/Bücher werden nicht überwacht.

### Falsche Kategorien

Falsche Kategorien sind wahrscheinlich die häufigste Ursache dafür, dass Ergebnisse in manuellen Suchen eines Indexers/Trackers angezeigt werden, aber nicht in . Der Indexer/Tracker sollte die Kategorie in den Suchergebnissen anzeigen, was dir helfen sollte herauszufinden, was fehlt. Wenn du Jackett oder Prowlarr verwendest, hat jeder Tracker eine Liste von speziell unterstützten Kategorien. Stelle sicher, dass du die richtigen für Kategorien verwendest. Viele finden es hilfreich, die Liste in einem Browserfenster sichtbar zu haben, während sie den Eintrag bearbeiten.

### Falsche Ergebnisse

Manchmal liefert der Indexer völlig irrelevante Ergebnisse. Readarr gibt Parameter ein, um die Suche einzuschränken, aber die zurückgegebenen Ergebnisse haben nichts damit zu tun. Oder manchmal sind sie größtenteils relevant, aber mit einigen falschen Ergebnissen. Das erste ist normalerweise ein Problem des Indexers, und du kannst es anhand der Trace-Protokolle erkennen, welcher Indexer dafür verantwortlich ist. Du kannst diesen Indexer deaktivieren und das Problem melden. Das andere ist normalerweise kategorisierte Releases, die auf dem Indexer/Tracker gemeldet werden sollten.

### Abfrage erfolgreich - Keine Ergebnisse zurückgegeben

Du erhältst eine Meldung ähnlich wie "Abfrage erfolgreich, aber es wurden keine Ergebnisse von deinem Indexer zurückgegeben. Dies kann ein Problem mit dem Indexer oder deinen Indexer-Kategorieeinstellungen sein."

Dies wird verursacht, wenn dein Indexer keine Ergebnisse zurückgibt, die in den von dir für den Indexer konfigurierten Kategorien liegen.

### Fehlende Ergebnisse

Wenn du Ergebnisse auf der Website findest, die in Readarr nicht angezeigt werden, ist das Problem wahrscheinlich eines der folgenden:

- [Falsche Kategorien - Siehe oben](#falsche-kategorien)
- Es wird eine ID-basierte Suche durchgeführt, und der Indexer hat die Releases nicht korrekt dieser ID zugeordnet. Dies ist etwas, das nur dein Indexer lösen kann. Er muss sicherstellen, dass das Release den richtigen zutreffenden IDs zugeordnet ist.
- Nicht so suchen, wie Readarr sucht: Es ist sehr wahrscheinlich, dass die Begriffe, nach denen du auf dem Indexer suchst, nicht der Art und Weise entsprechen, wie Readarr danach sucht. Du kannst sehen, wie Readarr in den Trace-Protokollen sucht. Textbasierte Abfragen haben in der Regel das Format `q=Wörter%20und%20Dinge%20hier`. Diese Zeichenkette ist HTTP-codiert und kann mit einem beliebigen Online-HTML-Codierungs/-Decodierungstool leicht decodiert werden.

### Zertifikatsvalidierung

Du wirst dich mit den meisten Indexern/Trackern über https verbinden, daher muss dies auf deinem System ordnungsgemäß funktionieren. Das bedeutet, dass deine Zeitzone und die Uhrzeit *korrekt* eingestellt sein müssen. Außerdem müssen deine Systemzertifikate auf dem neuesten Stand sein.

### Erreichen von Rate-Limits

Wenn du deinen über ein VPN oder einen Proxy ausführst, konkurrierst du möglicherweise mit 10, 100 oder 1000 anderen Personen, die alle versuchen, Dienste wie , theXEM und/oder deine Indexer und Tracker zu nutzen. Rate-Limiting und DDOS-Schutz werden oft anhand der IP-Adresse durchgeführt, und dein VPN/Proxy-Ausgangspunkt ist *eine* IP-Adresse. Es sei denn, du bist in einem repressiven Land wie China, Australien oder Südafrika, du brauchst kein VPN/Proxy .

Rarbg neigt dazu, eine Art Rate-Limiting in ihrer API zu haben und zeigt an, dass keine Ergebnisse vorliegen.

### IP-Sperre

Ähnlich wie bei Rate-Limits kann es vorkommen, dass bestimmte Indexer - wie Nyaa - eine IP-Adresse vollständig sperren. Dies ist in der Regel halbpermanent, und die Lösung besteht darin, eine neue IP-Adresse von deinem ISP oder VPN-Anbieter zu erhalten.

### Verwendung des Jackett /all-Endpunkts

Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere sind potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ kannst du dir das Jackett & NZBHydra2-Alternative [Prowlarr](/prowlarr) ansehen.

[Sogar Jackett sagt, dass /all vermieden werden sollte und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)

Die Verwendung des all-Endpunkts hat keine Vorteile (außer reduziertem Verwaltungsaufwand), nur Nachteile:

- Du verlierst die Kontrolle über indexerspezifische Einstellungen (Kategorien, Suchmodi usw.).
- Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen.
- Indexerspezifische Kategorien (\>= 100000) können nicht verwendet werden.
- Langsame Indexer verlangsamen das Gesamtergebnis.
- Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt.

Durch das Hinzufügen jedes Indexers einzeln kannst du die Kategorien für jeden Indexer individuell anpassen, was bei Verwendung des `/all`-Endpunkts zu Problemen führen kann, wenn die Verwendung der falschen Kategorie auf einigen Trackern Fehler verursacht. In  ist jeder Indexer auf 1000 Ergebnisse begrenzt, wenn die Seitenumbruch unterstützt wird, oder auf 100, wenn nicht, was bedeutet, dass du beim Hinzufügen von immer mehr Trackern zu Jackett immer wahrscheinlicher Ergebnisse abschneidest. Schließlich, wenn *einer* der Tracker in `/all` einen Fehler zurückgibt, deaktiviert  ihn und du erhältst keine Ergebnisse mehr.

### Verwendung von NZBHydra2 als einzelner Eintrag

Die Verwendung von NZBHydra2 als einzelner Indexer-Eintrag (d. h. 1 NZBHydra2-Eintrag in Readarr für viele Indexer in NZBHydra2) anstelle von mehreren (d. h. vielen NZBHydra2-Einträgen in Readarr für viele Indexer in NZBHydra2) hat dieselben Probleme wie der `/all`-Endpunkt von Jackett.

### Problem nicht aufgelistet

Du kannst auch einige gängige Berechtigungs- und Netzwerkprobleme in unserem Leitfaden überprüfen (/permissions-and-networking). Andernfalls bespreche das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem ist, schlage bitte vor, es dem Wiki hinzuzufügen.

## Fehler

Dies sind einige der häufigen Fehler, die beim Hinzufügen eines Indexers auftreten können.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist beim Senden aufgetreten

Dies wird durch den Indexer verursacht, der ein von der aktuellen .NET-Version in [Readarr => System => Status](/readarr/system#status) nicht unterstütztes SSL-Protokoll verwendet.

### Die Anforderung hat das Zeitlimit überschritten

Readarr erhält keine Antwort vom Indexer.

```none
    System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten: ’https://example.org/api?t=caps&apikey=(entfernt) —> System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Verbindung zum Indexer nicht möglich

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen.
```

Dies kann auch durch Folgendes verursacht werden:

- falsch konfigurierte oder Verwendung eines VPNs
- falsch konfigurierte oder Verwendung eines Proxys
- lokale DNS-Probleme
- lokale IPv6-Probleme - normalerweise ist IPv6 aktiviert, aber nicht funktionsfähig
- die Verwendung von Privoxy und eine falsche Konfiguration davon

### Problem nicht aufgelistet

Du kannst auch einige gängige Berechtigungs- und Netzwerkprobleme in unserem Leitfaden überprüfen (/permissions-and-networking). Andernfalls bespreche das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem ist, schlage bitte vor, es dem Wiki hinzuzufügen.