---
title: Prowlarr FAQ
description: Prowlarr FAQ
published: true
date: 2023-08-28T19:29:30.585Z
tags: prowlarr, faq
editor: markdown
dateCreated: 2021-11-03T03:01:18.079Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
  - [Tvungen godkendelse](#tvungen-godkendelse)
  - [Hvordan nulstiller jeg statistik?](#hvordan-nulstiller-jeg-statistik)
  - [Kategori ikke tilgængelig eller mangler](#kategori-ikke-tilgængelig-eller-mangler)
  - [Kan jeg tilføje en hvilken som helst (generisk) Torznab- eller Newznab-indeks?](#kan-jeg-tilføje-en-hvilken-som-helst-generisk-torznab-eller-newznab-indeks)
  - [Kan jeg tilføje en hvilken som helst (generisk) Torrent RSS-feed?](#kan-jeg-tilføje-en-hvilken-som-helst-generisk-torrent-rss-feed)
  - [Kan jeg bruge flaresolverr-indekser?](#kan-jeg-bruge-flaresolverr-indekser)
  - [Hvordan tilføjer jeg en indekser, der er nede eller ikke fungerer?](#hvordan-tilføjer-jeg-en-indekser-der-er-nede-eller-ikke-fungerer)
  - [Prowlarr synkroniserer ikke med Sonarr](#prowlarr-synkroniserer-ikke-med-sonarr)
  - [Prowlarr synkroniserer ikke X-indekser med appen](#prowlarr-synkroniserer-ikke-x-indekser-med-appen)
  - [Hvilke \*Arr-indekserindstillinger sammenlignes for fuld synkronisering af appen?](#hvilke-arr-indekserindstillinger-sammenlignes-for-fuld-synkronisering-af-appen)
  - [Hvordan opdaterer jeg Prowlarr?](#hvordan-opdaterer-jeg-prowlarr)
    - [Kan jeg opdatere Prowlarr inde i min Docker-container?](#kan-jeg-opdatere-prowlarr-inde-i-min-docker-container)
    - [Installation af en nyere version](#installation-af-en-nyere-version)
      - [Native](#native)
      - [Docker](#docker)
  - [Kan jeg skifte fra `nightly` tilbage til `develop`?](#kan-jeg-skifte-fra-nightly-tilbage-til-develop)
  - [Kan jeg skifte mellem grene?](#kan-jeg-skifte-mellem-grene)
  - [Hjælp, min Mac siger, at Prowlarr ikke kan åbnes, fordi udvikleren ikke kan verificeres](#hjælp-min-mac-siger-at-prowlarr-ikke-kan-åbnes-fordi-udvikleren-ikke-kan-verificeres)
  - [Hjælp, min Mac siger, at Prowlarr.app er beskadiget og kan ikke åbnes](#hjælp-min-mac-siger-at-prowlarrapp-er-beskadiget-og-kan-ikke-åbnes)
  - [Hvordan anmoder jeg om en funktion til Prowlarr?](#hvordan-anmoder-jeg-om-en-funktion-til-prowlarr)
  - [Jeg får en fejl: Database disk image is malformed](#jeg-får-en-fejl-database-disk-image-is-malformed)
  - [Jeg bruger Prowlarr på en Mac, og den stoppede pludselig med at virke. Hvad skete der?](#jeg-bruger-prowlarr-på-en-mac-og-den-stoppede-pludselig-med-at-virke-hvad-skete-der)
  - [Hvordan skifter jeg fra Windows Service til en Tray App?](#hvordan-skifter-jeg-fra-windows-service-til-en-tray-app)
  - [Hvordan sikkerhedskopierer/gendanner jeg Prowlarr?](#hvordan-sikkerhedskopierer-gendanner-jeg-prowlarr)
    - [Sikkerhedskopiering af Prowlarr](#sikkerhedskopiering-af-prowlarr)
      - [Brug af indbygget sikkerhedskopiering](#brug-af-indbygget-sikkerhedskopiering)
      - [Brug af filsystemet direkte](#brug-af-filsystemet-direkte)
    - [Gendannelse fra sikkerhedskopi](#gendannelse-fra-sikkerhedskopi)
      - [Brug af zip-sikkerhedskopi](#brug-af-zip-sikkerhedskopi)
      - [Brug af filsystem-sikkerhedskopi](#brug-af-filsystem-sikkerhedskopi)
      - [Gendannelse af filsystem på Synology NAS](#gendannelse-af-filsystem-på-synology-nas)
  - [WebUI indlæses kun på localhost på Windows](#webui-indlæses-kun-på-localhost-på-windows)
  - [Sådan finder du cookies](#sådan-finder-du-cookies)
  - [uTorrent virker ikke længere](#utorrent-virker-ikke-længere)
  - [Jeg fik en pop-up, der sagde, at config.xml var beskadiget, hvad nu?](#jeg-fik-en-pop-up-der-sagde-at-configxml-var-beskadiget-hvad-nu)
  - [Ugyldigt certifikat og andre HTTPS- eller SSL-problemer](#ugyldigt-certifikat-og-andre-https-eller-ssl-problemer)
  - [Hjælp, jeg har låst mig selv ude](#hjælp-jeg-har-låst-mig-selv-ude)
  - [Underlige UI-problemer](#underlige-ui-problemer)
  - [VPN'er, Prowlarr og \*ARRs](#vpner-prowlarr-og-arrs)
  - [Hvordan stopper jeg browseren fra at starte ved opstart?](#hvordan-stopper-jeg-browseren-fra-at-starte-ved-opstart)
  - [Kan jeg nemt tilføje alle indekser på én gang?](#kan-jeg-nemt-tilføje-alle-indekser-på-én-gang)
  
## Tvungen godkendelse

Hvis Prowlarr er eksponeret, så UI'en kan tilgås uden for dit lokale netværk, skal du have en form for godkendelsesmetode aktiveret for at få adgang til UI'en. Dette kræves også i stigende grad af trackere og indekser.

Fra Prowlarr v1 er godkendelse obligatorisk.

### Godkendelsesmetode

- `Basic` (Browser pop-up) - Denne indstilling viser en lille pop-up, når du tilgår din Prowlarr, der giver dig mulighed for at indtaste et brugernavn og adgangskode.
- `Forms` (Login-side) - Denne indstilling viser en login-side, der ligner dem, du finder på andre hjemmesider, så du kan logge ind på din Prowlarr.
- `External` - Konfigureres kun via konfigurationsfilen
  - Hvis du bruger en **ekstern godkendelse** som f.eks. Authelia, Authetik, NGINX Basic auth osv., kan du undgå at skulle godkende to gange ved at lukke appen ned, indstille `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurationsfilen](/prowlarr/appdata-directory) og genstarte appen. **Bemærk, at flere `AuthenticationMethod`-poster i filen ikke understøttes, og kun den øverste værdi vil blive brugt**.

### Påkrævet godkendelse

- Hvis du ikke eksponerer appen eksternt og/eller ikke ønsker, at godkendelse skal være påkrævet for lokal adgang (f.eks. LAN), skal du ændre indstillingen i Indstillinger => Generel sikkerhed => Påkrævet godkendelse til `Deaktiveret for lokale adresser`.
  - Den tilsvarende konfigurationsfil for dette er `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`.
  
## Hvordan nulstiller jeg statistik?

- For at nulstille dine statistikker og rydde historikken skal du gøre følgende:

1. Historik => Indstillinger
1. Indstil Historikoprydning til `1`. Dette vil kun bevare historikken og statistikken fra i går.
1. Gå til System => Opgaver
1. Kør opgaven "Ryd historik op"
1. Kør opgaven "Husvedligeholdelse"
1. Gå tilbage til Historik => Indstillinger
1. Indstil Historikoprydning til den ønskede periode for bevarelse af historik og statistik.

## Kategori ikke tilgængelig eller mangler

- Bemærk, at brugerdefinerede/ikke-standard indeksspecifikke kategorier er mappet til standardkategorier, så søgning i standardkategorier vil omfatte alle brugerdefinerede kategorier. Gennemgå din specifikke indeksspecifikke kategorimapping for flere detaljer.

## Kan jeg tilføje en hvilken som helst (generisk) Torrent RSS-feed?

Ja. Brug "TorrentRSS".

Følgende attributter er obligatoriske:

- guid
- title
- infohash
- enclosure eller link

Følgende attributter er valgfrie, men anbefales:

- size
- pubDate

## Kan jeg tilføje en hvilken som helst (generisk) Torznab- eller Newznab-indeks?

- Ja.
- Gå til `Indekser` => `Tilføj indeks` (<kb>+</kb>) => `Generisk Torznab` eller `Generisk Newznab`

## Kan jeg bruge flaresolverr-indekser?

- Ja.

1. Konfigurér din flaresolverr-instans ved at tilføje den som en proxy i [Indstillinger => Indekser](/prowlarr/settings#indexer-proxies)
1. Tilføj en tag til den oprettede flaresovlerr-proxy
1. Tilføj den samme tag til din [Indekser](/prowlarr/indexers)

> Tagsene skal matche, og Cloudflare skal registreres for, at Flaresolverr kan bruges. En Flaresolverr-proxy er deaktiveret, hvis der ikke bruges nogen tags.
{.is-warning}

> [Se TRaSH's vejledninger om "Sådan opsættes Flaresolverr"](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/) for flere detaljer
{.is-info}

## Hvordan tilføjer jeg en indekser, der er nede eller ikke fungerer?

- Følg de normale trin for at tilføje indekser, men bemærk følgende ændringer.
- Fjern markeringen i afkrydsningsfeltet (Deaktiver) ud for "Aktiveret"
- Tryk på "Gem"
- Tryk igen på "Gem" for at udløse en tvungen gemmehandling
- Rediger indekseren (Skruenøgleikon)
- Markér afkrydsningsfeltet (Aktiver) ud for "Aktiveret"
- Tryk på "Gem"
- Tryk igen på "Gem" for at udløse en tvungen gemmehandling

## Prowlarr synkroniserer ikke med Sonarr

- Prowlarr understøtter kun Sonarr v3 og nyere.
- Sonarr v2 (tidligere kendt som nzbdrone) understøttes ikke af Prowlarr og understøttes generelt ikke længere og er blevet afsluttet siden marts 2021.

## Prowlarr synkroniserer ikke X-indekser med appen

- Prowlarr synkroniserer kun, hvis "Tilføj og fjern" eller "Fuld synkronisering" er aktiveret for appen.
- Kun i tilfælde, hvor en app og en indekser har matchende tags eller ingen tags overhovedet, vil en indekser blive synkroniseret med en app.
- Indeksere synkroniseres baseret på de evner/kategorier, de hævder at understøtte.
  - Hvis en indekser kun understøtter TV-kategorier, vil den ikke blive synkroniseret med Lidarr, Radarr og Readarr.
- En given indekser vil kun blive synkroniseret med Sonarr, hvis "Understøttede" kategorier kan vælges som en avanceret indstilling på appbasis.
- Indeksere vil ikke forsøge at blive synkroniseret, hvis de specifikke kategorier, som indekseren understøtter, ikke er valgt i Indstillinger => Program => {App} => Synkroniseringskategorier (avancerede indstillinger), og logfilerne vil ikke vise nogen indikation af et synkroniseringsforsøg.
- Den mest almindelige årsag til dette er, at \*Arrs kun accepterer indeksere, hvis deres testforespørgsler returnerer resultater, der indeholder mindst en af de konfigurerede kategorier. Med andre ord, hvis du synkroniserer til en app, og din indeksers tomme forespørgsel ikke returnerer resultater med nogen udgivelse inden for de kategorier, der er konfigureret for appen, vil den ikke være i stand til at tilføje indekseren til \*Arr.
- Den specifikke fejl vil være en HTTP 400 fra \*Arr, der angiver "Forespørgsel lykkedes, men der blev ikke returneret resultater i de konfigurerede kategorier fra din indekser. Dette kan være et problem med indekseren eller dine indekseringsindstillinger."
  - Det kan være, at indekseren simpelthen ikke kan bruges med den \*Arr. Dette er almindeligt, når man forsøger at bruge offentlige trackere eller usenet-indekser med Readarr og Lidarr.
  - Justér de synkroniserede kategorier i de avancerede indstillinger for \*Arr-applikationen i Prowlarr.
    - Bemærk, at visse trackere - primært "dårlige" offentlige trackere - kræver, at man vælger og synkroniserer kategorien "8000 - Andet". Dette er ofte - men ikke altid - angivet i trackernes detaljer i Prowlarr.
    - Prøv igen senere.
    - Hvis problemet fortsætter, kan du have en beskadiget database. Tjek dine logfiler for forekomster af "Database disk image is malformed" eller "Error creating main database". Se [dette afsnit](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed) for mulige løsninger.

## Hvilke \*Arr-indekserindstillinger sammenlignes for fuld synkronisering af appen?

- App/Prowlarr: Indeksernavn
- App/Prowlarr: Aktivér/deaktiver RSS
- App/Prowlarr: Aktivér/deaktiver automatisk søgning
- App/Prowlarr: Aktivér/deaktiver interaktiv søgning
- App/Prowlarr: Indekserprioritet
- App/Prowlarr: API-nøgle
- App/Prowlarr: URL
- App/Prowlarr: Basurl
- App/Prowlarr: Port
- App/Prowlarr: Kategorier
- App/Prowlarr: Seed-forhold og seed-tid
- App/Prowlarr: Minimum antal seedere
- App/Prowlarr: *Alle andre indstillinger, der kan konfigureres/styres i Prowlarr*
- Prowlarr: Implementering (f.eks. YML eller C#)

Hvis en af de ovenstående ændres mellem \*Arr-appen og Prowlarr, når fuld synkronisering er aktiveret, vil indekseren blive synkroniseret og opdateret i \*Arr.

## Hvordan opdaterer jeg Prowlarr?

- Gå til Indstillinger og derefter fanen Generelt og vis avancerede indstillinger (brug knappen ved siden af gem-knappen).

1. Under afsnittet Opdateringer skal du ændre grennavnet til `master`, `develop` eller `nightly`.
1. Gem.

*Dette vil ikke installere bitene fra den gren med det samme, det vil ske under den næste opdatering.*

- `master` - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    (Standard/Stabil): Den er blevet testet af brugere på develop- og nightly-grenene, og der er ikke kendt nogen større problemer. På GitHub er dette `master`-grenen.

- `develop` - ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  (Beta): Dette er kanten af testningen. Udgivet efter test i nightly for at sikre, at der ikke er umiddelbare problemer. Nye funktioner og fejlrettelser udgives først her efter nightly. Den kan betragtes som halvstabil, men er stadig `beta`.

> På GitHub er dette et øjebliksbillede af `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- `nightly` - ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  (Alpha/Ustabil): Dette er den nyeste version. Den udgives, så snart koden er blevet forpligtet og bestået alle automatiserede tests. Denne version er måske ikke blevet brugt af os eller andre brugere endnu. Der er ingen garanti for, at den vil køre i visse tilfælde. Denne gren anbefales kun til avancerede brugere. Der forventes problemer og egen undersøgelse i denne gren. ***Brug denne gren kun, hvis du ved, hvad du laver, og er villig til at gøre en indsats for at rette en mislykket opdatering.*** Denne version opdateres øjeblikkeligt.

> **Advarsel: Du kan muligvis ikke skifte tilbage til `develop` efter at have skiftet til denne gren.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Bemærk: Hvis du har installeret via Docker, skal du tilføje `:latest`, `:testing`, `:develop` eller `:nightly` til slutningen af din container-tag afhængigt af, hvem der laver dine builds.

|                                                                      | `master` (stabil) ![Nuværende Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Nuværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (ustabil) ![Nuværende Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `latest`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `latest`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### Kan jeg opdatere Prowlarr inde i min Docker-container?

- *Teknisk set, ja.* **Men du bør absolut ikke gøre det.** Det er en grundlæggende filosofi i Docker. Der kan opstå databaseproblemer, hvis du opgraderer din installation til den nyeste `nightly`, men derefter opdaterer Docker-containeren selv (muligvis nedgraderer til en ældre version).

### Installation af en nyere version

#### Native

1. Gå til System og derefter fanen Opdateringer
1. Nyere versioner, der endnu ikke er installeret, vil have en opdateringsknap ved siden af dem. Klik på knappen for at installere opdateringen.

#### Docker

1. Træk dit tag igen og opdater din container

## Kan jeg skifte fra `nightly` tilbage til `develop`?

## Kan jeg skifte mellem grene?

- Hvis versionen er identisk, kan du skifte, ellers skal du kontakte udviklingsteamet for at se, om du kan skifte fra `nightly` til `develop`; eller `develop` til `nightly` for din specifikke build.
- Hvis du ikke følger disse instruktioner, kan din Prowlarr blive ubrugelig eller kaste fejl. Du er blevet advaret
  - De mest almindelige fejl er databasefejl om manglende kolonner eller tabeller.

## Hjælp, min Mac siger, at Prowlarr ikke kan åbnes, fordi udvikleren ikke kan verificeres

- Dette er enkelt, se venligst dette link for mere information [her](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
- Alternativt kan det være nødvendigt at selvsignere Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## Hjælp, min Mac siger, at Prowlarr.app er beskadiget og kan ikke åbnes

Det skyldes enten en korrupt download (så prøv igen) eller sikkerhedsproblemer, som blev besvaret lige før dette.

## Hvordan anmoder jeg om en funktion til Prowlarr?

For at anmode om en funktion til Prowlarr skal du først søge på GitHub for at sikre dig, at der ikke allerede findes en lignende anmodning, og derefter [klikke her](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=) for at tilføje din anmodning.

## Jeg får en fejl: Database disk image is malformed

- **Fejl med `Error creating log database` indikerer problemer med logs.db**
  - Dette kan hurtigt løses ved at omdøbe eller fjerne databasen. Logs-databasen indeholder uvigtige oplysninger om kommandohistorik og opdateringsinstallationshistorik samt Info-, Warn- og Error-poster
- **Fejl med `Error creating main database` eller generisk `database disk image is malformed` uden specificeret database indikerer problemer med prowlarr.db**
  - Fortsæt med de nedenstående trin
- Dette betyder, at din SQLite-database, der gemmer størstedelen af ​​informationen for Prowlarr, er korrupt. Dine muligheder er at prøve (en) sikkerhedskopi(er), prøve at gendanne den eksisterende database, prøve at gendanne sikkerhedskopierne eller hvis alt andet fejler, starte forfra med en frisk ny database.
- Denne fejl kan vises, hvis databasefilen ikke kan skrives af bruger-/gruppe \*Arr kører som. Tilladelser, der er årsagen, vil sandsynligvis kun være et problem for nye installationer, migrerede installationer til en ny server, hvis du for nylig har ændret tilladelserne for din appdata-mappe eller hvis du har ændret brugeren og gruppen \*Arr kører som.
- Dit bedste og første mulighed er at [prøve at gendanne fra en sikkerhedskopi](#how-do-i-backuprestore-my-prowlarr)
- Du kan også prøve at gendanne din database. Dette er normalt den eneste mulighed, når dette problem opstår efter en opdatering. Prøv kommandoen [sqlite3 `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Hvis din sqlite ikke har `.recover` eller du ønsker en mere GUI-venlig måde (f.eks. Windows), skal du følge [vores instruktioner på dette wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- En anden mulig årsag til, at du får en fejl med din database, er, at du placerer din database på et netværksdrev (nfs eller smb eller noget andet, der ikke er lokalt). **SQLite er designet til situationer, hvor data og applikationen eksisterer på samme maskine.** Derfor skal din \*Arr AppData-mappe (/config mount for docker) være på lokal lagerplads. [SQLite og netværksdrev fungerer ikke godt sammen og vil på et tidspunkt forårsage en beskadiget database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruger mergerFS, skal du fjerne `direct_io`, da SQLite bruger mmap, som ikke understøttes af `direct_io`, som forklaret i mergerFS [dokumentationen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruger Prowlarr på en Mac, og den stoppede pludselig med at fungere. Hvad skete der?

- Mest sandsynligt skyldes dette en MacOS-fejl, der fik Prowlarr-databasen til at blive beskadiget. Se venligst FAQ-indgangen for at gendanne en beskadiget database.

## Hvordan skifter jeg fra Windows Service til en Tray App?

- Luk Prowlarr ned
- Kør serviceuninstall.exe, der er i Prowlarr-mappen
- Kør Prowlarr.exe som administrator mindst én gang for at give det korrekte tilladelser og åbne firewallen. Når det er fuldført, kan du lukke det og køre det normalt.
- (Valgfrit) Opret en genvej til Prowlarr.exe i opstartsmappe for at starte automatisk ved opstart.

## Hvordan sikkerhedskopierer/gendanner jeg Prowlarr?

### Sikkerhedskopiering af Prowlarr

#### Brug af indbygget sikkerhedskopiering

- Gå til System => Backup i Prowlarr UI'en
- Klik på Sikkerhedskopier-knappen
- Download zip-filen efter at sikkerhedskopien er oprettet for at gemme den sikkert

#### Brug af filsystemet direkte

- Find placeringen af AppData-mappen for Prowlarr  
  - Via Prowlarr UI'en gå til System => Om  
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Stop Prowlarr - Dette forhindrer, at databasen bliver beskadiget
- Kopier indholdet til et sikkert sted

### Gendannelse fra sikkerhedskopi

> Gendannelse til et operativsystem, der bruger forskellige stier, vil ikke virke (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows), flytning mellem OS X og Linux kan muligvis fungere, da begge bruger stier, der indeholder `/` i stedet for `\` som Windows bruger, men det understøttes ikke. Du skal manuelt redigere alle stier i databasen.
{.is-warning}

#### Brug af zip-sikkerhedskopi

- Geninstaller Prowlarr (hvis relevant / ikke allerede installeret)
- Kør Prowlarr
- Gå til System => Backup
- Vælg Gendan sikkerhedskopi
- Vælg Vælg fil
- Vælg din sikkerhedskopizip-fil
- Vælg Gendan

#### Brug af filsystem-sikkerhedskopi

- Geninstaller Prowlarr (hvis relevant / ikke allerede installeret)
- Find placeringen af AppData-mappen for Prowlarr  
  - Kør Prowlarr én gang og gå via UI'en til System => Om  
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Stop Prowlarr
- Slet indholdet af AppData-mappen **(Inklusive .db-wal/.db-journal-filerne, hvis de findes)**
- Gendan fra din sikkerhedskopi
- Start Prowlarr
- Hvis stierne er de samme, vil alt fortsætte, hvor det slap

#### Gendannelse af filsystem på Synology NAS

> ADVARSEL: Gendannelse på en Synology kræver kendskab til Linux og Root SSH-adgang til Synology-enheden.
{.is-warning}

- Geninstaller Prowlarr (hvis relevant / ikke allerede installeret)
- Find placeringen af AppData-mappen for Prowlarr  
  - Kør Prowlarr én gang og gå via UI'en til System => Om  
  - [Prowlarr Appdata Directory](/prowlarr/appdata-directory)
- Stop Prowlarr
- Opret forbindelse til Synology NAS via SSH og log ind som root  

> På nogle installationer er brugeren anderledes end i nedenstående kommandoer: `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- Udfør følgende kommandoer:

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- Opdater tilladelserne på filerne:

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Start Prowlarr

## WebUI indlæses kun på localhost på Windows

Hvis du kun kan nå din webgrænseflade på `http://localhost:9696/` eller `http://127.0.0.1:9696`, skal du køre Prowlarr som administrator mindst én gang, måske endda altid.

## Find cookies

Nogle websteder kan ikke logges ind automatisk og kræver, at du logger ind manuelt og derefter giver cookies til Prowlarr for at fungere. [Se venligst denne artikel for detaljer.](/useful-tools#finding-cookies)

## uTorrent virker ikke længere

- Sørg for, at Web UI er aktiveret

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- Tænd for Web UI

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Sørg for, at Alt Listening Port (Avanceret => Web UI) ikke er det samme som Listening Port (Forbindelser). Vi vil foreslå at ændre Web UI Alt Listening Port for ikke at påvirke portvideresendelse for forbindelser.

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## Jeg fik en pop-up, der sagde, at config.xml var korrupt, hvad gør jeg nu?

Prowlarr kunne ikke læse din konfigurationsfil ved opstart, da den på en eller anden måde blev beskadiget. For at få Prowlarr tilbage online skal du slette `.xml` i din AppData-mappe. Når den er slettet, skal du starte Prowlarr, og den vil starte på standardporten (9696). Du skal nu konfigurere eventuelle indstillinger, du har konfigureret på siden Generelle indstillinger.

## Ugyldigt certifikat og andre HTTPS- eller SSL-problemer

Din downloadklient fungerer ikke længere, og du får en fejl som f.eks. `Localhost er et ugyldigt certifikat`?

Prowlarr validerer SSL-certifikater. Hvis der ikke er angivet et SSL-certifikat i downloadklienten, eller hvis du bruger et selvsigneret https-certifikat uden CA-certifikatet tilføjet til din lokale certifikatbutik, vil Prowlarr nægte at oprette forbindelse. Der findes gratis korrekt signeret certifikater fra Let's Encrypt.

Hvis din downloadklient og Prowlarr er på samme maskine, er der ingen grund til at bruge HTTPS, så den nemmeste løsning er at deaktivere SSL for forbindelsen. De fleste vil være enige i, at det heller ikke er nødvendigt i et lokalt netværk. Det er muligt at deaktivere validering af certifikater i avancerede indstillinger, hvis du ønsker at beholde en usikker SSL-konfiguration.

## Hjælp, jeg har låst mig selv ude

{#help-i-have-forgotten-my-password}

Hvis du vil deaktivere godkendelse (for at nulstille dit glemte brugernavn eller adgangskode), skal du redigere `config.xml`, som vil være inde i [Prowlarr Appdata-mappen](/prowlarr/appdata-directory).

1. Åbn config.xml i en teksteditor.
2. Find linjen med godkendelsesmetoden, som vil være `<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`.
3. Ændr linjen `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`.
4. Genstart Prowlarr.
5. Prowlarr vil nu være tilgængelig uden en adgangskode. Du skal gå til `Indstillinger: Generelt` i brugergrænsefladen og indstille dit brugernavn og adgangskode.

## Underlige UI-problemer

- Hvis du oplever underlige UI-problemer eller en bestemt visning eller sortering ikke fungerer, skal du prøve at se det i et Chrome Inkognitovindue eller Firefox Privatvindue. Hvis det fungerer fint der, skal du rydde din browsers cache og cookies for din specifikke IP/domæne. For mere information, se artiklen [Ryd cache, cookies og lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wiki'en.

## VPN'er, Jackett og \*ARRs

- Medmindre du befinder dig i et undertrykkende land som Kina, Australien eller Sydafrika, er din torrentklient typisk det eneste, der skal være bag en VPN. Fordi VPN-endpunktet deles af mange brugere, kan du opleve begrænsning af hastigheden, beskyttelse mod DDOS og IP-forbud fra forskellige tjenester, som hver software bruger.
- Med andre ord kan og vil det at placere \*Arrs (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bag en VPN gøre applikationerne ubrugelige i nogle tilfælde, fordi tjenesterne ikke er tilgængelige.

> **For at være klar, det handler ikke om, hvorvidt VPN'er vil forårsage problemer med \*Arrs, men hvornår: billedudbydere vil blokere dig, og Cloudflare er foran de fleste \*Arr-servere (opdateringer, metadata osv.) og kan også blokere dig**
{.is-warning}

- **Mange private trackere vil udelukke dig, hvis du bruger eller får adgang til dem (f.eks. ved hjælp af Jackett eller Prowlarr) via en VPN.**

### Brug af en VPN

- Hvis en VPN er påkrævet, og Docker bruges, anbefales det at bruge Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er påkrævet, og Docker ikke bruges, skal din VPN-klient ***understøtte*** opdeling af tunnelen, så kun de nødvendige (Download Client) apps er bag VPN'en.
- Mange problemer med at få adgang til trackere kan løses ved at bruge Googles eller Cloudflares DNS-servere i stedet for din internetudbyders DNS-servere.
- I nogle tilfælde (f.eks. britiske internetudbydere) kan du være nødt til at placere din torrent-downloadklient bag en VPN og Jackett/Prowlarr som følger:
  - Placer Jackett bag VPN'en og sørg for, at opdeling af tunnelen tillader lokal adgang.
  - For Prowlarr skal du konfigurere din VPN-klient til at levere en proxy og tilføje proxyen i Indstillinger => Indekser. Giv proxyen en tag, og tildel det samme tag til eventuelle indekser, der skal bruge den.
    - Hvis det absolut er nødvendigt, og hvis din VPN ikke giver en måde at oprette en proxy på, kan du placere Prowlarr bag VPN'en og sørge for, at opdeling af tunnelen tillader lokal adgang.

## Hvordan stopper jeg browseren fra at starte ved opstart?

Afhængigt af dit operativsystem er der flere mulige måder.

- I `Indstillinger` => `Generelt` på nogle operativsystemer er der en afkrydsningsboks til at starte browseren ved opstart.
- Når du starter Prowlarr, kan du tilføje `-nobrowser` (*nix) eller `/nobrowser` (Windows) til argumenterne.
- Stop Prowlarr og rediger config.xml-filen, og ændr `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Kan jeg nemt tilføje alle indekser på én gang?

Nej. Dette ville ikke være en god idé, og denne funktionalitet vil ikke blive tilføjet. Det er meget bedre at vælge dine indekser omhyggeligt, være opmærksom på statistikken for at fjerne indekser, der er for langsomme eller ikke producerer resultater. Korrekt beskæring og vedligeholdelse af dine indekser vil resultere i meget bedre resultater generelt og hurtigere resultater ved søgninger fra dine apps.