---
title: Radarr Indstillinger
description: Beskrivelse af Radarr's indstillingsmenuer
published: true
date: 2023-08-27T22:02:11.780Z
tags: radarr, needs-love, indstillinger
editor: markdown
dateCreated: 2021-05-29T15:57:25.304Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Menuindstillinger](#menuindstillinger)
- [Mediehåndtering](#mediehåndtering)
  - [Fællesskabsforslag til navngivning](#fællesskabsforslag-til-navngivning)
  - [Filmnavngivning](#filmnavngivning)
    - [Standard filmformat](#standard-filmformat)
    - [Filmnavngivning](#filmnavngivning-1)
    - [Film-ID'er](#film-ider)
    - [Kvalitet](#kvalitet)
    - [Medieoplysninger](#medieoplysninger)
    - [Udgivelsesgruppe](#udgivelsesgruppe)
    - [Udgave](#udgave)
    - [Brugerdefinerede formater (navngivning)](#brugerdefinerede-formater-navngivning)
    - [Original](#original)
  - [Filmmappeformat](#filmmappeformat)
    - [Filmnavngivning](#filmnavngivning-2)
    - [Film-ID](#film-id)
  - [Mapper](#mapper)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
  - [Tilladelser](#tilladelser)
  - [Rodmapper](#rodmapper)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Forsinkelsesprofiler](#forsinkelsesprofiler)
    - [Anvendelse](#anvendelse)
    - [Sådan fungerer forsinkelsesprofiler](#sådan-fungerer-forsinkelsesprofiler)
      - [Eksempler](#eksempler)
        - [Eksempel 1](#eksempel-1)
        - [Eksempel 2](#eksempel-2)
        - [Eksempel 3](#eksempel-3)
- [Kvalitet](#kvalitet-1)
  - [Betydning af kvalitetstabellen](#betydning-af-kvalitetstabellen)
  - [Definerede kvaliteter](#definerede-kvaliteter)
- [Brugerdefinerede formater](#brugerdefinerede-formater)
  - [Betingelser for brugerdefinerede formater](#betingelser-for-brugerdefinerede-formater)
    - [Modifikatorer](#modifikatorer)
    - [Betingelser](#betingelser)
    - [Indstillinger og rangering af profilering](#indstillinger-og-rangering-af-profilering)
      - [Importering / Eksportering af brugerdefinerede formater](#importering-eksportering-af-brugerdefinerede-formater)
      - [Importering / Opdatering af eksisterende brugerdefinerede formater](#importering-opdatering-af-eksisterende-brugerdefinerede-formater)
    - [Samling af brugerdefinerede formater](#samling-af-brugerdefinerede-formater)
- [Indexere](#indexere)
  - [Understøttede indexere](#understøttede-indexere)
    - [Indstillinger for indexere](#indstillinger-for-indexere)
    - [Usenet-indexer-konfiguration](#usenet-indexer-konfiguration)
    - [Torrent-tracker-konfiguration](#torrent-tracker-konfiguration)
      - [Indexer-flag](#indexer-flag)
  - [Indstillinger](#indstillinger)
  - [Begrænsninger](#begrænsninger)
- [Downloadklienter](#downloadklienter)
  - [Overblik](#overblik)
  - [Processer for downloadklienter](#processer-for-downloadklienter)
    - [Usenet-proces](#usenet-proces)
    - [Torrent-proces](#torrent-proces)
  - [Downloadklienter](#downloadklienter-1)
    - [Understøttede downloadklienter](#understøttede-downloadklienter)
    - [Indstillinger for Usenet-klient](#indstillinger-for-usenet-klient)
    - [Indstillinger for torrentklient](#indstillinger-for-torrentklient)
    - [Kompatibilitet med fjernelse af download i torrentklient](#kompatibilitet-med-fjernelse-af-download-i-torrentklient)
  - [Håndtering af fuldførte downloads](#håndtering-af-fuldførte-downloads)
    - [Fjern fuldførte downloads](#fjern-fuldførte-downloads)
    - [Håndtering af mislykkede downloads](#håndtering-af-mislykkede-downloads)
  - [Fjernstyrede sti-mappinger](#fjernstyrede-sti-mappinger)
- [Importlister](#importlister)
  - [Lister](#lister)
  - [Listeindstillinger](#listeindstillinger)
  - [Listeundtagelser](#listeundtagelser)
- [Forbindelse](#forbindelse)
  - [Forbindelser](#forbindelser)
  - [Forbindelsestriggere](#forbindelsestriggere)
- [Metadata](#metadata)
  - [Indstillinger](#indstillinger-1)
  - [Metadataforbrugere](#metadataforbrugere)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Vært](#vært)
  - [Sikkerhed](#sikkerhed)
  - [Proxy](#proxy)
  - [Logning](#logning)
  - [Analyse](#analyse)
  - [Opdateringer](#opdateringer)
  - [Sikkerhedskopier](#sikkerhedskopier)
- [Brugergrænseflade](#brugergrænseflade)
  - [Kalender](#kalender)
  - [Film](#film)
  - [Datoer](#datoer)
  - [Stil](#stil)
  - [Sprog](#sprog)

Denne side vil gennemgå alle indstillingerne i Radarr og hvordan de fungerer. Dette er ikke ment som en omfattende "sådan indstiller du Radarr". Hvis du ønsker det, skal du bruge [Quick Start](/radarr/quick-start-guide) siden i stedet.

# Menuindstillinger

For at komme til indstillingssiden skal du vælge Indstillinger fra sidepanelet. Følgende undermenuindstillinger vil være tilgængelige:

![settings_1_menu.png](/assets/radarr/settings_1_menu.png)

Bemærk også, at der for hver individuel indstillingsside er nogle indstillinger øverst i menuen:

![settings_2_topmenu.png](/assets/radarr/settings_2_topmenu.png)

- Skjul/Vis avanceret er vigtigt for alle elementer, der er markeret som `(Avanceret indstilling)`, ellers vises de ikke. Disse menuelementer vises i orange på skærmbillederne.

- Du skal gemme dine ændringer, før du forlader skærmen. Dette gøres ved at klikke på diskikonet. Hvis du ikke har foretaget ændringer, vises "Ingen ændringer" og er gråtonet, som vist ovenfor.

# Mediehåndtering

> Nogle af disse indstillinger er kun synlige gennem `Vis avancerede indstillinger`, som er øverst i værktøjslinjen under søgefeltet{.is-info}

## Fællesskabsforslag til navngivning

> Her er nogle fællesskabsforslag til navngivning fra [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-recommended-naming-scheme/) {.is-info}

### Filmfiler

- Radarr v4.2.2.6489 eller nyere

`{Movie CleanTitle} {(Udgivelsesår)} {imdb-{ImdbId}} {edition-{Edition Tags}} {[Brugerdefinerede formater]}{[Kvalitet fuld]}{[Medieoplysninger 3D]}{[Medieoplysninger VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}]{MediaInfo AudioLanguages}[{Mediainfo VideoCodec}]{-Udgivelsesgruppe}`

- Ældre Radarr-versioner

`{Movie CleanTitle} {(Udgivelsesår)} {Edition Tags} [imdb-{ImdbId}]{[Brugerdefinerede formater]}{[Kvalitet fuld]}{[Medieoplysninger 3D]}{[Medieoplysninger VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels}][{Mediainfo VideoCodec}]{-Udgivelsesgruppe}`

### Filmmapper

`{Movie CleanTitle} ({Udgivelsesår})`

## Filmnavngivning

- Omdøb film - Hvis ikke markeret, vil Radarr bruge det eksisterende navn, hvis omdøbning er deaktiveret
  - Hvis ikke markeret:
    - Importering af downloadklient
      - Downloadklientens udgivelsestitel bruges
    - Manuel (Ad-Hoc) import: Oprindeligt filnavn
- Erstat ulovlige tegn - Hvis ikke markeret, vil Radarr i stedet fjerne dem.

  - Tegnene er: `:` `\` `/` `>` `<` `?` `*` `|` `"`
- Erstatning af kolon (`:`) - Denne indstilling bestemmer, hvordan Radarr håndterer kolonner i filnavnet. Denne er kun tilgængelig, når "Erstat ulovlige tegn" er aktiveret.
  - Slet - Selvforklarende
    - Eksempel: Film,The.mkv => FilmThe.mkv
  - Erstat med bindestreg - Fjerner kolonet og tilføjer en bindestreg i stedet
    - Eksempel: Film,The.mkv => Film-The.mkv
  - Erstat med mellemrum - Fjerner kolonet og tilføjer et mellemrum i stedet
    - Eksempel: Film,The.mkv => Film The.mkv
  - Erstat med mellemrum bindestreg mellemrum - selvforklarende
    - Eksempel: Film,The.mkv => Film - The.mkv

### Standard filmformat

- Her vælger du navngivelseskonventionen for dine film

- Rullemenu (øverst til højre)
  - Venstre boks - Håndtering af mellemrum
    Mellemrum ( ) - Brug mellemrum i navngivningen (Standard)
    Periode (.) - Brug punktummer i stedet for mellemrum i navngivningen
    Underscore (_) - Brug understregninger i stedet for mellemrum i navngivningen
    Bindestreg (-) - Brug bindestreger i stedet for mellemrum i navngivningen
  - Højre boks - Håndtering af store og små bogstaver
    Standard sag - Gør titlen til store og små bogstaver (~camel-case) (Standard)
    Store bogstaver - Gør titlen til store bogstaver
    Små bogstaver - Gør titlen til små bogstaver

### Filmnavngivning

- `{Movie Title}` = Filmtitel!
- `{Movie Title:DE}` = Filmtitel
- `{Movie CleanTitle}` = Filmtitel!
- `{Movie TitleThe}` = Filmtitel!, The
- `{Movie OriginalTitle}` = Originaltitel
- `{Movie CleanOriginalTitle}` = Originaltitel
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = Filmsamling
- `{Movie Certification}` = R
- `{Release Year}` = 2009

`CleanTitle` [gør følgende](https://github.com/Radarr/Radarr/blob/5948f564827eabb7afc1e89bf4a5987e3c71dc74/src/NzbDrone.Core/Organizer/FileNameBuilder.cs#L207):

- Erstat `&` med `and`
- Erstat `/` og `\` med ` `
- Fjern `,`,`<`,`>`,`/`,`\`,`;`,`:`,`'`,`|`, `~`,`!`,`?`,`@`,`$`,`%`,`^`,`*`,`-`,`_`,`=` i henhold til følgende regulære udtryk:

```regex
(?<=\s)(,|<|>|\/|\\|;|:|'|""|\||`|~|!|\?|@|$|%|^|\*|-|_|=){1}(?=\s)|('|:|\?|,)(?=(?:(?:s|m)\s)|\s|$)|(\(|\)|\[|\]|\{|\})
```

### Film-ID'er

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

> Imdb-tags, der bruges i Plex-navngivelsesformatet, skjules betinget, når værdien er tom `{imdb-{ImdbId}}` {.is-info}

### Kvalitet

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Medieoplysninger

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

> `MediaInfo Full`, `AudioLanguages` og `SubtitleLanguages` understøtter i øjeblikket ikke et `:EN+DE` suffiks, der tillades i Sonarr til at filtrere sprogene inkluderet i filnavnet. Der er en åben [issue](https://github.com/Radarr/Radarr/issues/4710) vedrørende dette.
~~`MediaInfo Full`, `AudioLanguages` og `SubtitleLanguages` understøtter et `:EN+DE` suffiks, der tillader dig at filtrere sprogene inkluderet i filnavnet. Brug `-DE` til at udelukke specifikke sprog. Ved at tilføje <kb>+</kb> (f.eks.: `:EN+`) vil det give `[EN]`,`[EN+--]` eller `[--]` afhængigt af de udelukkede sprog. For eksempel - `{MediaInfo Full:EN+DE}`.~~
{.is-info}

> `MediaInfo VideoDynamicRangeType` vil give mulige værdier som: DV, DV HDR10, DV HLG, DV SDR, HDR10, HDR10Plus, HLG og PQ.
{.is-info}

### Udgivelsesgruppe

- `{Release Group}` = Rls Grp

### Udgave

- `{Edition Tags}` = IMAX

> Fra v4.2.2.6489 vil udgavetags, der bruges i Radarr efter Plex's navngivelsesformat `{edition-{Edition Tags}}`, betinget skjules som `{-Group}` gør, når værdien for udgavetags er tom
{.is-info}

### Brugerdefinerede formater (navngivning)

- `{Custom Formats}` = Surround Sound x264

> Brugerdefinerede formater vil være det bogstavelige brugerdefinerede formaternavn og kræver, at brugerdefineret format er aktiveret for at blive inkluderet i omdøbning {.is-info}

### Original

- `{Original Title}` = Movie.Title.HDTV.x264-EVOLVE
- `{Original Filename}` = Movie.title.hdtv.x264-EVOLVE

> `Original Title` er udgivelsesnavnet, og det anbefales at bruge det.
{.is-info}

>`Original Filename` anbefales ikke. Det er det bogstavelige oprindelige filnavn og kan være forvirrende `t1i0p3s7i8yuti`.{.is-warning}

## Filmmappeformat

Her vælger du navngivelseskonventionen for mappen, der indeholder sæsonmapperne eller filmfilerne. Klik på `?` for at åbne dialogboksen `Folder Name Tokens` (Mappetokens).

### Filmnavngivning

- `{Movie Title}` = Filmnavn!
- `{Movie Title:DE}` = FilTitel
- `{Movie CleanTitle}` = Filmnavn
- `{Movie TitleThe}` = Filmnavn, The
- `{Movie OriginalTitle}` = Originaltitel
- `{Movie TitleFirstCharacter}` = S
- `{Movie Collection}` = Filmsamling
- `{Movie Certification}` = R
- `{Release Year}` = 2009

### Film-ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456

## Mapper

- Opret tomme mediemapper - Opret manglende filmmapper under diskscanning
- Slet tomme mapper - Slet tomme filmmapper under diskscanning og når filmfiler slettes

## Importering

- Spring kontrol af ledig plads over - Brug, når Radarr ikke kan registrere ledig plads fra din serierodmappe
- Minimum ledig plads - Aktivering af dette forhindrer import, hvis der efterlades mindre end denne mængde diskplads
- Brug hardlinks i stedet for kopi - Brug hardlinks, når du prøver at kopiere filer fra torrents, der stadig er i seed

  - For mere information om dette klik [her](https://trash-guides.info/hardlinks)

> Sjældent - men muligvis - kan filspærringer forhindre omdøbning af filer, der stadig er i seed. Du kan midlertidigt deaktivere seeding og bruge Radarr's omdøbningsfunktion som en midlertidig løsning.
{.is-warning}

- Importer ekstra filer - Importer matchende ekstra filer (undertekster, nfo osv.) efter import af en fil

## Filhåndtering

- Fjern overvågning af slettede film - Film, der er slettet fra disken, bliver automatisk fjernet fra overvågning i Radarr.
- Download korrekte og repacks - Om der automatisk skal opgraderes til korrekte og repacks. Brug `Foretræk ikke` til at sortere efter foretrukken ord-score over korrekte og repacks.

  - Foretræk og opgrader - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl nye repacks og korrekte som opgradering af nuværende udgivelser.
  - Opgrader ikke automatisk - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl ikke nye repacks og korrekte som opgradering af nuværende udgivelser.
  - Foretræk ikke - Ignorer effektivt repacks og korrekte. Du skal administrere eventuelle præferencer for disse med [Brugerdefinerede formater](#brugerdefinerede-formater).

> \* `KORREKT` - betyder, at der var et problem med den tidligere udgivelse. Downloads mærket som KORREKT viser, at problemerne er blevet løst i denne udgivelse. Dette er gjort af en gruppe, der ikke udgav originalen.
> \* `REPACK` - betyder, at der var et problem med den tidligere udgivelse, og det er rettet af den oprindelige gruppe. Downloads mærket som REPACK viser, at problemerne er blevet løst i denne udgivelse. Dette er gjort af en gruppe, der udgav originalen.
{.is-info}

> [Brug brugerdefinerede formater til automatisk opgradering til korrekte og repacks](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)
{.is-info}

- Analyser videofiler - Udtræk filoplysninger som opløsning, køretid og codec-oplysninger fra filer. Dette kræver, at Radarr læser dele af filen, hvilket kan medføre høj disk- eller netværksaktivitet under scanning.
- Genindlæs filmmappe efter opdatering
  - Altid - Dette vil genindlæse filmmapper baseret på opgaveplanen. Dette anbefales i de fleste tilfælde, herunder hvis du bruger Bazarr.
  - Efter manuel opdatering - Du skal manuelt genindlæse disken. Dette anbefales til brugere af cloud-lagring.
  - Aldrig - Som det siger, genindlæs aldrig filmmapperne. Dette anbefales ikke.
- Ændre fil-dato - Ændre fil-dato ved import/genindlæsning
  - Ingen - Radarr ændrer ikke datoen, der vises i din filbrowser.
  - I biografernes dato - Datoen, hvor filmen blev udgivet i biograferne.
  - Fysisk udgivelsesdato - Datoen, hvor filmen blev udgivet enten på disk (fysisk) eller på nettet.
- Genbrugsbin - Filmfiler vil blive placeret her, når de slettes i stedet for at blive permanent slettet.
- Rensning af genbrugsbin - Dette er, hvor gammel en given fil kan være, før den bliver permanent slettet.

> Filer i genbrugsbinen, der er ældre end det valgte antal dage, vil blive ryddet automatisk {.is-warning}

## Tilladelser

- Indstil tilladelser - Skal `chmod` køres, når filer importeres/omdøbes?
  - chmod-mappe - Oktal, der anvendes under import/omdøbning til mediemapper og filer (uden udførelsesbit)

> Dropdown-boksen har en forudindstillet liste over meget almindeligt anvendte tilladelser, der kan bruges. Du kan dog manuelt indtaste en mappe-oktal, hvis du ønsker det.{.is-info}

> Dette virker kun, hvis brugeren, der kører `Radarr`, er ejeren af filen. Det er bedre at sikre, at downloadklienten indstiller tilladelserne korrekt.{.is-warning}

- chown-gruppe - Gruppenavn eller GID. Brug GID til fjernfiler-systemer

> Dette virker kun, hvis brugeren, der kører `Radarr`, er ejeren af filen. Det er bedre at sikre, at downloadklienten indstiller tilladelserne korrekt.{.is-warning}

## Rodmapper

- Sti - Dette viser stien til dit mediebibliotek.
- Ledig plads - Dette er den ledige plads, der rapporteres til Radarr fra systemet.
- Umapperede mapper - Dette er mapper, der ikke har en film tilknyttet.

> `X` i slutningen vil fjerne denne rodsti{.is-info}

- Tilføj rodmappe - Dette giver dig mulighed for at vælge en rodsti til enten at placere nye importerede downloads i denne mappe eller lade Radarr scanne eksisterende medier.

> Brugere af ikke-Windows:
> \* Hvis du bruger et NFS-mount, skal du sørge for, at `nolock` er aktiveret.
> \* Hvis du bruger et SMB-mount, skal du sørge for, at `nobrl` er aktiveret.
{.is-warning}

# Profiler

## Kvalitetsprofiler

- Indstil profiler for kvaliteten af film, du ønsker at downloade.

> Når du vælger en eksisterende profil eller tilføjer en ekstra profil, vises et nyt vindue{.is-info}

> Bemærk: Kvaliteten, der har en blå boks, er kvaliteten, som alt med denne profil fortsat vil blive opgraderet til.
{.is-info}

- Plus-ikon (<kb>+</kb>) - Opret en ny kvalitetsprofil

- Navn - Vælg et **UNIKT** navn til den kvalitetsprofil, du opretter.
- Opgraderinger tilladt - Når denne indstilling er markeret, og du beder Radarr om at downloade en `WEB 1080p`, da det er den første udgivelse af en bestemt film, og senere kan nogen uploade en `Bluray-1080p`, vil Radarr automatisk opgradere til den bedre kvalitet ***hvis*** `Opgrader indtil` har den kvalitet valgt.
- Opgrader indtil - Når denne kvalitet er nået, vil Radarr ikke længere downloade film.

> Bemærk: Dette gælder kun, hvis du har `Bluray-1080p` højere end `WEB 1080p` inden for afsnittet `Kvaliteter`
{.is-warning}

- Kvaliteter - Kvaliteter højere på listen foretrækkes mere, selvom de ikke er markeret. Kvaliteter inden for samme gruppe er lige. Kun markerede kvaliteter ønskes.
  - Rediger grupper - Nogle kvaliteter er grupperet sammen for at reducere størrelsen på listen samt gruppere lignende udgivelser. Et godt eksempel på dette er `WebDL` og `WebRip`, da disse er meget ens og typisk har lignende bitrater. Når du redigerer grupperne, kan du ændre præference inden for hver af grupperne. [Se TRaSH's guide til, hvordan man fusionerer kvaliteter](https://trash-guides.info/merge-quality)

  - [Se kvaliteter](#kvaliteter-defineret)

> Som standard er kvaliteterne indstillet fra laveste (nederst) til højeste (øverst)
{.is-info}

- Sprog - Vælg dit foretrukne sprog.

- Brugerdefineret format - Radarr scorer hver udgivelse ved hjælp af summen af score for matchende brugerdefinerede formater. Hvis en ny udgivelse ville forbedre scoren, ved samme eller bedre kvalitet, vil Radarr hente den.
Se [Brugerdefinerede formater](#brugerdefinerede-formater) for flere detaljer.

## Forsinkelsesprofiler

- Forsinkelsesprofiler giver dig mulighed for at reducere antallet af udgivelser, der downloades til en film ved at tilføje en forsinkelse, mens Radarr fortsætter med at søge efter udgivelser, der bedre matcher dine præferencer.
- Foretrukken protokol - Dette vil enten være `Usenet` eller `Torrent`, afhængigt af hvilken downloadprotokol du foretrækker.
- Usenet-forsinkelse - Indstil antallet af minutter, du vil vente, før downloaden starter.
- Torrent-forsinkelse - Indstil antallet af minutter, du vil vente, før downloaden starter.
- Bypass, hvis højeste kvalitet - Bypass forsinkelsen, når udgivelsen har den højeste aktiverede kvalitetsprofil med den foretrukne protokol.
- Tags - Ved at give denne forsinkelsesprofil en tag kan du tagge en given film for at få den til at følge reglerne her.
- Skruenøgleikon - Dette giver dig mulighed for at redigere forsinkelsesprofilen.
- Plus-ikon (<kb>+</kb>) - Opret en ny forsinkelsesprofil

### Anvendelser

Nogle medier vil modtage et halvt dusin forskellige udgivelser af varierende kvalitet i timerne efter en udgivelse, og uden forsinkelsesprofiler kan Radarr forsøge at downloade dem alle. Med forsinkelsesprofiler kan Radarr konfigureres til at ignorere de første par timer med udgivelser.

Forsinkelsesprofiler er også nyttige, hvis du vil lægge vægt på en protokol (Usenet eller BitTorrent) over den anden. (Se eksempel 3)

### Sådan virker forsinkelsesprofiler

Timeren starter, så snart Radarr registrerer, at en film har en tilgængelig udgivelse. Denne udgivelse vises i din kø med et urikon for at angive, at den er under forsinkelse.

> Uret starter fra udgivelsestidspunktet for de uploadede udgivelser og ikke fra det tidspunkt, Radarr ser dem.
{.is-info}

I løbet af forsinkelsesperioden vil Radarr bemærke eventuelle nye udgivelser, der bliver tilgængelige. Når forsinkelsestimeren udløber, vil Radarr downloade den ene udgivelse, der bedst matcher dine kvalitetspræferencer.

Forsinkelsestiden kan være forskellig for Usenet og Torrents. Hver profil kan være forbundet med en eller flere tags, så du kan tilpasse, hvilke shows der har hvilke profiler. En forsinkelsesprofil uden tag betragtes som standard og gælder for alle shows, der ikke har et specifikt tag.

> Forsinkelsesprofiler starter fra tidspunktet, hvor indekseren rapporterer, at udgivelsen blev uploadet. Dette betyder, at indhold, der er ældre end det antal minutter, du har indstillet, ikke påvirkes på nogen måde af din forsinkelsesprofil og vil blive downloadet øjeblikkeligt. Derudover vil **enhver manuel søgning** efter indhold (søgninger uden RSS-feed) ignorere indstillingerne for forsinkelsesprofilen.
{.is-warning}

#### Eksempler

- For hvert eksempel skal du antage, at brugeren har følgende kvalitetsprofil aktiveret: WebDL-720p og derover er tilladt, WebDL-1080p er kvalitetsgrænsen, og BluRay1080p er den højest rangerede kvalitet.

##### Eksempel 1

- I dette simple eksempel er profilen indstillet med en 120 minutters (to timers) forsinkelse for både Usenet og Torrent.

- Kl. 23:00 opdager Radarr den første udgivelse af en film, der blev uploadet kl. 22:50, og den 120 minutters ur begynder at tælle. Kl. 00:50 vil Radarr evaluere eventuelle udgivelser, den har fundet i de sidste to timer, og downloade den bedste, som er WebDL 720p.

- Kl. 03:00 findes en anden udgivelse, som er WebDL 720p, der blev tilføjet til din indekser kl. 02:46. En anden 120 minutters ur begynder at tælle. Kl. 04:46 downloades den bedst tilgængelige udgivelse. Da kvalitetsgrænsen nu er nået, kan filmen ikke længere opgraderes, og Radarr vil stoppe med at lede efter nye udgivelser.

- På et hvilket som helst tidspunkt, hvis der findes en WebDL 1080p-udgivelse, downloades den øjeblikkeligt, fordi det er den højest rangerede kvalitet. Hvis der er en aktiv forsinkelsestimer, annulleres den.

##### Eksempel 2

- Dette eksempel har forskellige timere for Usenet og Torrents. Antag en 120 minutters timer for Usenet og en 180 minutters timer for BitTorrent.

- Kl. 23:00 opdages den første udgivelse af en film af Radarr, og begge timere starter. Udleveringen blev tilføjet til indekseren kl. 22:15. Kl. 00:15 vil Radarr evaluere eventuelle udgivelser, og hvis der er nogen acceptable Usenet-udgivelser, vil den bedste blive downloadet, og begge timere vil slutte. Hvis ikke vil Radarr vente indtil kl. 00:15 og downloade den bedste udgivelse, uanset hvilken kilde den kommer fra.

##### Eksempel 3

- En almindelig brug af forsinkelsesprofiler er at lægge vægt på en protokol over den anden. For eksempel vil du kun downloade en BitTorrent-udgivelse, hvis der ikke er blevet uploadet noget til Usenet efter et bestemt tidsrum.

- Du kan indstille en 60 minutters timer for BitTorrent og en 0 minutters timer for Usenet.

- Hvis den første udgivelse, der registreres, er fra Usenet, vil Radarr downloade den øjeblikkeligt.

- Hvis den første udgivelse er fra BitTorrent, vil Radarr indstille en 60 minutters timer. Hvis der i løbet af den tid findes en kvalificerende Usenet-udgivelse, ignoreres BitTorrent-udgivelsen, og Usenet-udgivelsen hentes.

- Ukendt - Selvforklarende
- SDTV - Efter luftoptagelser fra en analog kilde (normalt kabel-tv eller OTA-standarddefinition). Billedkvaliteten er generelt god (til opløsningen), og de er normalt kodet i DivX/XviD eller MP4.
- WEBDL-480p - WEB-DL (P2P) henviser til en fil, der er ripset tabløst fra en streamingtjeneste som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer osv. eller downloadet via en online distributionshjemmeside som iTunes. Kvaliteten er ret god, da de ikke er genkodet. Video (H.264 eller H.265) og lyd (AC3/AAC) streams er normalt udtrukket fra iTunes eller Amazon Video og remuxed til en MKV-container uden at gå på kompromis med kvaliteten. En fordel ved disse udgivelser er, at de normalt ikke har netværkslogoer på skærmen. Disse er næsten lige så gode som en Blu-ray kilde, men kan lide af lydforsinkelse eller visuelle artefakter fra streamingtjenesternes adaptive bitrate. Hvis en ripper mister forbindelsen til internettet, så bitrate falder, kan den oprindelige bitrate ændre sig dynamisk, hvilket kan medføre variationer i billedkvaliteten. De fleste udgivelser, der lider af en ekstrem mængde visuelle artefakter, er NUKED, og der udgives normalt en PROPER for at rette eventuelle vilde variationer i den adaptive bitrate. Dette vil være i 480p (SD) kvalitet.
- WEBRip-480p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 480p (SD) kvalitet.
- DVD - En genkodning af den endelige udgivne DVD9. Hvis det er muligt, udgives det før detailhandlen. Det bør være fremragende kvalitet (til opløsningen). DVDrips udgives normalt i DivX/XviD eller MP4.
- Bluray-480p - En genkodning af den endelige udgivne Blu-ray, nedskaleret til 480p opløsning (720x480 @ 16:9, en anden billedformat kan have en anden opløsning). Hvis det er muligt, udgives det før detailhandlen. Det bør være fremragende kvalitet for opløsningen. Bitrater kan variere, men de er generelt kodet til DivX, XviD eller AVC og tilbyder en lille opfattet kvalitetsreduktion i forhold til den originale kilde, samtidig med at filstørrelsen reduceres drastisk. Disse er normalt MKV eller MP4, men der findes også nogle DivX/XviD i AVI-format.
- HDTV-720p - En genkodning af den endelige udgivne Blu-ray, men sendt over HD-kabel eller satellit (1280x720 @ 16:9, en anden billedformat kan have en anden opløsning). Det kan være ændret i længde eller indhold afhængigt af netværket, det kommer fra. Det udgives normalt flere måneder efter en detailudgivelse, men nogle gange udgives opskalerede versioner af en standard definition film på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopier af den specifikke film, der er tilgængelige. Disse er normalt MKV eller MP4.
- HDTV-1080p - En genkodning af den endelige udgivne Blu-ray, men sendt over HD-kabel eller satellit (1920x1080 @ 16:9, en anden billedformat kan have en anden opløsning). Det kan være ændret i længde eller indhold afhængigt af netværket, det kommer fra. Det udgives normalt flere måneder efter en detailudgivelse, men nogle gange udgives opskalerede versioner af en standard definition film på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopier af den specifikke film, der er tilgængelige. Disse er normalt MKV eller MP4-container.
- WEBRip-720p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 720p kvalitet.
- Bluray-720p - En genkodning af den endelige udgivne Blu-ray, nedskaleret til 720p opløsning (1280x720 @ 16:9, en anden billedformat kan have en anden opløsning). Hvis det er muligt, udgives det før detailhandlen. Det bør være fremragende kvalitet for opløsningen. Bitrater kan variere, men de er generelt kodet til AVC eller HEVC og tilbyder en lille opfattet kvalitetsreduktion i forhold til den originale kilde, samtidig med at filstørrelsen reduceres drastisk. Disse er normalt MKV eller MP4-container.
- WEBDL-1080p - WEB-DL (P2P) henviser til en fil, der er ripset tabløst fra en streamingtjeneste som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer osv. eller downloadet via en online distributionshjemmeside som iTunes. Kvaliteten er ret god, da de ikke er genkodet. Video (H.264 eller H.265) og lyd (AC3/AAC) streams er normalt udtrukket fra iTunes eller Amazon Video og remuxed til en MKV-container uden at gå på kompromis med kvaliteten. En fordel ved disse udgivelser er, at de normalt ikke har netværkslogoer på skærmen. Disse er næsten lige så gode som en Blu-ray kilde, men kan lide af lydforsinkelse eller visuelle artefakter fra streamingtjenesternes adaptive bitrate. Hvis en ripper mister forbindelsen til internettet, så bitrate falder, kan den oprindelige bitrate ændre sig dynamisk, hvilket kan medføre variationer i billedkvaliteten. De fleste udgivelser, der lider af en ekstrem mængde visuelle artefakter, er NUKED, og der udgives normalt en PROPER for at rette eventuelle vilde variationer i den adaptive bitrate. Dette vil være i 1080p kvalitet.
- WEBRip-1080p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 1080p kvalitet.
- Bluray-1080p - En genkodning af den endelige udgivne Blu-ray, i sin oprindelige 1080p opløsning (1920x1080 @ 16:9, en anden billedformat kan have en anden opløsning). Hvis det er muligt, udgives det før detailhandlen. Det bør være fremragende kvalitet og samme opløsning som kilden. Bitrater kan variere, men de er generelt kodet til AVC eller HEVC og tilbyder en lille opfattet kvalitetsreduktion i forhold til den originale kilde, samtidig med at filstørrelsen reduceres lidt. Disse er normalt MKV eller MP4-container.
- Remux-1080p - En remux er en rip af en Blu-ray eller HD DVD-skive til en anden containerformat eller blot fjernelse af menuer og bonusmateriale, samtidig med at indholdet af dens lyd- og videostreams bevares (også bevare de nuværende codecs), hvilket garanterer den nøjagtige 1:1 filmkvalitet som på den originale skive. Dette er i 1080p kvalitet.
- HDTV-2160p - TVRip er en optagelseskilde fra et optagekort. HDTV står for optaget kilde fra HD-tv. Med en HDTV-kilde kan kvaliteten nogle gange endda overgå DVD. Film i dette format begynder at blive populære. Nogle reklamer og kommercielle bannere kan ses på nogle udgivelser under afspilning. Dette er i 2160p (4K) kvalitet.
- WEBDL-2160p - WEB-DL (P2P) henviser til en fil, der er ripset tabløst fra en streamingtjeneste som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer osv. eller downloadet via en online distributionshjemmeside som iTunes. Kvaliteten er ret god, da de ikke er genkodet. Video (H.264 eller H.265) og lyd (AC3/AAC) streams er normalt udtrukket fra iTunes eller Amazon Video og remuxed til en MKV-container uden at gå på kompromis med kvaliteten. En fordel ved disse udgivelser er, at de normalt ikke har netværkslogoer på skærmen. Disse er næsten lige så gode som en Blu-ray kilde, men kan lide af lydforsinkelse eller visuelle artefakter fra streamingtjenesternes adaptive bitrate. Hvis en ripper mister forbindelsen til internettet, så bitrate falder, kan den oprindelige bitrate ændre sig dynamisk, hvilket kan medføre variationer i billedkvaliteten. De fleste udgivelser, der lider af en ekstrem mængde visuelle artefakter, er NUKED, og der udgives normalt en PROPER for at rette eventuelle vilde variationer i den adaptive bitrate. Dette vil være i 2160p (4K) kvalitet.
- WEBRip-2160p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 2160p (4K) kvalitet.
- Bluray-2160p - En genkodning af den endelige udgivne Blu-ray, i sin oprindelige 2160p opløsning (3840x2160 @ 16:9, en anden billedformat kan have en anden opløsning). 4K-versioner af film, der udgives, er normalt i HEVC codec og kan være enten 8-bit eller 10-bit farvegengivelse eller fra en HDR-kilde. Disse er normalt MKV eller MP4-container.
- Remux-2160p - En remux er en rip af en Blu-ray eller HD DVD-skive til en anden containerformat eller blot fjernelse af menuer og bonusmateriale, samtidig med at indholdet af dens lyd- og videostreams bevares (også bevare de nuværende codecs), hvilket garanterer den nøjagtige 1:1 filmkvalitet som på den originale skive. Dette er i 2160p (4K) kvalitet.

# Brugerdefinerede formater

{#custom-formats-2}

- Sørg for at få den rigtige udgivelse hver gang! Brugerdefinerede formater giver fin kontrol over prioritering og valg af udgivelser. Lige så simpelt som et enkelt foretrukket ord eller så komplekst som du ønsker med flere kriterier og regulære udtryk.
- Brugerdefinerede formater beregnes dynamisk i stedet for at blive gemt i databasen, så de opdateres, så snart du ændrer definitionerne.
- Brugerdefinerede formater bruges inden for dine kvalitetsprofiler til at bestemme scoringen af hvert brugerdefineret format. Inden for hver kvalitetsprofil kan du indstille en minimumscore for brugerdefineret format for at hente en udgivelse og også en opgraderingsscore.
- Det anbefales stærkt at tilføje følgende brugerdefinerede formater fra [TRaSH's Guides](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/) for at undgå uønskede downloads. Se TRaSH Guide Custom Format-artiklen og yderligere 3 TRaSH Custom Format Guides, der henvises til øverst på siden Collection of Custom Formats for mere information.
  - [DV (WEB-DL)](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#dv-webdl) vil undgå at hente udgivelser med Dolby Vision (DV), der har en grøn farvetone, hvis DV ikke understøttes.
  - [BR-DISK](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/#br-disk) for at undgå at hente dårligt navngivne BR-DISKs, der ikke matcher BR-DISK-kvalitetsanalyse.

---

- Navn - Navnet på det brugerdefinerede format
- Inkluder brugerdefineret format ved omdøbning - Inkluder navnet på det brugerdefinerede format ved omdøbning?

> Brugerdefinerede formater har ingen indflydelse på, hvad der søges efter - kun hvordan resultaterne evalueres. Det er heller ikke muligt at ændre på nogen måde, hvordan Radarr søger.
{.is-info}

Profiler er, hvor brugerdefinerede formatpoint beregnes.  

## Betingelser for brugerdefinerede formater

### Modifikatorer

- Negér - kampen vendes, så betingelsen er opfyldt, hvis og kun hvis den ikke-negérede betingelse ikke er opfyldt
- Påkrævet - gælder kun for formater med mere end én betingelse af samme type og ændrer matchereglerne for typegrupper. Hvis denne indstilling er aktiveret, betyder det, at denne specifikke betingelse skal opfyldes for, at det brugerdefinerede format skal gælde, uanset om en anden betingelse af samme type ellers ville opfylde typegruppen. **Bemærk: Du skal kun bruge dette, hvis du bruger en betingelse mere end én gang. Med andre ord, hvis du har et brugerdefineret format med 2 påkrævede betingelser for udgivelsestitel og 3 ikke-påkrævede sprog betingelser, skal det opfylde BEGGE de påkrævede betingelser for udgivelsestitel og det skal opfylde EN AF de 3 sprog betingelser.** På samme måde, hvis du har et brugerdefineret format med 4 udgivelsestitel betingelser, og ingen er påkrævet, vil det brugerdefinerede format gælde, hvis NOGEN af betingelserne er opfyldt.

### Betingelser

> **Forskellige betingelsestyper** fungerer som `og` inden for det samme brugerdefinerede format. **Flere betingelser af samme type** fungerer som `eller`, medmindre Påkrævet bruges
{.is-info}

- **Alle betingelser, der bruger regulære udtryk, er ikke-forskelssensitive**
- Bemærk følgende GitHub-problemer
  - [Brugerdefinerede formater gælder ikke før filmåret i udgivelsestitler #4859](https://github.com/Radarr/Radarr/issues/4859)
  - [Brugerdefineret format matcher ikke for termen "xvid" i slutningen af udgivelsesnavnet #6824](https://github.com/Radarr/Radarr/issues/6824)
- Udgivelsestitel - Dette er et regulært udtryk, der matcher udgivelsestitlen og efter download filnavnet på disken.
  - Bemærk: Radarr betragter kun tekst efter filmens titel og år, hvilket betyder, at alt, der går forud for titlen, ignoreres.
- Udgave - Dette tag matcher eventuelle udgaver, som Radarr kan analysere. Du kan indsætte en værdi, som Radarr vil forsøge at matche mod det, der blev analyseret (ikke forskelssensitivt).
- Sprog - Dette sprog matcher eventuelle sprog, som Radarr analyserer. Alle tidligere valgbare sprog i profiler fungerer her.
- [Indexer Flag](/radarr/settings#indexer-flags) - Dette tag matcher eventuelle Indexer Flags, som Radarr kan analysere.
- Kilde - Kilden, hvor en udgivelse blev ripset fra (f.eks. BLURAY).
- Opløsning - Opløsningen analyseret fra enten udgivelsesnavnet eller mediainfo (hvis tilgængelig).
- Kvalitetsmodifikator - Kvalitetsmodifikator indstiller ting som Telescene, Telesync, Remux, Regional. Det adskiller en given kilde og opløsningspar, når der er flere kvalitets (kilde)typer, der kan anvendes.
- Størrelse - Dette matcher udgivelsesstørrelsen. Udgivelsesstørrelsen konverteres til gigabyte og sammenlignes med minimums- og maksimumsværdierne.
- Gruppe - Dette matcher gruppen, som Radarr analyserer baseret på Radarr's gruppedetektionslogik.

### Indstillinger for profilering og rangering

- Brugerdefinerede formater implementeres inden for og har deres indflydelse styret af kvalitetsprofiler. Opgraderingsindtil-scoren forhindrer opgradering, når en udgivelse med denne ønskede score er blevet downloadet.
- En score på 0 resulterer i, at det brugerdefinerede format kun er informativt og ikke har nogen indflydelse på udgivelsesrangering eller søgte sprog.
- Minimumscoren kræver, at udgivelsernes samlede brugerdefinerede formatscore når denne tærskel, ellers vil de blive afvist.
  - Brugerdefinerede formater, der matcher med uønskede attributter, bør gives en negativ score for at mindske deres appel.
  - Direkte afvisninger bør gives en negativ score, der er lav nok til, at selv hvis alle de andre formater med positive scores blev tilføjet, ville scoren stadig falde under minimumet.
- [Se TRaSH's Guides for, hvordan man opsætter og bruger brugerdefinerede formater](https://trash-guides.info/Radarr/Radarr-setup-custom-formats/)

#### Import af / eksport af brugerdefinerede formater

- [Se TRaSH's Guides for, hvordan man importerer/eksporterer brugerdefinerede formater.](https://trash-guides.info/Radarr/Radarr-import-custom-formats/) Det er dog muligt at importere og eksportere brugerdefinerede formater.

#### Import af / opdatering af eksisterende brugerdefinerede formater

- [Se TRaSH's Guides for, hvordan man importerer eller opdaterer eksisterende brugerdefinerede formater.](https://trash-guides.info/Radarr/Radarr-how-to-update-custom-formats/)

### Samling af brugerdefinerede formater

- [TRaSH vedligeholder en samling af brugerdefinerede formater](https://trash-guides.info/Radarr/Radarr-collection-of-custom-formats/)

# Indexere

> Oplysninger om understøttede indexere kan findes på siden [Flere oplysninger (Understøttet)](/radarr/supported#indexers) for dette afsnit
{.is-info}

## Understøttede indexere

- En liste over understøttede indexere findes på siden [Flere oplysninger (Understøttet)](/radarr/supported#indexers)

### Indstillinger for indexere

- Når du har klikket på <kb>+</kb>-knappen for at tilføje en ny indexer, vil du blive præsenteret for et nyt vindue med mange forskellige indstillinger. I Radarr betragtes både Usenet Indexers og Torrent Trackers som "Indexers".

- Der er to sektioner her: Usenet og Torrents. Afhængigt af hvilken downloadklient du vil bruge, skal du vælge den type indexer, du vil bruge.

### Konfiguration af Usenet Indexer

- Newznab - Her finder du forudindstillinger for populære Usenet-indekser (som er udfyldt, alt hvad du behøver er din API-nøgle, som leveres af Usenet-indekseren efter eget valg), sammen med muligheden for at oprette en brugerdefineret indekser
- Software, der fungerer med Usenet og integrerer godt med Radarr, er [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr), som integrerer med både Usenet og Torrents
- Uanset om du vælger en forudfyldt indekser eller en brugerdefineret indekseropsætning, vil du blive præsenteret for et nyt vindue til at indtaste alle dine indstillinger
- Vælg mellem forudindstillingerne eller tilføj en brugerdefineret indekser (som f.eks. NZBHydra2 eller Prowlarr)
- Navn - Navnet på indekseren i Radarr
- Aktivér RSS - Hvis aktiveret, brug denne indekser til at overvåge filer, der ønskes og mangler, eller som endnu ikke har nået deres cutoff.
- Aktivér automatisk søgning - Hvis aktiveret, brug denne indekser til automatisk søgning, herunder søgning ved tilføjelse
- Aktivér interaktiv søgning - Hvis aktiveret, brug denne indekser til manuel interaktiv søgning.
- URL - Indekserens URL, som f.eks. `https://api.nzbgeek.info`.
- API-sti - Indekserens API-sti. Dette er normalt `/api`
- Flersproget - Indstil hvilke sprog `MULTI` der er for denne indekser.
- API-nøgle - Indekserens API-nøgle til at få adgang til API'en.
- Kategorier - Standardkategorier vil blive brugt, medmindre de redigeres. Det er sandsynligt, at disse standardkategorier ikke er optimale. Når denne indstilling redigeres, forespørger Radarr indekseren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standarder ryddes, så snart en kategori skiftes.
- (Avanceret indstilling) Yderligere parametre - Yderligere Newznab-parametre, der skal tilføjes til forespørgselslinket
- Fjern år fra søgestrengen - Skal Radarr fjerne året efter filmens titel, når der søges på denne indekser?
- (Avanceret indstilling) Indekserprioritet - Prioritet for denne indekser for at foretrække en indekser frem for en anden i scenarier med udgivelsesafgørelse. 1 er højeste prioritet, og 50 er laveste prioritet.
- (Avanceret indstilling) Downloadklient - Vælg og specificer hvilken downloadklient der bruges til at hente fra denne indekser
- Tags - Brug kun denne indekser til film med mindst én matchende tag. Lad være blank for at bruge med alle film.

### Konfiguration af torrent-tracker

- Ligegyldigt om du vælger en forudfyldt torrent-tracker eller en brugerdefineret torrent-trackeropsætning, vil du blive præsenteret for et nyt vindue til at indtaste alle dine indstillinger
- En af de bedste og enkleste måder at bruge torrent-trackere, der ikke er naturligt understøttet af Radarr, er at bruge et andet program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Disse programmer fungerer godt sammen med Radarr som en søgeindekser, der indeholder al din information og sender den til Radarr.
- Torznab - Denne mulighed vil indstille dig med en Jackett-forudindstilling, hvis du bruger flere trackere, skal du have hver post have et unikt navn
- Torznab-indekser
- Vælg mellem forudindstillingerne eller tilføj en brugerdefineret indekser (som f.eks. Jackett)
- Navn - Navnet på indekseren i Radarr
- Aktivér RSS - Hvis aktiveret, brug denne indekser til at overvåge filer, der ønskes og mangler, eller som endnu ikke har nået deres cutoff.
- Aktivér automatisk søgning - Hvis aktiveret, brug denne indekser til automatisk søgning, herunder søgning ved tilføjelse
- Aktivér interaktiv søgning - Hvis aktiveret, brug denne indekser til manuel interaktiv søgning.
- URL - Indekserens URL, som f.eks. `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sti - Indekserens API-sti. Dette er normalt `/api`
- API-nøgle - Indekserens API-nøgle til at få adgang til API'en.
- Flersproget - Indstil hvilke sprog `MULTI` der er for denne indekser.
- Kategorier - Standardkategorier vil blive brugt, medmindre de redigeres. Det er sandsynligt, at disse standardkategorier ikke er optimale. Når denne indstilling redigeres, forespørger Radarr indekseren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standarder ryddes, så snart en kategori skiftes.
- (Avanceret indstilling) Yderligere parametre - Yderligere Torznab-parametre, der skal tilføjes til forespørgselslinket
- Fjern år fra søgestrengen - Skal Radarr fjerne året efter filmens titel, når der søges på denne indekser?
- Minimum seedere - Det mindste antal seedere, der kræves for, at en udgivelse fra denne tracker skal hentes.
- Seed Ratio - Hvis tomt, brug standardværdien for downloadklienten. Ellers er det mindste seed ratio, der kræves for, at din downloadklient skal opfylde for udgivelser fra denne indekser, inden den sættes på pause af din klient og fjernes af Radarr (Kræver fuldført downloadhåndtering - Fjern aktiveret)
- Seed Time - Hvis tomt, brug standardværdien for downloadklienten. Ellers er det mindste seed-tid i minutter, som din downloadklient skal opfylde for udgivelser fra denne indekser, inden den sættes på pause af din klient og fjernes af Radarr (Kræver fuldført downloadhåndtering - Fjern aktiveret)
- Påkrævede flag - Hvilke indekserflag er påkrævet?

#### Indekserflag

| Flag             | Symbol | Beskrivelse                                                                                                                                                                                                                 |
| ---------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `G_Freeleech`    | ⬇⬇     | Nogle gange indstiller torrent-websteder en torrent til at være freeleech. Dette betyder, at download af denne torrent ikke tæller med i din downloadkvota eller -ratio. Dette er virkelig nyttigt, hvis du endnu ikke har opbygget en god ratio. |
| `G_Halfleech`    | ⇩⇩     | Lignende `G_Freeleech`, angiver `G_Halfleech`, at kun halvdelen af størrelsen på denne torrent tæller med i din downloadkvota eller -ratio.                                                                               |
| `G_DoubleUpload` | ⬆      | Lignende `G_Freeleech`, angiver `G_DoubleUpload`, at enhver mængde data, du uploader via seeding, tæller dobbelt med i din uploadkvota og -ratio. Dette er meget nyttigt, hvis du vil opbygge en ratio-buffer.      |
| `PTP_Golden`     | 🌟      | På PassThePopcorn får nogle torrents mærket *Golden*, når de opfylder visse kodningsstandarder. Disse er normalt de bedste kodninger, med næsten ingen synlig kvalitetstab. Du kan læse mere på deres wiki-side. |
| `PTP_Approved`   | ✔      | På PassThePopcorn bliver nogle torrents godkendt, når de opfylder minimumsstandarderne for kodning (f.eks. ingen lave bitrater). Se deres wiki for mere information.                                                              |
| `HDB_Internal`   | 🚪      | Udgivelser på HDBits får dette mærke, når udgivelsen blev uploadet af en af HDBits' egne udgivelsesgrupper.                                                                                                       |
| `G_Scene`        | ☠      | Lignende `G_Freeleech`, angiver `G_Freeleech75`, at kun 25% af størrelsen på denne torrent tæller med i din downloadkvota eller -ratio.                                                                              |
| `G_Freeleech75`  | ⇩⬇     | Lignende `G_Freeleech`, angiver `G_Freeleech75`, at kun 25% af størrelsen på denne torrent tæller med i din downloadkvota eller -ratio.                                                                              |
| `G_Freeleech25`  | ⇩      | Lignende `G_Freeleech`, angiver `G_Freeleech25`, at kun 75% af størrelsen på denne torrent tæller med i din downloadkvota eller -ratio.                                                                              |

- (Avanceret indstilling) Indekserprioritet - Prioritet for denne indekser for at foretrække en indekser frem for en anden i scenarier med udgivelsesafgørelse. 1 er højeste prioritet, og 50 er laveste prioritet.
- (Avanceret indstilling) Downloadklient - Vælg og specificer hvilken downloadklient der bruges til at hente fra denne indekser
- Tags - Brug kun denne indekser til film med mindst én matchende tag. Lad være blank for at bruge med alle film.

## Indstillinger

- Minimumsalder - Kun Usenet: Minimumsalder i minutter for NZB'er, før de hentes. Brug dette til at give nye udgivelser tid til at sprede sig til din Usenet-udbyder.
- Opbevaring - Kun Usenet: Indstil til nul for ubegrænset opbevaring
- Maksimal størrelse - Maksimal størrelse for en udgivelse, der skal hentes i MB. Indstil til nul for ubegrænset. Bemærk, at dette gælder globalt.
- Foretrukne indekserflag - Prioriter udgivelser med specielle flag. (Se Påkrævede flag ovenfor)
- Tilgængelighedsforsinkelse - Tidsinterval før (-#) eller efter (#) den tilgængelige dato for at søge efter film
  - Dette er nyttigt for at forsinke søgning efter en udgivelse for at give fællesskabet tid til at udføre de bedste kodninger.
  - Typisk anbefales en filmtilgængelighed på `Udgivet` med en forsinkelse på `-21` eller `-14`.
- RSS-synkroniseringsinterval - Interval i minutter. Indstil til nul for at deaktivere (dette stopper al automatisk udgivelseshentning) Minimum: 10 minutter Maksimum: 120 minutter
  - Se venligst [Hvordan finder Radarr film?](/radarr/faq#how-does-radarr-find-movies) for en bedre forståelse af, hvordan RSS-synkronisering vil hjælpe dig

> Hvis Radarr har været offline i en længere periode, vil Radarr forsøge at bladre tilbage for at finde den sidste udgivelse, den behandlede, i et forsøg på at undgå at gå glip af en udgivelse. Så længe din indekser understøtter bladring, og det ikke har været for længe, vil Radarr være i stand til at behandle de udgivelser, den ville have gået glip af, og undgå at du skal udføre en søgning efter de gik glip af udgivelser.{.is-info}

- Whitelistede underteksttags - Tags, der indtastes her, vil ikke blive betragtet som hardcodede undertekster.
- Tillad hardcodede undertekster - Hvis aktiveret, tillad automatisk download af udgivelser med hardcodede undertekster

# Downloadklienter

> Information om understøttede downloadklienter kan findes på siden [Mere info (Understøttet)](/radarr/supported#download-clients) for denne sektion
{.is-info}

## Oversigt

- Download og import er, hvor de fleste mennesker oplever problemer. Set fra et overordnet perspektiv skal softwaren kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Dette betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alle opsætninger kan være lidt forskellige. Men der er mange forkerte opsætninger.

## Processer for downloadklienter

### Usenet-proces

- Radarr sender en downloadanmodning til din klient og tilknytter den med etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: film, tv, serier, musik osv.
- Radarr overvåger dine downloadklients aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er afsluttet, vil Radarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe og kan tilgås af Radarr
- Radarr scanner den afsluttede filplacering for filer, som Radarr kan bruge. Den analyserer filnavnet for at matche det med den ønskede medie. Hvis det kan gøre det, omdøber den filen i henhold til dine specifikationer og flytter den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringerne skal være de samme for din afsluttede downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Radarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er I/O-intensivt.

### Torrent-proces

- Radarr sender en downloadanmodning til din klient og tilknytter den med etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: film, tv, serier, musik osv.
- Radarr overvåger dine downloadklients aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Afsluttede filer efterlades på deres oprindelige placering for at give dig mulighed for at seede filen (forhold eller tid kan justeres i downloadklienten eller fra Radarr under den specifikke downloadklient). Når filer importeres til din mediemappe, opretter Radarr et hardlink til filen, hvis det understøttes af din opsætning, eller kopierer den, hvis hardlinks ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din afsluttede downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Radarr falde tilbage og kopiere filen.
- Hvis indstillingen "Fuldført downloadhåndtering - Fjern" er aktiveret i Radarrs indstillinger, vil Radarr slette den oprindelige fil og torrent fra din klient, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet (dvs. sat på pause).

## Downloadklienter

Klik på `Indstillinger => Downloadklienter`, og klik derefter på <kb>+</kb> for at tilføje en ny downloadklient. Din downloadklient skal allerede være konfigureret og kørende.

### Understøttede downloadklienter

- En liste over understøttede downloadklienter findes på siden [Mere info (Understøttet)](/radarr/supported#download-clients)

Vælg den downloadklient, du ønsker at tilføje, og der vil være en pop op-boks til at indtaste forbindelsesoplysninger. Disse oplysninger er ens for de fleste klienter. Nogle vil bede om et brugernavn eller adgangskode, nogle vil spørge, om der skal tilføjes nye downloads i en paused/start-tilstand osv.

### Indstillinger for Usenet-klient

- Navn - Navnet på downloadklienten i Radarr
- Aktivér - Aktivér denne downloadklient
- Vært - URL'en til din downloadklient
- Port - Porten til din downloadklient
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er normalt nødvendigt for omvendte proxier.
- API-nøgle - API-nøglen til at godkende din klient
- Brugernavn - Brugernavnet til at godkende din klient (normalt ikke nødvendigt)
- Adgangskode - Adgangskoden til at godkende din klient (normalt ikke nødvendigt)
- Kategori - Kategorien i din downloadklient, som \*Arr vil bruge. For at undgå uvedkommende downloads i Aktivitet anbefales det stærkt at angive en kategori.
- Nylig prioritet - downloadklientprioritet for nyligt udgivet medier
- Ældre prioritet - downloadklientprioritet for medier, der ikke er udgivet for nylig
- (Avanceret indstilling) Klientprioritet - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet
- Håndtering af fuldførte downloads
  - Fjern (Per klientindstilling) - Fjern fuldførte downloads, når de er færdige (usenet) eller stoppet/fuldført (torrents). Se [Fuldført downloadhåndtering for flere detaljer](#completed-download-handling)

### Indstillinger for torrentklient



- Navn - Navnet på downloadklienten i Radarr
- Aktivér - Aktivér denne downloadklient
- Vært - URL'en til din downloadklient
- Port - Porten til din downloadklient; dette er normalt webgui-porten
- Brug SSL - Brug en sikker forbindelse med din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- Brugernavn - brugernavnet til at godkende din klient
- Adgangskode - adgangskoden til at godkende din klient
- Kategori - kategorien i din downloadklient, som \*Arr vil bruge. For at undgå irrelevante downloads i Aktivitet anbefales det stærkt at angive en kategori.
- Kategori efter import - kategorien der skal angives efter at udgivelsen er downloadet og importeret. Bemærk venligst, at dette bryder fjernelse af afsluttet downloadhåndtering.
- Nylig prioritet - downloadklientprioritet for nyligt udgivet medier
- Ældre prioritet - downloadklientprioritet for medier, der ikke er udgivet for nylig
- Indledende tilstand - Indledende tilstand for torrents (kun Qbittorrent: Tvinger omgåelse af alle seed-tærskler)
- (Avanceret indstilling) Klientprioritet - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet
- Håndtering af afsluttede downloads
  - Fjern (per klientindstilling) - Fjern afsluttede downloads, når de er færdige (usenet) eller stoppet/færdige (torrents). Se [Håndtering af afsluttede downloads for flere detaljer](#completed-download-handling)
    - For torrents kræver dette, at din downloadklient sættes på pause, når seed-målene nås. Det kræver også, at seed-målene understøttes af Radarr i henhold til nedenstående tabel. Torrents skal også forblive i samme kategori.

### Kompatibilitet med fjernelse af download i torrentklient

- Radarr kan kun indstille seed-forhold/tid på klienter, der understøtter indstillingen af denne værdi via deres API, når torrenten tilføjes. Seed-mål kan indstilles globalt i klienten selv eller pr. tracker i \*Arr-indstillinger for hver indexer. Se tabellen nedenfor for klientkompatibilitet.

|      Klient       |                                Forhold                                |                                    Tid                                    |
| :---------------: | :------------------------------------------------------------------: | :------------------------------------------------------------------------: |
|       Aria2       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |    ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)    |
|      Deluge       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |    ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)    |
| Download Station  | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |    ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)    |
|       Flood       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |      ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)      |
|     Hadouken      | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |    ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)    |
|    qBittorrent    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |      ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)      |
|     rTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |      ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)      |
| Torrent Blackhole | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |    ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)    |
|   Transmission    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Understøttet-Idle%20Limit*-blue)\* |
|     uTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |      ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)      |
|       Vuze        |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |      ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)      |

> ![Idle Limit](https://img.shields.io/badge/Understøttet-Idle%20Limit*-blue) - Transmission har internt en kontrol af inaktiv tid, men Radarr sammenligner den med seedningstiden, hvis inaktivitetsgrænsen er indstillet på en per-torrent-basis. Dette gøres som en løsning på Transmission's API-begrænsninger.{.is-info}

## Håndtering af afsluttede downloads

- Håndtering af afsluttede downloads er, hvordan Radarr importerer medier fra din downloadklient til dine seriemapper. Mange almindelige problemer er relateret til dårlige Docker-stier og/eller andre Docker-tilladelsesproblemer.

- (Avanceret global indstilling) Aktivér - Importer automatisk afsluttede downloads fra downloadklienten
- (Avanceret indstilling) Kontroller interval for færdiggjorte downloads - Indstil, hvor ofte du vil forespørge downloadklientens køer og opdatere overvågede downloads, minimum 1 minut
- (Per klientindstilling) Fjern - Fjern afsluttede downloads, når de er færdige (usenet) eller stoppet/færdige (torrents)
  - For torrents kræver dette, at din downloadklient sættes på pause, når seed-målene nås. Det kræver også, at seed-målene understøttes af Radarr i henhold til ovenstående tabel. Torrents skal også forblive i samme kategori.

### Fjern afsluttede downloads

- Radarr sender en downloadanmodning til din klient og forbinder den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
- Radarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er færdig, ved Radarr den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et andet sted end din mediemappe.
- Radarr scanner denne færdige filplacering for videofiler. Den analyserer videofilens navn for at matche den med en film. Hvis det kan gøre det, omdøber den filen i henhold til dine specifikationer og flytter den til den tildelte biblioteksmappe.
- Overskydende filer fra downloaden sendes til papirkurven eller genbrug.

Hvis du downloader ved hjælp af en BitTorrent-klient, er processen lidt anderledes:

- Færdige filer efterlades på deres oprindelige placering for at tillade seeding. Når filer importeres til din tildelte biblioteksmappe, vil Radarr forsøge at oprette en hardlink til filen eller falde tilbage til at kopiere (bruger dobbelt plads), hvis hardlinks ikke understøttes.
- Hvis indstillingen "Håndtering af afsluttede downloads - Fjern" er aktiveret i indstillingerne, vil Radarr bede torrentklienten om at slette den oprindelige fil og torrent, men dette vil kun ske, hvis klienten rapporterer, at seeding er fuldført, torrenten er i samme kategori (dvs. ikke bruger en kategori efter import), seedmålet nået understøttes af Radarr, og torrenten er sat på pause (stoppet).

### Håndtering af mislykkede downloads

- Håndtering af mislykkede downloads er kun kompatibel med SABnzbd og NZBGet.
- Håndtering af mislykkede downloads gælder ikke for torrents, og der er ingen planer om at tilføje en sådan funktionalitet.

- Der er flere komponenter, der udgør processen for håndtering af mislykkede downloads:

- Kontroller downloader:
  - Kø - Kontroller din downloaders kø for adgangskodebeskyttede (krypterede) udgivelser, der er markeret som mislykket
  - Historik - Kontroller din downloaders historik for fejl (f.eks. ikke nok til reparation eller udpakning mislykkedes)
- Når Radarr finder en mislykket download, starter den behandlingen og gør følgende:
  - Tilføjer en mislykket begivenhed til Radarr's historik
  - Fjerner den mislykkede download fra downloadklienten for at frigøre plads og rydde downloadede filer (valgfrit)
  - Begynder at søge efter en erstatningsfil (valgfrit)
  - Blokeringsliste (tidligere 'Blacklisting') tillader automatisk spring af nzbs, når de mislykkes, dette betyder, at nzb aldrig vil blive downloadet automatisk af Radarr igen (du kan stadig tvinge downloaden via en manuel søgning).
  - Der er 2 avancerede indstillinger (på siden 'Downloadklient' indstillinger), der styrer adfærden for mislykket download i Radarr, i øjeblikket er de alle aktiveret som standard.

- Genhent - Kontroller, om Radarr skal søge efter den samme fil efter en fejl
- (Avanceret indstilling) Fjern - Om downloaden automatisk skal fjernes fra downloadklienten, når fejlen opdages

## Fjern sti-mapping

- Fjern sti-mapping fungerer som en simpel find fjern sti og erstat med lokal sti. Dette bruges primært til enten fusionerede lokale/fjernopstillinger ved hjælp af mergerfs eller lignende eller bruges, når applikationen og downloadklienten ikke er på samme server.
- En fjern sti-mapping bruges, når din downloadklient rapporterer en sti for fuldførte data enten på en anden server eller på en måde, som \*Arr ikke adresserer den mappe.
- Generelt er en fjern sti-map kun nødvendig, hvis din downloadklient er på Linux, når \*Arr er på Windows eller omvendt. En fjern sti-map er også muligvis nødvendig, hvis du blander Docker- og Native-klienter eller hvis du bruger en fjernserver.
- En fjern sti-map er en DUMB søg/erstat (hvor den finder den FJERNE værdi, erstatter den med den LOKALE værdi for den angivne vært).
- Hvis fejlmeddelelsen om en dårlig sti ikke indeholder den ERSTATTEDE værdi, fungerer sti-mappingen ikke, som du forventer. Den typiske løsning er at tilføje og fjerne mappingen.
- [Se TRaSH's vejledning for yderligere oplysninger om fjern sti-mapping](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og din downloadklient er Docker-containere, er det sjældent nødvendigt med en fjern sti-map. Det anbefales at [gennemgå Docker-guiden](/docker-guide) og/eller [følge TRaSH's vejledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlister

> Oplysninger om understøttede listetyper kan findes på siden [Flere oplysninger (Understøttet)](/radarr/supported#lists) for denne sektion
{.is-info}

## Lister

Importlister er en del af Radarr, der giver dig mulighed for at følge en given listeskaber. Lad os sige, at du følger en bestemt listeskaber på Trakt/TMDb og virkelig kan lide deres ArrowVerse Collection-sektion og gerne vil se alle shows på deres liste. Du kigger i din Radarr og opdager, at du ikke har disse serier. I stedet for at søge én efter én og tilføje disse elementer og derefter søge dine indexere efter disse serier, kan du gøre alt dette på én gang med en liste. Listene kan indstilles til at importere alle serierne på den kurators liste samt automatisk tildele en kvalitetsprofil, automatisk tilføje og automatisk overvåge den serie.

- FORSIGTIG: Hvis lister gøres forkert, vil de absolut ødelægge dit bibliotek med en masse skrald, som du ikke har til hensigt at se. Så sørg for at vide, hvad du importerer, før du klikker på Gem. Dvs. se fysisk på listen, før du overhovedet går til Radarr.

- Her kan du vælge <kb>+</kb>-knappen for at åbne et nyt pop op-vindue
- Fra dette nye vindue får du præsenteret mange forskellige muligheder for at opsætte din liste fra mange forskellige listeleverandører. Som tidligere nævnt skal du være forsigtig med lister. Det anbefales kraftigt ikke at vælge Søg ved tilføjelse-knappen, før du er helt sikker på, at listen, du vælger/opsætter, tilføjer de serier, du leder efter.
- Når du har valgt den listeudbyder, du vil trække fra (såsom IMDb eller Trakt), får du præsenteret et nyt vindue.
De fleste indstillinger for lister er ret selvforklarende, nogle lister kræver, at du godkender med udbyderen, f.eks. Trakt (kræver, at du har en konto hos Trakt.tv)

## Listeindstillinger

- (Avanceret indstilling) Opdateringsinterval for liste - Hvor ofte skal Radarr undersøge listen for opdateringer? [Dette er mindst 6 timer.](/radarr/faq#why-are-lists-sync-times-so-long-and-can-i-change-it)
- (Avanceret indstilling) Niveau for rensning af bibliotek - Film i biblioteket fjernes eller overvåges, hvis de ikke er på dine liste(r)
  - Deaktiveret - Rens ikke biblioteket (Anbefales)
  - Kun log - Log kun film, der ikke er på listen(e), og foretag ingen andre handlinger
  - Behold og fjern overvågning af film - Behold film, der ikke er på listen(e), men fjern overvågningen af dem i Radarr.
  - Fjern film og behold filer - Fjern film, der ikke er på listen(e), fra Radarr, men slet ikke deres filer
  - Fjern film og slet filer - Fjern film, der ikke er på listen(e), fra Radarr, og slet deres filer

## Listeundtagelser

- Undtagelse for importliste - Dette giver dig mulighed for at beskære din liste over film, du ikke ønsker at se igen. Et eksempel på dette er, hvis din liste tilfældigvis indeholder en film, der er på et fremmedsprog, og det er usandsynligt, at du nogensinde vil finde denne film på dit modersmål, og du ikke ønsker at se den med undertekster. Du kan udelukke en film fra at blive tilføjet i fremtiden. Imidlertid kan du tilføje den tilbage til listen i undtagelsessektionen, så når listen kører igen, vil den blive læst til dit bibliotek.

# Forbindelse

> Oplysninger om understøttede forbindelsestyper kan findes på siden [Flere oplysninger (Understøttet)](/radarr/supported#notifications) for denne sektion
{.is-info}

## Forbindelser

Forbindelser er, hvordan du vil have Radarr til at kommunikere med omverdenen.

- Ved at trykke på <kb>+</kb>-knappen præsenteres du for et nyt vindue, der giver dig mulighed for at konfigurere mange forskellige slutpunkter

- En liste over understøttede meddelelser og forbindelser findes på siden [Flere oplysninger (Understøttet)](/radarr/supported#notifications)

## Forbindelsesudløsere

- Ved Grab - Få besked, når film er tilgængelige til download og er sendt til en downloadklient
- Ved import - Få besked, når film er importeret med succes
- Ved opgradering - Få besked, når film opgraderes til en bedre kvalitet
- Ved omdøbning - Få besked, når film omdøbes
- Ved tilføjelse af film - Få besked, når film tilføjes til Radarr's bibliotek til styring eller overvågning
- Ved sletning af film - Få besked, når film slettes
- Ved sletning af filmfil - Få besked, når filmfiler slettes
- Ved sletning af filmfil til opgradering - Få besked, når filmfiler slettes til opgraderinger
- Ved sundhedsproblem - Få besked om fejl i sundhedstjek
  - Inkluder sundhedsadvarsler - Få besked om sundhedsadvarsler ud over fejl.
- Ved opdatering af applikation - Få besked, når Radarr opdateres til en ny version

# Metadata

## Indstillinger

- Certificeringsland - Vælg landet, der skal bruges til filmcertificeringer (f.eks. R (USA) eller 12A (UK))

## Metadataforbrugere

> Oplysninger om understøttede metadataforbrugere kan findes på siden [Flere oplysninger (Understøttet)](/radarr/supported#metadata) for denne sektion
{.is-info}

Her kan du vælge den type metadata, der skal bruges af din medieafspiller

Kodi vil være en af de mest almindeligt anvendte muligheder her, hvis det er den software, der bruges. Dette vil tillade Radarr at oprette en NFO-fil samt tilknyttede filmpostere, der skal skrabes ind i din afspiller

# Tags

- Tag-sektionen i Radarr bruges til at linke forskellige aspekter af Radarr. De er også nyttige til at spore, hvilke film der kommer fra hvilke lister.
- Tags er særligt nyttige til:

  - Forsinkelsesprofiler
  - Restriktioner
  - Indexere

- Tags kan bruges til at linke Forsinkelsesprofiler, Indexere og Restriktioner og Film sammen.
- For eksempel:
  - Du vil kun have, at en bestemt indexer skal bruges til en bestemt film. Du ville oprette en tag og tildele filmen og indexeret det tag.
  - Du vil have, at en bestemt restriktion kun skal gælde for en bestemt film. Du ville oprette en tag og tildele restriktionen og filmen det tag.
  - Denne proces er den samme for Forsinkelsesprofiler.

> En film vil bruge både indexere, der har matchende tags, og indexere, der ikke har tags.
{.is-warning}

> Bemærk: Tags påvirker ikke "Brugerdefinerede formater", "Kvalitetsprofiler" eller andre aspekter, der ikke er nævnt ovenfor.
{.is-info}

# Generelt

## Vært

- Bind Address - Gyldig IPv4-adresse eller '*' for alle grænseflader
  - 0.0.0.0 eller `*` - enhver adresse kan oprette forbindelse
  - 127.0.0.1 eller localhost - kun lokalværtsapplikationer kan oprette forbindelse
  - Enhver anden IP (f.eks. 1.2.3.4) - kun den IP (1.2.3.4) kan oprette forbindelse
- Portnummer - Portnummeret, du vil bruge til at få adgang til webgrænsefladen for Radarr

> Bemærk: Hvis du bruger Docker, skal du ikke ændre denne indstilling.
{.is-warning}

- URL-base - Til understøttelse af omvendt proxy, standard er tom

> Bemærk: Hvis du bruger en omvendt proxy (f.eks. mydomain.com/radarr), skal du indtaste '/radarr' som URL-base.
{.is-info}

- Aktivér SSL - Hvis du har SSL-legitimationsoplysninger og gerne vil sikre kommunikationen til og fra din Radarr, skal du aktivere denne indstilling.

> Bemærk: Brug ikke dette, medmindre du ved, hvad du laver.
{.is-warning}

## Sikkerhed

- Godkendelse - Hvordan vil du godkende adgang til din Radarr-instans
  - Fra og med Radarr v5 er godkendelse nu obligatorisk. [Se FAQ-indgangen om obligatorisk godkendelse for detaljer.](/radarr/faq#forced-authentication)
  - ~~Ingen - Du har ingen godkendelse for at få adgang til din Radarr. Normalt hvis du er den eneste bruger på dit netværk, ikke har nogen på dit netværk, der vil have adgang til din Radarr, eller din Radarr ikke er eksponeret for internettet~~
  - Grundlæggende (Browser pop-up) - Denne indstilling viser en lille pop-up, når du får adgang til din Radarr, der giver dig mulighed for at indtaste et brugernavn og adgangskode
  - Formularer (Loginside) - Denne indstilling har en velkendt login-skærm, ligesom andre websteder har, der giver dig mulighed for at logge på din Radarr
- API-nøgle - Dette er, hvordan andre programmer kommunikerer eller får Radarr til at kommunikere med andre programmer. Hvis denne nøgle gives til den forkerte person med adgang, kan der ske alle mulige ting med din bibliotek. Derfor er API-nøglen sløret i logfilerne
- Certifikatvalidering - Ændrer, hvor streng valideringen af HTTPS-certifikater er
  - Aktiveret - Valider alle HTTPS-certifikater (anbefales)
  - Deaktiveret for lokale adresser - Valider alle HTTPS-certifikater undtagen dem på localhost og LAN
  - Deaktiveret - Valider ingen HTTPS-certifikater
  
## Proxy

Proxy - Denne indstilling giver dig mulighed for at køre den information, din Radarr henter og søger efter, gennem en proxy. Dette kan være nyttigt, hvis du befinder dig i et land, der ikke tillader download af torrentfiler

- Brug Proxy - Aktivér for at bruge en proxy
- Proxytype - Vælg din proxytype (HTTPS, Socks4 eller Socks5)
- Værtsnavn - Indtast dit proxy-værtsnavn (Inkluder ikke http/https eller nogen anden protokol)
- Port - Indtast din proxy-port
- Brugernavn - Indtast dit proxy-brugernavn, hvis relevant
- Adgangskode - Indtast din proxy-adgangskode, hvis relevant
- Ignorerede adresser - Indtast en kommasepareret liste over adresser, der skal omgås proxyen
- Omgå proxy for lokale adresser - Markér afkrydsningsfeltet for at omgå proxyen for lokale adresser. Lokale anmodninger identificeres ved manglende punktum (.) i URI'en, f.eks. <http://webserver/>, eller ved at få adgang til den lokale server, herunder <http://localhost>, <http://loopback> eller <http://127.0.0.1>. Når dette ikke er markeret, sendes alle internetanmodninger gennem proxyserveren.

## Logning

- Logniveau - Sandsynligvis et af de mest nyttige fejlfindingværktøjer
  - Info - Dette er den mest grundlæggende måde, Radarr indsamler information på. Denne logfil indeholder fatal, fejl, advarsel og info-oplysninger.
  - Debug - Debug inkluderer alle de oplysninger, som Info inkluderer, plus flere oplysninger, der kan være nyttige. Denne logfil indeholder fatal, fejl, advarsel, info og debug-oplysninger.
  - Trace - Den mest avancerede og detaljerede logning på Radarr. Trace inkluderer alle de oplysninger, der er indsamlet af Info og Debug og mere. Dette er den mest almindelige type log, der bliver bedt om, når der fejlfindes på Discord eller Reddit. Hvis du har brug for hjælp, skal du vælge din log til Trace og gentage den opgave, der gav dig problemer, for at fange loggen. Denne logfil indeholder fatal, fejl, advarsel, info, debug og trace-oplysninger.

## Analyse

- Analyse - Send anonym brugs- og fejlinformation til Radarr's servere (Servarr). Dette inkluderer oplysninger om din browser, hvilke Radarr WebUI-sider du bruger, fejlrapportering samt OS- og runtime-version. Vi vil bruge disse oplysninger til at prioritere funktioner og fejlrettelser.

## Opdateringer

- (Avanceret indstilling) Gren - Dette er grenen af Radarr, du kører på.
  - [Se denne FAQ-indgang for mere information](/radarr/faq#how-do-i-update-radarr)
- Automatisk - Hent og installer opdateringer automatisk. Du vil stadig kunne installere fra System: Opdateringer. Bemærk: Windows-brugere opdateres altid automatisk.
- Mekanisme - Brug Radarr's indbyggede opdateringsfunktion eller et script
  - Indbygget - Brug Radarr's egen opdateringsfunktion
  - Script - Få Radarr til at køre opdateringsscriptet
  - Docker - Opdater ikke Radarr indefra Docker, træk i stedet et helt nyt billede med den nye opdatering
- Script - Synlig kun når mekanismen er indstillet til Script - Sti til opdateringsscript
- Opdateringsproces - Radarr vil downloade opdateringsfilen, verificere dens integritet, udpakke den til en midlertidig placering og kalde den valgte metode. Opdateringsprocessen køres under samme bruger som Radarr, den skal have tilladelser til at opdatere Radarr-filerne samt stoppe/starte Radarr.
- Indbygget - Den indbyggede metode vil tage sikkerhedskopier af Radarr-filer og indstillinger, stoppe Radarr, opdatere installationen og starte Radarr igen. Hvis dit system ikke kan håndtere stop af Radarr og vil forsøge at genstarte det automatisk, kan det være bedst at bruge et script i stedet. Hvis opdateringen mislykkes, genstartes den tidligere version af Radarr.
- Script - Scriptet skal håndtere det samme som den indbyggede opdatering, hvis du skal håndtere stop og start af tjenester (upstart/launchd/etc), skal du gøre det her.

## Sikkerhedskopier

- Sikkerhedskopisektionen giver dig mulighed for at fortælle Radarr, hvordan du vil håndtere sikkerhedskopier

- (Avanceret indstilling) Mappe - Dette giver dig mulighed for at vælge placeringen for sikkerhedskopier. I Docker vil du være begrænset til, hvad du tillader, at containeren ser. Stier er relative til appdata-mappen; hvis det er nødvendigt, kan du angive en absolut sti til sikkerhedskopier uden for appdata-mappen.
- (Avanceret indstilling) Interval - Hvor ofte vil du have, at Radarr skal lave en sikkerhedskopi
- (Avanceret indstilling) Opbevaring - Hvor længe vil du have, at Radarr skal beholde hver sikkerhedskopi. Efter oprettelse af en ny sikkerhedskopi fjernes den ældste sikkerhedskopi

> Manuelle sikkerhedskopier bevares for evigt, opbevares i samme mappe og har forskellige navne.
{.is-info}

# Brugergrænseflade

## Kalender

- Første ugedag - Her kan du vælge, hvilken dag du mener, at ugen skal starte på.
- Ugekolonneoverskrift - Her kan du vælge overskriften for kolonnerne

## Film

- Kørselsformat - Vælg, hvordan køretider skal formateres, enten som timer og minutter eller minutter

## Datoer

- Kort datoformat - Hvordan vil du have, at Radarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du have, at Radarr skal vise datoer i langt format?
- Tidsformat - Vil du have et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du have, at Radarr skal vise relative (i dag/i går/osv.) eller absolutte datoer?

## Stil

- Aktivér farveblindtilstand - Ændret stil for at tillade farveblinde brugere at skelne farvekodede oplysninger bedre

## Sprog

- Sprog for filmoplysninger - Vælg sproget, som Radarr skal vise filmoplysninger på i brugergrænsefladen
- Brugergrænsefladesprog - Vælg sproget, som Radarr skal bruge i applikationens brugergrænseflade