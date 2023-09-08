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

Serie-siden viser dit komplette bibliotek og giver dig mulighed for at vælge individuelle serier (dog kan søgning være mere effektiv i store biblioteker) og foretage søgninger efter specifikke serier samt redigere dem. Den giver dig også mulighed for at filtrere dine serier.

# Filtre

Filtre-mulighederne giver dig mulighed for at indsnævre dine serier og er utroligt nyttige. Det kan bruges til at se udgivelsesdatoer, navne, antal episoder, diskstørrelse og meget mere, herunder brugerdefinerede filtre, der passer til alle dine behov. Disse kan også bruges i masseeditor.

# Tilføj Ny

Den nye tilføjelsesfunktion giver dig mulighed for at tilføje en ny serie, som Sonarr skal overvåge og downloade.

- Rodmappe - Den valgte [rod-/biblioteksmappe](/sonarr/settings#root-folders) i Sonarr, som denne serie skal bruge
- Overvågning - Hvordan vil du have, at serien overvåges i starten?
  - Alle episoder - Overvåg alle episoder undtagen specialafsnit
  - Fremtidige episoder - Overvåg episoder, der endnu ikke er blevet vist
  - Manglende episoder - Overvåg episoder, der enten ikke har filer eller endnu ikke er blevet vist
  - Eksisterende episoder - Overvåg episoder, der har filer
  - Første sæson - Overvåg alle episoder i den første sæson; alle andre sæsoner vil blive ignoreret
  - Seneste sæson - Overvåg alle episoder i den seneste sæson og fremtidige sæsoner
  - Ingen - Ingen episoder vil blive overvåget
- Kvalitetsprofil - Den [kvalitetsprofil](/sonarr/settings#quality-profiles), der skal bruges til denne serie
- Serietype - Hvilken serietype skal bruges til denne serie; dette ændrer, hvordan søgninger foretages [Se FAQ-indgangen for mere information](/sonarr/faq#whats-the-different-series-types)
- Sæsonmappe - Aktivér eller deaktiver oprettelse og brug af sæsonmapper for denne serie
- Tags - Bruges til at tildele serier til udgivelsesprofiler, forsinkelsesprofiler, indekser eller bare til at organisere dine serier
- [ ] Start søgning efter manglende episoder - baseret på dine valgte overvågningsindstillinger, søg efter alle manglende og overvågede episoder i denne serie
- [ ] Start søgning efter afkortede episoder - baseret på dine valgte overvågningsindstillinger og kun relevant, hvis du har eksisterende filer til dine episoder i serie-mappen, søg efter alle eksisterende og overvågede episoder i denne serie, der ikke opfylder eller overstiger din kvalitetsprofils afkortning

# Biblioteksimport

Biblioteksimport giver dig mulighed for at importere eksisterende, organiserede serier og episodefiler til Sonarr via eksisterende filer i stien. Dette er særligt nyttigt, når du opretter en ny Sonarr-instans og ønsker at beholde dine eksisterende serier.

- Biblioteksimport er til tilføjelse og import af et eksisterende organiseret bibliotek af serier til Sonarr.

- Biblioteksimport kan ikke bruges til:
  - Import af filer fra en download-mappe
  - Tilføjelse eller import af en eller flere filer, der ikke er korrekt navngivet og organiseret i deres egen serie-mappe inden for din rodmappe eller en mappe, du ønsker at tilføje som en rodmappe
  - Andre anvendelser, der ikke handler om at tilføje en serie eller episode til Sonarr og importere serien og dens fil(er) fra rod- (biblioteks-)mappen, der blev angivet i biblioteksimporten

> \* Ikke-Windows: Hvis du bruger en NFS-montering, skal `nolock` være aktiveret.
> \* Hvis du bruger en SMB-montering, skal `nobrl` være aktiveret.
{.is-warning}

> **Brugeren og gruppen, du har konfigureret Sonarr til at køre som, skal have læse- og skriveadgang til dette sted.** {.is-info}

> Din downloadklient downloader til en download-mappe, og Sonarr importerer det til din mediemappe (endelige destination), som din medieserver bruger.
{.is-info}

> **Din download-mappe og mediemappe kan ikke være det samme sted**
{.is-danger}

# Masseeditor

Masseeditoren giver dig mulighed for at redigere serier i massevis. Du kan ændre alle tidligere indstillinger, der blev foretaget, da du tilføjede serien.

# Sæsonpas

Dette viser information om, hvor mange sæsoner hver serie har, og hvor mange episoder der mangler i hver sæson.