---
title: Radarr Fehlerbehebung
description: Fehlerbehebung für Radarr, einschließlich Abrufen von Protokolldateien, Fehlerbehebung bei der Suche und häufig auftretenden Problemen sowie Fehlerbehebung beim Herunterladen/Importieren
published: true
date: 2023-08-12T09:40:45.369Z
tags: radarr, fehlerbehebung
editor: markdown
dateCreated: 2021-08-03T21:05:52.988Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Hilfe anfordern](#hilfe-anfordern)
- [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien)
  - [Standardmäßiger Protokollspeicherort](#standardmäßiger-protokollspeicherort)
  - [Aktualisierungsprotokollspeicherort](#aktualisierungsprotokollspeicherort)
  - [Protokolle freigeben](#protokolle-freigeben)
  - [Trace-/Debug-Protokolle](#trace-debug-protokolle)
  - [Protokolle löschen](#protokolle-löschen)
- [Mehrere Protokolldateien](#mehrere-protokolldateien)
- [Wiederherstellung nach einem fehlgeschlagenen Update](#wiederherstellung-nach-einem-fehlgeschlagenen-update)
  - [Das Problem ermitteln](#das-problem-ermitteln)
    - [Datenbank-Disk-Image ist beschädigt](#datenbank-disk-image-ist-beschädigt)
    - [Migrationsproblem](#migrationsproblem)
    - [UI-Migrationsprobleme](#ui-migrationsprobleme)
    - [Berechtigungsproblem](#berechtigungsproblem)
  - [Das Problem beheben](#das-problem-beheben)
    - [Migrationsprobleme](#migrationsprobleme)
    - [Berechtigungsprobleme](#berechtigungsprobleme)
    - [Manuelles Upgrade](#manuelles-upgrade)
- [Downloads und Importieren](#downloads-und-importieren)
  - [Testen des Download-Clients](#testen-des-download-clients)
  - [Testen eines Downloads](#testen-eines-downloads)
  - [Testen eines Imports](#testen-eines-imports)
  - [Häufig auftretende Probleme](#häufig-auftretende-probleme)
    - [WebUI des Download-Clients ist nicht aktiviert](#webui-des-download-clients-ist-nicht-aktiviert)
    - [Fehlerhafte oder fehlerhaft konfigurierte SSL](#fehlerhafte-oder-fehlerhaft-konfigurierte-ssl)
    - [Freigabe unter Windows nicht sichtbar](#freigabe-unter-windows-nicht-sichtbar)
    - [Netzwerklaufwerke sind nicht zuverlässig](#netzwerklaufwerke-sind-nicht-zuverlässig)
    - [Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade](#docker-und-benutzer-gruppe-besitz-berechtigungen-und-pfade)
    - [Remote-Pfadzuordnung](#remote-pfadzuordnung)
      - [Remote-Mount oder Remote-Synchronisierung (Syncthing)](#remote-mount-oder-remote-synchronisierung-syncthing)
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
  - [Protokollierung auf Trace erhöhen](#protokollierung-auf-trace-erhöhen)
  - [Testen eines Indexers oder Trackers](#testen-eines-indexers-oder-trackers)
  - [Testen einer Suche](#testen-einer-suche)
  - [Häufig auftretende Probleme](#häufig-auftretende-probleme-1)
    - [Tracker benötigt RawSearch-Fähigkeiten](#tracker-benötigt-rawsearch-fähigkeiten)
    - [Medien sind nicht überwacht](#medien-sind-nicht-überwacht)
    - [Falsche Kategorien](#falsche-kategorien)
    - [Erfolgreiche Abfrage - Keine Ergebnisse zurückgegeben](#erfolgreiche-abfrage-keine-ergebnisse-zurückgegeben)
    - [Falsche Ergebnisse](#falsche-ergebnisse)
    - [Fehlende Ergebnisse](#fehlende-ergebnisse)
    - [Zertifikatsvalidierung](#zertifikatsvalidierung)
    - [Erreichen von Rate-Limits](#erreichen-von-rate-limits)
    - [IP-Sperre](#ip-sperre)
    - [Jahr stimmt nicht überein](#jahr-stimmt-nicht-überein)
    - [Fehlendes Jahr](#fehlendes-jahr)
    - [Verwendung des Jackett /all-Endpunkts](#verwendung-des-jackett-all-endpunkts)
    - [Verwendung von NZBHydra2 als einzelner Eintrag](#verwendung-von-nzbhydra2-als-einzelner-eintrag)
    - [Nicht aufgeführtes Problem](#nicht-aufgeführtes-problem-1)
  - [Fehler](#fehler)
    - [Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist aufgetreten](#die-zugrunde-liegende-verbindung-wurde-geschlossen-ein-unerwarteter-fehler-ist-aufgetreten)
    - [Die Anforderung hat das Zeitlimit überschritten](#die-anforderung-hat-das-zeitlimit-überschritten)
    - [Nicht aufgeführtes Problem](#nicht-aufgeführtes-problem-2)

# Hilfe anfordern

Benötigen Sie Hilfe? Das ist in Ordnung, jeder braucht manchmal Hilfe. Sie können in Echtzeit Hilfe über den Chat erhalten auf

- [<i class="fab fa-discord"></i>&emsp;Discord *Offizieller Radarr-Discord*](https://radarr.video/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offizieller Radarr-Subreddit*](https://reddit.com/r/radarr)
{.links-list}

Bevor Sie dorthin gehen und einen Beitrag veröffentlichen, stellen Sie sicher, dass Ihre Hilfsanfrage so gut wie möglich ist. Beschreiben Sie das Problem klar und geben Sie eine kurze Beschreibung Ihrer Konfiguration an, einschließlich Dingen wie Ihrem Betriebssystem/Distribution, der Version von .NET, der Version von Radarr, dem Download-Client und dessen Version. **Wenn Sie [Docker](https://www.docker.com/) verwenden, führen Sie bitte zuerst den [Docker-Leitfaden](/docker-guide) durch, da dies häufig auftretende Pfad-/Berechtigungsprobleme löst. Andernfalls halten Sie bitte ein [Docker Compose](/docker-guide#docker-compose) bereit. [Wie man ein Docker Compose generiert](https://trash-guides.info/compose)** Erzählen Sie uns, was Sie bereits versucht haben, worauf Sie geachtet haben. Verwenden Sie den Abschnitt [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien), um Ihre Protokollierung auf Trace zu erhöhen, das Problem zu reproduzieren, den relevanten Kontext auf einer Pastebin-Seite zu veröffentlichen und einen Link dazu in Ihrem Beitrag anzugeben. Vielleicht fügen Sie sogar einige Screenshots hinzu, um das Problem zu verdeutlichen.

Je mehr wir wissen, desto einfacher ist es, Ihnen zu helfen.

# Protokollierung und Protokolldateien

Es ist wahrscheinlich sinnvoll, auch die häufigen Probleme bei der Fehlerbehebung zu überprüfen:
- [Häufig auftretende Probleme bei Downloads und Importieren](#häufig-auftretende-probleme)
- [Häufig auftretende Probleme bei der Suche nach Indexern und Trackern](#häufig-auftretende-probleme-1)
{.links-list}

Wenn Sie nach Debug-Protokollen gefragt werden, enthalten Ihre Protokolle den Eintrag `debug`, und wenn Sie nach Trace-Protokollen gefragt werden, enthalten Ihre Protokolle den Eintrag `trace`. Wenn die von Ihnen bereitgestellten Protokolle diese Einträge nicht enthalten, handelt es sich nicht um die angeforderten Protokolle.

- Vermeiden Sie es, die gesamte Protokolldatei zu teilen, es sei denn, Sie werden dazu aufgefordert.
- Laden Sie Protokolle nicht direkt in Discord hoch oder fügen Sie sie als Textwände ein, es sei denn, Sie werden dazu aufgefordert.
- Teilen Sie die Protokolle nicht als Anhang, als Zip-Archiv oder in irgendeiner anderen Form außer als Text über die unten genannten Dienste

Um gute und nützliche Protokolle für die Weitergabe bereitzustellen:

> Stellen Sie sicher, dass kein spammy Task ausgeführt wird, wie z.B. eine RSS-Aktualisierung
{.is-warning}

1. [Erhöhen Sie die Protokollierung auf Trace (Einstellungen => Allgemein => Protokollstufe oder Bearbeiten der Konfigurationsdatei)](#trace-debug-protokolle)
2. [Protokolle löschen (System => Protokolle => Protokolle löschen oder Löschen aller Protokolle im Protokollordner)](#protokolle-löschen)
3. Reproduzieren Sie das Problem (Wiederholen Sie, was die Dinge zum Absturz bringt)
4. [Öffnen Sie die Trace-Protokolldatei (radarr.trace.txt) über die Benutzeroberfläche oder die Protokolldatei](#standardmäßiger-protokollspeicherort) im Dateisystem und finden Sie den relevanten Kontext
5. Kopieren Sie einen großen Abschnitt vor dem Problem, das Problem selbst und einen großen Abschnitt nach dem Problem.
6. Verwenden Sie [Gist](https://gist.github.com/), [0bin (**Stellen Sie sicher, dass die Colorierung deaktiviert ist**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) oder ähnliche Seiten - mit Ausnahme der unten angegebenen Seiten - um die kopierten Protokolle zu teilen

**Warnungen:**
- **Verwenden Sie nicht [pastebin.com](https://pastebin.com), da deren Filter dazu neigen, die Protokolle zu blockieren.
- Verwenden Sie nicht [pastebin.pl](https://pastebin.pl), da ihre Website häufig nicht erreichbar ist.
- Verwenden Sie nicht [JustPasteIt](https://justpaste.it/), da ihre Website das Überprüfen von Protokollen nicht ermöglicht.
- Laden Sie Ihr Protokoll nicht als Datei hoch.
- Laden Sie Ihre Protokolle nicht über Google Drive, Dropbox oder eine andere nicht oben genannte Website hoch und teilen Sie sie.
- Archivieren Sie Ihre Protokolle nicht (zip, tar (tarball), 7zip usw.).
- Teilen Sie keine Konsolenausgabe, Docker-Container-Ausgabe oder etwas anderes als die angegebenen Anwendungsprotokolle

**Wichtiger Hinweis:**
- Wenn Sie [0bin](https://0bin.net/) verwenden, stellen Sie sicher, dass die Colorierung deaktiviert ist und dass das Protokoll nach dem Lesen nicht mehr verfügbar ist.

- Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie N++ verwenden. Sie können die Funktion "In Dateien suchen" von Notepad++ verwenden, um bei Bedarf in alten Protokolldateien zu suchen.
- **Nur Unix:** Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie grep verwenden. Wenn Sie beispielsweise Informationen über den Film/die Serie/das Buch/das Lied/den Indexer "Shooter" finden möchten, können Sie den folgenden Befehl ausführen: `grep -inr -C 100 -e 'Shooter' /Pfad/zu/Protokollen/*.trace*.txt` Wenn Ihr [Appdata-Verzeichnis](/radarr/appdata-directory) in Ihrem Home-Verzeichnis liegt, würden Sie Folgendes ausführen: `grep -inr -C 100 -e 'Shooter' /home/$Benutzer/.config/logs/*.trace*.txt`

```none

    * Die Flags haben folgende Funktionen
    * -i: Groß-/Kleinschreibung ignorieren
    * -n: Zeilennummer anzeigen
    *  -r: Alle Dateien im Pfad rekursiv überprüfen
    * -C: Anzahl der Zeilen vor und nach der gefundenen Zeile angeben
    * -e: Das zu suchende Muster

```

## Standardmäßiger Protokollspeicherort

Die Protokolldateien befinden sich im [Appdata-Verzeichnis](/radarr/appdata-directory) von Radarr, im Ordner logs/. Sie können auch über die Benutzeroberfläche unter System => Protokolle => Dateien auf die Protokolldateien zugreifen.

> Hinweis: Die Protokolltabelle ("Ereignisse") in der Benutzeroberfläche ist nicht dasselbe wie die Protokolldateien und nicht so nützlich. Wenn Sie nach Protokollen gefragt werden, kopieren Sie bitte aus den Protokolldateien und nicht aus der Tabelle.
{.is-info}

## Aktualisierungsprotokollspeicherort

Die Aktualisierungsprotokolldateien befinden sich im [Appdata-Verzeichnis](/radarr/appdata-directory) von Radarr, im Ordner UpdateLogs/.

## Protokolle freigeben

Die Protokolle können in einem Forum oder Reddit-Beitrag lang und schwer lesbar sein und in Discord Spam verursachen. Verwenden Sie daher bitte [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) oder eine ähnliche Pastebin-Seite. In der Regel ist nicht die gesamte Datei erforderlich, sondern nur ein guter Teil des Kontexts vor und nach dem Problem/Fehler. Vergessen Sie nicht, auf das Ende von spammy Tasks wie einer RSS-Synchronisierung oder einer Bibliotheksaktualisierung zu warten.

## Trace-/Debug-Protokolle

Sie können die Protokollstufe unter Einstellungen => Allgemein => Protokollierung ändern. Radarr muss nicht neu gestartet werden, damit die Änderung wirksam wird. Diese Änderung betrifft nur die Protokolldateien, nicht die Protokollierungsdatenbank. Die neuesten Debug-/Trace-Protokolldateien haben die Namen `radarr.debug.txt` bzw. `radarr.trace.txt`.

Wenn Sie keinen Zugriff auf die Benutzeroberfläche haben, um die Protokollierungsstufe festzulegen, können Sie dies tun, indem Sie die Datei config.xml im AppData-Verzeichnis bearbeiten und den Wert LogLevel auf Debug oder Trace anstelle von Info setzen.

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

Radarr verwendet rollende Protokolldateien, die auf jeweils 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer `radarr.txt`, für die anderen Dateien ist `radarr.0.txt` die nächstneuere (je höher die Zahl, desto älter ist sie). Diese Protokolldatei enthält Einträge für `fatal`, `error`, `warn` und `info`.

Wenn der Debug-Protokollmodus aktiviert ist, sind zusätzliche rollende Protokolldateien `radarr.debug.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info` und `debug`. Sie decken in der Regel einen Zeitraum von 40 Stunden ab.

Wenn der Trace-Protokollmodus aktiviert ist, sind zusätzliche rollende Protokolldateien `radarr.trace.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info`, `debug` und `trace`. Aufgrund der umfangreichen Trace-Protokollierung decken sie in der Regel höchstens ein paar Stunden ab.

# Wiederherstellung nach einem fehlgeschlagenen Update

- Wir tun alles, um Probleme bei der Aktualisierung zu vermeiden, aber wenn sie auftreten, führen Sie die folgenden Schritte aus, um Ihre Installation wiederherzustellen.
- In diesem Abschnitt werden auch häufig auftretende Probleme nach der Aktualisierung behandelt.

## Das Problem ermitteln

- Der beste Ort, um nachzusehen, wenn die Anwendung nach einem Update nicht startet, ist das Überprüfen der [Aktualisierungsprotokolle](#aktualisierungsprotokollspeicherort), um festzustellen, ob das Update erfolgreich abgeschlossen wurde. Wenn es dabei keine Probleme gibt, ist der nächste Schritt, Ihre regulären Anwendungsprotokolldateien anzusehen. Erhöhen Sie vor dem erneuten Starten die Protokollierung mit [Protokollierung](/radarr/settings#logging) und [Protokolldateien](/radarr/system#log-files), um sie zu finden und die Protokollstufe zu erhöhen.
- Das am häufigsten auftretende Problem ist, dass das System, auf dem die App installiert ist, das `/tmp`-Verzeichnis manipuliert und während des Upgrades kritische \*Arr-Dateien gelöscht hat, wodurch sowohl das Upgrade als auch das Rollback fehlschlagen. In diesem Fall installieren Sie einfach die Anwendung über der vorhandenen fehlerhaften Installation.

### Datenbank-Disk-Image ist beschädigt

- Siehe unseren [FAQ-Eintrag](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)

### Migrationsproblem

- Migrationsfehler sind nicht identisch, aber hier ist ein Beispiel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### UI-Migrationsprobleme

- Wenn Sie zwischen [nicht unterstützten Versionen/Zweigen](/radarr/faq#can-i-switch-between-branches) wechseln, kann es zu einem Migrationsproblem kommen, das wie unten dargestellt aussieht. Die Lösung besteht darin, zu dem Zweig oder der höheren Version zurückzukehren, auf dem/die Sie zuvor waren, oder eine [Sicherung wiederherzustellen](/radarr/faq#how-do-i-backuprestore-radarr) für Ihre aktuelle Version.

![radarr-migration-error-ui.png](/assets/radarr/radarr-migration-error-ui.png)

### Berechtigungsproblem

- Berechtigungsprobleme treten auf, wenn die Anwendung keinen Zugriff auf die relevanten temporären Ordner und/oder den Anwendungsbinärordner hat. Beheben Sie die Berechtigungen, damit der Benutzer/die Gruppe, unter der/die die Anwendung ausgeführt wird, den entsprechenden Zugriff hat.

- Synology-Benutzer können auf diesen Synology-Bug stoßen: `Zugriff auf den Pfad '/proc/{eine Zahl}/maps' verweigert`.

- Synology-Benutzer können auch auf Platzmangel in `/tmp` auf bestimmten NAS-Geräten stoßen. Sie müssen einen anderen Pfad für `/tmp` für die App angeben. Suchen Sie Unterstützung im SynoCommunity oder anderen Synology-Supportkanälen.

## Behebung des Problems

### Probleme bei der Migration

Bei einem Migrationsproblem können Sie zunächst nicht viel tun. Wenn das Problem spezifisch für Sie ist (oder es noch keine Beiträge dazu gibt), erstellen Sie bitte einen Beitrag in [unserem Subreddit](https://reddit.com/r/radarr) oder besuchen Sie unseren [Discord](https://radarr.video/discord). Wenn andere das gleiche Problem haben, können Sie sicher sein, dass wir daran arbeiten.

> Stellen Sie bitte sicher, dass Sie nicht versucht haben, eine Datenbank von der `nightly`-Version auf die stabile Version zu verwenden. Das Wechseln zwischen verschiedenen Versionen wird nicht empfohlen.{.is-info}

### Berechtigungsprobleme

- Beheben Sie die Berechtigungen, um sicherzustellen, dass der Benutzer/die Gruppe, unter der/dem die Anwendung läuft, sowohl auf `/tmp` als auch auf das Installationsverzeichnis der Anwendung zugreifen (lesen und schreiben) kann.

- Synology-Benutzer, die Probleme mit `/proc/###/maps` haben, sollten Sonarr oder die anderen \*Arr-Anwendungen beenden und aktualisieren, um dieses Problem zu beheben. Dies ist ein Problem mit dem SynoCommunity-Paket.

### Manuelles Upgrade

Laden Sie die neueste Version von unserer Website herunter.

Installieren Sie das Update (.exe) oder entpacken Sie den Inhalt über Ihre vorhandene Installation und starten Sie Radarr wie gewohnt neu.

# Downloads und Import

Das Herunterladen und Importieren ist der Bereich, in dem *die meisten* Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss Radarr in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch *viel mehr* verschiedene Setups. Das bedeutet, dass es zwar einige *übliche* Setups gibt, aber kein *richtiges* Setup und jedes Setup etwas anders sein kann.

> **Der erste Schritt besteht darin, das Protokollierungslevel auf Trace zu erhöhen. Weitere Informationen zur Anpassung der Protokollierung und zum Durchsuchen von Protokollen finden Sie unter [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien). Wiederholen Sie dann das Problem und verwenden Sie die Protokolle auf Trace-Ebene aus diesem Zeitraum, um das Problem zu untersuchen.** Wenn Ihnen jemand hilft, geben Sie den Kontext vorher/nachher in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website an, um ihn anzuzeigen. Es muss nicht die gesamte Datei sein und es sollte nicht *nur* der Fehler sein. Wiederholen Sie das Problem auch dann, wenn Aufgaben, die das Protokoll spammen, nicht ausgeführt werden.
{.is-danger}

Wenn Sie Hilfe suchen, lesen Sie unbedingt [Hilfe anfordern](#hilfe-anfordern), damit Sie uns die benötigten Details bereitstellen können.

## Testen des Download-Clients

Stellen Sie sicher, dass Ihr Download-Client läuft. Beginnen Sie mit dem Testen des Download-Clients. Wenn es nicht funktioniert, können Sie in den Protokollen auf Trace-Ebene Details sehen. Sie sollten eine URL finden, die Sie in Ihren Browser eingeben und überprüfen können, ob sie funktioniert. Es könnte ein Verbindungsproblem sein, das auf eine falsche IP, einen falschen Hostnamen, einen falschen Port oder sogar eine Firewall hinweisen könnte. Es könnte offensichtlich sein, wie ein Authentifizierungsproblem, bei dem Sie den Benutzernamen, das Passwort oder den API-Schlüssel falsch eingegeben haben. Beachten Sie, dass einige Seedboxen die Verwendung von HTTPS, Port 443 und einer URL-Basis (erweiterte Optionen) erfordern, anstelle des tatsächlichen Ports Ihres Download-Clients.

## Testen eines Downloads

Nun werden wir einen Download ausprobieren. Wählen Sie einen Film aus und führen Sie eine manuelle Suche durch. Wählen Sie eine dieser Dateien aus und versuchen Sie, sie herunterzuladen. Wird sie an den Download-Client gesendet? Wird sie mit der richtigen Kategorie angezeigt? Erscheint sie in der Aktivität? Erscheint sie in den Protokollen auf Trace-Ebene während der Aufgaben "Fertige Downloads überprüfen" (Aktualisieren von überwachten Downloads und Verarbeiten von überwachten Downloads), die etwa alle Minute ausgeführt werden? Wird sie während dieser Aufgabe korrekt analysiert? Hat der Warteschlangen-Download einen vernünftigen Namen? Da Suchvorgänge auf eindeutigen IDs auf einigen Indexern/Trackern basieren, kann es vorkommen, dass ein Download mit einem Namen in die Warteschlange gestellt wird, den er nicht erkennen kann.

## Testen eines Imports

Importprobleme sollten sich fast immer als Eintrag in der Aktivität mit einem orangefarbenen Symbol manifestieren, über das Sie den Fehler anzeigen können. Wenn sie nicht in der Aktivität angezeigt werden, sollten Sie sich zunächst auf dieses Problem konzentrieren und es beheben. Die meisten Importfehler sind Berechtigungsprobleme. Denken Sie daran, dass sowohl der Lese- als auch der Schreibzugriff auf den Download-Ordner möglich sein müssen. Manchmal können auch Berechtigungen im Bibliotheksordner das Problem sein, daher sollten Sie beide überprüfen.

Es sind auch falsche Pfadprobleme möglich, aber in normalen Setups weniger häufig. Der Schlüssel zum Verständnis von Pfadproblemen besteht darin zu wissen, dass den Pfad zum Download von der Download-Client über dessen API erhält. Dies wird zu einem Problem in einzigartigen Anwendungsfällen, z.B. wenn der Download-Client auf einem anderen System (vielleicht sogar einem anderen Betriebssystem) läuft. Es kann auch in einer Docker-Umgebung auftreten, wenn die Volumes nicht richtig konfiguriert sind. Eine Remote-Pfadzuordnung ist eine gute Lösung, wenn Sie keine Kontrolle haben, z.B. bei einer Seedbox-Konfiguration. Bei einer Docker-Umgebung ist es besser, die Pfade zu korrigieren.

## Häufige Probleme

Nachfolgend sind einige häufige Probleme aufgeführt.

### Die Web-Benutzeroberfläche des Download-Clients ist nicht aktiviert

Radarr kommuniziert mit Ihrem Download-Client über dessen API und greift über die Web-Benutzeroberfläche des Clients darauf zu. Stellen Sie sicher, dass die Web-Benutzeroberfläche des Clients aktiviert ist und der verwendete Port nicht mit anderen Client-Ports oder Ports auf Ihrem System in Konflikt steht.

### SSL wird verwendet und falsch konfiguriert

Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie sowohl Ihre Instanz als auch Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in [der SSL-FAQ](/radarr/faq#ungültiges-zertifikat-und-andere-https-oder-ssl-probleme).

### Freigabe unter Windows nicht sichtbar

Der Standardbenutzer für einen Windows-Dienst ist `LocalService`, der in der Regel keinen Zugriff auf Ihre Freigaben hat. Bearbeiten Sie den Dienst und richten Sie ihn so ein, dass er unter Ihrem eigenen Benutzerkonto ausgeführt wird. Weitere Informationen finden Sie in der FAQ [Warum kann ich meine Dateien auf einem Remote-Server nicht sehen?](/radarr/faq#warum-kann-ich-meine-dateien-auf-einem-remote-server-nicht-sehen).

### Gemappte Netzlaufwerke sind nicht zuverlässig

Obwohl gemappte Netzlaufwerke wie `X:\` praktisch sind, sind sie nicht so zuverlässig wie UNC-Pfade wie `\\server\share` und sie sind auch vor dem Anmelden nicht verfügbar. Konfigurieren Sie Ihren Download-Client so, dass er bei Bedarf UNC-Pfade verwendet. Wenn sich Ihre Bibliothek auf einem Netzwerkfreigabe befindet, stellen Sie sicher, dass Ihre Stammordner UNC-Pfade verwenden. Wenn Ihr Download-Client an eine Freigabe sendet, müssen Sie dort UNC-Pfade konfigurieren, da den Download-Pfad vom Download-Client erhält. Sie können Ihre gemappten Netzlaufwerke für sich selbst verwenden, verwenden Sie sie jedoch nicht für die Automatisierung.

### Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade

Docker fügt eine weitere Ebene von Komplexität hinzu, die leicht falsch konfiguriert werden kann, aber dennoch zu einer funktionierenden Einrichtung führt, die verschiedene Probleme aufweist. Anstatt sie hier zu erläutern, lesen Sie diesen Wiki-Artikel [für diese Automatisierungssoftware und Docker](/docker-guide), der sich mit Benutzer, Gruppe, Besitz, Berechtigungen und Pfaden befasst. Er ist nicht spezifisch für ein bestimmtes Docker-System, sondern behandelt die Dinge auf einer höheren Ebene, damit Sie sie in Ihrer eigenen Umgebung implementieren können.

### Remote-Pfadzuordnung

Wenn Sie Radarr in Docker und den Download-Client in einer Nicht-Docker-Umgebung (oder umgekehrt) haben oder die Programme auf verschiedenen Servern haben, benötigen Sie möglicherweise eine Remote-Pfadzuordnung.

Die Protokolle geben etwas Ähnliches an.

```none
2022-02-03 14:03:54.3|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /volume3/data/torrents/movies/The.Orville.2022.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Daher existiert `/volume3/data` nicht in Radarrs Container oder ist nicht zugänglich.

- [Einstellungen => Download-Clients => Remote-Pfadzuordnungen](/radarr/settings#remote-path-mappings)
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht für diesen Ordner verwendet wird.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft und \*Arr auf Windows oder umgekehrt. Eine Remote-Pfadzuordnung ist auch möglicherweise erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine einfache Suchen/Ersetzen-Funktion (wobei der REMOTE-Wert durch den LOCAL-Wert für den angegebenen Host ersetzt wird).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie in TRaSHs Tutorial](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist eine Remote-Pfadzuordnung selten erforderlich. Es wird empfohlen, [das Docker-Handbuch](/docker-guide) zu überprüfen und/oder [TRaSHs Tutorial](https://trash-guides.info/hardlinks) zu befolgen.
{.is-info}

#### Remote-Mount oder Remote-Synchronisierung (Syncthing)

- Sie müssen sicherstellen, dass die Synchronisierung die ganze Zeit erfolgt, während sie herunterlädt. Und Sie müssen das lokale Synchronisationsziel so einrichten, dass es beim Import von \*Arr zu Hardlinks werden kann, d.h. dass es dasselbe Dateisystem hat und so aussieht.
  - Synchronisieren Sie in einem niedrigeren, gemeinsamen Ordner, der sowohl unvollständige als auch abgeschlossene Dateien enthält.
  - Synchronisieren Sie an einen Speicherort, der auf demselben Dateisystem lokal wie Ihre Bibliothek liegt und so aussieht (Docker und Netzwerkfreigaben machen es leicht, dies falsch zu konfigurieren).
  - Sie möchten die unvollständigen und abgeschlossenen Dateien synchronisieren, damit, wenn der Torrent-Client den Verschiebevorgang durchführt, dies lokal reflektiert wird und alle Dateien bereits "dort" sind (auch wenn sie noch heruntergeladen werden). Dann möchten Sie Hardlinks verwenden, denn selbst wenn der Import vor Abschluss erfolgt, werden sie trotzdem fertiggestellt.
  - Auf diese Weise wird während des gesamten Herunterladens synchronisiert, dann verschiebt der Torrent-Client in den TV-Unterordner und die Synchronisierung spiegelt das wider. Auf diese Weise sind die Downloads größtenteils fertig, wenn sie als abgeschlossen deklariert werden. Und selbst wenn sie noch nicht ganz fertig sind, ist es dank der möglichen Hardlinks in Ordnung.
  - (Optional - falls zutreffend und/oder erforderlich (z.B. bei Verwendung eines Remote-Usenet-Clients)) Konfigurieren Sie ein benutzerdefiniertes Skript, das beim Import/Download/Upgrade ausgeführt wird, um die Remote-Datei zu entfernen.
- Alternativ ist eine Remote-Mount-Konfiguration anstelle einer Remote-Synchronisierung wesentlich weniger kompliziert, aber in der Regel langsamer.
  - Mounten Sie Ihren Remote-Speicher mit sshfs oder einem anderen Netzdateisystemprotokoll.
  - Stellen Sie sicher, dass der Benutzer und die Gruppe, unter der \*Arr ausgeführt wird, Lese- oder Schreibzugriff haben.
  - Konfigurieren Sie eine Remote-Pfadzuordnung, um den REMOTE-Pfad zu finden und durch den entsprechenden LOCAL-Wert zu ersetzen.

### Berechtigungen im Bibliotheksordner

Die Protokolle sehen wie folgt aus:

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/media/Movie Name (2010). Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Vergessen Sie nicht, die Berechtigungen und den Besitz des *Zielordners* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Downloads zu konzentrieren, und das ist *in der Regel* die Ursache für Berechtigungsprobleme, aber es *könnte* auch das Ziel sein. Überprüfen Sie, ob die Zielordner vorhanden sind. Überprüfen Sie, ob eine Ziel-*Datei* bereits vorhanden ist oder nicht gelöscht oder in den Papierkorb verschoben werden kann. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren, Hardlinken oder Verschieben der heruntergeladenen Datei zulassen. Der Benutzer oder die Gruppe, unter der \*Arr ausgeführt wird, muss in der Lage sein, den Stammordner zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies aufgrund der Ausführung als Dienst auftreten:
  - Der Windows-Dienst wird standardmäßig unter dem Konto "LocalService" ausgeführt. Dieses Konto hat standardmäßig keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Sie Download-Clients verwenden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "LocalService" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die App als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten. Weitere Informationen finden Sie in der FAQ, wie Sie von einem Dienst zu einer Tray-Anwendung wechseln können.

- Für Synology-Benutzer siehe [SynoCommunitys Artikel zu Berechtigungen für ihre Pakete](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Berechtigungen im Download-Ordner

Die Protokolle sehen wie folgt aus:

```none
2022-02-28 18:51:01.1|Error|DownloadedMovieImportService|Import failed, path does not exist or is not accessible by Radarr: /data/downloads/The.Movie. Ensure the path exists and the user running Radarr has the correct permissions to access this file/folder
```

Vergessen Sie nicht, die Berechtigungen und den Besitz der *Quelle* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Ziels zu konzentrieren, und das ist eine *mögliche* Ursache für Berechtigungsprobleme, aber in der Regel liegt es an der Quelle. Überprüfen Sie, ob die Quellordner vorhanden sind. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren/Hardlinken oder Kopieren+Löschen/Verschieben der heruntergeladenen Datei zulassen. Der Benutzer oder die Gruppe, unter der \*Arr ausgeführt wird, muss in der Lage sein, den Download-Ordner zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies aufgrund der Ausführung als Dienst auftreten:
  - Der Windows-Dienst wird standardmäßig unter dem Konto "LocalService" ausgeführt. Dieses Konto hat standardmäßig keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Sie Download-Clients verwenden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "LocalService" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die App als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten. Weitere Informationen finden Sie in der FAQ, wie Sie von einem Dienst zu einer Tray-Anwendung wechseln können.

- Für Synology-Benutzer siehe [SynoCommunitys Artikel zu Berechtigungen für ihre Pakete](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Download-Ordner und Bibliotheksordner sind nicht unterschiedliche Ordner

- Der Download-Client sollte in einen von \*Arr zugänglichen Ordner herunterladen, der nicht Ihr Stamm-/Bibliotheksordner ist. \*Arr sollte aus diesem separaten Download-Ordner in Ihren Bibliotheksordner importieren.
- Sie sollten niemals direkt in Ihren Stammordner herunterladen. Sie sollten auch nicht Ihren Stammordner als den abgeschlossenen Ordner oder unvollständigen Ordner Ihres Download-Clients verwenden.
- [**Dies führt auch zu einer Gesundheitsprüfung im System**](/radarr/system#herunterladen-in-den-stammordner)
- In der Anwendung wird ein Stammordner als der konfigurierte Medienbibliotheksordner definiert. Dies ist nicht der Stammordner eines Mounts. Ihr Download-Client hat einen unvollständigen oder abgeschlossenen Ordner (oder verschiebt abgeschlossene Downloads) in Ihren Stamm- (Bibliotheks-)Ordner. Dies führt häufig zu Problemen und wird nicht empfohlen. Ändern Sie Ihren Download-Client so, dass er Downloads nicht in Ihren Stammordner platziert. Beachten Sie, dass "Platzieren" auch bedeutet, dass Ihre Download-Client-Kategorie auf Ihren Stammordner festgelegt ist oder wenn NZBGet/SABnzbd die Sortierung aktiviert haben und in Ihren Stammordner sortieren. Bitte beachten Sie, dass diese Überprüfung alle definierten/konfigurierten Stammordner betrachtet, nicht nur die aktuell verwendeten Stammordner. Mit anderen Worten, der Ordner, in den Ihr Download-Client herunterlädt oder abgeschlossene Downloads verschiebt, sollte nicht derselbe Ordner sein, den Sie als Ihren Stamm-/Bibliotheks-/endgültigen Medienzielordner in der \*Arr-Anwendung konfiguriert haben.
- Konfigurierte Stammordner (auch Bibliotheksordner genannt) finden Sie unter [Einstellungen => Medienverwaltung => Stammordner](/radarr/settings/#root-folders)
- Ein Beispiel ist, wenn Ihre Downloads in `\data\downloads` gespeichert werden, dann haben Sie einen Stammordner als `\data\downloads` festgelegt.
- Es wird empfohlen, Pfade wie `\data\media\` für Ihren Stammordner/Bibliothek und `\data\downloads\` für Ihre Downloads zu verwenden.

> Ihr Download-Ordner und Ihr Stamm-/Bibliotheksordner MÜSSEN sich unterscheiden.
{.is-warning}

### Falsche Kategorie

Radarr sollte so eingerichtet sein, dass es eine Kategorie verwendet, damit es nur versucht, seine eigenen Downloads zu verarbeiten. Es ist selten, dass ein Torrent ohne die richtige Kategorie hinzugefügt wird, aber es kann vorkommen. Wenn Sie Torrents manuell hinzufügen und sie verarbeiten möchten, müssen sie die richtige Kategorie haben. Sie kann jederzeit festgelegt werden, da \*Arr versucht, Downloads alle Minute zu verarbeiten.

### Gepackte Torrents

Die Protokolle geben Fehler wie folgt an:

```none
No files found are eligible for import
```

Wenn Ihr Torrent in `.rar`-Dateien gepackt ist, müssen Sie die Entpackung einrichten. Wir empfehlen [Unpackerr](https://github.com/unpackerr/unpackerr), da es die Entpackung richtig durchführt: Es verhindert beschädigte teilweise Importe und bereinigt die entpackten Dateien nach dem Import.

Der Fehler kann auch auftreten, wenn sich kein gültiges Mediendatei im Ordner befindet.

### Wiederholte Downloads

Es gibt mehrere Ursachen für wiederholte Downloads, aber eine davon hängt mit benutzerdefinierten Formaten zusammen. Es ist möglich, dass der Veröffentlichungsname mit einem benutzerdefinierten Format übereinstimmt, die heruntergeladenen Dateien jedoch nicht. Dadurch geraten Sie in eine Schleife, in der Sie die Elemente immer wieder herunterladen, weil es wie ein Upgrade aussieht, dann aber keines ist, dann wieder auftaucht und wie ein Upgrade aussieht, dann aber keines ist. Je nach Ihrem benutzerdefinierten Format können Sie dieses Problem möglicherweise umgehen, indem Sie das benutzerdefinierte Format in Ihr Umbenennungsschema aufnehmen. (Aktivieren Sie das benutzerdefinierte Format, um es in der Umbenennung einzuschließen, und fügen Sie dann das benutzerdefinierte Format Ihrem Umbenennungsschema hinzu)

Dies kann auch daran liegen, dass der Download nie tatsächlich importiert wird und dann aus der Warteschlange fehlt. Dadurch wird immer wieder ein neuer Download abgerufen und nie importiert. Bitte sehen Sie sich die verschiedenen anderen häufigen Probleme und Fehlerbehebungsschritte dafür an.

### Usenet-Download wird nicht importiert

Radarr betrachtet nur die 60 neuesten Downloads in SABnzbd und NZBGet. Wenn Sie Ihren Verlauf beibehalten, bedeutet dies, dass während großer Warteschlangen mit Importproblemen Downloads stillschweigend verpasst und nicht importiert werden können. Der beste Weg, dies zu vermeiden, besteht darin, Ihren Verlauf zu löschen, damit alle noch angezeigten Elemente untersucht werden können. Sie können dies erreichen, indem Sie unter "Abgeschlossen und fehlgeschlagen" die Option "Entfernen" aktivieren. Bei NZBGet werden die Elemente in den versteckten Verlauf verschoben, was großartig ist. Leider verfügt SABnzbd nicht über eine ähnliche Funktion. Das Beste, was Sie dort erreichen können, ist die Verwendung des NZB-Backup-Ordners.

### Download-Client löscht Elemente

Der Download-Client sollte nicht dafür verantwortlich sein, Downloads zu entfernen. Usenet-Clients sollten so konfiguriert sein, dass sie Downloads nicht aus dem Verlauf entfernen. Torrent-Clients sollten so eingerichtet sein, dass sie Torrents nicht entfernen, wenn sie fertig sind (stattdessen pausieren oder stoppen). Dies liegt daran, dass Radarr mit dem Download-Client kommuniziert, um zu wissen, was importiert werden soll. Wenn sie entfernt werden, gibt es nichts zu importieren... selbst wenn sich ein Ordner mit Dateien befindet.

Bei SABnzbd wird dies mit der Einstellung "Verlauf beibehalten" behandelt.

### Download kann keinem Bibliothekselement zugeordnet werden

Aus verschiedenen Gründen können Veröffentlichungen nach dem Abrufen und Senden an den Download-Client nicht analysiert werden. "Aktivität => Optionen => Unbekannte anzeigen" (dies ist in neueren Versionen standardmäßig aktiviert) zeigt alle Elemente an, die nicht anderweitig ignoriert oder bereits in der Download-Client-Kategorie von \*Arr importiert wurden. Diese müssen in der Regel manuell zugeordnet und importiert werden.

Gründe dafür sind:
- Der Filmtitel enthält ein `:` auf TMDb und TMDb hat keinen alternativen Titel mit einem `-` oder mit einem Leerzeichen anstelle des `:`
- Der Dateiname enthält nicht das erforderliche Jahr
- AKA oder seltsame mehrere Namen; Radarr hat nur begrenzte Unterstützung dafür
- Der Dateiname passt zu mehreren Filmen
- Der Veröffentlichungsname oder die Veröffentlichungs-ID des Indexers stimmt nicht mit dem Dateinamen überein

Dies kann auch auftreten, wenn Sie eine Veröffentlichung in Ihrem Download-Client haben, aber dieses Medienelement (Film/Folge/Buch/Song) in der Anwendung nicht vorhanden ist.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist bei einem Sendevorgang aufgetreten

Dies wird durch den Indexer verursacht, der ein von der aktuellen .NET-Version in [Radarr => System => Status](/radarr/system#status) nicht unterstütztes SSL-Protokoll verwendet.

### Die Anforderung hat das Zeitlimit überschritten

Radarr erhält keine Antwort vom Client.

```none
    System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten: ’https://example.org/api?t=caps&apikey=(entfernt) —> System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Verbindung mit Indexer konnte nicht hergestellt werden

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Ein Task wurde abgebrochen.
```

Dies kann auch durch folgende Ursachen verursacht werden:

- falsch konfigurierte oder Verwendung eines VPN
- falsch konfigurierte oder Verwendung eines Proxys
- lokale DNS-Probleme - Versuchen Sie, zu einem anderen DNS-Anbieter zu wechseln
- lokale IPv6-Probleme - normalerweise ist IPv6 aktiviert, aber nicht funktionsfähig
- die Verwendung von Privoxy und dessen falsche Konfiguration

## Nicht aufgeführtes Problem

Sie können auch einige gängige Berechtigungs- und Netzwerkfehlerbehebungsbefehle [in unserem Leitfaden](/permissions-and-networking) überprüfen. Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem sein könnte, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.

# Indexer und Tracker durchsuchen

- Wenn Sie [Prowlarr](/prowlarr) verwenden, können Sie sich das [Verlauf](/prowlarr/history) aller Abfragen anzeigen lassen, die Prowlarr erhalten hat, und wie sie an die Websites gesendet wurden. Stellen Sie sicher, dass in Prowlarr unter Verlauf => Optionen "Parameter" aktiviert ist. Das (i)-Symbol bietet zusätzliche Details.

## Protokollierung auf Trace-Ebene erhöhen

> **Der erste Schritt besteht darin, die Protokollierung auf Trace-Ebene zu erhöhen. Informationen zum Anpassen der Protokollierung und zum Durchsuchen von Protokollen finden Sie unter [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien). Wiederholen Sie dann das Problem und verwenden Sie die Protokolle auf Trace-Ebene aus diesem Zeitraum, um das Problem zu untersuchen.** Wenn Ihnen jemand hilft, geben Sie den Kontext vorher/nachher in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website an, um ihn anzuzeigen. Es muss nicht die gesamte Datei sein, und es sollte nicht *nur* der Fehler sein. Sie sollten das Problem auch reproduzieren, während Aufgaben, die das Protokollspam nicht ausführen, nicht ausgeführt werden.
{.is-danger}

## Indexer oder Tracker testen

Wenn Sie einen Indexer oder Tracker testen, finden Sie in den Debug- oder Trace-Protokollen die verwendete URL. Im folgenden Beispiel sehen Sie einen erfolgreichen Test. Sie können sehen, dass er den Indexer über eine bestimmte URL mit bestimmten Parametern abfragt und dann die Antwort erhält. Sie können diese URL in Ihrem Browser testen, indem Sie `apikey=(entfernt)` durch den richtigen API-Schlüssel wie `apikey=123` ersetzen. Sie können mit den Parametern experimentieren, wenn Sie einen Fehler vom Indexer erhalten, oder sehen, ob Sie Konnektivitätsprobleme haben, wenn es überhaupt nicht funktioniert. Nachdem Sie es in Ihrem eigenen Browser getestet haben, sollten Sie es auch von dem System aus testen, auf dem es ausgeführt wird, *wenn* Sie es noch nicht getan haben.

## Suche testen

Wie beim oben beschriebenen Indexer/Tracker-Test können Sie bei Debug- oder Trace-Level-Protokollierung die verwendete URL aus den Protokolldateien abrufen, wenn Sie eine Suche auslösen. Beim Testen ist es am besten, eine so spezifische Suche wie möglich durchzuführen. Eine manuelle Suche ist gut, weil sie spezifisch ist und Sie die Ergebnisse in der Benutzeroberfläche sehen können, während Sie die Protokolle untersuchen.

Bei diesem Test suchen Sie nach offensichtlichen Fehlern und führen einige einfache Tests durch. Sie können sehen, dass die Suche die URL `https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(entfernt)&q=O+Brother+Where+Art+Thou` verwendet, die Sie selbst in einem Browser ausprobieren können, nachdem Sie `(entfernt)` durch Ihren API-Schlüssel für diesen Indexer ersetzt haben. Funktioniert es? Sehen Sie die erwarteten Ergebnisse? In dieser URL sehen Sie, dass sie die spezifische Kategorie 2000 festgelegt hat. Wenn Sie also nicht die erwarteten Ergebnisse sehen, ist dies ein wahrscheinlicher Grund. Wenn der Film auf dem Indexer nicht ordnungsgemäß kategorisiert ist, muss dies behoben werden. Schauen Sie sich das Beispiel für die XML-Ausgabe der manuellen Suche unten an, um ein Beispiel für die Ausgabe einer funktionierenden Abfrage zu sehen.

- XML-Ausgabe der manuellen Suche

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=movie&cat=2000&apikey=(entfernt)&q=O+Brother+Where+Art+Thou" rel="self" type="application/rss+xml"/>
<title>api.nzbgeek.info</title>
<description>NZBgeek API</description>
<link>http://api.nzbgeek.info/</link>
<language>en-gb</language>
<webMaster>info@nzbgeek.info (NZBgeek)</webMaster>
<category/>
<image>
<url>https://api.nzbgeek.info/covers/nzbgeek.png</url>
<title>api.nzbgeek.info</title>
<link>http://api.nzbgeek.info/</link>
<description>NZBgeek</description>
</image>
<newznab:response offset="0" total="17"/>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=e83b7ae75bca71e92367fab29b036731&apikey=(entfernt)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(entfernt)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=e83b7ae75bca71e92367fab29b036731</comments>
<pubDate>Sat, 10 Jul 2021 08:33:22 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=e83b7ae75bca71e92367fab29b036731&apikey=(entfernt)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="e83b7ae75bca71e92367fab29b036731"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=c00a92567863801ab1a4901458ae31ba&apikey=(entfernt)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(entfernt)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=c00a92567863801ab1a4901458ae31ba</comments>
<pubDate>Sun, 28 Mar 2021 10:50:38 +0000</pubDate>
<category>Movies > BluRay</category>
<description>O.Brother.Where.Art.Thou.2000.1080p.BluRay.H264.AC3.DD5.1</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=c00a92567863801ab1a4901458ae31ba&apikey=(entfernt)" length="4041237000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2050"/>
<newznab:attr name="size" value="4041237000"/>
<newznab:attr name="guid" value="c00a92567863801ab1a4901458ae31ba"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=75f5be8b4cd573c2359b638350689f73&apikey=(entfernt)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(entfernt)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=75f5be8b4cd573c2359b638350689f73</comments>
<pubDate>Sun, 28 Jul 2019 00:46:00 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.2000.720p.BrRip.x264-YIFY</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=75f5be8b4cd573c2359b638350689f73&apikey=(entfernt)" length="936738000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="936738000"/>
<newznab:attr name="guid" value="75f5be8b4cd573c2359b638350689f73"/>
</item>
<item>
<title>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</title>
<guid isPermaLink="true">https://api.nzbgeek.info/api?t=details&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(entfernt)</guid>
<link>https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(entfernt)</link>
<comments>https://nzbgeek.info/geekseek.php?guid=a0fe801d9ba0a703db7d2164e996aa1f</comments>
<pubDate>Mon, 14 Aug 2017 15:34:36 +0000</pubDate>
<category>Movies > HD</category>
<description>O.Brother.Where.Art.Thou.[bdrip-1080p-multilang-multisub-CHAPTERS]</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=a0fe801d9ba0a703db7d2164e996aa1f&apikey=(entfernt)" length="9746182000" type="application/x-nzb"/>
<newznab:attr name="category" value="2000"/>
<newznab:attr name="category" value="2040"/>
<newznab:attr name="size" value="9746182000"/>
<newznab:attr name="guid" value="a0fe801d9ba0a703db7d2164e996aa1f"/>
</item>
</channel>
</rss>
```

***Bilder benötigt***

![searches-indexers-and-trackers1.png](/assets/radarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/radarr/searches-indexers-and-trackers2.png)

- Ausschnitt aus dem Trace-Protokoll

```none
Ausschnitt aus dem Trace-Protokoll für eine manuelle Suche erforderlich
```

- Vollständiges Trace-Protokoll einer Suche

```none
Vollständiger Abschnitt des Trace-Protokolls für eine manuelle Suche erforderlich
```

## Häufige Probleme

Nachfolgend sind einige häufige Probleme aufgeführt.

### Tracker benötigt RawSearch-Fähigkeiten

- Radarr sucht nach `Kikis Delivery Service`, aber Ihr Tracker hat nur Ergebnisse für `Kiki's Delivery Service`
- Dies liegt daran, dass Ihr Tracker keine normalen standardisierten Suchen unterstützt.
- Die Lösung besteht darin, die Suchfähigkeiten der Definition Ihres Trackers zu aktualisieren, um anzuzeigen, dass er `RawSearch` [erfordert und unterstützt](https://github.com/Radarr/Radarr/issues/4502#issuecomment-981143905)
- Jackett unterstützt die Flagge, aber die Fähigkeiten müssen für jeden Indexer aktualisiert werden. Erstellen Sie eine Feature-Anfrage für Jackett, um diese Funktionalität für Ihren Indexer hinzuzufügen.
- Prowlarr unterstützt die Flagge, aber die Fähigkeiten müssen für jeden Indexer aktualisiert werden. Erstellen Sie eine Feature-Anfrage für Prowlarr, um diese Funktionalität für Ihren Indexer hinzuzufügen.

### Medien sind nicht überwacht

Der/die Film(e) wird/werden nicht überwacht.

### Falsche Kategorien

Falsche Kategorien sind wahrscheinlich die häufigste Ursache dafür, dass Ergebnisse bei manuellen Suchen in einem Indexer/Tracker angezeigt werden, aber nicht in Radarr. Der Indexer/Tracker sollte die Kategorie in den Suchergebnissen anzeigen, was Ihnen dabei helfen sollte, herauszufinden, was fehlt. Wenn Sie Jackett oder Prowlarr verwenden, hat jeder Tracker eine Liste der speziell unterstützten Kategorien. Stellen Sie sicher, dass Sie die richtigen für die Kategorien verwenden. Viele finden es hilfreich, die Liste in einem Browserfenster sichtbar zu haben, während sie den Eintrag bearbeiten.

### Erfolgreiche Abfrage - Keine Ergebnisse zurückgegeben

Sie erhalten eine ähnliche Meldung wie `Abfrage erfolgreich, aber es wurden keine Ergebnisse von Ihrem Indexer zurückgegeben. Dies kann ein Problem mit dem Indexer oder Ihren Indexer-Kategorieeinstellungen sein.`

Dies wird durch Ihren Indexer verursacht, der keine Ergebnisse zurückgibt, die sich in den von Ihnen für den Indexer konfigurierten Kategorien befinden.

### Falsche Ergebnisse

Manchmal liefert der Indexer völlig irrelevante Ergebnisse. Radarr gibt Parameter ein, um die Suche einzuschränken, aber die zurückgegebenen Ergebnisse haben nichts damit zu tun. Oder manchmal sind sie größtenteils relevant, aber mit einigen falschen Ergebnissen. Das erste ist in der Regel ein Indexer-Problem, das Sie anhand der Protokollaufzeichnungen erkennen können. Sie können diesen Indexer deaktivieren und das Problem melden. Das andere betrifft in der Regel kategorisierte Veröffentlichungen, die auf dem Indexer/Tracker gemeldet werden können.

### Fehlende Ergebnisse

Wenn Sie auf der Website Ergebnisse finden, die nicht in Radarr angezeigt werden, ist Ihr Problem wahrscheinlich eines von mehreren Möglichkeiten:

- [Falsche Kategorien - siehe oben](#wrong-categories)
- Es wird eine ID-basierte Suche (IMDbId, TMDbId usw.) durchgeführt und der Indexer hat die Veröffentlichungen nicht korrekt dieser ID zugeordnet. Dies ist etwas, das nur Ihr Indexer lösen kann. Sie müssen sicherstellen, dass die Veröffentlichung den richtigen anwendbaren IDs zugeordnet ist.
- Sie suchen nicht so, wie Radarr sucht. Es ist sehr wahrscheinlich, dass die Begriffe, nach denen Sie auf dem Indexer suchen, nicht der Art und Weise entsprechen, wie Radarr danach sucht. Sie können sehen, wie Radarr in den Protokollaufzeichnungen sucht. Textbasierte Abfragen haben in der Regel das Format `q=words%20and%20things%20here`. Dieser String ist HTTP-codiert und kann mit einem beliebigen Online-HTML-Decodierungs/-Codierungstool leicht decodiert werden.
- [Siehe FAQ, wie Radarr mit ausländischen Filmtiteln umgeht und wann Radarr danach sucht](/radarr/faq#how-does-radarr-handle-foreign-movies-or-foreign-titles)

### Zertifikatsvalidierung

Sie werden sich mit den meisten Indexern/Trackern über https verbinden, daher müssen Sie sicherstellen, dass dies auf Ihrem System ordnungsgemäß funktioniert. Das bedeutet, dass Ihre Zeitzone und die Uhrzeit korrekt eingestellt sein müssen. Außerdem müssen Ihre Systemzertifikate auf dem neuesten Stand sein.

### Erreichen von Rate-Limits

Wenn Sie Ihren Verkehr über ein VPN oder einen Proxy leiten, konkurrieren Sie möglicherweise mit 10, 100 oder 1000 anderen Personen, die alle versuchen, Dienste wie , theXEM und/oder Ihre Indexer und Tracker zu nutzen. Rate-Limiting und DDOS-Schutz werden häufig anhand der IP-Adresse durchgeführt, und Ihr VPN/Proxy-Ausgangspunkt ist eine IP-Adresse. Es sei denn, Sie befinden sich in einem repressiven Land wie China, Australien oder Südafrika, müssen Sie kein VPN/Proxy verwenden.

Rarbg neigt dazu, eine Art von Rate-Limiting in ihrer API zu haben und reagiert mit keinen Ergebnissen.

### IP-Sperre

Ähnlich wie bei Rate-Limits kann es vorkommen, dass bestimmte Indexer - wie Nyaa - eine IP-Adresse vollständig sperren. Dies ist in der Regel halbpermanent, und die Lösung besteht darin, eine neue IP-Adresse von Ihrem ISP oder VPN-Anbieter zu erhalten.

### Jahr stimmt nicht überein

- [Siehe diesen FAQ-Eintrag](/radarr/faq#how-does-radarr-determine-the-year-of-a-movie)
  - Radarr erhält Metadaten von TMDb
  - Radarr verwendet das Jahr des ältesten **Kinostarts** und das älteste **Premierendatum** für die Übereinstimmung
- In einigen Fällen wurde der Film verschoben oder verschoben, und das Jahr, das von den Release-Gruppen verwendet wird, stimmt weder mit dem Jahr des ältesten Premierendatums noch mit dem Jahr des ältesten Kinostarts überein. In diesen Situationen müssen Sie manuell erfassen und importieren.

### Jahr fehlt

Radarr wird keine Veröffentlichung erfassen, wenn der Name der Veröffentlichung kein Jahr enthält. Dies ist eine schlechte Veröffentlichung und kann nur manuell erfasst werden. Dies ist eine häufige Sache, die übersehen wird, wenn versucht wird, herauszufinden, warum ein Film nicht wie erwartet erfasst wurde.

### Verwendung des Jackett /all-Endpunkts

Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ können Sie sich das Jackett & NZBHydra2-Alternative [Prowlarr](/prowlarr) ansehen.

[Sogar Jackett sagt, dass /all vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)

Die Verwendung des all-Endpunkts hat keine Vorteile (außer reduziertem Verwaltungsaufwand), nur Nachteile:

- Sie verlieren die Kontrolle über indexer-spezifische Einstellungen (Kategorien, Suchmodi usw.)
- Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen
- Indexer-spezifische Kategorien (\>= 100000) können nicht verwendet werden.
- Langsame Indexer verlangsamen das Gesamtergebnis
- Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt

Das Hinzufügen jedes Indexers einzeln ermöglicht eine Feinabstimmung der Kategorien auf Basis des Indexers, was bei Verwendung des `/all`-Endpunkts zu Problemen führen kann, wenn die falsche Kategorie auf einigen Trackern Fehler verursacht. In , ist jeder Indexer auf 1000 Ergebnisse begrenzt, wenn die Seitenumbruch unterstützt wird, oder auf 100, wenn nicht. Das bedeutet, dass Sie, je mehr Tracker Sie zu Jackett hinzufügen, immer wahrscheinlicher Ergebnisse verpassen. Schließlich, wenn *einer* der Tracker in `/all` einen Fehler zurückgibt, wird  deaktiviert und Sie erhalten keine Ergebnisse mehr.

### Verwendung von NZBHydra2 als einzelner Eintrag

Die Verwendung von NZBHydra2 als einzelner Indexer-Eintrag (d.h. 1 NZBHydra2-Eintrag in Radarr für viele Indexer in NZBHydra2) anstelle von mehreren (d.h. viele NZBHydra2-Einträge in Radarr für viele Indexer in NZBHydra2) hat dieselben Probleme wie der `/all`-Endpunkt von Jackett.

### Problem nicht aufgelistet

Sie können auch einige gängige Berechtigungs- und Netzwerkprobleme mit den Befehlen zur Fehlerbehebung [in unserem Leitfaden](/permissions-and-networking) überprüfen. Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem sein könnte, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.

## Fehler

Dies sind einige der häufigen Fehler, die beim Hinzufügen eines Indexers auftreten können.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist bei einem Sendevorgang aufgetreten

Dies wird durch den Indexer verursacht, der ein von der aktuellen .NET-Version in [Radarr => System => Status](/radarr/system#status) nicht unterstütztes SSL-Protokoll verwendet.

### Die Anforderung hat Zeitüberschreitung

Radarr erhält keine Antwort vom Indexer.

```none
    System.NET.WebException: Die Anforderung hat Zeitüberschreitung: ’https://example.org/api?t=caps&apikey=(entfernt) —> System.NET.WebException: Die Anforderung hat Zeitüberschreitung
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Verbindung mit Indexer konnte nicht hergestellt werden

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen.
```

Dies kann auch durch folgende Ursachen verursacht werden:

- Falsch konfiguriertes VPN oder falsche Verwendung eines VPNs
- Falsch konfiguriertes Proxy oder falsche Verwendung eines Proxys
- Lokale DNS-Probleme - Versuchen Sie, einen anderen DNS-Anbieter zu verwenden
- Lokale IPv6-Probleme - in der Regel ist IPv6 aktiviert, aber nicht funktionsfähig
- Verwendung von Privoxy und falsche Konfiguration

### Problem nicht aufgelistet

Sie können auch einige gängige Berechtigungs- und Netzwerkprobleme mit den Befehlen zur Fehlerbehebung [in unserem Leitfaden](/permissions-and-networking) überprüfen. Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem sein könnte, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.