---
title: Nützliche Tools
description: 
published: true
date: 2023-08-28T09:19:27.683Z
tags: useful-tools
editor: markdown
dateCreated: 2021-06-05T20:51:53.183Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Wiederherstellen einer beschädigten Datenbank](#wiederherstellen-einer-beschädigten-datenbank)
  - [Wiederherstellen einer beschädigten Datenbank (UI) (Windows)](#wiederherstellen-einer-beschädigten-datenbank-ui-windows)
  - [Wiederherstellung der Datenbank über die Befehlszeile](#wiederherstellung-der-datenbank-über-die-befehlszeile)
- [Cookies finden](#cookies-finden)
  - [Chrome](#chrome)
  - [Firefox](#firefox)
- [Cookies und lokalen Speicher löschen](#cookies-und-lokalen-speicher-löschen)
  - [Chrome](#chrome-1)
  - [Firefox](#firefox-1)
  - [Microsoft Edge (Chromium)](#microsoft-edge-chromium)
  {.links-list}
- [Andere Projekte und Programme - Anwendungen für Anfragen (\*Arrs)](#andere-projekte-und-programme-anwendungen-für-anfragen-arrs)
  - [Notifiarr](#notifiarr-fka-discord-notifier)
  - [Ombi](#ombi)
  - [Overseerr](#overseerr)
  - [Petio](#petio)
  {.links-list}
- [Andere Projekte und Programme - \*Arr-bezogen](#andere-projekte-und-programme-arr-bezogen)
  - [Fernsteuerung](#fernsteuerung)
    - [LunaSea](#lunasea)
    - [Radarr & Sonarr Companion - Android App](#radarr-sonarr-companion-android-app)
    - [nzb360 - Android App](#nzb360-android-app)
    {.links-list}
  - [Lidarr](#lidarr)
    - [AMD](#amd)
    - [AMVD](#amvd)
  - [Radarr](#radarr)
    - [AMTD](#amtd)
  - [Untertitel](#untertitel)
    - [Bazarr](#bazarr)
- [Andere Projekte und Programme - Torrents/Herunterladen](#andere-projekte-und-programme-torrentsherunterladen)
  - [Cross-Seed](#cross-seed)
  - [Unpackerr](#unpackerr)
  - [qBit Management](#qbit-management)
- [Andere Projekte und Programme](#andere-projekte-und-programme)
  - [Filebot](#filebot)
  - [JDupes](#jdupes)
  - [Just A Bunch Of Starr Scripts](#just-a-bunch-of-starr-scripts)
  - [Just A Bunch Of Plex Scripts (JBOPS)](#just-a-bunch-of-plex-scripts)
  - [Plex Meta Manager](#plex-meta-manager)
  - [Tautulli](#tautulli)
  - [Tdarr](#tdarr)
  - [tdarr_inform](#tdarr_inform)
  {.links-list}
- [Anleitung zur Twitter-Verbindung](#anleitung-zur-twitter-verbindung)

Die folgenden Apps sind Begleiter zur \*Arr Suite von Anwendungen oder allgemein zur Mediensammlung. Sie werden nicht vom \*Arr-Entwicklungsteam gewartet, entwickelt oder unterstützt. Bitte wenden Sie sich bei spezifischen Supportfragen an das jeweilige Anwendungsentwicklungsteam.

# Wiederherstellen einer beschädigten Datenbank

Beachten Sie, dass sich die Datenbank der Anwendung im Anwendungsdatenverzeichnis befindet, das unten verlinkt ist. Das Verzeichnis kann auch als Argument "datadir" übergeben werden.

- [Lidarr Appdata-Verzeichnis](/lidarr/appdata-directory)
- [Prowlarr Appdata-Verzeichnis](/prowlarr/appdata-directory)
- [Radarr Appdata-Verzeichnis](/radarr/appdata-directory)
- [Readarr Appdata-Verzeichnis](/readarr/appdata-directory)
- [Sonarr Appdata-Verzeichnis](/sonarr/appdata-directory)
{.links-list}

> Es gibt zwei Möglichkeiten, die Datenbank wiederherzustellen, die unten aufgeführt sind.{.is-info}

- [Verwendung von DB Browser für SQLite und der Benutzeroberfläche (UI)](#wiederherstellen-einer-beschädigten-datenbank-ui)
- [Verwendung der `.recover`-Funktion von Sqlite über die Befehlszeile](#wiederherstellung-der-datenbank-über-die-befehlszeile)
{.links-list}

## Wiederherstellen einer beschädigten Datenbank (UI) (Windows)

{#windows}
{#wiederherstellen-einer-beschädigten-datenbank-ui}

> Beachten Sie, dass dies im Wesentlichen dasselbe ist wie `.recover`, das Sqlite v3.29 erfordert. [Bitte beachten Sie die Sqlite-Dokumentation für weitere Details zum Befehl `.recover`](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database). Die Schritte dazu sind unten verlinkt {.is-info}

> [DB Browser für SQLite (DB4S)](https://SQLitebrowser.org/) ist ein hochwertiges, visuelles, Open-Source-Tool zum Erstellen, Entwerfen und Bearbeiten von Datenbankdateien, die mit SQLite kompatibel sind. DB4S ist für Benutzer und Entwickler gedacht, die Datenbanken erstellen, suchen und bearbeiten möchten. DB4S verwendet eine vertraute tabellenähnliche Benutzeroberfläche, und komplexe SQL-Befehle müssen nicht erlernt werden.
{.is-info}

1. Stoppen Sie die Anwendung.
1. Erstellen Sie eine Kopie Ihrer beschädigten Datenbank (`.db`) und kopieren Sie alle `.shm`- und `.wal`-Dateien.
1. Öffnen Sie Ihre beschädigte Datenbank in [DB Browser für SQLite (DB4S)](https://SQLitebrowser.org/).
1. Datei => Exportieren => Datenbank in SQL-Datei exportieren.
1. Wählen Sie alle Tabellen aus.
1. Aktivieren Sie "Spaltennamen in INSERT INTO beibehalten".
1. Exportieren Sie alles.
1. Überschreiben Sie das alte Schema.
1. Speichern Sie.
1. Schließen Sie die Datenbank.
1. Neue Datenbank => Datei => Importieren => importieren Sie die Datei aus dem vorherigen Export-Schritt.
1. Bei Importfehlern oder Problemen mit Einschränkungen bereinigen Sie den problematischen INSERT-Befehl, sofern möglich, oder löschen Sie ihn.
1. Führen Sie den folgenden SQL-Befehl aus: `VACUUM;`
1. Speichern Sie die Datenbank, wenn Sie dazu aufgefordert werden.
1. Tools => Integritätsprüfung; das Ergebnis sollte "OK" anzeigen.
1. Schließen Sie die Datenbank.
1. Entfernen Sie alle `wal`-, `shm`- und `db`-Dateien aus dem Konfigurationsordner.
1. Speichern Sie (oder kopieren Sie, wenn \*Arr nicht auf demselben System wie DB4S ausgeführt wird) die neue Datenbank im Konfigurationsordner und weisen Sie die Anwendung darauf hin. Alle \*Arrs benennen ihre Datenbank als `<appname>.db`, z.B. `radarr.db`.
1. Korrigieren Sie die Berechtigungen für die wiederhergestellte Datenbank, falls erforderlich. Der Besitzer sollte der Benutzer und die Gruppe sein, unter der \*Arr konfiguriert ist.
1. Starten Sie die Anwendung.

Bitte beachten Sie, dass das GIF den Befehl `VACUUM;` nicht abdeckt.

![dbrecover.gif](/dbrecover.gif)

## Wiederherstellung der Datenbank über die Befehlszeile

{#nix}

Die folgenden Anweisungen gelten für \*Nix-Betriebssysteme, das Konzept ist jedoch auf der Windows-Befehlszeile ähnlich.

> Hierbei wird der Befehl [sqlite3 `.recover`](https://www.sqlite.org/cli.html#recover_data_from_a_corrupted_database) verwendet. Beachten Sie, dass Sqlite 3.29+ erforderlich ist. {.is-info}

> Da sqlite3 von \*Arrs benötigt wird, wird davon ausgegangen, dass Sie sqlite3 auf Ihrem System installiert haben. {.is-info}

1. Stoppen Sie die Anwendung.
1. Greifen Sie über SSH auf Ihren Server zu oder öffnen Sie anderweitig eine Shell.
1. Geben Sie `sqlite3 <Pfad zur beschädigten Datenbank> ".recover" | sqlite3 <Ausgabepfad für die wiederhergestellte Datenbank>` ein.
1. Korrigieren Sie die Berechtigungen für die wiederhergestellte Datenbank, falls erforderlich. Der Besitzer sollte der Benutzer und die Gruppe sein, unter der \*Arr konfiguriert ist.
1. Entfernen Sie die alte beschädigte Datenbank sowie alle `wal`- oder `shm`-Dateien aus dem Ordner.
1. Benennen Sie die wiederhergestellte Datenbank um. Alle \*Arrs benennen ihre Datenbank als `<appname>.db`, z.B. `radarr.db`.
1. Starten Sie die Anwendung.

# Cookies finden

- Einige Websites können nicht automatisch eingeloggt werden und erfordern, dass Sie sich manuell anmelden und dann die Cookies weitergeben, um zu funktionieren. Die folgenden Seiten beschreiben, wie Sie dies tun können.

## Allgemeine Anweisungen

1. Melden Sie sich mit Ihrem Browser über die von Ihnen gewählte Site-Link-Adresse auf der Website an.
1. Öffnen Sie das DevTools-Fenster, indem Sie F12 drücken.
1. Wählen Sie den Netzwerk-Tab aus.
1. Klicken Sie auf die Schaltfläche "Doc" (Chrome-Browser) oder "HTML" (Firefox-Browser).
1. Aktualisieren Sie die Seite, indem Sie F5 drücken.
1. Klicken Sie auf den ersten Eintrag in der Liste.
1. Wählen Sie den Tab "Headers" im rechten Bereich aus.
1. Suchen Sie nach "cookie:" im Abschnitt "Request Headers". Beachten Sie den Hilfetext in der Benutzeroberfläche Ihres Trackers für weitere Details.
1. Markieren und kopieren Sie den gesamten Cookie-String (alles nach "cookie:").
1. Löschen Sie alles, was sich bereits im Cookie-Feld der Prowlarr-Indexer-Konfiguration befindet.
1. Fügen Sie den kopierten Cookie-String in dieses Feld ein.
1. Klicken Sie auf "Speichern".

> Wenn der User-Agent für Ihren Tracker erforderlich ist, finden Sie ihn in den Request Headers. {.is-info}

### Hinweise

- Stellen Sie sicher, dass Sie den Browser vom selben Gerät aus verwenden, auf dem Prowlarr ausgeführt wird, da Cookies selten von anderen Plattformen aus funktionieren.
- Auf der Login-Seite der Website aktivieren Sie keine Optionen, die Ihre Sitzung auf eine IP-Adresse beschränken oder nach kurzer Zeit abmelden. Wenn es eine Option "Remember me" gibt, verwenden Sie sie.
- Stellen Sie sicher, dass Sie vor dem Abrufen des Cookies auf die Torrent-Suchseite der Website zugreifen können. Alles, was die Website daran hindert (Warnungen, ungelesene Hinweise oder ungelesene PMs oder eine niedrige Ratio-Warnung), wird Prowlarr daran hindern, nach Verwendung des Cookies einen erfolgreichen Test durchzuführen.

## Chrome

- Gehen Sie zur Website des Torrent-Trackers und melden Sie sich an.

- Drücken Sie F12.

- Unter dem Tab "Anwendung" oben gibt es auf der linken Seite "Speicher". Dort sehen Sie einen Abschnitt "Cookies" und darunter die URL Ihres Trackers. Klicken Sie darauf.

- Klicken Sie auf "Pass" auf diesem Tab oder einem ähnlichen Eintrag, und es wird ein Feld mit der Aufschrift "Cookie-Wert" und einem etwa 25-30 Zeichen langen String angezeigt. Kopieren Sie dies und fügen Sie es in die Anwendung ein, die es benötigt.

  - Wenn der String ähnlich aussieht wie `cid=cid-that-you-got-from-the-browser; sid=sid-that-you-got-from-the-browser`, sollte der gesamte Eintrag verwendet werden.

![cookie_chrome.png](/assets/prowlarr/cookie_chrome.png)

- Sie können auch die Chrome-Dokumentation [Chrome-Cookies](https://developer.chrome.com/docs/devtools/storage/cookies/) konsultieren.

## Firefox

- [Bitte sehen Sie sich die Dokumentation von Mozilla an](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector/Cookies)

![faq_3_cookies.png](/assets/general/faq_3_cookies.png)

# Cookies und lokalen Speicher löschen

## Chrome

1. Navigieren Sie zu `chrome://settings/siteData`.
1. Geben Sie den Namen der Website (oder App) ein, die Sie löschen möchten.
1. Klicken Sie auf das Papierkorb-Symbol für die Website.

## Firefox

- Bitte lesen Sie den [Hilfeartikel von Mozilla](https://support.mozilla.org/en-US/kb/clear-cookies-and-site-data-firefox).

## Microsoft Edge (Chromium)

1. Navigieren Sie zu `edge://settings/siteData`.
1. Geben Sie den Namen der Website (oder App) ein, die Sie löschen möchten.
1. Klicken Sie auf den Pfeil für die Website.
1. Klicken Sie auf das Papierkorb-Symbol für die Website.

# Andere Projekte und Programme - Anwendungen für Anfragen (\*Arrs)

## Notifiarr (fka Discord Notifier)

[Notifiarr](https://notifiarr.com/) ist ein von einem der \*Arr-Entwickler erstelltes Tool, das detailliertere Discord-Benachrichtigungen ermöglicht. Es bietet eine konfigurierbare Möglichkeit, Benachrichtigungen (einschließlich Reaktionen) basierend auf ausgewählten Auslösern hinzuzufügen. Die Website bietet eine Benutzeroberfläche zum Auswählen dessen, was in der Benachrichtigung angezeigt werden soll. Es unterstützt Benachrichtigungen für Grab, Import, Upgrade, Health und Failed sowie vieles mehr.

[Wiki](https://notifiarr.wiki/)

Highlights

- Anwendungsstatus
- Anfragen und Genehmigungen (\~Ombi)
- Anpassbare Benachrichtigungen für \*ARR-Anwendungen
- Anfragesystem mit Genehmigungen
- Folgesystem für Benutzer zur Überwachung einer Serie oder eines Films und Benachrichtigung (über @mentions)
- Serverstatus
- Häufige neue Funktionen

## Ombi

[Ombi](https://github.com/tidusjar/Ombi/) ermöglicht Benutzern das Anfordern von Filmen, TV-Serien (Staffeln oder einzelnen Episoden) und Musikalben.

## Overseerr

[Overseerr](https://overseerr.dev/) ist ein Anforderungsverwaltungs- und Medienentdeckungstool, das mit Ihrer vorhandenen Plex-Umgebung zusammenarbeitet.

## Petio

[Petio](https://petio.tv/) ist eine Drittanbieter-Begleit-App, die Plex-Serverbesitzern zur Verfügung steht, um es ihren Benutzern zu ermöglichen, Inhalte anzufordern, zu überprüfen und zu entdecken.

Die App ist so konzipiert, dass sie sofort vertraut und intuitiv erscheint, selbst für Benutzer, die technisch nicht versiert sind. Petio hilft Ihnen dabei, Anfragen von Ihren Benutzern zu verwalten, sich mit anderen Drittanbieter-Apps wie Sonarr und Radarr zu verbinden, Benutzer zu benachrichtigen, wenn Inhalte verfügbar sind, und den Fortschritt der Anfragen zu verfolgen. Petio ermöglicht es Benutzern auch, Medien auf Ihrem Server und außerhalb schnell und einfach zu entdecken, verwandte Inhalte zu finden und Bewertungen abzugeben, um ihre Meinung für andere Benutzer zu hinterlassen.

# Andere Projekte und Programme - \*Arr-bezogen

## Fernsteuerung

### LunaSea

[LunaSea](https://www.lunasea.app/) ist ein voll ausgestatteter, Open-Source-Controller, der sich selbst hostet! Es konzentriert sich darauf, Ihnen ein nahtloses Erlebnis zwischen all Ihren selbst gehosteten Mediensoftware zu bieten.

### Radarr & Sonarr Companion - Android App

Fügen Sie mit Ihrem Telefon ganz einfach neue Filme/Serien zu Ihrem System hinzu. App verfügbar im [Google Play Store](https://play.google.com/store/apps/details?id=easy.radarr)

### nzb360 - Android App

nzb360 ermöglicht die Verwaltung von Sonarr, Radarr, Lidarr, Torrents, Usenet und anderen Diensten. App verfügbar im [Google Play Store](https://play.google.com/store/apps/details?id=com.kevinforeman.nzb360). Weitere Informationen finden Sie auf der [offiziellen Website](https://nzb360.com/).

## Lidarr

### AMD

[Automated Music Downloader](https://github.com/RandomNinjaAtk/docker-amd) RandomNinjaAtk/amd ist ein Lidarr-Begleitskript zum automatischen Herunterladen von Musik für Lidarr.

### AMVD

[Automated Music Video Downloader](https://github.com/RandomNinjaAtk/docker-amvd) RandomNinjaAtk/amvd ist ein Lidarr-Begleitskript zum automatischen Herunterladen und Taggen von Musikvideos für die Verwendung in anderen Videoanwendungen (Plex/Kodi/Jellyfin/Emby).

## Radarr

## AMTD

[Automated Movie Trailer Downloader](https://github.com/RandomNinjaAtk/docker-amtd) RandomNinjaAtk/amtd ist ein Radarr-Begleitskript zum automatischen Herunterladen von Filmtrailern und Extras für die Verwendung in anderen Videoanwendungen (Plex/Kodi/Jellyfin/Emby).

## Untertitel

## Bazarr

[Bazarr](https://github.com/morpheus65535/bazarr) ist eine Begleitanwendung für Sonarr und Radarr, die Untertitel basierend auf Ihren Anforderungen verwaltet und herunterlädt.

# Andere Projekte und Programme - Torrents/Herunterladen

## Cross-Seed

[Cross-Seed](https://github.com/mmgoodnow/cross-seed) ist eine App, die Ihnen hilft, Torrents herunterzuladen, die Sie basierend auf Ihren vorhandenen Torrents überkreuzen können. Sie ist so konzipiert, dass sie konservativ abgleicht, um manuelle Eingriffe zu minimieren. Sie unterstützt derzeit Jackett und Qbittorrent/rTorrent.

## Toolbarr

[Toolbarr](https://github.com/Notifiarr/toolbarr) bietet eine Reihe von Dienstprogrammen zur Behebung von Problemen mit Starr-Anwendungen. Mit Toolbarr können Sie verschiedene Aktionen gegen Ihre Starr-Anwendungen und deren SQLite3-Datenbanken durchführen.

## Unpackerr

[Unpackerr](https://github.com/unpackerr/unpackerr) Diese Anwendung läuft als Daemon auf Ihrem Download-Host. Sie überprüft abgeschlossene Downloads und entpackt sie, damit \*Arr sie importieren kann.

Es gibt eine Handvoll Optionen zum Extrahieren und Löschen von Dateien, nachdem Ihr Client sie heruntergeladen hat. Captain mochte jedoch keine von ihnen, also hat er seine eigene geschrieben. Er wollte eine kleine Einzelbinary mit vernünftigem Logging, die heruntergeladene Archive extrahieren und den Chaos nach dem Import aufräumen kann.

## qBit Management

[qBit Management, auch bekannt als "qbit_manage"](https://github.com/StuffAnThings/qbit_manage), ist ein Programm zur Verwaltung Ihrer qBittorrent-Instanz, z.B.:



- Markiere Torrents basierend auf der Tracker-URL (markiere nur Torrents, die keine Tags haben)
- Aktualisiere Kategorien basierend auf dem Speicherverzeichnis
- Entferne nicht registrierte Torrents (lösche Daten und Torrent, wenn sie nicht cross-seeded werden, sonst wird nur der Torrent entfernt)
- Füge automatisch Cross-Seed-Torrents im pausierten Zustand hinzu (in Verbindung mit dem [Cross-Seed-Skript](#cross-seed) verwendet)
- Überprüfe pausierte Torrents, sortiert nach geringster Größe, und setze sie fort, wenn sie abgeschlossen sind
- Entferne verwaiste Dateien aus deinem Stammverzeichnis, die von qBittorrent nicht referenziert werden
- Markiere Torrents, die keine Hardlinks haben, und ermögliche optional die Bereinigung, um diese Torrents und Inhalte basierend auf dem maximalen Verhältnis und/oder der Zeit, in der sie gesät wurden, zu löschen

# Andere Projekte und Programme

## Filebot

[FileBot](https://www.filebot.net/) ist das ultimative Werkzeug zur Organisation und Umbenennung von Filmen, TV-Serien und Anime sowie zum Abrufen von Untertiteln und Artwork. Es ist intelligent und funktioniert einfach.

## JDupes

[Jdupes](https://github.com/jbruchon/jdupes) ist ein Programm zur Identifizierung und Durchführung von Aktionen bei doppelten Dateien.

> TRaSH [hat einen Leitfaden](https://trash-guides.info/jdupes) dazu {.is-info}

- `jdupes -M -r "/data/tv/" "/data/tv/.torrents/"` <= damit werden doppelte Dateien überprüft und eine Zusammenfassung der Ergebnisse angezeigt

- `jdupes -L -r "/data/tv/" "/data/tv/.torrents/"` <= damit werden sie als Hardlinks neu erstellt und der verwendete doppelte Speicherplatz reduziert

## Just A Bunch Of Starr Scripts

- [Just A Bunch Of Starr Scripts](https://github.com/angrycuban13/Just-A-Bunch-Of-Starr-Scripts)
- [Upgradinatorr](https://github.com/angrycuban13/Scripts/blob/main/Upgradinatorr/README.md) ist ein PowerShell-Skript zum manuellen Suchen von n Elementen, die in deiner Radarr/Sonarr-Medienbibliothek nicht mit einem bestimmten Tag versehen sind. n ist die Anzahl der Elemente, nach denen dieses Skript suchen wird. Dadurch wird vermieden, dass deine Indexer überlastet werden und du gesperrt wirst :)

## Just A Bunch Of Plex Scripts

- [Just A Bunch Of Plex Scripts (JBOPS)](https://github.com/blacktwin/JBOPS)
- [TRaSH Guides JBOPS 4K Transcode Stopping with Tautulli](https://trash-guides.info/Plex/Tips/4k-transcoding/)

## Plex Meta Manager

[Plex Meta Manager (PMM)](https://github.com/meisnate12/Plex-Meta-Manager) ist ein Python-Skript zur Aktualisierung von Metadaten für Filme, Serien und Sammlungen sowie zum automatischen Erstellen von Sammlungen.

## Tautulli

[Tautulli](https://tautulli.com/) ist eine Anwendung von Drittanbietern, die du neben deinem Plex Media Server ausführen kannst, um Aktivitäten zu überwachen und verschiedene Statistiken zu verfolgen. Diese Statistiken umfassen vor allem, was angesehen wurde, wer es angesehen hat, wann und wo es angesehen wurde und wie es angesehen wurde. Das Einzige, was fehlt, ist "warum es angesehen wurde", aber wer bin ich, um deine 42 Wiedergaben von "Frozen" zu hinterfragen. Alle Statistiken werden in einer übersichtlichen Benutzeroberfläche mit vielen Tabellen und Diagrammen präsentiert, sodass du leicht mit anderen über deinen Server prahlen kannst.

## Tdarr

[Tdarr](https://tdarr.io) ist eine Closed-Source-Webanwendung zur Automatisierung der Verwaltung von Transcode/Remux in deiner Medienbibliothek und stellt sicher, dass deine Dateien genau so sind, wie du sie benötigst, in Bezug auf Codecs/Streams/Container usw. Es wurde entwickelt, um mit [Sonarr](/sonarr)/[Radarr](/radarr) zusammenzuarbeiten und basiert auf Modularisierung, Parallelisierung und Skalierbarkeit. Jede hinzugefügte Bibliothek hat ihre eigenen Transcode-Einstellungen, Filter und Zeitpläne. Die Worker können bei Bedarf gestartet und beendet werden und sind in 3 Typen unterteilt: 'allgemein', 'Transcode' und 'Gesundheitsprüfung'. Die Worker-Limits können sowohl vom Scheduler als auch manuell verwaltet werden.

## tdarr_inform

[tdarr_inform](https://github.com/deathbybandaid/tdarr_inform) ist ein benutzerdefiniertes Skript für Sonarr und Radarr, um Tdarr über neue/geänderte/gelöschte Dateien zu informieren, ohne auf Dateisystemereignisse oder häufiges Scannen der Festplatte angewiesen zu sein.

## Deleterr

[Deleterr](https://github.com/rfsbraz/deleterr) ist ein Tool zum Löschen von veralteten und inaktiven Medien aus Plex/Sonarr/Radarr. Es hilft dabei, begrenzten Speicherplatz zu verwalten, wenn du Benutzern erlaubst, Shows über Overseerr/Ombi anzufordern, aber nicht manuell den verfügbaren Festplattenspeicher überwachen möchtest. Es ist konfigurierbar, um nur Medien zu löschen, die deinen definierten Kriterien entsprechen.

## Twitter Connect

Erstelle eine Twitter-Anwendung (falls noch nicht geschehen) unter <https://apps.twitter.com/>

Fülle die obligatorischen Felder sowie die Callback-URL aus. Setze sie auf eine öffentlich verfügbare URL (nicht localhost). Sie muss nicht existieren, aber sie muss gesetzt sein. Die Verwendung von <https://sonarr.tv/twitter> oder <https://radarr.video> ist ausreichend.