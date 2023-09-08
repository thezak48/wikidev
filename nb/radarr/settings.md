---
title: Radarr-innstillinger
description: Beskrivelse av Radarr-innstillingsmenyer
published: true
date: 2023-08-27T22:02:11.780Z
tags: radarr, needs-love, innstillinger
editor: markdown
dateCreated: 2021-05-29T15:57:25.304Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Menyalternativer](#menyalternativer)
- [Mediehåndtering](#mediehåndtering)
  - [Forslag til fellesskapsnavn](#forslag-til-fellesskapsnavn)
  - [Filnavngivning for filmer](#filnavngivning-for-filmer)
    - [Standard filformat](#standard-filformat)
    - [Filnavngivning for filmer](#filnavngivning-for-filmer-1)
    - [Film-ID-er](#film-id-er)
    - [Kvalitet](#kvalitet)
    - [Medieinformasjon](#medieinformasjon)
    - [Utgivelsesgruppe](#utgivelsesgruppe)
    - [Utgave](#utgave)
    - [Egendefinerte formater (navngivning)](#egendefinerte-formater-navngivning)
    - [Original](#original)
  - [Filmappeformat](#filmappeformat)
    - [Filnavngivning for filmer](#filnavngivning-for-filmer-2)
    - [Film-ID](#film-id)
  - [Mapper](#mapper)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
  - [Tillatelser](#tillatelser)
  - [Rotmapper](#rotmapper)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Forsinkelsesprofiler](#forsinkelsesprofiler)
    - [Bruksområder](#bruksområder)
    - [Hvordan forsinkelsesprofiler fungerer](#hvordan-forsinkelsesprofiler-fungerer)
      - [Eksempler](#eksempler)
        - [Eksempel 1](#eksempel-1)
        - [Eksempel 2](#eksempel-2)
        - [Eksempel 3](#eksempel-3)
- [Kvalitet](#kvalitet-1)
  - [Betydning av kvalitetstabell](#betydning-av-kvalitetstabell)
  - [Definerte kvaliteter](#definerte-kvaliteter)
- [Egendefinerte formater](#egendefinerte-formater)
  - [Betingelser for egendefinerte formater](#betingelser-for-egendefinerte-formater)
    - [Modifikatorer](#modifikatorer)
    - [Betingelser](#betingelser)
    - [Profileringsinnstillinger og rangering](#profileringsinnstillinger-og-rangering)
      - [Importering/Eksportering av egendefinerte formater](#importeringeksportering-av-egendefinerte-formater)
      - [Importering/oppdatering av eksisterende egendefinerte formater](#importeringoppdatering-av-eksisterende-egendefinerte-formater)
    - [Samling av egendefinerte formater](#samling-av-egendefinerte-formater)
- [Indekser](#indekser)
  - [Støttede indekser](#støttede-indekser)
    - [Indeksinnstillinger](#indeksinnstillinger)
    - [Usenet-indekskonfigurasjon](#usenet-indekskonfigurasjon)
    - [Torrent-sporer-konfigurasjon](#torrent-sporer-konfigurasjon)
      - [Indeksflagg](#indeksflagg)
  - [Alternativer](#alternativer)
  - [Begrensninger](#begrensninger)
- [Nedlastingsklienter](#nedlastingsklienter)
  - [Oversikt](#oversikt)
  - [Prosesser for nedlastingsklienter](#prosesser-for-nedlastingsklienter)
    - [Usenet-prosess](#usenet-prosess)
    - [Torrent-prosess](#torrent-prosess)
  - [Nedlastingsklienter](#nedlastingsklienter-1)
    - [Støttede nedlastingsklienter](#støttede-nedlastingsklienter)
    - [Innstillinger for Usenet-klient](#innstillinger-for-usenet-klient)
    - [Innstillinger for torrentklient](#innstillinger-for-torrentklient)
    - [Kompatibilitet for fjerning av nedlastinger i torrentklient](#kompatibilitet-for-fjerning-av-nedlastinger-i-torrentklient)
  - [Håndtering av fullførte nedlastinger](#håndtering-av-fullførte-nedlastinger)
    - [Fjern fullførte nedlastinger](#fjern-fullførte-nedlastinger)
    - [Håndtering av mislykkede nedlastinger](#håndtering-av-mislykkede-nedlastinger)
  - [Fjernstyrte stiavbildninger](#fjernstyrte-stiavbildninger)
- [Importlister](#importlister)
  - [Lister](#lister)
  - [Listealternativer](#listealternativer)
  - [Listeeksklusjoner](#listeeksklusjoner)
- [Koble til](#koble-til)
  - [Tilkoblinger](#tilkoblinger)
  - [Tilkoblingstriggere](#tilkoblingstriggere)
- [Metadata](#metadata)
  - [Alternativer](#alternativer-1)
  - [Metadataforbrukere](#metadataforbrukere)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Vert](#vert)
  - [Sikkerhet](#sikkerhet)
  - [Proxy](#proxy)
  - [Logging](#logging)
  - [Analyse](#analyse)
  - [Oppdateringer](#oppdateringer)
  - [Sikkerhetskopier](#sikkerhetskopier)
- [Brukergrensesnitt](#brukergrensesnitt)
  - [Kalender](#kalender)
  - [Filmer](#filmer)
  - [Datoer](#datoer)
  - [Stil](#stil)
  - [Språk](#språk)

Denne siden vil gå gjennom alle innstillingene som er tilgjengelige i Radarr og hvordan de fungerer. Dette er ikke ment å være en omfattende "hvordan sette opp Radarr"-guide. Hvis du ønsker det, kan du bruke [Quick Start](/radarr/quick-start-guide)-siden i stedet.

# Menyalternativer

For å komme til innstillingssiden, velg Innstillinger fra sidepanelet. Følgende undermenyalternativer vil være tilgjengelige:

![settings_1_menu.png](/assets/radarr/settings_1_menu.png)

Merk også at for hver enkelt innstillingsside er det noen alternativer øverst i menyen:

![settings_2_topmenu.png](/assets/radarr/settings_2_topmenu.png)

- Skjul/Vis avansert er viktig for alle elementer som er merket som `(Avansert alternativ)` nedenfor, ellers vil de ikke vises. Disse menyelementene vises i oransje på skjermbildene.

- Du må lagre endringene før du forlater skjermen. Du gjør dette ved å klikke på diskikonet. Hvis du ikke har gjort noen endringer, vil det stå "Ingen endringer" og være utgrået, som vist ovenfor.

# Mediehåndtering

> Noen av disse innstillingene er bare synlige ved hjelp av `Vis avanserte innstillinger`, som er øverst i menylinjen under søkefeltet{.is-info}

## Forslag til fellesskapsnavn

> Her er noen forslag til fellesskapsnavn fra [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/){.is-info}

### Filmer

- Radarr v4.2.2.6489 eller nyere

`{Movie CleanTitle} {(Utgivelsesår)} {imdb-{ImdbId}} {edition-{Edition Tags}} {[Egendefinerte formater]}{[Quality Full]}{[MediaInfo 3D]}{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}]{MediaInfo AudioLanguages}[{Mediainfo VideoCodec}]{-Release Group}`

- Eldre Radarr-versjoner

`{Movie CleanTitle} {(Utgivelsesår)} {Edition Tags} [imdb-{ImdbId}]{[Egendefinerte formater]}{[Quality Full]}{[MediaInfo 3D]}{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}][{Mediainfo VideoCodec}]{-Release Group}`

### Filmappe

`{Movie CleanTitle} ({Utgivelsesår})`

## Filnavngivning for filmer

- Gi nytt navn til filmer - Hvis ikke valgt, vil Radarr bruke det eksisterende navnet hvis navneendring er deaktivert
  - Hvis ikke valgt:
    - Importering av nedlastingsklient
      - Nedlastingsklientens utgivelsestittel brukes
    - Manuell (ad hoc) importering: Opprinnelig filnavn
- Erstatt ulovlige tegn - Hvis ikke valgt, vil Radarr fjerne dem i stedet.

  - Tegnene er: `:` `\` `/` `>` `<` `?` `*` `|` `"`
- Erstatning for kolon (`:`) - Denne innstillingen bestemmer hvordan Radarr håndterer kolon i filnavnet. Denne er bare tilgjengelig når "Erstatt ulovlige tegn" er aktivert.
  - Slett - Selvforklarende
    - Eksempel: Movie,The.mkv => MovieThe.mkv
  - Erstatt med bindestrek - Fjerner kolonet og legger til en bindestrek i stedet
    - Eksempel: Movie,The.mkv => Movie-The.mkv
  - Erstatt med mellomrom - Fjerner kolonet og legger til et mellomrom i stedet
    - Eksempel: Movie,The.mkv => Movie The.mkv
  - Erstatt med mellomrom bindestrek mellomrom - selvforklarende
    - Eksempel: Movie,The.mkv => Movie - The.mkv

### Standard filformat for filmer

- Her velger du navnekonvensjonen for filmene dine

- Rullegardinmeny (øverst til høyre)
  - Venstre boks - Håndtering av mellomrom
    Mellomrom ( ) - Bruk mellomrom i navngivningen (standard)
    Periode (.) - Bruk punktum i stedet for mellomrom i navngivningen
    Understrek (_) - Bruk understrek i stedet for mellomrom i navngivningen
    Bindestrek (-) - Bruk bindestrek i stedet for mellomrom i navngivningen
  - Høyre boks - Håndtering av store og små bokstaver
    Standardstørrelse - Gjør tittelen stor og liten (~camel-case) (standard)
    Store bokstaver - Gjør tittelen helt stor
    Små bokstaver - Gjør tittelen helt liten

### Filnavngivning for filmer

- `{Movie Title}` = Filmtittel!
- `{Movie Title:DE}` = Filmtittel
- `{Movie CleanTitle}` = Filmtittel
- `{Movie TitleThe}` = Filmtittel, The
- `{Movie OriginalTitle}` = Original tittel
- `{Movie CleanOriginalTitle}` = Original tittel
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = Filmsamlingen
- `{Movie Certification}` = R
- `{Release Year}` = 2009

`CleanTitle` [gjør følgende](https://github.com/Radarr/Radarr/blob/5948f564827eabb7afc1e89bf4a5987e3c71dc74/src/NzbDrone.Core/Organizer/FileNameBuilder.cs#L207):

- Erstatt `&` med `and`
- Erstatt `/` og `\` med ` `
- Fjern `,`,`<`,`>`,`/`,`\`,`;`,`:`,`'`,`|`, `~`,`!`,`?`,`@`,`$`,`%`,`^`,`*`,`-`,`_`,`=` i henhold til følgende regex:

```regex
(?<=\s)(,|<|>|\/|\\|;|:|'|""|\||`|~|!|\?|@|$|%|^|\*|-|_|=){1}(?=\s)|('|:|\?|,)(?=(?:(?:s|m)\s)|\s|$)|(\(|\)|\[|\]|\{|\})
```

### Film-ID-er

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

> Imdb-tagene som brukes i Plex-navngivningsformatet, vil skjules betinget når verdien er tom `{imdb-{ImdbId}}`{.is-info}

### Kvalitet

- `{Quality Full}` = HDTV 720p Riktig
- `{Quality Title}` = HDTV 720p

### Medieinformasjon

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguages}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`, `AudioLanguages` og `SubtitleLanguages` støtter for øyeblikket ikke en `:EN+DE`-suffiks som tillates i Sonarr for å filtrere språkene som er inkludert i filnavnet. Det er en åpen [sak](https://github.com/Radarr/Radarr/issues/4710) angående dette.
~~`MediaInfo Full`, `AudioLanguages` og `SubtitleLanguages` støtter en `:EN+DE`-suffiks som lar deg filtrere språkene som er inkludert i filnavnet. Bruk `-DE` for å ekskludere bestemte språk. Ved å legge til <kb>+</kb> (f.eks.: `:EN+`) vil det vises `[EN]`,`[EN+--]` eller `[--]` avhengig av ekskluderte språk. For eksempel - `{MediaInfo Full:EN+DE}`.~~{.is-info}

> `MediaInfo VideoDynamicRangeType` vil gi mulige verdier: DV, DV HDR10, DV HLG, DV SDR, HDR10, HDR10Plus, HLG og PQ.{.is-info}

### Utgivelsesgruppe

- `{Release Group}` = Rls Grp

### Utgave

- `{Edition Tags}` = IMAX

> Fra og med v4.2.2.6489 vil utgavetagger som brukes i Radarr etter Plex' navngivningsformat `{edition-{Edition Tags}}` skjules betinget som `{-Group}` gjør når utgavetaggverdien er tom{.is-info}

### Egendefinerte formater (navngivning)

- `{Custom Formats}` = Surround Sound x264

> Egendefinerte formater vil være den bokstavelige navnet på egendefinert format og krever at egendefinert format er aktivert for å bli inkludert i navngivningen{.is-info}

### Original

- `{Original Title}` = Movie.Title.HDTV.x264-EVOLVE
- `{Original Filename}` = Movie.title.hdtv.x264-EVOLVE

> `Original Title` er utgivelsesnavnet og det anbefales å bruke det{.is-info}

>`Original Filename` anbefales ikke. Det er det bokstavelige opprinnelige filnavnet og kan være obfuskert `t1i0p3s7i8yuti`{.is-warning}

## Filmappeformat

Her setter du navnekonvensjonen for mappen som inneholder sesongmapper eller filer for filmer. Klikk på `?` for å åpne dialogboksen `Folder Name Tokens` (mappetokens).

### Filnavngivning for filmer

- `{Movie Title}` = Filmtittel!
- `{Movie Title:DE}` = Filnavn
- `{Movie CleanTitle}` = Filmtittel
- `{Movie TitleThe}` = Filmtittel, The
- `{Movie OriginalTitle}` = Original tittel
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = Filmsamlingen
- `{Movie Certification}` = R
- `{Release Year}` = 2009

### Film-ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

## Mapper

- Opprett tomme mediemapper - Opprett manglende filmapper under disk-skanning
- Slett tomme mapper - Slett tomme filmapper under disk-skanning og når filer slettes

## Importering

- Hopp over sjekk av ledig plass - Brukes når Radarr ikke kan oppdage ledig plass fra rotmappen for serier
- Minimum ledig plass - Ved å veksle dette vil importeringen forhindres hvis det vil være mindre enn denne mengden diskplass tilgjengelig
- Bruk hardlenker i stedet for kopi - Bruk hardlenker når du prøver å kopiere filer fra torrents som fortsatt blir seedet

  - For mer informasjon om dette, klikk [her](https://trash-guides.info/hardlinks)

> Sjelden, men muligens, kan filsperrer forhindre at filer som blir seedet, blir omdøpt. Du kan midlertidig deaktivere seeding og bruke Radarrs omdøpingsfunksjon som en løsning.{.is-warning}

- Importer ekstra filer - Importer matchende ekstra filer (undertekster, nfo, osv.) etter importering av en fil

## Filhåndtering

- Avmonitorer slettede filmer - Filmer som er slettet fra disken blir automatisk avmonitorert i Radarr.
- Last ned riktig og repacks - Om du vil oppgradere automatisk til Propers/Repacks. Bruk `Ikke foretrekk` for å sortere etter foretrukket ordpoeng over propers/repacks.

  - Foretrekk og oppgrader - Ranger repacks og propers høyere enn ikke-repacks og ikke-propers. Behandle nye repacks og propers som oppgradering til nåværende utgivelser.
  - Ikke oppgrader automatisk - Ranger repacks og propers høyere enn ikke-repacks og ikke-propers. Behandle ikke nye repacks og propers som oppgradering til nåværende utgivelser.
  - Ikke foretrekk - Ignorer repacks og propers. Du må håndtere preferanse for disse med [egendefinerte formater](#egendefinerte-formater).

> \* `PROPER` - betyr at det var et problem med den forrige utgivelsen. Nedlastinger merket som PROPER viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som ikke slapp originalen.
> \* `REPACK` - betyr at det var et problem med den forrige utgivelsen og det er rettet av den opprinnelige gruppen. Nedlastinger merket som REPACK viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som slapp originalen.
{.is-info}

> [Bruk egendefinerte formater for automatisk oppgradering til propers/repacks](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)
{.is-info}

- Analyser videofiler - Hent ut filinformasjon som oppløsning, kjøretid og kodekinformasjon fra filer. Dette krever at Radarr leser deler av filen, noe som kan føre til høy disk- eller nettverksaktivitet under skanninger.
- Skann filmmappe etter oppdatering
  - Alltid - Dette vil skanne filmmapper basert på oppgaveplanen. Dette anbefales for de fleste tilfeller, inkludert hvis du bruker Bazarr.
  - Etter manuell oppdatering - Du må manuelt skanne disken. Dette anbefales for brukere av skybasert lagring.
  - Aldri - Akkurat som det sier, aldri skann filmmapper. Dette anbefales ikke.
- Endre fil-dato - Endre fil-dato ved import/skanning
  - Ingen - Radarr vil ikke endre datoen som vises i filutforskeren din
  - Kinodato - Datoen filmen ble utgitt på kino.
  - Fysisk utgivelsesdato - Datoen filmen ble utgitt enten på disk (fysisk) eller på nettet.
- Gjenvinningsmappe - Filmfiler vil havne her når de blir slettet i stedet for å bli permanent slettet
- Rengjøring av gjenvinningsmappe - Dette er hvor gammel en gitt fil kan være før den blir permanent slettet

> Filer i gjenvinningsmappen som er eldre enn det valgte antallet dager, vil bli ryddet automatisk {.is-warning}

## Tillatelser

- Sett tillatelser - Skal `chmod` kjøres når filer importeres/omdøpes?
  - chmod-mappen - Oktal, brukt under import/omdøping av mediamapper og filer (uten kjøretillatelser)

> Rullegardinmenyen har en forhåndsdefinert liste over vanlig brukte tillatelser som kan brukes. Du kan imidlertid manuelt angi en oktal verdi for mappen hvis du ønsker det.{.is-info}

> Dette fungerer bare hvis brukeren som kjører `Radarr` er eieren av filen. Det er bedre å sørge for at nedlastingsklienten setter tillatelsene riktig.{.is-warning}

- chown-gruppe - Gruppenavn eller GID. Bruk GID for eksterne filsystemer

> Dette fungerer bare hvis brukeren som kjører `Radarr` er eieren av filen. Det er bedre å sørge for at nedlastingsklienten setter tillatelsene riktig.{.is-warning}

## Rotmapper

- Sti - Dette viser stien til mediebiblioteket ditt
- Ledig plass - Dette er den ledige plassen som rapporteres til Radarr fra systemet
- Ukartlagte mapper - Dette er mapper som ikke er tilknyttet en film

> `X`-en på slutten vil fjerne denne rotstien
{.is-info}

- Legg til rotmappe - Dette lar deg velge en rotsti for et sted å enten plassere nye importerte nedlastinger i denne mappen eller å la Radarr skanne eksisterende medier.

> Brukere som ikke bruker Windows:
> \* Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
> \* Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.
{.is-warning}

# Profiler

## Kvalitetsprofiler

- Sett profiler for kvaliteten på filmene du ønsker å laste ned.

> Når du velger en eksisterende profil eller legger til en ekstra profil, vil et nytt vindu vises{.is-info}

> Merk: Kvaliteten som har en blå boks er kvaliteten som alle medier med denne profilen vil fortsette å oppgraderes til.
{.is-info}

- Plusstegn (<kb>+</kb>) - Opprett en ny kvalitetsprofil

- Navn - Velg et **UNIKT** navn for kvalitetsprofilen du oppretter
- Oppgraderinger tillatt - Når dette alternativet er merket av og du ber Radarr om å laste ned en `WEB 1080p` fordi det er den første utgivelsen av en bestemt film, vil Radarr automatisk oppgradere til bedre kvalitet ***hvis*** `Oppgrader til` har den kvaliteten valgt
- Oppgrader til - Når denne kvaliteten er nådd, vil Radarr ikke lenger laste ned filmer

> Merk: Dette gjelder bare hvis du har `Bluray-1080p` høyere enn `WEB 1080p` innenfor `Kvaliteter`-delen
{.is-warning}

- Kvaliteter - Kvaliteter som er høyere på listen, foretrekkes selv om de ikke er merket av. Kvaliteter innenfor samme gruppe er likestilte. Bare merkede kvaliteter ønskes.
  - Rediger grupper - Noen kvaliteter er gruppert sammen for å redusere størrelsen på listen, samt gruppere lignende utgivelser. Et godt eksempel på dette er `WebDL` og `WebRip`, da disse er veldig like og vanligvis har lignende bithastigheter. Når du redigerer gruppene, kan du endre preferansen innenfor hver av gruppene. [Se TRaSH's Guide for hvordan du slår sammen kvaliteter](https://trash-guides.info/merge-quality)

  - [Se definerte kvaliteter](#definerte-kvaliteter)

> Som standard er kvalitetene satt fra laveste (nederst) til høyeste (øverst)
{.is-info}

- Språk - Velg ønsket språk

- Egendefinert format - Radarr scorer hver utgivelse ved å summere poengene for tilsvarende egendefinerte formater. Hvis en ny utgivelse ville forbedre poengsummen, med samme eller bedre kvalitet, vil Radarr laste den ned.
Se [Egendefinerte formater](#egendefinerte-formater) for mer informasjon.

## Forsinkelsesprofiler

- Forsinkelsesprofiler lar deg redusere antall utgivelser som blir lastet ned for en film ved å legge til en forsinkelse mens Radarr fortsetter å se etter utgivelser som bedre samsvarer med preferansene dine.
- Foretrukket protokoll - Dette vil enten være `Usenet` eller `Torrent`, avhengig av hvilken nedlastingsprotokoll du foretrekker
- Usenet-forsinkelse - Angi antall minutter du vil vente før nedlastingen starter
- Torrent-forsinkelse - Angi antall minutter du vil vente før nedlastingen starter
- Bypass hvis høyeste kvalitet - Bypass forsinkelsen når utgivelsen har den høyeste aktiverte kvalitetsprofilen med foretrukket protokoll
- Merker - Ved å gi denne forsinkelsesprofilen et merke, kan du merke en bestemt film for å følge reglene som er satt her.
- Skiftenøkkelikon - Dette lar deg redigere forsinkelsesprofilen
- Plusstegn (<kb>+</kb>) - Opprett en ny forsinkelsesprofil

### Bruksområder

Noen medier vil motta et halvt dusin forskjellige utgivelser av varierende kvalitet i timene etter en utgivelse, og uten forsinkelsesprofiler kan Radarr prøve å laste ned alle sammen. Med forsinkelsesprofiler kan Radarr konfigureres til å ignorere de første timene med utgivelser.

Forsinkelsesprofiler er også nyttige hvis du vil vektlegge en protokoll (Usenet eller BitTorrent) over den andre. (Se Eksempel 3)

### Hvordan forsinkelsesprofiler fungerer

Tidtakeren starter så snart Radarr oppdager at en film har en tilgjengelig utgivelse. Denne utgivelsen vises i køen din med et klokkeikon for å indikere at den er under forsinkelse.

> Klokken starter fra tidspunktet utgivelsen ble lastet opp og ikke fra tidspunktet Radarr ser den.
{.is-info}

I løpet av forsinkelsesperioden vil Radarr merke seg eventuelle nye utgivelser som blir tilgjengelige. Når forsinkelsestimeren utløper, vil Radarr laste ned den ene utgivelsen som best samsvarer med kvalitetspreferansene dine.

Tidtakerperioden kan være forskjellig for Usenet og Torrents. Hver profil kan være tilknyttet en eller flere merker for å tilpasse hvilke programmer som har hvilke profiler. En forsinkelsesprofil uten merke regnes som standard og gjelder for alle programmer som ikke har et spesifikt merke.

> Forsinkelsesprofiler starter fra tidspunktet indekseren rapporterer at utgivelsen ble lastet opp. Dette betyr at innhold som er eldre enn antall minutter du har satt, ikke påvirkes på noen måte av forsinkelsesprofilen din, og vil bli lastet ned umiddelbart. I tillegg vil **alle manuelle søk** etter innhold (søk uten RSS-strøm) ignorere innstillingene for forsinkelsesprofilen.
{.is-warning}

#### Eksempler

- For hvert eksempel, anta at brukeren har følgende kvalitetsprofil aktiv: WebDL-720p og høyere er tillatt, WebDL-1080p er kvalitetsgrensen, og BluRay1080p er den høyest rangerte kvaliteten.

##### Eksempel 1

- I dette enkle eksempelet er profilen satt med en 120 minutters (to timers) forsinkelse for både Usenet og Torrent.

- Klokken 23:00 oppdager Radarr den første utgivelsen for en film, og den ble lastet opp klokken 22:50, og 120 minutters klokke starter. Klokken 00:50 vil Radarr vurdere eventuelle utgivelser den har funnet i løpet av de siste to timene, og laste ned den beste, som er WebDL 720p.

- Klokken 03:00 blir det funnet en annen utgivelse, som er WebDL 720p og ble lagt til i indeksen din klokken 02:46. En annen 120 minutters klokke starter. Klokken 04:46 blir den beste tilgjengelige utgivelsen lastet ned. Siden kvalitetsgrensen nå er nådd, kan ikke filmen oppgraderes lenger, og Radarr vil slutte å lete etter nye utgivelser.

- På et hvilket som helst tidspunkt, hvis det blir funnet en WebDL 1080p-utgivelse, vil den bli lastet ned umiddelbart fordi det er den høyest rangerte kvaliteten. Hvis det er en aktiv forsinkelsestimer, vil den bli kansellert.

##### Eksempel 2

- Dette eksempelet har forskjellige tidtakere for Usenet og Torrents. Anta en 120 minutters timer for Usenet og en 180 minutters timer for BitTorrent.

- Klokken 23:00 oppdages den første utgivelsen for en film av Radarr, og begge tidtakerne starter. Utgivelsen ble lagt til indeksen din klokken 22:15. Klokken 00:15 vil Radarr vurdere eventuelle utgivelser, og hvis det er noen akseptable Usenet-utgivelser, vil den beste bli lastet ned og begge tidtakerne vil avsluttes. Hvis ikke, vil Radarr vente til 00:15 og laste ned den beste utgivelsen, uavhengig av hvilken kilde den kom fra.

##### Eksempel 3

- En vanlig bruk for forsinkelsesprofiler er å vektlegge en protokoll over den andre. For eksempel kan du bare ønske å laste ned en BitTorrent-utgivelse hvis ingenting har blitt lastet opp til Usenet etter en viss tid.

- Du kan sette en 60 minutters timer for BitTorrent og en 0 minutters timer for Usenet.

- Hvis den første utgivelsen som oppdages er fra Usenet, vil Radarr laste den ned umiddelbart.

- Hvis den første utgivelsen er fra BitTorrent, vil Radarr sette en 60 minutters timer. Hvis det blir oppdaget noen kvalifiserte Usenet-utgivelser i løpet av den tiden, vil BitTorrent-utgivelsen bli ignorert, og Usenet-utgivelsen vil bli lastet ned.

## Utgivelsesprofiler

- Her kan du sette globale begrensninger basert på et par parametere
- Klikk på <kb>+</kb> og et nytt vindu vil åpne seg
- Må inneholde - I dette feltet kan du fortelle Radarr at hvis en utgivelse ikke inneholder en bestemt streng, vil ikke Radarr laste ned den utgivelsen. Dette er ikke forskjellsensitivt som standard, og regex kan brukes.
- Må ikke inneholde - I dette feltet kan du fortelle Radarr at hvis en utgivelse inneholder en bestemt streng, vil ikke Radarr laste ned den utgivelsen. Dette er ikke forskjellsensitivt som standard, og regex kan brukes.
- Merker - Her kan du bruke disse innstillingene på filmer med minst en av de gitte [merkene](#merker).

# Kvalitet

## Betydning av kvalitetstabell

- Kvalitet - Navnet på kvaliteten i scenen (hardkodet)
- Tittel - Navnet på kvaliteten i brukergrensesnittet (konfigurerbart)
- Megabyte per minutt - Selvforklarende
- Størrelsesgrense - Selvforklarende
- Min - Minimum antall megabyte per minutt (MB/min) en kvalitet kan ha.
- Foretrukket - Foretrukket antall megabyte per minutt (MB/min) en kvalitet kan ha.
- Maks - Maksimum antall megabyte per minutt (MB/min) en kvalitet kan ha.

## Definerte kvaliteter

- Ukjent - Selvforklarende
- SDTV - Post-luft-rips fra en analog kilde (vanligvis kabel-TV eller OTA standard definisjon). Bildekvaliteten er generelt god (for oppløsningen) og de er vanligvis kodet i DivX/XviD eller MP4.
- WEBDL-480p - WEB-DL (P2P) refererer til en fil som er ripet tapfritt fra en strømmetjeneste, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, osv., eller lastet ned via en online distribusjonsnettsted som iTunes. Kvaliteten er ganske god, siden de ikke er kodet på nytt. Videoen (H.264 eller H.265) og lyden (AC3/AAC) er vanligvis ekstrahert fra iTunes eller Amazon Video og remukset inn i en MKV-beholder uten å ofre kvaliteten. En fordel med disse utgivelsene er at de vanligvis ikke har nettverkslogoer på skjermen. Disse er nesten like gode som en Blu-ray-kilde, men kan lide av lydforsinkelse eller visuelle artefakter fra den adaptive bithastigheten til strømmetjenestene. Hvis en ripper mister internettforbindelsen til et punkt der bithastigheten senkes, kan kildebithastigheten endre seg dynamisk, noe som kan føre til variasjoner i bildekvaliteten. De fleste utgivelser som lider av en ekstrem mengde visuelle artefakter er NUKED, og en PROPER blir vanligvis utgitt for å fikse eventuelle ville variasjoner i adaptiv bithastighet. Dette vil være i 480p (SD) kvalitet.
- WEBRip-480p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokoller og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 480p (SD) kvalitet.
- DVD - En nykoding av den endelige utgitte DVD9. Hvis det er mulig, blir dette utgitt før butikksalget. Det skal være utmerket kvalitet (for oppløsningen). DVDrips blir vanligvis utgitt i DivX/XviD eller MP4.
- Bluray-480p - En nykoding av den endelige utgitte Blu-ray, nedskalert til 480p-oppløsning (720x480 @ 16:9, en annen sideforhold kan være en annen oppløsning). Hvis det er mulig, blir dette utgitt før butikksalget. Det skal være utmerket kvalitet for oppløsningen. Bitrater kan variere, men disse er vanligvis kodet til DivX, XviD eller AVC og tilbyr en liten oppfattet kvalitetsreduksjon i forhold til den opprinnelige kilden samtidig som filstørrelsen reduseres drastisk. Disse er vanligvis MKV eller MP4, men noen DivX/XviD er også tilgjengelige som bruker AVI.
- HDTV-720p - En nykoding av den endelige utgitte Blu-ray, men sendt over HD-kabel eller satellitt (1280x720 @ 16:9, en annen sideforhold kan være en annen oppløsning). Den kan være endret for kjøretid eller innhold avhengig av nettverket den kommer fra. Denne blir vanligvis utgitt flere måneder etter en butikkutgivelse, men noen ganger blir oppskalerte versjoner av en standard definisjonsfilm utgitt på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopiene av den spesifikke filmen som er tilgjengelig. Disse er vanligvis MKV eller MP4.
- HDTV-1080p - En nykoding av den endelige utgitte Blu-ray, men sendt over HD-kabel eller satellitt (1920x1080 @ 16:9, en annen sideforhold kan være en annen oppløsning). Den kan være endret for kjøretid eller innhold avhengig av nettverket den kommer fra. Denne blir vanligvis utgitt flere måneder etter en butikkutgivelse, men noen ganger blir oppskalerte versjoner av en standard definisjonsfilm utgitt på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopiene av den spesifikke filmen som er tilgjengelig. Disse er vanligvis MKV eller MP4-beholder.
- WEBRip-720p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokoller og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 720p kvalitet.
- Bluray-720p - En nykoding av den endelige utgitte Blu-ray, nedskalert til 720p-oppløsning (1280x720 @ 16:9, en annen sideforhold kan være en annen oppløsning). Hvis det er mulig, blir dette utgitt før butikksalget. Det skal være utmerket kvalitet for oppløsningen. Bitrater kan variere, men disse er vanligvis kodet til AVC eller HEVC og tilbyr en liten oppfattet kvalitetsreduksjon i forhold til den opprinnelige kilden samtidig som filstørrelsen reduseres drastisk. Disse er vanligvis MKV eller MP4-beholder.
- WEBDL-1080p - WEB-DL (P2P) refererer til en fil som er ripet tapfritt fra en strømmetjeneste, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, osv., eller lastet ned via en online distribusjonsnettsted som iTunes. Kvaliteten er ganske god, siden de ikke er kodet på nytt. Videoen (H.264 eller H.265) og lyden (AC3/AAC) er vanligvis ekstrahert fra iTunes eller Amazon Video og remukset inn i en MKV-beholder uten å ofre kvaliteten. En fordel med disse utgivelsene er at de vanligvis ikke har nettverkslogoer på skjermen. Disse er nesten like gode som en Blu-ray-kilde, men kan lide av lydforsinkelse eller visuelle artefakter fra den adaptive bithastigheten til strømmetjenestene. Hvis en ripper mister internettforbindelsen til et punkt der bithastigheten senkes, kan kildebithastigheten endre seg dynamisk, noe som kan føre til variasjoner i bildekvaliteten. De fleste utgivelser som lider av en ekstrem mengde visuelle artefakter er NUKED, og en PROPER blir vanligvis utgitt for å fikse eventuelle ville variasjoner i adaptiv bithastighet. Dette vil være i 1080p kvalitet.
- WEBRip-1080p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokoller og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 1080p kvalitet.
- Bluray-1080p - En nykoding av den endelige utgitte Blu-ray, i sin opprinnelige 1080p-oppløsning (1920x1080 @ 16:9, en annen sideforhold kan være en annen oppløsning). Hvis det er mulig, blir dette utgitt før butikksalget. Det skal være utmerket kvalitet og samme oppløsning som kilden. Bitrater kan variere, men disse er vanligvis kodet til AVC eller HEVC og tilbyr en liten oppfattet kvalitetsreduksjon i forhold til den opprinnelige kilden samtidig som filstørrelsen reduseres noe. Disse er vanligvis MKV eller MP4-beholder.
- Remux-1080p - En remux er en rip av en Blu-ray- eller HD DVD-plate til en annen beholderformat eller bare fjerner menyene og bonusmaterialet fra platen samtidig som innholdet i lyd- og videostreamene beholdes (også beholder de nåværende kodekene), og garanterer den nøyaktige 1:1 filmkvaliteten som på den opprinnelige platen. Dette er i 1080p kvalitet.
- HDTV-2160p - TVRip er en fangstkilde fra et fangstkort. HDTV står for fanget kilde fra HD-TV. Med en HDTV-kilde kan kvaliteten noen ganger til og med overgå DVD. Filmer i dette formatet begynner å bli populære. Noen annonser og kommersielle bannere kan sees på noen utgivelser under avspilling. Dette er i 2160p (4K) kvalitet.
- WEBDL-2160p - WEB-DL (P2P) refererer til en fil som er ripet tapfritt fra en strømmetjeneste, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, osv., eller lastet ned via en online distribusjonsnettsted som iTunes. Kvaliteten er ganske god, siden de ikke er kodet på nytt. Videoen (H.264 eller H.265) og lyden (AC3/AAC) er vanligvis ekstrahert fra iTunes eller Amazon Video og remukset inn i en MKV-beholder uten å ofre kvaliteten. En fordel med disse utgivelsene er at de vanligvis ikke har nettverkslogoer på skjermen. Disse er nesten like gode som en Blu-ray-kilde, men kan lide av lydforsinkelse eller visuelle artefakter fra den adaptive bithastigheten til strømmetjenestene. Hvis en ripper mister internettforbindelsen til et punkt der bithastigheten senkes, kan kildebithastigheten endre seg dynamisk, noe som kan føre til variasjoner i bildekvaliteten. De fleste utgivelser som lider av en ekstrem mengde visuelle artefakter er NUKED, og en PROPER blir vanligvis utgitt for å fikse eventuelle ville variasjoner i adaptiv bithastighet. Dette vil være i 2160p (4K) kvalitet.
- WEBRip-2160p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokoller og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 2160p (4K) kvalitet.
- Bluray-2160p - En nykoding av den endelige utgitte Blu-ray, i sin opprinnelige 2160p-oppløsning (3840x2160 @ 16:9, en annen sideforhold kan være en annen oppløsning). 4K-versjoner av filmer som er utgitt i generelt HEVC-kodek og kan være enten 8-bit eller 10-bit fargereproduksjon eller fra en HDR-kilde. Disse er vanligvis MKV eller MP4-beholder.
- Remux-2160p - En remux er en rip av en Blu-ray- eller HD DVD-plate til en annen beholderformat eller bare fjerner menyene og bonusmaterialet fra platen samtidig som innholdet i lyd- og videostreamene beholdes (også beholder de nåværende kodekene), og garanterer den nøyaktige 1:1 filmkvaliteten som på den opprinnelige platen. Dette er i 2160p (4K) kvalitet.

# Egendefinerte formater

{#custom-formats-2}

- Sørg for at du får riktig utgivelse hver gang! Egendefinerte formater gir fin kontroll over prioritering og valg av utgivelser. Det kan være så enkelt som et enkelt foretrukket ord eller så komplekst som du ønsker med flere kriterier og regex.
- Egendefinerte formater beregnes dynamisk i stedet for å bli lagret i databasen, slik at de oppdateres så snart du endrer definisjonene.
- Egendefinerte formater brukes innenfor kvalitetsprofilene dine for å bestemme poengsummen for hvert egendefinerte format. Innenfor hver kvalitetsprofil kan du sette en minimum poengsum for et utgivelse for å bli lastet ned, og også en oppgraderingspoengsum.
- Det anbefales sterkt å legge til følgende egendefinerte formater fra [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) for å unngå uønskede nedlastinger. Se TRaSH Guide Custom Format-artikkelen og de tre andre TRaSH Custom Format Guides som er referert til øverst på siden for Collection of Custom Formats for mer informasjon.
  - [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) vil unngå å laste ned utgivelser med Dolby Vision (DV) som har en grønn fargetone hvis DV ikke støttes.
  - [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) for å unngå å laste ned dårlig navngitte BR-DISKer som ikke samsvarer med BR-DISK-kvalitetsanalyse.

---

- Navn - Navnet på det egendefinerte formatet
- Inkluder egendefinert format ved navngiving - Inkluder navnet på det egendefinerte formatet ved navngiving?

> Egendefinerte formater har ingen innvirkning på hva som blir søkt etter - bare hvordan resultatene blir evaluert. Det er heller ikke mulig å endre på noen måte søket Radarr bruker.
{.is-info}

Profiler er der egendefinerte formatpoengsum blir konfigurert.

## Egendefinerte formatbetingelser

### Modifikatorer

- Negere - samsvar er invertert, så betingelsen er oppfylt bare hvis den ikke-negerte betingelsen ikke er oppfylt
- Påkrevd - gjelder bare for formater med mer enn én betingelse av samme type og endrer reglene for samsvar for typegrupper. Hvis denne opsjonen er aktivert, betyr det at denne spesifikke betingelsen må være oppfylt for at det egendefinerte formatet skal gjelde, uavhengig av om en annen betingelse av samme type ellers ville oppfylt typegruppen. **Merk: Du bruker bare dette hvis du bruker en betingelse mer enn én gang. Med andre ord, hvis du har et egendefinert format med 2 påkrevde betingelser for utgivelsestittel og 3 ikke-påkrevde språkbetingelser, må det oppfylle BEGGE de påkrevde betingelsene for utgivelsestittel og det må oppfylle EN AV de 3 språkbetingelsene.** På samme måte, hvis du har et egendefinert format med 4 utgivelsestittelbetingelser og ingen er påkrevd, vil det egendefinerte formatet gjelde hvis EN AV betingelsene er oppfylt.

### Betingelser

> **Forskjellige betingelsestyper** fungerer som `og` innenfor samme egendefinerte format. **Flere betingelser av samme type** fungerer som `eller` med mindre Påkrevd brukes
{.is-info}

- **Alle betingelser som bruker RegEx er ikke forskjellsensitiv**
- Merk følgende GitHub-issues
  - [Custom Formats do not apply before the Movie Year in release titles #4859](https://github.com/Radarr/Radarr/issues/4859)
  - [Custom Format doesn't match for term "xvid" at end of release name #6824](https://github.com/Radarr/Radarr/issues/6824)
- Utgivelsestittel - Dette er et regulært uttrykk som sammenlignes med utgivelsestittelen og, etter nedlasting, filnavnet på disken.
  - Merk: Radarr vurderer bare tekst etter filmtittelen og år, noe som betyr at alt som kommer før tittelen blir ignorert.
- Utgave - Denne taggen sammenlignes med eventuelle utgaver Radarr kan analysere. Du kan sette inn hvilken som helst verdi som Radarr vil prøve å sammenligne med det som ble analysert (ikke forskjellsensitivt).
- Språk - Dette språket sammenlignes med eventuelle språk Radarr analyserer. Alle språk som tidligere var valgbare i profiler fungerer her.
- [Indekseringsflagg](/radarr/settings#indexer-flags) - Denne taggen sammenlignes med eventuelle indekseringsflagg som Radarr kan analysere.
- Kilde - Kilden der en utgivelse ble ripet fra (f.eks. BLURAY).
- Oppløsning - Oppløsningen som ble analysert fra enten utgivelsesnavnet eller mediainfo (hvis tilgjengelig).
- Kvalitetsmodifikator - Kvalitetsmodifikator setter ting som Telescene, Telesync, Remux, Regional. Den skiller en gitt kilde og oppløsningspar når det er flere kvalitets (kilde) typer som kan brukes.
- Størrelse - Dette sammenlignes med utgivelsesstørrelsen. Utgivelsesstørrelsen konverteres til gigabyte og sammenlignes med min- og maksverdiene.
- Gruppe - Dette sammenlignes med gruppen som Radarr analyserer basert på Radarrs gruppedeteksjonslogikk.

### Profilinnstillinger og rangering

- Egendefinerte formater implementeres innenfor og har sin innvirkning kontrollert av kvalitetsprofiler. Oppgraderingspoengsummen forhindrer oppgradering når en utgivelse med denne ønskede poengsummen er lastet ned.
- En poengsum på 0 resulterer i at det egendefinerte formatet bare er informativt og har ingen innvirkning på rangering av utgivelser eller søkte språk.
- Minimumspoengsummen krever at utgivelser kumulativt egendefinert formatpoengsum når denne terskelen, ellers vil de bli avvist.
  - Egendefinerte formater som samsvarer med uønskede attributter, bør få en negativ poengsum for å redusere attraktiviteten deres.
  - Fullstendige avvisninger bør få en negativ poengsum som er lav nok til at selv om alle de andre formatene med positive poengsummer ble lagt til, ville poengsummen fortsatt falle under minimumet.
- [Se TRaSH's Guides for hvordan du setter opp og bruker egendefinerte formater](https://trash-guides.info/Radarr/Radarr-setup-custom-formats/)

#### Importering / Eksportering av egendefinerte formater

- [Se TRaSH's Guides for hvordan du importerer/eksporterer egendefinerte formater.](https://trash-guides.info/Radarr/Radarr-import-custom-formats/) Du kan imidlertid importere og eksportere egendefinerte formater.

#### Importering / Oppdatering av eksisterende egendefinerte formater

- [Se TRaSH's Guides for hvordan du importerer eller oppdaterer eksisterende egendefinerte formater.](https://trash-guides.info/Radarr/Radarr-how-to-update-custom-formats/)

### Samling av egendefinerte formater

- [TRaSH vedlikeholder en samling av egendefinerte formater](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)

# Indekseringsverktøy

> Informasjon om støttede indekseringsverktøy finner du på siden [Mer informasjon (Støttet)](/radarr/supported#indexers) for denne delen
{.is-info}

## Støttede indekseringsverktøy

- En liste over støttede indekseringsverktøy finnes på siden [Mer informasjon (Støttet)](/radarr/supported#indexers)

### Innstillinger for indekseringsverktøy

- Når du har klikket på <kb>+</kb>-knappen for å legge til et nytt indekseringsverktøy, får du en ny dialogboks med mange forskjellige alternativer. For formålet med denne wikien betrakter Radarr både Usenet-indekseringsverktøy og torrentsporere som "indekseringsverktøy".

- Det er to seksjoner her: Usenet og Torrents. Basert på hvilken nedlastingsklient du vil bruke, må du velge typen indekseringsverktøy du vil bruke.

### Konfigurasjon av Usenet-indekseringsverktøy

- Newznab - Her finner du forhåndsinnstillinger for populære Usenet-indeksere (som er forhåndsutfylt, alt du trenger er API-nøkkelen din som blir gitt av Usenet-indeksen du velger) sammen med muligheten til å opprette en tilpasset indekser
- Programvare som fungerer med Usenet og integrerer godt med Radarr er [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr) som integrerer med både Usenet og Torrents
- Uavhengig av om du velger en forhåndsutfylt indekser eller en tilpasset indekseroppsett, vil du bli presentert med et nytt vindu for å legge inn alle innstillingene dine
- Velg mellom forhåndsinnstillingene eller legg til en tilpasset indekser (som NZBHydra2 eller Prowlarr)
- Navn - Navnet på indeksen i Radarr
- Aktiver RSS - Hvis aktivert, bruk denne indeksen for å se etter filer som er ønsket og mangler eller ikke har nådd cutoff.
- Aktiver automatisk søk - Hvis aktivert, bruk denne indeksen for automatisk søk, inkludert søk ved tillegg
- Aktiver interaktivt søk - Hvis aktivert, bruk denne indeksen for manuelle interaktive søk.
- URL - URL-en som er oppgitt av indeksen, for eksempel `https://api.nzbgeek.info`.
- API-sti - API-stien som er oppgitt av indeksen. Dette er vanligvis `/api`
- Flerspråklig - Angi hvilke språk `MULTI` som er for denne indeksen.
- API-nøkkel - API-nøkkelen som er oppgitt av indeksen for å få tilgang til API-et.
- Kategorier - Standardkategorier vil bli brukt med mindre de blir redigert. Det er sannsynlig at disse standardkategoriene ikke er optimale. Når du redigerer denne innstillingen, spør Radarr indeksen om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir slått av eller på.
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere for Newznab som skal legges til i spørringslenken
- Fjern år fra søkestrengen - Skal Radarr fjerne året etter filmtittelen når det søkes på denne indeksen?
- (Avansert alternativ) Indekserprioritet - Prioritet for denne indeksen for å foretrekke en indeks over en annen i utgivelseskonfliktsituasjoner. 1 er høyeste prioritet og 50 er laveste prioritet.
- (Avansert alternativ) Nedlastingsklient - Velg og spesifiser hvilken nedlastingsklient som brukes for nedlastinger fra denne indeksen
- Merker - Bruk bare denne indeksen for filmer med minst ett matchende merke. La være blankt for å bruke med alle filmer.

### Konfigurasjon av torrentsporere

- På samme måte som med Usenet er det en rekke forhåndsutfylte torrentsporingsinformasjon. Hvis du ikke er medlem av noen av disse spesifikke sporerne, vil de ikke være til nytte for deg.
- En av de beste og enkleste måtene å bruke torrentsporere som ikke støttes naturlig med Radarr, er å bruke et annet program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Disse programmene fungerer godt sammen med Radarr som en søkeindekser som inneholder all informasjonen din og sender den til Radarr.
- Torznab - Dette alternativet vil sette deg opp med en Jackett-forhåndsinnstilling, hvis du bruker flere sporer, må hver oppføring ha et unikt navn
- Torznab-indeks
- Velg mellom forhåndsinnstillingene eller legg til en tilpasset indekser (som Jackett)
- Navn - Navnet på indeksen i Radarr
- Aktiver RSS - Hvis aktivert, bruk denne indeksen for å se etter filer som er ønsket og mangler eller ikke har nådd cutoff.
- Aktiver automatisk søk - Hvis aktivert, bruk denne indeksen for automatisk søk, inkludert søk ved tillegg
- Aktiver interaktivt søk - Hvis aktivert, bruk denne indeksen for manuelle interaktive søk.
- URL - URL-en som er oppgitt av indeksen, for eksempel `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sti - API-stien som er oppgitt av indeksen. Dette er vanligvis `/api`
- API-nøkkel - API-nøkkelen som er oppgitt av indeksen for å få tilgang til API-et.
- Flerspråklig - Angi hvilke språk `MULTI` som er for denne indeksen.
- Kategorier - Standardkategorier vil bli brukt med mindre de blir redigert. Det er sannsynlig at disse standardkategoriene ikke er optimale. Når du redigerer denne innstillingen, spør Radarr indeksen om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir slått av eller på.
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere for Torznab som skal legges til i spørringslenken
- Fjern år fra søkestrengen - Skal Radarr fjerne året etter filmtittelen når det søkes på denne indeksen?
- Minimum antall seedere - Minimum antall seedere som kreves for at en utgivelse fra denne sporeren skal bli lastet ned.
- Seedratio - Hvis tomt, bruker nedlastingsklienten standardverdien. Ellers er minimum seedratio som kreves for at nedlastingsklienten din skal oppfylle for utgivelser fra denne indeksen før den blir satt på pause av klienten din og fjernet av Radarr (krever håndtering av fullførte nedlastinger - fjerning er aktivert)
- Seedtid - Hvis tomt, bruker nedlastingsklienten standardverdien. Ellers er minimum seedtid i minutter som kreves for at nedlastingsklienten din skal oppfylle for utgivelser fra denne indeksen før den blir satt på pause av klienten din og fjernet av Radarr (krever håndtering av fullførte nedlastinger - fjerning er aktivert)
- Påkrevde flagg - Hvilke indeksflagg er påkrevd?

#### Indeksflagg

| Flag             | Symbol | Beskrivelse                                                                                                                                                                                                                   |
| ---------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `G_Freeleech`    | ⬇⬇     | Noen ganger setter torrent-nettsteder en torrent til å være freeleech. Dette betyr at nedlastingen av denne torrenten ikke vil telle mot kvoten eller forholdet ditt. Dette er veldig nyttig hvis du ennå ikke har bygget opp et godt forhold. |
| `G_Halfleech`    | ⇩⇩     | Lignende som `G_Freeleech`, betyr `G_Halfleech` at bare halvparten av størrelsen på denne torrenten vil telle mot kvoten eller forholdet ditt.                                                                                   |
| `G_DoubleUpload` | ⬆      | Lignende som `G_Freeleech`, betyr `G_DoubleUpload` at all data du laster opp via seeding blir telt dobbelt mot kvoten og forholdet ditt. Dette er veldig nyttig hvis du vil bygge opp en forholdsbuffe.                             |
| `PTP_Golden`     | 🌟      | På PassThePopcorn får noen torrents *Golden*-merket når de oppfyller visse kodingsstandarder. Dette er vanligvis de beste kodene, med nesten ingen merkbar kvalitetstap. Du kan lære mer på wiki-siden deres.                   |
| `PTP_Approved`   | ✔      | På PassThePopcorn blir noen torrents godkjent når de oppfyller minimumsstandardene for koding (f.eks. ingen lave bithastigheter). Se wikien deres for mer informasjon.                                                        |
| `HDB_Internal`   | 🚪      | Utgivelser på HDBits får dette merket når utgivelsen ble lastet opp av en av utgivelsesgruppene til HDBits selv.                                                                                                               |
| `G_Scene`        | ☠      | Lignende som `G_Freeleech`, betyr `G_Freeleech75` at bare 25% av størrelsen på denne torrenten vil telle mot kvoten eller forholdet ditt.                                                                                     |
| `G_Freeleech75`  | ⇩⬇     | Lignende som `G_Freeleech`, betyr `G_Freeleech75` at bare 25% av størrelsen på denne torrenten vil telle mot kvoten eller forholdet ditt.                                                                                     |
| `G_Freeleech25`  | ⇩      | Lignende som `G_Freeleech`, betyr `G_Freeleech25` at bare 75% av størrelsen på denne torrenten vil telle mot kvoten eller forholdet ditt.                                                                                     |

- (Avansert alternativ) Indekserprioritet - Prioritet for denne indeksen for å foretrekke en indeks over en annen i utgivelseskonfliktsituasjoner. 1 er høyeste prioritet og 50 er laveste prioritet.
- (Avansert alternativ) Nedlastingsklient - Velg og spesifiser hvilken nedlastingsklient som brukes for nedlastinger fra denne indeksen
- Merker - Bruk bare denne indeksen for filmer med minst ett matchende merke. La være blankt for å bruke med alle filmer.

## Alternativer

- Minimumsalder - Kun Usenet: Minimumsalder i minutter for NZB-er før de blir lastet ned. Bruk dette for å gi nye utgivelser tid til å spre seg til Usenet-leverandøren din.
- Oppbevaring - Kun Usenet: Sett til null for ubegrenset oppbevaring
- Maksimal størrelse - Maksimal størrelse for en utgivelse som skal lastes ned i MB. Sett til null for ubegrenset. Vær oppmerksom på at dette gjelder globalt.
- Foretrekk indeksflagg - Prioriter utgivelser med spesielle flagg. (Se Påkrevde flagg ovenfor)
- Tilgjengelighetsforsinkelse - Tidsperiode før (-#) eller etter (#) tilgjengelighetsdatoen for å søke etter filmen
  - Dette er nyttig for å forsinke søket etter en utgivelse for å gi fellesskapet tid til å utføre de beste kodene.
  - Vanligvis anbefales en filmtilgjengelighet på `Utgitt` med en forsinkelse på `-21` eller `-14`.
- RSS-synkroniseringsintervall - Intervall i minutter. Sett til null for å deaktivere (dette vil stoppe all automatisk utgavehenting) Minimum: 10 minutter Maksimum: 120 minutter
  - Se [Hvordan finner Radarr filmer?](/radarr/faq#how-does-radarr-find-movies) for bedre forståelse av hvordan RSS-synkronisering vil hjelpe deg

> Hvis Radarr har vært frakoblet i en lengre periode, vil Radarr forsøke å bla tilbake for å finne den siste utgivelsen den behandlet for å unngå å gå glipp av en utgivelse. Så lenge indeksen din støtter paging og det ikke har gått for lang tid, vil Radarr kunne behandle utgivelsene den ville ha gått glipp av og unngå at du må søke etter de utgivelsene du gikk glipp av.{.is-info}

- Whitelistede undertittelmerker - Merker som legges inn her, vil ikke bli betraktet som hardkodede undertekster.
- Tillat hardkodede undertekster - Hvis aktivert, tillat at utgivelser med hardkodede undertekster lastes ned automatisk

# Nedlastingsklienter

> Informasjon om støttede nedlastingsklienter finner du på siden [Mer informasjon (Støttet)](/radarr/supported#download-clients) for denne delen
{.is-info}

## Oversikt

- Nedlasting og import er der de fleste opplever problemer. Fra et overordnet perspektiv må programvaren kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det er et stort utvalg av støttede nedlastingsklienter og enda flere forskjellige oppsett. Dette betyr at selv om det er noen vanlige oppsett, er det ikke ett riktig oppsett, og alle oppsett kan være litt forskjellige. Men det er mange feilaktige oppsett.

## Prosesser for nedlastingsklienter

### Usenet-prosess

- Radarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: filmer, tv, serier, musikk, osv.
- Radarr vil overvåke de aktive nedlastingene i nedlastingsklienten din som bruker det kategorinavnet. Den overvåker dette via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Radarr kjenne den endelige filplasseringen som rapportert av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din og tilgjengelig for Radarr
- Radarr vil skanne den fullførte filplasseringen etter filer som Radarr kan bruke. Den vil analysere filnavnet for å matche det med forespurt media. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til angitt medieplassering.
- Atomiske flyttinger (øyeblikkelige flyttinger) er aktivert som standard. Filsystemet og monteringspunktene må være de samme for fullføringsmappen og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Radarr falle tilbake og kopiere filen og deretter slette den fra kilden, noe som er I/O-intensivt.

### Torrent-prosess

- Radarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: filmer, tv, serier, musikk, osv.
- Radarr vil overvåke de aktive nedlastingene i nedlastingsklienten din som bruker det kategorinavnet. Denne overvåkingen skjer via nedlastingsklientens API.
- Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Radarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil Radarr opprette en hardlenke til filen hvis det støttes av oppsettet ditt, eller kopiere hvis hardlenker ikke støttes.
- Hardlenker er aktivert som standard. [En hardlenke vil ikke bruke noe ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for fullføringsmappen og mediebiblioteket ditt. Hvis opprettelsen av hardlenken mislykkes eller oppsettet ditt ikke støtter hardlenker, vil Radarr falle tilbake og kopiere filen.
- Hvis alternativet "Fullførte nedlastingshåndtering - Fjern" er aktivert i Radarrs innstillinger, vil Radarr slette den opprinnelige filen og torrenten fra klienten din, men bare hvis klienten rapporterer at seeding er fullført og torrenten er stoppet (dvs. satt på pause).

## Nedlastingsklienter

Klikk på `Innstillinger => Nedlastingsklienter`, og klikk deretter på <kb>+</kb> for å legge til en ny nedlastingsklient. Nedlastingsklienten din bør allerede være konfigurert og kjøre.

### Støttede nedlastingsklienter

- En liste over støttede nedlastingsklienter finner du på siden [Mer informasjon (Støttet)](/radarr/supported#download-clients)

Velg nedlastingsklienten du ønsker å legge til, og det vil vises en popup-boks der du kan angi tilkoblingsdetaljer. Disse detaljene er like for de fleste klienter. Noen vil be om et brukernavn eller passord, noen vil spørre om du vil legge til nye nedlastinger i en pauset/start-tilstand, osv.

### Innstillinger for Usenet-klient

- Navn - Navnet på nedlastingsklienten i Radarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- API-nøkkel - API-nøkkelen for å autentisere mot klienten din
- Brukernavn - brukernavnet for å autentisere mot klienten din (vanligvis ikke nødvendig)
- Passord - passordet for å autentisere mot klienten din (vanligvis ikke nødvendig)
- Kategori - kategorien i nedlastingsklienten din som \*Arr vil bruke. For å unngå at irrelevante nedlastinger vises i aktiviteten, anbefales det sterkt å angi en kategori.
- Nylig prioritet - nedlastingsklientprioritet for nylig utgitte medier
- Eldre prioritet - nedlastingsklientprioritet for medier som ikke nylig er utgitt
- (Avansert alternativ) Klientprioritet - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet og 50 er laveste prioritet
- Fullført nedlastingshåndtering
  - Fjern (Per klientinnstilling) - Fjern fullførte nedlastinger når de er ferdige (usenet) eller stoppet/fullført (torrenter). Se [Fullført nedlastingshåndtering for mer informasjon](#completed-download-handling)

### Innstillinger for torrentklient



- Navn - Navnet på nedlastingsklienten i Radarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URLen til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din; dette er vanligvis webgui-porten
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URLen; dette er vanligvis nødvendig for omvendte proxyer.
- Brukernavn - brukernavnet for å autentisere deg mot klienten din
- Passord - passordet for å autentisere deg mot klienten din
- Kategori - kategorien i nedlastingsklienten din som \*Arr vil bruke. For å unngå irrelevante nedlastinger som vises i Aktivitet, anbefales det sterkt å angi en kategori.
- Kategori etter import - kategorien som skal angis etter at utgivelsen er lastet ned og importert. Vær oppmerksom på at dette bryter med fjerning av fullførte nedlastinger.
- Nylig prioritet - nedlastingsklientprioritet for nylig utgitte medier
- Eldre prioritet - nedlastingsklientprioritet for medier som ikke nylig er utgitt
- Innledende tilstand - Innledende tilstand for torrents (bare Qbittorrent: Tvinger forbi alle seed-grenser)
- (Avansert alternativ) Klientprioritet - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet og 50 er laveste prioritet
- Håndtering av fullførte nedlastinger
  - Fjern (Per klientinnstilling) - Fjern fullførte nedlastinger når de er ferdige (usenet) eller stoppet/fullført (torrenter). Se [Håndtering av fullførte nedlastinger for mer informasjon](#håndtering-av-fullførte-nedlastinger)
    - For torrenter krever dette at nedlastingsklienten din setter på pause når seed-målene er nådd. Det krever også at seed-målene støttes av Radarr i henhold til tabellen nedenfor. Torrenter må også være i samme kategori.

### Kompatibilitet for fjerning av nedlastinger for torrentklienter

- Radarr kan bare angi seed-forhold/tid på klienter som støtter å sette denne verdien via APIen når torrenten legges til. Seed-mål kan settes globalt i klienten selv eller per tracker i \*Arr-innstillingene for hver indekser. Se tabellen nedenfor for klientkompatibilitet.

|      Klient       |                                Forhold                                |                                   Tid                                    |
| :---------------: | :------------------------------------------------------------------: | :-----------------------------------------------------------------------: |
|       Aria2       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|      Deluge       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
| Download Station  | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|       Flood       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     Hadouken      | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|    qBittorrent    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     rTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
| Torrent Blackhole | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-kritisk)   |
|   Transmission    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Støttet-Idle%20Limit*-blue)\* |
|     uTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|       Vuze        |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Støttet-Idle%20Limit*-blue) - Transmission har internt en inaktivitetssjekk, men Radarr sammenligner den med seedetiden hvis inaktivitetsgrensen er satt per torrent. Dette gjøres som en løsning på Transmission sin API-begrensning.{.is-info}

## Håndtering av fullførte nedlastinger

- Håndtering av fullførte nedlastinger er hvordan Radarr importerer medier fra nedlastingsklienten din til serie-mappene dine. Mange vanlige problemer er relatert til dårlige Docker-stier og/eller andre Docker-tilgangsproblemer.

- (Avansert global innstilling) Aktiver - Importer fullførte nedlastinger automatisk fra nedlastingsklienten
- (Avansert alternativ) Sjekk etter fullførte nedlastinger intervall - Angi hvor ofte du vil spørre nedlastingsklientens køer og oppdatere overvåkede nedlastinger, minimum 1 minutt
- (Per klientinnstilling) Fjern - Fjern fullførte nedlastinger når de er ferdige (usenet) eller stoppet/fullført (torrenter)
  - For torrenter krever dette at nedlastingsklienten din setter på pause når seed-målene er nådd. Det krever også at seed-målene støttes av Radarr i henhold til tabellen ovenfor. Torrenter må også være i samme kategori.

### Fjern fullførte nedlastinger

- Radarr sender en nedlastingsforespørsel til klienten din og tilknytter den med en etikett eller kategorinavn som du har konfigurert i innstillingene for nedlastingsklienten.
- Radarr overvåker aktive nedlastinger i nedlastingsklienten din som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vet Radarr den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din.
- Radarr skanner denne fullførte filplasseringen etter videofiler. Den analyserer videofilnavnet for å matche det med en film. Hvis den kan gjøre det, vil den gi filen et nytt navn i henhold til dine spesifikasjoner og flytte den til den tilordnede bibliotekmappen.
- Overflødige filer fra nedlastingen sendes til papirkurven eller resirkuleringen.

Hvis du laster ned ved hjelp av en BitTorrent-klient, er prosessen litt annerledes:

- Fullførte filer blir liggende på sin opprinnelige plassering for å tillate seeding. Når filene importeres til den tilordnede bibliotekmappen, vil Radarr forsøke å opprette en hardlink til filen eller falle tilbake til å kopiere (bruk dobbelt plass) hvis hardlinker ikke støttes.
- Hvis alternativet "Håndtering av fullførte nedlastinger - Fjern" er aktivert i innstillingene, vil Radarr be torrentklienten om å slette den opprinnelige filen og torrenten, men dette vil bare skje hvis klienten rapporterer at seeding er fullført, torrenten er i samme kategori (dvs. ikke bruker en post-import-kategori), seed-målet som er nådd, støttes av Radarr, og torrenten er satt på pause (stoppet).

### Håndtering av mislykkede nedlastinger

- Håndtering av mislykkede nedlastinger er bare kompatibel med SABnzbd og NZBGet.
- Håndtering av mislykkede nedlastinger gjelder ikke for torrenter, og det er heller ingen planer om å legge til en slik funksjonalitet.

- Det er flere komponenter som utgjør prosessen for håndtering av mislykkede nedlastinger:

- Sjekk nedlaster:
  - Kø - Sjekk nedlasterens kø for passordbeskyttede (krypterte) utgivelser som er merket som mislykket
  - Historikk - Sjekk nedlasterens historikk for mislykkede nedlastinger (f.eks. ikke nok til å reparere, eller utpakking mislyktes)
- Når Radarr finner en mislykket nedlasting, begynner den å behandle dem og gjør noen ting:
  - Legger til en mislykket hendelse i Radarrs historikk
  - Fjerner den mislykkede nedlastingen fra nedlastingsklienten for å frigjøre plass og fjerne nedlastede filer (valgfritt)
  - Begynner å søke etter en erstatningsfil (valgfritt)
  - Blokkeringsliste (tidligere kjent som 'Blacklisting') tillater automatisk hopping over nzbs når de mislykkes, dette betyr at nzb aldri vil bli lastet ned automatisk av Radarr igjen (du kan fortsatt tvinge nedlastingen via et manuelt søk).
  - Det er 2 avanserte alternativer (på siden for innstillinger for 'Nedlastingsklient') som kontrollerer oppførselen til mislykkede nedlastinger i Radarr, for øyeblikket er de alle aktivert som standard.

- Last ned på nytt - Kontrollerer om Radarr skal søke etter samme fil etter en feil
- (Avansert alternativ) Fjern - Om nedlastingen automatisk skal fjernes fra nedlastingsklienten når feilen oppdages

## Eksterne stiavbildninger

- Eksterne stiavbildninger fungerer som en enkel søk etter ekstern sti og erstatt med lokal sti. Dette brukes hovedsakelig for enten sammenslåtte lokale/eksterne oppsett ved hjelp av mergerfs eller lignende, eller når applikasjonen og nedlastingsklienten ikke er på samme server.
- En ekstern stiavbildning brukes når nedlastingsklienten din rapporterer en sti for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er en ekstern stiavbildning bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows eller omvendt. En ekstern stiavbildning kan også være nødvendig hvis du blander Docker- og Native-klienter eller hvis du bruker en ekstern server.
- En ekstern stiavbildning er en ENKEL søk/erstatt (hvor den finner VERDIEN for EKSTERN, erstatt den med VERDIEN for LOKAL for den angitte verten).
- Hvis feilmeldingen om en ugyldig sti ikke inneholder VERDIEN SOM ER ERSTATTET, fungerer ikke stiavbildningen som forventet. Den vanlige løsningen er å legge til og fjerne avbildningen.
- [Se TRaSHs opplæring for mer informasjon om ekstern stiavbildning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-containere, er det sjelden behov for en ekstern stiavbildning. Det anbefales å [gjennomgå Docker-guiden](/docker-guide) og/eller [følge TRaSHs opplæring](https://trash-guides.info/hardlinks)
{.is-info}

# Importlister

> Informasjon om støttede listeformater finner du på siden [Mer informasjon (Støttet)](/radarr/supported#lists) for denne delen
{.is-info}

## Lister

Importlister er en del av Radarr som lar deg følge en bestemt listeoppretter. La oss si at du følger en bestemt listeoppretter på Trakt/TMDb og virkelig liker deres ArrowVerse Collection-seksjon og vil se alle showene på listen deres. Du ser i Radarr og innser at du ikke har disse seriene. I stedet for å søke etter dem en etter en og legge dem til og deretter søke etter dem på indekserne dine. Du kan gjøre alt dette på en gang med en liste. Listene kan settes til å importere alle seriene på den kuratorens liste, samt å automatisk tilordne en kvalitetsprofil, automatisk legge til og automatisk overvåke den serien.

- ADVARSEL: Hvis lister blir gjort feil, vil de absolutt ødelegge biblioteket ditt med en haug med søppel du ikke har til hensikt å se. Så sørg for at du vet hva du importerer før du klikker på lagre. Dvs. se på listen fysisk før du går til Radarr.

- Her kan du velge <kb>+</kb>-knappen for å åpne et nytt popup-vindu
- I dette nye vinduet får du mange forskjellige alternativer for å sette opp listen din fra mange forskjellige listeleverandører. Som nevnt tidligere, vær forsiktig med lister. Det anbefales sterkt å ikke velge "Søk ved legging til"-knappen før du er helt sikker på at listen du velger/oppsetter legger til seriene du leter etter.
- Når du har valgt listeleverandøren du vil hente fra (for eksempel IMDb eller Trakt), får du presentert et nytt vindu.
De fleste innstillingene for lister er ganske selvforklarende, noen lister krever at du autentiserer deg med leverandøren, for eksempel Trakt (som krever at du har en konto hos Trakt.tv)

## Listealternativer

- (Avansert alternativ) Oppdateringsintervall for liste - Hvor ofte skal Radarr sjekke listen for oppdateringer? [Dette er minimum 6 timer.](/radarr/faq#why-are-lists-sync-times-so-long-and-can-i-change-it)
- (Avansert alternativ) Nivå for rensing av bibliotek - Filmer i biblioteket vil bli fjernet eller ikke overvåket hvis de ikke er på listen(e) dine
  - Deaktivert - Ikke rens biblioteket (anbefales)
  - Kun logg - Bare logg filmene som ikke er på listen(e) og utfør ingen andre handlinger
  - Behold og ikke overvåk film - Behold filmer som ikke er på listen(e), men ikke overvåk dem i Radarr.
  - Fjern film og behold filer - Fjern filmer som ikke er på listen(e) fra Radarr, men ikke slett filene deres
  - Fjern film og slett filer - Fjern filmer som ikke er på listen(e) fra Radarr og slett filene deres

## Ekskludering av lister

- Ekskludering av importliste - Dette lar deg fjerne filmer du ikke ønsker å se igjen fra listen din. Et eksempel på dette er hvis listen din tilfeldigvis inneholder en film som er på et fremmed språk og det er lite sannsynlig at du noensinne vil finne denne filmen på ditt morsmål og ikke ønsker å se den med undertekster. Du kan ekskludere en film fra å bli lagt til i fremtiden. Imidlertid kan du legge den tilbake i listen i eksklusjonsdelen, slik at når listen kjører igjen, vil den bli lest inn i biblioteket ditt.

# Koble til

> Informasjon om støttede tilkoblingstyper finner du på siden [Mer informasjon (Støttet)](/radarr/supported#notifications) for denne delen
{.is-info}

## Tilkoblinger

Tilkoblinger er hvordan du vil at Radarr skal kommunisere med omverdenen.

- Ved å trykke på <kb>+</kb>-knappen vil du få opp et nytt vindu som lar deg konfigurere mange forskjellige endepunkter

- En liste over støttede varsler og tilkoblinger finnes på siden [Mer informasjon (Støttet)](/radarr/supported#notifications)

## Tilkoblingstriggere

- Ved henting - Få beskjed når filmer er tilgjengelige for nedlasting og har blitt sendt til en nedlastingsklient
- Ved import - Få beskjed når filmer er importert vellykket
- Ved oppgradering - Få beskjed når filmer oppgraderes til bedre kvalitet
- Ved omdøping - Få beskjed når filmer blir omdøpt
- Ved tillegg av film - Få beskjed når filmer blir lagt til Radarrs bibliotek for administrering eller overvåking
- Ved sletting av film - Få beskjed når filmer blir slettet
- Ved sletting av fil for film - Få beskjed når filer for filmer blir slettet
- Ved sletting av fil for oppgradering - Få beskjed når filer for filmer blir slettet for oppgraderinger
- Ved helseproblem - Få beskjed om helsekontrollfeil
  - Inkluder helseadvarsler - Få beskjed om helseadvarsler i tillegg til feil.
- Ved oppdatering av applikasjonen - Få beskjed når Radarr blir oppdatert til en ny versjon

# Metadata

## Alternativer

- Sertifiseringsland - Velg landet som skal brukes for filmklassifiseringer (f.eks. R (US) eller 12A (UK))

## Metadataforbrukere

> Informasjon om støttede metadataforbrukere finner du på siden [Mer informasjon (Støttet)](/radarr/supported#metadata) for denne delen
{.is-info}

Her kan du velge hvilken type metadata som skal brukes av mediespilleren din

Kodi vil være en av de mest brukte alternativene her hvis det er programvaren som brukes. Dette vil tillate Radarr å opprette en NFO-fil samt tilhørende filmpostere som skal hentes inn i spilleren din

# Merker

- Merkeseksjonen i Radarr brukes til å koble forskjellige aspekter av Radarr sammen. De er også nyttige for å spore hvilke filmer som kommer fra hvilke lister.
- Merker er spesielt nyttige for:

  - Forsinkelsesprofiler
  - Restriksjoner
  - Indekser

- Merker kan brukes til å koble Forsinkelsesprofiler, Indekser og Restriksjoner og Filmer sammen.
- For eksempel:
  - Du vil bare at en bestemt indekser skal brukes for en bestemt film. Du ville opprette et merke og tilordne filmen og indeksen det merket.
  - Du vil at en bestemt restriksjon bare skal gjelde for en bestemt film. Du ville opprette et merke og tilordne restriksjonen og filmen det merket.
  - Denne prosessen gjelder også for Forsinkelsesprofiler.

> En film vil bruke både indekser som har samsvarende merker og indekser som ikke har merker.
{.is-warning}

> Merk: Merker påvirker ikke "Tilpassede formater", "Kvalitetsprofiler" eller noen andre aspekter som ikke er nevnt ovenfor.
{.is-info}

# Generelt

## Vert

- Bind Address - Gyldig IPv4-adresse eller '*' for alle grensesnitt
  - 0.0.0.0 eller `*` - alle adresser kan koble til
  - 127.0.0.1 eller localhost - bare lokale applikasjoner kan koble til
  - Enhver annen IP (f.eks. 1.2.3.4) - bare den IP-adressen (1.2.3.4) kan koble til
- Portnummer - Portnummeret du ønsker å bruke for å få tilgang til webgrensesnittet for Radarr

> Merk: Hvis du bruker Docker, ikke endre denne innstillingen.
{.is-warning}

- URL-base - For støtte for omvendt proxy, standard er tom

> Merk: Hvis du bruker en omvendt proxy (for eksempel: mydomain.com/radarr), skriver du inn '/radarr' for URL-base.
{.is-info}

- Aktiver SSL - Hvis du har SSL-legitimasjon og ønsker å sikre kommunikasjonen til og fra Radarr, aktiverer du dette alternativet.

> Merk: Ikke bruk dette med mindre du vet hva du gjør.
{.is-warning}

## Sikkerhet

- Autentisering - Hvordan vil du autentisere for å få tilgang til Radarr-instansen din
  - Fra og med Radarr v5 er autentisering nå obligatorisk. [Se den obligatoriske autentiserings-FAQ-en for detaljer.](/radarr/faq#forced-authentication)
  - ~~Ingen - Du har ingen autentisering for å få tilgang til Radarr. Vanligvis hvis du er den eneste brukeren i nettverket ditt, ikke har noen i nettverket ditt som vil ha tilgang til Radarr eller at Radarr ikke er eksponert for nettet~~
  - Grunnleggende (nettleser pop-up) - Dette alternativet viser en liten pop-up når du får tilgang til Radarr, slik at du kan skrive inn brukernavn og passord
  - Skjema (påloggingsside) - Dette alternativet har en kjent påloggingsrute som ligner på andre nettsteder, slik at du kan logge på Radarr
- API-nøkkel - Dette er hvordan andre programmer kan kommunisere eller få Radarr til å kommunisere med andre programmer. Hvis denne nøkkelen gis til feil person med tilgang, kan det gjøres mange ting med biblioteket ditt. Derfor er API-nøkkelen sladdet i loggene
- Sertifikatvalidering - Endre hvor streng HTTPS-sertifikatvalidering er
  - Aktivert - Valider alle HTTPS-sertifikater (anbefalt)
  - Deaktivert for lokale adresser - Valider alle HTTPS-sertifikater unntatt de på localhost og LAN
  - Deaktivert - Ikke valider noen HTTPS-sertifikater
  
## Proxy

Proxy - Dette alternativet lar deg kjøre informasjonen Radarr henter og søker etter gjennom en proxy. Dette kan være nyttig hvis du er i et land som ikke tillater nedlasting av torrent-filer

- Bruk proxy - Aktiver for å bruke en proxy
- Proxytype - Velg proxytype (HTTPS, Socks4 eller Socks5)
- Vertsnavn - Skriv inn proxyvertsnavnet ditt (Ikke inkluder http/https eller noen annen protokoll)
- Port - Skriv inn proxyporten din
- Brukernavn - Skriv inn proxybrukernavnet ditt hvis aktuelt
- Passord - Skriv inn proxypassordet ditt hvis aktuelt
- Ignorerte adresser - Skriv inn en kommaseparert liste over adresser som skal omgå proxyen
- Omgå proxy for lokale adresser - Merk av i boksen for å omgå proxyen for lokale adresser. Lokale forespørsler identifiseres ved mangelen på en periode (.) i URI-en, som i <http://webserver/>, eller tilgang til den lokale serveren, inkludert <http://localhost>, <http://loopback> eller <http://127.0.0.1>. Når dette ikke er merket av, går alle internettforespørsler gjennom proxyserveren.

## Logging

- Loggnivå - Sannsynligvis et av de mest nyttige feilsøkingsverktøyene
  - Info - Dette er den mest grunnleggende måten Radarr samler informasjon på, og den inneholder bare en minimal mengde informasjon i loggene. Denne loggfilen inneholder oppføringer for fatal, feil, advarsel og info.
  - Debug - Debug vil inkludere all informasjonen som Info inkluderer, pluss mer informasjon som kan være nyttig. Denne loggfilen inneholder oppføringer for fatal, feil, advarsel, info og debug.
  - Trace - Den mest avanserte og detaljerte loggingen på Radarr, Trace vil inkludere all informasjonen som er samlet inn av Info og Debug, og mer. Dette er den vanligste typen logg som blir bedt om når man feilsøker på Discord eller Reddit. Hvis du trenger hjelp, velger du loggen din til Trace og gjentar oppgaven som ga deg problemer for å fange loggen. Denne loggfilen inneholder oppføringer for fatal, feil, advarsel, info, debug og trace.

## Analyse

- Analyse - Send anonym bruk og feilinformasjon til Radarrs servere (Servarr). Dette inkluderer informasjon om nettleseren din, hvilke Radarr WebUI-sider du bruker, feilrapportering samt OS- og runtime-versjon. Vi vil bruke denne informasjonen til å prioritere funksjoner og feilretting.

## Oppdateringer

- (Avansert alternativ) Gren - Dette er grenen av Radarr du kjører på.
  - [Se denne FAQ-en for mer informasjon](/radarr/faq#how-do-i-update-radarr)
- Automatisk - Last ned og installer oppdateringer automatisk. Du vil fortsatt kunne installere fra System: Oppdateringer. Merk: Windows-brukere blir alltid oppdatert automatisk.
- Mekanisme - Bruk Radarrs innebygde oppdaterer eller et skript
  - Innebygd - Bruk Radarrs egen oppdaterer
  - Skript - La Radarr kjøre oppdateringsskriptet
  - Docker - Ikke oppdater Radarr fra innsiden av Docker, i stedet hent et helt nytt bilde med den nye oppdateringen
- Skript - Synlig bare når mekanismen er satt til Skript - Sti til oppdateringsskriptet
- Oppdateringsprosess - Radarr vil laste ned oppdateringsfilen, verifisere integriteten og pakke den ut til en midlertidig plassering og kalle den valgte metoden. Oppdateringsprosessen vil kjøres under samme bruker som Radarr kjører under, den trenger tillatelser til å oppdatere Radarr-filene samt stoppe/starte Radarr.
- Innebygd - Den innebygde metoden vil sikkerhetskopiere Radarr-filer og -innstillinger, stoppe Radarr, oppdatere installasjonen og starte Radarr. Hvis systemet ditt ikke håndterer stopp av Radarr og prøver å starte det på nytt automatisk, kan det være best å bruke et skript i stedet. Hvis oppdateringen mislykkes, vil forrige versjon av Radarr startes på nytt.
- Skript - Skriptet skal håndtere det samme som den innebygde oppdatereren. Hvis du må håndtere stopp og start av tjenester (upstart/launchd/etc), må du gjøre det her.

## Sikkerhetskopier

- Sikkerhetskopiseksjonen lar deg fortelle Radarr hvordan du vil håndtere sikkerhetskopier

- (Avansert alternativ) Mappe - Dette lar deg velge plasseringen for sikkerhetskopien. I Docker vil du være begrenset til hva du tillater at kontaineren skal se. Stier er relative til appdata-mappen; om nødvendig kan du angi en absolutt sti for å sikkerhetskopiere utenfor appdata-mappen.
- (Avansert alternativ) Intervall - Hvor ofte vil du at Radarr skal lage en sikkerhetskopi
- (Avansert alternativ) Oppbevaring - Hvor lenge vil du at Radarr skal beholde hver sikkerhetskopi. Etter at en ny sikkerhetskopi er opprettet, vil den eldste sikkerhetskopien bli fjernet

> Manuelle sikkerhetskopier beholdes for alltid, lagres i samme mappe og har forskjellige navn.
{.is-info}

# Brukergrensesnitt

## Kalender

- Første ukedag - Her kan du velge hva du mener den første dagen i uken skal være.
- Ukekolonneoverskrift - Her kan du velge overskriften for kolonnene

## Filmer

- Kjøretidsformat - Velg hvordan kjøretider skal formateres, enten som timer og minutter eller minutter

## Datoer

- Kort datoformat - Hvordan vil du at Radarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du at Radarr skal vise datoer i langt format?
- Tidsformat - Vil du ha et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du at Radarr skal vise relative (I dag/I går/osv.) eller absolutte datoer?

## Stil

- Aktiver fargeblindmodus - Endret stil for å gjøre det lettere for fargeblinde brukere å skille fargekodet informasjon

## Språk

- Språk for filminformasjon - Velg språket for å vise filminformasjon i brukergrensesnittet til Radarr
- Brukergrensesnittspråk - Velg språket som Radarr skal bruke i applikasjonens brukergrensesnitt