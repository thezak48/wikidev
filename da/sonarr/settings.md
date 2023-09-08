---
title: Sonarr Indstillinger
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, needs-love, indstillinger
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Menuindstillinger](#menuindstillinger)
- [Mediehåndtering](#mediehåndtering)
  - [Forslag til fællesskabsnavngivning](#forslag-til-fællesskabsnavngivning)
  - [Episodenavngivning](#episodenavngivning)
    - [Standard episodformat](#standard-episodformat)
    - [Serienavngivning](#serienavngivning)
    - [Serie-ID'er](#serie-id'er)
    - [Sæsoner](#sæsoner)
    - [Episoder](#episoder)
    - [Sendetidspunkt](#sendetidspunkt)
    - [Episodetitel](#episodetitel)
    - [Kvalitet](#kvalitet)
    - [Medieoplysninger](#medieoplysninger)
    - [Andet](#andet)
    - [Original](#original)
  - [Dagligt episodformat](#dagligt-episodformat)
  - [Anime episodformat](#anime-episodformat)
    - [Absolut episodenummer](#absolut-episodenummer)
  - [Serie-mappenavnformat](#serie-mappenavnformat)
    - [Serienavngivning](#serienavngivning-1)
    - [Serie-ID'er](#serie-id'er-1)
  - [Sæsonmappenavnformat](#sæsonmappenavnformat)
    - [Sæsoner](#sæsoner-1)
  - [Sæsonmappenavnformat](#sæsonmappenavnformat-1)
    - [Specials](#specials)
  - [Multi-episodestil](#multi-episodestil)
  - [Mapper](#mapper)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
  - [Tilladelser](#tilladelser)
  - [Rodmapper](#rodmapper)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Sprogprofiler](#sprogprofiler)
  - [Forsinkelsesprofiler](#forsinkelsesprofiler)
    - [Anvendelse](#anvendelse)
    - [Sådan fungerer forsinkelsesprofiler](#sådan-fungerer-forsinkelsesprofiler)
      - [Eksempler](#eksempler)
        - [Eksempel 1](#eksempel-1)
        - [Eksempel 2](#eksempel-2)
        - [Eksempel 3](#eksempel-3)
  - [Udgivelsesprofiler](#udgivelsesprofiler)
- [Kvalitet](#kvalitet-1)
  - [Betydning af kvalitetstabellen](#betydning-af-kvalitetstabellen)
  - [Definerede kvaliteter](#definerede-kvaliteter)
- [Indexere](#indexere)
  - [Understøttede indexere](#understøttede-indexere)
    - [Indexerindstillinger](#indexerindstillinger)
    - [Usenet Indexer-konfiguration](#usenet-indexer-konfiguration)
    - [Torrent Tracker-konfiguration](#torrent-tracker-konfiguration)
  - [Indstillinger](#indstillinger)
- [Downloadklienter](#downloadklienter)
  - [Overblik](#overblik)
  - [Processer for downloadklienter](#processer-for-downloadklienter)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
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
  - [Listeundtagelser](#listeundtagelser)
- [Forbindelse](#forbindelse)
  - [Forbindelser](#forbindelser)
  - [Forbindelsestriggere](#forbindelsestriggere)
- [Metadata](#metadata)
  - [Metadata](#metadata-1)
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
  - [Datoer](#datoer)
  - [Stil](#stil)
  
Denne side vil gennemgå alle de indstillinger, der er tilgængelige i Sonarr, og hvordan de fungerer. Dette er ikke ment som en omfattende "Sådan opsættes Sonarr". Se i stedet [Hurtigstart](/sonarr/quick-start-guide)-siden.

# Menuindstillinger

For at komme til indstillingssiden skal du vælge Indstillinger i venstremenuen. Følgende undermenuindstillinger vil være tilgængelige:

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

Bemærk også, at der for hver individuel indstillingsside er nogle indstillinger øverst i menuen:

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- Skjul/Vis avanceret er vigtigt for eventuelle elementer, der er markeret nedenfor som `(Avanceret indstilling)`, ellers vises de ikke. Disse menupunkter vises i orange på skærmbillederne.

- Du skal gemme dine ændringer, før du forlader skærmen. Dette gøres ved at klikke på diskikonet. Hvis du ikke har foretaget ændringer, vises "Ingen ændringer" og er gråtonet, som vist ovenfor.

# Mediehåndtering

> Nogle af disse indstillinger er kun synlige via `Vis avancerede indstillinger`, som er placeret øverst i værktøjslinjen under søgefeltet{.is-info}

## Forslag til fællesskabsnavngivning

> Her er nogle forslag til fællesskabsnavngivning fra [TRaSH's Guides](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/){.is-info}

> Advarsel: Fra og med v3.0.6.1431 understøtter Sonarr nu genkendelse af Dolby Vision (DV) og High Dynamic Range (HDR) typer. Hvis du bruger en ældre version, skal du erstatte: `{[MediaInfo VideoDynamicRangeType]}` med `{[MediaInfoVideoDynamicRange]}`{.is-warning}

- Standardserier: `{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Daglige serier: `{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Anime-serier: `{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- Sæsonmapper: `Sæson {season:00}`

- Multi-episodestil: `Scene`

- Seriemapper: `{Series TitleYear} [imdb-{ImdbId}]`

## Episodenavngivning

- Omdøb episoder - Markér for at aktivere Sonarr til at omdøbe filer
  - Hvis ikke markeret:
    - Import af downloadklient
      - Ikke-sæsonpakke: Downloadklientens udgivelsestitel bruges
      - Sæsonpakke: Oprindeligt filnavn
    - Manuel (Ad-Hoc) import: Oprindeligt filnavn

- Erstat ulovlige tegn - Hvis ikke markeret, fjerner Sonarr dem i stedet.
  - Tegnene er: `:` `\` `/` `>` `<` `?` `*` `|` `"`

### Standard episodformat

Standard episodformat - Indstil navngivningskonventionen for dine episoder af standard serietype. Klik på `?`-ikonet for at åbne dialogboksen `Filnavnetokens`.

- Rullemenu (øverst til højre)
  - Venstre boks - Håndtering af mellemrum
  - Mellemrum ( ) - Brug mellemrum i navngivningen (standard)
  - Periode (.) - Brug punktummer i stedet for mellemrum i navngivningen
  - Underscore (_) - Brug understregninger i stedet for mellemrum i navngivningen
  - Bindestreg (-) - Brug bindestreger i stedet for mellemrum i navngivningen
  - Højre boks - Håndtering af store og små bogstaver
  - Standard sag - Gør titlen til store og små bogstaver (~camel-case) (standard)
  - Store bogstaver - Gør titlen til store bogstaver
  - Små bogstaver - Gør titlen til små bogstaver

### Serienavngivning

- `{Series Title}` = Seriens navn!
- `{Series CleanTitleYear}` = Seriens navn! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Seriens navn!
- `{Series TitleThe}` = Seriens navn!, The
- `{Series TitleYear}` = Seriens navn (2010)
- `{Series Year}` = (2010)

### Serie-ID'er

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### Sæsoner

- `{season:0}` = 1
- `{season:00}` =  01

### Episoder

- `{episode:0}` = 1
- `{episode:00}` = 01

### Sendetidspunkt

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### Episodetitel

- `{Episode Title}` = Episodetitel
- `{Episode CleanTitle}` =  Episodetitel

### Kvalitet

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Medieoplysninger

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguagesAll}` = \[DE\]
- `{MediaInfo AudioLanguagesAll}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`, `AudioLanguages` og `SubtitleLanguages` understøtter en `:EN+DE`-suffiks, der giver dig mulighed for at filtrere sprogene, der er inkluderet i filnavnet. Brug `-DE` til at udelukke specifikke sprog. Hvis du tilføjer <kb>+</kb> (f.eks.: `:EN+`), vil det resultere i `[EN]`, `[EN+--]` eller `[--]` afhængigt af de udeladte sprog. For eksempel `{MediaInfo Full:EN+DE}`{.is-info}

> `AudioLanguages` viser ikke et sprog for lyd, hvis der kun findes ét sprog, og det er EN (engelsk). For at få den ønskede adfærd og som et eksempel, der viser tysk og engelsk, skal du bruge {MediaInfo AudioLanguagesAll:DE+EN} i stedet{.is-info}

> `MediaInfo VideoDynamicRangeType` vil give mulige værdier: DV, DV HDR10, HDR10, HDR10Plus, HLG, PQ og HDR{.is-info}

### Andet

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL eller NF

> \* Foretrukne ord vil være det ord eller de ord, der var de bogstavelige match af eventuelle foretrukne ord, du har. I det ovenstående eksempel ville det være et foretrukket ord som `iNTERNAL` eller tilsvarende et foretrukket ord som `/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i` ville returnere `AMZN` eller `Amazon`{.is-info}

### Original

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> `Original Title` er udgivelsesnavnet, og det er det, der foreslås at blive brugt{.is-info}

>`Original Filename` anbefales ikke. Det er det bogstavelige oprindelige filnavn og kan være obfuskeret `t1i0p3s7i8yu7ti`{.is-warning}

## Dagligt episodformat

Dagligt episodformat - Indstil navngivningskonventionen for dine episoder af daglig serietype. Klik på `?` for at åbne dialogboksen `Filnavnetokens`.

Se [Standard episodformat](/sonarr/settings#standard-episode-format) for mere information om denne dialogboks.

## Anime episodformat

Anime episodformat - Indstil navngivningskonventionen for dine episoder af anime serietype. Klik på `?` for at åbne dialogboksen `Filnavnetokens`.

Se [Standard episodformat](/sonarr/settings#standard-episode-format) for mere information om denne dialogboks.

### Absolut episodenummer

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## Serie-mappenavnformat

(Avanceret indstilling) - Serie-mappe - Indstil navngivningskonventionen for mappen. Klik på `?` for at åbne dialogboksen `Filnavnetokens`.

### Serienavngivning

- `{Series Title}` = Seriens navn!
- `{Series CleanTitleYear}` = Seriens navn! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Seriens navn!
- `{Series TitleThe}` = Seriens navn!, The
- `{Series TitleYear}` = Seriens navn (2010)
- `{Series Year}` = (2010)

### Serie-ID'er

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## Sæsonmappenavnformat

### Sæsoner

- `{season:0}` = 1
- `{season:00}` = 01

## Sæsonmappenavnformat

### Specials

Navn til `Specials` (sæson) mappen

- `Specials`

> Det anbefales at bruge `Specials`{.is-info}

## Multi-episodestil

- `Extend` = `S01E01-02-03`
- `Duplicate` = `S01E01.S01E01`
- `Repeat` = `S01E01E02E03`
- `Scene` = `S01E01-E02-E03`
- `Range` = `S01E01-03`
- `Prefixed Range` = `S01E01-E03`

> Det anbefales at bruge `Scene`{.is-info}

## Mapper

- Opret tomme mediemapper - Opret manglende seriemapper under diskscanning
- Slet tomme mapper - Slet tomme seriemapper og sæsonmapper under diskscanning og når episodfiler slettes

## Importering

- Titel på afsnit påkrævet - Forhindrer import i op til 48 timer fra episodens [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) sendetid, hvis episodens titel er i navngivningsformatet, og episodens titel er TBA (To Be Announced). Efter 48 timer vil importen blive importeret, selvom titlen stadig er TBA.
  - Altid - Vent altid op til 48 timer på en titel, før du importerer, hvis episoden er TBA.
  - Kun for sæsonpakker - Vent kun op til 48 timer på en titel, før du importerer, hvis episoden er TBA, og der findes en sæsonpakke eller bulkudgivelse. <- Dette anbefales.
  - Aldrig - Forsink ikke import, hvis episoden er TBA.
- Spring kontrol af ledig plads over - Brug, når Sonarr ikke kan registrere ledig plads fra din serie rodmappe.
- Minimum ledig plads - Hvis dette aktiveres, forhindres import, hvis der vil være mindre end denne mængde diskplads tilgængelig.
- Brug hardlinks i stedet for kopiering - Brug hardlinks, når du prøver at kopiere filer fra torrents, der stadig bliver seedet.
  - For mere information om dette klik [her](https://trash-guides.info/hardlinks)

 > Sjældent - men muligvis - kan filspærringer forhindre omdøbning af filer, der bliver seedet. Du kan midlertidigt deaktivere seeding og bruge Sonarrs omdøbningsfunktion som en løsning. {.is-warning}

- Importer ekstra filer - Importer matchende ekstra filer (undertekster, nfo, osv.) efter import af en fil.
  Hvis et undertekstfilnavn indeholder yderligere tags som f.eks. `cc` eller `forced`, vil de blive bevaret, så længe de genkendes (i øjeblikket i udviklingsversionen).

## Filhåndtering

- Fjern overvågning af slettede episoder - Episoder, der er slettet fra disken, overvåges automatisk ikke længere i Sonarr.
- Download korrekte og repacks - Om Sonarr automatisk skal opgradere til korrekte og repacks. Brug "Foretræk ikke" til at sortere efter foretrukne ordscore over korrekte og repacks.
  - Foretræk og opgrader - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl nye repacks og korrekte som en opgradering til nuværende udgivelser.
  - Opgrader ikke automatisk - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl ikke nye repacks og korrekte som en opgradering til nuværende udgivelser.
  - Foretræk ikke - Ignorer effektivt repacks og korrekte. Du skal administrere eventuelle præferencer for disse med [Udgivelsesprofiler (Foretrukne ord)](#release-profiles).

> `PROPER` - betyder, at der var et problem med den tidligere udgivelse. Downloads mærket som PROPER viser, at problemerne er blevet løst i den udgivelse. Dette er gjort af en gruppe, der ikke udgav originalen.
> `REPACK` - betyder, at der var et problem med den tidligere udgivelse, og det er rettet af den oprindelige gruppe. Downloads mærket som REPACK viser, at problemerne er blevet løst i den udgivelse. Dette er gjort af en gruppe, der udgav originalen. {.is-info}

> [Brug foretrukne ord til automatisk opgradering til korrekte og repacks](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#propers-and-repacks) {.is-info}

- Analyser videofiler - Udtræk filoplysninger som opløsning, køretid og codec-oplysninger fra filer. Dette kræver, at Sonarr læser dele af filen, hvilket kan medføre høj disk- eller netværksaktivitet under scanning.
- Genindlæs seriemappe efter opdatering - Genindlæs seriemappen efter opdatering af serien
  - Altid - Dette vil genindlæse seriemappen baseret på opgaveplanen
  - Efter manuel opdatering - Du skal manuelt genindlæse disken
  - Aldrig - Som det siger, genindlæs aldrig seriemappen.
- Skift filens dato - Skift filens dato ved import/genindlæsning
  - Ingen - Sonarr ændrer ikke datoen, der vises i din filbrowser
  - Lokal udgivelse - Datoen, videoen blev sendt lokalt
  - UTC-udgivelsesdato - Datoen, videoen blev udgivet baseret på UTC
- Genbrugsbin - Episodefiler vil blive flyttet hertil, når de slettes, i stedet for at blive slettet permanent
- Rensning af genbrugsbin - Dette er, hvor gammel en given fil kan være, før den slettes permanent

> Filer i genbrugsbinen, der er ældre end det valgte antal dage, vil blive ryddet automatisk. {.is-warning}

## Tilladelser

- Indstil tilladelser - Skal `chmod` køres, når filer importeres/omdøbes?
  - chmod-mappe - Oktal, der anvendes under import/omdøbning til mediemapper og filer (uden udførelsesbit)

> Rullemenuen har en forudindstillet liste over meget almindeligt anvendte tilladelser, der kan bruges. Du kan dog manuelt indtaste en oktal mappe, hvis du ønsker det. {.is-info}

> Dette virker kun, hvis brugeren, der kører `Sonarr`, er ejeren af filen. Det er bedre at sikre, at downloadklienten indstiller tilladelserne korrekt. {.is-warning}

- chown-gruppe - Gruppenavn eller GID. Brug GID til fjernfiler.

> Dette virker kun, hvis brugeren, der kører `Sonarr`, er ejeren af filen. Det er bedre at sikre, at downloadklienten indstiller tilladelserne korrekt. {.is-warning}

## Rodmapper

- Sti - Dette viser stien til dit mediebibliotek
- Ledig plads - Dette er den ledige plads, der rapporteres til Sonarr fra systemet
- Umapperede mapper - Dette er mapper, der ikke har en tilknyttet serie

> `X` i slutningen vil fjerne denne rodmappe. {.is-info}

- Tilføj rodmappe - Dette giver dig mulighed for at vælge en rodmappe til et sted at enten placere nye importeret downloads i denne mappe eller tillade Sonarr at scanne eksisterende medier.

> Brugere af ikke-Windows:
> \* Hvis du bruger et NFS-mount, skal du sikre dig, at `nolock` er aktiveret.
> \* Hvis du bruger et SMB-mount, skal du sikre dig, at `nobrl` er aktiveret. {.is-warning}

# Profiler

## Kvalitetsprofiler

- Indstil profiler for kvaliteten af de serier, du ønsker at downloade.

> Når du vælger en eksisterende profil eller tilføjer en ekstra profil, vises et nyt vindue. {.is-info}

> Bemærk: Kvaliteten, der har en blå boks, er kvaliteten, som alt med denne profil fortsat vil blive opgraderet til. {.is-info}

- Navn - Vælg et **UNIKT** navn til den kvalitetsprofil, du opretter
- Opgraderinger tilladt - Når denne indstilling er markeret, og du beder Sonarr om at downloade en `WEB 1080p`, da det er den første udgivelse af en bestemt episode, og senere er nogen i stand til at uploade en `Bluray-1080p`, vil Sonarr automatisk opgradere til den bedre kvalitet ***hvis*** `Opgrader indtil` har den kvalitet valgt
- Opgrader indtil - Når denne kvalitet er nået, vil Sonarr ikke længere downloade episoder

> Bemærk: Dette gælder kun, hvis du har `Bluray-1080p` højere end `WEB 1080p` inden for afsnittet `Kvaliteter` {.is-warning}

- Kvaliteter - Kvaliteter højere på listen foretrækkes mere, selvom de ikke er markeret. Kvaliteter inden for samme gruppe er lige. Kun markerede kvaliteter ønskes.
- Rediger grupper - Nogle kvaliteter er grupperet sammen for at reducere størrelsen på listen samt gruppere lignende udgivelser. Et godt eksempel på dette er `WebDL` og `WebRip`, da disse er meget ens og typisk har lignende bitrater. Når du redigerer grupperne, kan du ændre præference inden for hver af grupperne. [Se TRaSh's guide til, hvordan man fusionerer kvaliteter](https://trash-guides.info/merge-quality)
  - [Se kvaliteter](#qualities-defined)

> Som standard er kvaliteterne indstillet fra laveste (nederst) til højeste (øverst) {.is-info}

## Sprogprofiler

- Indstil profiler for sproget i de serier, du ønsker at downloade.

> Bemærk, at prioriteringen/rækkefølgen betyder noget, selvom sproget ikke ønskes (valgt). {.is-info}

- Navn - Vælg et **UNIKT** navn til den sprogprofil, du opretter
- Opgraderinger tilladt - Hvis ikke markeret (deaktiveret), vil sprog ikke blive opgraderet. Hvis du f.eks. beder Sonarr om at downloade en kinesisk version, da det er den første udgivelse af en bestemt serie, og senere er nogen i stand til at uploade en engelsk version, så vil Sonarr automatisk opgradere til den bedre kvalitet

> Dette er kun gyldigt, hvis engelsk er højere på sproglisten end kinesisk, og begge er valgt {.is-warning}

- Sprog - Sprog højere på listen foretrækkes mere. Kun markerede sprog ønskes

## Forsinkelsesprofiler

- Forsinkelsesprofiler giver dig mulighed for at reducere antallet af udgivelser, der downloades til en episode ved at tilføje en forsinkelse, mens Sonarr fortsætter med at overvåge udgivelser, der bedre matcher dine præferencer.
- Foretrukket protokol - Dette vil enten være `Usenet` eller `Torrent` afhængigt af, hvilken downloadprotokol du foretrækker
- Usenet-forsinkelse - Indstil antallet af minutter, du vil vente, før downloaden starter
- Torrent-forsinkelse - Indstil antallet af minutter, du vil vente, før downloaden starter
- Bypass, hvis højeste kvalitet - Bypass forsinkelse, når udgivelsen har den højeste aktiverede kvalitetsprofil med den foretrukne protokol
- Tags - Ved at give denne forsinkelsesprofil en tag kan du tagge en given serie til at følge reglerne, der er angivet her.
- Skruenøgleikon - Dette giver dig mulighed for at redigere forsinkelsesprofilen
- Plusikon (<kb>+</kb>) - Opret en ny forsinkelsesprofil

### Anvendelser

Nogle medier vil modtage et halvt dusin forskellige udgivelser af varierende kvalitet i timerne efter en udgivelse, og uden forsinkelsesprofiler kan Sonarr forsøge at downloade dem alle. Med forsinkelsesprofiler kan Sonarr konfigureres til at ignorere de første par timer med udgivelser.

Forsinkelsesprofiler er også nyttige, hvis du vil lægge vægt på en protokol (Usenet eller BitTorrent) over den anden. (Se [Eksempel 3](/sonarr/settings/#example-3))

### Sådan fungerer forsinkelsesprofiler

Timeren starter, så snart Sonarr registrerer, at en episode har en tilgængelig udgivelse. Denne udgivelse vises i din kø med et urikon for at angive, at den er under forsinkelse.

> Timeren starter fra tidspunktet for upload af udgivelsen og ikke fra det tidspunkt, Sonarr ser den. {.is-info}

I løbet af forsinkelsesperioden vil Sonarr bemærke eventuelle nye udgivelser, der bliver tilgængelige. Når forsinkelsestimeren udløber, vil Sonarr downloade den ene udgivelse, der bedst matcher dine kvalitetspræferencer.

Tidsperioden kan være forskellig for Usenet og Torrents. Hver profil kan være forbundet med en eller flere tags for at give dig mulighed for at tilpasse, hvilke shows der har hvilke profiler. En forsinkelsesprofil uden tag betragtes som standard og gælder for alle shows, der ikke har et specifikt tag.

> Forsinkelsesprofiler starter fra tidspunktet, hvor indekseren rapporterer, at udgivelsen blev uploadet. Dette betyder, at indhold, der er ældre end det antal minutter, du har indstillet, ikke påvirkes på nogen måde af din forsinkelsesprofil og vil blive downloadet øjeblikkeligt. Derudover vil **eventuelle manuelle søgninger** efter indhold (søgninger uden for RSS-feed) ignorere indstillingerne for forsinkelsesprofil. {.is-warning}

#### Eksempler

- For hvert eksempel skal du antage, at brugeren har følgende kvalitetsprofil aktiveret: HDTV 720p og derover er tilladt, WebDL 720p er kvalitetsgrænsen, WebDL 1080p er den højest rangerede kvalitet.

##### Eksempel 1

- I dette simple eksempel er profilen indstillet med en 120 minutters (to timers) forsinkelse for både Usenet og Torrent.

- Kl. 23:00 opdager Sonarr den første udgivelse af en episode, der blev uploadet kl. 22:50, og den 120 minutters timer begynder. Kl. 00:50 vil Sonarr evaluere eventuelle udgivelser, den har fundet i de sidste to timer, og downloade den bedste, som er WebDL 720p.

- Kl. 03:00 findes en anden udgivelse, som er WebDL 720p, der blev tilføjet til din indekser kl. 02:46. En anden 120 minutters timer begynder. Kl. 04:46 downloades den bedst tilgængelige udgivelse. Da kvalitetsgrænsen nu er nået, kan episoden ikke længere opgraderes, og Sonarr vil stoppe med at lede efter nye udgivelser.

- På et hvilket som helst tidspunkt, hvis der findes en WebDL 1080p-udgivelse, vil den blive downloadet øjeblikkeligt, fordi det er den højest rangerede kvalitet. Hvis der er en aktiv forsinkelsestimer, vil den blive annulleret.

##### Eksempel 2

- Dette eksempel har forskellige timere for Usenet og Torrents. Antag en 120 minutters timer for Usenet og en 180 minutters timer for BitTorrent.

- Kl. 23:00 opdages den første udgivelse af en episode af Sonarr, og begge timere starter. Udgivelsen blev tilføjet til indekseren kl. 22:15. Kl. 00:15 vil Sonarr evaluere eventuelle udgivelser, og hvis der er nogen acceptable Usenet-udgivelser, vil den bedste blive downloadet, og begge timere vil slutte. Hvis ikke, vil Sonarr vente indtil kl. 00:15 og downloade den bedste udgivelse, uanset hvilken kilde den kommer fra.

##### Eksempel 3

- En almindelig brug af forsinkelsesprofiler er at lægge vægt på en protokol over den anden. For eksempel vil du kun downloade en BitTorrent-udgivelse, hvis der ikke er blevet uploadet noget til Usenet efter et bestemt tidsrum.

- Du kan indstille en 60 minutters timer for BitTorrent og en 0 minutters timer for Usenet.

- Hvis den første udgivelse, der registreres, er fra Usenet, vil Sonarr downloade den øjeblikkeligt.

- Hvis den første udgivelse er fra BitTorrent, vil Sonarr indstille en 60 minutters timer. Hvis der i løbet af den timer findes en kvalificeret Usenet-udgivelse, vil BitTorrent-udgivelsen blive ignoreret, og Usenet-udgivelsen vil blive hentet.

## Udgivelsesprofiler

- Ikke alle udgivelser er ens, hver udgivelsesgruppe har deres egen måde at pakke og kode deres materiale på. Her kan du vælge de foretrukne udgivelser, du leder efter.

> Du kan bruge regex (standard tilfælde-sensitiv) i værdierne "Skal indeholde", "Må ikke indeholde" og "Foretrukne" ord. Regex skal være som `/regex-her/i` {.is-info}

- Navn - Vælg et **UNIKT** navn til udgivelsesprofilen, du opretter
- Aktivér profil - Aktiver eller deaktiver denne profil
- Skal indeholde - Udgivelsen skal indeholde mindst et af disse termer (ikke sprogfølsomt)
- Må ikke indeholde - Udgivelsen vil blive afvist, hvis den indeholder et eller flere af termerne (ikke sprogfølsomt)
- Foretrukne - Her kan du vælge et givent ord og give det en score.
  - Lad os sige, at du leder efter udgivelser med en bestemt gruppe af ord. Lad os sige, at du vil fortælle Sonarr, at du vil have Repacks eller Propers frem for almindelige udgivelser. Her skal du indsætte ordet Repack i en af felterne og give det en værdi (sige 100), men du leder også efter DTS-HD-lyd, så du skal indsætte det og også give det en score (sige 100 igen). Når Sonarr går igennem og ser på alle udgivelserne fra RSS-feedet, og den støder på en udgivelse, der har både Repack og DTS-HD, vil det give en score på 200. Det er meget højere end alle de andre, der ikke har nogen af disse ord. Dette fortæller Sonarr, at dette har en højere score, og det vil være den første fil, der vælges til download.
- Inkluder foretrukne ved omdøbning - Når du bruger {Foretrukne ord} tagget i navngivningsskemaet
- Indekser - Angiv, hvilken indekser profilen gælder for.

> Dette er nyttigt, hvis du kun vil have specifikke udgivelser fra en given indekser/tracker. {.is-info}

- Tags - Ved at give denne udgivelsesprofil en tag kan du tagge en given serie til at følge reglerne, der er angivet her. Hvis du lader dette felt være tomt, gælder disse regler for alle serier

- [TRaSH vedligeholder en liste over WEB-DL-udgivelsesprofiler](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/)
- [TRaSH Anime-profiler](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx-Anime/)

# Kvalitet

## Betydning af kvalitetstabellen

- Kvalitet - Navnet på kvaliteten i scenen (hardcodet)
- Titel - Navnet på kvaliteten i GUI'en (konfigurerbar)
- Megabyte per time - Selvforklarende
- Størrelsesbegrænsning - Selvforklarende
- Min - Minimum antal megabyte per minut (MB/min), en kvalitet kan have.
- Maks - Maksimum antal megabyte per minut (MB/min), en kvalitet kan have.

## Definerede kvaliteter

- Ukendt - Selvforklarende
- SDTV - Efter luftoptagelser fra en analog kilde (normalt kabel-tv eller OTA-standarddefinition). Billedkvaliteten er generelt god (til opløsningen), og de er normalt kodet i DivX/XviD eller MP4.
- WEBDL-480p - WEB-DL (P2P) henviser til en fil, der er ripset tabløst fra en streamingtjeneste som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer osv. eller downloadet via en online distributionswebsite som iTunes. Kvaliteten er ret god, da de ikke er kodet igen. Video (H.264 eller H.265) og lyd (AC3/AAC) streams er normalt udtrukket fra iTunes eller Amazon Video og remuxed ind i en MKV-container uden at gå på kompromis med kvaliteten. En fordel ved disse udgivelser er, at de normalt ikke har netværkslogoer på skærmen. Disse er næsten lige så gode som en Blu-ray-kilde, men kan lide af lydforsinkelse eller visuelle artefakter fra streamingtjenesternes adaptive bitrate. Hvis en ripper mister sin internetforbindelse til et punkt, hvor bitraten falder, kan kildens bitrate ændre sig dynamisk, hvilket medfører variationer i billedkvaliteten. De fleste udgivelser, der lider af en ekstrem mængde visuelle artefakter, er NUKED, og der udgives normalt en PROPER for at rette eventuelle vilde variationer i adaptiv bitrate. Dette vil være i 480p (SD) kvalitet.
- WEBRip-480p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 480p (SD) kvalitet.
- DVD - En genkodning af den endelige udgivne DVD9. Hvis det er muligt, bliver dette udgivet PRE detail. Det bør være fremragende kvalitet (til opløsningen). DVDrips udgives normalt i DivX/XviD eller MP4.
- Bluray-480p - En genkodning af den endelige udgivne Blu-ray, nedskaleret til 480p opløsning (720x480 @ 16:9, en anden billedformat kan have en anden opløsning). Hvis det er muligt, bliver dette udgivet PRE detail. Det bør være fremragende kvalitet til opløsningen. Bitrater kan variere, men de er generelt kodet til DivX, XviD eller AVC og tilbyder en lille opfattet kvalitetsreduktion i forhold til den originale kilde, samtidig med at filstørrelsen reduceres drastisk. Disse er normalt MKV eller MP4, men der er også nogle DivX/XviD i AVI-format.
- HDTV-720p - En genkodning af den endelige udgivne Blu-ray, men sendt over HD-kabel eller satellit (1280x720 @ 16:9, en anden billedformat kan have en anden opløsning). Det kan være ændret i forhold til køretid eller indhold afhængigt af det netværk, det kommer fra. Dette udgives normalt flere måneder efter en detailudgivelse, men nogle gange udgives opskalerede versioner af en standarddefinitionsfilm på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopier af den specifikke film, der er tilgængelige. Disse er normalt MKV eller MP4.
- HDTV-1080p - En genkodning af den endelige udgivne Blu-ray, men sendt over HD-kabel eller satellit (1920x1080 @ 16:9, en anden billedformat kan have en anden opløsning). Det kan være ændret i forhold til køretid eller indhold afhængigt af det netværk, det kommer fra. Dette udgives normalt flere måneder efter en detailudgivelse, men nogle gange udgives opskalerede versioner af en standarddefinitionsfilm på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopier af den specifikke film, der er tilgængelige. Disse er normalt MKV eller MP4-container.
- Raw-HD - En rå feed af en HD-stream.
- WEBRip-720p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 720p kvalitet.
- Bluray-720p - En genkodning af den endelige udgivne Blu-ray, nedskaleret til 720p opløsning (1280x720 @ 16:9, en anden billedformat kan have en anden opløsning). Hvis det er muligt, bliver dette udgivet PRE detail. Det bør være fremragende kvalitet til opløsningen. Bitrater kan variere, men de er generelt kodet til AVC eller HEVC og tilbyder en lille opfattet kvalitetsreduktion i forhold til den originale kilde, samtidig med at filstørrelsen reduceres drastisk. Disse er normalt MKV eller MP4-container.
- WEBDL-1080p - WEB-DL (P2P) henviser til en fil, der er ripset tabløst fra en streamingtjeneste som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer osv. eller downloadet via en online distributionswebsite som iTunes. Kvaliteten er ret god, da de ikke er kodet igen. Video (H.264 eller H.265) og lyd (AC3/AAC) streams er normalt udtrukket fra iTunes eller Amazon Video og remuxed ind i en MKV-container uden at gå på kompromis med kvaliteten. En fordel ved disse udgivelser er, at de normalt ikke har netværkslogoer på skærmen. Disse er næsten lige så gode som en Blu-ray-kilde, men kan lide af lydforsinkelse eller visuelle artefakter fra streamingtjenesternes adaptive bitrate. Hvis en ripper mister sin internetforbindelse til et punkt, hvor bitraten falder, kan kildens bitrate ændre sig dynamisk, hvilket medfører variationer i billedkvaliteten. De fleste udgivelser, der lider af en ekstrem mængde visuelle artefakter, er NUKED, og der udgives normalt en PROPER for at rette eventuelle vilde variationer i adaptiv bitrate. Dette vil være i 1080p kvalitet.
- WEBRip-1080p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 1080p kvalitet.
- Bluray-1080p - En genkodning af den endelige udgivne Blu-ray, i sin oprindelige 1080p opløsning (1920x1080 @ 16:9, en anden billedformat kan have en anden opløsning). Hvis det er muligt, bliver dette udgivet PRE detail. Det bør være fremragende kvalitet og samme opløsning som kilden. Bitrater kan variere, men de er generelt kodet til AVC eller HEVC og tilbyder en lille opfattet kvalitetsreduktion i forhold til den originale kilde, samtidig med at filstørrelsen reduceres lidt. Disse er normalt MKV eller MP4-container.
- Remux-1080p - En remux er en rip af en Blu-ray- eller HD DVD-skive til en anden containerformat eller blot fjernelse af skivens menuer og bonusmateriale, samtidig med at indholdet af dens lyd- og videostreams bevares (og de nuværende codecs bevares), hvilket garanterer den nøjagtige 1:1-filmkvalitet som på den originale skive. Dette er i 1080p kvalitet.
- HDTV-2160p - TVRip er en optagelseskilde fra et optagekort. HDTV står for optaget kilde fra HD-tv. Med en HDTV-kilde kan kvaliteten nogle gange endda overgå DVD. Film i dette format begynder at blive populære. Nogle reklamer og kommercielle bannere kan ses på nogle udgivelser under afspilning. Dette er i 2160p (4K) kvalitet.
- WEBDL-2160p - WEB-DL (P2P) henviser til en fil, der er ripset tabløst fra en streamingtjeneste som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer osv. eller downloadet via en online distributionswebsite som iTunes. Kvaliteten er ret god, da de ikke er kodet igen. Video (H.264 eller H.265) og lyd (AC3/AAC) streams er normalt udtrukket fra iTunes eller Amazon Video og remuxed ind i en MKV-container uden at gå på kompromis med kvaliteten. En fordel ved disse udgivelser er, at de normalt ikke har netværkslogoer på skærmen. Disse er næsten lige så gode som en Blu-ray-kilde, men kan lide af lydforsinkelse eller visuelle artefakter fra streamingtjenesternes adaptive bitrate. Hvis en ripper mister sin internetforbindelse til et punkt, hvor bitraten falder, kan kildens bitrate ændre sig dynamisk, hvilket medfører variationer i billedkvaliteten. De fleste udgivelser, der lider af en ekstrem mængde visuelle artefakter, er NUKED, og der udgives normalt en PROPER for at rette eventuelle vilde variationer i adaptiv bitrate. Dette vil være i 2160p (4K) kvalitet.
- WEBRip-2160p - I en WEB-Rip (P2P) bliver filen ofte udtrukket ved hjælp af HLS- eller RTMP/E-protokoller og remuxed fra en TS-, MP4- eller FLV-container til MKV. Dette vil være i 2160p (4k) kvalitet.
- Bluray-2160p - En genkodning af den endelige udgivne Blu-ray, i sin oprindelige 2160p opløsning (3840x2160 @ 16:9, en anden billedformat kan have en anden opløsning). 4K-versioner af film, der udgives, er generelt i HEVC-kodeformat og kan være enten 8-bit eller 10-bit farvegengivelse eller fra en HDR-kilde. Disse er normalt MKV eller MP4-container.
- Remux-2160p - En remux er en rip af en Blu-ray- eller HD DVD-skive til en anden containerformat eller blot fjernelse af skivens menuer og bonusmateriale, samtidig med at indholdet af dens lyd- og videostreams bevares (og de nuværende codecs bevares), hvilket garanterer den nøjagtige 1:1-filmkvalitet som på den originale skive. Dette er i 2160p (4K) kvalitet.

# Indexere

> Information om understøttede indexere kan findes på siden [Mere info (Understøttet)](/sonarr/supported#indexers) for dette afsnit
{.is-info}

## Understøttede indexere

- En liste over understøttede indexere findes på siden [Mere info (Understøttet)](/sonarr/supported#indexers)

### Indstillinger for indexere

- Når du har klikket på <kb>+</kb>-knappen for at tilføje en ny indexer, vises et nyt vindue med mange forskellige indstillinger. I denne wiki betragter Sonarr både Usenet Indexers og Torrent Trackers som "Indexere".

- Der er to sektioner her: Usenet og Torrents. Afhængigt af hvilken downloadklient du vil bruge, skal du vælge den type indexer, du vil bruge.

### Konfiguration af Usenet Indexer

- Newznab - Her finder du forudindstillinger for populære Usenet indexere (som er udfyldt, alt hvad du behøver er din API-nøgle, som leveres af Usenet indexer efter eget valg) samt muligheden for at oprette en brugerdefineret indexer.
- Software, der fungerer med Usenet og integrerer godt med Sonarr, er [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr), der integrerer både Usenet og Torrents.
- Uanset om du vælger en forudindstillet indexer eller en brugerdefineret indexeropsætning, vises et nyt vindue, hvor du kan indtaste alle dine indstillinger.
- Vælg mellem forudindstillingerne eller tilføj en brugerdefineret indexer (som f.eks. NZBHydra2 eller Prowlarr).
- Navn - Navnet på indexer i Sonarr.
- Aktivér RSS - Hvis det er aktiveret, brug denne indexer til at overvåge filer, der ønskes og mangler eller endnu ikke har nået deres cutoff.
- Aktivér automatisk søgning - Hvis det er aktiveret, brug denne indexer til automatisk søgning, herunder søgning ved tilføjelse.
- Aktivér interaktiv søgning - Hvis det er aktiveret, brug denne indexer til manuelle interaktive søgninger.
- URL - URL'en til indexer, som indexereren leverer, f.eks. `https://api.nzbgeek.info`.
- API-sti - Stien til API'en, som indexereren leverer. Dette er normalt `/api`.
- API-nøgle - Nøglen, som indexereren leverer, for at få adgang til API'en.
- Kategorier - Standardkategorierne bruges, medmindre de redigeres. Det er sandsynligt, at disse standardkategorier ikke er optimale. Når denne indstilling redigeres, forespørger Sonarr indexereren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standardindstillinger ryddes, så snart en kategori skiftes.
- Animekategorier - Kategorierne, som Sonarr vil bruge til anime-søgninger. Der bruges ingen kategorier, medmindre de redigeres. Når denne indstilling redigeres, forespørger Sonarr indexereren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standardindstillinger ryddes, så snart en kategori skiftes.
- Søgning efter standardformat for anime - Søg også efter anime ved hjælp af standardnummereringen (gælder kun for anime-serietyper) [Mere information om serietyper her](/sonarr/faq#whats-the-different-series-types)
- (Avanceret indstilling) Yderligere parametre - Yderligere Newznab-parametre, der skal tilføjes til forespørgselslinket
- (Avanceret indstilling) Indexer-prioritet - Prioritet for denne indexer for at foretrække en indexer frem for en anden i scenarier med release-afgørelse. 1 er højeste prioritet, og 50 er laveste prioritet.
- (Avanceret indstilling) Downloadklient - Vælg og specificer, hvilken downloadklient der bruges til hentninger fra denne indexer.
- Tags - Brug kun denne indexer til serier med mindst en matchende tag. Lad være blank for at bruge med alle serier.

### Konfiguration af Torrent Tracker

- Som med Usenet er der en række forudfyldte oplysninger om Torrent-trackere. Hvis du ikke er medlem af nogen af disse specifikke trackere, vil de ikke være til nogen nytte for dig.
- En af de bedste og enkleste måder at bruge Torrent-trackere, der ikke naturligt understøttes af Sonarr, er at bruge et andet program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Disse software fungerer godt sammen med Sonarr som en søgeindexer, der indeholder al din information og sender den til Sonarr.
- Torznab - Denne mulighed vil indstille dig med en Jackett-forudindstilling, hvis du bruger flere trackere, skal du have hver post have et unikt navn.
- Torznab Indexer
- Vælg mellem forudindstillingerne eller tilføj en brugerdefineret indexer (som f.eks. Jackett eller Prowlarr).
- Navn - Navnet på indexer i Sonarr.
- Aktivér RSS - Hvis det er aktiveret, brug denne indexer til at overvåge filer, der ønskes og mangler eller endnu ikke har nået deres cutoff.
- Aktivér automatisk søgning - Hvis det er aktiveret, brug denne indexer til automatisk søgning, herunder søgning ved tilføjelse.
- Aktivér interaktiv søgning - Hvis det er aktiveret, brug denne indexer til manuelle interaktive søgninger.
- URL - URL'en, som indexereren leverer, f.eks. `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sti - Stien til API'en, som indexereren leverer. Dette er normalt `/api`.
- API-nøgle - Nøglen, som indexereren leverer, for at få adgang til API'en.
- Kategorier - Standardkategorierne bruges, medmindre de redigeres. Det er sandsynligt, at disse standardkategorier ikke er optimale. Når denne indstilling redigeres, forespørger Sonarr indexereren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standardindstillinger ryddes, så snart en kategori skiftes.
- Animekategorier - Kategorierne, som Sonarr vil bruge til anime-søgninger. Der bruges ingen kategorier, medmindre de redigeres. Når denne indstilling redigeres, forespørger Sonarr indexereren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standardindstillinger ryddes, så snart en kategori skiftes.
- Søgning efter standardformat for anime - Søg også efter anime ved hjælp af standardnummereringen (gælder kun for anime-serietyper) [Mere information om serietyper her](/sonarr/faq#whats-the-different-series-types)
- (Avanceret indstilling) Yderligere parametre - Yderligere Torznab-parametre, der skal tilføjes til forespørgselslinket
- (Avanceret indstilling) Minimum Seeders - Det mindste antal seedere, der kræves for, at en udgivelse fra denne tracker skal hentes.
- (Avanceret indstilling) Seed Ratio - Hvis det er tomt, brug standardindstillingen for downloadklienten. Ellers er det mindste seedforhold, der kræves for, at din downloadklient skal opfylde for udgivelser fra denne indexer, før den sættes på pause af din klient og fjernes af Sonarr (Kræver afsluttet downloadhåndtering - Fjern aktiveret)
- (Avanceret indstilling) Seed Time - Hvis det er tomt, brug standardindstillingen for downloadklienten. Ellers er det mindste seedtid i minutter, der kræves for, at din downloadklient skal opfylde for udgivelser fra denne indexer, før den sættes på pause af din klient og fjernes af Sonarr (Kræver afsluttet downloadhåndtering - Fjern aktiveret)
- (Avanceret indstilling) Indexer-prioritet - Prioritet for denne indexer for at foretrække en indexer frem for en anden i scenarier med release-afgørelse. 1 er højeste prioritet, og 50 er laveste prioritet.
- (Avanceret indstilling) Downloadklient - Vælg og specificer, hvilken downloadklient der bruges til hentninger fra denne indexer.
- Tags - Brug kun denne indexer til serier med mindst en matchende tag. Lad være blank for at bruge med alle serier.

## Indstillinger

- Minimumsalder - Kun Usenet: Minimumsalder i minutter for NZB'er, før de hentes. Brug dette til at give nye udgivelser tid til at sprede sig til din Usenet-udbyder.
- Bevaring - Kun Usenet: Indstil til nul for at indstille til ubegrænset bevaring
- Maksimal størrelse - Maksimal størrelse for en udgivelse, der skal hentes i MB. Indstil til nul for at indstille til ubegrænset. Bemærk venligst, at dette gælder globalt.
- RSS-synkroniseringsinterval - Interval i minutter. Indstil til nul for at deaktivere (dette stopper alle automatiske udgivelseshentninger) Minimum: 10 minutter Maksimum: 120 minutter
  - Se venligst [Hvordan finder Sonarr episoder?](/sonarr/faq#how-does-sonarr-find-episodes) for en bedre forståelse af, hvordan RSS-synkronisering vil hjælpe dig

> Hvis Sonarr har været offline i en længere periode, vil Sonarr forsøge at bladre tilbage for at finde den sidste udgivelse, den behandlede, i et forsøg på at undgå at gå glip af en udgivelse. Så længe din indexer understøtter sideinddeling, og det ikke har været for længe, vil Sonarr være i stand til at behandle de udgivelser, den ville have gået glip af, og undgå at du skal udføre en søgning efter de manglende udgivelser.{.is-info}

# Downloadklienter

> Information om understøttede downloadklienter kan findes på siden [Mere info (Understøttet)](/sonarr/supported#download-clients) for dette afsnit
{.is-info}

## Oversigt

- Download og import er, hvor de fleste mennesker oplever problemer. Set fra et overordnet perspektiv skal softwaren kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Dette betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alles opsætning kan være lidt anderledes. Men der er mange forkerte opsætninger.

## Processer for downloadklienter

## Usenet

- Sonarr vil sende en downloadanmodning til din klient og associere den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Sonarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er færdig, vil Sonarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe og tilgængelig for Sonarr.
- Sonarr vil scanne den færdige filplacering for filer, som Sonarr kan bruge. Den vil analysere filnavnet for at matche det med den ønskede medie. Hvis det kan gøre det, vil den omdøbe filen i henhold til dine specifikationer og flytte den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringerne skal være de samme for din færdige downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Sonarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er IO-intensivt.
- Hvis indstillingen "Behandling af færdige downloads - Fjern" er aktiveret i Sonarrs indstillinger, vil resterende filer fra downloaden blive sendt til papirkurven eller genbrug via en anmodning til din klient om at slette/fjerne udgivelsen.

## BitTorrent

- Sonarr vil sende en downloadanmodning til din klient og associere den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Sonarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Færdige filer efterlades på deres oprindelige placering for at tillade seeding af filen (forhold eller tid kan justeres i downloadklienten eller fra Sonarr under den specifikke downloadklient). Når filerne importeres til din mediemappe, vil Sonarr oprette en hardlink til filen, hvis det understøttes af din opsætning, eller kopiere den, hvis hardlinks ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din færdige downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Sonarr falde tilbage og kopiere filen.
- Hvis indstillingen "Behandling af færdige downloads - Fjern" er aktiveret i Sonarrs indstillinger, vil Sonarr slette torrenten fra din klient og bede klienten om at fjerne torrentdataene, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet (pauser ved fuldførelse).

## Downloadklienter

Klik på `Indstillinger` => `Downloadklienter` og klik derefter på <kb>+</kb> for at tilføje en ny downloadklient. Din downloadklient skal allerede være konfigureret og kørende.

### Understøttede downloadklienter

- En liste over understøttede downloadklienter findes på siden [Flere oplysninger (Understøttet)](/sonarr/supported#download-clients)

Vælg den downloadklient, du ønsker at tilføje, og der vil være en pop op-boks til at indtaste forbindelsesoplysninger. Disse oplysninger er ens for de fleste klienter. Nogle vil bede om et brugernavn eller adgangskode, nogle vil spørge, om der skal tilføjes nye downloads i en pause/start-tilstand osv.

### Indstillinger for Usenet-klient

- Navn - Navnet på downloadklienten i Sonarr
- Aktiver - Aktiver denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient; dette er normalt webgui-porten
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- API-nøgle - API-nøglen til at godkende over for din klient
- Brugernavn - Brugernavnet til at godkende over for din klient (normalt ikke nødvendigt)
- Adgangskode - Adgangskoden til at godkende over for din klient (normalt ikke nødvendigt)
- Kategori - Kategorien i din downloadklient, som \*Arr vil bruge. For at undgå irrelevante downloads i aktiviteten anbefales det stærkt at angive en kategori.
- Nylig prioritet - downloadklientprioritet for nyligt udgivet medie
- Ældre prioritet - downloadklientprioritet for medie, der ikke er udgivet for nylig
- (Avanceret indstilling) Klientprioritet - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet
- Behandling af færdige downloads
  - Fjern (Per klientindstilling) - Fjern færdige downloads, når de er færdige (usenet) eller stoppet/fuldført (torrents). Se [Behandling af færdige downloads for flere detaljer](#completed-download-handling)

### Indstillinger for torrentklient

- Navn - Navnet på downloadklienten i Sonarr
- Aktiver - Aktiver denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- Brugernavn - Brugernavnet til at godkende over for din klient
- Adgangskode - Adgangskoden til at godkende over for din klient
- Kategori - Kategorien i din downloadklient, som \*Arr vil bruge. For at undgå irrelevante downloads i aktiviteten anbefales det stærkt at angive en kategori.
- Kategori efter import - Kategorien, der skal angives efter at udgivelsen er downloadet og importeret. Bemærk, at dette bryder fjernelse af behandling af færdige downloads.
- Nylig prioritet - downloadklientprioritet for nyligt udgivet medie
- Ældre prioritet - downloadklientprioritet for medie, der ikke er udgivet for nylig
- Starttilstand - Starttilstand for torrents (kun Qbittorrent: Tvungen omgår alle seed-tærskler)
- (Avanceret indstilling) Klientprioritet - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet
- Behandling af færdige downloads
  - Fjern (Per klientindstilling) - Fjern færdige downloads, når de er færdige (usenet) eller stoppet/fuldført (torrents). Se [Behandling af færdige downloads for flere detaljer](#completed-download-handling)
    - For torrents kræver dette, at din downloadklient sættes på pause, når seed-målene nås. Det kræver også, at seed-målene understøttes af Sonarr i henhold til nedenstående tabel. Torrents skal også forblive i samme kategori.

### Kompatibilitet for fjernelse af download i torrentklient

- Sonarr kan kun indstille seed-forhold/tid på klienter, der understøtter indstillingen af denne værdi via deres API, når torrenten tilføjes. Seed-mål kan indstilles globalt i klienten selv eller pr. tracker i \*Arr-indstillingerne for hver indexer. Se tabellen nedenfor for klientkompatibilitet.

|      Klient       |                                Forhold                                |                                  Tid                                   |
| :---------------: | :------------------------------------------------------------------: | :--------------------------------------------------------------------: |
|       Aria2       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|      Deluge       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
| Download Station  | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|       Flood       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|     Hadouken      | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|    qBittorrent    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|     rTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
| Torrent Blackhole | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|   Transmission    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Understøttet-Idle%20Limit*-blue) |
|     uTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|       Vuze        |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Understøttet-Idle%20Limit*-blue) - Transmission har internt en kontrol af inaktiv tid, men Sonarr sammenligner den med seedningstiden, hvis inaktivitetsgrænsen er indstillet på en per-torrent-basis. Dette gøres som en løsning på Transmission's API-begrænsninger.{.is-info}

## Behandling af færdige downloads

- Behandling af færdige downloads er, hvordan Sonarr importerer medier fra din downloadklient til dine seriemapper. Mange almindelige problemer er relateret til dårlige Docker-stier og/eller andre Docker-tilladelsesproblemer.

- (Avanceret global indstilling) Aktiver - Importer automatisk færdige downloads fra downloadklienten
- (Per klientindstilling) Fjern - Fjern færdige downloads, når de er færdige (usenet) eller stoppet/fuldført (torrents)
  - For torrents kræver dette, at din downloadklient sættes på pause, når seed-målene nås. Det kræver også, at seed-målene understøttes af Sonarr i henhold til tabellen ovenfor. Torrents skal også forblive i samme kategori.

### Fjern færdige downloads

- Sonarr vil sende en downloadanmodning til din klient og associere den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
- Sonarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er færdig, vil Sonarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe.
- Sonarr vil scanne den færdige filplacering for videofiler. Den vil analysere videofilens navn for at matche den med en episode. Hvis det kan gøre det, vil den omdøbe filen i henhold til dine specifikationer og flytte den til den angivne biblioteksmappe.
- Resterende filer fra downloaden sendes til papirkurven eller genbrug.

Hvis du downloader ved hjælp af en BitTorrent-klient, er processen lidt anderledes:

- Færdige filer efterlades på deres oprindelige placering for at tillade seeding. Når filer importeres til din angivne biblioteksmappe, vil Sonarr forsøge at oprette en hardlink til filen eller falde tilbage til at kopiere (bruge dobbelt plads), hvis hardlinks ikke understøttes.
- Hvis indstillingen "Behandling af færdige downloads - Fjern" er aktiveret i indstillingerne, vil Sonarr bede torrentklienten om at slette den oprindelige fil og torrent, men dette sker kun, hvis klienten rapporterer, at seeding er fuldført, torrenten er i samme kategori (dvs. ikke bruger en kategori efter import), seed-målet er nået og torrenten er sat på pause (stoppet).

### Håndtering af mislykkede downloads

- Håndtering af mislykkede downloads er kun kompatibel med SABnzbd og NZBGet.
- Håndtering af mislykkede downloads gælder ikke for torrents, og der er ingen planer om at tilføje en sådan funktionalitet.

- Der er flere komponenter, der udgør processen for håndtering af mislykkede downloads:

- Kontroller downloader:
  - Kø - Kontroller din downloaders kø for adgangskodebeskyttede (krypterede) udgivelser, der er markeret som mislykket
  - Historik - Kontroller din downloaders historik for fejl (f.eks. ikke nok blokke til reparation eller fejl ved udpakning)
- Når Sonarr finder en mislykket download, begynder den at behandle dem og gør følgende:
  - Tilføjer en mislykket begivenhed til Sonarrs historik
  - Fjerner den mislykkede download fra downloadklienten for at frigøre plads og rydde downloaded filer (valgfrit)
  - Begynder at søge efter en erstatningsfil (valgfrit)
  - Blokeringsliste (tidligere 'Sortliste') tillader automatisk spring af nzbs, når de mislykkes. Dette betyder, at nzb aldrig vil blive downloadet automatisk af Sonarr igen (du kan stadig tvinge downloaden via en manuel søgning).
  - Der er 2 avancerede indstillinger (på siden 'Downloadklient' indstillinger), der styrer adfærden for mislykket download i Sonarr, i øjeblikket er de alle aktiveret som standard.

- Genhent - Kontroller, om Sonarr skal søge efter den samme fil efter en fejl
- (Avanceret indstilling) Fjern - Om downloaden automatisk skal fjernes fra downloadklienten, når fejlen opdages

## Fjernstyrede stibilleder

- Fjernstyrede stibilleder fungerer som en simpel søgning efter fjernstien og erstatning med lokal sti. Dette bruges primært til enten fusionerede lokale/fjernopstillinger ved hjælp af mergerfs eller lignende eller bruges, når applikationen og downloadklienten ikke er på samme server.
- Et fjernstibillede bruges, når din downloadklient rapporterer en sti for fuldførte data enten på en anden server eller på en måde, som \*Arr ikke adresserer den mappe.
- Generelt er et fjernstibillede kun nødvendigt, hvis din downloadklient kører på Linux, når \*Arr kører på Windows eller omvendt. Et fjernstibillede kan også være nødvendigt, hvis du blander Docker- og Native-klienter eller hvis du bruger en fjernserver.
- Et fjernstibillede er en DUM søgning/erstatning (hvor den finder den FJERNEDE værdi, erstatter den med den LOKALE værdi for den angivne vært).
- Hvis fejlmeddelelsen om en dårlig sti ikke indeholder den ERSTATTEDE værdi, fungerer stibilledet ikke, som du forventer. Den typiske løsning er at tilføje og fjerne stibilledet.
- [Se TRaSH's vejledning for yderligere oplysninger om fjernstibilleder](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og din downloadklient er Docker-containere, er det sjældent nødvendigt med et fjernstibillede. Det anbefales at [gennemgå Docker-guiden](/docker-guide) og/eller [følge TRaSH's vejledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlister

> Oplysninger om understøttede listetyper findes på siden [Flere oplysninger (Understøttet)](/sonarr/supported#lists) for denne sektion
{.is-info}

## Lister

- Importlister er en del af Sonarr, der giver dig mulighed for at følge en given listeskaber. Lad os sige, at du følger en bestemt listeskaber på Trakt/TMDb og virkelig kan lide deres ArrowVerse Collection-sektion og vil se alle shows på deres liste. Du kigger i din Sonarr og opdager, at du ikke har disse serier. I stedet for at søge én efter én og tilføje disse elementer og derefter søge dine indexere efter disse serier, kan du gøre alt dette på én gang med en liste. Listene kan indstilles til at importere alle serier på den kurators liste samt automatisk tildele en kvalitetsprofil, automatisk tilføje og automatisk overvåge den serie.

- FORSIGTIG: Hvis lister gøres forkert, vil de absolut ødelægge dit bibliotek med en masse skrald, som du ikke har til hensigt at se. Så sørg for at være sikker på, hvad du importerer, før du klikker på Gem. Dvs. se fysisk på listen, før du overhovedet går til Sonarr.

- Her kan du vælge knappen <kb>+</kb> for at åbne et nyt pop op-vindue
- Fra dette nye vindue præsenteres du for mange forskellige muligheder for at opsætte din liste fra mange forskellige listeleverandører. Som tidligere nævnt skal du være forsigtig med lister. Det anbefales kraftigt ikke at vælge knappen Søg ved tilføjelse, før du er helt sikker på, at listen, du vælger/opsætter, tilføjer de serier, du leder efter.
- Når du har valgt den listeleverandør, du ønsker at trække fra (såsom IMDb eller Trakt), får du præsenteret et nyt vindue.
De fleste indstillinger for lister er ret selvforklarende, nogle lister kræver, at du godkender dig hos udbyderen, f.eks. Trakt (hvilket kræver, at du har en konto hos Trakt.tv)

## Listeundtagelser

- Importer udelukkelse - Dette giver dig mulighed for at fjerne serier fra din liste, som du ikke ønsker at se igen. Et eksempel på dette er, hvis din liste tilfældigvis indeholder en serie på et fremmedsprog, og det er usandsynligt, at du nogensinde vil finde denne film på dit modersmål og ikke ønsker at se den med undertekster. Du kan udelukke en serie fra at blive tilføjet i fremtiden. Men i afsnittet for udelukkelse af liste kan du tilføje den tilbage til listen, så når listen kører igen, vil den blive læst til dit bibliotek.

# Forbindelse

> Information om understøttede forbindelsestyper kan findes på siden [Mere info (Understøttet)](/sonarr/supported#notifications) for dette afsnit
{.is-info}

## Forbindelser

- Forbindelser er måden, hvorpå du ønsker, at Sonarr skal kommunikere med omverdenen.

- Ved at trykke på <kb>+</kb>-knappen får du vist et nyt vindue, hvor du kan konfigurere mange forskellige slutpunkter.

- En liste over understøttede meddelelser og forbindelser findes på siden [Mere info (Understøttet)](/sonarr/supported#notifications)

## Forbindelsesudløsere

- Ved download - Få besked, når episoder er tilgængelige til download og er blevet sendt til en downloadklient.
- Ved import - {Tidligere kendt som Ved download} Få besked, når episoder er blevet importeret.
- Ved opgradering - Få besked, når episoder opgraderes til bedre kvalitet.
- Ved omdøbning - Få besked, når episoder omdøbes.
- Ved sletning af serie - Få besked, når serier slettes.
- Ved sletning af episodfiler - Få besked, når episodfiler slettes.
- Ved sletning af episodfiler til opgradering - Få besked, når episodfiler slettes til opgradering.
- Ved sundhedsproblem - Få besked ved fejl i sundhedstjek.
  - Inkluder sundhedsadvarsler - Få besked ved sundhedsadvarsler udover fejl.
- Ved programopdatering - Få besked, når Sonarr opdateres til en ny version.

# Metadata

## Metadata

> Information om understøttede metadataforbrugere kan findes på siden [Mere info (Understøttet)](/sonarr/supported#metadata) for dette afsnit
{.is-info}

- Her kan du vælge den type metadata, der skal bruges af din medieafspiller.

- Kodi vil være en af de mest almindeligt anvendte muligheder her, hvis det er den software, der bruges. Dette vil tillade Sonarr at oprette en NFO-fil samt tilknyttede filmpostere, der skal skrabes ind i din afspiller.

# Tags

- Tag-sektionen i Sonarr bruges til at linke forskellige aspekter af Sonarr.
- Tags er særligt nyttige til:
  - Forsinkelsesprofiler
  - Udgivelsesprofiler
  - Indekser
- Tags kan bruges til at linke forsinkelsesprofiler, udgivelsesprofiler, indekser og serier sammen.
- For eksempel:
  - Du vil kun have, at en bestemt indekser skal bruges til en bestemt serie. Du ville oprette en tag og tildele serien og indekseren den tag.
  - Du vil have, at en bestemt udgivelsesprofil kun skal bruge en bestemt forsinkelsesprofil. Du ville oprette en tag og tildele udgivelsesprofilen og forsinkelsesprofilen den tag.

> En serie vil bruge både indeksere, der har matchende tags, og indeksere, der ikke har tags.
{.is-warning}

> Bemærk: Tags påvirker ikke "Skal indeholde", "Må ikke indeholde", "Foretrukne" ord eller andre aspekter, der ikke er nævnt ovenfor.
{.is-info}

# Generelt

## Vært

- Bind-adresse - Gyldig IP4-adresse eller '*' for alle grænseflader
  - 0.0.0.0 eller `*` - enhver adresse kan oprette forbindelse
  - 127.0.0.1 eller localhost - kun lokalapplikationer kan oprette forbindelse
  - Enhver anden IP (f.eks. 1.2.3.4) - kun den IP (1.2.3.4) kan oprette forbindelse
- Portnummer - Portnummeret, du ønsker at bruge til at få adgang til webgrænsefladen for Sonarr

> Bemærk: Hvis du bruger Docker, skal du ikke ændre denne indstilling.
{.is-warning}

- URL-base - Til understøttelse af omvendt proxy, standard er tom

> Bemærk: Hvis du bruger en omvendt proxy (f.eks. mydomain.com/sonarr), skal du indtaste '/sonarr' for URL-base.
{.is-info}

- Instansnavn - Instansnavn i faneblad og til Syslog-appnavn

> Hvis du kører flere instanser, tilføjes instansnavnet til webbrowserens fanebladnavn. {.is-info}

- Aktivér SSL - Hvis du har SSL-legitimationsoplysninger, og du vil sikre kommunikationen til og fra din Sonarr, skal du aktivere denne indstilling.

> Bemærk: Brug ikke dette, medmindre du ved, hvad du laver.
{.is-warning}

## Sikkerhed

- Godkendelse - Hvordan vil du godkende adgang til din Sonarr-instans
  - Ingen - Du har ingen godkendelse for at få adgang til din Sonarr. Normalt hvis du er den eneste bruger af dit netværk, ikke har nogen på dit netværk, der vil have adgang til din Sonarr, eller din Sonarr ikke er eksponeret for internettet
  - Grundlæggende (Browser-pop-up) - Denne mulighed viser en lille pop-up, når du får adgang til din Sonarr, der giver dig mulighed for at indtaste et brugernavn og adgangskode
  - Formularer (Loginside) - Denne mulighed har en velkendt login-skærm, ligesom andre websteder, der giver dig mulighed for at logge på din Sonarr
- API-nøgle - Dette er, hvordan andre programmer vil kommunikere eller have Sonarr til at kommunikere med andre programmer. Hvis denne nøgle gives til den forkerte person med adgang, kan der ske alle mulige ting med dit bibliotek. Derfor er API-nøglen sløret i logfilerne.
- Certifikatvalidering - Ændrer, hvor streng validering af HTTPS-certifikater er
  - Aktiveret - Valider alle HTTPS-certifikater (anbefales)
  - Deaktiveret for lokale adresser - Valider alle HTTPS-certifikater undtagen dem på localhost og LAN
  - Deaktiveret - Valider ingen HTTPS-certifikater

## Proxy

- Proxy - Denne indstilling giver dig mulighed for at køre den information, din Sonarr henter og søger efter, gennem en proxy. Dette kan være nyttigt, hvis du befinder dig i et land, der ikke tillader download af torrentfiler.

- Brug proxy - Aktivér for at bruge en proxy
- Proxytype - Vælg din proxytype (HTTPS, Socks4 eller Socks5)
- Værtsnavn - Indtast dit proxy-værtsnavn (Udelad ikke http/https eller nogen anden protokol)
- Port - Indtast din proxy-port
- Brugernavn - Indtast dit proxy-brugernavn, hvis relevant
- Adgangskode - Indtast din proxy-adgangskode, hvis relevant
- Ignorerede adresser - Indtast en kommasepareret liste over adresser, der skal omgås proxyen
- Omgå proxy for lokale adresser - Markér afkrydsningsfeltet for at omgå proxyen for lokale adresser. Lokale anmodninger identificeres ved manglende punktum (.) i URI'en, f.eks. <http://webserver/> eller adgang til den lokale server, herunder <http://localhost>, <http://loopback> eller <http://127.0.0.1>. Når dette ikke er markeret, foretages alle internetanmodninger via proxyserveren.

## Logning

- Logniveau - Sandsynligvis et af de mest nyttige fejlfindingværktøjer
  - Info - Dette er den mest grundlæggende måde, hvorpå Sonarr indsamler information. Denne logfil indeholder fatal, fejl, advarsel og info-entréer.
  - Debug - Debug inkluderer al den information, som Info inkluderer, plus mere information, der kan være nyttig. Denne logfil indeholder fatal, fejl, advarsel, info og debug-entréer.
  - Trace - Den mest avancerede og detaljerede logning i Sonarr. Trace inkluderer al den information, der er indsamlet af Info og Debug og mere. Dette er den mest almindelige type log, der bliver bedt om ved fejlfinding på Discord eller Reddit. Hvis du har brug for hjælp, skal du vælge din log til Trace og gentage opgaven, der gav dig problemer, for at fange loggen. Denne logfil indeholder fatal, fejl, advarsel, info, debug og trace-entréer.

## Analyse

- Analyse - Send anonyme brugs- og fejlinformationer til Sonarrs servere (SkyHook). Dette inkluderer oplysninger om din browser, hvilke Sonarr WebUI-sider du bruger, fejlrapportering samt OS- og runtime-version. Vi vil bruge disse oplysninger til at prioritere funktioner og fejlrettelser.

## Opdateringer

- (Avanceret indstilling) Gren - Dette er grenen af Sonarr, du kører på.
  - [Se denne FAQ-indgang for mere information](/sonarr/faq#how-do-i-update-sonarr)
- Automatisk - Hent og installer opdateringer automatisk. Du vil stadig kunne installere fra System: Opdateringer. Bemærk: Windows-brugere opdateres altid automatisk.
- Mekanisme - Brug Sonarrs indbyggede opdateringsfunktion eller et script
  - Indbygget - Brug Sonarrs egen opdateringsfunktion
  - Script - Få Sonarr til at køre opdateringsscriptet
  - Docker - Opdater ikke Sonarr indefra Docker, træk i stedet et helt nyt billede med den nye opdatering
  - Apt - Indstillet af Debian/Ubuntu-pakken, når opdatering håndteres udelukkende via Apt
- Script - Synlig kun når Mekanisme er indstillet til Script - Sti til opdateringsscript
- Opdateringsproces - Sonarr vil downloade opdateringsfilen, verificere dens integritet, udpakke den til en midlertidig placering og kalde den valgte metode. Opdateringsprocessen køres under samme bruger, som Sonarr kører under, og den skal have tilladelser til at opdatere Sonarr-filerne samt stoppe/starte Sonarr.
- Indbygget - Den indbyggede metode vil tage en sikkerhedskopi af Sonarr-filer og -indstillinger, stoppe Sonarr, opdatere installationen og starte Sonarr igen. Hvis dit system ikke kan håndtere stop af Sonarr og vil forsøge at genstarte det automatisk, kan det være bedst at bruge et script i stedet. Hvis opdateringen mislykkes, vil den tidligere version af Sonarr blive genstartet.
- Script - Scriptet skal håndtere det samme som den indbyggede opdatering, hvis du skal håndtere stop og start af tjenester (upstart/launchd/etc), skal du gøre det her.

## Sikkerhedskopier

- Sikkerhedskopisektionen giver dig mulighed for at fortælle Sonarr, hvordan du vil håndtere sikkerhedskopier

- Mappe - Dette giver dig mulighed for at vælge placeringen for sikkerhedskopier. I Docker vil du være begrænset til, hvad du tillader, at containeren ser. Stier er relative til appdata-mappen; hvis det er nødvendigt, kan du angive en absolut sti til sikkerhedskopier uden for appdata-mappen.
- Interval - Hvor ofte vil du have, at Sonarr skal lave en sikkerhedskopi
- Opbevaring - Hvor længe vil du have, at Sonarr skal beholde hver sikkerhedskopi. Efter at der er lavet en ny sikkerhedskopi, vil den ældste sikkerhedskopi blive fjernet

# Brugergrænseflade

## Kalender

- Første ugedag - Her kan du vælge, hvad du mener, den første ugedag skal være.
- Ugekolonneoverskrift - Her kan du vælge overskriften for kolonnerne

## Datoer

- Kort datoformat - Hvordan vil du have, at Sonarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du have, at Sonarr skal vise datoer i langt format?
- Tidsformat - Vil du have et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du have, at Sonarr skal vise relative (i dag/i går/osv.) eller absolutte datoer?

## Stil

- Aktivér farveblind tilstand - Ændret stil for at tillade farveblinde brugere at skelne farvekodede oplysninger bedre