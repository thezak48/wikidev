---
title: Radarr Unterstützt
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# Inhaltsverzeichnis

> Diese Seite ist noch in Bearbeitung und erfordert zusätzliche Anstrengungen.{.is-warning}

Diese Seite ist die Disambiguierungsseite für alle `unterstützten` Wiki-Links (normalerweise "mehr Informationen" in der Benutzeroberfläche).

# Download-Clients

{#downloadclient}

- Aria2 {#aria2}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Flood {#flood}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)
  - Da uTorrent Adware und früher Spyware war, wird es nicht empfohlen. Die meisten Benutzer verwenden Qbittorrent.
- Vuze {#vuze}
  - [Siehe die Einstellungsseite](/radarr/settings#download-clients)

# Indexer

{#indexer}

## Usenet

- Newznab {#newznab}
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
  - Newznab ist eine standardisierte API, die von vielen Usenet-Indexseiten verwendet wird. Es gibt viele Voreinstellungen, aber alle erfordern einen API-Schlüssel, um zugänglich zu sein.
  - Indexer-Anwendungen wie [Prowlarr](/prowlarr) und [NZBHydra2](https://github.com/theotherp/nzbhydra2) können erweiterte Funktionen wie Statistik-Tracking bieten.
- omgwtfnzbs {#omgwtfnzbs}
  - Eine veraltete Legacy-Implementierung eines privaten Usenet-Indexers. Verwenden Sie stattdessen Newznab.
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - Privater Tracker
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - Privater Tracker
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - Privater Tracker
  > Die native Implementierung von IP Torrents unterstützt keine Suche. Verwenden Sie es stattdessen über Prowlarr oder Jackett als Torznab {.is-info}
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - Torrent-Tracker ausschließlich für japanische Medien (Anime).
  > Nyaa ist gegen Automatisierung und sperrt häufig Ihre IP-Adresse. {.is-info}
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - Privater Tracker
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - Öffentlicher Tracker
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- Torrent-RSS-Feed {#torrentrssindexer}
  - Generischer Torrent-RSS-Feed-Parser.
  > Der RSS-Feed muss ein `pubdate` enthalten. Die Freigabegröße wird ebenfalls empfohlen. {.is-info}
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - Ein veraltetes Couchpotato-Format vor Torznab.
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab ist ein Wortspiel aus Torrent und Newznab. Es verwendet die gleiche Struktur und Syntax wie die Newznab-API-Spezifikation, stellt jedoch torrent-spezifische Attribute und .torrent-Dateien bereit. Es unterstützt daher einen aktuellen RSS-Feed UND die Möglichkeit zur Suche im Rückstand. Die Spezifikation wird von der Newznab-Organisation nicht gewartet oder unterstützt. (Die gleiche API-Spezifikation wird mit nZEDb geteilt)
  - Dies wird hauptsächlich von [Prowlarr](/prowlarr) und [Jackett](https://github.com/Jackett/Jackett) unterstützt
  - [Siehe die Einstellungsseite](/radarr/settings#indexer-settings)

> Viele Torrent-Tracker sind auf die Community angewiesen und haben Regeln, die den Besuch von Websites, Karma, Abstimmungen, Kommentaren usw. vorschreiben.
> Bitte überprüfen Sie die Regeln und Etikette Ihres Trackers und halten Sie Ihre Community am Leben.
> Wir übernehmen keine Verantwortung, wenn Ihr Konto wegen Missachtung von Regeln oder der Anhäufung von Hit and Runs (HnRs)/niedrigem Verhältnis gesperrt wird. {.is-warning}

# Benachrichtigungen

{#notification}

- Boxcar {#boxcar}
- Benutzerdefiniertes Skript {#customscript}
  - Dies ermöglicht es Ihnen, ein benutzerdefiniertes Skript zu erstellen, das ausgeführt wird, wenn eine bestimmte Aktion stattfindet. Weitere Informationen finden Sie unter [Benutzerdefinierte Skripte](/radarr/custom-scripts).
- Discord {#discord}
  - Mit Abstand eine der häufigsten Möglichkeiten, Benachrichtigungen über Aktionen, die in Ihrem Radarr stattfinden, zu erhalten.
- E-Mail {#email}
  - Senden Sie sich selbst oder jemandem, den Sie mit E-Mails belästigen möchten, eine E-Mail. Wenn Sie Gmail verwenden, müssen Sie den Zugriff von weniger sicheren Apps aktivieren. Wenn Sie Gmail verwenden und die Zwei-Faktor-Authentifizierung aktiviert haben, müssen Sie ein App-spezifisches Passwort verwenden.

> Sie können eine "schöne Adresse" wie `EinSchönerName <email@example.org>` verwenden {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi entstand aus der Liebe zur Medienwiedergabe. Es ist ein Unterhaltungszentrum, das alle Ihre digitalen Medien in einer schönen und benutzerfreundlichen Oberfläche zusammenführt. Es ist zu 100% kostenlos und Open Source, sehr anpassbar und läuft auf einer Vielzahl von Geräten. Es wird von einem engagierten Team von Freiwilligen und einer riesigen Community unterstützt. Durch Hinzufügen von Kodi als Verbindung können Sie die Bibliothek von Kodi aktualisieren, wenn ein neuer Film zu Radarr hinzugefügt wurde.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - Siehe den Eintrag zu [Nützlichen Tools - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)
- Plex Media Server {#plexserver}
  - Der Server für Ihr selbst gehostetes Plex-System. Wenn Sie dies aktivieren, können Sie Ihrem Plex-Server eine Aktualisierung senden, die ihn darüber informiert, dass ein neuer/aktualisierter Film verfügbar ist.
  - Dies ist selten erforderlich und nur erforderlich, wenn Plex das Dateisystem nicht überwachen kann.
  - In den wenigen Situationen, in denen Plex das Dateisystem nicht überwachen kann - wie bestimmte Arten von Remote-Mounts und einige ältere Netzwerk-Mounts - wird empfohlen, die App plexautoscan anstelle der Plex-Verbindung zu verwenden.
- Ein Werkzeug wie [plexautoscan](https://github.com/l3uddz/plex_autoscan) ist eine weitere Option.

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Trakt {#trakt}
- Twitter {#twitter}
  - Siehe diesen Eintrag zu [Tipps und Tricks](/useful-tools#twitter)
- Webhook {#webhook}

# Listen

{#importlist}

- CouchPotato {#couchpotatoimport}
- Benutzerdefinierte Listen {#radarrlistimport}
- IMDb-Listen {#imdblistimport}
  - Um Ihre IMDb-Watchlist hinzuzufügen, gehen Sie zu Ihrer Liste und klicken Sie auf "Bearbeiten". Stellen Sie sicher, dass die Datenschutzeinstellung auf "Öffentlich" eingestellt ist. In der Adressleiste finden Sie die `lsxxxxxx`-Nummer, die Sie in Radarr eingeben müssen.

    1. Gehen Sie zu Ihren IMDB-Listeneinstellungen
    1. Stellen Sie sicher, dass die Datenschutzeinstellung auf "Öffentlich" (d.h. "Deaktiviert") eingestellt ist
    1. Verwenden Sie die `ls`-Nummer innerhalb der URL

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex Watchlist {#plex}
  - Erfordert: v4.1.0.6176+
  - Fügen Sie einfach eine Plex-Watchlist für den authentifizierten Plex-Benutzer zu Radarr hinzu. Beachten Sie, dass Ihre Liste Filme enthalten muss.
  - Um mehrere Benutzer-Watchlists zu haben, müssen Sie die Listen jedes Benutzers hinzufügen und sich mit ihrem Plex-Benutzer authentifizieren.
- Radarr {#radarrimport}
  - TRaSH hat [eine Anleitung](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) zum Synchronisieren von zwei Instanzen
- RSS-Liste {#rssimport}
- StevenLu Custom {#stevenluimport}
	- Ermöglicht das Erstellen von benutzerdefinierten Filmlisten im JSON-Format.
  	Ihr Feed muss für jeden Film entweder einen `Titel` oder eine `imdb_id` enthalten, beides kann angegeben werden.
  		> Beachten Sie, dass `imdb_id` sicherer ist als `Titel`, da es keine breite Suche erfordert
    Hier ist ein Beispiel für ein gültiges JSON:
      ```
      [
          {
            "title": "The Wastetown",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/6J32RMp8uko8CUEM3rYP962hQun.jpg",
            "imdb_id": "tt22889064"
          },
          {
            "title": "Wild Sunflowers",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/tHK4c0UZKrqkmXZ2HJeGNhNetRz.jpg",
            "imdb_id": "tt13774830"
          }
      ]
      ```
      - In Elementen können zusätzliche Schlüssel hinzugefügt werden (werden ignoriert)
      - Für eine leere Liste geben Sie einfach ein leeres JSON-Array `[]` zurück
- StevenLu List {#stevenlu2import}
- TMDb-Sammlung {#tmdbcollectionimport}
  - Sammlungslisten werden in Radarr v4.2 nicht mehr unterstützt und wurden in Sammlungen in Radarr migriert. Weitere Informationen finden Sie im Abschnitt [Sammlungen](/radarr/library#collections).
- TMDb-Unternehmen {#tmdbcompanyimport}
- TMDb-Schlüsselwort {#tmdbkeywordimport}
- TMDb-Liste {#tmdblistimport}
- TMDb-Person {#tmdbpersonimport}
  - Wenn die TMDb-Personen-URL `https://www.themoviedb.org/person/500-tom-cruise` lautet, ist die Personen-ID `500`
- TMDb-Populär {#tmdbpopularimport}
  - Top verwendet <https://developers.themoviedb.org/3/movies/get-top-rated-movies>
  - Beliebt verwendet <https://developers.themoviedb.org/3/movies/get-popular-movies>
  - Im Kino verwendet <https://developers.themoviedb.org/3/movies/get-now-playing>
  - Kommende verwendet <https://developers.themoviedb.org/3/movies/get-upcoming>
- TMDb-Benutzer {#tmdbuserimport}
- Trakt-Liste {#traktlistimport}
  - Benutzername - Stellen Sie sicher, dass Sie den tatsächlichen Benutzernamen des Benutzers und nicht den Namen des Benutzers eingeben
  - Liste - Stellen Sie sicher, dass Sie den Listenname verwenden, wie er in der Listen-URL angezeigt wird
  - Beispiel: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - Benutzername: `some-user-name`
    - Liste: `trakt-list-name`
- Trakt-Populäre Liste {#traktpopularimport}
- Trakt-Benutzer {#traktuserimport}
  - Dieser Typ sollte verwendet werden, wenn Sie Ihre eigene Watchlist verwenden

# Metadaten

{#metadata}

- Emby (Legacy) {#mediabrowsermetadata}
  - Aktivieren - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
  - Film-Metadaten - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
- Kodi (XBMC) / Emby {#xbmcmetadata}
  - Aktivieren - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
  - Film-Metadaten - Erstellen Sie eine `<Dateiname>.nfo` mit den Film-Metadaten
  - (Erweiterte Option) Film-Metadaten-URL - Erstellen Sie `movie.nfo` mit TMDb- und IMDb-Film-URLs
  - Metadatensprache - Wählen Sie die Sprache aus, die Radarr verwenden soll, um die Metadaten zu schreiben, sofern in dieser Sprache verfügbar
  - Film-Bilder - Erstellen Sie verschiedene Filmbilder, einschließlich Poster und Banner
  - Verwenden Sie Movie.nfo - Schreiben Sie die nfo-Datei als `movie.nfo` anstelle des Standards
  - Sammlungsname - Radarr schreibt den Sammlungsnamen in die .nfo-Datei
- Roksbox {#roksboxmetadata}
  - Aktivieren - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
  - Film-Metadaten - Erstellen Sie eine XML-Datei für jeden Film
  - Film-Bilder - Erstellen Sie `Movie.jpg`
- WDTV {#wdtvmetadata}
  - Aktivieren - Aktivieren Sie die Erstellung von Metadatendateien für diesen Metadatentyp
  - Film-Metadaten - Erstellen Sie `<Dateiname>.xml` für jede Episode
  - Film-Bilder - Erstellen Sie `folder.jpg`