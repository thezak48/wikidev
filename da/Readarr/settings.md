---
title: Readarr Indstillinger
description: 
published: true
date: 2023-04-29T18:17:11.930Z
tags: readarr, indstillinger
editor: markdown
dateCreated: 2021-11-25T15:07:27.926Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Menuindstillinger](#menuindstillinger)
- [Mediehåndtering](#mediehåndtering)
  - [Rodmapper](#rodmapper)
    - [Indstillinger for rodmappe](#indstillinger-for-rodmappe)
  - [Fjernstyrede sti-mappinger](#fjernstyrede-sti-mappinger)
  - [Bogfilnavngivning](#bogfilnavngivning)
  - [Bognavngivning](#bognavngivning)
    - [Standard bogformat](#standard-bogformat)
    - [Forfatter](#forfatter)
    - [Bog](#bog)
    - [Udgivelsesdato](#udgivelsesdato)
    - [Kvalitet](#kvalitet)
    - [Medieinfo](#medieinfo)
    - [Andet](#andet)
    - [Original](#original)
  - [Forfattermappeformat](#forfattermappeformat)
    - [Forfatter](#forfatter-1)
  - [Mapper](#mapper)
  - [Importering](#importering)
  - [Filhåndtering](#filhåndtering)
- [Tilladelser](#tilladelser)
- [Profiler](#profiler)
  - [Kvalitetsprofiler](#kvalitetsprofiler)
  - [Metadataprofiler](#metadataprofiler)
  - [Udgivelsesprofiler](#udgivelsesprofiler)
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
- [Indexere](#indexere)
  - [Understøttede indexere](#understøttede-indexere)
    - [Indstillinger for indexere](#indstillinger-for-indexere)
    - [Usenet-indexerkonfiguration](#usenet-indexerkonfiguration)
    - [Torrent-trackerkonfiguration](#torrent-trackerkonfiguration)
  - [Indstillinger](#indstillinger)
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
  - [Håndtering af afsluttede downloads](#håndtering-af-afsluttede-downloads)
    - [Fjern afsluttede downloads](#fjern-afsluttede-downloads)
    - [Håndtering af mislykkede downloads](#håndtering-af-mislykkede-downloads)
  - [Fjernstyrede sti-mappinger](#fjernstyrede-sti-mappinger-1)
- [Importlister](#importlister)
  - [Importlister](#importlister-1)
  - [Undtagelser for importlister](#undtagelser-for-importlister)
  - [Tilføjelse af en importliste](#tilføjelse-af-en-importliste)
- [Forbindelse](#forbindelse)
  - [Forbindelser](#forbindelser)
  - [Forbindelsestriggere](#forbindelsestriggere)
- [Metadata](#metadata)
  - [Calibre-metadata](#calibre-metadata)
  - [Skriv metadata til lydfiler](#skriv-metadata-til-lydfiler)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Vært](#vært)
  - [Sikkerhed](#sikkerhed)
  - [Proxy](#proxy)
  - [Logning](#logning)
  - [Analyse](#analyse)
  - [Opdateringer](#opdateringer)
  - [Opdateringer](#opdateringer-1)
  - [Sikkerhedskopier](#sikkerhedskopier)
- [UI (brugergrænseflade)](#ui-brugergrænseflade)
  - [Kalender](#kalender)
  - [Datoer](#datoer)
  - [Stil](#stil)
  - [Sprog](#sprog)

Denne side vil gennemgå alle indstillingerne i Readarr og hvordan de fungerer. Dette er ikke ment som en omfattende "sådan sætter du Readarr op". Hvis du ønsker det, skal du bruge siden [Hurtigstart](/readarr/quick-start-guide) i stedet.

# Menuindstillinger

For at komme til indstillingssiden skal du vælge Indstillinger i venstremenuen. Følgende undermenuindstillinger vil være tilgængelige:

![settings_1_menu.png](/assets/readarr/settings_1_menu.png)

Bemærk også, at der for hver individuel indstillingsside er nogle indstillinger øverst i menuen:

![settings_2_topmenu.png](/assets/readarr/settings_2_topmenu.png)

- Skjul/Vis avanceret er vigtigt for alle elementer, der er markeret nedenfor som `(Avanceret indstilling)`, ellers vises de ikke. Disse menupunkter vises i orange på skærmbillederne.

- Du skal gemme dine ændringer, før du forlader skærmen. Dette gør du ved at klikke på diskikonet. Hvis du ikke har foretaget ændringer, vises "Ingen ændringer" og er gråtonet, som vist ovenfor.

# Mediehåndtering

> Nogle af disse indstillinger er kun synlige gennem `Vis avancerede indstillinger`, som er placeret øverst i værktøjslinjen under søgefeltet{.is-info}

## Rodmapper

- En liste over dine konfigurerede rodmapper (biblioteksmapper) vises.
- Klik på <kb>+</kb>-knappen for at tilføje en ny rodmappe eller klik på et eksisterende kort for at redigere det.

### Indstillinger for rodmappe

- Navn - Navnet på rodmappe til brug i brugergrænsefladen
- Sti - Mappen, der indeholder dit bogbibliotek, dvs. den endelige destination, som Readarr ser det.
  - Bemærk, at dette skal være anderledes end den placering, din downloadklient placerer filer.
  - Hvis du bruger Docker og Calibre-integration, skal monteringerne være de samme som din bogmappe.

{#calibre}

- Specifikke indstillinger for Calibre (Kun hvis Brug Calibre er aktiveret)
  - Brug Calibre - Aktivér/deaktivér brugen af Calibre Content Server til at administrere din rodmappe.

> \* Bemærk, at dette **ikke kan aktiveres på en eksisterende rodmappe**.
> \* Bemærk, at dette **ikke kan deaktiveres på en eksisterende rodmappe, hvor Calibre er aktiveret**.
> \* Bemærk, at dette kræver **Calibre Content Server** og ikke fungerer med Calibre Web eller Calibre.
> \* Bemærk, at hardlinks ikke fungerer med Calibre-integration.
> \* Bemærk, at dette kræver, at Calibre har aktiveret "Kræv brugernavn og adgangskode for at få adgang til indholdsserveren".
> \* Hvis "Kræv brugernavn og adgangskode for at få adgang til indholdsserveren" ikke er aktiveret i Calibre, vil manglende overholdelse resultere i en fejlmeddelelse om, at "Anonyme brugere ikke har tilladelse til at foretage ændringer".
{.is-warning}

- Calibre-vært - IP/domænet for værten for Calibre Content Server
- Calibre-port - Porten, som Calibre Content Server lytter på
- (Avanceret) Calibre URL-base - Tilføj et præfiks til Calibre-URL'en, f.eks. `http://[vært]:[port]/[urlBase]`
- Calibre-brugernavn - Brugernavn til at få adgang til Calibre Content Server
- Calibre-adgangskode - Adgangskode til at få adgang til Calibre Content Server
- Calibre-bibliotek - Navn på Calibre Content Server-bibliotek. Lad være blank for standardværdi
- Konverter til format - (Valgfrit) Bed Calibre Content Server om at konvertere til andre formater med en kommasepareret liste.
  - Gennemgå ikonet (i) i appen for en aktuel liste over muligheder.
  - Mulighederne er: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-outputprofil - Vælg den outputprofil for Calibre Content Server, der skal bruges
  - Outputprofilen fortæller Calibre Content Server-konverteringssystemet, hvordan dokumentet skal optimeres til den angivne enhed (f.eks. ved at ændre størrelsen på billeder til enhedens skærmstørrelse). I nogle tilfælde kan en outputprofil bruges til at optimere outputtet til en bestemt enhed, men dette er sjældent nødvendigt.
- Brug SSL - Aktivér eller deaktivér brugen af SSL (HTTPS) til Calibre Content Server
- Overvågning - Konfigurer dine overvågningsindstillinger for bøger, der opdages i denne mappe
  - Alle bøger - Overvåg alle bøger
  - Fremtidige bøger - Overvåg bøger, der endnu ikke er udgivet
  - Manglende bøger - Overvåg bøger, der enten ikke har filer eller endnu ikke er udgivet
  - Eksisterende bøger - Overvåg bøger, der enten har filer eller endnu ikke er udgivet
  - Første bog - Overvåg den første bog. Alle andre bøger vil blive ignoreret
  - Seneste bog - Overvåg den seneste bog og fremtidige bøger
  - Ingen - Ingen bøger vil blive overvåget, medmindre de tilføjes eksplicit
- Kvalitetsprofil - Standard kvalitetsprofil for bøger og forfattere, der opdages i denne mappe
- Metadataprofil - Vælg metadataprofilen, der skal bruges til forfattere, der opdages i denne mappe. Vælg Ingen for kun at indlæse bøger, der blev tilføjet eller opdaget eksplicit.
- Standard Readarr-tags - Standardtags for forfattere, der opdages i denne mappe

> Brugere af ikke-Windows-systemer:
> \* Hvis du bruger et NFS-mount, skal `nolock` være aktiveret.
> \* Hvis du bruger et SMB-mount, skal `nobrl` være aktiveret.
{.is-warning}

## Fjernstyrede sti-mappinger

- Fjernstyrede sti-mappinger fungerer som en simpel find-og-erstat-funktion for fjernstyring af sti og lokal sti. Dette bruges primært til enten sammensmeltede lokale/fjernstyrede opsætninger ved hjælp af mergerfs eller lignende eller når applikationen og downloadklienten eller Calibre ikke er på samme server.
- Se afsnittet i [Downloadklienter => Fjernstyrede sti-mappinger](#fjernstyrede-sti-mappinger-1) og erstat `<Downloadklient>` med `<Calibre>` for mere information.

## Bogfilnavngivning

![bookfilenaming.png](/assets/readarr/bookfilenaming.png)

**Hvis du bruger Calibre-integration, får du ikke mulighed for at navngive bogfiler. Calibre tager sig af dette for dig. Du skal kun ændre disse indstillinger, hvis du ikke bruger Calibre.**

> Bemærk, at mens Readarr er i beta, anbefales det at deaktivere omdøbning i Readarr, hvis du bruger Calibre, bare for en sikkerheds skyld, hvis der skulle opstå en utilsigtet fejl. {.is-info}

Almindeligt anvendte navngivningsskemaer er:

- Standard bogformat
  - `{Bogtitel}\{Forfatternavn}` - `{Bogtitel}`, hvilket derefter vil resultere i en mappe med navnet `Cujo` og en undermappe, der indeholder en fil med navnet `Stephen King - Cujo.m4b`

- Forfattermappeformat
  - `{Forfatternavn}`, hvilket derefter vil resultere i: `Stephen King`

## Bognavngivning

- Omdøb bøger - Hvis dette er slået fra (ingen markering i boksen), vil Readarr bruge det eksisterende filnavn, hvis omdøbning er deaktiveret.
  - Hvis ikke markeret:
    - Import fra downloadklient
      - Downloadklientens udgivelsestitel bruges
    - Manuel (ad hoc) import: Oprindeligt filnavn

> Hvis du lader være med at markere Omdøb bøger, gælder ingen af de følgende navngivningsindstillinger - du har fortalt Readarr, at du slet ikke ønsker nogen omdøbning. Bogen importeres direkte i forfattermappen.
{.is-info}

> Dette gælder ikke, hvis Calibre bruges, da Calibre håndterer fil-/mappenavngivelse ved hjælp af sit eget interne skema.
{.is-info}

- Erstat ulovlige tegn - Hvis dette er deaktiveret, fjerner Readarr ulovlige tegn. Hvis det er aktiveret, erstatter Readarr ulovlige tegn. Eksempler inkluderer `\ # / $ * < >` og mere.

### Standard bogformat

- Vælg navngivningen

- Rullemenu (øverst til højre)
  - Venstre boks - Håndtering af mellemrum
    - `Mellemrum ( )` - Brug mellemrum i navngivningen (standard)
    - `Punktum (.)` - Brug punktummer i stedet for mellemrum i navngivningen
    - `Understreg (_)` - Brug understregninger i stedet for mellemrum i navngivningen
    - `Bindestreg (-)` - Brug bindestreger i stedet for mellemrum i navngivningen
  - Højre boks - Håndtering af store og små bogstaver
    - `Standardstørrelse` - Gør titlen til store og små bogstaver (~camel-case) (standard)
    - `Store bogstaver` - Gør titlen til store bogstaver
    - `Små bogstaver` - Gør titlen til små bogstaver

### Forfatter

- `{Forfatternavn}` = Forfatterens navn
- `{ForfatternavnThe}` = Forfatterens navn, The
- `{ForfatterCleanName}` = Forfatterens navn
- `{ForfatterSortName}` = Navn, Forfatter
- `{ForfatterDisambiguation}` = Forfatternavn (disambiguation bruges fra GoodReads for flere forfattere med samme navn)

### Bog

- `{Bogtitel}` = Bogens titel!: Undertitel!
- `{BogtitelThe}` = Bogens titel!, The: Undertitel!
- `{BogCleanTitle}` = Bogens titel: Undertitel
- `{BogtitelNoSub}` = Bogens titel!
- `{BogtitelTheNoSub}` = Bogens titel!, The
- `{BogCleanTitleNoSub}` = Bogens titel
- `{BogUndertitel}` = Undertitel!
- `{BogUndertitelThe}` Undertitel!, The
- `{BogCleanUndertitel}` = Undertitel
- `{BogDisambiguation}` = Bognavn! (disambiguationstitel bruges fra GoodReads)
- `{Bogserie}` = Serietitel
- `{BogseriePosition}` = 1
- `{BogserieTitle}` = Serietitel #1
- `{PartNumber:0}` eller `{PartNumber:0}` = 2
- `{PartNumber:00}` = 02
- `{PartCount}` eller `{PartCount:0} = 9
- `{PartCount:00}` = 09

### Udgivelsesdato

- `{Udgivelsesår}` = 2016
- `{UdgivelsesårFirst}` = 2015
- `{Udgaveår}` = 2016

### Kvalitet

- `{KvalitetFuld}` = AZW3 Korrekt
- `{KvalitetTitel}` = AZW3

### Medieinfo

- `{MedieinfoAudioCodec}` = MP3
- `{MedieinfoAudioChannels}` = 2.0
- `{MedieinfoAudioBitRate}` = 320kbps
- `{MedieinfoAudioBitsPerSample}` = 24bit
- `{MedieinfoAudioSampleRate}` = 44.1kHz

### Andet

- `{Udgivelsesgruppe}` = Rls Grp
- `{Foretrukne ord}` = iNTERNAL

### Original

- `{Originaltitel}` = Forfatter.Navn.Bog.Navn.2018.AZW3-EVOLVE
- `{Originalfilnavn}` = 01-bognavn

> Originalfilnavn anbefales ikke. Det er det bogstavelige oprindelige filnavn og kan være obfuskeret t1i0p3s7i8yuti. Originaltitel er udgivelsesnavnet og bør i stedet bruges.
{.is-info}
  
## Forfattermappeformat

- (Avanceret indstilling) Her indstiller du navngivningskonventionen for forfattermappenavnet.

> Dette gælder ikke, hvis Calibre bruges, da Calibre håndterer fil-/mappenavngivelse ved hjælp af sit eget interne skema.
{.is-info}

### Forfatter

- `{Forfatternavn}` = Forfatterens navn
- `{ForfatternavnThe}` = Forfatterens navn, The
- `{ForfatterCleanName}` = Forfatterens navn
- `{ForfatterSortName}` = Navn, Forfatter
- `{ForfatterDisambiguation}` = Forfatternavn (disambiguation bruges fra GoodReads for flere forfattere med samme navn)

## Mapper
  
![mm_folders.png](/assets/readarr/mm_folders.png)
  
- (Avanceret indstilling) Opret tomme forfattermapper - Markér afkrydsningsfeltet for at oprette tomme forfattermapper, når en ny forfatter tilføjes.
- (Avanceret indstilling) Slet tomme forfattermapper - Markér afkrydsningsfeltet for at slette tomme forfattermapper, hvis der ikke er nogen bøger i dem.
  
> Én af disse afkrydsningsfelter kan være markeret, men de må ikke BEGGE være markeret. {.is-warning}

> Dette gælder ikke, hvis Calibre bruges, da Calibre håndterer fil-/mappenavngivelse ved hjælp af sit eget interne skema.
{.is-info}



## Importering
  
![mm_importing.png](/assets/readarr/mm_importing.png)
  
- (Avanceret indstilling) Spring kontrol af ledig plads over - Hvis aktiveret springes kontrol af ledig plads over inden importering
- (Avanceret indstilling) Minimum ledig plads - Indtast den minimum ledige plads, som drevet skal have, før importeringen stopper.
- (Avanceret indstilling) Brug hardlinks i stedet for kopiering - Marker denne boks for at bruge hardlinks i stedet for kopiering (for torrents). Bemærk, at dette er aktiveret som standard.
  
> Du bør ideelt set bruge dette, hvor det er muligt. For at kunne bruge hardlinks skal du have din kilde/destination på det samme filsystem (drev, partition) og monteringspunkter. [Se TRaSH's Hardlink Guide for mere information](https://trash-guides.info/hardlinks/)
  
- Importer ekstra filer - Hvis aktiveret, importeres de angivne ekstra filer, der findes i mappen for bogen, når den importeres
- (Avanceret indstilling) Importer ekstra filer - Hvis "Importer ekstra filer" er aktiveret, skal du indtaste en kommasepareret liste over filtypetilføjelser, der skal importeres.

> Hvis du bruger Readarr til lydbøger, skal du tilføje .cue til denne liste, da den indeholder dine kapiteloplysninger!
{.is-info}
  
## Filhåndtering
  
  ![mm_filemgmt.png](/assets/readarr/mm_filemgmt.png)

- Ignorer slettede bøger - Marker denne boks for at fjerne overvågning af bøger, der er registreret som slettet eller utilgængelige fra Readarr's rodmappe.
- Download korrekte og repacks - Om der automatisk skal opgraderes til korrekte/repacks. Brug "Foretræk ikke" til at sortere efter foretrukken ordvurdering over korrekte/repacks
  - Foretræk og opgrader - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl nye repacks og korrekte som en opgradering af nuværende udgivelser.
  - Opgrader ikke automatisk - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl ikke nye repacks og korrekte som en opgradering af nuværende udgivelser.
  - Foretræk ikke - Ignorer effektivt repacks og korrekte. Du skal administrere eventuelle præferencer for disse med [Foretrukne ord](#udgivelsesprofiler).
  
> \* `PROPER` - betyder, at der var et problem med den tidligere udgivelse. Downloads, der er mærket som PROPER, viser, at problemerne er blevet løst i den udgivelse. Dette er gjort af en gruppe, der ikke udgav originalen.
> \* `REPACK` - betyder, at der var et problem med den tidligere udgivelse, og det er blevet rettet af den oprindelige gruppe. Downloads, der er mærket som REPACK, viser, at problemerne er blevet løst i den udgivelse. Dette er gjort af en gruppe, der udgav originalen.
{.is-info}

- (Avanceret indstilling) Overvåg rodmapper for filændringer - Marker denne boks for at udløse en genindlæsning, når det registreres, at rodmappen er blevet ændret.
- (Avanceret indstilling) Genindlæs forfattermappe efter opdatering - Vælg, hvornår en forfattermappe skal genindlæses efter opdatering af forfatteren.
  - Altid - Dette vil genindlæse forfattermapper baseret på opgaveplanen
  - Efter manuel opdatering - Du skal manuelt genindlæse disken
  - Aldrig - Ligesom det siger, genindlæs aldrig forfattermapperne.
- (Avanceret indstilling) Tillad fingeraftryk - Vælg, hvordan fingeraftryk skal håndteres, hvilket giver øget nøjagtighed for bogmatchning, på bekostning af CPU/disktid.
  - Altid - Brug altid fingeraftryk, hvis det er muligt
  - Kun for nye importeringer - Kun brug fingeraftryk på nyimporterede udgivelser
  - Aldrig - Ligesom det siger, brug aldrig fingeraftryk
- (Avanceret indstilling) Ændre filens dato - Ændre filens dato ved import/genindlæsning
  - Ingen - Readarr ændrer ikke datoen, der vises i din givne filbrowser
  - Bogudgivelsesdato - Datoen, hvor bogen blev udgivet.
- (Avanceret indstilling) Papirkurv - Bogfiler vil blive flyttet hertil, når de slettes, i stedet for at blive slettet permanent
- (Avanceret indstilling) Rensning af papirkurv - Dette er, hvor gammel en given fil kan være, før den slettes permanent

> Det anbefales kraftigt at bruge en papirkurv. Det er nemt at slette filer, og det er nemt at gendanne dem, hvis du bruger papirkurven.
{.is-warning}

# Tilladelser

- Indstil tilladelser - Skal `chmod` køres, når filer importeres/omdøbes?
  - chmod-mappe - Oktal, der anvendes under import/omdøbning til mediemapper og filer (uden udførelsesbit)

> Rullemenuen har en forudindstillet liste over meget almindeligt anvendte tilladelser, der kan bruges. Du kan dog manuelt indtaste en oktal mappe, hvis du ønsker det.
{.is-info}

> Dette virker kun, hvis brugeren, der kører `Readarr`, er ejeren af filen. Det er bedre at sikre, at downloadklienten indstiller tilladelserne korrekt.
{.is-warning}

- chown-gruppe - Gruppenavn eller GID. Brug GID til fjernfiler-systemer

> Dette virker kun, hvis brugeren, der kører `Readarr`, er ejeren af filen. Det er bedre at sikre, at downloadklienten indstiller tilladelserne korrekt.
{.is-warning}

# Profiler

## Kvalitetsprofiler

Kvalitetsprofiler bruges til at bestemme, hvilke formater af bøger der er acceptable for en bog i dit bibliotek.
  
![qualityprofile.png](/assets/readarr/qualityprofile.png)

- Indstil profiler for kvaliteten af de bøger, du ønsker at downloade.

> Når du vælger en eksisterende profil eller tilføjer en ekstra profil, vises et nyt vindue
> Bemærk: Kvaliteten, der har en blå boks, er kvaliteten, som alt med denne profil fortsat vil blive opgraderet til.
{.is-info}

- Plus-ikon (<kb>+</kb>) - Opret en ny kvalitetsprofil

- Navn - Indtast et **UNIKT** navn for den kvalitetsprofil, du opretter
- Opgraderinger tilladt - Når denne indstilling er markeret, og du beder Readarr om at downloade en `EPUB`, fordi det er den første udgivelse af en bestemt bog, og senere uploader nogen en `AZW3`, vil Readarr automatisk opgradere til den bedre kvalitet ***hvis*** `Opgrader indtil` har den kvalitet valgt
  - Opgrader indtil - Når denne kvalitet er nået, vil Readarr ikke længere downloade bøger

> Bemærk: Dette gælder kun, hvis du har `AZW3` højere end `EPUB` inden for afsnittet `Kvaliteter`
{.is-warning}

- Kvaliteter - Kvaliteter, der er højere på listen, foretrækkes mere uanset ønsket (aktiveret/markeret) status. for rangering uanset aktiveret status. Kvaliteter inden for samme gruppe er lige. Kun aktiverede (markerede) kvaliteter ønskes (tilladt)
  - Rediger grupper - Nogle kvaliteter er grupperet sammen for at reducere størrelsen på listen samt gruppere lignende udgivelser. Et godt eksempel på dette er `WebDL` og `WebRip`, da disse er meget ens og typisk har lignende bitrater. Når du redigerer grupperne, kan du ændre præference inden for hver af grupperne.

  - [Se Kvaliteter](#kvaliteter-defineret)

> Som standard er kvaliteterne indstillet fra "dårligste" (nederst) til "bedste" (øverst)
{.is-info}

## Metadataprofiler

Metadataprofiler bruges til at bestemme, hvilke bøger fra GoodReads der skal tilføjes under en forfatter, når en ny forfatter tilføjes.

- Plus-ikon (<kb>+</kb>) - Opret en ny metadataprofil

![metaprofiles.png](/assets/readarr/metaprofiles.png)
  
- Navn - Indtast et **UNIKT** navn for metadataprofilen
- Minimum popularitet - Indtast den minimum popularitet, som en bog skal have for at blive tilføjet til en forfatter.

> Hvis du indstiller dette for højt, vil bøger ikke blive tilføjet til Readarr, men hvis du indstiller det for lavt, vil der dukke obskure udgivelser op.
{.is-warning}

> Indstil dette til `10000000000` præcist for at oprette en profil, der svarer til `Ingen`, men stadig tillader filtrering af udgaver og bøger. Bemærk, at `Ingen` ikke anvender nogen metadatafiltre, og du kan få udenlandske udgaver.
{.is-info}

- Minimum antal sider - Indtast det minimum antal sider, som en bog skal have for at blive tilføjet til en forfatter.
- Spring bøger over uden udgivelsesdato over - Aktiver for at springe bøger over uden en udgivelsesdato.
- Spring bøger over uden ISBN eller ASIN over - Aktiver for at springe bøger over, der ikke indeholder hverken et ISBN eller ASIN-nummer.
- Spring delbøger og sæt over - Aktiver for at springe delbøger og sæt over.
- Spring sekundære seriebøger over - Aktiver for at springe sekundære seriebøger over.
- Tilladte sprog - Indtast en kommasepareret liste over ISO 639-3-sprogkoder eller 'null' for tilladte sprog for dine bøger
- Må ikke indeholde - Indtast ord eller sætninger, som en bogtitel ikke må indeholde for at blive tilføjet.
  
> Du kan oprette flere metadataprofiler og anvende en separat profil til hver forfatter efter behov. Men du kan kun anvende en enkelt metadataprofil til en given forfatter.
{.is-info}
  
## Udgivelsesprofiler

Udgivelsesprofiler bruges til at bestemme, om indexeringsnavne kvalificerer sig til download.

![releaseprofiles.png](/assets/readarr/releaseprofiles.png)  
  
- Aktivér profil - Marker boksen for at aktivere denne profil.
- Skal indeholde - Tilføj en liste over ord eller sætninger, der SKAL være i udgivelsesnavnet for at blive betragtet som gyldigt.
- Må ikke indeholde - Tilføj en liste over ord eller sætninger, der IKKE må være i udgivelsesnavnet for at blive betragtet som gyldigt.
- Foretrukne (ord) - Her kan du tilføje vilkår eller regex med score (positive og negative) for at blive betragtet som mere eller mindre foretrukne. Du kan f.eks. foretrække "uforkortet" med en positiv score.
  
> Udgivelser med en højere score for foretrukne ord end den eksisterende fil er ALTID en opgradering!
{.is-info}
  
- Inkluder foretrukne ved omdøbning - Marker denne boks for at inkludere dine foretrukne ord (eller regex-match) i tildelingen af `{Foretrukne ord}` i filnavngivningen.

> Du bør inkludere `{Foretrukne ord}` i din filnavngivelse og markere denne boks, hvis du bruger dem, fordi du ellers kan ende i en download-loop.
{.is-warning}

- Indexer - I denne rullemenu kan du begrænse denne udgivelsesprofil til en enkelt indexer. Dette bør næsten altid efterlades som `(any)` (enhver).
- Tags - Indtast en tag her for at kunne anvende denne tag på forfattere med samme tag. Hvis du ikke anvender en tag her, gælder denne profil for ALLE forfattere.

## Forsinkelsesprofiler

- Forsinkelsesprofiler giver dig mulighed for at reducere antallet af udgivelser, der bliver downloadet til en bog ved at tilføje en forsinkelse, mens Readarr fortsætter med at overvåge udgivelser, der bedre matcher dine præferencer.
- Protokol - Dette vil enten være `Usenet` eller `Torrent` afhængigt af, hvilken downloadklient du foretrækker
- Usenet-forsinkelse - Indstil antallet af minutter, du vil vente, før downloaden starter
- Torrent-forsinkelse - Indstil antallet af minutter, du vil vente, før downloaden starter
- Bypass, hvis højeste kvalitet - Bypass forsinkelsen, når udgivelsen har den højeste aktiverede kvalitetsprofil med den foretrukne protokol
- Tags - Ved at give denne forsinkelsesprofil en tag kan du mærke en given bog for at få den til at følge reglerne, der er angivet her.
- Skruenøgleikon - Dette giver dig mulighed for at redigere forsinkelsesprofilen
- Plus-ikon (<kb>+</kb>) - Opret en ny forsinkelsesprofil

### Anvendelser

Nogle medier vil modtage et halvt dusin forskellige udgivelser af varierende kvalitet i timerne efter en udgivelse, og uden forsinkelsesprofiler kan Readarr forsøge at downloade dem alle. Med forsinkelsesprofiler kan Readarr konfigureres til at ignorere de første par timer med udgivelser.

Forsinkelsesprofiler er også nyttige, hvis du vil lægge vægt på en protokol (Usenet eller BitTorrent) over den anden. (Se Eksempel 3)

### Sådan fungerer forsinkelsesprofiler

Timeren begynder, så snart Readarr registrerer, at en bog har en tilgængelig udgivelse. Denne udgivelse vises i din kø med et urikon for at angive, at den er under forsinkelse.

> Uret starter fra udgivelsestidspunktet for udgivelserne og ikke fra det tidspunkt, Readarr ser dem. {.is-info}

I løbet af forsinkelsesperioden vil Readarr bemærke eventuelle nye udgivelser, der bliver tilgængelige. Når forsinkelsestimeren udløber, vil Readarr downloade den ene udgivelse, der bedst matcher dine kvalitetspræferencer.

Tidsperioden kan være forskellig for Usenet og torrents. Hver profil kan være forbundet med en eller flere tags for at give dig mulighed for at tilpasse, hvilke bøger der har hvilke profiler. En forsinkelsesprofil uden tag betragtes som standard og gælder for alle bøger, der ikke har et specifikt tag.

> Forsinkelsesprofiler starter fra det tidspunkt, som indexeret rapporterer, at udgivelsen blev uploadet. Dette betyder, at indhold, der er ældre end det antal minutter, du har indstillet, ikke påvirkes på nogen måde af din forsinkelsesprofil og vil blive downloadet øjeblikkeligt. Derudover vil **eventuelle manuelle søgninger** efter indhold (søgninger uden for RSS-feed) ignorere indstillingerne for forsinkelsesprofil.
{.is-warning}

#### Eksempler

- For hvert eksempel skal det antages, at brugeren har følgende kvalitetsprofil aktiveret: EPUB og derover er tilladt MOBI er kvalitetsgrænsen * AZW3 er den højest rangerede kvalitet

##### Eksempel 1

- I dette enkle eksempel er profilen indstillet med en 120 minutters (to timers) forsinkelse for både Usenet og torrents.

- Kl. 23:00 registrerer Readarr den første udgivelse af en bog, der blev uploadet kl. 22:50, og den 120 minutters timer begynder. Kl. 00:50 vil Readarr evaluere eventuelle udgivelser, den har fundet i de sidste to timer, og downloade den bedste, som er MOBI.

- Kl. 03:00 findes en anden udgivelse, som er MOBI, der blev tilføjet til dit indexer kl. 02:46. En anden 120 minutters timer begynder. Kl. 04:46 downloades den bedst tilgængelige udgivelse. Da kvalitetsgrænsen nu er nået, kan bogen ikke længere opgraderes, og Readarr stopper med at lede efter nye udgivelser.

- På et hvilket som helst tidspunkt, hvis der findes en AZW3-udgivelse, downloades den øjeblikkeligt, fordi det er den højest rangerede kvalitet. Hvis der er en aktiv forsinkelsestimer, annulleres den.

##### Eksempel 2

- Dette eksempel har forskellige timere for Usenet og torrents. Antag en 120 minutters timer for Usenet og en 180 minutters timer for BitTorrent.

- Kl. 23:00 registrerer Readarr den første udgivelse af en bog, og begge timere starter. Udleveringen blev tilføjet til indexeret kl. 22:15. Kl. 00:15 vil Readarr evaluere eventuelle udgivelser, og hvis der er nogen acceptable Usenet-udgivelser, downloades den bedste, og begge timere afsluttes. Hvis der ikke er nogen, vil Readarr vente indtil kl. 00:15 og downloade den bedste udgivelse, uanset hvilken kilde den kommer fra.

##### Eksempel 3

- En almindelig brug af forsinkelsesprofiler er at lægge vægt på en protokol over den anden. For eksempel vil du kun downloade en BitTorrent-udgivelse, hvis der ikke er blevet uploadet noget til Usenet efter et bestemt tidsrum.

- Du kan indstille en 60 minutters timer for BitTorrent og en 0 minutters timer for Usenet.

- Hvis den første udgivelse, der registreres, er fra Usenet, downloades den øjeblikkeligt af Readarr.

- Hvis den første udgivelse er fra BitTorrent, indstiller Readarr en 60 minutters timer. Hvis der i løbet af den tid findes en kvalificerende Usenet-udgivelse, ignoreres BitTorrent-udgivelsen, og Usenet-udgivelsen hentes.

# Kvalitet

![qualitydefinitions.png](/assets/readarr/qualitydefinitions.png)

## Betydning af kvalitetstabellen

- Kvalitet - Navnet på kvaliteten i scenen (hardcodet)
- Titel - Navnet på kvaliteten i brugergrænsefladen (konfigurerbar)
- Megabyte per minut - Selvforklarende
- Størrelsesbegrænsning - Selvforklarende
- Min - Den mindste bytes eller kilobytes per sekund (b/s|kb/s), som en kvalitet kan have.
- Maks - Den maksimale bytes eller kilobytes per sekund (b/s|kb/s), som en kvalitet kan have.

## Definerede kvaliteter

- Ukendt tekst - Selvforklarende
- PDF - Portable Document File
- MOBI - En af de mest anvendte e-bogsfilformater
- EPUB - Endnu et af de mest anvendte e-bogsfilformater
- AZW3 - AZW3 er en e-bogsfil, der er udviklet af Amazon. Den bruges i Amazon Kindles til at se e-bøger.
- Ukendt lyd - Selvforklarende
- MP3 - Almindeligt lydformat med tab
- M4B - Almindeligt lydbogsfilformat
- FLAC - Free Lossless Audio Codec, et lydformat, der ligner MP3, men er tabløst

# Indexere

> Oplysninger om understøttede indexere kan findes på siden [Flere oplysninger (Understøttet)](/readarr/supported#indexers) for dette afsnit
{.is-info}

## Understøttede indexere

- En liste over understøttede indexere findes på siden [Flere oplysninger (Understøttet)](/readarr/supported#indexers)

### Indstilling af indexer

- Når du har klikket på <kb>+</kb>-knappen for at tilføje en ny indexer, får du vist et nyt vindue med mange forskellige indstillinger. I denne wiki betragter Readarr både Usenet-indexere og torrent-trackere som "indexere".

- Der er to sektioner her: Usenet og torrents. Afhængigt af hvilken downloadklient du vil bruge, skal du vælge den type indexer, du vil bruge.

### Konfiguration af Usenet-indexer

- Newznab - Her finder du forudindstillinger for populære Usenet-indekser (som er udfyldt, alt hvad du behøver er din API-nøgle, som leveres af Usenet-indekseren efter eget valg), sammen med muligheden for at oprette en brugerdefineret indekser.
- Software, der fungerer med Usenet og integrerer godt med Readarr, er [NZBHydra2](https://github.com/theotherp/nzbhydra2/) eller [Prowlarr](/prowlarr), som integrerer med både Usenet og Torrents.
- Uanset om du vælger en forudindstillet indekser eller en brugerdefineret indekseropsætning, vil du blive præsenteret for et nyt vindue til at indtaste alle dine indstillinger.
- Vælg mellem forudindstillingerne eller tilføj en brugerdefineret indekser (som f.eks. NZBHydra2 eller Prowlarr).
- Navn - Navnet på indekseren i Readarr.
- Aktivér RSS - Hvis det er aktiveret, brug denne indekser til at overvåge efter filer, der ønskes og mangler eller endnu ikke har nået deres cutoff.
- Aktivér automatisk søgning - Hvis det er aktiveret, brug denne indekser til automatisk søgning, herunder søgning ved tilføjelse.
- Aktivér interaktiv søgning - Hvis det er aktiveret, brug denne indekser til manuel interaktiv søgning.
- URL - Indekserens URL, som indekseren har angivet, f.eks. `https://api.nzbgeek.info`.
- API-sti - Indekserens API-sti, som indekseren har angivet. Dette er normalt `/api`.
- Flersproget - Indstil hvilke sprog `MULTI` der er for denne indekser.
- API-nøgle - Indekserens API-nøgle til at få adgang til API'en.
- Kategorier - Standardkategorier vil blive brugt, medmindre de redigeres. Det er sandsynligt, at disse standardkategorier ikke er optimale. Når denne indstilling redigeres, forespørger Readarr indekseren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standardindstillinger ryddes, så snart en kategori skiftes.
- (Avanceret indstilling) Tidlig downloadgrænse - Tid før udgivelsesdato, som Readarr vil downloade fra denne indekser. Lad være blank for ingen grænse. Dette ligner tilgængelighed i Radarr.
- (Avanceret indstilling) Yderligere parametre - Yderligere Newznab-parametre, der skal tilføjes til forespørgselslinket.
- (Avanceret indstilling) Indekserprioritet - Prioritet for denne indekser for at foretrække en indekser frem for en anden i tilfælde af ligestilling i udgivelsesscenarier. 1 er højeste prioritet, og 50 er laveste prioritet.

### Konfiguration af torrent-tracker

- På samme måde som Usenet er der en række forudindstillede torrent-trackeroplysninger. Hvis du ikke er medlem af nogen af disse specifikke trackere, vil de ikke være til nogen nytte for dig.
- En af de enkleste måder at bruge Torrent-trackere med Readarr er ved at bruge et andet program som [Prowlarr](/prowlarr) eller [Jackett](https://github.com/Jackett/Jackett). Disse software fungerer godt med Readarr og fungerer som en søgeindekser, der indeholder al din information og sender den til Readarr.
- Torznab - Denne mulighed vil indstille dig med en Jackett-forudindstilling, hvis du bruger flere trackere, skal du have hver post med et unikt navn.
- Torznab-indekser
- Vælg mellem forudindstillingerne eller tilføj en brugerdefineret indekser (som f.eks. Jackett).
- Navn - Navnet på indekseren i Readarr.
- Aktivér RSS - Hvis det er aktiveret, brug denne indekser til at overvåge efter filer, der ønskes og mangler eller endnu ikke har nået deres cutoff.
- Aktivér automatisk søgning - Hvis det er aktiveret, brug denne indekser til automatisk søgning, herunder søgning ved tilføjelse.
- Aktivér interaktiv søgning - Hvis det er aktiveret, brug denne indekser til manuel interaktiv søgning.
- URL - Indekserens URL, f.eks. `http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`.
- API-sti - Indekserens API-sti, som indekseren har angivet. Dette er normalt `/api`.
- API-nøgle - Indekserens API-nøgle til at få adgang til API'en.
- Flersproget - Indstil hvilke sprog `MULTI` der er for denne indekser.
- Kategorier - Standardkategorier vil blive brugt, medmindre de redigeres. Det er sandsynligt, at disse standardkategorier ikke er optimale. Når denne indstilling redigeres, forespørger Readarr indekseren om dens tilgængelige kategorier og viser dem i en valgbar liste. De forældede standardindstillinger ryddes, så snart en kategori skiftes.
- (Avanceret indstilling) Tidlig downloadgrænse - Tid før udgivelsesdato, som Readarr vil downloade fra denne indekser. Lad være blank for ingen grænse. Dette ligner tilgængelighed i Radarr.
- (Avanceret indstilling) Yderligere parametre - Yderligere Newznab-parametre, der skal tilføjes til forespørgselslinket.
- (Avanceret indstilling) Indekserprioritet - Prioritet for denne indekser for at foretrække en indekser frem for en anden i tilfælde af ligestilling i udgivelsesscenarier. 1 er højeste prioritet, og 50 er laveste prioritet.
- (Avanceret indstilling) Minimum antal seedere - Det mindste antal seedere, der kræves for at hente en udgivelse fra denne tracker.
- (Avanceret indstilling) Seedratio - Hvis det er tomt, brug standardværdien for downloadklienten. Ellers er det mindste seedratio, der kræves for, at din downloadklient opfylder kravene for udgivelser fra denne indekser, inden den sættes på pause af din klient og fjernes af Readarr (Kræver aktivering af håndtering af fuldførte downloads - Fjern).
- (Avanceret indstilling) Seedtid - Hvis det er tomt, brug standardværdien for downloadklienten. Ellers er det mindste seedtid i minutter, der kræves for, at din downloadklient opfylder kravene for udgivelser fra denne indekser, inden den sættes på pause af din klient og fjernes af Readarr (Kræver aktivering af håndtering af fuldførte downloads - Fjern).
- (Avanceret indstilling) Discography Seed Time - Ignorer, overføres fra Lidarr.
- (Avanceret indstilling) Indekserprioritet - Prioritet for denne indekser for at foretrække en indekser frem for en anden i tilfælde af ligestilling i udgivelsesscenarier. 1 er højeste prioritet, og 50 er laveste prioritet.

## Indstillinger

- Minimumsalder - Kun Usenet: Minimumsalder i minutter for NZB'er, før de hentes. Brug dette til at give nye udgivelser tid til at sprede sig til din Usenet-udbyder.
- Bevaring - Kun Usenet: Indstil til nul for ubegrænset bevaring.
- Maksimal størrelse - Maksimal størrelse for en udgivelse, der skal hentes i MB. Indstil til nul for ubegrænset. Bemærk, at dette gælder globalt.
- RSS-synkroniseringsinterval - Interval i minutter. Indstil til nul for at deaktivere (dette stopper al automatisk hentning af udgivelser) Minimum: 10 minutter Maksimum: 120 minutter
  - Se venligst [Hvordan finder Readarr bøger?](/readarr/faq#how-does-readarr-find-books) for en bedre forståelse af, hvordan RSS-synkronisering vil hjælpe dig.

> Hvis Readarr har været offline i en længere periode, vil Readarr forsøge at bladre tilbage for at finde den sidste udgivelse, den behandlede, i et forsøg på at undgå at gå glip af en udgivelse. Så længe din indekser understøtter bladring, og det ikke er for længe siden, vil Readarr være i stand til at behandle de udgivelser, den ville have gået glip af, og undgå at du behøver at søge efter de manglende udgivelser.{.is-info}

# Downloadklienter

> Oplysninger om understøttede downloadklienter kan findes på siden [Mere info (Understøttet)](/readarr/supported#download-clients) for denne sektion
{.is-info}

## Oversigt

- Download og import er, hvor de fleste mennesker oplever problemer. Set fra et overordnet perspektiv skal softwaren kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Det betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alle opsætninger kan være lidt forskellige. Men der er mange forkerte opsætninger.

## Processer for downloadklienter

### Usenet-proces

- Readarr sender en downloadanmodning til din klient og tilknytter den til etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: bøger, tv, serier, musik osv.
- Readarr overvåger dine downloadklients aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er afsluttet, vil Readarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et andet sted end din mediemappe og er tilgængelig for Readarr.
- Readarr scanner denne afsluttede filplacering for filer, som Readarr kan bruge. Den analyserer filnavnet for at matche det med den ønskede medie. Hvis det kan gøre det, omdøber den filen i henhold til dine specifikationer og flytter den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringerne skal være de samme for din afsluttede downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Readarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er I/O-intensivt.

### Torrent-proces

- Readarr sender en downloadanmodning til din klient og tilknytter den til etiketten eller kategorinavnet, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: bøger, tv, serier, musik osv.
- Readarr overvåger dine downloadklients aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Færdiggjorte filer efterlades på deres oprindelige placering, så du kan seede filen (forhold eller tid kan justeres i downloadklienten eller fra Readarr under den specifikke downloadklient). Når filer importeres til din mediemappe, vil Readarr oprette en hardlink til filen, hvis det understøttes af din opsætning, eller kopiere den, hvis hardlinks ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din afsluttede downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Readarr falde tilbage og kopiere filen.
- Hvis indstillingen "Færdiggjort downloadhåndtering - Fjern" er aktiveret i Readarrs indstillinger, vil Readarr slette den oprindelige fil og torrent fra din klient, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet.

## Downloadklienter

Klik på `Indstillinger => Downloadklienter`, og klik derefter på <kb>+</kb> for at tilføje en ny downloadklient. Din downloadklient skal allerede være konfigureret og kørende.

### Understøttede downloadklienter

- En liste over understøttede downloadklienter findes på siden [Mere info (Understøttet)](/readarr/supported#download-clients)

Vælg den downloadklient, du ønsker at tilføje, og der vil være en pop op-boks til at indtaste forbindelsesoplysninger. Disse oplysninger er ens for de fleste klienter. Nogle vil bede om et brugernavn eller adgangskode, nogle vil spørge, om der skal tilføjes nye downloads i en pause/start-tilstand osv.

### Indstillinger for Usenet-klient

- Navn - Navnet på downloadklienten i Readarr.
- Aktivér - Aktivér denne downloadklient.
- Vært - URL'en til din downloadklient.
- Port - Porten til din downloadklient.
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- API-nøgle - API-nøglen til at godkende din klient.
- Brugernavn - Brugernavnet til at godkende din klient (normalt ikke nødvendigt).
- Adgangskode - Adgangskoden til at godkende din klient (normalt ikke nødvendigt).
- Kategori - Kategorien i din downloadklient, som \*Arr vil bruge. For at undgå urelaterede downloads i Aktivitet anbefales det stærkt at angive en kategori.
- Nylig prioritet - downloadklientprioritet for nyligt udgivet medier.
- Ældre prioritet - downloadklientprioritet for medier, der ikke er udgivet for nylig.
- (Avanceret indstilling) Klientprioritet - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet.

### Indstillinger for torrentklient

- Navn - Navnet på downloadklienten i Readarr.
- Aktivér - Aktivér denne downloadklient.
- Vært - URL'en til din downloadklient.
- Port - Porten til din downloadklient; dette er normalt webgui-porten.
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- Brugernavn - Brugernavnet til at godkende din klient.
- Adgangskode - Adgangskoden til at godkende din klient.
- Kategori - Kategorien i din downloadklient, som \*Arr vil bruge. For at undgå urelaterede downloads i Aktivitet anbefales det stærkt at angive en kategori.
- Kategori efter import - Kategorien, der skal angives efter, at udgivelsen er hentet og importeret. Bemærk, at dette bryder fjernelse af håndtering af fuldførte downloads.
- Nylig prioritet - downloadklientprioritet for nyligt udgivet medier.
- Ældre prioritet - downloadklientprioritet for medier, der ikke er udgivet for nylig.
- Indledende tilstand - Indledende tilstand for torrents (kun Qbittorrent: Tvungen omgår alle seed-tærskler).
- (Avanceret indstilling) Klientprioritet - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet.

### Kompatibilitet med fjernelse af download i torrentklient

- Readarr kan kun indstille seedratio/tid på klienter, der understøtter indstilling af denne værdi via deres API, når torrenten tilføjes. Seedmål kan indstilles globalt i klienten selv eller pr. tracker i \*Arr-indstillinger for hver indekser. Se tabellen nedenfor for klientkompatibilitet.

|      Klient       |                                Ratio                                 |                                   Tid                                    |
| :---------------: | :------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|      Deluge       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
| Download Station  | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|       Flood       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|     Hadouken      | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|    qBittorrent    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|     rTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
| Torrent Blackhole | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|   Transmission    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   | ![Idle-grænse](https://img.shields.io/badge/Understøttet-Idle%20grænse*-blue) |
|     uTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|       Vuze        |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |

> ![Idle-grænse](https://img.shields.io/badge/Understøttet-Idle%20grænse*-blue) - Transmission har internt en kontrol af inaktiv tid, men Readarr sammenligner den med seedetiden, hvis inaktivgrænsen er indstillet på en per-torrent-basis. Dette gøres som en omgåelse af Transmissions API-begrænsninger.{.is-info}

## Håndtering af fuldførte downloads

- Håndtering af fuldførte downloads er, hvordan Readarr importerer medier fra din downloadklient til dine seriemapper. Mange almindelige problemer er relateret til dårlige Docker-stier og/eller andre Docker-tilladelsesproblemer.

- Aktivér - Importer automatisk fuldførte downloads fra downloadklienten.
- (Avanceret indstilling) Fjern - Fjern fuldførte downloads, når de er færdige (Usenet) eller stoppet/fuldført (torrents).

### Fjern fuldførte downloads

- Readarr vil sende en downloadanmodning til din klient og associere den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
- Readarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er fuldført, vil Readarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et andet sted end din mediemappe.
- Readarr vil scanne den fuldførte filplacering for videofiler. Den vil analysere videofilens navn for at matche den med en bog. Hvis det kan gøre det, vil den omdøbe filen i henhold til dine specifikationer og flytte den til den tildelte biblioteksmappe.
- Overskydende filer fra downloaden vil blive sendt til papirkurven eller genbrug.

Hvis du downloader ved hjælp af en BitTorrent-klient, er processen lidt anderledes:

- Færdige filer efterlades på deres oprindelige placering for at tillade dig at seede. Når filer importeres til din tildelte biblioteksmappe, vil Readarr forsøge at oprette en hardlink til filen eller falde tilbage til at kopiere (brug dobbelt plads), hvis hardlinks ikke understøttes.
- Hvis indstillingen "Behandling af fuldførte downloads - Fjern" er aktiveret i indstillingerne, vil Readarr bede torrentklienten om at slette den oprindelige fil og torrent, men dette vil kun ske, hvis klienten rapporterer, at seeding er fuldført, torrenten er i samme kategori (dvs. ikke bruger en post-importkategori), seedmålet nås og torrenten er sat på pause (stoppet).

### Håndtering af mislykkede downloads

- Håndtering af mislykkede downloads er kun kompatibel med SABnzbd og NZBGet.
- Håndtering af mislykkede downloads gælder ikke for torrents, og der er ingen planer om at tilføje en sådan funktionalitet.

- Der er flere komponenter, der udgør processen for håndtering af mislykkede downloads:

- Kontroller downloader:
  - Kø - Kontroller din downloaders kø for adgangskodebeskyttede (krypterede) udgivelser, der er markeret som mislykkede
  - Historik - Kontroller din downloaders historik for fejl (f.eks. ikke nok til reparation eller udpakning mislykkedes)
- Når Readarr finder en mislykket download, starter den behandlingen og gør følgende:
  - Tilføjer en mislykket begivenhed til Readarrs historik
  - Fjerner den mislykkede download fra downloadklienten for at frigøre plads og rydde downloadede filer (valgfrit)
  - Begynder at søge efter en erstatningsfil (valgfrit)
  - Blokeringsliste (tidligere kendt som 'Sortliste') giver automatisk spring over af nzbs, når de mislykkes. Dette betyder, at nzb aldrig vil blive downloadet automatisk af Readarr igen (du kan stadig tvinge downloaden via en manuel søgning).
  - Der er 2 avancerede indstillinger (på siden 'Downloadklient' indstillinger), der styrer adfærden for mislykkede downloads i Readarr, i øjeblikket er de alle aktiveret som standard.

- Genhent - Kontroller, om Readarr skal søge efter den samme fil efter en fejl
- (Avanceret indstilling) Fjern - Om downloaden automatisk skal fjernes fra downloadklienten, når fejlen opdages

## Fjernstyrede sti-mappinger

- Fjernstyret sti-mapping fungerer som en simpel søgning efter fjernstien og erstatning med lokal sti. Dette bruges primært til enten fusionerede lokale/fjernopsætninger ved hjælp af mergerfs eller lignende eller bruges, når applikationen og downloadklienten ikke er på samme server.
- En fjernstyret sti-mapping bruges, når din downloadklient rapporterer en sti for fuldførte data enten på en anden server eller på en måde, som \*Arr ikke adresserer den mappe.
- Generelt er en fjernstyret sti-kort kun nødvendig, hvis din downloadklient kører på Linux, når \*Arr kører på Windows eller omvendt. En fjernstyret sti-kort kan også være nødvendig, hvis du blander Docker- og Native-klienter eller hvis du bruger en fjernserver.
- En fjernstyret sti-kort er en DUM søgning/erstatning (hvor den finder den FJERNEDE værdi, erstatter den med den LOKALE værdi for den angivne vært).
- Hvis fejlmeddelelsen om en dårlig sti ikke indeholder den ERSTATTEDE værdi, fungerer sti-mappingen ikke, som du forventer. Den typiske løsning er at tilføje og fjerne kortlægningen.
- [Se TRaSH's vejledning for yderligere oplysninger om fjernstyret sti-mapping](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og din downloadklient er Docker-containere, er det sjældent nødvendigt med en fjernstyret sti-mapping. Det anbefales at du [gennemgår Docker-guiden](/docker-guide) og/eller [følger TRaSH's vejledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlister

> Oplysninger om understøttede listetyper findes på siden [Flere oplysninger (Understøttet)](/readarr/supported#lists) for dette afsnit
{.is-info}

Importlister giver dig mulighed for automatisk at tilføje elementer til Readarr fra dine GoodReads-hylder eller fra andre brugere. Dette har potentialet til at tilføje mange uventede elementer til din Readarr-database, så brug det med forsigtighed.

![importlists.png](/assets/readarr/importlists.png)

## Importlister

Dette viser de lister, du i øjeblikket har, og giver dig mulighed for at tilføje nye lister. Tilføjelse af lister dækkes mere detaljeret nedenfor.

## Undtagelser for importlister

Alt på denne liste er blevet udelukket fra at blive tilføjet af lister og vil aldrig blive tilføjet fra nogen liste. Du kan fjerne elementer fra denne liste ved at klikke på dem.

## Tilføjelse af en importliste

Efter at have klikket på <kb>+</kb>, skal du vælge hvilken type liste, du vil tilføje:

![addlist.png](/assets/readarr/addlist.png)

I dette tilfælde vil vi tilføje en GoodReads bogreoliste.

![bookshelflist.png](/assets/readarr/bookshelflist.png)

- Navn - Indtast et navn til denne liste.
- Aktivér automatisk tilføjelse - Hvis det er aktiveret, tilføjes alt på listen automatisk til Readarr.

> Dette vil tilføje alle forfattere og ALLE BØGER fra den forfatter til Readarr!

- Overvågning - Vælg dit overvågningsniveau for tilføjede elementer. Gyldige muligheder er `Ingen`, `Valgt bog` og `Alle forfatterbøger`. Alle bøger tilføjes til Readarr, men de vil blive overvåget eller ikke-overvåget baseret på dette valg.
- Søg efter nye elementer - Hvis det er aktiveret, skal Readarr starte en søgning efter manglende overvågede elementer, når de tilføjes fra en liste. Hvis du tilføjer mange forfattere/overvågede bøger, kan dette overbelaste dit system!
- Rodmappe - Vælg rodmappe for forfattere, der tilføjes fra denne liste
- Kvalitetsprofil - Vælg din kvalitetsprofil for forfattere, der tilføjes fra denne liste
- Metadataprofil - Vælg din metadataprofil for forfattere, der tilføjes fra denne liste
- Readarr-tags - Vælg hvilke tags der gælder for forfattere, der tilføjes fra denne liste

> Det anbefales kraftigt, at du tilføjer et beskrivende tag her. Ellers vil du ikke vide, hvilken liste der har tilføjet disse elementer til Readarr, og når de er tilføjet, kan du aldrig få denne information igen! Denne information logges ikke!

Lister synkroniseres som standard hver 24. time, men kan udløses manuelt fra siden `Indstillinger` => `Opgaver`. Du kan ikke automatisere denne proces hurtigere end det.

# Forbindelse

> Oplysninger om understøttede forbindelsestyper findes på siden [Flere oplysninger (Understøttet)](/readarr/supported#notifications) for dette afsnit
{.is-info}

## Forbindelser

Forbindelser er, hvordan du vil have Readarr til at kommunikere med omverdenen.

- Ved at trykke på <kb>+</kb>-knappen får du en ny vindue, hvor du kan konfigurere mange forskellige slutpunkter

- En liste over understøttede meddelelser og forbindelser findes på siden [Flere oplysninger (Understøttet)](/readarr/supported#notifications)

## Forbindelsesudløsere

- Ved Grab - Få besked, når bøger er tilgængelige til download og er blevet sendt til en downloadklient
- Ved import af udgivelse - Få besked, når bøger er blevet importeret succesfuldt
- Ved opgradering - Få besked, når bøger opgraderes til bedre kvalitet
- Ved downloadfejl - Få besked, når en bogdownload mislykkes (kun usenet)
- Ved importfejl - Få besked, når en bogdownload mislykkes ved import
- Ved omdøbning - Få besked, når bøger bliver omdøbt
- Ved sletning af forfatter - Få besked, når en forfatter bliver slettet
- Ved sletning af bog - Få besked, når en bog bliver slettet
- Ved sletning af bogfil - Få besked, når en bogfil bliver slettet
- Ved sletning af bogfil til opgradering - Få besked, når en bogfil bliver slettet til en opgradering
- Ved omtaggning af bog - Få besked, når bøger bliver omtagggede
- Ved sundhedsproblem - Få besked om sundhedstjekfejl
  - Inkluder sundhedsadvarsler - Få besked om sundhedsadvarsler udover fejl.

# Metadata

{#write-metadata-to-book-files}

> Oplysninger om understøttede metadataforbrugere findes på siden [Flere oplysninger (Understøttet)](/readarr/supported#metadata) for dette afsnit
{.is-info}

Denne side giver dig mulighed for at oprette/opdatere metadata-tags/omslag.

![metadata.png](/assets/readarr/metadata.png)

## Calibre-metadata

Hvis du bruger Calibre til at administrere din e-bogssamling, vil du bruge disse indstillinger til at styre det.

- Send metadata til Calibre
  - Alle filer; hold synkroniseret med GoodReads - Skriv tags til alle filer og opdater, hvis GoodReads opdaterer
  - Alle filer; kun første import - Skriv tags til alle filer en gang og opdater ikke, hvis GoodReads opdaterer
  - Kun for nye downloads - Skriv tags kun til nye downloads, når de importeres
- Opdater omslag - Aktivér for at fortælle Calibre Content Server at bruge de samme bogomslag som Readarr
- Indlejr metadata i bogfiler - Aktivér for at fortælle Calibre Content Server at skrive og indlejre metadata i bogfilerne.

## Skriv metadata til lydfiler

Hvis du bruger lydbøger, vil du bruge disse indstillinger til at styre det.

- Mærk lydfiler med metadata
  - Alle filer; hold synkroniseret med GoodReads - Skriv tags til alle filer og opdater, hvis GoodReads opdaterer
  - Alle filer; kun første import - Skriv tags til alle filer en gang og opdater ikke, hvis GoodReads opdaterer
  - Kun for nye downloads - Skriv tags kun til nye downloads, når de importeres
- Rens eksisterende tags - Aktivér for at fjerne alle tags fra filer undtagen dem, der er tilføjet af Readarr

# Tags

- Tag-sektionen i Readarr bruges til at linke forskellige aspekter af Readarr.
- Tags er særligt nyttige til:

  - Udgivelsesprofiler
  - Indekser
  - Importlister

- Tags kan bruges til at linke udgivelsesprofiler, indekser, importlister og forfattere/bøger sammen.
- For eksempel:
  - Du vil have en bestemt forfatter/bog til kun at bruge en bestemt indekser. Du ville oprette en tag og tildele forfatteren/bogen og indekseren det tag.
  - Du vil have en bestemt importliste til kun at bruge en bestemt udgivelsesprofil. Du ville oprette en tag og tildele importlisten og udgivelsesprofilen det tag.

> Det anbefales kraftigt, at du tilføjer et beskrivende tag til en importliste udover det, der er nævnt ovenfor.

> Bemærk: Tags påvirker ikke nogen "Kvalitetsprofiler", "Metadataprofiler" eller andre aspekter, der ikke er nævnt ovenfor.
{.is-info}

# Generelt

Denne side er for generelle Readarr-indstillinger, der ikke er dækket i andre sektioner.

## Vært

![genhost.png](/assets/readarr/genhost.png)

- Bind-adresse - Gyldig IP4-adresse eller '*' for alle grænseflader
  - 0.0.0.0 eller `*` - enhver adresse kan oprette forbindelse
  - 127.0.0.1 eller localhost - kun lokalapplikationer kan oprette forbindelse
  - Enhver anden IP (f.eks. 1.2.3.4) - kun den IP (1.2.3.4) kan oprette forbindelse
- Portnummer - Portnummeret, som du vil bruge til at få adgang til Readarrs webbrugergrænseflade

> Bemærk: Hvis du bruger Docker, skal du ikke ændre denne indstilling.
{.is-warning}

- URL-base - Til understøttelse af omvendt proxy, standard er tom

> Bemærk: Hvis du bruger en omvendt proxy (f.eks. mydomain.com/readarr), skal du indtaste '/readarr' for URL-base.
{.is-info}

- Aktivér SSL - Hvis du har SSL-legitimationsoplysninger og gerne vil sikre kommunikationen til og fra din Readarr, skal du aktivere denne indstilling.

> Bemærk: Brug ikke dette, medmindre du ved, hvad du laver.
{.is-warning}

## Sikkerhed

![gensecurity.png](/assets/readarr/gensecurity.png)

- Godkendelse - Hvordan vil du godkende adgang til din Readarr-instans
  - Ingen - Du har ingen godkendelse for at få adgang til din Readarr. Typisk hvis du er den eneste bruger af dit netværk, ikke har nogen på dit netværk, der vil have adgang til din Readarr, eller din Readarr ikke er eksponeret for internettet
  - Grundlæggende (Browser pop-up) - Denne indstilling viser en lille pop-up, når du får adgang til din Readarr, der giver dig mulighed for at indtaste et brugernavn og adgangskode
  - Formularer (Loginside) - Denne indstilling har en velkendt login-skærm, ligesom andre websteder, der giver dig mulighed for at logge på din Readarr
- API-nøgle - Dette er, hvordan andre programmer vil kommunikere eller have Readarr til at kommunikere med andre programmer. Denne nøgle, hvis den gives til den forkerte person med adgang, kan gøre alle mulige ting ved din bibliotek. Derfor er API-nøglen sløret i logfilerne.
- Validering af certifikat - Ændrer, hvor streng HTTPS-certifikatvalidering er
  - Aktiveret - Valider alle HTTPS-certifikater (anbefales)
  - Deaktiveret for lokale adresser - Valider alle HTTPS-certifikater undtagen dem på localhost og LAN
  - Deaktiveret - Valider ikke nogen HTTPS-certifikater

## Proxy

![genproxy.png](/assets/readarr/genproxy.png)

- Proxy - Denne indstilling giver dig mulighed for at køre den information, din Radarr henter og søger efter, gennem en proxy. Dette kan være nyttigt, hvis du befinder dig i et land, der ikke tillader download af torrentfiler

- Brug proxy - Aktivér for at bruge en proxy
- Proxytype - Vælg din proxytype (HTTPS, Socks4 eller Socks5)
- Værtsnavn - Indtast dit proxy-værtsnavn (Inkluder ikke http/https eller nogen anden protokol)
- Port - Indtast din proxy-port
- Brugernavn - Indtast dit proxy-brugernavn, hvis relevant
- Adgangskode - Indtast din proxy-adgangskode, hvis relevant
- Ignorerede adresser - Indtast en kommasepareret liste over adresser, der skal omgås proxyen
- Omgå proxy for lokale adresser - Markér afkrydsningsfeltet for at omgå proxyen for lokale adresser.

## Logning

![genlogging.png](/assets/readarr/genlogging.png)

- Logniveau - Sandsynligvis et af de mest nyttige fejlfindingværktøjer
  - Info - Dette er den mest grundlæggende måde, som Readarr indsamler oplysninger på. Denne logfil indeholder fatal, fejl, advarsel og info-entréer.
  - Debug - Debug inkluderer alle de oplysninger, som Info inkluderer, plus mere information, der kan være nyttig. Denne logfil indeholder fatal, fejl, advarsel, info og debug-entréer.
  - Trace - Den mest avancerede og detaljerede logning på Readarr, Trace inkluderer alle de oplysninger, der er indsamlet af Info og Debug og mere. Dette er den mest almindelige type log, der vil blive bedt om ved fejlfinding på Discord eller Reddit. Hvis du har brug for hjælp, skal du vælge din log til Trace og gentage den opgave, der gav dig problemer for at fange loggen. Denne logfil indeholder fatal, fejl, advarsel, info, debug og trace-entréer.

## Analyse

![genanalytics.png](/assets/readarr/genanalytics.png)

- Analyse - Send anonyme brugs- og fejlinformationer til Readarrs servere (Servarr). Dette inkluderer oplysninger om din browser, hvilke Readarr WebUI-sider du bruger, fejlrapportering samt OS- og runtime-version. Vi vil bruge disse oplysninger til at prioritere funktioner og fejlrettelser.

## Opdateringer

![genupdates.png](/assets/readarr/genupdates.png)

- (Avanceret indstilling) Gren - Dette er grenen af Readarr, som du kører på.
  - [Se denne FAQ-indgang for mere information](/readarr/faq#how-do-i-update-readarr)
- Automatisk - Download og installer opdateringer automatisk. Du vil stadig kunne installere fra System: Opdateringer. Bemærk: Windows-brugere opdateres altid automatisk.
- Mekanisme - Brug Readarrs indbyggede opdateringsværktøj eller et script
  - Indbygget - Brug Readarrs eget opdateringsværktøj
  - Script - Få Readarr til at køre opdateringsscriptet
  - Docker - Opdater ikke Readarr indefra Docker, træk i stedet et helt nyt billede med den nye opdatering
- Script - Synlig kun når mekanismen er indstillet til Script - Sti til opdateringsscript
- Opdateringsproces - Readarr vil downloade opdateringsfilen, verificere dens integritet og udpakke den til en midlertidig placering og kalde den valgte metode. Opdateringsprocessen køres under den samme bruger, som Readarr kører under, den skal have tilladelser til at opdatere Readarr-filerne samt stoppe/starte Readarr.
- Indbygget - Den indbyggede metode vil tage sikkerhedskopier af Readarr-filer og -indstillinger, stoppe Readarr, opdatere installationen og starte Readarr, hvis dit system ikke håndterer stop af Readarr og forsøger at genstarte det automatisk, kan det være bedst at bruge et script i stedet. Hvis opdateringen mislykkes, startes den tidligere version af Readarr igen.
- Script - Scriptet skal håndtere det samme som det indbyggede opdateringsværktøj, hvis du skal håndtere stop og start af tjenester (upstart/launchd/etc), skal du gøre det her.

## Sikkerhedskopier

![genbackups.png](/assets/readarr/genbackups.png)

- Sikkerhedskopisektionen giver dig mulighed for at fortælle Readarr, hvordan du vil håndtere sikkerhedskopier

- Mappe - Dette giver dig mulighed for at vælge placeringen for sikkerhedskopien. I Docker vil du være begrænset til, hvad du tillader, at containeren ser. Stier er relative til appdata-mappen; hvis det er nødvendigt, kan du angive en absolut sti til sikkerhedskopiering uden for appdata-mappen.
- Interval - Hvor ofte vil du have, at Readarr skal lave en sikkerhedskopi
- Opbevaring - Hvor længe vil du have, at Readarr skal beholde hver sikkerhedskopi. Efter at en ny sikkerhedskopi er lavet, vil den ældste sikkerhedskopi blive fjernet

Som standard udføres sikkerhedskopier hver 7. dag, og de sidste 4 opbevares.

# UI (Brugergrænseflade)

Denne side giver dig mulighed for at tilpasse indstillingerne for brugergrænsefladen.

## Kalender

![uicalendar.png](/assets/readarr/uicalendar.png)

- Første ugedag - Her kan du vælge, hvilken dag du mener, der skal være den første dag i ugen.
- Ugekolonneoverskrift - Her kan du vælge overskriften for kolonnerne.

## Datoer

![caldates.png](/assets/readarr/caldates.png)

- Kort datoformat - Hvordan vil du have, at Readarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du have, at Readarr skal vise datoer i langt format?
- Tidsformat - Vil du have et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du have, at Readarr skal vise relative (i dag/i går/osv.) eller absolutte datoer?

## Stil

![calstyle.png](/assets/readarr/calstyle.png)

- Aktivér farveblindtilstand - Ændret stil for at gøre det lettere for farveblinde brugere at skelne farvekodede oplysninger.

## Sprog

![callanguage.png](/assets/readarr/callanguage.png)

- Brugergrænsefladesprog - Vælg sproget, som Radarr skal bruge i applikationens brugergrænseflade.