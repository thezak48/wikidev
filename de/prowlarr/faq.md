---
title: Prowlarr FAQ
description: Prowlarr FAQ
published: true
date: 2023-08-28T19:29:30.585Z
tags: prowlarr, faq
editor: markdown
dateCreated: 2021-11-03T03:01:18.079Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
  - [Erzwungene Authentifizierung](#erzwungene-authentifizierung)
  - [Wie setze ich Statistiken zurück?](#wie-setze-ich-statistiken-zurück)
  - [Kategorie nicht verfügbar oder fehlt](#kategorie-nicht-verfügbar-oder-fehlt)
  - [Kann ich einen beliebigen (generischen) Torznab- oder Newznab-Indexer hinzufügen?](#kann-ich-einen-beliebigen-generischen-torznab-oder-newznab-indexer-hinzufügen)
  - [Kann ich einen beliebigen (generischen) Torrent-RSS-Feed hinzufügen?](#kann-ich-einen-beliebigen-generischen-torrent-rss-feed-hinzufügen)
  - [Kann ich flaresolverr-Indexer verwenden?](#kann-ich-flaresolverr-indexer-verwenden)
  - [Wie füge ich einen Indexer hinzu, der nicht funktioniert oder nicht verfügbar ist?](#wie-füge-ich-einen-indexer-hinzu-der-nicht-funktioniert-oder-nicht-verfügbar-ist)
  - [Prowlarr synchronisiert nicht mit Sonarr](#prowlarr-synchronisiert-nicht-mit-sonarr)
  - [Prowlarr synchronisiert Indexer nicht mit der App](#prowlarr-synchronisiert-indexer-nicht-mit-der-app)
  - [Welche \*Arr-Indexer-Einstellungen werden für die vollständige App-Synchronisierung verglichen?](#welche-arr-indexer-einstellungen-werden-für-die-vollständige-app-synchronisierung-verglichen)
  - [Wie aktualisiere ich Prowlarr?](#wie-aktualisiere-ich-prowlarr)
    - [Kann ich Prowlarr innerhalb meines Docker-Containers aktualisieren?](#kann-ich-prowlarr-innerhalb-meines-docker-containers-aktualisieren)
    - [Installation einer neueren Version](#installation-einer-neueren-version)
      - [Native](#native)
      - [Docker](#docker)
  - [Kann ich von `nightly` zu `develop` wechseln?](#kann-ich-von-nightly-zu-develop-wechseln)
  - [Kann ich zwischen Branches wechseln?](#kann-ich-zwischen-branches-wechseln)
  - [Hilfe, mein Mac sagt, dass Prowlarr nicht geöffnet werden kann, weil der Entwickler nicht verifiziert werden kann](#hilfe-mein-mac-sagt-dass-prowlarr-nicht-geöffnet-werden-kann-weil-der-entwickler-nicht-verifiziert-werden-kann)
  - [Hilfe, mein Mac sagt, dass Prowlarr.app beschädigt ist und nicht geöffnet werden kann](#hilfe-mein-mac-sagt-dass-prowlarrapp-beschädigt-ist-und-nicht-geöffnet-werden-kann)
  - [Wie kann ich eine Funktion für Prowlarr anfordern?](#wie-kann-ich-eine-funktion-für-prowlarr-anfordern)
  - [Ich erhalte einen Fehler: Datenbank-Disk-Image ist beschädigt](#ich-erhalte-einen-fehler-datenbank-disk-image-ist-beschädigt)
  - [Ich verwende Prowlarr auf einem Mac und es funktioniert plötzlich nicht mehr. Was ist passiert?](#ich-verwende-prowlarr-auf-einem-mac-und-es-funktioniert-plötzlich-nicht-mehr-was-ist-passiert)
  - [Wie wechsle ich vom Windows-Dienst zu einer Tray-App?](#wie-wechsle-ich-vom-windows-dienst-zu-einer-tray-app)
  - [Wie sichere/verwende ich Prowlarr wiederherstellen?](#wie-sichereverwende-ich-prowlarr-wiederherstellen)
    - [Sichern von Prowlarr](#sichern-von-prowlarr)
      - [Verwendung der integrierten Sicherung](#verwendung-der-integrierten-sicherung)
      - [Verwendung des Dateisystems direkt](#verwendung-des-dateisystems-direkt)
    - [Wiederherstellen aus der Sicherung](#wiederherstellen-aus-der-sicherung)
      - [Verwendung der ZIP-Sicherung](#verwendung-der-zip-sicherung)
      - [Verwendung der Dateisystem-Sicherung](#verwendung-der-dateisystem-sicherung)
      - [Wiederherstellung des Dateisystems auf Synology NAS](#wiederherstellung-des-dateisystems-auf-synology-nas)
  - [WebUI lädt nur lokal auf Windows](#webui-lädt-nur-lokal-auf-windows)
  - [Cookies finden](#cookies-finden)
  - [uTorrent funktioniert nicht mehr](#utorrent-funktioniert-nicht-mehr)
  - [Ich habe einen Pop-up erhalten, dass config.xml beschädigt ist, was nun?](#ich-habe-einen-pop-up-erhalten-dass-configxml-beschädigt-ist-was-nun)
  - [Ungültiges Zertifikat und andere HTTPS- oder SSL-Probleme](#ungültiges-zertifikat-und-andere-https-oder-ssl-probleme)
  - [Hilfe, ich habe mich ausgesperrt](#hilfe-ich-habe-mich-ausgesperrt)
  - [Seltsame UI-Probleme](#seltsame-ui-probleme)
  - [VPNs, Prowlarr und die \*ARRs](#vpns-prowlarr-und-die-arrs)
  - [Wie verhindere ich, dass der Browser beim Start geöffnet wird?](#wie-verhindere-ich-dass-der-browser-beim-start-geöffnet-wird)
  - [Kann ich alle Indexer auf einmal hinzufügen?](#kann-ich-alle-indexer-auf-einmal-hinzufügen)

## Erzwungene Authentifizierung

Wenn Prowlarr so konfiguriert ist, dass die Benutzeroberfläche von außerhalb Ihres lokalen Netzwerks aus zugänglich ist, sollten Sie eine Form der Authentifizierung aktiviert haben, um auf die Benutzeroberfläche zugreifen zu können. Dies wird auch von Trackern und Indexern zunehmend gefordert.

Ab Prowlarr v1 ist die Authentifizierung obligatorisch.

### Authentifizierungsmethode

- `Basic` (Browser-Popup) - Diese Option zeigt beim Zugriff auf Prowlarr ein kleines Popup an, in dem Sie einen Benutzernamen und ein Passwort eingeben können.
- `Forms` (Anmeldeseite) - Diese Option zeigt eine vertraut aussehende Anmeldeseite an, ähnlich wie bei anderen Websites, auf der Sie sich bei Prowlarr anmelden können.
- `External` - Nur über Konfigurationsdatei konfigurierbar
  - Wenn Sie eine **externe Authentifizierung** wie Authelia, Authetik, NGINX Basic Auth usw. verwenden, können Sie eine doppelte Authentifizierung verhindern, indem Sie die App herunterfahren, `<AuthenticationMethod>External</AuthenticationMethod>` in der [Konfigurationsdatei](/prowlarr/appdata-directory) festlegen und die App neu starten. **Beachten Sie, dass mehrere `AuthenticationMethod`-Einträge in der Datei nicht unterstützt werden und nur der oberste Wert verwendet wird**.

### Erforderliche Authentifizierung

- Wenn Sie die App nicht extern freigeben und/oder keine Authentifizierung für den lokalen (z. B. LAN-) Zugriff wünschen, ändern Sie in Einstellungen => Allgemeine Sicherheit => Erforderliche Authentifizierung auf `Deaktiviert für lokale Adressen`.
  - Das Konfigurationsdatei-Äquivalent dazu lautet `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`.

## Wie setze ich Statistiken zurück?

- Um Ihre Statistiken zurückzusetzen und den Verlauf zu löschen, gehen Sie wie folgt vor:

1. Verlauf => Optionen
1. Setzen Sie die Verlaufsbereinigung auf `1`. Dadurch wird nur der Verlauf bis gestern und die Statistiken beibehalten.
1. Navigieren Sie zu System => Aufgaben
1. Führen Sie die Aufgabe "Verlauf bereinigen" aus
1. Führen Sie die Aufgabe "Hausputz" aus
1. Gehen Sie zurück zu Verlauf => Optionen
1. Legen Sie die Verlaufsbereinigung auf die gewünschte Aufbewahrungsfrist für Verlauf und Statistiken fest.

## Kategorie nicht verfügbar oder fehlt

- Bitte beachten Sie, dass benutzerdefinierte/nicht standardmäßige Indexer-spezifische Kategorien auf Standardkategorien abgebildet werden, sodass bei der Suche alle benutzerdefinierten Kategorien berücksichtigt werden. Überprüfen Sie die Definition der Kategoriezuordnung Ihres spezifischen Indexers für weitere Details.

## Kann ich einen beliebigen (generischen) Torrent-RSS-Feed hinzufügen?

Ja. Verwenden Sie "TorrentRSS".

Die folgenden Attribute sind obligatorisch:

- guid
- title
- infohash
- enclosure oder link

Die folgenden Attribute sind optional, aber empfohlen:

- size
- pubDate

## Kann ich einen beliebigen (generischen) Torznab- oder Newznab-Indexer hinzufügen?

- Ja.
- Gehen Sie zu `Indexers` => `Indexer hinzufügen` (<kb>+</kb>) => `Generischer Torznab` oder `Generischer Newznab`

## Kann ich flaresolverr-Indexer verwenden?

- Ja.

1. Konfigurieren Sie Ihre flaresolverr-Instanz, indem Sie sie als Proxy in [Einstellungen => Indexer](/prowlarr/settings#indexer-proxies) hinzufügen.
1. Fügen Sie dem erstellten flaresovlerr-Proxy einen Tag hinzu.
1. Fügen Sie dem [Indexer](/prowlarr/indexers) denselben Tag hinzu.

> Die Tags müssen übereinstimmen und Cloudflare muss erkannt werden, damit Flaresolverr verwendet wird. Ein Flaresolverr-Proxy ist deaktiviert, wenn keine Tags verwendet werden.
{.is-warning}

> [Siehe TRaSH's Guides zu "Wie man Flaresolverr einrichtet"](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/) für weitere Details.
{.is-info}

## Wie füge ich einen Indexer hinzu, der nicht funktioniert oder nicht verfügbar ist?

- Befolgen Sie die Standard-Schritte zum Hinzufügen des Indexers und beachten Sie dabei die folgenden Änderungen.
- Deaktivieren Sie das Kontrollkästchen (Deaktivieren) "Aktiviert"
- Klicken Sie auf "Speichern"
- Klicken Sie erneut auf "Speichern", um eine erzwungene Speicherung auszulösen
- Bearbeiten Sie den Indexer (Schraubenschlüssel-Symbol)
- Aktivieren Sie das Kontrollkästchen (Aktivieren) "Aktiviert"
- Klicken Sie auf "Speichern"
- Klicken Sie erneut auf "Speichern", um eine erzwungene Speicherung auszulösen

## Prowlarr synchronisiert nicht mit Sonarr

- Prowlarr unterstützt nur Sonarr v3+
- Sonarr v2 (ehemals nzbdrone) wird von Prowlarr nicht unterstützt und ist allgemein nicht mehr unterstützt und wurde seit März 2021 eingestellt.

## Prowlarr synchronisiert Indexer nicht mit der App

- Prowlarr synchronisiert nur, wenn "Hinzufügen und Entfernen" oder "Vollständige Synchronisierung" für die App aktiviert ist.
- Nur in Fällen, in denen eine App und ein Indexer übereinstimmende Tags oder gar keine Tags haben, wird ein Indexer mit einer App synchronisiert.
- Indexer werden basierend auf den von ihnen behaupteten Fähigkeiten/Kategorien synchronisiert.
  - Wenn ein Indexer nur TV-Kategorien unterstützt, wird er nicht mit Lidarr, Radarr und Readarr synchronisiert.
- Ein bestimmter Indexer wird nur mit Sonarr synchronisiert, wenn "Unterstützte" Kategorien als erweiterte Einstellung pro App ausgewählt werden können.
- Indexer werden nicht synchronisiert, wenn die spezifischen Kategorien, die vom Indexer unterstützt werden, nicht in Einstellungen => Anwendung => {App} => Synchronisierte Kategorien (erweiterte Einstellungen) ausgewählt sind, und in den Protokollen wird keine Anzeige eines Synchronisierungsversuchs angezeigt.
- Die häufigste Ursache dafür ist, dass die \*Arrs nur Indexer akzeptieren, deren Testabfragen Ergebnisse enthalten, die mindestens eine der konfigurierten Kategorien enthalten. Mit anderen Worten, wenn Sie eine App synchronisieren und die leere Abfrage Ihres Indexers keine Ergebnisse mit einer Veröffentlichung in den für die App konfigurierten Kategorien zurückgibt, kann der Indexer nicht zu \*Arr hinzugefügt werden.
- Der spezifische Fehler wird ein HTTP 400 von \*Arr mit der Meldung `Query successful, but no results in the configured categories were returned from your indexer. This may be an issue with the indexer or your indexer category settings.` sein.
  - Möglicherweise kann dieser Indexer einfach nicht mit dieser \*Arr verwendet werden. Dies ist häufig der Fall, wenn versucht wird, öffentliche Tracker oder Usenet-Indexer mit Readarr und Lidarr zu verwenden.
  - Passen Sie die in den erweiterten Einstellungen für die \*Arr-Anwendung in Prowlarr synchronisierten Kategorien an.
    - Beachten Sie, dass bestimmte Tracker - hauptsächlich "schlechte" öffentliche Tracker - erfordern, dass Sie die Kategorie `8000 - Andere` auswählen und synchronisieren. Dies wird in der Regel - aber nicht immer - in den Tracker-Details in Prowlarr angegeben.
  - Versuchen Sie es später erneut.
  - Wenn das Problem weiterhin besteht, haben Sie möglicherweise eine beschädigte Datenbank. Überprüfen Sie Ihre Protokolle auf Vorkommnisse von `Database disk image is malformed` oder `Error creating main database`. Weitere mögliche Lösungen finden Sie in [diesem Abschnitt](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed).

## Welche \*Arr-Indexer-Einstellungen werden für die vollständige App-Synchronisierung verglichen?

- App/Prowlarr: Indexer-Name
- App/Prowlarr: RSS aktivieren/deaktivieren
- App/Prowlarr: Automatische Suche aktivieren/deaktivieren
- App/Prowlarr: Interaktive Suche aktivieren/deaktivieren
- App/Prowlarr: Indexer-Priorität
- App/Prowlarr: API-Schlüssel
- App/Prowlarr: URL
- App/Prowlarr: Basis-URL
- App/Prowlarr: Port
- App/Prowlarr: Kategorien
- App/Prowlarr: Seed-Verhältnis und Seed-Zeit
- App/Prowlarr: Mindestanzahl an Seedern
- App/Prowlarr: *Alle anderen in Prowlarr konfigurierbaren Einstellungen*
- Prowlarr: Implementierung (z. B. YML oder C#)

Mit aktivierter vollständiger Synchronisierung wird der Indexer in \*Arr synchronisiert und aktualisiert, wenn sich einer der oben genannten Punkte zwischen der \*Arr-App und Prowlarr ändert.

## Wie aktualisiere ich Prowlarr?

- Gehen Sie zu Einstellungen und dann zum Tab Allgemein und zeigen Sie erweiterte Einstellungen an (verwenden Sie den Umschalter neben der Speichern-Schaltfläche).

1. Ändern Sie im Abschnitt Updates den Branch-Namen in `master`, `develop` oder `nightly`.
1. Speichern Sie.

*Dies installiert die Bits aus diesem Branch nicht sofort, sondern erfolgt während des nächsten Updates.*

- `master` - ![Aktueller Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    (Standard/Stabil): Es wurde von Benutzern auf den Entwicklungs- und Nightly-Branches getestet und es sind keine größeren Probleme bekannt. Auf GitHub handelt es sich um den `master`-Branch.

- `develop` - ![Aktueller Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  (Beta): Dies ist der Test-Edge. Nachdem es in Nightly getestet wurde, um sofortige Probleme auszuschließen, wird es hier zuerst neue Funktionen und Fehlerkorrekturen veröffentlicht. Es kann als halbstabil angesehen werden, ist aber immer noch `beta`.

> Auf GitHub handelt es sich um einen Schnappschuss des `develop`-Branchs zu einem bestimmten Zeitpunkt.
{.is-warning}

- `nightly` - ![Aktueller Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  (Alpha/Unstable): Dies ist die bleeding edge. Es wird veröffentlicht, sobald der Code übernommen und alle automatisierten Tests bestanden wurden. Diese Version wurde möglicherweise noch nicht von uns oder anderen Benutzern verwendet. Es besteht keine Garantie, dass es in einigen Fällen überhaupt ausgeführt wird. Dieser Branch wird nur fortgeschrittenen Benutzern empfohlen. Probleme und Selbstuntersuchungen werden in diesem Branch erwartet. ***Verwenden Sie diesen Branch nur, wenn Sie wissen, was Sie tun, und bereit sind, bei einem fehlgeschlagenen Update selbst Hand anzulegen.*** Diese Version wird sofort aktualisiert.

> **Warnung: Möglicherweise können Sie nach dem Wechsel zu diesem Branch nicht mehr zu `develop` zurückkehren.** Auf GitHub handelt es sich um den `develop`-Branch.
{.is-danger}

- Hinweis: Wenn Ihre Installation über Docker erfolgt, fügen Sie Ihrem Container-Tag je nach Hersteller der Builds `:latest`, `:testing`, `:develop` oder `:nightly` hinzu.



|                                                                      | `master` (stabil) ![Aktueller Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Aktueller Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (unstabil) ![Aktueller Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### Kann ich Prowlarr in meinem Docker-Container aktualisieren?

- *Technisch gesehen ja.* **Aber du solltest es auf keinen Fall tun.** Das ist ein grundlegendes Prinzip von Docker. Es können Probleme mit der Datenbank auftreten, wenn du deine Installation auf die neueste `nightly` aktualisierst und dann den Docker-Container selbst aktualisierst (möglicherweise auf eine ältere Version zurückgehend).

### Installation einer neueren Version

#### Nativ

1. Gehe zu System und dann zum Tab Updates.
1. Neuere Versionen, die noch nicht installiert sind, haben einen Update-Button neben sich. Wenn du auf diesen Button klickst, wird das Update installiert.

#### Docker

1. Ziehe dein Tag erneut und aktualisiere deinen Container.

## Kann ich von `nightly` zu `develop` wechseln?

## Kann ich zwischen Branches wechseln?

- Wenn die Version identisch ist, kannst du wechseln. Andernfalls prüfe beim Entwicklungsteam nach, ob du von `nightly` zu `develop` wechseln kannst oder umgekehrt für deine spezifische Version.
- Wenn du diese Anweisungen nicht befolgst, kann dein Prowlarr unbrauchbar werden oder Fehler verursachen. Du wurdest gewarnt.
  - Die häufigsten Fehler sind Datenbankfehler, die fehlende Spalten oder Tabellen betreffen.

## Hilfe, mein Mac sagt, dass Prowlarr nicht geöffnet werden kann, weil der Entwickler nicht verifiziert werden kann

- Das ist einfach, bitte siehe diesen Link für weitere Informationen [hier](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
- Alternativ musst du Prowlarr selbst signieren: `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## Hilfe, mein Mac sagt, dass Prowlarr.app beschädigt ist und nicht geöffnet werden kann

Das liegt entweder an einem beschädigten Download (also versuche es erneut) oder an den oben genannten Sicherheitsproblemen.

## Wie kann ich eine Funktion für Prowlarr anfordern?

Um eine Funktion für Prowlarr anzufordern, suche zuerst auf GitHub, um sicherzustellen, dass keine ähnliche Anfrage vorhanden ist, und klicke dann [hier](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=), um deine Anfrage hinzuzufügen.

## Ich erhalte einen Fehler: Datenbank-Disk-Image ist beschädigt

- **Fehler wie `Error creating log database` deuten auf Probleme mit logs.db hin**
  - Dies kann schnell behoben werden, indem du die Datenbank umbenennst oder entfernst. Die Protokolldatenbank enthält unwichtige Informationen über den Befehlsverlauf und die Update-Installationshistorie sowie Info-, Warn- und Fehlermeldungen.
- **Fehler wie `Error creating main database` oder allgemeine `database disk image is malformed` ohne spezifizierte Datenbank deuten auf Probleme mit prowlarr.db hin**
  - Fahre mit den unten angegebenen Schritten fort.
- Das bedeutet, dass deine SQLite-Datenbank, die die meisten Informationen für Prowlarr speichert, beschädigt ist. Du hast die Möglichkeit, (eine) Sicherung(en) auszuprobieren, die vorhandene Datenbank wiederherzustellen, die Sicherung(en) wiederherzustellen oder im schlimmsten Fall mit einer neuen, frischen Datenbank neu zu beginnen.
- Dieser Fehler kann auftreten, wenn die Datenbankdatei vom Benutzer/der Benutzergruppe, unter der \*Arr ausgeführt wird, nicht beschreibbar ist. Berechtigungen sind wahrscheinlich nur ein Problem bei neuen Installationen, migrierten Installationen auf einen neuen Server, wenn du kürzlich die Berechtigungen deines Appdata-Verzeichnisses geändert hast oder wenn du den Benutzer und die Gruppe geändert hast, unter der \*Arr ausgeführt wird.
- Deine beste und erste Option ist, [versuche eine Wiederherstellung aus einer Sicherung](#wie-sichere-ich-mein-prowlarr).
- Du kannst auch versuchen, deine Datenbank wiederherzustellen. Dies ist in der Regel die einzige Option, wenn dieses Problem nach einem Update auftritt. Versuche den [sqlite3 `.recover` Befehl](/useful-tools#recovering-a-corrupt-db)
  - Wenn dein sqlite nicht über `.recover` verfügt oder du eine benutzerfreundlichere GUI (z. B. Windows) wünschst, folge [unseren Anweisungen in diesem Wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- Eine weitere mögliche Ursache für den Fehler mit deiner Datenbank ist, dass du deine Datenbank auf einem Netzlaufwerk (nfs oder smb oder etwas anderem, das nicht lokal ist) platzierst. **SQLite ist für Situationen ausgelegt, in denen Daten und Anwendung auf demselben Rechner vorhanden sind.** Daher muss dein \*Arr AppData-Ordner (/config mount für Docker) auf lokalem Speicher sein. [SQLite und Netzlaufwerke vertragen sich nicht und führen letztendlich zu einer beschädigten Datenbank](https://www.sqlite.org/draft/useovernet.html).
- Wenn du mergerFS verwendest, musst du `direct_io` entfernen, da SQLite mmap verwendet, was von `direct_io` nicht unterstützt wird, wie in der mergerFS [Dokumentation hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs) erklärt wird.

## Ich benutze Prowlarr auf einem Mac und es funktioniert plötzlich nicht mehr. Was ist passiert?

- Wahrscheinlich liegt das an einem MacOS-Bug, der dazu geführt hat, dass die Prowlarr-Datenbank beschädigt wurde. Bitte überprüfe den FAQ-Eintrag zur Wiederherstellung einer beschädigten Datenbank.

## Wie wechsle ich vom Windows-Dienst zu einer Tray-App?

- Schließe Prowlarr.
- Führe serviceuninstall.exe im Prowlarr-Verzeichnis aus.
- Führe Prowlarr.exe einmal als Administrator aus, um ihm die erforderlichen Berechtigungen zu geben und die Firewall zu öffnen. Sobald der Vorgang abgeschlossen ist, kannst du das Programm schließen und normal ausführen.
- (Optional) Erstelle eine Verknüpfung zu Prowlarr.exe im Autostart-Ordner, um es beim Start automatisch zu starten.

## Wie sichere/restore ich Prowlarr?

### Sichern von Prowlarr

#### Verwendung der integrierten Sicherung

- Gehe in der Prowlarr-Benutzeroberfläche zu System => Backup.
- Klicke auf den Backup-Button.
- Lade das Zip-Archiv nach der Erstellung der Sicherung herunter, um es sicher aufzubewahren.

#### Direkte Verwendung des Dateisystems

- Finde den Speicherort des AppData-Verzeichnisses für Prowlarr heraus
  - Gehe über die Prowlarr-Benutzeroberfläche zu System => About
  - [Prowlarr Appdata-Verzeichnis](/prowlarr/appdata-directory)
- Stoppe Prowlarr - Dadurch wird verhindert, dass die Datenbank beschädigt wird.
- Kopiere den Inhalt an einen sicheren Ort.

### Wiederherstellen aus einer Sicherung

> Das Wiederherstellen auf ein Betriebssystem mit unterschiedlichen Pfaden funktioniert nicht (Windows zu Linux, Linux zu Windows, Windows zu OS X oder OS X zu Windows). Der Wechsel zwischen OS X und Linux könnte funktionieren, da beide Pfade mit `/` anstelle von `\` arbeiten, wie es Windows tut, aber das wird nicht unterstützt. Du musst alle Pfade in der Datenbank manuell bearbeiten.
{.is-warning}

#### Verwendung der Zip-Sicherung

- Installiere Prowlarr erneut (falls zutreffend / noch nicht installiert).
- Starte Prowlarr.
- Navigiere zu System => Backup.
- Wähle Wiederherstellen aus.
- Wähle Datei auswählen.
- Wähle deine Backup-Zip-Datei aus.
- Wähle Wiederherstellen.

#### Verwendung der Dateisystem-Sicherung

- Installiere Prowlarr erneut (falls zutreffend / noch nicht installiert).
- Finde den Speicherort des AppData-Verzeichnisses für Prowlarr heraus
  - Führe Prowlarr einmal aus und gehe über die Benutzeroberfläche zu System => About
  - [Prowlarr Appdata-Verzeichnis](/prowlarr/appdata-directory)
- Stoppe Prowlarr.
- Lösche den Inhalt des AppData-Verzeichnisses **(einschließlich der .db-wal/.db-journal-Dateien, sofern vorhanden)**
- Stelle die Sicherung wieder her.
- Starte Prowlarr.
- Solange die Pfade gleich sind, wird alles dort fortgesetzt, wo es aufgehört hat.

#### Dateisystem-Wiederherstellung auf Synology NAS

> VORSICHT: Die Wiederherstellung auf einem Synology erfordert Kenntnisse in Linux und Root-SSH-Zugriff auf das Synology-Gerät.
{.is-warning}

- Installiere Prowlarr erneut (falls zutreffend / noch nicht installiert).
- Finde den Speicherort des AppData-Verzeichnisses für Prowlarr heraus
  - Führe Prowlarr einmal aus und gehe über die Benutzeroberfläche zu System => About
  - [Prowlarr Appdata-Verzeichnis](/prowlarr/appdata-directory)
- Stoppe Prowlarr.
- Verbinde dich über SSH mit dem Synology NAS und melde dich als Root an.

> Bei einigen Installationen ist der Benutzer anders als in den folgenden Befehlen: `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- Führe die folgenden Befehle aus:

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- Aktualisiere die Berechtigungen für die Dateien:

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Starte Prowlarr.

## Die WebUI lädt nur auf localhost unter Windows

Wenn du nur über `http://localhost:9696/` oder `http://127.0.0.1:9696` auf deine Web-Benutzeroberfläche zugreifen kannst, musst du Prowlarr mindestens einmal als Administrator ausführen, möglicherweise sogar immer.

## Cookies finden

Einige Websites können nicht automatisch eingeloggt werden und erfordern, dass du dich manuell einloggst und dann die Cookies an Prowlarr übergibst, damit es funktioniert. [Bitte siehe diesen Artikel für weitere Details.](/useful-tools#finding-cookies)

## uTorrent funktioniert nicht mehr

- Stelle sicher, dass die Web-Benutzeroberfläche aktiviert ist

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- Aktiviere die Web-Benutzeroberfläche

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Stelle sicher, dass der alternative Listening-Port (Advanced => Web UI) nicht mit dem Listening-Port (Connections) identisch ist. Wir empfehlen, den alternativen Listening-Port für die Web-Benutzeroberfläche zu ändern, um keine Probleme mit der Portweiterleitung für Verbindungen zu verursachen.

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## Ich habe eine Fehlermeldung erhalten, dass die Datei config.xml beschädigt ist. Was nun?

Prowlarr konnte Ihre Konfigurationsdatei beim Start nicht lesen, da sie aus irgendeinem Grund beschädigt wurde. Um Prowlarr wieder online zu bringen, müssen Sie die Datei `.xml` in Ihrem AppData-Ordner löschen. Starten Sie anschließend Prowlarr und es wird auf dem Standardport (9696) gestartet. Sie sollten nun alle Einstellungen neu konfigurieren, die Sie auf der Seite "Allgemeine Einstellungen" vorgenommen haben.

## Ungültiges Zertifikat und andere HTTPS- oder SSL-Probleme

Ihr Download-Client funktioniert nicht mehr und Sie erhalten einen Fehler wie "Localhost ist ein ungültiges Zertifikat"?

Prowlarr überprüft SSL-Zertifikate. Wenn im Download-Client kein SSL-Zertifikat festgelegt ist oder Sie ein selbstsigniertes HTTPS-Zertifikat verwenden, ohne das CA-Zertifikat zum lokalen Zertifikatsspeicher hinzugefügt zu haben, wird Prowlarr die Verbindung ablehnen. Kostenlose ordnungsgemäß signierte Zertifikate sind von Let's Encrypt erhältlich.

Wenn Ihr Download-Client und Prowlarr auf demselben Gerät sind, besteht kein Grund, HTTPS zu verwenden. Die einfachste Lösung besteht darin, SSL für die Verbindung zu deaktivieren. Die meisten würden zustimmen, dass es auch in einem lokalen Netzwerk nicht erforderlich ist. Es ist möglich, die Zertifikatsüberprüfung in den erweiterten Einstellungen zu deaktivieren, wenn Sie eine unsichere SSL-Konfiguration beibehalten möchten.

## Hilfe, ich habe mich ausgesperrt

{#help-i-have-forgotten-my-password}

Um die Authentifizierung zu deaktivieren (um Ihren vergessenen Benutzernamen oder Ihr Passwort zurückzusetzen), müssen Sie die Datei `config.xml` bearbeiten, die sich im [Prowlarr Appdata-Verzeichnis](/prowlarr/appdata-directory) befindet.

1. Öffnen Sie config.xml in einem Texteditor.
2. Suchen Sie die Zeile mit der Authentifizierungsmethode: `<AuthenticationMethod>Basic</AuthenticationMethod>` oder `<AuthenticationMethod>Forms</AuthenticationMethod>`.
3. Ändern Sie die Zeile `AuthenticationMethod` in `<AuthenticationMethod>None</AuthenticationMethod>`.
4. Starten Sie Prowlarr neu.
5. Prowlarr ist jetzt ohne Passwort zugänglich. Gehen Sie zur Registerkarte "Einstellungen: Allgemein" in der Benutzeroberfläche und legen Sie Ihren Benutzernamen und Ihr Passwort fest.

## Seltsame Probleme mit der Benutzeroberfläche

- Wenn Sie seltsame Probleme mit der Benutzeroberfläche haben oder eine bestimmte Ansicht oder Sortierung nicht funktioniert, versuchen Sie es in einem Chrome-Inkognito-Fenster oder einem Firefox-Privatfenster. Wenn es dort einwandfrei funktioniert, löschen Sie den Browser-Cache und die Cookies für Ihre spezifische IP-/Domain. Weitere Informationen finden Sie im Wiki-Artikel [Cache, Cookies und lokaler Speicher löschen](/useful-tools#clearing-cookies-and-local-storage).

## VPNs, Jackett und die \*ARRs

- Sofern Sie sich nicht in einem repressiven Land wie China, Australien oder Südafrika befinden, muss normalerweise nur Ihr Torrent-Client hinter einem VPN stehen. Da der VPN-Endpunkt von vielen Benutzern gemeinsam genutzt wird, können Sie Einschränkungen bei der Geschwindigkeit, DDOS-Schutz und IP-Sperren von verschiedenen Diensten erleben, die jede Software verwendet.
- Mit anderen Worten, das Hinterlegen der \*ARRs (Lidarr, Prowlarr, Radarr, Readarr und Lidarr) hinter einem VPN kann dazu führen, dass die Anwendungen in einigen Fällen nicht zugänglich sind.

> **Um es klar zu sagen: Es geht nicht darum, ob VPNs Probleme mit den \*ARRs verursachen, sondern wann: Bildanbieter werden Sie blockieren und Cloudflare steht vor den meisten \*ARR-Servern (Updates, Metadaten usw.) und kann Sie ebenfalls blockieren**
{.is-warning}

- **Viele private Tracker werden Sie sperren, wenn Sie sie über ein VPN verwenden oder darauf zugreifen (z. B. über Jackett oder Prowlarr).**

### Verwendung eines VPNs

- Wenn ein VPN erforderlich ist und Docker verwendet wird, wird empfohlen, die Download-Client + VPN-Container von Hotio oder Binhex zu verwenden.
- Wenn ein VPN erforderlich ist und Docker nicht verwendet wird, muss Ihr VPN-Client ***Split Tunneling*** unterstützen, damit nur die erforderlichen (Download-Client) Apps hinter dem VPN stehen.
- Viele Probleme beim Zugriff auf Tracker können behoben werden, indem Sie anstelle der DNS-Server Ihres Internetdienstanbieters die DNS-Server von Google oder Cloudflare verwenden.
- In einigen Fällen (z. B. bei britischen Internetdienstanbietern) müssen Sie Ihren Torrent-Download-Client möglicherweise hinter einem VPN und Jackett/Prowlarr wie folgt platzieren:
  - Platzieren Sie Jackett hinter dem VPN und stellen Sie sicher, dass Split Tunneling den lokalen Zugriff zulässt.
  - Für Prowlarr konfigurieren Sie Ihren VPN-Client so, dass er einen Proxy bereitstellt, und fügen Sie den Proxy in den Einstellungen => Indexers hinzu. Geben Sie dem Proxy einen Tag und weisen Sie den Indexern, die ihn verwenden müssen, denselben Tag zu.
    - Wenn es unbedingt erforderlich ist und Ihr VPN keine Möglichkeit bietet, einen Proxy zu erstellen, können Sie Prowlarr hinter dem VPN platzieren und sicherstellen, dass Split Tunneling den lokalen Zugriff zulässt.

## Wie verhindere ich, dass der Browser beim Start geöffnet wird?

Je nach Betriebssystem gibt es mehrere mögliche Lösungen.

- In einigen Betriebssystemen gibt es in den "Einstellungen" => "Allgemein" ein Kontrollkästchen, um den Browser beim Start zu öffnen.
- Wenn Sie Prowlarr aufrufen, können Sie `-nobrowser` (*nix) oder `/nobrowser` (Windows) zu den Argumenten hinzufügen.
- Beenden Sie Prowlarr und bearbeiten Sie die Datei config.xml. Ändern Sie `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Kann ich alle Indexer auf einmal hinzufügen?

Nein. Dies wäre keine gute Idee und diese Funktion wird nicht hinzugefügt. Es ist viel besser, Ihre Indexer sorgfältig auszuwählen, auf die Statistiken zu achten und Indexer zu entfernen, die zu langsam sind oder keine Ergebnisse liefern. Durch ordnungsgemäßes Beschneiden und Warten Ihrer Indexer erzielen Sie insgesamt viel bessere Ergebnisse und schnellere Suchergebnisse in Ihren Apps.