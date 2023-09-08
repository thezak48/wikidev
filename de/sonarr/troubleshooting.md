---
title: Sonarr Fehlerbehebung
description: 
published: true
date: 2023-07-24T19:54:54.368Z
tags: sonarr, fehlerbehebung
editor: markdown
dateCreated: 2021-06-20T19:13:01.108Z
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
- [Downloads und Importieren](#downloads-und-importieren)
  - [Testen des Download-Clients](#testen-des-download-clients)
  - [Testen eines Downloads](#testen-eines-downloads)
  - [Testen eines Imports](#testen-eines-imports)
  - [Häufige Probleme](#häufige-probleme)
    - [Ein oder mehrere erwartete Episoden wurden nicht importiert oder fehlen](#ein-oder-mehrere-erwartete-episoden-wurden-nicht-importiert-oder-fehlen)
    - [Verwendung von Sonarr v2](#verwendung-von-sonarr-v2)
    - [WebUI des Download-Clients ist nicht aktiviert](#webui-des-download-clients-ist-nicht-aktiviert)
    - [SSL wird verwendet und falsch konfiguriert](#ssl-wird-verwendet-und-falsch-konfiguriert)
    - [Freigabe unter Windows nicht sichtbar](#freigabe-unter-windows-nicht-sichtbar)
    - [Zugriff auf Netzlaufwerke ist nicht zuverlässig](#zugriff-auf-netzlaufwerke-ist-nicht-zuverlässig)
    - [Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade](#docker-und-benutzer-gruppe-besitz-berechtigungen-und-pfade)
    - [Remote-Pfadzuordnung](#remote-pfadzuordnung)
      - [Remote-Mount oder Remote-Sync (Syncthing)](#remote-mount-oder-remote-sync-syncthing)
    - [Berechtigungen für den Bibliotheksordner](#berechtigungen-für-den-bibliotheksordner)
    - [Berechtigungen für den Download-Ordner](#berechtigungen-für-den-download-ordner)
    - [Download-Ordner und Bibliotheksordner sind nicht unterschiedliche Ordner](#download-ordner-und-bibliotheksordner-sind-nicht-unterschiedliche-ordner)
    - [Falsche Kategorie](#falsche-kategorie)
    - [Gepackte Torrents](#gepackte-torrents)
    - [Wiederholte Downloads](#wiederholte-downloads)
    - [Usenet-Download verpasst Import](#usenet-download-verpasst-import)
    - [Download-Client löscht Elemente](#download-client-löscht-elemente)
    - [Download kann keinem Bibliothekselement zugeordnet werden](#download-kann-keinem-bibliothekselement-zugeordnet-werden)
      - [Gefundene übereinstimmende Serie über Grab-History, aber Serie wurde über Serien-ID zugeordnet. Automatischer Import ist nicht möglich](#gefundene-übereinstimmende-serie-über-grab-history-aber-serie-wurde-über-serien-id-zugeordnet-automatischer-import-ist-nicht-möglich)
    - [Episodenname ist TBA](#episodenname-ist-tba)
    - [Verbindungstimeout](#verbindungstimeout)
  - [Problem nicht aufgelistet](#problem-nicht-aufgelistet)
- [Suchen, Indexer und Tracker](#suchen-indexer-und-tracker)
  - [Protokollierung auf Trace umstellen](#protokollierung-auf-trace-umstellen)
  - [Testen eines Indexers oder Trackers](#testen-eines-indexers-oder-trackers)
  - [Testen einer Suche](#testen-einer-suche)
  - [Häufige Probleme](#häufige-probleme-1)
    - [Indexer werden nicht durchsucht](#indexer-werden-nicht-durchsucht)
    - [Schlecht benannte Veröffentlichungen](#schlecht-benannte-veröffentlichungen)
    - [Tracker benötigt RawSearch Caps](#tracker-benötigt-rawsearch-caps)
    - [Serie benötigt einen Alias](#serie-benötigt-einen-alias)
    - [Serie benötigt eine XEM-Zuordnung](#serie-benötigt-eine-xem-zuordnung)
    - [Falscher Serientyp](#falscher-serientyp)
      - [Täglich](#täglich)
      - [Standard](#standard)
      - [Anime](#anime)
    - [Medien sind nicht überwacht](#medien-sind-nicht-überwacht)
    - [Abfrage erfolgreich - keine Ergebnisse zurückgegeben](#abfrage-erfolgreich-keine-ergebnisse-zurückgegeben)
    - [Falsche Kategorien](#falsche-kategorien)
    - [Falsche Ergebnisse](#falsche-ergebnisse)
    - [Fehlende Ergebnisse](#fehlende-ergebnisse)
    - [Zertifikatsvalidierung](#zertifikatsvalidierung)
    - [Erreichen von Rate-Limits](#erreichen-von-rate-limits)
    - [IP-Sperre](#ip-sperre)
    - [Verwendung des Jackett /all-Endpunkts](#verwendung-des-jackett-all-endpunkts)
    - [Verwendung von NZBHydra2 als einzelner Eintrag](#verwendung-von-nzbhydra2-als-einzelner-eintrag)
    - [Indexer wird nicht durchsucht](#indexer-wird-nicht-durchsucht)
    - [Jackett-Manuelle Suche findet mehr Ergebnisse](#jackett-manuelle-suche-findet-mehr-ergebnisse)
    - [Release-Profile werden nicht beachtet](#release-profile-werden-nicht-beachtet)
    - [Problem nicht aufgelistet](#problem-nicht-aufgelistet-1)
  - [Fehler](#fehler)
    - [Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist aufgetreten](#die-zugrunde-liegende-verbindung-wurde-geschlossen-ein-unerwarteter-fehler-ist-aufgetreten)
    - [Die Anforderung hat das Zeitlimit überschritten](#die-anforderung-hat-das-zeitlimit-überschritten)
    - [Problem nicht aufgelistet](#problem-nicht-aufgelistet-2)

# Hilfe anfordern

Benötigen Sie Hilfe? Das ist in Ordnung, jeder braucht manchmal Hilfe. Sie können in Echtzeit Hilfe über den Chat erhalten auf

- [<i class="fab fa-discord"></i>&emsp;Discord *Offizieller Sonarr-Discord*](https://discord.sonarr.tv/)
- [<i class="fab fa-reddit"></i>&emsp;Reddit *Offizieller Sonarr-Subreddit*](https://reddit.com/r/sonarr)
{.links-list}

Bevor Sie dorthin gehen und einen Beitrag veröffentlichen, stellen Sie sicher, dass Ihre Hilfsanfrage so gut wie möglich ist. Beschreiben Sie das Problem klar und geben Sie eine kurze Beschreibung Ihrer Konfiguration an, einschließlich Dingen wie Ihrem Betriebssystem/Distribution, Version von .net/Mono, Version von Sonarr, Download-Client und dessen Version. **Wenn Sie [Docker](https://www.docker.com/) verwenden, führen Sie bitte zuerst den [Docker-Leitfaden](/docker-guide) durch, da dies häufig auftretende Probleme mit Pfaden/Berechtigungen löst. Andernfalls halten Sie bitte ein [Docker Compose](/docker-guide#docker-compose) bereit. [Wie man ein Docker Compose generiert](https://trash-guides.info/compose)** Erzählen Sie uns, was Sie bereits versucht haben, worauf Sie geachtet haben. Verwenden Sie den Abschnitt [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien), um Ihre Protokollierung auf Trace umzustellen, das Problem zu reproduzieren, den relevanten Kontext auf Pastebin hochzuladen und einen Link dazu in Ihrem Beitrag anzugeben. Vielleicht fügen Sie sogar einige Screenshots hinzu, um das Problem zu verdeutlichen.

Je mehr wir wissen, desto einfacher können wir Ihnen helfen.

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

> Stellen Sie sicher, dass kein spammy Task läuft, wie z.B. ein RSS-Refresh
{.is-warning}

1. [Stellen Sie die Protokollierung auf Trace um (Einstellungen => Allgemein => Protokollstufe oder Bearbeiten der Konfigurationsdatei)](#trace-debug-protokolle)
2. [Protokolle löschen (System => Protokolle => Protokolle löschen oder Löschen aller Protokolle im Protokollordner)](#protokolle-löschen)
3. Reproduzieren Sie das Problem (Wiederholen Sie, was die Dinge kaputt macht)
4. [Öffnen Sie die Trace-Protokolldatei (sonarr.trace.txt) über die Benutzeroberfläche oder die Protokolldatei](#standard-protokolldateien) im Dateisystem und finden Sie den relevanten Kontext
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
- Wenn Sie [0bin](https://0bin.net/) verwenden, stellen Sie sicher, dass die Colorierung deaktiviert ist und dass Sie die Protokolle nicht nach dem Lesen löschen.

- Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie N++ verwenden. Sie können die Funktion "In Dateien suchen" von Notepad++ verwenden, um bei Bedarf in alten Protokolldateien zu suchen.
- **Nur Unix:** Alternativ, wenn Sie nach einem bestimmten Eintrag in einer alten Protokolldatei suchen, aber nicht sicher sind, welche, können Sie grep verwenden. Wenn Sie beispielsweise Informationen über den Film/die Serie/das Buch/das Lied/den Indexer "Shooter" finden möchten, können Sie den folgenden Befehl ausführen: `grep -inr -C 100 -e 'Shooter' /path/to/logs/*.trace*.txt` Wenn Ihr [Appdata-Verzeichnis](/sonarr/appdata-directory) in Ihrem Home-Verzeichnis liegt, würden Sie Folgendes ausführen: `grep -inr -C 100 -e 'Shooter' /home/$User/.config/logs/*.trace*.txt`

```none

    * Die Flags haben folgende Funktionen
    * -i: Groß-/Kleinschreibung ignorieren
    * -n: Zeilennummer anzeigen
    *  -r: rekursiv alle Dateien im Pfad überprüfen
    * -C: Anzahl der Zeilen vor und nach der gefundenen Zeile angeben
    * -e: das zu suchende Muster

```

## Standard-Protokolldateien

Die Protokolldateien befinden sich im [Appdata-Verzeichnis](/sonarr/appdata-directory) von Sonarr, im Ordner logs/. Sie können auch über die Benutzeroberfläche unter System => Protokolle => Dateien auf die Protokolldateien zugreifen.

> Hinweis: Die Protokolltabelle ("Ereignisse") in der Benutzeroberfläche ist nicht dasselbe wie die Protokolldateien und nicht so nützlich. Wenn Sie nach Protokollen gefragt werden, kopieren Sie bitte aus den Protokolldateien und nicht aus der Tabelle.
{.is-info}

## Aktualisierungs-Protokolldateien

Die Aktualisierungsprotokolldateien befinden sich im [Appdata-Verzeichnis](/sonarr/appdata-directory) von Sonarr, im Ordner UpdateLogs/.

## Protokolle teilen

Die Protokolle können in Foren- oder Reddit-Beiträgen lang und schwer lesbar sein und in Discord spammy sein. Verwenden Sie daher bitte [Pastebin](https://pastebin.ubuntu.com/), [Hastebin](https://hastebin.com/), [Gist](https://gist.github.com), [0bin](https://0bin.net) oder eine ähnliche Pastebin-Site. In der Regel ist nicht die gesamte Datei erforderlich, sondern nur ein guter Teil des Kontexts vor und nach dem Problem/Fehler. Vergessen Sie nicht, auf das Ende von spammy Tasks wie einer RSS-Synchronisierung oder einer Bibliotheksaktualisierung zu warten.

## Trace-/Debug-Protokolle

Sie können die Protokollstufe unter Einstellungen => Allgemein => Protokollierung ändern. Sonarr muss nicht neu gestartet werden, damit die Änderung wirksam wird. Diese Änderung betrifft nur die Protokolldateien, nicht die Protokollierungsdatenbank. Die neuesten Debug-/Trace-Protokolldateien haben die Namen `sonarr.debug.txt` bzw. `sonarr.trace.txt`.

Wenn Sie keinen Zugriff auf die Benutzeroberfläche haben, um die Protokollierungsstufe festzulegen, können Sie dies tun, indem Sie die Datei config.xml im AppData-Verzeichnis bearbeiten und den Wert LogLevel auf Debug oder Trace anstelle von Info setzen.

```xml
 <Config>
  [...]
  <LogLevel>debug</LogLevel>
  [...]
 </Config>
```

## Protokolle löschen

Sie können Protokolldateien und die Protokolldatenbank direkt über die Benutzeroberfläche löschen, unter System => Protokolle => Dateien und System => Protokolle => Löschen (Mülleimer-Symbol)

# Mehrere Protokolldateien

Sonarr verwendet rollende Protokolldateien, die auf jeweils 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer `sonarr.txt`, für die anderen Dateien ist `sonarr.0.txt` die nächstneuere (je höher die Zahl, desto älter ist sie). Diese Protokolldatei enthält `fatal`, `error`, `warn` und `info` Einträge.

Wenn der Debug-Protokollstufe aktiviert ist, sind zusätzliche `sonarr.debug.txt` rollende Protokolldateien vorhanden. Diese Protokolldateien enthalten `fatal`, `error`, `warn`, `info` und `debug` Einträge. Sie decken in der Regel einen Zeitraum von 40 Stunden ab.

Wenn die Trace-Protokollstufe aktiviert ist, sind zusätzliche `sonarr.trace.txt` rollende Protokolldateien vorhanden. Diese Protokolldateien enthalten `fatal`, `error`, `warn`, `info`, `debug` und `trace` Einträge. Aufgrund der umfangreichen Trace-Protokollierung decken sie in der Regel höchstens ein paar Stunden ab.

# Wiederherstellung nach einem fehlgeschlagenen Update

Wir tun alles, um Probleme bei der Aktualisierung zu vermeiden, aber wenn sie auftreten, führen Sie die folgenden Schritte aus, um Ihre Installation wiederherzustellen.

## Das Problem ermitteln

Der beste Ort, um nachzusehen, wenn die Anwendung nach einem Update nicht startet, ist das Überprüfen der [Aktualisierungsprotokolle](#aktualisierungs-protokolldateien) und sehen, ob das Update erfolgreich abgeschlossen wurde. Wenn diese keine Probleme aufweisen, ist der nächste Schritt, Ihre regulären Anwendungsprotokolldateien anzusehen. Bevor Sie erneut versuchen zu starten, verwenden Sie [Protokollierung](/sonarr/einstellungen#protokollierung) und [Protokolldateien](/sonarr/system#protokolldateien), um sie zu finden und die Protokollstufe zu erhöhen.

### Migrationsproblem

- Migrationsfehler sind nicht identisch, aber hier ist ein Beispiel:

```none
14-2-4 18:56:49.5|Info|MigrationLogger|\*\*\* 36: update\_with\_quality\_converters migrating \*\*\*

14-2-4 18:56:49.6|Error|MigrationLogger|SQL logic error or missing database duplicate column name: Items

While Processing: "ALTER TABLE "QualityProfiles" ADD COLUMN "Items" TEXT"

```

### Berechtigungsproblem

- Berechtigungsprobleme entstehen, wenn die Anwendung keinen Zugriff auf die relevanten temporären Ordner und/oder den Anwendungs-Binärordner hat. Beheben Sie die Berechtigungen, damit der Benutzer/die Gruppe, unter der die Anwendung ausgeführt wird, den entsprechenden Zugriff hat.

- Synology-Benutzer können auf diesen Synology-Bug stoßen: `Zugriff auf den Pfad '/proc/{eine Zahl}/maps' verweigert`.

- Synology-Benutzer können auch auf Platzmangel in `/tmp` auf bestimmten NAS-Geräten stoßen. Sie müssen einen anderen Pfad für `/tmp` für die App angeben. Suchen Sie in der SynoCommunity oder anderen Synology-Supportkanälen nach Hilfe.

## Behebung des Problems

Bei einem Migrationsproblem können Sie zunächst nicht viel tun. Wenn das Problem spezifisch für Sie ist (oder es noch keine Beiträge gibt), erstellen Sie bitte einen Beitrag in [unserem Subreddit](https://reddit.com/r/sonarr) oder besuchen Sie unseren [Discord-Server](https://discord.sonarr.tv/). Wenn andere das gleiche Problem haben, können Sie sicher sein, dass wir daran arbeiten.

> Stellen Sie bitte sicher, dass Sie nicht versucht haben, eine Datenbank von `develop` in der stabilen Version zu verwenden. Das Wechseln zwischen Branches wird nicht empfohlen.{.is-info}

### Berechtigungsprobleme

- Beheben Sie die Berechtigungen, um sicherzustellen, dass der Benutzer/die Gruppe, unter der die Anwendung läuft, sowohl auf `/tmp` als auch auf das Installationsverzeichnis der Anwendung zugreifen (lesen und schreiben) kann.

- Synology-Benutzer, die Probleme mit `/proc/###/maps` haben, sollten Sonarr oder die anderen \*Arr-Anwendungen beenden und aktualisieren. Dadurch sollte das Problem behoben werden. Dies ist ein Problem mit dem SynoCommunity-Paket.

### Manuelles Upgrade

Laden Sie die neueste Version von unserer Website herunter.

Installieren Sie das Update (.exe) oder entpacken Sie den Inhalt (.zip) über Ihre vorhandene Installation und starten Sie Sonarr wie gewohnt neu.

# Downloads und Importieren

Das Herunterladen und Importieren ist der Bereich, in dem *die meisten* Benutzer Probleme haben. Grundsätzlich muss Sonarr in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch *viel mehr* verschiedene Konfigurationen. Das bedeutet, dass es zwar einige *übliche* Konfigurationen gibt, aber es gibt keine *richtige* Konfiguration und jede Konfiguration kann etwas anders sein.

> **Der erste Schritt besteht darin, das Protokollierungsniveau auf Trace zu erhöhen. Weitere Informationen zum Anpassen der Protokollierung und zum Durchsuchen von Protokollen finden Sie unter [Protokollierung und Protokolldateien](#protokollierung-und-protokolldateien). Wiederholen Sie dann das Problem und verwenden Sie die Protokolle auf Trace-Ebene aus diesem Zeitraum, um das Problem zu untersuchen.**
> Wenn Ihnen jemand hilft, stellen Sie den Kontext vor/nach dem Problem in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website bereit, um ihn anzuzeigen.
> Es muss nicht die gesamte Datei sein und es sollte nicht *nur* der Fehler sein. Sie sollten das Problem auch reproduzieren, während keine Aufgaben ausgeführt werden, die das Protokoll spammen.
{.is-danger}

Wenn Sie Hilfe suchen, lesen Sie unbedingt [Anfrage um Hilfe](#anfrage-um-hilfe), damit Sie uns die benötigten Informationen zur Verfügung stellen können.

## Testen des Download-Clients

Stellen Sie sicher, dass Ihr Download-Client läuft. Beginnen Sie mit dem Test des Download-Clients. Wenn es nicht funktioniert, können Sie in den Protokollen auf Trace-Ebene Details sehen. Sie sollten eine URL finden, die Sie in Ihren Browser eingeben können, um zu sehen, ob sie funktioniert. Es könnte ein Verbindungsproblem sein, das auf eine falsche IP-Adresse, einen falschen Hostnamen, einen falschen Port oder sogar eine Firewall hinweisen könnte. Es könnte offensichtlich sein, wie ein Authentifizierungsproblem, bei dem Sie den Benutzernamen, das Passwort oder den API-Schlüssel falsch eingegeben haben.

## Testen eines Downloads

Nun werden wir einen Download ausprobieren. Wählen Sie eine Episode einer Serie aus und führen Sie eine manuelle Suche durch. Wählen Sie eine dieser Dateien aus und versuchen Sie, sie herunterzuladen. Wird sie an den Download-Client gesendet? Wird sie mit der richtigen Kategorie angezeigt? Erscheint sie in der Aktivität? Erscheint sie in den Protokollen auf Trace-Ebene während der Aufgaben "Fertige Downloads überprüfen" (Aktualisieren von überwachten Downloads und Verarbeiten von überwachten Downloads), die etwa alle Minute ausgeführt werden? Wird sie während dieser Aufgabe korrekt analysiert? Hat der heruntergeladene Download einen vernünftigen Namen? Da Suchvorgänge bei einigen Indexern/Trackern anhand der ID erfolgen, kann es vorkommen, dass ein Download mit einem Namen in die Warteschlange gestellt wird, den er nicht erkennen kann.

## Testen eines Imports

Importprobleme sollten fast immer als Eintrag in der Aktivität mit einem orangefarbenen Symbol angezeigt werden, über das Sie den Fehler anzeigen können. Wenn sie nicht in der Aktivität angezeigt werden, sollten Sie sich zunächst auf dieses Problem konzentrieren und es beheben. Die meisten Importfehler sind *Berechtigungsprobleme*. Denken Sie daran, dass Sonarr Lese- und Schreibzugriff auf den Download-Ordner haben muss. Manchmal können auch Berechtigungen im Bibliotheksordner das Problem sein, also überprüfen Sie beide.

Falsche Pfadprobleme sind ebenfalls möglich, treten jedoch in normalen Konfigurationen weniger häufig auf. Der Schlüssel zum Verständnis von Pfadproblemen besteht darin zu wissen, dass Sonarr den Pfad zum Download *vom* Download-Client über dessen API erhält. Dies wird zu einem Problem in einzigartigen Anwendungsfällen, z.B. wenn der Download-Client auf einem anderen System (vielleicht sogar einem anderen Betriebssystem) läuft. Es kann auch in einer Docker-Konfiguration auftreten, wenn die Volumes nicht richtig eingerichtet sind. Eine Remote-Pfadzuordnung ist eine gute Lösung, wenn Sie keine Kontrolle haben, z.B. bei einer Seedbox-Konfiguration. Bei einer Docker-Konfiguration ist es besser, die Pfade zu korrigieren.

## Häufige Probleme

Hier sind einige häufige Probleme aufgeführt.

### Eine oder mehrere erwartete Episoden wurden nicht importiert oder fehlen

- Wenn alle Episoden importiert wurden, ist die häufigste Ursache, dass ein Season Pack heruntergeladen wurde, das nicht alle Episoden der Staffel enthält. Klicken Sie auf das `X`, um den Release zu entfernen und zu ignorieren.
- Bei allen anderen Problemen konnten eine oder mehrere Episoden nicht importiert werden. Überprüfen Sie die Informationen in der Benutzeroberfläche und andere häufige Probleme.

### Verwendung von Sonarr v2

Sonarr v2 wurde seit 3/2021 eingestellt und wird nicht mehr unterstützt. Es ist nicht kompatibel mit qBittorrent v4.3.0 oder neuer. Aktualisieren Sie auf Sonarr v3.

### Die WebUI des Download-Clients ist nicht aktiviert

Sonarr kommuniziert über die API mit Ihrem Download-Client und greift über die WebUI des Clients darauf zu. Stellen Sie sicher, dass die WebUI des Clients aktiviert ist und der verwendete Port nicht mit anderen Client-Ports oder Ports auf Ihrem System in Konflikt steht.

### Falsche Verwendung und falsche Konfiguration von SSL

Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie Ihre Instanz und Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in [der SSL-FAQ](/sonarr/faq#invalid-certificate-and-other-HTTPS-or-SSL-issues).

### Freigabe unter Windows nicht sichtbar

Der Standardbenutzer für einen Windows-Dienst ist `LocalService`, der in der Regel keinen Zugriff auf Ihre Freigaben hat. Bearbeiten Sie den Dienst und richten Sie ihn so ein, dass er unter Ihrem eigenen Benutzerkonto ausgeführt wird. Weitere Informationen finden Sie in der FAQ [Warum kann ich meine Dateien auf einem Remote-Server nicht sehen?](/sonarr/faq#why-cant-i-see-my-files-on-a-remote-server).

### Netzwerklaufwerke sind nicht zuverlässig

Obwohl Netzwerklaufwerke wie `X:\` praktisch sind, sind sie nicht so zuverlässig wie UNC-Pfade wie `\\server\share` und sie sind auch vor der Anmeldung nicht verfügbar. Konfigurieren Sie Ihre Download-Clients so, dass sie bei Bedarf UNC-Pfade verwenden. Wenn sich Ihre Bibliothek auf einem Netzwerkfreigabe befindet, stellen Sie sicher, dass Ihre Stammordner UNC-Pfade verwenden. Wenn Ihr Download-Client an eine Freigabe sendet, müssen Sie dort UNC-Pfade konfigurieren, da Sonarr den Download-Pfad vom Download-Client erhält. Sie können Ihre Netzwerklaufwerke für den persönlichen Gebrauch behalten, verwenden Sie sie jedoch nicht für die Automatisierung.

### Docker und Benutzer, Gruppe, Besitz, Berechtigungen und Pfade

Docker fügt eine weitere Ebene von Komplexität hinzu, die leicht falsch konfiguriert werden kann, aber dennoch zu einer funktionierenden Einrichtung mit verschiedenen Problemen führt. Anstatt sie hier zu erläutern, lesen Sie diesen Wiki-Artikel [für diese Automatisierungssoftware und Docker](/docker-guide), der sich mit Benutzer, Gruppe, Besitz, Berechtigungen und Pfaden befasst. Er ist nicht spezifisch für ein bestimmtes Docker-System, sondern behandelt die Dinge auf einer höheren Ebene, damit Sie sie in Ihrer eigenen Umgebung implementieren können.

### Remote-Pfadzuordnung

Wenn Sie Sonarr in Docker und den Download-Client nicht in Docker (oder umgekehrt) haben oder die Programme auf verschiedenen Servern haben, benötigen Sie möglicherweise eine Remote-Pfadzuordnung.

Die Protokolle sehen wie folgt aus:

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/torrents/tv/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Daher existiert `/volume3/data` nicht in Sonarrs Container oder ist nicht zugänglich.

- [Einstellungen => Download-Clients => Remote-Pfadzuordnungen](/sonarr/settings#remote-path-mappings)
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht für diesen Ordner verwendet wird.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft und \*Arr auf Windows oder umgekehrt. Eine Remote-Pfadzuordnung ist auch möglicherweise erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine einfache Suchen/Ersetzen-Funktion (sie sucht nach dem REMOTE-Wert und ersetzt ihn durch den LOCAL-Wert für den angegebenen Host).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie in TRaSHs Tutorial](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist eine Remote-Pfadzuordnung selten erforderlich. Es wird empfohlen, dass Sie [den Docker-Guide](/docker-guide) überprüfen und/oder [TRaSHs Tutorial](https://trash-guides.info/hardlinks) befolgen.
{.is-info}

#### Remote-Mount oder Remote-Synchronisierung (Syncthing)

- Sie müssen sicherstellen, dass es die ganze Zeit synchronisiert wird, während es herunterlädt. Und Sie müssen sicherstellen, dass das lokale Synchronisationsziel als Hardlinks verwendet werden kann, wenn \*Arr importiert wird, d.h. dass es sich um dasselbe Dateisystem handelt und so aussieht.
  - Synchronisieren Sie in einem niedrigeren, gemeinsamen Ordner, der sowohl unvollständige als auch vollständige Dateien enthält.
  - Synchronisieren Sie an einen Speicherort, der auf demselben Dateisystem lokal wie Ihre Bibliothek liegt und so aussieht (Docker und Netzwerkfreigaben machen es leicht, dies falsch zu konfigurieren).
  - Sie möchten die unvollständigen und vollständigen Dateien synchronisieren, damit, wenn der Torrent-Client den Verschiebevorgang durchführt, dies lokal reflektiert wird und alle Dateien bereits "dort" sind (auch wenn sie noch heruntergeladen werden). Dann möchten Sie Hardlinks verwenden, denn selbst wenn der Import vor Abschluss erfolgt, werden sie trotzdem fertiggestellt.
  - Auf diese Weise wird während des gesamten Downloads synchronisiert, dann verschiebt der Torrent-Client in den Unterordner "tv" und die Synchronisierung spiegelt das wider. Auf diese Weise sind die Downloads größtenteils vorhanden, wenn sie als abgeschlossen deklariert werden. Und selbst wenn sie noch nicht vollständig sind, ist es in Ordnung, dass der Hardlink möglich ist.
  - (Optional - falls zutreffend und/oder erforderlich (z.B. Remote-Usenet-Client)) Konfigurieren Sie ein benutzerdefiniertes Skript, das beim Import/Download/Upgrade ausgeführt wird, um die Remote-Datei zu entfernen.
- Alternativ ist eine Remote-Mount-Konfiguration anstelle einer Remote-Synchronisierung erheblich weniger kompliziert zu konfigurieren, funktioniert jedoch in der Regel langsamer.
  - Mounten Sie Ihren Remote-Speicher mit sshfs oder einem anderen Netzdateisystemprotokoll.
  - Stellen Sie sicher, dass der Benutzer und die Gruppe, unter der \*Arr ausgeführt wird, Lese- oder Schreibzugriff haben.
  - Konfigurieren Sie eine Remote-Pfadzuordnung, um den REMOTE-Pfad zu finden und durch den entsprechenden LOCAL-Pfad zu ersetzen.

### Berechtigungen auf dem Bibliotheksordner

Die Protokolle sehen wie folgt aus:

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume3/data/tv/The Orville/Season 03/The.Orville.S03E08.1080p.WEB.H264-GGEZ[rarbg]. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

Vergessen Sie nicht, die Berechtigungen und den Besitz des *Zielordners* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Downloads zu konzentrieren, und das ist *in der Regel* die Ursache für Berechtigungsprobleme, aber es *könnte* auch das Ziel sein. Überprüfen Sie, ob die Zielordner vorhanden sind. Überprüfen Sie, ob eine Ziel-*Datei* bereits vorhanden ist oder nicht gelöscht oder in den Papierkorb verschoben werden kann. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren, Hardlinken oder Verschieben der heruntergeladenen Datei zulassen. Der Benutzer oder die Gruppe, unter der Sonarr ausgeführt wird, muss in der Lage sein, den Stammordner zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies aufgrund der Ausführung als Dienst erfolgen:
  - Der Windows-Dienst wird unter dem Konto "Local Service" ausgeführt. Standardmäßig hat dieses Konto keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Download-Clients so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "Local Service" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die App als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Die Option dazu wird während der Installation angeboten. Weitere Informationen zur Umstellung von einem Dienst auf eine Tray-Anwendung finden Sie in der FAQ.

- Für Synology-Benutzer siehe [SynoCommunitys Artikel zu Berechtigungen für ihre Pakete](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Berechtigungen auf dem Download-Ordner

Sie sehen einen Fehler ähnlich wie den folgenden:

```none
2022-02-03 14:03:54.3|Error|DownloadedEpisodesImportService|Import failed, path does not exist or is not accessible by Sonarr: /volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES.1/a4187f6c3c4445f98e85da52b83c84e8.mkv. Ensure the path exists and the user running Sonarr has the correct permissions to access this file/folder
```

oder

```none
2022-02-03 10:40:41.8|Warn|Sabnzbd|[Resident.Alien.S02E02.720p.WEB.H264-CAKES] Error occurred while trying to delete data from '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES/'.
 
[v3.0.6.1342] System.UnauthorizedAccessException: Access to the path '/volume1/THE VOID/Downloads/Usenet Downloads/complete/Resident.Alien.S02E02.720p.WEB.H264-CAKES' is denied.
```

Vergessen Sie nicht, die Berechtigungen und den Besitz der *Quelle* zu überprüfen. Es ist einfach, sich auf den Besitz und die Berechtigungen des Ziels zu fixieren, und das ist eine *mögliche* Ursache für Berechtigungsprobleme, aber in der Regel liegt es an der Quelle. Überprüfen Sie, ob die Quellordner vorhanden sind. Überprüfen Sie, ob der Besitz und die Berechtigungen das Kopieren/Hardlinken oder Kopieren+Löschen/Verschieben der Datei zulassen. Der Benutzer oder die Gruppe, unter der Sonarr ausgeführt wird, muss in der Lage sein, auf die Download-Dateien zuzugreifen und sie zu lesen und zu schreiben.

- Für Windows-Benutzer kann dies aufgrund der Ausführung als Dienst erfolgen:
  - Der Windows-Dienst wird unter dem Konto "Local Service" ausgeführt. Standardmäßig hat dieses Konto keine Berechtigung zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen. Dies ist besonders relevant, wenn Download-Clients so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.
  - "Local Service" hat auch im Allgemeinen sehr begrenzte Berechtigungen. Es wird daher empfohlen, die App als System Tray-Anwendung zu installieren, wenn der Benutzer angemeldet bleiben kann. Die Option dazu wird während der Installation angeboten. Weitere Informationen zur Umstellung von einem Dienst auf eine Tray-Anwendung finden Sie in der FAQ.

- Für Synology-Benutzer siehe [SynoCommunitys Artikel zu Berechtigungen für ihre Pakete](https://github.com/SynoCommunity/spksrc/wiki/Permission-Management)

- Nicht-Windows: Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
- Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist.

### Download-Ordner und Bibliotheksordner sind nicht unterschiedliche Ordner

- Der Download-Client sollte in einen Ordner herunterladen, der von \*Arr aus zugänglich ist und nicht Ihr Root-/Bibliotheksordner ist. Sie sollten aus diesem separaten Download-Ordner in Ihren Bibliotheksordner importieren.
- Sie sollten niemals direkt in Ihren Root-Ordner herunterladen. Sie sollten auch nicht Ihren Root-Ordner als abgeschlossenen oder unvollständigen Ordner des Download-Clients verwenden.
- [**Dies führt auch zu einer Gesundheitsprüfung im System**](/sonarr/system#downloading-into-root-folder)
- Innerhalb der Anwendung wird ein Root-Ordner als der konfigurierte Medienbibliotheksordner definiert. Dies ist nicht der Root-Ordner eines Laufwerks. Ihr Download-Client hat einen unvollständigen oder vollständigen Ordner (oder verschiebt abgeschlossene Downloads) in Ihren Root-(Bibliotheks-)Ordner. Dies führt häufig zu Problemen und wird nicht empfohlen. Um dies zu beheben, ändern Sie Ihren Download-Client so, dass er Downloads nicht in Ihren Root-Ordner platziert. Beachten Sie, dass 'Platzieren' auch bedeutet, dass Ihre Download-Client-Kategorie auf Ihren Root-Ordner eingestellt ist oder wenn NZBGet/SABnzbd das Sortieren aktiviert haben und in Ihren Root-Ordner sortieren. Bitte beachten Sie, dass diese Überprüfung alle definierten/konfigurierten Root-Ordner betrachtet, nicht nur die aktuell verwendeten Root-Ordner. Mit anderen Worten, der Ordner, in den Ihr Download-Client herunterlädt oder abgeschlossene Downloads verschiebt, sollte nicht derselbe Ordner sein, den Sie als Ihren Root-/Bibliotheks-/endgültigen Medienzielordner in der \*Arr-Anwendung konfiguriert haben.
- Konfigurierte Root-Ordner (auch als Bibliotheksordner bezeichnet) finden Sie unter [Einstellungen => Medienverwaltung => Root-Ordner](/sonarr/settings/#root-folders)
- Ein Beispiel ist, wenn Ihre Downloads in `\data\downloads` gespeichert werden, dann haben Sie einen Root-Ordner als `\data\downloads` festgelegt.
- Es wird empfohlen, Pfade wie `\data\media\` für Ihren Root-Ordner/Bibliothek und `\data\downloads\` für Ihre Downloads zu verwenden.

> Ihr Download-Ordner und Ihr Root-/Bibliotheksordner MÜSSEN getrennt sein
{.is-warning}

### Falsche Kategorie

Sonarr sollte so eingerichtet sein, dass es eine Kategorie verwendet, damit es nur versucht, seine eigenen Downloads zu verarbeiten. Es ist selten, dass ein Torrent ohne die richtige Kategorie hinzugefügt wird, aber es kann vorkommen. Wenn Sie Torrents manuell hinzufügen und sie verarbeiten möchten, müssen sie die richtige Kategorie haben. Sie kann jederzeit festgelegt werden, da Sonarr alle paar Minuten Downloads verarbeitet.

### Gepackte Torrents

Die Protokolle zeigen Fehler wie

```none
Keine geeigneten Dateien zum Importieren gefunden
```

Wenn Ihr Torrent in `.rar`-Dateien gepackt ist, müssen Sie die Entpackung einrichten. Wir empfehlen [Unpackerr](https://github.com/unpackerr/unpackerr), da es das Entpacken richtig macht: Es verhindert beschädigte teilweise Importe und bereinigt die entpackten Dateien nach dem Import.

Der Fehler kann auch auftreten, wenn sich keine gültige Mediendatei im Ordner befindet.

### Wiederholte Downloads

Es gibt einige Ursachen für wiederholte Downloads, aber eine davon hängt mit der Indexer-Beschränkung in den Freigabeprofilen zusammen. Da der Indexer *nicht* mit den Daten gespeichert wird, sind alle `preferred word`-Werte für Medien in Ihrer Bibliothek *null*, aber während der "RSS"- und Suchfunktion werden sie angewendet. Gleiches gilt für die Einschränkungen "must contain" oder "must-not" - sie gelten nur für diesen Indexer; alles andere ist erlaubt. Dadurch geraten Sie in eine Schleife, in der Sie die Elemente immer wieder herunterladen, weil es wie ein Upgrade aussieht, dann keines ist, dann wieder auftaucht und wie ein Upgrade aussieht, dann keines ist. Beschränken Sie Ihr Freigabeprofil nicht auf einen Indexer.

Dies kann auch daran liegen, dass der Download nie tatsächlich importiert wird und dann aus der Warteschlange fehlt, sodass ein neuer Download ständig heruntergeladen und nie importiert wird. Bitte beachten Sie die verschiedenen anderen häufigen Probleme und Fehlerbehebungsschritte dafür.

### Usenet-Download wird nicht importiert

Sonarr betrachtet nur die 60 neuesten Downloads in SABnzbd und NZBGet. Wenn Sie also Ihre Historie behalten, bedeutet dies, dass bei großen Warteschlangen mit Importproblemen Downloads stillschweigend verpasst und nicht importiert werden können. Der beste Weg, dies zu vermeiden, besteht darin, Ihre Historie zu löschen, damit alle noch vorhandenen Elemente untersucht werden können. Sie können dies erreichen, indem Sie "Entfernen" unter "Abgeschlossene und fehlgeschlagene Download-Handler" aktivieren. Bei NZBGet werden die Elemente in die *versteckte* Historie verschoben, was großartig ist. Leider verfügt SABnzbd nicht über eine ähnliche Funktion. Das Beste, was Sie dort erreichen können, ist die Verwendung des nzb-Backup-Ordners.

### Download-Client löscht Elemente

Der Download-Client sollte keine Downloads entfernen. Usenet-Clients sollten so konfiguriert sein, dass sie Downloads nicht aus der Historie entfernen. Torrent-Clients sollten so eingerichtet sein, dass sie Torrents nicht entfernen, wenn sie fertig sind (stattdessen pausieren oder stoppen). Dies liegt daran, dass Sonarr mit dem Download-Client kommuniziert, um zu wissen, was importiert werden soll. Wenn sie *entfernt* werden, gibt es nichts zu importieren, selbst wenn sich ein Ordner voller Dateien befindet.

Bei SABnzbd wird dies mit der Einstellung "Historie beibehalten" gehandhabt.

### Download kann keinem Bibliothekselement zugeordnet werden

Aus verschiedenen Gründen können Releases nach dem Herunterladen und Senden an den Download-Client nicht analysiert werden. Die Aktivität => Optionen => "Unbekannte anzeigen" (dies ist in aktuellen Versionen standardmäßig aktiviert) zeigt alle Elemente an, die nicht anderweitig ignoriert/ bereits in der Download-Client-Kategorie von \*Arr importiert wurden. Diese müssen in der Regel manuell zugeordnet und importiert werden.

Dies kann auch auftreten, wenn Sie ein Release in Ihrem Download-Client haben, aber dieses Medienelement (Film/Folge/Buch/Song) in der Anwendung nicht vorhanden ist.

#### Übereinstimmende Serie über Grab-Historie gefunden, aber Serie wurde anhand der Serien-ID abgeglichen. Automatischer Import ist nicht möglich

- Dieser Importfehler ist ähnlich dem oben genannten Fehler "kann nicht zugeordnet werden".
- Sonarr hat das Release aufgrund der Meldung Ihres Indexers oder Trackers, dass das Release die TVDb-ID (oder IMDb-ID) für eine gewünschte Serie hatte, heruntergeladen.
- Die Serie der heruntergeladenen Datei stimmt nicht mit der gemeldeten ID überein, daher importiert Sonarr die Datei nicht.
- Abhängig vom Serientitel und dem Release-Namen - vorausgesetzt, das Release ist korrekt für die zugehörige Serien-ID - muss Sonarr wahrscheinlich einen Alias hinzufügen. [Dieser FAQ-Eintrag enthält weitere Informationen](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x) zur Anforderung eines Alias.
- Alternativ ist das Release falsch gekennzeichnet und gehört nicht zur gemeldeten Serien-ID. Dies sollte Ihrem Indexer gemeldet werden, damit er entsprechende Maßnahmen ergreifen kann.
- Um diesen Fehler zu beheben:
  1. Überprüfen Sie die Serie der Datei.
  1. Fordern Sie einen Alias an (falls zutreffend).
  1. Importieren Sie die Datei manuell (Menschensymbol rechts) aus der Aktivität => Warteschlange ODER klicken Sie auf das `X` in der Warteschlange, um das Release in Ihrem Client zu ignorieren und optional auf die Blockliste zu setzen / optional aus dem Client zu entfernen.

### Episodenname ist TBA

Auf TVDB werden Episodennamen, die unbekannt sind, mit TBA betitelt, und es gibt einen 24-Stunden-Cache auf der API. Änderungen auf der TVDB-Website dauern in der Regel 24-48 Stunden, um bei Sonarr anzukommen, aufgrund des TVDB-Caches, des Skyhook-Caches und des Intervalls zur Aktualisierung der Serien.

Die Einstellung [Erforderlicher Episodentitel](/sonarr/settings#importing) in Sonarr steuert das Importverhalten, wenn der Titel TBA ist, aber nach 24 Stunden ab dem Ausstrahlungsdatum der Episode wird das Release importiert, auch wenn der Titel immer noch TBA ist. Es erfolgt auch keine automatische Umbenennung von Dateien mit TBA-Titel.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist beim Senden aufgetreten

Dies wird durch den Indexer verursacht, der ein von der aktuellen .NET-Version nicht unterstütztes SSL-Protokoll verwendet, das in [Sonarr => System => Status](/sonarr/system#status) gefunden wurde.

### Die Anforderung hat das Zeitlimit überschritten

Sonarr erhält keine Antwort vom Client.

```none
    System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten: ’https://example.org/api?t=caps&apikey=(entfernt) —> System.NET.WebException: Die Anforderung hat das Zeitlimit überschritten
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Verbindung mit Indexer nicht möglich

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen.
```

Dies kann auch durch folgende Ursachen verursacht werden:

- Falsche Konfiguration oder Verwendung eines VPNs
- Falsche Konfiguration oder Verwendung eines Proxys
- Lokale DNS-Probleme - Versuchen Sie, einen anderen DNS-Anbieter zu verwenden
- Lokale IPv6-Probleme - normalerweise ist IPv6 aktiviert, aber nicht funktionsfähig
- Verwendung von Privoxy und falsche Konfiguration

## Nicht aufgeführtes Problem

Sie können auch einige gängige Berechtigungs- und Netzwerkfehlerbehebungsbefehle [in unserem Leitfaden](/permissions-and-networking) überprüfen. Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein häufiges Problem sein könnte, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.

# Indexer und Tracker durchsuchen

- Der FAQ-Eintrag [Warum hat Sonarr eine erwartete Episode nicht heruntergeladen?](/sonarr/faq#why-didnt-sonarr-grab-an-episode-i-was-expecting) ist wahrscheinlich auch hilfreich.
- Wenn Sie [Prowlarr](/prowlarr) verwenden, können Sie im [Verlauf](/prowlarr/history) alle Abfragen anzeigen, die Prowlarr erhalten hat, und wie sie an die Websites gesendet wurden. Stellen Sie sicher, dass in Prowlarr History => Optionen "Parameter" aktiviert ist. Das (i)-Symbol bietet weitere Details.
- Die Fehlerbehebungsschritte finden Sie unten

## Protokollierung auf Trace-Ebene erhöhen

> **Der erste Schritt besteht darin, die Protokollierung auf Trace-Ebene zu erhöhen. Informationen zum Anpassen der Protokollierung und zum Durchsuchen von Protokollen finden Sie unter [Protokollierung und Protokolldateien](#logging-and-log-files). Wiederholen Sie dann das Problem und verwenden Sie die Protokolle auf Trace-Ebene aus diesem Zeitraum, um das Problem zu untersuchen.** Wenn Ihnen jemand hilft, geben Sie den Kontext vor/nach dem Problem in einem [pastebin](https://0bin.net), [Gist](https://gist.com) oder einer ähnlichen Website an, um ihn anzuzeigen. Es muss nicht die gesamte Datei sein und es sollte nicht *nur* der Fehler sein. Sie sollten das Problem auch reproduzieren, während Aufgaben, die das Protokoll spammen, nicht ausgeführt werden.
{.is-danger}

## Testen eines Indexers oder Trackers

Wenn Sie einen Indexer oder Tracker testen, finden Sie in den Debug- oder Trace-Protokollen die verwendete URL. Ein Beispiel für einen erfolgreichen Test finden Sie unten. Sie können sehen, dass er den Indexer über eine bestimmte URL mit bestimmten Parametern abfragt und dann die Antwort erhält. Sie können diese URL in Ihrem Browser testen, indem Sie `apikey=(entfernt)` durch den richtigen API-Schlüssel wie `apikey=123` ersetzen. Sie können mit den Parametern experimentieren, wenn Sie einen Fehler vom Indexer erhalten, oder sehen, ob Sie Konnektivitätsprobleme haben, wenn es überhaupt nicht funktioniert. Nachdem Sie es in Ihrem eigenen Browser getestet haben, sollten Sie es auch von dem System aus testen, auf dem es ausgeführt wird, *wenn* Sie es noch nicht getan haben.

## Suche testen

Genau wie der oben beschriebene Indexer-/Tracker-Test können Sie bei Debug- oder Trace-Level-Protokollierung die verwendete URL aus den Protokolldateien abrufen, wenn Sie eine Suche auslösen. Beim Testen ist es am besten, so spezifisch wie möglich zu suchen. Eine manuelle (interaktive) Suche nach einer einzelnen Episode oder Staffel ist gut, weil sie spezifisch ist und Sie die Ergebnisse in der Benutzeroberfläche sehen können, während Sie die Protokolle untersuchen. Manuelle (interaktive) Suchen werden ausgelöst, indem Sie zu einer Serie gehen und auf das Menschensymbol für eine Episode oder Staffel klicken.

Bei diesem Test suchen Sie nach offensichtlichen Fehlern und führen einige einfache Tests durch. Sie können sehen, dass die Suche die URL `https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(entfernt)&offset=0&limit=100&tvdbid=354629&season=1&ep=1` verwendet, die Sie selbst in einem Browser ausprobieren können, nachdem Sie (entfernt) durch Ihren API-Schlüssel für diesen Indexer ersetzt haben. Funktioniert es? Sehen Sie die erwarteten Ergebnisse? Gilt dieser FAQ-Eintrag? In dieser URL können Sie sehen, dass bestimmte Kategorien mit `cat=5030,5040,5045,5080` festgelegt wurden, daher ist dies ein wahrscheinlicher Grund, wenn Sie nicht die erwarteten Ergebnisse sehen. Sie können auch sehen, dass nach tvdbid mit `tvdbid=354629` gesucht wurde, daher muss die Episode auf dem Indexer ordnungsgemäß kategorisiert sein, um angezeigt zu werden. Sie können auch sehen, dass nach bestimmter Staffel und Episode mit season=1 und ep=1 gesucht wird, daher werden Sie diese Ergebnisse nicht sehen, wenn dies auf dem Indexer nicht korrekt ist. Schauen Sie sich unten das Beispiel für die XML-Ausgabe der manuellen Suche an, um die Ausgabe einer funktionierenden Abfrage zu sehen.

- XML-Ausgabe der manuellen Suche

```xml
<rss xmlns:atom="http://www.w3.org/2005/Atom" xmlns:newznab="http://www.newznab.com/DTD/2010/feeds/attributes/" version="2.0">
<channel>
<atom:link href="https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1" rel="self" type="application/rss+xml"/>
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
<newznab:response offset="0" total="2"/>
<item>
<title>The.Fix.S01E01.1080p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/358e0f946f953771c7688864b0334ba1
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=358e0f946f953771c7688864b0334ba1
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:32 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.1080p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=358e0f946f953771c7688864b0334ba1&apikey=(removed)" length="3810861000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="3810861000"/>
<newznab:attr name="guid" value="358e0f946f953771c7688864b0334ba1"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="55"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:54:15 +0000"/>
</item>
<item>
<title>The.Fix.S01E01.720p.AMZN.WEB-DL</title>
<guid isPermaLink="true">
https://api.nzbgeek.info/details/f7e4ac2875b6a1ce45bae91ab19e9699
</guid>
<link>
https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)
</link>
<comments>
https://nzbgeek.info/geekseek.php?guid=f7e4ac2875b6a1ce45bae91ab19e9699
</comments>
<pubDate>Wed, 20 Mar 2019 05:03:33 +0000</pubDate>
<category>TV > HD</category>
<description>The.Fix.S01E01.720p.AMZN.WEB-DL</description>
<enclosure url="https://api.nzbgeek.info/api?t=get&id=f7e4ac2875b6a1ce45bae91ab19e9699&apikey=(removed)" length="1195794000" type="application/x-nzb"/>
<newznab:attr name="category" value="5000"/>
<newznab:attr name="category" value="5040"/>
<newznab:attr name="size" value="1195794000"/>
<newznab:attr name="guid" value="f7e4ac2875b6a1ce45bae91ab19e9699"/>
<newznab:attr name="tvdbid" value="354629"/>
<newznab:attr name="season" value="S01"/>
<newznab:attr name="episode" value="E01"/>
<newznab:attr name="tvairdate" value="2019-03-18T00:00:00Z"/>
<newznab:attr name="grabs" value="14"/>
<newznab:attr name="usenetdate" value="Wed, 20 Mar 2019 04:51:45 +0000"/>
</item>
</channel>
</rss>
```

![searches-indexers-and-trackers1.png](/assets/sonarr/searches-indexers-and-trackers1.png)
![searches-indexers-and-trackers2.png](/assets/sonarr/searches-indexers-and-trackers2.png)

- Protokollausschnitt

```none
2021-03-20 13:15:23.6|Info|NzbSearchService|Suche in 1 Indexern nach [The Fix : S01E01]
2021-03-20 13:15:23.6|Debug|Newznab|Lade Feed herunter https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
2021-03-20 13:15:23.6|Trace|HttpClient|Anfrage: [GET] https://api.nzbgeek.info/api?t=tvsearch&cat=5030,5040,5045,5080&extended=1&apikey=(removed)&offset=0&limit=100&tvdbid=354629&season=1&ep=1
```

- Vollständiges Protokoll einer Suche

```none
2022-04-24 20:14:26.7|Info|ReleaseSearchService|Searching indexers for [Fairy Tail : S02E91 (91)]. 5 active indexers
2022-04-24 20:14:26.7|Debug|ReleaseSearchService|Total of 0 reports were found for [Fairy Tail : S02E91 (91)] from 5 indexers
2022-04-24 20:14:26.7|Info|DownloadDecisionMaker|No results found
```

- Note that in the above case there are 5 indexers being searched, but no results are found. This can happen if the releases for the requested episode are poorly named or not available on the indexers. Some possible solutions are:
  - Wait for a better release: Sometimes, the desired release may not be available immediately after the episode airs. It's possible that a better release will become available later.
  - Manually search for the release: If you know the specific release you're looking for, you can manually search for it using the indexer's website or search functionality.
  - Check the indexer's availability: It's possible that the indexer is experiencing issues or downtime. Check the indexer's status or try searching with a different indexer to see if the issue persists.
  - Check the indexer's category settings: Make sure that the indexer is configured to search for the correct category or type of release. If the release is categorized differently on the indexer, it may not be included in the search results.
  - Check the indexer's search capabilities: Some indexers may have limitations on the types of searches they support. Make sure that the indexer supports the specific search query you're using (e.g., season/episode format, specific keywords, etc.).
  - Improve release parsing: If the releases for the series are consistently poorly named, you can try improving the release parsing settings in Sonarr. This can help Sonarr better match the releases to the correct episodes.

- Series Packs werden nicht unterstützt
- Mehrere Staffelpakete werden nicht unterstützt
- In vielen Fällen kann Sonarr das zurückgegebene Ergebnis einfach keiner bekannten Serie zuordnen. In diesen Fällen sehen Ihre Protokolle ähnlich aus wie unten. Diese müssten manuell abgerufen und wahrscheinlich importiert werden. Der Schlüsselsatz, den Sie in den Protokollen sehen sollten, lautet `|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings`

```none
2022-02-23 14:11:09.7|Debug|Parser|Parsing string 'Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR'
2022-02-23 14:11:09.7|Trace|Parser|^(?<title>.+?)[-_. ]+?(?:S|Season|Saison|Series)[-_. ]?(?<season>\d{1,2}(?![-_. ]?\d+))(\W+|_|$)(?<extras>EXTRAS|SUBPACK)?(?!\\)
2022-02-23 14:11:09.7|Debug|Parser|Episode Parsed. Johnny Bravo 1997 Season 1 4 - Season 01 
2022-02-23 14:11:09.7|Debug|Parser|Language parsed: English
2022-02-23 14:11:09.7|Debug|QualityParser|Trying to parse quality for Johnny Bravo 1997 Season 1 4 S01 S04 Specials 576p Mixed x265 HEVC 10bit AAC 2 0 Ghost QxR
2022-02-23 14:11:09.7|Debug|Parser|Quality parsed: SDTV v1
2022-02-23 14:11:09.7|Debug|Parser|Release Group parsed: 
2022-02-23 14:11:09.8|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] Unable to identify correct episode(s) using release name and scene mappings
```

### Tracker benötigt RawSearch-Fähigkeiten

- Sonarr sucht nach `9 1 1`, aber Ihr Tracker hat nur Ergebnisse für `9-1-1` oder `John s Show` und `John's Show`
- Dies liegt daran, dass Ihr Tracker keine normalen standardisierten Suchanfragen unterstützt.
- Die Lösung besteht darin, die Suchfähigkeiten der Definition Ihres Trackers zu aktualisieren, um anzuzeigen, dass es `RawSearch` erfordert und unterstützt. (https://github.com/Sonarr/Sonarr/issues/1225#issuecomment-981153943)
- Jackett unterstützt die Flagge, aber die Fähigkeiten müssen für jeden Indexer einzeln aktualisiert werden. Erstellen Sie eine Feature-Anfrage für Jackett, um diese Funktionalität für Ihren Indexer hinzuzufügen.
- Prowlarr unterstützt die Flagge, aber die Fähigkeiten müssen für jeden Indexer einzeln aktualisiert werden. Erstellen Sie eine Feature-Anfrage für Prowlarr, um diese Funktionalität für Ihren Indexer hinzuzufügen.

### Serie benötigt einen Alias

Veröffentlichungen können als `The Series Name` hochgeladen werden, aber TVDB hat die Serie als `Series Name` oder ähnliche Namensunterschiede. Bitte lesen Sie [diesen FAQ-Eintrag](/sonarr/faq#why-cannot-sonarr-import-episode-files-for-series-x-why-cannot-sonarr-find-releases-for-series-x)

### Serie benötigt eine XEM-Zuordnung

Veröffentlichungen können als `Series Title S02E45` oder `Other Series Title S2022E42` hochgeladen werden, aber TVDB hat diese Episode als `Series Title S03E01` oder `Other Series Title S03E42`. Bitte lesen Sie [diesen FAQ-Eintrag](/sonarr/faq#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

### Falscher Serientyp

Der Serientyp beeinflusst die Art und Weise, wie Sonarr sucht. Der Serientyp sollte basierend auf der Art und Weise ausgewählt werden, wie die Serie auf den Indexern veröffentlicht wird.
[Weitere Informationen finden Sie in diesem FAQ-Eintrag](/sonarr/faq#whats-the-different-series-types)

> Wenn der Serientyp **Anime** verwendet wird, ist es [möglich, dass Ihr Indexer auch mit dem Standardtyp durchsucht wird.](/sonarr/settings#indexers)
{.is-info}

#### Täglich

Die Protokolle zeigen `Searching indexers for [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Die Protokolle zeigen `Searching indexers for [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Die Protokolle zeigen `Searching indexers for [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

### Medien sind nicht überwacht

Die Protokolle zeigen etwas Ähnliches wie

```none
2022-03-30 13:46:03.0|Debug|MonitoredEpisodeSpecification|No episodes in the release are monitored. Rejecting
2022-03-30 13:46:03.0|Debug|DownloadDecisionMaker|Release rejected for the following reasons: [Permanent] One or more episodes is not monitored
```

Die Serie/Staffel/Folge(n) werden nicht überwacht. Überprüfen Sie den Überwachungsstatus der Serie, Staffel und Folge(n).

> Staffelpakete werden nur abgerufen, wenn alle Episoden der Staffel überwacht werden und das Staffelpaket alle vorhandenen Episoden aktualisiert oder alle Episoden fehlen.
{.is-info}

### Erfolgreiche Abfrage - Keine Ergebnisse zurückgegeben

Sie erhalten eine Meldung ähnlich wie `Abfrage erfolgreich, aber es wurden keine Ergebnisse von Ihrem Indexer zurückgegeben. Dies kann ein Problem mit dem Indexer oder Ihren Indexer-Kategorieneinstellungen sein.`

Dies wird verursacht, wenn Ihr Indexer keine Ergebnisse zurückgibt, die in den von Ihnen für den Indexer konfigurierten Kategorien liegen.

### Falsche Kategorien

Falsche Kategorien sind wahrscheinlich die häufigste Ursache dafür, dass Ergebnisse bei manuellen Suchen in einem Indexer/Tracker angezeigt werden, aber nicht in \*Arr. Der Indexer/Tracker sollte die Kategorie in den Suchergebnissen anzeigen, was Ihnen helfen sollte, herauszufinden, was fehlt. Wenn Sie Jackett oder Prowlarr verwenden, hat jeder Tracker eine Liste der speziell unterstützten Kategorien. Stellen Sie sicher, dass Sie die richtigen für die Kategorien verwenden. Viele finden es hilfreich, die Liste in einem Browserfenster sichtbar zu haben, während sie den Eintrag in Sonarr bearbeiten.

> Beachten Sie, dass, wenn Sie `Anime Categories` in Ihren Indexer-Einstellungen leer lassen, der Indexer nicht für Suchen vom Typ Anime Series verwendet wird.
> Ebenso wird der Indexer nicht für Standard- oder Daily-Serientyp-Suchen verwendet, wenn Sie `Categories` in Ihren Indexer-Einstellungen leer lassen.
{.is-info}

### Falsche Ergebnisse

Manchmal liefert der Indexer völlig irrelevante Ergebnisse; Sonarr gibt Parameter ein, um die Suche auf eine Serie zu beschränken. Manchmal sind die zurückgegebenen Ergebnisse völlig unzusammenhängend. Oder manchmal überwiegend relevant mit einigen falschen Ergebnissen. Das erste ist in der Regel ein Indexer-Problem, das Sie anhand der Trace-Protokolle erkennen können. Sie können diesen Indexer deaktivieren und das Problem melden. Das andere sind in der Regel kategorisierte Veröffentlichungen, die auf dem Indexer/Tracker gemeldet werden können.

Bestimmte Tracker - wie EZTV und andere öffentliche Tracker - liefern zufällige Ergebnisse zurück, wenn sie keine exakte Übereinstimmung für die abgefragte Serie/Staffel/Folge haben. Hierfür gibt es keine Lösung.

### Fehlende Ergebnisse

Wenn Sie auf der Website Ergebnisse finden, die in Sonarr nicht angezeigt werden, liegt Ihr Problem wahrscheinlich an einer der folgenden Möglichkeiten:

- [Falsche Kategorien - siehe oben](#wrong-categories)
- Es wird eine ID-basierte Suche (IMDbId, TVDBId, etc.) durchgeführt und der Indexer hat die Veröffentlichungen nicht korrekt auf diese ID zugeordnet. Dies ist etwas, das nur Ihr Indexer lösen kann. Sie müssen sicherstellen, dass die Veröffentlichung den richtigen anwendbaren IDs zugeordnet ist.
- Es wird nicht so gesucht, wie Sonarr sucht. Es ist sehr wahrscheinlich, dass die Begriffe, nach denen Sie auf dem Indexer suchen, nicht der Art und Weise entsprechen, wie Sonarr danach sucht. Sie können sehen, wie Sonarr in den Trace-Protokollen sucht. Textbasierte Suchanfragen haben in der Regel das Format `q=words%20and%20things%20here`. Diese Zeichenkette ist HTTP-codiert und kann mit einem beliebigen Online-HTML-Codierungs/-Decodierungstool leicht decodiert werden.
- Verpasste Chunks des RSS-Feeds neuer Uploads. Die Protokolle sehen wie folgt aus und ein Ereignis mit Warnung wird vermerkt.

```none
2022-02-22 08:03:38.7|Debug|Torznab|Downloading Feed http://jackett:9117/api/v2.0/indexers/torrentdownloads/results/torznab?t=tvsearch&cat=5000,100008&extended=1&apikey=(removed)&offset=2900&limit=100
2022-02-22 08:03:40.7|Warn|Torznab|Indexer TorrentDownloads rss sync didn't cover the period between 2/21/2022 8:32:06 PM and 2/21/2022 9:02:42 PM UTC. Search may be required.
```

### Zertifikatsvalidierung

Sie werden sich mit den meisten Indexern/Trackern über https verbinden, daher müssen Sie sicherstellen, dass dies auf Ihrem System ordnungsgemäß funktioniert. Das bedeutet, dass Ihre Zeitzone und Ihre Uhrzeit *korrekt* eingestellt sein müssen. Außerdem müssen Ihre Systemzertifikate auf dem neuesten Stand sein.

### Erreichen von Rate-Limits

Wenn Sie Ihren Verkehr über ein VPN oder einen Proxy leiten, konkurrieren Sie möglicherweise mit 10, 100 oder 1000 anderen Personen, die alle versuchen, Dienste wie , theXEM und/oder Ihre Indexer und Tracker zu nutzen. Rate-Limiting und DDOS-Schutz werden häufig anhand der IP-Adresse durchgeführt, und Ihr VPN/Proxy-Ausgangspunkt ist *eine* IP-Adresse. Wenn Sie sich nicht in einem repressiven Land wie China, Australien oder Südafrika befinden, müssen Sie kein VPN/Proxy verwenden.

Rarbg neigt dazu, eine Art von Rate-Limiting in ihrer API zu haben und zeigt keine Ergebnisse an.

### IP-Sperre

Ähnlich wie bei Rate-Limits kann es vorkommen, dass bestimmte Indexer - wie Nyaa - eine IP-Adresse vollständig sperren. Dies ist in der Regel halbpermanent, und die Lösung besteht darin, eine neue IP-Adresse von Ihrem ISP oder VPN-Anbieter zu erhalten.

### Verwendung des Jackett /all-Endpunkts

Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ können Sie die Jackett & NZBHydra2-Alternative [Prowlarr](/prowlarr) ausprobieren.

[Sogar Jackett sagt, dass /all vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)

Die Verwendung des all-Endpunkts hat keine Vorteile (außer einer reduzierten Verwaltungskomplexität), nur Nachteile:

- Sie verlieren die Kontrolle über indexer-spezifische Einstellungen (Kategorien, Suchmodi usw.)
- Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen
- Indexer-spezifische Kategorien (\>= 100000) können nicht verwendet werden.
- Langsame Indexer verlangsamen das Gesamtergebnis
- Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt
- Unzusammenhängende Ergebnisse
- Fehlende Ergebnisse

Das Hinzufügen jedes Indexers einzeln ermöglicht eine Feinabstimmung der Kategorien auf Basis des Indexers, was bei Verwendung des `/all`-Endpunkts zu Problemen führen kann, wenn die falsche Kategorie auf einigen Trackern Fehler verursacht. In Sonarr ist jeder Indexer auf 1000 Ergebnisse begrenzt, wenn die Seitenumbruch unterstützt wird, oder auf 100, wenn dies nicht der Fall ist. Das bedeutet, dass Sie, je mehr Tracker Sie zu Jackett hinzufügen, immer wahrscheinlicher Ergebnisse verpassen. Schließlich, wenn *einer* der Tracker in `/all` einen Fehler zurückgibt, wird er deaktiviert und Sie erhalten keine Ergebnisse mehr.

### Verwendung von NZBHydra2 als einzelner Eintrag

Die Verwendung von NZBHydra2 als einzelner Indexer-Eintrag (d.h. 1 NZBHydra2-Eintrag in Sonarr für viele Indexer in NZBHydra2) anstelle von mehreren (d.h. viele NZBHydra2-Einträge in Sonarr für viele Indexer in NZBHydra2) hat die gleichen Probleme wie der `/all`-Endpunkt von Jackett.

### Indexer wird nicht durchsucht

- Wenn ein Indexer nicht durchsucht zu werden scheint, liegt dies wahrscheinlich daran, dass der Indexer den Abfragetyp nicht unterstützt. Der häufigste Fall ist, dass Nyaa nur Abfragen unterstützt und keine Staffel-/Folgenabfragen. Die Trace-Protokolle geben nach einem Neustart bei der ersten Suche an, welche Fähigkeiten ein Indexer hat oder nicht hat.

### Jackett-Manuelle Suche findet mehr Ergebnisse

- [Siehe diesen FAQ-Eintrag](/sonarr/faq#jackett-shows-more-results-than-sonarr-when-manually-searching)

### Release-Profile werden nicht beachtet

Es gibt einige Ursachen dafür, dass es so aussieht, als ob Ihre Profile ignoriert werden. Die häufigste Ursache ist die Indexer-Einschränkung in den Release-Profilen. Da der Indexer *nicht* mit den Daten gespeichert wird, sind alle `preferred word`-Werte für Medien in Ihrer Bibliothek *null*, aber während "RSS" und Suche werden sie angewendet. Gleiches gilt für alle Einschränkungen für `must contain` oder `must-not` contain, die nur für diesen Indexer gelten; alles andere ist erlaubt. Dadurch kann es den Anschein haben, als ob Release-Profile ignoriert werden oder Upgrade-Schleifen auftreten.

### Problem nicht aufgelistet

Sie können auch einige gängige Berechtigungs- und Netzwerkprobleme mit den in unserem Leitfaden aufgeführten Befehlen zur Fehlerbehebung überprüfen [in unserem Leitfaden](/permissions-and-networking). Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein Problem ist, das häufig auftritt, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.

## Fehler

Dies sind einige der häufigen Fehler, die beim Hinzufügen eines Indexers auftreten können.

### Die zugrunde liegende Verbindung wurde geschlossen: Ein unerwarteter Fehler ist bei einem Sendevorgang aufgetreten

Dies wird verursacht, wenn der Indexer ein von der aktuellen .NET-Version nicht unterstütztes SSL-Protokoll verwendet, das in [Sonarr => System => Status](/sonarr/system#status) gefunden wurde.

### Die Anforderung hat das Zeitlimit überschritten

Sonarr erhält keine Antwort vom Indexer.

```none
    System.NET.WebException: The request timed out: ’https://example.org/api?t=caps&apikey=(removed) —> System.NET.WebException: The request timed out
```

```none
2022-11-01 10:16:54.3|Warn|Newznab|Unable to connect to indexer

[v4.3.0.6671] System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

Dies kann auch durch folgende Ursachen verursacht werden:

- falsch konfiguriert oder Verwendung eines VPNs
- falsch konfiguriert oder Verwendung eines Proxys
- lokale DNS-Probleme - Versuchen Sie, zu einem anderen DNS-Anbieter zu wechseln
- lokale IPv6-Probleme - normalerweise ist IPv6 aktiviert, aber nicht funktionsfähig
- die Verwendung von Privoxy und eine falsche Konfiguration davon

### Problem nicht aufgelistet

Sie können auch einige gängige Berechtigungs- und Netzwerkprobleme mit den in unserem Leitfaden aufgeführten Befehlen zur Fehlerbehebung überprüfen [in unserem Leitfaden](/permissions-and-networking). Andernfalls besprechen Sie das Problem bitte mit dem Support-Team auf Discord. Wenn dies ein Problem ist, das häufig auftritt, schlagen Sie bitte vor, es dem Wiki hinzuzufügen.