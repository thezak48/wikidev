---
title: Radarr Bibliotek
description: 
published: true
date: 2022-11-14T15:04:06.364Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:24:18.386Z
---

# Film

## Biblioteksvisning

- Opdater alle - Opdater metadata for alle film, opdater plakater, genindlæs filmmapper og genindlæs filmfiler (hvis aktiveret)
- Opdater og Scan - Opdater metadata for den aktuelt viste film og genindlæs dens mappe
- RSS-synkronisering - Opdater RSS-feedet fra dine indekser og se om der er noget nyt, der kan hentes
- Søg alle / Søg filtreret / Søg valgt - Søg i alle film eller valgte film i den aktuelle visning
- Manuel import (filmregister) - Importer manuelt en filmfil til en film, du har tilføjet til Radarr fra en hvilken som helst mappe, som Radarr kan få adgang til
  - Flyt automatisk - Forsøg automatisk at matche en fil til en film i Radarr og importer ved at flytte den.
  - Interaktiv import - Gennemgå alle filer inden for stien og forsøg at matche til en film i Radarr, så brugeren kan gennemgå resultaterne. Flyt eller kopier/hardlink er en valgmulighed i nederste venstre hjørne.
- Manuel import (film) - Importer manuelt en filmfil til en film, du har tilføjet til Radarr fra filmens tildelte mappe
  - Flyt automatisk - Forsøg automatisk at matche en fil til en film i Radarr og importer ved at flytte den.
  - Interaktiv import - Gennemgå alle filer inden for stien og forsøg at matche til en film i Radarr, så brugeren kan gennemgå resultaterne. Flyt eller kopier/hardlink er en valgmulighed i nederste venstre hjørne.
- Filmredaktør / Filmregister - Skift mellem masseeditor-tilstand og filmregister-tilstand
- Indstillinger - Skift visningsindstillinger
- Visning - Skift visningstype
  - Tabel - Tabulær visning (listevisning)
  - Plakater - Vis plakater (lignende Plex)
  - Oversigt - Vis oversigtsinformation og plakaten (detaljeret visning)
- Sorter - Sorter den aktuelle visning

### Filtre

- Filter - Filtrer den aktuelle visning
  - Kun overvåget - Titler, der overvåges for opdateringer.
  - Ikke-overvåget - Titler, der IKKE overvåges for opdateringer.
  - Manglende - I databasen, overvåget, men mangler i filsystemet.
  - Efterspurgte - I databasen, overvåget, mangler, men burde være tilgængelige baseret på tilgængelighedsindstillingerne
  - Afkortningskrav ikke opfyldt - Titel på filsystemet, men overvåger stadig efter ønsket kvalitet.
  - Brugerdefinerede filtre
    - Overvåget (boolesk)
    - Betragtes som tilgængelig (boolesk)
    - Minimum tilgængelighed (Enum)
      - Annonceret
      - I biograferne
      - Udgivet
    - Titel \[indeholder\] (Streng)
    - Udgivelsesstatus (Enum)
      - TBA
      - Annonceret
      - I biograferne
      - Udgivet
      - Slettet
        - Slettet fra TMDb
    - Studie (Enum Studios)
    - Samling (Enum Collections)
    - Kvalitetsprofil (Enum QualityProfiles)
    - Tilføjet (statisk DateTime, relativ TimeDelta)
    - År (Int)
    - I biograferne (statisk DateTime, relativ TimeDelta)
    - Fysisk udgivelse (statisk DateTime, relativ TimeDelta)
    - Digital udgivelse (statisk DateTime, relativ TimeDelta)
    - Spilletid (Int)
    - Sti \[indeholder\] (Streng)
    - Størrelse på disk (Int)
    - Genrer \[indeholder\] (Enum Genres)
    - TMDB-vurdering (Float)
    - TMDB-stemmer (Int)
    - IMDb-vurdering
    - Tomatovurdering
    - IMDb-stemmer
    - Certificering (Enum Rating (PG-13, R, osv.))
    - Tags \[indeholder\] (Enum Tags)

# Tilføj ny

![radarr-add-new-empty.png](/assets/radarr/radarr-add-new-empty.png)

- Hvis du vil tilføje en ny film, er dette siden, du vil gøre det fra.
  - Du finder vejledningen i vores [Hurtigstartguide](/radarr/quick-start-guide).
- Under søgefeltet kan du også finde knappen Importer eksisterende film. Hvis det er tilfældet for dig, kan du finde gode oplysninger om det også i vores [Hurtigstartguide](/radarr/quick-start-guide).
- Hvis du får en fejlmeddelelse om "stien allerede er konfigureret", [se denne FAQ-indgang](/radarr/faq#path-is-already-configured-for-an-existing-movie).

# Biblioteksimport

Biblioteksimport giver dig mulighed for at importere eksisterende organiserede film og hver films fil via eksisterende filer i sti-mappen. Dette er særligt nyttigt, når du opretter en ny Radarr-instans og ønsker at beholde dine eksisterende film.

- Biblioteksimport er til tilføjelse og import af et eksisterende organiseret bibliotek med film til Radarr.
- Biblioteksimport kan ikke bruges til:
  - Import af filer fra en downloadmappe
  - Tilføjelse eller import af en eller flere filer, der ikke er korrekt navngivet og organiseret i deres egen filmmappe inden for din rodmappe eller en mappe, du ønsker at tilføje som en rodmappe
  - Andre anvendelser, der ikke indebærer tilføjelse af en film til Radarr og import af filmen og dens fil fra den rod (biblioteks)mappe, der blev angivet for biblioteksimport
- Hvis du får en fejlmeddelelse om "stien allerede er konfigureret", [se denne FAQ-indgang](/radarr/faq#path-is-already-configured-for-an-existing-movie).

> Det er påkrævet, at filmmapper og filer har året i deres navn for at blive importeret og analyseret.{.is-warning}

> \* Ikke-Windows: Hvis du bruger en NFS-montering, skal du sørge for, at `nolock` er aktiveret.
> \* Hvis du bruger en SMB-montering, skal du sørge for, at `nobrl` er aktiveret.
{.is-warning}

> **Brugeren og gruppen, du har konfigureret Radarr til at køre som, skal have læse- og skriveadgang til dette sted.**
{.is-info}

> Din downloadklient downloader til en downloadmappe, og Radarr importerer det til din mediemappe (endelige destination), som din medieserver bruger.
{.is-info}

> **Din downloadmappe og mediemappe kan ikke være den samme placering**
{.is-danger}

# Samlinger

Wikien udvikles og vedligeholdes af fællesskabet.
Der er ikke blevet foretaget nogen bidrag til denne sektion for at afspejle og beskrive samlingssiden i Radarr.

# Opdag

Opdag viser anbefalede film

- Hvis du ikke har nogen lister, vises de 90 mest anbefalede film baseret på TMDb-film, der anbefales til filmene i dit bibliotek, samt de 10 anbefalinger fra dine seneste tilføjelser.

> Tip: Du kan deaktivere Radarr-anbefalede film og kun se film fra dine lister i `Indstillinger`.
{.is-info}

- Hvis du har lister, vises de ovennævnte anbefalinger OG poster fra dine lister.

> Tip: Skift `Filter` til `Ny ikke-ekskluderet` for kun at vise film, der ikke er i dit bibliotek.
{.is-info}

![radarr-discover-empty.png](/assets/radarr/radarr-discover-empty.png)

- Hvis du har en ny installation med få eller ingen film, er det sandsynligt, at dine opdagelsesanbefalinger vil være sparsomme. Du skal tilføje indhold til biblioteket for at få anbefalinger. Du har flere muligheder:
  1. Klik på knappen [Tilføj ny film](/radarr/library#add-new) for at tilføje film manuelt.
  1. Klik på knappen [Importer eksisterende bibliotek](/radarr/library#library-import) for at importere et eksisterende bibliotek.
  1. Klik på knappen [Tilføj lister](/radarr/settings#lists) for at tilføje en liste til Radarr. Yderligere oplysninger om lister kan findes på siden [Mere info (Understøttet)](/radarr/faq#what-are-lists-and-what-can-they-do-for-me) for denne sektion.

![radarr-discover-add-new-movies.png](/assets/radarr/radarr-discover-add-new-movies.png)

- Når du har tilføjet en film ved en af de tre ovennævnte muligheder, får du præsenteret forskellige film at opdage.
    1. Her kan du vælge, hvilke film du vil tilføje til dit bibliotek
    1. Her kan du vælge alle filmene på denne liste, hvis du føler dig ekstra vild
    1. Vælg, hvilken rodmappe du vil have, at disse film skal gå til, når de er importeret
    1. Vælg, hvilken tilgængelighed filmen skal have, inden den hentes
    1. Vælg eventuelle kvalitetsprofiler, du allerede har oprettet ([Flere oplysninger](/radarr/settings#quality-profiles))
    1. Vil du have, at Radarr skal overvåge denne film for eventuelle opgraderinger i kvalitet?
    1. Vil du have, at Radarr automatisk skal søge efter denne film, efter at du har tilføjet den?
    1. Vil du have, at Radarr skal udelukke disse film fra eventuelle lister, der ville blive importeret? ([Flere oplysninger](/radarr/settings#list-exclusion))
    1. Til sidst, tilføj filmen til dit bibliotek.