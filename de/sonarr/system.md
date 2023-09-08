# Status

## Health

- Diese Seite enthält eine Liste von Fehlermeldungen der Gesundheitsprüfungen. Diese Gesundheitsprüfungen werden regelmäßig von Sonarr durchgeführt und bei bestimmten Ereignissen. Die resultierenden Warnungen und Fehler werden hier aufgelistet, um Ratschläge zur Behebung zu geben.

### Systemwarnungen

#### Derzeit installierte .NET Framework-Version ist veraltet und wird nicht unterstützt

- Sonarr verwendet das .NET Framework. Wir müssen Sonarr gegen die niedrigste von unseren Benutzern verwendete unterstützte Version erstellen. Gelegentlich erhöhen wir die Version, gegen die wir erstellen, um neue Funktionen nutzen zu können. Offensichtlich haben Sie seit einiger Zeit keine entsprechenden Windows-Updates angewendet und müssen .NET aktualisieren, um neuere Versionen von Sonarr verwenden zu können.

- Das Aktualisieren des .NET Frameworks ist auf Windows sehr einfach, erfordert jedoch häufig einen Neustart.

#### Derzeit installierte .NET Framework-Version wird unterstützt, aber ein Upgrade wird empfohlen

- Sonarr verwendet das .NET Framework. Wir müssen Sonarr gegen die niedrigste von unseren Benutzern unterstützte Version erstellen. Durch ein Upgrade auf neuere Versionen können wir gegen neuere Versionen erstellen und neue Framework-Funktionen verwenden.

- Das Aktualisieren des .NET Frameworks ist auf Windows sehr einfach, erfordert jedoch häufig einen

#### Derzeit installierte Mono-Version ist veraltet und wird nicht unterstützt

- Sonarr v4 ist in .NET geschrieben und v3 erforderte Mono. Mono 5.20 ist das absolute Minimum für Sonarr.
- Das Upgrade-Verfahren für Mono variiert je nach Plattform.

> Mono wird ab Sonarr Version 4.0 nicht mehr unterstützt
{.is-warning}

#### Derzeit installierte SQLite-Version wird nicht unterstützt

- Sonarr speichert seine Daten in einer SQLite-Datenbank. Die auf Ihrem System installierte SQLite3-Bibliothek ist zu alt. Sonarr erfordert mindestens Version 3.9.0.

> Beachten Sie, dass Sonarr `libSQLite3.so` verwendet, das möglicherweise in einem SQLite3-Upgrade-Paket enthalten ist oder nicht.
{.is-info}

#### Paketwartungsnachricht

- Ihr Paketbetreuer hat eine Nachricht für Sie. Dies wird vom Betreuer gesteuert und nicht von Sonarr.

#### Ein neues Update ist verfügbar

- Freuen Sie sich, die Entwickler haben ein neues Update veröffentlicht. Dies bedeutet in der Regel großartige neue Funktionen und behobene Fehler (richtig?). Offensichtlich haben Sie die automatische Aktualisierung nicht aktiviert, sodass Sie herausfinden müssen, wie Sie auf Ihrer Plattform aktualisieren können. Das Drücken der Schaltfläche "Installieren" auf der Seite System => Updates ist wahrscheinlich ein guter Ausgangspunkt.

> Diese Warnung wird nicht angezeigt, wenn Ihre aktuelle Version weniger als 14 Tage alt ist
{.is-info}

#### Update kann nicht installiert werden, da der Startordner und/oder der UI-Ordner vom Benutzer nicht beschreibbar sind

{#cannot-install-update-because-UI-folder-is-not-writable-by-the-user}

{#cannot-install-update-because-startup-folder-is-not-writable-by-the-user}

Dies bedeutet, dass Sonarr sich nicht selbst aktualisieren kann. Sie müssen Sonarr manuell aktualisieren oder die Berechtigungen für das Startverzeichnis von Sonarr (das Installationsverzeichnis) so festlegen, dass Sonarr sich selbst aktualisieren kann.

#### Update kann nicht installiert werden, da der Startordner in einem App-Translokationsordner liegt

In macOS Sierra hat Apple eine seltsame Sicherheitsfunktion namens App-Translokation (manchmal auch als Gatekeeper Path Randomization bezeichnet) hinzugefügt, die bedeutet, dass nach dem Herunterladen einer Anwendung, wenn Sie die resultierende Anwendung nicht irgendwohin (überallhin!) Mit dem Finder verschieben (Sie müssen den Finder verwenden!), wird die Anwendung so ausgeführt, als ob sie sich an einem vom System zufällig gewählten Pfad befindet.

#### Aktualisierung ist nicht möglich, um das Löschen von AppData beim Update zu verhindern

Sonarr hat erkannt, dass der AppData-Ordner für Ihr Betriebssystem im Verzeichnis liegt, das die Sonarr-Binärdateien enthält. Normalerweise wäre dies C:\ProgramData für Windows und ~/.config für Linux.

Bitte schauen Sie sich System => Info an, um die aktuellen AppData- und Startordner anzuzeigen.
Dies bedeutet, dass Sonarr sich nicht selbst aktualisieren kann, ohne ein Datenverlustrisiko einzugehen.
Wenn Sie Linux verwenden, müssen Sie wahrscheinlich das Home-Verzeichnis für den Benutzer ändern, der Sonarr ausführt, und den aktuellen Inhalt des Verzeichnisses ~/.config/Sonarr kopieren, um Ihre Datenbank zu erhalten.

#### IP-Adresse für den konfigurierten Proxy-Host konnte nicht aufgelöst werden

Überprüfen Sie Ihre Proxy-Einstellungen und stellen Sie sicher, dass sie korrekt sind
Stellen Sie sicher, dass Ihr Proxy aktiv, ausgeführt und erreichbar ist

#### Proxy-Test fehlgeschlagen

Ihr konfigurierter Proxy-Test ist fehlgeschlagen. Überprüfen Sie den bereitgestellten HTTP-Fehler und/oder überprüfen Sie die Protokolle für weitere Details.

#### Systemzeit weicht um mehr als 1 Tag ab

Die Systemzeit weicht um mehr als 1 Tag ab. Geplante Aufgaben werden möglicherweise nicht ordnungsgemäß ausgeführt, bis die Zeit korrigiert ist
Überprüfen Sie Ihre Systemzeit und stellen Sie sicher, dass sie mit einem autoritativen Zeitserver synchronisiert ist und korrekt ist

#### MediaInfo-Bibliothek konnte nicht geladen werden

Die MediaInfo-Bibliothek konnte nicht geladen werden. Sonarr benötigt MediaInfo (`libmediainfo`), um die Videoattribute von Dateien zu bewerten.

#### Mono Legacy TLS aktiviert

{#sonarr-mono-4.x-tls-workaround-still-enabled-consider-removing-mono_tls_provider-legacy-environment-option}

Mono 4.x TLS-Workaround ist immer noch aktiviert. Erwägen Sie das Entfernen der Umgebungsoption MONO_TLS_PROVIDER=legacy.

### Download-Clients

#### Es ist kein Download-Client verfügbar

Ein ordnungsgemäß konfigurierter und aktivierter Download-Client ist erforderlich, damit Sonarr Medien herunterladen kann. Da Sonarr verschiedene Download-Clients unterstützt, sollten Sie feststellen, welcher Ihren Anforderungen am besten entspricht. Wenn Sie bereits einen Download-Client installiert haben, sollten Sie Sonarr so konfigurieren, dass er ihn verwendet und eine Kategorie erstellt. Siehe Einstellungen => Download-Client.

#### Es konnte keine Verbindung zum Download-Client hergestellt werden

Sonarr konnte keine Verbindung zum konfigurierten Download-Client herstellen. Überprüfen Sie, ob der Download-Client betriebsbereit ist, und überprüfen Sie die URL erneut. Dies kann auch auf einen Authentifizierungsfehler hinweisen.
Dies liegt in der Regel an einem falsch konfigurierten Download-Client. Dinge, die Sie in der Regel überprüfen können:
Die IP-Adresse Ihres Download-Clients, wenn er sich auf demselben Bare-Metal-Computer befindet, ist dies in der Regel 127.0.0.1
Die Portnummer, die Ihr Download-Client verwendet, diese sind mit der Standardportnummer ausgefüllt, aber wenn Sie sie geändert haben, müssen Sie dieselbe Nummer in Sonarr eingeben.
Stellen Sie sicher, dass die SSL-Verschlüsselung nicht aktiviert ist, wenn Sie Ihre Sonarr-Instanz und Ihren Download-Client in einem lokalen Netzwerk verwenden. Weitere Informationen finden Sie in der SSL-FAQ.

#### Download-Clients sind aufgrund eines Fehlers nicht verfügbar

Einer oder mehrere Ihrer Download-Clients reagieren nicht auf Anfragen von Sonarr. Daher hat Sonarr beschlossen, die Abfrage des Download-Clients in seinem normalen 1-Minuten-Zyklus vorübergehend zu stoppen, der normalerweise verwendet wird, um aktive Downloads zu verfolgen und abgeschlossene Downloads zu importieren. Sonarr wird jedoch weiterhin versuchen, Downloads an den Client zu senden, wird aber höchstwahrscheinlich scheitern.
Sie sollten System => Protokolle überprüfen, um den Grund für die Fehler zu sehen.
Wenn Sie diesen Download-Client nicht mehr verwenden, deaktivieren Sie ihn in Sonarr, um Fehler zu vermeiden.

#### Abgeschlossene Download-Verarbeitung aktivieren

- Sonarr erfordert die Aktivierung der abgeschlossenen Download-Verarbeitung, um Dateien importieren zu können, die vom Download-Client heruntergeladen wurden. Es wird empfohlen, die abgeschlossene Download-Verarbeitung zu aktivieren.
(Die abgeschlossene Download-Verarbeitung ist standardmäßig aktiviert...)

#### Docker-Fehler bei der Remotepfadzuordnung

- Dieser Fehler ist in der Regel mit falschen Docker-Pfaden in Ihrem Download-Client oder Sonarr verbunden.

- Ein Beispiel dafür wäre:
  - Download-Client: Download-Pfad: /mnt/user/downloads:/downloads
  - Radarr: Download-Pfad: /mnt/user/downloads:/data
- In diesem Beispiel legt der Download-Client seine Downloads in /downloads ab und teilt Radarr dann mit, dass der fertige Film in /downloads ist. Sonarr kommt dann und sagt "Okay, cool, lass mich in /downloads nachsehen" Nun, in Radarr haben Sie keinen /downloads-Pfad zugewiesen, sondern einen /data-Pfad, daher wird dieser Fehler angezeigt.
- Die einfachste Lösung dafür ist KONSISTENZ. Wenn Sie ein Schema in Ihrem Download-Client verwenden, verwenden Sie es überall.

- Team Sonarr ist ein großer Fan von einfach /data zu verwenden.
  - Download-Client: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Jetzt können Sie in Ihrem Download-Client angeben, wo Sie Ihre Downloads in /data platzieren möchten. Dies variiert je nach Client, aber Sie sollten ihm sagen können "Ja, Download-Client platziere meine Dateien in." /data/torrents (oder Usenet)/movies und da Sie in Radarr /data verwendet haben, wenn der Download-Client Radarr mitteilt, dass er fertig ist, wird Radarr kommen und sagen "Super, ich habe ein /data und ich kann auch /torrents (oder Usenet)/movies sehen, alles ist in Ordnung auf der Welt."
- Es gibt viele großartige Anleitungen: Unser Wiki [Docker-Anleitung](/docker-guide) und TRaSH's [Hardlinks und Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Diese Anleitungen legen zwar großen Wert auf Hardlinks und Atomic-Moves, aber das allgemeine Konzept von Containern und der Funktionsweise der Pfadzuordnung ist der Kern dieser Diskussionen.

- Weitere Informationen finden Sie in [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/).

#### In das Root-Verzeichnis herunterladen

{#downloads-in-root-folder}

- In der Anwendung wird ein Root-Ordner als der konfigurierte Medienbibliotheksordner definiert. Dies ist nicht das Stammverzeichnis eines Mounts. Ihr Download-Client hat einen unvollständigen oder vollständigen (oder verschiebt abgeschlossene Downloads) in Ihren Root (Bibliotheks-) Ordner.
- Dies führt häufig zu Problemen - einschließlich Datenverlust - und sollte nicht durchgeführt werden. Ändern Sie Ihren Download-Client so, dass er Downloads nicht in Ihrem Root-Ordner platziert. Beachten Sie, dass "Platzieren" auch bedeutet, dass Ihre Download-Client-Kategorie auf Ihren Root-Ordner festgelegt ist oder wenn NZBGet/SABnzbd sortiert aktiviert haben und in Ihren Root-Ordner sortieren.
- Bitte beachten Sie, dass diese Überprüfung alle definierten/konfigurierten Root-Ordner überprüft, nicht nur die aktuell verwendeten Root-Ordner. Mit anderen Worten, der Ordner, in den Ihr Download-Client herunterlädt oder abgeschlossene Downloads verschiebt, sollte nicht derselbe Ordner sein, den Sie als Ihren Root/Bibliotheks-/endgültigen Medienzielordner in der *arr-Anwendung konfiguriert haben.
- Konfigurierte Root-Ordner (auch als Bibliotheksordner bezeichnet) finden Sie in [Einstellungen => Medienverwaltung => Root-Ordner](/sonarr/settings/#root-folders)
- Ein Beispiel ist, wenn Ihre Downloads in `/data/downloads` gehen, dann haben Sie einen Root-Ordner als `/data/downloads` festgelegt.
- Es wird empfohlen, Pfade wie `/data/media/` für Ihren Root-Ordner/Bibliothek und `/data/downloads/` für Ihre Downloads zu verwenden.
- Lesen Sie unsere [Docker-Anleitung](/docker-guide) und TRaSH's [Hardlinks und Instant Moves (Atomic-Moves) Anleitung](https://trash-guides.info/hardlinks/) für weitere Informationen zur korrekten und optimalen Pfadkonfiguration. Beachten Sie, dass die Konzepte für Docker und Nicht-Docker gelten

> Ihr Download-Ordner, in dem Ihr Download-Client die Downloads platziert, und Ihr Root/Bibliotheks-Ordner MÜSSEN getrennt sein. \*Arr importiert die Datei(en) aus dem Download-Ordner Ihres Download-Clients in Ihre Bibliothek. Der Download-Client sollte nichts verschieben oder etwas in Ihre Bibliothek herunterladen.
{.is-warning}

#### Falsche Download-Client-Einstellungen

- Der Speicherort, an den Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne eine Remotepfadzuordnung zu wechseln, umfassen.

#### Falsche Remotepfadzuordnung

- Der Speicherort, an den Ihr Download-Client Dateien herunterlädt, verursacht Probleme. Überprüfen Sie die Protokolle für weitere Informationen. Dies kann Berechtigungen oder den Versuch, von Windows zu Linux oder von Linux zu Windows ohne eine Remotepfadzuordnung zu wechseln, umfassen. Weitere Informationen finden Sie in [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/).

#### Berechtigungsfehler

- Sonarr oder der Benutzer, unter dem Sonarr ausgeführt wird, kann nicht auf den Speicherort zugreifen, an den Ihr Download-Client Dateien herunterlädt. Dies ist in der Regel ein Berechtigungsproblem.

#### Remote-Datei wurde während der Verarbeitung teilweise entfernt

- Eine über einen Remotepfad zugängliche Datei scheint vor Abschluss der Verarbeitung entfernt worden zu sein.

#### Remotepfad wird verwendet und Import ist fehlgeschlagen

- Überprüfen Sie Ihre Protokolle für weitere Informationen; siehe unsere Fehlerbehebungshandbücher

### In das Root-Verzeichnis herunterladen

{#downloads-in-root-folder}

- Innerhalb der Anwendung wird ein Stammordner als der konfigurierte Medienbibliotheksordner definiert. Dies ist nicht der Stammordner eines Mounts. Ihr Download-Client hat unvollständige oder abgeschlossene Downloads (oder verschiebt abgeschlossene Downloads) in Ihren Stamm (Bibliotheks-) Ordner.
- Dies führt häufig zu Problemen - einschließlich Datenverlust - und sollte nicht durchgeführt werden. Um dies zu beheben, ändern Sie Ihren Download-Client so, dass er Downloads nicht in Ihren Stammordner platziert. Beachten Sie, dass "Platzieren" auch bedeutet, dass Ihre Download-Client-Kategorie auf Ihren Stammordner eingestellt ist oder wenn NZBGet/SABnzbd die Sortierung aktiviert haben und in Ihren Stammordner sortieren.
- Bitte beachten Sie, dass diese Überprüfung alle definierten/konfigurierten Stammordner betrachtet, nicht nur die aktuell verwendeten Stammordner. Mit anderen Worten, der Ordner, in den Ihr Download-Client Downloads herunterlädt oder abgeschlossene Downloads verschiebt, sollte nicht derselbe Ordner sein, den Sie als Ihren Stamm-/Bibliotheks-/endgültigen Medienzielordner in der *arr-Anwendung konfiguriert haben.
- Konfigurierte Stammordner (auch als Bibliotheksordner bezeichnet) finden Sie unter [Einstellungen => Medienverwaltung => Stammordner](/sonarr/settings/#root-folders)
- Ein Beispiel ist, wenn Ihre Downloads in `/data/downloads` gespeichert werden, dann haben Sie einen Stammordner als `/data/downloads` festgelegt.
- Es wird empfohlen, Pfade wie `/data/media/` für Ihren Stammordner/Bibliothek und `/data/downloads/` für Ihre Downloads zu verwenden.
- Lesen Sie unseren [Docker-Leitfaden](/docker-guide) und TRaSH's [Hardlinks und Instant Moves (Atomic-Moves) Leitfaden](https://trash-guides.info/hardlinks/) für weitere Informationen zur korrekten und optimalen Pfadkonfiguration. Beachten Sie, dass die Konzepte sowohl für Docker als auch für Nicht-Docker gelten.

> Ihr Download-Ordner, in dem Ihr Download-Client die Downloads platziert, und Ihr Stamm-/Bibliotheksordner MÜSSEN getrennt sein. \*Arr importiert die Datei(en) aus dem Download-Ordner Ihres Download-Clients in Ihre Bibliothek. Der Download-Client sollte nichts verschieben oder etwas in Ihre Bibliothek herunterladen.
{.is-warning}

#### Die Behandlung abgeschlossener Downloads ist deaktiviert

{#completedfailed-download-handling}

- Es ist erforderlich, die Behandlung abgeschlossener Downloads zu verwenden, da sie eine bessere Kompatibilität für die Entpackungs- und Nachverarbeitungslogik verschiedener Download-Clients bietet. Mit ihr importiert Sonarr einen Download erst, wenn der Download-Client ihn als bereit meldet.
- Wenn die Behandlung abgeschlossener Downloads deaktiviert ist:
  - Alle Importe müssen manuell behandelt werden
  - Diese Gesundheitsprüfung bleibt bestehen und kann nicht abgelehnt oder deaktiviert werden
  - Episoden werden immer in Sonarr fehlen und können dauerhaft abgegriffen werden
    - Von Benutzern manuell in den Serienordner in Sonarrs Bibliotheksordner verschobene und umbenannte Episoden werden möglicherweise vom zweimal täglichen erneuten Scannen erfasst, wenn sie ordnungsgemäß benannt sind und zu diesem Zeitpunkt nicht fehlen.
  - Der Benutzer muss manuell die Überwachung aufheben oder ein benutzerdefiniertes Skript für das Ereignis "Beim Erfassen" konfigurieren.
  - FlexGet ist wahrscheinlich ein besseres Werkzeug für den Anwendungsfall, wenn Sie die Medienbibliotheksverwaltungsfunktionen von Sonarr nicht verwenden möchten und einfach etwas benötigen, um RSS-Feeds zu analysieren und Veröffentlichungen an den Download-Client zu senden.

> Die Behandlung abgeschlossener Downloads funktioniert nur ordnungsgemäß, wenn der Download-Client und Sonarr auf demselben Computer ausgeführt werden, da Sonarr den Pfad zum Importieren direkt vom Download-Client erhält. Andernfalls ist eine Remote-Zuordnung erforderlich.
> Die Behandlung abgeschlossener Downloads erfordert, dass Sonarr Lese- und Schreibzugriff auf das Verzeichnis für abgeschlossene Downloads hat.
{.is-warning}

### Indexer

#### Keine Indexer verfügbar, bei denen die automatische Suche aktiviert ist. Sonarr liefert keine automatischen Suchergebnisse.

- Ganz einfach, Sie haben keine Ihrer Indexer so eingestellt, dass automatische Suchen erlaubt sind. Gehen Sie zu Einstellungen > Indexer, wählen Sie einen Indexer aus, bei dem Sie automatische Suchen zulassen möchten, und klicken Sie dann auf Speichern.

#### Keine Indexer verfügbar, bei denen die RSS-Synchronisierung aktiviert ist. Sonarr greift nicht automatisch auf neue Veröffentlichungen zu.

{#no-indexers-available-with-rss-sync-enabled,-sonarr-will-not-grab-new-releases-automatically}
{#all-rss-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Sonarr verwendet den RSS-Feed, um neue Veröffentlichungen zu erfassen, wenn sie auftreten. [Weitere Informationen finden Sie in den FAQ](/sonarr/faq#how-does-sonarr-find-episodes)
- Um dieses Problem zu beheben, gehen Sie zu Einstellungen > Indexer, wählen Sie einen Indexer aus, den Sie haben, und aktivieren Sie die RSS-Synchronisierung.

#### Keine Indexer aktiviert

- Sonarr benötigt Indexer, um neue Veröffentlichungen entdecken zu können. Alle Ihre Indexer sind deaktiviert oder Sie haben keine Indexer hinzugefügt.

#### Aktivierte Indexer unterstützen keine Suche

{#all-search-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Keiner der von Ihnen aktivierten und verfügbaren Indexer unterstützt die Suche. Das bedeutet, dass Sonarr nur über die RSS-Feeds neue Veröffentlichungen finden kann. Die Suche nach Serien (entweder automatische Suche oder manuelle Suche) liefert niemals Ergebnisse. Die einzige Möglichkeit, dies zu beheben, besteht darin, einen weiteren Indexer hinzuzufügen.

#### Keine Indexer verfügbar, bei denen die interaktive Suche aktiviert ist. Sonarr liefert keine interaktiven Suchergebnisse.

{#no-indexers-available-with-interactive-search-enabled-sonarr-will-not-provide-any-interactive-search-results}

- Keiner der von Ihnen aktivierten und verfügbaren Indexer unterstützt die interaktive Suche. Das bedeutet, dass die Anwendung nur über die RSS-Feeds oder eine automatische Suche neue Veröffentlichungen finden kann.

#### Indexer sind aufgrund von Fehlern nicht verfügbar

- Fehler sind aufgetreten, als Sonarr versuchte, einen Ihrer Indexer zu verwenden. Um die Anzahl der Wiederholungsversuche zu begrenzen, wird Sonarr den Indexer für eine zunehmende Zeit (bis zu 24 Stunden) nicht verwenden.
- Dieser Mechanismus wird ausgelöst, wenn Sonarr keine Antwort vom Indexer erhalten konnte (könnte durch DNS, Proxy/VPN-Verbindung, Authentifizierung oder ein Indexer-Problem verursacht werden) oder die NZB-/Torrent-Datei nicht vom Indexer abrufen konnte. Bitte überprüfen Sie die Protokolle, um festzustellen, welche Art von Fehler das Problem verursacht hat.
- Sie können diese Warnung verhindern, indem Sie den betroffenen Indexer deaktivieren.
- Führen Sie einen Test auf dem Indexer aus, um Sonarr dazu zu zwingen, den Indexer erneut zu überprüfen. Beachten Sie, dass die Warnung der Gesundheitsprüfung nicht immer sofort verschwindet und Sie möglicherweise den Task "Gesundheit überprüfen" ausführen müssen.

#### Jackett All Endpoint verwendet

- Der Jackett /all-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere sind potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Selbst die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des /all-Endpunkts hat keine Vorteile, nur Nachteile:
  - Sie verlieren die Kontrolle über indexer-spezifische Einstellungen (Kategorien, Suchmodi usw.)
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen
  - Indexer-spezifische Kategorien (\>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt
  - Wenn einer der Tracker in /all einen Fehler zurückgibt, deaktiviert \*Arr ihn und Sie erhalten keine Ergebnisse mehr.

##### Lösungen

- Fügen Sie jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu.
- Schauen Sie sich [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schauen Sie sich [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwenden Sie jedoch nicht ihren einzelnen aggregierten Endpunkt und verwenden Sie `multi`, wenn die Synchronisierung verwendet wird.

### Medien & Listen

#### Serie(n) wurde(n) von TheTVDB entfernt

- Die betroffene Serie(n) wurde(n) von [The TVDb](https://thetvdb.com) entfernt. Dies geschieht normalerweise, weil die Serie ein Duplikat ist oder als Teil einer anderen Serie betrachtet wird. Alternativ behandelt TVDb sie als Serie; hoffentlich auch TMDb, damit [Radarr](/radarr) verwendet werden kann. Um dies zu korrigieren, müssen Sie die betroffene Serie entfernen und gegebenenfalls die richtige Serie hinzufügen.

#### Listen sind aufgrund von Fehlern nicht verfügbar

{#import-lists-are-unavailable-due-to-failures}

- In der Regel bedeutet dies einfach, dass Sonarr nicht mehr über die API oder durch Anmeldung bei Ihrem ausgewählten Listenanbieter kommunizieren kann. Wenn das Problem weiterhin besteht, sollten Sie sie kontaktieren, um sie auszuschließen, da ihre Systeme von Zeit zu Zeit überlastet sein können.
- Überprüfen Sie System => Ereignisse, die nach Warnungen (Warnungen & Fehler) gefiltert sind, um die historischen Fehler zu sehen, oder überprüfen Sie die Protokolle für weitere Details.

#### Importliste fehlt Stammordner

- Eine oder mehrere Ihrer Importlisten sind auf einen Stammordner konfiguriert, auf den Sonarr keinen Zugriff hat.
- Dies kann auf Berechtigungsprobleme, ein fehlendes Mount oder einfach darauf zurückzuführen sein, dass die Listen nach der Neuorganisation Ihres Setups aktualisiert werden müssen.

#### Stammordner fehlt

- Ein Stammordner wurde zu Sonarr hinzugefügt und existiert nicht oder ist nicht zugänglich.
- Dieser Fehler wird in der Regel identifiziert, wenn eine Serie nach einem Stammordner sucht, der nicht mehr verfügbar ist.
- Dieser Fehler kann auch auftreten, wenn eine Liste immer noch auf einen Stammordner zeigt, der nicht mehr verfügbar ist.
- Wenn Sie diese Warnung entfernen möchten, suchen Sie einfach die Serie, die immer noch den alten Stammordner verwendet, und bearbeiten Sie sie so, dass der richtige Stammordner verwendet wird.

- Der einfachste Weg, die problematische Serie zu finden, besteht darin:

  - Gehen Sie zum Masseneditor-Tab
  - Erstellen Sie einen benutzerdefinierten Filter mit dem alten Stammordnerpfad
  - Wählen Sie Massenbearbeitung in der oberen Leiste aus und wählen Sie aus dem Dropdown-Menü "Stammordner" den neuen Stammordnerpfad aus, zu dem Sie diese Serien verschieben möchten.
  - Als Nächstes erhalten Sie einen Popup, in dem steht Möchten Sie die Serienordner in 'Stammordner' verschieben? Dies wird auch angeben Dies wird auch den Serienordner gemäß dem Serienordnerformat in den Einstellungen umbenennen. Wählen Sie einfach Nein aus, wenn Sie nicht möchten, dass Lidarr Ihre Dateien verschiebt.
  - Führen Sie den Task "Gesundheit überprüfen" in System => Aufgaben aus.

#### Serienpfad-Mount ist schreibgeschützt

{#series-mount-ro}

Ein Mount, der einen Serienpfad enthält, ist schreibgeschützt und kann vom Benutzer, unter dem Sonarr ausgeführt wird, nicht beschrieben werden.

## Festplattenspeicher

- In diesem Abschnitt wird Ihnen der verfügbare Festplattenspeicher angezeigt.
- In Docker kann dies knifflig sein, da Ihnen in der Regel der verfügbare Speicherplatz innerhalb Ihres Docker-Images angezeigt wird.

## Über

- Hier erfahren Sie mehr über Ihre aktuelle Installation von Sonarr.

## Weitere Informationen

- Startseite: Sonarr's [Startseite](https://www.sonarr.tv)
- Wiki: Sie sind bereits hier.
- Reddit: [r/sonarr](https://www.reddit.com/r/sonarr)
- Discord: Treten Sie unserem [Discord](https://discord.sonarr.tv/) bei.
- Spenden: Wenn Sie großzügig sind und spenden möchten, klicken Sie [hier](https://sonarr.tv/donate).
- Quellcode: [GitHub](https://www.github.com/sonarr/sonarr)
- Funktionsanfragen: Haben Sie eine großartige Idee? Teilen Sie sie [hier](https://www.github.com/sonarr/sonarr/issues).

# Aufgaben

## Geplant

- In diesem Abschnitt werden alle geplanten Aufgaben aufgelistet, die Sonarr ausführt.

- Anwendungsaktualisierung überprüfen - Dies wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan ausgeführt und prüft, ob Sonarr auf der neuesten Version ist und löst dann das Aktualisierungsskript aus, um Sonarr zu aktualisieren. Einstellungen => Aktualisierung

> Hinweis: Wenn Sie Docker verwenden, wird dadurch Ihr Container nicht aktualisiert, da ein neues Image heruntergeladen werden muss.
{.is-warning}

- Backup - Dies führt gemäß dem festgelegten Zeitplan ein Backup der Datenbank von Sonarr durch. Weitere Informationen dazu finden Sie hier. Weitere Informationen zu Backups finden Sie unter System => Backups.
- Gesundheit überprüfen - Die Gesundheitsprüfung wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan durchgeführt und überprüft die allgemeine Gesundheit von Sonarr. Eine Liste möglicher gesundheitsbezogener Probleme finden Sie im Wiki-Eintrag zu Gesundheitsprüfungen.
- Papierkorb bereinigen - Der Papierkorb wird gemäß dem in der Benutzeroberfläche angezeigten Zeitplan geleert. Dies wird nur verwendet, wenn der Papierkorb in der Dateiverwaltung festgelegt ist.
- Aufräumen - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan werden alle Spinnweben entfernt, die Böden gefegt und gesaugt, gewischt und sogar ordentlich gefaltete Notizen für Sie erstellt. Aber den Müll rausbringen tut es nicht. Dafür wurde es einfach nicht genug bezahlt.
- Importliste synchronisieren - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan werden Ihre Listen ausgeführt und möglicherweise neue Serien importiert. Weitere Informationen zu Listen finden Sie unter Einstellungen => Listen.
- Bereinigung von Nachrichten - Gemäß dem in der Benutzeroberfläche angezeigten Zeitplan werden die Nachrichten bereinigt, die in der unteren linken Ecke von Sonarr angezeigt werden.
- Aktualisierung der überwachten Downloads - Dadurch wird die Download-Warteschlange unter Aktivität aktualisiert. Es wird im Wesentlichen Ihr Download-Client abgefragt, um nach abgeschlossenen Downloads zu suchen.
- Aktualisierung der Serien - Dadurch wird die Metadaten für alle überwachten und nicht überwachten Serien aktualisiert.
- RSS-Synchronisierung - Dadurch wird die RSS-Synchronisierung ausgeführt. Dies kann in Einstellungen => Indexer => Optionen geändert werden. Weitere Informationen zur RSS-Funktion finden Sie in unseren [FAQ](/sonarr/faq).

> Alle diese Aufgaben können außerhalb ihrer geplanten Zeiten manuell ausgeführt werden, indem Sie auf das Symbol ganz rechts neben jeder Aufgabe klicken.
{.is-info}

## Warteschlange

Die Warteschlange zeigt Ihnen laufende und bevorstehende Aufgaben sowie eine Historie der kürzlich ausgeführten Aufgaben und deren Dauer an.

# Backup

> Wenn Sie wissen möchten, wie Sie Ihre Sonarr-Instanz sichern/wiederherstellen können, klicken Sie [hier](/sonarr/faq).
{.is-info}

Im Backup-Bereich werden Ihnen frühere Backups angezeigt (sofern Sie keine frische Installation haben, die noch keine Backups erstellt hat).

- Jetzt sichern - Diese Option löst eine manuelle Sicherung der Datenbank von Sonarr aus.
- Backup wiederherstellen - Dadurch wird ein neuer Bildschirm geöffnet, um aus einem früheren Backup wiederherzustellen.
  - Durch Auswahl von Datei auswählen wird Ihr Browser aufgefordert, einen Dialog zum Wiederherstellen aus einem Sonarr-Zip-Backup zu öffnen.

- Wenn Sie frühere Backups haben und diese von Sonarr herunterladen möchten, um sie an einem anderen Ort zu speichern, können Sie einfach eine dieser Dateien auswählen, um sie herunterzuladen.
- Rechts neben jeder der vorherigen Downloads haben Sie zwei Optionen.

  - Wiederherstellen (Uhr-Symbol) - Zum Wiederherstellen aus einem früheren Backup - Dadurch wird ein neues Fenster geöffnet, um zu bestätigen, dass Sie aus diesem Backup wiederherstellen möchten.
  - Löschen (Mülleimer) - Zum Löschen eines früheren Backups

# Aktualisierungen

Der Aktualisierungsbildschirm zeigt die letzten 5 Aktualisierungen sowie die aktuelle Version an, die Sie verwenden.
Auf dieser Seite werden auch die Update-Notizen der Entwickler angezeigt, in denen steht, was in Sonarr behoben oder hinzugefügt wurde (Freuen Sie sich!)

> Ein Wartungsrelease enthält Fehlerbehebungen und andere verschiedene Verbesserungen. Werfen Sie einen Blick auf die Commit-Historie auf Github für Details.
{.is-info}

# Ereignisse

Der Ereignis-Tab zeigt Ihnen, was in Ihrem Sonarr passiert ist. Dies kann verwendet werden, um einige leichte Probleme zu diagnostizieren. Dies ersetzt jedoch nicht die Protokolle, die in der Protokollierung besprochen werden.

> Ereignisse entsprechen den INFO-Protokollen. {.is-info}

- Komponenten - Diese Spalte zeigt an, welche Komponente in Sonarr ausgelöst wurde.
- Nachricht - Diese Spalte zeigt an, welche Nachricht von der Komponente aus der vorherigen Spalte gesendet wurde.
- Zahnrad-Symbol - Diese Option ermöglicht es Ihnen, die Anzahl der angezeigten Komponenten/Nachrichten pro Seite zu ändern (Standardmäßig sind es 50).
- Optionen oben auf der Seite
  - Aktualisieren - Diese Option aktualisiert die aktuelle Seite und lädt ein neues Ereignisprotokoll.
  - Löschen - Dadurch wird das aktuelle Ereignisprotokoll gelöscht und Sie können von vorne beginnen.

# Protokolldateien

- Auf dieser Seite können Sie die aktuellen Protokolldateien für Sonarr herunterladen und anzeigen.

- In der obersten Zeile gibt es mehrere Optionen, mit denen Sie Ihre Protokolldateien steuern können.

- In der obersten Zeile ganz links befindet sich ein Dropdown-Menü, mit dem Sie zwischen Protokolldateien und Updater-Protokolldateien wechseln können.
  - Protokolldateien - Das A und O eines jeden Support-Problems. Weitere Informationen zu Protokolldateien finden Sie hier.
  - Updater-Protokolldateien - Hier werden die Protokolldateien für das Aktualisierungsskript von Sonarr angezeigt.

> Wenn Sie Docker verwenden, ist dies leer, da Sie ein neues Docker-Image herunterladen sollten, um ein Update durchzuführen.
{.is-info}

- Aktualisieren - Dadurch wird die aktuelle Seite aktualisiert und alle neu erstellten Protokolldateien angezeigt.
- Löschen - Dadurch werden alle Protokolle gelöscht und Sie können von vorne beginnen.
- Dateiname - Dadurch wird der Dateiname angezeigt, der mit dem Protokoll verknüpft ist.
- Zuletzt geschrieben - Dies ist die lokale Zeit, zu der diese bestimmte Protokolldatei geschrieben wurde.
  - Sonarr verwendet rollende Protokolldateien, die jeweils auf 1 MB begrenzt sind. Die aktuelle Protokolldatei ist immer sonarr.txt, für die anderen Dateien ist sonarr.0.txt die nächstneuere (je höher die Zahl, desto älter ist sie) bis zu insgesamt 51 Protokolldateien. Diese Protokolldatei enthält Einträge für `fatal`, `error`, `warn` und `info`.
  - Wenn der Debug-Protokollpegel aktiviert ist, sind zusätzliche sonarr.debug.txt rollende Protokolldateien vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info` und `debug`. Sie decken normalerweise einen Zeitraum von etwa 40 Stunden ab.
  - Wenn der Trace-Protokollpegel aktiviert ist, sind zusätzliche sonarr.trace.txt rollende Protokolldateien vorhanden, bis zu 51 Dateien. Diese Protokolldateien enthalten Einträge für `fatal`, `error`, `warn`, `info`, `debug` und `trace`. Aufgrund der ausführlichen Trace-Informationen deckt es normalerweise nur ein paar Stunden ab.