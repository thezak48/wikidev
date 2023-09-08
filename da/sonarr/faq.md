## Hvordan ændrer jeg fra Windows Service til en Tray App?

Hvis du tidligere har installeret Sonarr som en Windows Service og ønsker at ændre den til en Tray App, skal du følge disse trin:

1. Stop Sonarr-service: Åbn en kommandoprompt som administrator og kør kommandoen `net stop Sonarr`.
2. Åbn Sonarr-indstillinger: Højreklik på Sonarr-ikonet i systembakken og vælg "Åbn Sonarr".
3. Gå til fanen "Generelt" i Sonarr-indstillinger.
4. Fjern markeringen af afkrydsningsfeltet "Start ved login" under "Startindstillinger".
5. Klik på "Gem" for at gemme ændringerne.
6. Luk Sonarr.
7. Åbn en kommandoprompt som administrator og naviger til Sonarr-installationsmappen (som standard `C:\ProgramData\Sonarr`).
8. Kør kommandoen `NzbDrone.Console.exe`.
9. Sonarr vil nu starte som en Tray App.

Bemærk, at når Sonarr kører som en Tray App, vil den ikke starte automatisk ved login. Du skal manuelt starte Sonarr ved at åbne programmet fra systembakken.

1. Luk Sonarr ned.
1. Kør serviceuninstall.exe, som findes i Sonarr-mappen.
1. Kør Sonarr.exe som administrator én gang for at give det de rette tilladelser og åbne firewallen. Når det er færdigt, kan du lukke det og køre det normalt.
1. (Valgfrit) Opret en genvej til Sonarr.exe i opstartsmappen for at starte det automatisk ved opstart.

## Hvordan sikkerhedskopierer/gendanner jeg min Sonarr?

### Sikkerhedskopiering af Sonarr

#### Brug af indbygget sikkerhedskopiering

- Gå til System => Backup i Sonarr-brugerfladen.
- Klik på Sikkerhedskopier-knappen.
- Download zip-filen efter at sikkerhedskopieringen er oprettet for at gemme den sikkert.

#### Brug af filsystemet direkte

- Find placeringen af AppData-mappen for Sonarr.
  - Gå til System => Om i Sonarr-brugerfladen.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stop Sonarr - Dette forhindrer, at databasen bliver beskadiget.
- Kopier indholdet til et sikkert sted.

### Gendannelse fra sikkerhedskopiering

> Gendannelse til et operativsystem, der bruger forskellige stier, vil ikke virke (Windows til Linux, Linux til Windows, Windows til OS X eller OS X til Windows). Flytning mellem OS X og Linux kan muligvis fungere, da begge bruger stier med `/` i stedet for `\`, som Windows bruger, men det understøttes ikke. Du skal manuelt redigere alle stier i databasen eller bruge [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Brug af zip-sikkerhedskopiering

- Geninstaller Sonarr (hvis relevant/ikke allerede installeret).
- Kør Sonarr.
- Gå til System => Backup.
- Vælg Gendan sikkerhedskopiering.
- Vælg Vælg fil.
- Vælg din sikkerhedskopierings-zip-fil.
- Vælg Gendan.

#### Brug af sikkerhedskopiering af filsystemet

- Geninstaller Sonarr (hvis relevant/ikke allerede installeret).
- Find placeringen af AppData-mappen for Sonarr.
  - Kør Sonarr én gang og gå til System => Om i brugerfladen.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stop Sonarr.
- Slet indholdet af AppData-mappen **(inklusive .db-wal/.db-journal-filerne, hvis de findes)**.
- Gendan fra din sikkerhedskopi.
- Start Sonarr.
- Hvis stierne er de samme, vil alt fortsætte, hvor det slap.

#### Gendannelse af filsystemet på Synology NAS

> ADVARSEL: Gendannelse på en Synology kræver kendskab til Linux og Root SSH-adgang til Synology-enheden.
{.is-warning}

- Geninstaller Sonarr (hvis relevant/ikke allerede installeret).
- Find placeringen af AppData-mappen for Sonarr.
  - Kør Sonarr én gang og gå til System => Om i brugerfladen.
  - [Sonarr Appdata Directory](/sonarr/appdata-directory)
- Stop Sonarr.
- Opret forbindelse til Synology NAS via SSH og log ind som root.

> På nogle installationer er brugernavnet anderledes end i nedenstående kommandoer: `chown -R sc-Sonarr:Sonarr *` {.is-info}

- Udfør følgende kommandoer:

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- Opdater tilladelserne på filerne:

```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Start Sonarr.

## Hjælp, jeg er blevet låst ude

{#help-i-have-forgotten-my-password}

> Hvis du bruger v4 af Sonarr, er typen `None` for `AuthenticationMethod` ikke længere gyldig - se denne [FAQ](/sonarr/faq-v4) for mere information {.is-info}

Hvis du vil deaktivere godkendelse (for at nulstille dit glemt brugernavn eller adgangskode), skal du redigere `config.xml`, som vil være inde i [Sonarr Appdata Directory](/sonarr/appdata-directory).

1. Åbn config.xml i en teksteditor.
1. Find linjen med godkendelsesmetoden, som vil være
   `<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Ændr linjen med `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Genstart Sonarr.
1. Sonarr vil nu være tilgængelig uden adgangskode. Du bør gå til `Indstillinger: Generelt` i brugerfladen og indstille dit brugernavn og adgangskode.

## Hvorfor er der to filer? \| Hvorfor er der en fil tilbage i downloads?

Dette er forventet. Med en konfiguration, der understøtter [hardlinks](https://trash-guides.info/hardlinks), vil dobbelt diskplads ikke blive brugt. Her er, hvordan Torrent-processen fungerer:

1. Sonarr sender en downloadanmodning til din klient og tilknytter den til et mærke eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten. Eksempler: film, tv, serier, musik osv.
1. Sonarr overvåger dine aktive downloads i downloadklienten, der bruger det kategorinavn. Denne overvågning sker via downloadklientens API.
1. Færdige filer efterlades på deres oprindelige placering, så du kan seede filen (forhold eller tid kan justeres i downloadklienten eller inden for den specifikke downloadklient). Når filerne importeres til din mediemappe, oprettes der en hardlink til filen, hvis det understøttes af din konfiguration, eller filen kopieres, hvis hardlinks ikke understøttes.
1. Hvis indstillingen "Fjern færdige downloads" er aktiveret i Sonarrs indstillinger, vil Sonarr slette den oprindelige fil og torrent fra din downloadklient, men kun hvis downloadklienten rapporterer, at seeding er fuldført, og torrenten er stoppet (dvs. sat på pause). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) for at få vejledning om, hvordan du konfigurerer din downloadklient optimalt.

> Hardlinks er aktiveret som standard. [Et hardlink bruger ikke yderligere diskplads](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/). Filsystemet og monteringerne skal være de samme for din færdige downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlink mislykkes, eller din konfiguration ikke understøtter hardlinks, vil den falde tilbage og kopiere filen.{.is-info}

## Jeg kan se, at funktionen/fejlen X er blevet rettet, hvorfor kan jeg ikke se det?

Sonarr består af to hovedkoder, `main` og `develop`.

- `main` udgives periodisk, når `develop`-grenen er stabil.
- `develop` er til forhåndsudgivelsestest og til brugere, der er villige til at være på forkanten. Når en funktion er markeret som i `develop`, vil den kun være tilgængelig for brugere, der kører `develop`-grenen, når den er flyttet til live (i `main`), er den officielt udgivet.

## Episodestatus - Hvordan beregnes den?

- Der er to dele af episodetællingen, den ene er antallet af episoder (Episode Count), og den anden er antallet af episoder med filer (Episode File Count). Hver del bruger lidt forskellig logik til at give dig den samlede fremgang for en serie eller sæson.

  - Episode Count => Episoden er allerede blevet sendt OG er overvåget ELLER - Episoden har en fil
  - Episode File Count => Episoden har en fil

- Hvis en serie har 10 episoder, der allerede er blevet sendt, og du ikke har nogen filer til dem, vil du have 0/10 episoder. Hvis du fjerner overvågningen af alle episoder i den serie, vil du have 0/0, og hvis du får alle episoderne til den serie, uanset om episoderne er overvåget eller ej, vil du have 10/10 episoder.

## Hvordan får jeg adgang til Sonarr fra en anden computer?

- Som standard lytter Sonarr ikke til anmodninger fra alle systemer (når det ikke køres som administrator), det vil kun lytte på localhost. Dette skyldes, hvordan webserveren, som Sonarr bruger, integreres med Windows (dette gælder også for aktuelle alternativer). Hvis Sonarr køres som administrator, vil det registrere sig korrekt i Windows og åbne firewallporten, så det kan tilgås fra andre systemer på dit netværk. Kørsel som administrator skal kun ske én gang (hvis du ændrer porten, skal det køres igen).

## Hvorfor opdaterer Sonarr seriens oplysninger så ofte?

- Sonarr opdaterer seriens og episoders oplysninger samt scanner disken for filer hvert 12. time. Dette kan virke aggressivt, men det er en meget vigtig proces. Dataopdateringen fra vores TVDb-proxy er vigtig, fordi nye episodeoplysninger synkroniseres ned, luftdatoer, antal episoder, status (fortsætter/afsluttet). Selv shows, der ikke sendes, bliver opdateret med nye oplysninger.
- Diskscanningen er mindre vigtig, men bruges til at kontrollere nye filer, der ikke blev sorteret af Sonarr, og til at registrere slettede filer.
- Den mest tidskrævende del er opdateringen af oplysningerne (hvis diskadgangshastigheden er rimelig), større shows tager længere tid på grund af antallet af episoder, der skal behandles.

> Det er ikke muligt at deaktivere denne opgave. Hvis denne opgave kører længe nok til, at du føler, at det er problemet, er der noget andet, der foregår, som skal løses i stedet for at stoppe denne opgave.
{.is-warning}

## Hvorfor er der et tal ved siden af Aktivitet?

- Dette tal viser antallet af episoder i din downloadklients kø og de sidste 60 elementer i dens historik, der endnu ikke er blevet importeret. Hvis tallet er blåt, fungerer det normalt, og episoderne skal importeres, når de er færdige. Gul betyder, at der er en advarsel på en af episoderne. Rød betyder, at der er opstået en fejl. I tilfælde af gul (advarsel) og rød (fejl) skal du se på køen under Aktivitet for at se, hvad problemet er (hold markøren over ikonet for at få flere detaljer).
- Du skal fjerne elementet fra din downloadklients kø eller historik for at fjerne dem fra Sonarrs kø.

## Hvad er forskellige serietyper?

- Serietype påvirker, hvordan Sonarr søger efter serier. En serietype er baseret på, hvordan serien udgives på indexere og er ikke nødvendigvis den sande 'type' af serien.
- De fleste shows skal være `Standard`. Til daglige shows, der normalt udgives med en dato, skal der bruges `Daily`. Endelig er der anime, hvor `Anime` *normalt* er det rigtige valg, men nogle gange kan `Standard` fungere bedre, så prøv det *andet* valg, hvis du har problemer.
- Bemærk, at hvis serietypen er indstillet til anime, og hvis ingen af dine aktiverede indexere har konfigureret animekategorier, springer den effektivt over indexeren, og det kan se ud som om, den ikke søger.
- Bemærk, at serietypen Anime ikke har nogen begreb om sæsonpakker eller sæsoner og vil forårsage, at hver episode søges individuelt.
- Bemærk, at ikke alle indexere understøtter søgning efter sæson/episode (standard).
- Serietyper kan ændres fra Mass Editor eller fra `Rediger`, når du ser en serie. Bemærk, at serietypen kan vælges ved import.

- Hvis der bruges **Anime** som serietype, er det [muligt også at få din indexer søgt med standardtypen.](/sonarr/settings#indexers)

### Serietyper

- **Anime** - Episoder udgivet med et absolut episodenummer
- **Daily** - Episoder udgivet dagligt eller mindre hyppigt, der bruger år-måned-dag (2017-05-25)
- **Standard** - Episoder udgivet med SxxEyy-mønster

### Eksempler på serietyper

Her er nogle eksempler på udgivelsesnavne for hver serietype. Den specifikke differentierende del er markeret med fed.

> Hvis der bruges **Anime** som serietype, er det [muligt også at få din indexer søgt med standardtypen.](/sonarr/settings#indexers)
{.is-info}

#### Daily

Logs vil vise `Søger indexere efter [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Logs vil vise `Søger indexere efter [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Logs vil vise `Søger indexere efter [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## Hvordan kan jeg omdøbe mine seriemapper?

{#rename-folders}

> Den samme proces gælder også for flytning/ændring af seriestier{.is-info}

Hvis du har justeret dit serienavnformat, efter at Sonarr allerede har oprettet nogle seriemapper, vil Sonarr ikke automatisk omdøbe eksisterende mapper. For at udløse en omdøbning af disse mapper skal følgende trin følges:

1. Serier
1. Mass Editor
1. Vælg de serier, der skal have deres mappe omdøbt
1. Skift rodmappe til den samme rodmappe, som serierne allerede eksisterer i
1. Vælg "Ja, flyt filer" for at få

> Hvis du bruger Plex eller Emby, vil dette udløse genregistrering af intros, miniaturebilleder, kapitler og forhåndsvisningsmetadata.
{.is-warning}

## Hvordan opdaterer jeg Sonarr?

- Gå til Indstillinger og derefter fanen Generelt og vis avancerede indstillinger (brug knappen ved siden af gem-knappen).

1. Under afsnittet Opdateringer skal du ændre grennavnet til `main` eller `develop`.
1. Gem

*Dette installerer ikke øjeblikkeligt bitene fra den gren, det sker under den næste opdatering.*

- main - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Standard/Stabil): Dette er blevet testet af brugere på nightly (`develop`) grenen, og det er ikke kendt for at have nogen større problemer. Denne gren skal bruges af flertallet af brugerne. På GitHub er dette `main` grenen.
- develop - ![Current Develop/Nightly](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Ustabil): Dette er nu det samme som main for brugere uden Docker og sandsynligvis den sidste v3-udgivelse.

> ~~**Advarsel: Du kan muligvis ikke skifte tilbage til `main` efter at have skiftet til denne gren.** På GitHub er dette `develop` grenen.~~
{.is-danger}

- v4 develop - ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alpha/Ustabil): **For brugere uden Docker er grenen `develop` efter installation af v4. For brugere med Docker er dette sandsynligvis mærket `develop`** Dette er det nyeste for Sonarr v4 Beta. Det udgives, så snart koden er blevet indsendt og bestået alle automatiserede tests. Denne version er muligvis ikke blevet brugt af os eller andre brugere endnu. Der er ingen garanti for, at den overhovedet vil køre i nogle tilfælde. Denne gren anbefales kun til avancerede brugere. Der forventes problemer og egen fejlsøgning i denne gren. På GitHub er dette `develop` grenen.

> **Advarsel: Du kan ikke skifte tilbage til (v3) `main` eller (v3) `develop` efter at have skiftet til v4-grenen uden at geninstallere og finde en v3-sikkerhedskopi.** På GitHub er dette `develop` grenen.
{.is-danger}

> v3 **non-docker**-installationer kan **ikke** opgraderes direkte til v4 og kræver installation af Sonarr v4
{.is-info}

- Bemærk: Hvis din installation er via Docker, skal du tilføje `:release`, `:latest`, `:nightly` eller `:develop` til slutningen af din container-tag afhængigt af, hvem der laver dine builds.

|                                                                    | `main` (stabil) ![Current Main/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (beta) ![Current v3 Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 beta) ![Current v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### Installation af en nyere version

#### Native

1. Gå til System og derefter fanen Opdateringer
1. Nyere versioner, der endnu ikke er installeret, vil have en opdateringsknap ved siden af dem. Klik på denne knap for at installere opdateringen.

> v3 kan ikke opdateres til beta v4 og kræver manuel installation. Se [v4 Beta-annoncering](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)
{.is-info}

#### Docker

1. Træk dit tag igen og opdater din container

## Kan jeg skifte fra `develop` tilbage til `main`?

- Se indgangen nedenfor

## Kan jeg skifte mellem grene?

> Du kan (næsten altid) øge din risiko.{.is-info}

- `main` kan skifte til `develop`
- Se nedenfor eller tjek med udviklingsteamet for at se, om du kan skifte fra `develop` til `main` for din specifikke build.
- Hvis du ikke følger disse instruktioner, kan det resultere i, at din Sonarr bliver ubrugelig eller kaster fejl. Du er blevet advaret. Hvis følgende fejl opstår, bruger du en nyere database med en ældre \*Arr-version, som ikke understøttes. Opgrader \*Arr til den version, du tidligere brugte, eller en nyere.
  - Eksempel på fejlmeddelelser:
    - `Fejl ved analyse af kolonne 45 (Language=31 - Int64)`
    - `DataMapper kunne ikke indlæse følgende felt: 'Languages' værdi`
    - `ID matcher ikke et kendt sprog Parameter name: id`
    - Andre lignende databasefejl om manglende kolonner eller tabeller.
- **Opdatering 7. august 2022**
  - `3.0.9.1549` er blevet udgivet som main/stabil
  - Hvis du er på develop og stadig er på `3.0.9.1549` eller lavere, kan du sikkert nedgradere til main
  - Hvis du er på en nyere version, *kan du være fanget* på nightly/develop, indtil en ny stabil udgivelse sker. Hvis du har en sikkerhedskopi fra før opgraderingen over den ovennævnte version, kan du geninstallere og gendanne sikkerhedskopien. Tjek med udviklingsteamet for at se, om du sikkert kan nedgradere.

# Sonarr og serier - problemer + metadata

## Hvordan håndterer Sonarr nummereringsproblemer med scener (American Dad!, osv.)?

### Sådan håndterer Sonarr nummereringsproblemer med scener

- Sonarr er afhængig af [TheXEM](http://thexem.info/), en fællesskabsdrevet hjemmeside, der giver brugerne mulighed for at oprette kortlægninger af shows, som scenerne (dem der uploader filerne) og TheTVDb (som typisk følger netværkets nummerering) er uenige om. Der er allerede en række shows derinde, men det er nemt at tilføje et nyt, og ændringerne accepteres normalt inden for et par dage (hvis de er korrekte). TheXEM bruges til at rette forskelle i episodenummerering (uoverensstemmelse om, hvorvidt en episode er en special eller ej) samt forskelle i sæsonnumre, f.eks. episoder, der udgives som S10E01, men TheTVDb angiver den samme episode som S2017E01.
- XEM retter typisk problemerne, når udgivelsesgruppernes (kendt som 'scenen') nummerering ikke stemmer overens med TVDb-nummereringen, så Sonarr ikke fungerer. Her kommer [XEM](http://thexem.info) ind i billedet, som opretter et kort, som Sonarr kan kigge på.
- Udgivelser har dobbeltepisoder i en enkelt fil, da det er sådan, de bliver sendt, men TVDb markerer hver episode individuelt.
- Udgivelsesgrupper bruger et år for sæsonen S2010, og TVDb bruger S01.
- [XEM](http://thexem.info) fungerer i de fleste tilfælde og holder det kørende gnidningsløst uden, at du nogensinde bemærker det. Men som med de fleste ting vil der altid være *problematisk undtagelser*, og i dette tilfælde er der en liste over dem.

> Visse indexere eller udgivelsesgrupper kan følge TVDb i stedet for `Scene` (dvs. XEM).
> Hvis dette observeres, bedes du indsende dem via scenekortlægningsformularen.
{.is-info}

- [Anmodede kortlægninger af tjenester *Gennemgå og sørg for, at aliaset og udgivelsen ikke allerede er anmodet eller tilføjet*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Formular til anmodning om kortlægning af tjenester *Lav en ny anmodning om et alias. Sørg for at udfylde formularen fuldt ud*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### Problematisk shows

> Dette er på ingen måde en udtømmende liste over shows, der har kendte problemer med kortlægning af scener; dog er disse nogle almindelige.
{.is-info}

- Dette er en ufuldstændig liste over de kendte shows og hvordan/hvorfor de er problematiske:  
- American Dad {#problemshow-americandad}
  - På grund af ændringer i sæsonen på netværket er American Dad typisk en sæson bagud mellem udgivelser og TVDb. Se XEM-kortet for detaljer
  - [American Dad](https://thexem.info/xem/show/4948) er i øjeblikket på S19 baseret på TVDb eller S18 baseret på Scene på tidspunktet for denne skrivning. Så hvis du søger i Sonarr efter sæson 19, vil du **kun** få resultater fra sæson 18 på grund af XEM-kortet.
  - Hvis du har en indexer/udgivelsesgruppe med sæson 19-episoder, bedes du indsende dem via scenekortlægningsformularen og sikre dig, at de ikke allerede er anmodet
    - [Anmodede kortlægninger af tjenester *Gennemgå og sørg for, at aliaset og udgivelsen ikke allerede er anmodet eller tilføjet*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Formular til anmodning om kortlægning af tjenester *Lav en ny anmodning om et alias. Sørg for at udfylde formularen fuldt ud*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - Dobbelt episodefiler i forhold til enkeltstående episoder på TVDb, men ikke alle episoder er dobbelte, så kortet kan blive tilføjet forkert og pege på, hvilke der er enkeltstående og hvilke der er dobbelte
- Pokémon {#problemshow-pokemon}
  - På TheXem tracker [Pokemon](http://thexem.info/xem/show/4638) *dubbede* episoder. Så hvis du vil have underteksterede episoder, er du måske ude af held. Hvis visse udgivelsesgrupper følger TVDb og ikke XEM-kortlægning, bedes du indsende dem via scenekortlægningsformularen og sikre dig, at de ikke allerede er anmodet
    - [Anmodede kortlægninger af tjenester *Gennemgå og sørg for, at aliaset og udgivelsen ikke allerede er anmodet eller tilføjet*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Formular til anmodning om kortlægning af tjenester *Lav en ny anmodning om et alias. Sørg for at udfylde formularen fuldt ud*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb har den oprindelige udsendelsesrækkefølge fra det spanske netværk, men Netflix købte rettighederne og klippede serien om til et andet antal episoder. Dette får "sæson 5" til at blive importeret over eksisterende "sæson 3"-episoder. [Yderligere information kan findes i denne Reddit-tråd](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- Kamen Rider {#problemshow-kamenrider}
  - Antologien (TVDb ID 74096) skal bruges i Sonarr til automatisering, da denne serie har både en antologientry (der samler alle sæsoner) og de individuelle sæsoner, der er opført som separate entries på TVDb. På grund af at antologientryet har individuelle sæsonnavneafbildninger på [TheXEM](https://thexem.info/xem/show/5376), er det ikke muligt at tilføje de individuelle sæsonentries til Sonarr uden at downloade og importere udgivelser manuelt.
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - Den nyeste sæson af Bleach: Thousand-Year Blood War bliver udgivet med forskellige navngivningsskemaer, hvilket gør det svært at automatisere og potentielt overskrive nogle af dine eksisterende episoder. Det kan kun automatiseres, hvis din udgivelsesgruppe enten:
    - Udgiver episoderne som S17Exx-nummerering, eller
    - Udgiver dem med det korrekte sæson 2-serietitel (findes her <https://thexem.info/xem/show/5476>) og har startet denne nye bue ved absolut episodenummer 1.
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys blev først sendt som 20 mindre episoder, men blev senere genudsendt som 10 lange episoder. Disse længere kombinerede episoder blev tilføjet som specialafsnit og skal navngives derefter. (S00E01 osv., ...)
- Horizon {#problemshow-horizon}
  - Et show, der sporadisk sender episoder siden 1964. Dette gør kortlægning særligt vanskelig, som du kan se på [TheXEM](https://thexem.info/xem/show/5495). De interesserede kan finde den oprindelige diskussion på Sonarr-discorden [her](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312).
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023) blev udgivet på Netflix som en ikke-lineær serie, hvilket betyder, at hver bruger fik en forskellig rækkefølge, når de så serien. Dette skaber et problem for Sonarr, da udgivelsesgrupper har forskellige episoderækkefølger for showet. For at forhindre forkert kortlægning af episoder vil Sonarr ikke automatisk hente episoder, og du bliver nødt til at hente og importere episoderne manuelt. Du kan matche dem baseret på episodetitel eller ved at se de første få sekunder og se, om episoden 'farve' matcher titlen.

Nogle eksempler på andre shows, der ofte har problemer, hvoraf de fleste kan løses ved hjælp af TheXEM-mapping, er: Arrested Development, Kitchen Nightmares (US), Mythbusters, Pawn Stars.

## Hvorfor kan Sonarr ikke importere episodefiler til serie X? / Hvorfor kan Sonarr ikke finde udgivelser til serie X?

Der kan være flere grunde til, at Sonarr ikke kan finde eller importere episoder til en bestemt serie.

> Sonarr bruger ikke aliaser eller oversættelser (f.eks. titler på fremmedsprog) fra TVDb.
{.is-warning}

> **For indexere, der understøtter søgninger baseret på ID**, bruges seriens TVDbID eller IMDbID til søgning. Serietitler og eventuelle aliaser bruges kun, hvis søgninger baseret på ID ikke giver resultater.
{.is-info}

- Sonarr er afhængig af at kunne matche titler, ofte bruger uploadere forskellige titler til episoder, f.eks. bliver `CSI: Crime Scene Investigation` bare postet som `CSI`, så Sonarr kan ikke matche navnene uden lidt hjælp. Disse håndteres af Scene Mapping, som Sonarr-teamet vedligeholder.
- Du kan også gennemgå [FAQ-indgangen for problematiske shows og nummereringsproblemer mellem releasegrupper og TVDb](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

> **For alle japanske anime skal der tilføjes aliaser til [thexem.info](https://thexem.info)**, for andre serier for at anmode om en ny mapping, se trinnene nedenfor. Yderligere oplysninger kan findes hos nogle af XEM-folkene, der hænger ud i #XEM-discord-kanalen på Sonarr Discord.
{.is-danger}

- [Anmodede mappingtjenester *Gennemgå og sørg for, at aliaset og udgivelsen ikke allerede er anmodet eller tilføjet*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Tjenester Scene Mapping-anmodningsformular *Opret en ny anmodning om et alias. Sørg for, at formularen er udfyldt fuldt ud*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> Typisk tilføjes Services-anmodninger inden for 1-5 dage
{.is-info}

> Anmod ikke om en mapping til japanske anime; brug XEM til det.
> Yderligere oplysninger kan findes hos nogle af XEM-folkene, der hænger ud i [\#XEM-discord-kanalen på Sonarr Discord](https://discord.gg/Z3D6u5hBJb)
{.is-danger}

> Hvis en ikke-japansk serie kræver sæsonmappning (f.eks. udgivet som S25E26, men TVDB er S26E2, så kræves der en XEM-mapping. Dette kan ikke gøres med Services-mapping.
{.is-info}

> Serien "Helt Perfekt" med TVDb-id'er `343189` og `252077` er svær at automatisere på grund af, at TVDb har det samme navn for begge shows, hvilket overtræder TVDb's egne regler. Den første indgang for serien får navnet. Eventuelle fremtidige indgange for serien skal have året som en del af seriens navn. Imidlertid er der tilføjet en sceneundtagelse for at mappe udgivelser (forskel på store og små bogstaver) Helt Perfekt-udgivelser, der indeholder `NORWEGIAN` -\> `252077` og indeholder `SWEDISH` -\> `343189`
{.is-info}

## TVDb er opdateret, hvorfor er Sonarr det ikke?

{#tvdb}

- TVDb har en cache på 24 timer på deres API.
- TVDb's API skal derefter udfylde deres CDN-cache, hvilket tager flere timer.
- Sonarr's Skyhook har en meget mindre cache på få timer ud over dette.
- Derudover kører Sonarr kun opgaven "Opdater serier" hver 12. time. Denne opgave kan køres manuelt fra System => Opgaver; "Opdater alle" fra Serier-indekset eller køres manuelt for en bestemt serie på den serie's side.

- Derfor vil det normalt tage mellem 36 og 48 timer (24 + ~3 + ~3 + 12) for en ændring på TVDb at blive automatisk indlæst i Sonarr.
- Hvis en serie eller episoder mangler på TVDb, vil det tage 36 til 48 timer fra det tidspunkt, de er tilføjet, for at de bliver indlæst i din Sonarr-instans.

{#missing-episodes}

- Hvis du ved, at der er foretaget en opdatering på TVDb for mere end 48 timer siden, skal du diskutere det på vores [Discord](https://discord.sonarr.tv/).

## Hvorfor kan jeg ikke tilføje en serie?

{#why-can-i-not-add-a-new-series}

- Hvis TheTVDb ikke er tilgængelig, kan Sonarr ikke få søgeresultater, og du vil ikke kunne tilføje nye serier ved at søge. Du kan muligvis tilføje en ny serie ved hjælp af TVDbID, hvis du ved, hvad det er. Brugergrænsefladen forklarer, hvordan du tilføjer det ved hjælp af en ID.
- Sonarr kan ikke tilføje nogen serier, der ikke har en engelsk titel. Hvis du prøver at tilføje en serie via TVDb ID, der ikke har en engelsk titel. Hvis der ikke findes en engelsk titel for den serie på TheTVDb, skal den tilføjes, og derefter [skal man vente på, at TVDb's cache ryddes](#tvdb).
- Showet skal være en tv-serie og ikke en film. Det skal også eksistere på TVDb. Hvis det er på IMDB, TMDB eller et andet sted, men ikke på TVDb, kan du ikke tilføje showet.
- Serien skal eksistere på TVDb.
- Visse serier kan faktisk betragtes som fortsættelser og sæsoner i deres primære serie.
  - Nogle kendte serier/sæsoner er:
  - [Dexter New Blood var sæson 9](https://thetvdb.com/series/dexter/seasons/official/9), men det er nu [sin egen serie](https://thetvdb.com/series/dexter-new-blood)

## Hvorfor kan jeg ikke tilføje en serie, når jeg kender TVDb ID'et?

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr kan ikke tilføje nogen serier, der ikke har en engelsk titel. Hvis du prøver at tilføje en serie via TVDb ID, der ikke har en engelsk titel, vil serien ikke blive fundet. Hvis der ikke findes en engelsk titel for den serie på TheTVDb, skal den tilføjes (hvis den er tilgængelig).
- Kontroller URL'en / serien - Sonarr understøtter ikke film; brug [Radarr](/radarr) til film

## Titel Slug i brug

- Der er to primære årsager til denne fejl, som er angivet nedenfor.

## Duplikerede navne uden år

- Denne fejl opstår ofte, når to serier har samme navn på TheTVDB. Hvis det er tilfældet, skal det andet show have året tilføjet til seriens titel.
  - Serie A
  - Serie A (2021)
- For at rette dette skal du vente på, at nogen til sidst (måske) opdaterer TVDb eller opdatere TVDb selv. Når det er rettet **og når det er godkendt af TVDb's moderatorer**, på grund af [TVDb's API-problemer](#tvdb-is-updated-why-isnt-sonarr), når det er opdateret, skal du vente 30+ timer, før den rettede titel kan bruges i Sonarr.

## Duplikerede navne med tegnsætning

- Det vil også ske med to serier, der har lignende navne, der kun adskiller sig ved tegnsætning. Hvis det er tilfældet, skal du rapportere dette på [Sonarr Discord](https://discord.sonarr.tv/).
  - Joe's Show (2022)
  - Joes Show (2022)

## Episoden har ikke et absolut nummer

- Episoderne på TVDb har ikke tildelt et absolut nummer. Opdater serien på TVDb, hvis det er nødvendigt, og vent derefter 36-48 timer, indtil opdateringen rydder TVDb's interne cache og indlæses i Sonarr

## Episode Air Times

- Inden for Sonarr er episodernes luftdato og -tidspunkter, der vises i browseren, baseret på klientens tid/tidszone, alle tidspunkter sendes fra Sonarr til browseren som UTC-tid (ISO-8601 formateret for at være præcis)
- TVDb dikterer - med undtagelse af streamingtjenester - at lufttiden og -datoen er baseret på den primære udsendelsesnetværks lokale tid i landets mest populære by. [Se TVDb's FAQ-indgang for detaljer](https://support.thetvdb.com/kb/faq.php?id=29)
- Episode Air Dates og Air Time på TVDb konverteres til UTC og bruger Sonarr's tidszone, der er kortlagt i Skyhook af Sonarr-teamet for det netværk, TVDb har for serien.
  - I det sjældne tilfælde, hvor et netværk ikke er kortlagt, antages tiden i TVDb at være US EST (UTC-5).
  - Hvis lufttiden ikke synes at stemme overens, når den konverteres fra lufttiden for netværkets lokale tidszone til din browsers tidszone, er det sandsynligt, at netværket skal kortlægges i Skyhook. [Kontakt udviklingsteamet på Discord](https://discord.sonarr.tv/) for support til opdatering af netværkets tidszone.  

# Sonarr Almindelige Problemer

## Stien er allerede konfigureret til en eksisterende serie

- Biblioteksimport viser "Eksisterende" eller du får en fejl med "Stien er konfigureret til en eksisterende serie"
- Dette sker, når du forsøger at tilføje en serie eller redigere en eksisterende series sti, der allerede er tildelt en anden serie.
- Sandsynligvis skyldes dette, at du ikke rettede en ikke-matchende serie, da du importerede dit bibliotek.
- Find og ret filmen, der allerede er tildelt den series sti.
  - Serierindeks
  - Tabelvisning
  - Indstillinger => Tilføj sti som en kolonne
  - Sorter og find filmen på den bemærkede problematiske sti.
- Alternativt kan du slette serien, der bruger den eksisterende sti, fra Sonarr

## System & Logs indlæses for evigt

- Det skyldes easy-privacy blocklist. De blokerer i det væsentlige enhver URL med /api/log? i den. Gennemgå listen og fortæl mig, om du synes, at det er en fornuftig idé at blokere alle URL'er på den liste, der potentielt bryder websteder. Der er dusinvis af URL'er derinde, der potentielt kan bryde websteder. Du valgte det i din adblocker. Den nemmeste løsning er at tilføje domænet, som Sonarr kører på, til undtagelseslisten. Men jeg anbefaler stadig at kontrollere listen.

## Underlige UI-problemer

- Hvis du oplever underlige UI-problemer som f.eks. at bibliotekssiden ikke viser noget eller en bestemt visning eller sortering ikke fungerer, skal du prøve at se det i et Chrome Inkognitovindue eller Firefox Privatvindue. Hvis det fungerer fint der, skal du rydde din browsers cache og cookies for din specifikke IP/domæne. Se den [Ryd Cache Cookies og Lokal Lagring](/useful-tools#clearing-cookies-and-local-storage) wiki-artikel for mere information.

## Webgrænsefladen indlæses kun på localhost på Windows

- Hvis du kun kan nå din webgrænseflade på <http://localhost:8989/> eller <http://127.0.0.1:8989>, skal du køre Sonarr som administrator mindst én gang.

## Jeg fik en pop op-meddelelse, der sagde, at config.xml er beskadiget, hvad nu?

- Sonarr kunne ikke læse din konfigurationsfil ved opstart, da den blev beskadiget på en eller anden måde. For at få Sonarr online igen skal du slette `.xml` i din [AppData-mappe](/sonarr/appdata-directory) og derefter starte Sonarr, og den starter på standardporten (8989). Du skal nu konfigurere eventuelle indstillinger, du har konfigureret på siden Generelle indstillinger.

## Ugyldigt certifikat og andre HTTPS- eller SSL-problemer

- Hvis du ikke bruger Windows, er det mest sandsynligt, at dine mono-certifikater er forældede og skal synkroniseres. [Se afsnittet om mono ssl i installationsartiklen for detaljer](/sonarr/installation#mono-ssl-issues)
- Din downloadklient fungerer ikke længere, og du får en fejl som f.eks. `Localhost er et ugyldigt certifikat`?
  - Sonarr validerer nu SSL-certifikater. Hvis der ikke er indstillet et SSL-certifikat i downloadklienten, eller hvis du bruger et selvsigneret https-certifikat uden at tilføje CA-certifikatet til din lokale certifikatbutik, vil Sonarr nægte at oprette forbindelse. Der findes gratis korrekt underskrevne certifikater fra [let's encrypt](https://letsencrypt.org/).
  - Hvis din downloadklient og Sonarr er på samme maskine, er der ingen grund til at bruge HTTPS, så den nemmeste løsning er at deaktivere SSL for forbindelsen. De fleste vil være enige i, at det heller ikke er nødvendigt i et lokalt netværk. Det er muligt at deaktivere validering af certifikater i avancerede indstillinger, hvis du vil beholde en usikker SSL-konfiguration.

## Hvordan stopper jeg browseren fra at åbne ved opstart?

Afhængigt af dit operativsystem er der flere mulige måder.

- I `Indstillinger` => `Generelt` på nogle operativsystemer er der en afkrydsningsboks til at åbne browseren ved opstart.
- Når du starter Sonarr, kan du tilføje `-nobrowser` (*nix) eller `/nobrowser` (Windows) til argumenterne.
- Stop Sonarr og rediger config.xml-filen, og ændr `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## VPN'er, Jackett og \*ARRs

- Medmindre du er i et undertrykkende land som Kina, Australien eller Sydafrika, er din torrentklient typisk det eneste, der skal være bag en VPN. Fordi VPN-endepunktet deles af mange brugere, kan du opleve hastighedsbegrænsning, DDOS-beskyttelse og IP-blokeringer fra forskellige tjenester, som hver software bruger.
- Med andre ord kan det at sætte \*Arrs (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bag en VPN gøre applikationerne ubrugelige i nogle tilfælde på grund af, at tjenesterne ikke er tilgængelige.

> **For at være klar handler det ikke om, hvorvidt VPN'er vil forårsage problemer med \*Arrs, men hvornår: billedudbydere vil blokere dig, og cloudflare er foran de fleste \*Arr-servere (opdateringer, metadata osv.) og kan også blokere dig**
{.is-warning}

- **Mange private trackere vil udelukke dig for at bruge eller få adgang til dem (dvs. bruge Jackett eller Prowlarr) via en VPN.**

### Brug af en VPN

- Hvis en VPN er påkrævet, og Docker bruges, anbefales det at bruge Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er påkrævet, og Docker ikke bruges, skal din VPN-klient ***understøtte split tunneling, så kun de nødvendige (Download Client) apps er bag VPN'en.
- Mange problemer med at få adgang til trackere kan løses ved at bruge Googles eller Cloudflares DNS-servere i stedet for din internetudbyders DNS-servere.
- I nogle tilfælde (f.eks. britiske internetudbydere) skal du muligvis sætte din torrent-downloadklient bag en VPN og Jackett/Prowlarr som følger:
  - Sæt Jackett bag VPN'en og sørg for, at split tunneling tillader lokal adgang
  - For Prowlarr skal du konfigurere din VPN-klient til at levere en proxy og tilføje proxyen i Indstillinger => Indexers. Giv proxyen en tag, og tildel den samme tag til eventuelle indexere, der skal bruge den.
    - Hvis det absolut er nødvendigt, og hvis din VPN ikke giver en måde at oprette en proxy på, kan du sætte Prowlarr bag VPN'en og sikre, at split tunneling tillader lokal adgang.

## Jeg ser logmeddelelser for shows, som jeg ikke har/ikke ønsker

- Disse meddelelser er helt normale og kommer fra RSS-feeds, som Sonarr tjekker for at se, om der er episoder, du ønsker. Normalt vises disse kun i debug/trace-logning, men i tilfælde af et problem med behandlingen af et element kan du se en advarsel eller fejl. Det er sikkert at ignorere advarsler/fejl, da de er for shows, du ikke ønsker. Hvis det er for et show, du ønsker, skal du åbne en supporttråd på forummet.

## Seeder-torrents slettes ikke automatisk

- Når en torrent, der stadig seedes, importeres, kopieres den eller hardlinkes (hvis det er aktiveret og *muligt*), så torrentklienten kan fortsætte med at seede. I en ideel opsætning vil torrent-downloadmappen og biblioteksmappen være på samme filsystem og *se ud som det* (Docker og netværksdrev gør det nemt at gøre det forkert), hvilket gør hardlinks mulige og minimerer spildt plads.
- Derudover kan du konfigurere dine mål for seedetid/forhold i Sonarr eller din downloadklient, konfigurere din downloadklient til at *pause* eller *stoppe*, når de er opfyldt, og aktivere Fjern under Afsluttede og Mislykkede Downloadhåndtering. På den måde vil torrents, der er færdige med at seede, blive fjernet fra downloadklienten af Sonarr.

## Hjælp, min Mac siger, at Sonarr ikke kan åbnes, fordi udvikleren ikke kan verificeres

- Dette er enkelt, se denne [link](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) for mere information.
[![Udvikler kan ikke verificeres](/assets/general/faq_1_mac.png)]

## Hjælp, min Mac siger, at Sonarr.app er beskadiget og kan ikke åbnes

- Det skyldes enten en korrupt download, så prøv igen, eller [sikkerhedsproblemer, se denne relaterede FAQ-indgang.](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Jeg får en fejl: Database disk image is malformed

> Du kan modtage denne fejl efter opgradering af sqlite3 til 3.41. Sonarr v3.0.9 understøtter ikke sqlite3 3.41 på grund af en breaking default-ændring. [Detaljer om problemet kan findes i Sonarr GHI #5464](https://github.com/Sonarr/Sonarr/issues/5464)
> Dette er løst med Sonarr v3.0.10, og brugerne skal opgradere Sonarr i overensstemmelse hermed.
{.is-warning}

- **Fejl med `Fejl ved oprettelse af logdatabase` indikerer problemer med logs.db**
  - Dette kan hurtigt løses ved at omdøbe eller fjerne databasen. Logdatabasen indeholder uvigtige oplysninger om kommandohistorik og opdateringsinstallationshistorik samt Info-, Warn- og Error-logger.
- **Fejl med `Fejl ved oprettelse af hoveddatabase` eller generisk `database disk image is malformed` uden specificeret database indikerer problemer med sonarr.db**
  - Fortsæt med de nedenstående trin.
- Dette betyder, at din SQLite-database, der gemmer størstedelen af informationen for Sonarr, er beskadiget. Dine muligheder er at prøve at genskabe den eksisterende database, prøve at genskabe sikkerhedskopierne, eller hvis alt andet fejler, starte forfra med en frisk ny database.
- Denne fejl kan vises, hvis databasefilen ikke kan skrives af bruger/gruppe, som \*Arr kører som. Tilladelser kan sandsynligvis kun være et problem for nye installationer, migrerede installationer til en ny server, hvis du for nylig har ændret tilladelserne for din appdata-mappe, eller hvis du har ændret brugeren og gruppen, som \*Arr kører som.
- Dit bedste og første valg er at [prøve at gendanne fra en sikkerhedskopi](#hvordan-sikkerhedskopierer-gendanner-jeg-min-sonarr)
- Du kan også prøve at genskabe din database. Dette er normalt den eneste mulighed, når dette problem opstår efter en opdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis din sqlite ikke har `.recover` eller du ønsker en mere GUI-venlig (f.eks. Windows) måde, så følg [vores instruktioner på dette wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- En anden mulig årsag til, at du får en fejl med din database, er, at du placerer din database på et netværksdrev (nfs eller smb eller noget andet, der ikke er lokalt). **SQLite er designet til situationer, hvor data og applikationen eksisterer på samme maskine.** Derfor skal din \*Arr AppData-mappe (/config mount for docker) være på lokal lagerplads. [SQLite og netværksdrev fungerer ikke godt sammen og vil på et tidspunkt forårsage en beskadiget database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruger mergerFS, skal du fjerne `direct_io`, da SQLite bruger mmap, som ikke understøttes af `direct_io`, som forklaret i mergerFS [dokumentationen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruger Sonarr på en Mac, og den stoppede pludselig med at fungere. Hvad skete der?

- Mest sandsynligt skyldes dette en MacOS-fejl, der fik en af Sonarr-databaserne til at blive beskadiget.
- [Følg disse trin for at løse problemet](#jeg-får-en-fejl-database-disk-image-is-malformed)
- Prøv derefter at starte Sonarr og se, om det virker. Hvis det ikke virker, har du brug for yderligere support. Indlæg i vores [reddit](http://reddit.com/r/Sonarr) eller hop på [discord](https://discord.sonarr.tv/) for hjælp.

## Hvorfor kan Sonarr ikke se mine filer på en fjernserver?

- For alle operativsystemer skal du sikre dig, at den bruger/gruppe, som \*Arr kører som, har læse- og skriveadgang til det monterede drev.
- For Linux skal du sikre dig:
  - Hvis du bruger et NFS-monteringspunkt, skal du sikre dig, at `nolock` er aktiveret for dit monteringspunkt.
  - Hvis du bruger et SMB-monteringspunkt, skal du sikre dig, at `nobrl` er aktiveret for dit monteringspunkt.
- For Windows: Kort sagt kan brugeren, som \*Arr kører som (hvis det er en tjeneste) eller under (hvis det er en bakkeapp), ikke få adgang til filstien på fjernserveren. Dette kan skyldes forskellige årsager, men den mest almindelige er, at \*Arr kører som en tjeneste, hvilket forårsager de beskrevne problemer nedenfor.

### Sonarr kører som standard under LocalService-kontoen, som ikke har adgang til beskyttede fjernfiler

- Kør Sonarr-tjenesten som en anden bruger, der har adgang til den delte mappe
- Åbn vinduet Administrative værktøjer \> Tjenester på din Windows-server.
- Stop Sonarr-tjenesten.
- Åbn dialogboksen Egenskaber \> Logon.
- Skift brugerkontoen for tjenesten til den ønskede brugerkonto.
- Kør Sonarr.exe ved hjælp af mappen Startup

### Du bruger et kortlagt netværksdrev (ikke en UNC-sti)

- Ændr dine stier til UNC-stier (`\\server\share`)
- Kør Sonarr.exe via mappen Startup

## Kortlagte netværksdrev vs. UNC-stier

- Brug af kortlagte netværksdrev fungerer generelt ikke særlig godt, især når Sonarr er konfigureret til at køre som en tjeneste. Den bedre måde at opsætte delinger på er ved hjælp af UNC-stier. Så i stedet for `X:\TV` skal du bruge `\\Server\TV`.

- Et vigtigt punkt at huske er, at Sonarr får stioplysninger fra downloaderen, så du skal også konfigurere NZBGet, SABNzbd eller en anden downloader til at bruge UNC-stier.

## Sonarr vil ikke fungere på Big Sur

Kør

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## Min brugerdefinerede script stoppede med at fungere efter opgradering fra v2

- Du har sandsynligvis videregivet argumenter i din forbindelse...det understøttes ikke.
- For at rette dette:
  1. Ændr dit argument til at være din sti
  1. Sørg for, at shebang i dit script peger på din pwsh-sti (hvis du ikke har en shebang-definition der, tilføj den)
  1. Sørg for, at pwsh-scriptet er eksekverbart

# Fælles problemer med Sonarr-søgning og -download

## Søgning var vellykket - Ingen resultater returneret

- [Se denne fejlfinding](/sonarr/troubleshooting#query-successful-no-results-returned)

## Hvorfor hentede Sonarr ikke en episode, jeg forventede?

Først skal du sikre dig, at du har læst og forstået afsnittet ovenfor kaldet ["Hvordan finder Sonarr episoder?](#how-does-sonarr-find-episodes) Sørg derefter for, at mindst en af dine indexere har den episode, du forventede at få fat i.

1. Klik på ikonet "Manuel søgning" ved siden af episodelisten i Sonarr. Er der nogen resultater? Hvis nej, har Sonarr enten problemer med at kommunikere med dine indexere, eller dine indexere har ikke episoden, eller episoden er forkert navngivet/kategoriseret på indexeren.
1. **Hvis der er resultater fra trin 1**, skal du kontrollere, om der er et rødt udråbstegn ved siden af dem. Hold musen over ikonet for at se, hvorfor den frigivelse ikke er en kandidat til automatisk download. Hvis hvert resultat har ikonet, vil der ikke blive foretaget nogen automatisk download.
1. **Hvis der er mindst ét gyldigt manuelt søgeresultat fra trin 2**, skulle der være foretaget en automatisk download. Hvis det ikke skete, er den mest sandsynlige årsag et midlertidigt kommunikationsproblem, der forhindrer en RSS-synkronisering fra din indexer. Det anbefales at have flere indexere sat op for at opnå de bedste resultater.
1. **Hvis der ikke er noget manuelt resultat fra en serie, men du kan finde det, når du gennemser din indexers hjemmeside** - Dette kan skyldes forskellige årsager, f.eks. at frigivelsen ikke er korrekt tagget på din indexer, hvilket forhindrer den i at blive returneret til Sonarr i en automatisk søgning. Denne [fejlfinding](/sonarr/troubleshooting#searches-indexers-and-trackers) giver nogle tip til, hvordan du kan finde årsagen. Ved at have flere aktive indexere kan du løse dette ved at give flere kilder til det samme indhold.

## Fundet matchende serie via grab-historik, men frigivelsen blev matchet til serien efter ID. Automatisk import er ikke mulig

- Se [denne fejlfinding](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- På TVDb, når episodenavne er ukendte, vil de blive kaldt TBA, og der er en cache på 24 timer på TVDb API'en. Ændringer på TVDb-webstedet tager normalt 24-48 timer om at nå Sonarr på grund af TVDb-cache (24 timer), skyhook-cache (et par timer) og seriens opdateringsinterval (hver 12. time). Indstillingen [Episode Title Required](/sonarr/settings#importing) i Sonarr styrer importadfærd, når titlen er TBA, men efter 48 timer fra seriens udsendelse vil frigivelsen blive importeret, selvom titlen stadig er TBA. Der er heller ingen automatisk omdøbning af filer med TBA-titel. Bemærk, at TBA-timeren beregnes ud fra episodens udsendelsesdato og tidspunkt, ikke fra hvornår du har hentet den eller uploadtiden.

## Sonarr siger "Ukendt serie" ved søgninger eller importeringer

- Se indgangen [Hvorfor kan Sonarr ikke importere episodfiler til serie X? / Hvorfor kan Sonarr ikke finde frigivelser til serie X?](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er også dets eneste fordel. Alt andet kan potentielt give problemer, så det er nødvendigt at tilføje hver tracker individuelt. Alternativt kan du overveje alternativet Jackett & NZBHydra2 [Prowlarr](/prowlarr)

- **Opdatering 5. februar 2022: \*Arr Support er blevet stoppet for jackett `\all`-endepunktet. Jackett /all-endepunktet understøttes ikke længere (f.eks. vil advarsler forekomme) fra v3.0.6.1457 på grund af, at det kun skaber problemer.**

- Jackett `/all`-endepunktet er praktisk, men det er også dets eneste fordel. Alt andet kan potentielt give problemer, så det er nu nødvendigt at tilføje hver tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af /all-endepunktet har ingen fordele, kun ulemper:
  - du mister kontrollen over indstillingen for den enkelte indexer (kategorier, søgemetoder osv.)
  - blanding af søgemetoder (IMDB, forespørgsel osv.) kan medføre resultater af lav kvalitet
  - specifikke kategorier for indexer (\>= 100000) kan ikke bruges.
  - langsomme indexere vil sænke den samlede resultat
  - det samlede antal resultater er begrænset til 1000
  - hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

### Jackett /All-løsninger

- Tilføj hver tracker i Jackett manuelt som en indexer i \*Arr
- Tjek [Prowlarr](/prowlarr), som kan synkronisere indexere til \*Arr og er udviklet af Lidarr/Radarr/Readarr-udviklingsteamet.
- Tjek [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indexere til \*Arr. Men brug ikke deres enkeltstående aggregat-endepunkt og brug `multi`, hvis synkroniseringen skal bruges.

## Jackett viser flere resultater end Sonarr ved manuel søgning

- Tjek dine konfigurerede kategorier for din tracker i Sonarr
- Dette skyldes normalt, at Sonarr søger i Jackett på en anden måde end dig. [Se denne fejlfinding for yderligere information](/sonarr/troubleshooting#searches-indexers-and-trackers).

## Find cookies

- Nogle websteder kan ikke logges ind automatisk og kræver, at du logger ind manuelt og derefter giver cookies til Sonarr for at fungere. [Se denne artikel for detaljer.](/useful-tools#finding-cookies)

## Udpak torrenter

- De fleste torrentklienter har ikke den automatiske håndtering af komprimerede arkiver som deres usenet-modparter. Vi anbefaler [unpackerr](https://github.com/unpackerr/unpackerr).

## Tilladelser

- Sonarr skal flytte filer væk fra, hvor downloaderen placerer dem, og ind i den endelige placering, så det betyder, at Sonarr skal kunne læse/skrive både i kilde- og destinationsmappen og -filerne.
- På Linux, hvor bedste praksis er, at tjenester kører som deres egen bruger, vil det sandsynligvis betyde, at du skal bruge en delt gruppe og indstille mappe tilladelser til `775` og filer til `664` både i din downloader og Sonarr. I umask-notation vil det være `002`.

## Tvungen godkendelse

- I Sonarr v4 (beta) er godkendelse obligatorisk. Se [Sonarr v4 FAQ - Tvungen godkendelse](/sonarr/faq-v4#forced-authentication) for detaljer.