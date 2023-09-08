---
title: Readarr Bibliotek
description: 
published: true
date: 2021-11-30T01:41:54.243Z
tags: readarr, needs-love, library
editor: markdown
dateCreated: 2021-11-30T00:50:59.442Z
---

# Bibliotek

Denne sektion er til styring af dit bibliotek med [forfattere](#forfattere) og [bøger](#bøger).

# Forfattere

- Biblioteksvisning
  - Opdater alle - Opdater metadata for alle forfattere, opdater plakater, genindlæs forfattermapper og genindlæs bogfiler (hvis aktiveret)
  - Opdater og Scan - Opdater metadata for den aktuelt viste forfatter og genindlæs dens mappe
  - RSS-synkronisering - Opdater RSS-feedet fra dine indexere og se om der er noget nyt, der kan hentes
  - Forfatterredigering / Forfatterindeks - Skift mellem masseeditor-tilstand og forfatterindeks (bibliotek) tilstand
  - Indstillinger - Skift visningsindstillinger
  - Visning - Skift visningstype
    - Tabel - Tabulær visning (listevisning)
    - Plakater - Vis plakater (lignende Plex)
    - Oversigt - Vis oversigtsinformation og plakaten (detaljeret visning)
  - Sorter - Sorter den aktuelle visning
  - Filtrer - Filtrer den aktuelle visning

# Bøger

- Biblioteksvisning
  - Opdater alle - Opdater metadata for alle forfattere, opdater plakater, genindlæs forfattermapper og genindlæs bogfiler (hvis aktiveret)
  - Opdater og Scan - Opdater metadata for den aktuelt viste forfatter og genindlæs dens mappe
  - RSS-synkronisering - Opdater RSS-feedet fra dine indexere og se om der er noget nyt, der kan hentes
  - Søg alle / Søg filtreret / Søg valgte - Søg i alle bøger eller valgte bøger i den aktuelle visning
  - Bogredigering / Bogindeks - Skift mellem masseeditor-tilstand og bogindeks (bibliotek) tilstand
  - Indstillinger - Skift visningsindstillinger
  - Visning - Skift visningstype
    - Tabel - Tabulær visning (listevisning)
    - Plakater - Vis plakater (lignende Plex)
    - Oversigt - Vis oversigtsinformation og plakaten (detaljeret visning)
  - Sorter - Sorter den aktuelle visning
  - Filtrer - Filtrer den aktuelle visning
  
# Tilføj Ny

![addnew.png](/assets/readarr/addnew.png)

- Du kan tilføje nye forfattere eller individuelle bøger ved at indtaste forfatterens navn eller bogens navn her og vælge det fra resultatlisten.
  - Du finder vejledningen i vores [Hurtigstartguide](/readarr/quick-start-guide)
- Du kan også tilføje forfattere ved hjælp af GoodReads ID, ISBN eller ASIN efter behov ved at bruge det viste format.

![poe.png](/assets/readarr/poe.png)

- Klik på forfatterens eller bogens navn for at tilføje det til Readarr. En boks vil dukke op med muligheder for dig.

![addauthor.png](/assets/readarr/addauthor.png)

- Rodmappe - Vælg rodmappe her. Skift ikke dette, hvis du bruger Calibre Content Server.
- Overvåg - Vælg overvågningsstatus for alle bøger af denne forfatter.
- Kvalitetsprofil - Vælg kvalitetsprofilen, der skal bruges, når du søger efter bøger af denne forfatter.
- (Kun bog) Metadataprofil - Vælg metadataprofilen, der skal bruges til denne bog.
- Tags - Hvis du vil have en tag anvendt på denne forfatters bøger, skal du indtaste den her.
- Start søgning efter manglende bog(e) - Vælg, om du vil starte en historisk søgning af dine indexere efter alle bøger af denne forfatter med det samme. Hvis du ikke gør dette, vil kun NYE uploadede bøger blive hentet fra dette tidspunkt og fremefter.
- Tilføj {Forfatternavn} eller Tilføj {Bognavn} - Klik på Tilføj-knappen for at tilføje denne forfatter til Readarr og begynde at hente metadata for alle bøger af denne forfatter. Denne proces kan tage noget tid, så det vil være fornuftigt ikke at tilføje for mange forfattere for hurtigt.

>Hvis du tilføjer en individuel bog og vælger `None`\* for [metadataprofilen](/readarr/settings#metadata-profiles), vil kun den bog blive vist under forfatteren, når den er tilføjet. Hvis du vil have andre bøger af den forfatter tilføjet, skal du vælge en passende metadataprofil.
> \* **Bemærk, at `None` ikke anvender nogen metadatafiltre, og du kan få uønskede udenlandske udgaver. For at omgå dette [opret en metadataprofil som beskrevet i FAQ'en](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Uafmappede Filer

![unmappedfiles.png](/assets/readarr/unmappedfiles.png)

Hvis der er bøger opført her, er de ikke genkendt af Readarr og er ikke opført som "eksisterende" i Readarr, men de er i en af de rodmapper, du har defineret.

Du kan få mere information ved at klikke på *i*-ikonet til højre.

Du kan manuelt importere bogen ved at klikke på *person*-ikonet til højre.

Du kan slette bogfilen ved at klikke på *skraldespand*-ikonet til højre.

Du kan også klikke på *Tilføj manglende* øverst for at forsøge at tilføje alle bøger til Readarr. Bemærk, at dette kan være tidskrævende, hvis du har mange bøger opført her.