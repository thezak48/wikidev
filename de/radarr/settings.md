---
title: Radarr-Einstellungen
description: Beschreibung der Einstellungsmenüs von Radarr
published: true
date: 2023-08-27T22:02:11.780Z
tags: radarr, needs-love, settings
editor: markdown
dateCreated: 2021-05-29T15:57:25.304Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Menüoptionen](#menüoptionen)
- [Medienverwaltung](#medienverwaltung)
  - [Vorschläge zur Community-Namensgebung](#vorschläge-zur-community-namensgebung)
  - [Filmbenennung](#filmbenennung)
    - [Standard-Filmformat](#standard-filmformat)
    - [Filmbenennung](#filmbenennung-1)
    - [Film-IDs](#film-ids)
    - [Qualität](#qualität)
    - [Medieninformationen](#medieninformationen)
    - [Release-Gruppe](#release-gruppe)
    - [Edition](#edition)
    - [Benutzerdefinierte Formate (Namensgebung)](#benutzerdefinierte-formate-namensgebung)
    - [Original](#original)
  - [Filmordnerformat](#filmordnerformat)
    - [Filmbenennung](#filmbenennung-2)
    - [Film-ID](#film-id)
  - [Ordner](#ordner)
  - [Importieren](#importieren)
  - [Dateiverwaltung](#dateiverwaltung)
  - [Berechtigungen](#berechtigungen)
  - [Stammordner](#stammordner)
- [Profile](#profile)
  - [Qualitätsprofile](#qualitätsprofile)
  - [Verzögerungsprofile](#verzögerungsprofile)
    - [Verwendungszwecke](#verwendungszwecke)
    - [Funktionsweise der Verzögerungsprofile](#funktionsweise-der-verzögerungsprofile)
      - [Beispiele](#beispiele)
        - [Beispiel 1](#beispiel-1)
        - [Beispiel 2](#beispiel-2)
        - [Beispiel 3](#beispiel-3)
- [Qualität](#qualität-1)
  - [Bedeutung der Qualitäts-Tabelle](#bedeutung-der-qualitäts-tabelle)
  - [Definierte Qualitäten](#definierte-qualitäten)
- [Benutzerdefinierte Formate](#benutzerdefinierte-formate)
  - [Bedingungen für benutzerdefinierte Formate](#bedingungen-für-benutzerdefinierte-formate)
    - [Modifikatoren](#modifikatoren)
    - [Bedingungen](#bedingungen)
    - [Einstellungen und Rangfolge für Profilerstellung](#einstellungen-und-rangfolge-für-profilerstellung)
      - [Importieren / Exportieren von benutzerdefinierten Formaten](#importieren-exportieren-von-benutzerdefinierten-formaten)
      - [Importieren / Aktualisieren vorhandener benutzerdefinierter Formate](#importieren-aktualisieren-vorhandener-benutzerdefinierter-format)
    - [Sammlung von benutzerdefinierten Formaten](#sammlung-von-benutzerdefinierten-formaten)
- [Indexer](#indexer)
  - [Unterstützte Indexer](#unterstützte-indexer)
    - [Indexer-Einstellungen](#indexer-einstellungen)
    - [Usenet-Indexer-Konfiguration](#usenet-indexer-konfiguration)
    - [Torrent-Tracker-Konfiguration](#torrent-tracker-konfiguration)
      - [Indexer-Flags](#indexer-flags)
  - [Optionen](#optionen)
  - [Einschränkungen](#einschränkungen)
- [Download-Clients](#download-clients)
  - [Übersicht](#übersicht)
  - [Download-Client-Prozesse](#download-client-prozesse)
    - [Usenet-Prozess](#usenet-prozess)
    - [Torrent-Prozess](#torrent-prozess)
  - [Download-Clients](#download-clients-1)
    - [Unterstützte Download-Clients](#unterstützte-download-clients)
    - [Usenet-Client-Einstellungen](#usenet-client-einstellungen)
    - [Torrent-Client-Einstellungen](#torrent-client-einstellungen)
    - [Kompatibilität der Torrent-Client-Entfernung von Downloads](#kompatibilität-der-torrent-client-entfernung-von-downloads)
  - [Abschluss der Download-Verarbeitung](#abschluss-der-download-verarbeitung)
    - [Abgeschlossene Downloads entfernen](#abgeschlossene-downloads-entfernen)
    - [Behandlung fehlgeschlagener Downloads](#behandlung-fehlgeschlagener-downloads)
  - [Remote-Pfadzuordnungen](#remote-pfadzuordnungen)
- [Importlisten](#importlisten)
  - [Listen](#listen)
  - [Listenoptionen](#listenoptionen)
  - [Listenausschlüsse](#listenausschlüsse)
- [Verbinden](#verbinden)
  - [Verbindungen](#verbindungen)
  - [Verbindungsauslöser](#verbindungsauslöser)
- [Metadaten](#metadaten)
  - [Optionen](#optionen-1)
  - [Metadatenverbraucher](#metadatenverbraucher)
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
  - [Filme](#filme)
  - [Termine](#termine)
  - [Stil](#stil)
  - [Sprache](#sprache)

Diese Seite erläutert alle verfügbaren Einstellungen in Radarr und wie sie funktionieren. Dies soll jedoch keine umfassende Anleitung zur Einrichtung von Radarr sein. Wenn Sie das möchten, verwenden Sie bitte die [Schnellstart](/radarr/quick-start-guide)-Seite.

# Menüoptionen

Um zur Einstellungsseite zu gelangen, wählen Sie "Einstellungen" in der Seitenleiste aus. Die folgenden Untermenüoptionen stehen zur Verfügung:

![settings_1_menu.png](/assets/radarr/settings_1_menu.png)

Beachten Sie auch, dass für jede einzelne Einstellungsseite einige Optionen oben im Menü verfügbar sind:

![settings_2_topmenu.png](/assets/radarr/settings_2_topmenu.png)

- "Erweitert ausblenden/zeigen" ist wichtig für alle Elemente, die unten als "(Erweiterte Option)" gekennzeichnet sind, da sie sonst nicht angezeigt werden. Diese Menüpunkte werden in den Screenshots orange angezeigt.

- Sie müssen Ihre Änderungen speichern, bevor Sie den Bildschirm verlassen. Klicken Sie dazu auf das Disketten-Symbol. Wenn Sie keine Änderungen vorgenommen haben, wird "Keine Änderungen" angezeigt und ausgegraut, wie oben gezeigt.

# Medienverwaltung

> Einige dieser Einstellungen sind nur sichtbar, wenn "Erweiterte Einstellungen anzeigen" aktiviert ist, das sich in der oberen Leiste unter der Suchleiste befindet{.is-info}

## Vorschläge zur Community-Namensgebung

> Hier sind einige Vorschläge zur Community-Namensgebung von [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/){.is-info}

### Filmdaten

- Radarr v4.2.2.6489 oder neuer

`{Movie CleanTitle} {(Erscheinungsjahr)} {imdb-{ImdbId}} {edition-{Edition Tags}} {[Benutzerdefinierte Formate]}{[Quality Full]}{[MediaInfo 3D]}{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}]{MediaInfo AudioLanguages}[{Mediainfo VideoCodec}]{-Release Group}`

- Ältere Radarr-Versionen

`{Movie CleanTitle} {(Erscheinungsjahr)} {Edition Tags} [imdb-{ImdbId}]{[Benutzerdefinierte Formate]}{[Quality Full]}{[MediaInfo 3D]}{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}][{Mediainfo VideoCodec}]{-Release Group}`

### Filmordner

`{Movie CleanTitle} ({Erscheinungsjahr})`

## Filmbenennung

- Filme umbenennen - Wenn nicht aktiviert, verwendet Radarr den vorhandenen Namen, wenn die Umbenennung deaktiviert ist
  - Wenn nicht aktiviert:
    - Importieren durch den Download-Client
      - Der Release-Titel des Download-Clients wird verwendet
    - Manueller (Ad-hoc-)Import: Originaldateiname
- Ersetzen verbotener Zeichen - Wenn nicht aktiviert, entfernt Radarr sie stattdessen.

  - Die Zeichen sind: `:` `\` `/` `>` `<` `?` `*` `|` `"`
- Ersetzung des Doppelpunkts (`:`) - Diese Einstellung bestimmt, wie Radarr Doppelpunkte in der Filmdatei behandelt. Dies ist nur verfügbar, wenn die Ersetzung verbotener Zeichen aktiviert ist.
  - Löschen - Selbst erklärend
    - Beispiel: Film,Der.mkv => FilmDer.mkv
  - Ersetzen durch Bindestrich - Entfernt den Doppelpunkt und fügt an seiner Stelle einen Bindestrich ein
    - Beispiel: Film,Der.mkv => Film-Der.mkv
  - Ersetzen durch Leerzeichen - Entfernt den Doppelpunkt und fügt an seiner Stelle ein Leerzeichen ein
    - Beispiel: Film,Der.mkv => Film Der.mkv
  - Ersetzen durch Leerzeichen Bindestrich Leerzeichen - Selbst erklärend
    - Beispiel: Film,Der.mkv => Film - Der.mkv

### Standard-Filmformat

- Hier wählen Sie die Namenskonvention für Ihre Filme aus

- Dropdown-Box (obere rechte Ecke)
  - Linke Box - Behandlung von Leerzeichen
    Leerzeichen ( ) - Verwenden Sie Leerzeichen in der Benennung (Standard)
    Punkt (.) - Verwenden Sie Punkte anstelle von Leerzeichen in der Benennung
    Unterstrich (_) - Verwenden Sie Unterstriche anstelle von Leerzeichen in der Benennung
    Bindestrich (-) - Verwenden Sie Bindestriche anstelle von Leerzeichen in der Benennung
  - Rechte Box - Behandlung der Groß- und Kleinschreibung
    Standard-Groß-/Kleinschreibung - Titel groß- und kleinschreiben (~camel-case) (Standard)
    Großbuchstaben - Titel komplett in Großbuchstaben
    Kleinbuchstaben - Titel komplett in Kleinbuchstaben

### Filmbenennung

- `{Movie Title}` = Der Filmtitel!
- `{Movie Title:DE}` = Titel des Films
- `{Movie CleanTitle}` = Der Filmtitel!
- `{Movie TitleThe}` = Filmtitel!, Der
- `{Movie OriginalTitle}` = Τίτλος ταινίας
- `{Movie CleanOriginalTitle}` = Τίτλος ταινίας
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = Die Filmesammlung
- `{Movie Certification}` = R
- `{Release Year}` = 2009

`CleanTitle` [führt folgende Aktionen aus](https://github.com/Radarr/Radarr/blob/5948f564827eabb7afc1e89bf4a5987e3c71dc74/src/NzbDrone.Core/Organizer/FileNameBuilder.cs#L207):

- Ersetzt `&` durch `and`
- Ersetzt `/` und `\` durch ` `
- Entfernt `,`,`<`,`>`,`/`,`\`,`;`,`:`,`'`,`|`, `~`,`!`,`?`,`@`,`$`,`%`,`^`,`*`,`-`,`_`,`=` gemäß dem folgenden regulären Ausdruck:

```regex
(?<=\s)(,|<|>|\/|\\|;|:|'|""|\||`|~|!|\?|@|$|%|^|\*|-|_|=){1}(?=\s)|('|:|\?|,)(?=(?:(?:s|m)\s)|\s|$)|(\(|\)|\[|\]|\{|\})
```

### Film-IDs

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

> Imdb-Tags, die im Plex-Namensformat verwendet werden, werden bedingt ausgeblendet, wenn der Wert leer ist `{imdb-{ImdbId}}` {.is-info}

### Qualität

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Medieninformationen

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguages}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`, `AudioLanguages` und `SubtitleLanguages` unterstützen derzeit kein Suffix `:EN+DE`, das in Sonarr erlaubt ist, um die in den Dateinamen aufgenommenen Sprachen zu filtern. Es gibt ein offenes [Problem](https://github.com/Radarr/Radarr/issues/4710) dazu.
~~`MediaInfo Full`, `AudioLanguages` und `SubtitleLanguages` unterstützen ein Suffix `:EN+DE`, mit dem Sie die in den Dateinamen aufgenommenen Sprachen filtern können. Verwenden Sie `-DE`, um bestimmte Sprachen auszuschließen. Durch Hinzufügen von <kb>+</kb> (z. B.: `:EN+`) wird `[EN]`,`[EN+--]` oder `[--]` je nach ausgeschlossenen Sprachen ausgegeben. Zum Beispiel - `{MediaInfo Full:EN+DE}`.~~
{.is-info}

> `MediaInfo VideoDynamicRangeType` gibt mögliche Werte zurück: DV, DV HDR10, DV HLG, DV SDR, HDR10, HDR10Plus, HLG und PQ.
{.is-info}

### Release-Gruppe

- `{Release Group}` = Rls Grp

### Edition

- `{Edition Tags}` = IMAX

> Ab v4.2.2.6489 werden Edition-Tags, die in Radarr dem Namensformat von Plex folgen (`{edition-{Edition Tags}}`), bedingt ausgeblendet, wie es `{-Group}` tut, wenn der Wert der Edition-Tags leer ist
{.is-info}

### Benutzerdefinierte Formate (Namensgebung)

- `{Benutzerdefinierte Formate}` = Surround Sound x264

> Benutzerdefinierte Formate sind der wörtliche Name des benutzerdefinierten Formats und müssen aktiviert sein, um in der Umbenennung enthalten zu sein {.is-info}

### Original

- `{Original Title}` = Movie.Title.HDTV.x264-EVOLVE
- `{Original Filename}` = Movie.title.hdtv.x264-EVOLVE

> `Original Title` ist der Veröffentlichungsname und wird empfohlen, verwendet zu werden.
{.is-info}

>`Original Filename` wird nicht empfohlen. Es handelt sich um den wörtlichen Originaldateinamen und kann verschleiert sein `t1i0p3s7i8yuti`.{.is-warning}

## Filmordnerformat

Hier legen Sie die Namenskonvention für den Ordner fest, der die Staffelordner oder Filmdateien enthält. Klicken Sie auf das `?`, um den Dialog "Ordnername-Token" aufzurufen.

### Filmbenennung

- `{Movie Title}` = Filmtitel!
- `{Movie Title:DE}` = DateiTitel
- `{Movie CleanTitle}` = Filmtitel
- `{Movie TitleThe}` = Filmtitel, Der
- `{Movie OriginalTitle}` = Τίτλος ταινίας
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = Die Filmesammlung
- `{Movie Certification}` = R
- `{Release Year}` = 2009

### Film-ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

## Ordner

- Leere Medienordner erstellen - Fehlende Filmordner während der Festplattenüberprüfung erstellen
- Leere Ordner löschen - Leere Filmordner während der Festplattenüberprüfung und beim Löschen von Filmdateien löschen

## Importieren

- Freien Speicherplatz überprüfen überspringen - Verwenden Sie dies, wenn Radarr den freien Speicherplatz nicht aus Ihrem Serienstammordner erkennen kann
- Mindestens freier Speicherplatz - Das Umschalten dieser Option verhindert den Import, wenn weniger als diese Menge an Festplattenspeicherplatz verfügbar wäre
- Verwenden von Hardlinks anstelle von Kopien - Verwenden Sie Hardlinks, wenn Sie versuchen, Dateien von Torrents zu kopieren, die noch gesät werden

  - Weitere Informationen dazu finden Sie [hier](https://trash-guides.info/hardlinks)

> Selten, aber möglicherweise verhindern Dateisperrungen das Umbenennen von Dateien, die noch gesät werden. Sie können das Seeding vorübergehend deaktivieren und die Umbenennungsfunktion von Radarr als Workaround verwenden.
{.is-warning}

- Zusätzliche Dateien importieren - Passende zusätzliche Dateien (Untertitel, nfo usw.) nach dem Import einer Datei importieren

## Dateiverwaltung

- Nicht überwachte gelöschte Filme - Filme, die von der Festplatte gelöscht wurden, werden automatisch in Radarr nicht überwacht.
- Proper & Repacks herunterladen - Ob automatisch auf Propers/Repacks aktualisiert werden soll oder nicht. Verwenden Sie `Nicht bevorzugen`, um die bevorzugte Wortbewertung über Propers/Repacks zu sortieren.

  - Bevorzugen und aktualisieren - Repacks und Propers höher bewerten als Nicht-Repacks und Nicht-Propers. Neue Repacks und Propers als Upgrade für aktuelle Versionen behandeln.
  - Nicht automatisch aktualisieren - Repacks und Propers höher bewerten als Nicht-Repacks und Nicht-Propers. Neue Repacks und Propers nicht als Upgrade für aktuelle Versionen behandeln.
  - Nicht bevorzugen - Repacks und Propers effektiv ignorieren. Sie müssen jegliche Präferenz für diese mit [Benutzerdefinierten Formaten](#benutzerdefinierte-formate) verwalten.

> \* `PROPER` - bedeutet, dass es ein Problem mit der vorherigen Version gab. Downloads, die als PROPER gekennzeichnet sind, zeigen an, dass die Probleme in dieser Version behoben wurden. Dies wird von einer Gruppe durchgeführt, die die Originalversion nicht veröffentlicht hat.
> \* `REPACK` - bedeutet, dass es ein Problem mit der vorherigen Version gab und dass es von der Originalgruppe behoben wurde. Downloads, die als REPACK gekennzeichnet sind, zeigen an, dass die Probleme in dieser Version behoben wurden. Dies wird von einer Gruppe durchgeführt, die die Originalversion veröffentlicht hat.
{.is-info}

> [Verwenden Sie benutzerdefinierte Formate für automatische Upgrades zu Propers/Repacks](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)
{.is-info}

- Video-Dateien analysieren - Dateiinformationen wie Auflösung, Laufzeit und Codec-Informationen aus Dateien extrahieren. Dies erfordert, dass Radarr Teile der Datei liest, was während der Scans zu hoher Festplatten- oder Netzwerkaktivität führen kann.
- Filmordner nach Aktualisierung neu scannen
  - Immer - Dies wird Filmordner basierend auf dem Aufgabenplan neu scannen. Dies wird für die meisten Fälle empfohlen, einschließlich der Verwendung von Bazarr.
  - Nach manueller Aktualisierung - Sie müssen die Festplatte manuell neu scannen. Dies wird für Benutzer von Cloud-Speicher empfohlen.
  - Nie - Wie der Name schon sagt, Filmordner nie neu scannen. Dies wird nicht empfohlen.
- Dateidatum ändern - Dateidatum beim Import/Neuscannen ändern
  - Keine - Radarr ändert das Datum nicht, das in Ihrem Dateibrowser angezeigt wird.
  - Veröffentlichungsdatum im Kino - Das Datum, an dem der Film im Kino veröffentlicht wurde.
  - Veröffentlichungsdatum physisch - Das Datum, an dem der Film entweder auf Datenträger (physisch) oder im Web veröffentlicht wurde.
- Papierkorb - Filmdateien werden hier abgelegt, wenn sie gelöscht werden, anstatt dauerhaft gelöscht zu werden.
- Papierkorb bereinigen - Wie alt eine bestimmte Datei sein kann, bevor sie dauerhaft gelöscht wird.

> Dateien im Papierkorb, die älter als die ausgewählte Anzahl von Tagen sind, werden automatisch bereinigt. {.is-warning}

## Berechtigungen

- Berechtigungen festlegen - Soll `chmod` ausgeführt werden, wenn Dateien importiert/umbenannt werden?
  - Ordnerberechtigungen - Oktal, angewendet beim Importieren/Umbenennen von Medienordnern und -dateien (ohne Ausführungsbits)

> Das Dropdown-Menü enthält eine voreingestellte Liste sehr häufig verwendeter Berechtigungen, die verwendet werden können. Sie können jedoch auch manuell eine Ordneroktalzahl eingeben, wenn Sie möchten. {.is-info}

> Dies funktioniert nur, wenn der Benutzer, der `Radarr` ausführt, der Eigentümer der Datei ist. Es ist besser, sicherzustellen, dass der Download-Client die Berechtigungen ordnungsgemäß festlegt. {.is-warning}

- Gruppenberechtigungen - Gruppenname oder GID. Verwenden Sie GID für Remote-Dateisysteme.

> Dies funktioniert nur, wenn der Benutzer, der `Radarr` ausführt, der Eigentümer der Datei ist. Es ist besser, sicherzustellen, dass der Download-Client die Berechtigungen ordnungsgemäß festlegt. {.is-warning}

## Stammordner

- Pfad - Hier wird der Pfad zu Ihrer Medienbibliothek angezeigt.
- Freier Speicherplatz - Hier wird der von Radarr vom System gemeldete freie Speicherplatz angezeigt.
- Nicht zugeordnete Ordner - Dies sind Ordner, die keinem Film zugeordnet sind.

> Das `X` am Ende entfernt diesen Stammordner. {.is-info}

- Stammordner hinzufügen - Hier können Sie einen Stammordner auswählen, um neue importierte Downloads in diesen Ordner zu platzieren oder Radarr das Scannen vorhandener Medien zu ermöglichen.

> Benutzer von Nicht-Windows-Systemen:
> \* Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` aktiviert ist.
> \* Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` aktiviert ist. {.is-warning}

# Profile

## Qualitätsprofile

- Legen Sie Profile für die Qualität der Filme fest, die Sie herunterladen möchten.

> Beim Auswählen eines vorhandenen Profils oder beim Hinzufügen eines zusätzlichen Profils wird ein neues Fenster angezeigt. {.is-info}

> Hinweis: Die Qualität, die in einem blauen Kästchen angezeigt wird, ist die Qualität, auf die alle Medien mit diesem Profil weiterhin aktualisiert werden. {.is-info}

- Plus-Symbol (<kb>+</kb>) - Erstellen Sie ein neues Qualitätsprofil

- Name - Wählen Sie einen **EINDEUTIGEN** Namen für das Qualitätsprofil, das Sie erstellen möchten.
- Upgrades zulassen - Wenn diese Option aktiviert ist und Sie Radarr mitteilen, einen `WEB 1080p` herunterzuladen, da dies die erste Veröffentlichung eines bestimmten Films ist, und später jemand in der Lage ist, einen `Bluray-1080p` hochzuladen, wird Radarr automatisch auf die bessere Qualität aktualisieren, ***wenn*** diese Qualität in `Upgrade bis` ausgewählt ist.
- Upgrade bis - Sobald diese Qualität erreicht ist, wird Radarr keine Filme mehr herunterladen.

> Hinweis: Dies gilt nur, wenn `Bluray-1080p` höher als `WEB 1080p` in der Sektion `Qualitäten` ist. {.is-warning}

- Qualitäten - Qualitäten, die weiter oben in der Liste stehen, werden bevorzugt, auch wenn sie nicht ausgewählt sind. Qualitäten innerhalb derselben Gruppe sind gleichwertig. Nur ausgewählte Qualitäten werden gewünscht.
  - Gruppen bearbeiten - Einige Qualitäten sind zu Gruppen zusammengefasst, um die Größe der Liste zu reduzieren und ähnliche Veröffentlichungen zu gruppieren. Ein gutes Beispiel dafür sind `WebDL` und `WebRip`, da diese sehr ähnlich sind und in der Regel ähnliche Bitraten haben. Beim Bearbeiten der Gruppen können Sie die Präferenz innerhalb jeder Gruppe ändern. [Siehe TRaSH's Guide, wie man Qualitäten zusammenführt](https://trash-guides.info/merge-quality)

  - [Siehe Qualitäten](#qualitäten-definiert)

> Standardmäßig sind die Qualitäten von niedrigster (unten) bis höchster (oben) eingestellt. {.is-info}

- Sprache - Wählen Sie Ihre bevorzugte Sprache aus.

- Benutzerdefiniertes Format - Radarr bewertet jede Veröffentlichung anhand der Summe der Bewertungen für übereinstimmende benutzerdefinierte Formate. Wenn eine neue Veröffentlichung die Bewertung verbessern würde, bei gleicher oder besserer Qualität, wird Radarr sie herunterladen.
Weitere Informationen finden Sie unter [Benutzerdefinierte Formate](#benutzerdefinierte-formate).

## Verzögerungsprofile

- Verzögerungsprofile ermöglichen es Ihnen, die Anzahl der Veröffentlichungen, die für einen Film heruntergeladen werden, zu reduzieren, indem Sie eine Verzögerung hinzufügen, während Radarr weiterhin nach Veröffentlichungen sucht, die besser zu Ihren Präferenzen passen.
- Bevorzugtes Protokoll - Dies kann entweder `Usenet` oder `Torrent` sein, je nachdem, welches Download-Protokoll Sie bevorzugen.
- Usenet-Verzögerung - Hier können Sie die Anzahl der Minuten festlegen, die gewartet werden sollen, bevor der Download startet.
- Torrent-Verzögerung - Hier können Sie die Anzahl der Minuten festlegen, die gewartet werden sollen, bevor der Download startet.
- Umgehen, wenn höchste Qualität - Verzögerung umgehen, wenn die Veröffentlichung das höchste aktiviertes Qualitätsprofil mit dem bevorzugten Protokoll hat.
- Tags - Durch Zuweisen dieses Verzögerungsprofils zu einem Tag können Sie einen bestimmten Film so kennzeichnen, dass er nach den hier festgelegten Regeln abgespielt wird.
- Schraubenschlüssel-Symbol - Hiermit können Sie das Verzögerungsprofil bearbeiten.
- Plus-Symbol (<kb>+</kb>) - Erstellen Sie ein neues Verzögerungsprofil

### Verwendung

Einige Medien erhalten in den Stunden nach der Veröffentlichung mehrere Veröffentlichungen unterschiedlicher Qualität, und ohne Verzögerungsprofile könnte Radarr versuchen, alle herunterzuladen. Mit Verzögerungsprofilen kann Radarr so konfiguriert werden, dass es die ersten paar Stunden der Veröffentlichungen ignoriert.

Verzögerungsprofile sind auch hilfreich, wenn Sie ein Protokoll (Usenet oder BitTorrent) gegenüber dem anderen betonen möchten. (Siehe Beispiel 3)

### Funktionsweise der Verzögerungsprofile

Der Timer beginnt, sobald Radarr erkennt, dass ein Film eine verfügbare Veröffentlichung hat. Diese Veröffentlichung wird in Ihrer Warteschlange mit einem Uhrensymbol angezeigt, um anzuzeigen, dass sie sich in einer Verzögerung befindet.

> Die Uhr beginnt ab der Zeit, zu der die Veröffentlichung hochgeladen wurde, und nicht ab dem Zeitpunkt, zu dem Radarr sie sieht. {.is-info}

Während des Verzögerungszeitraums werden alle neuen Veröffentlichungen, die verfügbar werden, von Radarr erfasst. Wenn der Verzögerungstimer abläuft, lädt Radarr die einzelne Veröffentlichung herunter, die am besten zu Ihren Qualitätspräferenzen passt.

Der Timer kann für Usenet und Torrents unterschiedlich sein. Jedes Profil kann mit einem oder mehreren Tags verknüpft werden, um Ihnen die Anpassung zu ermöglichen, welche Shows welches Profil haben. Ein Verzögerungsprofil ohne Tag gilt als Standard und gilt für alle Shows, die kein spezifisches Tag haben.

> Verzögerungsprofile beginnen ab dem Zeitpunkt, zu dem der Indexer meldet, dass die Veröffentlichung hochgeladen wurde. Dies bedeutet, dass Inhalte, die älter als die von Ihnen festgelegte Anzahl von Minuten sind, in keiner Weise von Ihrem Verzögerungsprofil betroffen sind und sofort heruntergeladen werden. Darüber hinaus ignorieren **manuelle Suchen** nach Inhalten (Suchen außerhalb des RSS-Feeds) die Einstellungen des Verzögerungsprofils. {.is-warning}

#### Beispiele

- Für jedes Beispiel nehmen Sie an, dass der Benutzer das folgende aktive Qualitätsprofil hat: WebDL-720p und höher sind erlaubt, WebDL-1080p ist die Qualitätsbegrenzung, BluRay1080p ist die höchste bewertete Qualität.

##### Beispiel 1

- In diesem einfachen Beispiel ist das Profil mit einer 120-minütigen (zweistündigen) Verzögerung für Usenet und Torrent festgelegt.

- Um 23:00 Uhr erkennt Radarr die erste Veröffentlichung für einen Film, die um 22:50 Uhr hochgeladen wurde, und der 120-minütige Timer beginnt. Um 00:50 Uhr bewertet Radarr alle Veröffentlichungen der letzten zwei Stunden und lädt die beste herunter, die WebDL 720p ist.

- Um 03:00 Uhr wird eine weitere Veröffentlichung gefunden, die um 02:46 Uhr zu Ihrem Indexer hinzugefügt wurde. Ein weiterer 120-minütiger Timer beginnt. Um 04:46 Uhr wird die beste verfügbare Veröffentlichung heruntergeladen. Da die Qualitätsbegrenzung jetzt erreicht ist, kann der Film nicht mehr aktualisiert werden und Radarr sucht nicht mehr nach neuen Veröffentlichungen.

- Zu jedem Zeitpunkt, wenn eine WebDL 1080p-Veröffentlichung gefunden wird, wird sie sofort heruntergeladen, da sie die höchste bewertete Qualität ist. Wenn zu diesem Zeitpunkt ein Verzögerungstimer aktiv ist, wird er abgebrochen.

##### Beispiel 2

- Dieses Beispiel hat unterschiedliche Timer für Usenet und Torrents. Nehmen Sie an, dass ein 120-minütiger Timer für Usenet und ein 180-minütiger Timer für BitTorrent festgelegt ist.

- Um 23:00 Uhr erkennt Radarr die erste Veröffentlichung für einen Film, und beide Timer beginnen. Die Veröffentlichung wurde um 22:15 Uhr zu Ihrem Indexer hinzugefügt. Um 00:15 Uhr bewertet Radarr alle Veröffentlichungen, und wenn es akzeptable Usenet-Veröffentlichungen gibt, wird die beste heruntergeladen und beide Timer enden. Andernfalls wartet Radarr bis 00:15 Uhr und lädt die beste Veröffentlichung herunter, unabhängig davon, aus welcher Quelle sie stammt.

##### Beispiel 3

- Eine häufige Verwendung von Verzögerungsprofilen besteht darin, ein Protokoll (Usenet oder BitTorrent) gegenüber dem anderen zu betonen. Sie möchten beispielsweise nur eine BitTorrent-Veröffentlichung herunterladen, wenn nach einer bestimmten Zeit nichts auf Usenet hochgeladen wurde.

- Sie könnten einen 60-minütigen Timer für BitTorrent und einen 0-minütigen Timer für Usenet festlegen.

- Wenn die erste erkannte Veröffentlichung von Usenet stammt, lädt Radarr sie sofort herunter.

- Wenn die erste Veröffentlichung von BitTorrent stammt, setzt Radarr einen 60-minütigen Timer. Wenn während dieses Timers eine qualifizierende Usenet-Veröffentlichung erkannt wird, wird die BitTorrent-Veröffentlichung ignoriert und die Usenet-Veröffentlichung wird heruntergeladen.

## Veröffentlichungsprofile

- Hier können Sie globale Einschränkungen basierend auf einigen Parametern festlegen.
- Klicken Sie auf das <kb>+</kb> und ein neues Fenster wird geöffnet.
- Muss enthalten - Hier können Sie Radarr mitteilen, dass eine Veröffentlichung nicht heruntergeladen werden soll, wenn sie einen bestimmten String nicht enthält. Dies ist standardmäßig nicht zeichengroß und Regex kann verwendet werden.
- Darf nicht enthalten - Hier können Sie Radarr mitteilen, dass eine Veröffentlichung nicht heruntergeladen werden soll, wenn sie einen bestimmten String enthält. Dies ist standardmäßig nicht zeichengroß und Regex kann verwendet werden.
- Tags - Hier können Sie diese Einstellungen auf Filme mit mindestens einem der angegebenen [Tags](#tags) anwenden.

# Qualität

## Bedeutung der Qualitätstabelle

- Qualität - Der Name der Qualität in der Szene (fest codiert)
- Titel - Der Name der Qualität in der Benutzeroberfläche (konfigurierbar)
- Megabyte pro Minute - Selbst erklärend
- Größenlimit - Selbst erklärend
- Min - Die minimale Anzahl von Megabyte pro Minute (MB/min), die eine Qualität haben kann.
- Bevorzugt - Die bevorzugte Anzahl von Megabyte pro Minute (MB/min), die eine Qualität haben kann.
- Max - Die maximale Anzahl von Megabyte pro Minute (MB/min), die eine Qualität haben kann.

## Definierte Qualitäten

- Unbekannt - Selbsterklärend
- SDTV - Nach der Ausstrahlung von einer analogen Quelle (in der Regel Kabelfernsehen oder OTA-Standardauflösung) gerippt. Die Bildqualität ist im Allgemeinen gut (für die Auflösung) und sie werden in der Regel in DivX/XviD oder MP4 codiert.
- WEBDL-480p - WEB-DL (P2P) bezieht sich auf eine Datei, die verlustfrei von einem Streaming-Dienst wie Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer usw. gerippt oder über eine Online-Vertriebswebsite wie iTunes heruntergeladen wurde. Die Qualität ist ziemlich gut, da sie nicht neu codiert werden. Die Video- (H.264 oder H.265) und Audio- (AC3/AAC) Streams werden in der Regel aus iTunes oder Amazon Video extrahiert und ohne Qualitätsverlust in einen MKV-Container remuxed. Ein Vorteil dieser Veröffentlichungen ist, dass sie, wie BD/DVDRips, in der Regel keine Netzwerklogos auf dem Bildschirm haben. Diese sind fast so gut wie eine Blu-ray-Quelle, können aber unter Audioverzögerungen oder visuellen Artefakten aufgrund der adaptiven Bitrate von Streaming-Diensten leiden. Wenn die Internetverbindung eines Rippers auf einen Punkt fällt, an dem die Bitrate sinkt, kann sich die Quellen-Bitrate dynamisch ändern, was zu Variationen in der Bildqualität führen kann. Die meisten Veröffentlichungen, die unter extremen visuellen Artefakten leiden, werden NUKED und in der Regel wird ein PROPER veröffentlicht, um wilde Variationen in der adaptiven Bitrate zu beheben. Dies wird in 480p (SD) Qualität sein.
- WEBRip-480p - Bei einem WEB-Rip (P2P) wird die Datei häufig mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 480p (SD) Qualität sein.
- DVD - Eine Neu-Kodierung der endgültig veröffentlichten DVD9. Wenn möglich, wird dies vor dem Verkauf veröffentlicht. Die Qualität sollte ausgezeichnet sein (für die Auflösung). DVDrips werden in der Regel in DivX/XviD oder MP4 veröffentlicht.
- Bluray-480p - Eine Neu-Kodierung der endgültig veröffentlichten Blu-ray, herunterskaliert auf eine Auflösung von 480p (720x480 @ 16:9, jede andere Seitenverhältnis kann eine andere Auflösung haben). Wenn möglich, wird dies vor dem Verkauf veröffentlicht. Die Qualität sollte für die Auflösung ausgezeichnet sein. Die Bitraten können variieren, aber diese werden in der Regel in DivX, XviD oder AVC codiert und bieten den Kompromiss einer geringfügigen wahrgenommenen Qualitätsminderung gegenüber der Originalquelle bei gleichzeitiger drastischer Reduzierung der Dateigröße. Diese sind in der Regel MKV oder MP4, aber es gibt auch einige DivX/XviD, die AVI verwenden.
- HDTV-720p - Eine Neu-Kodierung der endgültig veröffentlichten Blu-ray, aber über HD-Kabel oder Satellit ausgestrahlt (1280x720 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Es kann für Laufzeit oder Inhalt je nach Netzwerk, von dem es stammt, modifiziert werden. Dies wird in der Regel mehrere Monate nach einer Verkaufsveröffentlichung veröffentlicht, aber manchmal werden hochskalierte Versionen eines Films mit Standardauflösung auf Kabelkanälen wie STARZ oder HBO veröffentlicht, und dies wären die einzigen HD-Kopien dieses bestimmten Films. Diese sind in der Regel MKV oder MP4.
- HDTV-1080p - Eine Neu-Kodierung der endgültig veröffentlichten Blu-ray, aber über HD-Kabel oder Satellit ausgestrahlt (1920x1080 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Es kann für Laufzeit oder Inhalt je nach Netzwerk, von dem es stammt, modifiziert werden. Dies wird in der Regel mehrere Monate nach einer Verkaufsveröffentlichung veröffentlicht, aber manchmal werden hochskalierte Versionen eines Films mit Standardauflösung auf Kabelkanälen wie STARZ oder HBO veröffentlicht, und dies wären die einzigen HD-Kopien dieses bestimmten Films. Diese sind in der Regel MKV oder MP4-Container.
- WEBRip-720p - Bei einem WEB-Rip (P2P) wird die Datei häufig mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 720p Qualität sein.
- Bluray-720p - Eine Neu-Kodierung der endgültig veröffentlichten Blu-ray, herunterskaliert auf eine Auflösung von 720p (1280x720 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Wenn möglich, wird dies vor dem Verkauf veröffentlicht. Die Qualität sollte für die Auflösung ausgezeichnet sein. Die Bitraten können variieren, aber diese werden in der Regel in AVC oder HEVC codiert und bieten den Kompromiss einer geringfügigen wahrgenommenen Qualitätsminderung gegenüber der Originalquelle bei gleichzeitiger drastischer Reduzierung der Dateigröße. Diese sind in der Regel MKV oder MP4-Container.
- WEBDL-1080p - WEB-DL (P2P) bezieht sich auf eine Datei, die verlustfrei von einem Streaming-Dienst wie Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer usw. gerippt oder über eine Online-Vertriebswebsite wie iTunes heruntergeladen wurde. Die Qualität ist ziemlich gut, da sie nicht neu codiert werden. Die Video- (H.264 oder H.265) und Audio- (AC3/AAC) Streams werden in der Regel aus iTunes oder Amazon Video extrahiert und ohne Qualitätsverlust in einen MKV-Container remuxed. Ein Vorteil dieser Veröffentlichungen ist, dass sie, wie BD/DVDRips, in der Regel keine Netzwerklogos auf dem Bildschirm haben. Diese sind fast so gut wie eine Blu-ray-Quelle, können aber unter Audioverzögerungen oder visuellen Artefakten aufgrund der adaptiven Bitrate von Streaming-Diensten leiden. Wenn die Internetverbindung eines Rippers auf einen Punkt fällt, an dem die Bitrate sinkt, kann sich die Quellen-Bitrate dynamisch ändern, was zu Variationen in der Bildqualität führen kann. Die meisten Veröffentlichungen, die unter extremen visuellen Artefakten leiden, werden NUKED und in der Regel wird ein PROPER veröffentlicht, um wilde Variationen in der adaptiven Bitrate zu beheben. Dies wird in 1080p Qualität sein.
- WEBRip-1080p - Bei einem WEB-Rip (P2P) wird die Datei häufig mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 1080p Qualität sein.
- Bluray-1080p - Eine Neu-Kodierung der endgültig veröffentlichten Blu-ray, in ihrer nativen 1080p-Auflösung (1920x1080 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). Wenn möglich, wird dies vor dem Verkauf veröffentlicht. Die Qualität sollte ausgezeichnet sein und die gleiche Auflösung wie die Quelle haben. Die Bitraten können variieren, aber diese werden in der Regel in AVC oder HEVC codiert und bieten den Kompromiss einer geringfügigen wahrgenommenen Qualitätsminderung gegenüber der Originalquelle bei geringfügiger Reduzierung der Dateigröße. Diese sind in der Regel MKV oder MP4-Container.
- Remux-1080p - Ein Remux ist ein Rip einer Blu-ray- oder HD-DVD-Disc in ein anderes Containerformat oder das Entfernen von Menüs und Bonusmaterial von der Disc, während die Inhalte ihrer Audio- und Videostreams intakt bleiben (auch die aktuellen Codecs beibehalten), wodurch die exakte 1:1-Filmqualität wie auf der Original-Disc garantiert wird. Dies ist in 1080p Qualität.
- HDTV-2160p - TVRip ist eine Aufzeichnungsquelle von einer Aufnahmekarte. HDTV steht für eine aufgezeichnete Quelle aus HD-Fernsehen. Mit einer HDTV-Quelle kann die Qualität manchmal sogar die einer DVD übertreffen. Filme in diesem Format werden immer beliebter. Einige Werbung und kommerzielle Banner können bei einigen Veröffentlichungen während der Wiedergabe zu sehen sein. Dies ist in 2160p (4K) Qualität.
- WEBDL-2160p - WEB-DL (P2P) bezieht sich auf eine Datei, die verlustfrei von einem Streaming-Dienst wie Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer usw. gerippt oder über eine Online-Vertriebswebsite wie iTunes heruntergeladen wurde. Die Qualität ist ziemlich gut, da sie nicht neu codiert werden. Die Video- (H.264 oder H.265) und Audio- (AC3/AAC) Streams werden in der Regel aus iTunes oder Amazon Video extrahiert und ohne Qualitätsverlust in einen MKV-Container remuxed. Ein Vorteil dieser Veröffentlichungen ist, dass sie, wie BD/DVDRips, in der Regel keine Netzwerklogos auf dem Bildschirm haben. Diese sind fast so gut wie eine Blu-ray-Quelle, können aber unter Audioverzögerungen oder visuellen Artefakten aufgrund der adaptiven Bitrate von Streaming-Diensten leiden. Wenn die Internetverbindung eines Rippers auf einen Punkt fällt, an dem die Bitrate sinkt, kann sich die Quellen-Bitrate dynamisch ändern, was zu Variationen in der Bildqualität führen kann. Die meisten Veröffentlichungen, die unter extremen visuellen Artefakten leiden, werden NUKED und in der Regel wird ein PROPER veröffentlicht, um wilde Variationen in der adaptiven Bitrate zu beheben. Dies wird in 2160p (4K) Qualität sein.
- WEBRip-2160p - Bei einem WEB-Rip (P2P) wird die Datei häufig mit den Protokollen HLS oder RTMP/E extrahiert und von einem TS-, MP4- oder FLV-Container in MKV remuxed. Dies wird in 2160p (4K) Qualität sein.
- Bluray-2160p - Eine Neu-Kodierung der endgültig veröffentlichten Blu-ray, in ihrer nativen 2160p-Auflösung (3840x2160 @ 16:9, jedes andere Seitenverhältnis kann eine andere Auflösung haben). 4K-Versionen von Filmen, die im Allgemeinen im HEVC-Codec vorliegen und entweder eine 8-Bit- oder 10-Bit-Farbwiedergabe oder eine HDR-Quelle haben können. Die Dateigröße wird geringfügig reduziert. Diese sind in der Regel MKV oder MP4-Container.
- Remux-2160p - Ein Remux ist ein Rip einer Blu-ray- oder HD-DVD-Disc in ein anderes Containerformat oder das Entfernen von Menüs und Bonusmaterial von der Disc, während die Inhalte ihrer Audio- und Videostreams intakt bleiben (auch die aktuellen Codecs beibehalten), wodurch die exakte 1:1-Filmqualität wie auf der Original-Disc garantiert wird. Dies ist in 2160p (4K) Qualität.

# Benutzerdefinierte Formate

{#custom-formats-2}

- Stellen Sie sicher, dass Sie jedes Mal die richtige Veröffentlichung erhalten! Benutzerdefinierte Formate ermöglichen eine feine Kontrolle über die Priorisierung und Auswahl von Veröffentlichungen. So einfach wie ein einzelnes bevorzugtes Wort oder so komplex wie Sie möchten, mit mehreren Kriterien und Regex.
- Benutzerdefinierte Formate werden dynamisch berechnet und nicht in der Datenbank gespeichert, sodass sie aktualisiert werden, sobald Sie die Definitionen ändern.
- Benutzerdefinierte Formate werden innerhalb Ihrer Qualitätsprofile verwendet, um die Bewertung jedes benutzerdefinierten Formats zu bestimmen. Innerhalb jedes Qualitätsprofils können Sie eine Mindestpunktzahl für ein benutzerdefiniertes Format festlegen, damit eine Veröffentlichung heruntergeladen wird, sowie eine Upgrade-Punktzahl.
- Es wird dringend empfohlen, die folgenden benutzerdefinierten Formate von [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) hinzuzufügen, um unerwünschte Downloads zu vermeiden. Weitere Informationen finden Sie im verlinkten TRaSH Guide Custom Format-Artikel und in den 3 zusätzlichen TRaSH Custom Format Guides oben auf der Seite Collection of Custom Formats.
  - [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) verhindert das Herunterladen von Veröffentlichungen mit Dolby Vision (DV), die einen grünen Farbton haben, wenn DV nicht unterstützt wird.
  - [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) verhindert das Herunterladen von schlecht benannten BR-DISKs, die nicht der BR-DISK-Qualitätsparsing entsprechen.

---

- Name - Der Name des benutzerdefinierten Formats
- Benutzerdefiniertes Format beim Umbenennen einschließen - Den Namen des benutzerdefinierten Formats beim Umbenennen einschließen?

> Benutzerdefinierte Formate haben keinen Einfluss darauf, wonach gesucht wird - nur wie die Ergebnisse bewertet werden. Es ist auch nicht möglich, die von Radarr verwendete Suche in irgendeiner Form zu ändern.
{.is-info}

Profile ist der Ort, an dem die Punktzahlen für benutzerdefinierte Formate konfiguriert werden.

## Bedingungen für benutzerdefinierte Formate

### Modifikatoren

- Negieren - Die Übereinstimmung wird invertiert, sodass die Bedingung erfüllt ist, wenn und nur wenn die nicht negierte Bedingung nicht erfüllt ist.
- Erforderlich - gilt nur für Formate mit mehr als einer Bedingung desselben Typs und ändert die Übereinstimmungsregeln für Typgruppen. Wenn diese Option aktiviert ist, muss diese spezifische Bedingung für das gesamte benutzerdefinierte Format erfüllt sein, unabhängig davon, ob eine andere Bedingung desselben Typs die Typgruppe erfüllen würde. **Hinweis: Sie verwenden dies nur, wenn Sie eine Bedingung mehr als einmal verwenden. Mit anderen Worten, wenn Sie ein benutzerdefiniertes Format mit 2 erforderlichen Bedingungen für den Veröffentlichungstitel und 3 nicht erforderlichen Sprachbedingungen haben, dann muss es BEIDE der erforderlichen Veröffentlichungstitel-Bedingungen erfüllen und EINE DER 3 Sprachbedingungen erfüllen.** Ebenso, wenn Sie ein benutzerdefiniertes Format mit 4 Veröffentlichungstitel-Bedingungen haben und keine davon erforderlich ist, wird das benutzerdefinierte Format angewendet, wenn IRGENDEINE der Bedingungen erfüllt ist.

### Bedingungen

> **Unterschiedliche Bedingungstypen** wirken als `und` innerhalb desselben benutzerdefinierten Formats. **Mehrere Bedingungen desselben Typs** wirken als `oder`, es sei denn, es wird "Erforderlich" verwendet.
{.is-info}

- **Alle Bedingungen, die RegEx verwenden, sind nicht groß-/kleinschreibungssensitiv**
- Beachten Sie die folgenden GitHub-Probleme
  - [Benutzerdefinierte Formate werden vor dem Filmjahr in Veröffentlichungstiteln nicht angewendet #4859](https://github.com/Radarr/Radarr/issues/4859)
  - [Benutzerdefiniertes Format passt nicht für den Begriff "xvid" am Ende des Veröffentlichungsnamens #6824](https://github.com/Radarr/Radarr/issues/6824)
- Veröffentlichungstitel - Dies ist ein regulärer Ausdruck, der mit dem Veröffentlichungstitel und nach dem Download mit dem Dateinamen auf der Festplatte abgeglichen wird.
  - Hinweis: Radarr berücksichtigt nur Text nach dem Filmtitel und dem Jahr, was bedeutet, dass alles vor dem Titel ignoriert wird.
- Edition - Dieser Tag wird mit allen Editionen abgeglichen, die Radarr analysieren kann. Sie können jeden Wert eingeben, den Radarr mit dem analysierten Wert abgleichen soll (Groß-/Kleinschreibung wird ignoriert).
- Sprache - Diese Sprache wird mit allen Sprachen abgeglichen, die Radarr analysiert. Alle zuvor in den Profilen auswählbaren Sprachen funktionieren hier.
- [Indexer-Flag](/radarr/settings#indexer-flags) - Dieser Tag wird mit allen Indexer-Flags abgeglichen, die Radarr analysieren kann.
- Quelle - Die Quelle, von der eine Veröffentlichung gerippt wurde (z.B. BLURAY).
- Auflösung - Die aus dem Veröffentlichungsnamen oder Mediainfo analysierte Auflösung.
- Qualitätsmodifikator - Der Qualitätsmodifikator legt Dinge wie Telescene, Telesync, Remux, Regional fest. Er unterscheidet ein bestimmtes Quellen- und Auflösungspaar, wenn mehrere Qualitäts (Quellen-)Typen zutreffen können.
- Größe - Dies wird mit der Veröffentlichungsgröße abgeglichen. Die Veröffentlichungsgröße wird in Gigabyte umgerechnet und mit den Mindest- und Maximalwerten verglichen.
- Gruppe - Dies wird mit der Gruppe abgeglichen, die Radarr basierend auf der Gruppenerkennungslogik von Radarr analysiert.

### Profilierungseinstellungen und Ranking

- Benutzerdefinierte Formate werden innerhalb von Qualitätsprofilen implementiert und haben ihren Einfluss durch diese gesteuert. Die Upgrade Until-Punktzahl verhindert ein Upgrade, sobald eine Veröffentlichung mit dieser gewünschten Punktzahl heruntergeladen wurde.
- Eine Punktzahl von 0 führt dazu, dass das benutzerdefinierte Format nur informativ ist und keinen Einfluss auf das Ranking der Veröffentlichung oder die gesuchten Sprachen hat.
- Die Mindestpunktzahl erfordert, dass die kumulative Punktzahl der benutzerdefinierten Formate von Veröffentlichungen diesen Schwellenwert erreicht, sonst werden sie abgelehnt.
  - Benutzerdefinierte Formate, die mit unerwünschten Attributen übereinstimmen, sollten eine negative Punktzahl erhalten, um ihre Attraktivität zu verringern.
  - Klare Ablehnungen sollten eine negative Punktzahl erhalten, die niedrig genug ist, dass selbst wenn alle anderen Formate mit positiven Punktzahlen hinzugefügt würden, die Punktzahl immer noch unterhalb des Minimums liegen würde.
- [Bitte sehen Sie sich TRaSH's Guides an, wie man benutzerdefinierte Formate einrichtet und verwendet](https://trash-guides.info/Radarr/Radarr-setup-custom-formats/)

#### Importieren / Exportieren von benutzerdefinierten Formaten

- [Bitte sehen Sie sich TRaSH's Guides an, wie man benutzerdefinierte Formate importiert/exportiert.](https://trash-guides.info/Radarr/Radarr-import-custom-formats/) Es ist jedoch möglich, benutzerdefinierte Formate zu importieren und zu exportieren.

#### Importieren / Aktualisieren vorhandener benutzerdefinierter Formate

- [Bitte sehen Sie sich TRaSH's Guides an, wie man vorhandene benutzerdefinierte Formate importiert oder aktualisiert.](https://trash-guides.info/Radarr/Radarr-how-to-update-custom-formats/)

### Sammlung von benutzerdefinierten Formaten

- [TRaSH pflegt eine Sammlung von benutzerdefinierten Formaten](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)

# Indexer

> Informationen zu unterstützten Indexern finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#indexers) für diesen Abschnitt
{.is-info}

## Unterstützte Indexer

- Eine Liste der unterstützten Indexer finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#indexers)

### Indexer-Einstellungen

- Sobald Sie auf die Schaltfläche <kb>+</kb> geklickt haben, um einen neuen Indexer hinzuzufügen, wird ein neues Fenster mit vielen verschiedenen Optionen angezeigt. Für die Zwecke dieses Wikis betrachtet Radarr sowohl Usenet-Indexer als auch Torrent-Tracker als "Indexer".

- Hier gibt es zwei Abschnitte: Usenet und Torrents. Abhängig von dem Download-Client, den Sie verwenden möchten, sollten Sie den Typ des Indexers auswählen, den Sie verwenden möchten.

### Usenet-Indexer-Konfiguration

- Newznab - Hier finden Sie voreingestellte populäre Usenet-Indexer (die bereits ausgefüllt sind, Sie benötigen lediglich Ihren API-Schlüssel, der vom Usenet-Indexer Ihrer Wahl bereitgestellt wird) sowie die Möglichkeit, einen benutzerdefinierten Indexer zu erstellen.
- Software, die gut mit Radarr zusammenarbeitet und mit Usenet und Torrents integriert ist, sind [NZBHydra2](https://github.com/theotherp/nzbhydra2/) oder [Prowlarr](/prowlarr).
- Unabhängig davon, ob Sie einen vorausgefüllten Indexer oder eine benutzerdefinierte Indexer-Konfiguration auswählen, wird ein neues Fenster angezeigt, in dem Sie alle Ihre Einstellungen eingeben können.
- Wählen Sie aus den voreingestellten Optionen oder fügen Sie einen benutzerdefinierten Indexer hinzu (wie z.B. NZBHydra2 oder Prowlarr).
- Name - Der Name des Indexers in Radarr.
- RSS aktivieren - Wenn aktiviert, wird dieser Indexer verwendet, um nach fehlenden oder noch nicht erreichten Cutoff-Dateien zu suchen.
- Automatische Suche aktivieren - Wenn aktiviert, wird dieser Indexer für automatische Suchvorgänge einschließlich der Suche beim Hinzufügen verwendet.
- Interaktive Suche aktivieren - Wenn aktiviert, wird dieser Indexer für manuelle interaktive Suchvorgänge verwendet.
- URL - Die vom Indexer bereitgestellte URL, z.B. `https://api.nzbgeek.info`.
- API-Pfad - Der vom Indexer bereitgestellte Pfad zur API. Dies ist in der Regel `/api`.
- Mehrsprachigkeit - Legen Sie fest, welche Sprachen für diesen Indexer verwendet werden sollen.
- API-Schlüssel - Der vom Indexer bereitgestellte Schlüssel zum Zugriff auf die API.
- Kategorien - Standardkategorien werden verwendet, es sei denn, sie werden bearbeitet. Wahrscheinlich sind diese Standardkategorien nicht optimal. Wenn Sie diese Einstellung bearbeiten, fragt Radarr den Indexer nach seinen verfügbaren Kategorien ab und zeigt sie in einer auswählbaren Liste an. Die veralteten Standardwerte werden gelöscht, sobald eine Kategorie umgeschaltet wird.
- (Erweiterte Option) Zusätzliche Parameter - Zusätzliche Newznab-Parameter, die dem Abfrage-Link hinzugefügt werden sollen.
- Jahr aus Suchzeichenkette entfernen - Soll Radarr das Jahr nach dem Filmtitel bei textbasierten Suchanfragen von diesem Indexer entfernen?
- (Erweiterte Option) Indexer-Priorität - Priorität dieses Indexers, um einen Indexer einem anderen in Szenarien mit gleichwertigen Veröffentlichungen vorzuziehen. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität.
- (Erweiterte Option) Download-Client - Wählen und geben Sie an, welcher Download-Client für Downloads von diesem Indexer verwendet wird.
- Tags - Verwenden Sie diesen Indexer nur für Filme mit mindestens einem übereinstimmenden Tag. Lassen Sie das Feld leer, um ihn für alle Filme zu verwenden.

### Torrent-Tracker-Konfiguration

- Wie beim Usenet gibt es eine Vielzahl von vorausgefüllten Torrent-Tracker-Informationen. Wenn Sie kein Mitglied dieser spezifischen Tracker sind, werden sie Ihnen nichts nützen.
- Eine der besten und einfachsten Möglichkeiten, Torrent-Tracker zu nutzen, die nicht nativ von Radarr unterstützt werden, besteht darin, ein zweites Programm wie [Prowlarr](/prowlarr) oder [Jackett](https://github.com/Jackett/Jackett) zu verwenden. Diese Software funktioniert gut mit Radarr als Suchindexer, der alle Ihre Informationen speichert und an Radarr sendet.
- Torznab - Diese Option richtet Sie mit einer Jackett-Voreinstellung ein. Wenn Sie mehrere Tracker verwenden, müssen Sie sicherstellen, dass jeder Eintrag einen eindeutigen Namen hat.
- Torznab-Indexer
- Wählen Sie aus den voreingestellten Optionen oder fügen Sie einen benutzerdefinierten Indexer hinzu (wie z.B. Jackett).
- Name - Der Name des Indexers in Radarr.
- RSS aktivieren - Wenn aktiviert, wird dieser Indexer verwendet, um nach fehlenden oder noch nicht erreichten Cutoff-Dateien zu suchen.
- Automatische Suche aktivieren - Wenn aktiviert, wird dieser Indexer für automatische Suchvorgänge einschließlich der Suche beim Hinzufügen verwendet.
- Interaktive Suche aktivieren - Wenn aktiviert, wird dieser Indexer für manuelle interaktive Suchvorgänge verwendet.
- URL - Die vom Indexer bereitgestellte URL, z.B. `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-Pfad - Der vom Indexer bereitgestellte Pfad zur API. Dies ist in der Regel `/api`.
- API-Schlüssel - Der vom Indexer bereitgestellte Schlüssel zum Zugriff auf die API.
- Mehrsprachigkeit - Legen Sie fest, welche Sprachen für diesen Indexer verwendet werden sollen.
- Kategorien - Standardkategorien werden verwendet, es sei denn, sie werden bearbeitet. Wahrscheinlich sind diese Standardkategorien nicht optimal. Wenn Sie diese Einstellung bearbeiten, fragt Radarr den Indexer nach seinen verfügbaren Kategorien ab und zeigt sie in einer auswählbaren Liste an. Die veralteten Standardwerte werden gelöscht, sobald eine Kategorie umgeschaltet wird.
- (Erweiterte Option) Zusätzliche Parameter - Zusätzliche Torznab-Parameter, die dem Abfrage-Link hinzugefügt werden sollen.
- Jahr aus Suchzeichenkette entfernen - Soll Radarr das Jahr nach dem Filmtitel bei textbasierten Suchanfragen von diesem Indexer entfernen?
- Mindestanzahl an Seedern - Die Mindestanzahl an Seedern, die für einen Release von diesem Tracker erforderlich ist, damit er heruntergeladen wird.
- Seed-Verhältnis - Wenn leer, wird der Standardwert des Download-Clients verwendet. Andernfalls ist das Mindest-Seed-Verhältnis erforderlich, das Ihr Download-Client für Releases von diesem Indexer erfüllen muss, bevor es von Ihrem Client pausiert und von Radarr entfernt wird (erfordert "Abgeschlossene Download-Verarbeitung - Entfernen" aktiviert).
- Seed-Zeit - Wenn leer, wird der Standardwert des Download-Clients verwendet. Andernfalls ist die Mindest-Seed-Zeit in Minuten erforderlich, die Ihr Download-Client für Releases von diesem Indexer erfüllen muss, bevor es von Ihrem Client pausiert und von Radarr entfernt wird (erfordert "Abgeschlossene Download-Verarbeitung - Entfernen" aktiviert).
- Erforderliche Flags - Welche Indexer-Flags sind erforderlich?

#### Indexer-Flags

| Flag             | Symbol | Beschreibung                                                                                                                                                                                                                 |
| ---------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `G_Freeleech`    | ⬇⬇     | Manchmal setzen Torrent-Seiten einen Torrent auf "Freeleech". Das bedeutet, dass der Download dieses Torrents nicht auf Ihr Download-Kontingent oder Ihre Ratio angerechnet wird. Dies ist sehr nützlich, wenn Sie noch keine gute Ratio aufgebaut haben. |
| `G_Halfleech`    | ⇩⇩     | Ähnlich wie `G_Freeleech` bedeutet `G_Halfleech`, dass nur die Hälfte der Größe dieses Torrents auf Ihr Download-Kontingent oder Ihre Ratio angerechnet wird.                                                                               |
| `G_DoubleUpload` | ⬆      | Ähnlich wie `G_Freeleech` bedeutet `G_DoubleUpload`, dass die von Ihnen über das Seeding hochgeladenen Daten doppelt auf Ihr Upload-Kontingent und Ihre Ratio angerechnet werden. Dies ist sehr nützlich, wenn Sie einen Ratio-Puffer aufbauen möchten.      |
| `PTP_Golden`     | 🌟      | Auf PassThePopcorn erhalten einige Torrents das Tag *Golden*, wenn sie bestimmte Kodierungsstandards erfüllen. Dies sind in der Regel die besten Kodierungen mit kaum wahrnehmbarem Qualitätsverlust. Weitere Informationen finden Sie in ihrem Wiki. |
| `PTP_Approved`   | ✔      | Auf PassThePopcorn werden einige Torrents genehmigt, wenn sie die Mindeststandards für die Kodierung erfüllen (z.B. keine niedrigen Bitraten). Weitere Informationen finden Sie in ihrem Wiki.                                                              |
| `HDB_Internal`   | 🚪      | Veröffentlichungen auf HDBits erhalten dieses Tag, wenn die Veröffentlichung von einer der Release-Gruppen von HDBits selbst hochgeladen wurde.                                                                                                       |
| `G_Scene`        | ☠      | Ähnlich wie `G_Freeleech` bedeutet `G_Freeleech75`, dass nur 25% der Größe dieses Torrents auf Ihr Download-Kontingent oder Ihre Ratio angerechnet wird.                                                                              |
| `G_Freeleech75`  | ⇩⬇     | Ähnlich wie `G_Freeleech` bedeutet `G_Freeleech75`, dass nur 25% der Größe dieses Torrents auf Ihr Download-Kontingent oder Ihre Ratio angerechnet wird.                                                                              |
| `G_Freeleech25`  | ⇩      | Ähnlich wie `G_Freeleech` bedeutet `G_Freeleech25`, dass nur 75% der Größe dieses Torrents auf Ihr Download-Kontingent oder Ihre Ratio angerechnet wird.                                                                              |

- (Erweiterte Option) Indexer-Priorität - Priorität dieses Indexers, um einen Indexer einem anderen in Szenarien mit gleichwertigen Veröffentlichungen vorzuziehen. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität.
- (Erweiterte Option) Download-Client - Wählen und geben Sie an, welcher Download-Client für Downloads von diesem Indexer verwendet wird.
- Tags - Verwenden Sie diesen Indexer nur für Filme mit mindestens einem übereinstimmenden Tag. Lassen Sie das Feld leer, um ihn für alle Filme zu verwenden.

## Optionen

- Mindestalter - Nur Usenet: Mindestalter in Minuten von NZBs, bevor sie heruntergeladen werden. Verwenden Sie dies, um neuen Veröffentlichungen Zeit zu geben, sich auf Ihrem Usenet-Anbieter zu verbreiten.
- Vorhaltezeit - Nur Usenet: Auf Null setzen, um eine unbegrenzte Vorhaltezeit festzulegen.
- Maximale Größe - Maximale Größe für einen Release, der heruntergeladen werden soll, in MB. Auf Null setzen, um unbegrenzte Größe festzulegen. Bitte beachten Sie, dass dies global gilt.
- Bevorzugte Indexer-Flags - Priorisieren Sie Veröffentlichungen mit speziellen Flags. (Siehe oben erforderliche Flags)
- Verfügbarkeitsverzögerung - Zeitraum vor (-#) oder nach (#) dem Verfügbarkeitsdatum, um nach einem Film zu suchen
  - Dies ist hilfreich, um die Suche nach einer Veröffentlichung zu verzögern und der Community Zeit zu geben, die besten Kodierungen durchzuführen.
  - In der Regel wird eine Filmverfügbarkeit von `Veröffentlicht` mit einer Verzögerung von `-21` oder `-14` empfohlen.
- RSS-Synchronisierungsintervall - Intervall in Minuten. Auf Null setzen, um zu deaktivieren (dadurch werden alle automatischen Release-Downloads gestoppt) Minimum: 10 Minuten Maximum: 120 Minuten
  - Bitte lesen Sie [Wie findet Radarr Filme?](/radarr/faq#how-does-radarr-find-movies) für ein besseres Verständnis, wie RSS-Synchronisierung Ihnen helfen kann.

> Wenn Radarr längere Zeit offline war, versucht Radarr, zurückzublättern, um die letzte verarbeitete Veröffentlichung zu finden, um zu vermeiden, dass eine Veröffentlichung verpasst wird. Solange Ihr Indexer das Blättern unterstützt und es nicht zu lange gedauert hat, kann Radarr die Veröffentlichungen verarbeiten, die es verpasst hätte, und Sie müssen keine Suche nach den verpassten Veröffentlichungen durchführen.{.is-info}

- Whitelist-Untertiteltags - Hier eingegebene Tags werden nicht als fest codierte Untertitel betrachtet.
- Fest codierte Untertitel zulassen - Wenn aktiviert, können Veröffentlichungen mit fest codierten Untertiteln automatisch heruntergeladen werden.

# Download-Clients

> Informationen zu unterstützten Download-Clients finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#download-clients) für diesen Abschnitt
{.is-info}

## Übersicht

- Das Herunterladen und Importieren ist der Bereich, in dem die meisten Benutzer Probleme haben. Aus einer übergeordneten Perspektive muss die Software in der Lage sein, mit Ihrem Download-Client zu kommunizieren und Zugriff auf die von ihm heruntergeladenen Dateien zu haben. Es gibt eine große Vielfalt an unterstützten Download-Clients und noch mehr verschiedene Setups. Das bedeutet, dass es zwar einige gemeinsame Setups gibt, aber kein einziges richtiges Setup und jedes Setup ein wenig anders sein kann. Es gibt jedoch viele falsche Setups.

## Ablauf der Download-Clients

### Usenet-Ablauf

- Radarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben. Beispiele: Filme, TV, Serien, Musik, etc.
- Radarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Radarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich an einem separaten Ort von Ihrem Medienordner befindet und von Radarr zugänglich ist.
- Radarr durchsucht diesen abgeschlossenen Speicherort nach Dateien, die Radarr verwenden kann. Es analysiert den Dateinamen, um ihn mit den angeforderten Medien abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie an den angegebenen Speicherort.
- Atomare Verschiebungen (sofortige Verschiebungen) sind standardmäßig aktiviert. Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek gleich sein. Wenn die atomare Verschiebung fehlschlägt oder Ihr Setup keine Hardlinks und atomare Verschiebungen unterstützt, wird Radarr auf das Kopieren der Datei zurückgreifen und sie dann von der Quelle löschen, was IO-intensiv ist.

### Torrent-Ablauf

- Radarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben. Beispiele: Filme, TV, Serien, Musik, etc.
- Radarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
- Abgeschlossene Dateien bleiben an ihrem ursprünglichen Speicherort, um Ihnen das Seeden der Datei zu ermöglichen (Verhältnis oder Zeit kann im Download-Client oder innerhalb von Radarr unter dem spezifischen Download-Client angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, erstellt Radarr einen Hardlink zur Datei, sofern dies von Ihrem Setup unterstützt wird, oder kopiert sie, wenn keine Hardlinks unterstützt werden.
- Hardlinks sind standardmäßig aktiviert. [Ein Hardlink benötigt keinen zusätzlichen Festplattenspeicher.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek gleich sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihr Setup keine Hardlinks unterstützt, wird Radarr auf das Kopieren der Datei zurückgreifen.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen von Radarr aktiviert ist, löscht Radarr die Originaldatei und den Torrent aus Ihrem Client, aber nur, wenn der Client meldet, dass das Seeden abgeschlossen ist und der Torrent gestoppt ist (d.h. pausiert).

- Name - Der Name des Download-Clients in Radarr
- Aktivieren - Aktivieren Sie diesen Download-Client
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients; dies ist in der Regel der WebGUI-Port
- SSL verwenden - Verwenden Sie eine sichere Verbindung mit Ihrem Download-Client. Bitte beachten Sie diesen häufigen Fehler.
- (Erweiterte Option) URL-Basis - Fügen Sie einen Präfix zur URL hinzu; dies ist häufig für Reverse Proxies erforderlich.
- Benutzername - der Benutzername zur Authentifizierung bei Ihrem Client
- Passwort - das Passwort zur Authentifizierung bei Ihrem Client
- Kategorie - die Kategorie in Ihrem Download-Client, die von \*Arr verwendet wird. Um irrelevante Downloads in der Aktivität zu vermeiden, wird dringend empfohlen, eine Kategorie festzulegen.
- Kategorie nach dem Import - die Kategorie, die nach dem Herunterladen und Importieren der Veröffentlichung festgelegt werden soll. Bitte beachten Sie, dass dadurch die Entfernung der abgeschlossenen Download-Verarbeitung unterbrochen wird.
- Aktuelle Priorität - Download-Client-Priorität für kürzlich veröffentlichte Medien
- Ältere Priorität - Download-Client-Priorität für nicht kürzlich veröffentlichte Medien
- Anfangszustand - Anfangszustand für Torrents (nur Qbittorrent: Erzwingt das Überspringen aller Seed-Schwellenwerte)
- (Erweiterte Option) Client-Priorität - Priorität des Download-Clients. Round-Robin wird für Clients desselben Typs (Torrent/Usenet) verwendet, die dieselbe Priorität haben. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität
- Abgeschlossene Download-Verarbeitung
  - Entfernen (Pro Client-Einstellung) - Entfernen Sie abgeschlossene Downloads, wenn sie fertiggestellt (Usenet) oder gestoppt/abgeschlossen (Torrents) sind. Weitere Informationen finden Sie unter [Abgeschlossene Download-Verarbeitung](#abgeschlossene-download-verarbeitung)
    - Für Torrents muss Ihr Download-Client pausieren, wenn die Seed-Ziele erreicht sind. Es erfordert auch, dass die Seed-Ziele von Radarr gemäß der unten stehenden Tabelle unterstützt werden. Torrents müssen auch in derselben Kategorie bleiben.

### Kompatibilität der Torrent-Client-Entfernung des Downloads

- Radarr kann nur das Seed-Verhältnis/-Zeit bei Clients einstellen, die diesen Wert über ihre API beim Hinzufügen des Torrents festlegen können. Seed-Ziele können global im Client selbst oder pro Tracker in den \*Arr-Einstellungen für jeden Indexer festgelegt werden. In der folgenden Tabelle finden Sie Informationen zur Kompatibilität des Clients.

|      Client       |                                Verhältnis                                |                                    Zeit                                    |
| :---------------: | :---------------------------------------------------------------------: | :------------------------------------------------------------------------: |
|       Aria2       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |    ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)    |
|      Deluge       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |    ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)    |
| Download Station  | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |    ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)    |
|       Flood       |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |      ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)      |
|     Hadouken      | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |    ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)    |
|    qBittorrent    |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |      ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)      |
|     rTorrent      |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |      ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)      |
| Torrent Blackhole | ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch) |    ![Nicht unterstützt](https://img.shields.io/badge/Unterstützt-Nein-kritisch)    |
|   Transmission    |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Unterstützt-Idle%20Limit*-blue)\* |
|     uTorrent      |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |      ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)      |
|       Vuze        |   ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)   |      ![Unterstützt](https://img.shields.io/badge/Unterstützt-Ja-success)      |

> ![Idle Limit](https://img.shields.io/badge/Unterstützt-Idle%20Limit*-blue) - Transmission hat intern eine Idle-Zeitprüfung, aber Radarr vergleicht sie mit der Seed-Zeit, wenn das Idle-Limit pro Torrent festgelegt ist. Dies geschieht als Workaround für die API-Beschränkungen von Transmission.{.is-info}

## Abgeschlossene Download-Verarbeitung

- Die abgeschlossene Download-Verarbeitung ist der Vorgang, mit dem Radarr Medien von Ihrem Download-Client in Ihre Serienordner importiert. Viele häufige Probleme hängen mit falschen Docker-Pfaden und/oder anderen Docker-Berechtigungsproblemen zusammen.

- (Erweiterte globale Einstellung) Aktivieren - Importieren Sie abgeschlossene Downloads automatisch aus dem Download-Client
- (Erweiterte Option) Intervall für die Überprüfung abgeschlossener Downloads - Legen Sie fest, wie oft die Warteschlangen der Download-Clients abgefragt und überwachte Downloads aktualisiert werden sollen, mindestens 1 Minute
- (Pro Client-Einstellung) Entfernen - Entfernen Sie abgeschlossene Downloads, wenn sie fertiggestellt (Usenet) oder gestoppt/abgeschlossen (Torrents) sind
  - Für Torrents muss Ihr Download-Client pausieren, wenn die Seed-Ziele erreicht sind. Es erfordert auch, dass die Seed-Ziele von Radarr gemäß der obigen Tabelle unterstützt werden. Torrents müssen auch in derselben Kategorie bleiben.

### Entfernen abgeschlossener Downloads

- Radarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben.
- Radarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Radarr den endgültigen Dateispeicherort, wie er von Ihrem Download-Client gemeldet wird. Dieser Dateispeicherort kann sich fast überall befinden, solange er sich an einem separaten Ort von Ihrem Medienordner befindet.
- Radarr durchsucht diesen abgeschlossenen Dateispeicherort nach Videodateien. Es analysiert den Videodateinamen, um ihn mit einem Film abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie in den zugewiesenen Bibliotheksordner.
- Übrig gebliebene Dateien aus dem Download werden in den Papierkorb oder das Recycling gesendet.

Wenn Sie mit einem BitTorrent-Client herunterladen, ist der Vorgang etwas anders:

- Abgeschlossene Dateien bleiben an ihrem ursprünglichen Speicherort, um das Seeden zu ermöglichen. Wenn Dateien in Ihren zugewiesenen Bibliotheksordner importiert werden, versucht Radarr, die Datei über einen Hardlink zu verknüpfen oder verwendet eine Kopie (verwendet doppelten Speicherplatz), wenn Hardlinks nicht unterstützt werden.
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen aktiviert ist, fordert Radarr den Torrent-Client auf, die Originaldatei und den Torrent zu löschen. Dies erfolgt jedoch nur, wenn der Client meldet, dass das Seeden abgeschlossen ist, der Torrent sich in derselben Kategorie befindet (d. h. keine Verwendung einer Kategorie nach dem Import), das von Radarr unterstützte Seed-Ziel erreicht ist und der Torrent pausiert (gestoppt) ist.

### Fehlgeschlagene Download-Verarbeitung

- Die fehlgeschlagene Download-Verarbeitung ist nur mit SABnzbd und NZBGet kompatibel.
- Die fehlgeschlagene Download-Verarbeitung gilt nicht für Torrents und es sind keine Pläne vorhanden, eine solche Funktionalität hinzuzufügen.

- Der Prozess der fehlgeschlagenen Download-Verarbeitung besteht aus mehreren Komponenten:

- Überprüfung des Downloaders:
  - Warteschlange - Überprüfen Sie die Warteschlange Ihres Downloaders auf passwortgeschützte (verschlüsselte) Veröffentlichungen, die als Fehler markiert sind
  - Verlauf - Überprüfen Sie den Verlauf Ihres Downloaders auf Fehler (z. B. nicht genug zum Reparieren oder Extrahieren fehlgeschlagen)
- Wenn Radarr einen fehlgeschlagenen Download findet, beginnt es mit der Verarbeitung und führt einige Aktionen aus:
  - Fügt ein fehlgeschlagenes Ereignis zum Verlauf von Radarr hinzu
  - Entfernt den fehlgeschlagenen Download aus dem Download-Client, um Speicherplatz freizugeben und heruntergeladene Dateien zu löschen (optional)
  - Beginnt mit der Suche nach einer Ersatzdatei (optional)
  - Blocklistung (ehemals "Blacklisting") ermöglicht das automatische Überspringen von NZBs, wenn sie fehlschlagen. Das bedeutet, dass das NZB nie wieder automatisch von Radarr heruntergeladen wird (Sie können den Download jedoch weiterhin über eine manuelle Suche erzwingen).
  - Es gibt 2 erweiterte Optionen (auf der Seite "Download-Client" Einstellungen), die das Verhalten der fehlgeschlagenen Downloads in Radarr steuern. Derzeit sind sie alle standardmäßig aktiviert.

- Erneut herunterladen - Steuert, ob Radarr nach einem Fehler nach derselben Datei sucht
- (Erweiterte Option) Entfernen - Ob der Download automatisch aus dem Download-Client entfernt werden soll, wenn der Fehler erkannt wird

## Remote-Pfadzuordnungen

- Die Remote-Pfadzuordnung fungiert als einfache Suche nach Remote-Pfad und Ersetzung durch lokalen Pfad. Dies wird hauptsächlich für zusammengeführte lokale/Remote-Setups mit MergerFS oder ähnlichem verwendet oder wenn die Anwendung und der Download-Client nicht auf demselben Server sind.
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht in diesem Ordner behandelt wird.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft, während \*Arr auf Windows oder umgekehrt läuft. Eine Remote-Pfadzuordnung ist auch möglicherweise erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine einfache Suche/Ersetzung (wenn der REMOTE-Wert gefunden wird, ersetzen Sie ihn durch den LOCAL-Wert für den angegebenen Host).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie im Tutorial von TRaSH](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist eine Remote-Pfadzuordnung selten erforderlich. Es wird empfohlen, [den Docker-Leitfaden](/docker-guide) zu überprüfen und/oder [dem Tutorial von TRaSH](https://trash-guides.info/hardlinks) zu folgen.{.is-info}

# Import-Listen

> Informationen zu unterstützten Listentypen finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#lists) für diesen Abschnitt
{.is-info}

## Listen

Import-Listen sind ein Teil von Radarr, mit denen Sie einem bestimmten Listen-Ersteller folgen können. Angenommen, Sie folgen einem bestimmten Listen-Ersteller auf Trakt/TMDb und mögen besonders seine ArrowVerse Collection-Sektion und möchten jede Show auf seiner Liste sehen. Sie schauen in Ihrem Radarr nach und stellen fest, dass Sie diese Serien nicht haben. Anstatt einzeln zu suchen und diese Elemente hinzuzufügen und dann Ihre Indexer nach diesen Serien zu durchsuchen, können Sie dies alles auf einmal mit einer Liste tun. Die Listen können so eingestellt werden, dass alle Serien auf der Liste des Kurators importiert werden und automatisch ein Qualitätsprofil zugewiesen, automatisch hinzugefügt und automatisch überwacht werden.

- VORSICHT: Wenn Listen falsch gemacht werden, werden sie Ihre Bibliothek mit einem Haufen Müll zerstören, den Sie nicht sehen möchten. Stellen Sie also sicher, was Sie importieren, bevor Sie auf Speichern klicken. D.h. schauen Sie sich die Liste an, bevor Sie überhaupt zu Radarr gehen.

- Hier können Sie auf die Schaltfläche <kb>+</kb> klicken, um ein neues Popup-Fenster zu öffnen
- In diesem neuen Fenster werden Ihnen viele verschiedene Optionen angezeigt, um Ihre Liste von vielen verschiedenen Listenanbietern einzurichten. Wie bereits erwähnt, seien Sie vorsichtig bei der Erstellung von Listen. Es wird dringend empfohlen, die Option "Bei Hinzufügen suchen" nicht auszuwählen, bevor Sie sicher sind, dass die Liste, die Sie auswählen/einrichten, die Serien hinzufügt, die Sie suchen.
- Sobald Sie den Listenanbieter ausgewählt haben, von dem Sie ziehen möchten (z.B. IMDb oder Trakt), wird Ihnen ein neues Fenster angezeigt.
Die meisten Einstellungen der Listen sind ziemlich selbsterklärend, einige Listen erfordern eine Authentifizierung beim Anbieter wie Trakt (Sie müssen ein Konto bei Trakt.tv haben).

## Listeneinstellungen

- (Erweiterte Option) Intervall für die Aktualisierung der Liste - Wie oft soll Radarr die Liste auf Aktualisierungen überprüfen? [Dies ist ein Minimum von 6 Stunden.](/radarr/faq#why-are-lists-sync-times-so-long-and-can-i-change-it)
- (Erweiterte Option) Bereinigungsstufe der Bibliothek - Filme in der Bibliothek werden entfernt oder nicht überwacht, wenn sie nicht in Ihren Liste(n) enthalten sind
  - Deaktiviert - Die Bibliothek nicht bereinigen (empfohlen)
  - Nur protokollieren - Nur die Filme protokollieren, die nicht auf den Liste(n) stehen, und keine weiteren Maßnahmen ergreifen
  - Film behalten und nicht überwachen - Filme, die nicht auf den Liste(n) stehen, behalten, aber in Radarr nicht überwachen.
  - Film entfernen und Dateien behalten - Filme, die nicht auf den Liste(n) stehen, aus Radarr entfernen, aber ihre Dateien nicht löschen
  - Film entfernen und Dateien löschen - Filme, die nicht auf den Liste(n) stehen, aus Radarr entfernen und ihre Dateien löschen

## Liste der Ausnahmen

- Import-Listenausnahme - Dadurch können Sie Ihre Liste von Filmen bereinigen, die Sie nicht mehr sehen möchten. Ein Beispiel dafür ist, wenn Ihre Liste zufällig einen Film enthält, der in einer Fremdsprache ist und es unwahrscheinlich ist, dass Sie diesen Film jemals in Ihrer Muttersprache finden und ihn nicht mit Untertiteln ansehen möchten. Sie können einen Film von der zukünftigen Hinzufügung ausschließen. In der Liste der Ausnahmen können Sie ihn jedoch wieder zur Liste hinzufügen, sodass er beim erneuten Ausführen der Liste in Ihre Bibliothek gelesen wird.

# Verbindungen

> Informationen zu unterstützten Verbindungstypen finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#notifications) für diesen Abschnitt
{.is-info}

## Verbindungen

Verbindungen sind die Art und Weise, wie Sie möchten, dass Radarr mit der Außenwelt kommuniziert.

- Durch Drücken der Schaltfläche <kb>+</kb> werden Sie mit einem neuen Fenster präsentiert, in dem Sie viele verschiedene Endpunkte konfigurieren können

- Eine Liste der unterstützten Benachrichtigungen und Verbindungen finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#notifications)

## Verbindungsauslöser

- Bei Grab - Benachrichtigt werden, wenn Filme zum Download verfügbar sind und an einen Download-Client gesendet wurden
- Bei Import - Benachrichtigt werden, wenn Filme erfolgreich importiert wurden
- Bei Upgrade - Benachrichtigt werden, wenn Filme auf eine bessere Qualität aktualisiert werden
- Bei Umbenennung - Benachrichtigt werden, wenn Filme umbenannt werden
- Bei Hinzufügen von Filmen - Benachrichtigt werden, wenn Filme zur Radarr-Bibliothek hinzugefügt werden, um sie zu verwalten oder zu überwachen
- Bei Löschung von Filmen - Benachrichtigt werden, wenn Filme gelöscht werden
- Bei Löschung von Filmdateien - Benachrichtigt werden, wenn Filmdateien gelöscht werden
- Bei Löschung von Filmdateien für ein Upgrade - Benachrichtigt werden, wenn Filmdateien für Upgrades gelöscht werden
- Bei Problemen mit der Gesundheit - Benachrichtigt werden bei Fehlern bei der Gesundheitsprüfung
  - Gesundheitswarnungen einschließen - Benachrichtigt werden bei Gesundheitswarnungen zusätzlich zu Fehlern.
- Bei Aktualisierung der Anwendung - Benachrichtigt werden, wenn Radarr auf eine neue Version aktualisiert wird

# Metadaten

## Optionen

- Zertifizierungsland - Wählen Sie das Land für Filmzertifizierungen aus (z. B. R (US) oder 12A (UK))

## Metadaten-Verbraucher

> Informationen zu unterstützten Metadaten-Verbrauchern finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/radarr/supported#metadata) für diesen Abschnitt
{.is-info}

Hier können Sie den Typ der Metadaten auswählen, die von Ihrem Media Player verwendet werden sollen

Kodi wird hier eine der am häufigsten verwendeten Optionen sein, wenn dies die verwendete Software ist. Dadurch kann Radarr eine NFO-Datei erstellen und zugehörige Filmplakate in Ihren Player einlesen

# Tags

- Der Tag-Bereich in Radarr wird verwendet, um verschiedene Aspekte von Radarr zu verknüpfen. Sie sind auch nützlich, um zu verfolgen, welche Filme aus welchen Listen stammen.
- Tags sind besonders nützlich für:

  - Verzögerungsprofile
  - Einschränkungen
  - Indexer

- Tags können verwendet werden, um Verzögerungsprofile, Indexer und Einschränkungen und Filme miteinander zu verknüpfen.
- Zum Beispiel:
  - Sie möchten, dass ein bestimmter Indexer nur für einen bestimmten Film verwendet wird. Sie würden einen Tag erstellen und dem Film und dem Indexer diesen Tag zuweisen.
  - Sie möchten, dass eine bestimmte Einschränkung nur für einen bestimmten Film gilt. Sie würden einen Tag erstellen und der Einschränkung und dem Film diesen Tag zuweisen.
  - Dieser Vorgang ist für Verzögerungsprofile gleich.

> Ein Film verwendet sowohl Indexer mit übereinstimmenden Tags als auch Indexer ohne Tags.
{.is-warning}

> Hinweis: Tags beeinflussen keine "Benutzerdefinierten Formate", "Qualitätsprofile" oder andere nicht oben genannte Aspekte.
{.is-info}

# Allgemein

## Host

- Bind-Adresse - Gültige IPv4-Adresse oder '*' für alle Schnittstellen
  - 0.0.0.0 oder `*` - jede Adresse kann sich verbinden
  - 127.0.0.1 oder localhost - nur Anwendungen auf dem lokalen Host können sich verbinden
  - Jede andere IP (z.B. 1.2.3.4) - nur diese IP (1.2.3.4) kann sich verbinden
- Portnummer - Die Portnummer, die Sie verwenden möchten, um auf die WebUI für Radarr zuzugreifen

> Hinweis: Wenn Sie Docker verwenden, ändern Sie diese Einstellung nicht.
{.is-warning}

- URL-Basis - Für Reverse-Proxy-Unterstützung, Standard ist leer

> Hinweis: Wenn Sie einen Reverse-Proxy verwenden (Beispiel: mydomain.com/radarr), geben Sie '/radarr' für die URL-Basis ein.
{.is-info}

- SSL aktivieren - Wenn Sie SSL-Zugangsdaten haben und die Kommunikation zu und von Ihrem Radarr absichern möchten, aktivieren Sie diese Option.

> Hinweis: Verwenden Sie dies nicht, es sei denn, Sie wissen, was Sie tun.
{.is-warning}

## Sicherheit

- Authentifizierung - Wie möchten Sie sich authentifizieren, um auf Ihre Radarr-Instanz zuzugreifen
  - Ab Radarr v5 ist die Authentifizierung jetzt obligatorisch. [Weitere Informationen finden Sie in der FAQ zur obligatorischen Authentifizierung.](/radarr/faq#forced-authentication)
  - ~~Keine - Sie haben keine Authentifizierung, um auf Ihre Radarr zuzugreifen. Normalerweise, wenn Sie der einzige Benutzer Ihres Netzwerks sind, niemanden in Ihrem Netzwerk haben, der auf Ihre Radarr zugreifen möchte, oder Ihre Radarr nicht im Web verfügbar ist~~
  - Basic (Browser-Popup) - Diese Option zeigt beim Zugriff auf Ihre Radarr ein kleines Popup an, in dem Sie einen Benutzernamen und ein Passwort eingeben können
  - Forms (Anmeldeseite) - Diese Option zeigt eine vertraut aussehende Anmeldeseite an, ähnlich wie bei anderen Websites, um sich bei Ihrer Radarr anzumelden
- API-Schlüssel - So kommunizieren andere Programme oder lassen Radarr mit anderen Programmen kommunizieren. Dieser Schlüssel kann bei unbefugtem Zugriff alle möglichen Dinge mit Ihrer Bibliothek tun. Aus diesem Grund wird der API-Schlüssel in den Protokollen geschwärzt.
- Zertifikatsvalidierung - Ändern Sie, wie streng die HTTPS-Zertifikatsvalidierung ist
  - Aktiviert - Überprüfen Sie alle HTTPS-Zertifikate (empfohlen)
  - Deaktiviert für lokale Adressen - Überprüfen Sie alle HTTPS-Zertifikate, außer denen auf localhost und im LAN
  - Deaktiviert - Überprüfen Sie keine HTTPS-Zertifikate

## Proxy

Proxy - Diese Option ermöglicht es Ihnen, die von Radarr abgerufenen Informationen und Suchvorgänge über einen Proxy laufen zu lassen. Dies kann nützlich sein, wenn Sie in einem Land sind, das das Herunterladen von Torrent-Dateien nicht erlaubt.

- Proxy verwenden - Aktivieren Sie dies, um einen Proxy zu verwenden
- Proxy-Typ - Wählen Sie Ihren Proxy-Typ (HTTPS, Socks4 oder Socks5)
- Hostname - Geben Sie Ihren Proxy-Hostname ein (ohne http/https oder ein anderes Protokoll)
- Port - Geben Sie Ihren Proxy-Port ein
- Benutzername - Geben Sie Ihren Proxy-Benutzernamen ein, falls zutreffend
- Passwort - Geben Sie Ihr Proxy-Passwort ein, falls zutreffend
- Ignorierte Adressen - Geben Sie eine durch Kommas getrennte Liste von Adressen ein, die den Proxy umgehen sollen
- Proxy für lokale Adressen umgehen - Aktivieren Sie das Kontrollkästchen, um den Proxy für lokale Adressen zu umgehen. Lokale Anfragen werden durch das Fehlen eines Punktes (.) in der URI identifiziert, z.B. <http://webserver/> oder Zugriff auf den lokalen Server, einschließlich <http://localhost>, <http://loopback> oder <http://127.0.0.1>. Wenn dies nicht aktiviert ist, werden alle Internetanfragen über den Proxyserver gesendet.

## Protokollierung

- Protokollstufe - Wahrscheinlich eines der nützlichsten Fehlerbehebungswerkzeuge
  - Info - Dies ist die grundlegendste Art und Weise, wie Radarr Informationen sammelt. Dies enthält nur eine sehr geringe Menge an Informationen in den Protokollen. Diese Protokolldatei enthält Einträge zu Fehlern, Warnungen und Informationen.
  - Debug - Debug enthält alle Informationen, die Info enthält, sowie zusätzliche nützliche Informationen. Diese Protokolldatei enthält Einträge zu Fehlern, Warnungen, Informationen und Debugging.
  - Trace - Das detaillierteste Protokollieren auf Radarr, Trace enthält alle Informationen, die von Info und Debug gesammelt wurden und mehr. Dies ist die häufigste Art von Protokoll, die bei der Fehlerbehebung auf Discord oder Reddit angefordert wird. Wenn Sie Hilfe benötigen, wählen Sie bitte Ihr Protokoll auf Trace und wiederholen Sie die Aufgabe, die Ihnen Probleme bereitet hat, um das Protokoll zu erfassen. Diese Protokolldatei enthält Einträge zu Fehlern, Warnungen, Informationen, Debugging und Trace.

## Analytik

- Analytik - Senden Sie anonyme Nutzungs- und Fehlerinformationen an die Server von Radarr (Servarr). Dies umfasst Informationen über Ihren Browser, welche Radarr WebUI-Seiten Sie verwenden, Fehlerberichte sowie Betriebssystem- und Laufzeitversionen. Wir werden diese Informationen verwenden, um Funktionen und Fehlerbehebungen zu priorisieren.

## Updates

- (Erweiterte Option) Branch - Dies ist der Zweig von Radarr, den Sie verwenden.
  - [Bitte sehen Sie sich diesen FAQ-Eintrag für weitere Informationen an](/radarr/faq#how-do-i-update-radarr)
- Automatisch - Updates automatisch herunterladen und installieren. Sie können weiterhin über System: Updates installieren. Hinweis: Windows-Benutzer werden immer automatisch aktualisiert.
- Mechanismus - Verwenden Sie den integrierten Radarr-Updater oder ein Skript
  - Integriert - Verwenden Sie den eigenen Updater von Radarr
  - Skript - Lassen Sie Radarr das Aktualisierungsskript ausführen
  - Docker - Aktualisieren Sie Radarr nicht innerhalb des Docker, sondern ziehen Sie ein brandneues Image mit dem neuen Update
- Skript - Nur sichtbar, wenn der Mechanismus auf Skript eingestellt ist - Pfad zum Aktualisierungsskript
- Aktualisierungsprozess - Radarr lädt die Aktualisierungsdatei herunter, überprüft deren Integrität, extrahiert sie an einen temporären Speicherort und ruft die gewählte Methode auf. Der Aktualisierungsprozess wird unter demselben Benutzer ausgeführt, unter dem Radarr ausgeführt wird. Es werden Berechtigungen benötigt, um die Radarr-Dateien zu aktualisieren sowie Radarr zu starten/stoppen.
- Integriert - Die integrierte Methode sichert Radarr-Dateien und -Einstellungen, stoppt Radarr, aktualisiert die Installation und startet Radarr. Wenn Ihr System das Stoppen von Radarr nicht verarbeiten kann und versucht, es automatisch neu zu starten, ist es möglicherweise besser, stattdessen ein Skript zu verwenden. Im Falle eines Fehlers wird die vorherige Version von Radarr neu gestartet.
- Skript - Das Skript sollte das gleiche wie der integrierte Updater behandeln. Wenn Sie das Starten und Stoppen von Diensten (upstart/launchd/etc) verwalten müssen, müssen Sie dies hier tun.

## Backups

- Der Backup-Bereich ermöglicht es Ihnen, Radarr mitzuteilen, wie Sie Backups behandeln möchten

- (Erweiterte Option) Ordner - Hier können Sie den Speicherort für das Backup auswählen. In Docker sind Sie auf das beschränkt, was der Container sehen darf. Pfade sind relativ zum Appdata-Ordner; falls erforderlich, können Sie einen absoluten Pfad angeben, um außerhalb des Appdata-Ordners zu sichern.
- (Erweiterte Option) Intervall - Wie oft soll Radarr ein Backup erstellen?
- (Erweiterte Option) Aufbewahrung - Wie lange soll Radarr jedes Backup aufbewahren? Nachdem ein neues Backup erstellt wurde, wird das älteste Backup entfernt.

> Manuelle Backups werden für immer aufbewahrt, im selben Ordner gespeichert und haben einen anderen Namen.
{.is-info}

# Benutzeroberfläche

## Kalender

- Erster Tag der Woche - Hier können Sie auswählen, welcher Tag als erster Tag der Woche gelten soll.
- Spaltenüberschrift der Woche - Hier können Sie die Überschrift für die Spalten auswählen

## Filme

- Laufzeitformat - Wählen Sie aus, wie Laufzeiten formatiert werden sollen, entweder Stunden & Minuten oder Minuten

## Daten

- Kurzes Datumsformat - Wie möchten Sie, dass Radarr kurze Datumsangaben anzeigt?
- Langes Datumsformat - Wie möchten Sie, dass Radarr lange Datumsangaben anzeigt?
- Zeitformat - Möchten Sie ein 12-Stunden- oder 24-Stunden-Format?
- Relative Daten anzeigen - Möchten Sie, dass Radarr relative (Heute/Gestern/usw.) oder absolute Daten anzeigt?

## Stil

- Farbfehlsichtigkeitsmodus aktivieren - Geänderter Stil, um farbfehlsichtigen Benutzern eine bessere Unterscheidung von farbcodierten Informationen zu ermöglichen

## Sprache

- Filmsprache - Wählen Sie die Sprache, in der Radarr Filminformationen in der Benutzeroberfläche anzeigen soll
- Benutzeroberflächensprache - Wählen Sie die Sprache, die Radarr in der Anwendungs-Benutzeroberfläche verwenden soll