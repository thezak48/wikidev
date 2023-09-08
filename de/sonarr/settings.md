---
title: Sonarr-Einstellungen
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, needs-love, Einstellungen
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Menüoptionen](#menüoptionen)
- [Medienverwaltung](#medienverwaltung)
  - [Vorschläge zur Community-Namensgebung](#vorschläge-zur-community-namensgebung)
  - [Episodenbenennung](#episodenbenennung)
    - [Standard-Episodenformat](#standard-episodenformat)
    - [Serienbenennung](#serienbenennung)
    - [Serien-IDs](#serien-ids)
    - [Staffeln](#staffeln)
    - [Episoden](#episoden)
    - [Ausstrahlungsdatum](#ausstrahlungsdatum)
    - [Episodentitel](#episodentitel)
    - [Qualität](#qualität)
    - [Medieninformationen](#medieninformationen)
    - [Sonstiges](#sonstiges)
    - [Original](#original)
  - [Tägliches Episodenformat](#tägliches-episodenformat)
  - [Anime-Episodenformat](#anime-episodenformat)
    - [Absolute Episodennummer](#absolute-episodennummer)
  - [Serienordnerformat](#serienordnerformat)
    - [Serienbenennung](#serienbenennung-1)
    - [Serien-IDs](#serien-ids-1)
  - [Staffelordnerformat](#staffelordnerformat)
    - [Staffeln](#staffeln-1)
  - [Staffelordnerformat](#staffelordnerformat-1)
    - [Specials](#specials)
  - [Mehrere Episodenstile](#mehrere-episodenstile)
  - [Ordner](#ordner)
  - [Importieren](#importieren)
  - [Dateiverwaltung](#dateiverwaltung)
  - [Berechtigungen](#berechtigungen)
  - [Stammordner](#stammordner)
- [Profile](#profile)
  - [Qualitätsprofile](#qualitätsprofile)
  - [Sprachprofile](#sprachprofile)
  - [Verzögerungsprofile](#verzögerungsprofile)
    - [Verwendung](#verwendung)
    - [Funktionsweise der Verzögerungsprofile](#funktionsweise-der-verzögerungsprofile)
      - [Beispiele](#beispiele)
        - [Beispiel 1](#beispiel-1)
        - [Beispiel 2](#beispiel-2)
        - [Beispiel 3](#beispiel-3)
  - [Freigabeprofile](#freigabeprofile)
- [Qualität](#qualität-1)
  - [Bedeutung der Qualitätstabelle](#bedeutung-der-qualitätstabelle)
  - [Definierte Qualitäten](#definierte-qualitäten)
- [Indexer](#indexer)
  - [Unterstützte Indexer](#unterstützte-indexer)
    - [Indexer-Einstellungen](#indexer-einstellungen)
    - [Usenet-Indexer-Konfiguration](#usenet-indexer-konfiguration)
    - [Torrent-Tracker-Konfiguration](#torrent-tracker-konfiguration)
  - [Optionen](#optionen)
- [Download-Clients](#download-clients)
  - [Übersicht](#übersicht)
  - [Download-Client-Prozesse](#download-client-prozesse)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Download-Clients](#download-clients-1)
    - [Unterstützte Download-Clients](#unterstützte-download-clients)
    - [Usenet-Client-Einstellungen](#usenet-client-einstellungen)
    - [Torrent-Client-Einstellungen](#torrent-client-einstellungen)
    - [Kompatibilität der Torrent-Client-Entfernung von Downloads](#kompatibilität-der-torrent-client-entfernung-von-downloads)
  - [Behandlung abgeschlossener Downloads](#behandlung-abgeschlossener-downloads)
    - [Abgeschlossene Downloads entfernen](#abgeschlossene-downloads-entfernen)
    - [Behandlung fehlgeschlagener Downloads](#behandlung-fehlgeschlagener-downloads)
  - [Pfadzuordnungen für Remote](#pfadzuordnungen-für-remote)
- [Importlisten](#importlisten)
  - [Listen](#listen)
  - [Listenausschlüsse](#listenausschlüsse)
- [Verbinden](#verbinden)
  - [Verbindungen](#verbindungen)
  - [Verbindungsauslöser](#verbindungsauslöser)
- [Metadaten](#metadaten)
  - [Metadaten](#metadaten-1)
- [Tags](#tags)
- [Allgemein](#allgemein)
  - [Host](#host)
  - [Sicherheit](#sicherheit)
  - [Proxy](#proxy)
  - [Protokollierung](#protokollierung)
  - [Analytik](#analytik)
  - [Updates](#updates)
  - [Backups](#backups)
- [Benutzeroberfläche](#benutzeroberfläche)
  - [Kalender](#kalender)
  - [Termine](#termine)
  - [Stil](#stil)
  
Diese Seite erläutert alle verfügbaren Einstellungen in Sonarr und wie sie funktionieren. Dies soll keine umfassende Anleitung zur Einrichtung von Sonarr sein. Stattdessen sollten Sie die Seite [Schnellstart](/sonarr/quick-start-guide) konsultieren.

# Menüoptionen

Um zur Einstellungsseite zu gelangen, wählen Sie bitte "Einstellungen" im linken Menü aus. Die folgenden Untermenüoptionen stehen zur Verfügung:

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

Beachten Sie auch, dass für jede einzelne Einstellungsseite einige Optionen oben im Menü verfügbar sind:

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- "Erweitert ausblenden/zeigen" ist wichtig für alle Elemente, die unten als "(Erweiterte Option)" gekennzeichnet sind, da sie sonst nicht angezeigt werden. Diese Menüpunkte werden auf den Screenshots orange angezeigt.

- Sie müssen Ihre Änderungen speichern, bevor Sie den Bildschirm verlassen. Klicken Sie dazu auf das Disketten-Symbol. Wenn Sie keine Änderungen vorgenommen haben, wird "Keine Änderungen" angezeigt und ausgegraut, wie oben gezeigt.

# Medienverwaltung

> Einige dieser Einstellungen sind nur sichtbar, wenn Sie "Erweiterte Einstellungen anzeigen" aktivieren, das sich in der oberen Leiste unter der Suchleiste befindet{.is-info}

## Vorschläge zur Community-Namensgebung

> Nachfolgend finden Sie einige Vorschläge zur Community-Namensgebung von [TRaSH's Guides](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/){.is-info}

> Warnung: Ab Version v3.0.6.1431 unterstützt Sonarr jetzt die Erkennung von Dolby Vision (DV) und High Dynamic Range (HDR). Wenn Sie eine niedrigere Version verwenden, ersetzen Sie `{[MediaInfo VideoDynamicRangeType]}` durch `{[MediaInfoVideoDynamicRange]}`{.is-warning}

- Standardserie: `{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Tägliche Serie: `{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Anime-Serie: `{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- Staffelordner: `Staffel {season:00}`

- Mehrere Episodenstile: `Szene`

- Serienordner: `{Series TitleYear} [imdb-{ImdbId}]`

## Episodenbenennung

- Episoden umbenennen - Aktivieren Sie diese Option, um Sonarr das Umbenennen von Dateien zu ermöglichen.
  - Wenn nicht aktiviert:
    - Import durch Download-Client
      - Nicht-Staffelpaket: Der Titel der Veröffentlichung des Download-Clients wird verwendet.
      - Staffelpaket: Originaldateiname
    - Manueller (Ad-hoc-)Import: Originaldateiname

- Unerlaubte Zeichen ersetzen - Wenn nicht aktiviert, entfernt Sonarr sie stattdessen.
  - Die Zeichen sind: `:` `\` `/` `>` `<` `?` `*` `|` `"`

### Standard-Episodenformat

Standard-Episodenformat - Legen Sie die Benennungskonvention für Ihre Standard-Serientyp-Episoden fest. Klicken Sie auf das `?`-Symbol, um den Dialog "Dateinamens-Token" aufzurufen.

- Dropdown-Menü (obere rechte Ecke)
  - Linkes Feld - Leerzeichenbehandlung
  - Leerzeichen ( ) - Verwenden Sie Leerzeichen in der Benennung (Standard)
  - Punkt (.) - Verwenden Sie Punkte anstelle von Leerzeichen in der Benennung
  - Unterstrich (_) - Verwenden Sie Unterstriche anstelle von Leerzeichen in der Benennung
  - Bindestrich (-) - Verwenden Sie Bindestriche anstelle von Leerzeichen in der Benennung
  - Rechtes Feld - Groß-/Kleinschreibung
  - Standardfall - Titel groß- und kleinschreiben (~camel-case) (Standard)
  - Großbuchstaben - Titel komplett in Großbuchstaben
  - Kleinbuchstaben - Titel komplett in Kleinbuchstaben

### Serienbenennung

- `{Series Title}` = Der Titel der Serie!
- `{Series CleanTitleYear}` = Der Titel der Serie! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Der Titel der Serie!
- `{Series TitleThe}` = Serientitel!, Der
- `{Series TitleYear}` = Der Titel der Serie (2010)
- `{Series Year}` = (2010)

### Serien-IDs

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### Staffeln

- `{season:0}` = 1
- `{season:00}` =  01

### Episoden

- `{episode:0}` = 1
- `{episode:00}` = 01

### Ausstrahlungsdatum

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### Episodentitel

- `{Episode Title}` = Episodentitel
- `{Episode CleanTitle}` =  Episodentitel

### Qualität

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Medieninformationen

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguagesAll}` = \[DE\]
- `{MediaInfo AudioLanguagesAll}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`, `AudioLanguages` und `SubtitleLanguages` unterstützen einen Suffix `:EN+DE`, mit dem Sie die in den Dateinamen aufgenommenen Sprachen filtern können. Verwenden Sie `-DE`, um bestimmte Sprachen auszuschließen. Durch Anhängen von <kb>+</kb> (z. B.: `:EN+`) wird `[EN]`, `[EN+--]` oder `[--]` je nach ausgeschlossenen Sprachen ausgegeben. Verwenden Sie beispielsweise `{MediaInfo Full:EN+DE}`.
{.is-info}

> `AudioLanguages` zeigt keine Sprache für Audio an, wenn nur eine Sprache vorhanden ist und es sich um EN (Englisch) handelt. Um das gewünschte Verhalten zu erhalten und beispielsweise Deutsch und Englisch anzuzeigen, verwenden Sie stattdessen {MediaInfo AudioLanguagesAll:DE+EN}.
{.is-info}

> `MediaInfo VideoDynamicRangeType` gibt mögliche Werte zurück: DV, DV HDR10, HDR10, HDR10Plus, HLG, PQ und HDR
{.is-info}

### Sonstiges

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL oder NF

> \* Preferred Words sind das Wort oder die Wörter, die den wörtlichen Übereinstimmungen aller bevorzugten Wörter entsprechen. Das obige Beispiel wäre ein bevorzugtes Wort `iNTERNAL` oder ähnlich ein bevorzugtes Wort `/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i` würde `AMZN` oder `Amazon` zurückgeben.
\* `{Preferred Words:<Release Profile Name>}` ist eine zusätzliche Option, um Übereinstimmungen nur aus bestimmten Freigabeprofilen zu verwenden.
{.is-info}

### Original

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> `Original Title` ist der Veröffentlichungsname und es wird empfohlen, ihn zu verwenden.
{.is-info}

>`Original Filename` wird nicht empfohlen. Es ist der wörtliche Originaldateiname und kann verschleiert sein `t1i0p3s7i8yu7ti`.
{.is-warning}

## Tägliches Episodenformat

Tägliches Episodenformat - Legen Sie die Benennungskonvention für Ihre täglichen Serientyp-Episoden fest. Klicken Sie auf das `?`-Symbol, um den Dialog "Dateinamens-Token" aufzurufen.

Weitere Informationen zu diesem Dialogfeld finden Sie unter [Standard-Episodenformat](/sonarr/settings#standard-episode-format).

## Anime-Episodenformat

Anime-Episodenformat - Legen Sie die Benennungskonvention für Ihre Anime-Serientyp-Episoden fest. Klicken Sie auf das `?`-Symbol, um den Dialog "Dateinamens-Token" aufzurufen.

Weitere Informationen zu diesem Dialogfeld finden Sie unter [Standard-Episodenformat](/sonarr/settings#standard-episode-format).

### Absolute Episodennummer

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## Serienordnerformat

(Erweiterte Option) - Serienordner - Legen Sie die Benennungskonvention für den Ordner fest. Klicken Sie auf das `?`-Symbol, um den Dialog "Dateinamens-Token" aufzurufen.

### Serienbenennung

- `{Series Title}` = Serienname!
- `{Series CleanTitleYear}` = Serientitel 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Serientitel
- `{Series TitleThe}` = Serientitel, Der
- `{Series TitleYear}` = Serientitel (2010)
- `{Series Year}` = (2010)

### Serien-IDs

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## Staffelordnerformat

### Staffeln

- `{season:0}` = 1
- `{season:00}` = 01

## Staffelordnerformat

### Specials

Name für den Ordner "Specials" (Staffel)

- `Specials`

> Es wird empfohlen, "Specials" zu verwenden.
{.is-info}

## Mehrere Episodenstile

- `Erweitern` = `S01E01-02-03`
- `Duplizieren` = `S01E01.S01E01`
- `Wiederholen` = `S01E01E02E03`
- `Szene` = `S01E01-E02-E03`
- `Bereich` = `S01E01-03`
- `Präfixbereich` = `S01E01-E03`

> Es wird empfohlen, "Szene" zu verwenden.
{.is-info}

## Ordner

- Leere Medienordner erstellen - Erstellen Sie fehlende Serienordner während des Festplatten-Scans
- Leere Ordner löschen - Löschen Sie leere Serien- und Staffelordner während des Festplatten-Scans und wenn Episodendateien gelöscht werden

## Importieren

- **SDTV** - Standard Definition Television. This is the lowest quality available and typically has a resolution of 480i or 576i.
- **WEBDL-480p** - Web-DL release with a resolution of 480p. This is a digital copy of a TV show or movie that has been released online.
- **DVD** - DVD quality. This is the standard quality for DVDs and typically has a resolution of 480p.
- **HDTV-720p** - High Definition Television with a resolution of 720p. This is a digital broadcast of a TV show or movie.
- **WEBDL-720p** - Web-DL release with a resolution of 720p. This is a digital copy of a TV show or movie that has been released online.
- **BluRay-720p** - Blu-ray quality with a resolution of 720p. This is the standard quality for Blu-ray discs.
- **HDTV-1080p** - High Definition Television with a resolution of 1080p. This is a digital broadcast of a TV show or movie.
- **WEBDL-1080p** - Web-DL release with a resolution of 1080p. This is a digital copy of a TV show or movie that has been released online.
- **BluRay-1080p** - Blu-ray quality with a resolution of 1080p. This is the standard quality for Blu-ray discs.
- **WEBDL-2160p** - Web-DL release with a resolution of 2160p. This is a digital copy of a TV show or movie that has been released online in 4K resolution.
- **BluRay-2160p** - Blu-ray quality with a resolution of 2160p. This is the standard quality for Blu-ray discs in 4K resolution.

- Unknown - Selbsterklärend
- SDTV - Nach der Ausstrahlung von einer analogen Quelle (in der Regel Kabelfernsehen oder OTA-Standardauflösung) gerippt. Die Bildqualität ist im Allgemeinen gut (für die Auflösung) und sie werden in der Regel in DivX/XviD oder MP4 codiert.
- WEBDL-480p - WEB-DL (P2P) bezieht sich auf eine Datei, die verlustfrei von einem Streaming-Dienst wie Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer usw. gerippt oder über eine Online-Vertriebswebsite wie iTunes heruntergeladen wurde. Die Qualität ist ziemlich gut, da sie nicht neu codiert werden. Die Video- (H.264 oder H.265) und Audio- (AC3/AAC) Streams werden in der Regel aus iTunes oder Amazon Video extrahiert und ohne Qualitätsverlust in einen MKV-Container remuxed. Ein Vorteil dieser Veröffentlichungen ist, dass sie in der Regel keine Netzwerklogos auf dem Bildschirm haben, ähnlich wie BD/DVDRips. Diese sind fast so gut wie eine Blu-ray-Quelle, können aber unter Audioverzögerungen oder visuellen Artefakten aufgrund der adaptiven Bitrate von Streaming-Diensten leiden. Wenn die Internetverbindung eines Rippers auf einen Punkt fällt, an dem die Bitrate sinkt, kann sich die Quellen-Bitrate dynamisch ändern, was zu Variationen in der Bildqualität führen kann. Die meisten Veröffentlichungen, die unter extremen visuellen Artefakten leiden, werden NUKED und in der Regel wird ein PROPER veröffentlicht, um wilde Variationen in der adaptiven Bitrate zu beheben. Dies wird in 480p (SD) Qualität sein.
- WEBRip-480p - Bei einem WEB-Rip (P2P) wird die Datei oft mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 480p (SD) Qualität sein.
- DVD - Eine Neu-Codierung der endgültig veröffentlichten DVD9. Wenn möglich, wird dies PRE Retail veröffentlicht. Die Qualität sollte ausgezeichnet sein (für die Auflösung). DVDrips werden in der Regel in DivX/XviD oder MP4 veröffentlicht.
- Bluray-480p - Eine Neu-Codierung der endgültig veröffentlichten Blu-ray, herunterskaliert auf eine Auflösung von 480p (720x480 @ 16:9, jede andere Seitenverhältnis kann eine andere Auflösung haben). Wenn möglich, wird dies PRE Retail veröffentlicht. Die Qualität sollte für die Auflösung ausgezeichnet sein. Die Bitraten können variieren, aber diese werden in der Regel in DivX, XviD oder AVC codiert und bieten den Kompromiss einer geringfügigen wahrgenommenen Qualitätsminderung gegenüber der Originalquelle bei gleichzeitiger drastischer Reduzierung der Dateigröße. Diese sind in der Regel MKV oder MP4, aber es gibt auch einige DivX/XviD, die AVI verwenden.
- HDTV-720p - Eine Neu-Codierung der endgültig veröffentlichten Blu-ray, aber über HD-Kabel oder Satellit ausgestrahlt (1280x720 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Es kann für Laufzeit oder Inhalt je nach Netzwerk, von dem es stammt, modifiziert werden. Dies wird in der Regel mehrere Monate nach einer Retail-Veröffentlichung veröffentlicht, aber manchmal werden hochskalierte Versionen eines Films mit Standardauflösung auf Kabelkanälen wie STARZ oder HBO veröffentlicht, und sie wären die einzigen HD-Kopien dieses bestimmten Films. Diese sind in der Regel MKV oder MP4.
- HDTV-1080p - Eine Neu-Codierung der endgültig veröffentlichten Blu-ray, aber über HD-Kabel oder Satellit ausgestrahlt (1920x1080 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Es kann für Laufzeit oder Inhalt je nach Netzwerk, von dem es stammt, modifiziert werden. Dies wird in der Regel mehrere Monate nach einer Retail-Veröffentlichung veröffentlicht, aber manchmal werden hochskalierte Versionen eines Films mit Standardauflösung auf Kabelkanälen wie STARZ oder HBO veröffentlicht, und sie wären die einzigen HD-Kopien dieses bestimmten Films. Diese sind in der Regel MKV oder MP4-Container.
- Raw-HD - Ein Rohfeed eines HD-Streams.
- WEBRip-720p - Bei einem WEB-Rip (P2P) wird die Datei oft mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 720p Qualität sein.
- Bluray-720p - Eine Neu-Codierung der endgültig veröffentlichten Blu-ray, herunterskaliert auf eine Auflösung von 720p (1280x720 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Wenn möglich, wird dies PRE Retail veröffentlicht. Die Qualität sollte für die Auflösung ausgezeichnet sein. Die Bitraten können variieren, aber diese werden in der Regel in AVC oder HEVC codiert und bieten den Kompromiss einer geringfügigen wahrgenommenen Qualitätsminderung gegenüber der Originalquelle bei gleichzeitiger drastischer Reduzierung der Dateigröße. Diese sind in der Regel MKV oder MP4-Container.
- WEBDL-1080p - WEB-DL (P2P) bezieht sich auf eine Datei, die verlustfrei von einem Streaming-Dienst wie Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer usw. gerippt oder über eine Online-Vertriebswebsite wie iTunes heruntergeladen wurde. Die Qualität ist ziemlich gut, da sie nicht neu codiert werden. Die Video- (H.264 oder H.265) und Audio- (AC3/AAC) Streams werden in der Regel aus iTunes oder Amazon Video extrahiert und ohne Qualitätsverlust in einen MKV-Container remuxed. Ein Vorteil dieser Veröffentlichungen ist, dass sie in der Regel keine Netzwerklogos auf dem Bildschirm haben, ähnlich wie BD/DVDRips. Diese sind fast so gut wie eine Blu-ray-Quelle, können aber unter Audioverzögerungen oder visuellen Artefakten aufgrund der adaptiven Bitrate von Streaming-Diensten leiden. Wenn die Internetverbindung eines Rippers auf einen Punkt fällt, an dem die Bitrate sinkt, kann sich die Quellen-Bitrate dynamisch ändern, was zu Variationen in der Bildqualität führen kann. Die meisten Veröffentlichungen, die unter extremen visuellen Artefakten leiden, werden NUKED und in der Regel wird ein PROPER veröffentlicht, um wilde Variationen in der adaptiven Bitrate zu beheben. Dies wird in 1080p Qualität sein.
- WEBRip-1080p - Bei einem WEB-Rip (P2P) wird die Datei oft mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 1080p Qualität sein.
- Bluray-1080p - Eine Neu-Codierung der endgültig veröffentlichten Blu-ray, in ihrer nativen 1080p-Auflösung (1920x1080 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Wenn möglich, wird dies PRE Retail veröffentlicht. Die Qualität sollte ausgezeichnet sein und die gleiche Auflösung wie die Quelle haben. Die Bitraten können variieren, aber diese werden in der Regel in AVC oder HEVC codiert und bieten den Kompromiss einer geringfügigen wahrgenommenen Qualitätsminderung gegenüber der Originalquelle bei geringfügiger Reduzierung der Dateigröße. Diese sind in der Regel MKV oder MP4-Container.
- Remux-1080p - Ein Remux ist ein Rip einer Blu-ray- oder HD-DVD-Disc in ein anderes Containerformat oder das Entfernen der Disc von Menüs und Bonusmaterial, während die Inhalte ihrer Audio- und Videostreams intakt bleiben (auch die aktuellen Codecs beibehalten), was die exakte 1:1-Filmqualität wie auf der Original-Disc garantiert. Dies ist in 1080p Qualität.
- HDTV-2160p - TVRip ist eine Aufzeichnungsquelle von einer Aufnahmekarte. HDTV steht für aufgezeichnete Quelle aus HD-Fernsehen. Mit einer HDTV-Quelle kann die Qualität manchmal sogar die von DVDs übertreffen. Filme in diesem Format werden immer beliebter. Auf einigen Veröffentlichungen können Werbung und kommerzielle Banner während der Wiedergabe zu sehen sein. Dies ist in 2160p (4K) Qualität.
- WEBDL-2160p - WEB-DL (P2P) bezieht sich auf eine Datei, die verlustfrei von einem Streaming-Dienst wie Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer usw. gerippt oder über eine Online-Vertriebswebsite wie iTunes heruntergeladen wurde. Die Qualität ist ziemlich gut, da sie nicht neu codiert werden. Die Video- (H.264 oder H.265) und Audio- (AC3/AAC) Streams werden in der Regel aus iTunes oder Amazon Video extrahiert und ohne Qualitätsverlust in einen MKV-Container remuxed. Ein Vorteil dieser Veröffentlichungen ist, dass sie in der Regel keine Netzwerklogos auf dem Bildschirm haben, ähnlich wie BD/DVDRips. Diese sind fast so gut wie eine Blu-ray-Quelle, können aber unter Audioverzögerungen oder visuellen Artefakten aufgrund der adaptiven Bitrate von Streaming-Diensten leiden. Wenn die Internetverbindung eines Rippers auf einen Punkt fällt, an dem die Bitrate sinkt, kann sich die Quellen-Bitrate dynamisch ändern, was zu Variationen in der Bildqualität führen kann. Die meisten Veröffentlichungen, die unter extremen visuellen Artefakten leiden, werden NUKED und in der Regel wird ein PROPER veröffentlicht, um wilde Variationen in der adaptiven Bitrate zu beheben. Dies wird in 2160p (4K) Qualität sein.
- WEBRip-2160p - Bei einem WEB-Rip (P2P) wird die Datei oft mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 2160p (4K) Qualität sein.
- Bluray-2160p - Eine Neu-Codierung der endgültig veröffentlichten Blu-ray, in ihrer nativen 2160p-Auflösung (3840x2160 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). 4K-Versionen von Filmen, die in der Regel im HEVC-Codec vorliegen und entweder eine 8-Bit- oder 10-Bit-Farbwiedergabe oder von einer HDR-Quelle stammen. Die Bitraten können variieren, aber diese werden in der Regel in MKV oder MP4-Containern codiert.
- Remux-2160p - Ein Remux ist ein Rip einer Blu-ray- oder HD-DVD-Disc in ein anderes Containerformat oder das Entfernen der Disc von Menüs und Bonusmaterial, während die Inhalte ihrer Audio- und Videostreams intakt bleiben (auch die aktuellen Codecs beibehalten), was die exakte 1:1-Filmqualität wie auf der Original-Disc garantiert. Dies ist in 2160p (4K) Qualität.

# Indexer

> Informationen zu unterstützten Indexern finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/sonarr/supported#indexers) für diesen Abschnitt
{.is-info}

## Unterstützte Indexer

- Eine Liste der unterstützten Indexer finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/sonarr/supported#indexers)

### Indexer-Einstellungen

- Sobald Sie auf die Schaltfläche <kb>+</kb> geklickt haben, um einen neuen Indexer hinzuzufügen, wird ein neues Fenster mit vielen verschiedenen Optionen angezeigt. Für diese Wiki betrachtet Sonarr sowohl Usenet-Indexer als auch Torrent-Tracker als "Indexer".

- Es gibt zwei Abschnitte hier: Usenet und Torrents. Abhängig von dem Download-Client, den Sie verwenden werden, sollten Sie den Typ des Indexers auswählen.

### Usenet-Indexer-Konfiguration

- Newznab - Hier finden Sie Voreinstellungen für beliebte Usenet-Indexer (die vorausgefüllt sind, Sie benötigen nur Ihren API-Schlüssel, der vom Usenet-Indexer Ihrer Wahl bereitgestellt wird) sowie die Möglichkeit, einen benutzerdefinierten Indexer zu erstellen.
- Software, die gut mit Usenet zusammenarbeitet und gut in Sonarr integriert ist, sind [NZBHydra2](https://github.com/theotherp/nzbhydra2/) oder [Prowlarr](/prowlarr), die sowohl Usenet als auch Torrents integrieren.
- Unabhängig davon, ob Sie einen vorausgefüllten Indexer oder eine benutzerdefinierte Indexer-Konfiguration auswählen, wird ein neues Fenster angezeigt, in dem Sie alle Ihre Einstellungen eingeben können.
- Wählen Sie aus den Voreinstellungen oder fügen Sie einen benutzerdefinierten Indexer hinzu (wie z.B. NZBHydra2 oder Prowlarr)
- Name - Der Name des Indexers in Sonarr
- RSS aktivieren - Wenn aktiviert, verwenden Sie diesen Indexer, um nach Dateien zu suchen, die gewünscht und fehlend oder noch nicht ihren Abschneidepunkt erreicht haben.
- Automatische Suche aktivieren - Wenn aktiviert, verwenden Sie diesen Indexer für automatische Suchen, einschließlich Suche beim Hinzufügen
- Interaktive Suche aktivieren - Wenn aktiviert, verwenden Sie diesen Indexer für manuelle interaktive Suchen.
- URL - Die vom Indexer bereitgestellte URL des Indexers, z.B. `https://api.nzbgeek.info`.
- API-Pfad - Der vom Indexer bereitgestellte Pfad zur API. Dies ist in der Regel `/api`
- API-Schlüssel - Der vom Indexer bereitgestellte Schlüssel zum Zugriff auf die API.
- Kategorien - Standardkategorien werden verwendet, es sei denn, sie werden bearbeitet. Wahrscheinlich sind diese Standardkategorien nicht optimal. Beim Bearbeiten dieser Einstellung fragt Sonarr den Indexer nach seinen verfügbaren Kategorien und zeigt sie in einer auswählbaren Liste an. Die veralteten Standardeinstellungen werden gelöscht, sobald eine Kategorie umgeschaltet wird.
- Anime-Kategorien - Die Kategorien, die Sonarr für Anime-Suchen verwendet. Es werden keine Kategorien verwendet, es sei denn, sie werden bearbeitet. Beim Bearbeiten dieser Einstellung fragt Sonarr den Indexer nach seinen verfügbaren Kategorien und zeigt sie in einer auswählbaren Liste an. Die veralteten Standardeinstellungen werden gelöscht, sobald eine Kategorie umgeschaltet wird.
- Anime Standard Format Suche - Suche auch nach Anime mit der Standardnummerierung (gilt nur für Anime-Serientypen) [Weitere Informationen zu Serientypen finden Sie hier](/sonarr/faq#whats-the-different-series-types)
- (Erweiterte Option) Zusätzliche Parameter - Zusätzliche Newznab-Parameter, die dem Abfrage-Link hinzugefügt werden sollen
- (Erweiterte Option) Indexer-Priorität - Priorität dieses Indexers, um einen Indexer einem anderen in Release-Tiebreaker-Szenarien vorzuziehen. 1 ist höchste Priorität und 50 ist niedrigste Priorität.
- (Erweiterte Option) Download-Client - Wählen und geben Sie an, welcher Download-Client für Downloads von diesem Indexer verwendet wird
- Tags - Verwenden Sie diesen Indexer nur für Serien mit mindestens einem passenden Tag. Lassen Sie das Feld leer, um ihn für alle Serien zu verwenden.

### Torrent-Tracker-Konfiguration

- Wie bei Usenet gibt es eine Vielzahl von vorausgefüllten Torrent-Tracker-Informationen. Wenn Sie kein Mitglied dieser spezifischen Tracker sind, werden sie Ihnen nichts nützen.
- Eine der besten und einfachsten Möglichkeiten, Torrent-Tracker zu nutzen, die von Sonarr nicht nativ unterstützt werden, besteht darin, ein zweites Programm wie [Prowlarr](/prowlarr) oder [Jackett](https://github.com/Jackett/Jackett) zu verwenden. Diese Software funktionieren gut mit Sonarr als Suchindexer, der alle Ihre Informationen enthält und sie an Sonarr sendet.
- Torznab - Diese Option richtet Sie mit einer Jackett-Voreinstellung ein. Wenn Sie mehrere Tracker verwenden, müssen Sie sicherstellen, dass jeder Eintrag einen eindeutigen Namen hat.
- Torznab-Indexer
- Wählen Sie aus den Voreinstellungen oder fügen Sie einen benutzerdefinierten Indexer hinzu (wie z.B. Jackett oder Prowlarr)
- Name - Der Name des Indexers in Sonarr
- RSS aktivieren - Wenn aktiviert, verwenden Sie diesen Indexer, um nach Dateien zu suchen, die gewünscht und fehlend oder noch nicht ihren Abschneidepunkt erreicht haben.
- Automatische Suche aktivieren - Wenn aktiviert, verwenden Sie diesen Indexer für automatische Suchen, einschließlich Suche beim Hinzufügen
- Interaktive Suche aktivieren - Wenn aktiviert, verwenden Sie diesen Indexer für manuelle interaktive Suchen.
- URL - Die vom Indexer bereitgestellte URL, z.B. `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-Pfad - Der vom Indexer bereitgestellte Pfad zur API. Dies ist in der Regel `/api`
- API-Schlüssel - Der vom Indexer bereitgestellte Schlüssel zum Zugriff auf die API.
- Kategorien - Standardkategorien werden verwendet, es sei denn, sie werden bearbeitet. Wahrscheinlich sind diese Standardkategorien nicht optimal. Beim Bearbeiten dieser Einstellung fragt Sonarr den Indexer nach seinen verfügbaren Kategorien und zeigt sie in einer auswählbaren Liste an. Die veralteten Standardeinstellungen werden gelöscht, sobald eine Kategorie umgeschaltet wird.
- Anime-Kategorien - Die Kategorien, die Sonarr für Anime-Suchen verwendet. Es werden keine Kategorien verwendet, es sei denn, sie werden bearbeitet. Beim Bearbeiten dieser Einstellung fragt Sonarr den Indexer nach seinen verfügbaren Kategorien und zeigt sie in einer auswählbaren Liste an. Die veralteten Standardeinstellungen werden gelöscht, sobald eine Kategorie umgeschaltet wird.
- Anime Standard Format Suche - Suche auch nach Anime mit der Standardnummerierung (gilt nur für Anime-Serientypen) [Weitere Informationen zu Serientypen finden Sie hier](/sonarr/faq#whats-the-different-series-types)
- (Erweiterte Option) Zusätzliche Parameter - Zusätzliche Torznab-Parameter, die dem Abfrage-Link hinzugefügt werden sollen
- (Erweiterte Option) Mindestanzahl an Seedern - Die Mindestanzahl an Seedern, die für einen Release von diesem Tracker erforderlich ist, um ihn herunterzuladen.
- (Erweiterte Option) Seed-Verhältnis - Wenn leer, wird der Standardwert des Download-Clients verwendet. Andernfalls ist das Mindest-Saatverhältnis erforderlich, das Ihr Download-Client für Releases von diesem Indexer erfüllen muss, bevor es von Ihrem Client angehalten und von Sonarr entfernt wird (erfordert abgeschlossene Download-Verarbeitung - Entfernen aktiviert)
- (Erweiterte Option) Seed-Zeit - Wenn leer, wird der Standardwert des Download-Clients verwendet. Andernfalls ist die Mindest-Saatzeit in Minuten erforderlich, die Ihr Download-Client für Releases von diesem Indexer erfüllen muss, bevor es von Ihrem Client angehalten und von Sonarr entfernt wird (erfordert abgeschlossene Download-Verarbeitung - Entfernen aktiviert)
- (Erweiterte Option) Indexer-Priorität - Priorität dieses Indexers, um einen Indexer einem anderen in Release-Tiebreaker-Szenarien vorzuziehen. 1 ist höchste Priorität und 50 ist niedrigste Priorität.
- (Erweiterte Option) Download-Client - Wählen und geben Sie an, welcher Download-Client für Downloads von diesem Indexer verwendet wird
- Tags - Verwenden Sie diesen Indexer nur für Serien mit mindestens einem passenden Tag. Lassen Sie das Feld leer, um ihn für alle Serien zu verwenden.

## Optionen

- Mindestalter - Nur Usenet: Mindestalter in Minuten von NZBs, bevor sie heruntergeladen werden. Verwenden Sie dies, um neuen Veröffentlichungen Zeit zu geben, sich auf Ihrem Usenet-Anbieter zu verbreiten.
- Vorhaltung - Nur Usenet: Auf Null setzen, um unbegrenzte Vorhaltung einzustellen
- Maximale Größe - Maximale Größe für einen Release, der heruntergeladen werden soll, in MB. Auf Null setzen, um unbegrenzte Größe einzustellen. Bitte beachten Sie, dass dies global gilt.
- RSS-Synchronisierungsintervall - Intervall in Minuten. Auf Null setzen, um zu deaktivieren (dadurch werden alle automatischen Release-Downloads gestoppt) Minimum: 10 Minuten Maximum: 120 Minuten
  - Bitte lesen Sie [Wie findet Sonarr Episoden?](/sonarr/faq#how-does-sonarr-find-episodes) für ein besseres Verständnis, wie RSS-Synchronisierung Ihnen helfen wird

> Wenn Sonarr für eine längere Zeit offline war, wird Sonarr versuchen, zurückzublättern, um die letzte Veröffentlichung zu finden, die es verarbeitet hat, um zu vermeiden, dass eine Veröffentlichung verpasst wird. Solange Ihr Indexer das Blättern unterstützt und es nicht zu lange gedauert hat, wird Sonarr in der Lage sein, die Veröffentlichungen zu verarbeiten, die es verpasst hätte, und vermeiden, dass Sie nach den verpassten Veröffentlichungen suchen müssen.{.is-info}

# Download-Clients

> Informationen zu unterstützten Download-Clients finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/sonarr/supported#download-clients) für diesen Abschnitt
{.is-info}

## Übersicht

- Das Herunterladen und Importieren ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss die Software in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Setups. Das bedeutet, dass es zwar einige gemeinsame Setups gibt, aber es gibt kein einziges richtiges Setup und jedes Setup kann ein wenig anders sein. Aber es gibt viele falsche Setups.

## Download-Client-Prozesse

## Usenet

- Sonarr wird eine Download-Anfrage an Ihren Client senden und sie mit einem von Ihnen in den Einstellungen des Download-Clients konfigurierten Label- oder Kategorienamen verknüpfen.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Sonarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Sonarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich separat von Ihrem Medienordner befindet und von Sonarr zugänglich ist.
- Sonarr durchsucht diesen abgeschlossenen Dateispeicherort nach Dateien, die Sonarr verwenden kann. Es analysiert den Dateinamen, um ihn mit den angeforderten Medien abzugleichen. Wenn dies möglich ist, benennt es die Datei gemäß Ihren Spezifikationen um und verschiebt sie an den angegebenen Medienort.
- Atomare Verschiebungen (sofortige Verschiebungen) sind standardmäßig aktiviert. Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek gleich sein. Wenn die atomare Verschiebung fehlschlägt oder Ihre Konfiguration keine Hardlinks und atomare Verschiebungen unterstützt, wird Sonarr auf das Kopieren der Datei zurückgreifen und sie dann aus der Quelle löschen, was eine hohe E/A-Auslastung bedeutet.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Sonarr-Einstellungen aktiviert ist, werden übrig gebliebene Dateien aus dem Download an Ihren Papierkorb oder Recycling-Bin gesendet, indem eine Anfrage an Ihren Client gesendet wird, um die Veröffentlichung zu löschen/entfernen.

## BitTorrent

- Sonarr wird eine Download-Anfrage an Ihren Client senden und sie mit einem von Ihnen in den Einstellungen des Download-Clients konfigurierten Label- oder Kategorienamen verknüpfen.
  - Beispiele: Filme, TV, Serien, Musik usw.
- Sonarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
- Abgeschlossene Dateien bleiben an ihrem ursprünglichen Speicherort, um das Seeden der Datei zu ermöglichen (Verhältnis oder Zeit kann im Download-Client oder innerhalb von Sonarr unter dem spezifischen Download-Client angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, wird Sonarr die Datei per Hardlink verknüpfen, sofern dies von Ihrer Konfiguration unterstützt wird, oder sie kopieren, wenn Hardlinks nicht unterstützt werden.
- Hardlinks sind standardmäßig aktiviert. [Ein Hardlink benötigt keinen zusätzlichen Speicherplatz.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek gleich sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihre Konfiguration keine Hardlinks unterstützt, wird Sonarr auf das Kopieren der Datei zurückgreifen.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Sonarr-Einstellungen aktiviert ist, wird Sonarr den Torrent aus Ihrem Client löschen und den Client auffordern, die Torrent-Daten zu entfernen, aber nur, wenn der Client meldet, dass das Seeden abgeschlossen ist und der Torrent gestoppt ist (nach Abschluss pausiert).

## Download-Clients

Klicken Sie auf `Einstellungen` => `Download-Clients` und klicken Sie dann auf das <kb>+</kb>, um einen neuen Download-Client hinzuzufügen. Ihr Download-Client sollte bereits konfiguriert und aktiv sein.

### Unterstützte Download-Clients

- Eine Liste der unterstützten Download-Clients finden Sie auf der [Weitere Informationen (Unterstützte)](/sonarr/supported#download-clients) Seite

Wählen Sie den Download-Client aus, den Sie hinzufügen möchten, und es wird ein Popup-Fenster angezeigt, in dem Sie die Verbindungsdetails eingeben können. Diese Details sind für die meisten Clients ähnlich. Einige fragen nach einem Benutzernamen oder Passwort, andere fragen, ob neue Downloads im pausierten/Startzustand hinzugefügt werden sollen, usw.

### Usenet-Client-Einstellungen

- Name - Der Name des Download-Clients in Sonarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients; dies ist in der Regel der WebGUI-Port
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- (Erweiterte Option) URL-Basis - Ein Präfix zur URL hinzufügen; dies ist häufig für Reverse Proxies erforderlich.
- API-Schlüssel - Der API-Schlüssel zur Authentifizierung bei Ihrem Client
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Kategorie - Die Kategorie in Ihrem Download-Client, die von \*Arr verwendet wird. Um nicht verwandte Downloads in der Aktivität zu vermeiden, wird dringend empfohlen, eine Kategorie festzulegen.
- Kürzliche Priorität - Download-Client-Priorität für kürzlich veröffentlichte Medien
- Ältere Priorität - Download-Client-Priorität für nicht kürzlich veröffentlichte Medien
- (Erweiterte Option) Client-Priorität - Priorität des Download-Clients. Round-Robin wird für Clients desselben Typs (Torrent/Usenet) verwendet, die dieselbe Priorität haben. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität
- Abgeschlossene Download-Verarbeitung
  - Entfernen (Pro Client-Einstellung) - Abgeschlossene Downloads entfernen, wenn sie fertig sind (Usenet) oder gestoppt/vollständig (Torrents). Weitere Informationen finden Sie unter [Abgeschlossene Download-Verarbeitung](#abgeschlossene-download-verarbeitung)

### Torrent-Client-Einstellungen

- Name - Der Name des Download-Clients in Sonarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- (Erweiterte Option) URL-Basis - Ein Präfix zur URL hinzufügen; dies ist häufig für Reverse Proxies erforderlich.
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client
- Kategorie - Die Kategorie in Ihrem Download-Client, die von \*Arr verwendet wird. Um nicht verwandte Downloads in der Aktivität zu vermeiden, wird dringend empfohlen, eine Kategorie festzulegen.
- Nach dem Import Kategorie - Die Kategorie, die nach dem Herunterladen und Importieren der Veröffentlichung festgelegt werden soll. Bitte beachten Sie, dass dies die Entfernung der abgeschlossenen Download-Verarbeitung unterbricht.
- Kürzliche Priorität - Download-Client-Priorität für kürzlich veröffentlichte Medien
- Ältere Priorität - Download-Client-Priorität für nicht kürzlich veröffentlichte Medien
- Anfangszustand - Anfangszustand für Torrents (nur Qbittorrent: Erzwingt das Überspringen aller Seed-Schwellenwerte)
- (Erweiterte Option) Client-Priorität - Priorität des Download-Clients. Round-Robin wird für Clients desselben Typs (Torrent/Usenet) verwendet, die dieselbe Priorität haben. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität
- Abgeschlossene Download-Verarbeitung
  - Entfernen (Pro Client-Einstellung) - Abgeschlossene Downloads entfernen, wenn sie fertig sind (Usenet) oder gestoppt/vollständig (Torrents). Weitere Informationen finden Sie unter [Abgeschlossene Download-Verarbeitung](#abgeschlossene-download-verarbeitung)
    - Bei Torrents muss Ihr Download-Client pausieren, wenn die Seed-Ziele erreicht sind. Es erfordert auch, dass die Seed-Ziele von Sonarr gemäß der unten stehenden Tabelle unterstützt werden. Torrents müssen auch in derselben Kategorie bleiben.

### Kompatibilität der Torrent-Client-Entfernung des Downloads

- Sonarr kann nur das Seed-Verhältnis/die Seed-Zeit bei Clients festlegen, die das Festlegen dieses Werts über ihre API unterstützen, wenn das Torrent hinzugefügt wird. Seed-Ziele können global im Client selbst oder pro Tracker in den \*Arr-Einstellungen für jeden Indexer festgelegt werden. In der folgenden Tabelle finden Sie Informationen zur Kompatibilität der Clients.

|      Client       |                                Verhältnis                                |                                   Zeit                                   |
| :---------------: | :---------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|      Deluge       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
| Download Station  | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|       Flood       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
|     Hadouken      | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|    qBittorrent    |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
|     rTorrent      |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
| Torrent Blackhole | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |   ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)   |
|   Transmission    |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Unterstützt-Idle%20Limit*-blue) |
|     uTorrent      |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |
|       Vuze        |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |     ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Unterstützt-Idle%20Limit*-blue) - Transmission hat intern eine Überprüfung der Leerlaufzeit, aber Sonarr vergleicht sie mit der Seed-Zeit, wenn das Leerlauf-Limit auf Basis einzelner Torrents festgelegt ist. Dies geschieht als Workaround für die API-Beschränkungen von Transmission.{.is-info}

## Abgeschlossene Download-Verarbeitung

- Die abgeschlossene Download-Verarbeitung ist der Vorgang, wie Sonarr Medien von Ihrem Download-Client in Ihre Serienordner importiert. Viele häufige Probleme hängen mit falschen Docker-Pfaden und/oder anderen Docker-Berechtigungsproblemen zusammen.

- (Erweiterte globale Einstellung) Aktivieren - Abgeschlossene Downloads automatisch aus dem Download-Client importieren
- (Pro Client-Einstellung) Entfernen - Abgeschlossene Downloads entfernen, wenn sie fertig sind (Usenet) oder gestoppt/vollständig (Torrents)
  - Bei Torrents muss Ihr Download-Client pausieren, wenn die Seed-Ziele erreicht sind. Es erfordert auch, dass die Seed-Ziele von Sonarr gemäß der obigen Tabelle unterstützt werden. Torrents müssen auch in derselben Kategorie bleiben.

### Abgeschlossene Downloads entfernen

- Sonarr wird eine Download-Anfrage an Ihren Client senden und sie mit einem von Ihnen in den Einstellungen des Download-Clients konfigurierten Label- oder Kategorienamen verknüpfen.
- Sonarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Sonarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich separat von Ihrem Medienordner befindet.
- Sonarr durchsucht diesen abgeschlossenen Dateispeicherort nach Videodateien. Es analysiert den Videodateinamen, um ihn mit einer Episode abzugleichen. Wenn dies möglich ist, benennt es die Datei gemäß Ihren Spezifikationen um und verschiebt sie an den zugewiesenen Bibliotheksordner.
- Übrig gebliebene Dateien aus dem Download werden in Ihren Papierkorb oder Recycling-Bin gesendet.

Wenn Sie mit einem BitTorrent-Client herunterladen, ist der Vorgang etwas anders:

- Abgeschlossene Dateien bleiben an ihrem ursprünglichen Speicherort, um das Seeden zu ermöglichen. Wenn Dateien in Ihren zugewiesenen Bibliotheksordner importiert werden, wird Sonarr versuchen, die Datei per Hardlink zu verknüpfen, oder bei Nichtunterstützung von Hardlinks auf das Kopieren (doppelte Speicherplatznutzung) zurückgreifen.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen aktiviert ist, wird Sonarr den Torrent-Client auffordern, die Originaldatei und den Torrent zu löschen, aber dies geschieht nur, wenn der Client meldet, dass das Seeden abgeschlossen ist, der Torrent sich in derselben Kategorie befindet (d. h. keine Verwendung einer Post-Import-Kategorie), das Seed-Ziel von Sonarr unterstützt wird und der Torrent pausiert (gestoppt) ist.

### Fehlgeschlagene Download-Verarbeitung

- Die fehlgeschlagene Download-Verarbeitung ist nur mit SABnzbd und NZBGet kompatibel.
- Die fehlgeschlagene Download-Verarbeitung gilt nicht für Torrents und es sind keine Pläne vorhanden, eine solche Funktionalität hinzuzufügen.

- Die fehlgeschlagene Download-Verarbeitung besteht aus mehreren Komponenten:

- Überprüfung des Downloaders:
  - Warteschlange - Überprüfen Sie die Warteschlange Ihres Downloaders auf passwortgeschützte (verschlüsselte) Veröffentlichungen, die als Fehler markiert sind
  - Verlauf - Überprüfen Sie den Verlauf Ihres Downloaders auf Fehler (z. B. nicht genügend Blöcke zur Reparatur oder Extraktion fehlgeschlagen)
- Wenn Sonarr einen fehlgeschlagenen Download findet, beginnt es mit der Verarbeitung und führt einige Aktionen aus:
  - Fügt ein fehlgeschlagenes Ereignis zum Verlauf von Sonarr hinzu
  - Entfernt den fehlgeschlagenen Download aus dem Download-Client, um Speicherplatz freizugeben und heruntergeladene Dateien zu löschen (optional)
  - Beginnt mit der Suche nach einer Ersatzdatei (optional)
  - Blocklistung (ehemals 'Blacklisting') ermöglicht das automatische Überspringen von NZBs, wenn sie fehlschlagen. Das bedeutet, dass das NZB von Sonarr nie automatisch heruntergeladen wird (Sie können den Download jedoch über eine manuelle Suche erzwingen).
  - Es gibt 2 erweiterte Optionen (auf der Seite "Download-Client" Einstellungen), die das Verhalten der fehlgeschlagenen Downloads in Sonarr steuern. Derzeit sind sie alle standardmäßig aktiviert.

- Erneut herunterladen - Steuert, ob Sonarr nach einem Fehler nach derselben Datei sucht
- (Erweiterte Option) Entfernen - Ob der Download automatisch aus dem Download-Client entfernt werden soll, wenn der Fehler erkannt wird

## Remote-Pfadzuordnungen

- Remote-Pfadzuordnung fungiert als einfache Suche nach Remote-Pfad und Ersetzung durch lokalen Pfad. Dies wird hauptsächlich für gemischte lokale/Remote-Setups mit MergerFS oder ähnlichem verwendet oder wenn die Anwendung und der Download-Client nicht auf demselben Server sind.
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht auf diesen Ordner verweist.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft, während \*Arr auf Windows oder umgekehrt läuft. Eine Remote-Pfadzuordnung ist auch möglicherweise erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine EINFACHE Suche/Ersetzung (wenn der REMOTE-Wert gefunden wird, wird er durch den LOCAL-Wert für den angegebenen Host ersetzt).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie in TRaSH's Tutorial](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist eine Remote-Pfadzuordnung selten erforderlich. Es wird empfohlen, [den Docker-Leitfaden](/docker-guide) zu überprüfen und/oder [TRaSH's Tutorial](https://trash-guides.info/hardlinks) zu befolgen.{.is-info}

# Import-Listen

> Informationen zu unterstützten Listentypen finden Sie auf der [Weitere Informationen (Unterstützte)](/sonarr/supported#lists) Seite für diesen Abschnitt
{.is-info}

## Listen

- Import-Listen sind ein Teil von Sonarr, mit denen Sie einem bestimmten Listen-Ersteller folgen können. Angenommen, Sie folgen einem bestimmten Listen-Ersteller auf Trakt/TMDb und mögen ihren ArrowVerse Collection-Bereich und möchten jede Show auf ihrer Liste sehen. Sie schauen in Ihrem Sonarr nach und stellen fest, dass Sie diese Serien nicht haben. Anstatt einzeln zu suchen und diese Elemente hinzuzufügen und dann Ihre Indexer nach diesen Serien zu durchsuchen, können Sie dies alles auf einmal mit einer Liste tun. Die Listen können so eingestellt werden, dass alle Serien auf der Liste des Kurators importiert werden und automatisch ein Qualitätsprofil zugewiesen, automatisch hinzugefügt und automatisch überwacht werden.

- VORSICHT: Wenn Listen falsch gemacht werden, werden sie Ihre Bibliothek mit einer Menge Müll, den Sie nicht sehen möchten, zerstören. Stellen Sie also sicher, dass Sie wissen, was Sie importieren, bevor Sie auf Speichern klicken. D.h. schauen Sie sich die Liste an, bevor Sie überhaupt zu Sonarr gehen.

- Hier können Sie auf die Schaltfläche <kb>+</kb> klicken, um ein neues Popup-Fenster zu öffnen.
- In diesem neuen Fenster werden Ihnen viele verschiedene Optionen angezeigt, um Ihre Liste von vielen verschiedenen Listenanbietern einzurichten. Wie bereits erwähnt, seien Sie vorsichtig bei der Verwendung von Listen. Es wird dringend empfohlen, die Option "Bei Hinzufügen suchen" nicht auszuwählen, bevor Sie sicher sind, dass die Liste, die Sie auswählen/einrichten, die Serien hinzufügt, die Sie suchen.
- Sobald Sie den Listenanbieter ausgewählt haben, von dem Sie ziehen möchten (wie IMDb oder Trakt), wird Ihnen ein neues Fenster angezeigt.
Die meisten Einstellungen der Listen sind ziemlich selbsterklärend, einige Listen erfordern eine Authentifizierung beim Anbieter wie Trakt (dafür ist ein Konto bei Trakt.tv erforderlich).

- Import-Listenausschluss - Dies ermöglicht es Ihnen, Ihre Liste von Serien zu bereinigen, die Sie nicht mehr sehen möchten. Ein Beispiel dafür ist, wenn Ihre Liste zufällig eine Serie enthält, die in einer Fremdsprache ist und es unwahrscheinlich ist, dass Sie diesen Film jemals in Ihrer Muttersprache finden und ihn nicht mit Untertiteln sehen möchten. Sie können eine Serie ausschließen, damit sie in Zukunft nicht mehr hinzugefügt wird. In der Sektion "Listenausschluss" können Sie sie jedoch wieder zur Liste hinzufügen, damit sie beim erneuten Ausführen der Liste in Ihre Bibliothek eingelesen wird.

# Verbindung

> Informationen zu unterstützten Verbindungstypen finden Sie auf der [Weitere Informationen (Unterstützt)](/sonarr/supported#notifications)-Seite für diesen Abschnitt
{.is-info}

## Verbindungen

- Verbindungen sind die Art und Weise, wie Sie möchten, dass Sonarr mit der Außenwelt kommuniziert.

- Durch Drücken der <kb>+</kb>-Taste wird ein neues Fenster geöffnet, in dem Sie viele verschiedene Endpunkte konfigurieren können.

- Eine Liste der unterstützten Benachrichtigungen und Verbindungen finden Sie unter [Weitere Informationen (Unterstützt)](/sonarr/supported#notifications)

## Verbindungsauslöser

- Bei Grab - Benachrichtigung, wenn Episoden zum Download verfügbar sind und an einen Download-Client gesendet wurden
- Bei Import - {Ehemals bekannt als Bei Download} Benachrichtigung, wenn Episoden erfolgreich importiert wurden
- Bei Upgrade - Benachrichtigung, wenn Episoden auf eine bessere Qualität aktualisiert wurden
- Bei Umbenennung - Benachrichtigung, wenn Episoden umbenannt werden
- Bei Serienlöschung - Benachrichtigung, wenn Serien gelöscht werden
- Bei Löschung der Episodendatei - Benachrichtigung, wenn Episodendateien gelöscht werden
- Bei Löschung der Episodendatei für Upgrade - Benachrichtigung, wenn Episodendateien für Upgrades gelöscht werden
- Bei Problemen mit der Gesundheit - Benachrichtigung bei Fehlern bei der Gesundheitsprüfung
  - Gesundheitswarnungen einschließen - Benachrichtigung bei Gesundheitswarnungen zusätzlich zu Fehlern.
- Bei Anwendungsupdate - Benachrichtigung, wenn Sonarr auf eine neue Version aktualisiert wird

# Metadaten

## Metadaten

> Informationen zu unterstützten Metadaten-Verbrauchern finden Sie auf der [Weitere Informationen (Unterstützt)](/sonarr/supported#metadata)-Seite für diesen Abschnitt
{.is-info}

- Hier können Sie den Typ der Metadaten auswählen, die von Ihrem Media Player verwendet werden sollen

- Kodi wird hier eine der am häufigsten verwendeten Optionen sein, wenn diese Software verwendet wird. Dadurch kann Sonarr eine NFO-Datei erstellen und zugehörige Filmplakate in Ihren Player einlesen

# Tags

- Der Tag-Bereich in Sonarr wird verwendet, um verschiedene Aspekte von Sonarr miteinander zu verknüpfen.
- Tags sind besonders nützlich für:
  - Verzögerungsprofile
  - Freigabeprofile
  - Indexer
- Tags können verwendet werden, um Verzögerungsprofile, Freigabeprofile, Indexer und Serien miteinander zu verknüpfen.
- Zum Beispiel:
  - Sie möchten, dass ein bestimmter Indexer nur für eine bestimmte Serie verwendet wird. Sie würden einen Tag erstellen und der Serie und dem Indexer diesen Tag zuweisen.
  - Sie möchten, dass ein bestimmtes Freigabeprofil nur ein bestimmtes Verzögerungsprofil verwendet. Sie würden einen Tag erstellen und dem Freigabeprofil und dem Verzögerungsprofil diesen Tag zuweisen.

> Eine Serie verwendet sowohl Indexer mit passenden Tags als auch Indexer ohne Tags.
{.is-warning}

> Hinweis: Tags beeinflussen nicht "Muss enthalten", "Darf nicht enthalten", "Bevorzugte" Wörter oder andere nicht oben genannte Aspekte.
{.is-info}

# Allgemein

## Host

- Bind-Adresse - Gültige IPv4-Adresse oder '*' für alle Schnittstellen
  - 0.0.0.0 oder `*` - jede Adresse kann sich verbinden
  - 127.0.0.1 oder localhost - nur lokale Anwendungen können sich verbinden
  - Jede andere IP (z.B. 1.2.3.4) - nur diese IP (1.2.3.4) kann sich verbinden
- Portnummer - Die Portnummer, über die Sie auf die WebUI für Sonarr zugreifen möchten

> Hinweis: Wenn Sie Docker verwenden, ändern Sie diese Einstellung nicht.
{.is-warning}

- URL-Basis - Für Reverse-Proxy-Unterstützung, Standard ist leer

> Hinweis: Wenn Sie einen Reverse-Proxy verwenden (Beispiel: meine-domain.com/sonarr), geben Sie '/sonarr' für URL-Basis ein.
{.is-info}

- Instanzname - Instanzname im Tab und für den Syslog-App-Namen

> Wenn Sie mehrere Instanzen ausführen, wird der Instanzname dem Namen des Webbrowser-Tabs hinzugefügt. {.is-info}

- SSL aktivieren - Wenn Sie SSL-Zertifikate haben und die Kommunikation mit Ihrem Sonarr verschlüsseln möchten, aktivieren Sie diese Option.

> Hinweis: Verwenden Sie dies nicht, es sei denn, Sie wissen, was Sie tun.
{.is-warning}

## Sicherheit

- Authentifizierung - Wie möchten Sie sich authentifizieren, um auf Ihre Sonarr-Instanz zuzugreifen
  - Keine - Sie haben keine Authentifizierung, um auf Ihre Sonarr zuzugreifen. Normalerweise, wenn Sie der einzige Benutzer Ihres Netzwerks sind, niemand in Ihrem Netzwerk Zugriff auf Ihre Sonarr haben möchte oder Ihre Sonarr nicht im Web verfügbar ist
  - Basic (Browser-Popup) - Diese Option zeigt beim Zugriff auf Ihre Sonarr ein kleines Popup an, in dem Sie einen Benutzernamen und ein Passwort eingeben können
  - Forms (Anmeldeseite) - Diese Option hat einen vertraut aussehenden Anmeldebildschirm, ähnlich wie andere Websites, um sich bei Ihrer Sonarr anzumelden
- API-Schlüssel - So kommunizieren andere Programme oder haben Sonarr mit anderen Programmen kommunizieren. Dieser Schlüssel kann, wenn er einer falschen Person mit Zugriff gegeben wird, alle möglichen Dinge mit Ihrer Bibliothek tun. Aus diesem Grund wird der API-Schlüssel in den Protokollen geschwärzt
- Zertifikatsvalidierung - Ändern Sie, wie streng die HTTPS-Zertifikatsvalidierung ist
  - Aktiviert - Alle HTTPS-Zertifikate validieren (empfohlen)
  - Deaktiviert für lokale Adressen - Alle HTTPS-Zertifikate außer denen auf localhost und im LAN validieren
  - Deaktiviert - Keine HTTPS-Zertifikate validieren

## Proxy

- Proxy - Diese Option ermöglicht es Ihnen, die von Sonarr abgerufenen Informationen und Suchanfragen über einen Proxy laufen zu lassen. Dies kann nützlich sein, wenn Sie in einem Land sind, das das Herunterladen von Torrent-Dateien nicht erlaubt

- Proxy verwenden - Aktivieren Sie diese Option, um einen Proxy zu verwenden
- Proxy-Typ - Wählen Sie Ihren Proxy-Typ (HTTPS, Socks4 oder Socks5)
- Hostname - Geben Sie Ihren Proxy-Hostname ein (Kein http/https oder ein anderes Protokoll angeben)
- Port - Geben Sie Ihren Proxy-Port ein
- Benutzername - Geben Sie Ihren Proxy-Benutzernamen ein, falls zutreffend
- Passwort - Geben Sie Ihr Proxy-Passwort ein, falls zutreffend
- Ignorierte Adressen - Geben Sie eine durch Kommas getrennte Liste von Adressen ein, die den Proxy umgehen sollen
- Proxy für lokale Adressen umgehen - Aktivieren Sie das Kontrollkästchen, um den Proxy für lokale Adressen zu umgehen. Lokale Anfragen werden durch das Fehlen eines Punktes (.) in der URI identifiziert, z.B. <http://webserver/> oder Zugriff auf den lokalen Server, einschließlich <http://localhost>, <http://loopback> oder <http://127.0.0.1>. Wenn dies nicht aktiviert ist, werden alle Internetanfragen über den Proxyserver gesendet.

## Protokollierung

- Protokollstufe - Wahrscheinlich eines der nützlichsten Fehlerbehebungswerkzeuge
  - Info - Dies ist die grundlegendste Art und Weise, wie Sonarr Informationen sammelt. Hier werden nur sehr wenige Informationen in den Protokollen enthalten sein. Diese Protokolldatei enthält tödliche, Fehler-, Warn- und Info-Einträge.
  - Debug - Debug enthält alle Informationen, die Info enthält, sowie weitere nützliche Informationen. Diese Protokolldateien enthalten tödliche, Fehler-, Warn-, Info- und Debug-Einträge.
  - Trace - Das fortschrittlichste und detaillierteste Protokollieren in Sonarr. Trace enthält alle von Info und Debug gesammelten Informationen und mehr. Dies ist die häufigste Art von Protokoll, die bei der Fehlerbehebung auf Discord oder Reddit angefordert wird. Wenn Sie Hilfe benötigen, wählen Sie bitte Ihr Protokoll auf Trace und wiederholen Sie die Aufgabe, die Ihnen Probleme bereitet hat, um das Protokoll zu erfassen. Diese Protokolldateien enthalten tödliche, Fehler-, Warn-, Info-, Debug- und Trace-Einträge.

## Analytik

- Analytik - Senden Sie anonyme Nutzungs- und Fehlerinformationen an die Server von Sonarr (SkyHook). Dies umfasst Informationen über Ihren Browser, welche Sonarr WebUI-Seiten Sie verwenden, Fehlerberichte sowie Betriebssystem- und Laufzeitversionen. Wir werden diese Informationen verwenden, um Funktionen und Fehlerbehebungen zu priorisieren.

## Updates

- (Erweiterte Option) Branch - Dies ist der Zweig von Sonarr, den Sie verwenden.
  - [Bitte lesen Sie diesen FAQ-Eintrag für weitere Informationen](/sonarr/faq#how-do-i-update-sonarr)
- Automatisch - Updates automatisch herunterladen und installieren. Sie können weiterhin über System: Updates installieren. Hinweis: Windows-Benutzer werden immer automatisch aktualisiert.
- Mechanismus - Verwenden Sie den integrierten Updater von Sonarr oder ein Skript
  - Integriert - Verwenden Sie den eigenen Updater von Sonarr
  - Skript - Lassen Sie Sonarr das Aktualisierungsskript ausführen
  - Docker - Aktualisieren Sie Sonarr nicht innerhalb des Docker, sondern ziehen Sie ein brandneues Image mit dem neuen Update
  - Apt - Festgelegt vom Debian/Ubuntu-Paket, wenn die Aktualisierung ausschließlich über Apt verwaltet wird
- Skript - Nur sichtbar, wenn Mechanismus auf Skript eingestellt ist - Pfad zum Aktualisierungsskript
- Aktualisierungsprozess - Sonarr lädt die Aktualisierungsdatei herunter, überprüft deren Integrität, extrahiert sie an einen temporären Speicherort und ruft die gewählte Methode auf. Der Aktualisierungsprozess wird unter demselben Benutzer ausgeführt, unter dem Sonarr ausgeführt wird. Er benötigt Berechtigungen, um die Sonarr-Dateien zu aktualisieren sowie Sonarr zu stoppen/starten.
- Integriert - Die integrierte Methode sichert Sonarr-Dateien und -Einstellungen, stoppt Sonarr, aktualisiert die Installation und startet Sonarr. Wenn Ihr System das Stoppen von Sonarr nicht verarbeiten kann und versucht, es automatisch neu zu starten, ist es möglicherweise besser, stattdessen ein Skript zu verwenden. Im Falle eines Fehlers wird die vorherige Version von Sonarr neu gestartet.
- Skript - Das Skript sollte das gleiche wie der integrierte Updater behandeln. Wenn Sie Dienste stoppen und starten müssen (upstart/launchd/etc), müssen Sie dies hier tun.

## Backups

- Der Backup-Bereich ermöglicht es Ihnen, Sonarr mitzuteilen, wie Sie Backups behandeln möchten

- Ordner - Hier können Sie den Speicherort für das Backup auswählen. In Docker sind Sie auf das beschränkt, was der Container sehen darf. Pfade sind relativ zum Appdata-Ordner; falls erforderlich, können Sie einen absoluten Pfad angeben, um außerhalb des Appdata-Ordners zu sichern.
- Intervall - Wie oft soll Sonarr ein Backup erstellen
- Aufbewahrung - Wie lange soll Sonarr jedes Backup aufbewahren. Nachdem ein neues Backup erstellt wurde, wird das älteste Backup entfernt

# Benutzeroberfläche

## Kalender

- Erster Tag der Woche - Hier können Sie auswählen, welcher Tag Ihrer Meinung nach der erste Tag der Woche sein sollte.
- Kopfzeile der Wochen-Spalte - Hier können Sie die Überschrift für die Spalten auswählen

## Daten

- Kurzes Datumsformat - Wie möchten Sie, dass Sonarr kurze Datumsangaben anzeigt?
- Langes Datumsformat - Wie möchten Sie, dass Sonarr lange Datumsangaben anzeigt?
- Zeitformat - Möchten Sie ein 12-Stunden- oder 24-Stunden-Format?
- Relative Daten anzeigen - Möchten Sie, dass Sonarr relative (Heute/Gestern/usw.) oder absolute Daten anzeigt?

## Stil

- Farbfehlsichtigkeitsmodus aktivieren - Geänderter Stil, um farbfehlsichtigen Benutzern eine bessere Unterscheidung von farbcodierten Informationen zu ermöglichen