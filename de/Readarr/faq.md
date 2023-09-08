- No, you cannot disable the refresh books task in Readarr. The refresh books task is responsible for updating the metadata and status of your books, ensuring that Readarr has the most up-to-date information. Disabling this task would prevent Readarr from accurately tracking the status of your books and could lead to inconsistencies in your library.

- Nein, und auch nicht durch SQL-Hackerei. Die Aufgabe zum Aktualisieren von Büchern ruft den Upstream-Servarr-Proxy ab und überprüft, ob sich die Metadaten für jedes Buch (IDs, Besetzung, Zusammenfassung, Bewertung, Übersetzungen, alternative Titel usw.) im Vergleich zu dem, was sich derzeit in Readarr befindet, aktualisiert haben. Falls erforderlich, werden die entsprechenden Bücher aktualisiert.
- Eine häufige Beschwerde ist, dass die Aktualisierungsaufgabe eine hohe E/A-Auslastung verursacht. Eine Einstellung, die Probleme verursachen kann, ist "Nach Aktualisierung Autorordner erneut scannen". Wenn Ihre Festplatten-E/A-Auslastung während einer Aktualisierung stark ansteigt, sollten Sie diese Einstellung auf "Manuell" ändern. Ändern Sie dies nicht auf "Nie", es sei denn, alle Änderungen an Ihrer Bibliothek (neue Bücher, Upgrades, Löschungen usw.) werden über Readarr durchgeführt. Wenn Sie Buchdateien manuell löschen oder ein Programm von Drittanbietern verwenden, stellen Sie dies nicht auf "Nie" ein.

## Kann ich sowohl eine E-Book- als auch eine Hörbuchversion desselben Buches haben?

- Nein. Mit einer einzigen Readarr-Instanz können Sie entweder das eine oder das andere haben, aber nicht beides. Wenn Sie beides möchten, müssen Sie zwei separate Readarr-Instanzen ausführen (ähnlich wie einige Leute 2 Instanzen von Sonarr oder Radarr für 1080p- und 4K-Versionen ihrer Medien ausführen).

## Muss ich Calibre verwenden?

- Nein. Im Allgemeinen bietet Calibre einige weitere Verbesserungen, wie z.B. die Möglichkeit, E-Books automatisch in ein anderes Format umzuwandeln, das den Fähigkeiten Ihres E-Readers entspricht, und auch eine Verbindung zu diesem E-Reader herzustellen. Aber wenn Sie Calibre vor der Installation von Readarr nicht verwendet haben, wird es Ihnen wahrscheinlich von begrenztem Nutzen sein, es zu installieren, und es handelt sich um ein sehr großes Programm.

## Warum kann Readarr meine Dateien auf einem Remote-Server nicht sehen?

- Stellen Sie für alle Betriebssysteme sicher, dass der Benutzer/die Gruppe, unter der/dem Sie \*Arr ausführen, Lese- und Schreibzugriff auf das eingebundene Laufwerk hat.
- Für Linux stellen Sie sicher:
  - Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass "nolock" für Ihr Laufwerk aktiviert ist.
  - Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass "nobrl" für Ihr Laufwerk aktiviert ist.
- Für Windows: Kurz gesagt: Der Benutzer, unter dem \*Arr ausgeführt wird (wenn als Dienst) oder unter dem es ausgeführt wird (wenn als Tray-App), kann nicht auf den Dateipfad auf dem Remote-Server zugreifen. Dies kann verschiedene Gründe haben, aber am häufigsten tritt das Problem auf, wenn \*Arr als Dienst ausgeführt wird.

### Readarr wird standardmäßig unter dem LocalService-Konto ausgeführt, das keinen Zugriff auf geschützte Remote-Dateifreigaben hat

- Führen Sie den Readarr-Dienst als anderen Benutzer aus, der Zugriff auf diese Freigabe hat.
- Öffnen Sie das Fenster "Verwaltungstools" > "Dienste" auf Ihrem Windows-Server.
- Stoppen Sie den Readarr-Dienst.
- Öffnen Sie den Dialog "Eigenschaften" > "Anmelden".
- Ändern Sie das Benutzerkonto des Dienstes auf das Zielbenutzerkonto.
- Führen Sie Readarr.exe über den Startordner aus.

### Sie verwenden ein gemapptes Netzlaufwerk (kein UNC-Pfad)

- Ändern Sie Ihre Pfade in UNC-Pfade (`\\server\freigabe`).
- Führen Sie Readarr.exe über den Startordner aus.

## Hilfe, ich habe mich ausgesperrt

{#help-i-have-forgotten-my-password}

Um die Authentifizierung zu deaktivieren (um Ihren vergessenen Benutzernamen oder Ihr vergessenes Passwort zurückzusetzen), müssen Sie `config.xml` bearbeiten, das sich im [Readarr-Appdata-Verzeichnis](/readarr/appdata-directory) befindet.

1. Öffnen Sie config.xml in einem Texteditor.
1. Suchen Sie die Zeile mit der Authentifizierungsmethode: `<AuthenticationMethod>Basic</AuthenticationMethod>` oder `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Ändern Sie die Zeile `AuthenticationMethod` in `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Starten Sie Readarr neu.
1. Readarr ist jetzt ohne Passwort zugänglich. Gehen Sie zur Registerkarte "Einstellungen: Allgemein" in der Benutzeroberfläche und legen Sie Ihren Benutzernamen und Ihr Passwort fest.

## Wie verhindere ich, dass der Browser beim Start geöffnet wird?

Je nach Betriebssystem gibt es mehrere mögliche Lösungen.

- In einigen Betriebssystemen gibt es in den "Einstellungen" > "Allgemein" ein Kontrollkästchen, um den Browser beim Start zu öffnen.
- Wenn Sie Readarr aufrufen, können Sie `-nobrowser` (*nix) oder `/nobrowser` (Windows) zu den Argumenten hinzufügen.
- Beenden Sie Readarr und bearbeiten Sie die Datei config.xml und ändern Sie `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Seltsame Probleme mit der Benutzeroberfläche

- Wenn Sie seltsame Probleme mit der Benutzeroberfläche haben, z.B. wenn die Bibliotheksseite nichts auflistet oder eine bestimmte Ansicht oder Sortierung nicht funktioniert, versuchen Sie es mit einem Inkognito-Fenster in Chrome oder einem privaten Fenster in Firefox. Wenn es dort einwandfrei funktioniert, löschen Sie den Browser-Cache und die Cookies für Ihre spezifische IP-/Domain. Weitere Informationen finden Sie im Wiki-Artikel [Cache, Cookies und lokalen Speicher löschen](/useful-tools#clearing-cookies-and-local-storage).

## VPNs, Jackett und die \*ARRs

- Es sei denn, Sie befinden sich in einem repressiven Land wie China, Australien oder Südafrika, in der Regel muss nur Ihr Torrent-Client hinter einem VPN sein. Da der VPN-Endpunkt von vielen Benutzern gemeinsam genutzt wird, können Sie Einschränkungen bei der Datenübertragungsrate, DDOS-Schutz und IP-Sperren von verschiedenen Diensten, die von der Software verwendet werden, erleben und erleiden.
- Mit anderen Worten, das Verwenden eines VPNs für die \*Arrs (Lidarr, Prowlarr, Radarr, Readarr und Lidarr) kann dazu führen, dass die Anwendungen in einigen Fällen aufgrund der Nichterreichbarkeit der Dienste nicht verwendet werden können.

> **Um es klar zu sagen: Es ist nicht die Frage, ob VPNs Probleme mit den \*Arrs verursachen, sondern wann: Bildanbieter werden Sie blockieren und Cloudflare steht vor den meisten \*Arr-Servern (Updates, Metadaten usw.) und wird Sie ebenfalls blockieren.**
{.is-warning}

- **Viele private Tracker werden Sie für die Verwendung oder den Zugriff auf sie (d.h. die Verwendung von Jackett oder Prowlarr) über ein VPN sperren.**

### Verwendung eines VPNs

- Wenn ein VPN erforderlich ist und Docker verwendet wird, wird empfohlen, die Download-Client + VPN-Container von Hotio oder Binhex zu verwenden.
- Wenn ein VPN erforderlich ist und Docker nicht verwendet wird, muss Ihr VPN-Client ***Split-Tunneling*** unterstützen, damit nur die erforderlichen (Download-Client-)Apps hinter dem VPN liegen.
- Viele Probleme beim Zugriff auf Tracker können behoben werden, indem Sie die DNS-Server von Google oder Cloudflare anstelle der DNS-Server Ihres Internetdienstanbieters verwenden.
- In einigen Fällen (z.B. bei britischen Internetdienstanbietern) müssen Sie Ihren Torrent-Download-Client möglicherweise hinter einem VPN und Jackett/Prowlarr wie folgt platzieren:
  - Setzen Sie Jackett hinter das VPN und stellen Sie sicher, dass das Split-Tunneling den lokalen Zugriff zulässt.
  - Konfigurieren Sie für Prowlarr Ihren VPN-Client so, dass er einen Proxy bereitstellt, und fügen Sie den Proxy in den Einstellungen => Indexers hinzu. Geben Sie dem Proxy einen Tag und verwenden Sie den gleichen Tag für alle Indexer, die ihn verwenden müssen.
    - Wenn dies unbedingt erforderlich ist und Ihr VPN keine Möglichkeit bietet, einen Proxy zu erstellen, können Sie Prowlarr hinter das VPN setzen und sicherstellen, dass das Split-Tunneling den lokalen Zugriff zulässt.

## Jacketts /all-Endpunkt

{#jackett-all-endpoint}

- Der Jackett-/all-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ können Sie die Alternative zu Jackett & NZBHydra2, [Prowlarr](/prowlarr), in Betracht ziehen.
- **Update vom 20. Januar 2022: Der Jackett-/all-Endpunkt wird ab Version 0.1.0.1188 nicht mehr unterstützt (Warnungen werden angezeigt), da er nur Probleme verursacht.**
- Der Jackett-/all-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Selbst die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des /all-Endpunkts hat keine Vorteile, nur Nachteile:
  - Sie verlieren die Kontrolle über indexer-spezifische Einstellungen (Kategorien, Suchmodi usw.).
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen.
  - Indexer-spezifische Kategorien (\>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis.
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt.
  - Wenn einer der Tracker in /all einen Fehler zurückgibt, deaktiviert \*Arr ihn und Sie erhalten keine Ergebnisse mehr.

### Lösungen für Jackett /all

- Fügen Sie jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu.
- Schauen Sie sich [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schauen Sie sich [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwenden Sie jedoch nicht deren einzelnen aggregierten Endpunkt, sondern verwenden Sie `multi`, wenn eine Synchronisierung verwendet wird.

## Warum gibt es zwei Dateien? | Warum bleibt eine Datei im Download-Ordner?

Das ist normal. Bei einer Konfiguration, die [Hardlinks](https://trash-guides.info/hardlinks) unterstützt, wird kein doppelter Speicherplatz verwendet. Nachfolgend wird erläutert, wie der Torrent-Prozess funktioniert.

1. Readarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben. Beispiele: Filme, TV, Serien, Musik usw.
1. Readarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
1. Abgeschlossene Dateien werden an ihrem ursprünglichen Speicherort belassen, um Ihnen das Seeden der Datei zu ermöglichen (Verhältnis oder Zeit können im Download-Client oder innerhalb des spezifischen Download-Clients angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, wird die Datei per Hardlink verknüpft, wenn dies von Ihrer Konfiguration unterstützt wird, oder kopiert, wenn Hardlinks nicht unterstützt werden.
1. Wenn die Option "Abgeschlossene Download-Verarbeitung - Abgeschlossene entfernen" in den Einstellungen von Readarr aktiviert ist, löscht Readarr die Originaldatei und den Torrent aus Ihrem Download-Client, aber nur, wenn der Download-Client meldet, dass das Seeden abgeschlossen ist und der Torrent gestoppt ist.

> Hardlinks sind standardmäßig aktiviert. [Ein Hardlink verbraucht keinen zusätzlichen Festplattenspeicher.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für Ihr abgeschlossenes Download-Verzeichnis und Ihre Medienbibliothek identisch sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihre Konfiguration keine Hardlinks unterstützt, wird auf die Dateikopie zurückgegriffen.
{.is-info}

## Calibre meldet "Calibre rejected duplicate book", obwohl es keins ist

Wenn Sie die Calibre-Integration verwenden, wird Calibre gelegentlich ein Buch ablehnen und sagen, dass es ein Duplikat ist. Es handelt sich wahrscheinlich nicht tatsächlich um ein Duplikat. Wenn dies passiert, kann Readarr nicht viel tun, und Sie müssen dieses Buch nicht überwachen, um zu verhindern, dass Readarr weiterhin versucht, es abzurufen und an Calibre zu senden. Dies ist nur einer der lustigen Nachteile der Calibre-Integration.