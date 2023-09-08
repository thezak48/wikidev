---
title: Sonarr Unterstützt
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> Diese Seite ist noch in Bearbeitung und erfordert zusätzliche Anstrengungen. {.is-warning}

Diese Seite ist die Disambiguierungsseite für alle "unterstützten" Wiki-Links (normalerweise "Weitere Informationen" in der Benutzeroberfläche).

# Download-Clients

{#downloadclient}

- Aria2 {#aria2}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Flood {#flood}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)
  - Aufgrund von uTorrent als Adware und ehemaliger Spyware wird es nicht empfohlen. Die meisten Benutzer verwenden Qbittorrent.
- Vuze {#vuze}
  - [Siehe die Einstellungsseite](/sonarr/settings#download-clients)

# Indexer

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - Usenet-Indexer ausschließlich für japanische Medien (Anime).
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
  - Newznab ist eine standardisierte API, die von vielen Usenet-Indexing-Sites verwendet wird. Es gibt viele Voreinstellungen, aber alle erfordern einen API-Schlüssel, um zugänglich zu sein.
  - Indexer-Anwendungen wie [Prowlarr](/prowlarr) und [NZBHydra2](https://github.com/theotherp/nzbhydra2) können erweiterte Funktionen wie Statistik-Tracking bieten.
- omgwtfnzbs {#omgwtfnzbs}
  - Eine veraltete Legacy-Implementierung eines privaten Usenet-Indexers. Verwenden Sie stattdessen Newznab.
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)

## Torrents

- BroadcasTheNet (BTN) {#broadcasthenet}
  - Privater Tracker
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - Privater Tracker
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privater Tracker
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privater Tracker
  > Die native Implementierung von IP Torrents unterstützt keine Suche. Verwenden Sie es stattdessen über Prowlarr oder Jackett als Torznab {.is-info}
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-Tracker ausschließlich für japanische Medien (Anime).
  - Nyaa unterstützt nur die Suche nach Anime-Serientypen.
  - Es gibt bekannte Probleme mit der nativen Sonarr-Version
    - [Nyaa seeders/leechers werden nicht mehr ordnungsgemäß analysiert. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - Dies kann behoben werden, wenn [Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637) zusammengeführt wird.
  - > Nyaa missbilligt die Automatisierung und sperrt häufig Ihre IP-Adresse. {.is-warning}
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Öffentlicher Tracker
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- Torrent-RSS-Feed {#torrentrssindexer}
  - Generischer Torrent-RSS-Feed-Parser.
  > Der RSS-Feed muss ein `pubdate` enthalten. Die Größe der Veröffentlichung wird ebenfalls empfohlen. {.is-info}
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - Privater Indexer
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab ist ein Wortspiel aus Torrent und Newznab. Es verwendet die gleiche Struktur und Syntax wie die Newznab-API-Spezifikation, stellt jedoch torrent-spezifische Attribute und .torrent-Dateien bereit. Es unterstützt daher einen aktuellen RSS-Feed und die Möglichkeit zur Suche im Rückstand. Die Spezifikation wird von der Newznab-Organisation nicht gewartet oder unterstützt. (Die gleiche API-Spezifikation wird mit nZEDb geteilt)
  - Dies wird hauptsächlich von [Prowlarr](/prowlarr) und [Jackett](https://github.com/Jackett/Jackett) unterstützt.
  - [Siehe die Einstellungsseite](/sonarr/settings#indexer-settings)

> Viele Torrent-Tracker leben von der Community und haben Regeln, die den Besuch von Websites, Karma, Stimmen, Kommentaren usw. vorschreiben können.
> Bitte überprüfen Sie die Regeln und Etikette Ihres Trackers und halten Sie Ihre Community am Leben.
> Wir übernehmen keine Verantwortung, wenn Ihr Konto aufgrund von Regelverstößen oder der Anhäufung von Hit and Runs (HnRs)/niedrigem Verhältnis gesperrt wird. {.is-warning}

# Benachrichtigungen

{#notification}

- Boxcar {#boxcar}
- Benutzerdefiniertes Skript {#customscript}
  - Dies ermöglicht es Ihnen, ein benutzerdefiniertes Skript zu erstellen, das ausgeführt wird, wenn eine bestimmte Aktion erfolgt. Weitere Informationen finden Sie unter [Benutzerdefinierte Skripte](/sonarr/custom-scripts).
- Discord {#discord}
  - Mit Abstand eine der häufigsten Möglichkeiten, Benachrichtigungen über Aktionen in Ihrem Sonarr zu erhalten.
  - Unterstützte Feldtypen:
  `Übersicht, Bewertung, Genres, Qualität, Gruppe, Größe, Links, Veröffentlichung, Poster, Fanart, Benutzerdefinierte Formate, Benutzerdefinierte Formatbewertung, Indexer`
- E-Mail {#email}
  - Senden Sie sich selbst oder jemandem, den Sie mit E-Mails belästigen möchten, eine E-Mail. Wenn Sie Gmail verwenden, müssen Sie den Zugriff für unsichere Apps aktivieren. Wenn Sie Gmail verwenden und die Zwei-Faktor-Authentifizierung aktiviert haben, müssen Sie ein App-spezifisches Passwort verwenden.

> Sie können eine "schöne Adresse" wie `SomePrettyName <email@example.org>` verwenden {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi entstand aus der Liebe zur Medienwiedergabe. Es ist ein Unterhaltungszentrum, das alle Ihre digitalen Medien in einer schönen und benutzerfreundlichen Oberfläche zusammenführt. Es ist zu 100% kostenlos und Open Source, sehr anpassbar und läuft auf einer Vielzahl von Geräten. Es wird von einem engagierten Team von Freiwilligen und einer großen Community unterstützt. Durch Hinzufügen von Kodi als Verbindung können Sie die Bibliothek von Kodi aktualisieren, wenn eine neue Episode zu Sonarr hinzugefügt wurde.
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - Veraltet
- Plex Media Center {#plexclient}
  - Veraltet
- Plex Media Server {#plexserver}
  - Der Server für Ihr selbst gehostetes Plex-System. Durch Aktivieren dieser Option können Sie Ihrem Plex-Server eine Benachrichtigung über eine neue/aktualisierte Episode senden.
  - Dies ist selten erforderlich und nur erforderlich, wenn Plex das Dateisystem nicht überwachen kann.
  - In den wenigen Situationen, in denen Plex das Dateisystem nicht überwachen kann - wie bestimmte Arten von Remote-Mounts und einige ältere Netzwerk-Mounts - wird empfohlen, die App plexautoscan anstelle der Plex-Verbindung zu verwenden.

> Beachten Sie, dass dies einen vollständigen Bibliotheksscan für den Bibliotheks-/Stammordner der Serie auslösen kann. Es wird dringend empfohlen, die native Plex-Funktionalität zu verwenden, die nur das Dateisystem überwacht, oder ein Tool wie [plexautoscan](https://github.com/l3uddz/plex_autoscan) zu verwenden. {.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - Siehe diesen [Tipps und Tricks-Eintrag](/useful-tools#twitter)
- Webhook {#webhook}

# Listen

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH hat [eine Anleitung](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/) zum Synchronisieren von zwei Instanzen
- Plex Watchlist {#pleximport}
  - Fügen Sie einfach eine Plex-Watchlist für den authentifizierten Plex-Benutzer zu Sonarr hinzu. Beachten Sie, dass Ihre Liste Shows enthalten muss.
  - Um die Watchlists mehrerer Benutzer zu haben, müssen Sie die Listen jedes Benutzers hinzufügen und sich mit ihrem Plex-Benutzer authentifizieren.
- Trakt-Liste {#traktlistimport}
  - Benutzername - Stellen Sie sicher, dass Sie den tatsächlichen Benutzernamen des Benutzers und nicht den Namen des Benutzers eingeben.
  - Liste - Stellen Sie sicher, dass Sie den Listenname verwenden, wie er in der Listen-URL angezeigt wird.
  - Beispiel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Benutzername: `some-user-name`
    - Liste: `trakt-list-name`
- Trakt-Popular-Liste {#traktpopularimport}
- Trakt-Benutzer {#traktuserimport}

> Trakt-Listen sollten Shows enthalten, nicht einzelne Episoden. Sonarr wird nur Shows abgleichen und hinzufügen. {.is-info}

# Metadaten

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktivieren - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
  - Serienmetadaten - Erstellen Sie eine `tvshow.nfo` mit vollständigen Serienmetadaten
  - (Erweiterte Option) Serienmetadaten-URL - Erstellen Sie tvshow.nfo mit der TheTVDb-URL der Serie
  - Episodenmetadaten - Erstellen Sie `<filename>.nfo` für jede Episode
  - Serienbilder - Erstellen Sie verschiedene Serienbilder, einschließlich Poster und Banner mit den Namen `poster.jpg` und `banner.jpg`
  - Staffelbilder - Erstellen Sie verschiedene Staffelbilder, einschließlich Poster und Banner mit den Namen `season##-poster.jpg` und `season##-banner.jpg`
  - Episodenbilder - Erstellen Sie verschiedene Episodenbilder wie Thumbnails mit den Namen `<filename>-thumb.jpg`
- Roksbox {#roksboxmetadata}
  - Aktivieren - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
  - Episodenmetadaten - Erstellen Sie `Season##\<filename>.xml` für jede Episode
  - Serienbilder - Erstellen Sie `Series Title.jpg`
  - Staffelbilder - Erstellen Sie `Season ##.jpg`
  - Episodenbilder - Erstellen Sie `Season##\<filename>.jpg`
- WDTV {#wdtvmetadata}
  - Aktivieren - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
  - Episodenmetadaten - Erstellen Sie `Season##\<filename>.xml` für jede Episode
  - Serienbilder - Erstellen Sie `folder.jpg`
  - Staffelbilder - Erstellen Sie `Season ##\folder.jpg`
  - Episodenbilder - Erstellen Sie `Season##\<filename>.metathumb`