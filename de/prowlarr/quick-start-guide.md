---
title: Prowlarr Schnellstartanleitung
description: 
published: true
date: 2023-04-06T16:04:33.682Z
tags: 
editor: markdown
dateCreated: 2023-04-06T16:04:33.682Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Indexer](#indexer)
- [Apps](#apps)
  - [Anwendungseinstellungen](#anwendungseinstellungen)
- [Download-Clients](#download-clients)
  - [Usenet-Client-Einstellungen](#usenet-client-einstellungen)
  - [Torrent-Client-Einstellungen](#torrent-client-einstellungen)
  - [Testen des Download-Clients](#testen-des-download-clients)
- [Setup abgeschlossen](#setup-abgeschlossen)

> Diese Seite ist noch in Bearbeitung und nicht vollständig.

> Für eine detailliertere Erläuterung aller Einstellungen siehe [Prowlarr => Einstellungen](/prowlarr/settings)

In dieser Anleitung werden wir die grundlegende Einrichtung erklären, die Sie vornehmen müssen, um mit Prowlarr zu beginnen. Wir werden einige Optionen überspringen, die Sie auf dem Bildschirm sehen können. Wenn Sie tiefer in diese Optionen eintauchen möchten, finden Sie eine ausführliche Erklärung auf der entsprechenden Seite in den FAQ und der Dokumentation.

> Bitte beachten Sie, dass in den Screenshots und GUI-Einstellungen in `orange` erweiterte Optionen enthalten sind. Sie müssen oben auf der Seite auf `Erweitert anzeigen` klicken, um sie sichtbar zu machen.

# Indexer

Das erste, was Sie in Prowlarr einrichten müssen, sind Indexer. Sie fügen jeden Indexer einzeln zu Prowlarr hinzu.

Klicken Sie auf `Indexer` und dann auf das +, um einen neuen Indexer hinzuzufügen.

![addindexer.png](/assets/prowlarr/addindexer.png)

Alle Indexer, die Sie hinzufügen können (Usenet und Torrent), sind aufgelistet, und Sie können eingeben, um eine teilweise Übereinstimmung mit einem vorhandenen Eintrag zu erzielen. Wenn der Indexer, den Sie hinzufügen möchten, nicht in der Liste vorhanden ist, können Sie "Generic Newznab" (für Usenet) oder "Generic Torznab" (für Torrents) hinzufügen.

![addgeneric.png](/assets/prowlarr/addgeneric.png)

Einige Indexer haben spezielle Einstellungen, aber die meisten sind standardmäßig wie gezeigt.

![addnewindexer.png](/assets/prowlarr/addnewindexer.png)

- Name - Wählen Sie einen Namen für diesen Indexer aus. Wenn er mit Ihren Apps synchronisiert wird, wird er `(Prowlarr)` dahinter hinzufügen.
- Aktivieren - Aktivieren Sie diese Option, um diesen Indexer zu aktivieren.
- Umleiten - Aktivieren Sie diese Option, wenn eine Umleitung erforderlich ist. Es gibt nur wenige Indexer, bei denen dies erforderlich ist, um eine Sperrung zu vermeiden. Wenn diese Option aktiviert ist, wird der Download-Link direkt an die Anwendung weitergeleitet, anstatt ihn über Prowlarr zu proxyen.

> Eine Umleitung ist in der Regel nur für eine Handvoll sehr spezifischer Indexer erforderlich.

- Sync-Profil - Wählen Sie hier Ihr Sync-Profil aus. Diese können in [`Einstellungen` => `Apps`](/prowlarr/settings#applications) erstellt werden. Das Standardprofil "Standard" existiert bereits und sieht so aus:

> Sie können unterschiedliche Einstellungen pro App haben, indem Sie mehrere Instanzen des Indexers erstellen.

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Wählen Sie die URL aus, die Prowlarr verwenden soll. Wenn leer, wird die Standard-/erste URL verwendet.
- Download-Link - Wenn Sie einen Torrent-Indexer hinzufügen, müssen Sie auswählen, welche Art von Download-Link verwendet werden soll.
- (Erweiterte Option) API-Pfad - Pfad zur API des Indexers. Normalerweise `/api`
- Anmeldeinformationen - Viele Indexer und Tracker erfordern eine Authentifizierung/Anmeldung auf irgendeine Weise. Sie müssen möglicherweise einen API-Schlüssel, einen RSS-Schlüssel, eine Sitzungs-ID, ein Cookie oder andere Anmeldeinformationen von Ihrem Indexer eingeben (normalerweise auf Ihrer Profilseite oder unter Sicherheit zu finden), Suchreihenfolgen auswählen oder andere Optionen für Ihren spezifischen Indexer.
  - API-Schlüssel
  - RSS-Schlüssel
  - Sitzungs-ID
  - Cookie
  - Benutzername/Passwort
  - usw.
- (Erweiterte Option) Zusätzliche Parameter - Zusätzliche Parameter, die zu den Anfragen für diesen Indexer hinzugefügt werden sollen.
- VIP-Ablauf - Geben Sie das Datum im ISO-Format (yyyy-MM-DD) ein, um 1 Woche vor Ablauf benachrichtigt zu werden; lassen Sie es sonst leer
- Tags - Verwenden Sie Tags, um Standard-Download-Clients festzulegen, Indexer-Proxies festzulegen, Indexer für Anwendungen festzulegen oder einfach Ihre Indexer zu organisieren.
- (Erweiterte Option) Abfrage-Limit - Wenn Ihr Indexer Ihre API-Aufrufe pro Tag begrenzt, können Sie hier die Anzahl eingeben, um die Grenze nicht zu überschreiten.
- (Erweiterte Option) Grab-Limit - Wenn Ihr Indexer Ihre Grabs pro Tag begrenzt, können Sie hier die Anzahl eingeben, um die Grenze nicht zu überschreiten. Sobald das Grab-Limit erreicht ist, lösen weitere Abfragen eine unbehandelte Ausnahme in \*Arr Apps aus. Andere Apps können unterschiedlich reagieren.
- (Erweiterte Option) Seed-Verhältnis - Nur für Torrent-Indexer: Das Verhältnis, das ein Torrent erreichen sollte, bevor es gestoppt wird. Leer bedeutet die Standard-Einstellung der App.
- (Erweiterte Option) Seed-Zeit - Nur für Torrent-Indexer: Die Zeit, die ein Torrent gesät werden sollte, bevor er gestoppt wird. Leer bedeutet die Standard-Einstellung der App.
- (Erweiterte Option) Indexer-Priorität - Wählen Sie hier die Indexer-Priorität von 1-50 (1 ist die höchste). Diese Prioritäten werden mit Ihren Apps synchronisiert.

Testen Sie Ihren Eintrag. Wenn ein grünes Häkchen angezeigt wird, können Sie Ihren Eintrag speichern und bei Bedarf für jeden Indexer, den Sie von Prowlarr verwenden möchten, wiederholen. Wenn es fehlschlägt, müssen Sie Ihre Protokolldatei auf den Fehler überprüfen (URL, API-Schlüssel usw.).

# Apps

Nachdem Sie Ihre Indexer hinzugefügt haben, verbinden wir Prowlarr mit Ihren anderen Apps.

Klicken Sie auf `Einstellungen` => `Apps` und dann auf das +, um eine unterstützte App hinzuzufügen.

![addapps.png](/assets/prowlarr/addapps.png)

Alle Programme, die Sie hinzufügen können, sind aufgelistet. Sie sollten nur Programme hinzufügen, die Sie bereits installiert haben, und wenn Sie mehrere Instanzen davon haben, müssen Sie jede von ihnen separat hinzufügen.

> Aktuell unterstützte Apps finden Sie auf der [Weitere Informationen (Unterstützte)](/prowlarr/supported#applications) Seite für diesen Abschnitt

Wenn Sie eine App hinzufügen, müssen Sie Werte im Popup-Fenster eingeben:

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Hinweis: Indexer werden basierend auf den von ihnen behaupteten Fähigkeiten/Kategorien synchronisiert. Wenn ein Indexer nur `tv`-Kategorien unterstützt, wird er nicht mit Lidarr, Radarr und Readarr synchronisiert. Er wird nur mit Sonarr synchronisiert. "Unterstützte" Kategorien können als erweiterte Einstellung pro App ausgewählt werden. **Beachten Sie auch, dass die \*Arrs nur Indexer akzeptieren, deren Testabfragen Ergebnisse enthalten, die mindestens eine der konfigurierten Kategorien enthalten.**

## Anwendungseinstellungen

- Name - Geben Sie einen Namen für diese App ein.
- Sync-Level - Wählen Sie das Sync-Level aus, das verwendet werden soll.
  - `Nur hinzufügen und entfernen` - Wenn Indexer zu Prowlarr hinzugefügt oder entfernt werden, wird die Remote-App aktualisiert. Wenn der Indexer zum Zeitpunkt der Synchronisierung nicht verfügbar ist, wird er in der Remote-App deaktiviert.
  - `Vollständige Synchronisierung` - Die vollständige Synchronisierung hält die Indexer dieser App vollständig synchron. Änderungen, die an Indexern in Prowlarr vorgenommen werden, werden dann mit dieser App synchronisiert. Jede Änderung, die an den Einstellungen auf der FAQ-Seite für diese Indexer in dieser App vorgenommen wird, wird von Prowlarr bei der nächsten Synchronisierung überschrieben. Eine Liste der Faktoren, die verwendet werden, um zu vergleichen und zu bestimmen, ob eine Synchronisierung erfolgen soll, finden Sie in den [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Deaktiviert` - verhindert die Synchronisierung von Indexern mit dem Programm vollständig.

> `Vollständige Synchronisierung` bedeutet, dass Prowlarr die meisten Einstellungen überschreibt, einschließlich der vom Benutzer ausgewählten Kategorien, die in Prowlarr konfigurierbar sind. Nicht von Prowlarr verwaltete Einstellungen werden jedoch nicht geändert. Jedoch [werden fast alle anderen Änderungen](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) eine Synchronisierung auslösen und die entsprechenden Einstellungen in \*Arr überschreiben.
{.is-warning}

- Tags - Wenn Sie während der Einrichtung einen Tag zu Ihrem Indexer hinzugefügt haben, werden nur Indexer mit diesem Tag für diesen Programmeintrag verwendet.
- Prowlarr-Server - Geben Sie hier die URL des Prowlarr-Servers ein (einschließlich http, Port und Basis-URL, falls erforderlich), wie die App darauf zugreifen würde.

> Beachten Sie, dass Sie, wenn Sie einen Reverse-Proxy verwenden, die URL-Basis hinzufügen müssen! Wenn Sie dies nicht tun, werden die Indexer beim Synchronisieren unterbrochen, und wenn Sie "Nur hinzufügen und entfernen" ausgewählt haben, wird dies nicht behoben, wenn Sie es bearbeiten!

- Anwendungsserver - Geben Sie hier die URL des App-Servers ein (einschließlich http, Port und Basis-URL, falls erforderlich) Ihrer Anwendung. Geben Sie bei Bedarf die vollständige URL-Basis ein.
- API-Schlüssel - Geben Sie hier den API-Schlüssel Ihrer Anwendung ein. Für \*Arrs finden Sie diesen in Einstellungen => Allgemein. Sie können diesen Schlüssel von Ihrem Programm im Tab `Einstellungen` => `Allgemein` erhalten und hier kopieren/einfügen.
- (Erweiterte Einstellung) Kategorien synchronisieren - Wählen Sie die Kategorien aus, die mit dieser App synchronisiert werden sollen. Indexer, die diese Kategorien unterstützen, werden synchronisiert.
  - Indexer-Benutzerdefinierte Kategorien werden in die Standard-Torznab/Newznab-Kategorien abgebildet, sodass die Suche nach den standardisierten Kategorien alle zugrunde liegenden benutzerdefinierten Kategorien einschließt. Indexer-Benutzerdefinierte Kategorien werden zur Feinabstimmung aufgelistet, wenn Sie sie nicht alle auf einmal möchten.

> Wenn Sie dies speichern, werden Ihre Indexer mit der App synchronisiert. Sie werden alle mit dem von Ihnen für Ihren Indexer gewählten Namen plus (Prowlarr) hinzugefügt. z.B. `{Indexer-Name} (Prowlarr)`

![nzbgeek.png](/assets/prowlarr/nzbgeek.png)

Gehen Sie dann in Ihr Programm und deaktivieren Sie die nicht-Prowlarr-Version des Indexers. Sobald alles reibungslos läuft, können Sie diese Einträge löschen und nur die (Prowlarr)-Versionen beibehalten.

Sie können die Kategorien für die Prowlarr-Indexer in Ihren Programmen überprüfen. Standardkategorien, die in die App abgebildet werden sollen, können als erweiterte Einstellung für die App in Prowlarr konfiguriert werden.

> **Bitte beachten Sie, dass benutzerdefinierte/nicht-standardmäßige Indexer-spezifische Kategorien auf Standardkategorien abgebildet werden, sodass die Suche nach Standardkategorien alle benutzerdefinierten Kategorien einschließt**

## Sync-Profile

Konfigurieren Sie die Sync-Profile, die für (eine) Anwendung(en) verwendet werden sollen.

- Name - Eindeutiger Name des Sync-Profils
- RSS aktivieren - Für Indexer mit diesem Profil RSS-Suchen/Abfragen für die \*Arr-App aktivieren
- Interaktive Suche aktivieren - Für Indexer mit diesem Profil interaktive (manuelle) Suchen für die \*Arr-App aktivieren
- Automatische Suche aktivieren - Für Indexer mit diesem Profil automatische Suchen für die \*Arr-App aktivieren
- Mindestanzahl Seeder - Für Indexer mit diesem Profil die Mindestanzahl an Seedern, die für \*Arr erforderlich sind, um einen Torrent herunterzuladen

# Download-Clients (Prowlarr-Suchen)

> Wenn Sie beabsichtigen, direkt in Prowlarr zu suchen, müssen Sie Download-Clients hinzufügen. Andernfalls müssen Sie sie hier nicht hinzufügen. Für Suchen von Ihren Apps aus werden die dort konfigurierten Download-Clients verwendet.

> Download-Clients sind nur für Prowlarr-In-App-Suchen und werden nicht mit Apps synchronisiert. Es sind keine Pläne vorhanden, eine solche Funktionalität hinzuzufügen.

Klicken Sie auf `Einstellungen` => `Download-Clients` und dann auf das +, um einen neuen Download-Client hinzuzufügen. Ihr Download-Client sollte bereits so konfiguriert sein, wie in dieser Anleitung beschrieben.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

> Aktuell unterstützte Download-Clients finden Sie auf der [Weitere Informationen (Unterstützte)](/prowlarr/supported#downloadclient) Seite für diesen Abschnitt

Wählen Sie den Download-Client aus, den Sie hinzufügen möchten, und es wird ein Popup-Fenster zur Eingabe der Verbindungsdetails angezeigt. Diese Details sind für die meisten Clients ähnlich. Einige fragen nach einem Benutzernamen oder Passwort, andere fragen, ob neue Downloads im pausierten/Startzustand hinzugefügt werden sollen, usw.  
![nzbget.png](/assets/prowlarr/nzbget.png)

> Die Priorität des Clients ist nur relevant, wenn 2 Clients desselben Typs (Usenet oder Torrent) hinzugefügt werden. 1 ist die höchste Priorität, und wenn mehrere Clients desselben Typs vorhanden sind und die gleiche Priorität haben, wechselt Prowlarr zwischen ihnen.

## Usenet-Client-Einstellungen

- Name - Der Name des Download-Clients in Prowlarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- URL-Basis - Ein Präfix zur URL hinzufügen; dies ist häufig für Reverse Proxies erforderlich.
- API-Schlüssel - Der API-Schlüssel zur Authentifizierung bei Ihrem Client
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Kategorie - Die Kategorie in Ihrem Download-Client, die Prowlarr verwenden wird
- Priorität - Download-Client-Priorität für hinzugefügte Elemente
- Client-Priorität - Priorität des Download-Clients in Prowlarr. Bei Clients desselben Typs (Torrent/Usenet) mit gleicher Priorität wird Round-Robin verwendet.

## Torrent-Client-Einstellungen

- Name - Der Name des Download-Clients in Prowlarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- URL-Basis - Ein Präfix zur URL hinzufügen; dies ist häufig für Reverse Proxies erforderlich.
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client
- Kategorie - Die Kategorie in Ihrem Download-Client, die Prowlarr verwenden wird
- Priorität - Download-Client-Priorität für hinzugefügte Elemente
- Anfangszustand - Anfangszustand für Torrents (nur Qbittorrent: Erzwungenes Umgehen aller Seed-Schwellenwerte)
- Client-Priorität - Priorität des Download-Clients in Prowlarr. Bei Clients desselben Typs (Torrent/Usenet) mit gleicher Priorität wird Round-Robin verwendet.

## Testen des Download-Clients

Testen Sie Ihren Eintrag. Wenn ein grünes Häkchen angezeigt wird, können Sie Ihren Eintrag speichern und bei Bedarf für jeden Download-Client, den Sie von Prowlarr verwenden möchten, wiederholen. Wenn es fehlschlägt, müssen Sie Ihre Protokolldatei auf den Fehler (Verbindung, Anmeldeinformationen usw.) überprüfen.

# Setup abgeschlossen

Das war's mit den Grundlagen! Sie können dann Benachrichtigungen und andere fortgeschrittenere Einrichtungsoptionen nach Bedarf hinzufügen. Diese sind in der vollständigen Einstellungsseite dokumentiert.