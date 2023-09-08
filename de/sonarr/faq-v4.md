---
title: Sonarr v4 Beta FAQ
description: Sonarr v4 Beta FAQ
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# Sonarr v4 Beta FAQ

> Sonarr v4 befindet sich derzeit in der Beta-Phase, daher sind Fehler und Probleme zu erwarten. Bitte nutzen Sie unsere Support-Kanäle, um Fragen zu stellen, Probleme zu melden oder Feedback zur v4-Beta zu geben. Wenn erforderlich, kann es sein, dass Sie gebeten werden, ein Problem auf Github zu eröffnen. Wenn Sie aufgefordert werden, ein Problem auf [Github](https://github.com/Sonarr/Sonarr) zu eröffnen, geben Sie bitte einen Link zur ursprünglichen Diskussion sowie alle anderen angeforderten Informationen an. {.is-warning}

## Was hat sich geändert?

Weitere Informationen finden Sie in der [v4 Beta-Ankündigung](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/).

Hier sind einige der Höhepunkte und markanten Änderungen:

- [Erzwungene Authentifizierung](#erzwungene-authentifizierung)
- Mono => Dotnet (mehr Geschwindigkeit; kein Mono mehr). Aufgrund dieser Änderung sind wahrscheinlich Aktualisierungen der Reverse Proxy-Konfiguration erforderlich:
  - [Nginx](#nginx)
  - [Apache](#apache)
- [Bevorzugte Wörter sind weg](#migration-von-bevorzugten-wörtern-zu-benutzerdefinierten-formaten) und wurden durch benutzerdefinierte Formate ersetzt
- [Sprachprofile sind weg](#wo-sind-die-sprachprofile-hin) und wurden durch benutzerdefinierte Formate ersetzt
- Dunkles/helles Thema
- SysLog- und Instanznamen-Unterstützung
- Zusammenführung des Masseneditors in die [Serienübersicht](#wo-ist-der-masseneditor-hin)
- Und vieles mehr

## Erzwungene Authentifizierung

Wenn Sonarr so freigegeben ist, dass die Benutzeroberfläche von außerhalb Ihres lokalen Netzwerks aus zugänglich ist, sollten Sie eine Form der Authentifizierung aktiviert haben, um auf die Benutzeroberfläche zugreifen zu können. Dies wird auch von Trackern und Indexern zunehmend gefordert.

Ab Sonarr v4 ist die Authentifizierung obligatorisch.

### Authentifizierungsmethode

- `Basic` (Browser-Popup) - Diese Option zeigt beim Zugriff auf Sonarr ein kleines Popup an, in dem Sie einen Benutzernamen und ein Passwort eingeben können.
- `Forms` (Anmeldeseite) - Diese Option verfügt über eine vertraut aussehende Anmeldeseite, ähnlich wie bei anderen Websites, auf der Sie sich bei Sonarr anmelden können.
- `External` - Nur über Konfigurationsdatei konfigurierbar
  - Wenn Sie eine **externe Authentifizierung** wie Authelia, Authetik, NGINX Basic Auth usw. verwenden, können Sie eine doppelte Authentifizierung verhindern, indem Sie die App herunterfahren, `<AuthenticationMethod>External</AuthenticationMethod>` in der [Konfigurationsdatei](/sonarr/appdata-directory) festlegen und die App neu starten. **Beachten Sie, dass mehrere `AuthenticationMethod`-Einträge in der Datei nicht unterstützt werden und nur der oberste Wert verwendet wird**.

### Erforderliche Authentifizierung

- Wenn Sie die App nicht extern freigeben und/oder keine Authentifizierung für den lokalen Zugriff (z. B. LAN) wünschen, ändern Sie in Einstellungen => Allgemeine Sicherheit => Erforderliche Authentifizierung auf `Deaktiviert für lokale Adressen`.
  - Das Konfigurationsdatei-Äquivalent dazu lautet `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`.

## Migration von bevorzugten Wörtern zu benutzerdefinierten Formaten

Das System der bevorzugten Wörter wurde durch das System der benutzerdefinierten Formate ersetzt. Dadurch wird eine viel feinere Granularität bei den Entscheidungen ermöglicht, die Sonarr treffen kann. Während bevorzugte Wörter für alle Qualitätsprofile galten, können benutzerdefinierte Formate für jedes Qualitätsprofil unterschiedliche Wichtigkeitsstufen erhalten.

Benutzerdefinierten Formaten kann auch eine Abschneideebene zugewiesen werden, sodass Upgrades gestoppt werden, sobald eine gewünschte Präferenzstufe erreicht ist, während das alte System der bevorzugten Wörter immer ein Upgrade durchführte, wenn eine bessere Version gefunden wurde.

### Muss (nicht) enthalten

"Muss enthalten" und "Darf nicht enthalten" bleiben in den Einstellungen des Freigabeprofils erhalten, wie es in v3 der Fall war.

### Dateinamens-Token

Das Token `{Preferred Words}` verwendete den Begriff, der in der Regex-Eingabe für die Benennung in Dateien übereinstimmte.
Das Token `{Custom Formats}` verwendet den Namen des benutzerdefinierten Formats für die Benennung in Dateien.

> Es wird empfohlen, Ihre bevorzugten Wort-Freigabeprofile VOR dem Upgrade zu screenshoten oder zu entfernen. Jede Zeile mit bevorzugten Wörtern wird nach der Migration zu einem eigenen benutzerdefinierten Format.
{.is-warning}

## Wo sind die Sprachprofile hin?

Sprachen werden in Sonarr v4 anders behandelt. Sie werden nicht mehr über das alte System der Sprachprofile verwaltet, sondern sind jetzt Teil der benutzerdefinierten Formate. Sie müssen benutzerdefinierte Formate für die gewünschten Sprachen erstellen und diese benutzerdefinierten Formaten dann Ihren Qualitätsprofilen mit einer entsprechenden Bewertung hinzufügen, um den Abruf dieser Sprache zu erzwingen.

> Weitere Informationen finden Sie in TRaSH Guide's [Anleitung zur Einrichtung von benutzerdefinierten Sprachformaten](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/).
{.is-info}

### Nur Englisch

**Aus [TRaSH => Sprache: Nur Englisch](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

Wenn Sie nur Veröffentlichungen in Englisch abrufen möchten, können Sie das folgende benutzerdefinierte Format verwenden. Importieren Sie dieses benutzerdefinierte Format und weisen Sie es dann jedem Ihrer Qualitätsprofile mit einer Punktzahl von -10000 zu. Wenn Ihre Mindestpunktzahl für benutzerdefinierte Formate 0 beträgt, werden alle Veröffentlichungen abgelehnt, die nicht als Englisch analysiert werden.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Sprache: Nur Englisch",
  "name": "Sprache: Nicht Englisch",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Nicht-englische Sprache",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 1
      }
    }
  ]
}
```

### Nur Originalsprache

**Aus [TRaSH => Sprache: Nur Originalsprache](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

Wenn Sie nur Veröffentlichungen in der Originalsprache der Serie (laut TVDb) abrufen möchten, können Sie das folgende benutzerdefinierte Format verwenden. Importieren Sie dieses benutzerdefinierte Format und weisen Sie es dann jedem Ihrer Qualitätsprofile mit einer Punktzahl von -10000 zu. Wenn Ihre Mindestpunktzahl für benutzerdefinierte Formate 0 beträgt, werden alle Veröffentlichungen abgelehnt, die nicht als Originalsprache der Serie (laut TVDb) analysiert werden.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "Sprache: Nur Originalsprache",
  "name": "Sprache: Nicht Original",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "Nicht-Originalsprache",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": -2
      }
    }
  ]
}
```

## Mein Reverse Proxy funktioniert nicht mehr?

Aufgrund von Änderungen im Backend von Sonarr (Migration von Mono zu Dotnet) funktioniert Ihr Reverse Proxy möglicherweise nicht mehr.

### Nginx

Ihre Nginx-Konfigurationsdatei muss geändert werden. Ersetzen Sie diese Zeile:

```nginx
   proxy_set_header   Host $proxy_host;
```

durch diese Zeile:

```nginx
  proxy_set_header   Host $host;
```

### Apache

Ihre Apache-Virtualhost-Konfigurationsdatei muss geändert werden. Fügen Sie diese Zeile hinzu:

```apache2
  ProxyPreserveHost On
```

## Was ist dieser neue Button "*Überschreiben und zur Download-Warteschlange hinzufügen*"?

Bei einer interaktiven Suche wurde ein zweiter Download-Button mit dem Titel "Überschreiben und zur Download-Warteschlange hinzufügen" hinzugefügt. Mit diesem Button können Sie zwei Dinge tun:

- Wählen Sie den Download-Client aus, an den der Download gesendet werden soll. Dies ist nützlich, wenn Sie mehrere Download-Clients für dasselbe Protokoll haben (z. B. mehrere Instanzen eines Torrent-Clients), anstatt Sonarr die Entscheidung zu überlassen, welchen Client er verwenden soll.
- Überschreiben Sie die von Sonarr analysierte Titel der Veröffentlichung, falls Sonarr sie falsch analysiert hat oder Sonarr sie nicht analysieren konnte, Sie die Veröffentlichung jedoch trotzdem abrufen möchten. Die folgenden analysierten Felder können überschrieben werden:
  - Serie
  - Staffelnummer
  - Episode(n)
  - Qualität
  - Sprache

## Wo ist der Masseneditor hin?

Die eigenständige Seite des Masseneditors wurde entfernt und die Funktion wurde in die Serienübersichtsseite integriert. Um Shows massenhaft zu bearbeiten, klicken Sie zunächst auf die Schaltfläche "Serien auswählen" oben in der Serienübersicht und wählen Sie die Shows aus, die Sie bearbeiten möchten.

Die Seite "Staffelpass" wurde ebenfalls entfernt. Ein Teil der Funktionalität bleibt im Serienübersichtseditor erhalten. Wählen Sie die Tabellenansicht und klicken Sie auf "Serien auswählen". Wenn Sie sich im Auswahlmodus befinden, fahren Sie mit der Maus über die Zahl in der Spalte "Staffeln", um das Popover für den Staffelpass für diese Show aufzurufen.

## Episoden zeigen Laufzeiten von 0 an

In v4 wird eine Laufzeit pro Episode von TVDb verwendet. Wenn die Laufzeit für die Episode 0 beträgt, wird versucht, auf die Laufzeit der Serie zurückzugreifen.
Wenn die Laufzeit der Serie ebenfalls 0 beträgt, verwendet Sonarr eine Laufzeit von 45 für jede Episode, die innerhalb von 24 Stunden nach der ersten Episode ausgestrahlt wurde.