---
title: Radarr Tips og Triks
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-and-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# TRaSH's egendefinerte formater

- [TRaSH har en guide](https://trash-guides.info/Radarr/) om hvordan du bruker [Radarr => Innstillinger => Egendefinerte formater](/radarr/settings#custom-formats) samt et delt lager av egendefinerte formater.

# Synkronisering av to Radarr-instanser

- TRaSH har [en guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) for å synkronisere to instanser

# Omdøping av filmmapper

- [Se denne FAQ-oppføringen](/radarr/faq#how-can-i-rename-my-movie-folders)

# Opprette en mappe for hver film

- Dette er bare nødvendig for å rydde opp / organisere en eksisterende bibliotek for å lette import til Radarr. Her er noen forskjellige metoder.

## Filebot

> Filebot støttes på Windows, Linux og MacOS {.is-info}

- [Filebot](https://www.filebot.net/) er et fantastisk verktøy for å organisere filmene dine på en måte som Radarr kan analysere riktig. Versjon 4.7.9 kan fortsatt lastes ned gratis fra et SourceForge-speil, men det finnes også betalte versjoner i Windows- og Apple-butikkene. På Linux kan distribusjonen du velger ha en pakke for det, som for eksempel Arch's AUR-pakke eller `.deb`-filer for Debian/Ubuntu fra nedlastingssiden deres. Den har både et GUI og en CLI, så den bør tilfredsstille nesten alle.

- Det er god hjelp tilgjengelig, inkludert siden deres for formatuttrykk. Mitt personlige forslag er å bruke noe som `{ny}\{fn}` hvis filene dine inkluderer nyttig informasjon som kvalitet, utgave og/eller gruppe, eller `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` hvis de ikke gjør det, som ville gi `Film (År)/Film (År) [Bluray-1080p]` eller `Film (År)/Film (År) [DVD-480p]` for eksempel. I stedet for Bluray kan du også bruke WEBDL hvis du heller vil at samlingen din skal bli vurdert som det.

- For å beholde dette mønsteret for fremtidige filmer, bør du sette:

- [Innstillinger => Mediehåndtering (Vis avanserte innstillinger) => Filnavngivelse for filmer](/radarr/settings#media-management)

  - Fil: `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - Mappe: `{Movie CleanTitle} {(Release Year)}`

- Merk: Du kan erstatte mellomrommene ovenfor med `.` eller `_` hvis du foretrekker den navngivningsformatet.

## Files 2 Folder

> Files 2 Folder er en Windows-applikasjon {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/) kan organisere filmene i biblioteket for import til Radarr. Pakk ut zip-filen til datamaskinen din og kjør .exe-filen som administrator, og klikk deretter Ja for å legge den til i høyreklikkmenyen.

Når den er installert, er det bare noen få klikk for å organisere alle filene dine i egne mapper.

1. Gå til filmappen din
1. Velg alle filene og høyreklikk for å åpne menyen
1. Velg alternativet `files 2 folder` i menyen
1. I Files 2 Folder-vinduet velger du `Flytt hver fil til individuelle undermapper basert på navnene deres`
1. Klikk OK
1. Vent et øyeblikk, og alle filene dine vil være i egne mapper.

## Linux Bash-skript

Følgende skript vil ta alle `*.mkv`-filer innenfor den valgte mappen din og flytte dem til en mappe basert på navnet deres. Merk at dette ikke går inn i undermapper innenfor start-/valgt mappen.

```shell
cd /sti/til/dine/filmfiler/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windows-kommandolinje

Gå til en kommandolinje i Windows (cmd.exe) `Som administrator`. Naviger til filmappen din. Kjør disse to kommandoene (kopier/lim inn er greit, det er ingenting å endre):

`for %i in (*) do md "%~ni"`

Dette vil opprette en mappe for hver fil i mappen.

`for %i in (*) do move "%i" "%~ni"`

Dette vil flytte alle filene dine til de nye mappene.

Hvis du trenger å rydde opp i tomme mapper, vil denne kommandoen gjøre det:

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows Powershell

Alternativt i Windows kan du kjøre følgende skript i Powershell for å iterere over hver fil i en mappe og flytte den til en mappe med samme navn.

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```