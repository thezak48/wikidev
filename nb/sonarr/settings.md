---
title: Sonarr-innstillinger
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, needs-love, innstillinger
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Menyalternativer](#menyalternativer)
- [Mediehåndtering](#mediehåndtering)
  - [Forslag til fellesskapsnavngivning](#forslag-til-fellesskapsnavngivning)
  - [Episodenavn](#episodenavn)
    - [Standard episodestruktur](#standard-episodestruktur)
    - [Serienavn](#serienavn)
    - [Serienummer](#serienummer)
    - [Sesonger](#sesonger)
    - [Episoder](#episoder)
    - [Sendedato](#sendedato)
    - [Episodetittel](#episodetittel)
    - [Kvalitet](#kvalitet)
    - [Medieinformasjon](#medieinformasjon)
    - [Annet](#annet)
    - [Original](#original)
  - [Struktur for daglige episoder](#struktur-for-daglige-episoder)
  - [Struktur for animeepisoder](#struktur-for-animeepisoder)
    - [Absolutt episodenummer](#absolutt-episodenummer)
  - [Struktur for seriemapper](#struktur-for-seriemapper)
    - [Serienavn](#serienavn-1)
    - [Serienummer](#serienummer-1)
  - [Struktur for sesongmapper](#struktur-for-sesongmapper)
    - [Sesonger](#sesonger-1)
  - [Struktur for spesialmapper](#struktur-for-spesialmapper)
    - [Spesialer](#spesialer)
  - [Stil for flere episoder](#stil-for-flere-episoder)
  - [Mapper](#mapper)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
  - [Tillatelser](#tillatelser)
  - [Rotmapper](#rotmapper)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Språkprofiler](#språkprofiler)
  - [Forsinkelsesprofiler](#forsinkelsesprofiler)
    - [Bruk](#bruk)
    - [Hvordan forsinkelsesprofiler fungerer](#hvordan-forsinkelsesprofiler-fungerer)
      - [Eksempler](#eksempler)
        - [Eksempel 1](#eksempel-1)
        - [Eksempel 2](#eksempel-2)
        - [Eksempel 3](#eksempel-3)
  - [Utgivelsesprofiler](#utgivelsesprofiler)
- [Kvalitet](#kvalitet-1)
  - [Betydning av kvalitetstabell](#betydning-av-kvalitetstabell)
  - [Definerte kvaliteter](#definerte-kvaliteter)
- [Indekser](#indekser)
  - [Støttede indekser](#støttede-indekser)
    - [Innstillinger for indekser](#innstillinger-for-indekser)
    - [Konfigurasjon av Usenet-indeks](#konfigurasjon-av-usenet-indeks)
    - [Konfigurasjon av torrent-sporer](#konfigurasjon-av-torrent-sporer)
  - [Alternativer](#alternativer)
- [Nedlastingsklienter](#nedlastingsklienter)
  - [Oversikt](#oversikt)
  - [Prosesser for nedlastingsklienter](#prosesser-for-nedlastingsklienter)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Nedlastingsklienter](#nedlastingsklienter-1)
    - [Støttede nedlastingsklienter](#støttede-nedlastingsklienter)
    - [Innstillinger for Usenet-klient](#innstillinger-for-usenet-klient)
    - [Innstillinger for torrentklient](#innstillinger-for-torrentklient)
    - [Kompatibilitet for fjerning av nedlastinger i torrentklient](#kompatibilitet-for-fjerning-av-nedlastinger-i-torrentklient)
  - [Håndtering av fullførte nedlastinger](#håndtering-av-fullførte-nedlastinger)
    - [Fjern fullførte nedlastinger](#fjern-fullførte-nedlastinger)
    - [Håndtering av mislykkede nedlastinger](#håndtering-av-mislykkede-nedlastinger)
  - [Fjernstiavbildinger](#fjernstiavbildinger)
- [Importlister](#importlister)
  - [Lister](#lister)
  - [Listeeksklusjoner](#listeeksklusjoner)
- [Koble til](#koble-til)
  - [Tilkoblinger](#tilkoblinger)
  - [Tilkoblingstriggere](#tilkoblingstriggere)
- [Metadata](#metadata)
  - [Metadata](#metadata-1)
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
  - [Datoer](#datoer)
  - [Stil](#stil)
  
Denne siden vil gå gjennom alle innstillingene som er tilgjengelige i Sonarr og hvordan de fungerer. Dette er ikke ment å være en omfattende "Hvordan sette opp Sonarr"-guide. Se i stedet [Hurtigstart](/sonarr/quick-start-guide)-siden.

# Menyalternativer

For å komme til innstillingssiden, velg Innstillinger fra venstremenyen. Følgende undermenyalternativer vil være tilgjengelige:

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

Merk også at for hver enkelt innstillingsside er det noen alternativer øverst i menyen:

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- Skjul/Vis avansert er viktig for alle elementer som er merket nedenfor som `(Avansert alternativ)`, ellers vil de ikke vises. Disse menyelementene vises i oransje på skjermbildene.

- Du må lagre endringene før du forlater skjermen. Dette gjør du ved å klikke på diskikonet. Hvis du ikke har gjort noen endringer, vil det stå "Ingen endringer" og være grått, som vist ovenfor.

# Mediehåndtering

> Noen av disse innstillingene er bare synlige ved å aktivere `Vis avanserte innstillinger`, som er øverst i verktøylinjen under søkefeltet{.is-info}

## Forslag til fellesskapsnavngivning

> Her er noen forslag til fellesskapsnavngivning fra [TRaSH's Guides](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/){.is-info}

> Advarsel: Fra og med v3.0.6.1431 støtter Sonarr nå gjenkjenning av Dolby Vision (DV) og High Dynamic Range (HDR). Hvis du bruker en eldre versjon, erstatt: `{[MediaInfo VideoDynamicRangeType]}` med `{[MediaInfoVideoDynamicRange]}`{.is-warning}

- Standardserier: `{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Daglige serier: `{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- Animeserier: `{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- Sesongmapper: `Season {season:00}`

- Stil for flere episoder: `Scene`

- Seriemapper: `{Series TitleYear} [imdb-{ImdbId}]`

## Episodenavn

- Gi nytt navn til episoder - Merk av for å aktivere Sonarr til å gi nytt navn til filer
  - Hvis ikke merket av:
    - Importering fra nedlastingsklient
      - Ikke sesongpakke: Nedlastingsklientens utgivelsestittel brukes
      - Sesongpakke: Opprinnelig filnavn
    - Manuell (ad hoc) importering: Opprinnelig filnavn

- Erstatt ulovlige tegn - Hvis ikke merket av, vil Sonarr fjerne dem i stedet.
  - Tegnene er: `:` `\` `/` `>` `<` `?` `*` `|` `"`

### Standard episodestruktur

Standard episodestruktur - Angi navnekonvensjonen for episodene i standardserietypen. Klikk på `?`-ikonet for å åpne dialogboksen `Filnavntokens`.

- Rullegardinmeny (øverst til høyre)
  - Venstre boks - Håndtering av mellomrom
  - Mellomrom ( ) - Bruk mellomrom i navngivningen (standard)
  - Periode (.) - Bruk punktum i stedet for mellomrom i navngivningen
  - Understrek (_) - Bruk understrek i stedet for mellomrom i navngivningen
  - Bindestrek (-) - Bruk bindestrek i stedet for mellomrom i navngivningen
  - Høyre boks - Håndtering av store og små bokstaver
  - Standard store og små bokstaver - Gjør tittelen til store og små bokstaver (~camel-case) (standard)
  - Store bokstaver - Gjør tittelen til store bokstaver
  - Små bokstaver - Gjør tittelen til små bokstaver

### Serienavn

- `{Series Title}` = Seriens navn!
- `{Series CleanTitleYear}` = Seriens navn! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Seriens navn!
- `{Series TitleThe}` = Seriens navn!, The
- `{Series TitleYear}` = Seriens navn (2010)
- `{Series Year}` = (2010)

### Serienummer

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### Sesonger

- `{season:0}` = 1
- `{season:00}` =  01

### Episoder

- `{episode:0}` = 1
- `{episode:00}` = 01

### Sendedato

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### Episodetittel

- `{Episode Title}` = Episodetittel
- `{Episode CleanTitle}` =  Episodetittel

### Kvalitet

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### Medieinformasjon

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

> `MediaInfo Full`, `AudioLanguages` og `SubtitleLanguages` støtter en `:EN+DE`-suffiks som lar deg filtrere språkene som er inkludert i filnavnet. Bruk `-DE` for å ekskludere bestemte språk. Hvis du legger til <kb>+</kb> (f.eks.: `:EN+`), vil det bli generert `[EN]`,`[EN+--]` eller `[--]` avhengig av ekskluderte språk. For eksempel `{MediaInfo Full:EN+DE}`{.is-info}

> `AudioLanguages` vil ikke vise et språk for lyd hvis det bare finnes ett språk og det er EN (engelsk). For å få ønsket oppførsel og som et eksempel for å vise tysk og engelsk, bruk {MediaInfo AudioLanguagesAll:DE+EN} i stedet{.is-info}

> `MediaInfo VideoDynamicRangeType` vil gi mulige verdier: DV, DV HDR10, HDR10, HDR10Plus, HLG, PQ og HDR{.is-info}

### Annet

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL eller NF

> \* Preferred words vil være ordet eller ordene som var de bokstavelige treffene for eventuelle foretrukne ord du har. Eksemplet ovenfor vil være et foretrukket ord som `iNTERNAL`, eller tilsvarende et foretrukket ord som `/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i` vil returnere `AMZN` eller `Amazon`{.is-info}

### Original

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> `Original Title` er utgivelsesnavnet og det er det som foreslås å brukes{.is-info}

>`Original Filename` anbefales ikke. Det er det bokstavelige opprinnelige filnavnet og kan være obfuskert `t1i0p3s7i8yu7ti`{.is-warning}

## Struktur for daglige episoder

Struktur for daglige episoder - Angi navnekonvensjonen for episodene i daglige serier. Klikk på `?` for å åpne dialogboksen `Filnavntokens`.

Se [Standard episodestruktur](/sonarr/settings#standard-episode-format) for mer informasjon om denne dialogboksen.

## Struktur for animeepisoder

Struktur for animeepisoder - Angi navnekonvensjonen for episodene i animeserier. Klikk på `?` for å åpne dialogboksen `Filnavntokens`.

Se [Standard episodestruktur](/sonarr/settings#standard-episode-format) for mer informasjon om denne dialogboksen.

### Absolutt episodenummer

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## Struktur for seriemapper

(Avansert alternativ) - Seriemappe - Angi navnekonvensjonen for mappen. Klikk på `?` for å åpne dialogboksen `Filnavntokens`.

### Serienavn

- `{Series Title}` = Seriens navn!
- `{Series CleanTitleYear}` = Seriens navn! 2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = Seriens navn!
- `{Series TitleThe}` = Seriens navn!, The
- `{Series TitleYear}` = Seriens navn (2010)
- `{Series Year}` = (2010)

### Serienummer

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## Struktur for sesongmapper

### Sesonger

- `{season:0}` = 1
- `{season:00}` = 01

## Struktur for spesialmapper

Navn for `Spesialer` (sesong)mappe

- `Spesialer`

> Det anbefales å bruke `Spesialer`{.is-info}

## Stil for flere episoder

- `Utvid` = `S01E01-02-03`
- `Dupliser` = `S01E01.S01E01`
- `Gjenta` = `S01E01E02E03`
- `Scene` = `S01E01-E02-E03`
- `Rekkevidde` = `S01E01-03`
- `Prefikset rekkevidde` = `S01E01-E03`

> Det anbefales å bruke `Scene`{.is-info}

## Mapper

- Opprett tomme mediemapper - Opprett manglende seriemapper under disk-skanning
- Slett tomme mapper - Slett tomme seriemapper og sesongmapper under disk-skanning og når episodfiler slettes

## Importering

- Episode Title Required - Påse at episodetittelen er påkrevd. Forhindre import i opptil 48 timer fra episodens [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)-sendetidspunkt hvis episodetittelen er i riktig format og episodetittelen er TBA (To Be Announced). Etter 48 timer vil importen bli gjort selv om tittelen fortsatt er TBA.
  - Alltid - Vent alltid i opptil 48 timer på en tittel før import hvis episoden er TBA.
  - Kun for masseutgivelser av sesonger - Vent bare i opptil 48 timer på en tittel før import hvis episoden er TBA og det er en masseutgivelse av en sesong. <- Dette anbefales.
  - Aldri - Ikke forsink import hvis episoden er TBA.
- Hopp over sjekk av ledig plass - Bruk når Sonarr ikke kan oppdage ledig plass fra rotmappen til serien din.
- Minimum ledig plass - Slå dette på for å forhindre import hvis det vil være mindre enn denne mengden diskplass tilgjengelig.
- Bruk hardlink i stedet for kopi - Bruk hardlink når du prøver å kopiere filer fra torrents som fortsatt blir seedet.
  - For mer informasjon om dette, klikk [her](https://trash-guides.info/hardlinks)

 > Sjelden, men muligvis, kan filsperrer forhindre at filer som blir seedet, blir omdøpt. Du kan midlertidig deaktivere seeding og bruke Sonarrs omdøpefunksjon som en midlertidig løsning.
{.is-warning}

- Importer ekstra filer - Importer matchende ekstra filer (undertekster, nfo, osv.) etter at en fil er importert.
  Hvis en undertekstfilnavn inneholder ekstra tagger som `cc` eller `forced`, vil de bli bevart så lenge de blir gjenkjent (for øyeblikket i utviklingsversjonen).

## Filbehandling

- Slutt å overvåke slettede episoder - Episoder som er slettet fra disken, blir automatisk sluttet å overvåke i Sonarr.
- Last ned riktig versjon og reparasjoner - Om Sonarr skal oppgradere automatisk til riktig versjon og reparasjoner. Bruk "Ikke foretrekk" for å sortere etter foretrukket ordpoeng over riktig versjon og reparasjoner.
  - Foretrekk og oppgrader - Ranger riktig versjon og reparasjoner høyere enn ikke-riktig versjon og ikke-reparasjoner. Behandle nye riktige versjoner og reparasjoner som oppgradering til gjeldende utgivelser.
  - Ikke oppgrader automatisk - Ranger riktig versjon og reparasjoner høyere enn ikke-riktig versjon og ikke-reparasjoner. Behandle ikke nye riktige versjoner og reparasjoner som oppgradering til gjeldende utgivelser.
  - Ikke foretrekk - Ignorer riktig versjon og reparasjoner. Du må håndtere eventuelle preferanser for disse med [Utgivelsesprofiler (Foretrukne ord)](#utgivelsesprofiler).

> `PROPER` - betyr at det var et problem med den forrige utgivelsen. Nedlastinger merket som PROPER viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som ikke ga ut originalen.
> `REPACK` - betyr at det var et problem med den forrige utgivelsen og at det er rettet opp av den opprinnelige gruppen. Nedlastinger merket som REPACK viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som ga ut originalen.
{.is-info}

> [Bruk foretrukne ord for automatisk oppgradering til riktig versjon og reparasjoner](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#propers-and-repacks)
{.is-info}

- Analyser videofiler - Hent ut filinformasjon som oppløsning, kjøretid og kodekinformasjon fra filer. Dette krever at Sonarr leser deler av filen, noe som kan føre til høy disk- eller nettverksaktivitet under skanning.
- Skann seriemappe etter oppdatering - Skann seriemappen på nytt etter oppdatering av serien
  - Alltid - Dette vil skanne seriemappen basert på oppgaveplanen
  - Etter manuell oppdatering - Du må skanne disken manuelt
  - Aldri - Akkurat som det står, ikke skann seriemappen på nytt.
- Endre filens dato - Endre filens dato ved import/skanning på nytt
  - Ingen - Sonarr vil ikke endre datoen som vises i filutforskeren din
  - Lokal utgivelsesdato - Datoen videoen ble sendt lokalt
  - UTC utgivelsesdato - Datoen videoen ble utgitt basert på UTC
- Gjenvinningsbin - Episodfiler vil havne her når de slettes i stedet for å bli permanent slettet
- Rengjøring av gjenvinningsbin - Dette er hvor gammel en gitt fil kan være før den blir permanent slettet

> Filer i gjenvinningsbinen som er eldre enn det valgte antallet dager, vil bli ryddet automatisk {.is-warning}

## Tillatelser

- Sett tillatelser - Skal `chmod` kjøres når filer importeres/omdøpes?
  - chmod-mappen - Åttetall, brukt under import/omdøping til mediamapper og filer (uten kjøretillatelser)

> Nedtrekksboksen har en forhåndsdefinert liste over vanlig brukte tillatelser som kan brukes. Du kan imidlertid manuelt angi en mappeoktal hvis du ønsker det.
{.is-info}

> Dette fungerer bare hvis brukeren som kjører `Sonarr` er eieren av filen. Det er bedre å sørge for at nedlastingsklienten setter tillatelsene riktig.
{.is-warning}

- chown-gruppe - Gruppenavn eller GID. Bruk GID for eksterne filsystemer

> Dette fungerer bare hvis brukeren som kjører `Sonarr` er eieren av filen. Det er bedre å sørge for at nedlastingsklienten setter tillatelsene riktig.
{.is-warning}

## Rotmapper

- Sti - Dette viser stien til mediebiblioteket ditt
- Ledig plass - Dette er ledig plass som rapporteres til Sonarr fra systemet
- Umappe-mapper - Dette er mapper som ikke har en tilknyttet serie

> `X` på slutten vil fjerne denne rotstien
{.is-info}

- Legg til rotmappe - Dette lar deg velge en rotsti som et sted å enten plassere nye importerte nedlastinger i denne mappen eller å tillate Sonarr å skanne eksisterende medier.

> Brukere som ikke bruker Windows:
> \* Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
> \* Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.
{.is-warning}

# Profiler

## Kvalitetsprofiler

- Sett profiler for kvaliteten på seriene du ønsker å laste ned.

> Når du velger en eksisterende profil eller legger til en ekstra profil, vil et nytt vindu vises
{.is-info}

> Merk: Kvaliteten som har en blå boks, er kvaliteten som alle medier med denne profilen vil fortsette å oppgraderes til.
{.is-info}

- Navn - Velg et **UNIKT** navn for kvalitetsprofilen du oppretter
- Oppgraderinger tillatt - Når dette alternativet er merket av, og du ber Sonarr om å laste ned en `WEB 1080p` fordi det er den første utgivelsen av en bestemt episode, og senere kan noen laste opp en `Bluray-1080p`, vil Sonarr automatisk oppgradere til bedre kvalitet ***hvis*** `Oppgrader til` har den kvaliteten valgt
- Oppgrader til - Når denne kvaliteten er nådd, vil Sonarr ikke lenger laste ned episoder

> Merk: Dette gjelder bare hvis du har `Bluray-1080p` høyere enn `WEB 1080p` innenfor `Kvaliteter`-delen
{.is-warning}

- Kvaliteter - Kvaliteter som er høyere på listen, foretrekkes selv om de ikke er merket av. Kvaliteter innenfor samme gruppe er likeverdige. Bare merkede kvaliteter ønskes.
- Rediger grupper - Noen kvaliteter er gruppert sammen for å redusere størrelsen på listen, samt gruppere lignende utgivelser. Et godt eksempel på dette er `WebDL` og `WebRip`, da disse er veldig like og vanligvis har lignende bithastigheter. Når du redigerer gruppene, kan du endre preferansen innenfor hver av gruppene. [Se TRaShs guide for hvordan du slår sammen kvaliteter](https://trash-guides.info/merge-quality)
  - [Se kvaliteter](#qualities-defined)

> Som standard er kvalitetene satt fra laveste (nederst) til høyeste (øverst)
{.is-info}

## Språkprofiler

- Sett profiler for språket på seriene du ønsker å laste ned.

> Vær oppmerksom på at prioriteringen/rekkefølgen har betydning, selv om språket ikke er ønsket (valgt).
{.is-info}

- Navn - Velg et **UNIKT** navn for språkprofilen du oppretter
- Oppgraderinger tillatt - Hvis ikke merket av (deaktivert), vil språk ikke bli oppgradert. For eksempel, hvis du ber Sonarr om å laste ned en kinesisk versjon fordi det er den første utgivelsen av en bestemt serie, og senere kan noen laste opp en engelsk versjon, vil Sonarr med dette alternativet merket av automatisk oppgradere til bedre kvalitet

> Dette er bare gyldig hvis engelsk er høyere på språklisten enn kinesisk, og begge er valgt
{.is-warning}

- Språk - Språk som er høyere på listen, foretrekkes. Bare merkede språk ønskes

## Forsinkelsesprofiler

- Forsinkelsesprofiler lar deg redusere antall utgivelser som blir lastet ned for en episode ved å legge til en forsinkelse mens Sonarr fortsetter å se etter utgivelser som bedre samsvarer med preferansene dine.
- Foretrukket protokoll - Dette vil enten være `Usenet` eller `Torrent`, avhengig av hvilken nedlastingsprotokoll du foretrekker
- Usenet-forsinkelse - Angi antall minutter du vil vente før nedlastingen starter for Usenet
- Torrent-forsinkelse - Angi antall minutter du vil vente før nedlastingen starter for Torrent
- Bypass hvis høyeste kvalitet - Bypass forsinkelsen når utgivelsen har den høyeste aktiverte kvalitetsprofilen med foretrukket protokoll
- Merker - Ved å gi denne forsinkelsesprofilen et merke, kan du merke en gitt serie for å følge reglene som er satt her.
- Skiftenøkkelikon - Dette lar deg redigere forsinkelsesprofilen
- Plussikon (<kb>+</kb>) - Opprett en ny forsinkelsesprofil

### Bruksområder

Noen medier vil motta et halvt dusin forskjellige utgivelser av varierende kvalitet i timene etter en utgivelse, og uten forsinkelsesprofiler kan Sonarr prøve å laste ned alle sammen. Med forsinkelsesprofiler kan Sonarr konfigureres til å ignorere de første timene med utgivelser.

Forsinkelsesprofiler er også nyttige hvis du vil legge vekt på en protokoll (Usenet eller BitTorrent) over den andre. (Se [Eksempel 3](/sonarr/settings/#example-3))

### Hvordan forsinkelsesprofiler fungerer

Telleren starter så snart Sonarr oppdager at en episode har en tilgjengelig utgivelse. Denne utgivelsen vises i køen din med et klokkeikon for å indikere at den er under forsinkelse.

> Klokken starter fra tidspunktet utgivelsen ble lastet opp og ikke fra tidspunktet Sonarr ser den.
{.is-info}

I løpet av forsinkelsesperioden vil Sonarr merke seg eventuelle nye utgivelser som blir tilgjengelige. Når forsinkelsestimeren utløper, vil Sonarr laste ned den ene utgivelsen som best samsvarer med kvalitetspreferansene dine.

Tidtakerperioden kan være forskjellig for Usenet og Torrents. Hver profil kan være tilknyttet en eller flere merker, slik at du kan tilpasse hvilke serier som har hvilke profiler. En forsinkelsesprofil uten merke regnes som standard og gjelder for alle serier som ikke har et spesifikt merke.

> Forsinkelsesprofiler starter fra tidspunktet som indekseren rapporterer at utgivelsen ble lastet opp. Dette betyr at innhold som er eldre enn antall minutter du har satt, ikke påvirkes på noen måte av forsinkelsesprofilen din, og vil bli lastet ned umiddelbart. I tillegg vil **alle manuelle søk** etter innhold (søk utenom RSS-feed) ignorere innstillingene for forsinkelsesprofilen.
{.is-warning}

#### Eksempler

- For hvert eksempel, anta at brukeren har følgende kvalitetsprofil aktiv: HDTV 720p og høyere er tillatt, WebDL 720p er kvalitetsgrensen, WebDL 1080p er den høyest rangerte kvaliteten

##### Eksempel 1

- I dette enkle eksempelet er profilen satt med en 120 minutters (to timers) forsinkelse for både Usenet og Torrent.

- Klokken 23:00 oppdager Sonarr den første utgivelsen for en episode, og den ble lastet opp kl. 22:50, og 120 minutters klokke starter. Kl. 00:50 vil Sonarr vurdere eventuelle utgivelser den har funnet i løpet av de siste to timene, og laste ned den beste, som er WebDL 720p.

- Kl. 03:00 blir det funnet en annen utgivelse, som er WebDL 720p, og den ble lagt til i indeksen din kl. 02:46. En annen 120 minutters klokke starter. Kl. 04:46 blir den beste tilgjengelige utgivelsen lastet ned. Siden kvalitetsgrensen nå er nådd, kan ikke episoden oppgraderes lenger, og Sonarr vil slutte å lete etter nye utgivelser.

- På et hvilket som helst tidspunkt, hvis det blir funnet en WebDL 1080p-utgivelse, vil den bli lastet ned umiddelbart fordi den er den høyest rangerte kvaliteten. Hvis det er en aktiv forsinkelsestimer, vil den bli kansellert.

##### Eksempel 2

- Dette eksempelet har forskjellige tidtakere for Usenet og Torrents. Anta en 120 minutters timer for Usenet og en 180 minutters timer for BitTorrent.

- Kl. 23:00 oppdages den første utgivelsen for en episode av Sonarr, og begge tidtakerne starter. Utgivelsen ble lagt til i indeksen kl. 22:15. Kl. 00:15 vil Sonarr vurdere eventuelle utgivelser, og hvis det er noen akseptable Usenet-utgivelser, vil den beste bli lastet ned, og begge tidtakerne vil avsluttes. Hvis ikke, vil Sonarr vente til kl. 00:15 og laste ned den beste utgivelsen, uavhengig av hvilken kilde den kommer fra.

##### Eksempel 3

- En vanlig bruk for forsinkelsesprofiler er å legge vekt på en protokoll over den andre. For eksempel kan du bare ønske å laste ned en BitTorrent-utgivelse hvis ingenting har blitt lastet opp til Usenet etter en viss tid.

- Du kan sette en 60 minutters timer for BitTorrent og en 0 minutters timer for Usenet.

- Hvis den første utgivelsen som oppdages, er fra Usenet, vil Sonarr laste den ned umiddelbart.

- Hvis den første utgivelsen er fra BitTorrent, vil Sonarr sette en 60 minutters timer. Hvis det blir oppdaget noen kvalifiserte Usenet-utgivelser i løpet av den timen, vil BitTorrent-utgivelsen bli ignorert, og Usenet-utgivelsen vil bli lastet ned.

## Utgivelsesprofiler

- Ikke alle utgivelser er like, hver utgivelsesgruppe har sin egen måte å pakke og kode materialet sitt på. Her kan du velge de foretrukne utgivelsene du leter etter.

> Du kan bruke regex (standard forskjell på store og små bokstaver) i feltene for "Må inneholde", "Må ikke inneholde" og "Foretrukne" ord. Regex må være i formen `/regex-her/i`
{.is-info}

- Navn - Velg et **UNIKT** navn for utgivelsesprofilen du oppretter
- Aktiver profil - Slå denne profilen på eller av
- Må inneholde - Utgivelsen må inneholde minst ett av disse termene (forskjell på store og små bokstaver)
- Må ikke inneholde - Utgivelsen vil bli avvist hvis den inneholder ett eller flere av termene (forskjell på store og små bokstaver)
- Foretrukne - Her kan du velge et gitt ord og gi det en poengsum.
  - La oss si at du leter etter utgivelser med en bestemt gruppe ord. La oss si at du vil fortelle Sonarr at du vil ha Repacks eller Propers fremfor vanlige utgivelser. Her vil du legge inn ordet Repack i ett av feltene og gi det en verdi (for eksempel 100), men du leter også etter DTS-HD-lyd, så du vil legge det inn der og gi det en poengsum (for eksempel 100 igjen). Når Sonarr går gjennom og ser på alle utgivelsene fra RSS-feeden, og den kommer over en utgivelse som har både Repack og DTS-HD, vil det gi en poengsum på 200. Dette er mye høyere enn alle de andre som ikke har noen av disse ordene. Dette forteller Sonarr at dette har en høyere poengsum, og det vil være den første filen som blir valgt for nedlasting.
- Inkluder foretrukne ved omdøping - Når du bruker {Foretrukne ord}-taggen i navneskjemaet
- Indekser - Spesifiser hvilken indekser profilen gjelder for.

> Dette er nyttig hvis du bare vil ha spesifikke utgivelser fra en gitt indekser/tracker
{.is-info}

- Merker - Ved å gi denne utgivelsesprofilen et merke, kan du merke en gitt serie for å følge reglene som er satt her. Hvis du lar dette feltet stå tomt, vil disse reglene gjelde for alle serier

- [TRaSH vedlikeholder en liste over WEB-DL-utgivelsesprofiler](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/)
- [TRaSH Anime-profiler](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx-Anime/)

# Kvalitet

## Betydning av kvalitetstabell

- Kvalitet - Navnet på kvaliteten i scenen (hardkodet)
- Tittel - Navnet på kvaliteten i brukergrensesnittet (konfigurerbart)
- Megabyte per time - Selvforklarende
- Størrelsesgrense - Selvforklarende
- Min - Minimum antall megabyte per minutt (MB/min) en kvalitet kan ha.
- Maks - Maksimum antall megabyte per minutt (MB/min) en kvalitet kan ha.

## Definerte kvaliteter

- Ukjent - Selvforklarende
- SDTV - Postlufting fra en analog kilde (vanligvis kabel-TV eller OTA standard definisjon). Bildekvaliteten er generelt god (for oppløsningen) og de er vanligvis kodet i DivX/XviD eller MP4.
- WEBDL-480p - WEB-DL (P2P) refererer til en fil som er ripet tappestfritt fra en strømmetjeneste, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, osv., eller lastet ned via en online distribusjonsside som iTunes. Kvaliteten er ganske god, siden de ikke er kodet på nytt. Videoen (H.264 eller H.265) og lyden (AC3/AAC) er vanligvis ekstrahert fra iTunes eller Amazon Video og remukset inn i en MKV-beholder uten å ofre kvaliteten. En fordel med disse utgivelsene er at de vanligvis ikke har nettverkslogoer på skjermen. Disse er nesten like gode som en Blu-ray-kilde, men kan lide av lydforsinkelse eller visuelle artefakter fra den adaptive bithastigheten til strømmetjenestene. Hvis en ripper mister internettforbindelsen til et punkt der bithastigheten senkes, kan kildebithastigheten endre seg dynamisk, noe som kan føre til variasjoner i bildekvaliteten. De fleste utgivelser som lider av en ekstrem mengde visuelle artefakter blir NUKED og en PROPER blir vanligvis utgitt for å fikse eventuelle ville variasjoner i adaptiv bithastighet. Dette vil være i 480p (SD) kvalitet.
- WEBRip-480p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokollene og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 480p (SD) kvalitet.
- DVD - En nykoding av den endelige utgitte DVD9. Hvis det er mulig, blir dette utgitt PRE-retail. Det bør være utmerket kvalitet (for oppløsningen). DVDrips blir vanligvis utgitt i DivX/XviD eller MP4.
- Bluray-480p - En nykoding av den endelige utgitte Blu-ray, nedskalert til 480p-oppløsning (720x480 @ 16:9, en annen sideforhold kan være en annen oppløsning). Hvis det er mulig, blir dette utgitt PRE-retail. Det bør være utmerket kvalitet for oppløsningen. Bithastighetene kan variere, men disse er generelt kodet til DivX, XviD eller AVC og tilbyr en liten oppfattet kvalitetsreduksjon i forhold til den opprinnelige kilden, samtidig som filstørrelsen reduseres drastisk. Disse er vanligvis MKV eller MP4, men noen DivX/XviD er også tilgjengelige som bruker AVI.
- HDTV-720p - En nykoding av den endelige utgitte Blu-ray, men sendt over HD-kabel eller satellitt (1280x720 @ 16:9, en annen sideforhold kan være en annen oppløsning). Den kan være endret for kjøretid eller innhold avhengig av nettverket den kommer fra. Dette blir vanligvis utgitt flere måneder etter en detaljhandelsutgivelse, men noen ganger blir oppskalerte versjoner av en standard definisjonsfilm utgitt på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopiene av den spesifikke filmen som er tilgjengelig. Disse er vanligvis MKV eller MP4.
- HDTV-1080p - En nykoding av den endelige utgitte Blu-ray, men sendt over HD-kabel eller satellitt (1920x1080 @ 16:9, en annen sideforhold kan være en annen oppløsning). Den kan være endret for kjøretid eller innhold avhengig av nettverket den kommer fra. Dette blir vanligvis utgitt flere måneder etter en detaljhandelsutgivelse, men noen ganger blir oppskalerte versjoner av en standard definisjonsfilm utgitt på kabelkanaler som STARZ eller HBO, og de vil være de eneste HD-kopiene av den spesifikke filmen som er tilgjengelig. Disse er vanligvis MKV eller MP4-beholder.
- Raw-HD - En rå strøm av en HD-strøm.
- WEBRip-720p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokollene og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 720p kvalitet.
- Bluray-720p - En nykoding av den endelige utgitte Blu-ray, nedskalert til 720p-oppløsning (1280x720 @ 16:9, en annen sideforhold kan være en annen oppløsning). Hvis det er mulig, blir dette utgitt PRE-retail. Det bør være utmerket kvalitet for oppløsningen. Bithastighetene kan variere, men disse er generelt kodet til AVC eller HEVC og tilbyr en liten oppfattet kvalitetsreduksjon i forhold til den opprinnelige kilden, samtidig som filstørrelsen reduseres drastisk. Disse er vanligvis MKV eller MP4-beholder.
- WEBDL-1080p - WEB-DL (P2P) refererer til en fil som er ripet tappestfritt fra en strømmetjeneste, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, osv., eller lastet ned via en online distribusjonsside som iTunes. Kvaliteten er ganske god, siden de ikke er kodet på nytt. Videoen (H.264 eller H.265) og lyden (AC3/AAC) er vanligvis ekstrahert fra iTunes eller Amazon Video og remukset inn i en MKV-beholder uten å ofre kvaliteten. En fordel med disse utgivelsene er at de vanligvis ikke har nettverkslogoer på skjermen. Disse er nesten like gode som en Blu-ray-kilde, men kan lide av lydforsinkelse eller visuelle artefakter fra den adaptive bithastigheten til strømmetjenestene. Hvis en ripper mister internettforbindelsen til et punkt der bithastigheten senkes, kan kildebithastigheten endre seg dynamisk, noe som kan føre til variasjoner i bildekvaliteten. De fleste utgivelser som lider av en ekstrem mengde visuelle artefakter blir NUKED og en PROPER blir vanligvis utgitt for å fikse eventuelle ville variasjoner i adaptiv bithastighet. Dette vil være i 1080p kvalitet.
- WEBRip-1080p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokollene og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 1080p kvalitet.
- Bluray-1080p - En nykoding av den endelige utgitte Blu-ray, i sin opprinnelige 1080p-oppløsning (1920x1080 @ 16:9, en annen sideforhold kan være en annen oppløsning). Hvis det er mulig, blir dette utgitt PRE-retail. Det bør være utmerket kvalitet og samme oppløsning som kilden. Bithastighetene kan variere, men disse er generelt kodet til AVC eller HEVC og tilbyr en liten oppfattet kvalitetsreduksjon i forhold til den opprinnelige kilden, samtidig som filstørrelsen reduseres litt. Disse er vanligvis MKV eller MP4-beholder.
- Remux-1080p - En remux er en rip av en Blu-ray- eller HD DVD-plate til en annen beholderformat eller bare fjerner menyene og bonusmaterialet fra platen samtidig som innholdet i lyd- og videostreamene beholdes (også de nåværende kodekene), og garanterer nøyaktig 1:1 filmkvalitet som på den opprinnelige disken. Dette er i 1080p kvalitet.
- HDTV-2160p - TVRip er en opptakskilde fra et opptakskort. HDTV står for opptakskilde fra HD-TV. Med en HDTV-kilde kan kvaliteten noen ganger til og med overgå DVD. Filmer i dette formatet begynner å bli populære. Noen annonser og kommersielle bannere kan sees på noen utgivelser under avspilling. Dette er i 2160p (4K) kvalitet.
- WEBDL-2160p - WEB-DL (P2P) refererer til en fil som er ripet tappestfritt fra en strømmetjeneste, som Netflix, Amazon Video, Hulu, Crunchyroll, Discovery GO, BBC iPlayer, osv., eller lastet ned via en online distribusjonsside som iTunes. Kvaliteten er ganske god, siden de ikke er kodet på nytt. Videoen (H.264 eller H.265) og lyden (AC3/AAC) er vanligvis ekstrahert fra iTunes eller Amazon Video og remukset inn i en MKV-beholder uten å ofre kvaliteten. En fordel med disse utgivelsene er at de vanligvis ikke har nettverkslogoer på skjermen. Disse er nesten like gode som en Blu-ray-kilde, men kan lide av lydforsinkelse eller visuelle artefakter fra den adaptive bithastigheten til strømmetjenestene. Hvis en ripper mister internettforbindelsen til et punkt der bithastigheten senkes, kan kildebithastigheten endre seg dynamisk, noe som kan føre til variasjoner i bildekvaliteten. De fleste utgivelser som lider av en ekstrem mengde visuelle artefakter blir NUKED og en PROPER blir vanligvis utgitt for å fikse eventuelle ville variasjoner i adaptiv bithastighet. Dette vil være i 2160p (4K) kvalitet.
- WEBRip-2160p - I en WEB-Rip (P2P) blir filen ofte ekstrahert ved hjelp av HLS- eller RTMP/E-protokollene og remukset fra en TS-, MP4- eller FLV-beholder til MKV. Dette vil være i 2160p (4k) kvalitet.
- Bluray-2160p - En nykoding av den endelige utgitte Blu-ray, i sin opprinnelige 2160p-oppløsning (3840x2160 @ 16:9, en annen sideforhold kan være en annen oppløsning). 4K-versjoner av filmer som er utgitt i generelt HEVC-kodek og kan være enten 8-bit eller 10-bit fargereproduksjon eller fra en HDR-kilde. Disse er vanligvis MKV eller MP4-beholder.
- Remux-2160p - En remux er en rip av en Blu-ray- eller HD DVD-plate til en annen beholderformat eller bare fjerner menyene og bonusmaterialet fra platen samtidig som innholdet i lyd- og videostreamene beholdes (også de nåværende kodekene), og garanterer nøyaktig 1:1 filmkvalitet som på den opprinnelige disken. Dette er i 2160p (4K) kvalitet.

# Indekseringsverktøy

> Informasjon om støttede indekseringsverktøy finner du på siden [Mer informasjon (Støttet)](/sonarr/supported#indexers) for denne delen
{.is-info}

## Støttede indekseringsverktøy

- En liste over støttede indekseringsverktøy finnes på siden [Mer informasjon (Støttet)](/sonarr/supported#indexers)

### Innstillinger for indekseringsverktøy

- Når du har klikket på <kb>+</kb>-knappen for å legge til et nytt indekseringsverktøy, vil du få opp et nytt vindu med mange forskjellige alternativer. For formålet med denne wikien betrakter Sonarr både Usenet-indekseringsverktøy og Torrent-sporere som "indekseringsverktøy".

- Det er to seksjoner her: Usenet og Torrents. Basert på hvilken nedlastingsklient du vil bruke, må du velge hvilken type indekseringsverktøy du vil bruke.

### Konfigurasjon av Usenet-indekseringsverktøy

- Newznab - Her finner du forhåndsinnstillinger for populære Usenet-indekseringsverktøy (som er forhåndsutfylt, alt du trenger er API-nøkkelen som er gitt av Usenet-indekseringsverktøyet du velger) sammen med muligheten til å opprette et tilpasset indekseringsverktøy.
- Programvare som fungerer med Usenet og integrerer godt med Sonarr er [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr) som integrerer med både Usenet og Torrents.
- Uansett om du velger et forhåndsutfylt indekseringsverktøy eller en tilpasset indekseringsverktøyoppsett, vil du få opp et nytt vindu for å legge inn alle innstillingene dine.
- Velg mellom forhåndsinnstillingene eller legg til et tilpasset indekseringsverktøy (som NZBHydra2 eller Prowlarr)
- Navn - Navnet på indekseringsverktøyet i Sonarr
- Aktiver RSS - Hvis aktivert, bruk dette indekseringsverktøyet for å se etter filer som er ønsket og mangler eller ennå ikke har nådd kuttet.
- Aktiver automatisk søk - Hvis aktivert, bruk dette indekseringsverktøyet for automatisk søk, inkludert søk ved tillegg
- Aktiver interaktivt søk - Hvis aktivert, bruk dette indekseringsverktøyet for manuelle interaktive søk.
- URL - URL-en som indekseringsverktøyet gir, for eksempel `https://api.nzbgeek.info`.
- API-sti - Stien som indekseringsverktøyet gir til API-en. Dette er vanligvis `/api`
- API-nøkkel - Nøkkelen som indekseringsverktøyet gir for å få tilgang til API-en.
- Kategorier - Standardkategorier vil bli brukt med mindre de redigeres. Det er sannsynlig at disse standardkategoriene ikke er optimale. Når du redigerer denne innstillingen, spør Sonarr indekseringsverktøyet om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir vekslet.
- Animekategorier - Kategoriene som Sonarr vil bruke for Anime-søk. Ingen kategorier vil bli brukt med mindre de redigeres. Når du redigerer denne innstillingen, spør Sonarr indekseringsverktøyet om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir vekslet.
- Søk etter standardformat for anime - Søk også etter anime ved hjelp av standardnummerering (gjelder bare for anime-serietyper) [Mer informasjon om serietyper her](/sonarr/faq#whats-the-different-series-types)
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere for Newznab som skal legges til i spørringslenken
- (Avansert alternativ) Indekseringsprioritet - Prioritet for dette indekseringsverktøyet for å foretrekke ett indekseringsverktøy over et annet i utgivelseskonfliktsituasjoner. 1 er høyeste prioritet og 50 er laveste prioritet.
- (Avansert alternativ) Nedlastingsklient - Velg og spesifiser hvilken nedlastingsklient som brukes for nedlastinger fra dette indekseringsverktøyet
- Merker - Bruk bare dette indekseringsverktøyet for serier med minst ett matchende merke. La være blankt for å bruke med alle serier.

### Konfigurasjon av Torrent-sporer

- Som med Usenet er det en rekke forhåndsutfylte Torrent-sporerinformasjon. Hvis du ikke er medlem av noen av disse spesifikke sporerne, vil de ikke være til noen nytte for deg.
- En av de beste og enkleste måtene å bruke Torrent-sporere som ikke er naturlig støttet med Sonarr, er å bruke et annet program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Disse programmene fungerer godt sammen med Sonarr som en søkeindekser som inneholder all informasjonen din og sender den til Sonarr.
- Torznab - Dette alternativet vil sette deg opp med en Jackett-forhåndsinnstilling, hvis du bruker flere sporer, må hver oppføring ha et unikt navn
- Torznab-indekseringsverktøy
- Velg mellom forhåndsinnstillingene eller legg til et tilpasset indekseringsverktøy (som Jackett eller Prowlarr)
- Navn - Navnet på indekseringsverktøyet i Sonarr
- Aktiver RSS - Hvis aktivert, bruk dette indekseringsverktøyet for å se etter filer som er ønsket og mangler eller ennå ikke har nådd kuttet.
- Aktiver automatisk søk - Hvis aktivert, bruk dette indekseringsverktøyet for automatisk søk, inkludert søk ved tillegg
- Aktiver interaktivt søk - Hvis aktivert, bruk dette indekseringsverktøyet for manuelle interaktive søk.
- URL - URL-en som indekseringsverktøyet gir, for eksempel `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sti - Stien som indekseringsverktøyet gir til API-en. Dette er vanligvis `/api`
- API-nøkkel - Nøkkelen som indekseringsverktøyet gir for å få tilgang til API-en.
- Kategorier - Standardkategorier vil bli brukt med mindre de redigeres. Det er sannsynlig at disse standardkategoriene ikke er optimale. Når du redigerer denne innstillingen, spør Sonarr indekseringsverktøyet om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir vekslet.
- Animekategorier - Kategoriene som Sonarr vil bruke for Anime-søk. Ingen kategorier vil bli brukt med mindre de redigeres. Når du redigerer denne innstillingen, spør Sonarr indekseringsverktøyet om tilgjengelige kategorier og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir vekslet.
- Søk etter standardformat for anime - Søk også etter anime ved hjelp av standardnummerering (gjelder bare for anime-serietyper) [Mer informasjon om serietyper her](/sonarr/faq#whats-the-different-series-types)
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere for Torznab som skal legges til i spørringslenken
- (Avansert alternativ) Minimum antall seedere - Minimum antall seedere som kreves for at en utgivelse fra denne sporeren skal bli lastet ned.
- (Avansert alternativ) Seedratio - Hvis det er tomt, bruk standardinnstillingen for nedlastingsklienten. Ellers er minimum seedratio som kreves for at nedlastingsklienten din skal oppfylle for utgivelser fra denne indekseringsverktøyet før den blir satt på pause av klienten din og fjernet av Sonarr (krever at fullført nedlastingshåndtering - fjerning er aktivert)
- (Avansert alternativ) Seedtid - Hvis det er tomt, bruk standardinnstillingen for nedlastingsklienten. Ellers er minimum seedtid i minutter som kreves for at nedlastingsklienten din skal oppfylle for utgivelser fra denne indekseringsverktøyet før den blir satt på pause av klienten din og fjernet av Sonarr (krever at fullført nedlastingshåndtering - fjerning er aktivert)
- (Avansert alternativ) Indekseringsprioritet - Prioritet for dette indekseringsverktøyet for å foretrekke ett indekseringsverktøy over et annet i utgivelseskonfliktsituasjoner. 1 er høyeste prioritet og 50 er laveste prioritet.
- (Avansert alternativ) Nedlastingsklient - Velg og spesifiser hvilken nedlastingsklient som brukes for nedlastinger fra dette indekseringsverktøyet
- Merker - Bruk bare dette indekseringsverktøyet for serier med minst ett matchende merke. La være blankt for å bruke med alle serier.

## Alternativer

- Minimumsalder - Kun Usenet: Minimumsalder i minutter for NZB-er før de blir lastet ned. Bruk dette for å gi nye utgivelser tid til å spre seg til Usenet-leverandøren din.
- Oppbevaring - Kun Usenet: Sett til null for ubegrenset oppbevaring
- Maksimal størrelse - Maksimal størrelse for en utgivelse som skal lastes ned i MB. Sett til null for ubegrenset. Vær oppmerksom på at dette gjelder globalt.
- RSS-synkroniseringsintervall - Intervall i minutter. Sett til null for å deaktivere (dette vil stoppe all automatisk utgavehenting) Minimum: 10 minutter Maksimum: 120 minutter
  - Se [Hvordan finner Sonarr episoder?](/sonarr/faq#how-does-sonarr-find-episodes) for bedre forståelse av hvordan RSS-synkronisering vil hjelpe deg

> Hvis Sonarr har vært frakoblet i lang tid, vil Sonarr forsøke å bla tilbake for å finne den siste utgivelsen den behandlet for å unngå å gå glipp av en utgivelse. Så lenge indekseringsverktøyet ditt støtter paging og det ikke har gått for lang tid, vil Sonarr kunne behandle utgivelsene den ville ha gått glipp av og unngå at du må søke etter de tapte utgivelsene.{.is-info}

# Nedlastingsklienter

> Informasjon om støttede nedlastingsklienter finner du på siden [Mer informasjon (Støttet)](/sonarr/supported#download-clients) for denne delen
{.is-info}

## Oversikt

- Nedlasting og import er der de fleste opplever problemer. Fra et overordnet perspektiv må programvaren kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det finnes et stort utvalg av støttede nedlastingsklienter og enda flere forskjellige oppsett. Dette betyr at selv om det er noen vanlige oppsett, er det ikke ett riktig oppsett, og alle oppsettene kan være litt forskjellige. Men det er mange feilaktige oppsett.

## Prosesser for nedlastingsklienter

## Usenet

- Sonarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Sonarr vil overvåke dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Sonarr kjenne den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din og tilgjengelig for Sonarr.
- Sonarr vil skanne denne fullførte filplasseringen etter filer som Sonarr kan bruke. Den vil analysere filnavnet for å matche det med den forespurte medien. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte medielokasjonen.
- Atomiske flyttinger (umiddelbare flyttinger) er aktivert som standard. Filsystemet og monteringspunktene må være de samme for fullføringsmappen for nedlastinger og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Sonarr bruke kopiering av filen og deretter slette den fra kilden, noe som er krevende for IO.
- Hvis alternativet "Fullførte nedlastingshåndtering - Fjern" er aktivert i Sonarrs innstillinger, vil gjenværende filer fra nedlastingen bli sendt til papirkurven eller resirkuleringen via en forespørsel til klienten din om å slette/fjerne utgivelsen.

## BitTorrent

- Sonarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
  - Eksempler: filmer, tv, serier, musikk, osv.
- Sonarr vil overvåke dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Fullførte filer blir liggende på sin opprinnelige plassering for å tillate deg å seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Sonarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil Sonarr opprette en hardlenke til filen hvis det støttes av oppsettet ditt, eller kopiere den hvis hardlenker ikke støttes.
- Hardlenker er aktivert som standard. [En hardlenke vil ikke bruke noe ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for fullføringsmappen for nedlastinger og mediebiblioteket ditt. Hvis opprettelsen av hardlenken mislykkes eller oppsettet ditt ikke støtter hardlenker, vil Sonarr bruke kopiering av filen.
- Hvis alternativet "Fullførte nedlastingshåndtering - Fjern" er aktivert i Sonarrs innstillinger, vil Sonarr slette torrenten fra klienten din og be klienten om å fjerne torrentdataene, men bare hvis klienten rapporterer at seeding er fullført og torrenten er stoppet (pauset ved fullføring).

## Nedlastingsklienter

Klikk på `Innstillinger` => `Nedlastingsklienter`, og klikk deretter på <kb>+</kb> for å legge til en ny nedlastingsklient. Nedlastingsklienten din bør allerede være konfigurert og kjøre.

### Støttede nedlastingsklienter

- En liste over støttede nedlastingsklienter finnes på siden [Mer informasjon (Støttet)](/sonarr/supported#download-clients)

Velg nedlastingsklienten du ønsker å legge til, og det vil vises en popup-boks der du kan angi tilkoblingsdetaljer. Disse detaljene er like for de fleste klienter. Noen vil be om et brukernavn eller passord, noen vil spørre om du vil legge til nye nedlastinger i en pauset/startet tilstand, osv.

### Innstillinger for Usenet-klienter

- Navn - Navnet på nedlastingsklienten i Sonarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din; dette er vanligvis webgui-porten
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proksier.
- API-nøkkel - API-nøkkelen for å autentisere mot klienten din
- Brukernavn - brukernavnet for å autentisere mot klienten din (vanligvis ikke nødvendig)
- Passord - passordet for å autentisere mot klienten din (vanligvis ikke nødvendig)
- Kategori - kategorien i nedlastingsklienten din som \*Arr vil bruke. For å unngå at urelaterte nedlastinger vises i aktiviteten, anbefales det sterkt å angi en kategori.
- Nylig prioritet - nedlastingsklientprioritet for nylig utgitte medier
- Eldre prioritet - nedlastingsklientprioritet for medier som ikke nylig er utgitt
- (Avansert alternativ) Klientprioritet - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet og 50 er laveste prioritet
- Håndtering av fullførte nedlastinger
  - Fjern (Per klientinnstilling) - Fjern fullførte nedlastinger når de er ferdige (usenet) eller stoppet/fullført (torrenter). Se [Fullførte nedlastingshåndtering for mer informasjon](#fullførte-nedlastingshåndtering)

### Innstillinger for torrentklienter

- Navn - Navnet på nedlastingsklienten i Sonarr
- Aktiver - Aktiver denne nedlastingsklienten
- Vert - URL-en til nedlastingsklienten din
- Port - Porten til nedlastingsklienten din
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proksier.
- Brukernavn - brukernavnet for å autentisere mot klienten din
- Passord - passordet for å autentisere mot klienten din
- Kategori - kategorien i nedlastingsklienten din som \*Arr vil bruke. For å unngå at urelaterte nedlastinger vises i aktiviteten, anbefales det sterkt å angi en kategori.
- Kategori etter import - kategorien som skal angis etter at utgivelsen er lastet ned og importert. Vær oppmerksom på at dette bryter med fjerning av fullførte nedlastinger.
- Nylig prioritet - nedlastingsklientprioritet for nylig utgitte medier
- Eldre prioritet - nedlastingsklientprioritet for medier som ikke nylig er utgitt
- Innledende tilstand - Innledende tilstand for torrenter (kun Qbittorrent: Tvinger forbi alle seed-grenser)
- (Avansert alternativ) Klientprioritet - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet og 50 er laveste prioritet
- Håndtering av fullførte nedlastinger
  - Fjern (Per klientinnstilling) - Fjern fullførte nedlastinger når de er ferdige (usenet) eller stoppet/fullført (torrenter). Se [Fullførte nedlastingshåndtering for mer informasjon](#fullførte-nedlastingshåndtering)
    - For torrenter krever dette at nedlastingsklienten din pauser når seed-målene er nådd. Det krever også at seed-målene støttes av Sonarr i henhold til tabellen nedenfor. Torrenter må også være i samme kategori.

### Kompatibilitet for fjerning av nedlastinger i torrentklienter

- Sonarr kan bare angi forhold eller tid for klienter som støtter å angi denne verdien via API-en deres når torrenten legges til. Seed-mål kan settes globalt i klienten selv eller per tracker i \*Arr-innstillingene for hver indekser. Se tabellen nedenfor for kompatibilitet med klienter.

|      Klient       |                                Forhold                                |                                   Tid                                    |
| :---------------: | :------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|      Deluge       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
| Download Station  | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|       Flood       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     Hadouken      | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|    qBittorrent    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     rTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
| Torrent Blackhole | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|   Transmission    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   | ![Idle-grense](https://img.shields.io/badge/Støttet-Idle%20grense*-blue) |
|     uTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|       Vuze        |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |

> ![Idle-grense](https://img.shields.io/badge/Støttet-Idle%20grense*-blue) - Transmission har internt en sjekk for ledig tid, men Sonarr sammenligner den med seedetiden hvis lediggrensen er satt per torrent. Dette gjøres som en løsning på Transmission's API-begrensninger.{.is-info}

## Fullførte nedlastingshåndtering

- Fullførte nedlastingshåndtering er hvordan Sonarr importerer medier fra nedlastingsklienten din til seriemappene dine. Mange vanlige problemer er relatert til dårlige Docker-stier og/eller andre Docker-tilgangsproblemer.

- (Avansert global innstilling) Aktiver - Importer fullførte nedlastinger automatisk fra nedlastingsklienten
- (Per klientinnstilling) Fjern - Fjern fullførte nedlastinger når de er ferdige (usenet) eller stoppet/fullført (torrenter)
  - For torrenter krever dette at nedlastingsklienten din pauser når seed-målene er nådd. Det krever også at seed-målene støttes av Sonarr i henhold til tabellen ovenfor. Torrenter må også være i samme kategori.

### Fjern fullførte nedlastinger

- Sonarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
- Sonarr vil overvåke dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Sonarr kjenne den endelige filplasseringen som rapporteres av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din.
- Sonarr vil skanne denne fullførte filplasseringen etter videofiler. Den vil analysere videofilnavnet for å matche det med en episode. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den angitte bibliotekmappen.
- Gjenværende filer fra nedlastingen vil bli sendt til papirkurven eller resirkuleringen.

Hvis du laster ned ved hjelp av en BitTorrent-klient, er prosessen litt annerledes:

- Fullførte filer blir liggende på sin opprinnelige plassering for å tillate seeding. Når filene importeres til den angitte bibliotekmappen, vil Sonarr forsøke å opprette en hardlenke til filen eller kopiere den (bruk dobbelt plass) hvis hardlenker ikke støttes.
- Hvis alternativet "Fullførte nedlastingshåndtering - Fjern" er aktivert i innstillingene, vil Sonarr be torrentklienten om å slette den opprinnelige filen og torrenten, men dette vil bare skje hvis klienten rapporterer at seeding er fullført, torrenten er i samme kategori (dvs. ikke bruker en post-import kategori), seed-målet som er nådd støttes av Sonarr, og torrenten er pauset (stoppet).

### Håndtering av mislykkede nedlastinger

- Håndtering av mislykkede nedlastinger er bare kompatibel med SABnzbd og NZBGet.
- Håndtering av mislykkede nedlastinger gjelder ikke for torrenter, og det er heller ingen planer om å legge til en slik funksjonalitet.

- Det er flere komponenter som utgjør prosessen for håndtering av mislykkede nedlastinger:

- Sjekk nedlaster:
  - Kø - Sjekk nedlasterens kø for passordbeskyttede (krypterte) utgivelser som er merket som mislykket
  - Historikk - Sjekk nedlasterens historikk for mislykkede nedlastinger (f.eks. ikke nok blokker for reparasjon, eller utpakking mislyktes)
- Når Sonarr finner en mislykket nedlasting, starter den behandlingen og gjør noen ting:
  - Legger til en mislykket hendelse i Sonarrs historikk
  - Fjerner den mislykkede nedlastingen fra nedlastingsklienten for å frigjøre plass og fjerne nedlastede filer (valgfritt)
  - Begynner å søke etter en erstatningsfil (valgfritt)
  - Blokkeringsliste (tidligere kjent som 'Blacklisting') tillater automatisk hopping over nzbs når de mislykkes, dette betyr at nzb-en ikke vil bli lastet ned automatisk av Sonarr igjen (du kan fortsatt tvinge nedlastingen via et manuelt søk).
  - Det er 2 avanserte alternativer (på siden for 'Nedlastingsklient'-innstillinger) som kontrollerer oppførselen til mislykkede nedlastinger i Sonarr, for øyeblikket er de alle aktivert som standard.

- Last ned på nytt - Kontrollerer om Sonarr skal søke etter samme fil etter en feil
- (Avansert alternativ) Fjern - Om nedlastingen automatisk skal fjernes fra nedlastingsklienten når feilen oppdages

## Eksterne stiavbildninger

- Eksterne stiavbildninger fungerer som en enkel finn fjernsti og erstatt med lokal sti. Dette brukes primært for enten sammenslåtte lokale/fjernoppsett ved bruk av mergerfs eller lignende, eller når applikasjonen og nedlastingsklienten ikke er på samme server.
- En ekstern stiavbildning brukes når nedlastingsklienten din rapporterer en sti for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er en ekstern stiavbildning bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows eller omvendt. En ekstern stiavbildning kan også være nødvendig hvis du blander Docker- og Native-klienter, eller hvis du bruker en ekstern server.
- En ekstern stiavbildning er en ENKEL søk/erstatt (der den finner VERDIEN FOR FJERNSTI, erstatt den med VERDIEN FOR LOKAL STI for den angitte verten).
- Hvis feilmeldingen om en ugyldig sti ikke inneholder VERDIEN SOM ER ERSTATTET, fungerer ikke stiavbildningen som forventet. Den vanlige løsningen er å legge til og fjerne avbildningen.
- [Se TRaSH's veiledning for mer informasjon om eksterne stiavbildninger](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-containere, er det sjelden behov for en ekstern stiavbildning. Det anbefales å [gjennomgå Docker-guiden](/docker-guide) og/eller [følge TRaSH's veiledning](https://trash-guides.info/hardlinks){.is-info}

# Importlister

> Informasjon om støttede listetyper finner du på siden [Mer informasjon (Støttet)](/sonarr/supported#lists) for denne delen
{.is-info}

## Lister

- Importlister er en del av Sonarr som lar deg følge en bestemt listeoppretter. La oss si at du følger en bestemt listeoppretter på Trakt/TMDb og virkelig liker deres ArrowVerse Collection-seksjon og ønsker å se alle showene på listen deres. Du ser i Sonarr og innser at du ikke har disse seriene. I stedet for å søke etter dem en etter en og legge dem til og deretter søke etter dem på indekserne dine. Du kan gjøre alt dette på en gang med en liste. Listene kan settes til å importere alle seriene på den kuratorens liste, samt automatisk tilordne en kvalitetsprofil, automatisk legge til og automatisk overvåke den serien.

- ADVARSEL: Hvis lister gjøres feil, vil de absolutt ødelegge biblioteket ditt med en haug med søppel du ikke har til hensikt å se. Så vær sikker på hva du importerer før du klikker lagre. Dvs. se på listen fysisk før du i det hele tatt går til Sonarr.

- Her kan du velge <kb>+</kb>-knappen for å åpne et nytt popup-vindu
- Fra dette nye vinduet får du mange forskjellige alternativer for å sette opp listen din fra mange forskjellige listeleverandører. Som nevnt tidligere, vær forsiktig med lister. Det anbefales på det sterkeste å ikke velge "Søk ved legging til"-knappen før du er helt sikker på at listen du velger/oppsetter legger til seriene du leter etter.
- Når du har valgt listeleverandøren du ønsker å hente fra (for eksempel IMDb eller Trakt), vil du få opp et nytt vindu.
De fleste innstillingene for lister er ganske selvforklarende, noen lister krever at du autentiserer deg med leverandøren, for eksempel Trakt (som krever at du har en konto med Trakt.tv)

- Importer ekskludering - Dette lar deg fjerne serier fra listen din som du ikke ønsker å se igjen. Et eksempel på dette er hvis listen din tilfeldigvis inneholder en serie på et fremmed språk som du ikke sannsynligvis vil finne på ditt eget språk og ikke ønsker å se den med undertekster. Du kan ekskludere en serie fra å bli lagt til i fremtiden. Imidlertid kan du legge den tilbake i ekskluderingslisten slik at når listen kjører igjen, vil den bli lest inn i biblioteket ditt.

# Koble til

> Informasjon om støttede tilkoblingstyper finner du på siden [Mer informasjon (Støttet)](/sonarr/supported#notifications) for denne delen
{.is-info}

## Tilkoblinger

- Tilkoblinger er hvordan du ønsker at Sonarr skal kommunisere med omverdenen.

- Ved å trykke på <kb>+</kb>-knappen vil du få opp et nytt vindu som lar deg konfigurere mange forskjellige endepunkter.

- En liste over støttede varsler og tilkoblinger finnes på siden [Mer informasjon (Støttet)](/sonarr/supported#notifications)

## Tilkoblingstriggere

- Ved nedlasting - Få varsel når episoder er tilgjengelige for nedlasting og har blitt sendt til en nedlastingsklient.
- Ved import - {Tidligere kjent som Ved nedlasting} Få varsel når episoder er importert.
- Ved oppgradering - Få varsel når episoder oppgraderes til bedre kvalitet.
- Ved omdøping - Få varsel når episoder blir omdøpt.
- Ved sletting av serie - Få varsel når serier blir slettet.
- Ved sletting av fil for episode - Få varsel når filer for episoder blir slettet.
- Ved sletting av fil for oppgradering - Få varsel når filer for episoder blir slettet for oppgraderinger.
- Ved helseproblem - Få varsel ved helsekontrollfeil.
  - Inkluder helseadvarsler - Få varsel om helseadvarsler i tillegg til feil.
- Ved oppdatering av program - Få varsel når Sonarr blir oppdatert til en ny versjon.

# Metadata

## Metadata

> Informasjon om støttede metadataforbrukere finner du på siden [Mer informasjon (Støttet)](/sonarr/supported#metadata) for denne delen
{.is-info}

- Her kan du velge hvilken type metadata som skal brukes av mediespilleren din.

- Kodi vil være en av de mest brukte alternativene her hvis det er programvaren som brukes. Dette vil tillate Sonarr å opprette en NFO-fil samt tilhørende filmpostere som kan hentes inn i spilleren din.

# Merker

- Merkedelen i Sonarr brukes til å koble forskjellige aspekter av Sonarr sammen.
- Merker er spesielt nyttige for:
  - Forsinkelsesprofiler
  - Utgivelsesprofiler
  - Indekser
- Merker kan brukes til å koble sammen forsinkelsesprofiler, utgivelsesprofiler, indekser og serier.
- For eksempel:
  - Du vil bare at en bestemt indekser skal brukes for en bestemt serie. Du ville opprette et merke og tilordne serien og indeksen til det merket.
  - Du vil at en bestemt utgivelsesprofil bare skal bruke en bestemt forsinkelsesprofil. Du ville opprette et merke og tilordne utgivelsesprofilen og forsinkelsesprofilen til det merket.

> En serie vil bruke både indekser som har matchende merker og indekser som ikke har merker.
{.is-warning}

> Merk: Merker påvirker ikke "Må inneholde", "Må ikke inneholde", "Foretrukket" ord eller noen andre aspekter som ikke er nevnt ovenfor.
{.is-info}

# Generelt

## Vert

- Bind-adresse - Gyldig IPv4-adresse eller '*' for alle grensesnitt
  - 0.0.0.0 eller `*` - alle adresser kan koble til
  - 127.0.0.1 eller localhost - bare lokalapplikasjoner kan koble til
  - En annen IP (f.eks. 1.2.3.4) - bare den IP-adressen (1.2.3.4) kan koble til
- Portnummer - Portnummeret du ønsker å bruke for å få tilgang til Sonarrs webgrensesnitt

> Merk: Hvis du bruker Docker, ikke endre denne innstillingen.
{.is-warning}

- URL-base - For støtte for omvendt proxy, standard er tom

> Merk: Hvis du bruker en omvendt proxy (for eksempel: mittområde.com/sonarr) skriver du inn '/sonarr' for URL-base.
{.is-info}

- Instansnavn - Instansnavn i fane og for Syslog-programnavn

> Hvis du kjører flere instanser, vil dette legge til instansnavnet i nettleserens fane. {.is-info}

- Aktiver SSL - Hvis du har SSL-sertifikater og ønsker å sikre kommunikasjonen til og fra Sonarr, aktiver dette alternativet.

> Merk: Ikke bruk dette med mindre du vet hva du gjør.
{.is-warning}

## Sikkerhet

- Autentisering - Hvordan ønsker du å autentisere for å få tilgang til Sonarr-instansen din
  - Ingen - Du har ingen autentisering for å få tilgang til Sonarr. Dette er vanligvis tilfelle hvis du er den eneste brukeren på nettverket ditt, ikke har noen på nettverket ditt som vil ha tilgang til Sonarr eller hvis Sonarr ikke er eksponert for nettet.
  - Grunnleggende (nettleser-popup) - Dette alternativet viser en liten popup når du får tilgang til Sonarr, som lar deg skrive inn brukernavn og passord.
  - Skjema (påloggingside) - Dette alternativet har en kjent påloggingside som ligner på andre nettsteder, som lar deg logge på Sonarr.
- API-nøkkel - Dette er hvordan andre programmer vil kommunisere eller la Sonarr kommunisere med andre programmer. Hvis denne nøkkelen gis til feil person med tilgang, kan det gjøres alle slags ting med biblioteket ditt. Derfor er API-nøkkelen sladdet i loggene.
- Sertifikatvalidering - Endre hvor streng HTTPS-sertifikatvalidering er
  - Aktivert - Valider alle HTTPS-sertifikater (anbefalt)
  - Deaktivert for lokale adresser - Valider alle HTTPS-sertifikater unntatt de på localhost og LAN
  - Deaktivert - Ikke valider noen HTTPS-sertifikater

## Proxy

- Proxy - Dette alternativet lar deg kjøre informasjonen Sonarr henter og søker gjennom en proxy. Dette kan være nyttig hvis du er i et land som ikke tillater nedlasting av torrentfiler.

- Bruk proxy - Aktiver for å bruke en proxy
- Proxytype - Velg proxytype (HTTPS, Socks4 eller Socks5)
- Vertsnavn - Skriv inn proxyvertsnavnet ditt (Ikke inkluder http/https eller noen annen protokoll)
- Port - Skriv inn proxyporten din
- Brukernavn - Skriv inn proxybrukernavnet ditt hvis aktuelt
- Passord - Skriv inn proxypassordet ditt hvis aktuelt
- Ignorerte adresser - Skriv inn en kommaseparert liste over adresser som skal omgå proxyen
- Omgå proxy for lokale adresser - Merk av for å omgå proxyen for lokale adresser. Lokale forespørsler identifiseres ved mangelen på en periode (.) i URI-en, som i <http://webserver/>, eller ved å få tilgang til den lokale serveren, inkludert <http://localhost>, <http://loopback> eller <http://127.0.0.1>. Når dette ikke er merket av, går alle internettforespørsler gjennom proxyserveren.

## Logging

- Loggnivå - Sannsynligvis et av de mest nyttige feilsøkingsverktøyene
  - Info - Dette er den mest grunnleggende måten Sonarr samler informasjon på. Denne loggfilen inneholder fatal, feil, advarsel og info-oppføringer.
  - Debug - Debug vil inkludere all informasjonen som Info inkluderer, pluss mer informasjon som kan være nyttig. Denne loggfilen inneholder fatal, feil, advarsel, info og debug-oppføringer.
  - Trace - Den mest avanserte og detaljerte loggingen på Sonarr. Trace vil inkludere all informasjon som er samlet inn av Info og Debug, og mer. Dette er den vanligste typen logg som blir bedt om ved feilsøking på Discord eller Reddit. Hvis du trenger hjelp, velg loggen din til Trace og gjenta oppgaven som ga deg problemer for å fange loggen. Denne loggfilen inneholder fatal, feil, advarsel, info, debug og trace-oppføringer.

## Analyse

- Analyse - Send anonym bruk og feilinformasjon til Sonarrs servere (SkyHook). Dette inkluderer informasjon om nettleseren din, hvilke Sonarr WebUI-sider du bruker, feilrapportering samt OS- og runtime-versjon. Vi vil bruke denne informasjonen til å prioritere funksjoner og feilretting.

## Oppdateringer

- (Avansert alternativ) Gren - Dette er grenen av Sonarr du kjører på.
  - [Se denne FAQ-posten for mer informasjon](/sonarr/faq#how-do-i-update-sonarr)
- Automatisk - Last ned og installer oppdateringer automatisk. Du vil fortsatt kunne installere fra System: Oppdateringer. Merk: Windows-brukere blir alltid oppdatert automatisk.
- Mekanisme - Bruk Sonarrs innebygde oppdaterer eller et skript
  - Innebygd - Bruk Sonarrs egen oppdaterer
  - Skript - La Sonarr kjøre oppdateringsskriptet
  - Docker - Ikke oppdater Sonarr fra innsiden av Docker, i stedet dra inn et helt nytt bilde med den nye oppdateringen
  - Apt - Satt av Debian/Ubuntu-pakken når oppdatering administreres eksklusivt via Apt
- Skript - Synlig bare når Mekanisme er satt til Skript - Sti til oppdateringsskript
- Oppdateringsprosess - Sonarr vil laste ned oppdateringsfilen, verifisere integriteten og pakke den ut til en midlertidig plassering og kalle den valgte metoden. Oppdateringsprosessen vil kjøres under samme bruker som Sonarr kjører under, den trenger tillatelser til å oppdatere Sonarr-filene samt stoppe/starte Sonarr.
- Innebygd - Den innebygde metoden vil sikkerhetskopiere Sonarr-filer og -innstillinger, stoppe Sonarr, oppdatere installasjonen og starte Sonarr. Hvis systemet ditt ikke takler å stoppe Sonarr og prøver å starte det på nytt automatisk, kan det være best å bruke et skript i stedet. Hvis oppdateringen mislykkes, vil forrige versjon av Sonarr bli startet på nytt.
- Skript - Skriptet skal håndtere det samme som den innebygde oppdatereren. Hvis du trenger å håndtere stopp og start av tjenester (upstart/launchd/etc), må du gjøre det her.

## Sikkerhetskopier

- Sikkerhetskopidelen lar deg fortelle Sonarr hvordan du vil håndtere sikkerhetskopier

- Mappe - Dette lar deg velge plasseringen for sikkerhetskopien. I Docker vil du være begrenset til hva du tillater at kontaineren skal se. Stier er relative til appdata-mappen; om nødvendig kan du angi en absolutt sti for å sikkerhetskopiere utenfor appdata-mappen.
- Intervall - Hvor ofte vil du at Sonarr skal lage en sikkerhetskopi
- Oppbevaring - Hvor lenge vil du at Sonarr skal beholde hver sikkerhetskopi. Etter at en ny sikkerhetskopi er opprettet, vil den eldste sikkerhetskopien bli fjernet.

# Brukergrensesnitt

## Kalender

- Første dag i uken - Her kan du velge hva du mener den første dagen i uken skal være.
- Ukekolonneoverskrift - Her kan du velge overskriften for kolonnene.

## Datoer

- Kort datoformat - Hvordan vil du at Sonarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du at Sonarr skal vise datoer i langt format?
- Tidsformat - Vil du ha et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du at Sonarr skal vise relative (I dag/I går/osv.) eller absolutte datoer?

## Stil

- Aktiver fargeblind modus - Endret stil for å gjøre det lettere for fargeblinde brukere å skille fargekodet informasjon