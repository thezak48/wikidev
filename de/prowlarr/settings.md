---
title: Prowlarr-Einstellungen
description: 
published: true
date: 2023-03-30T14:07:39.851Z
tags: 
editor: markdown
dateCreated: 2021-06-06T15:04:48.057Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Menüoptionen](#menüoptionen)
- [Indexer-Proxies](#indexer-proxies)
  - [Proxy-Einstellungen](#proxy-einstellungen)
  - [FlareSolverr-Proxy-Einstellungen](#flaresolverr-proxy-einstellungen)
  - [HTTP-Proxy-Einstellungen](#http-proxy-einstellungen)
  - [Socks4-Proxy-Einstellungen](#socks4-proxy-einstellungen)
  - [Socks5-Proxy-Einstellungen](#socks5-proxy-einstellungen)
- [Anwendungen](#anwendungen)
  - [Anwendungseinstellungen](#anwendungseinstellungen)
  - [Testen der Anwendung](#testen-der-anwendung)
- [Download-Clients (Prowlarr-Suchen)](#download-clients-prowlarr-suchen)
  - [Usenet-Client-Einstellungen](#usenet-client-einstellungen)
  - [Torrent-Client-Einstellungen](#torrent-client-einstellungen)
  - [Testen des Download-Clients](#testen-des-download-clients)
- [Benachrichtigungen](#benachrichtigungen)
  - [Verbindungen](#verbindungen)
  - [Benachrichtigungsauslöser](#benachrichtigungsauslöser)
- [Tags](#tags)
- [Allgemein](#allgemein)
  - [Host](#host)
  - [Sicherheit](#sicherheit)
  - [Proxy](#proxy)
  - [Protokollierung](#protokollierung)
  - [Analytik](#analytik)
  - [Updates](#updates)
  - [Backups](#backups)
- [UI](#ui)
  - [Datumsangaben](#datumsangaben)
  - [Stil](#stil)
  - [Sprache](#sprache)
  
Diese Seite enthält eine Übersicht über alle verfügbaren Einstellungen in Prowlarr und wie sie funktionieren. Dies ist keine umfassende Anleitung zur Einrichtung von Prowlarr. Wenn Sie das möchten, verwenden Sie bitte die [Schnellstart](/prowlarr/quick-start-guide)-Seite.

# Menüoptionen

Um zur Einstellungsseite zu gelangen, wählen Sie bitte "Einstellungen" im linken Menü aus. Die folgenden Untermenüoptionen stehen zur Verfügung:

![settings_1_menu.png](/assets/prowlarr/settings_1_menu.png)

Beachten Sie auch, dass für jede einzelne Einstellungsseite einige Optionen oben im Menü vorhanden sind:

![settings_2_topmenu.png](/assets/prowlarr/settings_2_topmenu.png)

- "Erweitert ausblenden/zeigen" ist wichtig für alle Elemente, die unten als "(Erweiterte Option)" gekennzeichnet sind, da sie sonst nicht angezeigt werden. Diese Menüpunkte werden in den Screenshots orange angezeigt.

- Sie müssen Ihre Änderungen speichern, bevor Sie den Bildschirm verlassen. Klicken Sie dazu auf das Diskettensymbol. Wenn Sie keine Änderungen vorgenommen haben, wird "Keine Änderungen" angezeigt und ausgegraut, wie oben gezeigt.

# Indexer-Proxies

> Informationen zu unterstützten Proxy-Typen finden Sie auf der [Weitere Informationen (Unterstützt)](/prowlarr/supported#indexer-proxies)-Seite für diesen Abschnitt
{.is-info}

Hier können Sie Proxies oder Flaresolverr-Konfigurationen für Indexer hinzufügen, die diese erfordern.

Navigieren Sie zu "Einstellungen" => "Indexer-Proxies" und klicken Sie dann auf das <kb>+</kb>, um einen Proxy hinzuzufügen.

![proxies.png](/assets/prowlarr/proxies.png)

## Proxy-Einstellungen
  
- Name - Name des Proxys in Prowlarr
- Tags - Die Tags für diesen Proxy. Proxies gelten für alle übereinstimmenden (gleiche Tags) Indexer. Wenn leer, gilt dieser Proxy für alle Indexer.

## FlareSolverr-Proxy-Einstellungen

- Host - Der vollständige Host-Pfad (einschließlich http und Port) zu Ihrer FlareSolverr-Instanz
- (Erweiterte Einstellung) Anforderungs-Timeout (Sekunden) - Der [FlareSolver-Anforderungswert `maxTimeout`](https://github.com/FlareSolverr/FlareSolverr#-requestget), den Prowlarr für FlareSolverr-Anfragen verwenden soll. Muss zwischen `1` Sekunde und `180` Sekunden liegen (Standard: `60` Sekunden)

> \* Ein FlareSolverr-Proxy wird nur für Anfragen verwendet, wenn und nur wenn Cloudflare von Prowlarr erkannt wird.
> \* Ein FlareSolverr-Proxy wird nur für Anfragen verwendet, wenn und nur wenn der Proxy und der Indexer übereinstimmende Tags haben.
> \* **Ein Flaresolverr-Proxy, der ohne Tags konfiguriert ist oder keine Indexer mit übereinstimmenden Tags hat, wird deaktiviert.**
{.is-info}

## HTTP-Proxy-Einstellungen

- Host - Die Host-Adresse Ihres Proxys
- Port - Der Port Ihres Proxys
- Benutzername - Der Benutzername Ihres Proxys
- Passwort - Das Passwort Ihres Proxys

## Socks4-Proxy-Einstellungen

- Host - Die Host-Adresse Ihres Proxys
- Port - Der Port Ihres Proxys
- Benutzername - Der Benutzername Ihres Proxys
- Passwort - Das Passwort Ihres Proxys

## Socks5-Proxy-Einstellungen

- Host - Die Host-Adresse Ihres Proxys
- Port - Der Port Ihres Proxys
- Benutzername - Der Benutzername Ihres Proxys
- Passwort - Das Passwort Ihres Proxys

# Anwendungen

> Informationen zu unterstützten Anwendungen finden Sie auf der [Weitere Informationen (Unterstützt)](/prowlarr/supported#applications)-Seite für diesen Abschnitt
{.is-info}

Hier fügen Sie die Anwendungen hinzu, die Prowlarr verwendet (Radarr, Sonarr, Lidarr, Readarr usw.) und wie sie mit Prowlarr synchronisiert bleiben.

- Klicken Sie auf "Einstellungen" => "Apps" und dann auf das <kb>+</kb>, um eine App hinzuzufügen.
- Sync App Indexers - Löst eine Synchronisierung aller Indexer zu allen Anwendungen aus
- Test All Apps - Löst einen Test aller Anwendungen aus
  
![addapps.png](/assets/prowlarr/addapps.png)

Es werden alle Programme aufgelistet, die Sie hinzufügen können. Sie sollten nur Programme hinzufügen, die Sie derzeit installiert haben, und wenn Sie mehrere Instanzen davon haben, sollten Sie jede von ihnen separat hinzufügen.

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Hinweis: Indexer werden basierend auf den von ihnen unterstützten Fähigkeiten/Kategorien synchronisiert. Wenn ein Indexer nur `tv`-Kategorien unterstützt, wird er nicht mit Lidarr, Radarr und Readarr synchronisiert. Er wird nur mit Sonarr synchronisiert. "Unterstützte" Kategorien können als erweiterte Einstellung pro App ausgewählt werden. **Beachten Sie auch, dass die \*Arrs nur Indexer akzeptieren, deren Testabfragen Ergebnisse enthalten, die mindestens eine der konfigurierten Kategorien enthalten.**
{.is-info}

## Anwendungseinstellungen

- Name - Geben Sie einen Namen für diese App ein.
- Sync Level - Wählen Sie das Synchronisationsniveau aus
  - `Nur hinzufügen und entfernen` - Wenn Indexer zu Prowlarr hinzugefügt oder entfernt werden, wird die Remote-App aktualisiert. Wenn der Indexer zum Zeitpunkt der Synchronisierung nicht verfügbar ist, wird er in der Remote-App deaktiviert.
  - `Vollständige Synchronisierung` - Die vollständige Synchronisierung hält die Indexer dieser App vollständig synchron. Änderungen an Indexern in Prowlarr werden dann auf diese App synchronisiert. Jede Änderung, die in den Einstellungen auf der FAQ-Seite für diese Indexer remote in dieser App vorgenommen wird, wird bei der nächsten Synchronisierung von Prowlarr überschrieben. Eine Liste der Faktoren, die zum Vergleich und zur Bestimmung einer Synchronisierung verwendet werden, finden Sie in den [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Deaktiviert` - verhindert die Synchronisierung von Indexern mit dem Programm.

> `Vollständige Synchronisierung` bedeutet, dass Prowlarr die meisten Einstellungen überschreibt, einschließlich der vom Benutzer ausgewählten Kategorien, die in Prowlarr konfigurierbar sind. Nicht von Prowlarr verwaltete Einstellungen werden jedoch nicht geändert. Jedoch [werden fast alle anderen Änderungen](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) eine Synchronisierung auslösen und die entsprechenden Einstellungen in \*Arr überschreiben.
{.is-warning}

- Tags - Wenn Sie Ihrem Indexer während der Einrichtung ein Tag hinzugefügt haben, werden nur Indexer mit diesem Tag für diesen Programmeintrag verwendet.
- Prowlarr-Server - Geben Sie die URL des Prowlarr-Servers (einschließlich http, Port und Baseurl, falls erforderlich) ein, wie die App darauf zugreifen würde.

> Beachten Sie, dass Sie bei Verwendung eines Reverse-Proxys die URL-Basis hier hinzufügen müssen! Wenn Sie dies nicht tun, werden die Indexer beim Synchronisieren beschädigt, und wenn Sie "Nur hinzufügen und entfernen" ausgewählt haben, wird dies nicht behoben, wenn Sie es bearbeiten!{.is-info}

- Anwendungsserver - Geben Sie hier die URL des App-Servers (einschließlich http, Port und Baseurl, falls erforderlich) Ihrer Anwendung ein. Geben Sie bei Bedarf die vollständige URL-Basis ein.
- API-Schlüssel - Geben Sie hier den API-Schlüssel Ihrer Anwendung ein. Für \*Arrs finden Sie diesen in "Einstellungen" => "Allgemein". Sie können dies von Ihrer Anwendung im Register "Einstellungen" => "Allgemein" abrufen und hier kopieren/einfügen.
- (Erweiterte Einstellung) Kategorien synchronisieren - Wählen Sie die Kategorien aus, die mit dieser App synchronisiert werden sollen. Indexer, die diese Kategorien unterstützen, werden synchronisiert.
  - Indexer-Benutzerdefinierte Kategorien werden in die Standard-Torznab/Newznab-Kategorien umgewandelt, sodass bei der Suche nach den standardisierten Kategorien alle zugrunde liegenden benutzerdefinierten Kategorien einbezogen werden. Indexer-Benutzerdefinierte Kategorien werden zur Feinabstimmung aufgelistet, wenn Sie sie nicht alle auf einmal möchten.
  
## Testen der Anwendung

Testen Sie Ihren Eintrag. Wenn ein grünes Häkchen angezeigt wird, können Sie Ihren Eintrag speichern und bei Bedarf für jede Anwendung wiederholen, die Sie mit Prowlarr synchronisieren möchten. Wenn der Test fehlschlägt, müssen Sie Ihr Protokoll auf den Fehler (URL, API-Schlüssel usw.) überprüfen.

## Synchronisierungsprofile

Konfigurieren Sie die Synchronisierungsprofile für (eine) Anwendung(en)

> Sie können verschiedene Einstellungen pro App haben, indem Sie mehrere Instanzen des Indexers erstellen
{.is-info}

- Name - Eindeutiger Name des Synchronisierungsprofils
- RSS aktivieren - Für Indexer mit diesem Profil RSS-Suchen/Abfragen für die \*Arr-App aktivieren
- Interaktive Suche aktivieren - Für Indexer mit diesem Profil interaktive (manuelle) Suchen für die \*Arr-App aktivieren
- Automatische Suche aktivieren - Für Indexer mit diesem Profil automatische Suchen für die \*Arr-App aktivieren
- Mindestanzahl an Seedern - Für Indexer mit diesem Profil die Mindestanzahl an Seedern, die von \*Arr für einen Torrent benötigt wird, festlegen

# Download-Clients (Prowlarr-Suchen)

{#download-clients}

> Informationen zu unterstützten Download-Clients finden Sie auf der [Weitere Informationen (Unterstützt)](/prowlarr/supported#download-clients)-Seite für diesen Abschnitt
{.is-info}

Wenn Sie beabsichtigen, direkt in Prowlarr zu suchen, müssen Sie Download-Clients hinzufügen. Andernfalls müssen Sie sie hier nicht hinzufügen. Für Suchen von Ihren Apps aus werden die dort konfigurierten Download-Clients verwendet.

> Prowlarr synchronisiert keine Download-Clients mit den Anwendungen.
{.is-info}

Klicken Sie auf "Einstellungen" => "Download-Clients" und dann auf das <kb>+</kb>, um einen neuen Download-Client hinzuzufügen. Ihr Download-Client sollte bereits entsprechend dieser Anleitung konfiguriert sein.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

Wählen Sie den Download-Client aus, den Sie hinzufügen möchten, und es wird ein Popup-Fenster angezeigt, in dem Sie Verbindungsdetails eingeben können. Diese Details sind für die meisten Clients ähnlich. Einige fragen nach einem Benutzernamen oder Passwort, andere fragen, ob neue Downloads im pausierten/Startzustand hinzugefügt werden sollen, usw.
  
> Die Priorität des Clients ist nur relevant, wenn 2 Clients desselben Typs (Usenet oder Torrent) hinzugefügt werden. 1 ist die höchste Priorität, und wenn mehrere Clients desselben Typs vorhanden sind und die gleiche Priorität haben, wechselt Prowlarr zwischen ihnen.
{.is-info}

## Usenet-Client-Einstellungen

- Name - Der Name des Download-Clients in Prowlarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- URL-Basis - Fügen Sie einen Präfix zur URL hinzu; dies ist häufig für Reverse-Proxys erforderlich.
- API-Schlüssel - Der API-Schlüssel zur Authentifizierung bei Ihrem Client
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client (in der Regel nicht erforderlich)
- Kategorie - Die Kategorie in Ihrem Download-Client, die Prowlarr verwenden wird
- Priorität - Priorität des Download-Clients für hinzugefügte Elemente
- Client-Priorität - Priorität des Download-Clients in Prowlarr. Bei Clients desselben Typs (Torrent/Usenet) mit gleicher Priorität wird Round-Robin verwendet.

## Torrent-Client-Einstellungen

- Name - Der Name des Download-Clients in Prowlarr
- Aktivieren - Diesen Download-Client aktivieren
- Host - Die URL Ihres Download-Clients
- Port - Der Port Ihres Download-Clients; dies ist in der Regel der WebGUI-Port
- SSL verwenden - Eine sichere Verbindung mit Ihrem Download-Client verwenden. Bitte beachten Sie diesen häufigen Fehler.
- URL-Basis - Fügen Sie einen Präfix zur URL hinzu; dies ist häufig für Reverse-Proxys erforderlich.
- Benutzername - Der Benutzername zur Authentifizierung bei Ihrem Client
- Passwort - Das Passwort zur Authentifizierung bei Ihrem Client
- Kategorie - Die Kategorie in Ihrem Download-Client, die Prowlarr verwenden wird
- Priorität - Priorität des Download-Clients für hinzugefügte Elemente
- Ausgangszustand - Ausgangszustand für Torrents (nur Qbittorrent: "Forced" umgeht alle Seed-Schwellenwerte)
- Client-Priorität - Priorität des Download-Clients in Prowlarr. Bei Clients desselben Typs (Torrent/Usenet) mit gleicher Priorität wird Round-Robin verwendet.

## Testen des Download-Clients

Testen Sie Ihren Eintrag. Wenn ein grünes Häkchen angezeigt wird, können Sie Ihren Eintrag speichern und bei Bedarf für jeden Download-Client wiederholen, den Prowlarr verwenden soll. Wenn der Test fehlschlägt, müssen Sie Ihr Protokoll auf den Fehler (Verbindung, Anmeldeinformationen usw.) überprüfen.

# Benachrichtigungen

> Informationen zu unterstützten Benachrichtigungsanbietern finden Sie auf der [Weitere Informationen (Unterstützt)](/prowlarr/supported#notifications)-Seite für diesen Abschnitt
{.is-info}

## Verbindungen

Verbindungen legen fest, wie Prowlarr mit der Außenwelt kommunizieren soll.

- Durch Drücken der <kb>+</kb>-Schaltfläche wird ein neues Fenster geöffnet, in dem Sie viele verschiedene Endpunkte konfigurieren können.

- Eine Liste der unterstützten Benachrichtigungen und Verbindungen finden Sie unter [Weitere Informationen (Unterstützt)](/prowlarr/supported#notifications)

## Benachrichtigungsauslöser

- Bei Freigabe erfassen - Benachrichtigung bei Freigabeerfassung in Prowlarr oder über die API erhalten
  - Manuelle Erfassungen einschließen - Benachrichtigung bei manuellen Erfassungen innerhalb der Prowlarr-Benutzeroberfläche erhalten
- Bei Problemen mit der Gesundheit - Benachrichtigung bei Fehlern bei der Gesundheitsprüfung erhalten
  - Gesundheitswarnungen einschließen - Benachrichtigung bei Gesundheitswarnungen zusätzlich zu Fehlern erhalten.
- Bei Anwendungsupdate - Benachrichtigung erhalten, wenn Prowlarr auf eine neue Version aktualisiert wird

# Tags

- Der Tag-Bereich in Prowlarr wird verwendet, um verschiedene Aspekte von Prowlarr zu verknüpfen.
- Tags sind besonders nützlich für:
  - Aktivieren des Flaresolverr-Proxys für die Verwendung mit einem Indexer; Beachten Sie, dass Flaresolverr-Proxys ohne Tag deaktiviert sind
  - Aktivieren eines HTTP- oder SOCKS-Proxys für die Verwendung mit einem Indexer
  - Festlegen von Indexern für bestimmte Apps

# Allgemein

Hier ändern Sie allgemeine Anwendungseinstellungen wie Port und Protokollierungsstufe.

Klicken Sie auf "Einstellungen" => "Allgemein".

> Viele der hier verfügbaren Optionen können nur angezeigt werden, indem Sie oben auf dem Bildschirm auf "Erweitert anzeigen" klicken. Alle Menüpunkte in Orange werden nur angezeigt, wenn "Erweitert anzeigen" aktiviert ist.
{.is-info}

## Host

![general_host.png](/assets/prowlarr/general_host.png)

- (Erweiterte Option) Bind-Adresse - Lassen Sie dies auf `*`, es sei denn, Sie müssen es ändern. Die IPv4-Adresse/der Host auf dem System, auf dem Prowlarr lauschen wird. (Standard: `*`)
  - Beachten Sie, dass `*` alle Adressen bedeutet
- Portnummer - Der Port, auf dem Prowlarr läuft. Er muss eindeutig sein. (Standard: 9696)
- BaseUrl - Geben Sie hier eine URL-Basis ein, wenn Sie einen Reverse-Proxy verwenden. (Neustart erforderlich) (Standard: leer)
- (Erweiterte Option) Instanzname - Name für Browser-Tab und SysLog (falls aktiviert) (Neustart erforderlich) (Standard: Prowlarr)
- (Erweiterte Option) SSL verwenden - Aktivieren Sie dieses Kontrollkästchen, wenn Sie eine https-Adresse zum Verbinden mit Prowlarr verwenden. Wenn Sie "localhost" oder eine IP-Adresse verwenden, sollte dies fast NIE aktiviert sein. (Standard: false)
- Browser starten (nur Windows) - Aktivieren Sie dieses Kontrollkästchen, wenn beim Start von Prowlarr ein Browserfenster geöffnet werden soll. (Standard: ja)

## Sicherheit

![general_security.png](/assets/prowlarr/general_security.png)

- Authentifizierung - Wie möchten Sie sich bei Ihrer Prowlarr-Instanz authentifizieren?
  - Keine - Sie haben keine Authentifizierung, um auf Ihre Prowlarr zuzugreifen. Normalerweise, wenn Sie der einzige Benutzer in Ihrem Netzwerk sind, niemand in Ihrem Netzwerk Zugriff auf Ihre Radarr haben möchte oder Ihre Radarr nicht über das Internet erreichbar ist.
  - Basic (Browser-Popup) - Diese Option zeigt beim Zugriff auf Ihre Prowlarr ein kleines Popup-Fenster an, in dem Sie einen Benutzernamen und ein Passwort eingeben können.
  - Formulare (Anmeldeseite) - Diese Option bietet eine vertraut aussehende Anmeldeseite, ähnlich wie bei anderen Websites, auf der Sie sich bei Ihrer Prowlarr anmelden können.
- API-Schlüssel - Der API-Schlüssel wird von externen Apps verwendet, um auf Prowlarr zuzugreifen. Dies ist geheim und sollte nicht mit anderen geteilt werden. Wenn er geteilt wird, sollten Sie ihn erneuern und Ihre Apps aktualisieren.
- Zertifikatsvalidierung - Ändern Sie die Strenge der HTTPS-Zertifikatsvalidierung.
  - Aktiviert - Überprüfen Sie alle HTTPS-Zertifikate (empfohlen).
  - Deaktiviert für lokale Adressen - Überprüfen Sie alle HTTPS-Zertifikate, außer denen auf localhost und im LAN.
  - Deaktiviert - Überprüfen Sie keine HTTPS-Zertifikate.

## Proxy

![general_proxy.png](/assets/prowlarr/general_proxy.png)

Proxy - Diese Option ermöglicht es Ihnen, die von Ihrer Prowlarr abgerufenen Informationen und Suchanfragen über einen Proxy zu leiten. Dies kann nützlich sein, wenn Sie sich in einem Land befinden, das das Herunterladen von Torrent-Dateien nicht erlaubt.

- Proxy verwenden - Aktivieren Sie diese Option, um einen Proxy zu verwenden.
- Proxy-Typ - Wählen Sie Ihren Proxy-Typ (HTTPS, Socks4 oder Socks5).
- Hostname - Geben Sie den Hostnamen Ihres Proxys ein (ohne http/https oder ein anderes Protokoll).
- Port - Geben Sie den Proxy-Port ein.
- Benutzername - Geben Sie Ihren Proxy-Benutzernamen ein, falls zutreffend.
- Passwort - Geben Sie Ihr Proxy-Passwort ein, falls zutreffend.
- Ignorierte Adressen - Geben Sie eine kommagetrennte Liste von Adressen ein, die den Proxy umgehen sollen.
- Proxy für lokale Adressen umgehen - Aktivieren Sie das Kontrollkästchen, um den Proxy für lokale Adressen zu umgehen.

## Protokollierung

![general_logging.png](/assets/prowlarr/general_logging.png)

Das Standard-Protokollniveau ist `Info`. Dies ist sehr grundlegende Protokollierung. Sie können es hier ändern, um detailliertere Protokollierung zu erhalten. Die Protokolldateien werden rotiert, sodass keine Gefahr besteht, zu viel Speicherplatz zu belegen.

- Protokollniveau - Wahrscheinlich eines der nützlichsten Tools zur Fehlerbehebung.
  - Info - Dies ist die grundlegendste Art und Weise, wie Prowlarr Informationen sammelt. Dies enthält nur eine sehr geringe Menge an Informationen in den Protokollen. Diese Protokolldatei enthält Einträge zu Fehlern, Warnungen und Informationen.
  - Debug - Debug enthält alle Informationen, die Info enthält, sowie zusätzliche nützliche Informationen. Diese Protokolldatei enthält Einträge zu Fehlern, Warnungen, Informationen und Debugging.
  - Trace - Die umfangreichste und detaillierteste Protokollierung in Prowlarr. Trace enthält alle Informationen, die von Info und Debug gesammelt wurden, und mehr. Dies ist der häufigste Protokolltyp, der bei der Fehlerbehebung in Discord oder Reddit angefordert wird. Wenn Sie Hilfe benötigen, wählen Sie bitte Ihr Protokoll auf Trace und wiederholen Sie die Aufgabe, die Ihnen Probleme bereitet hat, um das Protokoll zu erfassen. Diese Protokolldatei enthält Einträge zu Fehlern, Warnungen, Informationen, Debugging und Trace.

## Analytics

![general_analytics.png](/assets/prowlarr/general_analytics.png)

- Analytics - Senden Sie anonyme Nutzungs- und Fehlerinformationen an die Server von Prowlarr (Servarr). Dies umfasst Informationen über Ihren Browser, welche Prowlarr WebUI-Seiten Sie verwenden, Fehlerberichte sowie Informationen über das Betriebssystem, die Laufzeitversion und verwandte Informationen. Wir werden diese Informationen verwenden, um Funktionen und Fehlerbehebungen zu priorisieren.

## Updates

![general_updates.png](/assets/prowlarr/general_updates.png)

- (Erweiterte Option) Branch - Dies ist der Zweig von Prowlarr, den Sie verwenden.
  - [Bitte lesen Sie diesen FAQ-Eintrag für weitere Informationen](/prowlarr/faq#how-do-i-update-prowlarr)
- Automatisch - Updates automatisch herunterladen und installieren. Sie können weiterhin über System: Updates installieren. Hinweis: Windows-Benutzer werden immer automatisch aktualisiert.
- Mechanismus - Verwenden Sie den integrierten Updater von Prowlarr oder ein Skript.
  - Integriert - Verwenden Sie den eigenen Updater von Prowlarr.
  - Skript - Lassen Sie Prowlarr das Aktualisierungsskript ausführen.
  - Docker - Aktualisieren Sie Prowlarr nicht von innerhalb des Docker, sondern ziehen Sie ein brandneues Image mit dem neuen Update.
- Skript - Nur sichtbar, wenn der Mechanismus auf Skript eingestellt ist - Pfad zum Aktualisierungsskript.
- Aktualisierungsprozess - Prowlarr lädt die Aktualisierungsdatei herunter, überprüft deren Integrität, extrahiert sie an einen temporären Speicherort und ruft die gewählte Methode auf. Der Aktualisierungsprozess wird unter demselben Benutzer ausgeführt, unter dem Prowlarr ausgeführt wird. Er benötigt Berechtigungen, um die Prowlarr-Dateien zu aktualisieren und Prowlarr zu starten/stoppen.
- Integriert - Die integrierte Methode sichert Prowlarr-Dateien und -Einstellungen, stoppt Prowlarr, aktualisiert die Installation und startet Prowlarr neu. Wenn Ihr System das Stoppen von Prowlarr nicht verarbeiten kann und versucht, es automatisch neu zu starten, ist es möglicherweise besser, stattdessen ein Skript zu verwenden. Im Falle eines Fehlers wird die vorherige Version von Prowlarr neu gestartet.
- Skript - Das Skript sollte dasselbe wie der integrierte Updater behandeln. Wenn Sie Dienste stoppen und starten müssen (upstart/launchd/etc), müssen Sie dies hier tun.

## Backups

![general_backups.png](/assets/prowlarr/general_backups.png)

- (Erweiterte Option) Ordner - Hier können Sie den Speicherort für das Backup auswählen. In Docker sind Sie auf das beschränkt, was der Container sehen darf. Die Pfade sind relativ zum Appdata-Ordner; falls erforderlich, können Sie einen absoluten Pfad angeben, um außerhalb des Appdata-Ordners zu sichern.
- (Erweiterte Option) Intervall - Wie oft soll Prowlarr ein Backup erstellen?
- (Erweiterte Option) Aufbewahrung - Wie lange soll Prowlarr jedes Backup aufbewahren? Nachdem ein neues Backup erstellt wurde, wird das älteste Backup entfernt.

> Manuelle Backups werden unbegrenzt aufbewahrt, im selben Ordner gespeichert und haben einen anderen Namen.
{.is-info}

# Benutzeroberfläche

## Daten

- Kurzes Datumsformat - Wie möchten Sie, dass Prowlarr kurze Datumsangaben anzeigt?
- Langes Datumsformat - Wie möchten Sie, dass Prowlarr lange Datumsangaben anzeigt?
- Zeitformat - Möchten Sie ein 12-Stunden- oder 24-Stunden-Format?
- Relative Daten anzeigen - Möchten Sie, dass Prowlarr relative (Heute/Gestern/usw.) oder absolute Daten anzeigt?

## Stil

- Thema - Wählen Sie das Farbthema, das Prowlarr verwenden soll, inspiriert von [Theme.Park](https://github.com/GilbN/theme.park).
- Farbsehschwäche-Modus aktivieren - Geänderter Stil, um es farbsehschwachen Benutzern zu ermöglichen, farbcodierte Informationen besser zu unterscheiden.

## Sprache

- UI-Sprache - Wählen Sie die Sprache, die Prowlarr in der Anwendungsoberfläche verwenden soll.