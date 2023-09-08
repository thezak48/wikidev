## Kan alle mine filmfiler gemmes i én mappe?

Ja, Radarr giver dig mulighed for at gemme alle dine filmfiler i én mappe. Du kan konfigurere dette ved at følge disse trin:

1. Åbn Radarr-webgrænsefladen.
2. Klik på "Indstillinger" i navigationsmenuen til venstre.
3. Vælg fanen "Mediehåndtering".
4. Rul ned til afsnittet "Filhåndtering".
5. Aktivér indstillingen "Flyt filer" ved at markere afkrydsningsfeltet.
6. Vælg den ønskede mappe ved at klikke på "Gennemse" og navigere til den ønskede placering.
7. Klik på "Gem" for at gemme ændringerne.

Bemærk, at hvis du vælger at gemme alle dine filmfiler i én mappe, vil filerne ikke længere være organiseret i undermapper baseret på filmens titel. Dette kan gøre det sværere at finde specifikke film, hvis du har en stor samling.

- Nej, og årsagen er, at Radarr er en forgrening af [Sonarr](/sonarr), hvor hver serie har en mappe. Denne begrænsning er et kendt problem for mange brugere og vil måske blive løst i en fremtidig version. Bemærk, at det ikke er en simpel ændring og faktisk kræver en komplet omskrivning af backenden.
- [GitHub-problemet med brugerdefinerede mapper](https://github.com/Radarr/Radarr/issues/153) dækker teknisk set denne anmodning, men der er ingen garanti for, at alle filmfiler i én mappe vil blive implementeret på det tidspunkt.
- En let hack-agtig løsning beskrives nedenfor. Bemærk, at du ikke må udløse en genindlæsning i Radarr, da den vil blive vist som manglende, og uanset hvad vil filmen aldrig blive opgraderet.
  - Brug et brugerdefineret script
    - Scriptet skal udløses ved import
    - Det skal designes til at flytte filen, når du ønsker det
    - Derefter skal det kalde Radarr API'en og ændre filmen til ikke-overvåget.
- Hvis du vil flytte alle dine film fra én mappe til individuelle mapper, kan du læse artiklen [Tips og tricks-sektionen => Opret en mappe til hver film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

## Kan jeg placere alle mine film i mit bibliotek i én mappe?

- Nej, se ovenfor.

## Hvordan opdaterer jeg Radarr?

- Gå til Indstillinger og derefter fanen Generelt og vis avancerede indstillinger (brug vippekontakten ved siden af gem-knappen).

1. Under afsnittet Opdateringer skal du ændre grennavnet til `master` eller `develop`.
1. Gem.

*Dette vil ikke installere biterne fra den gren øjeblikkeligt, det vil ske under den næste opdatering.*

- ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Det er blevet testet af brugere på udviklings- og nightly-grenene, og der er ikke kendt nogen større problemer. Denne version vil modtage opdateringer cirka en gang om måneden. På GitHub er dette `master`-grenen.

- ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Beta): Dette er kanten for testning. Udgivet efter testning i nightly for at sikre, at der ikke er umiddelbare problemer. Nye funktioner og fejlrettelser udgives først her efter nightly. Det kan betragtes som halvstabilt, men er stadig `beta`. Denne version vil modtage opdateringer enten ugentligt eller hver anden uge afhængigt af udviklingen.

> **Advarsel: Du kan muligvis ikke skifte tilbage til `master` efter at have skiftet til denne gren.** På GitHub er dette et øjebliksbillede af `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alpha/Ustabil): Dette er den absolut nyeste version. Den udgives, så snart koden er forpligtet og består alle automatiserede tests. Denne version er muligvis ikke blevet brugt af os eller andre brugere endnu. Der er ingen garanti for, at den vil køre i visse tilfælde. Denne gren anbefales kun til avancerede brugere. Der forventes problemer og egen undersøgelse i denne gren. ***Brug denne gren kun, hvis du ved, hvad du laver, og er villig til at få beskidte hænder for at gendanne en mislykket opdatering.*** Denne version opdateres øjeblikkeligt.

> **Advarsel: Du kan muligvis ikke skifte tilbage til `master` efter at have skiftet til denne gren.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Bemærk: Hvis du har installeret via Docker, skal du tilføje `:release`, `:latest`, `:testing` eller `:develop` til slutningen af din container-tag afhængigt af, hvem der laver dine bygninger.

|                                                                    | ![Current Master/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kan jeg opdatere Radarr inde i min Docker-container?

- *Teknisk set ja.* **Men du bør absolut ikke gøre det.** Det er en grundlæggende filosofi i Docker. Der kan opstå databaseproblemer, hvis du opgraderer din installation indeni til den nyeste `nightly`, men derefter opdaterer Docker-containeren selv (muligvis nedgraderer til en ældre version).

### Installation af en nyere version

#### Lokal installation

1. Gå til System og derefter fanen Opdateringer
1. Nyere versioner, der endnu ikke er installeret, vil have en opdateringsknap ved siden af dem. Klik på den knap for at installere opdateringen.

#### Docker

1. Træk din tag igen og opdater din container

## Kan jeg skifte fra `nightly` tilbage til `develop`?

## Kan jeg skifte mellem grenene?

- Hvis versionen er identisk, kan du skifte, ellers skal du kontakte udviklingsteamet for at se, om du kan skifte fra `nightly` til `master`; `nightly` til `develop`; eller `develop` til `master` for din specifikke version.
- Hvis du ikke følger disse instruktioner, kan din Radarr blive ubrugelig eller kaste fejl. Du er blevet advaret. Hvis følgende fejl opstår, bruger du en nyere database med en ældre \*Arr-version, som ikke understøttes. Opgrader \*Arr til den version, du tidligere brugte, eller en nyere.
  - Eksempel på fejlmeddelelser:
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - Andre lignende databasefejl om manglende kolonner eller tabeller.

## Hvordan sikkerhedskopierer/gendanner jeg Radarr?

### Sikkerhedskopiering af Radarr

#### Brug af indbygget sikkerhedskopiering

- Gå til System => Sikkerhedskopier i Radarr UI'en
- Klik på Sikkerhedskopier-knappen
- Download zip-filen efter sikkerhedskopieringen er oprettet for at gemme den sikkert

#### Brug af filsystemet direkte

- Find placeringen af AppData-mappen for Radarr
  - Gå til System => Om i Radarr UI'en
  - [Radarr Appdata-mappen](/radarr/appdata-directory)
- Stop Radarr - Dette forhindrer, at databasen bliver beskadiget
- Kopier indholdet til et sikkert sted

### Gendannelse fra sikkerhedskopiering

> Gendannelse til et operativsystem, der bruger forskellige stier, vil ikke virke (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows). Flytning mellem OS X og Linux kan muligvis fungere, da begge bruger stier, der indeholder `/` i stedet for `\`, som Windows bruger, men det understøttes ikke. Du skal manuelt redigere alle stier i databasen eller bruge [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Brug af zip-sikkerhedskopiering

- Geninstaller Radarr (hvis relevant / ikke allerede installeret)
- Kør Radarr
- Gå til System => Sikkerhedskopier
- Vælg Gendan sikkerhedskopiering
- Vælg Vælg fil
- Vælg din sikkerhedskopierings-zip-fil
- Vælg Gendan

#### Brug af filsystem-sikkerhedskopiering

- Geninstaller Radarr (hvis relevant / ikke allerede installeret)
- Find placeringen af AppData-mappen for Radarr
  - Kør Radarr én gang og gå til System => Om i UI'en
  - [Radarr Appdata-mappen](/radarr/appdata-directory)
- Stop Radarr
- Slet indholdet af AppData-mappen **(Inklusive .db-wal/.db-journal-filerne, hvis de findes)**
- Gendan fra din sikkerhedskopiering
- Start Radarr
- Hvis stierne er de samme, vil alt fortsætte, hvor det slap

#### Gendannelse af filsystem på Synology NAS

> FORSIGTIG: Gendannelse på en Synology kræver kendskab til Linux og root SSH-adgang til Synology-enheden.
{.is-warning}

- Geninstaller Radarr (hvis relevant / ikke allerede installeret)
- Find placeringen af AppData-mappen for Radarr
  - Kør Radarr én gang og gå til System => Om i UI'en
  - [Radarr Appdata-mappen](/radarr/appdata-directory)
- Stop Radarr
- Opret forbindelse til Synology NAS via SSH og log ind som root

> På nogle installationer er brugeren anderledes end i nedenstående kommandoer: `chown -R sc-Radarr:Radarr *` {.is-info}

- Udfør følgende kommandoer:

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- Opdater tilladelserne på filerne:

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Start Radarr

# Almindelige problemer med Radarr

## En opgave blev annulleret

- Radarr modtog intet svar fra serveren, som anmodningen blev sendt til, efter 100 sekunder.
- Logfilerne vil indeholde `System.Threading.Tasks.TaskCanceledException: A task was canceled.` (En opgave blev annulleret).
- Dette skyldes ofte:
  - forkert konfigureret eller brug af en VPN
  - forkert konfigureret eller brug af en proxy
  - lokale DNS-problemer - Prøv at skifte til en anden DNS-udbyder
  - lokale IPv6-problemer - *mest almindeligt* - typisk er IPv6 aktiveret på værtsystemet, men ikke funktionsdygtigt
  - brug af Privoxy og forkert konfiguration af det
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) anmodninger
- Du kan fejlfinde med DNS `nslookup <domæne.tld fra sporingslogfiler>` og ipv6 med `curl -sv -6 "<url fra sporingslogfiler>"` / al anden forbindelse med `curl -sv -4 "<url fra sporingslogfiler>"`

## Stien er allerede konfigureret til en eksisterende film

![existing-movie.png](/assets/radarr/existing-movie.png)

- Biblioteksimport viser "Eksisterende" eller du får en fejl med "Stien er konfigureret til en eksisterende film"
- Dette sker, når du forsøger at tilføje en film eller redigere en eksisterende films sti, der allerede er tildelt en anden film.
- Sandsynligvis skyldes dette, at du ikke rettede en ikke-matchende film, da du importerede dit bibliotek.
- Find og ret filmen, der allerede er tildelt den pågældende films sti.
  - Filindeks
  - Tabelvisning
  - Indstillinger => Tilføj sti som en kolonne
  - Sorter og find filmen med den bemærkede problematiske sti.
- Alternativt kan du slette filmen med den eksisterende sti fra Radarr

## Hvordan kan jeg omdøbe mine filmmapper?

{#rename-folders}

> Den samme proces gælder også for at flytte/ændre stier til film. Hvis du kun opdaterer stier i Radarr og ikke har brug for at flytte filerne, skal du ikke vælge "Ja, flyt filer" i trin 5.
{.is-info}

1. Film
1. Filmredigering
1. Vælg hvilke film, der skal have ændret deres mappe
1. Skift rodmappen til den samme rodmappe, som filmene i øjeblikket findes i
1. Vælg "Ja, flyt filer"

> Hvis du bruger Plex, vil dette udløse genregistrering af intros, miniaturebilleder, kapitler og forhåndsvisningsmetadata.
{.is-warning}

## Fil- og mappenavngivning for film

- I øjeblikket kræver Radarr, at hver film er i en mappe med formatet, der indeholder mindst `Filmens titel (År)/`, valgfrit er `_` eller `.` gyldige adskiller. For at lette korrekt identifikation af kvalitet og opløsning under import er et filnavn som `Filmens titel (År) [Kvalitet-Opløsning].ext` bedst, igen er `_` eller `.` gyldige adskiller.

  - Et nyttigt værktøj til at foretage disse ændringer i din samling er [filebot](http://www.filebot.net/#download), som har en betalt version i både Apple og Windows-butikkerne, men kan findes gratis på deres legacy [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) site. Det har både en GUI og CLI, så du kan bruge det, du er komfortabel med. For det ovenstående eksempel udvides `{ny}` til `Navn (År)` og `{vf}` giver opløsningen som `1080p`. Der er intet at slutte sig til kvaliteten, så du kan falske det ved hjælp af `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`, som vil navngive alt under 720p til `[DVD-572p]` og større eller lig med 720p som `[Bluray-1080p]`.

- Se [Tips og tricks-sektionen => Opret en mappe til hver film](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) for flere detaljer.

## Mapper til film er navngivet forkert

- Navngivning af filmmappe er baseret på metadataen (navn/år) på det tidspunkt, hvor filmen blev tilføjet. Hvis du har tilføjet en film, før den blev udgivet, skal du muligvis bruge den ovenstående trick til at omdøbe mappen for at afspejle de nye aktuelle data.
- Selvom dine film allerede er i mapper, kan mapperne muligvis ikke være navngivet korrekt. Mappenavnet skal være `Filmens titel (År)`, og det er vigtigt at have titlen og året i mappens navn lige nu.

  - Eksempler, der fungerer godt:
    - `/mnt/Film/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Børnefilm/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Eksempler, der fungerer, men kræver manuel håndtering:
    - Efter bogstaver: `/mnt/Film/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Efter vurdering: `/mnt/Film/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Efter genre: `/mnt/Film/Krimi, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Disse eksempler kræver manuel håndtering, når filmen tilføjes. Hver af eksemplerne vil have mange rodmapper, som f.eks. `A-D` og `E-G` i eksemplet med første bogstav, `R` og `PG-13` i eksemplet med vurdering, og du kan gætte på mangfoldigheden af genre-mapper. Når du tilføjer en ny film, skal den korrekte grundmappe vælges for, at dette format kan fungere.
  - Eksempler, der ikke fungerer:
    - Enkeltmappe: `/mnt/Børnefilm/Frozen (2013) [Bluray-1080p].mkv`
      - På nuværende tidspunkt skal filmene blot være i en mappe, der er opkaldt efter filmen. Der er ingen måde at omgå dette på, før der er udført udviklingsarbejde for at tilføje denne funktion.
    - **Fil**navngivelsesformater fra v0.2, der inkluderer **fil**egenskaber i **filmmappe**navnet som ``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}`` vil ikke fungere i v3.
      - Mapper er relateret til filmen og uafhængige af filen. Derudover vil dette bryde med den planlagte understøttelse af flere filer pr. film.
      - Den anden grund til, at det blev fjernet, var, at det ofte forårsagede forvirring, databasekorruption og generelt kun var halvfærdigt.
  - [Tips og tricks-sektionen => Opret en mappe til hver film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) er en god kilde til at sikre, at din fil- og mappstruktur fungerer godt.

## Kan jeg deaktivere opgaven "Opdater film"?

- Nej, og du bør heller ikke gøre det ved hjælp af SQL-hackery. Opgaven "Opdater film" forespørger den opstrøms Servarr-proxy og kontrollerer, om metadataen for hver film (id'er, rollebesætning, resumé, vurdering, oversættelser, alternative titler osv.) er blevet opdateret i forhold til det, der i øjeblikket er i Radarr. Hvis det er nødvendigt, opdateres de relevante film.
- En almindelig klage er, at opgaven "Opdater" forårsager tung I/O-brug.
- Den vigtigste indstilling er "Genindlæs filmmappe efter opdatering". Hvis dit disk-I/O-brug stiger under en opdatering, kan du ændre genindlæsningsindstillingen til `Manuel`.
  - Skift ikke dette til `Aldrig`, medmindre alle ændringer i dit bibliotek (nye film, opgraderinger, sletninger osv.) udføres gennem Radarr.
  - Hvis du sletter filmfiler manuelt eller via Plex eller et andet tredjepartsprogram, skal du ikke indstille dette til `Aldrig`.
- Den anden indstilling, der kan ændres, er "Analyser videofiler", som anbefales at være aktiveret, hvis du bruger tdarr eller på anden måde eksternt ændrer dine filer. Hvis du ikke gør det, kan du trygt deaktivere "Analyser videofiler" for at reducere noget I/O.

## Hvordan anmoder jeg om en funktion til Radarr?

- Dette er nemt [klik her](https://github.com/Radarr/Radarr/issues)

## Hjælp, min Mac siger, at Radarr ikke kan åbnes, fordi udvikleren ikke kan verificeres

- Dette er enkelt, se venligst dette link for mere information [her](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Udvikler kan ikke verificeres](developer-cannot-be-verified.png "Udvikler kan ikke verificeres")
- Alternativt kan du være nødt til at selvsignere Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Hjælp, min Mac siger, at Radarr.app er beskadiget og kan ikke åbnes

- Det skyldes enten en korrupt download, så prøv igen, eller [sikkerhedsproblemer, se denne relaterede FAQ-indgang.](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Jeg får en fejl: Database disk image is malformed

> \* For Radarr-brugere, der oplever dette efter opgradering til v4.X-versioner. v4-versioner udfører flere vidtrækkende migrationer, fordi hvis din database tidligere havde korruption et hvilket som helst sted (som måske ikke var påviselig tidligere kørende Radarr), vil migrationen mislykkes. Dette vil forhindre Radarr i at starte. Det er sandsynligt, at alle dine sikkerhedskopier også er beskadigede, så det er sandsynligt, at gendannelse af disse ikke vil løse problemet.
> \* Hvis den migrerede database ikke kan åbnes eller ikke kan gendannes, skal du oprette en kopi af databasen fra en nylig sikkerhedskopi og anvende databasens gendannelsesproces på den fil og derefter prøve at starte Radarr med den gendannede sikkerhedskopi. Den skal derefter migrere uden problemer.
{.is-warning}

- **Fejl med `Error creating log database` indikerer problemer med logs.db**
  - Dette kan hurtigt løses ved at omdøbe eller fjerne databasen. Logs-databasen indeholder uvigtige oplysninger om kommandohistorik og opdateringsinstallationshistorik samt Info-, Warn- og Error-poster.
- **Fejl med `Error creating main database` eller generisk `database disk image is malformed` uden angivet database indikerer problemer med radarr.db**
  - Fortsæt med de nedenstående trin
- Dette betyder, at din SQLite-database, der gemmer størstedelen af ​​oplysningerne for Radarr, er beskadiget. Dine muligheder er at prøve (en) sikkerhedskopi(er), prøve at gendanne den eksisterende database, prøve at gendanne sikkerhedskopierne eller hvis alt andet fejler, starte forfra med en frisk ny database.
- Denne fejl kan vises, hvis databasefilen ikke kan skrives af bruger/gruppe, som \*Arr kører som. Tilladelser som årsag vil sandsynligvis kun være et problem for nye installationer, migrerede installationer til en ny server, hvis du for nylig har ændret tilladelserne for din appdata-mappe eller hvis du har ændret brugeren og gruppen, som \*Arr kører som.
- Dit bedste og første mulighed er at [prøve at gendanne fra en sikkerhedskopi](#how-do-i-backuprestore-my-radarr). Men for brugere, der modtager dette efter opgradering til v4, er det meget usandsynligt, at sikkerhedskopien i sig selv vil fungere, og du bliver nødt til at prøve de andre nævnte gendannelsesmetoder.
- Du kan også prøve at gendanne din database. Dette er normalt den eneste mulighed, når dette problem opstår efter en opdatering. Prøv kommandoen [sqlite3 `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Hvis din sqlite ikke har `.recover` eller du ønsker en mere GUI-venlig måde (f.eks. Windows), skal du følge [vores instruktioner på dette wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- En anden mulig årsag til, at du får en fejl med din database, er, at du placerer din database på et netværksdrev (nfs eller smb eller noget andet, der ikke er lokalt). **SQLite er designet til situationer, hvor data og applikation eksisterer på samme maskine.** Derfor skal din \*Arr AppData-mappe (/config-mount til docker) være på lokal lagerplads. [SQLite og netværksdrev fungerer ikke godt sammen og vil på et tidspunkt forårsage en beskadiget database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruger mergerFS, skal du fjerne `direct_io`, da SQLite bruger mmap, som ikke understøttes af `direct_io`, som forklaret i mergerFS [dokumentationen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruger Radarr på en Mac, og den stoppede pludselig med at fungere. Hvad skete der?

- Mest sandsynligt skyldes dette en MacOS-fejl, der forårsagede, at en af ​​databaserne blev beskadiget.
- Se ovenstående indgang om beskadiget database.
- Prøv derefter at starte og se, om det virker. Hvis det ikke virker, har du brug for yderligere support. Indsend i vores [subreddit /r/radarr](http://reddit.com/r/radarr) eller hop på [vores discord](https://radarr.video/discord) for hjælp.

## Hvorfor kan Radarr ikke se mine filer på en fjernserver?

- For alle operativsystemer skal du sikre dig, at den bruger/gruppe, som du kører \*Arr som, har læse- og skriveadgang til det monterede drev.
- For Linux skal du sikre dig:
  - Hvis du bruger en NFS-montering, skal du sikre dig, at `nolock` er aktiveret for din montering.
  - Hvis du bruger en SMB-montering, skal du sikre dig, at `nobrl` er aktiveret for din montering.
- For Windows: Kort sagt kan brugeren, som \*Arr kører som (hvis det er en tjeneste) eller under (hvis det er en bakkeapp), ikke få adgang til filstien på fjernserveren. Dette kan skyldes forskellige årsager, men den mest almindelige er, at \*Arr kører som en tjeneste, hvilket forårsager de beskrevne problemer.

### Radarr kører som standard under LocalService-kontoen, som ikke har adgang til beskyttede fjernfilaktier

- Kør Radarr-tjenesten som en anden bruger, der har adgang til den delte mappe
- Åbn vinduet Administrative værktøjer \> Tjenester på din Windows-server.
- Stop Radarr-tjenesten.
- Åbn dialogboksen Egenskaber \> Logon.
- Skift brugerkontoen for tjenesten til målbrugerkontoen.
- Kør Radarr.exe ved hjælp af mappen Startup
- Du bruger en tildelt netværksdrev (ikke en UNC-sti)

### Skift dine stier til UNC-stier (`\\server\share`)
- Kør Radarr.exe via mappen Startup

## Hvordan skifter jeg fra Windows-tjenesten til en bakkeapp?

1. Luk Radarr ned
1. Kør serviceuninstall.exe, der er i Radarr-mappen
1. Kør `Radarr.exe` som administrator én gang for at give den korrekte tilladelse og åbne firewallen. Når det er færdigt, kan du lukke det og køre det normalt.
1. (Valgfrit) Drop en genvej til .exe i opstartsmappe for at starte automatisk ved opstart.

## Hjælp, jeg har låst mig ude

{#help-i-have-forgotten-my-password}

For at deaktivere godkendelse (for at nulstille dit glemte brugernavn eller adgangskode) skal du redigere `config.xml`, som vil være inde i [Radarr Appdata-mappen](/radarr/appdata-directory)

1. Åbn config.xml i en teksteditor
1. Find linjen med godkendelsesmetoden, der vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Ændr linjen `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Genstart Radarr
1. Radarr vil nu være tilgængelig uden adgangskode, du skal gå til `Indstillinger: Generelt` i brugergrænsefladen og indstille dit brugernavn og adgangskode

## Hvordan stopper jeg browseren fra at åbne ved opstart?

Afhængigt af dit operativsystem er der flere mulige måder.

- I `Indstillinger` => `Generelt` på nogle operativsystemer er der en afkrydsningsboks til at åbne browseren ved opstart.
- Når du starter Radarr, kan du tilføje `-nobrowser` (*nix) eller `/nobrowser` (Windows) til argumenterne.
- Stop Radarr og rediger config.xml-filen, og ændr `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Underlige UI-problemer

- Hvis du oplever mærkelige UI-problemer som f.eks. at bibliotekssiden ikke viser noget eller en visning eller sortering ikke fungerer, skal du prøve at se i en Chrome Inkognitovindue eller Firefox Privat vindue. Hvis det fungerer fint der, skal du rydde din browsers cache og cookies for din specifikke IP/domæne. Se [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) wiki-artiklen for mere information.

## Webgrænsefladen indlæses kun på localhost på Windows

- Hvis du kun kan nå din webgrænseflade på <http://localhost:7878/> eller <http://127.0.0.1:7878/>, skal du køre som administrator mindst én gang.

## Tilladelser

- Radarr skal flytte filer væk fra, hvor downloaderen placerer dem, til den endelige placering, så dette betyder, at den skal kunne læse/skrive både i kilde- og destinationsmappen og filerne.
- På Linux, hvor bedste praksis er, at tjenester kører som deres egen bruger, vil dette sandsynligvis betyde at bruge en delt gruppe og indstille mappe tilladelser til `775` og filer til `664` både i din downloader og \*Arr. I umask-notation vil det være `002`.

## System og logs indlæses uendeligt

- Det er easy-privacy-blocklisten. De blokerer i det væsentlige enhver URL med /api/log? i den. Gennemgå listen og fortæl mig, om du synes, at det at blokere alle URL'er på den liste er en fornuftig idé, der er dusinvis af URL'er deri, der potentielt bryder websteder. Du har valgt det i din adblocker. Den nemme løsning er at tilføje domænet, som Radarr kører på, til whitelisten. Men jeg anbefaler stadig at kontrollere listen.

## Udpak torrenter

- De fleste torrentklienter leveres ikke med automatisk håndtering af komprimerede arkiver som deres usenet-modparter. Vi anbefaler [unpackerr](https://github.com/unpackerr/unpackerr).

## uTorrent fungerer ikke længere

- Sørg for, at webgrænsefladen er aktiveret
- Sørg for, at den alternative lytteport (Avanceret => Webgrænseflade) ikke er den samme som lytteporten (Forbindelser)
- Vi vil foreslå at ændre den alternative lytteport for webgrænsefladen for ikke at påvirke portvideresendelse for forbindelser.

## Jeg fik en pop-up, der sagde, at config.xml var beskadiget, hvad nu?

- Radarr kunne ikke læse din konfigurationsfil ved opstart, da den blev beskadiget på en eller anden måde. For at komme online igen skal du slette `.xml` i din [appdata-mappe](/radarr/appdata-directory), når den er slettet, skal du starte og den vil starte på standardporten (7878), du skal nu konfigurere eventuelle indstillinger, du har konfigureret på siden Generelle indstillinger.

## Ugyldigt certifikat og andre HTTPS- eller SSL-problemer

- Din downloadklient er stoppet med at fungere, og du får en fejl som "Localhost er et ugyldigt certifikat"?
  - Radarr validerer SSL-certifikater. Hvis der ikke er angivet et SSL-certifikat i downloadklienten, eller hvis du bruger et selvsigneret HTTPS-certifikat uden at tilføje CA-certifikatet til din lokale certifikatbutik, vil Radarr nægte at oprette forbindelse. Der findes gratis korrekt underskrevne certifikater fra [let's encrypt](https://letsencrypt.org/).
  - Hvis din downloadklient og Radarr kører på samme maskine, er der ingen grund til at bruge HTTPS, så den nemmeste løsning er at deaktivere SSL for forbindelsen. De fleste vil være enige i, at det heller ikke er nødvendigt i et lokalt netværk. Det er muligt at deaktivere validering af certifikater i avancerede indstillinger, hvis du ønsker at beholde en usikker SSL-konfiguration.

## VPN'er, Jackett og \*ARRs

- Medmindre du befinder dig i et undertrykkende land som Kina, Australien eller Sydafrika, er din torrentklient typisk det eneste, der skal være bag en VPN. Da VPN-endepunktet deles af mange brugere, kan du opleve begrænsning af hastigheden, beskyttelse mod DDOS-angreb og IP-blokeringer fra forskellige tjenester, som hver software bruger.
- Med andre ord kan det at placere \*ARRs (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bag en VPN gøre applikationerne ubrugelige i nogle tilfælde, fordi tjenesterne ikke er tilgængelige.

> **For at være klar, handler det ikke om, hvorvidt VPN'er vil forårsage problemer med \*ARRs, men hvornår: billedudbydere vil blokere dig, og cloudflare er foran de fleste \*ARR-servere (opdateringer, metadata osv.) og kan også blokere dig**
{.is-warning}

- **Mange private trackere vil udelukke dig, hvis du bruger eller får adgang til dem (f.eks. ved hjælp af Jackett eller Prowlarr) via en VPN.**

### Brug af en VPN

- Hvis en VPN er påkrævet, og Docker bruges, anbefales det at bruge Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er påkrævet, og Docker ikke bruges, skal din VPN-klient ***understøtte split tunneling, så kun de nødvendige (Download Client) apps er bag VPN'en.
- Mange problemer med at få adgang til trackere kan løses ved at bruge Googles eller Cloudflares DNS-servere i stedet for din internetudbyders DNS-servere.
- I nogle tilfælde (f.eks. britiske internetudbydere) kan du være nødt til at placere din torrent-downloadklient bag en VPN og Jackett/Prowlarr som følger:
  - Placer Jackett bag VPN'en og sørg for, at split tunneling tillader lokal adgang.
  - For Prowlarr skal du konfigurere din VPN-klient til at levere en proxy og tilføje proxyen i Indstillinger => Indexers. Giv proxyen en tag, og tildel den samme tag til eventuelle indexers, der skal bruge den.
    - Hvis det absolut er nødvendigt, og hvis din VPN ikke giver en måde at oprette en proxy på, kan du placere Prowlarr bag VPN'en og sørge for, at split tunneling tillader lokal adgang.

# Radarr Søgning og Download Almindelige Problemer

## Hvorfor kan jeg ikke tilføje en ny film til Radarr?

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarr bruger [The Movie Database (TMDb)](http://themoviedb.org) til filmoplysninger og billeder som fanart, bannere og baggrunde. Generelt er der nogle grunde til, at du måske ikke kan tilføje en film:
  - TMDb kan ikke lide, at der bruges specialtegn, når der søges efter film via API'en (som Radarr bruger), så prøv at søge efter et oversat navn og/eller uden specialtegn.
  - Du kan også tilføje ved hjælp af TMDb ID eller, hvis TMDb har det, IMDb ID
  - Filmen er endnu ikke blevet tilføjet til TMDb, følg deres [guide](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006) for at få den tilføjet.

## Jackett viser flere resultater end ved manuel søgning

- Dette skyldes normalt, at du søger anderledes i Jackett end du gør manuelt. Se vores [fejlfinding artikel](/radarr/troubleshooting) for mere information.

## Hvordan bestemmer Radarr året for en film?

- Radarr får metadata fra [TMDb](https://www.themoviedb.org/)
- Radarr bruger året for den ældste **biografpremiere** og den ældste **premiere** til matchning.
  - Bemærk, at hvis der ikke findes en biografpremiere, vil logikken falde tilbage på den ældste fysiske eller digitale udgivelsesdato.
- Hvis en film mangler en digital, fysisk, biograf- eller premiereudgivelsesdato, skal TMDb opdateres.
- [TMDb's Contribution Bible](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) nævner følgende om deres udgivelsestyper.
  - **Premiere** - En premierevisning kan være en festivalvisning (f.eks. TIFF) eller en premierebegivenhed med skuespillerne og filmholdet i en stor by (f.eks. LA, London, Toronto).
  - **Biograf** - Kan bruges til den oprindelige udgivelse og eventuelle efterfølgende officielle udgivelser. Bruges til bred eller mættet udgivelse. I USA betragtes 600-1.999 skærme som en bred udgivelse, og 2000+ betragtes som en mættet udgivelse.
  - **Biograf (begrænset)** - Begrænset biografudgivelse er en distributionsstrategi, hvor en ny film udgives i et par biografer i et land, typisk i større storbyområder. I USA er antallet af biografer færre end 600.
  - **Fysisk** - Inkluderer alle VHS-, DVD- og Blu-ray-udgivelser.
  - **Digital** - Alle relevante udgivelser kan tilføjes, herunder streamingplatforme, VOD-udlejning eller -køb. Digitale visninger, herunder online filmfestivaler og virtuelle biografudgivelser, tæller også som digitale udgivelser.

## Hvordan håndterer Radarr udenlandske film eller udenlandske titler?

> [TRaSH's Custom Format Language Guide](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kan være nyttig til at hjælpe med at få film på det/den ønskede sprog.{.is-info}

> Fra og med 2023-02-12 vil Radarrs metadata-cache begynde at betragte en films oprindelige sprog som TMDb's talesprog, hvis og kun hvis der kun findes ét talesprog for filmen på TMDb; ellers vil filmens oprindelige TMDb-sprog blive brugt.
{.is-warning}

## ID-søgninger

- **Indexere, der understøtter ID-baserede søgninger** - Søgninger på indexere og trackere, der understøtter ID-baserede søgninger (TMDbId, IMDbId osv.) - såsom mange Usenet-indexere og mange private torrent-trackere - bruger ikke tekstforespørgsler, hvis der returneres resultater for en ID-baseret søgning. Hvis der returneres resultater, vil der ikke falde tilbage til en navn/tekstsøgning. Hvis du mangler resultater fra din indexer, skyldes det, at de har frigivelserne forbundet med den forkerte film-id.
  - Sprog for frigivelsen kan også udledes fra indexerens eller trackernes frigivelsessprog i resultatet, hvis det er angivet, i stedet for at blive analyseret ud fra navnet

## Tekstsøgninger

- **Indexere, der ikke understøtter ID-baserede søgninger eller ID-baserede søgninger uden resultater** - Søgning på vil bruge filmens oprindelige titel, engelske titel og oversatte titel fra de sprog, du har foretrukket i filmens kvalitetsprofil og eventuelle brugerdefinerede formater med scores i kvalitetsprofilen større end nul.
- Parsing (dvs. importering) søger efter et match i alle oversættelser og alternative titler.
  - Sprog for frigivelsen kan også udledes fra indexerens eller trackernes frigivelsessprog i resultatet, hvis det er angivet, i stedet for at blive analyseret ud fra navnet

## Få udenlandske film

- For at få en film på et fremmedsprog skal du indstille filmens kvalitetsprofil til sproget Original (Filmens oprindelige sprog\*), et bestemt sprog for den profil eller `Any` og oprette og score større end 0 brugerdefinerede formater med sprogvilkår for at bestemme, hvilket sprog der skal hentes.
- Bemærk, at dette ikke inkluderer nogen indexer-sprog, der er konfigureret i indexerens indstillinger som `multi`.
  - Bemærk, at fra [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) af Radarr antages det ikke længere, at `multi` inkluderer engelsk
  - Brugerne kan justere deres indstillinger pr. indexer for at definere, hvilket sprog `multi` angiver

## Hvordan håndterer Radarr "multi" i navne?

- Med Radarr v4.1+ antager Radarr, at
`multi` kun er filmens sprog og **IKKE** engelsk som i tidligere versioner.
  - Brugerne kan justere deres indstillinger pr. indexer for at definere, hvilket sprog `multi` angiver
- Bemærk, at `multi`-definitioner kun hjælper til frigivelsesanalyse og ikke til udenlandske titler eller filmsøgninger.

## Hjælp, film tilføjet, men ikke søgt

- Radarr søger ikke *aktivt* efter manglende film automatisk. I stedet foretages der periodiske forespørgsler om nye indlæg til alle indexer, der er konfigureret til RSS. Når en ønsket film eller en film, der ikke opfylder kriterierne, vises på denne liste, bliver den downloadet. Dette betyder, at indtil en film bliver indsendt (eller genindsendt), bliver den ikke downloadet.
- Hvis du tilføjer en film, som du vil have nu, er det bedste valg at markere afkrydsningsfeltet "Start søgning efter manglende film", til venstre for knappen *Tilføj film* (**1**). Du kan også gå til siden for en film, du har tilføjet, og klikke på forstørrelsesglasset "Søg" (**2**) knappen eller bruge Wanted-visningen til at søge efter manglende eller ikke-opfyldte film.

  - Tilføj og søg efter film, når du tilføjer en film
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Søg efter en eksisterende film
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jacketts /all Endpoint

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordel. Alt andet kan potentielt give problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

- **Opdatering 1. januar 2022: Jackett `/all`-endepunktet understøttes ikke længere (dvs. advarsler vil forekomme) fra version 4.0.0.5730 på grund af, at det kun skaber problemer.**

- Jackett /all-endepunktet er praktisk, men det er den eneste fordel. Alt andet kan potentielt give problemer, så det er nu nødvendigt at tilføje hver tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af /all-endepunktet har ingen fordele, kun ulemper:
  - Du mister kontrollen over indstillinger specifikke for indexer (kategorier, søgemetoder osv.)
  - Blanding af søgemetoder (IMDB, forespørgsel osv.) kan give resultater af lav kvalitet
  - Indekserspecifikke kategorier (\>= 100000) kan ikke bruges.
  - Langsomme indexere vil sænke den samlede resultat
  - Det samlede antal resultater er begrænset til 1000
  - Hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

### Jackett /All-løsninger

- Tilføj hver tracker i Jackett manuelt som en indexer i \*Arr
- Se [Prowlarr](/prowlarr), som kan synkronisere indexere med \*Arr og er udviklet af Lidarr/Radarr/Readarr-udviklingsteamet.
- Se [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indexere med \*Arr. Men brug ikke deres enkeltstående aggregat-endepunkt og brug `multi`, hvis synkroniseringen skal bruges.

## Hvorfor er der to filer? | Hvorfor er der en fil tilbage i downloads?

Dette er forventet. Med en konfiguration, der understøtter [hardlinks](https://trash-guides.info/hardlinks), vil der ikke blive brugt dobbelt plads. Her er, hvordan Torrent-processen fungerer.

1. Radarr sender en downloadanmodning til din klient og forbinder den med et label eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: film, tv, serier, musik osv.
1. Radarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Denne overvågning sker via din downloadklients API.
1. Færdige filer efterlades på deres oprindelige placering for at give dig mulighed for at seede filen (forhold eller tid kan justeres i downloadklienten eller fra inden for under den specifikke downloadklient). Når filer importeres til din mediemappe, oprettes der en hardlink til filen, hvis det understøttes af din konfiguration, eller filen kopieres, hvis hardlinks ikke understøttes.
1. Hvis indstillingen "Behandling af færdig download - Fjern færdige" er aktiveret i Radarrs indstillinger, vil Radarr slette den oprindelige fil og torrent fra din downloadklient, men kun hvis downloadklienten rapporterer, at seeding er fuldført, og torrenten er stoppet (dvs. sat på pause). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for at få vejledning om, hvordan du konfigurerer din downloadklient optimalt.

> Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din færdige downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din konfiguration ikke understøtter hardlinks, vil der blive kopieret en fil i stedet.
{.is-info}

## Hvorfor virker Radarr ikke bag en omvendt proxy?

- Fra og med v3 er Radarr skiftet til .NET og en ny webserver. For at SignalR kan fungere, knapperne i brugergrænsefladen kan fungere, ændringer i databasen kan tages i brug og andre elementer. Kræves følgende tilføjelse til location-blokken for Radarr:

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- Sørg for, at du **ikke** inkluderer `proxy_set_header Connection "Upgrade";` som foreslået af nginx-dokumentationen. **DETTE VIL IKKE VIRKE**
- [Se dette ASP.NET Core-problem](https://github.com/aspnet/AspNetCore/issues/17081)
- Hvis du bruger en CDN som Cloudflare, skal websockets være aktiveret for at tillade websocket-forbindelser.
- Hvis du oplever uventede omdirigeringer, skal du sikre dig, at din værtsheader videresendes.