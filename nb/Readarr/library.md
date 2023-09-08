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

Denne delen er for å administrere biblioteket ditt med [forfattere](#forfattere) og [bøker](#bøker).

# Forfattere

- Bibliotekvisning
  - Oppdater alle - Oppdater metadata for alle forfattere, oppdater plakater, skann forfattermapper på nytt og skann bokfiler på nytt (hvis aktivert)
  - Oppdater og skann - Oppdater metadataen for den forfatteren som vises, og skann mappen dens på nytt
  - RSS-synkronisering - Oppdater RSS-strømmen fra indekserne dine og se om det er noe nytt som kan hentes
  - Forfatterredigerer / Forfatterindeks - Bytt mellom Masseredigeringsmodus og Forfatterindeks (bibliotek) modus
  - Alternativer - Endre visningsalternativer
  - Visning - Bytt visningstype
    - Tabell - Tabellvisning (listevisning)
    - Plakater - Vis plakater (liknende Plex)
    - Oversikt - Vis oversiktsinformasjon og plakaten (detaljert visning)
  - Sorter - Sorter gjeldende visning
  - Filtrer - Filtrer gjeldende visning

# Bøker

- Bibliotekvisning
  - Oppdater alle - Oppdater metadata for alle forfattere, oppdater plakater, skann forfattermapper på nytt og skann bokfiler på nytt (hvis aktivert)
  - Oppdater og skann - Oppdater metadataen for den forfatteren som vises, og skann mappen dens på nytt
  - RSS-synkronisering - Oppdater RSS-strømmen fra indekserne dine og se om det er noe nytt som kan hentes
  - Søk alle / Søk filtrert / Søk valgt - Søk i alle bøker eller valgte bøker i gjeldende visning
  - Bokredigerer / Bokinndex - Bytt mellom Masseredigeringsmodus og Bokinndex (bibliotek) modus
  - Alternativer - Endre visningsalternativer
  - Visning - Bytt visningstype
    - Tabell - Tabellvisning (listevisning)
    - Plakater - Vis plakater (liknende Plex)
    - Oversikt - Vis oversiktsinformasjon og plakaten (detaljert visning)
  - Sorter - Sorter gjeldende visning
  - Filtrer - Filtrer gjeldende visning
  
# Legg til ny

![addnew.png](/assets/readarr/addnew.png)

- Du kan legge til nye forfattere eller individuelle bøker ved å skrive inn forfatterens navn eller boktittel her, og velge det fra resultatlisten.
  - Du finner hvordan du gjør dette i vår [Hurtigstartguide](/readarr/quick-start-guide)
- Du kan også legge til forfattere ved hjelp av GoodReads ID, ISBN eller ASIN etter behov, ved å bruke formatet som vises.

![poe.png](/assets/readarr/poe.png)

- Klikk på forfatterens eller bokens navn for å legge den til i Readarr. En boks vil dukke opp med alternativer for deg.

![addauthor.png](/assets/readarr/addauthor.png)

- Rotmappe - Velg rotmappen her. Ikke endre dette hvis du bruker Calibre Content Server.
- Overvåk - Velg overvåkningstilstanden for alle bøker for denne forfatteren.
- Kvalitetsprofil - Velg kvalitetsprofilen som skal brukes når du leter etter bøker for denne forfatteren.
- (Bare bok) Metadataprofil - Velg metadataprofilen som skal brukes for denne boken.
- Merker - Hvis du vil ha en merkelapp på denne forfatterens bøker, skriv den inn her.
- Start søk etter manglende bok(er) - Velg om du vil starte et historisk søk etter alle bøker av denne forfatteren umiddelbart. Hvis du ikke gjør dette, vil bare NYE opplastede bøker bli hentet fra dette tidspunktet og fremover.
- Legg til {Forfatternavn} eller Legg til {Boktittel} - Klikk på Legg til-knappen for å legge til denne forfatteren i Readarr og starte henting av metadata for alle bøker av denne forfatteren. Denne prosessen kan ta litt tid, så det vil være lurt å ikke legge til for mange forfattere for raskt.

>Hvis du legger til en individuell bok og velger `None`\* for [metadataprofilen](/readarr/settings#metadata-profiles), vil bare den boken vises under forfatteren når den er lagt til. Hvis du vil legge til andre bøker for den forfatteren, velger du en passende metadataprofil.
> \* **Merk at `None` ikke bruker noen metadatafiltre, og du kan få uønskede utenlandske utgaver. For å omgå dette [opprett en metadataprofil som beskrevet i FAQ-en](/readarr/faq#metadata-profile-none-allowing-foreign-releases)**
{.is-warning}

# Ukartlagte filer

![unmappedfiles.png](/assets/readarr/unmappedfiles.png)

Hvis det er bøker oppført her, er de ikke gjenkjent av Readarr og er ikke oppført som "eksisterende" i Readarr, men de er i en av de definerte rotmappene dine.

Du kan få mer informasjon ved å klikke på *i*-ikonet til høyre.

Du kan importere boken manuelt ved å klikke på *person*-ikonet til høyre.

Du kan slette bokfilen ved å klikke på *søppelbøtte*-ikonet til høyre.

Du kan også klikke på *Legg til manglende* øverst for å prøve å legge til alle bøker i Readarr. Merk at dette kan ta lang tid hvis du har mange bøker oppført her.