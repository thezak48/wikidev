---
title: Prowlarr Fehlerbehebung
description: 
published: true
date: 2023-08-20T00:20:04.841Z
tags: prowlarr, fehlerbehebung
editor: markdown
dateCreated: 2021-06-20T20:05:25.223Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Hilfe anfordern](#hilfe-anfordern)
- [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien)
  - [Standard-Protokolldateien](#standard-protokolldateien)
  - [Aktualisierungs-Protokolldateien](#aktualisierungs-protokolldateien)
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
- [NGINX-Fehler](#nginx-fehler)
- [Indexer-, Anwendungs- und Download-Client-Probleme](#indexer-anwendungs-und-download-client-probleme)
  - [Die Rahmenabmessungen können nicht bestimmt werden oder ein beschädigter Rahmen wurde empfangen](##die-rahmenabmessungen-können-nicht-bestimmt-werden-oder-ein-beschädigter-rahmen-wurde-empfangen)
  - [Verbindungstimeout](#verbindungstimeout)
  - [Sonarr HTTP 404-Fehler](#sonarr-http-404-fehler)
  - [\*Arr HTTP 400-Fehler](#arr-http-400-fehler)
  - [503 HTTP Service nicht verfügbar](#503-http-service-nicht-verfügbar)
  - [Ungültige Torrents](#ungültige-torrents)
  - [Suchen, Indexer und Tracker](#suchen-indexer-und-tracker)

# Hilfe anfordern

Benötigen Sie Hilfe? Das ist in Ordnung, jeder braucht manchmal Hilfe. Sie können in Echtzeit Hilfe über den Chat erhalten auf

- [<i class="fab fa-discord"></i>&emsp;Discord *Offizieller Prowlarr Discord*](https://prowlarr.com/discord)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offizieller Prowlarr Subreddit*](https://reddit.com/r/prowlarr)
{.links-list}

Aber bevor Sie dorthin gehen und einen Beitrag veröffentlichen, stellen Sie sicher, dass Ihre Hilfsanfrage so gut wie möglich ist. Beschreiben Sie das Problem klar und geben Sie eine kurze Beschreibung Ihrer Konfiguration an, einschließlich Dingen wie Ihrem Betriebssystem/Distribution, der Version von .NET, der Version von Prowlarr, dem Download-Client und dessen Version. **Wenn Sie [Docker](https://www.docker.com/) verwenden, führen Sie bitte zuerst den [Docker-Leitfaden](/docker-guide) durch, da dies häufig auftretende Probleme mit Pfaden und Berechtigungen löst. Andernfalls halten Sie bitte ein [Docker Compose](/docker-guide#docker-compose) bereit. [Wie man ein Docker Compose generiert](https://trash-guides.info/compose)** Erzählen Sie uns, was Sie bereits versucht haben, worauf Sie geachtet haben. Verwenden Sie den Abschnitt [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien), um Ihre Protokollierung auf Trace-Niveau zu erhöhen, das Problem zu reproduzieren, den relevanten Kontext auf Pastebin hochzuladen und einen Link dazu in Ihrem Beitrag anzugeben. Vielleicht fügen Sie sogar einige Screenshots hinzu, um das Problem zu verdeutlichen.

Je mehr wir wissen, desto einfacher ist es, Ihnen zu helfen.

# Protokollierung und Protokolldateien

Es ist wahrscheinlich sinnvoll, auch die [Indexer-, Anwendungs- und Download-Client-Probleme Häufige Probleme](#indexer-anwendungs-und-download-client-probleme) zu überprüfen.

> Wenn Sie aufgefordert werden, die Indexer-Antwort für Entwicklung oder Debugging bereitzustellen, lesen Sie weiter in diesem blauen Abschnitt...ansonsten fahren Sie mit den unten stehenden Schritten fort. Für das Debuggen von Indexer-Antworten ist es wahrscheinlich hilfreich, zu `Einstellungen/Entwicklung` (versteckte Seite) in Prowlarr zu gehen und vorübergehend die erweiterte Indexer-Protokollierung zu aktivieren, um die Indexer-Antwort zu protokollieren. Dies sollte nicht die ganze Zeit aktiviert sein
{.is-info}

Wenn Sie nach Debug-Protokollen gefragt werden, enthalten Ihre Protokolle den Eintrag `debug`, und wenn Sie nach Trace-Protokollen gefragt werden, enthalten Ihre Protokolle den Eintrag `trace`. Wenn die von Ihnen bereitgestellten Protokolle dies nicht enthalten, handelt es sich nicht um die angeforderten Protokolle.

- Vermeiden Sie es, die gesamte Protokolldatei zu teilen, es sei denn, Sie werden dazu aufgefordert.
- Laden Sie Protokolle nicht direkt in Discord hoch oder fügen Sie sie als Textwände ein, es sei denn, Sie werden dazu aufgefordert.
- Teilen Sie die Protokolle nicht als Anhang, als Zip-Archiv oder in irgendeiner anderen Form als Text, der über die unten aufgeführten Dienste geteilt wird.

Um gute und nützliche Protokolle für das Teilen bereitzustellen:

> Stellen Sie sicher, dass keine spammy Aufgabe ausgeführt wird, wie z.B. ein RSS-Refresh
{.is-warning}

1. [Erhöhen Sie die Protokollierung auf Trace-Niveau (Einstellungen => Allgemein => Protokollstufe oder Bearbeiten der Konfigurationsdatei)](#trace-debug-protokolle)
2. [Protokolle löschen (System => Protokolle => Protokolle löschen oder Löschen aller Protokolle im Protokollordner)](#protokolle-löschen)
3. Reproduzieren Sie das Problem (Wiederholen Sie, was die Dinge zum Absturz bringt)
4. [Öffnen Sie die Trace-Protokolldatei (Lidarr.trace.txt) über die Benutzeroberfläche oder die Protokolldatei](#standard-protokolldateien) auf dem Dateisystem und finden Sie den relevanten Kontext
5. Kopieren Sie einen großen Abschnitt vor dem Problem, das Problem selbst und einen großen Abschnitt nach dem Problem.
6. Verwenden Sie [Gist](https://gist.github.com/), [0bin (**Stellen Sie sicher, dass die Colorierung deaktiviert ist**)](https://0bin.net/), [PrivateBin](https://privatebin.net/), [Notifiarr PrivateBin](http://logs.notifiarr.com/), [Hastebin](https://hastebin.com/), [Ubuntu's Pastebin](https://pastebin.ubuntu.com/) oder ähnliche Websites - mit Ausnahme der unten aufgeführten Websites - um die kopierten Protokolle von oben zu teilen

**Warnungen:**
- **Verwenden Sie nicht [pastebin.com](https://pastebin.com), da deren Filter dazu neigen, die Protokolle zu blockieren.
- Verwenden Sie nicht [pastebin.pl](https://pastebin.pl), da ihre Website häufig nicht erreichbar ist.
- Verwenden Sie nicht [JustPasteIt](https://justpaste.it/), da ihre Website das Überprüfen von Protokollen nicht erleichtert.
- Laden Sie Ihr Protokoll nicht als Datei hoch.
- Laden Sie Ihre Protokolle nicht über Google Drive, Dropbox oder eine andere Website hoch und teilen Sie sie nicht.
- Archivieren Sie Ihre Protokolle nicht (zip, tar (tarball), 7zip usw.).
- Teilen Sie keine Konsolenausgabe, Docker-Container-Ausgabe oder etwas anderes als die angegebenen Anwendungsprotokolle.

**Wichtiger Hinweis:**
- Wenn Sie [0bin](https://0bin.net/) verwenden, stellen Sie sicher, dass die Colorierung deaktiviert ist und brennen Sie nicht nach dem Lesen.

- Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie N++ verwenden. Sie können die Funktion "In Dateien suchen" von Notepad++ verwenden, um alte Protokolldateien bei Bedarf zu durchsuchen.
- **Nur Unix:** Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie grep verwenden. Wenn Sie beispielsweise Informationen über den Film/die Serie/das Buch/das Lied/Indexer "Shooter" finden möchten, können Sie den folgenden Befehl ausführen: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Wenn Ihr [Appdata-Verzeichnis](/prowlarr/appdata-directory) in Ihrem Home-Verzeichnis liegt, würden Sie Folgendes ausführen: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Die Flags haben folgende Funktionen
    * -i: Groß-/Kleinschreibung ignorieren
    * -n: Zeilennummer anzeigen
    *  -r: rekursiv alle Dateien im Pfad überprüfen
    * -C: Anzahl der Zeilen vor und nach der gefundenen Zeile angeben
    * -e: das zu suchende Muster

```

## Standard-Protokolldateien

Die Protokolldateien befinden sich im [Appdata-Verzeichnis](/prowlarr/appdata-directory) von Prowlarr, im Ordner logs/. Sie können auch über die Benutzeroberfläche unter System => Protokolle => Dateien auf die Protokolldateien zugreifen.

> Hinweis: Die Protokolltabelle ("Ereignisse") in der Benutzeroberfläche ist nicht dasselbe wie die Protokolldateien und nicht so nützlich. Wenn Sie nach Protokollen gefragt werden, kopieren Sie bitte aus den Protokolldateien und nicht aus der Tabelle.
{.is-info}

## Aktualisierungs-Protokolldateien

Die Aktualisierungsprotokolldateien befinden sich im [Appdata-Verzeichnis](/prowlarr/appdata-directory) von Prowlarr, im Ordner UpdateLogs/.

## Protokolle teilen

Die Protokolle können in einem Forum oder Reddit-Beitrag lang und schwer lesbar sein und in Discord spammy sein. Verwenden Sie daher bitte [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) oder eine ähnliche Pastebin-Website. In der Regel ist nicht die gesamte Datei erforderlich, sondern nur ein guter Teil des Kontexts vor und nach dem Problem/Fehler. Vergessen Sie nicht, auf das Ende von spammy Aufgaben wie einer RSS-Synchronisierung oder einer Bibliotheksaktualisierung zu warten.

## Trace-/Debug-Protokolle

Sie können die Protokollstufe unter Einstellungen => Allgemein => Protokollierung ändern. Prowlarr muss nicht neu gestartet werden, damit die Änderung wirksam wird. Diese Änderung betrifft nur die Protokolldateien, nicht die Protokolldatenbank. Die neuesten Debug-/Trace-Protokolldateien haben die Namen `prowlarr.debug.txt` bzw. `prowlarr.trace.txt`.

Wenn Sie nicht auf die Benutzeroberfläche zugreifen können, um die Protokollierungsstufe festzulegen, können Sie dies tun, indem Sie die Datei config.xml im AppData-Verzeichnis bearbeiten und den Wert LogLevel auf Debug oder Trace anstelle von Info setzen.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Protokolle löschen

Sie können Protokolldateien und die Protokolldatenbank direkt über die Benutzeroberfläche unter `System` => `Protokolle` => `Dateien` und `System` => `Protokolle` => `Löschen` (Mülleimer-Symbol) löschen.

# Mehrere Protokolldateien

Prowlarr verwendet rollende Protokolldateien, die auf jeweils 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer Prowlarr.txt, für die anderen Dateien ist Prowlarr.0.txt die nächstneuere (je höher die Zahl, desto älter ist sie). Diese Protokolldatei enthält Einträge für `fatal`, `error`, `warn` und `info`.

Wenn der Debug-Protokollpegel aktiviert ist, sind zusätzliche rollende Protokolldateien `prowlarr.debug.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info` und `debug`. Sie decken in der Regel einen Zeitraum von 40 Stunden ab.

Wenn der Trace-Protokollpegel aktiviert ist, sind zusätzliche rollende Protokolldateien `prowlarr.trace.txt` vorhanden. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info`, `debug` und `trace`. Aufgrund der Trace-Verbosity decken sie in der Regel höchstens ein paar Stunden ab, manchmal sogar weniger als eine Minute, wenn Sie etwas Intensives tun.

# Wiederherstellung nach einem fehlgeschlagenen Update

Wir tun alles, um Probleme bei der Aktualisierung zu vermeiden, aber wenn sie auftreten, führen Sie die folgenden Schritte aus, um Ihre Installation wiederherzustellen.

## Das Problem ermitteln

- Der beste Ort, um nachzusehen, wenn die Anwendung nach einem Update nicht startet, ist das Überprüfen der [Aktualisierungsprotokolle](#aktualisierungs-protokolldateien) und festzustellen, ob das Update erfolgreich abgeschlossen wurde. Wenn diese keine Probleme aufweisen, ist der nächste Schritt, Ihre regulären Anwendungsprotokolldateien anzusehen. Bevor Sie erneut versuchen zu starten, verwenden Sie [Protokollierung](/prowlarr/einstellungen#protokollierung) und [Protokolldateien](/prowlarr/system#protokolldateien), um sie zu finden und den Protokollpegel zu erhöhen.
- Das am häufigsten auftretende Problem ist, dass das System, auf dem die App installiert ist, das `/tmp`-Verzeichnis manipuliert hat und während des Upgrades kritische \*Arr-Dateien gelöscht hat, was sowohl das Upgrade als auch das Rollback zum Scheitern bringt. In diesem Fall installieren Sie einfach die App über der vorhandenen fehlerhaften Installation.

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

- Synology-Benutzer können auch auf Platzmangel in `/tmp` auf bestimmten NAS-Geräten stoßen. Sie müssen einen anderen Pfad für `/tmp` für die App angeben. Suchen Sie Unterstützung im SynoCommunity oder anderen Synology-Supportkanälen.

## Das Problem beheben

Bei einem Migrationsproblem können Sie zunächst nicht viel tun. Wenn das Problem spezifisch für Sie ist (oder es noch keine Beiträge dazu gibt), erstellen Sie bitte einen Beitrag in [unserem Subreddit](https://reddit.com/r/prowlarr) oder schauen Sie in unserem [Discord](https://prowlarr.com/discord) vorbei. Wenn es andere mit dem gleichen Problem gibt, können Sie sicher sein, dass wir daran arbeiten.

> Bitte stellen Sie sicher, dass Sie nicht versucht haben, eine Datenbank von `nightly` in der stabilen Version zu verwenden. Das Wechseln zwischen Branches ist nicht ratsam.{.is-info}

### Berechtigungsprobleme

- Beheben Sie die Berechtigungen, um sicherzustellen, dass der Benutzer/die Gruppe, unter der die Anwendung ausgeführt wird, sowohl auf `/tmp` als auch auf das Installationsverzeichnis der Anwendung zugreifen kann (Lesen und Schreiben).

- Für Synology-Benutzer, die Probleme mit `/proc/###/maps` haben, sollte das Stoppen von Sonarr oder den anderen \*Arr-Anwendungen und das Aktualisieren das Problem beheben. Dies ist ein Problem mit dem SynoCommunity-Paket.

### Manuelles Upgrade

Laden Sie die neueste Version von unserer Website herunter.

Installieren Sie das Update (.exe) oder entpacken Sie den Inhalt (.zip) über Ihrer vorhandenen Installation und führen Sie Prowlarr wie gewohnt aus.

# NGINX-Fehler

In Ihrer Prowlarr-Konfiguration benötigen Sie diese Zeile:

`proxy_set_header Host $host;`

Wenn Sie eine andere `proxy_set_header` haben, müssen Sie sie durch die oben genannte Zeile ersetzen.

# Indexer-, Anwendungs- und Download-Client-Probleme

- Grundsätzlich muss Prowlarr mit Ihren Indexern kommunizieren können.
- Wenn Sie die Anwendungssynchronisierung verwenden, muss Prowlarr auch mit Ihren Anwendungen kommunizieren können und die Anwendungen müssen mit Prowlarr kommunizieren können.
- Wenn Sie einen Download-Client in Prowlarr für manuelle Downloads in Prowlarr haben, muss Prowlarr mit Ihrem Download-Client kommunizieren können.

> Beachten Sie, dass Protokolle, die Abfragen von Indexer ID 0 anzeigen: Die ID 0 ist ein generischer Test-Endpunkt, der es uns ermöglicht, zu testen, ob \*Arr auf Prowlarr zurückrufen und eine Verbindung herstellen kann, ohne tatsächlich von einem funktionierenden Indexer abhängig zu sein.
{.is-info}

Hier sind einige häufige Ursachen

## Die Rahmenabmessungen können nicht bestimmt werden oder ein beschädigter Rahmen wurde empfangen

`Die Rahmenabmessungen können nicht bestimmt werden oder ein beschädigter Rahmen wurde empfangen.`

Prowlarr hatte ein Sicherheitsproblem beim Verbinden mit der Website.

Dies wird in der Regel verursacht durch:

- lokale DNS-Probleme - Versuchen Sie, einen anderen DNS-Anbieter zu verwenden

## Verbindungstimeout

`Die Anfrage hat das Zeitlimit überschritten`

Prowlarr erhält keine Antwort vom Client. [Siehe unseren Allgemeinen Netzwerk- und Berechtigungs-Fehlerbehebung-Leitfaden](/permissions-and-networking)

Dies wird in der Regel verursacht durch:

- falsch konfigurierte oder Verwendung eines VPNs
- falsch konfigurierte oder Verwendung eines Proxys
- lokale DNS-Probleme - Versuchen Sie, einen anderen DNS-Anbieter zu verwenden
- lokale IPv6-Probleme - in der Regel ist IPv6 aktiviert, aber nicht funktionsfähig
- die Verwendung von Privoxy

## Sonarr HTTP 404-Fehler

- Dies tritt in der Regel aufgrund der Verwendung einer veralteten (End-of-Life) Version von Sonarr auf, die nicht über die v3-API-Endpunkte verfügt
- Prowlarr unterstützt Sonarr v2 nicht
- Prowlarr unterstützt nur Sonarr v3

## \*Arr HTTP 400-Fehler

- Siehe diesen FAQ-Eintrag: [Prowlarr synchronisiert X Indexer nicht mit der App](/prowlarr/faq#prowlarr-will-not-sync-x-indexer-to-app)

## 503 HTTP Service nicht verfügbar

- Dies tritt in der Regel auf, wenn Ihr Tracker Sie über Cloudflare blockiert und [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr) erforderlich ist

## Ungültige Torrents

- Versuchen Sie, den Link über die URL und die von Prowlarr verwendeten Variablen herunterzuladen.
- Versuchen Sie, den Torrent über Prowlarr zu proxyen (d.h. verwenden Sie den Prowlarr-Link, den die App verwendet hat, um die Datei herunterzuladen).
- Stellen Sie sicher, dass Ihr Cookie oder andere Anmeldeinformationen für Ihren Indexer nicht abgelaufen sind und gültig sind.
- Wenn das Problem durch Prowlarr verursacht wird, melden Sie bitte einen Fehler.

## Suchen in Indexern und Trackern

- [Lidarr-Suche und Indexer](/lidarr/troubleshooting#searches-indexers-and-trackers)
- [Radarr-Suche und Indexer](/radarr/troubleshooting#searches-indexers-and-trackers)
- [Readarr-Suche und Indexer](/readarr/troubleshooting#searches-indexers-and-trackers)
- [Sonarr-Suche und Indexer](/sonarr/troubleshooting#searches-indexers-and-trackers)
{.links-list}