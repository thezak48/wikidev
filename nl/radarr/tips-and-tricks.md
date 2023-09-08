---
title: Radarr Tips en Trucs
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-en-trucs
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# Aangepaste indelingen van TRaSH

- [TRaSH heeft een handleiding](https://trash-guides.info/Radarr/) over hoe je [Radarr => Instellingen => Aangepaste indelingen](/radarr/settings#custom-formats) kunt gebruiken, evenals een gedeelde repository van aangepaste indelingen.

# Synchroniseren van twee Radarr-instanties

- TRaSH heeft [een handleiding](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) voor het synchroniseren van twee instanties.

# Hernoemen van filmmappen

- [Zie deze FAQ-entry](/radarr/faq#how-can-i-rename-my-movie-folders)

# Een map maken voor elke film

- Dit is alleen nodig om een bestaande bibliotheek op te schonen / te organiseren om importeren in Radarr te vergemakkelijken. Hieronder staan een paar verschillende methoden.

## Filebot

> Filebot wordt ondersteund op Windows, Linux en MacOS {.is-info}

- [Filebot](https://www.filebot.net/) is een fantastisch hulpprogramma om je films op een manier te organiseren die Radarr succesvol kan verwerken. Versie 4.7.9 kan nog steeds gratis worden gedownload van een SourceForge-mirror, maar er zijn ook betaalde versies in de Windows- en Apple-winkels. Op Linux heeft je distributie naar keuze mogelijk een pakket ervoor, zoals het AUR-pakket in Arch of `.deb`-bestanden voor Debian/Ubuntu van hun downloadpagina. Het heeft zowel een GUI als een CLI, dus het zou bijna iedereen moeten bevredigen.

- Er is geweldige hulp beschikbaar, inclusief hun pagina met formatexpressies. Mijn persoonlijke suggestie is om iets als `{ny}\{fn}` te gebruiken als je bestanden nuttige details bevatten zoals kwaliteit, editie en/of groep, of `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` als dat niet het geval is, wat bijvoorbeeld `Film (Jaar)/Film (Jaar) [Bluray-1080p]` of `Film (Jaar)/Film (Jaar) [DVD-480p]` zou opleveren. In plaats van Bluray kun je ook WEBDL gebruiken als je wilt dat je collectie zo wordt beschouwd.

- Om dit patroon voor toekomstige films te behouden, moet je het volgende instellen:

- [Instellingen => Mediabeheer (Geavanceerde instellingen weergegeven) => Filmindeling](/radarr/settings#media-management)

  - Bestand: `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - Map: `{Movie CleanTitle} {(Release Year)}`

- Opmerking: Je kunt de spaties hierboven vervangen door `.` of `_` als je de voorkeur geeft aan die naamgevingsindeling.

## Files 2 Folder

> Files 2 Folder is een Windows-toepassing {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/) kan je filmcollectie georganiseerd houden voor import in Radarr. Pak eenvoudig het zipbestand uit op je computer en voer het .exe-bestand uit als beheerder, klik vervolgens op Ja om het aan je rechtsklikmenu toe te voegen.

Nadat het is geïnstalleerd, zijn er slechts een paar klikken nodig om al je bestanden in hun eigen mappen te organiseren.

1. Blader naar je map met films
1. Selecteer alle bestanden en klik met de rechtermuisknop om het menu te openen
1. Selecteer de optie `files 2 folder` in het menu
1. In het venster Files 2 Folder selecteer je `Verplaats elk bestand naar individuele submappen op basis van hun namen`
1. Klik op OK
1. Wacht even en al je bestanden zullen in hun eigen map staan.

## Linux Bash-script

Het volgende script neemt alle `*.mkv`-bestanden in je geselecteerde map en verplaatst ze naar een map op basis van hun naam. Let op dat dit niet in submappen binnen de start-/geselecteerde map gaat.

```shell
cd /pad/naar/je/film/bestanden/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windows-opdrachtregel

Ga naar een opdrachtregel in Windows (cmd.exe) `Als beheerder`. Navigeer naar je map met films. Voer deze twee opdrachten uit (kopiëren/plakken is prima, er hoeft niets te worden gewijzigd):

`for %i in (*) do md "%~ni"`

Hiermee wordt voor elk bestand in de map een map gemaakt.

`for %i in (*) do move "%i" "%~ni"`

Hiermee worden al je bestanden verplaatst naar de nieuwe mappen.

Als je lege mappen wilt opruimen, gebruik je deze opdracht:

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows Powershell

Als alternatief kun je in Windows het volgende script in Powershell uitvoeren om elk bestand in een map te doorlopen en het naar een map met dezelfde naam te verplaatsen.

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```