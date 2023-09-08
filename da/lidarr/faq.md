---
title: Lidarr FAQ
description: Ofte stillede spørgsmål om Lidarr
published: true
date: 2023-08-31T19:08:18.905Z
tags: lidarr, needs-love, faq
editor: markdown
dateCreated: 2021-06-14T14:33:41.344Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
  - [Hvordan fungerer Lidarr?](#hvordan-fungerer-lidarr)
  - [Hvordan finder Lidarr udgivelser?](#hvordan-finder-lidarr-udgivelser)
  - [Tvungen godkendelse](#tvungen-godkendelse)
  - [Hvordan sammenlignes mulige downloads?](#hvordan-sammenlignes-mulige-downloads)
  - [Lidarr stoppede med at virke efter opdatering til Ubuntu 22.04](#lidarr-stoppede-med-at-virke-efter-opdatering-til-ubuntu-2204)
  - [Hvorfor kan jeg ikke tilføje en ny udgivelse eller kunstner til Lidarr?](#hvorfor-kan-jeg-ikke-tilføje-en-ny-udgivelse-eller-kunstner-til-lidarr)
  - [Hvorfor kan jeg ikke tilføje et album med forskellige kunstnere?](#hvorfor-kan-jeg-ikke-tilføje-et-album-med-forskellige-kunstnere)
  - [Hvorfor viser Lidarr kun studiealbummer? Hvordan finder jeg singler eller EP'er?](#hvorfor-viser-lidarr-kun-studiealbummer-hvordan-finder-jeg-singler-eller-eps)
  - [Kan jeg tilføje bare et album?](#kan-jeg-tilføje-bare-et-album)
  - [Kan jeg downloade enkeltspor?](#kan-jeg-downloade-enkeltspor)
  - [Hvorfor vises kunstneren X ikke i søgningen?](#hvorfor-vises-kunstneren-x-ikke-i-søgningen)
  - [Lidarr matchede et album med for mange spor. Hvordan kan jeg ændre albummet til den korrekte udgivelse?](#lidarr-matchede-et-album-med-for-mange-spor-hvordan-kan-jeg-ændre-albummet-til-den-korrekte-udgivelse)
  - [Jeg kan ikke finde en udgivelse i Lidarr, men den er på MusicBrainz](#jeg-kan-ikke-finde-en-udgivelse-i-lidarr-men-den-er-på-musicbrainz)
  - [Hvor ofte synkroniseres Lidarr's og MusicBrainz's databaser?](#hvor-ofte-synkroniseres-lidarrs-og-musicbrainzs-databaser)
  - [Hvordan kan jeg tilføje manglende kunstnerbilleder?](#hvordan-kan-jeg-tilføje-manglende-kunstnerbilleder)
  - [Hvordan kan jeg få manglende albumbilleder? (Cover Art)](#hvordan-kan-jeg-få-manglende-albumbilleder-cover-art)
  - [Jeg har problemer med at importere mine kunstnere, hvad kan det være?](#jeg-har-problemer-med-at-importere-mine-kunstnere-hvad-kan-det-være)
  - [Hvordan kan jeg omdøbe mine kunstnermapper?](#hvordan-kan-jeg-omdøbe-mine-kunstnermapper)
  - [Hvordan kan jeg masse-slette kunstnere fra ønskelisten?](#hvordan-kan-jeg-masse-slette-kunstnere-fra-ønskelisten)
  - [Hvorfor virker Lidarr ikke bag en omvendt proxy](#hvorfor-virker-lidarr-ikke-bag-en-omvendt-proxy)
  - [Hvordan opdaterer jeg Lidarr?](#hvordan-opdaterer-jeg-lidarr)
    - [Kan jeg opdatere Lidarr inde i min Docker-container?](#kan-jeg-opdatere-lidarr-inde-i-min-docker-container)
    - [Installation af en nyere version](#installation-af-en-nyere-version)
      - [Native](#native)
      - [Docker](#docker)
  - [Kan jeg skifte fra `nightly` tilbage til `develop`?](#kan-jeg-skifte-fra-nightly-tilbage-til-develop)
  - [Kan jeg skifte mellem grene?](#kan-jeg-skifte-mellem-grene)
  - [Jeg får en fejl: Database disk image is malformed](#jeg-får-en-fejl-database-disk-image-is-malformed)
  - [Hvordan sikkerhedskopierer/gendanner jeg min Lidarr?](#hvordan-sikkerhedskopierergendanner-jeg-min-lidarr)
    - [Sikkerhedskopiering af Lidarr](#sikkerhedskopiering-af-lidarr)
      - [Brug af indbygget sikkerhedskopiering](#brug-af-indbygget-sikkerhedskopiering)
      - [Brug af filsystemet direkte](#brug-af-filsystemet-direkte)
    - [Gendannelse fra sikkerhedskopi](#gendannelse-fra-sikkerhedskopi)
      - [Brug af zip-sikkerhedskopi](#brug-af-zip-sikkerhedskopi)
      - [Brug af sikkerhedskopi fra filsystemet](#brug-af-sikkerhedskopi-fra-filsystemet)
      - [Gendannelse af filsystemet på Synology NAS](#gendannelse-af-filsystemet-på-synology-nas)
  - [Jeg bruger Lidarr på en Mac, og den stoppede pludselig med at virke. Hvad skete der?](#jeg-bruger-lidarr-på-en-mac-og-den-stoppede-pludselig-med-at-virke-hvad-skete-der)
  - [Jeg bruger en Pi og Raspbian, og Lidarr vil ikke starte](#jeg-bruger-en-pi-og-raspbian-og-lidarr-vil-ikke-starte)
  - [Hvorfor tager synkronisering af lister så lang tid, og kan jeg ændre det?](#hvorfor-tager-synkronisering-af-lister-så-lang-tid-og-kan-jeg-ændre-det)
  - [Kan jeg deaktivere opdatering af udgivelser?](#kan-jeg-deaktivere-opdatering-af-udgivelser)
  - [Hvorfor kan Lidarr ikke se mine filer på en fjernserver?](#hvorfor-kan-lidarr-ikke-se-mine-filer-på-en-fjernserver)
    - [Lidarr kører som standard under LocalService-kontoen, som ikke har adgang til beskyttede fjernfiler](#lidarr-kører-som-standard-under-localservice-kontoen-som-ikke-har-adgang-til-beskyttede-fjernfiler)
    - [Du bruger et kortlagt netværksdrev (ikke en UNC-sti)](#du-bruger-et-kortlagt-netværksdrev-ikke-en-unc-sti)
  - [Hjælp, jeg har låst mig selv ude](#hjælp-jeg-har-låst-mig-selv-ude)
  - [Hvordan stopper jeg browseren fra at starte ved opstart?](#hvordan-stopper-jeg-browseren-fra-at-starte-ved-opstart)
  - [Mærkelige UI-problemer](#mærkelige-ui-problemer)
  - [VPNs, Jackett og \*ARRs](#vpns-jackett-og-arrs)
  - [Jacketts /all-endepunkt](#jacketts-all-endepunkt)
    - [Jackett /All-løsninger](#jackett-all-løsninger)
  - [Hvorfor er der to filer? | Hvorfor er der en fil tilbage i downloads?](#hvorfor-er-der-to-filer--hvorfor-er-der-en-fil-tilbage-i-downloads)
  - [Jeg får advarsler fra min cloud-lagring om API-grænser](#jeg-får-advarsler-fra-min-cloud-lagring-om-api-grænser)

## Hvordan fungerer Lidarr?

- Lidarr er afhængig af RSS-feeds til at automatisere hentning af udgivelser, når de bliver offentliggjort, både nye udgivelser og tidligere udgivelser, der bliver genudgivet eller genudsendt. RSS-feedet er de seneste udgivelser fra et websted, typisk mellem 50 og 100 udgivelser, selvom nogle websteder giver flere og andre færre. RSS-feedet består af alle nyligt tilgængelige udgivelser, herunder udgivelser af ønsket medie, som du ikke følger. Hvis du kigger på fejlfindingslogfilerne, kan du se, at disse udgivelser bliver behandlet, hvilket er helt normalt.
- Lidarr pålægger en minimumsinterval på 10 minutter for RSS-synkronisering og en maksimuminterval på 2 timer. 15 minutter er det anbefalede minimum af de fleste indekseringswebsteder, selvom nogle tillader kortere intervaller, og 2 timer sikrer, at Lidarr checker ofte nok til ikke at gå glip af en udgivelse (selvom den kan bladre gennem RSS-feedet på mange indekseringswebsteder for at hjælpe med det). Nogle indekseringswebsteder tillader klienter at udføre en RSS-synkronisering hyppigere end hvert 10. minut, i sådanne tilfælde anbefaler vi at bruge Lidarr's Release-Push API-endepunkt sammen med en IRC-annoncekanal til at sende udgivelser til Lidarr til behandling, hvilket kan ske næsten i realtid og med mindre belastning på indekseringswebstedet og Lidarr, da Lidarr ikke behøver at anmode om RSS-feedet for ofte og behandle de samme udgivelser igen og igen.

## Hvordan finder Lidarr udgivelser?

- Lidarr søger ''ikke'' regelmæssigt efter albumfiler, der mangler eller ikke opfylder deres kvalitetsmål. I stedet forespørger den ret ofte dine indekseringswebsteder og trackere efter ''alle'' de nyoprettede udgivelser og sammenligner derefter med sin liste over udgivelser, der mangler eller skal opgraderes. Eventuelle match bliver downloadet. Dette gør det muligt for Lidarr at dække en bibliotek af ''enhver størrelse'' med kun 24-100 forespørgsler om dagen (RSS-interval på 15-60 minutter). Hvis du forstår dette, vil du indse, at det kun dækker fremtiden.
- Så hvordan håndterer du nutiden og fortiden? Når du tilføjer et album, skal du indstille den korrekte sti, profil og overvågningsstatus og derefter bruge afkrydsningsfeltet Start søgning efter manglende album. Hvis albummet endnu ikke er udgivet, behøver du ikke at starte en søgning.
- Med andre ord vil Lidarr kun finde udgivelser, der er nyoploadet til dine indekseringswebsteder. Den vil ikke aktivt forsøge at finde udgivelser, du ønsker, der blev uploadet i fortiden.
- Hvis du allerede har tilføjet albummet, men nu vil søge efter det, har du nogle valgmuligheder. Du kan gå til albummets side og bruge søgeknappen, der vil udføre en søgning og derefter automatisk vælge en. Du kan bruge fanen Søg og se ''alle'' resultaterne og manuelt vælge den, du ønsker. Eller du kan bruge filtrene `Mangler`, `Ønsket` eller `Klipning ikke opfyldt`.
- Hvis Lidarr har været offline i en længere periode, vil Lidarr forsøge at bladre tilbage for at finde den sidste udgivelse, den behandlede, for at undgå at gå glip af en udgivelse. Så længe din indekseringswebsted understøtter bladring, og det ikke er for længe siden, vil Lidarr være i stand til at behandle de udgivelser, den ville have gået glip af, og undgå at du skal udføre en søgning efter de manglende udgivelser.

## Tvungen godkendelse

Hvis Lidarr er eksponeret, så UI'en kan tilgås uden for dit lokale netværk, skal du have en form for godkendelsesmetode aktiveret for at få adgang til UI'en. Dette kræves også i stigende grad af trackere og indekseringswebsteder.

Fra og med Lidarr v2 er godkendelse obligatorisk.

### Godkendelsesmetode

- `Basic` (Browser pop-up) - Denne indstilling viser en lille pop-up, når du tilgår din Lidarr, der giver dig mulighed for at indtaste et brugernavn og adgangskode.
- `Forms` (Login-side) - Denne indstilling har en login-side, der ligner dem, du finder på andre websteder, og som giver dig mulighed for at logge ind på din Lidarr.
- `External` - Konfigurerbar via konfigurationsfilen
  - Hvis du bruger en **ekstern godkendelse** som f.eks. Authelia, Authetik, NGINX Basic auth osv., kan du undgå at skulle godkende to gange ved at lukke appen ned, indstille `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurationsfilen](/lidarr/appdata-directory) og genstarte appen. **Bemærk, at flere `AuthenticationMethod`-poster i filen ikke understøttes, og kun den øverste værdi vil blive brugt**.

### Påkrævet godkendelse

- Hvis du ikke udsætter appen eksternt og/eller ikke ønsker, at godkendelse skal være påkrævet for lokal adgang (f.eks. LAN), skal du ændre indstillingen i Indstillinger => Generel sikkerhed => Påkrævet godkendelse til `Deaktiveret for lokale adresser`
  - Den tilsvarende indstilling i konfigurationsfilen er `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`

## Hvordan sammenlignes mulige downloads?

> Generelt har kvalitet højeste prioritet. Hvis du ønsker, at kvalitet ikke skal være den vigtigste prioritet, kan du sammenflette dine kvaliteter. [Se TRaSH's guide](https://trash-guides.info/merge-quality)***
{.is-info}

- Den aktuelle logik [kan findes her](https://github.com/Lidarr/Lidarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs).

- Fra og med 2022-01-23 er logikken som følger:

1. Kvalitet
1. Foretrukken ordvurdering
1. Protokol (som konfigureret i den relevante forsinkelsesprofil)
1. Indekseringsprioritet
1. Seedere/leechere (hvis torrent)
1. Antal albummer
1. Alder (hvis Usenet)
1. Størrelse

## Lidarr stoppede med at virke efter opdatering til Ubuntu 22.04

- Lidarr v0.8 er ikke kompatibel og understøttes ikke på Ubuntu 22.04
- Kun Lidarr v1 understøtter Ubuntu 22.04
- [Se dette FAQ-indlæg for grene og versioner](#hvordan-opdaterer-jeg-lidarr)

## Hvorfor kan jeg ikke tilføje en ny udgivelse eller kunstner til Lidarr?

- Udspillet er sandsynligvis af typen "ukendt" på MusicBrainz

## Hvorfor kan jeg ikke tilføje et album med forskellige kunstnere?

- "Various Artists" og andre meta-kunstnere på MusicBrainz skyldes antallet af poster, de indeholder.

## Hvorfor viser Lidarr kun studiealbummer? Hvordan finder jeg singler eller EP'er?

- Lidarr viser som standard kun studiealbummer for hver kunstner. Du kan dog udvide albumtyperne for en kunstner eller for hele dit bibliotek ved at bruge metadata-profiler.

## Kan jeg tilføje bare et album?

- Ikke i øjeblikket.

## Kan jeg downloade enkeltspor?

- Lidarr fungerer ved at søge efter og downloade fulde udgivelser, så enkeltspor kan ikke downloades, medmindre de blev udgivet som singler af kunstneren.

## Hvorfor vises kunstneren X ikke i søgningen?

- Søgningen er stadig under udvikling. Kunstnere, der ikke vises i søgningen, kan tilføjes ved at søge efter `lidarr:mbid`, hvor `mbid` er kunstnerens MusicBrainz-ID.

## Lidarr matchede et album med for mange spor. Hvordan kan jeg ændre albummet til den korrekte udgivelse?

- Åbn albummets detaljeside og vælg redigeringsikonet i topmenuen. Her kan du finde en rulleliste over alle udgivelser, der er knyttet til det album.

## Jeg kan ikke finde en udgivelse i Lidarr, men den er på MusicBrainz

- Dette skyldes sandsynligvis, at udgivelsen har en "ukendt" udgivelsesstatus. Opdater MusicBrainz.

## Hvor ofte synkroniseres Lidarr's og MusicBrainz's databaser?

- Hver time fem minutter over timen

## Hvordan kan jeg tilføje manglende kunstnerbilleder?

- Tilføj kunst til fanart.tv og vent ~7+ dage, indtil det rydder igennem cachen. Opdater derefter metadataen.

## Hvordan kan jeg få manglende albumbilleder? (Cover Art)

- Tilføj coverart til musicbrainz og vent ~1 time+ på, at det rydder igennem cachen. Opdater derefter metadataen.

## Jeg har problemer med at importere mine kunstnere, hvad kan det være?

- Kunstnerimportprocessen importerer kun kunstnernavne og stioplysninger, som derefter gemmes i databasen, således at a) metadata kan hentes, og b) downloadet indhold kan placeres på samme placering i fremtiden. Til dette formål skal brugerkontoen, som Lidarr kører under, have både læse- og skriveadgang til din data-mappe.

## Hvordan kan jeg omdøbe mine kunstnermapper?

{#rename-folders}

> Den samme proces gælder også for flytning/ændring af kunstnerstier.
{.is-info}

1. Bibliotek
1. Masseeditor
1. Vælg de kunstnere, der skal have deres mappe omdøbt
1. Skift rodmappe til den samme rodmappe, som kunstnerne allerede eksisterer i
1. Vælg "Ja, flyt filer"

## Hvordan kan jeg masse-slette kunstnere fra ønskelisten?

- Brug Masseeditor => Vælg de kunstnere, du vil slette => Slet

## Hvorfor virker Lidarr ikke bag en omvendt proxy

- Lidarr bruger .NET og en ny webserver. For at SignalR kan fungere, for at UI-knapperne kan fungere, for at databaseændringer kan tage effekt og for andre ting kræver det følgende tilføjelse til placeringen for Lidarr i konfigurationsfilen:
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;

- Sørg for, at du `ikke` inkluderer `proxy_set_header Connection "Upgrade";`, som foreslået af nginx-dokumentationen. `DETTE VIL IKKE VIRKE`
- [Se dette ASP.NET Core-problem](https://github.com/aspnet/AspNetCore/issues/17081)
- Hvis du bruger en CDN som Cloudflare, skal du sørge for, at websockets er aktiveret for at tillade websocket-forbindelser.

## Hvordan opdaterer jeg Lidarr?

- Gå til Indstillinger og derefter fanen Generelt og vis avancerede indstillinger (brug vippekontakten ved siden af gem-knappen).

1. Under afsnittet Opdateringer skal du ændre grennavnet til `master` eller `develop`
1. Gem

*Dette installerer ikke øjeblikkeligt bitene fra den gren, det sker under den næste opdatering.*



- `master` - ![Nuværende Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Denne version er blevet testet af brugere på udviklings- og nightly-grenene, og der er ikke kendt nogen større problemer. Denne version vil modtage opdateringer cirka en gang om måneden. På GitHub er dette `master`-grenen.

- `develop` - ![Nuværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) - (Beta): Dette er kanten til test. Udgivet efter test i nightly for at sikre, at der ikke er umiddelbare problemer. Nye funktioner og fejlrettelser udgives først her efter nightly. Det kan betragtes som halvstabilt, men er stadig `beta`. Denne version vil modtage opdateringer enten ugentligt eller hver anden uge afhængigt af udviklingen.

> **Advarsel: Du kan muligvis ikke skifte tilbage til `master` efter at have skiftet til denne gren.** På GitHub er dette et øjebliksbillede af `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- `nightly` - ![Nuværende Nightly/Ustabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) - (Alpha/Ustabil): Dette er den nyeste version. Den udgives, så snart koden er forpligtet og består alle automatiserede tests. Denne version er muligvis ikke blevet brugt af os eller andre brugere endnu. Der er ingen garanti for, at den vil køre i visse tilfælde. Denne gren anbefales kun til avancerede brugere. Der forventes problemer og egen undersøgelse i denne gren. ***Brug denne gren kun, hvis du ved, hvad du laver, og er villig til at få beskidte hænder for at gendanne en mislykket opdatering.*** Denne version opdateres øjeblikkeligt.

> **Advarsel: Du kan muligvis ikke skifte tilbage til `master` efter at have skiftet til denne gren.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Bemærk: Hvis du installerer via Docker, skal du tilføje `:release`, `:latest`, `:testing` eller `:develop` til slutningen af din container-tag afhængigt af, hvem der laver dine bygninger. Bemærk venligst, at `nightly`-grenene bevidst ikke er angivet nedenfor.

|                                                                    | `master` (stabil) ![Nuværende Master/Seneste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Nuværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/develop/changes) | `nightly` (alpha) ![Nuværende Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://lidarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/lidarr)                       | `release`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-lidarr) | `latest`                                                                                                                                                                                                              | `develop`                                                                                                                                                                                                           | `nightly`                                                                                                                                                                                                             |

### Kan jeg opdatere Lidarr inde i min Docker-container?

- *Teknisk set, ja.* **Men du bør absolut ikke gøre det.** Det er en grundlæggende filosofi i Docker. Der kan opstå databaseproblemer, hvis du opgraderer din installation indeni til den nyeste `nightly`, men derefter opdaterer Docker-containeren selv (muligvis nedgraderer til en ældre version).

### Installation af en nyere version

#### Native

1. Gå til System og derefter fanen Opdateringer
1. Nyere versioner, der endnu ikke er installeret, vil have en opdateringsknap ved siden af dem. Klik på den knap for at installere opdateringen.

#### Docker

1. Træk din tag igen og opdater din container

## Kan jeg skifte fra `nightly` tilbage til `develop`?

## Kan jeg skifte mellem grene?

- Hvis versionen er identisk, kan du skifte, ellers skal du kontakte udviklingsteamet for at se, om du kan skifte fra `nightly` til `master`; `nightly` til `develop`; eller `develop` til `master` for din specifikke bygning.
- Hvis du ikke følger disse instruktioner, kan din Lidarr blive ubrugelig eller kaste fejl. Du er blevet advaret
  - Den mest almindelige fejl er noget som `Error parsing column 45 (Language=31 - Int64)` eller andre lignende databasefejl omkring manglende kolonner eller tabeller.

## Jeg får en fejl: Database disk image is malformed

- **Fejl med `Error creating log database` indikerer problemer med logs.db**
  - Dette kan hurtigt løses ved at omdøbe eller fjerne databasen. Logs-databasen indeholder uvigtige oplysninger om kommandohistorik og opdateringsinstallationshistorik samt Info-, Warn- og Error-poster
- **Fejl med `Error creating main database` eller generisk `database disk image is malformed` uden specificeret database indikerer problemer med lidarr.db**
  - Fortsæt med de nedenstående trin
- Dette betyder, at din SQLite-database, der gemmer størstedelen af ​​informationen for Lidarr, er beskadiget. Dine muligheder er at prøve (en) sikkerhedskopi(er), prøve at gendanne den eksisterende database, prøve at gendanne sikkerhedskopierne eller hvis alt andet fejler, starte forfra med en frisk ny database.
- Denne fejl kan vises, hvis databasefilen ikke kan skrives af brugergruppen \*Arr kører som. Tilladelser som årsag vil sandsynligvis kun være et problem for nye installationer, migrerede installationer til en ny server, hvis du for nylig har ændret tilladelserne for din appdata-mappe eller hvis du har ændret brugeren og gruppen \*Arr kører som.
- Dit bedste og første mulighed er at [prøve at gendanne fra en sikkerhedskopi](#hvordan-sikkerhedskopierer-gendanner-jeg-min-lidarr)
- Du kan også prøve at gendanne din database. Dette er normalt den eneste mulighed, når dette problem opstår efter en opdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis din sqlite ikke har `.recover` eller du ønsker en mere GUI-venlig måde (f.eks. Windows), skal du følge [vores instruktioner på dette wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- En anden mulig årsag til, at du får en fejl med din database, er, at du placerer din database på et netværksdrev (nfs eller smb eller noget andet, der ikke er lokalt). **SQLite er designet til situationer, hvor data og applikationen eksisterer på samme maskine.** Derfor skal din \*Arr AppData-mappe (/config mount for docker) være på lokal lagerplads. [SQLite og netværksdrev fungerer ikke godt sammen og vil på et tidspunkt forårsage en beskadiget database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruger mergerFS, skal du fjerne `direct_io`, da SQLite bruger mmap, som ikke understøttes af `direct_io`, som forklaret i mergerFS [dokumentationen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Hvordan sikkerhedskopierer/gendanner jeg min Lidarr?

### Sikkerhedskopiering af Lidarr

#### Brug af indbygget sikkerhedskopiering

- Gå til System => Backup i Lidarr UI'en
- Klik på Sikkerhedskopier-knappen
- Download zip-filen efter at sikkerhedskopien er oprettet for at gemme den sikkert

#### Brug af filsystemet direkte

- Find placeringen af AppData-mappen for Lidarr  
  - Via Lidarr UI'en gå til System => Om  
  - [Lidarr Appdata-mappen](/lidarr/appdata-directory)
- Stop Lidarr - Dette forhindrer, at databasen bliver beskadiget
- Kopier indholdet til et sikkert sted

### Gendannelse fra sikkerhedskopi

> Gendannelse til et operativsystem, der bruger forskellige stier, vil ikke fungere (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows), flytning mellem OS X og Linux kan muligvis fungere, da begge bruger stier, der indeholder `/` i stedet for `\` som Windows bruger, men det understøttes ikke. Du skal manuelt redigere alle stier i databasen.
{.is-warning}

#### Brug af zip-sikkerhedskopi

- Geninstaller Lidarr (hvis relevant / ikke allerede installeret)
- Kør Lidarr
- Gå til System => Backup
- Vælg Gendan sikkerhedskopi
- Vælg Vælg fil
- Vælg din sikkerhedskopizip-fil
- Vælg Gendan

#### Brug af filsystem-sikkerhedskopi

- Geninstaller Lidarr (hvis relevant / ikke allerede installeret)
- Find placeringen af AppData-mappen for Lidarr  
  - Kør Lidarr en gang og gå via UI'en til System => Om  
  - [Lidarr Appdata-mappen](/lidarr/appdata-directory)
- Stop Lidarr
- Slet indholdet af AppData-mappen **(Inklusive .db-wal/.db-journal-filerne, hvis de findes)**
- Gendan fra din sikkerhedskopi
- Start Lidarr
- Så længe stierne er de samme, vil alt fortsætte, hvor det slap

#### Gendannelse af filsystem på Synology NAS

> ADVARSEL: Gendannelse på en Synology kræver kendskab til Linux og Root SSH-adgang til Synology-enheden.
{.is-warning}

- Geninstaller Lidarr (hvis relevant / ikke allerede installeret)
- Find placeringen af AppData-mappen for Lidarr  
  - Kør Lidarr en gang og gå via UI'en til System => Om  
  - [Lidarr Appdata-mappen](/lidarr/appdata-directory)
- Stop Lidarr
- Opret forbindelse til Synology NAS via SSH og log ind som root  

> På nogle installationer er brugeren anderledes end nedenstående kommandoer: `chown -R sc-Lidarr:Lidarr *` {.is-info}

- Udfør følgende kommandoer:

```shell
rm -r /usr/local/Lidarr/var/.config/Lidarr/Lidarr.db
cp -f /tmp/Lidarr_backup/* /usr/local/Lidarr/var/.config/Lidarr/
```

- Opdater tilladelserne på filerne:

 ```shell
cd /usr/local/Lidarr/var/.config/Lidarr/
chown -R Lidarr:users *
chmod -R 0644 *
```

- Start Lidarr

## Jeg bruger Lidarr på en Mac, og den stoppede pludselig med at fungere. Hvad skete der?

- Mest sandsynligt skyldes dette en MacOS-fejl, der forårsagede, at en af ​​databaserne blev beskadiget.

- Se ovenstående indgang om beskadiget database.

- Prøv derefter at starte og se, om det virker. Hvis det ikke virker, har du brug for yderligere support. Indsend i vores [subreddit /r/lidarr](http://reddit.com/r/lidarr) eller hop på [vores discord](https://lidarr.audio/discord) for hjælp.

## Jeg bruger en Pi og Raspbian, og Lidarr vil ikke starte

Raspbian har en version af libseccomp2, der er for gammel til at understøtte kørsel af en Docker-container baseret på Ubuntu 20.04, som både hotio og LinuxServer bruger som deres grundlag. Du skal enten bruge `--privileged`, opdatere libseccomp2 fra Ubuntu eller få et bedre operativsystem (Vi anbefaler Ubuntu 20.04 arm64).

**Mulig løsning:**

Lykkedes med at løse problemet ved at installere backporten fra debian repo. Generelt anbefales det ikke at bruge backport i blanket opgraderingstilstand. Installation af en enkelt pakke kan være ok, men kan også forårsage problemer. Så forstå, hvad du laver.

Trin til at løse:

Sørg først for, at du kører Raspbian buster, f.eks. ved hjælp af `lsb_release -a`

> Distributor ID: Raspbian
> Description: Raspbian GNU/Linux 10 (buster)
> Release: 10
> Codename: buster

- Hvis du bruger buster:
  - Kør følgende for at tilføje backports til dine kilder

  ```shell
   echo "deb <http://deb.debian.org/debian> buster-backports main" | sudo tee /etc/apt/sources.list.d/buster-backports.list
   ```

  - Installer backporten af libseccomp2

  ```shell
  sudo apt update && sudo apt-get -t buster-backports install libseccomp2
  ```

## Hvorfor tager synkronisering af lister så lang tid, og kan jeg ændre det?

Lister var aldrig og er heller ikke beregnet til at være "tilføj det nu", de er værktøjer til "hej, jeg vil gerne have dette, tilføj det på et tidspunkt".

Du kan udløse en manuel opdatering af en liste, skrive et script og udløse det via API'en eller tilføje udgivelser direkte til Lidarr.

Denne ændring blev foretaget for at undgå, at vores server blev dræbt af folk, der opdaterede lister hvert 10. minut.

## Kan jeg deaktivere opgaven "Opdater udgivelser"?

Nej, og du bør heller ikke gøre det gennem nogen SQL-hack. Opgaven "Opdater udgivelser" forespørger den upstream Servarr-proxy og kontrollerer, om metadataen for hver udgivelse (id'er, rollebesætning, resumé, vurdering, oversættelser, alternative titler osv.) er blevet opdateret i forhold til det, der er i øjeblikket i Lidarr. Hvis det er nødvendigt, opdateres de relevante udgivelser.

En almindelig klage er, at opgaven "Opdater" forårsager tung I/O-brug. En indstilling, der kan forårsage problemer, er "Genindlæs kunstnermappe efter opdatering". Hvis din disk I/O-brug stiger under en opdatering, kan du ændre genindlæsningsindstillingen til `Manuel`. Skift ikke dette til `Aldrig`, medmindre alle ændringer i dit bibliotek (nye udgivelser, opgraderinger, sletninger osv.) udføres gennem Lidarr. Hvis du sletter udgivelsesfiler manuelt eller med et program fra tredjepart, skal du ikke indstille dette til `Aldrig`.

## Hvorfor kan Lidarr ikke se mine filer på en fjernserver?

- For alle operativsystemer skal du sikre dig, at den bruger/gruppe, som du kører \*Arr som, har læse- og skriveadgang til det monterede drev.
- For Linux skal du sikre dig:
  - Hvis du bruger en NFS-montering, skal du sikre dig, at `nolock` er aktiveret for din montering.
  - Hvis du bruger en SMB-montering, skal du sikre dig, at `nobrl` er aktiveret for din montering.
- For Windows: Kort sagt: Brugeren, som \*Arr kører som (hvis det er en tjeneste) eller under (hvis det er en bakkeapp), kan ikke få adgang til filstien på den fjernserver. Dette kan skyldes forskellige årsager, men den mest almindelige er, at \*Arr kører som en tjeneste, hvilket forårsager de beskrevne problemer.

### Lidarr kører som standard under LocalService-kontoen, som ikke har adgang til beskyttede fjernfiler

- Kør Lidarr-tjenesten som en anden bruger, der har adgang til den delte mappe
- Åbn vinduet Administrative værktøjer \> Tjenester på din Windows-server.
- Stop Lidarr-tjenesten.
- Åbn dialogboksen Egenskaber \> Logon.
- Skift brugerkontoen for tjenesten til målbrugerkontoen.
- Kør Lidarr.exe ved hjælp af opstartsmappe

### Du bruger et kortlagt netværksdrev (ikke en UNC-sti)

- Skift dine stier til UNC-stier (`\\server\share`)
- Kør Lidarr.exe via opstartsmappe

## Hjælp, jeg har låst mig ude

{#help-i-have-forgotten-my-password}

For at deaktivere godkendelse (for at nulstille dit glemte brugernavn eller adgangskode) skal du redigere `config.xml`, som vil være inde i [Lidarr Appdata-mappen](/lidarr/appdata-directory)

1. Åbn config.xml i en teksteditor
1. Find linjen med godkendelsesmetoden, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Ændr linjen `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Genstart Lidarr
1. Lidarr vil nu være tilgængelig uden adgangskode, du skal gå til `Indstillinger: Generelt` i brugergrænsefladen og indstille dit brugernavn og adgangskode

## Hvordan stopper jeg browseren fra at starte ved opstart?

Afhængigt af dit operativsystem er der flere mulige måder.

- I `Indstillinger` => `Generelt` på nogle operativsystemer er der en afkrydsningsboks til at starte browseren ved opstart.
- Når du starter Lidarr, kan du tilføje `-nobrowser` (*nix) eller `/nobrowser` (Windows) til argumenterne.
- Stop Lidarr og rediger config.xml-filen, og ændr `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Underlige UI-problemer

- Hvis du oplever underlige UI-problemer som f.eks. at bibliotekssiden ikke viser noget eller en bestemt visning eller sortering ikke fungerer, skal du prøve at se det i et Chrome Inkognitovindue eller Firefox Privat vindue. Hvis det fungerer fint der, skal du rydde din browsers cache og cookies for din specifikke IP/domæne. Se den [Ryd Cache Cookies og Lokal Lagring](/useful-tools#clearing-cookies-and-local-storage) wiki-artikel for mere information.

## VPN'er, Jackett og \*ARRs

- Medmindre du befinder dig i et undertrykkende land som Kina, Australien eller Sydafrika, er din torrentklient typisk det eneste, der skal være bag en VPN. Fordi VPN-endepunktet deles af mange brugere, kan du opleve begrænsning af hastigheden, beskyttelse mod DDOS og IP-blokeringer fra forskellige tjenester, som hver software bruger.
- Med andre ord kan det at placere \*Arrs (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bag en VPN gøre applikationerne ubrugelige i nogle tilfælde på grund af manglende adgang til tjenesterne.

> **For at være klar er det ikke et spørgsmål om, hvorvidt VPN'er vil forårsage problemer med \*Arrs, men hvornår: billedudbydere vil blokere dig, og cloudflare er foran de fleste \*Arr-servere (opdateringer, metadata osv.) og kan også blokere dig**
{.is-warning}

- **Mange private trackere vil udelukke dig, hvis du bruger eller får adgang til dem (f.eks. ved hjælp af Jackett eller Prowlarr) via en VPN.**

### Brug af en VPN

- Hvis en VPN er påkrævet, og Docker bruges, anbefales det at bruge Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er påkrævet, og Docker ikke bruges, skal din VPN-klient ***understøtte*** split tunneling, så kun de nødvendige (Download Client) apps er bag VPN'en.
- Mange problemer med adgang til trackere kan løses ved at bruge Googles eller Cloudflares DNS-servere i stedet for din internetudbyders DNS-servere.
- I nogle tilfælde (f.eks. britiske internetudbydere) skal du muligvis placere din torrent-downloadklient bag en VPN og Jackett/Prowlarr som følger:
  - Placer Jackett bag VPN'en og sørg for, at split tunneling tillader lokal adgang
  - For Prowlarr skal du konfigurere din VPN-klient til at levere en proxy og tilføje proxyen i Indstillinger => Indekser. Giv proxyen en tag, og tildel den samme tag til eventuelle indekser, der skal bruge den.
    - Hvis det absolut er nødvendigt, og hvis din VPN ikke giver en måde at oprette en proxy på, kan du placere Prowlarr bag VPN'en og sikre, at split tunneling tillader lokal adgang.

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordel. Alt andet er potentielle problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje at bruge Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)
- **Opdatering april 2022: \*Arr-support er blevet fjernet for jackett `/all`, fordi det kun skaber problemer.**
- Jackett /all-endepunktet er praktisk, men det er den eneste fordel. Alt andet er potentielle problemer, så det er nu nødvendigt at tilføje hver tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af /all-endepunktet har ingen fordele, kun ulemper:
  - du mister kontrollen over indstillingen for den enkelte indekser (kategorier, søgemetoder osv.)
  - blanding af søgemetoder (IMDB, forespørgsel osv.) kan give resultater af lav kvalitet
  - indekser-specifikke kategorier (\>= 100000) kan ikke bruges.
  - langsomme indekser vil sænke den samlede hastighed
  - det samlede antal resultater er begrænset til 1000
  - hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

### Jackett /All-løsninger

- Tilføj hver tracker i Jackett manuelt som en indekser i \*Arr
- Prøv [Prowlarr](/prowlarr), som kan synkronisere indeksere til \*Arr og er udviklet af Lidarr/Radarr/Readarr-udviklingsteamet.
- Prøv [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indeksere til \*Arr. Men brug ikke deres enkeltstående aggregat-endepunkt, og brug `multi`, hvis synkroniseringen skal bruges.

## Hvorfor er der to filer? | Hvorfor er der en fil tilbage i downloads?

Dette er forventet. Med en konfiguration, der understøtter [hardlinks](https://trash-guides.info/hardlinks), vil dobbelt plads ikke blive brugt. Her er, hvordan Torrent-processen fungerer.

1. Lidarr sender en downloadanmodning til din klient og tilknytter den med et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: film, tv, serier, musik osv.
1. Lidarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Denne overvågning sker via din downloadklients API.
1. Færdige filer efterlades på deres oprindelige placering for at tillade, at du seed-filerne (forhold eller tid kan justeres i downloadklienten eller inden for den specifikke downloadklient). Når filer importeres til din mediemappe, oprettes der en hardlink til filen, hvis det understøttes af din konfiguration, eller filen kopieres, hvis hardlinks ikke understøttes.
1. Hvis indstillingen "Behandling af færdig download - Fjern færdige" er aktiveret i Lidarrs indstillinger, vil Lidarr slette den oprindelige fil og torrent fra din downloadklient, men kun hvis downloadklienten rapporterer, at seeding er fuldført, og torrenten er stoppet (dvs. sat på pause). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for at få vejledning om, hvordan du konfigurerer din downloadklient optimalt.

> Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din færdige downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlink mislykkes, eller din konfiguration ikke understøtter hardlinks, vil den falde tilbage og kopiere filen.
{.is-info}

## Jeg får konstant advarsler fra min cloud-lagring om API-grænser

Lidarr er ikke som de andre Arrs. Den bruger tags i stedet for filnavne til drift. Hvis du opbevarer Lidarr-filer på cloud-lagring, skal den downloade filen for at læse tagsene. Dette vil meget hurtigt overskride eventuelle API-grænser, du har hos din lagringsudbyder. Vi fraråder kraftigt at opbevare dit Lidarr-bibliotek på en cloud-lagringstjeneste, og eventuelle problemer, du oplever, skyldes sandsynligvis denne opsætning.