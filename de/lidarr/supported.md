---
title: Lidarr Unterstützt
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> Diese Seite ist noch in Bearbeitung und erfordert zusätzliche Anstrengungen.{.is-warning}

Diese Seite ist die Disambiguierungsseite für alle "unterstützten" Wiki-Links (normalerweise `Weitere Informationen` in der Benutzeroberfläche).

# Download-Clients

{#downloadclient}

- Deluge {#deluge}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Flood {#flood}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)
  - Da uTorrent Adware und früher Spyware ist, wird es nicht empfohlen. Die meisten Benutzer verwenden qBittorrent.
- Vuze {#vuze}
  - [Siehe die Einstellungsseite](/lidarr/settings#download-clients)

# Indexer

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
  - Newznab ist eine standardisierte API, die von vielen Usenet-Indexierungsseiten verwendet wird. Es gibt viele Voreinstellungen, aber alle erfordern einen API-Schlüssel, um zugänglich zu sein.
  - Indexer-Anwendungen wie [Prowlarr](/prowlarr) und [NZBHydra2](https://github.com/theotherp/nzbhydra2) können erweiterte Funktionen wie Statistik-Tracking bieten.

## Torrents

- FileList {#filelist}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privater Tracker
  > Die native Implementierung von IP Torrents unterstützt keine Suche {.is-info}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Öffentlicher Tracker
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- Torrent RSS-Feed {#torrentrssindexer}
  - Generischer Torrent-RSS-Feed-Parser.
  > Der RSS-Feed muss ein `pubdate` enthalten. Die Größe der Veröffentlichung wird ebenfalls empfohlen.
  {.is-info}
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privater Indexer
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab ist ein Wortspiel aus Torrent und Newznab. Es verwendet die gleiche Struktur und Syntax wie die Newznab-API-Spezifikation, stellt jedoch torrent-spezifische Attribute und .torrent-Dateien bereit. Es unterstützt daher einen aktuellen RSS-Feed und Backlog-Suchfunktionen. Die Spezifikation wird von der Newznab-Organisation nicht gewartet oder unterstützt. (Die gleiche API-Spezifikation wird auch von nZEDb verwendet)
  - Dies wird hauptsächlich von [Prowlarr](/prowlarr) und [Jackett](https://github.com/Jackett/Jackett) unterstützt
  - [Siehe die Einstellungsseite](/lidarr/settings#indexer-settings)

# Benachrichtigungen

{#notification}

- Boxcar {#boxcar}
- Benutzerdefiniertes Skript {#customscript}
  - Dies ermöglicht es Ihnen, ein benutzerdefiniertes Skript zu erstellen, das ausgeführt wird, wenn eine bestimmte Aktion auftritt. Weitere Informationen finden Sie unter [Benutzerdefinierte Skripte](/lidarr/custom-scripts).
- Discord {#discord}
  - Mit Abstand eine der häufigsten Möglichkeiten, Benachrichtigungen über Aktionen zu erhalten, die auf Ihrem Lidarr stattfinden.
- E-Mail {#email}
  - Senden Sie sich selbst oder jemandem, den Sie mit E-Mails belästigen möchten, einfach eine E-Mail. Wenn Sie Gmail verwenden, müssen Sie den Zugriff von weniger sicheren Apps aktivieren. Wenn Sie Gmail verwenden und die Zwei-Faktor-Authentifizierung aktiviert haben, müssen Sie ein App-spezifisches Passwort verwenden.

 > Sie können eine "schöne Adresse" wie `EinHübscherName <email@example.org>` verwenden {.is-info}

- Emby (Media Browser) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi entstand aus der Liebe zur Medienwiedergabe. Es ist ein Unterhaltungszentrum, das alle Ihre digitalen Medien in einer schönen und benutzerfreundlichen Oberfläche zusammenführt. Es ist zu 100% kostenlos und Open Source, sehr anpassbar und läuft auf einer Vielzahl von Geräten. Es wird von einem engagierten Team von Freiwilligen und einer großen Community unterstützt. Durch Hinzufügen von Kodi als Verbindung können Sie die Bibliothek von Kodi aktualisieren, wenn ein neuer Song zu Lidarr hinzugefügt wurde.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Siehe den Eintrag zu [Nützlichen Tools - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Der Server für Ihr selbst gehostetes Plex-System. Wenn Sie dies aktivieren, können Sie Ihrem Plex-Server eine Aktualisierung senden, um ihn darüber zu informieren, dass eine neue/aktualisierte Episode verfügbar ist.
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Siehe diesen Eintrag zu [Tipps und Tricks](/useful-tools#twitter)
- Webhook {#webhook}

# Listen

{#importlist}

- Headphones {#headphonesimport}
- Last.fm-Tag {#lastfmtag}
- Last.fm-Benutzer {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr-Listen {#lidarrlists}
- MusicBrainz-Serie {#musicbrainzseries}
- Spotify gefolgte Künstler {#spotifyfollowedartists}
- Spotify-Playlists {#spotifyplaylist}
- Spotify gespeicherte Alben {#spotifysavedalbums}

# Metadaten

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}