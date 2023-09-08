---
title: Radarr Tipps und Tricks
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tipps-und-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# TRaSH's Benutzerdefinierte Formate

- [TRaSH hat einen Leitfaden](https://trash-guides.info/Radarr/) zur Verwendung von [Radarr => Einstellungen => Benutzerdefinierte Formate](/radarr/settings#custom-formats) sowie ein gemeinsames Repository für benutzerdefinierte Formate.

# Synchronisieren von zwei Radarr-Instanzen

- TRaSH hat [einen Leitfaden](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) zum Synchronisieren von zwei Instanzen.

# Umbenennen von Filmordnern

- [Siehe diesen FAQ-Eintrag](/radarr/faq#how-can-i-rename-my-movie-folders)

# Erstellen eines Ordners für jeden Film

- Dies ist nur erforderlich, um eine vorhandene Bibliothek aufzuräumen/zu organisieren und den Import in Radarr zu erleichtern. Hier sind einige verschiedene Methoden.

## Filebot

> Filebot wird auf Windows, Linux und MacOS unterstützt {.is-info}

- [Filebot](https://www.filebot.net/) ist ein fantastisches Dienstprogramm, um Ihre Filme so zu organisieren, dass Radarr sie erfolgreich analysieren kann. Version 4.7.9 kann immer noch kostenlos von einem SourceForge-Spiegel heruntergeladen werden, aber es gibt auch kostenpflichtige Versionen in den Windows- und Apple-Stores. Unter Linux kann Ihre bevorzugte Distribution möglicherweise ein Paket dafür haben, wie z.B. das AUR-Paket in Arch oder `.deb`-Dateien für Debian/Ubuntu von ihrer Download-Seite. Es hat sowohl eine GUI als auch eine CLI und sollte daher fast jeden zufriedenstellen.

- Es gibt eine große Hilfe zur Verfügung, einschließlich ihrer Formatexpressions-Seite. Mein persönlicher Vorschlag ist es, etwas wie `{ny}\{fn}` zu verwenden, wenn Ihre Dateien nützliche Details wie Qualität, Ausgabe und/oder Gruppe enthalten, oder `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`, wenn sie das nicht tun. Dies würde zum Beispiel `Film (Jahr)/Film (Jahr) [Bluray-1080p]` oder `Film (Jahr)/Film (Jahr) [DVD-480p]` ergeben. Anstelle von Bluray könnten Sie auch WEBDL verwenden, wenn Sie möchten, dass Ihre Sammlung so betrachtet wird.

- Um dieses Muster für zukünftige Filme beizubehalten, sollten Sie Folgendes festlegen:

- [Einstellungen => Medienverwaltung (Erweiterte Einstellungen anzeigen) => Filmbenennung](/radarr/settings#media-management)

  - Datei: `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - Ordner: `{Movie CleanTitle} {(Release Year)}`

- Hinweis: Sie können die Leerzeichen oben durch `.` oder `_` ersetzen, wenn Sie dieses Benennungsformat bevorzugen.

## Files 2 Folder

> Files 2 Folder ist eine Windows-Anwendung {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/) kann Ihre Film-Bibliothek für den Import in Radarr organisieren. Extrahieren Sie einfach die ZIP-Datei auf Ihrem Computer und führen Sie die .exe als Administrator aus. Klicken Sie dann auf Ja, um sie dem Kontextmenü hinzuzufügen.

Sobald es installiert ist, sind es nur wenige Klicks, um alle Ihre Dateien in eigene Ordner zu organisieren.

1. Navigieren Sie zu Ihrem Filmordner.
1. Wählen Sie alle Dateien aus und klicken Sie mit der rechten Maustaste, um das Menü aufzurufen.
1. Wählen Sie die Option "Files 2 Folder" im Menü.
1. Wählen Sie im Fenster "Files 2 Folder" die Option "Jede Datei in einzelne Unterordner verschieben, basierend auf ihren Namen".
1. Klicken Sie auf OK.
1. Warten Sie einen Moment, und alle Ihre Dateien befinden sich in eigenen Ordnern.

## Linux Bash-Skript

Das folgende Skript nimmt alle `*.mkv`-Dateien in Ihrem ausgewählten Ordner und verschiebt sie in einen Ordner, der auf ihrem Namen basiert. Beachten Sie, dass dies nicht in Unterordner innerhalb des Start-/Ausgangsordners geht.

```shell
cd /Pfad/zu/Ihren/Filmdateien/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windows-Befehlszeile

Wechseln Sie in Windows zur Befehlszeile (cmd.exe) `Als Administrator`. Navigieren Sie zu Ihrem Filmordner. Führen Sie diese beiden Befehle aus (Kopieren/Einfügen ist in Ordnung, es gibt nichts zu ändern):

`for %i in (*) do md "%~ni"`

Dies erstellt für jede Datei im Verzeichnis einen Ordner.

`for %i in (*) do move "%i" "%~ni"`

Dies verschiebt alle Ihre Dateien in die neuen Verzeichnisse.

Wenn Sie leere Verzeichnisse aufräumen müssen, führt dieser Befehl dies aus:

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows Powershell

Alternativ können Sie in Windows das folgende Skript in Powershell ausführen, um über jede Datei in einem Verzeichnis zu iterieren und sie in einen Ordner mit demselben Namen zu verschieben.

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```