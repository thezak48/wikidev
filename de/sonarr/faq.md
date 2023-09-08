## Wie wechsle ich vom Windows-Dienst zur Tray-App?

Wenn Sie Sonarr als Windows-Dienst installiert haben und stattdessen die Tray-App verwenden möchten, können Sie wie folgt vorgehen:

1. Beenden Sie den Sonarr-Dienst, indem Sie die Windows-Diensteverwaltung öffnen, den Sonarr-Dienst auswählen und auf "Beenden" klicken.
2. Öffnen Sie den Sonarr-Installationsordner (standardmäßig "C:\ProgramData\NzbDrone").
3. Starten Sie die Datei "NzbDrone.exe", um die Sonarr-Tray-App zu starten.
4. Klicken Sie mit der rechten Maustaste auf das Sonarr-Symbol in der Taskleiste und wählen Sie "Open Sonarr" aus dem Kontextmenü, um das Sonarr-Webinterface zu öffnen.

Jetzt verwenden Sie die Sonarr-Tray-App anstelle des Windows-Dienstes. Beachten Sie, dass die Tray-App nur aktiv ist, solange sie geöffnet ist. Wenn Sie Ihren Computer neu starten, müssen Sie die Tray-App erneut starten, um Sonarr zu verwenden.

1. Schließen Sie Sonarr.
1. Führen Sie serviceuninstall.exe im Sonarr-Verzeichnis aus.
1. Führen Sie Sonarr.exe einmal als Administrator aus, um ihm die erforderlichen Berechtigungen zu geben und die Firewall zu öffnen. Sobald der Vorgang abgeschlossen ist, können Sie es schließen und normal ausführen.
1. (Optional) Erstellen Sie eine Verknüpfung zu Sonarr.exe im Autostart-Ordner, um es beim Start automatisch zu starten.

## Wie sichere/verwende ich Sonarr wiederherstellen?

### Sichern von Sonarr

#### Verwendung der integrierten Sicherung

- Gehen Sie in der Sonarr-Benutzeroberfläche zu System => Backup.
- Klicken Sie auf die Schaltfläche "Backup".
- Laden Sie die ZIP-Datei nach der Erstellung der Sicherung herunter und bewahren Sie sie sicher auf.

#### Direkte Verwendung des Dateisystems

- Suchen Sie den Speicherort des AppData-Verzeichnisses für Sonarr heraus.
  - Gehen Sie über die Sonarr-Benutzeroberfläche zu System => About.
  - [Sonarr Appdata-Verzeichnis](/sonarr/appdata-directory)
- Beenden Sie Sonarr - Dadurch wird verhindert, dass die Datenbank beschädigt wird.
- Kopieren Sie den Inhalt an einen sicheren Ort.

### Wiederherstellen aus einer Sicherung

> Die Wiederherstellung auf ein Betriebssystem mit unterschiedlichen Pfaden funktioniert nicht (Windows zu Linux, Linux zu Windows, Windows zu macOS oder macOS zu Windows). Ein Wechsel zwischen macOS und Linux kann funktionieren, da beide Pfade mit `/` anstelle von `\` verwendet werden, wie es Windows verwendet, aber dies wird nicht unterstützt. Sie müssen alle Pfade in der Datenbank manuell bearbeiten oder [Toolbarr](https://github.com/Notifiarr/toolbarr) verwenden.
{.is-warning}

#### Verwendung der ZIP-Sicherung

- Installieren Sie Sonarr neu (falls zutreffend / noch nicht installiert).
- Starten Sie Sonarr.
- Navigieren Sie zu System => Backup.
- Wählen Sie "Backup wiederherstellen".
- Wählen Sie "Datei auswählen".
- Wählen Sie Ihre Sicherungs-ZIP-Datei aus.
- Wählen Sie "Wiederherstellen".

#### Verwendung der Dateisystem-Sicherung

- Installieren Sie Sonarr neu (falls zutreffend / noch nicht installiert).
- Suchen Sie den Speicherort des AppData-Verzeichnisses für Sonarr heraus.
  - Führen Sie Sonarr einmal aus und gehen Sie über die Benutzeroberfläche zu System => About.
  - [Sonarr Appdata-Verzeichnis](/sonarr/appdata-directory)
- Beenden Sie Sonarr.
- Löschen Sie den Inhalt des AppData-Verzeichnisses **(einschließlich der .db-wal/.db-journal-Dateien, sofern vorhanden)**.
- Stellen Sie Ihre Sicherung wieder her.
- Starten Sie Sonarr.
- Solange die Pfade gleich sind, wird alles dort fortgesetzt, wo es aufgehört hat.

#### Dateisystem-Wiederherstellung auf Synology NAS

> VORSICHT: Die Wiederherstellung auf einem Synology erfordert Kenntnisse in Linux und Root-SSH-Zugriff auf das Synology-Gerät.
{.is-warning}

- Installieren Sie Sonarr neu (falls zutreffend / noch nicht installiert).
- Suchen Sie den Speicherort des AppData-Verzeichnisses für Sonarr heraus.
  - Führen Sie Sonarr einmal aus und gehen Sie über die Benutzeroberfläche zu System => About.
  - [Sonarr Appdata-Verzeichnis](/sonarr/appdata-directory)
- Beenden Sie Sonarr.
- Verbinden Sie sich über SSH mit dem Synology NAS und melden Sie sich als Root an.

> Bei einigen Installationen ist der Benutzername in den folgenden Befehlen unterschiedlich: `chown -R sc-Sonarr:Sonarr *` {.is-info}

- Führen Sie die folgenden Befehle aus:

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- Aktualisieren Sie die Berechtigungen für die Dateien:

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Starten Sie Sonarr.

## Hilfe, ich habe mich ausgesperrt

{#help-i-have-forgotten-my-password}

> Wenn Sie Sonarr v4 verwenden, ist der Authentifizierungstyp "None" nicht mehr gültig - siehe diese [FAQ](/sonarr/faq-v4) {.is-info}

Um die Authentifizierung zu deaktivieren (um Ihren vergessenen Benutzernamen oder Ihr vergessenes Passwort zurückzusetzen), müssen Sie die Datei `config.xml` bearbeiten, die sich im [Sonarr Appdata-Verzeichnis](/sonarr/appdata-directory) befindet.

1. Öffnen Sie config.xml in einem Texteditor.
1. Suchen Sie die Zeile mit der Authentifizierungsmethode: `<AuthenticationMethod>Basic</AuthenticationMethod>` oder `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Ändern Sie die Zeile `AuthenticationMethod` in `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Starten Sie Sonarr neu.
1. Sonarr ist jetzt ohne Passwort zugänglich. Gehen Sie in die Benutzeroberfläche zu "Einstellungen: Allgemein" und legen Sie Ihren Benutzernamen und Ihr Passwort fest.

## Warum gibt es zwei Dateien? \| Warum bleibt eine Datei im Download-Ordner?

Dies ist normal. Bei einer Konfiguration, die [Hardlinks](https://trash-guides.info/hardlinks) unterstützt, wird kein doppelter Speicherplatz verwendet. Hier ist, wie der Torrent-Prozess funktioniert:

1. Sonarr sendet eine Download-Anforderung an Ihren Client und ordnet sie einem Label oder Kategorienamen zu, den Sie in den Einstellungen des Download-Clients konfiguriert haben. Beispiele: Filme, TV, Serien, Musik usw.
1. Sonarr überwacht die aktiven Downloads Ihres Download-Clients, die diesen Kategorienamen verwenden. Diese Überwachung erfolgt über die API Ihres Download-Clients.
1. Abgeschlossene Dateien werden an ihrem ursprünglichen Speicherort belassen, damit Sie die Datei seeden können (das Verhältnis oder die Zeit können im Download-Client oder innerhalb des spezifischen Download-Clients angepasst werden). Wenn Dateien in Ihren Medienordner importiert werden, wird die Datei per Hardlink verknüpft, wenn dies von Ihrer Konfiguration unterstützt wird, oder kopiert, wenn Hardlinks nicht unterstützt werden.
1. Wenn die Option "Abgeschlossene Download-Verarbeitung - Abgeschlossene entfernen" in den Einstellungen von Sonarr aktiviert ist, löscht Sonarr die Originaldatei und den Torrent aus Ihrem Download-Client, aber nur, wenn der Download-Client meldet, dass das Seeden abgeschlossen ist und der Torrent angehalten ist (d. h. pausiert). Informationen zur optimalen Konfiguration Ihres Download-Clients finden Sie in den [Download-Client-Anleitungen von TRaSH](https://trash-guides.info/Downloaders/).

> Hardlinks sind standardmäßig aktiviert. [Ein Hardlink verwendet keinen zusätzlichen Speicherplatz](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/). Das Dateisystem und die Mounts müssen für das Verzeichnis der abgeschlossenen Downloads und Ihre Medienbibliothek gleich sein. Wenn die Erstellung des Hardlinks fehlschlägt oder Ihre Konfiguration keine Hardlinks unterstützt, wird die Datei kopiert.{.is-info}

## Ich sehe, dass das Feature/der Fehler X behoben wurde. Warum sehe ich es nicht?

Sonarr besteht aus zwei Hauptcodezweigen: `main` und `develop`.

- `main` wird regelmäßig veröffentlicht, wenn der `develop`-Zweig stabil ist.
- `develop` ist für Vorabtests und Benutzer gedacht, die gerne auf dem neuesten Stand sind. Wenn ein Feature als "develop" markiert ist, steht es nur Benutzern zur Verfügung, die den "develop"-Zweig ausführen. Sobald es in den Live-Bereich (in "main") verschoben wurde, wird es offiziell veröffentlicht.

## Episodenfortschritt - Wie wird er berechnet?

- Der Episodenfortschritt besteht aus zwei Teilen: der Anzahl der Episoden (Episode Count) und der Anzahl der Episoden mit Dateien (Episode File Count). Jeder Teil verwendet eine etwas andere Logik, um den Gesamtfortschritt einer Serie oder Staffel anzuzeigen.

  - Episode Count => Die Episode wurde bereits ausgestrahlt UND wird überwacht ODER - Die Episode hat eine Datei.
  - Episode File Count => Die Episode hat eine Datei.

- Wenn eine Serie 10 Episoden hat, die alle ausgestrahlt wurden und Sie keine Dateien dafür haben, hätten Sie 0/10 Episoden. Wenn Sie alle Episoden in dieser Serie nicht überwachen würden, hätten Sie 0/0, und wenn Sie alle Episoden für diese Serie erhalten würden, unabhängig davon, ob die Episoden überwacht werden oder nicht, hätten Sie 10/10 Episoden.

## Wie greife ich von einem anderen Computer auf Sonarr zu?

- Standardmäßig hört Sonarr nicht auf Anfragen von allen Systemen (wenn es nicht als Administrator ausgeführt wird), sondern nur auf localhost. Dies liegt daran, wie der von Sonarr verwendete Webserver in Windows integriert ist (dies gilt auch für aktuelle Alternativen). Wenn Sonarr als Administrator ausgeführt wird, registriert es sich korrekt bei Windows und öffnet den Firewall-Port, sodass es von anderen Systemen in Ihrem Netzwerk aus erreicht werden kann. Das Ausführen als Administrator muss nur einmal erfolgen (wenn Sie den Port ändern, muss es erneut ausgeführt werden).

## Warum aktualisiert Sonarr die Serieninformationen so häufig?

- Sonarr aktualisiert Serien- und Episodeninformationen zusätzlich zum erneuten Scannen der Festplatte nach Dateien alle 12 Stunden. Dies mag aggressiv erscheinen, ist aber ein sehr wichtiger Prozess. Die Aktualisierung der Daten von unserem TVDb-Proxy ist wichtig, da neue Episodeninformationen synchronisiert werden: Ausstrahlungsdaten, Anzahl der Episoden, Status (fortlaufend/beendet). Selbst Shows, die nicht ausgestrahlt werden, werden mit neuen Informationen aktualisiert.
- Der Festplattenscan ist weniger wichtig, wird jedoch verwendet, um nach neuen Dateien zu suchen, die nicht von Sonarr sortiert wurden, und um gelöschte Dateien zu erkennen.
- Der zeitaufwändigste Teil ist die Aktualisierung der Informationen (bei vernünftiger Festplattenzugriffsgeschwindigkeit). Größere Shows dauern länger aufgrund der Anzahl der zu verarbeitenden Episoden.

> Es ist nicht möglich, diese Aufgabe zu deaktivieren. Wenn diese Aufgabe lange genug ausgeführt wird, dass Sie der Meinung sind, dass sie das Problem verursacht, liegt ein anderes Problem vor, das gelöst werden muss, anstatt diese Aufgabe zu stoppen.
{.is-warning}

## Warum gibt es eine Zahl neben "Aktivität"?

- Diese Zahl zeigt die Anzahl der Episoden in der Warteschlange Ihres Download-Clients und die letzten 60 Elemente in der Historie, die noch nicht importiert wurden. Wenn die Zahl blau ist, funktioniert sie normal und sollte Episoden importieren, wenn sie abgeschlossen sind. Gelb bedeutet, dass eine Warnung für eine der Episoden vorliegt. Rot bedeutet, dass ein Fehler aufgetreten ist. Bei Gelb (Warnung) und Rot (Fehler) müssen Sie die Warteschlange unter "Aktivität" überprüfen, um das Problem zu sehen (bewegen Sie den Mauszeiger über das Symbol, um weitere Details zu erhalten).
- Sie müssen den Artikel aus der Warteschlange oder der Historie Ihres Download-Clients entfernen, um sie aus der Warteschlange von Sonarr zu entfernen.

## Was sind die verschiedenen Serientypen?

- Der Serientyp beeinflusst die Art und Weise, wie Sonarr nach Serien sucht. Ein Serientyp basiert darauf, wie die Serie in den Indexern veröffentlicht wird, und entspricht nicht unbedingt dem tatsächlichen "Typ" der Serie.
- Die meisten Shows sollten den Typ "Standard" haben. Für tägliche Shows, die normalerweise mit einem Datum veröffentlicht werden, sollte "Daily" verwendet werden. Schließlich gibt es Anime, bei dem "Anime" *in der Regel* richtig ist, aber manchmal kann "Standard" besser funktionieren, also probieren Sie den *anderen* aus, wenn Sie Probleme haben.
- Bitte beachten Sie, dass der Serientyp "Anime" keine Konzepte von Staffelpaketen oder Staffeln hat und jede Episode einzeln durchsucht wird.
- Bitte beachten Sie, dass nicht alle Indexer Staffel-/Episodensuchen (Standard) unterstützen.
- Die Serientypen können im Masseneditor oder in "Bearbeiten", wenn Sie eine Serie anzeigen, geändert werden. Beachten Sie, dass der Serientyp beim Import auswählbar ist.

- Wenn der **Anime**-Serientyp verwendet wird, ist es [möglich, dass Ihr Indexer auch mit dem Standardtyp durchsucht wird.](/sonarr/settings#indexers)

### Serientypen

- **Anime** - Episoden werden mit einer absoluten Episodennummer veröffentlicht.
- **Daily** - Episoden werden täglich oder seltener veröffentlicht und verwenden das Format Jahr-Monat-Tag (2017-05-25).
- **Standard** - Episoden werden im Format SxxEyy veröffentlicht.

### Beispiele für Serientypen

Nachfolgend finden Sie einige Beispiele für Veröffentlichungsnamen für jeden Serientyp. Das spezifische Unterscheidungsmerkmal ist fett hervorgehoben.

> Wenn der **Anime**-Serientyp verwendet wird, ist es [möglich, dass Ihr Indexer auch mit dem Standardtyp durchsucht wird.](/sonarr/settings#indexers)
{.is-info}

#### Daily

Die Protokolle zeigen "Suche in Indexern nach [The Witcher : 2021-12-20]"

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Die Protokolle zeigen "Suche in Indexern nach [The Witcher : S01E09]"

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Die Protokolle zeigen "Suche in Indexern nach [The Witcher : S01E09 (09)]"

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## Wie kann ich meine Serienordner umbenennen?

{#rename-folders}

> Derselbe Vorgang gilt auch für das Verschieben/Ändern von Serienpfaden{.is-info}

Wenn Sie das Format des Seriennamens angepasst haben, nachdem Sonarr bereits einige Serienordner erstellt hat, benennt Sonarr die vorhandenen Ordner nicht automatisch um. Um eine Umbenennung dieser Ordner auszulösen, sollten Sie die folgenden Schritte ausführen:

1. Serien
1. Masseneditor
1. Wählen Sie die Serien aus, deren Ordner umbenannt werden sollen.
1. Ändern Sie den Stammordner in denselben Stammordner, in dem sich die Serien bereits befinden.
1. Wählen Sie "Ja, Dateien verschieben", um

> Wenn Sie Plex oder Emby verwenden, wird dadurch die erneute Erkennung von Intros, Thumbnails, Kapiteln und Vorschaumetadaten ausgelöst.
{.is-warning}

## Wie aktualisiere ich Sonarr?

- Gehen Sie zu Einstellungen und dann zum Tab Allgemein und zeigen Sie erweiterte Einstellungen an (verwenden Sie den Umschalter neben der Speichern-Schaltfläche).

1. Ändern Sie unter dem Abschnitt Updates den Branch-Namen in `main` oder `develop`.
1. Speichern Sie.

*Dies installiert die Bits aus diesem Branch nicht sofort, sondern während des nächsten Updates.*

- main - ![Aktuelle Hauptversion/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Standard/Stabil): Dies wurde von Benutzern im Nightly (`develop`) Branch getestet und es sind keine größeren Probleme bekannt. Dieser Branch sollte von den meisten Benutzern verwendet werden. Auf GitHub ist dies der `main`-Branch.
- develop - ![Aktuelle Entwicklerversion/Nightly](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Instabil): Dies ist jetzt für Nicht-Docker-Benutzer dasselbe wie `main` und wahrscheinlich die letzte v3-Version.

> ~~**Warnung: Sie können möglicherweise nicht mehr zu `main` wechseln, nachdem Sie zu diesem Branch gewechselt sind.** Auf GitHub ist dies der `develop`-Branch.~~
{.is-danger}

- v4 develop - ![Aktuelle v4-Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Instabil): **Für Nicht-Docker-Benutzer ist der Branch `develop`, sobald v4 installiert ist. Für Docker-Benutzer handelt es sich wahrscheinlich um das Tag `develop`** Dies ist der Bleeding-Edge für Sonarr v4 Beta. Es wird veröffentlicht, sobald der Code überprüft und alle automatisierten Tests bestanden wurden. Dieses Build wurde möglicherweise noch nicht von uns oder anderen Benutzern verwendet. Es besteht keine Garantie, dass es in einigen Fällen überhaupt ausgeführt wird. Dieser Branch wird nur fortgeschrittenen Benutzern empfohlen. Probleme und Selbstuntersuchungen werden in diesem Branch erwartet. Auf GitHub ist dies der `develop`-Branch.

> **Warnung: Sie können nicht mehr zu (v3) `main` oder (v3) `develop` wechseln, nachdem Sie zum v4-Branch gewechselt sind, ohne eine v3-Sicherung wiederherzustellen und zu suchen.** Auf GitHub ist dies der `develop`-Branch.
{.is-danger}

> v3 **nicht-Docker**-Installationen können **nicht** direkt auf v4 aktualisiert werden und erfordern die Installation von Sonarr v4
{.is-info}

- Hinweis: Wenn Ihre Installation über Docker erfolgt, fügen Sie Ihrem Container-Tag `:release`, `:latest`, `:nightly` oder `:develop` hinzu, abhängig davon, wer Ihre Builds erstellt.

|                                                                    | `main` (stable) ![Aktuelle Haupt-/Neueste Version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Haupt&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (Beta) ![Aktuelle v3 Entwicklung/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Entwicklung&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 Beta) ![Aktuelle v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-Vorschau&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### Installation einer neueren Version

#### Native

1. Gehe zu System und dann zum Tab Updates.
1. Neuere Versionen, die noch nicht installiert sind, haben einen Update-Button neben sich. Durch Klicken auf diesen Button wird das Update installiert.

> v3 kann nicht auf Beta v4 aktualisiert werden und erfordert eine manuelle Installation. Siehe die [v4 Beta Ankündigung](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)
{.is-info}

#### Docker

1. Ziehe dein Tag erneut und aktualisiere deinen Container.

## Kann ich von `develop` zu `main` wechseln?

- Siehe den folgenden Eintrag

## Kann ich zwischen Branches wechseln?

> Du kannst (fast) immer dein Risiko erhöhen.{.is-info}

- `main` kann zu `develop` wechseln
- Siehe unten oder erkundige dich anderweitig beim Entwicklungsteam, ob du von `develop` zu `main` für deine spezifische Version wechseln kannst.
- Wenn diese Anweisungen nicht befolgt werden, kann es dazu führen, dass Sonarr nicht mehr funktioniert oder Fehler verursacht. Du wurdest gewarnt. Wenn die folgenden Fehlermeldungen auftreten, verwendest du eine neuere Datenbank mit einer älteren \*Arr-Version, die nicht unterstützt wird. Aktualisiere \*Arr auf die Version, die du zuvor verwendet hast oder eine neuere.
  - Beispiel-Fehlermeldungen:
    - `Fehler beim Parsen von Spalte 45 (Sprache=31 - Int64)`
    - `Der DataMapper konnte das folgende Feld nicht laden: 'Sprachen' Wert`
    - `ID stimmt nicht mit einer bekannten Sprache überein. Parametername: id`
    - Andere ähnliche Datenbankfehler bezüglich fehlender Spalten oder Tabellen.
- **Update vom 7. August 2022**
  - `3.0.9.1549` wurde als Haupt-/Stable-Version veröffentlicht
  - Für diejenigen, die sich in der Entwicklung befinden und immer noch `3.0.9.1549` oder eine ältere Version verwenden, können sicher auf `main` downgraden
  - Wenn du eine neuere Version verwendest, könntest du *möglicherweise* auf nightly/develop feststecken, bis eine neue stabile Version veröffentlicht wird. Wenn du ein Backup von vor dem Upgrade auf die oben genannte Version hast, kannst du es neu installieren und das Backup wiederherstellen. Erkundige dich beim Entwicklungsteam, ob du sicher downgraden kannst.

# Sonarr und Serienprobleme + Metadaten

## Wie geht Sonarr mit Problemen bei der Nummerierung von Episoden um (American Dad!, etc)?

### Wie Sonarr Probleme bei der Nummerierung von Episoden behandelt

- Sonarr verlässt sich auf [TheXEM](http://thexem.info/), eine von der Community betriebene Website, auf der Benutzer Zuordnungen von Shows erstellen können, die von der Szene (den Personen, die die Dateien veröffentlichen) und TheTVDb (die normalerweise der Nummerierung des Netzwerks folgt) abweichen. Es gibt bereits eine Reihe von Shows auf der Website, aber es ist einfach, eine weitere hinzuzufügen, und in der Regel werden die Änderungen innerhalb weniger Tage akzeptiert (wenn sie korrekt sind). TheXEM wird verwendet, um Unterschiede in der Episodennummerierung (Uneinigkeit, ob eine Episode eine Spezialfolge ist oder nicht) sowie Unterschiede in der Staffelnummerierung zu korrigieren, z. B. wenn Episoden als S10E01 veröffentlicht werden, TheTVDb jedoch dieselbe Episode als S2017E01 auflistet.
- XEM behebt in der Regel die Probleme, wenn die Nummerierung der Release-Gruppen (umgangssprachlich als "die Szene" bekannt) nicht mit der Nummerierung von TVDb übereinstimmt, sodass Sonarr nicht funktioniert. Hier kommt [XEM](http://thexem.info) ins Spiel, das eine Karte erstellt, auf die Sonarr zugreifen kann.
- Release-Gruppen verwenden eine Jahreszahl für die Staffel (S2010), während TVDb S01 verwendet.
- [XEM](http://thexem.info) funktioniert in den meisten Fällen und sorgt dafür, dass alles reibungslos läuft, ohne dass du es überhaupt bemerkst. Wie bei den meisten Dingen gibt es jedoch immer *problematische Ausnahmen* und in diesem Fall gibt es eine Liste davon.

> Bestimmte Indexer oder Release-Gruppen folgen möglicherweise TVDb anstelle von `Scene` (d. h. XEM).
> Wenn dies beobachtet wird, reiche sie bitte über das Scene-Mapping-Formular ein.
{.is-info}

- [Services Requested Mappings *Überprüfe und stelle sicher, dass der Alias und die Veröffentlichung nicht bereits angefordert oder hinzugefügt wurden*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Services Scene Mapping Request Form *Stelle eine neue Anfrage für einen Alias. Stelle sicher, dass das Formular vollständig ausgefüllt ist*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### Problematische Shows

> Dies ist keineswegs eine vollständige Liste von Shows, bei denen Probleme mit dem Scene-Mapping bekannt sind, aber dies sind einige gängige Beispiele.
{.is-info}

- Dies ist eine unvollständige Liste der bekannten Shows und warum sie problematisch sind:  
- American Dad {#problemshow-americandad}
  - Aufgrund von Änderungen der Staffelnummern durch das Netzwerk weicht American Dad in der Regel um 1 Staffel zwischen den Veröffentlichungen und TVDb ab. Weitere Details findest du in der XEM-Karte.
  - [American Dad](https://thexem.info/xem/show/4948) befindet sich derzeit auf S19 basierend auf TVDb oder S18 basierend auf der Szene zum Zeitpunkt des Schreibens. Wenn du in Sonarr nach Staffel 19 suchst, erhältst du **nur** Ergebnisse für Staffel 18 aufgrund der XEM-Karte.
  - Wenn du einen Indexer / eine Release-Gruppe mit Episoden der 19. Staffel hast, reiche sie bitte über das Scene-Mapping-Formular ein und stelle sicher, dass sie nicht bereits angefordert wurden
    - [Services Requested Mappings *Überprüfe und stelle sicher, dass der Alias und die Veröffentlichung nicht bereits angefordert oder hinzugefügt wurden*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Services Scene Mapping Request Form *Stelle eine neue Anfrage für einen Alias. Stelle sicher, dass das Formular vollständig ausgefüllt ist*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - Doppelfolgen-Dateien gegenüber einzelnen Episoden in TVDb, aber nicht alle Episoden sind Doppelfolgen, sodass die Zuordnung falsch sein kann, welche Episoden Doppelfolgen sind und welche nicht.
- Pokémon {#problemshow-pokemon}
  - Bei TheXem verfolgt [Pokemon](http://thexem.info/xem/show/4638) *synchronisierte* Episoden. Wenn du also untertitelte Episoden möchtest, hast du möglicherweise Pech. Wenn bestimmte Release-Gruppen TVDb folgen und nicht die XEM-Zuordnung, reiche sie bitte über das Scene-Mapping-Formular ein und stelle sicher, dass sie nicht bereits angefordert wurden
    - [Services Requested Mappings *Überprüfe und stelle sicher, dass der Alias und die Veröffentlichung nicht bereits angefordert oder hinzugefügt wurden*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Services Scene Mapping Request Form *Stelle eine neue Anfrage für einen Alias. Stelle sicher, dass das Formular vollständig ausgefüllt ist*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb hat die ursprüngliche Ausstrahlungsreihenfolge des spanischen Senders, aber Netflix hat die Rechte gekauft und die Serie in eine andere Episodenanzahl umgeschnitten. Dadurch wird "Staffel 5" über vorhandene "Staffel 3"-Episoden importiert. [Weitere Informationen findest du in diesem Reddit-Thread](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- Kamen Rider {#problemshow-kamenrider}
  - Der Anthologie-Eintrag ([TVDb ID 74096](https://thetvdb.com/series/kamen-rider)) sollte in Sonarr für die Automatisierung verwendet werden, da diese Show sowohl einen Anthologie-Eintrag (der alle Staffeln sammelt) als auch die einzelnen Staffeln als separate Einträge auf TVDb hat. Aufgrund der individuellen Staffelnamen-Zuordnungen des Anthologie-Eintrags auf [TheXEM](https://thexem.info/xem/show/5376) ist es nicht möglich, die einzelnen Staffeleinträge automatisch zu Sonarr hinzuzufügen, ohne Releases manuell herunterzuladen und zu importieren.
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - Die neueste Staffel von Bleach: Thousand-Year Blood War wird mit verschiedenen Benennungsschemata veröffentlicht, was die Automatisierung erschwert und möglicherweise einige deiner vorhandenen Episoden überschreibt. Die Automatisierung ist nur möglich, wenn deine Release-Gruppe entweder:
    - die Episoden mit der Nummerierung S17Exx veröffentlicht oder
    - sie mit dem korrekten Serientitel der zweiten Staffel veröffentlicht (hier zu finden <https://thexem.info/xem/show/5476>) und mit der absoluten Episodennummer 1 mit diesem neuen Handlungsstrang begonnen hat.
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys wurde zuerst als 20 kleinere Episoden ausgestrahlt, wurde jedoch später als 10 lange Episoden erneut ausgestrahlt. Diese längeren kombinierten Episoden wurden als Specials hinzugefügt und sollten entsprechend benannt werden (S00E01 usw.).
- Horizon {#problemshow-horizon}
  - Eine Show, die seit 1964 sporadisch Episoden ausstrahlt. Dies macht die Zuordnung besonders schwierig, wie du auf [TheXEM](https://thexem.info/xem/show/5495) sehen kannst. Interessierte können die ursprüngliche Diskussion im Sonarr-Discord [hier](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312) finden.
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023) wurde auf Netflix als nicht-lineare Show veröffentlicht, was bedeutet, dass jeder Benutzer eine andere Reihenfolge beim Anschauen der Serie erhalten hat. Dies führt bei Sonarr zu Problemen, da Release-Gruppen unterschiedliche Episodenreihenfolgen für die Show haben. Um eine falsche Zuordnung von Episoden zu verhindern, greift Sonarr nicht automatisch auf Episoden zu, und du musst die Episoden manuell herunterladen und importieren. Du kannst sie anhand des Episodentitels zuordnen oder die ersten paar Sekunden vorab anzeigen und die Farbe der Episode mit dem Titel abgleichen.

Einige Beispiele für andere Shows, die häufig Probleme haben und bei denen TheXEM-Mappings helfen können, sind: Arrested Development, Kitchen Nightmares (US), Mythbusters, Pawn Stars.

## Warum kann Sonarr keine Episoden für Serie X importieren? / Warum kann Sonarr keine Releases für Serie X finden?

Es gibt mehrere Gründe, warum Sonarr möglicherweise keine Episoden für eine bestimmte Serie finden oder importieren kann.

> Sonarr verwendet keine Aliase oder Übersetzungen (z. B. fremdsprachige Titel) von TVDb.
{.is-warning}

> **Für Indexer, die ID-basierte Suchen unterstützen**, werden die TVDbID oder IMDbID der Serie für die Suche verwendet. Serientitel und Aliase werden nur verwendet, wenn ID-basierte Suchen keine Ergebnisse liefern.
{.is-info}

- Sonarr basiert darauf, Titel abzugleichen. Oft verwenden die Uploader verschiedene Titel für Episoden, z. B. wird `CSI: Crime Scene Investigation` als `CSI` gepostet. Sonarr kann die Namen ohne Hilfe nicht abgleichen. Diese werden durch das Scene Mapping behandelt, das vom Sonarr-Team gepflegt wird.
- Sie können auch die [FAQ-Einträge zu problematischen Shows und Release-Gruppen im Vergleich zur TVDb-Nummerierung](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc) überprüfen.

> **Für alle japanischen Animes müssen Aliase zu [thexem.info](https://thexem.info) hinzugefügt werden**. Um für andere Serien eine neue Zuordnung anzufordern, befolgen Sie die unten stehenden Schritte. Weitere Informationen finden Sie bei einigen XEM-Leuten im #XEM-Discord-Kanal auf dem Sonarr-Discord.
{.is-danger}

- [Dienste angeforderte Zuordnungen *Überprüfen Sie, ob der Alias und das Release nicht bereits angefordert oder hinzugefügt wurden*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Dienste Scene Mapping-Anforderungsformular *Erstellen Sie eine neue Anforderung für einen Alias. Stellen Sie sicher, dass das Formular vollständig ausgefüllt ist*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> In der Regel werden Dienstanfragen innerhalb von 1-5 Tagen hinzugefügt.
{.is-info}

> Fordern Sie keine Zuordnung für japanische Animes an. Verwenden Sie dafür XEM.
> Weitere Informationen finden Sie bei einigen XEM-Leuten im [\#XEM-Discord-Kanal auf dem Sonarr-Discord](https://discord.gg/Z3D6u5hBJb).
{.is-danger}

> Wenn eine nicht-japanische Serie eine Season-Zuordnung erfordert (z. B. veröffentlicht als S25E26, aber TVDB ist S26E2), ist eine XEM-Zuordnung erforderlich. Dies kann nicht mit einer Dienstzuordnung erfolgen.
{.is-info}

> Die Serie "Helt Perfekt" mit den TVDb-IDs `343189` und `252077` ist aufgrund der Tatsache, dass TVDb für beide Shows denselben Namen hat und damit gegen die eigenen Regeln von TVDb verstößt, schwer zu automatisieren. Der erste Eintrag für die Serie erhält den Namen. Alle zukünftigen Einträge für die Serie müssen das Jahr als Teil des Seriennamens enthalten. Es wurde jedoch eine Ausnahme für die Szene hinzugefügt, um Releases (Groß- und Kleinschreibung beachten) von Helt Perfekt zuzuordnen, die `NORWEGIAN` enthalten -\> `252077` und die `SWEDISH` enthalten -\> `343189`
{.is-info}

## TVDb wurde aktualisiert, warum nicht Sonarr?

{#tvdb}

- TVDb hat einen 24-Stunden-Cache auf ihrer API.
- Die TVDb-API muss dann über den CDN-Cache verbreitet werden, was mehrere Stunden dauert.
- Sonarrs Skyhook hat zusätzlich dazu einen viel kleineren Cache von wenigen Stunden.
- Darüber hinaus führt Sonarr die Aktualisierung der Serienaufgabe nur alle 12 Stunden durch. Diese Aufgabe kann manuell von System => Aufgaben aus gestartet werden; "Alle aktualisieren" aus dem Serienindex oder manuell für eine bestimmte Serie auf der Seite dieser Serie gestartet werden.

- Daher dauert es in der Regel zwischen 36 und 48 Stunden (24 + ~3 + ~3 + 12), bis eine Änderung auf TVDb automatisch in Sonarr übernommen wird.

- Wenn eine Serie oder Episoden auf TVDb fehlen, dauert es 36 bis 48 Stunden, bis sie nach ihrer Hinzufügung in Ihrer Sonarr-Instanz angezeigt werden.

{#missing-episodes}

- Wenn Sie wissen, dass eine TVDb-Aktualisierung vor mehr als 48 Stunden erfolgt ist, besprechen Sie dies bitte in unserem [Discord](https://discord.sonarr.tv/).

## Warum kann ich keine Serie hinzufügen?

{#why-can-i-not-add-a-new-series}

- Wenn TheTVDb nicht verfügbar ist, kann Sonarr keine Suchergebnisse abrufen und Sie können keine neuen Serien durch Suche hinzufügen. Sie können eine neue Serie über die TVDbID hinzufügen, wenn Sie diese kennen. Die Benutzeroberfläche erklärt, wie Sie sie über eine ID hinzufügen können.
- Sonarr kann keine Serien hinzufügen, die keinen englischen Titel haben. Wenn Sie versuchen, eine Serie über die TVDbID hinzuzufügen, die keinen englischen Titel hat, wird die Serie nicht gefunden. Wenn für diese Serie kein englischer Titel auf TheTVDb vorhanden ist, muss er hinzugefügt werden und dann [muss man auf die Löschung des Caches von TVDb warten](#tvdb).
- Die Show muss eine TV-Serie sein und darf kein Film sein. Sie muss auch auf TVDb existieren. Wenn sie auf IMDB, TMDB oder irgendwo anders, aber nicht auf TVDb vorhanden ist, können Sie die Show nicht hinzufügen.
- Die Serie muss auf TVDb existieren.
- Bestimmte Serien können tatsächlich als Fortsetzungen und Staffeln in ihrer Hauptserie betrachtet werden.
  - Einige bekannte Serien/Staffeln sind:
  - [Dexter New Blood war Staffel 9](https://thetvdb.com/series/dexter/seasons/official/9), aber es ist jetzt [eine eigene Serie](https://thetvdb.com/series/dexter-new-blood)

## Warum kann ich keine Serie hinzufügen, wenn ich die TVDb-ID kenne?

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr kann keine Serien hinzufügen, die keinen englischen Titel haben. Wenn Sie versuchen, eine Serie über die TVDbID hinzuzufügen, die keinen englischen Titel hat, wird die Serie nicht gefunden. Wenn für diese Serie kein englischer Titel auf TheTVDb vorhanden ist, muss er hinzugefügt werden (falls verfügbar).
- Überprüfen Sie die URL / Serie - Sonarr unterstützt keine Filme; verwenden Sie [Radarr](/radarr) für Filme

## Titel-Slug wird bereits verwendet

- Es gibt zwei Hauptursachen für diesen Fehler, die unten aufgeführt sind.

## Doppelte Namen ohne Jahr

- Dieser Fehler tritt häufig auf, wenn zwei Serien auf TheTVDB denselben Titel haben. In diesem Fall sollte der zweiten Serie das Jahr zum Serientitel hinzugefügt werden.
  - Serie A
  - Serie A (2021)
- Um dies zu beheben, warten Sie darauf, dass jemand irgendwann (vielleicht) TVDb aktualisiert oder aktualisieren Sie TVDb selbst. Sobald dies korrigiert ist **und sobald es von den Moderatoren von TVDb genehmigt wurde**, aufgrund der [API-Probleme von TVDb](#tvdb-is-updated-why-isnt-sonarr) müssen Sie nach der Aktualisierung 30+ Stunden warten, bevor der korrigierte Titel in Sonarr verwendet werden kann.

## Doppelte Namen mit Interpunktion

- Es tritt auch auf, wenn zwei ähnlich benannte Serien nur durch Interpunktion unterschieden werden. Wenn dies der Fall ist, melden Sie dies bitte im [Sonarr-Discord](https://discord.sonarr.tv/).
  - Joe's Show (2022)
  - Joes Show (2022)

## Episode hat keine absolute Nummer

- Die Episode(n) auf TVDb haben keine absolute Nummer zugewiesen. Aktualisieren Sie die Serie auf TVDb, wenn erforderlich, und warten Sie dann 36-48 Stunden, bis das Update den internen Cache von TVDb gelöscht und in Sonarr geladen hat.

## Episoden-Ausstrahlungszeiten

- In Sonarr basieren die angezeigten Episoden-Ausstrahlungsdaten und -zeiten im Browser auf der Zeit/Zeitzone des Clients. Alle Zeiten werden von Sonarr als UTC-Zeiten (im ISO-8601-Format) an den Browser gesendet.
- TVDb gibt vor - mit Ausnahmen für Streaming-Dienste - dass die Ausstrahlungszeit und das Datum auf der lokalen Zeit des Hauptausstrahlungsnetzwerks in der beliebtesten Stadt des Landes basieren. [Weitere Informationen finden Sie in der FAQ von TVDb](https://support.thetvdb.com/kb/faq.php?id=29)
- Die Ausstrahlungsdaten und -zeiten der Episoden auf TVDb werden in UTC umgerechnet und verwenden die Zeitzone von Sonarr, die im Skyhook vom Sonarr-Team für das Netzwerk, das TVDb für die Serie hat, zugeordnet ist.
  - Im seltenen Fall, dass ein Netzwerk nicht zugeordnet ist, wird die Zeit in TVDb als US EST (UTC-5) angenommen.
  - Wenn die Ausstrahlungszeit beim Umrechnen von der Ausstrahlungszeit der Netzwerk-Zeitzone in die Zeitzone Ihres Browsers nicht zu stimmen scheint, liegt es wahrscheinlich daran, dass das Netzwerk im Skyhook zugeordnet werden muss. [Kontaktieren Sie das Entwicklungsteam auf Discord](https://discord.sonarr.tv/), um Unterstützung bei der Aktualisierung der Netzwerk-Zeitzone zu erhalten.

# Häufige Probleme mit Sonarr

## Der Pfad ist bereits für eine vorhandene Serie konfiguriert

- Die Bibliotheksimporthilfe zeigt "Vorhanden" an oder es wird ein Fehler "Der Pfad ist für eine vorhandene Serie konfiguriert" angezeigt.
- Dies tritt auf, wenn Sie versuchen, eine Serie hinzuzufügen oder den Pfad einer vorhandenen Serie zu bearbeiten, der bereits einer anderen Serie zugewiesen ist.
- Wahrscheinlich wurde dies verursacht, indem eine nicht übereinstimmende Serie nicht korrigiert wurde, als der Benutzer seine Bibliothek importiert hat.
- Suchen und korrigieren Sie den Film, der bereits diesem Pfad der Serie zugewiesen ist.
  - Serienindex
  - Tabellenansicht
  - Optionen => Pfad als Spalte hinzufügen
  - Sortieren und den Film am angegebenen problematischen Pfad finden.
- Alternativ können Sie die Serie mit dem vorhandenen Pfad aus Sonarr löschen

## System & Logs lädt endlos

- Das liegt an der Easy-Privacy-Blockliste. Sie blockiert im Grunde genommen jede URL mit /api/log? darin. Überprüfen Sie die Liste und überlegen Sie, ob Sie es für sinnvoll halten, alle URLs in dieser Liste zu blockieren. Es gibt Dutzende von URLs in dieser Liste, die potenziell Websites beschädigen können. Sie haben das in Ihrem Adblocker ausgewählt. Die einfache Lösung besteht darin, die Domain, auf der Sonarr läuft, auf die Whitelist zu setzen. Ich empfehle jedoch, die Liste zu überprüfen.

## Seltsame UI-Probleme

- Wenn Sie seltsame UI-Probleme haben, z. B. dass die Bibliotheksseite nichts auflistet oder eine bestimmte Ansicht oder Sortierung nicht funktioniert, versuchen Sie es in einem Chrome-Inkognito-Fenster oder Firefox-Privatfenster. Wenn es dort einwandfrei funktioniert, löschen Sie den Browser-Cache und die Cookies für Ihre spezifische IP-/Domain. Weitere Informationen finden Sie im Wiki-Artikel [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage).

## Die Web-Benutzeroberfläche lädt nur lokal auf Windows

- Wenn Sie Ihre Web-Benutzeroberfläche nur unter <http://localhost:8989/> oder <http://127.0.0.1:8989> erreichen können, müssen Sie Sonarr mindestens einmal als Administrator ausführen.

## Ich habe einen Pop-up-Fehler, der besagt, dass config.xml beschädigt ist, was nun?

- Sonarr konnte Ihre Konfigurationsdatei beim Start nicht lesen, da sie aus irgendeinem Grund beschädigt wurde. Um Sonarr wieder online zu bringen, müssen Sie `.xml` in Ihrem [AppData-Ordner](/sonarr/appdata-directory) löschen. Starten Sie dann Sonarr und es wird auf dem Standardport (8989) gestartet. Sie sollten nun alle Einstellungen erneut konfigurieren, die Sie auf der Seite "Allgemeine Einstellungen" konfiguriert haben.

## Ungültiges Zertifikat und andere HTTPS- oder SSL-Probleme

- Wenn Sie kein Windows verwenden, sind höchstwahrscheinlich die Zertifikate Ihres Mono veraltet und müssen synchronisiert werden. [Weitere Informationen finden Sie im Abschnitt über Mono-SSL im Installationsartikel](/sonarr/installation#mono-ssl-issues)
- Ihr Download-Client funktioniert nicht mehr und Sie erhalten einen Fehler wie "Localhost ist ein ungültiges Zertifikat"?
  - Sonarr überprüft jetzt SSL-Zertifikate. Wenn im Download-Client kein SSL-Zertifikat festgelegt ist oder Sie ein selbstsigniertes HTTPS-Zertifikat ohne das CA-Zertifikat verwenden, das in Ihrem lokalen Zertifikatsspeicher hinzugefügt wurde, wird Sonarr die Verbindung ablehnen. Kostenlose ordnungsgemäß signierte Zertifikate sind von [Let's Encrypt](https://letsencrypt.org/) erhältlich.
  - Wenn Ihr Download-Client und Sonarr auf demselben Computer ausgeführt werden, besteht kein Grund, HTTPS zu verwenden. Die einfachste Lösung besteht darin, SSL für die Verbindung zu deaktivieren. Die meisten würden zustimmen, dass es auch in einem lokalen Netzwerk nicht erforderlich ist. Es ist möglich, die Zertifikatsprüfung in den erweiterten Einstellungen zu deaktivieren, wenn Sie eine unsichere SSL-Konfiguration beibehalten möchten.

## Wie verhindere ich, dass der Browser beim Start geöffnet wird?

Je nach Betriebssystem gibt es mehrere mögliche Lösungen.

- In `Einstellungen` => `Allgemein` gibt es in einigen Betriebssystemen ein Kontrollkästchen zum Öffnen des Browsers beim Start.
- Beim Aufrufen von Sonarr können Sie `-nobrowser` (*nix) oder `/nobrowser` (Windows) zu den Argumenten hinzufügen.
- Beenden Sie Sonarr und bearbeiten Sie die Datei config.xml und ändern Sie `<LaunchBrowser>True</LaunchBrowser>` in `<LaunchBrowser>False</LaunchBrowser>`.

## VPNs, Jackett und die \*ARRs

- Sofern Sie sich nicht in einem repressiven Land wie China, Australien oder Südafrika befinden, muss Ihr Torrent-Client in der Regel das einzige sein, das sich hinter einem VPN befinden muss. Da der VPN-Endpunkt von vielen Benutzern gemeinsam genutzt wird, können Sie Geschwindigkeitsbegrenzungen, DDOS-Schutz und IP-Sperren von verschiedenen Diensten, die jede Software verwendet, erleben und erfahren.
- Mit anderen Worten, das Hinterlegen der \*Arrs (Lidarr, Prowlarr, Radarr, Readarr und Lidarr) hinter einem VPN kann dazu führen, dass die Anwendungen in einigen Fällen aufgrund der Nichterreichbarkeit der Dienste nicht verwendbar sind.

> **Um es klar zu sagen, es geht nicht darum, ob VPNs Probleme mit den \*Arrs verursachen, sondern wann: Bildanbieter werden Sie blockieren und Cloudflare befindet sich vor den meisten \*Arr-Servern (Updates, Metadaten usw.) und wird Sie ebenfalls blockieren**
{.is-warning}

- **Viele private Tracker werden Sie für die Verwendung oder den Zugriff auf sie (d. h. die Verwendung von Jackett oder Prowlarr) über ein VPN sperren.**

### Verwendung eines VPN

- Wenn ein VPN erforderlich ist und Docker verwendet wird, wird empfohlen, die Download-Client + VPN-Container von Hotio oder Binhex zu verwenden.
- Wenn ein VPN erforderlich ist und Docker nicht verwendet wird, muss Ihr VPN-Client ***Split-Tunneling*** unterstützen, damit nur die erforderlichen (Download-Client-)Apps hinter dem VPN liegen.
- Viele Probleme beim Zugriff auf Tracker können behoben werden, indem Sie die DNS-Server von Google oder Cloudflare anstelle der DNS-Server Ihres Internetdienstanbieters verwenden.
- In einigen Fällen (z. B. bei britischen ISPs) müssen Sie Ihren Torrent-Download-Client hinter einem VPN und Jackett/Prowlarr wie folgt platzieren:
  - Setzen Sie Jackett hinter das VPN und stellen Sie sicher, dass Split-Tunneling den lokalen Zugriff zulässt.
  - Für Prowlarr konfigurieren Sie Ihren VPN-Client so, dass er einen Proxy bereitstellt, und fügen Sie den Proxy in Einstellungen => Indexer hinzu. Geben Sie dem Proxy einen Tag und weisen Sie allen Indexern, die ihn verwenden müssen, denselben Tag zu.
    - Wenn es unbedingt erforderlich ist und Ihr VPN keine Möglichkeit bietet, einen Proxy zu erstellen, können Sie Prowlarr hinter das VPN stellen und sicherstellen, dass Split-Tunneling den lokalen Zugriff zulässt.

## Ich sehe Protokollnachrichten für Shows, die ich nicht habe/nicht haben möchte

- Diese Nachrichten sind völlig normal und stammen aus den RSS-Feeds, die Sonarr überprüft, um festzustellen, ob es Episoden gibt, die Sie möchten. Normalerweise erscheinen diese nur im Debug-/Trace-Protokoll, aber bei Problemen bei der Verarbeitung eines Elements können Sie eine Warnung oder einen Fehler sehen. Es ist sicher, die Warnungen/Fehler zu ignorieren, da sie für Shows sind, die Sie nicht möchten. Wenn es sich um eine Show handelt, die Sie möchten, eröffnen Sie einen Support-Thread in den Foren.

## Seeding-Torrents werden nicht automatisch gelöscht

- Wenn ein Torrent, der noch gepeert wird, importiert wird, wird er kopiert oder hart verlinkt (wenn aktiviert und *möglich*), damit der Torrent-Client weiterhin peert. In einer idealen Konfiguration befinden sich der Torrent-Download-Ordner und der Bibliotheksordner auf demselben Dateisystem und *sehen so aus* (Docker und Netzwerkfreigaben machen es leicht, dies falsch zu machen), was das Erstellen von Hartlinks ermöglicht und den verschwendeten Speicherplatz minimiert.
- Darüber hinaus können Sie Ihre Ziele für die Seed-Zeit/-Verhältnis in Sonarr oder Ihrem Download-Client konfigurieren, Ihren Download-Client so einrichten, dass er *pausiert* oder *gestoppt* wird, wenn diese Ziele erreicht sind, und unter Abgeschlossenem und Fehlgeschlagenem Download-Handler die Option "Entfernen" aktivieren. Auf diese Weise werden Torrents, die mit dem Peeren fertig sind, von Sonarr aus dem Download-Client entfernt.

## Hilfe, mein Mac sagt, Sonarr kann nicht geöffnet werden, weil der Entwickler nicht überprüft werden kann

- Das ist einfach, bitte sehen Sie sich diesen Link für weitere Informationen [hier](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
[![Entwickler kann nicht überprüft werden](/assets/general/faq_1_mac.png)]

## Hilfe, mein Mac sagt, Sonarr.app ist beschädigt und kann nicht geöffnet werden

- Das liegt entweder an einem beschädigten Download, also versuchen Sie es erneut, oder [an Sicherheitsproblemen, bitte sehen Sie sich diesen verwandten FAQ-Eintrag an.](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Ich erhalte einen Fehler: Datenbank-Datenträgerabbild ist beschädigt

> Sie können dies nach dem Upgrade von sqlite3 auf 3.41 erhalten. Sonarr v3.0.9 unterstützt sqlite3 3.41 aufgrund einer brechenden Standardänderung nicht. [Details zum Problem finden Sie in Sonarr GHI #5464](https://github.com/Sonarr/Sonarr/issues/5464)
> Dies ist mit Sonarr v3.0.10 behoben und Benutzer sollten Sonarr entsprechend aktualisieren.
{.is-warning}

- **Fehler bei `Fehler beim Erstellen der Protokolldatenbank` deuten auf Probleme mit logs.db hin**
  - Dieses Problem kann schnell behoben werden, indem die Datenbank umbenannt oder entfernt wird. Die Protokolldatenbank enthält unwichtige Informationen über den Befehlsverlauf, die Update-Installationshistorie sowie Info-, Warn- und Fehlermeldungen.
- **Fehler bei `Fehler beim Erstellen der Hauptdatenbank` oder allgemeine `Datenbankdiskimage ist beschädigt` ohne spezifizierte Datenbank deuten auf Probleme mit sonarr.db hin**
  - Fahren Sie mit den unten angegebenen Schritten fort.
- Dies bedeutet, dass Ihre SQLite-Datenbank, die die meisten Informationen für Sonarr speichert, beschädigt ist. Ihre Optionen bestehen darin, (eine) Sicherung(en) zu versuchen, die vorhandene Datenbank wiederherzustellen, die Sicherung(en) wiederherzustellen oder im schlimmsten Fall mit einer neuen frischen Datenbank neu zu beginnen.
- Dieser Fehler kann auftreten, wenn die Datenbankdatei vom Benutzer/der Benutzergruppe, unter der \*Arr ausgeführt wird, nicht beschreibbar ist. Berechtigungen sind wahrscheinlich nur ein Problem bei neuen Installationen, migrierten Installationen auf einem neuen Server, wenn Sie kürzlich die Berechtigungen für Ihr AppData-Verzeichnis geändert haben oder wenn Sie den Benutzer und die Gruppe geändert haben, unter der \*Arr ausgeführt wird.
- Ihre beste und erste Option besteht darin, [versuchen Sie, eine Sicherung wiederherzustellen](#wie-sichere-ich-mein-sonarr).
- Sie können auch versuchen, Ihre Datenbank wiederherzustellen. Dies ist in der Regel die einzige Option, wenn dieses Problem nach einem Update auftritt. Versuchen Sie den [sqlite3 `.recover` Befehl](/useful-tools#recovering-a-corrupt-db).
  - Wenn Ihr sqlite nicht über `.recover` verfügt oder Sie eine benutzerfreundlichere GUI (z. B. Windows) wünschen, befolgen Sie [unsere Anweisungen in diesem Wiki](/useful-tools#recovering-a-corrupt-db-ui).
- Eine weitere mögliche Ursache für einen Fehler in Ihrer Datenbank ist, dass Sie Ihre Datenbank auf einem Netzlaufwerk (NFS oder SMB oder etwas anderem, das nicht lokal ist) platzieren. **SQLite ist für Situationen ausgelegt, in denen Daten und Anwendung auf demselben Computer vorhanden sind.** Daher muss sich Ihr \*Arr AppData-Ordner (/config mount für Docker) auf lokalem Speicher befinden. [SQLite und Netzlaufwerke vertragen sich nicht gut und führen letztendlich zu einer beschädigten Datenbank](https://www.sqlite.org/draft/useovernet.html).
- Wenn Sie mergerFS verwenden, müssen Sie `direct_io` entfernen, da SQLite mmap verwendet, das von `direct_io` nicht unterstützt wird, wie in den mergerFS [Dokumenten hier](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs) erklärt.

## Ich verwende Sonarr auf einem Mac und es funktioniert plötzlich nicht mehr. Was ist passiert?

- Wahrscheinlich liegt dies an einem MacOS-Bug, der dazu geführt hat, dass eine der Sonarr-Datenbanken beschädigt wurde.
- [Befolgen Sie diese Schritte, um das Problem zu beheben](#ich-erhalte-einen-fehler-datenbankdiskimage-ist-beschädigt).
- Versuchen Sie dann, Sonarr zu starten und prüfen Sie, ob es funktioniert. Wenn es nicht funktioniert, benötigen Sie weitere Unterstützung. Posten Sie in unserem [Reddit](http://reddit.com/r/Sonarr) oder kommen Sie auf [Discord](https://discord.sonarr.tv/) für Hilfe.

## Warum kann Sonarr meine Dateien auf einem Remote-Server nicht sehen?

- Stellen Sie für alle Betriebssysteme sicher, dass der Benutzer/die Benutzergruppe, unter der \*Arr ausgeführt wird, Lese- und Schreibzugriff auf das eingebundene Laufwerk hat.
- Für Linux stellen Sie sicher:
  - Wenn Sie ein NFS-Laufwerk verwenden, stellen Sie sicher, dass `nolock` für Ihr Laufwerk aktiviert ist.
  - Wenn Sie ein SMB-Laufwerk verwenden, stellen Sie sicher, dass `nobrl` für Ihr Laufwerk aktiviert ist.
- Für Windows: Kurz gesagt, der Benutzer, unter dem \*Arr ausgeführt wird (wenn Dienst) oder der Benutzer, unter dem \*Arr ausgeführt wird (wenn Tray-App), kann nicht auf den Dateipfad auf dem Remote-Server zugreifen. Dies kann verschiedene Gründe haben, aber das häufigste ist, dass \*Arr als Dienst ausgeführt wird, was zu den unten beschriebenen Problemen führt.

### Sonarr wird standardmäßig unter dem LocalService-Konto ausgeführt, das keinen Zugriff auf geschützte Remote-Dateifreigaben hat

- Führen Sie den Sonarr-Dienst als anderen Benutzer aus, der Zugriff auf diese Freigabe hat.
- Öffnen Sie das Fenster "Verwaltungstools" \> "Dienste" auf Ihrem Windows-Server.
- Stoppen Sie den Sonarr-Dienst.
- Öffnen Sie den Dialog "Eigenschaften" \> "Anmelden".
- Ändern Sie das Benutzerkonto des Dienstes auf das Zielbenutzerkonto.
- Führen Sie Sonarr.exe über den Startordner aus.

### Sie verwenden ein zugeordnetes Netzlaufwerk (kein UNC-Pfad)

- Ändern Sie Ihre Pfade in UNC-Pfade (`\\Server\Freigabe`).
- Führen Sie Sonarr.exe über den Startordner aus.

## Zugeordnete Netzlaufwerke vs. UNC-Pfade

- Die Verwendung von zugeordneten Netzlaufwerken funktioniert im Allgemeinen nicht sehr gut, insbesondere wenn Sonarr so konfiguriert ist, dass es als Dienst ausgeführt wird. Der bessere Weg, Freigaben einzurichten, besteht darin, UNC-Pfade zu verwenden. Verwenden Sie also anstelle von `X:\TV` den Pfad `\\Server\TV`.

- Ein wichtiger Punkt, der zu beachten ist, ist, dass Sonarr Pfadinformationen vom Downloader erhält. Sie müssen also auch Ihren NZBGet, SABNzbd oder jeden anderen Downloader so einrichten, dass er ebenfalls UNC-Pfade verwendet.

## Sonarr funktioniert nicht unter Big Sur

Führen Sie den folgenden Befehl aus:

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## Mein benutzerdefiniertes Skript funktioniert nach dem Upgrade von v2 nicht mehr

- Wahrscheinlich haben Sie Argumente in Ihrer Verbindung übergeben, was nicht unterstützt wird.
- Um dies zu korrigieren:
  1. Ändern Sie Ihr Argument in Ihren Pfad.
  1. Stellen Sie sicher, dass der Shebang in Ihrem Skript auf Ihren pwsh-Pfad verweist (wenn Sie keine Shebang-Definition darin haben, fügen Sie sie hinzu).
  1. Stellen Sie sicher, dass das pwsh-Skript ausführbar ist.

# Häufige Probleme bei der Suche und dem Download in Sonarr

## Erfolgreiche Abfrage - Keine Ergebnisse zurückgegeben

- [Siehe diesen Fehlerbehebungseintrag](/sonarr/troubleshooting#query-successful-no-results-returned)

## Warum hat Sonarr eine erwartete Episode nicht heruntergeladen?

Stellen Sie zunächst sicher, dass Sie den Abschnitt oben mit dem Titel "Wie findet Sonarr Episoden?" gelesen und verstanden haben. Stellen Sie dann sicher, dass mindestens einer Ihrer Indexer die erwartete Episode zum Herunterladen hat.

1. Klicken Sie auf das Symbol "Manuelle Suche" neben der Episodenliste in Sonarr. Gibt es Ergebnisse? Wenn nicht, hat Sonarr entweder Probleme bei der Kommunikation mit Ihren Indexern, Ihre Indexer haben die Episode nicht oder die Episode ist auf dem Indexer falsch benannt/kategorisiert.
1. **Wenn es Ergebnisse aus Schritt 1 gibt**, überprüfen Sie sie auf das rote Ausrufezeichen-Symbol. Fahren Sie mit der Maus über das Symbol, um zu sehen, warum diese Veröffentlichung nicht für automatische Downloads in Frage kommt. Wenn jedes Ergebnis das Symbol hat, wird kein automatischer Download durchgeführt.
1. **Wenn es mindestens ein gültiges manuelles Suchergebnis aus Schritt 2 gibt**, sollte ein automatischer Download stattgefunden haben. Wenn dies nicht der Fall ist, ist die wahrscheinlichste Ursache ein vorübergehendes Kommunikationsproblem, das ein RSS-Sync von Ihrem Indexer verhindert. Es wird empfohlen, mehrere Indexer einzurichten, um optimale Ergebnisse zu erzielen.
1. **Wenn es kein manuelles Ergebnis von einer Show gibt, Sie es jedoch auf der Website Ihres Indexers finden können** - Dies kann verschiedene Gründe haben, zum Beispiel ist die Veröffentlichung auf Ihrem Indexer nicht ordnungsgemäß getaggt, sodass sie bei einer automatischen Suche nicht an Sonarr zurückgegeben wird. Dieser [Fehlerbehebungseintrag](/sonarr/troubleshooting#searches-indexers-and-trackers) bietet einige Tipps zur Ermittlung der Ursache. Durch das Aktivieren mehrerer Indexer können Sie dieses Problem lösen, indem Sie mehr Quellen für denselben Inhalt bereitstellen.

## Gefundene übereinstimmende Serie über die Grab-Historie, aber die Veröffentlichung wurde anhand der Serien-ID zugeordnet. Automatischer Import ist nicht möglich

- Siehe [diesen Fehlerbehebungseintrag](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- Auf TVDb werden Episodennamen mit "TBA" (To Be Announced) bezeichnet, wenn sie unbekannt sind, und die TVDb-API hat einen 24-Stunden-Cache. Änderungen auf der TVDb-Website dauern in der Regel 24-48 Stunden, um bei Sonarr anzukommen, aufgrund des TVDb-Caches (24 Stunden), des Skyhook-Caches (einige Stunden) und des Aktualisierungsintervalls der Serie (alle 12 Stunden). Die [Einstellung "Erforderlicher Episodentitel"](https://sonarr.tv/settings#importing) in Sonarr steuert das Importverhalten, wenn der Titel "TBA" ist, aber nach 48 Stunden nach der Ausstrahlung der Serie wird die Veröffentlichung importiert, auch wenn der Titel immer noch "TBA" ist. Es erfolgt auch keine automatische Umbenennung von Dateien mit dem Titel "TBA". Beachten Sie, dass der TBA-Timer ab dem Ausstrahlungsdatum und der -zeit der Episode berechnet wird, nicht ab dem Zeitpunkt, zu dem Sie sie heruntergeladen oder hochgeladen haben.

## Sonarr zeigt bei Suchen oder Importen unbekannte Serie an

- Siehe den Eintrag [Warum kann Sonarr keine Episodendateien für Serie X importieren? / Warum kann Sonarr keine Veröffentlichungen für Serie X finden?](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)

## Jackett's /all-Endpunkt

{#jackett-all-endpoint}

- Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es erforderlich, jeden Tracker einzeln hinzuzufügen. Alternativ können Sie sich die Jackett & NZBHydra2-Alternative [Prowlarr](/prowlarr) ansehen.

- **Update vom 5. Februar 2022: Die Unterstützung für den Jackett `\all`-Endpunkt wurde eingestellt. Der Jackett /all-Endpunkt wird ab v3.0.6.1457 nicht mehr unterstützt (Warnungen werden angezeigt), da er nur Probleme verursacht.**

- Der Jackett `/all`-Endpunkt ist praktisch, aber das ist sein einziger Vorteil. Alles andere birgt potenzielle Probleme, daher ist es jetzt erforderlich, jeden Tracker einzeln hinzuzufügen.
- [Sogar die Entwickler von Jackett sagen, dass er vermieden und nicht verwendet werden sollte.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Die Verwendung des /all-Endpunkts hat keine Vorteile, nur Nachteile:
  - Sie verlieren die Kontrolle über indexer-spezifische Einstellungen (Kategorien, Suchmodi usw.).
  - Das Mischen von Suchmodi (IMDB, Abfrage usw.) kann zu Ergebnissen von geringer Qualität führen.
  - Indexer-spezifische Kategorien (\>= 100000) können nicht verwendet werden.
  - Langsame Indexer verlangsamen das Gesamtergebnis.
  - Die Gesamtzahl der Ergebnisse ist auf 1000 begrenzt.
  - Wenn einer der Tracker in /all einen Fehler zurückgibt, wird \*Arr ihn deaktivieren und Sie erhalten keine Ergebnisse mehr.

### Lösungen für Jackett /All

- Fügen Sie jeden Tracker in Jackett manuell als Indexer in \*Arr hinzu.
- Schauen Sie sich [Prowlarr](/prowlarr) an, das Indexer mit \*Arr synchronisieren kann und vom Lidarr/Radarr/Readarr-Entwicklungsteam stammt.
- Schauen Sie sich [NZBHydra2](https://github.com/theotherp/nzbhydra2) an, das Indexer mit \*Arr synchronisieren kann. Verwenden Sie jedoch nicht ihren einzelnen Aggregat-Endpunkt und verwenden Sie `multi`, wenn die Synchronisierung verwendet wird.

## Jackett zeigt bei manueller Suche mehr Ergebnisse als Sonarr

- Überprüfen Sie die konfigurierten Kategorien für Ihren Tracker in Sonarr.
- Dies liegt normalerweise daran, dass Sonarr Jackett anders durchsucht als Sie. [Siehe diesen Fehlerbehebungseintrag für weitere Informationen](/sonarr/troubleshooting#searches-indexers-and-trackers).

## Cookies finden

- Einige Websites können nicht automatisch eingeloggt werden und erfordern, dass Sie sich manuell anmelden und dann die Cookies an Sonarr weitergeben, damit es funktioniert. [Bitte lesen Sie diesen Artikel für weitere Informationen.](/useful-tools#finding-cookies)

## Torrents entpacken

- Die meisten Torrent-Clients verfügen nicht über die automatische Verarbeitung von komprimierten Archiven wie ihre Usenet-Gegenstücke. Wir empfehlen [unpackerr](https://github.com/unpackerr/unpackerr).

## Berechtigungen

- Sonarr muss Dateien vom Speicherort verschieben, an dem der Downloader sie ablegt, in den endgültigen Speicherort. Dies bedeutet, dass Sonarr sowohl auf das Quell- als auch auf das Zielverzeichnis und die Dateien lesen/schreiben muss.
- Auf Linux, wo bewährte Verfahren vorsehen, dass Dienste als eigener Benutzer ausgeführt werden, bedeutet dies wahrscheinlich die Verwendung einer gemeinsamen Gruppe und das Festlegen von Ordnerberechtigungen auf `775` und Dateien auf `664` sowohl in Ihrem Downloader als auch in Sonarr. In der umask-Notation wäre das `002`.

## Erzwungene Authentifizierung

- In Sonarr v4 (Beta) ist die Authentifizierung obligatorisch. Bitte lesen Sie die [Sonarr v4 FAQ - Erzwungene Authentifizierung](/sonarr/faq-v4#forced-authentication) für weitere Details.