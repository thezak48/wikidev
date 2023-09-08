---
title: Readarr Unterstützt
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> Diese Seite ist noch in Bearbeitung und erfordert zusätzliche Anstrengungen.{.is-warning}

Diese Seite ist die Disambiguierungsseite für alle "unterstützten" Wiki-Links (normalerweise "Weitere Informationen" in der Benutzeroberfläche).

# Download-Clients

{#downloadclient}

- Aria2 {#aria2}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Flood {#flood}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)
  - Da uTorrent Adware und früher Spyware ist, wird es nicht empfohlen. Die meisten Benutzer verwenden qBittorrent.
- Vuze {#vuze}
  - [Siehe die Einstellungsseite](/readarr/settings#download-clients)

# Indexer

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
  - Newznab ist eine standardisierte API, die von vielen Usenet-Indexseiten verwendet wird. Es gibt viele Voreinstellungen, aber alle erfordern einen API-Schlüssel, um zugänglich zu sein.
  - Indexer-Anwendungen wie [Prowlarr](/prowlarr) und [NZBHydra2](https://github.com/theotherp/nzbhydra2) können erweiterte Funktionen wie Statistik-Tracking bieten.
- omgwtfnzbs {#omgwtfnzbs}
  - Ein privater Usenet-Indexer
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privater Tracker
  > Die native Implementierung von IP Torrents unterstützt keine Suche {.is-info}
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-Tracker ausschließlich für japanische Medien (Anime).
  > Nyaa ist gegen Automatisierung und sperrt häufig Ihre IP-Adresse. {.is-info}
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Öffentlicher Tracker
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
- Torrent-RSS-Feed {#torrentrssindexer}
  - Generischer Torrent-RSS-Feed-Parser.
  > Der RSS-Feed muss ein `pubdate` enthalten. Die Freigabegröße wird ebenfalls empfohlen. {.is-info}
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privater Indexer
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab ist ein Wortspiel aus Torrent und Newznab. Es verwendet die gleiche Struktur und Syntax wie die Newznab-API-Spezifikation, stellt jedoch torrent-spezifische Attribute und .torrent-Dateien bereit. Es unterstützt daher einen aktuellen RSS-Feed und die Möglichkeit zur Rückwärtssuche. Die Spezifikation wird von der Newznab-Organisation nicht gewartet oder unterstützt. (Die gleiche API-Spezifikation wird mit nZEDb geteilt)
  - Dies wird hauptsächlich von [Prowlarr](/prowlarr) und [Jackett](https://github.com/Jackett/Jackett) unterstützt.
  - [Siehe die Einstellungsseite](/readarr/settings#indexer-settings)

# Benachrichtigungen

{#notification}

- Boxcar {#boxcar}
- Benutzerdefiniertes Skript {#customscript}
  - Damit können Sie ein benutzerdefiniertes Skript erstellen, das ausgeführt wird, wenn eine bestimmte Aktion erfolgt. Weitere Informationen finden Sie unter [Benutzerdefinierte Skripte](/readarr/custom-scripts).
- Discord {#discord}
  - Mit Abstand eine der häufigsten Möglichkeiten, Benachrichtigungen über Aktionen auf Ihrem Readarr zu erhalten.
- E-Mail {#email}
  - Senden Sie sich selbst oder jemandem, den Sie mit E-Mails belästigen möchten, eine E-Mail. Wenn Sie Gmail verwenden, müssen Sie weniger sichere Apps aktivieren. Wenn Sie Gmail verwenden und die Zwei-Faktor-Authentifizierung aktiviert haben, müssen Sie ein App-spezifisches Passwort verwenden.

 > Sie können eine "schöne Adresse" wie `SomePrettyName <email@example.org>` verwenden {.is-info}

- GoodReads-Bücherregale {#goodreadsbookshelf}
- GoodReads-Eigene Bücher {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Siehe den Eintrag zu [Nützlichen Tools - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology-Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Siehe diesen Eintrag zu [Tipps und Tricks](/useful-tools#twitter)
- Webhook {#webhook}

# Listen

{#importlist}

- GoodReads-Bücherregale {#goodreadsbookshelf}
  - (Erweiterte Option) Benutzer-ID - Geben Sie hier eine Benutzer-ID ein, wenn es sich nicht um Ihre eigene Benutzer-ID handelt.
  - Bücherregale - Wählen Sie aus, welche Bücherregale von GoodReads importiert werden sollen.
  - Mit GoodReads authentifizieren - Klicken Sie auf die Schaltfläche, um sich mit GoodReads zu authentifizieren.

> Mehrere GoodReads-Benutzer können als separate Listen hinzugefügt werden. Zusätzlich zur Verwendung eines authentifizierten Benutzers können andere Benutzer hinzugefügt werden, indem erweiterte Optionen aktiviert und die Benutzer-ID eingegeben werden. Klicken Sie dann auf "Mit GoodReads authentifizieren", um die Regale des Benutzers abzurufen. {.is-info}

- GoodReads-Eigene Bücher {#goodreadsownedbooks}
  - (Erweiterte Option) Benutzer-ID - Geben Sie hier eine Benutzer-ID ein, wenn es sich nicht um Ihre eigene Benutzer-ID handelt.
  - Bücherregale - Wählen Sie aus, welche Bücherregale von GoodReads importiert werden sollen.
  - Mit GoodReads authentifizieren - Klicken Sie auf die Schaltfläche, um sich mit GoodReads zu authentifizieren.

> Mehrere GoodReads-Benutzer können als separate Listen hinzugefügt werden. Zusätzlich zur Verwendung eines authentifizierten Benutzers können andere Benutzer hinzugefügt werden, indem erweiterte Optionen aktiviert und die Benutzer-ID eingegeben werden. Klicken Sie dann auf "Mit GoodReads authentifizieren", um die Regale des Benutzers abzurufen. {.is-info}

- GoodReads-Listen {#goodreadslistimportlist}
  - Listen-ID - Geben Sie die öffentliche Listen-ID von GoodReads ein, die als Liste hinzugefügt werden soll.
- GoodReads-Serien {#goodreadsseriesimportlist}
  - Serien-ID - Geben Sie die Serien-ID von GoodReads ein, die als Liste hinzugefügt werden soll.
- LazyLibrarian {#lazylibrarianimport}
  - URL - URL Ihrer LazyLibrarian-Instanz
  - API-Schlüssel - API-Schlüssel Ihrer LazyLibrarian-Instanz
- Readarr {#readarrimport}
  - Vollständige URL - Vollständige URL der Readarr-Instanz, aus der importiert werden soll, z.B. `http://localhost:8787/readarr`
  - API-Schlüssel - API-Schlüssel der Readarr-Instanz, aus der importiert werden soll
  - Profile - Profile von der Readarr-Instanz, aus der importiert werden soll
  - Tags - Tags von der Readarr-Instanz, aus der importiert werden soll

# Metadaten

{#metadata}

- Calibre {#calibre}
  - [Siehe die Einstellungsseite](/readarr/settings#write-metadata-to-book-files)
- Audio-Tagging {#audiotagging}
  - [Siehe die Einstellungsseite](/readarr/settings#write-metadata-to-book-files)