## Können alle meine Filmdateien in einem Ordner gespeichert werden?

Ja, Radarr ermöglicht es Ihnen, alle Ihre Filmdateien in einem einzigen Ordner zu speichern. Sie können dies tun, indem Sie den Dateispeicherort für Ihre Filme in den Radarr-Einstellungen konfigurieren.

Gehen Sie wie folgt vor, um alle Ihre Filmdateien in einem Ordner zu speichern:

1. Öffnen Sie die Radarr-Benutzeroberfläche in Ihrem Webbrowser.
2. Klicken Sie auf das Symbol "Einstellungen" in der Symbolleiste oben.
3. Wählen Sie die Registerkarte "Medienverwaltung" aus.
4. Scrollen Sie nach unten zum Abschnitt "Dateiverwaltung".
5. Aktivieren Sie die Option "Dateien in einem Ordner speichern".
6. Geben Sie den gewünschten Ordnerpfad in das Textfeld "Dateispeicherort" ein.
7. Klicken Sie auf "Speichern", um die Änderungen zu übernehmen.

Nachdem Sie diese Einstellung vorgenommen haben, werden alle Ihre Filmdateien in dem angegebenen Ordner gespeichert. Bitte beachten Sie, dass dies für alle zukünftigen Filme gilt, die Sie zu Radarr hinzufügen. Bereits vorhandene Filme werden nicht automatisch in den neuen Ordner verschoben. Sie müssen dies manuell tun, wenn Sie alle vorhandenen Filme in den neuen Ordner verschieben möchten.

> **Hinweis:** Stellen Sie sicher, dass der angegebene Ordner über ausreichend Speicherplatz verfügt, um alle Ihre Filmdateien aufzunehmen.

- Nein, das ist nicht möglich. Radarr ist eine Abspaltung von [Sonarr](/sonarr), bei der jeder TV-Show einen eigenen Ordner hat. Diese Einschränkung ist ein bekannter Schmerzpunkt für viele Benutzer und wird möglicherweise in einer zukünftigen Version behoben. Bitte beachten Sie, dass dies keine einfache Änderung ist und eine vollständige Neuschreibung des Backends erfordert.
- Das [GitHub Issue zur benutzerdefinierten Ordnerstruktur](https://github.com/Radarr/Radarr/issues/153) behandelt technisch gesehen diese Anfrage, aber es gibt keine Garantie, dass die Implementierung von Filmdateien in einem Ordner zu diesem Zeitpunkt erfolgen wird.
- Eine mögliche Lösung besteht darin, ein benutzerdefiniertes Skript zu verwenden. Beachten Sie jedoch, dass Sie keinen Rescan in Radarr auslösen dürfen, da der Film dann als fehlend angezeigt wird und unabhängig davon nie aktualisiert wird.
  - Verwenden Sie ein benutzerdefiniertes Skript:
    - Das Skript sollte beim Import ausgelöst werden.
    - Es sollte so konzipiert sein, dass es die Datei verschiebt, wann immer Sie möchten.
    - Anschließend muss es die Radarr-API aufrufen und den Film auf "nicht überwacht" setzen.
- Wenn Sie alle Ihre Filme von einem Ordner in separate Ordner verschieben möchten, lesen Sie den Artikel [Tipps und Tricks => Erstellen Sie für jeden Film einen Ordner](/radarr/tips-and-tricks#creating-a-folder-for-each-movie).

## Kann ich alle meine Filme in einer Bibliothek in einem Ordner speichern?

- Nein, siehe oben.

## Wie aktualisiere ich Radarr?

- Gehen Sie zu "Einstellungen" und dann zum Tab "Allgemein" und zeigen Sie erweiterte Einstellungen an (verwenden Sie den Umschalter neben dem Speichern-Button).

1. Unter dem Abschnitt "Updates" ändern Sie den Branch-Namen in `master` oder `develop`.
1. Speichern Sie.

*Dies installiert die Bits aus diesem Branch nicht sofort, sondern während des nächsten Updates.*

- ![Aktuelle Master/Stable-Version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Diese Version wurde von Benutzern auf den Entwicklungs- und Nightly-Branches getestet und es sind keine größeren Probleme bekannt. Diese Version erhält ungefähr monatlich Updates. Auf GitHub handelt es sich um den `master`-Branch.

- ![Aktuelle Develop/Beta-Version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Beta): Dies ist der Test-Edge. Nachdem es in der Nightly-Version getestet wurde, um sofortige Probleme auszuschließen, werden hier neue Funktionen und Fehlerkorrekturen zuerst veröffentlicht. Es kann als halb stabil angesehen werden, ist aber immer noch `beta`. Diese Version erhält wöchentlich oder zweiwöchentlich Updates, abhängig von der Entwicklung.

> **Warnung: Es ist möglicherweise nicht möglich, nach dem Wechsel zu diesem Branch zu `master` zurückzukehren.** Auf GitHub handelt es sich um einen Schnappschuss des `develop`-Branchs zu einem bestimmten Zeitpunkt.
{.is-warning}

- ![Aktuelle Nightly/Unstable-Version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alpha/Unstable): Dies ist die Bleeding-Edge-Version. Sie wird veröffentlicht, sobald der Code übermittelt wurde und alle automatisierten Tests bestanden hat. Dieser Build wurde möglicherweise noch nicht von uns oder anderen Benutzern verwendet. Es besteht keine Garantie, dass er in einigen Fällen überhaupt ausgeführt wird. Dieser Branch wird nur fortgeschrittenen Benutzern empfohlen. In diesem Branch werden Probleme erwartet und eine eigene Untersuchung ist erforderlich. ***Verwenden Sie diesen Branch nur, wenn Sie wissen, was Sie tun, und bereit sind, bei einem fehlgeschlagenen Update selbst Hand anzulegen.*** Diese Version wird sofort aktualisiert.

> **Warnung: Es ist möglicherweise nicht möglich, nach dem Wechsel zu diesem Branch zu `master` zurückzukehren.** Auf GitHub handelt es sich um den `develop`-Branch.
{.is-danger}

- Hinweis: Wenn Sie eine Docker-Installation haben, fügen Sie `:release`, `:latest`, `:testing` oder `:develop` am Ende Ihres Container-Tags hinzu, abhängig davon, wer Ihre Builds erstellt.

|                                                                    | ![Aktuelle Master/Latest-Version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Aktuelle Develop/Beta-Version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Aktuelle Nightly/Alpha-Version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kann ich Radarr in meinem Docker-Container aktualisieren?

- *Technisch gesehen ja.* **Aber du solltest es auf keinen Fall tun.** Das ist ein grundlegendes Prinzip von Docker. Es können Probleme mit der Datenbank auftreten, wenn Sie Ihre Installation auf die neueste `nightly`-Version aktualisieren und dann den Docker-Container selbst aktualisieren (möglicherweise auf eine ältere Version zurücksetzen).

### Installation einer neueren Version

#### Native

1. Gehen Sie zu System und dann zum Tab Updates.
1. Neuere Versionen, die noch nicht installiert sind, haben einen Update-Button neben sich. Klicken Sie auf diesen Button, um das Update zu installieren.

#### Docker

1. Ziehen Sie Ihr Tag erneut und aktualisieren Sie Ihren Container.

## Kann ich von `nightly` zu `develop` wechseln?

## Kann ich zwischen Branches wechseln?

- Wenn die Version identisch ist, können Sie wechseln. Andernfalls überprüfen Sie beim Entwicklungsteam, ob Sie von `nightly` zu `master`, von `nightly` zu `develop` oder von `develop` zu `master` für Ihren spezifischen Build wechseln können.
- Wenn Sie diese Anweisungen nicht befolgen, kann Ihr Radarr unbrauchbar werden oder Fehler verursachen. Sie wurden gewarnt. Wenn die folgenden Fehlermeldungen auftreten, verwenden Sie eine neuere Datenbank mit einer älteren \*Arr-Version, die nicht unterstützt wird. Aktualisieren Sie \*Arr auf die Version, die Sie zuvor verwendet haben oder eine neuere Version.
  - Beispiel-Fehlermeldungen:
    - `Fehler beim Parsen von Spalte 45 (Language=31 - Int64)`
    - `Der DataMapper konnte das folgende Feld nicht laden: 'Languages' Wert`
    - `ID stimmt nicht mit einer bekannten Sprache überein. Parametername: id`
    - Andere ähnliche Datenbankfehler bezüglich fehlender Spalten oder Tabellen.

## Wie sichere/verwende ich Radarr wiederherstellen?

### Sichern von Radarr

#### Verwendung der integrierten Sicherung

- Gehen Sie in der Radarr-Benutzeroberfläche zu System => Backup.
- Klicken Sie auf die Schaltfläche "Sichern".
- Laden Sie die ZIP-Datei nach der Erstellung der Sicherung herunter und bewahren Sie sie sicher auf.

#### Verwendung des Dateisystems direkt

- Suchen Sie den Speicherort des AppData-Verzeichnisses für Radarr heraus.
  - Gehen Sie über die Radarr-Benutzeroberfläche zu System => About.
  - [Radarr Appdata-Verzeichnis](/radarr/appdata-directory)
- Stoppen Sie Radarr - Dadurch wird verhindert, dass die Datenbank beschädigt wird.
- Kopieren Sie den Inhalt an einen sicheren Ort.

### Wiederherstellen aus einer Sicherung

> Das Wiederherstellen auf ein Betriebssystem mit unterschiedlichen Pfaden funktioniert nicht (Windows zu Linux, Linux zu Windows, Windows zu macOS oder macOS zu Windows). Ein Wechsel zwischen macOS und Linux kann funktionieren, da beide Pfade mit `/` anstelle von `\` verwendet werden, wie es Windows verwendet, aber dies wird nicht unterstützt. Sie müssen alle Pfade in der Datenbank manuell bearbeiten oder [Toolbarr](https://github.com/Notifiarr/toolbarr) verwenden.
{.is-warning}

#### Verwendung der ZIP-Sicherung

- Installieren Sie Radarr erneut (falls zutreffend / noch nicht installiert).
- Starten Sie Radarr.
- Gehen Sie zu System => Backup.
- Wählen Sie "Sicherung wiederherstellen".
- Wählen Sie "Datei auswählen".
- Wählen Sie Ihre Sicherungs-ZIP-Datei aus.
- Wählen Sie "Wiederherstellen".

#### Verwendung der Dateisystem-Sicherung

- Installieren Sie Radarr erneut (falls zutreffend / noch nicht installiert).
- Suchen Sie den Speicherort des AppData-Verzeichnisses für Radarr heraus.
  - Führen Sie Radarr einmal aus und gehen Sie über die Benutzeroberfläche zu System => About.
  - [Radarr Appdata-Verzeichnis](/radarr/appdata-directory)
- Stoppen Sie Radarr.
- Löschen Sie den Inhalt des AppData-Verzeichnisses **(einschließlich der .db-wal/.db-journal-Dateien, sofern vorhanden)**.
- Stellen Sie Ihre Sicherung wieder her.
- Starten Sie Radarr.
- Solange die Pfade gleich sind, wird alles dort fortgesetzt, wo es aufgehört hat.

#### Wiederherstellen des Dateisystems auf einem Synology NAS

> VORSICHT: Die Wiederherstellung auf einem Synology erfordert Kenntnisse in Linux und Root-SSH-Zugriff auf das Synology-Gerät.
{.is-warning}

- Installieren Sie Radarr erneut (falls zutreffend / noch nicht installiert).
- Suchen Sie den Speicherort des AppData-Verzeichnisses für Radarr heraus.
  - Führen Sie Radarr einmal aus und gehen Sie über die Benutzeroberfläche zu System => About.
  - [Radarr Appdata-Verzeichnis](/radarr/appdata-directory)
- Stoppen Sie Radarr.
- Verbinden Sie sich über SSH mit dem Synology NAS und melden Sie sich als Root an.

> Bei einigen Installationen ist der Benutzer anders als in den folgenden Befehlen: `chown -R sc-Radarr:Radarr *` {.is-info}

- Führen Sie die folgenden Befehle aus:

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- Aktualisieren Sie die Berechtigungen für die Dateien:

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Starten Sie Radarr.

# Häufige Probleme mit Radarr

## Eine Aufgabe wurde abgebrochen

- Radarr hat nach 100 Sekunden keine Antwort vom Server erhalten, an den die Anfrage gesendet wurde.
- Die Protokolle enthalten `System.Threading.Tasks.TaskCanceledException: Eine Aufgabe wurde abgebrochen.`
- Dies wird oft verursacht durch:
  - fehlerhafte Konfiguration oder Verwendung eines VPNs
  - fehlerhafte Konfiguration oder Verwendung eines Proxys
  - lokale DNS-Probleme - Versuchen Sie, einen anderen DNS-Anbieter zu verwenden
  - lokale IPv6-Probleme - *am häufigsten* - normalerweise ist IPv6 auf dem Host-System aktiviert, aber nicht funktionsfähig
  - die Verwendung von Privoxy und eine fehlerhafte Konfiguration davon
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) Anfragen
- Sie können mit DNS `nslookup <Domain.tld aus den Trace-Protokollen>` und IPv6 mit `curl -sv -6 "<URL aus den Trace-Protokollen>"` / alle anderen Konnektivitätsprobleme mit `curl -sv -4 "<URL aus den Trace-Protokollen>"` Fehlerbehebung durchführen.

## Der Pfad ist bereits für einen vorhandenen Film konfiguriert

![existing-movie.png](/assets/radarr/existing-movie.png)

- Die Bibliothekseinführung zeigt "Vorhanden" an oder es wird ein Fehler "Der Pfad ist für einen vorhandenen Film konfiguriert" angezeigt.
- Dies tritt auf, wenn Sie versuchen, einen Film hinzuzufügen oder den Pfad eines vorhandenen Films zu bearbeiten, der bereits einem anderen Film zugewiesen ist.
- Wahrscheinlich wurde dies verursacht, indem ein nicht übereinstimmender Film nicht korrigiert wurde, als der Benutzer seine Bibliothek importiert hat.
- Suchen und korrigieren Sie den Film, der bereits diesem Pfad zugewiesen ist.
  - Filmindex
  - Tabellenansicht
  - Optionen => Pfad als Spalte hinzufügen
  - Sortieren und den Film am angegebenen problematischen Pfad finden.
- Alternativ können Sie den Film mit dem vorhandenen Pfad aus Radarr löschen.

## Wie kann ich die Namen meiner Filmordner ändern?

{#rename-folders}

> Der gleiche Prozess gilt auch für das Verschieben/Ändern von Film-Pfaden. Wenn Sie nur Pfade in Radarr aktualisieren und die Dateien nicht verschieben möchten, wählen Sie in Schritt 5 "Ja, Dateien verschieben" nicht aus.
{.is-info}

1. Filme
1. Film-Editor
1. Wählen Sie aus, welche Filme ihren Ordner umbenannt haben müssen
1. Ändern Sie den Stammordner in den gleichen Stammordner, in dem sich die Filme derzeit befinden
1. Wählen Sie "Ja, Dateien verschieben"

> Wenn Sie Plex verwenden, wird dadurch die erneute Erkennung von Intros, Miniaturansichten, Kapiteln und Vorschaudaten ausgelöst.
{.is-warning}

## Benennung von Filmdateien und -ordnern

- Derzeit erfordert Radarr, dass jeder Film in einem Ordner mit dem Format `Filmtitel (Jahr)/` vorhanden ist, optional sind `_` oder `.` gültige Trennzeichen. Um eine korrekte Qualitäts- und Auflösungserkennung während des Imports zu ermöglichen, ist ein Dateiname wie `Filmtitel (Jahr) [Qualität-Auflösung].ext` am besten, wobei `_` oder `.` ebenfalls gültige Trennzeichen sind.

  - Ein nützliches Tool für diese Änderungen in Ihrer Sammlung ist [filebot](http://www.filebot.net/#download), das sowohl in den Apple- als auch in den Windows-Stores eine kostenpflichtige Version hat, aber auf ihrer alten [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) -Website kostenlos erhältlich ist. Es hat sowohl eine GUI als auch eine CLI, sodass Sie verwenden können, womit Sie sich wohl fühlen. Für das obige Beispiel erweitert `{ny}` zu `Name (Jahr)` und `{vf}` gibt die Auflösung wie `1080p` an. Es gibt nichts, um die Qualität zu ermitteln, daher können Sie sie mit `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` fälschen, was alles unter 720p zu `[DVD-572p]` und größer oder gleich 720p wie `[Bluray-1080p]` benennt.

- Weitere Informationen finden Sie im Abschnitt [Tipps und Tricks => Erstellen Sie einen Ordner für jeden Film](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie).

## Falsch benannte Filmordner

- Der Name des Filmordners basiert auf den Metadaten (Name/Jahr) zum Zeitpunkt des Hinzufügens des Films. Wenn Sie einen Film hinzugefügt haben, bevor er veröffentlicht wurde, müssen Sie möglicherweise den Trick zum Umbenennen des Filmordners verwenden, um den Namen des Filmordners zu aktualisieren und die neuen aktuellen Daten widerzuspiegeln.
- Selbst wenn Ihre Filme bereits in Ordnern vorhanden sind, sind die Ordner möglicherweise nicht korrekt benannt. Der Ordnername sollte `Filmtitel (Jahr)` lauten, wobei der Titel und das Jahr im Namen des Ordners derzeit entscheidend sind.

  - Beispiele, die gut funktionieren:
    - `/mnt/Filme/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Kinderfilme/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Beispiele, die funktionieren, aber manuelle Verwaltung erfordern:
    - Nach Buchstaben: `/mnt/Filme/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Nach Bewertung: `/mnt/Filme/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Nach Genre: `/mnt/Filme/Krimi, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Diese Beispiele erfordern bei Hinzufügen eines neuen Films eine manuelle Verwaltung. Jedes der Beispiele hat viele Stammverzeichnisse, wie z.B. `A-D` und `E-G` im Beispiel mit dem ersten Buchstaben, `R` und `PG-13` im Beispiel mit der Bewertung, und Sie können sich die Vielfalt der Genre-Ordner vorstellen. Beim Hinzufügen eines neuen Films muss das richtige Stammverzeichnis für dieses Format ausgewählt werden, damit es funktioniert.
  - Beispiele, die nicht funktionieren:
    - Einzelner Ordner: `/mnt/Kinderfilme/Frozen (2013) [Bluray-1080p].mkv`
      - Derzeit müssen Filme einfach in einem Ordner mit dem Namen des Films sein. Es gibt keine Möglichkeit, dies zu umgehen, bis Entwicklungsarbeiten durchgeführt werden, um diese Funktion hinzuzufügen.
    - **Film**-Ordnerbenennungsformate ab v0.2, die **Datei**-Eigenschaften im **Filmordner**-Namen enthalten, wie ``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}``, funktionieren in v3 nicht.
      - Ordner sind mit dem Film verbunden und unabhängig von der Datei. Darüber hinaus wird dies mit der geplanten Unterstützung für mehrere Dateien pro Film nicht funktionieren.
      - Der andere Grund für die Entfernung war, dass dies häufig zu Verwirrung, Datenbankkorruption und im Allgemeinen zu unvollständigen Ergebnissen führte.
  - Der Abschnitt [Tipps und Tricks => Erstellen Sie einen Ordner für jeden Film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) ist eine großartige Quelle, um sicherzustellen, dass Ihre Datei- und Ordnerstruktur hervorragend funktioniert.

## Kann ich die Aktualisierungsaufgabe für Filme deaktivieren?

- Nein, und Sie sollten dies auch nicht durch SQL-Manipulationen tun. Die Aktualisierungsaufgabe für Filme fragt den Upstream-Servarr-Proxy ab und überprüft, ob die Metadaten für jeden Film (IDs, Besetzung, Zusammenfassung, Bewertung, Übersetzungen, alternative Titel usw.) im Vergleich zu dem, was derzeit in Radarr vorhanden ist, aktualisiert wurden. Wenn erforderlich, werden die entsprechenden Filme aktualisiert.
- Eine häufige Beschwerde ist, dass die Aktualisierungsaufgabe zu einer starken I/O-Nutzung führt.
- Die Hauptoption ist "Filmordner nach Aktualisierung erneut scannen". Wenn die Festplatten-I/O-Nutzung während einer Aktualisierung stark ansteigt, sollten Sie die Einstellung "Erneut scannen" auf `Manuell` ändern.
  - Ändern Sie dies nicht auf `Nie`, es sei denn, alle Änderungen an Ihrer Bibliothek (neue Filme, Upgrades, Löschungen usw.) werden über Radarr durchgeführt.
  - Wenn Sie Filmdateien manuell oder über Plex oder ein anderes Programm eines Drittanbieters löschen, setzen Sie dies nicht auf `Nie`.
- Die andere Einstellung, die geändert werden kann, ist "Videodateien analysieren", was empfohlen wird, wenn Sie tdarr verwenden oder Ihre Dateien anderweitig extern ändern. Wenn Sie dies nicht tun, können Sie "Videodateien analysieren" sicher deaktivieren, um etwas I/O zu reduzieren.

## Wie kann ich eine Funktion für Radarr anfordern?

- Das ist einfach [klicken Sie hier](https://github.com/Radarr/Radarr/issues)

## Hilfe, mein Mac sagt, dass Radarr nicht geöffnet werden kann, weil der Entwickler nicht verifiziert werden kann

- Das ist einfach, bitte sehen Sie sich diesen Link für weitere Informationen an [hier](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Entwickler kann nicht verifiziert werden](developer-cannot-be-verified.png "Entwickler kann nicht verifiziert werden")
- Alternativ müssen Sie Radarr selbst signieren `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Hilfe, mein Mac sagt, dass Radarr.app beschädigt ist und nicht geöffnet werden kann

- Das liegt entweder an einem beschädigten Download, also versuchen Sie es erneut, oder [Sicherheitsproblemen, bitte sehen Sie sich diesen FAQ-Eintrag an.](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Ich erhalte einen Fehler: Datenbankdiskimage ist beschädigt

> \* Für Radarr-Benutzer, die dies nach dem Upgrade auf v4.X-Versionen erleben. v4-Versionen führen aufgrund dessen mehrere weitreichende Migrationen durch. Wenn Ihre Datenbank an irgendeiner Stelle zuvor beschädigt war (was beim Ausführen von Radarr zuvor möglicherweise nicht erkennbar war), schlägt die Migration fehl. Dadurch kann Radarr nicht gestartet werden. Es ist wahrscheinlich, dass auch alle Ihre Backups beschädigt sind. Das Wiederherstellen dieser wird das Problem wahrscheinlich nicht lösen.
> \* Wenn die nach der Migration erstellte Datenbank nicht geöffnet werden kann oder nicht wiederhergestellt werden kann, erstellen Sie eine Kopie der Datenbank aus einem aktuellen Backup und wenden Sie den Datenbankwiederherstellungsprozess auf diese Datei an. Versuchen Sie dann, Radarr mit der wiederhergestellten Backup-Datei zu starten. Es sollte dann ohne Probleme migrieren.
{.is-warning}

- **Fehler wie `Error creating log database` deuten auf Probleme mit logs.db hin**
  - Dies kann schnell behoben werden, indem die Datenbank umbenannt oder entfernt wird. Die Protokolldatenbank enthält unwichtige Informationen zu Befehlshistorie, Update-Installationshistorie sowie Info-, Warn- und Fehlermeldungen.
- **Fehler wie `Error creating main database` oder allgemeine `database disk image is malformed` ohne spezifizierte Datenbank deuten auf Probleme mit radarr.db hin**
  - Fahren Sie mit den unten angegebenen Schritten fort.
- Dies bedeutet, dass Ihre SQLite-Datenbank, die die meisten Informationen für Radarr speichert, beschädigt ist. Ihre Optionen bestehen darin, (ein) Backup(s) zu versuchen, die vorhandene Datenbank wiederherzustellen, die Backup(s) wiederherzustellen oder falls alles andere fehlschlägt, mit einer neuen frischen Datenbank neu zu beginnen.
- Dieser Fehler kann auftreten, wenn die Datenbankdatei vom Benutzer/der Gruppe \*Arr, unter dem/die \*Arr ausgeführt wird, nicht beschreibbar ist. Berechtigungen sind wahrscheinlich nur ein Problem für neue Installationen, migrierte Installationen auf einen neuen Server, wenn Sie kürzlich die Berechtigungen für Ihr Appdata-Verzeichnis geändert haben oder wenn Sie den Benutzer und die Gruppe geändert haben, unter dem/die \*Arr ausgeführt wird.
- Ihre beste und erste Option besteht darin, [versuchen Sie, ein Backup wiederherzustellen](#how-do-i-backuprestore-my-radarr). Für Benutzer, die dies nach dem Upgrade auf v4 erhalten, ist es jedoch höchst unwahrscheinlich, dass das Backup selbst funktioniert, und Sie müssen die anderen genannten Wiederherstellungsmethoden ausprobieren.
- Sie können auch versuchen, Ihre Datenbank wiederherzustellen. Dies ist in der Regel die einzige Option, wenn dieses Problem nach einem Update auftritt. Versuchen Sie den [sqlite3 `.recover` Befehl](/useful-tools#recovering-a-corrupt-db)
  - Wenn Ihr sqlite nicht über `.recover` verfügt oder Sie eine benutzerfreundlichere GUI (z. B. Windows) wünschen, befolgen Sie [unsere Anweisungen in diesem Wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- Eine weitere mögliche Ursache für den Fehler in Ihrer Datenbank ist, dass Sie Ihre Datenbank auf einem Netzlaufwerk (NFS oder SMB oder etwas anderem, das nicht lokal ist) platzieren. **SQLite ist für Situationen ausgelegt, in denen Daten und Anwendung auf demselben Computer vorhanden sind.** Daher muss sich Ihr \*Arr AppData-Ordner (/config mount für Docker) auf lokalem Speicher befinden. [SQLite und Netzlaufwerke spielen nicht gut zusammen und führen letztendlich zu einer beschädigten Datenbank](https://www.sqlite.org/draft/useovernet.html).
- Wenn Sie mergerFS verwenden, müssen Sie `direct_io` entfernen, da SQLite mmap verwendet, das von `direct_io` nicht unterstützt wird, wie in der mergerFS [Dokumentation hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs) erklärt.

## Ich verwende Radarr auf einem Mac und es funktioniert plötzlich nicht mehr. Was ist passiert?

- Wahrscheinlich handelt es sich dabei um einen MacOS-Bug, der dazu geführt hat, dass eine der Datenbanken beschädigt wurde.
- Siehe den oben genannten Eintrag zur beschädigten Datenbank.
- Versuchen Sie dann, das Programm zu starten und sehen Sie, ob es funktioniert. Wenn es nicht funktioniert, benötigen Sie weitere Unterstützung. Posten Sie in unserem [Subreddit /r/radarr](http://reddit.com/r/radarr) oder kommen Sie auf [unseren Discord-Server](https://radarr.video/discord), um Hilfe zu erhalten.

## Warum kann Radarr meine Dateien auf einem Remote-Server nicht sehen?

- Stellen Sie für alle Betriebssysteme sicher, dass der Benutzer/die Gruppe, unter dem/die \*Arr ausgeführt wird, Lese- und Schreibzugriff auf das eingebundene Laufwerk hat.
- Für Linux stellen Sie sicher:
  - Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` für Ihr Laufwerk aktiviert ist.
  - Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` für Ihr Laufwerk aktiviert ist.
- Für Windows: Kurz gesagt, der Benutzer, unter dem \*Arr ausgeführt wird (wenn als Dienst) oder unter dem \*Arr ausgeführt wird (wenn als Tray-App), kann nicht auf den Dateipfad auf dem Remote-Server zugreifen. Dies kann verschiedene Gründe haben, aber das häufigste ist, dass \*Arr als Dienst ausgeführt wird, was zu den unten beschriebenen Problemen führt.

### Radarr wird standardmäßig unter dem LocalService-Konto ausgeführt, das keinen Zugriff auf geschützte Remote-Dateifreigaben hat

- Führen Sie den Radarr-Dienst als anderen Benutzer aus, der Zugriff auf diese Freigabe hat
- Öffnen Sie das Fenster "Administrative Tools" => "Services" auf Ihrem Windows-Server.
- Stoppen Sie den Radarr-Dienst.
- Öffnen Sie den Dialog "Eigenschaften" => "Anmelden".
- Ändern Sie das Benutzerkonto des Dienstes in das Zielbenutzerkonto.
- Führen Sie Radarr.exe über den Startordner aus

### Sie verwenden ein zugeordnetes Netzlaufwerk (kein UNC-Pfad)

- Ändern Sie Ihre Pfade in UNC-Pfade (`\\server\share`)
- Führen Sie Radarr.exe über den Startordner aus

## Wie wechsle ich vom Windows-Dienst zu einer Tray-App?

1. Beenden Sie Radarr
1. Führen Sie serviceuninstall.exe im Radarr-Verzeichnis aus
1. Führen Sie `Radarr.exe` einmal als Administrator aus, um ihm die erforderlichen Berechtigungen zu geben und die Firewall zu öffnen. Sobald dies abgeschlossen ist, können Sie es schließen und normal ausführen.
1. (Optional) Legen Sie eine Verknüpfung zur .exe-Datei im Startordner ab, um sie beim Start automatisch zu starten.

## Hilfe, ich habe mich ausgesperrt

{#help-i-have-forgotten-my-password}

Um die Authentifizierung zu deaktivieren (um Ihren vergessenen Benutzernamen oder Ihr Passwort zurückzusetzen), müssen Sie `config.xml` bearbeiten, das sich im [Radarr Appdata-Verzeichnis](/radarr/appdata-directory) befindet.

1. Öffnen Sie config.xml in einem Texteditor
1. Suchen Sie die Zeile mit der Authentifizierungsmethode:
`<AuthenticationMethod>Basic</AuthenticationMethod>` oder `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Ändern Sie die Zeile `AuthenticationMethod` in `<AuthenticationMethod>None</AuthenticationMethod>`
1. Starten Sie Radarr neu
1. Radarr ist jetzt ohne Passwort zugänglich. Sie sollten zu `Einstellungen: Allgemein` in der Benutzeroberfläche gehen und Ihren Benutzernamen und Ihr Passwort festlegen

## Wie verhindere ich, dass der Browser beim Start geöffnet wird?

Je nach Betriebssystem gibt es mehrere mögliche Möglichkeiten.

- In `Einstellungen` => `Allgemein` gibt es auf einigen Betriebssystemen ein Kontrollkästchen zum Starten des Browsers beim Start.
- Wenn Sie Radarr aufrufen, können Sie `-nobrowser` (*nix) oder `/nobrowser` (Windows) zu den Argumenten hinzufügen.
- Beenden Sie Radarr und bearbeiten Sie die Datei config.xml und ändern Sie `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## Seltsame UI-Probleme

- Wenn Sie seltsame UI-Probleme haben, wie z.B. die Bibliotheksseite, auf der nichts aufgelistet ist, oder eine bestimmte Ansicht oder Sortierung nicht funktioniert, versuchen Sie es in einem Chrome-Inkognito-Fenster oder einem Firefox-Privatfenster. Wenn es dort einwandfrei funktioniert, löschen Sie Ihren Browser-Cache und Ihre Cookies für Ihre spezifische IP-/Domain. Weitere Informationen finden Sie im Wiki-Artikel [Cache, Cookies und lokaler Speicher löschen](/useful-tools#clearing-cookies-and-local-storage).

## Die Web-Benutzeroberfläche lädt nur unter localhost auf Windows

- Wenn Sie Ihre Web-Benutzeroberfläche nur unter <http://localhost:7878/> oder <http://127.0.0.1:7878/> erreichen können, müssen Sie mindestens einmal als Administrator ausführen.

## Berechtigungen

- Radarr muss Dateien von dem Ort verschieben, an dem der Downloader sie ablegt, in den endgültigen Speicherort. Dies bedeutet, dass sowohl auf das Quell- als auch auf das Zielverzeichnis und die Dateien gelesen/schreibgeschützt zugegriffen werden muss.
- Unter Linux, wo bewährte Verfahren vorsehen, dass Dienste als eigener Benutzer ausgeführt werden, müssen Sie wahrscheinlich eine gemeinsame Gruppe verwenden und die Ordnerberechtigungen auf `775` und die Dateien auf `664` sowohl in Ihrem Downloader als auch in \*Arr einstellen. In der umask-Notation wäre das `002`.

## System & Logs lädt endlos

- Es handelt sich um die Easy-Privacy-Blockliste. Sie blockieren im Grunde genommen jede URL mit `/api/log?` darin. Schauen Sie sich die Liste an und überlegen Sie, ob es sinnvoll ist, alle URLs in dieser Liste zu blockieren. Es gibt Dutzende von URLs, die potenziell Websites zerstören können. Sie haben diese Option in Ihrem Adblocker ausgewählt. Die einfache Lösung besteht darin, die Domain, auf der Radarr ausgeführt wird, auf die Whitelist zu setzen. Ich empfehle jedoch, die Liste zu überprüfen.

## Torrents entpacken

- Die meisten Torrent-Clients verfügen nicht über die automatische Verarbeitung von komprimierten Archiven wie ihre Usenet-Gegenstücke. Wir empfehlen [unpackerr](https://github.com/unpackerr/unpackerr).

## uTorrent funktioniert nicht mehr

- Stellen Sie sicher, dass die Web-Benutzeroberfläche aktiviert ist
- Stellen Sie sicher, dass der alternative Listening-Port (Erweitert => Web-Benutzeroberfläche) nicht mit dem Listening-Port (Verbindungen) identisch ist
- Wir empfehlen, den alternativen Listening-Port der Web-Benutzeroberfläche zu ändern, um keine Portweiterleitung für Verbindungen zu beeinträchtigen.

## Ich habe eine Meldung erhalten, dass config.xml beschädigt ist, was nun?

- Radarr konnte Ihre Konfigurationsdatei beim Start nicht lesen, da sie aus irgendeinem Grund beschädigt wurde. Um wieder online zu gehen, müssen Sie `.xml` in Ihrem [Appdata-Verzeichnis](/radarr/appdata-directory) löschen. Sobald Sie dies gelöscht haben, starten Sie und es wird auf dem Standardport (7878) gestartet. Sie sollten nun alle Einstellungen erneut konfigurieren, die Sie auf der Seite "Allgemeine Einstellungen" konfiguriert haben.

## Ungültiges Zertifikat und andere HTTPS- oder SSL-Probleme

- Dein Download-Client funktioniert nicht mehr und du erhältst einen Fehler wie `Localhost ist ein ungültiges Zertifikat`?
  - Radarr überprüft SSL-Zertifikate. Wenn kein SSL-Zertifikat im Download-Client festgelegt ist oder du ein selbstsigniertes HTTPS-Zertifikat ohne das CA-Zertifikat hinzugefügt hast, wird Radarr die Verbindung ablehnen. Kostenlose ordnungsgemäß signierte Zertifikate sind von [Let's Encrypt](https://letsencrypt.org/) erhältlich.
  - Wenn dein Download-Client und dein Radarr auf demselben Computer sind, gibt es keinen Grund, HTTPS zu verwenden. Die einfachste Lösung besteht darin, SSL für die Verbindung zu deaktivieren. Die meisten würden zustimmen, dass es auch in einem lokalen Netzwerk nicht erforderlich ist. Es ist möglich, die Zertifikatsvalidierung in den erweiterten Einstellungen zu deaktivieren, wenn du eine unsichere SSL-Konfiguration beibehalten möchtest.

## VPNs, Jackett und die \*ARRs

- Sofern du dich nicht in einem repressiven Land wie China, Australien oder Südafrika befindest, sollte dein Torrent-Client in der Regel das einzige sein, das hinter einem VPN steht. Da der VPN-Endpunkt von vielen Benutzern gemeinsam genutzt wird, kannst du und wirst wahrscheinlich Geschwindigkeitsbegrenzungen, DDOS-Schutz und IP-Sperren von verschiedenen Diensten erleben, die jede Software verwendet.
- Mit anderen Worten, das Hinterlegen der \*Arrs (Lidarr, Prowlarr, Radarr, Readarr und Lidarr) hinter einem VPN kann und wird in einigen Fällen dazu führen, dass die Anwendungen aufgrund der Nichterreichbarkeit der Dienste nicht verwendbar sind.

> **Um es klar zu sagen, es ist nicht die Frage, ob VPNs Probleme mit den \*Arrs verursachen, sondern wann: Bildanbieter werden dich blockieren und Cloudflare steht vor den meisten \*Arr-Servern (Updates, Metadaten usw.) und wird dich auch blockieren.**
{.is-warning}

- **Viele private Tracker werden dich verbannen, wenn du sie über ein VPN verwendest oder darauf zugreifst (z. B. mit Jackett oder Prowlarr).**

### Verwendung eines VPNs

- Wenn ein VPN erforderlich ist und Docker verwendet wird, wird empfohlen, die Download-Client + VPN-Container von Hotio oder Binhex zu verwenden.
- Wenn ein VPN erforderlich ist und Docker nicht verwendet wird, muss dein VPN-Client ***Split Tunneling*** unterstützen, damit nur die erforderlichen (Download-Client) Apps hinter dem VPN stehen.
- Viele Probleme beim Zugriff auf Tracker können behoben werden, indem du die DNS-Server von Google oder Cloudflare anstelle der DNS-Server deines Internetdienstanbieters verwendest.
- In einigen Fällen (z. B. bei britischen Internetdienstanbietern) musst du deinen Torrent-Download-Client möglicherweise hinter einem VPN und Jackett/Prowlarr wie folgt platzieren:
  - Setze Jackett hinter das VPN und stelle sicher, dass Split Tunneling den lokalen Zugriff zulässt.
  - Für Prowlarr konfiguriere deinen VPN-Client so, dass er einen Proxy bereitstellt, und füge den Proxy in den Einstellungen => Indexers hinzu. Gib dem Proxy einen Tag und weise allen Indexern, die ihn verwenden müssen, denselben Tag zu.
    - Wenn es unbedingt erforderlich ist und dein VPN keine Möglichkeit bietet, einen Proxy zu erstellen, kannst du Prowlarr hinter das VPN setzen und sicherstellen, dass Split Tunneling den lokalen Zugriff zulässt.

# Radarr-Suche und häufige Probleme beim Herunterladen

## Warum kann ich keinen neuen Film zu Radarr hinzufügen?

{#warum-kann-ich-einen-neuen-film-nicht-zu-radarr-hinzufügen}

- Radarr verwendet [The Movie Database (TMDb)](http://themoviedb.org) für Filminformationen und Bilder wie Fanart, Banner und Hintergründe. Im Allgemeinen gibt es einige Gründe, warum du möglicherweise keinen Film hinzufügen kannst:
  - TMDb mag es nicht, wenn bei der Suche nach Filmen über die API (die Radarr verwendet) Sonderzeichen verwendet werden. Versuche es also mit einem übersetzten Namen und/oder ohne Sonderzeichen.
  - Du kannst auch nach der TMDb-ID oder, falls vorhanden, der IMDb-ID suchen.
  - Der Film wurde noch nicht zu TMDb hinzugefügt. Befolge ihre [Anleitung](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006), um ihn hinzuzufügen.

## Jackett zeigt mehr Ergebnisse als bei manueller Suche

- Dies liegt normalerweise daran, dass du Jackett anders durchsuchst als bei der manuellen Suche. Weitere Informationen findest du in unserem [Problembehandlungsartikel](/radarr/troubleshooting).

## Wie bestimmt Radarr das Jahr eines Films?

- Radarr erhält Metadaten von [TMDb](https://www.themoviedb.org/)
- Radarr verwendet das Jahr des ältesten **Theatrical Release**-Datums und das älteste **Premier**-Datum für die Übereinstimmung.
  - Beachte, dass falls kein Theatrical Release existiert, die Logik auf das älteste physische oder digitale Veröffentlichungsdatum zurückgreift.
- Wenn einem Film ein digitales, physisches, theatralisches oder Premier-Veröffentlichungsdatum fehlt, sollte dies in TMDb aktualisiert werden.
- [TMDb's Contribution Bible](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) enthält folgende Informationen zu ihren Veröffentlichungstypen.
  - **Premiere** - Eine Premiere kann in Form einer Festivalvorführung (z. B. TIFF) oder einer Premiere-Veranstaltung mit der Besetzung und Crew in einer großen Stadt (z. B. LA, London, Toronto) stattfinden.
  - **Theatrical** - Kann für die ursprüngliche Veröffentlichung und alle nachfolgenden offiziellen Veröffentlichungen verwendet werden. Wird für breite oder Sättigungsveröffentlichungen verwendet. In den USA gelten 600-1.999 Bildschirme als breite Veröffentlichung und 2000+ als Sättigungsveröffentlichung.
  - **Theatrical (limited)** - Eine begrenzte Kinoveröffentlichung ist eine Vertriebsstrategie für Filme, bei der ein neuer Film in einigen Kinos eines Landes veröffentlicht wird, normalerweise in großen Metropolen. In den USA gibt es weniger als 600 Kinos.
  - **Physical** - Umfasst alle VHS-, DVD- und Blu-ray-Veröffentlichungen.
  - **Digital** - Alle relevanten Veröffentlichungen können hinzugefügt werden, einschließlich Streaming-Plattformen, VOD-Miete oder -Kauf. Digitale Vorführungen, einschließlich Online-Filmfestivals und virtuelle Kinoveröffentlichungen, gelten ebenfalls als digitale Veröffentlichungen.

## Wie geht Radarr mit ausländischen Filmen oder ausländischen Titeln um?

> [TRaSH's Anleitung zur benutzerdefinierten Formatierungssprache](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kann hilfreich sein, um Filme in der gewünschten Sprache zu erhalten.{.is-info}

> Ab dem 12. Februar 2023 wird der Metadatencache von Radarr die Originalsprache eines Films als TMDb-Sprache verwenden, wenn und nur wenn der Film auf TMDb nur eine gesprochene Sprache hat. Andernfalls wird die ursprüngliche TMDb-Sprache des Films verwendet.
{.is-warning}

## ID-Suchen

- **Indexer, die ID-basierte Suchen unterstützen** - Suchen auf Indexern und Trackern, die ID-basierte Suchen (TMDbId, IMDbId usw.) unterstützen - wie viele Usenet-Indexer und viele private Torrent-Tracker - werden Textabfragen nicht verwendet, wenn Ergebnisse für eine ID-basierte Suche zurückgegeben werden. Wenn Ergebnisse zurückgegeben werden, wird keine Namens-/Textsuche durchgeführt. Wenn du keine Ergebnisse von deinem Indexer erhältst, liegt dies daran, dass die Veröffentlichung(en) mit der falschen Film-ID verknüpft sind.
  - Die Sprache der Veröffentlichung kann auch von der Sprache der Veröffentlichung des Indexers oder Trackers im Ergebnis abgeleitet werden, sofern angegeben, anstatt aus dem Namen analysiert zu werden.

## Textsuchen

- **Indexer, die keine ID-basierten Suchen unterstützen oder bei denen ID-basierte Suchen keine Ergebnisse liefern** - Die Suche verwendet den Originaltitel des Films, den englischen Titel und den übersetzten Titel aus den Sprachen, die du in deinem Qualitätsprofil für Filmeinstellungen und in benutzerdefinierten Formaten mit Punktzahlen größer als null festgelegt hast.
- Das Parsen (d. h. Importieren) sucht nach Übereinstimmungen in allen Übersetzungen und alternativen Titeln.
  - Die Sprache der Veröffentlichung kann auch von der Sprache der Veröffentlichung des Indexers oder Trackers im Ergebnis abgeleitet werden, sofern angegeben, anstatt aus dem Namen analysiert zu werden.

## Ausländische Filme erhalten

- Um einen Film in einer fremden Sprache zu erhalten, setze die Sprache des Qualitätsprofils deines Films auf Original (Originalsprache des Films\*), eine bestimmte Sprache für dieses Profil oder `Any` und erstelle benutzerdefinierte Formate mit Bedingungen für die Sprache und einer Punktzahl größer als 0, um festzulegen, welche Sprache verwendet werden soll.
- Beachte, dass dies keine Indexersprachen umfasst, die in den Einstellungen des Indexers als `multi` konfiguriert sind.
  - Beachte, dass ab [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) von Radarr nicht mehr davon ausgegangen wird, dass `multi` Englisch einschließt.
  - Benutzer können ihre Einstellungen pro Indexer anpassen, um festzulegen, welche Sprache(n) `multi` angibt.

## Wie geht Radarr mit "multi" in Namen um?

- Mit Radarr v4.1+ geht Radarr davon aus, dass `multi` nur die Sprache des Films ist und **NICHT** Englisch, wie in früheren Versionen.
  - Benutzer können ihre Einstellungen pro Indexer anpassen, um festzulegen, welche Sprache(n) `multi` angibt.
- Beachte, dass `multi`-Definitionen nur für die Veröffentlichungsparsing und nicht für fremdsprachige Titel oder Filmsuchen hilfreich sind.

## Hilfe, Film hinzugefügt, aber nicht gesucht

- Radarr sucht nicht *aktiv* automatisch nach fehlenden Filmen. Stattdessen wird regelmäßig eine Abfrage neuer Beiträge an alle für RSS konfigurierten Indexer gesendet. Wenn ein gewünschter oder abgeschnittener Film in dieser Liste auftaucht, wird er heruntergeladen. Das bedeutet, dass ein Film erst heruntergeladen wird, wenn er gepostet (oder erneut gepostet) wird.
- Wenn du einen Film hinzufügst, den du sofort haben möchtest, ist die beste Option, das Kontrollkästchen "Suche nach fehlendem Film starten" links neben der Schaltfläche *Film hinzufügen* (**1**) zu aktivieren. Du kannst auch zur Seite eines Films gehen, den du hinzugefügt hast, und auf das Lupensymbol "Suche" (**2**) klicken oder die Ansicht "Gewünscht" verwenden, um nach fehlenden oder abgeschnittenen Filmen zu suchen.

  - Film hinzufügen und suchen beim Hinzufügen eines Films
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Suche nach einem vorhandenen Film
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jacketts /all-Endpunkt

{#jackett-all-endpoint}

- Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ kannst du auch das Jackett & NZBHydra2-Alternative [Prowlarr](/prowlarr) ausprobieren.

- **Update vom 1. Januar 2022: Der Jackett `/all`-Endpunkt wird ab der Version 4.0.0.5730 nicht mehr unterstützt (Warnungen werden angezeigt), da er nur Probleme verursacht.**

- Der Jackett /all-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Selbst die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des /all-Endpunkts hat keine Vorteile, nur Nachteile:
  - Du verlierst die Kontrolle über indexer-spezifische Einstellungen (Kategorien, Suchmodi usw.).
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen.
  - Indexer-spezifische Kategorien (\>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis.
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt.
  - Wenn einer der Tracker in /all einen Fehler zurückgibt, deaktiviert \*Arr ihn und du erhältst keine Ergebnisse mehr.

### Lösungen für Jackett /All

- Füge jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu.
- Schau dir [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schau dir [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwende jedoch nicht ihren einzelnen aggregierten Endpunkt und verwende `multi`, wenn die Synchronisierung verwendet wird.

## Warum gibt es zwei Dateien? | Warum bleibt eine Datei im Download-Ordner?

Das ist normal. Bei einer Konfiguration, die [Hardlinks](https://trash-guides.info/hardlinks) unterstützt, wird kein doppelter Speicherplatz verwendet. Hier ist, wie der Torrent-Prozess funktioniert.

1. Radarr sendet eine Download-Anforderung an deinen Client und ordnet sie einem Label oder Kategorienamen zu, den du in den Einstellungen des Download-Clients konfiguriert hast. Beispiele: Filme, TV, Serien, Musik usw.
1. Radarr überwacht die aktiven Downloads deines Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API deines Download-Clients.
1. Abgeschlossene Dateien werden an ihrem ursprünglichen Speicherort belassen, um das Seederlebnis zu ermöglichen (Verhältnis oder Zeit können im Download-Client oder innerhalb des spezifischen Download-Clients angepasst werden). Wenn Dateien in deinen Medienordner importiert werden, wird die Datei per Hardlink verknüpft, sofern dies von deiner Konfiguration unterstützt wird, oder kopiert, wenn Hardlinks nicht unterstützt werden.
1. Wenn die Option "Abgeschlossene Download-Verarbeitung - Abgeschlossene entfernen" in den Einstellungen von Radarr aktiviert ist, löscht Radarr die Originaldatei und den Torrent aus deinem Download-Client, aber nur, wenn der Download-Client meldet, dass das Seederlebnis abgeschlossen ist und der Torrent angehalten ist (d. h. pausiert). Siehe [TRaSH's Download-Client-Anleitungen](https://trash-guides.info/Downloaders/) für die optimale Konfiguration deines Download-Clients.

> Hardlinks sind standardmäßig aktiviert. [Ein Hardlink erfordert keinen zusätzlichen Festplattenspeicherplatz.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Das Dateisystem und die Mounts müssen für deinen abgeschlossenen Download-Ordner und deine Medienbibliothek identisch sein. Wenn das Erstellen von Hardlinks fehlschlägt oder deine Konfiguration keine Hardlinks unterstützt, wird die Datei kopiert.
{.is-info}

## Warum funktioniert Radarr nicht hinter einem Reverse Proxy?

- Ab Version 3 hat Radarr auf .NET und einen neuen Webserver umgestellt. Damit SignalR funktioniert, die UI-Schaltflächen funktionieren, Datenbankänderungen übernommen werden und andere Elemente. Es ist die folgende Ergänzung zum location-Block für Radarr erforderlich:

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- Stelle sicher, dass du **nicht** `proxy_set_header Connection "Upgrade";` wie in der nginx-Dokumentation vorgeschlagen, einfügst. **DAS FUNKTIONIERT NICHT**
- [Siehe dieses ASP.NET Core Problem](https://github.com/aspnet/AspNetCore/issues/17081)
- Wenn du einen CDN wie Cloudflare verwendest, stelle sicher, dass Websockets aktiviert sind, um Websocket-Verbindungen zu ermöglichen.
- Wenn unerwartete Weiterleitungen auftreten, stelle sicher, dass dein Host-Header weitergeleitet wird.