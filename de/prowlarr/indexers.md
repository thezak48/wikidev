---
title: Prowlarr Indexer
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

Diese Seite beschreibt, wie Indexer in Prowlarr hinzugefügt und konfiguriert werden können.

# Hinzufügen eines Indexers

Um einen Indexer hinzuzufügen, klicken Sie zunächst links auf `Indexers` und dann oben auf der Seite auf <kb>+</kb> `Add Indexer`.

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

Wählen Sie Ihren Indexer aus der Liste aus oder geben Sie einen Teil des Namens in das Feld ein, um Ihren Indexer zu finden. Wenn Ihr Indexer nicht aufgeführt ist, können Sie möglicherweise "Generic Newznab" (für Usenet) oder "Generic Torznab" (für Torrents) verwenden. Andernfalls besuchen Sie unsere [Indexer Request Seite](https://requests.prowlarr.com/).

> Die Verwendung von `Generic Newznab` oder `Generic Torznab` setzt voraus, dass Ihr Indexer standardisierte *znab-Formate unterstützt. Wenn dies nicht der Fall ist, funktioniert dies nicht.
{.is-info}

> Hinweis: Fast jede Usenet-Seite ist mit Generic Newznab kompatibel.
{.is-warning}

> Wenn Ihr Tracker oder Indexer nicht aufgeführt ist und nicht auf unserer [supported indexers](/prowlarr/supported-indexers) Seite steht, können Sie eine Anfrage stellen, um ihn über unsere [Indexer Requests Site](https://requests.prowlarr.com) hinzuzufügen.
{.is-info}

# Bearbeiten eines Indexers

Um einen Indexer zu bearbeiten, klicken Sie zunächst links auf `Indexers` und dann auf das Schraubenschlüssel-Symbol ganz rechts neben dem Indexer, den Sie bearbeiten möchten.

# Anzeigen einer Indexer-ID oder -URL

Um Details zu einem Indexer anzuzeigen, klicken Sie zunächst links auf `Indexers` und dann auf den Indexer-Link in der Spalte "Indexer Name" (ehemals das (i)-Symbol rechts).

Verfügbare Details können sein:

- ID in Prowlarr
- Beschreibung
- Codierung
- Sprache
- Website
- Newznab/Torznab Prowlarr-URL
- Site-Funktionen

# Indexer-Einstellungen

Nachdem Sie Ihren Indexer ausgewählt haben, wird ein Popup-Fenster angezeigt, das weitere Informationen enthält, die Sie konfigurieren müssen. Beachten Sie, dass sich die spezifischen Einstellungen für jeden Indexer geringfügig ändern können, basierend auf den erforderlichen Feldern und dem Typ des Indexers, den Sie konfigurieren.

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Name - Wählen Sie einen Namen für diesen Indexer aus. Wenn er mit Ihren Apps synchronisiert wird, wird "(Prowlarr)" dahinter hinzugefügt.
- Aktivieren - Aktivieren Sie das Kontrollkästchen, um diesen Indexer zu aktivieren.
- Umleiten - Aktivieren Sie das Kontrollkästchen, wenn eine Umleitung erforderlich ist. Es gibt nur wenige Indexer, bei denen dies erforderlich ist, um ein Verbot zu vermeiden. Wenn aktiviert, wird der Grab-Link direkt an die Anwendung weitergeleitet, anstatt ihn über Prowlarr zu proxyen.

> Eine Umleitung ist in der Regel nur für eine Handvoll sehr spezifischer Indexer erforderlich.
{.is-info}

- Sync-Profil - Wählen Sie hier Ihr Sync-Profil aus. Diese können in [`Einstellungen` => `Apps`](/prowlarr/settings#applications) erstellt werden. Das Standardprofil existiert bereits und sieht so aus:

> Sie können unterschiedliche Einstellungen pro App haben, indem Sie mehrere Instanzen des Indexers erstellen.
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Wählen Sie die URL aus, die Prowlarr verwenden soll. Wenn leer, wird die Standard-/erste URL verwendet.
- Download-Link - Wenn Sie einen Torrent-Indexer hinzufügen, müssen Sie möglicherweise auswählen, welche Art von Download-Link verwendet werden soll.
- (Erweiterte Option) API-Pfad - Pfad zur API des Indexers. In der Regel `/api`
- Anmeldeinformationen - Viele Indexer und Tracker erfordern eine Authentifizierung / Anmeldung auf irgendeine Weise. Sie müssen möglicherweise einen API-Schlüssel, einen RSS-Schlüssel, eine Sitzungs-ID, ein Cookie oder andere Anmeldeinformationen von Ihrem Indexer eingeben (normalerweise auf Ihrer Profilseite oder unter Sicherheit zu finden), Suchreihenfolgen auswählen oder andere Optionen für Ihren spezifischen Indexer.
  - API-Schlüssel
  - RSS-Schlüssel
  - Sitzungs-ID
  - Cookie
  - Benutzername/Passwort
  - usw.
- (Erweiterte Option) Zusätzliche Parameter - Zusätzliche Parameter, die zu den Anfragen für diesen Indexer hinzugefügt werden sollen.
- VIP-Ablauf - Geben Sie das Datum im ISO-Format (yyyy-MM-DD) ein, um 1 Woche vor Ablauf benachrichtigt zu werden; andernfalls leer lassen
- Tags - Verwenden Sie Tags, um Standard-Download-Clients festzulegen, Indexer-Proxies festzulegen, Indexer an Anwendungen anzugeben oder einfach Ihre Indexer zu organisieren.
- (Erweiterte Option) Abfrage-Limit - Wenn Ihr Indexer Ihre API-Aufrufe pro Tag begrenzt, können Sie hier die Anzahl eingeben, um die Grenze nicht zu überschreiten.
- (Erweiterte Option) Grab-Limit - Wenn Ihr Indexer Ihre Grabs pro Tag begrenzt, können Sie hier die Anzahl eingeben, um die Grenze nicht zu überschreiten. Sobald das Grab-Limit erreicht ist, lösen weitere Abfragen eine unbehandelte Ausnahme in \*Arr Apps aus. Andere Apps können sich unterschiedlich verhalten.
- (Erweiterte Option) Seed-Verhältnis - Nur für Torrent-Indexer: Das Verhältnis, das ein Torrent erreichen sollte, bevor es gestoppt wird. Leer bedeutet die Standardoption der App.
- (Erweiterte Option) Seed-Zeit - Nur für Torrent-Indexer: Die Zeit, die ein Torrent gesät werden sollte, bevor es gestoppt wird. Leer bedeutet die Standardoption der App. Die Werte sind in Minuten angegeben.
- (Erweiterte Option) Indexer-Priorität - Priorität dieses Indexers, um einen Indexer einem anderen in Release-Tiebreaker-Szenarien vorzuziehen. 1 ist die höchste Priorität und 50 ist die niedrigste Priorität. Diese Prioritäten werden mit den \*Arr-Apps synchronisiert.

- Testen Sie Ihren Indexer, und wenn ein grünes Häkchen angezeigt wird, können Sie ihn speichern. Je nach Ihren Synchronisierungseinstellungen wird er automatisch zu Ihren Apps hinzugefügt, wenn Sie ihn speichern.

## Hinzufügen einer benutzerdefinierten YML-Definition

- Beachten Sie, dass die YML-Definition für einen kurzen Zeitraum zwischengespeichert wird und wenn Sie Änderungen zu Entwicklungszecken vornehmen, müssen Sie auf den Cache warten oder Prowlarr neu starten.
- Wenn Sie eine benutzerdefinierte Cardigann-kompatible YML-Definitionsdatei für einen nicht unterstützten Indexer hinzufügen oder Änderungen an einer vorhandenen Definition testen möchten:
  - Navigieren Sie zum (oder erstellen Sie) den Ordner "Custom Indexer Definition" mit dem Namen `Custom` im Ordner `Definitions` des [App Data-Ordners von Prowlarr](/prowlarr/appdata-directory).
    - Beispadtpfade:
      - Windows: `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux: `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX: `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - Speichern Sie die [Cardigann-kompatible YML-Datei](/prowlarr/cardigann-yml-definition) in dem Ordner und stellen Sie sicher, dass Prowlarr Berechtigungen zum Zugriff darauf hat.

> Der Dateiname und die ID in der Definition müssen eindeutig sein und dürfen nicht mit anderen vorhandenen Definitionen in Konflikt geraten. Es wird dringend empfohlen, dass der Name in der Definition ebenfalls eindeutig ist.
{.is-info}

# Unterstützte Indexer

- [Siehe diese Wiki-Seite für eine Liste der unterstützten Indexer ab der neuesten Nightly-Version.](/prowlarr/supported-indexers/)