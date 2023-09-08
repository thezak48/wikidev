# Readarr-Einstellungen

## Inhaltsverzeichnis

- [Menüoptionen](#menüoptionen)
- [Medienverwaltung](#medienverwaltung)
  - [Stammordner](#stammordner)
    - [Stammordnereinstellungen](#stammordnereinstellungen)
  - [Remote-Pfadzuordnungen](#remote-pfadzuordnungen)
  - [Buchdateibenennung](#buchdateibenennung)
  - [Buchbenennung](#buchbenennung)
    - [Standard-Buchformat](#standard-buchformat)
    - [Autor](#autor)
    - [Buch](#buch)
    - [Veröffentlichungsdatum](#veröffentlichungsdatum)
    - [Qualität](#qualität)
    - [Medieninformationen](#medieninformationen)
    - [Sonstiges](#sonstiges)
    - [Original](#original)
  - [Autorenordnerformat](#autorenordnerformat)
    - [Autor](#autor-1)
  - [Ordner](#ordner)
  - [Importieren](#importieren)
  - [Dateiverwaltung](#dateiverwaltung)
- [Berechtigungen](#berechtigungen)
- [Profile](#profile)
  - [Qualitätsprofile](#qualitätsprofile)
  - [Metadatenprofile](#metadatenprofile)
  - [Veröffentlichungsprofile](#veröffentlichungsprofile)
  - [Verzögerungsprofile](#verzögerungsprofile)
    - [Verwendung](#verwendung)
    - [Funktionsweise der Verzögerungsprofile](#funktionsweise-der-verzögerungsprofile)
      - [Beispiele](#beispiele)
        - [Beispiel 1](#beispiel-1)
        - [Beispiel 2](#beispiel-2)
        - [Beispiel 3](#beispiel-3)
- [Qualität](#qualität-1)
  - [Bedeutung der Qualitätsangaben](#bedeutung-der-qualitätsangaben)
  - [Definierte Qualitäten](#definierte-qualitäten)
- [Indexer](#indexer)
  - [Unterstützte Indexer](#unterstützte-indexer)
    - [Indexereinstellungen](#indexereinstellungen)
    - [Usenet-Indexer-Konfiguration](#usenet-indexer-konfiguration)
    - [Torrent-Tracker-Konfiguration](#torrent-tracker-konfiguration)
  - [Optionen](#optionen)
- [Download-Clients](#download-clients)
  - [Übersicht](#übersicht)
  - [Prozesse des Download-Clients](#prozesse-des-download-clients)
    - [Usenet-Prozess](#usenet-prozess)
    - [Torrent-Prozess](#torrent-prozess)
  - [Download-Clients](#download-clients-1)
    - [Unterstützte Download-Clients](#unterstützte-download-clients)
    - [Usenet-Client-Einstellungen](#usenet-client-einstellungen)
    - [Torrent-Client-Einstellungen](#torrent-client-einstellungen)
    - [Kompatibilität der Torrent-Client-Entfernung von Downloads](#kompatibilität-der-torrent-client-entfernung-von-downloads)
  - [Behandlung abgeschlossener Downloads](#behandlung-abgeschlossener-downloads)
    - [Abgeschlossene Downloads entfernen](#abgeschlossene-downloads-entfernen)
    - [Behandlung fehlgeschlagener Downloads](#behandlung-fehlgeschlagener-downloads)
  - [Remote-Pfadzuordnungen](#remote-pfadzuordnungen-1)
- [Importlisten](#importlisten)
  - [Importlisten](#importlisten-1)
  - [Importlistenausschlüsse](#importlistenausschlüsse)
  - [Hinzufügen einer Importliste](#hinzufügen-einer-importliste)
- [Verbinden](#verbinden)
  - [Verbindungen](#verbindungen)
  - [Verbindungsauslöser](#verbindungsauslöser)
- [Metadaten](#metadaten)
  - [Calibre-Metadaten](#calibre-metadaten)
  - [Metadaten in Audiodateien schreiben](#metadaten-in-audiodateien-schreiben)
- [Tags](#tags)
- [Allgemein](#allgemein)
  - [Host](#host)
  - [Sicherheit](#sicherheit)
  - [Proxy](#proxy)
  - [Protokollierung](#protokollierung)
  - [Analytik](#analytik)
  - [Updates](#updates)
  - [Updates](#updates-1)
  - [Backups](#backups)
- [Benutzeroberfläche (UI)](#benutzeroberfläche-ui)
  - [Kalender](#kalender)
  - [Daten](#daten)
  - [Stil](#stil)
  - [Sprache](#sprache)

Diese Seite erläutert alle verfügbaren Einstellungen in Readarr und wie sie funktionieren. Dies soll jedoch keine umfassende Anleitung zur Einrichtung von Readarr sein. Wenn Sie das möchten, verwenden Sie bitte die Seite [Schnellstart](/readarr/quick-start-guide).

## Menüoptionen

Um zur Einstellungsseite zu gelangen, wählen Sie bitte "Einstellungen" im linken Menü aus. Die folgenden Untermenüoptionen stehen zur Verfügung:

![settings_1_menu.png](/assets/readarr/settings_1_menu.png)

Beachten Sie auch, dass für jede einzelne Einstellungsseite einige Optionen oben im Menü verfügbar sind:

![settings_2_topmenu.png](/assets/readarr/settings_2_topmenu.png)

- "Erweitert ausblenden/zeigen" ist wichtig für alle Elemente, die unten als "(Erweiterte Option)" gekennzeichnet sind, da sie sonst nicht angezeigt werden. Diese Menüpunkte werden in den Screenshots orange angezeigt.

- Sie müssen Ihre Änderungen speichern, bevor Sie den Bildschirm verlassen. Klicken Sie dazu auf das Diskettensymbol. Wenn Sie keine Änderungen vorgenommen haben, wird "Keine Änderungen" angezeigt und ausgegraut, wie oben gezeigt.

## Medienverwaltung

> Einige dieser Einstellungen sind nur sichtbar, wenn "Erweiterte Einstellungen anzeigen" aktiviert ist, das sich in der oberen Leiste unter der Suchleiste befindet{.is-info}

### Stammordner

- Eine Liste Ihrer konfigurierten Stammordner (Bibliotheksordner) wird angezeigt.
- Klicken Sie auf die Schaltfläche <kb>+</kb>, um einen neuen Stammordner hinzuzufügen, oder klicken Sie auf die Karte eines vorhandenen Ordners, um ihn zu bearbeiten.

#### Stammordnereinstellungen

- Name - Der Name des Stammordners für UI-Zwecke
- Pfad - Der Ordner, der Ihre Buchbibliothek enthält, d.h. das endgültige Ziel, wie es von Readarr gesehen wird.
  - Beachten Sie, dass dieser sich vom Speicherort unterscheiden muss, an dem Ihr Download-Client Dateien ablegt.
  - Wenn Sie Docker und Calibre-Integration verwenden, müssen die Mounts mit Ihrem Bücherordner übereinstimmen.

{#calibre}

- Calibre-spezifische Einstellungen (Nur wenn "Calibre verwenden" aktiviert ist)
  - Calibre verwenden - Aktivieren/Deaktivieren der Verwendung des Calibre Content Servers zur Verwaltung Ihres Stammordners.

> \* Beachten Sie, dass dies **nicht für einen vorhandenen Stammordner aktiviert werden kann**.
> \* Beachten Sie, dass dies **für einen vorhandenen Calibre-aktivierten Stammordner nicht deaktiviert werden kann**.
> \* Beachten Sie, dass dies **Calibre Content Server** erfordert und nicht mit Calibre Web oder Calibre funktioniert.
> \* Beachten Sie, dass Hardlinks nicht mit der Calibre-Integration funktionieren.
> \* Beachten Sie, dass dies erfordert, dass Calibre "Benutzername und Passwort zum Zugriff auf den Inhalte-Server erforderlich" aktiviert hat.
> \* Wenn "Benutzername und Passwort zum Zugriff auf den Inhalte-Server erforderlich" in Calibre nicht aktiviert ist, wird ein Fehler "Anonyme Benutzer dürfen keine Änderungen vornehmen" angezeigt.
{.is-warning}

- Calibre-Host - Die IP/Domäne des Hosts des Calibre Content Servers
- Calibre-Port - Der Port, auf dem der Calibre Content Server lauscht
- (Erweitert) Calibre-URL-Basis - Fügen Sie einen Präfix zur Calibre-URL hinzu, z.B. `http://[host]:[port]/[urlBase]`
- Calibre-Benutzername - Benutzername zum Zugriff auf den Calibre Content Server
- Calibre-Passwort - Passwort zum Zugriff auf den Calibre Content Server
- Calibre-Bibliothek - Name der Calibre Content Server-Bibliothek. Lassen Sie dies leer für die Standardeinstellung.
- In Format konvertieren - (Optional) Fordern Sie den Calibre Content Server auf, in andere Formate zu konvertieren, mit einer durch Kommas getrennten Liste.
  - Überprüfen Sie das (i)-Symbol in der App für eine aktuelle Liste der Optionen.
  - Optionen sind: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-Ausgabeprofil - Wählen Sie das Ausgabeprofil des Calibre Content Servers aus, das verwendet werden soll.
  - Das Ausgabeprofil gibt dem Konvertierungssystem des Calibre Content Servers an, wie das erstellte Dokument für das angegebene Gerät optimiert werden soll (z.B. durch Anpassung der Bildgröße an die Bildschirmgröße des Geräts). In einigen Fällen kann ein Ausgabeprofil verwendet werden, um die Ausgabe für ein bestimmtes Gerät zu optimieren, dies ist jedoch selten erforderlich.
- SSL verwenden - Aktivieren oder Deaktivieren der Verwendung von SSL (HTTPS) für den Calibre Content Server
- Überwachen - Konfigurieren Sie Ihre Überwachungsoptionen für in diesem Ordner erkannte Bücher
  - Alle Bücher - Alle Bücher überwachen
  - Zukünftige Bücher - Bücher überwachen, die noch nicht veröffentlicht wurden
  - Fehlende Bücher - Bücher überwachen, die keine Dateien haben oder noch nicht veröffentlicht wurden
  - Vorhandene Bücher - Bücher überwachen, die Dateien haben oder noch nicht veröffentlicht wurden
  - Erstes Buch - Nur das erste Buch überwachen. Alle anderen Bücher werden ignoriert.
  - Neuestes Buch - Das neueste Buch und zukünftige Bücher überwachen
  - Keine - Es werden keine Bücher überwacht, es sei denn, sie werden explizit hinzugefügt
- Qualitätsprofil - Standard-Qualitätsprofil für Bücher und Autoren, die in diesem Ordner erkannt werden
- Metadatenprofil - Wählen Sie das Metadatenprofil aus, das für in diesem Ordner erkannte Autoren verwendet werden soll. Wählen Sie "Keine", um nur Bücher zu laden, die explizit hinzugefügt oder erkannt wurden.
- Standard-Readarr-Tags - Standard-Tags für in diesem Ordner erkannte Autoren

> Benutzer von Nicht-Windows-Systemen:
> \* Wenn Sie ein NFS-Mount verwenden, stellen Sie sicher, dass "nolock" aktiviert ist.
> \* Wenn Sie ein SMB-Mount verwenden, stellen Sie sicher, dass "nobrl" aktiviert ist.
{.is-warning}

### Remote-Pfadzuordnungen

- Die Remote-Pfadzuordnung fungiert als einfache Suche nach Remote-Pfad und Ersetzung durch lokalen Pfad. Dies wird hauptsächlich für zusammengeführte lokale/Remote-Setups mit mergerfs oder ähnlichem verwendet oder wenn die Anwendung und der Download-Client oder Calibre nicht auf demselben Server sind.
- Weitere Informationen finden Sie im Abschnitt [Download-Clients => Remote-Pfadzuordnung](#remote-pfadzuordnungen-1) ersetzen Sie `<Download-Client>` durch `<Calibre>`

### Buchdateibenennung

![bookfilenaming.png](/assets/readarr/bookfilenaming.png)

**Wenn Sie die Calibre-Integration verwenden, können Sie den Dateinamen des Buches nicht festlegen. Calibre kümmert sich darum. Sie sollten diese Einstellungen nur ändern, wenn Sie Calibre nicht verwenden.**

> Bitte beachten Sie, dass während Readarr sich in der Beta-Phase befindet, wenn Sie Calibre verwenden, wird empfohlen, die Umbenennung in Readarr zu deaktivieren, nur für den Fall, dass ein unbeabsichtigter Fehler durchrutscht. {.is-info}

Häufig verwendete Benennungsschemata sind:

- Standard-Buchformat
  - `{Buchtitel}\{Autorname}` - `{Buchtitel}`, was dann einen Ordner mit dem Namen `Cujo` und ein Unterverzeichnis mit einer Datei mit dem Namen `Stephen King - Cujo.m4b` erzeugen würde.

- Autorenordnerformat
  - `{Autorname}`, was dann `Stephen King` erzeugen würde.

### Buchbenennung

- Bücher umbenennen - Wenn dies deaktiviert ist (kein Häkchen im Kästchen), verwendet Readarr den vorhandenen Dateinamen, wenn die Umbenennung deaktiviert ist.
  - Wenn nicht aktiviert:
    - Import des Download-Clients
      - Der Titel der Veröffentlichung des Download-Clients wird verwendet.
    - Manueller (Ad-hoc-)Import: Originaldateiname

> Wenn Sie "Bücher umbenennen" nicht aktivieren, gelten die folgenden Benennungen nicht - Sie haben Readarr mitgeteilt, dass Sie keine Umbenennung wünschen. Das Buch wird direkt in den Autorenordner importiert.
{.is-info}

> Dies gilt nicht, wenn Calibre verwendet wird, da Calibre die Datei-/Ordnerbenennung mit seinem eigenen internen Schema handhabt.
{.is-info}

- Ungültige Zeichen ersetzen - Wenn dies deaktiviert ist, entfernt Readarr ungültige Zeichen. Wenn es aktiviert ist, ersetzt Readarr ungültige Zeichen. Beispiele für ungültige Zeichen sind `\ # / $ * < >` und mehr.

### Standard-Buchformat

- Wählen Sie die Benennung aus

- Dropdown-Box (obere rechte Ecke)
  - Linke Box - Behandlung von Leerzeichen
    - `Leerzeichen ( )` - Leerzeichen in der Benennung verwenden (Standard)
    - `Punkt (.)` - Punkte anstelle von Leerzeichen in der Benennung verwenden
    - `Unterstrich (_)` - Unterstriche anstelle von Leerzeichen in der Benennung verwenden
    - `Bindestrich (-)` - Bindestriche anstelle von Leerzeichen in der Benennung verwenden
  - Rechte Box - Behandlung der Groß-/Kleinschreibung
    - `Standard-Groß-/Kleinschreibung` - Titel groß- und kleinschreiben (~Camel-Case) (Standard)
    - `Großbuchstaben` - Titel komplett in Großbuchstaben
    - `Kleinbuchstaben` - Titel komplett in Kleinbuchstaben

### Autor

- `{Autorname}` = Name des Autors
- `{AutornameThe}` = Name des Autors, The
- `{AutorCleanName}` = Name des Autors
- `{AutorSortName}` = Name, Autor
- `{AutorDisambiguation}` = Autorname (Disambiguierung, die von GoodReads für mehrere Autoren mit demselben Namen verwendet wird)

### Buch

- `{Buchtitel}` = Titel des Buches!: Untertitel!
- `{BuchtitelThe}` = Titel des Buches!, The: Untertitel!
- `{BuchCleanTitle}` = Titel des Buches: Untertitel
- `{BuchTitelNoSub}` = Titel des Buches!
- `{BuchTitelTheNoSub}` = Titel des Buches!, The
- `{BuchCleanTitleNoSub}` = Titel des Buches
- `{BuchUntertitel}` = Untertitel!
- `{BuchUntertitelThe}` = Untertitel!, The
- `{BuchCleanSubtitle}` = Untertitel
- `{BuchDisambiguation}` = Buchname! (Disambiguierungstitel, der von GoodReads verwendet wird)
- `{BuchSerie}` = Serientitel
- `{BuchSeriePosition}` = 1
- `{BuchSerieTitle}` = Serientitel #1
- `{PartNumber:0}` oder `{PartNumber:0}` = 2
- `{PartNumber:00}` = 02
- `{PartCount}` oder `{PartCount:0} = 9
- `{PartCount:00}` = 09

### Veröffentlichungsdatum

- `{Veröffentlichungsjahr}` = 2016
- `{VeröffentlichungsjahrFirst}` = 2015
- `{Editionsjahr}` = 2016

### Qualität

- `{Qualität Voll}` = AZW3 Proper
- `{Qualität Titel}` = AZW3

### Medieninformationen

- `{MediaInfo AudioCodec}` = MP3
- `{MediaInfo AudioChannels}` = 2.0
- `{MediaInfo AudioBitRate}` = 320kbps
- `{MediaInfo AudioBitsPerSample}` = 24bit
- `{MediaInfo AudioSampleRate}` = 44.1kHz

### Sonstiges

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL

### Original

- `{Originaler Titel}` = Autor.Name.Buch.Name.2018.AZW3-EVOLVE
- `{Originaler Dateiname}` = 01-Buchname

> Der Originaldateiname wird nicht empfohlen. Es handelt sich um den wörtlichen Originaldateinamen und kann obfuscated t1i0p3s7i8yuti sein. Verwenden Sie stattdessen den Originaltitel.
{.is-info}
  
## Autorenordnerformat

- (Erweiterte Option) Hier legen Sie die Benennungskonvention für den Autorenordnernamen fest.

> Dies gilt nicht, wenn Calibre verwendet wird, da Calibre die Datei-/Ordnerbenennung mit seinem eigenen internen Schema handhabt.
{.is-info}

### Autor

- `{Autorname}` = Name des Autors
- `{AutornameThe}` = Name des Autors, The
- `{AutorCleanName}` = Name des Autors
- `{AutorSortName}` = Name, Autor
- `{AutorDisambiguation}` = Autorname (Disambiguierung, die von GoodReads für mehrere Autoren mit demselben Namen verwendet wird)

## Ordner

![mm_folders.png](/assets/readarr/mm_folders.png)
  
- (Erweiterte Option) Leere Autorenordner erstellen - Aktivieren Sie das Kästchen, um leere Autorenordner zu erstellen, wenn ein neuer Autor hinzugefügt wird.
- (Erweiterte Option) Leere Autorenordner löschen - Aktivieren Sie das Kästchen, um leere Autorenordner zu löschen, wenn sich keine Bücher darin befinden.
  
> Eines dieser Kästchen kann aktiviert sein, aber sie sollten NICHT BEIDE aktiviert sein. {.is-warning}

> Dies gilt nicht, wenn Calibre verwendet wird, da Calibre die Datei-/Ordnerbenennung mit seinem eigenen internen Schema handhabt.
{.is-info}

## Importieren
  
![mm_importing.png](/assets/readarr/mm_importing.png)
  
- (Erweiterte Option) Freien Speicherplatz überprüfen überspringen - Wenn aktiviert, wird vor dem Importieren der freie Speicherplatz nicht überprüft.
- (Erweiterte Option) Mindestens freier Speicherplatz - Geben Sie den minimalen freien Speicherplatz für das Laufwerk ein, bevor der Importvorgang gestoppt wird.
- (Erweiterte Option) Verwenden von Hardlinks anstelle von Kopien - Aktivieren Sie dieses Kontrollkästchen, um Hardlinks anstelle von Kopien zu verwenden (für Torrents). Beachten Sie, dass dies standardmäßig aktiviert ist.
  
> Sie sollten dies möglichst verwenden. Damit Hardlinks verwendet werden können, müssen sich Quelle/Ziel auf demselben Dateisystem (Laufwerk, Partition) und denselben Einhängepunkten befinden. [Weitere Informationen finden Sie in TRaSH's Hardlink Guide](https://trash-guides.info/hardlinks/)
  
- Zusätzliche Dateien importieren - Wenn aktiviert, werden beim Importieren angegebene zusätzliche Dateien importiert, die sich im Ordner des Buches befinden.
- (Erweiterte Option) Zusätzliche Dateien importieren - Wenn "Zusätzliche Dateien importieren" aktiviert ist, geben Sie eine durch Kommas getrennte Liste von Erweiterungen ein, die importiert werden sollen.

> Wenn Sie Readarr für Hörbücher verwenden, sollten Sie .cue zu dieser Liste hinzufügen, da es Ihre Kapitelinformationen enthält!
{.is-info}
  
## Dateiverwaltung
  
  ![mm_filemgmt.png](/assets/readarr/mm_filemgmt.png)

- Gelöschte Bücher ignorieren - Aktivieren Sie dieses Kontrollkästchen, um Bücher zu überwachen, die als gelöscht oder nicht zugänglich erkannt wurden, und sich im Stammordner von Readarr befinden.
- Korrekte und Repacks herunterladen - Ob automatisch auf Propers/Repacks aktualisiert werden soll. Verwenden Sie "Nicht bevorzugen", um nach bevorzugten Wörtern zu sortieren, anstatt nach Propers/Repacks.
  - Bevorzugen und Aktualisieren - Repacks und Propers höher als Nicht-Repacks und Nicht-Propers einstufen. Neue Repacks und Propers als Upgrade für aktuelle Versionen behandeln.
  - Nicht automatisch aktualisieren - Repacks und Propers höher als Nicht-Repacks und Nicht-Propers einstufen. Neue Repacks und Propers nicht als Upgrade für aktuelle Versionen behandeln.
  - Nicht bevorzugen - Repacks und Propers effektiv ignorieren. Sie müssen jegliche Präferenz für diese mit [Bevorzugten Wörtern](#release-profiles) verwalten.
  
> \* `PROPER` - bedeutet, dass es ein Problem mit der vorherigen Version gab. Downloads, die als PROPER gekennzeichnet sind, zeigen an, dass die Probleme in dieser Version behoben wurden. Dies wird von einer Gruppe durchgeführt, die die Originalversion nicht veröffentlicht hat.
> \* `REPACK` - bedeutet, dass es ein Problem mit der vorherigen Version gab und dass es von der Originalgruppe korrigiert wurde. Downloads, die als REPACK gekennzeichnet sind, zeigen an, dass die Probleme in dieser Version behoben wurden. Dies wird von einer Gruppe durchgeführt, die die Originalversion veröffentlicht hat.
{.is-info}

- (Erweiterte Option) Überwachen der Stammordner auf Dateiänderungen - Aktivieren Sie dieses Kontrollkästchen, um einen erneuten Scan auszulösen, wenn festgestellt wird, dass sich im Stammordner Änderungen ergeben haben.
- (Erweiterte Option) Autorordner nach Aktualisierung erneut scannen - Wählen Sie aus, wann ein Autorordner nach Aktualisierung des Autors erneut gescannt werden soll.
  - Immer - Dadurch werden Autorordner basierend auf dem Aufgabenplan erneut gescannt.
  - Nach manueller Aktualisierung - Sie müssen den Datenträger manuell erneut scannen.
  - Nie - Wie der Name schon sagt, Autorordner nie erneut scannen.
- (Erweiterte Option) Fingerprinting zulassen - Wählen Sie aus, wie Fingerprinting gehandhabt werden soll, um eine genauere Buchzuordnung zu ermöglichen, auf Kosten von CPU-/Festplattenzeit.
  - Immer - Fingerprinting immer verwenden, wenn möglich
  - Nur für neue Importe - Nur neu importierte Versionen fingerprinten
  - Nie - Wie der Name schon sagt, Fingerprinting nie verwenden
- (Erweiterte Option) Dateidatum ändern - Dateidatum beim Importieren/Neuscannen ändern
  - Keine - Readarr ändert das Datum nicht, das in Ihrem Dateibrowser angezeigt wird
  - Buchveröffentlichungsdatum - Das Datum, an dem das Buch veröffentlicht wurde.
- (Erweiterte Option) Papierkorb - Buchdateien werden hier abgelegt, wenn sie gelöscht werden, anstatt dauerhaft gelöscht zu werden
- (Erweiterte Option) Papierkorb bereinigen - So alt kann eine bestimmte Datei sein, bevor sie dauerhaft gelöscht wird

> Es wird dringend empfohlen, einen Papierkorb zu verwenden. Es ist einfach, Dateien zu löschen, und die Wiederherstellung ist einfach, wenn Sie den Papierkorb verwenden.
{.is-warning}

# Berechtigungen

- Berechtigungen festlegen - Soll `chmod` ausgeführt werden, wenn Dateien importiert/umbenannt werden?
  - Ordner berechtigen - Oktal, wird während des Imports/Umbenennens auf Medienordner und -dateien angewendet (ohne Ausführungsbits)

> Die Dropdown-Box enthält eine voreingestellte Liste sehr häufig verwendeter Berechtigungen, die verwendet werden können. Sie können jedoch auch manuell eine Ordneroktalzahl eingeben, wenn Sie möchten.
{.is-info}

> Dies funktioniert nur, wenn der Benutzer, der `Readarr` ausführt, der Eigentümer der Datei ist. Es ist besser, sicherzustellen, dass der Download-Client die Berechtigungen ordnungsgemäß setzt.
{.is-warning}

- Gruppe ändern - Gruppenname oder GID. Verwenden Sie GID für Remote-Dateisysteme

> Dies funktioniert nur, wenn der Benutzer, der `Readarr` ausführt, der Eigentümer der Datei ist. Es ist besser, sicherzustellen, dass der Download-Client die Berechtigungen ordnungsgemäß setzt.
{.is-warning}

# Profile

## Qualitätsprofile

Qualitätsprofile werden verwendet, um festzulegen, welche Formate von Büchern für ein Buch in Ihrer Bibliothek akzeptabel sind.
  
![qualityprofile.png](/assets/readarr/qualityprofile.png)

- Legen Sie Profile für die Qualität der Bücher fest, die Sie herunterladen möchten.

> Wenn Sie ein vorhandenes Profil auswählen oder ein zusätzliches Profil hinzufügen, wird ein neues Fenster angezeigt.
> Hinweis: Die Qualität, die in einem blauen Kasten angezeigt wird, ist die Qualität, auf die alle Medien mit diesem Profil weiterhin aktualisiert werden.
{.is-info}

- Plus-Symbol (<kb>+</kb>) - Erstellen Sie ein neues Qualitätsprofil

- Name - Geben Sie einen **EINDEUTIGEN** Namen für das Qualitätsprofil ein, das Sie erstellen
- Upgrades zulassen - Wenn diese Option aktiviert ist und Sie Readarr mitteilen, dass ein `EPUB` heruntergeladen werden soll, da es die erste Veröffentlichung eines bestimmten Buches ist, und später jemand in der Lage ist, ein `AZW3` hochzuladen, wird Readarr automatisch auf die bessere Qualität aktualisiert, ***wenn*** `Upgrade Until` diese Qualität ausgewählt hat
  - Bis zur Aktualisierung - Sobald diese Qualität erreicht ist, lädt Readarr keine Bücher mehr herunter

> Hinweis: Dies gilt nur, wenn Sie `AZW3` höher als `EPUB` in der Sektion `Qualities` haben
{.is-warning}

- Qualitäten - Qualitäten, die weiter oben in der Liste stehen, werden unabhängig vom gewünschten (aktivierten/ausgewählten) Status bevorzugt. Qualitäten innerhalb derselben Gruppe sind gleichwertig. Nur aktiviert (ausgewählte) Qualitäten sind gewünscht (zugelassen)
  - Gruppen bearbeiten - Einige Qualitäten sind zu Gruppen zusammengefasst, um die Größe der Liste zu reduzieren und ähnliche Veröffentlichungen zu gruppieren. Ein gutes Beispiel dafür sind `WebDL` und `WebRip`, da diese sehr ähnlich sind und in der Regel ähnliche Bitraten haben. Beim Bearbeiten der Gruppen können Sie die Präferenz innerhalb jeder Gruppe ändern.

  - [Siehe Qualitäten](#qualities-defined)

> Standardmäßig sind die Qualitäten von "schlechtester" (unten) bis "bester" (oben) eingestellt
{.is-info}

## Metadatenprofile

Metadatenprofile werden verwendet, um festzulegen, welche Bücher von GoodReads unter einem Autor hinzugefügt werden sollen, wenn ein neuer Autor hinzugefügt wird.

- Plus-Symbol (<kb>+</kb>) - Erstellen Sie ein neues Metadatenprofil

![metaprofiles.png](/assets/readarr/metaprofiles.png)
  
- Name - Geben Sie einen **EINDEUTIGEN** Namen für das Metadatenprofil ein
- Minimale Beliebtheit - Geben Sie die minimale Beliebtheit an, die ein Buch haben muss, um für einen Autor hinzugefügt zu werden.

> Wenn Sie dies zu hoch einstellen, werden Bücher nicht zu Readarr hinzugefügt, aber wenn Sie es zu niedrig einstellen, werden obskure Veröffentlichungen angezeigt.
{.is-warning}

> Setzen Sie dies genau auf `10000000000`, um ein Profil zu erstellen, das `None` entspricht, aber andere Filterungen von Ausgaben und Büchern zulässt. Beachten Sie, dass `None` keine Metadatenfilter anwendet und Sie möglicherweise ausländische Ausgaben erhalten.
{.is-info}

- Minimale Seitenzahl - Geben Sie die minimale Anzahl von Seiten an, die ein Buch haben muss, um für einen Autor hinzugefügt zu werden.
- Bücher mit fehlendem Veröffentlichungsdatum überspringen - Aktivieren Sie diese Option, um Bücher mit fehlendem Veröffentlichungsdatum zu überspringen.
- Bücher ohne ISBN oder ASIN überspringen - Aktivieren Sie diese Option, um Bücher zu überspringen, die weder eine ISBN noch eine ASIN-Nummer enthalten.
- Teilbücher und Sets überspringen - Aktivieren Sie diese Option, um Teilbücher und Sets zu überspringen.
- Sekundäre Serienbücher überspringen - Aktivieren Sie diese Option, um sekundäre Serienbücher zu überspringen.
- Zulässige Sprachen - Geben Sie eine durch Kommas getrennte Liste von ISO 639-3-Sprachcodes oder 'null' für zulässige Sprachen für Ihre Bücher ein
- Darf nicht enthalten - Geben Sie Wörter oder Phrasen ein, die ein Buchtitel nicht enthalten darf, um hinzugefügt zu werden.
  
> Sie können mehrere Metadatenprofile erstellen und bei Bedarf jeweils ein separates Profil auf jeden Autor anwenden. Sie können jedoch nur ein einziges Metadatenprofil auf einen bestimmten Autor anwenden.
{.is-info}
  
## Veröffentlichungsprofile

Veröffentlichungsprofile werden verwendet, um festzulegen, ob Indexer-Veröffentlichungsnamen für den Download qualifizieren.

![releaseprofiles.png](/assets/readarr/releaseprofiles.png)  
  
- Profil aktivieren - Aktivieren Sie dieses Kontrollkästchen, um dieses Profil zu aktivieren.
- Muss enthalten - Fügen Sie eine Liste von Wörtern oder Phrasen hinzu, die IMMER im Veröffentlichungsnamen enthalten sein müssen, um als gültig betrachtet zu werden.
- Darf nicht enthalten - Fügen Sie eine Liste von Wörtern oder Phrasen hinzu, die NICHT im Veröffentlichungsnamen enthalten sein dürfen, um als gültig betrachtet zu werden.
- Bevorzugt (Wörter) - Hier können Sie Begriffe oder Regex mit Punktzahlen (positiv und negativ) hinzufügen, um sie als mehr oder weniger bevorzugt zu betrachten. Sie können beispielsweise "ungekürzt" mit einer positiven Punktzahl bevorzugen.
  
> Veröffentlichungen mit einer höheren bevorzugten Wortpunktzahl als die vorhandene Datei sind IMMER ein Upgrade!
{.is-info}
  
- Bevorzugte beim Umbenennen einschließen - Aktivieren Sie dieses Kontrollkästchen, um Ihre bevorzugten Wörter (oder Regex-Übereinstimmungen) in der Zuweisung des Dateinamens `{Preferred Words}` einzuschließen.
  
> Sie sollten `{Preferred Words}` in Ihren Dateinamen aufnehmen und dieses Kontrollkästchen aktivieren, wenn Sie sie verwenden, da Sie sonst in einer Download-Schleife landen können.
{.is-warning}

- Indexer - In diesem Dropdown-Menü können Sie dieses Veröffentlichungsprofil auf einen einzelnen Indexer beschränken. Dies sollte fast immer auf `(beliebig)` belassen werden.
- Tags - Geben Sie hier einen Tag ein, um diesen Tag auf Autoren mit demselben Tag anwenden zu können. Wenn Sie hier keinen Tag anwenden, gilt dieses Profil für ALLE Autoren.

## Verzögerungsprofile

- Verzögerungsprofile ermöglichen es Ihnen, die Anzahl der Veröffentlichungen zu reduzieren, die für ein Buch heruntergeladen werden, indem Sie eine Verzögerung hinzufügen, während Readarr weiterhin nach Veröffentlichungen sucht, die besser zu Ihren Präferenzen passen.
- Protokoll - Dies kann entweder `Usenet` oder `Torrent` sein, abhängig von dem bevorzugten Downloadprotokoll
- Usenet-Verzögerung - Festgelegt durch die Anzahl der Minuten, die Sie warten möchten, bevor der Download startet
- Torrent-Verzögerung - Festgelegt durch die Anzahl der Minuten, die Sie warten möchten, bevor der Download startet
- Umgehen, wenn höchste Qualität - Verzögerung umgehen, wenn die Veröffentlichung die höchste aktiviert Qualität mit dem bevorzugten Protokoll hat
- Tags - Durch das Hinzufügen eines Tags zu diesem Verzögerungsprofil können Sie einen bestimmten Film mit den hier festgelegten Regeln versehen.
- Schraubenschlüssel-Symbol - Hiermit können Sie das Verzögerungsprofil bearbeiten
- Plus-Symbol (<kb>+</kb>) - Erstellen Sie ein neues Verzögerungsprofil

### Verwendung

Einige Medien erhalten in den Stunden nach der Veröffentlichung eine halbe Dutzend verschiedene Veröffentlichungen unterschiedlicher Qualität, und ohne Verzögerungsprofile könnte Readarr versuchen, alle herunterzuladen. Mit Verzögerungsprofilen kann Readarr so konfiguriert werden, dass es die ersten paar Stunden der Veröffentlichungen ignoriert.

Verzögerungsprofile sind auch hilfreich, wenn Sie ein Protokoll (Usenet oder BitTorrent) gegenüber dem anderen betonen möchten. (Siehe Beispiel 3)

### Funktionsweise von Verzögerungsprofilen

Der Timer beginnt, sobald Readarr eine Veröffentlichung für ein Buch erkennt. Diese Veröffentlichung wird in Ihrer Warteschlange mit einem Uhrensymbol angezeigt, um anzuzeigen, dass sie einer Verzögerung unterliegt.

> Die Uhr beginnt ab der Zeit, zu der die Veröffentlichung hochgeladen wurde, und nicht ab dem Zeitpunkt, zu dem Readarr sie sieht. {.is-info}

Während des Verzögerungszeitraums werden alle neuen Veröffentlichungen, die verfügbar werden, von Readarr vermerkt. Wenn der Verzögerungstimer abläuft, lädt Readarr die einzelne Veröffentlichung herunter, die am besten zu Ihren Qualitätspräferenzen passt.

Der Timer kann für Usenet und Torrents unterschiedlich sein. Jedes Profil kann mit einem oder mehreren Tags verknüpft werden, um Ihnen die Anpassung zu ermöglichen, welche Shows welches Profil haben. Ein Verzögerungsprofil ohne Tag gilt als Standard und gilt für alle Shows, die kein spezifisches Tag haben.

> Verzögerungsprofile beginnen ab dem Zeitstempel, den der Indexer für das Hochladen der Veröffentlichung angibt. Dies bedeutet, dass Inhalte, die älter als die von Ihnen festgelegte Anzahl von Minuten sind, in keiner Weise von Ihrem Verzögerungsprofil beeinflusst werden und sofort heruntergeladen werden. Darüber hinaus ignorieren **alle manuellen Suchen** nach Inhalten (Suchen außerhalb des RSS-Feeds) die Einstellungen des Verzögerungsprofils.
{.is-warning}

#### Beispiele

- Für jedes Beispiel wird angenommen, dass der Benutzer das folgende Qualitätsprofil aktiv hat: EPUB und höher sind erlaubt, MOBI ist die Qualitätsbegrenzung * AZW3 ist die höchstbewertete Qualität

##### Beispiel 1

- In diesem einfachen Beispiel ist das Profil mit einer 120-minütigen (zweistündigen) Verzögerung für Usenet und Torrent festgelegt.

- Um 23:00 Uhr wird die erste Veröffentlichung für ein Buch von Readarr erkannt, und sie wurde um 22:50 Uhr hochgeladen, und der 120-minütige Timer beginnt. Um 0:50 Uhr wertet Readarr alle Veröffentlichungen aus, die es in den letzten zwei Stunden gefunden hat, und lädt die beste herunter, die MOBI ist.

- Um 3:00 Uhr wird eine weitere Veröffentlichung gefunden, die MOBI ist und um 2:46 Uhr zu Ihrem Indexer hinzugefügt wurde. Ein weiterer 120-minütiger Timer beginnt. Um 4:46 Uhr wird die beste verfügbare Veröffentlichung heruntergeladen. Da die Qualitätsbegrenzung jetzt erreicht ist, ist das Buch nicht mehr aktualisierbar, und Readarr sucht nicht mehr nach neuen Veröffentlichungen.

- Zu jedem Zeitpunkt, wenn eine AZW3-Veröffentlichung gefunden wird, wird sie sofort heruntergeladen, da sie die höchstbewertete Qualität ist. Wenn zu diesem Zeitpunkt ein Verzögerungstimer aktiv ist, wird er abgebrochen.

##### Beispiel 2

- In diesem Beispiel gibt es unterschiedliche Timer für Usenet und Torrents. Nehmen Sie einen 120-minütigen Timer für Usenet und einen 180-minütigen Timer für BitTorrent an.

- Um 23:00 Uhr wird die erste Veröffentlichung für ein Buch von Readarr erkannt, und beide Timer beginnen. Die Veröffentlichung wurde um 22:15 Uhr zu Ihrem Indexer hinzugefügt. Um 0:15 Uhr wertet Readarr alle Veröffentlichungen aus, und wenn es akzeptable Usenet-Veröffentlichungen gibt, wird die beste heruntergeladen, und beide Timer enden. Wenn nicht, wartet Readarr bis 0:15 Uhr und lädt die beste Veröffentlichung herunter, unabhängig davon, aus welcher Quelle sie stammt.

##### Beispiel 3

- Eine häufige Verwendung für Verzögerungsprofile besteht darin, ein Protokoll (Usenet oder BitTorrent) gegenüber dem anderen zu betonen. Sie möchten beispielsweise nur eine BitTorrent-Veröffentlichung herunterladen, wenn nach einer bestimmten Zeit nichts auf Usenet hochgeladen wurde.

- Sie könnten einen 60-minütigen Timer für BitTorrent und einen 0-minütigen Timer für Usenet festlegen.

- Wenn die erste Veröffentlichung, die erkannt wird, von Usenet stammt, wird sie sofort heruntergeladen.

- Wenn die erste Veröffentlichung von BitTorrent stammt, setzt Readarr einen 60-minütigen Timer. Wenn während dieses Timers eine qualifizierende Usenet-Veröffentlichung erkannt wird, wird die BitTorrent-Veröffentlichung ignoriert und die Usenet-Veröffentlichung wird heruntergeladen.

# Qualität

![qualitydefinitions.png](/assets/readarr/qualitydefinitions.png)

## Bedeutung der Qualitätstabelle

- Qualität - Der Name der Qualität in der Szene (fest codiert)
- Titel - Der Name der Qualität in der Benutzeroberfläche (konfigurierbar)
- Megabyte pro Minute - Selbst erklärend
- Größenbeschränkung - Selbst erklärend
- Min - Die minimale Anzahl von Bytes oder Kilobytes pro Sekunde (b/s|kb/s), die eine Qualität haben kann.
- Max - Die maximale Anzahl von Bytes oder Kilobytes pro Sekunde (b/s|kb/s), die eine Qualität haben kann.

## Definierte Qualitäten

- Unbekannter Text - Selbst erklärend
- PDF - Portable Document File
- MOBI - Eines der am weitesten verbreiteten eBook-Dateiformate
- EPUB - Ein weiteres der am weitesten verbreiteten eBook-Dateiformate
- AZW3 - AZW3 ist eine eBook-Datei, die von Amazon entwickelt wurde. Sie wird in Amazon Kindles verwendet, um eBooks anzuzeigen.
- Unbekannter Ton - Selbst erklärend
- MP3 - Gängiges verlustbehaftetes Audioformat
- M4B - Gängiges Audiobook-Dateiformat
- FLAC - Free Lossless Audio Codec, ein Audioformat ähnlich wie MP3, aber verlustfrei

- Entfernen Sie abgeschlossene Downloads, wenn sie fertig sind (Usenet) oder gestoppt/abgeschlossen sind (Torrents)

- Readarr sendet eine Download-Anfrage an Ihren Client und ordnet sie einem Label oder einer Kategorie zu, die Sie in den Einstellungen des Download-Clients konfiguriert haben.
- Readarr überwacht die aktiven Downloads Ihres Download-Clients, die diese Kategorie verwenden. Dies geschieht über die API Ihres Download-Clients.
- Wenn der Download abgeschlossen ist, kennt Readarr den endgültigen Speicherort der Datei, wie er von Ihrem Download-Client gemeldet wird. Dieser Speicherort kann fast überall sein, solange er sich an einem separaten Ort von Ihrem Medienordner befindet.
- Readarr durchsucht diesen abgeschlossenen Dateispeicherort nach Videodateien. Es analysiert den Dateinamen des Videos, um ihn mit einem Buch abzugleichen. Wenn dies möglich ist, benennt es die Datei entsprechend Ihren Spezifikationen um und verschiebt sie in den zugewiesenen Bibliotheksordner.
- Übrig gebliebene Dateien aus dem Download werden in den Papierkorb oder in die Recycling-Tonne verschoben.

Wenn Sie einen BitTorrent-Client verwenden, läuft der Prozess etwas anders ab:

- Abgeschlossene Dateien werden an ihrem ursprünglichen Speicherort belassen, um das Seeden zu ermöglichen. Wenn die Dateien in Ihren zugewiesenen Bibliotheksordner importiert werden, versucht Readarr, die Datei per Hardlink zu verknüpfen. Wenn Hardlinks nicht unterstützt werden, wird eine Kopie erstellt (doppelte Speicherplatzbelegung).
- Wenn die Option "Abgeschlossene Download-Verarbeitung - Entfernen" in den Einstellungen aktiviert ist, fordert Readarr den Torrent-Client auf, die Originaldatei und den Torrent zu löschen. Dies geschieht jedoch nur, wenn der Client meldet, dass das Seeden abgeschlossen ist, der Torrent sich in derselben Kategorie befindet (d. h. keine Verwendung einer nach dem Import erstellten Kategorie), das von Readarr unterstützte Seed-Ziel erreicht wurde und der Torrent pausiert (gestoppt) ist.

### Verarbeitung fehlgeschlagener Downloads

- Die Verarbeitung fehlgeschlagener Downloads ist nur mit SABnzbd und NZBGet kompatibel.
- Die Verarbeitung fehlgeschlagener Downloads gilt nicht für Torrents, und es gibt keine Pläne, eine solche Funktionalität hinzuzufügen.

- Es gibt mehrere Komponenten, die den Prozess der Verarbeitung fehlgeschlagener Downloads ausmachen:

- Überprüfung des Downloaders:
  - Warteschlange - Überprüfen Sie die Warteschlange Ihres Downloaders auf passwortgeschützte (verschlüsselte) Releases, die als fehlgeschlagen markiert sind
  - Verlauf - Überprüfen Sie den Verlauf Ihres Downloaders auf Fehler (z. B. nicht genügend Reparaturmöglichkeiten oder fehlgeschlagene Extraktion)
- Wenn Readarr einen fehlgeschlagenen Download findet, beginnt es mit der Verarbeitung und führt einige Aktionen aus:
  - Fügt ein fehlgeschlagenes Ereignis zum Verlauf von Readarr hinzu
  - Entfernt den fehlgeschlagenen Download aus dem Download-Client, um Speicherplatz freizugeben und heruntergeladene Dateien zu löschen (optional)
  - Beginnt mit der Suche nach einer Ersatzdatei (optional)
  - Blocklisting (früher "Blacklisting") ermöglicht das automatische Überspringen von NZBs, wenn sie fehlschlagen. Das bedeutet, dass das NZB von Readarr nie automatisch erneut heruntergeladen wird (Sie können den Download jedoch weiterhin über eine manuelle Suche erzwingen).
  - Es gibt 2 erweiterte Optionen (auf der Seite "Download-Client" in den Einstellungen), die das Verhalten des fehlgeschlagenen Downloads in Readarr steuern. Derzeit sind sie alle standardmäßig aktiviert.

- Erneut herunterladen - Steuert, ob Readarr nach einem Fehler nach derselben Datei sucht
- (Erweiterte Option) Entfernen - Gibt an, ob der Download automatisch aus dem Download-Client entfernt werden soll, wenn der Fehler erkannt wird

## Remote-Pfadzuordnungen

- Remote-Pfadzuordnungen dienen als einfache Suche nach Remote-Pfad und Ersetzung durch lokalen Pfad. Dies wird hauptsächlich für zusammengeführte lokale/Remote-Setups mit MergerFS oder ähnlichem verwendet oder wenn die Anwendung und der Download-Client nicht auf demselben Server ausgeführt werden.
- Eine Remote-Pfadzuordnung wird verwendet, wenn Ihr Download-Client einen Pfad für abgeschlossene Daten meldet, entweder auf einem anderen Server oder auf eine Weise, die von \*Arr nicht für diesen Ordner berücksichtigt wird.
- Im Allgemeinen ist eine Remote-Pfadzuordnung nur erforderlich, wenn Ihr Download-Client auf Linux läuft, während \*Arr auf Windows oder umgekehrt läuft. Eine Remote-Pfadzuordnung ist möglicherweise auch erforderlich, wenn Docker- und Native-Clients gemischt werden oder wenn ein Remote-Server verwendet wird.
- Eine Remote-Pfadzuordnung ist eine einfache Suche/Ersetzung (wo der REMOTE-Wert gefunden wird, wird er durch den LOCAL-Wert für den angegebenen Host ersetzt).
- Wenn die Fehlermeldung über einen ungültigen Pfad den ERSETZTEN Wert nicht enthält, funktioniert die Pfadzuordnung nicht wie erwartet. Die übliche Lösung besteht darin, die Zuordnung hinzuzufügen und zu entfernen.
- [Weitere Informationen zur Remote-Pfadzuordnung finden Sie in TRaSH's Tutorial](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Wenn sowohl \*Arr als auch Ihr Download-Client Docker-Container sind, ist eine Remote-Pfadzuordnung selten erforderlich. Es wird empfohlen, [den Docker-Leitfaden](/docker-guide) zu lesen und/oder [TRaSH's Tutorial](https://trash-guides.info/hardlinks) zu folgen.
{.is-info}

# Import-Listen

> Informationen zu unterstützten Listentypen finden Sie auf der Seite [Weitere Informationen (Unterstützt)](/readarr/supported#lists) für diesen Abschnitt
{.is-info}

Mit Import-Listen können Sie Elemente automatisch von Ihren GoodReads-Regalen oder von anderen Benutzern zu Readarr hinzufügen. Dies kann viele unerwartete Elemente zu Ihrer Readarr-Datenbank hinzufügen, daher verwenden Sie es bitte mit Vorsicht.

![importlists.png](/assets/readarr/importlists.png)

## Import-Listen

Hier sehen Sie die Listen, die Sie derzeit haben, und können neue Listen hinzufügen. Das Hinzufügen von Listen wird weiter unten detaillierter erläutert.

## Import-Listenausschlüsse

Alles, was hier aufgeführt ist, wurde von der Hinzufügung durch Listen ausgeschlossen und wird niemals von einer Liste hinzugefügt. Sie können Elemente durch Anklicken daraus entfernen.

## Hinzufügen einer Import-Liste

Nach dem Klicken auf das <kb>+</kb> wählen Sie aus, welche Art von Liste Sie hinzufügen möchten:

![addlist.png](/assets/readarr/addlist.png)

In diesem Fall fügen wir eine GoodReads-Bücherregal-Liste hinzu.

![bookshelflist.png](/assets/readarr/bookshelflist.png)

- Name - Geben Sie einen Namen für diese Liste ein.
- Automatisches Hinzufügen aktivieren - Wenn aktiviert, werden alle Elemente in der Liste automatisch zu Readarr hinzugefügt.

> Dadurch werden alle Autoren und ALLE BÜCHER dieses Autors zu Readarr hinzugefügt!

- Überwachen - Wählen Sie Ihren Überwachungsgrad für hinzugefügte Elemente aus. Gültige Optionen sind `Keine`, `Ausgewähltes Buch` und `Alle Bücher des Autors`. Alle Bücher werden zu Readarr hinzugefügt, aber je nach Auswahl überwacht oder nicht überwacht.
- Nach neuen Elementen suchen - Wenn aktiviert, initiiert Readarr eine Suche nach fehlenden überwachten Elementen, wenn sie von einer Liste hinzugefügt werden. Wenn Sie viele Autoren/überwachte Bücher hinzufügen, kann dies Ihr System überlasten!
- Stammordner - Wählen Sie den Stammordner für Autoren aus, die von dieser Liste hinzugefügt werden
- Qualitätsprofil - Wählen Sie Ihr Qualitätsprofil für Autoren aus, die von dieser Liste hinzugefügt werden
- Metadatenprofil - Wählen Sie Ihr Metadatenprofil für Autoren aus, die von dieser Liste hinzugefügt werden
- Readarr-Tags - Wählen Sie die Tags aus, die für Autoren gelten, die von dieser Liste hinzugefügt werden

> Es wird dringend empfohlen, hier einen aussagekräftigen Tag hinzuzufügen. Andernfalls wissen Sie nicht, welche Liste diese Elemente zu Readarr hinzugefügt hat, und sobald sie hinzugefügt sind, können Sie diese Informationen nie wieder abrufen! Diese Informationen werden nicht protokolliert!

Standardmäßig werden Listen alle 24 Stunden synchronisiert, können jedoch manuell von der Seite `Einstellungen` => `Aufgaben` ausgelöst werden. Sie können diesen Vorgang nicht schneller automatisieren als das.

# UI (Benutzeroberfläche)

Diese Seite ermöglicht es Ihnen, die Anzeigeoptionen der Benutzeroberfläche anzupassen.

## Kalender

![uicalendar.png](/assets/readarr/uicalendar.png)

- Erster Wochentag - Hier können Sie auswählen, welcher Tag Ihrer Meinung nach der erste Tag der Woche sein sollte.
- Wochenüberschrift - Hier können Sie die Überschrift für die Spalten auswählen.

## Daten

![caldates.png](/assets/readarr/caldates.png)

- Kurzes Datumsformat - Wie möchten Sie, dass Readarr kurze Daten anzeigt?
- Langes Datumsformat - Wie möchten Sie, dass Readarr lange Datumsformate anzeigt?
- Zeitformat - Möchten Sie ein 12-Stunden- oder 24-Stunden-Format?
- Relative Daten anzeigen - Möchten Sie, dass Readarr relative (Heute/Gestern/usw.) oder absolute Daten anzeigt?

## Stil

![calstyle.png](/assets/readarr/calstyle.png)

- Farbenblind-Modus aktivieren - Verändert den Stil, um es farbenblinden Benutzern zu ermöglichen, farbcodierte Informationen besser zu unterscheiden.

## Sprache

![callanguage.png](/assets/readarr/callanguage.png)

- UI-Sprache - Wählen Sie die Sprache, die Radarr in der Anwendungs-Benutzeroberfläche verwenden soll.