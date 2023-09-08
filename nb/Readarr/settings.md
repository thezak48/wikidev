---
title: Readarr Innstillinger
description: 
published: true
date: 2023-04-29T18:17:11.930Z
tags: readarr, innstillinger
editor: markdown
dateCreated: 2021-11-25T15:07:27.926Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [Menyalternativer](#menyalternativer)
- [Mediehåndtering](#mediehåndtering)
  - [Rotmapper](#rotmapper)
    - [Innstillinger for rotmappe](#innstillinger-for-rotmappe)
  - [Eksterne stiavbildinger](#eksterne-stiavbildinger)
  - [Bokfilnavngivelse](#bokfilnavngivelse)
  - [Boknavngivelse](#boknavngivelse)
    - [Standard bokformat](#standard-bokformat)
    - [Forfatter](#forfatter)
    - [Bok](#bok)
    - [Utgivelsesdato](#utgivelsesdato)
    - [Kvalitet](#kvalitet)
    - [Medieinformasjon](#medieinformasjon)
    - [Annet](#annet)
    - [Original](#original)
  - [Format for forfattermappe](#format-for-forfattermappe)
    - [Forfatter](#forfatter-1)
  - [Mapper](#mapper)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
- [Tillatelser](#tillatelser)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Metadataprofiler](#metadataprofiler)
  - [Utgivelsesprofiler](#utgivelsesprofiler)
  - [Forsinkelsesprofiler](#forsinkelsesprofiler)
    - [Bruk](#bruk)
    - [Hvordan forsinkelsesprofiler fungerer](#hvordan-forsinkelsesprofiler-fungerer)
      - [Eksempler](#eksempler)
        - [Eksempel 1](#eksempel-1)
        - [Eksempel 2](#eksempel-2)
        - [Eksempel 3](#eksempel-3)
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
  - [Prosesser for nedlastingsklient](#prosesser-for-nedlastingsklient)
    - [Usenet-prosess](#usenet-prosess)
    - [Torrent-prosess](#torrent-prosess)
  - [Nedlastingsklienter](#nedlastingsklienter-1)
    - [Støttede nedlastingsklienter](#støttede-nedlastingsklienter)
    - [Innstillinger for Usenet-klient](#innstillinger-for-usenet-klient)
    - [Innstillinger for torrent-klient](#innstillinger-for-torrent-klient)
    - [Kompatibilitet for fjerning av nedlasting i torrent-klient](#kompatibilitet-for-fjerning-av-nedlasting-i-torrent-klient)
  - [Håndtering av fullførte nedlastinger](#håndtering-av-fullførte-nedlastinger)
    - [Fjern fullførte nedlastinger](#fjern-fullførte-nedlastinger)
    - [Håndtering av mislykkede nedlastinger](#håndtering-av-mislykkede-nedlastinger)
  - [Eksterne stiavbildinger](#eksterne-stiavbildinger-1)
- [Importlister](#importlister)
  - [Importlister](#importlister-1)
  - [Ekskluderinger fra importliste](#ekskluderinger-fra-importliste)
  - [Legge til en importliste](#legge-til-en-importliste)
- [Koble til](#koble-til)
  - [Tilkoblinger](#tilkoblinger)
  - [Tilkoblingstriggere](#tilkoblingstriggere)
- [Metadata](#metadata)
  - [Calibre-metadata](#calibre-metadata)
  - [Skriv metadata til lydfiler](#skriv-metadata-til-lydfiler)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Vert](#vert)
  - [Sikkerhet](#sikkerhet)
  - [Proxy](#proxy)
  - [Logging](#logging)
  - [Analyse](#analyse)
  - [Oppdateringer](#oppdateringer)
  - [Oppdateringer](#oppdateringer-1)
  - [Sikkerhetskopier](#sikkerhetskopier)
- [UI (Brukergrensesnitt)](#ui-brukergrensesnitt)
  - [Kalender](#kalender)
  - [Datoer](#datoer)
  - [Stil](#stil)
  - [Språk](#språk)

Denne siden vil gå gjennom alle innstillingene som er tilgjengelige i Readarr og hvordan de fungerer. Dette er ikke ment å være en omfattende "hvordan sette opp Readarr". Hvis du ønsker det, kan du bruke siden [Rask start](/readarr/quick-start-guide) i stedet.

# Menyalternativer

For å komme til innstillingssiden, velg Innstillinger fra venstremenyen. Følgende undermenyalternativer vil være tilgjengelige:

![settings_1_menu.png](/assets/readarr/settings_1_menu.png)

Merk også at for hver enkelt innstillingsside er det noen alternativer øverst i menyen:

![settings_2_topmenu.png](/assets/readarr/settings_2_topmenu.png)

- Skjul/Vis avansert er viktig for alle elementer som er merket nedenfor som `(Avansert alternativ)`, ellers vil de ikke vises. Disse menyelementene vises i oransje på skjermbildene.

- Du må lagre endringene før du forlater skjermen. Dette gjør du ved å klikke på diskikonet. Hvis du ikke har gjort noen endringer, vil det stå "Ingen endringer" og være grået ut, som vist ovenfor.

# Mediehåndtering

> Noen av disse innstillingene er bare synlige via `Vis avanserte innstillinger`, som er øverst i menylinjen under søkefeltet{.is-info}

## Rotmapper

- En liste over konfigurerte rotmapper (biblioteksmapper) vises.
- Klikk på <kb>+</kb>-knappen for å legge til en ny rotmappe, eller klikk på et eksisterende kort for å redigere det.

### Innstillinger for rotmappe

- Navn - Navnet på rotmappen for brukergrensesnittet
- Sti - Mappen som inneholder bokbiblioteket ditt, dvs. destinasjonen slik Readarr ser det.
  - Merk at dette må være forskjellig fra plasseringen der nedlastingsklienten plasserer filene.
  - Hvis du bruker Docker og Calibre-integrasjon, må monteringene være de samme som for bokmappen din.

{#calibre}

- Spesifikke innstillinger for Calibre (bare hvis bruk av Calibre er aktivert)
  - Bruk Calibre - Aktiver/deaktiver bruk av Calibre Content Server for å administrere rotmappen din.

> \* Merk at dette **ikke kan aktiveres for en eksisterende rotmappe**.
> \* Merk at dette **ikke kan deaktiveres for en eksisterende rotmappe som bruker Calibre**.
> \* Merk at dette krever **Calibre Content Server** og fungerer ikke med Calibre Web eller Calibre.
> \* Merk at hardlinker ikke fungerer med Calibre-integrasjon.
> \* Merk at dette krever at Calibre har aktivert "Krev brukernavn og passord for å få tilgang til innholdsserveren".
> \* Hvis "Krev brukernavn og passord for å få tilgang til innholdsserveren" ikke er aktivert i Calibre, vil det føre til en feil med meldingen "Anonyme brukere har ikke tillatelse til å gjøre endringer".
{.is-warning}

- Calibre-vert - IP/domene til verten for Calibre Content Server
- Calibre-port - Porten som Calibre Content Server lytter på
- (Avansert) Calibre URL-base - Legg til et prefiks i Calibre-URL-en, f.eks. `http://[vert]:[port]/[urlBase]`
- Calibre-brukernavn - Brukernavn for å få tilgang til Calibre Content Server
- Calibre-passord - Passord for å få tilgang til Calibre Content Server
- Calibre-bibliotek - Navn på Calibre Content Server-biblioteket. La stå tomt for standardverdi
- Konverter til format - (Valgfritt) Be Calibre Content Server om å konvertere til andre formater med en kommaseparert liste.
  - Se (i)-ikonet i appen for en oppdatert liste over alternativer.
  - Alternativer er: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-utdataprofil - Velg utdataprofilen for Calibre Content Server som skal brukes
  - Utdataprofilen forteller Calibre Content Server-konverteringssystemet hvordan dokumentet skal optimaliseres for den angitte enheten (for eksempel ved å endre størrelsen på bilder for enhetens skjermstørrelse). I noen tilfeller kan en utdataprofil brukes til å optimalisere utdataen for en bestemt enhet, men dette er sjelden nødvendig.
- Bruk SSL - Aktiver eller deaktiver bruk av SSL (HTTPS) for Calibre Content Server
- Overvåking - Konfigurer overvåkingsalternativene for bøker som oppdages i denne mappen
  - Alle bøker - Overvåk alle bøker
  - Fremtidige bøker - Overvåk bøker som ikke er utgitt ennå
  - Manglende bøker - Overvåk bøker som ikke har filer eller ikke er utgitt ennå
  - Eksisterende bøker - Overvåk bøker som har filer eller ikke er utgitt ennå
  - Første bok - Overvåk den første boken. Alle andre bøker vil bli ignorert
  - Siste bok - Overvåk den siste boken og fremtidige bøker
  - Ingen - Ingen bøker vil bli overvåket med mindre de legges til eksplisitt
- Kvalitetsprofil - Standard kvalitetsprofil for bøker og forfattere som oppdages i denne mappen
- Metadataprofil - Velg metadataprofilen som skal brukes for forfattere som oppdages i denne mappen. Velg Ingen for å bare laste inn bøker som ble lagt til eller oppdaget eksplisitt.
- Standard Readarr-tagger - Standardtagger for forfattere som oppdages i denne mappen

> Brukere som ikke bruker Windows:
> \* Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
> \* Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.
{.is-warning}

## Eksterne stiavbildinger

- Ekstern stiavbilding fungerer som en enkel søk-og-erstatt for ekstern sti og lokal sti. Dette brukes primært for sammenslåtte lokale/eksterne oppsett ved bruk av mergerfs eller lignende, eller når applikasjonen og nedlastingsklienten eller Calibre ikke er på samme server.
- For mer informasjon, se avsnittet i [Nedlastingsklienter => Eksterne stiavbildinger](#eksterne-stiavbildinger-1) erstatt `<Nedlastingsklient>` med `<Calibre>`

## Bokfilnavngivelse

![bookfilenaming.png](/assets/readarr/bookfilenaming.png)

**Hvis du bruker Calibre-integrasjon, får du ikke navngi bokfiler. Calibre tar seg av dette for deg. Du bør bare endre disse innstillingene hvis du ikke bruker Calibre.**

> Vær oppmerksom på at mens Readarr er i beta; hvis du bruker Calibre, anbefales det å deaktivere navngivelse i Readarr i tilfelle det skulle oppstå en utilsiktet feil. {.is-info}

Vanlig brukte navneskjemaer er:

- Standard bokformat
  - `{Boktittel}\{Forfatternavn}` - `{Boktittel}` som deretter vil gi en mappe med navnet `Cujo`, og en undermappe som inneholder en fil med navnet `Stephen King - Cujo.m4b`

- Format for forfattermappe
  - `{Forfatternavn}` som deretter vil gi: `Stephen King`

## Boknavngivelse

- Gi nytt navn til bøker - Hvis dette er slått av (ingen hake i boksen), vil Readarr bruke det eksisterende filnavnet hvis navngivelse er deaktivert.
  - Hvis ikke haket av:
    - Import fra nedlastingsklient
      - Nedlastingsklientens utgivelsestittel brukes
    - Manuell (ad hoc) import: Opprinnelig filnavn

> Hvis du lar "Gi nytt navn til bøker" være uavkrysset, gjelder ingen av navngivelsene nedenfor - du har fortalt Readarr at du ikke ønsker noen navngivelse i det hele tatt. Boken vil bli importert direkte til forfattermappen. {.is-info}

> Dette gjelder ikke hvis Calibre brukes, da Calibre håndterer fil-/mappenavn ved hjelp av sitt eget interne skjema. {.is-info}

- Erstatt ulovlige tegn - Hvis dette er deaktivert, vil Readarr fjerne ulovlige tegn. Hvis det er aktivert, vil Readarr erstatte ulovlige tegn. Eksempler inkluderer `\ # / $ * < >` og mer.

### Standard bokformat

- Velg navngivelsen

- Rullegardinmeny (øverst til høyre)
  - Venstre boks - Håndtering av mellomrom
    - `Mellomrom ( )` - Bruk mellomrom i navngivelsen (standard)
    - `Punktum (.)` - Bruk punktum i stedet for mellomrom i navngivelsen
    - `Understrek (_)` - Bruk understrek i stedet for mellomrom i navngivelsen
    - `Bindestrek (-)` - Bruk bindestrek i stedet for mellomrom i navngivelsen
  - Høyre boks - Håndtering av store og små bokstaver
    - `Standardstørrelse` - Gjør tittelen stor og liten (~camel-case) (standard)
    - `Store bokstaver` - Gjør tittelen helt stor
    - `Små bokstaver` - Gjør tittelen helt liten

### Forfatter

- `{Forfatternavn}` = Forfatterens navn
- `{ForfatternavnThe}` = Forfatterens navn, The
- `{ForfatterCleanName}` = Forfatterens navn
- `{ForfatterSortName}` = Navn, Forfatter
- `{ForfatterDisambiguation}` = Forfatternavn (disambiguering brukt fra GoodReads for flere forfattere med samme navn)

### Bok

- `{Boktittel}` = Bokens tittel!: Undertittel!
- `{BoktittelThe}` = Bokens tittel!, The: Undertittel!
- `{BokCleanTitle}` = Bokens tittel: Undertittel
- `{BoktittelNoSub}` = Bokens tittel!
- `{BoktittelTheNoSub}` = Bokens tittel!, The
- `{BokCleanTitleNoSub}` = Bokens tittel
- `{BokUndertittel}` = Undertittel!
- `{BokUndertittelThe}` Undertittel!, The
- `{BokCleanUndertittel}` = Undertittel
- `{BokDisambiguation}` = Boktittel! (disambigueringstittel brukt fra GoodReads)
- `{Bokserie}` = Serietittel
- `{Bokserieposisjon}` = 1
- `{Bokserieposisjon}` = Serietittel #1
- `{Delnummer:0}` eller `{Delnummer:0}` = 2
- `{Delnummer:00}` = 02
- `{Delantall}` eller `{Delantall:0} = 9
- `{Delantall:00}` = 09

### Utgivelsesdato

- `{Utgivelsesår}` = 2016
- `{UtgivelsesårFørst}` = 2015
- `{Utgaveår}` = 2016

### Kvalitet

- `{KvalitetFull}` = AZW3 Riktig
- `{KvalitetTittel}` = AZW3

### Medieinformasjon

- `{MedieInfoLydformat}` = MP3
- `{MedieInfoLydkanaler}` = 2.0
- `{MedieInfoLydbitrate}` = 320kbps
- `{MedieInfoLydbitdybde}` = 24bit
- `{MedieInfoLydprøvefrekvens}` = 44.1kHz

### Annet

- `{Utgivelsesgruppe}` = Rls Grp
- `{Foretrukne ord}` = iNTERNAL

### Original

- `{Opprinnelig tittel}` = Forfatter.Navn.Bok.Navn.2018.AZW3-EVOLVE
- `{Opprinnelig filnavn}` = 01-boknavn

> Opprinnelig filnavn anbefales ikke. Det er det bokstavelige opprinnelige filnavnet og kan være obfuskert t1i0p3s7i8yuti. Opprinnelig tittel er utgivelsesnavnet og bør brukes i stedet. {.is-info}
  
## Format for forfattermappe

- (Avansert alternativ) Dette er der du setter navnekonvensjonen for navnet på forfattermappen.

> Dette gjelder ikke hvis Calibre brukes, da Calibre håndterer fil-/mappenavn ved hjelp av sitt eget interne skjema. {.is-info}

### Forfatter

- `{Forfatternavn}` = Forfatterens navn
- `{ForfatternavnThe}` = Forfatterens navn, The
- `{ForfatterCleanName}` = Forfatterens navn
- `{ForfatterSortName}` = Navn, Forfatter
- `{ForfatterDisambiguation}` = Forfatternavn (disambiguering brukt fra GoodReads for flere forfattere med samme navn)

## Mapper
  
![mm_folders.png](/assets/readarr/mm_folders.png)
  
- (Avansert alternativ) Opprett tomme forfattermapper - Velg boksen for å opprette tomme forfattermapper når en ny forfatter legges til.
- (Avansert alternativ) Slett tomme forfattermapper - Velg boksen for å slette tomme forfattermapper hvis det ikke er noen bøker i dem.
  
> En av disse boksene kan være merket av, men de bør ikke BEGGE være merket av. {.is-warning}

> Dette gjelder ikke hvis Calibre brukes, da Calibre håndterer fil-/mappenavn ved hjelp av sitt eget interne skjema. {.is-info}



## Importering
  
![mm_importing.png](/assets/readarr/mm_importing.png)
  
- (Avansert alternativ) Hopp over sjekk av ledig plass - Hvis aktivert, hopp over sjekk av ledig plass før importering
- (Avansert alternativ) Minimum ledig plass - Angi minimum ledig plass for stasjonen før importeringen stopper.
- (Avansert alternativ) Bruk hardlenker i stedet for kopiering - Merk av denne boksen for å bruke hardlenker i stedet for kopiering (for Torrents). Vær oppmerksom på at dette er aktivert som standard.
  
> Du bør ideelt sett bruke dette hvor det er mulig. For at hardlenker skal kunne brukes, må kilden/målet være på samme filsystem (stasjon, partisjon) og monteringspunkter. [Se TRaSH's Hardlink Guide for mer informasjon](https://trash-guides.info/hardlinks/)
  
- Importer ekstra filer - Hvis aktivert, importer spesifiserte ekstra filer som befinner seg i bokmappen når den importeres
- (Avansert alternativ) Importer ekstra filer - Hvis Importer ekstra filer er aktivert, skriv inn en kommaseparert liste over filtyper som skal importeres.

> Hvis du bruker Readarr for lydbøker, bør du legge til .cue i denne listen, da den inneholder kapittelinformasjonen din!
{.is-info}
  
## Filbehandling
  
  ![mm_filemgmt.png](/assets/readarr/mm_filemgmt.png)

- Ignorer slettede bøker - Merk av denne boksen for å ikke overvåke bøker som er oppdaget som slettet eller utilgjengelig fra Readarrs rotmappe.
- Last ned riktig og repacks - Om du automatisk skal oppgradere til riktig versjon/repakker. Bruk `Ikke foretrekk` for å sortere etter foretrukket ordpoeng over riktig/repakker
  - Foretrekk og oppgrader - Ranger repakker og riktig høyere enn ikke-repakker og ikke-riktig. Behandle nye repakker og riktig som oppgradering til gjeldende utgivelser.
  - Ikke oppgrader automatisk - Ranger repakker og riktig høyere enn ikke-repakker og ikke-riktig. Behandle ikke nye repakker og riktig som oppgradering til gjeldende utgivelser.
  - Ikke foretrekk - Ignorer repakker og riktig. Du må håndtere eventuelle preferanser for disse med [Foretrukne ord](#utgivelsesprofiler).
  
> \* `RIKTIG` - betyr at det var et problem med den forrige utgivelsen. Nedlastinger merket som RIKTIG viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som ikke ga ut originalen.
> \* `REPACK` - betyr at det var et problem med den forrige utgivelsen og er rettet opp av den opprinnelige gruppen. Nedlastinger merket som REPACK viser at problemene er løst i den utgivelsen. Dette er gjort av en gruppe som ga ut originalen.
{.is-info}

- (Avansert alternativ) Overvåk rotmapper for filendringer - Merk av denne boksen for å utløse en ny skanning når det oppdages endringer i rotmappen.
- (Avansert alternativ) Skann forfattermappe på nytt etter oppdatering - Velg når en forfattermappe skal skannes på nytt etter oppdatering av forfatteren.
  - Alltid - Dette vil skanne forfattermapper basert på oppgaveplanen
  - Etter manuell oppdatering - Du må manuelt skanne disken på nytt
  - Aldri - Akkurat som det står, aldri skanne forfattermapper på nytt.
- (Avansert alternativ) Tillat fingeravtrykk - Velg hvordan fingeravtrykk skal håndteres, noe som gir økt nøyaktighet for bokmatching, på bekostning av CPU/disktid.
  - Alltid - Bruk alltid fingeravtrykk hvis mulig
  - Kun for nye importeringer - Bruk bare fingeravtrykk på nyimporterte utgivelser
  - Aldri - Akkurat som det står, ikke bruk fingeravtrykk
- (Avansert alternativ) Endre filens dato - Endre filens dato ved import/skanning på nytt
  - Ingen - Readarr vil ikke endre datoen som vises i filutforskeren din
  - Bokutgivelsesdato - Datoen boken ble utgitt.
- (Avansert alternativ) Gjenvinningskurv - Bokfiler vil havne her når de slettes i stedet for å bli permanent slettet
- (Avansert alternativ) Rengjøring av gjenvinningskurv - Dette er hvor gammel en gitt fil kan være før den blir permanent slettet

> Det anbefales på det sterkeste å bruke en gjenvinningskurv. Det er enkelt å slette filer, og det er enkelt å gjenopprette dem hvis du bruker kurven.
{.is-warning}

# Tillatelser

- Sett tillatelser - Skal `chmod` kjøres når filer importeres/omdøpes?
  - chmod-mappen - Oktal, brukt under import/omdøping av mediamapper og filer (uten kjøretillatelser)

> Nedtrekksmenyen har en forhåndsdefinert liste over svært vanlig brukte tillatelser som kan brukes. Du kan imidlertid manuelt angi en oktal verdi for mappen hvis du ønsker det.
{.is-info}

> Dette fungerer bare hvis brukeren som kjører `Readarr` er eieren av filen. Det er bedre å sørge for at nedlastingsklienten setter tillatelsene riktig.
{.is-warning}

- chown-gruppe - Gruppenavn eller GID. Bruk GID for eksterne filsystemer

> Dette fungerer bare hvis brukeren som kjører `Readarr` er eieren av filen. Det er bedre å sørge for at nedlastingsklienten setter tillatelsene riktig.
{.is-warning}

# Profiler

## Kvalitetsprofiler

Kvalitetsprofiler brukes til å bestemme hvilke formater av bøker som er akseptable for en bok i biblioteket ditt.
  
![qualityprofile.png](/assets/readarr/qualityprofile.png)

- Sett profiler for kvaliteten på bøker du ønsker å laste ned.

> Når du velger en eksisterende profil eller legger til en ekstra profil, vises et nytt vindu
> Merk: Kvaliteten som har en blå boks, er kvaliteten som eventuelle medier med denne profilen vil fortsette å oppgraderes til.
{.is-info}

- Plusstegn (<kb>+</kb>) - Opprett en ny kvalitetsprofil

- Navn - Skriv inn et **UNIKT** navn for kvalitetsprofilen du oppretter
- Oppgraderinger tillatt - Når dette alternativet er merket av, og du ber Readarr om å laste ned en `EPUB` fordi det er den første utgivelsen av en bestemt bok, vil Readarr automatisk oppgradere til bedre kvalitet ***hvis*** `Oppgrader til` har den kvaliteten valgt
  - Oppgrader til - Når denne kvaliteten er nådd, vil ikke Readarr laste ned flere bøker

> Merk: Dette gjelder bare hvis du har `AZW3` høyere enn `EPUB` innenfor `Kvaliteter`-delen
{.is-warning}

- Kvaliteter - Kvaliteter som er høyere på listen, foretrekkes uavhengig av ønsket (aktivert/merket av) status. Kvaliteter innenfor samme gruppe er likeverdige. Bare merkede (aktiverte) kvaliteter er ønsket (tillatt)
  - Rediger grupper - Noen kvaliteter er gruppert sammen for å redusere størrelsen på listen, samt gruppere lignende utgivelser. Et godt eksempel på dette er `WebDL` og `WebRip`, da disse er veldig like og vanligvis har lignende bithastigheter. Når du redigerer gruppene, kan du endre preferansen innenfor hver av gruppene.

  - [Se Kvaliteter](#kvaliteter-definert)

> Som standard er kvalitetene satt fra "dårligst" (nederst) til "best" (øverst)
{.is-info}

## Metadataprofiler

Metadataprofiler brukes til å bestemme hvilke bøker fra GoodReads som skal legges til under en forfatter når en ny forfatter legges til.

- Plusstegn (<kb>+</kb>) - Opprett en ny metadataprofil

![metaprofiles.png](/assets/readarr/metaprofiles.png)
  
- Navn - Skriv inn et **UNIKT** navn for metadataprofilen
- Minimum popularitet - Skriv inn minimum popularitet for at en bok skal legges til for en forfatter.

> Hvis du setter dette for høyt, vil ikke bøker bli lagt til i Readarr, men hvis du setter det for lavt, vil obskure publikasjoner dukke opp.
{.is-warning}

> Sett dette til `10000000000` nøyaktig for å opprette en profil som tilsvarer `Ingen`, men som fortsatt tillater filtrering av utgaver og bøker. Merk at `Ingen` ikke bruker noen metadatafiltre, og du kan få utenlandske utgaver.
{.is-info}

- Minimum antall sider - Skriv inn det minste antallet sider en bok må ha for å bli lagt til for en forfatter.
- Hopp over bøker uten utgivelsesdato - Aktiver for å hoppe over bøker uten utgivelsesdato.
- Hopp over bøker uten ISBN eller ASIN - Aktiver for å hoppe over bøker som ikke inneholder enten et ISBN- eller ASIN-nummer.
- Hopp over delbøker og sett - Aktiver for å hoppe over delbøker og sett.
- Hopp over sekundære seriebøker - Aktiver for å hoppe over sekundære seriebøker.
- Tillatte språk - Skriv inn en kommaseparert liste over ISO 639-3-språkkoder, eller 'null' for tillatte språk for bøkene dine
- Må ikke inneholde - Skriv inn ord eller fraser som en boktittel ikke må inneholde for å bli lagt til.
  
> Du kan opprette flere metadataprofiler og bruke en separat profil for hver forfatter etter behov. Men du kan bare bruke en enkelt metadataprofil for en bestemt forfatter.
{.is-info}
  
## Utgivelsesprofiler

Utgivelsesprofiler brukes til å avgjøre om utgivelsesnavn fra indekseren kvalifiserer for nedlasting.

![releaseprofiles.png](/assets/readarr/releaseprofiles.png)  
  
- Aktiver profil - Merk av denne boksen for å aktivere denne profilen.
- Må inneholde - Legg til en liste over ord eller fraser som MÅ være i utgivelsesnavnet for å bli ansett som gyldig.
- Må ikke inneholde - Legg til en liste over ord eller fraser som IKKE skal være i utgivelsesnavnet for å bli ansett som gyldig.
- Foretrukket (ord) - Her kan du legge til vilkår eller regex med poeng (positive og negative) som skal anses som mer eller mindre foretrukne. For eksempel kan du foretrekke "uavkortet" med en positiv poengsum.
  
> Utgivelser med høyere poengsum for foretrukne ord enn den eksisterende filen er ALLTID en oppgradering!
{.is-info}
  
- Inkluder foretrukne ved omdøping - Merk av denne boksen for å inkludere dine foretrukne ord (eller regex-treff) i `{Foretrukne ord}`-filnavnsattributtet.
  
> Du bør inkludere `{Foretrukne ord}` i filnavnet ditt, og merk av denne boksen hvis du bruker dem, fordi du ellers kan havne i en nedlastingsløkke.
{.is-warning}

- Indekserer - I denne nedtrekksmenyen kan du begrense denne utgivelsesprofilen til en enkelt indekser. Denne bør nesten alltid stå på `(hvilken som helst)`
- Merker - Skriv inn et merke her, for å kunne bruke dette merket på forfattere med samme merke. Hvis du ikke bruker et merke her, gjelder denne profilen for ALLE forfattere.

## Forsinkelsesprofiler

- Forsinkelsesprofiler lar deg redusere antall utgivelser som blir lastet ned for en bok ved å legge til en forsinkelse mens Readarr fortsetter å overvåke utgivelser som bedre samsvarer med preferansene dine.
- Protokoll - Dette vil enten være `Usenet` eller `Torrent` avhengig av hvilken nedlastingsprotokoll du foretrekker
- Usenet-forsinkelse - Angi antall minutter du vil vente før nedlastingen starter
- Torrent-forsinkelse - Angi antall minutter du vil vente før nedlastingen starter
- Bypass hvis høyeste kvalitet - Bypass forsinkelsen når utgivelsen har den høyeste aktiverte kvalitetsprofilen med foretrukket protokoll
- Merker - Ved å gi denne forsinkelsesprofilen et merke, kan du merke en gitt bok for å få den til å følge reglene som er satt her.
- Skiftenøkkelikon - Dette lar deg redigere forsinkelsesprofilen
- Plusstegn (<kb>+</kb>) - Opprett en ny forsinkelsesprofil

### Bruksområder

Noen medier vil motta et halvt dusin forskjellige utgivelser av varierende kvalitet i timene etter en utgivelse, og uten forsinkelsesprofiler kan Readarr prøve å laste ned alle sammen. Med forsinkelsesprofiler kan Readarr konfigureres til å ignorere de første par timene med utgivelser.

Forsinkelsesprofiler er også nyttige hvis du vil legge vekt på en protokoll (Usenet eller BitTorrent) over den andre. (Se Eksempel 3)

### Hvordan forsinkelsesprofiler fungerer

Tidtakeren starter så snart Readarr oppdager at en bok har en tilgjengelig utgivelse. Denne utgivelsen vises i køen din med et klokkeikon for å indikere at den er under forsinkelse.

> Klokken starter fra utgivelsestidspunktet for utgivelsene og ikke fra tidspunktet Readarr ser dem. {.is-info}

I løpet av forsinkelsesperioden vil Readarr merke seg eventuelle nye utgivelser som blir tilgjengelige. Når forsinkelsestimeren utløper, vil Readarr laste ned den ene utgivelsen som best samsvarer med kvalitetspreferansene dine.

Tidsperioden kan være forskjellig for Usenet og Torrents. Hver profil kan være tilknyttet en eller flere merker for å tilpasse hvilke bøker som har hvilke profiler. En forsinkelsesprofil uten merke regnes som standard og gjelder for alle bøker som ikke har et spesifikt merke.

> Forsinkelsesprofiler starter fra tidspunktet indekseren rapporterer at utgivelsen ble lastet opp. Dette betyr at innhold som er eldre enn antall minutter du har satt, ikke påvirkes på noen måte av forsinkelsesprofilen din, og vil bli lastet ned umiddelbart. I tillegg vil **eventuelle manuelle søk** etter innhold (søk utenom RSS-feed) ignorere innstillingene for forsinkelsesprofilen.
{.is-warning}

#### Eksempler

- For hvert eksempel, anta at brukeren har følgende kvalitetsprofil aktiv: EPUB og høyere er tillatt MOBI er kvalitetsgrensen * AZW3 er den høyest rangerte kvaliteten

##### Eksempel 1

- I dette enkle eksempelet er profilen satt med en 120 minutters (to timers) forsinkelse for både Usenet og Torrent.

- Klokken 23:00 oppdager Readarr den første utgivelsen for en bok, og den ble lastet opp klokken 22:50, og 120 minutters klokke starter. Klokken 00:50 vil Readarr vurdere eventuelle utgivelser den har funnet i løpet av de siste to timene, og laste ned den beste, som er MOBI.

- Klokken 03:00 blir det funnet en annen utgivelse, som er MOBI og ble lagt til indekseren din klokken 02:46. En annen 120 minutters klokke starter. Klokken 04:46 blir den beste tilgjengelige utgivelsen lastet ned. Siden kvalitetsgrensen nå er nådd, kan ikke boken oppgraderes lenger, og Readarr slutter å lete etter nye utgivelser.

- På et hvilket som helst tidspunkt, hvis en AZW3-utgivelse blir funnet, vil den bli lastet ned umiddelbart fordi det er den høyest rangerte kvaliteten. Hvis det er en aktiv forsinkelsestimer, vil den bli kansellert.

##### Eksempel 2

- Dette eksempelet har forskjellige tidsur for Usenet og Torrents. Anta en 120 minutters timer for Usenet og en 180 minutters timer for BitTorrent.

- Klokken 23:00 oppdager Readarr den første utgivelsen for en bok, og begge timere starter. Utgivelsen ble lagt til indekseren klokken 22:15. Klokken 00:15 vil Readarr vurdere eventuelle utgivelser, og hvis det er noen akseptable Usenet-utgivelser, vil den beste bli lastet ned, og begge timere vil avsluttes. Hvis ikke, vil Readarr vente til 00:15 og laste ned den beste utgivelsen, uavhengig av hvilken kilde den kom fra.

##### Eksempel 3

- En vanlig bruk for forsinkelsesprofiler er å legge vekt på en protokoll over den andre. For eksempel kan du bare ønske å laste ned en BitTorrent-utgivelse hvis ingenting har blitt lastet opp til Usenet etter en viss tid.

- Du kan sette en 60 minutters timer for BitTorrent og en 0 minutters timer for Usenet.

- Hvis den første utgivelsen som oppdages, er fra Usenet, vil Readarr laste den ned umiddelbart.

- Hvis den første utgivelsen er fra BitTorrent, vil Readarr sette en 60 minutters timer. Hvis det blir oppdaget noen kvalifiserte Usenet-utgivelser i løpet av den tiden, vil BitTorrent-utgivelsen bli ignorert, og Usenet-utgivelsen vil bli lastet ned.

# Kvalitet

![qualitydefinitions.png](/assets/readarr/qualitydefinitions.png)

## Betydning av kvalitetstabell

- Kvalitet - Navnet på kvaliteten i scenen (hardkodet)
- Tittel - Navnet på kvaliteten i brukergrensesnittet (konfigurerbart)
- Megabyte per minutt - Selvforklarende
- Størrelsesgrense - Selvforklarende
- Min - Minimum antall byte eller kilobyte per sekund (b/s|kb/s) en kvalitet kan ha.
- Maks - Maksimum antall byte eller kilobyte per sekund (b/s|kb/s) en kvalitet kan ha.

## Definerte kvaliteter

- Ukjent tekst - Selvforklarende
- PDF - Portable Document File
- MOBI - En av de mest brukte ebokfilformatene
- EPUB - Et annet av de mest brukte ebokfilformatene
- AZW3 - AZW3 er en ebokfil som er utviklet av Amazon. Den brukes i Amazon Kindles for å vise ebøker.
- Ukjent lyd - Selvforklarende
- MP3 - Vanlig tapende lydformat
- M4B - Vanlig lydbokfilformat
- FLAC - Free Lossless Audio Codec, et lydformat som ligner på MP3, men tappest

# Indekserere

> Informasjon om støttede indekserere finner du på siden [Mer informasjon (Støttet)](/readarr/supported#indexers) for denne delen
{.is-info}

## Støttede indekserere

- En liste over støttede indekserere finnes på siden [Mer informasjon (Støttet)](/readarr/supported#indexers)

### Innstillinger for indekserere

- Når du har klikket på <kb>+</kb>-knappen for å legge til en ny indekserer, vil du bli presentert med et nytt vindu med mange forskjellige alternativer. For formålet med denne wikien anser Readarr både Usenet-indekserere og Torrent-sporere som "indekserere".

- Det er to seksjoner her: Usenet og Torrents. Basert på hvilken nedlastingsklient du vil bruke, vil du velge typen indekserer du vil gå for.

### Konfigurasjon av Usenet-indekserer

- Newznab - Her finner du forhåndsinnstillinger for populære Usenet-indeksider (som er forhåndsutfylt, alt du trenger er API-nøkkelen din som blir gitt av Usenet-indeksen du velger) sammen med muligheten til å opprette en tilpasset indeks.
- Programvare som fungerer med Usenet og integrerer godt med Readarr er [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr) som integrerer med både Usenet og Torrents.
- Uavhengig av om du velger en forhåndsutfylt indeks eller en tilpasset indeksoppsett, vil du bli presentert med et nytt vindu for å legge inn alle innstillingene dine.
- Velg mellom forhåndsinnstillingene eller legg til en tilpasset indeks (som NZBHydra2 eller Prowlarr).
- Navn - Navnet på indeksen i Readarr.
- Aktiver RSS - Hvis aktivert, bruk denne indeksen for å se etter filer som er ønsket og mangler eller som ennå ikke har nådd sin grense.
- Aktiver automatisk søk - Hvis aktivert, bruk denne indeksen for automatisk søk, inkludert søk ved tillegg.
- Aktiver interaktivt søk - Hvis aktivert, bruk denne indeksen for manuelle interaktive søk.
- URL - URL-en som indeksen gir, for eksempel `https://api.nzbgeek.info`.
- API-sti - Stien til API-en som indeksen gir. Dette er vanligvis `/api`.
- Flerspråklig - Angi hvilke språk `MULTI` som er tilgjengelige for denne indeksen.
- API-nøkkel - Nøkkelen som indeksen gir for å få tilgang til API-en.
- Kategorier - Standardkategorier vil bli brukt med mindre de blir redigert. Det er sannsynlig at disse standardkategoriene ikke er optimale. Når du redigerer denne innstillingen, spør Readarr indeksen om hvilke kategorier som er tilgjengelige og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir vekslet.
- (Avansert alternativ) Tidlig nedlastingsgrense - Tid før utgivelsesdato som Readarr vil laste ned fra denne indeksen, la være blank for ingen grense. Dette er lignende tilgjengelighet i Radarr.
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere for Newznab som skal legges til i spørringslenken.
- (Avansert alternativ) Indeksprioritet - Prioritet for denne indeksen for å foretrekke en indeks over en annen i situasjoner med lik utgivelse. 1 er høyeste prioritet og 50 er laveste prioritet.

### Konfigurasjon av torrent-sporere

- På samme måte som med Usenet er det en rekke forhåndsutfylte torrent-sporerinformasjon. Hvis du ikke er medlem av noen av disse spesifikke sporerne, vil de ikke være til nytte for deg.
- En av de enkleste måtene å bruke torrent-sporere med Readarr på er å bruke et annet program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Disse programmene fungerer godt med Readarr og fungerer som en søkeindeks som inneholder all informasjonen din og sender den til Readarr.
- Torznab - Dette alternativet vil sette deg opp med en Jackett-forhåndsinnstilling, hvis du bruker flere sporer, må hver oppføring ha et unikt navn.
- Torznab-indeks
- Velg mellom forhåndsinnstillingene eller legg til en tilpasset indeks (som Jackett).
- Navn - Navnet på indeksen i Readarr.
- Aktiver RSS - Hvis aktivert, bruk denne indeksen for å se etter filer som er ønsket og mangler eller som ennå ikke har nådd sin grense.
- Aktiver automatisk søk - Hvis aktivert, bruk denne indeksen for automatisk søk, inkludert søk ved tillegg.
- Aktiver interaktivt søk - Hvis aktivert, bruk denne indeksen for manuelle interaktive søk.
- URL - URL-en som indeksen gir, for eksempel `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sti - Stien til API-en som indeksen gir. Dette er vanligvis `/api`.
- API-nøkkel - Nøkkelen som indeksen gir for å få tilgang til API-en.
- Flerspråklig - Angi hvilke språk `MULTI` som er tilgjengelige for denne indeksen.
- Kategorier - Standardkategorier vil bli brukt med mindre de blir redigert. Det er sannsynlig at disse standardkategoriene ikke er optimale. Når du redigerer denne innstillingen, spør Readarr indeksen om hvilke kategorier som er tilgjengelige og viser dem i en valgbar liste. De utdaterte standardene vil fjernes så snart en kategori blir vekslet.
- (Avansert alternativ) Tidlig nedlastingsgrense - Tid før utgivelsesdato som Readarr vil laste ned fra denne indeksen, la være blank for ingen grense. Dette er lignende tilgjengelighet i Radarr.
- (Avansert alternativ) Tilleggsparametere - Tilleggsparametere for Newznab som skal legges til i spørringslenken.
- (Avansert alternativ) Indeksprioritet - Prioritet for denne indeksen for å foretrekke en indeks over en annen i situasjoner med lik utgivelse. 1 er høyeste prioritet og 50 er laveste prioritet.
- (Avansert alternativ) Minimum antall seedere - Minimum antall seedere som kreves for at en utgivelse fra denne sporeren skal bli lastet ned.
- (Avansert alternativ) Seedratio - Hvis tomt, bruker den standardverdien for nedlastingsklienten. Ellers er minimum seedratio som kreves for at nedlastingsklienten din skal oppfylle for utgivelser fra denne indeksen før den blir satt på pause av klienten din og fjernet av Readarr (krever aktivert håndtering av fullførte nedlastinger - fjern).
- (Avansert alternativ) Seedtid - Hvis tomt, bruker den standardverdien for nedlastingsklienten. Ellers er minimum seedtid i minutter som kreves for at nedlastingsklienten din skal oppfylle for utgivelser fra denne indeksen før den blir satt på pause av klienten din og fjernet av Readarr (krever aktivert håndtering av fullførte nedlastinger - fjern).
- (Avansert alternativ) Diskografiseedtid - Ignorer, overføres fra Lidarr.
- (Avansert alternativ) Indeksprioritet - Prioritet for denne indeksen for å foretrekke en indeks over en annen i situasjoner med lik utgivelse. 1 er høyeste prioritet og 50 er laveste prioritet.

## Alternativer

- Minimumsalder - Kun Usenet: Minimumsalder i minutter for NZB-er før de blir lastet ned. Bruk dette for å gi nye utgivelser tid til å spre seg til Usenet-leverandøren din.
- Oppbevaring - Kun Usenet: Sett til null for ubegrenset oppbevaring.
- Maksimal størrelse - Maksimal størrelse for en utgivelse som skal lastes ned i MB. Sett til null for ubegrenset. Vær oppmerksom på at dette gjelder globalt.
- RSS-synkroniseringsintervall - Intervall i minutter. Sett til null for å deaktivere (dette vil stoppe all automatisk nedlasting av utgivelser). Minimum: 10 minutter Maksimum: 120 minutter
  - Se [Hvordan finner Readarr bøker?](/readarr/faq#how-does-readarr-find-books) for en bedre forståelse av hvordan RSS-synkronisering vil hjelpe deg.

> Hvis Readarr har vært frakoblet i en lengre periode, vil Readarr forsøke å bla tilbake for å finne den siste utgivelsen den behandlet for å unngå å gå glipp av en utgivelse. Så lenge indeksen din støtter blading og det ikke har gått for lang tid, vil Readarr kunne behandle utgivelsene den ellers ville ha gått glipp av og unngå at du må søke etter de tapte utgivelsene.{.is-info}

# Nedlastingsklienter

> Informasjon om støttede nedlastingsklienter finner du på siden [Mer informasjon (Støttet)](/readarr/supported#download-clients) for denne delen
{.is-info}

## Oversikt

- Nedlasting og import er der de fleste opplever problemer. Fra et overordnet perspektiv må programvaren kunne kommunisere med nedlastingsklienten din og ha tilgang til filene den laster ned. Det er et stort utvalg av støttede nedlastingsklienter og en enda større variasjon i oppsett. Dette betyr at selv om det er noen vanlige oppsett, er det ikke ett riktig oppsett, og alle oppsett kan være litt forskjellige. Men det er mange feilaktige oppsett.

## Prosesser for nedlastingsklienter

### Usenet-prosess

- Readarr vil sende en nedlastingsforespørsel til klienten din og tilordne den med etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: bøker, tv, serier, musikk, osv.
- Readarr vil overvåke nedlastingsklientens aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Readarr kjenne den endelige filplasseringen som rapportert av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din og tilgjengelig for Readarr.
- Readarr vil skanne den fullførte filplasseringen etter filer som Readarr kan bruke. Den vil analysere filnavnet for å matche det med forespurt media. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til angitt medieplassering.
- Atomiske flyttinger (umiddelbare flyttinger) er aktivert som standard. Filsystemet og monteringspunktene må være de samme for den fullførte nedlastingsmappen og mediebiblioteket ditt. Hvis den atomiske flyttingen mislykkes eller oppsettet ditt ikke støtter hardlenker og atomiske flyttinger, vil Readarr falle tilbake og kopiere filen og deretter slette den fra kilden, noe som er I/O-intensivt.

### Torrent-prosess

- Readarr vil sende en nedlastingsforespørsel til klienten din og tilordne den med etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: bøker, tv, serier, musikk, osv.
- Readarr vil overvåke nedlastingsklientens aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Readarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil Readarr opprette en hardlenke til filen hvis det støttes av oppsettet ditt, eller kopiere den hvis hardlenker ikke støttes.
- Hardlenker er aktivert som standard. [En hardlenke vil ikke bruke noe ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for den fullførte nedlastingsmappen og mediebiblioteket ditt. Hvis opprettelsen av hardlenken mislykkes eller oppsettet ditt ikke støtter hardlenker, vil Readarr falle tilbake og kopiere filen.
- Hvis alternativet "Fullført nedlastingshåndtering - Fjern" er aktivert i Readarrs innstillinger, vil Readarr slette den opprinnelige filen og torrenten fra klienten din, men bare hvis klienten rapporterer at seeding er fullført og torrenten er stoppet.

## Nedlastingsklienter

Klikk på `Innstillinger => Nedlastingsklienter`, og klikk deretter på <kb>+</kb> for å legge til en ny nedlastingsklient. Nedlastingsklienten din bør allerede være konfigurert og kjøre.

### Støttede nedlastingsklienter

- En liste over støttede nedlastingsklienter finnes på siden [Mer informasjon (Støttet)](/readarr/supported#download-clients)

Velg nedlastingsklienten du ønsker å legge til, og det vil vises en popup-boks der du kan legge inn tilkoblingsdetaljer. Disse detaljene er like for de fleste klienter. Noen vil be om brukernavn eller passord, noen vil spørre om du vil legge til nye nedlastinger i en pauset/startet tilstand, osv.

### Innstillinger for Usenet-klient

- Navn - Navnet på nedlastingsklienten i Readarr.
- Aktiver - Aktiver denne nedlastingsklienten.
- Vert - URL-en til nedlastingsklienten din.
- Port - Porten til nedlastingsklienten din.
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- API-nøkkel - API-nøkkelen for å autentisere mot klienten din.
- Brukernavn - Brukernavnet for å autentisere mot klienten din (vanligvis ikke nødvendig).
- Passord - Passordet for å autentisere mot klienten din (vanligvis ikke nødvendig).
- Kategori - Kategorien innenfor nedlastingsklienten din som \*Arr vil bruke. For å unngå at urelaterte nedlastinger vises i Aktivitet, anbefales det sterkt å sette en kategori.
- Nylig prioritet - Nedlastingsklientprioritet for nylig utgitte medier.
- Eldre prioritet - Nedlastingsklientprioritet for medier som ikke nylig er utgitt.
- (Avansert alternativ) Klientprioritet - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet og 50 er laveste prioritet.

### Innstillinger for torrentklient

- Navn - Navnet på nedlastingsklienten i Readarr.
- Aktiver - Aktiver denne nedlastingsklienten.
- Vert - URL-en til nedlastingsklienten din.
- Port - Porten til nedlastingsklienten din; dette er vanligvis webgui-porten.
- Bruk SSL - Bruk en sikker tilkobling med nedlastingsklienten din. Vær oppmerksom på denne vanlige feilen.
- (Avansert alternativ) URL-base - Legg til et prefiks i URL-en; dette er vanligvis nødvendig for omvendte proxyer.
- Brukernavn - Brukernavnet for å autentisere mot klienten din.
- Passord - Passordet for å autentisere mot klienten din.
- Kategori - Kategorien innenfor nedlastingsklienten din som \*Arr vil bruke. For å unngå at urelaterte nedlastinger vises i Aktivitet, anbefales det sterkt å sette en kategori.
- Kategori etter import - Kategorien som skal settes etter at utgivelsen er lastet ned og importert. Vær oppmerksom på at dette bryter med fjerning av fullført nedlastingshåndtering.
- Nylig prioritet - Nedlastingsklientprioritet for nylig utgitte medier.
- Eldre prioritet - Nedlastingsklientprioritet for medier som ikke nylig er utgitt.
- Innledende tilstand - Innledende tilstand for torrents (kun Qbittorrent: Tvinger forbi alle seed-krav).
- (Avansert alternativ) Klientprioritet - Prioritet for nedlastingsklienten. Round-Robin brukes for klienter av samme type (torrent/usenet) som har samme prioritet. 1 er høyeste prioritet og 50 er laveste prioritet.

### Kompatibilitet for fjerning av nedlastinger for torrentklienter

- Readarr kan bare angi seedratio/tid på klienter som støtter å angi denne verdien via API-en når torrenten blir lagt til. Seedmål kan settes globalt i klienten selv eller per sporingsenhet i \*Arr-innstillingene for hver indeks. Se tabellen nedenfor for klientkompatibilitet.

|      Klient       |                                Ratio                                 |                                   Tid                                    |
| :---------------: | :------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|      Deluge       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
| Download Station  | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|       Flood       |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     Hadouken      | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|    qBittorrent    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|     rTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
| Torrent Blackhole | ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical) |   ![Ikke støttet](https://img.shields.io/badge/Støttet-Nei-critical)   |
|   Transmission    |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Støttet-Idle%20Limit*-blue) |
|     uTorrent      |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |
|       Vuze        |   ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)   |     ![Støttet](https://img.shields.io/badge/Støttet-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Støttet-Idle%20Limit*-blue) - Transmission har internt en sjekk for ledig tid, men Readarr sammenligner den med seedetiden hvis lediggrensen er satt for hver torrent. Dette gjøres som en løsning på Transmission's API-begrensninger.{.is-info}

## Håndtering av fullførte nedlastinger

- Håndtering av fullførte nedlastinger er hvordan Readarr importerer media fra nedlastingsklienten din til seriemappene dine. Mange vanlige problemer er relatert til dårlige Docker-stier og/eller andre Docker-tilgangsproblemer.

- Aktiver - Importer fullførte nedlastinger automatisk fra nedlastingsklienten
- (Avansert alternativ) Fjern - Fjern fullførte nedlastinger når de er ferdige (Usenet) eller stoppet/fullført (torrenter)

### Fjern fullførte nedlastinger

- Readarr vil sende en nedlastingsforespørsel til klienten din og knytte den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten.
- Readarr vil overvåke dine nedlastingsklienters aktive nedlastinger som bruker det kategorinavnet. Dette overvåkes via nedlastingsklientens API.
- Når nedlastingen er fullført, vil Readarr kjenne den endelige filplasseringen som rapportert av nedlastingsklienten din. Denne filplasseringen kan være nesten hvor som helst, så lenge den er et annet sted enn mediamappen din.
- Readarr vil skanne den fullførte filplasseringen for videofiler. Den vil analysere videofilnavnet for å matche det med en bok. Hvis den kan gjøre det, vil den omdøpe filen i henhold til dine spesifikasjoner og flytte den til den tildelte biblioteksmappen.
- Gjenværende filer fra nedlastingen vil bli sendt til papirkurven eller resirkuleringen din.

Hvis du laster ned ved hjelp av en BitTorrent-klient, er prosessen litt annerledes:

- Fullførte filer blir liggende på sin opprinnelige plassering for å tillate seeding. Når filene importeres til den tildelte biblioteksmappen, vil Readarr forsøke å opprette en hardlink til filen, eller falle tilbake til å kopiere (bruk dobbelt plass) hvis hardlinker ikke støttes.
- Hvis alternativet "Fullført nedlastingsbehandling - Fjern" er aktivert i innstillingene, vil Readarr be torrentklienten om å slette den opprinnelige filen og torrenten, men dette vil bare skje hvis klienten rapporterer at seeding er fullført, torrenten er i samme kategori (dvs. ikke bruker en post-importkategori), målet for seeding som støttes av Readarr er nådd, og torrenten er satt på pause (stoppet).

### Håndtering av mislykkede nedlastinger

- Håndtering av mislykkede nedlastinger er bare kompatibel med SABnzbd og NZBGet.
- Håndtering av mislykkede nedlastinger gjelder ikke for torrents, og det er ingen planer om å legge til en slik funksjonalitet.

- Det er flere komponenter som utgjør prosessen for håndtering av mislykkede nedlastinger:

- Sjekk nedlaster:
  - Kø - Sjekk nedlasterens kø for passordbeskyttede (krypterte) utgivelser som er merket som mislykket
  - Historikk - Sjekk nedlasterens historikk for mislykkede nedlastinger (f.eks. ikke nok til å reparere, eller utpakking mislyktes)
- Når Readarr finner en mislykket nedlasting, starter den behandlingen og gjør noen ting:
  - Legger til en mislykket hendelse i Readarrs historikk
  - Fjerner den mislykkede nedlastingen fra nedlastingsklienten for å frigjøre plass og fjerne nedlastede filer (valgfritt)
  - Starter søket etter en erstatningsfil (valgfritt)
  - Blokkeringsliste (tidligere kalt 'Blacklisting') tillater automatisk hopping over nzbs når de mislykkes, dette betyr at nzb aldri vil bli lastet ned automatisk av Readarr igjen (du kan fortsatt tvinge nedlastingen via et manuelt søk).
  - Det er 2 avanserte alternativer (på siden 'Nedlastingsklient' innstillinger) som kontrollerer oppførselen til mislykkede nedlastinger i Readarr, for øyeblikket er de alle på som standard.

- Last ned på nytt - Kontrollerer om Readarr skal søke etter samme fil etter en feil
- (Avansert alternativ) Fjern - Om nedlastingen automatisk skal fjernes fra nedlastingsklienten når feilen oppdages

## Eksterne stiavbildninger

- Eksterne stiavbildninger fungerer som en enkel finn ekstern sti og erstatt med lokal sti. Dette brukes primært for enten sammenslåtte lokale/eksterne oppsett ved hjelp av mergerfs eller lignende, eller når applikasjonen og nedlastingsklienten ikke er på samme server.
- En ekstern stiavbildning brukes når nedlastingsklienten din rapporterer en sti for fullførte data enten på en annen server eller på en måte som \*Arr ikke adresserer den mappen.
- Generelt sett er en ekstern stiavbildning bare nødvendig hvis nedlastingsklienten din kjører på Linux når \*Arr kjører på Windows, eller omvendt. En ekstern stiavbildning kan også være nødvendig hvis du blander Docker- og Native-klienter, eller hvis du bruker en ekstern server.
- En ekstern stiavbildning er en ENKEL søk/erstatt (hvor den finner VERDIEN FOR EKSTERN, erstatt den med VERDIEN FOR LOKAL for den angitte verten).
- Hvis feilmeldingen om en ugyldig sti ikke inneholder VERDIEN SOM ER ERSTATTET, fungerer ikke stiavbildningen som forventet. Den vanlige løsningen er å legge til og fjerne avbildningen.
- [Se TRaSH's veiledning for mer informasjon om ekstern stiavbildning](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og nedlastingsklienten din er Docker-containere, er det sjelden behov for en ekstern stiavbildning. Det anbefales at du [gjennomgår Docker-guiden](/docker-guide) og/eller [følger TRaSH's veiledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlister

> Informasjon om støttede listetyper finner du på siden [Mer informasjon (Støttet)](/readarr/supported#lists) for denne delen
{.is-info}

Importlister lar deg legge til elementer i Readarr automatisk fra dine GoodReads-hyller eller fra andre brukere. Dette kan potensielt legge til mange uventede elementer i Readarr-databasen din, så bruk det med forsiktighet.

![importlists.png](/assets/readarr/importlists.png)

## Importlister

Dette viser deg listene du har for øyeblikket, og lar deg legge til nye lister. Å legge til lister blir dekket mer detaljert nedenfor.

## Importlisteutelukkelser

Alt som er oppført her, er utelukket fra å bli lagt til av lister, og vil aldri bli lagt til fra noen liste. Du kan fjerne elementer fra dette ved å klikke på dem.

## Legge til en importliste

Etter å ha klikket på <kb>+</kb>, velg hvilken type liste du vil legge til:

![addlist.png](/assets/readarr/addlist.png)

I dette tilfellet skal vi legge til en GoodReads bokhylleliste.

![bookshelflist.png](/assets/readarr/bookshelflist.png)

- Navn - Skriv inn et navn for denne listen.
- Aktiver automatisk tillegg - Hvis aktivert, vil alt på listen automatisk legges til i Readarr.

> Dette vil legge til alle forfattere og ALLE BØKER fra den forfatteren i Readarr!

- Overvåk - Velg overvåkingsnivået for ting som legges til. Gyldige alternativer er `Ingen`, `Valgt bok` og `Alle forfatterbøker`. Alle bøker legges til i Readarr, men vil bli overvåket eller ikke overvåket basert på dette valget.
- Søk etter nye elementer - Hvis aktivert, vil Readarr starte et søk etter manglende overvåkede elementer når de legges til fra en liste. Hvis du legger til mange forfattere/overvåkede bøker, kan dette overbelaste systemet ditt!
- Rotmappe - Velg rotmappen for forfattere som legges til fra denne listen
- Kvalitetsprofil - Velg kvalitetsprofilen for forfattere som legges til fra denne listen
- Metadataprofil - Velg metadataprofilen for forfattere som legges til fra denne listen
- Readarr-tagger - Velg hvilke tagger som gjelder for forfattere som legges til fra denne listen

> Det anbefales sterkt å legge til en beskrivende tagg her. Ellers vil du ikke vite hvilken liste som la til disse elementene i Readarr, og når de er lagt til, kan du aldri få denne informasjonen igjen! Denne informasjonen blir ikke logget!

Lister synkroniseres som standard hver 24. time, men kan utløses manuelt fra siden `Innstillinger` => `Oppgaver`. Du kan ikke automatisere denne prosessen raskere enn det.

# Koble til

> Informasjon om støttede tilkoblingstyper finner du på siden [Mer informasjon (Støttet)](/readarr/supported#notifications) for denne delen
{.is-info}

## Tilkoblinger

Tilkoblinger er hvordan du vil at Readarr skal kommunisere med omverdenen.

- Ved å trykke på <kb>+</kb>-knappen vil du få opp et nytt vindu som lar deg konfigurere mange forskjellige endepunkter

- En liste over støttede varsler og tilkoblinger finnes på siden [Mer informasjon (Støttet)](/readarr/supported#notifications)

## Tilkoblingstriggere

- Ved Grab - Få varsel når bøker er tilgjengelige for nedlasting og har blitt sendt til en nedlastingsklient
- Ved Import av utgivelse - Få varsel når bøker er importert vellykket
- Ved Oppgradering - Få varsel når bøker oppgraderes til bedre kvalitet
- Ved Nedlastingsfeil - Få varsel når en boknedlasting mislykkes (kun usenet)
- Ved Importfeil - Få varsel når en boknedlasting mislykkes ved import
- Ved Omdøping - Få varsel når bøker blir omdøpt
- Ved Sletting av forfatter - Få varsel når en forfatter blir slettet
- Ved Sletting av bok - Få varsel når en bok blir slettet
- Ved Sletting av bokfil - Få varsel når en bokfil blir slettet
- Ved Sletting av bokfil for oppgradering - Få varsel når en bokfil blir slettet for en oppgradering
- Ved Omtagging av bok - Få varsel når bøker blir omtaggert
- Ved Helseproblem - Få varsel ved helsekontrollfeil
  - Inkluder helseadvarsler - Få varsel om helseadvarsler i tillegg til feil.

# Metadata

{#write-metadata-to-book-files}

> Informasjon om støttede metadatakonsumenter finner du på siden [Mer informasjon (Støttet)](/readarr/supported#metadata) for denne delen
{.is-info}

Denne siden lar deg opprette/oppdatere metadatakoder/omslag.

![metadata.png](/assets/readarr/metadata.png)

## Calibre-metadata

Hvis du bruker Calibre til å administrere e-boksamlingen din, vil du bruke disse alternativene til å kontrollere den.

- Send metadata til Calibre
  - Alle filer; hold synkronisert med GoodReads - Skriv koder til alle filer og oppdater hvis GoodReads oppdateres
  - Alle filer; bare første import - Skriv koder til alle filer en gang og ikke oppdater hvis GoodReads oppdateres
  - Kun for nye nedlastinger - Skriv koder bare til nye nedlastinger når de importeres
- Oppdater omslag - Aktiver for å fortelle Calibre Content Server å bruke de samme bokomslagene som Readarr
- Bygg inn metadata i bokfiler - Aktiver for å fortelle Calibre Content Server å skrive og bygge inn metadata i bokfilene.

## Skriv metadata til lydfiler

Hvis du bruker lydbøker, vil du bruke disse alternativene til å kontrollere det.

- Merk lydfiler med metadata
  - Alle filer; hold synkronisert med GoodReads - Skriv koder til alle filer og oppdater hvis GoodReads oppdateres
  - Alle filer; bare første import - Skriv koder til alle filer en gang og ikke oppdater hvis GoodReads oppdateres
  - Kun for nye nedlastinger - Skriv koder bare til nye nedlastinger når de importeres
- Rens eksisterende koder - Aktiver for å fjerne alle koder fra filer unntatt de som er lagt til av Readarr

# Tagger

- Tag-seksjonen i Readarr brukes til å knytte forskjellige aspekter av Readarr sammen.
- Tagger er spesielt nyttige for:

  - Utgivelsesprofiler
  - Indekserere
  - Importlister

- Tagger kan brukes til å knytte utgivelsesprofiler, indekserere, importlister og forfattere/bøker sammen.
- For eksempel:
  - Du vil at en bestemt forfatter/bok bare skal bruke en bestemt indekserer. Du ville opprette en tagg og tilordne forfatteren/boken og indeksereren den taggen.
  - Du vil at en bestemt importliste bare skal bruke en bestemt utgivelsesprofil. Du ville opprette en tagg og tilordne importlisten og utgivelsesprofilen den taggen.

> Det anbefales sterkt å legge til en beskrivende tagg til en importliste i tillegg til det som er nevnt ovenfor.

> Merk: Tagger påvirker ikke noen "Kvalitetsprofiler", "Metadataprofiler" eller andre aspekter som ikke er nevnt ovenfor.
{.is-info}

# Generelt

Denne siden er for generelle Readarr-innstillinger som ikke dekkes i andre seksjoner.

## Vert

![genhost.png](/assets/readarr/genhost.png)

- Bind-adresse - Gyldig IPv4-adresse eller '*' for alle grensesnitt
  - 0.0.0.0 eller `*` - alle adresser kan koble til
  - 127.0.0.1 eller localhost - bare lokalnettverksprogrammer kan koble til
  - En annen IP (f.eks. 1.2.3.4) - bare den IP-adressen (1.2.3.4) kan koble til
- Portnummer - Portnummeret du vil bruke for å få tilgang til Readarrs webgrensesnitt

> Merk: Hvis du bruker Docker, ikke endre denne innstillingen.
{.is-warning}

- URL-base - For støtte for omvendt proxy, standard er tomt

> Merk: Hvis du bruker en omvendt proxy (eksempel: mydomain.com/readarr), skriver du '/readarr' for URL-base.
{.is-info}

- Aktiver SSL - Hvis du har SSL-sertifikater og vil sikre kommunikasjonen til og fra Readarr, aktiver dette alternativet.

> Merk: Ikke bruk dette med mindre du vet hva du gjør.
{.is-warning}

## Sikkerhet

![gensecurity.png](/assets/readarr/gensecurity.png)

- Autentisering - Hvordan vil du autentisere for å få tilgang til Readarr-instansen din
  - Ingen - Du har ingen autentisering for å få tilgang til Readarr. Dette er vanligvis hvis du er den eneste brukeren i nettverket ditt, ikke har noen på nettverket ditt som vil ha tilgang til Readarr, eller hvis Readarr ikke er eksponert for weben
  - Grunnleggende (nettleser-popup) - Dette alternativet viser en liten popup når du får tilgang til Readarr, som lar deg skrive inn brukernavn og passord
  - Skjemaer (innloggingsside) - Dette alternativet har en innloggingsskjerm som ligner på innloggingsskjermen til andre nettsteder, som lar deg logge på Readarr
- API-nøkkel - Dette er hvordan andre programmer vil kommunisere eller få Readarr til å kommunisere med andre programmer. Hvis denne nøkkelen gis til feil person med tilgang, kan den gjøre alle slags ting med biblioteket ditt. Derfor blir API-nøkkelen sladdet i loggene
- Sertifikatvalidering - Endre hvor streng HTTPS-sertifikatvalidering er
  - Aktivert - Valider alle HTTPS-sertifikater (anbefalt)
  - Deaktivert for lokale adresser - Valider alle HTTPS-sertifikater unntatt de på localhost og LAN
  - Deaktivert - Ikke valider noen HTTPS-sertifikater

## Proxy

![genproxy.png](/assets/readarr/genproxy.png)

- Proxy - Dette alternativet lar deg sende informasjonen Radarr henter og søker etter gjennom en proxy. Dette kan være nyttig hvis du er i et land som ikke tillater nedlasting av torrentfiler

- Bruk proxy - Aktiver for å bruke en proxy
- Proxytype - Velg proxytypen din (HTTPS, Socks4 eller Socks5)
- Vertsnavn - Skriv inn proxyvertsnavnet ditt (Ikke inkluder http/https eller noen annen protokoll)
- Port - Skriv inn proxyporten din
- Brukernavn - Skriv inn proxybrukernavnet ditt hvis aktuelt
- Passord - Skriv inn proxypassordet ditt hvis aktuelt
- Ignorerte adresser - Skriv inn en kommaseparert liste over adresser som skal omgå proxyen
- Omgå proxy for lokale adresser - Merk av i boksen for å omgå proxyen for lokale adresser.

## Logging

![genlogging.png](/assets/readarr/genlogging.png)

- Loggnivå - En av de mest nyttige feilsøkingsverktøyene
  - Info - Dette er den mest grunnleggende måten Readarr samler informasjon på, og vil inneholde svært minimal mengde informasjon i loggene. Denne loggfilen inneholder alvorlige, feil, advarsler og info-oppføringer.
  - Debug - Debug vil inkludere all informasjonen som Info inkluderer, pluss mer informasjon som kan være nyttig. Denne loggfilen inneholder alvorlige, feil, advarsler, info- og debug-oppføringer
  - Trace - Den mest avanserte og detaljerte loggingen på Readarr, Trace vil inkludere all informasjonen som Info og Debug samler, pluss mer. Dette er den vanligste typen logg som blir bedt om ved feilsøking på Discord eller Reddit. Hvis du trenger hjelp, velger du loggen din til Trace og gjør oppgaven som ga deg problemer på nytt for å fange loggen. Denne loggfilen inneholder alvorlige, feil, advarsler, info, debug- og trace-oppføringer.

## Analyse

![genanalytics.png](/assets/readarr/genanalytics.png)

- Analyse - Send anonym bruker- og feilinformasjon til Readarrs servere (Servarr). Dette inkluderer informasjon om nettleseren din, hvilke Readarr WebUI-sider du bruker, feilrapportering samt OS- og runtime-versjon. Vi vil bruke denne informasjonen til å prioritere funksjoner og feilretting.

## Oppdateringer

![genupdates.png](/assets/readarr/genupdates.png)

- (Avansert alternativ) Gren - Dette er grenen av Readarr du kjører på.
  - [Se denne FAQ-posten for mer informasjon](/readarr/faq#how-do-i-update-readarr)
- Automatisk - Last ned og installer oppdateringer automatisk. Du vil fortsatt kunne installere fra System: Oppdateringer. Merk: Windows-brukere blir alltid oppdatert automatisk.
- Mekanisme - Bruk Readarrs innebygde oppdaterer eller et skript
  - Innebygd - Bruk Readarrs egen oppdaterer
  - Skript - Få Readarr til å kjøre oppdateringsskriptet
  - Docker - Ikke oppdater Readarr fra innsiden av Docker, i stedet dra en helt ny image med den nye oppdateringen
- Skript - Synlig bare når Mekanisme er satt til Skript - Sti til oppdateringsskriptet
- Oppdateringsprosess - Readarr vil laste ned oppdateringsfilen, verifisere integriteten og pakke den ut til en midlertidig plassering og kalle den valgte metoden. Oppdateringsprosessen vil kjøres under samme bruker som Readarr kjører under, den trenger tillatelser til å oppdatere Readarr-filene samt stoppe/starte Readarr.
- Innebygd - Den innebygde metoden vil ta sikkerhetskopi av Readarr-filer og -innstillinger, stoppe Readarr, oppdatere installasjonen og starte Readarr, hvis systemet ditt ikke håndterer stopp av Readarr og vil prøve å starte den på nytt automatisk, kan det være best å bruke et skript i stedet. Ved feil vil forrige versjon av Readarr bli startet på nytt.
- Skript - Skriptet skal håndtere det samme som den innebygde oppdatereren, hvis du trenger å stoppe og starte tjenester (upstart/launchd/etc), må du gjøre det her.

## Sikkerhetskopier

![genbackups.png](/assets/readarr/genbackups.png)

- Sikkerhetskopiseksjonen lar deg fortelle Readarr hvordan du vil håndtere sikkerhetskopier

- Mappe - Dette lar deg velge sikkerhetskopimappen. I Docker vil du være begrenset til hva du tillater at beholderen skal se. Stier er relative til appdata-mappen; om nødvendig kan du angi en absolutt sti for å sikkerhetskopiere utenfor appdata-mappen.
- Intervall - Hvor ofte vil du at Readarr skal lage en sikkerhetskopi
- Oppbevaring - Hvor lenge vil du at Readarr skal beholde hver sikkerhetskopi. Etter at en ny sikkerhetskopi er opprettet, vil den eldste sikkerhetskopien bli fjernet.

Som standard utføres sikkerhetskopier hver 7. dag, og de siste 4 beholdes.

# UI (Brukergrensesnitt)

Denne siden lar deg tilpasse visningsalternativene for brukergrensesnittet.

## Kalender

![uicalendar.png](/assets/readarr/uicalendar.png)

- Første dag i uken - Her kan du velge hvilken dag du mener er den første dagen i uken.
- Ukekolonneoverskrift - Her kan du velge overskriften for kolonnene.

## Datoer

![caldates.png](/assets/readarr/caldates.png)

- Kort datoformat - Hvordan vil du at Readarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du at Readarr skal vise datoer i langt format?
- Tidsformat - Vil du ha et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du at Readarr skal vise relative (i dag/i går/osv.) eller absolutte datoer?

## Stil

![calstyle.png](/assets/readarr/calstyle.png)

- Aktiver fargeblindmodus - Endret stil for å hjelpe fargeblinde brukere med å bedre skille fargekodet informasjon.

## Språk

![callanguage.png](/assets/readarr/callanguage.png)

- Brukergrensesnittspråk - Velg språket som Radarr skal bruke i brukergrensesnittet.