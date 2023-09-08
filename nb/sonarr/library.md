---
title: Sonarr Bibliotek
description: 
published: true
date: 2022-10-28T17:18:11.116Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-06-11T23:31:01.289Z
---

# Serier

Serie-siden viser hele biblioteket ditt og lar deg velge individuelle serier (men søk kan være mer effektivt i store biblioteker) og søke etter spesifikke serier, samt redigere dem. Den lar deg også filtrere seriene dine.

# Filtre

Filtre-alternativene lar deg begrense seriene dine og er utrolig nyttige. Det kan brukes til å se utgivelsesdatoer, navn, antall episoder, diskstørrelse og mye mer, inkludert tilpassede filtre, for å passe alle dine behov. Disse kan også brukes i masse-redigeringsverktøyet.

# Legg til ny

Funksjonen for å legge til nytt lar deg legge til en ny serie for Sonarr å overvåke og laste ned.

- Rotmappe - Den valgte [rot-/biblioteksmappen](/sonarr/settings#root-folders) i Sonarr som skal brukes for denne serien
- Overvåk - Hvordan ønsker du at serien skal overvåkes i utgangspunktet?
  - Alle episoder - Overvåk alle episoder unntatt spesialepisoder
  - Fremtidige episoder - Overvåk episoder som ennå ikke har blitt sendt
  - Manglende episoder - Overvåk episoder som ikke har filer eller som ennå ikke har blitt sendt
  - Eksisterende episoder - Overvåk episoder som har filer
  - Første sesong - Overvåk alle episoder i den første sesongen; alle andre sesonger vil bli ignorert
  - Siste sesong - Overvåk alle episoder i den siste sesongen og fremtidige sesonger
  - Ingen - Ingen episoder vil bli overvåket
- Kvalitetsprofil - [Kvalitetsprofilen](/sonarr/settings#quality-profiles) som skal brukes for denne serien
- Serietype - Hvilken serietype skal brukes for denne serien; dette endrer hvordan søk utføres [Se FAQ-innlegget for mer informasjon](/sonarr/faq#whats-the-different-series-types)
- Sesongmappe - Aktiver eller deaktiver opprettelse og bruk av sesongmapper for denne serien
- Merker - Brukes til å tilordne serier til utgivelsesprofiler, forsinkelsesprofiler, indekser eller bare for å organisere seriene dine
- [ ] Start søk etter manglende episoder - basert på valgte overvåkingsinnstillinger, søk etter alle manglende og overvåkede episoder i denne serien
- [ ] Start søk etter episoder som ikke oppfyller kutt - basert på valgte overvåkingsinnstillinger og bare aktuelt hvis du har eksisterende filer for episodene i seriemappen din, søk etter alle eksisterende og overvåkede episoder i denne serien som ikke oppfyller eller overstiger kvalitetsprofilens kutt

# Bibliotekimport

Bibliotekimport lar deg importere eksisterende, organiserte serier og episodfiler til Sonarr via eksisterende filer i sti-mappen. Dette er spesielt nyttig når du oppretter en ny Sonarr-instans og ønsker å beholde de eksisterende seriene dine.

- Bibliotekimport brukes for å legge til og importere et eksisterende organisert bibliotek med serier i Sonarr.

- Bibliotekimport kan ikke brukes til:
  - Importere filer fra en nedlastingsmappe
  - Legge til eller importere én eller flere filer som ikke er riktig navngitt og organisert i sin egen seriemappe innenfor rotmappen din eller en mappe du ønsker å legge til som en rotmappe
  - Andre bruksområder som ikke innebærer å legge til en serie eller episode i Sonarr og importere serien og dens fil(er) fra rot- (biblioteks-) mappen som ble angitt for bibliotekimporten

> \* Non-Windows: Hvis du bruker en NFS-montering, må `nolock` være aktivert.
> \* Hvis du bruker en SMB-montering, må `nobrl` være aktivert.
{.is-warning}

> **Brukeren og gruppen du konfigurerte Sonarr til å kjøre som, må ha lese- og skrivetilgang til dette stedet.** {.is-info}

> Nedlastingsklienten din laster ned til en nedlastingsmappe, og Sonarr importerer det til mediamappen din (endelig destinasjon) som medieserveren din bruker.
{.is-info}

> **Nedlastingsmappen og mediamappen kan ikke være samme sted**
{.is-danger}

# Masse-redigeringsverktøy

Masse-redigeringsverktøyet lar deg redigere serier i stor skala. Du kan endre hvilke som helst av de tidligere innstillingene som ble gjort da du la til serien.

# Sesongpass

Dette viser informasjon om hvor mange sesonger hver serie har og hvor mange episoder som mangler i hver sesong.