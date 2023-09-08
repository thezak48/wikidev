---
title: Radarr Tips og Tricks
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-and-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# TRaSH's Brugerdefinerede Formater

- [TRaSH har en guide](https://trash-guides.info/Radarr/) om, hvordan man bruger [Radarr => Indstillinger => Brugerdefinerede Formater](/radarr/settings#custom-formats) samt et delt lager af brugerdefinerede formater.

# Synkronisering af to Radarr-instanser

- TRaSH har [en guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) til synkronisering af to instanser

# Omdøbning af filmmapper

- [Se dette FAQ-indlæg](/radarr/faq#how-can-i-rename-my-movie-folders)

# Oprettelse af en mappe til hver film

- Dette er kun nødvendigt for at rydde op / organisere og eksisterende bibliotek for at lette importen til Radarr. Her er nogle forskellige metoder.

## Filebot

> Filebot understøttes på Windows, Linux og MacOS {.is-info}

- [Filebot](https://www.filebot.net/) er et fantastisk værktøj til at organisere dine film på en måde, som Radarr kan analysere korrekt. Version 4.7.9 kan stadig downloades gratis fra et SourceForge-spejl, men der er også betalte versioner i Windows- og Apple-butikkerne. På Linux kan dit foretrukne distribution have en pakke til det, som f.eks. Arch's AUR-pakke eller `.deb`-filer til Debian/Ubuntu fra deres downloadside. Det har både et GUI og en CLI, så det burde tilfredsstille næsten alle.

- Der er stor hjælp tilgængelig, herunder deres side med formatudtryk. Mit personlige forslag er at bruge noget som `{ny}\{fn}` hvis dine filer inkluderer nyttige detaljer som kvalitet, udgave og/eller gruppe eller `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` hvis de ikke gør det, hvilket ville give `Film (År)/Film (År) [Bluray-1080p]` eller `Film (År)/Film (År) [DVD-480p]` for eksempel. I stedet for Bluray kan du også bruge WEBDL, hvis du foretrækker, at din samling bliver betragtet som det.

- For at bevare dette mønster for fremtidige film skal du indstille:

- [Indstillinger => Mediehåndtering (Viste avancerede indstillinger) => Filnavngivning af film](/radarr/settings#media-management)

  - Fil: `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - Mappe: `{Movie CleanTitle} {(Release Year)}`

- Bemærk: Du kan erstatte mellemrummene ovenfor med `.` eller `_`, hvis du foretrækker den navngivningsform.

## Files 2 Folder

> Files 2 Folder er en Windows-applikation {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/) kan organisere dit film bibliotek til import til Radarr. Du skal blot udpakke zip-filen på din computer og køre .exe-filen som administrator, og klik derefter ja for at tilføje den til dit højreklikmenu.

Når den er installeret, er det kun få klik for at organisere alle dine filer i deres egne mapper.

1. Gå til din filmmappe
1. Vælg alle filer og højreklik for at få menuen frem
1. Vælg muligheden `files 2 folder` i menuen
1. I Files 2 Folder-vinduet skal du vælge `Flyt hver fil til individuelle undermapper baseret på deres navne`
1. Klik på OK
1. Vent et øjeblik, og alle dine filer vil være i deres egne mapper.

## Linux Bash Script

Følgende script vil tage alle `*.mkv`-filer inden for den valgte mappe og flytte dem til en mappe baseret på deres navn. Bemærk, at dette ikke går ned i undermapper inden for den startende/valgte mappe.

```shell
cd /sti/til/dine/film/filer/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windows Command Line

Gå til en kommandolinje i Windows (cmd.exe) `Som administrator`. Naviger til din filmmappe. Kør disse to kommandoer (kopier/indsæt er fint, der er intet at ændre):

`for %i in (*) do md "%~ni"`

Dette vil oprette en mappe for hver fil i mappen.

`for %i in (*) do move "%i" "%~ni"`

Dette vil flytte alle dine filer til de nye mapper.

Hvis du skal rydde op i tomme mapper, kan denne kommando gøre det:

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows Powershell

Alternativt kan du i Windows køre følgende script i Powershell for at iterere over hver fil i en mappe og flytte den til en mappe med samme navn.

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```