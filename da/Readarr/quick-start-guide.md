---
title: Readarr Hurtigstartsguide
description: 
published: true
date: 2022-09-07T23:19:05.590Z
tags: readarr
editor: markdown
dateCreated: 2021-12-11T19:42:31.825Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Hurtigstartopsætningsguide](#hurtigstartopsætningsguide)
- [Opstart](#opstart)
- [Mediehåndtering](#mediehåndtering)
- [Bognavngivning](#bognavngivning)
- [Mapper](#mapper)
- [Importering](#importering)
- [Filhåndtering](#filhåndtering)
- [Rodmapper og Calibre-integration](#rodmapper-og-calibre-integration)
  - [Calibre-indholdsserver (valgfrit)](#calibre-indholdsserver-valgfrit)
  - [Calibre-integration](#calibre-integration)
- [Downloadklienter](#downloadklienter)
  - [{.tabset}](#tabset)
    - [Usenet](#usenet)
    - [BitTorrent](#bittorrent)
- [Sådan importerer du dit eksisterende organiserede mediebibliotek](#sådan-importerer-du-dit-eksisterende-organiserede-mediebibliotek)
  - [Importering af eksisterende medier](#importering-af-eksisterende-medier)
- [Tilføj nye bøger](#tilføj-nye-bøger)

# Hurtigstartopsætningsguide

> Denne side er stadig under udarbejdelse og er ikke fuldstændig. Bidrag er velkomne.

> For en mere detaljeret gennemgang af alle indstillinger, se [Readarr => Indstillinger](/readarr/settings)
{.is-info}

I denne guide vil vi forsøge at forklare den grundlæggende opsætning, du skal udføre for at komme i gang med Readarr. Vi vil springe nogle indstillinger over, som du måske ser på skærmen. Hvis du vil dykke dybere ned i disse, kan du se den relevante side i FAQ'en og dokumentationen for en fuld forklaring.

> Bemærk venligst, at inden for skærmbillederne og GUI-indstillingerne i `orange` er avancerede indstillinger, så du skal klikke på `Vis avanceret` øverst på siden for at gøre dem synlige.
{.is-warning}

# Opstart

Efter installation og opstart åbner du en browser og går til `http://{din_ip_her}:8787`

![qs_startup.png](/assets/readarr/qs_startup.png)

# Mediehåndtering

Først kigger vi på indstillingerne for `Mediehåndtering`, hvor vi kan konfigurere vores foretrukne navngivning og filhåndteringsindstillinger.

`Indstillinger` => `Mediehåndtering`

![mediamanagement.png](/assets/readarr/mediamanagement.png)

# Bognavngivning

![booknaming.png](/assets/readarr/booknaming.png)

- Aktivér/deaktivér omdøbning af dine bøger (i modsætning til at lade navnene være som de er, eller som de var, da du downloadede dem).
- Hvis du vil have erstattet eller fjernet ulovlige tegn (`\ / : * ? " < > | ~ - % & + { }`).
- Her vælger du navngivelseskonventionen for de faktiske bogfiler. Bemærk, at navnet på bogmappen også defineres her.
- `(Avanceret indstilling) Her indstiller du navngivelseskonventionen for forfattermappen.`

> Dette gælder ikke, hvis Calibre bruges, da Calibre håndterer fil-/mappenavngivelse ved hjælp af sin egen interne skema.
{.is-info}

# Mapper

![folders.png](/assets/readarr/folders.png)

- (Avanceret indstilling) Opret tomme forfattermapper - Aktivér for at oprette tomme forfattermapper, når en ny forfatter tilføjes til Readarr.
- (Avanceret indstilling) Slet tomme mapper - Aktivér for at slette tomme forfattermapper, når der ikke er flere bøger tilbage for den forfatter.

> En af disse felter kan afkrydses, men BEGGE felter skal ikke afkrydses.
{.is-warning}

> Dette gælder ikke, hvis Calibre bruges, da Calibre håndterer fil-/mappenavngivelse ved hjælp af sin egen interne skema.
{.is-info}

# Importering

![importing.png](/assets/readarr/importing.png)

- (Avanceret indstilling) Spring over kontrol af ledig plads - Hvis aktiveret springes kontrol af ledig plads over inden importering.
- (Avanceret indstilling) Minimum ledig plads - Indtast den mindste ledige plads, som drevet skal have, før importeringen stopper.
- (Avanceret indstilling) Brug hardlinks i stedet for kopier - Afkryds denne boks for at bruge hardlinks i stedet for kopier (til torrents). Bemærk, at dette er aktiveret som standard.
  
> Du bør ideelt set bruge dette, hvor det er muligt. For at kunne bruge hardlinks skal du have din kilde/destination på det samme filsystem (drev, partition) og monteringspunkter. [Se TRaSH's Hardlink Guide for mere information](https://trash-guides.info/hardlinks/)
{.is-info}
  
- Importer ekstra filer - Hvis aktiveret, importeres de angivne ekstra filer, der findes i bogens mappe, når den importeres.
- (Avanceret indstilling) Importer ekstra filer - Hvis "Importer ekstra filer" er aktiveret, skal du indtaste en kommasepareret liste over filtypetilføjelser, der skal importeres.

> Hvis du bruger Readarr til lydbøger, skal du tilføje .cue til denne liste, da den indeholder dine kapiteloplysninger!
{.is-info}

# Filhåndtering

![filemanagement.png](/assets/readarr/filemanagement.png)

- Bøger, der er slettet fra disken, overvåges automatisk ikke længere i Readarr.

- Ignorer slettede bøger - Afkryds denne boks for at fjerne overvågning af bøger, der er markeret som slettet eller utilgængelige fra Readarr's rodmappe.
- Download korrekte og repacks - Om du automatisk vil opgradere til korrekte og repacks. Brug "Foretræk ikke" til at sortere efter foretrukken ordvurdering frem for korrekte og repacks.
  - Foretræk og opgrader - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl nye repacks og korrekte som opgradering til nuværende udgivelser.
  - Opgrader ikke automatisk - Ranger repacks og korrekte højere end ikke-repacks og ikke-korrekte. Behandl ikke nye repacks og korrekte som opgradering til nuværende udgivelser.
  - Foretræk ikke - Ignorer i praksis repacks og korrekte. Du skal selv håndtere eventuelle præferencer for disse med [Foretrukne ord](#udgivelsesprofiler).

> \* `PROPER` - betyder, at der var et problem med den foregående udgivelse. Downloads, der er mærket som PROPER, viser, at problemerne er blevet løst i den udgivelse. Dette er udført af en gruppe, der ikke udgav originalen.
> \* `REPACK` - betyder, at der var et problem med den foregående udgivelse, og det er blevet rettet af den oprindelige gruppe. Downloads, der er mærket som REPACK, viser, at problemerne er blevet løst i den udgivelse. Dette er udført af en gruppe, der udgav originalen.
{.is-info}

- (Avanceret indstilling) Overvåg rodmapper for filændringer - Afkryds denne boks for at udløse en genindlæsning, når det registreres, at rodmappe er blevet ændret.
- (Avanceret indstilling) Genindlæs forfattermappe efter opdatering - Vælg, hvornår en forfattermappe skal genindlæses efter opdatering af forfatteren.
  - Altid - Dette vil genindlæse forfattermapper baseret på opgaveplanlægningen
  - Efter manuel opdatering - Du skal manuelt genindlæse disken
  - Aldrig - Som det står, genindlæs aldrig forfattermapperne.
- (Avanceret indstilling) Tillad fingeraftryk - Vælg, hvordan fingeraftryk skal håndteres, hvilket giver øget nøjagtighed for bogmatchning, på bekostning af CPU-/disktid.
  - Altid - Brug altid fingeraftryk, hvis det er muligt
  - Kun for nye importeringer - Kun brug fingeraftryk for nyimporterede udgivelser
  - Aldrig - Som det står, brug aldrig fingeraftryk
- (Avanceret indstilling) Ændre fildato - Ændre filens dato ved import/genindlæsning
  - Ingen - Readarr ændrer ikke datoen, der vises i din filbrowser
  - Bogudgivelsesdato - Datoen, bogen blev udgivet.
- (Avanceret indstilling) Genbrugspapirkurv - Bogfiler vil blive flyttet hertil, når de slettes, i stedet for at blive slettet permanent
- (Avanceret indstilling) Rensning af genbrugspapirkurv - Dette er, hvor gammel en given fil kan være, før den slettes permanent

> Det anbefales stærkt at bruge en genbrugspapirkurv. Det er nemt at slette filer, og det er nemt at gendanne dem, hvis du bruger papirkurven.
{.is-warning}

# Rodmapper og Calibre-integration

![rootfolders1.png](/assets/readarr/rootfolders1.png)

Her tilføjer vi rodmappe, som Readarr vil bruge til at importere dit eksisterende organiserede mediebibliotek, og hvor Readarr vil importere (kopiere/hardlink/flytte) dine medier efter, at din downloadklient har downloadet dem.

> **Brugeren og gruppen, du har konfigureret Readarr til at køre som, skal have læse- og skriveadgang til dette sted.** {.is-info}

Du kan også vælge at bruge Calibre til at administrere dit bibliotek på denne skærm. Dette kræver, at du kører Calibre Content Server. Dette er IKKE Calibre-Web.

> Brugere, der ikke bruger Windows:
> \* Hvis du bruger et NFS-mount, skal du sørge for, at `nolock` er aktiveret.
> \* Hvis du bruger et SMB-mount, skal du sørge for, at `nobrl` er aktiveret.
{.is-warning}

> Hvis du vil bruge Calibre, skal de bøger, du vil have, at Readarr skal genkende ved den første biblioteksimport, **allerede være i Calibre**. Bøger i mappen, der ikke er i Calibre, vil blive ignoreret. Hardlinks bruges ikke, når Calibre-integration tilføjes.
> **Bemærk, at du ikke kan tilføje Calibre-integration til en rodmappe, efter at den er oprettet.**
{.is-danger}

> Din downloadklient downloader til en downloadmappe, og Readarr importerer det til din mediemappe (endelig destination), som din medieserver bruger. Din downloadmappe og mediemappe kan ikke være det samme sted!
{.is-warning}

Glem ikke at gemme dine ændringer.

## Calibre-indholdsserver (valgfrit)

Hvis du vil bruge Calibre til at administrere dine bøger, skal du konfigurere Calibre-indholdsserveren. Dette er igen ikke Calibre-Web, men en del af Calibre selv. Du skal køre Calibre, og du skal konfigurere indholdsserveren.

> Hvis du vælger at bruge Calibre, kan du ikke ændre noget i Calibres database. Hvis du ikke overholder denne advarsel, bliver du nødt til at slette din Readarr-database og starte forfra
{.is-danger}

Hvis du bruger Docker, skal din Calibre-monterede bogmappe og din Readarr-monterede bogmappe være den samme.

> Bemærk, at mens Readarr er i beta, anbefales det at deaktivere omdøbning i Readarr, bare for at være på den sikre side, hvis der skulle opstå en utilsigtet fejl.
{.is-info}

For at gøre dette åbner du Calibre og klikker på `Indstillinger / Deling over netværket`

![calibreprefs.png](/assets/readarr/calibreprefs.png)

Først tilføjer du en brugerkonto. Kontoen skal have adgang til "make changes".

![calibreacct.png](/assets/readarr/calibreacct.png)

Derefter skal du genstarte Calibre. Når du er tilbage, konfigurerer og starter du indholdsserveren. Den skal vise, at den kører. Indstil den til at køre automatisk ved opstart. Efter at have gemt, skal du genstarte Calibre igen. Sørg for, at serveren er startet, når den starter op igen, og gå derefter videre til næste sektion.

> Du skal vælge "Require username and password to access the content server" for at Readarr kan fungere korrekt. Hvis du ikke gør det, får du en fejlmeddelelse, der siger "Anonymous users are not allowed to make changes", når Readarr importerer en bog!
{.is-info}

![calibreserver.png](/assets/readarr/calibreserver.png)

## Calibre-integration

![calibre1.png](/assets/readarr/calibre1.png)

Nedenstående er Calibre-specifikke indstillinger og vises kun, hvis `Brug Calibre` er aktiveret

- Brug Calibre - Aktivér/deaktivér brugen af Calibre-indholdsserver til at administrere din rodmappe.

> \* Bemærk, at dette **ikke kan aktiveres på en eksisterende rodmappe**.
> \* Bemærk, at dette **ikke kan deaktiveres på en eksisterende rodmappe med Calibre-integration**.
> \* Bemærk, at dette kræver **Calibre-indholdsserver** og ikke fungerer med Calibre Web eller Calibre.
> \* Bemærk, at hardlinks ikke fungerer med Calibre-integration.
> \* Bemærk, at det kræver, at Calibre har aktiveret "Require username and password to access the content server".
> \* Hvis "Require username and password to access the content server" ikke er aktiveret i Calibre, får du en fejlmeddelelse med "Anonymous users are not allowed to make changes"
{.is-warning}

> Hvis du vælger at bruge Calibre, kan du ikke ændre noget i Calibres database. Hvis du ikke overholder denne advarsel, bliver du nødt til at slette din Readarr-database og starte forfra
{.is-danger}

- Calibre-vært - IP-/domænenavnet på værten for Calibre-indholdsserveren
- Calibre-port - Porten, som Calibre-indholdsserveren lytter på
- (Avanceret) Calibre-URL-base - Tilføj et præfiks til Calibre-URL'en, f.eks. `http://[vært]:[port]/[urlBase]`
- Calibre-brugernavn - Brugernavn til at få adgang til Calibre-indholdsserveren
- Calibre-adgangskode - Adgangskode til at få adgang til Calibre-indholdsserveren
- Calibre-bibliotek - Navnet på Calibre-indholdsserverbiblioteket. Lad det være tomt for standardværdien
- Konverter til format - (Valgfrit) Bed Calibre-indholdsserveren om at konvertere til andre formater med en kommasepareret liste.
  - Gennemgå ikonet (i) i appen for en aktuel liste over muligheder.
  - Mulighederne er: MOBI, EPUB, AZW3, DOCX, FB2, HTMLZ, LIT, LRF, PDB, PDF, PMLZ, RB, RTF, SNB, TCR, TXT, TXTZ, ZIP
- Calibre-outputprofil - Vælg Calibre-indholdsserverens outputprofil, der skal bruges
  - Outputprofilen fortæller Calibre-indholdsserverens konverteringssystem, hvordan dokumentet skal optimeres til den angivne enhed (f.eks. ved at ændre størrelsen på billeder til enhedens skærmstørrelse). I nogle tilfælde kan en outputprofil bruges til at optimere outputtet til en bestemt enhed, men dette er sjældent nødvendigt.
- Brug SSL - Aktivér eller deaktivér brugen af SSL (HTTPS) til Calibre-indholdsserveren

> Hvis du tilføjer en enkelt bog og vælger `None`\* for [metadataprofilen](/readarr/settings#metadata-profiles), vil kun den bog blive vist under forfatteren, når den tilføjes. Hvis du vil have andre bøger tilføjet til den forfatter, skal du vælge en passende metadataprofil.
> \* **Bemærk, at `None` ikke anvender nogen metadatafiltre, og du kan få uønskede udenlandske udgaver. For at omgå dette [opretter du en metadataprofil som beskrevet i FAQ'en](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Downloadklienter

`Indstillinger` => `Downloadklienter`

Download og importering er, hvor de fleste mennesker oplever problemer. Set fra et overordnet perspektiv skal softwaren kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Det betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alle opsætninger kan være lidt forskellige. Men der er mange forkerte opsætninger.

> Se [indstillingssiden](/readarr/settings#download-clients), på siden [Mere info (Understøttet)](/readarr/supported#download-clients) for denne sektion og [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for mere information.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Readarr sender en downloadanmodning til din klient og forbinder den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Readarr overvåger dine downloadklients aktive downloads, der bruger det kategorinavn. Overvågningen sker via din downloadklients API.
- Når downloaden er afsluttet, kender Readarr den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe og kan tilgås af Readarr.
- Readarr scanner denne afsluttede filplacering for filer, som Readarr kan bruge. Den analyserer filnavnet for at matche det med det ønskede medie. Hvis det kan gøre det, omdøber den filen i henhold til dine specifikationer og flytter den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringspunkterne skal være de samme for din afsluttede downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Readarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er I/O-intensivt.
- Hvis indstillingen "Behandling af afsluttede downloads - Fjern" er aktiveret i Readarrs indstillinger, sendes resterende filer fra downloaden til papirkurven eller genbrugspapirkurven via en anmodning til din klient om at slette/fjerne udgivelsen.

### BitTorrent

{#bittorrent}

- Readarr vil sende en downloadanmodning til din klient og associere den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Readarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Denne overvågning sker via din downloadklients API.
- Færdige filer efterlades på deres oprindelige placering for at tillade dig at seede filen (ratio eller tid kan justeres i downloadklienten eller fra Readarr under den specifikke downloadklient). Når filer importeres til din mediemappe, vil Readarr oprette en hardlink til filen, hvis det understøttes af din opsætning, eller kopiere den, hvis hardlinks ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din færdige downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Readarr falde tilbage og kopiere filen.
- Hvis indstillingen "Færdig downloadhåndtering - Fjern" er aktiveret i Readarrs indstillinger, vil Readarr slette torrenten fra din klient og bede klienten om at fjerne torrentdataene, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet (pauser ved fuldførelse).

# Sådan importerer du dit eksisterende organiserede mediebibliotek

> Bemærk, at Readarr ikke regelmæssigt søger efter bøger. Se disse to FAQ-indlæg for detaljer for at forstå, hvordan Readarr fungerer.
[Hvordan finder Readarr bøger?](/readarr/faq#how-does-readarr-find-books) og [Hvordan fungerer Readarr?](/readarr/faq#how-does-readarr-work)
{.is-info}

Efter at have konfigureret dine profiler/kvalitetsstørrelser og tilføjet dine indexere og downloadklient(er), er det tid til at importere dit eksisterende organiserede mediebibliotek.

Kommer snart - Bidrag er velkomne

## Import af eksisterende medier

Kommer snart - Bidrag er velkomne

# Tilføj nye bøger

[Henvend dig til bibliotekssiden for yderligere information](/readarr/library#add-new)