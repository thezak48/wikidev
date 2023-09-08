## Kan alle mine filmfiler gemmes i én mappe?

Ja, Radarr giver dig mulighed for at konfigurere en enkelt mappe til opbevaring af alle dine filmfiler. Dette kan gøres ved at følge disse trin:

1. Åbn Radarr-webgrænsefladen og gå til "Indstillinger" > "Mediehåndtering".
2. Rul ned til afsnittet "Filhåndtering".
3. Aktivér indstillingen "Flyt filer".
4. Vælg en mappe, hvor du vil gemme alle dine filmfiler.
5. Klik på "Gem" for at gemme dine ændringer.

Bemærk, at når du har konfigureret en enkelt mappe til opbevaring af dine filmfiler, vil Radarr automatisk flytte filerne til denne mappe, når de er blevet downloadet eller opdateret. Dette kan hjælpe med at organisere dine filer og gøre det nemmere at finde dem.

- Nej, og årsagen er, at Radarr er en forgrening af [Sonarr](/sonarr), hvor hver serie har en mappe. Denne begrænsning er et kendt problem for mange brugere og vil måske blive løst i en fremtidig version. Bemærk, at det ikke er en simpel ændring og faktisk kræver en komplet omskrivning af backenden.
- [GitHub-problemet med brugerdefinerede mapper](https://github.com/Radarr/Radarr/issues/153) dækker teknisk set denne anmodning, men der er ingen garanti for, at alle filmfiler i én mappe vil blive implementeret på det tidspunkt.
- En lille "hack-ish" løsning beskrives nedenfor. Bemærk, at du ikke må udløse en genindlæsning i Radarr, da den ellers vil blive vist som manglende, og uanset hvad vil filmen aldrig blive opgraderet.
  - Brug et brugerdefineret script
    - Scriptet skal udløses ved import
    - Det skal være designet til at flytte filen, når du ønsker det
    - Derefter skal det kalde Radarr API'en og ændre filmen til ikke-overvåget.
- Hvis du vil flytte alle dine film fra én mappe til individuelle mapper, kan du læse artiklen [Tips og tricks-sektionen => Opret en mappe til hver film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

## Kan jeg placere alle mine film i mit bibliotek i én mappe?

- Nej, se ovenfor.

## Hvordan opdaterer jeg Radarr?

- Gå til Indstillinger og derefter fanen Generelt og vis avancerede indstillinger (brug knappen ved siden af gem-knappen).

1. Under afsnittet Opdateringer skal du ændre grennavnet til `master` eller `develop`.
1. Gem

*Dette vil ikke installere biterne fra den gren med det samme, det vil ske under den næste opdatering.*

- ![Nuværende Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Den er blevet testet af brugere på udviklings- og nightly-grenene, og der er ikke kendt nogen større problemer. Denne version vil modtage opdateringer cirka en gang om måneden. På GitHub er dette `master`-grenen.

- ![Nuværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Beta): Dette er kanten til testning. Udgivet efter testning i nightly for at sikre, at der ikke er umiddelbare problemer. Nye funktioner og fejlrettelser udgives først her efter nightly. Den kan betragtes som halvstabil, men er stadig `beta`. Denne version vil modtage opdateringer enten ugentligt eller hver anden uge afhængigt af udviklingen.

> **Advarsel: Du kan muligvis ikke skifte tilbage til `master` efter at have skiftet til denne gren.** På GitHub er dette et øjebliksbillede af `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- ![Nuværende Nightly/Ustabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alpha/Ustabil): Dette er den nyeste version. Den udgives, så snart koden er indsendt og består alle automatiserede tests. Denne version er muligvis ikke blevet brugt af os eller andre brugere endnu. Der er ingen garanti for, at den vil køre i visse tilfælde. Denne gren anbefales kun til avancerede brugere. Der forventes problemer og egen undersøgelse i denne gren. ***Brug denne gren kun, hvis du ved, hvad du laver, og er villig til at tage fat for at rette en mislykket opdatering.*** Denne version opdateres øjeblikkeligt.

> **Advarsel: Du kan muligvis ikke skifte tilbage til `master` efter at have skiftet til denne gren.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Bemærk: Hvis du har installeret via Docker, skal du tilføje `:release`, `:latest`, `:testing` eller `:develop` til slutningen af din container-tag afhængigt af, hvem der laver dine bygninger.

|                                                                    | ![Nuværende Master/Seneste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Nuværende Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Nuværende Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kan jeg opdatere Radarr inde i min Docker-container?

- *Teknisk set ja.* **Men du bør absolut ikke gøre det.** Det er en grundlæggende filosofi i Docker. Der kan opstå databaseproblemer, hvis du opgraderer din installation inden i den nyeste `nightly`, men derefter opdaterer Docker-containeren selv (muligvis nedgraderer til en ældre version).

### Installation af en nyere version

#### Lokal installation

1. Gå til System og derefter fanen Opdateringer
1. Nyere versioner, der endnu ikke er installeret, vil have en opdateringsknap ved siden af dem. Klik på den knap for at installere opdateringen.

#### Docker

1. Træk din tag igen og opdater din container

## Kan jeg skifte fra `nightly` tilbage til `develop`?

## Kan jeg skifte mellem grenene?

- Hvis versionen er identisk, kan du skifte, ellers skal du kontakte udviklingsteamet for at se, om du kan skifte fra `nightly` til `master`; `nightly` til `develop`; eller `develop` til `master` for din specifikke bygning.
- Hvis du ikke følger disse instruktioner, kan din Radarr blive ubrugelig eller kaste fejl. Du er blevet advaret. Hvis du støder på fejlmeddelelserne nedenfor, bruger du en nyere database med en ældre \*Arr-version, som ikke understøttes. Opgrader \*Arr til den version, du tidligere brugte, eller en nyere.
  - Eksempel på fejlmeddelelser:
    - `Fejl ved analyse af kolonne 45 (Language=31 - Int64)`
    - `DataMapper kunne ikke indlæse følgende felt: 'Languages' værdi`
    - `ID svarer ikke til et kendt sprog Parameter navn: id`
    - Andre lignende databasefejl om manglende kolonner eller tabeller.

## Hvordan sikkerhedskopierer/gendanner jeg Radarr?

### Sikkerhedskopiering af Radarr

#### Brug af indbygget sikkerhedskopiering

- Gå til System => Sikkerhedskopier i Radarr-brugergrænsefladen
- Klik på Sikkerhedskopier-knappen
- Download zip-filen efter sikkerhedskopieringen er oprettet for at gemme den sikkert

#### Brug af filsystemet direkte

- Find placeringen af AppData-mappen for Radarr
  - Gå til System => Om i Radarr-brugergrænsefladen
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
  - Kør Radarr én gang og gå til System => Om i brugergrænsefladen
  - [Radarr Appdata-mappen](/radarr/appdata-directory)
- Stop Radarr
- Slet indholdet af AppData-mappen **(Inklusive .db-wal/.db-journal-filerne, hvis de findes)**
- Gendan fra din sikkerhedskopi
- Start Radarr
- Hvis stierne er de samme, vil alt fortsætte, hvor det slap

#### Gendannelse af filsystem på Synology NAS

> FORSIGTIG: Gendannelse på en Synology kræver kendskab til Linux og Root SSH-adgang til Synology-enheden.
{.is-warning}

- Geninstaller Radarr (hvis relevant / ikke allerede installeret)
- Find placeringen af AppData-mappen for Radarr
  - Kør Radarr én gang og gå til System => Om i brugergrænsefladen
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
  - forkert konfiguration eller brug af en VPN
  - forkert konfiguration eller brug af en proxy
  - lokale DNS-problemer - Prøv at skifte til en anden DNS-udbyder
  - lokale IPv6-problemer - *mest almindeligt* - typisk er IPv6 aktiveret på værtsystemet, men fungerer ikke
  - brug af Privoxy og forkert konfiguration af det
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) (begrænsning af hastigheden) af anmodninger
- Du kan fejlfinde med DNS `nslookup <domæne.tld fra sporingslogfiler>` og IPv6 med `curl -sv -6 "<url fra sporingslogfiler>"` / alle andre forbindelser med `curl -sv -4 "<url fra sporingslogfiler>"`

## Stien er allerede konfigureret til en eksisterende film

![existing-movie.png](/assets/radarr/existing-movie.png)

- Biblioteksimport viser "Eksisterende" eller du får en fejlmeddelelse om, at "Stien er konfigureret til en eksisterende film".
- Dette sker, når du forsøger at tilføje en film eller redigere en eksisterende films sti, der allerede er tildelt en anden film.
- Sandsynligvis skyldes dette, at du ikke rettede en ikke-matchende film, da du importerede dit bibliotek.
- Find og ret filmen, der allerede er tildelt den pågældende films sti.
  - Filindeks
  - Tabelvisning
  - Indstillinger => Tilføj sti som en kolonne
  - Sorter og find filmen med den nævnte problematiske sti.
- Alternativt kan du slette filmen med den eksisterende sti fra Radarr

## Hvordan kan jeg omdøbe mine filmmapper?

{#rename-folders}

> Den samme proces gælder også for at flytte/ændre stier til film. Hvis du kun opdaterer stier i Radarr og ikke har brug for at flytte filerne, skal du ikke vælge "Ja, flyt filer" i trin 5.
{.is-info}

1. Film
1. Filmredigering
1. Vælg hvilke film, der skal have ændret deres mappe
1. Skift rodmappen til den samme rodmappe, som filmene i øjeblikket eksisterer i
1. Vælg "Ja, flyt filer"

> Hvis du bruger Plex, vil dette udløse genregistrering af introduktioner, miniaturebilleder, kapitler og forhåndsvisningsmetadata.
{.is-warning}

## Fil- og mappenavngivning for film

- I øjeblikket kræver Radarr, at hver film er i en mappe med formatet, der indeholder mindst `Filmens titel (År)/`, valgfrit er `_` eller `.` gyldige adskiller. For at lette korrekt identifikation af kvalitet og opløsning under import er et filnavn som `Filmens titel (År) [Kvalitet-Opløsning].ext` bedst, igen er `_` eller `.` gyldige adskiller.

  - Et nyttigt værktøj til at foretage disse ændringer i din samling er [filebot](http://www.filebot.net/#download), som har en betalt version i både Apple og Windows-butikkerne, men kan findes gratis på deres legacy [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) site. Det har både en GUI og CLI, så du kan bruge det, du er komfortabel med. For det ovenstående eksempel udvides `{ny}` til `Navn (År)` og `{vf}` giver opløsningen som `1080p`. Der er intet at slutte sig til kvaliteten, så du kan forfalske det ved hjælp af `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`, som vil navngive alt lavere end 720p til `[DVD-572p]` og større eller lig med 720p som `[Bluray-1080p]`.

- Se [Tips og tricks-sektionen => Opret en mappe til hver film](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) for flere detaljer.

## Filmmapper navngivet forkert

- Navngivning af filmmappe er baseret på metadataen (navn/år) på det tidspunkt, hvor filmen blev tilføjet. Hvis du har tilføjet en film, før den blev udgivet, skal du muligvis bruge den ovenstående trick til at omdøbe mappen for at afspejle de nye aktuelle data.
- Selvom dine film allerede er i mapper, kan mapperne muligvis ikke være navngivet korrekt. Mappenavnet skal være `Filmens titel (År)`, og det er afgørende at have titlen og året i mappens navn lige nu.

  - Eksempler, der fungerer godt:
    - `/mnt/Film/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Børnefilm/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Eksempler, der fungerer, men kræver manuel håndtering:
    - Efter bogstaver: `/mnt/Film/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Efter vurdering: `/mnt/Film/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Efter genre: `/mnt/Film/Krimi, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Disse eksempler kræver manuel håndtering, når filmen tilføjes. Hver af eksemplerne vil have mange rodmapper, som f.eks. `A-D` og `E-G` i det første bogstaveksempel, `R` og `PG-13` i vurderingseksemplet, og du kan gætte mangfoldigheden af genre-mapper. Når du tilføjer en ny film, skal den korrekte grundmappe vælges for, at dette format kan fungere.
  - Eksempler, der ikke fungerer:
    - Enkeltmappe: `/mnt/Børnefilm/Frozen (2013) [Bluray-1080p].mkv`
      - På nuværende tidspunkt skal filmene simpelthen være i en mappe, der er opkaldt efter filmen. Der er ingen måde at omgå dette på, før der er udført udviklingsarbejde for at tilføje denne funktion.
    - **Film** Mappenavne fra v0.2, der inkluderer **Fil** egenskaber i **filmmappe** navnet som ``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}`` vil ikke fungere i v3.
      - Mapper er relateret til filmen og uafhængige af filen. Derudover vil dette bryde med den planlagte understøttelse af flere filer pr. film.
      - Den anden grund til, at det blev fjernet, var, at det ofte forårsagede forvirring, databasekorruption og generelt kun var halvbagt.
  - [Tips og tricks-sektionen => Opret en mappe til hver film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) er en god kilde til at sikre, at din fil- og mappstruktur fungerer godt.

## Kan jeg deaktivere opgaven "Opdater film"?

- Nej, og du bør heller ikke gøre det gennem nogen SQL-hack. Opgaven "Opdater film" forespørger den opstrøms Servarr-proxy og kontrollerer, om metadataen for hver film (id'er, rollebesætning, resumé, vurdering, oversættelser, alternative titler osv.) er blevet opdateret i forhold til det, der i øjeblikket er i Radarr. Hvis det er nødvendigt, opdateres de relevante film.
- En almindelig klage er, at opgaven "Opdater" forårsager tung I/O-brug.
- Den vigtigste indstilling er "Scan filmmappe efter opdatering". Hvis dit disk-I/O-brug stiger under en opdatering, kan du ændre indstillingen for at scanne manuelt (`Manual`).
  - Skift ikke dette til `Never`, medmindre alle ændringer i dit bibliotek (nye film, opgraderinger, sletninger osv.) udføres gennem Radarr.
  - Hvis du sletter filmfiler manuelt eller via Plex eller et andet tredjepartsprogram, skal du ikke indstille dette til `Never`.
- Den anden indstilling, der kan ændres, er "Analyser videofiler", som anbefales at være aktiveret, hvis du bruger tdarr eller på anden måde eksternt ændrer dine filer. Hvis du ikke gør det, kan du trygt deaktivere "Analyser videofiler" for at reducere noget I/O.

## Hvordan anmoder jeg om en funktion til Radarr?

- Dette er nemt [klik her](https://github.com/Radarr/Radarr/issues)

## Hjælp, min Mac siger, at Radarr ikke kan åbnes, fordi udvikleren ikke kan verificeres

- Dette er enkelt, se venligst dette link for mere information [her](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Udvikler kan ikke verificeres](developer-cannot-be-verified.png "Udvikler kan ikke verificeres")
- Alternativt kan du være nødt til at selvsignere Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Hjælp, min Mac siger, at Radarr.app er beskadiget og kan ikke åbnes

- Det skyldes enten en korrupt download, så prøv igen, eller [sikkerhedsproblemer, se denne relaterede FAQ-indgang.](#help-my-mac-says-radarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Jeg får en fejl: Database disk image is malformed

> \* For Radarr-brugere, der oplever dette efter opgradering til v4.X-versioner. v4-versioner udfører flere vidtrækkende migrationer, fordi hvis din database tidligere havde korruption et hvilket som helst sted (som måske ikke var påviselig tidligere kørende Radarr), vil migrationen fejle. Dette vil forhindre Radarr i at starte. Det er sandsynligt, at alle dine sikkerhedskopier også er beskadigede, så det vil sandsynligvis ikke løse problemet at gendanne dem.
> \* Hvis den postmigrerede database ikke kan åbnes eller ikke kan gendannes, skal du oprette en kopi af databasen fra en nylig sikkerhedskopi og anvende databasens gendannelsesproces på den fil og derefter prøve at starte Radarr med den gendannede sikkerhedskopifil. Den skal derefter migrere uden problemer.
{.is-warning}

- **Fejl med `Error creating log database` indikerer problemer med logs.db**
  - Dette kan hurtigt løses ved at omdøbe eller fjerne databasen. Logs-databasen indeholder uvigtige oplysninger om kommandohistorik og opdateringsinstallationshistorik samt Info-, Warn- og Error-poster.
- **Fejl med `Error creating main database` eller generisk `database disk image is malformed` uden specificeret database indikerer problemer med radarr.db**
  - Fortsæt med de nedenstående trin
- Dette betyder, at din SQLite-database, der gemmer størstedelen af ​​informationen for Radarr, er beskadiget. Dine muligheder er at prøve (en) sikkerhedskopi(er), prøve at gendanne den eksisterende database, prøve at gendanne sikkerhedskopierne eller hvis alt andet fejler, starte forfra med en frisk ny database.
- Denne fejl kan vises, hvis databasefilen ikke kan skrives af bruger/gruppe, som \*Arr kører som. Tilladelser, der er årsagen, vil sandsynligvis kun være et problem for nye installationer, migrerede installationer til en ny server, hvis du for nylig har ændret tilladelserne for din appdata-mappe eller hvis du har ændret brugeren og gruppen, som \*Arr kører som.
- Dit bedste og første mulighed er at [prøve at gendanne fra en sikkerhedskopi](#how-do-i-backuprestore-my-radarr). Men for brugere, der modtager dette efter opgradering til v4, er det meget usandsynligt, at sikkerhedskopien i sig selv vil fungere, og du bliver nødt til at prøve de andre nævnte gendannelsesmetoder.
- Du kan også prøve at gendanne din database. Dette er normalt den eneste mulighed, når dette problem opstår efter en opdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis din sqlite ikke har `.recover` eller du ønsker en mere GUI (f.eks. Windows) venlig måde, skal du følge [vores instruktioner på dette wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- En anden mulig årsag til, at du får en fejl med din database, er, at du placerer din database på et netværksdrev (nfs eller smb eller noget andet, der ikke er lokalt). **SQLite er designet til situationer, hvor data og applikation eksisterer på samme maskine.** Derfor skal din \*Arr AppData-mappe (/config-mount til docker) være på lokal lagring. [SQLite og netværksdrev fungerer ikke godt sammen og vil på et tidspunkt forårsage en beskadiget database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruger mergerFS, skal du fjerne `direct_io`, da SQLite bruger mmap, som ikke understøttes af `direct_io`, som forklaret i mergerFS [dokumentationen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruger Radarr på en Mac, og den stoppede pludselig med at fungere. Hvad skete der?

- Mest sandsynligt skyldes dette en MacOS-fejl, der fik en af ​​databaserne til at blive beskadiget.
- Se ovenstående indgang om beskadiget database.
- Prøv derefter at starte og se, om det virker. Hvis det ikke virker, har du brug for yderligere support. Indsend i vores [subreddit /r/radarr](http://reddit.com/r/radarr) eller hop på [vores discord](https://radarr.video/discord) for hjælp.

## Hvorfor kan Radarr ikke se mine filer på en fjernserver?

- For alle operativsystemer skal du sikre dig, at bruger/gruppe, som du kører \*Arr som, har læse- og skriveadgang til det monterede drev.
- For Linux skal du sikre dig:
  - Hvis du bruger en NFS-montering, skal du sikre dig, at `nolock` er aktiveret for din montering.
  - Hvis du bruger en SMB-montering, skal du sikre dig, at `nobrl` er aktiveret for din montering.
- For Windows: Kort sagt: brugeren, som \*Arr kører som (hvis det er en tjeneste) eller under (hvis det er en bakkeapp), kan ikke få adgang til filstien på fjernserveren. Dette kan skyldes forskellige årsager, men den mest almindelige er, at \*Arr kører som en tjeneste, hvilket forårsager de beskrevne problemer.

### Radarr kører som standard under LocalService-kontoen, som ikke har adgang til beskyttede fjernfiler

- Kør Radarrs tjeneste som en anden bruger, der har adgang til den deling
- Åbn vinduet Administrative værktøjer \> Tjenester på din Windows-server.
- Stop Radarr-tjenesten.
- Åbn dialogboksen Egenskaber \> Logon.
- Skift brugerkontoen for tjenesten til den ønskede brugerkonto.
- Kør Radarr.exe ved hjælp af mappen Startup
- Du bruger en kortlagt netværksdrev (ikke en UNC-sti)

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
1. Find linjen med godkendelsesmetoden, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Skift linjen `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Genstart Radarr
1. Radarr vil nu være tilgængelig uden adgangskode, du skal gå til `Indstillinger: Generelt` i brugergrænsefladen og indstille dit brugernavn og adgangskode

## Hvordan stopper jeg browseren fra at åbne ved opstart?

Afhængigt af dit operativsystem er der flere mulige måder.

- I `Indstillinger` => `Generelt` på nogle operativsystemer er der en afkrydsningsboks til at åbne browseren ved opstart.
- Når du starter Radarr, kan du tilføje `-nobrowser` (*nix) eller `/nobrowser` (Windows) til argumenterne.
- Stop Radarr og rediger config.xml-filen, og ændr `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Underlige UI-problemer

- Hvis du oplever mærkelige UI-problemer som f.eks. at bibliotekssiden ikke viser noget eller en visning eller sortering ikke fungerer, skal du prøve at se i en Chrome Inkognitovindue eller Firefox Privat vindue. Hvis det fungerer fint der, skal du rydde din browsers cache og cookies for din specifikke IP/domæne. Se [Ryd cache, cookies og lokal lagring](/useful-tools#clearing-cookies-and-local-storage) wiki-artiklen for mere information.

## Webgrænsefladen indlæses kun på localhost på Windows

- Hvis du kun kan nå din webgrænseflade på <http://localhost:7878/> eller <http://127.0.0.1:7878/>, skal du køre som administrator mindst én gang.

## Tilladelser

- Radarr skal flytte filer væk fra, hvor downloaderen placerer dem, til den endelige placering, så dette betyder, at den skal læse/skrive både i kilde- og destinationsmappen og filer.
- På Linux, hvor bedste praksis er, at tjenester kører som deres egen bruger, vil dette sandsynligvis betyde at bruge en delt gruppe og indstille mappe tilladelser til `775` og filer til `664` både i din downloader og . I umask-notation vil det være `002`.

## System og logs indlæses for evigt

- Det er easy-privacy blocklist. De blokerer i det væsentlige enhver URL med /api/log? i den. Gennemgå listen og fortæl mig, om du synes, at det er en fornuftig idé at blokere alle URL'er på den liste, der potentielt bryder websteder. Du valgte det i din adblocker. Den nemme løsning er at tilføje domænet, som Radarr kører på, til din whitelist. Men jeg anbefaler stadig at kontrollere listen.

## Udpak torrents

- De fleste torrentklienter leveres ikke med automatisk håndtering af komprimerede arkiver som deres usenet-modparter. Vi anbefaler [unpackerr](https://github.com/unpackerr/unpackerr).

## uTorrent fungerer ikke længere

- Sørg for, at webgrænsefladen er aktiveret
- Sørg for, at den alternative lytteport (Avanceret => Webgrænseflade) ikke er den samme som lytteporten (Forbindelser)
- Vi vil foreslå at ændre den alternative lytteport for webgrænsefladen for ikke at forstyrre portvideresendelse for forbindelser.

## Jeg fik en pop-up, der sagde, at config.xml var beskadiget, hvad nu?

- Radarr kunne ikke læse din konfigurationsfil ved opstart, da den blev beskadiget på en eller anden måde. For at komme online igen skal du slette `.xml` i din [appdata-mappe](/radarr/appdata-directory), når den er slettet, skal du starte og den vil starte på standardporten (7878), du skal nu konfigurere eventuelle indstillinger, du har konfigureret på siden Generelle indstillinger.

## Ugyldigt certifikat og andre HTTPS- eller SSL-problemer

- Din downloadklient er stoppet med at fungere, og du får en fejl som "Localhost er et ugyldigt certifikat"?
  - Radarr validerer SSL-certifikater. Hvis der ikke er angivet et SSL-certifikat i downloadklienten, eller hvis du bruger et selvsigneret HTTPS-certifikat uden CA-certifikatet tilføjet til din lokale certifikatbutik, vil Radarr nægte at oprette forbindelse. Der findes gratis korrekt underskrevne certifikater fra [let's encrypt](https://letsencrypt.org/).
  - Hvis din downloadklient og Radarr kører på samme maskine, er der ingen grund til at bruge HTTPS, så den nemmeste løsning er at deaktivere SSL for forbindelsen. De fleste vil være enige i, at det heller ikke er nødvendigt i et lokalt netværk. Det er muligt at deaktivere validering af certifikater i avancerede indstillinger, hvis du ønsker at beholde en usikker SSL-konfiguration.

## VPN'er, Jackett og \*ARRs

- Medmindre du befinder dig i et undertrykkende land som Kina, Australien eller Sydafrika, er din torrentklient typisk det eneste, der skal være bag en VPN. Da VPN-endepunktet deles af mange brugere, kan du opleve begrænsning af hastigheden, beskyttelse mod DDOS-angreb og IP-blokeringer fra forskellige tjenester, som hver software bruger.
- Med andre ord kan det at placere \*ARRs (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bag en VPN gøre applikationerne ubrugelige i nogle tilfælde, fordi tjenesterne ikke er tilgængelige.

> **For at være klar, det handler ikke om, hvorvidt VPN'er vil forårsage problemer med \*ARRs, men hvornår: billedudbydere vil blokere dig, og cloudflare er foran de fleste \*ARR-servere (opdateringer, metadata osv.) og kan også blokere dig**
{.is-warning}

- **Mange private trackere vil udelukke dig, hvis du bruger eller får adgang til dem (f.eks. ved hjælp af Jackett eller Prowlarr) via en VPN.**

### Brug af en VPN

- Hvis en VPN er påkrævet, og Docker bruges, anbefales det at bruge Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er påkrævet, og Docker ikke bruges, skal din VPN-klient ***understøtte opdeling af tunnel***, så kun de nødvendige (Download Client) apps er bag VPN'en.
- Mange problemer med at få adgang til trackere kan løses ved at bruge Googles eller Cloudflares DNS-servere i stedet for din internetudbyders DNS-servere.
- I nogle tilfælde (f.eks. britiske internetudbydere) kan du være nødt til at placere din torrent-downloadklient bag en VPN og Jackett/Prowlarr som følger:
  - Placer Jackett bag VPN'en og sørg for, at opdeling af tunnel tillader lokal adgang.
  - For Prowlarr skal du konfigurere din VPN-klient til at levere en proxy og tilføje proxyen i Indstillinger => Indexers. Giv proxyen en tag, og tildel den samme tag til eventuelle indexers, der skal bruge den.
    - Hvis det absolut er nødvendigt, og hvis din VPN ikke giver en måde at oprette en proxy på, kan du placere Prowlarr bag VPN'en og sikre, at opdeling af tunnel tillader lokal adgang.

# Radarr Søgning og Download - Almindelige problemer

## Hvorfor kan jeg ikke tilføje en ny film til Radarr?

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarr bruger [The Movie Database (TMDb)](http://themoviedb.org) til filmoplysninger og billeder som fanart, bannere og baggrunde. Generelt er der nogle grunde til, at du måske ikke kan tilføje en film:
  - TMDb kan ikke lide, at der bruges specialtegn, når der søges efter film via API'en (som Radarr bruger), så prøv at søge efter et oversat navn og/eller uden specialtegn.
  - Du kan også tilføje ved hjælp af TMDb ID eller, hvis TMDb har det, IMDb ID.
  - Filmen er endnu ikke blevet tilføjet til TMDb, følg deres [guide](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006) for at få den tilføjet.

## Jackett viser flere resultater end ved manuel søgning

- Dette skyldes normalt, at du søger anderledes i Jackett end du gør manuelt. Se vores [fejlfinding artikel](/radarr/troubleshooting) for mere information.

## Hvordan bestemmer Radarr året for en film?

- Radarr får metadata fra [TMDb](https://www.themoviedb.org/)
- Radarr bruger året for den ældste **Theatrical Release**-dato og den ældste **Premier**-dato til matchning.
  - Bemærk, at hvis der ikke findes en Theatrical Release, vil logikken falde tilbage til den ældste fysiske eller digitale udgivelsesdato.
- Hvis en film mangler en digital, fysisk, teatralsk eller premieredato, skal TMDb opdateres.
- [TMDb's Contribution Bible](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) bemærker følgende om deres udgivelsestyper.
  - **Premiere** - En premierevisning kan tage form af en festivalvisning (f.eks. TIFF) eller en premierebegivenhed med skuespillerne og filmholdet i en stor by (f.eks. LA, London, Toronto).
  - **Theatrical** - Kan bruges til den oprindelige udgivelse og eventuelle efterfølgende officielle udgivelser. Bruges til bred eller mættet udgivelse. I USA betragtes 600-1.999 skærme som en bred udgivelse, og 2000+ betragtes som en mættet udgivelse.
  - **Theatrical (begrænset)** - Begrænset teatralsk udgivelse er en distributionsstrategi for film, hvor en ny film udgives i et par biografer i et land, typisk i større storbyområder. I USA er antallet af biografer færre end 600.
  - **Fysisk** - Inkluderer alle VHS-, DVD- og Blu-ray-udgivelser.
  - **Digital** - Alle relevante udgivelser kan tilføjes, herunder streamingplatforme, VOD-udlejning eller -køb. Digitale visninger, herunder online filmfestivaler og virtuelle biografudgivelser, tæller også som digitale udgivelser.

## Hvordan håndterer Radarr udenlandske film eller udenlandske titler?

> [TRaSH's Custom Format Language Guide](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kan være nyttig til at hjælpe med at få film på det/den ønskede sprog.{.is-info}

> Fra og med 2023-02-12 vil Radarrs metadata-cache begynde at betragte en films oprindelige sprog som TMDb's talesprog, hvis og kun hvis der kun findes ét talesprog for filmen på TMDb; ellers vil filmens oprindelige TMDb-sprog blive brugt.
{.is-warning}

## ID-søgninger

- **Indexere, der understøtter ID-baserede søgninger** - Søgninger på indexere og trackere, der understøtter ID-baserede søgninger (TMDbId, IMDbId osv.) - såsom mange Usenet-indexere og mange private torrent-trackere - tekstforespørgsler bruges ikke, hvis der returneres resultater for en ID-baseret søgning. Hvis der returneres resultater, vil der ikke falde tilbage til en navn/tekstsøgning. Hvis du mangler resultater fra din indexer, skyldes det, at de har frigivelserne forbundet med den forkerte film-id.
  - Sprog for frigivelsen kan også afledes af indexerens eller trackernes frigivelsessprog i resultatet, hvis det er angivet, i stedet for at blive analyseret ud fra navnet.

## Tekstsøgninger

- **Indexere, der ikke understøtter ID-baserede søgninger eller ID-baserede søgninger uden resultater** - Søgning på vil bruge filmens oprindelige titel, engelske titel og oversatte titel fra [de sprog, du har foretrukket i filmens kvalitetsprofil og eventuelle brugerdefinerede formater med score i kvalitetsprofilen større end nul](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Parsing (dvs. importering) søger efter et match i alle oversættelser og alternative titler.
  - Sprog for frigivelsen kan også afledes af indexerens eller trackernes frigivelsessprog i resultatet, hvis det er angivet, i stedet for at blive analyseret ud fra navnet.

## Hentning af udenlandske film

- For at få en film på et fremmedsprog skal du indstille filmens kvalitetsprofil Sprog til Original (Filmens oprindelige sprog\*), et bestemt sprog for den profil eller `Any` og oprette og score større end 0 [Brugerdefinerede formater med sprogvilkår for at bestemme, hvilket sprog der skal hentes - se TRaSH's Guide for detaljer](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Bemærk, at dette ikke inkluderer nogen indexer-sprog, der er konfigureret som `multi` i indexerens indstillinger.
  - Bemærk, at fra [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) antages det ikke længere, at `multi` inkluderer engelsk.
  - Brugere kan justere deres indstillinger pr. indexer for at definere, hvilket sprog `multi` angiver.

## Hvordan håndterer Radarr "multi" i navne?

- Med Radarr v4.1+ antager Radarr, at
`multi` kun er filmens sprog og **IKKE** engelsk som i tidligere versioner.
  - Brugere kan justere deres indstillinger pr. indexer for at definere, hvilket sprog `multi` angiver.
- Bemærk, at `multi`-definitioner kun hjælper til frigivelsesanalyse og ikke til udenlandske titler eller film-søgninger.

## Hjælp, film tilføjet, men ikke søgt

- Radarr søger ikke *aktivt* efter manglende film automatisk. I stedet foretages der periodiske forespørgsler om nye indlæg til alle indexer, der er konfigureret til RSS. Når en ønsket film eller en film, der ikke opfylder cutoff, vises på denne liste, bliver den downloadet. Dette betyder, at indtil en film bliver indsendt (eller genindsendt), bliver den ikke downloadet.
- Hvis du tilføjer en film, som du gerne vil have nu, er det bedste valg at markere afkrydsningsfeltet "Start søgning efter manglende film", til venstre for knappen *Tilføj film* (**1**). Du kan også gå til siden for en film, du har tilføjet, og klikke på forstørrelsesglasset "Søg" (**2**) knappen eller bruge visningen Ønsket for at søge efter manglende eller ikke-opfyldte film.

  - Tilføj og søg efter film, når du tilføjer en film
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Søg efter en eksisterende film
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordel. Alt andet kan give problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

- **Opdatering 1. januar 2022: Jackett `/all`-endepunktet understøttes ikke længere (dvs. advarsler vil forekomme) fra og med 4.0.0.5730 på grund af, at det kun skaber problemer.**

- Jackett /all-endepunktet er praktisk, men det er den eneste fordel. Alt andet kan give problemer, så det er nu nødvendigt at tilføje hver tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af /all-endepunktet har ingen fordele, kun ulemper:
  - Du mister kontrollen over indexer-specifikke indstillinger (kategorier, søgemetoder osv.)
  - Blanding af søgemetoder (IMDB, forespørgsel osv.) kan give resultater af lav kvalitet
  - Indexer-specifikke kategorier (\>= 100000) kan ikke bruges.
  - Langsomme indexere vil sænke den samlede resultat
  - Totalt antal resultater er begrænset til 1000
  - Hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

### Jackett /All-løsninger

- Tilføj hver tracker i Jackett manuelt som en indexer i \*Arr
- Se [Prowlarr](/prowlarr), som kan synkronisere indexere med \*Arr og er udviklet af Lidarr/Radarr/Readarr-udviklingsteamet.
- Se [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indexere med \*Arr. Men brug ikke deres enkeltstående aggregat-endepunkt og brug `multi`, hvis synkroniseringen skal bruges.

## Hvorfor er der to filer? | Hvorfor er der en fil tilbage i downloads?

Dette er forventet. Med en konfiguration, der understøtter [hardlinks](https://trash-guides.info/hardlinks), vil der ikke blive brugt dobbelt plads. Her er, hvordan Torrent-processen fungerer.

1. Radarr sender en downloadanmodning til din klient og forbinder den med et label eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: film, tv, serier, musik osv.
1. Radarr overvåger dine downloadklienters aktive downloads, der bruger det kategorinavn. Denne overvågning sker via din downloadklients API.
1. Færdige filer efterlades på deres oprindelige placering for at tillade, at du deler filen (forhold eller tid kan justeres i downloadklienten eller fra inden for under den specifikke downloadklient). Når filerne importeres til din mediemappe, oprettes der en hardlink til filen, hvis din konfiguration understøtter det, eller filen kopieres, hvis hardlinks ikke understøttes.
1. Hvis indstillingen "Behandling af fuldførte downloads - Fjern fuldførte" er aktiveret i Radarrs indstillinger, vil Radarr slette den oprindelige fil og torrent fra din downloadklient, men kun hvis downloadklienten rapporterer, at seeding er fuldført, og torrenten er stoppet (dvs. sat på pause). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for at få vejledning om, hvordan du konfigurerer din downloadklient optimalt.

> Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din konfiguration ikke understøtter hardlinks, vil der blive kopieret en fil i stedet.
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
- Hvis du oplever uventede omdirigeringer, skal du sikre dig, at dit værtsheader videresendes.