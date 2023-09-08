---
title: Radarr Tips och Tricks
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-and-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# TRaSH's Anpassade Format

- [TRaSH har en guide](https://trash-guides.info/Radarr/) om hur man använder [Radarr => Inställningar => Anpassade format](/radarr/settings#custom-formats) samt en delad förvaring av anpassade format.

# Synkronisering av två Radarr-instanser

- TRaSH har [en guide](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/) för att synkronisera två instanser

# Ändra namn på filmmappar

- [Se detta FAQ-inlägg](/radarr/faq#how-can-i-rename-my-movie-folders)

# Skapa en mapp för varje film

- Detta behövs endast för att rensa upp/organisera en befintlig bibliotek för att underlätta import till Radarr. Nedan följer några olika metoder.

## Filebot

> Filebot stöds på Windows, Linux och MacOS {.is-info}

- [Filebot](https://www.filebot.net/) är ett fantastiskt verktyg för att organisera dina filmer på ett sätt som Radarr kan tolka korrekt. Version 4.7.9 kan fortfarande laddas ner gratis från en SourceForge-spegel, men det finns också betalda versioner i Windows- och Apple-butikerna. På Linux kan ditt val av distribution ha ett paket för det, som Arch's AUR-paket eller `.deb`-filer för Debian/Ubuntu från deras nedladdningssida. Det har både ett GUI och ett CLI, så det bör tillfredsställa nästan alla.

- Det finns bra hjälp tillgänglig, inklusive deras sida för formatuttryck. Mitt personliga förslag är att använda något som `{ny}\{fn}` om dina filer inkluderar användbar information som kvalitet, utgåva och/eller grupp eller `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` om de inte gör det, vilket skulle ge `Film (År)/Film (År) [Bluray-1080p]` eller `Film (År)/Film (År) [DVD-480p]` till exempel. Istället för Bluray kan du också använda WEBDL om du föredrar att din samling betraktas som det.

- För att behålla detta mönster för framtida filmer bör du ställa in:

- [Inställningar => Mediahantering (Visa avancerade inställningar) => Filnamn för filmer](/radarr/settings#media-management)

  - Fil: `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - Mapp: `{Movie CleanTitle} {(Release Year)}`

- Observera: Du kan ersätta mellanslagen ovan med `.` eller `_` om du föredrar det namnformatet.

## Files 2 Folder

> Files 2 Folder är en Windows-applikation {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/) kan organisera din filmbibliotek för import till Radarr. Extrahera helt enkelt zip-filen till din dator och kör .exe-filen som administratör, klicka sedan på Ja för att lägga till den i ditt högerklicksmeny.

När det är installerat är det bara några klick för att organisera alla dina filer i egna mappar.

1. Bläddra till din filmmapp
1. Markera alla filer och högerklicka för att visa menyn
1. Välj alternativet `files 2 folder` i menyn
1. I Files 2 Folder-fönstret väljer du `Flytta varje fil till individuella undermappar baserat på deras namn`
1. Klicka på OK
1. Vänta en stund och alla dina filer kommer att vara i egna mappar.

## Linux Bash-skript

Följande skript kommer att ta alla `*.mkv`-filer inom den valda mappen och flytta dem till en mapp baserad på deras namn. Observera att detta inte går in i undermappar inom start-/vald mapp.

```shell
cd /sökväg/till/dina/filmer/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windows Kommandorad

Gå till en kommandorad i Windows (cmd.exe) `Som administratör`. Navigera till din filmmapp. Kör dessa två kommandon (kopiera/klistra in är okej, det finns inget att ändra):

`for %i in (*) do md "%~ni"`

Detta kommer att skapa en mapp för varje fil i katalogen.

`for %i in (*) do move "%i" "%~ni"`

Detta kommer att flytta alla dina filer till de nya mapparna.

Om du behöver rensa upp tomma mappar kan detta kommando göra det:

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows Powershell

Alternativt kan du i Windows köra följande skript i Powershell för att iterera över varje fil i en mapp och flytta den till en mapp med samma namn.

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```