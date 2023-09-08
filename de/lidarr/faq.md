---
title: Lidarr FAQ
description: Häufig gestellte Fragen zu Lidarr
published: true
date: 2023-08-31T19:08:18.905Z
tags: lidarr, needs-love, faq
editor: markdown
dateCreated: 2021-06-14T14:33:41.344Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
  - [Wie funktioniert Lidarr?](#wie-funktioniert-lidarr)
  - [Wie findet Lidarr Veröffentlichungen?](#wie-findet-lidarr-veröffentlichungen)
  - [Erzwungene Authentifizierung](#erzwungene-authentifizierung)
  - [Wie werden mögliche Downloads verglichen?](#wie-werden-mögliche-downloads-verglichen)
  - [Lidarr funktioniert nicht mehr nach dem Update auf Ubuntu 22.04](#lidarr-funktioniert-nicht-mehr-nach-dem-update-auf-ubuntu-2204)
  - [Warum kann ich keine neue Veröffentlichung oder Künstler zu Lidarr hinzufügen?](#warum-kann-ich-keine-neue-veröffentlichung-oder-künstler-zu-lidarr-hinzufügen)
  - [Warum kann ich kein Album von verschiedenen Künstlern hinzufügen?](#warum-kann-ich-kein-album-von-verschiedenen-künstlern-hinzufügen)
  - [Warum zeigt Lidarr nur Studioalben an? Wie finde ich Singles oder EPs?](#warum-zeigt-lidarr-nur-studioalben-an-wie-finde-ich-singles-oder-eps)
  - [Kann ich nur ein Album hinzufügen?](#kann-ich-nur-ein-album-hinzufügen)
  - [Kann ich einzelne Titel herunterladen?](#kann-ich-einzelne-titel-herunterladen)
  - [Warum wird Künstler X nicht in der Suche angezeigt?](#warum-wird-künstler-x-nicht-in-der-suche-angezeigt)
  - [Lidarr hat ein Album mit zu vielen Titeln zugeordnet. Wie kann ich das Album zur richtigen Veröffentlichung ändern?](#lidarr-hat-ein-album-mit-zu-vielen-titeln-zugeordnet-wie-kann-ich-das-album-zur-richtigen-veröffentlichung-ändern)
  - [Ich kann eine Veröffentlichung in Lidarr nicht finden, aber sie ist auf MusicBrainz](#ich-kann-eine-veröffentlichung-in-lidarr-nicht-finden-aber-sie-ist-auf-musicbrainz)
  - [Wie oft synchronisieren sich die Datenbanken von Lidarr und MusicBrainz?](#wie-oft-synchronisieren-sich-die-datenbanken-von-lidarr-und-musicbrainz)
  - [Wie kann ich fehlende Künstlerbilder hinzufügen?](#wie-kann-ich-fehlende-künstlerbilder-hinzufügen)
  - [Wie kann ich fehlende Albumbilder erhalten? (Cover Art)](#wie-kann-ich-fehlende-albumbilder-erhalten-cover-art)
  - [Ich habe Probleme beim Importieren meiner Künstler, woran könnte es liegen?](#ich-habe-probleme-beim-importieren-meiner-künstler-woran-könnte-es-liegen)
  - [Wie kann ich meine Künstlerordner umbenennen?](#wie-kann-ich-meine-künstlerordner-umbenennen)
  - [Wie kann ich Künstler massenhaft von der Wunschliste löschen?](#wie-kann-ich-künstler-massenhaft-von-der-wunschliste-löschen)
  - [Warum funktioniert Lidarr nicht hinter einem Reverse Proxy?](#warum-funktioniert-lidarr-nicht-hinter-einem-reverse-proxy)
  - [Wie aktualisiere ich Lidarr?](#wie-aktualisiere-ich-lidarr)
    - [Kann ich Lidarr innerhalb meines Docker-Containers aktualisieren?](#kann-ich-lidarr-innerhalb-meines-docker-containers-aktualisieren)
    - [Installation einer neueren Version](#installation-einer-neueren-version)
      - [Native](#native)
      - [Docker](#docker)
  - [Kann ich von `nightly` zu `develop` wechseln?](#kann-ich-von-nightly-zu-develop-wechseln)
  - [Kann ich zwischen Branches wechseln?](#kann-ich-zwischen-branches-wechseln)
  - [Ich erhalte einen Fehler: Database disk image is malformed](#ich-erhalte-einen-fehler-database-disk-image-is-malformed)
  - [Wie sichere/restore ich Lidarr?](#wie-sichere-restore-ich-lidarr)
    - [Sichern von Lidarr](#sichern-von-lidarr)
      - [Verwendung der integrierten Sicherung](#verwendung-der-integrierten-sicherung)
      - [Verwendung des Dateisystems direkt](#verwendung-des-dateisystems-direkt)
    - [Wiederherstellen aus der Sicherung](#wiederherstellen-aus-der-sicherung)
      - [Verwendung der Zip-Sicherung](#verwendung-der-zip-sicherung)
      - [Verwendung der Dateisystem-Sicherung](#verwendung-der-dateisystem-sicherung)
      - [Dateisystem-Wiederherstellung auf Synology NAS](#dateisystem-wiederherstellung-auf-synology-nas)
  - [Ich verwende Lidarr auf einem Mac und es funktioniert plötzlich nicht mehr. Was ist passiert?](#ich-verwende-lidarr-auf-einem-mac-und-es-funktioniert-plötzlich-nicht-mehr-was-ist-passiert)
  - [Ich verwende einen Pi und Raspbian und Lidarr startet nicht](#ich-verwende-einen-pi-und-raspbian-und-lidarr-startet-nicht)
  - [Warum dauern die Synchronisierungszeiten von Listen so lange und kann ich sie ändern?](#warum-dauern-die-synchronisierungszeiten-von-listen-so-lange-und-kann-ich-sie-ändern)
  - [Kann ich die Aktualisierung der Veröffentlichungen deaktivieren?](#kann-ich-die-aktualisierung-der-veröffentlichungen-deaktivieren)
  - [Warum kann Lidarr meine Dateien auf einem Remote-Server nicht sehen?](#warum-kann-lidarr-meine-dateien-auf-einem-remote-server-nicht-sehen)
    - [Lidarr läuft standardmäßig unter dem LocalService-Konto, das keinen Zugriff auf geschützte Remote-Dateifreigaben hat](#lidarr-läuft-standardmäßig-unter-dem-localservice-konto-das-keinen-zugriff-auf-geschützte-remote-dateifreigaben-hat)
    - [Sie verwenden ein zugeordnetes Netzlaufwerk (kein UNC-Pfad)](#sie-verwenden-ein-zugeordnetes-netzlaufwerk-kein-unc-pfad)
  - [Hilfe, ich habe mich ausgesperrt](#hilfe-ich-habe-mich-ausgesperrt)
  - [Wie verhindere ich, dass der Browser beim Start geöffnet wird?](#wie-verhindere-ich-dass-der-browser-beim-start-geöffnet-wird)
  - [Seltsame UI-Probleme](#seltsame-ui-probleme)
  - [VPNs, Jackett und die \*ARRs](#vpns-jackett-und-die-arrs)
  - [Jacketts /all-Endpunkt](#jacketts-all-endpunkt)
    - [Jackett /All-Lösungen](#jackett-all-lösungen)
  - [Warum gibt es zwei Dateien? | Warum bleibt eine Datei im Download-Ordner übrig?](#warum-gibt-es-zwei-dateien--warum-bleibt-eine-datei-im-download-ordner-übrig)
  - [Ich erhalte ständig Warnungen von meinem Cloud-Speicher über API-Limits](#ich-erhalte-ständig-warnungen-von-meinem-cloud-speicher-über-api-limits)

## Wie funktioniert Lidarr?

- Lidarr verwendet RSS-Feeds, um Veröffentlichungen automatisch abzurufen, wenn sie veröffentlicht werden, sowohl neue Veröffentlichungen als auch zuvor veröffentlichte Veröffentlichungen, die erneut veröffentlicht oder neu veröffentlicht werden. Der RSS-Feed enthält die neuesten Veröffentlichungen einer Website, in der Regel zwischen 50 und 100 Veröffentlichungen, obwohl einige Websites mehr und andere weniger bereitstellen. Der RSS-Feed besteht aus allen kürzlich verfügbaren Veröffentlichungen, einschließlich Veröffentlichungen für angeforderte Medien, denen Sie nicht folgen. Wenn Sie sich die Debug-Protokolle ansehen, sehen Sie, dass diese Veröffentlichungen verarbeitet werden, was völlig normal ist.
- Lidarr legt ein Minimum von 10 Minuten für das RSS-Synchronisierungsintervall und ein Maximum von 2 Stunden fest. 15 Minuten sind das von den meisten Indexern empfohlene Minimum, obwohl einige niedrigere Intervalle zulassen, und 2 Stunden stellen sicher, dass Lidarr häufig genug überprüft, um keine Veröffentlichung zu verpassen (obwohl es auf vielen Indexern durch den RSS-Feed blättern kann, um dabei zu helfen). Einige Indexer erlauben es Clients, häufiger als alle 10 Minuten eine RSS-Synchronisierung durchzuführen. In solchen Szenarien empfehlen wir die Verwendung des Release-Push-API-Endpunkts von Lidarr zusammen mit einem IRC-Ankündigungskanal, um Veröffentlichungen in Lidarr zur Verarbeitung zu übertragen. Dies kann nahezu in Echtzeit und mit weniger Overhead auf dem Indexer und Lidarr geschehen, da Lidarr den RSS-Feed nicht zu häufig anfordern und dieselben Veröffentlichungen immer wieder verarbeiten muss.

## Wie findet Lidarr Veröffentlichungen?

- Lidarr sucht nicht regelmäßig nach fehlenden Albumdateien oder solchen, die ihre Qualitätsziele nicht erreicht haben. Stattdessen fragt es Ihre Indexer und Tracker relativ häufig nach ''allen'' neu veröffentlichten Veröffentlichungen ab und vergleicht diese dann mit seiner Liste der fehlenden oder aktualisierungsbedürftigen Veröffentlichungen. Alle Übereinstimmungen werden heruntergeladen. Dadurch kann Lidarr eine Bibliothek ''beliebiger Größe'' mit nur 24-100 Abfragen pro Tag (RSS-Intervall von 15-60 Minuten) abdecken. Wenn Sie dies verstehen, werden Sie feststellen, dass es nur die ''Zukunft'' abdeckt.
- Wie gehen Sie also mit der Gegenwart und Vergangenheit um? Wenn Sie ein Album hinzufügen, müssen Sie den richtigen Pfad, das Profil und den Überwachungsstatus festlegen und dann das Kontrollkästchen "Nach fehlendem Album suchen" aktivieren. Wenn das Album noch nicht veröffentlicht wurde, müssen Sie keine Suche starten.
- Anders ausgedrückt findet Lidarr nur Veröffentlichungen, die neu auf Ihren Indexern hochgeladen wurden. Es wird nicht aktiv versuchen, Veröffentlichungen zu finden, die Sie möchten und die in der Vergangenheit hochgeladen wurden.
- Wenn Sie das Album bereits hinzugefügt haben, aber jetzt danach suchen möchten, haben Sie einige Möglichkeiten. Sie können zur Seite des Albums gehen und die Suchschaltfläche verwenden, die eine Suche durchführt und automatisch eine auswählt. Sie können den Tab "Suche" verwenden und ''alle'' Ergebnisse anzeigen und das gewünschte auswählen. Oder Sie können die Filter "Fehlend", "Gewünscht" oder "Abgeschnitten nicht erfüllt" verwenden.
- Wenn Lidarr längere Zeit offline war, versucht Lidarr, zurückzublättern, um die letzte Veröffentlichung zu finden, die es verarbeitet hat, um das Verpassen einer Veröffentlichung zu vermeiden. Solange Ihr Indexer das Blättern unterstützt und es nicht zu lange her ist, kann Lidarr die Veröffentlichungen verarbeiten, die es verpasst hätte, und Sie müssen keine Suche nach den verpassten Veröffentlichungen durchführen.

## Erzwungene Authentifizierung

Wenn Lidarr so freigegeben ist, dass die Benutzeroberfläche von außerhalb Ihres lokalen Netzwerks aus zugänglich ist, sollten Sie eine Form der Authentifizierung aktiviert haben, um auf die Benutzeroberfläche zugreifen zu können. Dies wird auch von Trackern und Indexern zunehmend gefordert.

Ab Lidarr v2 ist die Authentifizierung obligatorisch.

### Authentifizierungsmethode

- `Basic` (Browser-Popup) - Diese Option zeigt beim Zugriff auf Lidarr ein kleines Popup an, in dem Sie einen Benutzernamen und ein Passwort eingeben können.
- `Forms` (Anmeldeseite) - Diese Option zeigt eine vertraut aussehende Anmeldeseite an, ähnlich wie bei anderen Websites, auf denen Sie sich bei Lidarr anmelden können.
- `External` - Nur über Konfigurationsdatei konfigurierbar
  - Wenn Sie eine **externe Authentifizierung** wie Authelia, Authetik, NGINX Basic Auth usw. verwenden, können Sie eine doppelte Authentifizierung vermeiden, indem Sie die App beenden, `<AuthenticationMethod>External</AuthenticationMethod>` in der [Konfigurationsdatei](/lidarr/appdata-directory) festlegen und die App neu starten. Beachten Sie, dass mehrere `AuthenticationMethod`-Einträge in der Datei nicht unterstützt werden und nur der oberste Wert verwendet wird.

### Erforderliche Authentifizierung

- Wenn Sie die App nicht extern freigeben und/oder keine Authentifizierung für den lokalen Zugriff (z. B. LAN) wünschen, ändern Sie in Einstellungen => Allgemeine Sicherheit => Erforderliche Authentifizierung auf `Deaktiviert für lokale Adressen`
  - Das Konfigurationsdatei-Äquivalent dazu lautet `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Wie werden mögliche Downloads verglichen?

> Im Allgemeinen hat Qualität Vorrang. Wenn Sie möchten, dass Qualität nicht die Hauptpriorität hat, können Sie Ihre Qualitäten zusammenführen. [Siehe TRaSH's Guide](https://trash-guides.info/merge-quality)***
{.is-info}

- Die aktuelle Logik [finden Sie hier](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- Stand 2022-01-23 lautet die Logik wie folgt:

1. Qualität
1. Bevorzugte Wortbewertung
1. Protokoll (wie in den entsprechenden Verzögerungsprofilen konfiguriert)
1. Indexer-Priorität
1. Seeds/Peers (bei Torrent)
1. Anzahl der Alben
1. Alter (bei Usenet)
1. Größe

## Lidarr funktioniert nicht mehr nach dem Update auf Ubuntu 22.04

- Lidarr v0.8 ist nicht kompatibel und wird nicht auf Ubuntu 22.04 unterstützt.
- Nur Lidarr v1 unterstützt Ubuntu 22.04.
- [Siehe diesen FAQ-Eintrag für die Branches und Versionen](#wie-aktualisiere-ich-lidarr)

## Warum kann ich keine neue Veröffentlichung oder Künstler zu Lidarr hinzufügen?

- Die Veröffentlichung hat wahrscheinlich den Typ "unbekannt" in MusicBrainz.

## Warum kann ich kein Album von verschiedenen Künstlern hinzufügen?

- Verschiedene Künstler und andere Meta-Künstler in MusicBrainz sind aufgrund der Anzahl der von ihnen bereitgestellten Einträge nicht möglich.

## Warum zeigt Lidarr nur Studioalben an? Wie finde ich Singles oder EPs?

- Lidarr zeigt standardmäßig nur Studioalben für jeden Künstler an. Sie können jedoch die Albumtypen pro Künstler oder für Ihre gesamte Bibliothek erweitern, indem Sie Metadatenprofile verwenden.

## Kann ich nur ein Album hinzufügen?

- Im Moment nicht.

## Kann ich einzelne Titel herunterladen?

- Lidarr sucht und lädt vollständige Veröffentlichungen herunter. Daher können einzelne Titel nur dann heruntergeladen werden, wenn sie als Single vom Künstler veröffentlicht wurden.

## Warum wird Künstler X nicht in der Suche angezeigt?

- Die Suche befindet sich noch in der Entwicklung. Künstler, die in der Suche nicht angezeigt werden, können hinzugefügt werden, indem Sie nach `lidarr:mbid` suchen, wobei `mbid` die MusicBrainz-ID des Künstlers ist.

## Lidarr hat ein Album mit zu vielen Titeln zugeordnet. Wie kann ich das Album zur richtigen Veröffentlichung ändern?

- Öffnen Sie die Detailseite des Albums und wählen Sie das Bearbeitungssymbol in der oberen Navigationsleiste aus. Dort finden Sie eine Dropdown-Liste aller mit diesem Album verknüpften Veröffentlichungen.

## Ich kann eine Veröffentlichung in Lidarr nicht finden, aber sie ist auf MusicBrainz

- Dies liegt wahrscheinlich daran, dass die Veröffentlichung einen "unbekannten" Veröffentlichungsstatus hat. Aktualisieren Sie MusicBrainz.

## Wie oft synchronisieren sich die Datenbanken von Lidarr und MusicBrainz?

- Jede Stunde um 5 nach der Stunde

## Wie kann ich fehlende Künstlerbilder hinzufügen?

- Fügen Sie Kunst zu fanart.tv hinzu und warten Sie ~7+ Tage, bis es durch den Cache gelöscht ist. Aktualisieren Sie dann die Metadaten.

## Wie kann ich fehlende Albumbilder erhalten? (Cover Art)

- Fügen Sie Coverart zu MusicBrainz hinzu und warten Sie ~1 Stunde+, bis es durch den Cache gelöscht ist. Aktualisieren Sie dann die Metadaten.

## Ich habe Probleme beim Importieren meiner Künstler, woran könnte es liegen?

- Der Künstlerimportprozess importiert nur die Künstlernamen und Pfadpositionen, die dann in der Datenbank gespeichert werden, damit a) Metadaten abgerufen werden können und b) heruntergeladene Inhalte in Zukunft am selben Ort abgelegt werden können. Zu diesem Zweck benötigt das Benutzerkonto, unter dem Lidarr ausgeführt wird, Lese- und Schreibzugriff auf Ihr Datenverzeichnis.

## Wie kann ich meine Künstlerordner umbenennen?

{#rename-folders}

> Derselbe Prozess gilt auch für das Verschieben/Ändern von Künstlerpfaden.
{.is-info}

1. Bibliothek
1. Masseneditor
1. Wählen Sie die Künstler aus, deren Ordner umbenannt werden sollen
1. Ändern Sie den Stammordner in den gleichen Stammordner, in dem sich die Künstler derzeit befinden
1. Wählen Sie "Ja, Dateien verschieben"

## Wie kann ich Künstler massenhaft von der Wunschliste löschen?

- Verwenden Sie den Masseneditor => Wählen Sie die Künstler aus, die Sie löschen möchten => Löschen

## Warum funktioniert Lidarr nicht hinter einem Reverse Proxy?

- Lidarr verwendet .NET und einen neuen Webserver. Damit SignalR funktioniert, die UI-Schaltflächen funktionieren, Datenbankänderungen übernommen werden und andere Elemente, ist die folgende Ergänzung zur location-Block für Lidarr erforderlich:
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- Stellen Sie sicher, dass Sie `proxy_set_header Connection "Upgrade";` nicht wie in der nginx-Dokumentation vorgeschlagen einschließen. `DIES FUNKTIONIERT NICHT`
- [Siehe dieses ASP.NET Core Problem](https://github.com/aspnet/AspNetCore/issues/17081)
- Wenn Sie einen CDN wie Cloudflare verwenden, stellen Sie sicher, dass Websockets aktiviert sind, um Websocket-Verbindungen zu ermöglichen.

## Wie aktualisiere ich Lidarr?

- Gehen Sie zu Einstellungen und dann zum Tab Allgemein und zeigen Sie erweiterte Einstellungen an (verwenden Sie den Umschalter neben der Speichern-Schaltfläche).

1. Ändern Sie unter dem Abschnitt Updates den Branch-Namen in `master` oder `develop`
1. Speichern

*Dies installiert die Bits aus diesem Branch nicht sofort, sondern während des nächsten Updates.*



- `master` - ![Aktueller Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Es wurde von Benutzern auf den Entwicklungs- und Nightly-Zweigen getestet und es sind keine größeren Probleme bekannt. Diese Version erhält ungefähr monatliche Updates. Auf GitHub handelt es sich um den `master`-Zweig.

- `develop` - ![Aktueller Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (Beta): Dies ist der Testbereich. Nachdem es in der Nightly-Version getestet wurde, um sofortige Probleme auszuschließen, werden hier neue Funktionen und Fehlerkorrekturen zuerst veröffentlicht. Es kann als halb stabil angesehen werden, ist aber immer noch `beta`. Diese Version erhält wöchentlich oder zweiwöchentlich Updates, abhängig von der Entwicklung.

> **Warnung: Möglicherweise können Sie nach dem Wechsel zu diesem Zweig nicht mehr zu `master` zurückkehren.** Auf GitHub handelt es sich um einen Schnappschuss des `develop`-Zweigs zu einem bestimmten Zeitpunkt.
{.is-warning}

- `nightly` - ![Aktueller Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (Alpha/Unstable): Dies ist die neueste Version. Sie wird veröffentlicht, sobald der Code übernommen und alle automatisierten Tests bestanden wurden. Diese Version wurde möglicherweise noch nicht von uns oder anderen Benutzern verwendet. Es besteht keine Garantie, dass sie in einigen Fällen überhaupt ausgeführt wird. Dieser Zweig wird nur fortgeschrittenen Benutzern empfohlen. Probleme und Eigenuntersuchungen werden in diesem Zweig erwartet. ***Verwenden Sie diesen Zweig nur, wenn Sie wissen, was Sie tun, und bereit sind, sich die Hände schmutzig zu machen, um ein fehlgeschlagenes Update wiederherzustellen.*** Diese Version wird sofort aktualisiert.

> **Warnung: Möglicherweise können Sie nach dem Wechsel zu diesem Zweig nicht mehr zu `master` zurückkehren.** Auf GitHub handelt es sich um den `develop`-Zweig.
{.is-danger}

- Hinweis: Wenn Sie die Installation über Docker durchführen, fügen Sie `:release`, `:latest`, `:testing` oder `:develop` an das Ende Ihres Container-Tags an, abhängig davon, wer Ihre Builds erstellt. Beachten Sie, dass `nightly`-Zweige absichtlich nicht unten aufgeführt sind.

|                                                                    | `master` (stable) ![Aktueller Master/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Aktueller Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (alpha) ![Aktueller Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### Kann ich Lidarr in meinem Docker-Container aktualisieren?

- *Technisch gesehen ja.* **Aber du solltest es auf keinen Fall tun.** Das ist ein grundlegendes Prinzip von Docker. Es können Probleme mit der Datenbank auftreten, wenn Sie Ihre Installation auf die neueste `nightly`-Version aktualisieren und dann den Docker-Container selbst aktualisieren (möglicherweise auf eine ältere Version zurückstufen).

### Installation einer neueren Version

#### Native

1. Gehe zu System und dann zum Tab Updates.
1. Neuere Versionen, die noch nicht installiert sind, haben einen Update-Button neben sich. Durch Klicken auf diesen Button wird das Update installiert.

#### Docker

1. Ziehen Sie Ihr Tag erneut und aktualisieren Sie Ihren Container.

## Kann ich von `nightly` zu `develop` wechseln?

## Kann ich zwischen den Zweigen wechseln?

- Wenn die Version identisch ist, können Sie wechseln. Andernfalls überprüfen Sie beim Entwicklungsteam, ob Sie von `nightly` zu `master` wechseln können; `nightly` zu `develop`; oder `develop` zu `master` für Ihren spezifischen Build.
- Wenn Sie diese Anweisungen nicht befolgen, kann Ihr Lidarr unbrauchbar werden oder Fehler verursachen. Sie wurden gewarnt.
  - Der häufigste Fehler ist etwas wie `Error parsing column 45 (Language=31 - Int64)` oder andere ähnliche Datenbankfehler in Bezug auf fehlende Spalten oder Tabellen.

## Ich erhalte einen Fehler: Database disk image is malformed

- **Fehler wie `Error creating log database` deuten auf Probleme mit logs.db hin**
  - Dies kann schnell behoben werden, indem die Datenbank umbenannt oder entfernt wird. Die Protokolldatenbank enthält unwichtige Informationen über den Befehlsverlauf und die Update-Installationshistorie sowie Info-, Warn- und Fehlermeldungen.
- **Fehler wie `Error creating main database` oder allgemeine `database disk image is malformed` ohne spezifizierte Datenbank deuten auf Probleme mit lidarr.db hin**
  - Fahren Sie mit den unten angegebenen Schritten fort.
- Dies bedeutet, dass Ihre SQLite-Datenbank, die die meisten Informationen für Lidarr speichert, beschädigt ist. Ihre Optionen bestehen darin, (eine) Sicherung(en) zu versuchen, die vorhandene Datenbank wiederherzustellen, die Sicherung(en) wiederherzustellen oder falls alles andere fehlschlägt, mit einer frischen neuen Datenbank neu zu beginnen.
- Dieser Fehler kann auftreten, wenn die Datenbankdatei vom Benutzer/der Benutzergruppe, unter der \*Arr ausgeführt wird, nicht beschreibbar ist. Berechtigungen sind wahrscheinlich nur ein Problem bei neuen Installationen, bei migrierten Installationen auf einen neuen Server, wenn Sie kürzlich die Berechtigungen für Ihr Appdata-Verzeichnis geändert haben oder wenn Sie den Benutzer und die Gruppe geändert haben, unter der \*Arr ausgeführt wird.
- Ihre beste und erste Option besteht darin, [versuchen Sie, eine Sicherung wiederherzustellen](#wie-sichere-ich-mein-lidarr).
- Sie können auch versuchen, Ihre Datenbank wiederherzustellen. Dies ist in der Regel die einzige Option, wenn dieses Problem nach einem Update auftritt. Versuchen Sie den [sqlite3-Befehl `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Wenn Ihr sqlite nicht über `.recover` verfügt oder Sie eine benutzerfreundlichere GUI (z. B. Windows) wünschen, befolgen Sie [unsere Anweisungen in diesem Wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- Eine weitere mögliche Ursache für den Fehler in Ihrer Datenbank ist, dass Sie Ihre Datenbank auf einem Netzlaufwerk (NFS oder SMB oder etwas anderem, das nicht lokal ist) platzieren. **SQLite ist für Situationen konzipiert, in denen Daten und Anwendung auf demselben Computer vorhanden sind.** Daher muss Ihr \*Arr AppData-Ordner (/config mount für Docker) auf lokalem Speicher sein. [SQLite und Netzlaufwerke funktionieren nicht gut zusammen und führen letztendlich zu einer beschädigten Datenbank](https://www.sqlite.org/draft/useovernet.html).
- Wenn Sie mergerFS verwenden, müssen Sie `direct_io` entfernen, da SQLite mmap verwendet, das von `direct_io` nicht unterstützt wird, wie in der mergerFS [Dokumentation hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs) erklärt.

## Wie sichere ich mein Lidarr?

### Lidarr sichern

#### Verwendung der integrierten Sicherung

- Gehe im Lidarr-Benutzerinterface zu System => Backup.
- Klicke auf die Schaltfläche Backup.
- Lade das Zip-Archiv nach der Erstellung der Sicherung herunter, um es sicher aufzubewahren.

#### Verwendung des Dateisystems direkt

- Finde den Speicherort des AppData-Verzeichnisses für Lidarr heraus.
  - Gehe über das Lidarr-Benutzerinterface zu System => About.
  - [Lidarr Appdata-Verzeichnis](/lidarr/appdata-directory)
- Stoppe Lidarr - Dadurch wird verhindert, dass die Datenbank beschädigt wird.
- Kopiere den Inhalt an einen sicheren Ort.

### Wiederherstellen aus einer Sicherung

> Das Wiederherstellen auf ein Betriebssystem mit unterschiedlichen Pfaden funktioniert nicht (Windows zu Linux, Linux zu Windows, Windows zu OS X oder OS X zu Windows). Der Wechsel zwischen OS X und Linux kann funktionieren, da beide Pfade mit `/` anstelle von `\` verwendet werden, wie es Windows verwendet, wird jedoch nicht unterstützt. Sie müssen alle Pfade in der Datenbank manuell bearbeiten.
{.is-warning}

#### Verwendung der Zip-Sicherung

- Neuinstallation von Lidarr (falls zutreffend / noch nicht installiert)
- Starte Lidarr
- Navigiere zu System => Backup
- Wähle Wiederherstellen aus Backup aus
- Wähle Datei auswählen aus
- Wähle deine Backup-Zip-Datei aus
- Wähle Wiederherstellen aus

#### Verwendung der Dateisystem-Sicherung

- Neuinstallation von Lidarr (falls zutreffend / noch nicht installiert)
- Finde den Speicherort des AppData-Verzeichnisses für Lidarr heraus.
  - Führe Lidarr einmal aus und gehe über das Benutzerinterface zu System => About.
  - [Lidarr Appdata-Verzeichnis](/lidarr/appdata-directory)
- Stoppe Lidarr
- Lösche den Inhalt des AppData-Verzeichnisses **(einschließlich der .db-wal/.db-journal-Dateien, sofern vorhanden)**
- Stelle aus deinem Backup wieder her
- Starte Lidarr
- Solange die Pfade gleich sind, wird alles dort fortgesetzt, wo es aufgehört hat

#### Dateisystem-Wiederherstellung auf Synology NAS

> VORSICHT: Die Wiederherstellung auf einem Synology erfordert Kenntnisse in Linux und Root-SSH-Zugriff auf das Synology-Gerät.
{.is-warning}

- Neuinstallation von Lidarr (falls zutreffend / noch nicht installiert)
- Finde den Speicherort des AppData-Verzeichnisses für Lidarr heraus.
  - Führe Lidarr einmal aus und gehe über das Benutzerinterface zu System => About.
  - [Lidarr Appdata-Verzeichnis](/lidarr/appdata-directory)
- Stoppe Lidarr
- Verbinde dich über SSH mit dem Synology NAS und melde dich als root an

> Bei einigen Installationen unterscheidet sich der Benutzer von den unten stehenden Befehlen: `chown -R sc-Lidarr:Lidarr *` {.is-info}

- Führe die folgenden Befehle aus:

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- Aktualisiere die Berechtigungen für die Dateien:

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- Starte Lidarr

## Ich verwende Lidarr auf einem Mac und es funktioniert plötzlich nicht mehr. Was ist passiert?

- Wahrscheinlich liegt dies an einem MacOS-Bug, der dazu geführt hat, dass eine der Datenbanken beschädigt wurde.

- Siehe den oben genannten Eintrag zur beschädigten Datenbank.

- Versuchen Sie dann, es zu starten und sehen Sie, ob es funktioniert. Wenn es nicht funktioniert, benötigen Sie weitere Unterstützung. Posten Sie in unserem [Subreddit /r/lidarr](http://reddit.com/r/lidarr) oder kommen Sie auf [unseren Discord-Server](https://lidarr.audio/discord), um Hilfe zu erhalten.

## Ich verwende einen Pi und Raspbian und Lidarr startet nicht

Raspbian hat eine Version von libseccomp2, die zu alt ist, um einen Docker-Container auf Basis von Ubuntu 20.04 auszuführen, den sowohl hotio als auch LinuxServer als Basis verwenden. Sie müssen entweder `--privileged` verwenden, libseccomp2 von Ubuntu aktualisieren oder ein besseres Betriebssystem verwenden (Wir empfehlen Ubuntu 20.04 arm64).

**Mögliche Lösung:**

Es ist gelungen, das Problem zu beheben, indem das Backport aus dem Debian-Repository installiert wurde. Es wird im Allgemeinen nicht empfohlen, das Backport im Modus für allgemeine Upgrades zu verwenden. Die Installation eines einzelnen Pakets kann in Ordnung sein, kann aber auch Probleme verursachen. Daher sollten Sie verstehen, was Sie tun.

Schritte zur Behebung:

Stellen Sie zunächst sicher, dass Sie Raspbian Buster verwenden, z.B. mit `lsb_release -a`

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- Wenn Sie Buster verwenden:
  - Führen Sie folgendes aus, um das Backport zu Ihren Quellen hinzuzufügen

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - Installieren Sie das Backport von libseccomp2

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## Warum dauern die Synchronisierungszeiten der Listen so lange und kann ich sie ändern?

Listen waren noch nie und sind nicht dazu gedacht, sofort hinzugefügt zu werden. Sie sind Werkzeuge für "Hey, ich möchte das irgendwann hinzufügen".

Sie können eine manuelle Aktualisierung der Liste auslösen, ein Skript erstellen und es über die API auslösen oder die Veröffentlichungen direkt zu Lidarr hinzufügen.

Diese Änderung wurde vorgenommen, um zu verhindern, dass unser Server durch Personen, die die Listen alle 10 Minuten aktualisieren, überlastet wird.

## Kann ich die Aufgabe "Veröffentlichungen aktualisieren" deaktivieren?

Nein, und Sie sollten dies auch nicht durch SQL-Manipulationen tun. Die Aufgabe "Veröffentlichungen aktualisieren" fragt den Upstream-Servarr-Proxy ab und überprüft, ob sich die Metadaten für jede Veröffentlichung (IDs, Besetzung, Zusammenfassung, Bewertung, Übersetzungen, alternative Titel usw.) im Vergleich zu dem, was in Lidarr vorhanden ist, aktualisiert haben. Falls erforderlich, werden die entsprechenden Veröffentlichungen aktualisiert.

Eine häufige Beschwerde ist, dass die Aktualisierungsaufgabe eine hohe I/O-Auslastung verursacht. Eine Einstellung, die Probleme verursachen kann, ist "Künstlerordner nach Aktualisierung erneut scannen". Wenn Ihre Festplatten-I/O-Auslastung während einer Aktualisierung stark ansteigt, sollten Sie die Einstellung "Erneut scannen" auf "Manuell" ändern. Ändern Sie dies nicht auf "Nie", es sei denn, alle Änderungen an Ihrer Bibliothek (neue Veröffentlichungen, Upgrades, Löschungen usw.) werden über Lidarr vorgenommen. Wenn Sie Veröffentlichungsdateien manuell löschen oder ein Programm von Drittanbietern verwenden, setzen Sie dies nicht auf "Nie".

## Warum kann Lidarr meine Dateien auf einem Remote-Server nicht sehen?

- Stellen Sie für alle Betriebssysteme sicher, dass der Benutzer/die Gruppe, unter der/dem Sie \*Arr ausführen, Lese- und Schreibzugriff auf das eingebundene Laufwerk hat.
- Für Linux stellen Sie sicher:
  - Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` für Ihr Laufwerk aktiviert ist.
  - Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` für Ihr Laufwerk aktiviert ist.
- Für Windows: Kurz gesagt: Der Benutzer, unter dem \*Arr ausgeführt wird (falls als Dienst) oder unter dem es ausgeführt wird (falls als Tray-App), kann nicht auf den Dateipfad auf dem Remote-Server zugreifen. Dies kann verschiedene Gründe haben, aber das häufigste ist, dass \*Arr als Dienst ausgeführt wird, was die unten beschriebenen Probleme verursacht.

### Lidarr wird standardmäßig unter dem Konto LocalService ausgeführt, das keinen Zugriff auf geschützte Remote-Dateifreigaben hat

- Führen Sie den Lidarr-Dienst als anderen Benutzer aus, der Zugriff auf diese Freigabe hat.
- Öffnen Sie das Fenster "Verwaltungstools" > "Dienste" auf Ihrem Windows-Server.
- Stoppen Sie den Lidarr-Dienst.
- Öffnen Sie den Dialog "Eigenschaften" > "Anmelden".
- Ändern Sie das Benutzerkonto des Dienstes auf das Zielbenutzerkonto.
- Führen Sie Lidarr.exe über den Startordner aus.

### Sie verwenden ein zugeordnetes Netzlaufwerk (kein UNC-Pfad)

- Ändern Sie Ihre Pfade in UNC-Pfade (`\\server\freigabe`).
- Führen Sie Lidarr.exe über den Startordner aus.

## Hilfe, ich habe mich ausgesperrt

{#help-i-have-forgotten-my-password}

Um die Authentifizierung zu deaktivieren (um Ihren vergessenen Benutzernamen oder Ihr vergessenes Passwort zurückzusetzen), müssen Sie `config.xml` bearbeiten, das sich im [Lidarr Appdata-Verzeichnis](/lidarr/appdata-directory) befindet.

1. Öffnen Sie config.xml in einem Texteditor.
1. Suchen Sie die Zeile mit der Authentifizierungsmethode: `<AuthenticationMethod>Basic</AuthenticationMethod>` oder `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Ändern Sie die Zeile `AuthenticationMethod` in `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Starten Sie Lidarr neu.
1. Lidarr ist jetzt ohne Passwort zugänglich. Gehen Sie zu "Einstellungen: Allgemein" in der Benutzeroberfläche und legen Sie Ihren Benutzernamen und Ihr Passwort fest.

## Wie verhindere ich, dass der Browser beim Start geöffnet wird?

Je nach Betriebssystem gibt es mehrere mögliche Methoden.

- In "Einstellungen" => "Allgemein" gibt es in einigen Betriebssystemen ein Kontrollkästchen, um den Browser beim Start zu öffnen.
- Wenn Sie Lidarr aufrufen, können Sie `-nobrowser` (*nix) oder `/nobrowser` (Windows) zu den Argumenten hinzufügen.
- Beenden Sie Lidarr und bearbeiten Sie die Datei config.xml und ändern Sie `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Seltsame Probleme mit der Benutzeroberfläche

- Wenn Sie seltsame Probleme mit der Benutzeroberfläche haben, z.B. wird auf der Bibliotheksseite nichts angezeigt oder eine bestimmte Ansicht oder Sortierung funktioniert nicht, versuchen Sie es in einem Chrome-Inkognito-Fenster oder Firefox-Privatfenster. Wenn es dort einwandfrei funktioniert, löschen Sie den Browser-Cache und die Cookies für Ihre spezifische IP-/Domain. Weitere Informationen finden Sie im Wiki-Artikel [Cache, Cookies und lokaler Speicher löschen](/useful-tools#clearing-cookies-and-local-storage).

## VPNs, Jackett und die \*ARRs

- Wenn Sie sich nicht in einem repressiven Land wie China, Australien oder Südafrika befinden, muss normalerweise nur Ihr Torrent-Client hinter einem VPN sein. Da der VPN-Endpunkt von vielen Benutzern gemeinsam genutzt wird, können Sie und werden Sie Rate-Limiting, DDOS-Schutz und IP-Sperren von verschiedenen Diensten, die jede Software verwendet, erleben.
- Mit anderen Worten, das Hinterlegen der \*Arrs (Lidarr, Prowlarr, Radarr, Readarr und Lidarr) hinter einem VPN kann dazu führen, dass die Anwendungen in einigen Fällen aufgrund der Nichterreichbarkeit der Dienste nicht verwendet werden können.

> **Um es klar zu sagen: Es ist nicht die Frage, ob VPNs Probleme mit den \*Arrs verursachen, sondern wann: Bildanbieter werden Sie blockieren und Cloudflare befindet sich vor den meisten \*Arr-Servern (Updates, Metadaten usw.) und wird Sie ebenfalls blockieren**
{.is-warning}

- **Viele private Tracker werden Sie sperren, wenn Sie sie verwenden oder auf sie zugreifen (d.h. Jackett oder Prowlarr) über ein VPN.**

### Verwendung eines VPN

- Wenn ein VPN erforderlich ist und Docker verwendet wird, wird empfohlen, die Hotio- oder Binhex-Download-Client + VPN-Container zu verwenden.
- Wenn ein VPN erforderlich ist und Docker nicht verwendet wird, muss Ihr VPN-Client ***Split-Tunneling*** unterstützen, damit nur die erforderlichen (Download-Client-)Apps hinter dem VPN liegen.
- Viele Probleme beim Zugriff auf Tracker können behoben werden, indem Sie die DNS-Server von Google oder Cloudflare anstelle der DNS-Server Ihres Internetdienstanbieters verwenden.
- In einigen Fällen (z.B. bei britischen Internetdienstanbietern) müssen Sie Ihren Torrent-Download-Client möglicherweise hinter einem VPN und Jackett/Prowlarr wie folgt platzieren:
  - Setzen Sie Jackett hinter das VPN und stellen Sie sicher, dass das Split-Tunneling den lokalen Zugriff zulässt.
  - Konfigurieren Sie für Prowlarr Ihren VPN-Client so, dass er einen Proxy bereitstellt, und fügen Sie den Proxy in "Einstellungen" => "Indexers" hinzu. Geben Sie dem Proxy einen Tag und verwenden Sie den gleichen Tag für alle Indexer, die ihn verwenden müssen.
    - Wenn dies unbedingt erforderlich ist und Ihr VPN keine Möglichkeit bietet, einen Proxy zu erstellen, können Sie Prowlarr hinter das VPN setzen und sicherstellen, dass das Split-Tunneling den lokalen Zugriff zulässt.

## Jacketts /all-Endpunkt

{#jackett-all-endpoint}

- Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ können Sie sich das Jackett & NZBHydra2-Alternative [Prowlarr](/prowlarr) ansehen.
- **April 2022 Update: Die Unterstützung für \*Arr wurde aus dem Jackett `/all` entfernt, da es nur Probleme verursacht.**
- Der Jackett /all-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Selbst die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des /all-Endpunkts hat keine Vorteile, nur Nachteile:
  - Sie verlieren die Kontrolle über indexer-spezifische Einstellungen (Kategorien, Suchmodi usw.).
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen.
  - Indexer-spezifische Kategorien (\>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis.
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt.
  - Wenn einer der Tracker in /all einen Fehler zurückgibt, deaktiviert \*Arr ihn und Sie erhalten keine Ergebnisse mehr.

### Lösungen für Jackett /All

- Fügen Sie jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu.
- Schauen Sie sich [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schauen Sie sich [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwenden Sie jedoch nicht ihren einzelnen aggregierten Endpunkt, sondern verwenden Sie `multi`, wenn die Synchronisierung verwendet wird.

## Warum gibt es zwei Dateien? | Warum bleibt eine Datei im Download-Ordner?

Das ist normal. Bei einer Konfiguration, die [Hardlinks](https://trash-guides.info/hardlinks) unterstützt, wird kein doppelter Speicherplatz verwendet. Hier ist, wie der Torrent-Prozess funktioniert.

1. Lidarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben. Beispiele: Filme, TV, Serien, Musik usw.
1. Lidarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
1. Abgeschlossene Dateien bleiben an ihrem ursprünglichen Speicherort, um das Seeden der Datei zu ermöglichen (Verhältnis oder Zeit kann im Download-Client oder innerhalb des spezifischen Download-Clients angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, wird die Datei per Hardlink verknüpft, wenn dies von Ihrer Konfiguration unterstützt wird, oder kopiert, wenn Hardlinks nicht unterstützt werden.
1. Wenn die Option "Abgeschlossene Download-Verarbeitung - Abgeschlossene entfernen" in den Einstellungen von Lidarr aktiviert ist, löscht Lidarr die Originaldatei und den Torrent aus Ihrem Download-Client, aber nur, wenn der Download-Client meldet, dass das Seeden abgeschlossen ist und der Torrent angehalten ist (d.h. pausiert). Informationen zur optimalen Konfiguration Ihres Download-Clients finden Sie in den [Download-Client-Anleitungen von TRaSH](https://trash-guides.info/Downloaders/).

> Hardlinks sind standardmäßig aktiviert. [Ein Hardlink verwendet keinen zusätzlichen Festplattenspeicher.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihre Konfiguration keine Hardlinks unterstützt, wird auf die Datei zurückgegriffen und sie wird kopiert.
{.is-info}

## Ich erhalte ständig Warnungen von meinem Cloud-Speicher über API-Limits

Lidarr ist anders als die anderen Arrs. Es verwendet Tags anstelle von Dateinamen für den Betrieb. Wenn Sie Lidarr-Dateien auf Cloud-Speicher aufbewahren, muss es die Datei herunterladen, um die Tags zu lesen. Dadurch werden Sie sehr schnell alle API-Limits überschreiten, die Sie bei Ihrem Speicheranbieter haben. Wir raten dringend davon ab, Ihre Lidarr-Bibliothek auf einem Cloud-Speicheranbieter zu speichern, und alle Probleme, die Sie möglicherweise haben, sind wahrscheinlich auf diese Konfiguration zurückzuführen.