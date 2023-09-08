---
title: Radarr Bibliotek
description: 
published: true
date: 2022-11-14T15:04:06.364Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:24:18.386Z
---

# Filmer

## Bibliotekvisning

- Oppdater alle - Oppdater metadata for alle filmer, oppdater plakater, skann mapper for filmer på nytt, og skann filer for filmer på nytt (hvis aktivert)
- Oppdater og skann - Oppdater metadata for den gjeldende filmen og skann mappen for den på nytt
- RSS-synkronisering - Oppdater RSS-feeden fra indekserne dine og se om det er noe nytt som har blitt lagt ut for å bli lastet ned
- Søk alle / Søk filtrert / Søk valgt - Søk etter alle filmer eller valgte filmer i gjeldende visning
- Manuell import (filmindeks) - Manuelt importer en filmfil for en film du har lagt til i Radarr fra hvilken som helst mappe som Radarr har tilgang til
  - Flytt automatisk - Forsøk automatisk å matche en fil med en film i Radarr og importer ved å flytte den.
  - Interaktiv import - Gå gjennom alle filene i banen og prøv å matche med en film i Radarr slik at brukeren kan gjennomgå resultatene. Flytt eller kopier/hardlink er et valgbart alternativ i nedre venstre hjørne.
- Manuell import (film) - Manuelt importer en filmfil for en film du har lagt til i Radarr fra filmens tildelte mappe
  - Flytt automatisk - Forsøk automatisk å matche en fil med en film i Radarr og importer ved å flytte den.
  - Interaktiv import - Gå gjennom alle filene i banen og prøv å matche med en film i Radarr slik at brukeren kan gjennomgå resultatene. Flytt eller kopier/hardlink er et valgbart alternativ i nedre venstre hjørne.
- Filmredigerer / Filmindeks - Bytt mellom Masseredigeringsmodus og Filmindeks (Bibliotek) modus
- Alternativer - Endre visningsalternativer
- Visning - Bytt visningstype
  - Tabell - Tabellvisning (listevisning)
  - Plakater - Vis plakater (lik Plex)
  - Oversikt - Vis oversiktsinformasjon og plakaten (detaljert visning)
- Sorter - Sorter gjeldende visning

### Filtre

- Filter - Filtrer gjeldende visning
  - Kun overvåket - Titler som overvåkes for oppdateringer.
  - Uovervåket - Titler som IKKE overvåkes for oppdateringer.
  - Mangler - I databasen, overvåket, men mangler fra filsystemet.
  - Ønsket - I databasen, overvåket, mangler, men bør være tilgjengelig basert på tilgjengelighetsinnstillingene
  - Kutt ikke oppfylt - Tittel på filsystemet, men overvåker fortsatt ønsket kvalitet.
  - Egendefinerte filtre
    - Overvåket (boolesk)
    - Vurdert tilgjengelig (boolesk)
    - Minimum tilgjengelighet (Enum)
      - Kunngjort
      - På kino
      - Utgitt
    - Tittel \[inneholder\] (Streng)
    - Utgivelsesstatus (Enum)
      - TBA
      - Kunngjort
      - På kino
      - Utgitt
      - Slettet
        - Slettet fra TMDb
    - Studio (Enum Studios)
    - Samling (Enum Samlinger)
    - Kvalitetsprofil (Enum Kvalitetsprofiler)
    - Lagt til (statisk DateTime, relativ TimeDelta)
    - År (Int)
    - På kino (statisk DateTime, relativ TimeDelta)
    - Fysisk utgivelse (statisk DateTime, relativ TimeDelta)
    - Digital utgivelse (statisk DateTime, relativ TimeDelta)
    - Spilletid (Int)
    - Bane \[inneholder\] (Streng)
    - Størrelse på disk (Int)
    - Sjangre \[inneholder\] (Enum Sjangre)
    - TMDB-vurdering (Flyttall)
    - TMDB-stemmer (Int)
    - IMDb-vurdering
    - Tomatovurdering
    - IMDb-stemmer
    - Sertifisering (Enum Vurdering (PG-13, R, osv.))
    - Merker \[inneholder\] (Enum Merker)

# Legg til ny

![radarr-add-new-empty.png](/assets/radarr/radarr-add-new-empty.png)

- Hvis du vil legge til en ny film, er dette siden du vil gjøre det fra.
  - Du finner hvordan du gjør det i vår [Hurtigstartguide](/radarr/quick-start-guide).
- Under søkefeltet finner du også knappen Importer eksisterende filmer. Hvis det er tilfelle for deg, finner du mye informasjon om det også i vår [Hurtigstartguide](/radarr/quick-start-guide).
- Hvis du får en feilmelding om "banen er allerede konfigurert", [se denne FAQ-oppføringen](/radarr/faq#path-is-already-configured-for-an-existing-movie).

# Bibliotekimport

Bibliotekimport lar deg importere eksisterende organiserte filmer og hver films fil via eksisterende filer i banebiblioteket. Dette er spesielt nyttig når du oppretter en ny Radarr-instans og ønsker å beholde de eksisterende filmene dine.

- Bibliotekimport er for å legge til og importere et eksisterende organisert filmbibliotek i Radarr.
- Bibliotekimport kan ikke brukes til:
  - Importere filer fra en nedlastingsmappe
  - Legge til eller importere en eller flere filer som ikke er riktig navngitt og organisert i sin egen filmmappe innenfor rotmappen eller en mappe du ønsker å legge til som rotmappe
  - Andre bruksområder som ikke innebærer å legge til en film i Radarr og importere filmen og dens fil fra rot (bibliotek) mappen som ble angitt for bibliotekimport
- Hvis du får en feilmelding om "banen er allerede konfigurert", [se denne FAQ-oppføringen](/radarr/faq#path-is-already-configured-for-an-existing-movie).
  
> Det er nødvendig at filmmapper og filer har året i navnet for å bli importert og analysert.{.is-warning}

> \* Ikke-Windows: Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert.
> \* Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert.
{.is-warning}

> **Brukeren og gruppen du konfigurerte Radarr til å kjøre som, må ha lese- og skrivetilgang til dette stedet.**
{.is-info}

> Nedlastingsklienten din laster ned til en nedlastingsmappe, og Radarr importerer den til mediamappen (endelig destinasjon) som medieserveren din bruker.
{.is-info}

> **Nedlastingsmappen og mediamappen kan ikke være samme sted**
{.is-danger}

# Samlinger

Wikien utvikles og vedlikeholdes av fellesskapet.
Denne delen har ikke fått noen bidrag for å gjenspeile og beskrive samlingssiden i Radarr.

# Oppdag

Oppdag viser anbefalte filmer

- Hvis du ikke har noen lister, vil den vise de 90 mest anbefalte filmene basert på TMDb-filmene som er anbefalt for filmene i biblioteket ditt, i tillegg til de 10 anbefalingene fra de nyeste tilleggene dine.

> Tips: Du kan deaktivere anbefalte filmer fra Radarr og bare se filmer fra listene dine i `Alternativer`.
{.is-info}

- Hvis du har lister, vil den vise anbefalingene nevnt ovenfor OG oppføringer fra listene dine.

> Tips: Endre `Filter` til `Ny ikke-ekskludert` for å bare vise filmer som ikke er i biblioteket ditt.
{.is-info}

![radarr-discover-empty.png](/assets/radarr/radarr-discover-empty.png)

- Sannsynligvis vil oppdag-anbefalingene dine være få hvis du har en ny installasjon med få eller ingen filmer. Du må legge til innhold i biblioteket for å få anbefalinger. Du har flere alternativer:
  1. Klikk på knappen [Legg til ny film](/radarr/library#add-new) for å legge til filmer manuelt.
  1. Klikk på knappen [Importer eksisterende bibliotek](/radarr/library#library-import) for å importere et eksisterende bibliotek.
  1. Klikk på knappen [Legg til lister](/radarr/settings#lists) for å legge til en liste i Radarr. Mer informasjon om lister finner du på siden [Mer informasjon (Støttet)](/radarr/faq#what-are-lists-and-what-can-they-do-for-me) for denne delen.

![radarr-discover-add-new-movies.png](/assets/radarr/radarr-discover-add-new-movies.png)

- Når du har lagt til en film ved hjelp av en av de tre alternativene nevnt ovenfor, vil du bli presentert med forskjellige filmer å oppdage.
    1. Her kan du velge hvilke filmer du vil legge til i biblioteket ditt
    1. Her kan du velge alle filmene som er på denne listen hvis du føler deg ekstra gal
    1. Velg hvilken rotsti du vil at disse filmene skal gå til når de er importert
    1. Velg hvilken tilgjengelighet du vil at filmen skal ha før den blir lastet ned
    1. Velg eventuelle kvalitetsprofiler du allerede har opprettet ([Mer informasjon](/radarr/settings#quality-profiles))
    1. Vil du at Radarr skal overvåke denne filmen for eventuelle oppgraderinger i kvalitet?
    1. Vil du at Radarr automatisk skal søke etter denne filmen etter at du har lagt den til?
    1. Vil du at Radarr skal ekskludere disse filmene fra eventuelle lister som blir importert? ([Mer informasjon](/radarr/settings#list-exclusion))
    1. Til slutt, legg til filmen i biblioteket ditt.