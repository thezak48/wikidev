## Kan alla mina filmfiler lagras i en enda mapp?

Ja, Radarr stöder att lagra alla filmfiler i en enda mapp. För att göra detta, gå till inställningarna för kvalitetsprofilen och välj "Avancerade inställningar". I avsnittet "Lagringsmetod" kan du välja "Lagra alla filer i en enda mapp". När du har aktiverat den här inställningen kommer alla dina filmfiler att placeras i samma mapp istället för att vara uppdelade i separata mappar baserat på filmens titel.

- Nej, och anledningen är att Radarr är en fork av [Sonarr](/sonarr), där varje show har en mapp. Denna begränsning är en känd smärtpunkt för många användare och kanske kommer att åtgärdas i en framtida version. Observera att det inte är en enkel ändring och kräver i princip en komplett omskrivning av backenden.
- [Custom Folder GitHub Issue](https://github.com/Radarr/Radarr/issues/153) täcker tekniskt sett denna begäran, men det finns ingen garanti för att alla filer för en film i en mapp kommer att implementeras vid den tiden.
- En liten hackig lösning beskrivs nedan. Observera att du inte får utlösa en omgenomsökning i Radarr, eftersom det då kommer att visas som saknat och oavsett kommer filmen aldrig att uppgraderas.
  - Använd ett anpassat skript
    - Skriptet bör aktiveras vid import
    - Det bör utformas för att flytta filen när du vill
    - Sedan måste det anropa Radarr API och ändra filmen till oövervakad.
- Om du vill flytta alla dina filmer från en mapp till individuella mappar kan du titta på artikeln [Tips och tricks => Skapa en mapp för varje film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

## Kan jag placera alla mina filmer i mitt bibliotek i en mapp?

- Nej, se ovan.

## Hur uppdaterar jag Radarr?

- Gå till Inställningar och sedan fliken Allmänt och visa avancerade inställningar (använd växeln bredvid spara-knappen).

1. Under avsnittet Uppdateringar ändrar du grennamnet till `master` eller `develop`
1. Spara

*Detta kommer inte att installera bitarna från den grenen omedelbart, det kommer att ske under nästa uppdatering.*

- ![Nuvarande Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Den har testats av användare på utvecklings- och nattliga grenar och det är inte känt att den har några större problem. Den här versionen kommer att få uppdateringar ungefär en gång i månaden. På GitHub är detta grenen `master`.

- ![Nuvarande Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Beta): Detta är kanten för testning. Släpps efter att ha testats i nattlig version för att säkerställa att det inte finns några omedelbara problem. Nya funktioner och buggfixar släpps här först efter nattlig version. Den kan betraktas som halvstabil, men är fortfarande `beta`. Den här versionen kommer att få uppdateringar antingen veckovis eller varannan vecka beroende på utveckling.

> **Varning: Du kanske inte kan gå tillbaka till `master` efter att ha bytt till den här grenen.** På GitHub är detta en ögonblicksbild av `develop`-grenen vid en specifik tidpunkt.
{.is-warning}

- ![Nuvarande Nightly/Ostabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alfa/Ostabil): Detta är den senaste versionen. Den släpps så snart koden har begåtts och passerar alla automatiserade tester. Denna version kan ännu inte ha använts av oss eller andra användare. Det finns ingen garanti för att den ens kommer att fungera i vissa fall. Den här grenen rekommenderas endast för avancerade användare. Problem och egen undersökning förväntas i denna gren. ***Använd den här grenen endast om du vet vad du gör och är villig att ta i lite för att återställa en misslyckad uppdatering.*** Den här versionen uppdateras omedelbart.

> **Varning: Du kanske inte kan gå tillbaka till `master` efter att ha bytt till den här grenen.** På GitHub är detta `develop`-grenen.
{.is-danger}

- Observera: Om du installerar via Docker lägger du till `:release`, `:latest`, `:testing` eller `:develop` i slutet av din container-tagg beroende på vem som gör dina byggningar.

|                                                                    | ![Nuvarande Master/Senaste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Nuvarande Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Nuvarande Nightly/Alfa](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kan jag uppdatera Radarr inuti min Docker-container?

- *Tekniskt sett, ja.* **Men du bör absolut inte göra det.** Det är en grundläggande princip för Docker. Det kan uppstå databasproblem om du uppgraderar din installation till den senaste `nightly`, men sedan uppdaterar Docker-containern själv (eventuellt nedgraderar till en äldre version).

### Installera en nyare version

#### Naturlig

1. Gå till System och sedan fliken Uppdateringar
1. Nyare versioner som inte är installerade än kommer att ha en uppdateringsknapp bredvid dem, klicka på den knappen för att installera uppdateringen.

#### Docker

1. Dra om din tagg och uppdatera din container

## Kan jag växla från `nightly` tillbaka till `develop`?

## Kan jag växla mellan grenar?

- Om versionen är identisk kan du växla, annars kontrollera med utvecklingsteamet om du kan växla från `nightly` till `master`; `nightly` till `develop`; eller `develop` till `master` för din specifika byggning.
- Om du inte följer dessa instruktioner kan din Radarr bli oanvändbar eller kasta fel. Du har blivit varnad. Om följande fel uppstår använder du en nyare databas med en äldre \*Arr-version som inte stöds. Uppgradera \*Arr till den version du tidigare hade eller nyare.
  - Exempel på felmeddelanden:
    - `Fel vid tolkning av kolumn 45 (Language=31 - Int64)`
    - `DataMapper kunde inte läsa in följande fält: 'Languages' värde`
    - `ID matchar inte ett känt språk Parameternamn: id`
    - Andra liknande databasfel om saknade kolumner eller tabeller.

## Hur säkerhetskopierar/återställer jag Radarr?

### Säkerhetskopiering av Radarr

#### Använda inbyggd säkerhetskopiering

- Gå till System => Säkerhetskopiering i Radarr UI
- Klicka på Säkerhetskopiera-knappen
- Ladda ner zip-filen efter att säkerhetskopieringen har skapats för att spara den på ett säkert ställe

#### Använda filsystemet direkt

- Hitta platsen för AppData-mappen för Radarr
  - Via Radarr UI, gå till System => Om
  - [Radarr Appdata-mapp](/radarr/appdata-directory)
- Stoppa Radarr - Detta förhindrar att databasen blir korrupt
- Kopiera innehållet till en säker plats

### Återställning från säkerhetskopia

> Att återställa till ett operativsystem som använder olika sökvägar kommer inte att fungera (Windows till Linux, Linux till Windows, Windows till OS X eller OS X till Windows), att flytta mellan OS X och Linux kan fungera, eftersom båda använder sökvägar som innehåller `/` istället för `\` som Windows använder, men det stöds inte. Du måste manuellt redigera alla sökvägar i databasen eller använda [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Använda zip-säkerhetskopia

- Installera Radarr igen (om tillämpligt / inte redan installerat)
- Kör Radarr
- Gå till System => Säkerhetskopiering
- Välj Återställ säkerhetskopia
- Välj Välj fil
- Välj din säkerhetskopierings-zip-fil
- Välj Återställ

#### Använda filsystemets säkerhetskopia

- Installera Radarr igen (om tillämpligt / inte redan installerat)
- Hitta platsen för AppData-mappen för Radarr
  - Kör Radarr en gång och gå via UI till System => Om
  - [Radarr Appdata-mapp](/radarr/appdata-directory)
- Stoppa Radarr
- Radera innehållet i AppData-mappen **(inklusive .db-wal/.db-journal-filerna om de finns)**
- Återställ från din säkerhetskopia
- Starta Radarr
- Så länge sökvägarna är desamma kommer allt att fortsätta där det slutade

#### Återställning av filsystemet på Synology NAS

> VARNING: Återställning på en Synology kräver kunskap om Linux och Root SSH-åtkomst till Synology-enheten.
{.is-warning}

- Installera Radarr igen (om tillämpligt / inte redan installerat)
- Hitta platsen för AppData-mappen för Radarr
  - Kör Radarr en gång och gå via UI till System => Om
  - [Radarr Appdata-mapp](/radarr/appdata-directory)
- Stoppa Radarr
- Anslut till Synology NAS via SSH och logga in som root

> På vissa installationer är användaren annorlunda än nedanstående kommandon: `chown -R sc-Radarr:Radarr *` {.is-info}

- Kör följande kommandon:

    ```shell
        rm -r /usr/local/Radarr/var/.config/Radarr/Radarr.db
        cp -f /tmp/Radarr_backup/* /usr/local/Radarr/var/.config/Radarr/
    ```

- Uppdatera behörigheterna för filerna:

    ```shell
        cd /usr/local/Radarr/var/.config/Radarr/
        chown -R Radarr:users *
        chmod -R 0644 *
    ```

- Starta Radarr

# Vanliga problem med Radarr

## En uppgift avbröts

- Radarr fick inget svar från servern som begäran gjordes till efter 100 sekunder.
- Loggarna kommer att innehålla `System.Threading.Tasks.TaskCanceledException: A task was canceled.`
- Detta orsakas ofta av:
  - felaktig konfiguration eller användning av en VPN
  - felaktig konfiguration eller användning av en proxy
  - lokala DNS-problem - Försök att byta till en annan DNS-leverantör
  - lokala IPv6-problem - *vanligast* - vanligtvis är IPv6 aktiverat på värdsystemet, men fungerar inte
  - användning av Privoxy och felaktig konfiguration av det
  - PiHole [Rate Limiting](https://docs.pi-hole.net/ftldns/configfile/#rate_limit) förfrågningar
- Du kan felsöka med DNS `nslookup <domän.tld från spårloggar>` och ipv6 med `curl -sv -6 "<url från spårloggar>"` / all annan anslutning med `curl -sv -4 "<url från spårloggar>"`

## Sökvägen är redan konfigurerad för en befintlig film

![existing-movie.png](/assets/radarr/existing-movie.png)

- Biblioteksimporten visar "Befintlig" eller så får du ett felmeddelande "Sökvägen är konfigurerad för en befintlig film"
- Detta inträffar när du försöker lägga till en film eller redigera en befintlig films sökväg som redan är tilldelad en annan film.
- Troligtvis orsakades detta av att du inte rättade till en felmatchad film när du importerade ditt bibliotek.
- Hitta och rätta till den film som redan är tilldelad den films sökväg.
  - Filmindex
  - Tabellvy
  - Alternativ => Lägg till sökväg som en kolumn
  - Sortera och hitta filmen med den noterade problematiska sökvägen.
- Alternativt kan du ta bort filmen som använder den befintliga sökvägen från Radarr

## Hur kan jag döpa om mina filmmappar?

{#rename-folders}

> Samma process gäller också för att flytta/ändra filvägar för filmer. Om du bara uppdaterar vägarna i Radarr och inte behöver flytta filerna, välj inte "Ja, flytta filer" i steg 5.
{.is-info}

1. Filmer
1. Filmredigerare
1. Välj vilka filmer som behöver byta namn på mappen
1. Ändra rotmappen till samma rotmapp som filmerna för närvarande finns i
1. Välj "Ja, flytta filer"

> Om du använder Plex kommer detta att utlösa omidentifiering av introduktioner, miniatyrer, kapitel och förhandsgranskningsmetadata.
{.is-warning}

## Namngivning av filmfiler och mappar

- För närvarande kräver Radarr att varje film finns i en mapp med formatet `Filmens titel (År)/`, valfritt är `_` eller `.` giltiga separatorer. För att underlätta korrekt identifiering av kvalitet och upplösning vid import är ett filnamn som `Filmens titel (År) [Kvalitet-Upplösning].ext` bäst, igen är `_` eller `.` giltiga separatorer.

  - Ett användbart verktyg för att göra dessa ändringar i din samling är [filebot](http://www.filebot.net/#download) som har en betalversion i både Apple och Windows-butikerna, men kan hittas gratis på deras äldre [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) webbplats. Det har både ett GUI och CLI, så du kan använda det du är bekväm med. För det ovanstående exemplet expanderar `{ny}` till `Namn (År)` och `{vf}` ger upplösningen som `1080p`. Det finns inget att härleda kvalitet, så du kan fejka det med hjälp av `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]` som kommer att namnge allt lägre än 720p till `[DVD-572p]` och större eller lika med 720p som `[Bluray-1080p]`.

- Se [Tips och tricks-avsnittet => Skapa en mapp för varje film](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) för mer information.

## Filmmappar namngivna felaktigt

- Namngivningen av filmmappar baseras på metadata (namn/år) vid tidpunkten då filmen lades till. Om du lade till en film innan den släpptes kan du behöva använda den ovan nämnda trick för att uppdatera namnet på filmmappen för att återspegla den nya aktuella datan.
- Även om dina filmer redan finns i mappar kanske inte mapparna är namngivna korrekt. Mappnamnet bör vara `Filmens titel (År)`, att ha titeln och året i mappens namn är avgörande just nu.

  - Exempel som fungerar bra:
    - `/mnt/Filmer/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Barnfilmer/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Exempel som fungerar, men kräver manuell hantering:
    - Efter bokstäver: `/mnt/Filmer/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Efter betyg: `/mnt/Filmer/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Efter genre: `/mnt/Filmer/Brott, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Dessa exempel kräver manuell hantering när filmen läggs till. Varje exempel kommer att ha många rotkataloger, som `A-D` och `E-G` i det första bokstavs-exemplet, `R` och `PG-13` i betygs-exemplet och du kan gissa vilka olika genre-mappar det finns. När du lägger till en ny film måste rätt grundmapp väljas för att detta format ska fungera.
  - Exempel som inte fungerar:
    - Enkel mapp: `/mnt/Barnfilmer/Frozen (2013) [Bluray-1080p].mkv`
      - För närvarande måste filmer helt enkelt vara i en mapp med samma namn som filmen. Det finns inget sätt att komma runt detta förrän utvecklingsarbetet är klart för att lägga till den här funktionen.
    - **Filmmapp-namn-format från v0.2 som inkluderar **Filminformation** i **filmmappens** namn som ``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}`` kommer inte att fungera i v3.
      - Mappar är relaterade till filmen och oberoende av filen. Dessutom kommer detta att brytas med det planerade stödet för flera filer per film.
      - Den andra anledningen till att det togs bort var att det orsakade frekventa förvirringar, databaskorruption och var generellt sett bara halvfärdigt.
  - [Tips och tricks-avsnittet => Skapa en mapp för varje film](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) är en bra källa för att se till att din fil- och mappstruktur fungerar bra.

## Kan jag inaktivera uppdatering av filmer?

- Nej, och du bör inte göra det genom någon SQL-hackning heller. Uppdateringsuppgiften för filmer frågar uppströms Servarr-proxy och kontrollerar om metadata för varje film (ID, rollista, sammanfattning, betyg, översättningar, alternativa titlar, etc.) har uppdaterats jämfört med vad som för närvarande finns i Radarr. Vid behov kommer den sedan att uppdatera de tillämpliga filmerna.
- Ett vanligt klagomål är att uppdateringsuppgiften orsakar tung I/O-användning.
- Den huvudsakliga inställningen är "Skanna om filmmapp efter uppdatering". Om din disk I/O-användning ökar under en uppdatering kan du ändra skanningsinställningen till `Manuell`.
  - Ändra inte detta till `Aldrig` om alla ändringar i ditt bibliotek (nya filmer, uppgraderingar, borttagningar etc.) görs genom Radarr.
  - Om du tar bort filmfiler manuellt eller via Plex eller ett annat tredjepartsprogram, ställ inte in detta till `Aldrig`.
- Den andra inställningen som kan ändras är "Analysera videofiler", vilket rekommenderas att aktiveras om du använder tdarr eller på annat sätt modifierar dina filer externt. Om du inte gör det kan du tryggt inaktivera "Analysera videofiler" för att minska lite I/O.

## Hur begär jag en funktion för Radarr?

- Detta är enkelt [klicka här](https://github.com/Radarr/Radarr/issues)

## Hjälp, min Mac säger att Radarr inte kan öppnas eftersom utvecklaren inte kan verifieras

- Detta är enkelt, se denna länk för mer information [här](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Utvecklaren kan inte verifieras](developer-cannot-be-verified.png "Utvecklaren kan inte verifieras")
- Alternativt kan du behöva självsignera Radarr `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Hjälp, min Mac säger att Radarr.app är skadad och kan inte öppnas

- Det beror antingen på en korrupt nedladdning, så försök igen eller [säkerhetsproblem, se denna relaterade FAQ-post.](#hjälp-min-mac-säger-att-radarr-inte-kan-öppnas-efter-att-utvecklaren-inte-kan-verifieras)

## Jag får ett felmeddelande: Databasens diskavbildning är skadad

> \* För Radarr-användare som upplever detta efter uppgradering till v4.X-versioner. v4-versioner gör flera långtgående migreringar eftersom om din databas hade tidigare korruption på någon plats (som kanske inte var upptäckbar tidigare när Radarr kördes) kommer migreringen att misslyckas. Detta kommer att orsaka att Radarr inte kan starta. Det är troligt att alla dina säkerhetskopior också är korrupta, så att bara återställa dem kommer troligen inte att lösa problemet.
> \* Om den migrerade databasen inte kan öppnas eller inte kan återställas, gör en kopia av databasen från en nyligen gjord säkerhetskopia och använd databasåterställningsprocessen på den filen och försök sedan starta Radarr med den återställda säkerhetskopian. Den bör då migrera utan problem.
{.is-warning}

- **Felmeddelanden om `Fel vid skapande av logg-databas` indikerar problem med logs.db**
  - Detta kan snabbt åtgärdas genom att byta namn på eller ta bort databasen. Logg-databasen innehåller oviktig information om kommandohistorik och uppdateringsinstallationshistorik, samt Info-, Warn- och Error-poster.
- **Felmeddelanden om `Fel vid skapande av huvuddatabas` eller generella `Databasens diskavbildning är skadad` utan angiven databas indikerar problem med radarr.db**
  - Fortsätt med de nedan angivna stegen
- Detta innebär att din SQLite-databas som lagrar det mesta av informationen för Radarr är korrupt. Dina alternativ är att försöka använda (en) säkerhetskopia(r), försöka återställa den befintliga databasen, försöka återställa säkerhetskopiorna eller om allt annat misslyckas börja om med en helt ny databas.
- Detta fel kan visas om databasfilen inte kan skrivas av användaren/gruppen som \*Arr körs som. Rättigheter kan vara orsaken till problemet endast för nya installationer, migrerade installationer till en ny server, om du nyligen har ändrat behörigheterna för din appdata-katalog eller om du har ändrat användaren och gruppen som \*Arr körs som.
- Ditt bästa och första alternativ är att [försöka återställa från en säkerhetskopia](#hur-backupåterställer-jag-min-radarr). Men för användare som får detta efter uppgradering till v4 är det mycket osannolikt att själva säkerhetskopin kommer att fungera och du måste prova de andra återställningsmetoderna som nämns.
- Du kan också försöka återställa din databas. Detta är vanligtvis det enda alternativet när detta problem uppstår efter en uppdatering. Prova [sqlite3 `.recover`-kommandot](/useful-tools#recovering-a-corrupt-db)
  - Om din sqlite inte har `.recover` eller om du vill ha ett mer GUI-vänligt sätt (t.ex. Windows) kan du följa [våra instruktioner på denna wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- En annan möjlig orsak till att du får ett fel med din databas är att du placerar din databas på en nätverksenhet (nfs eller smb eller något annat som inte är lokalt). **SQLite är utformat för situationer där data och applikationen existerar på samma maskin.** Därför måste din \*Arr AppData-mapp (/config-montering för docker) vara på lokal lagring. [SQLite och nätverksenheter fungerar inte bra tillsammans och kommer så småningom att orsaka en skadad databas](https://www.sqlite.org/draft/useovernet.html).
- Om du använder mergerFS måste du ta bort `direct_io` eftersom SQLite använder mmap som inte stöds av `direct_io`, som förklaras i mergerFS [dokumentationen här](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jag använder Radarr på en Mac och den slutade plötsligt fungera. Vad har hänt?

- Detta beror förmodligen på en bugg i MacOS som orsakade att en av databaserna blev korrupt.
- Se ovanstående avsnitt om att databasen är skadad.
- Försök sedan starta och se om det fungerar. Om det inte fungerar behöver du ytterligare support. Skriv inlägg i vår [subreddit /r/radarr](http://reddit.com/r/radarr) eller gå med i [vår discord](https://radarr.video/discord) för hjälp.

## Varför kan inte Radarr se mina filer på en fjärrserver?

- För alla operativsystem, se till att användaren/gruppen som du kör \*Arr som har läs- och skrivrättigheter till den monterade enheten.
- För Linux, se till:
  - Om du använder en NFS-montering, se till att `nolock` är aktiverat för din montering.
  - Om du använder en SMB-montering, se till att `nobrl` är aktiverat för din montering.
- För Windows: Kort sagt: användaren som \*Arr körs som (om det är en tjänst) eller under (om det är en fältapp) kan inte komma åt filvägen på fjärrservern. Det kan bero på olika skäl, men det vanligaste är att \*Arr körs som en tjänst, vilket orsakar de problem som beskrivs nedan.

### Radarr körs som standard under LocalService-kontot som inte har åtkomst till skyddade fjärrfilresurser

- Kör Radarr-tjänsten som en annan användare som har åtkomst till den resursen
- Öppna fönstret för Administrativa verktyg \> Tjänster på din Windows-server.
- Stoppa Radarr-tjänsten.
- Öppna dialogrutan Egenskaper \> Logga på.
- Ändra användarkontot för tjänsten till målkontot.
- Kör Radarr.exe med hjälp av mapparna för automatisk start

### Du använder en kartlagd nätverksenhet (inte en UNC-sökväg)

- Ändra dina sökvägar till UNC-sökvägar (`\\server\share`)
- Kör Radarr.exe via mapparna för automatisk start

## Hur ändrar jag från Windows-tjänsten till en fältapp?

1. Stäng av Radarr
1. Kör serviceuninstall.exe som finns i Radarr-mappen
1. Kör `Radarr.exe` som administratör en gång för att ge den rätt behörigheter och öppna brandväggen. När det är klart kan du stänga det och köra det normalt.
1. (Valfritt) Lägg till en genväg till .exe-filen i mappen för automatisk start för att starta automatiskt vid uppstart.

## Hjälp, jag har låst mig ute

{#help-i-have-forgotten-my-password}

För att inaktivera autentisering (för att återställa ditt glömda användarnamn eller lösenord) måste du redigera `config.xml` som kommer att finnas i [Radarr Appdata-katalogen](/radarr/appdata-directory)

1. Öppna config.xml i en textredigerare
1. Hitta raden för autentiseringsmetod som kommer att vara
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Ändra raden för `AuthenticationMethod` till `<AuthenticationMethod>None</AuthenticationMethod>`
1. Starta om Radarr
1. Radarr kommer nu att vara tillgängligt utan lösenord, du bör gå till `Inställningar: Allmänt` i gränssnittet och ange ditt användarnamn och lösenord

## Hur stoppar jag webbläsaren från att starta vid uppstart?

Beroende på ditt operativsystem finns det flera möjliga sätt.

- I `Inställningar` => `Allmänt` på vissa operativsystem finns det en kryssruta för att starta webbläsaren vid uppstart.
- När du startar Radarr kan du lägga till `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumenten.
- Stoppa Radarr och redigera config.xml-filen och ändra `<LaunchBrowser>True</LaunchBrowser>` till `<LaunchBrowser>False</LaunchBrowser>`.

## Konstiga UI-problem

- Om du upplever konstiga UI-problem som att bibliotekssidan inte listar något eller att en viss vy eller sortering inte fungerar, försök att visa det i ett Chrome Inkognitofönster eller Firefox Privat fönster. Om det fungerar bra där, rensa webbläsarens cache och cookies för din specifika IP/domän. För mer information, se artikeln [Rensa cache, cookies och lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wikin.

## Webbgränssnittet laddas bara på localhost på Windows

- Om du bara kan nå ditt webbgränssnitt på <http://localhost:7878/> eller <http://127.0.0.1:7878/>, måste du köra som administratör minst en gång.

## Behörigheter

- Radarr kommer att behöva flytta filer från där nedladdaren placerar dem till den slutliga platsen, så detta innebär att den måste läsa/skriva till både käll- och destinationsmappen och filerna.
- På Linux, där bästa praxis är att köra tjänster som sin egen användare, kommer detta förmodligen att innebära att du använder en delad grupp och ställer in mappbehörigheter till `775` och filer till `664` både i din nedladdare och . I umask-notation skulle det vara `002`.

## System och loggar laddas för evigt

- Det är EasyPrivacy-blocklistan. De blockerar i princip alla URL:er med /api/log? i dem. Titta över listan och bedöm om du tycker att det är en vettig idé att blockera alla URL:er i den, det finns dussintals URL:er där som potentiellt bryter webbplatser. Du valde det i din annonsblockerare. Det enkla sättet är att lägga till domänen som Radarr körs på i whitelistan. Men jag rekommenderar ändå att du kontrollerar listan.

## Packa upp torrents

- De flesta torrentklienter har inte automatisk hantering av komprimerade arkiv som deras Usenet-motsvarigheter. Vi rekommenderar [unpackerr](https://github.com/unpackerr/unpackerr).

## uTorrent fungerar inte längre

- Se till att webbgränssnittet är aktiverat
- Se till att den alternativa lyssningsporten för webbgränssnittet (Avancerat => Web UI) inte är samma som lyssningsporten (Anslutningar)
- Vi rekommenderar att du ändrar den alternativa lyssningsporten för webbgränssnittet så att den inte stör någon portvidarebefordran för anslutningar.

## Jag fick ett popup-fönster som sa att config.xml var korrupt, vad gör jag nu?

- Radarr kunde inte läsa din konfigurationsfil vid start eftersom den på något sätt blev korrupt. För att komma tillbaka online måste du ta bort `.xml` i din [appdata-katalog](/radarr/appdata-directory), när den är borttagen startar du och den kommer att starta på standardporten (7878), du bör nu konfigurera om eventuella inställningar du konfigurerade på sidan för allmänna inställningar.

## Ogiltigt certifikat och andra HTTPS- eller SSL-problem

- Din nedladdningsklient har slutat fungera och du får ett fel som "Localhost är ett ogiltigt certifikat"?
  - Radarr validerar SSL-certifikat. Om det inte finns något SSL-certifikat inställt i nedladdningsklienten, eller om du använder ett självsignerat https-certifikat utan att ha lagt till CA-certifikatet i din lokala certifikatbutik, kommer Radarr att vägra att ansluta. Gratis korrekt signerade certifikat finns tillgängliga från [let's encrypt](https://letsencrypt.org/).
  - Om din nedladdningsklient och din dator är på samma maskin finns det ingen anledning att använda HTTPS, så det enklaste sättet är att inaktivera SSL för anslutningen. De flesta skulle hålla med om att det inte är nödvändigt i ett lokalt nätverk heller. Det är möjligt att inaktivera certifikatvalidering i avancerade inställningar om du vill behålla en osäker SSL-konfiguration.

## VPN, Jackett och \*ARRs

- Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika är det vanligtvis bara din torrentklient som behöver vara bakom en VPN. Eftersom VPN-ändpunkten delas av många användare kan du och kommer att uppleva begränsningar av hastigheten, DDOS-skydd och IP-blockeringar från olika tjänster som varje program använder.
- Med andra ord kan det göra att \*ARRs (Lidarr, Prowlarr, Radarr, Readarr och Lidarr) blir oanvändbara i vissa fall på grund av att tjänsterna inte är tillgängliga om du sätter dem bakom en VPN.

> **För att vara tydlig handlar det inte om ifall VPN kommer att orsaka problem med \*ARRs, utan när: bildleverantörer kommer att blockera dig och cloudflare finns framför de flesta \*ARR-servrar (uppdateringar, metadata osv.) och kan också blockera dig**
{.is-warning}

- **Många privata spårare kommer att blockera dig om du använder eller får åtkomst till dem (t.ex. genom Jackett eller Prowlarr) via en VPN.**

### Användning av VPN

- Om en VPN krävs och Docker används rekommenderas det att använda Hotio eller Binhex's Download Client + VPN Containers.
- Om en VPN krävs och Docker inte används måste din VPN-klient ***stödja uppdelad tunnel*** så att endast de nödvändiga (nedladdningsklient) apparna är bakom VPN:en.
- Många problem med att komma åt spårare kan lösas genom att använda Googles eller Cloudflares DNS-servrar istället för din internetleverantörs DNS-servrar.
- I vissa fall (t.ex. brittiska internetleverantörer) kan du behöva sätta din torrentnedladdningsklient bakom en VPN och Jackett/Prowlarr enligt följande:
  - sätt Jackett bakom VPN:en och se till att uppdelad tunnel tillåter lokal åtkomst
  - för Prowlarr konfigurerar du din VPN-klient för att tillhandahålla en proxy och lägger till proxyn i Inställningar => Indexers. Ge proxyn en tagg och ge samma tagg till eventuella indexers som behöver använda den.
    - Om det absolut krävs och om din VPN inte har ett sätt att skapa en proxy kan du sätta Prowlarr bakom VPN:en och se till att uppdelad tunnel tillåter lokal åtkomst.

# Vanliga problem med sökning och nedladdning i Radarr

## Varför kan jag inte lägga till en ny film i Radarr?

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarr använder [The Movie Database (TMDb)](http://themoviedb.org) för filminformation och bilder som fanart, banners och bakgrunder. Generellt sett finns det några anledningar till varför du kanske inte kan lägga till en film:
  - TMDb gillar inte att specialtecken används vid sökning efter filmer via API:et (som Radarr använder), så försök att söka med ett översatt namn och/eller utan specialtecken.
  - Du kan också lägga till genom TMDb ID eller, om TMDb har det, IMDb ID
  - Filmen har ännu inte lagts till i TMDb, följ deras [guide](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006) för att få den tillagd.

## Jackett visar fler resultat än vid manuell sökning

- Detta beror vanligtvis på att du söker i Jackett på ett annat sätt än du gör manuellt. Se vår [felsökningsartikel](/radarr/troubleshooting) för mer information.

## Hur bestämmer Radarr året för en film?

- Radarr hämtar metadata från [TMDb](https://www.themoviedb.org/)
- Radarr använder det äldsta **Theatrical Release**-datumet och det äldsta **Premier**-datumet för att matcha.
  - Observera att om det inte finns något Theatrical Release kommer logiken att falla tillbaka på det äldsta fysiska eller digitala släppdatumet.
- Om en film saknar ett digitalt, fysiskt, teatraliskt eller premiärsläppdatum bör TMDb uppdateras.
- [TMDb's Contribution Bible](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) noterar följande om deras släppkategorier.
  - **Premiere** - En premiärvisning kan vara en festivalvisning (t.ex. TIFF) eller ett premiärevenemang med skådespelare och filmteam i en storstad (t.ex. LA, London, Toronto).
  - **Theatrical** - Kan användas för originalsläppet och alla efterföljande officiella släpp. Används för breda eller mättade släpp. I USA anses 600-1 999 biografer vara ett brett släpp och 2 000+ som ett mättat släpp.
  - **Theatrical (limited)** - Begränsat teatraliskt släpp är en distributionsstrategi för att släppa en ny film på ett fåtal biografer i ett land, vanligtvis i större storstadsområden. I USA är antalet biografer färre än 600.
  - **Physical** - Inkluderar alla VHS-, DVD- och Blu-ray-utgåvor.
  - **Digital** - Alla relevanta släpp kan läggas till, inklusive streamingplattformar, VOD-uthyrning eller -köp. Digitala visningar, inklusive online-filmfestivaler och virtuella biografsläpp, räknas också som digitala släpp.

## Hur hanterar Radarr utländska filmer eller utländska titlar?

> [TRaSH's Custom Format Language Guide](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kan vara användbar för att hjälpa till att få filmer på det/den språk du vill ha.{.is-info}

> Från och med 2023-02-12 kommer Radarrs metadata-cache att börja betrakta en films ursprungsspråk som TMDbs talade språk om och endast om endast 1 talat språk finns för filmen på TMDb; annars kommer filmens ursprungliga TMDb-språk att användas.
{.is-warning}

## Sökningar med ID

- **Indexer som stöder sökningar baserade på ID** - Sökningar på indexeringar och spårare som stöder ID-baserade sökningar (TMDbId, IMDbId osv.) - som många Usenet-indexeringar och många privata Torrent-spårare - textfrågor används inte om resultat returneras för en ID-baserad sökning. Om resultat returneras kommer det inte att falla tillbaka till en namn/textsökning. Om du saknar resultat från din indexer beror det på att de har släppen associerade med felaktigt film-ID.
  - Släppets språk kan också härledas från indexerarens eller spårarens släpps språk i resultatet om det tillhandahålls, istället för att tolkas från namnet

## Textsökningar

- **Indexer som inte stöder ID-baserade sökningar eller ID-baserade sökningar utan resultat** - Sökningar kommer att använda filmens ursprungliga titel, engelska titel och översatt titel från de språk du har valt i filmens kvalitetsprofil och eventuella anpassade format med poäng i kvalitetsprofilen större än noll.
- Parsning (dvs. import) letar efter en matchning i alla översättningar och alternativa titlar.
  - Släppets språk kan också härledas från indexerarens eller spårarens släpps språk i resultatet om det tillhandahålls, istället för att tolkas från namnet

## Att få utländska filmer

- För att få en film på ett främmande språk, ställ in filmens kvalitetsprofilsspråk till Original (Filmens ursprungsspråk\*), ett specifikt språk för den profilen eller `Any` och skapa och ge poäng större än 0 till anpassade format med språkvillkor för att bestämma vilket språk som ska hämtas.
- Observera att detta inte inkluderar några indexeringspråk som är konfigurerade som `multi`.
  - Observera att från och med [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) antas inte längre att `multi` inkluderar engelska
  - Användare kan justera sina inställningar per indexerare för att ange vilket/vilka språk `multi` indikerar

## Hur hanterar Radarr "multi" i namn?

- Med Radarr v4.1+ antar Radarr att
`multi` endast är filmens språk och **INTE** engelska som i tidigare versioner.
  - Användare kan justera sina inställningar per indexerare för att ange vilket/vilka språk `multi` indikerar
- Observera att `multi`-definitioner bara hjälper till för parsning av släpp och inte för utländska titlar eller filmsökningar.

## Hjälp, filmen har lagts till men inte sökt

- Radarr söker inte *aktivt* efter saknade filmer automatiskt. Istället görs en periodisk förfrågan om nya inlägg till alla indexerare som är konfigurerade för RSS. När en efterfrågad film eller en film som inte uppfyller klippningskriterierna dyker upp i den listan laddas den ner. Det betyder att en film inte kommer att laddas ner förrän den har publicerats (eller publicerats igen).
- Om du lägger till en film som du vill ha nu är det bästa alternativet att markera rutan "Starta sökning efter saknad film", till vänster om knappen *Lägg till film* (**1**). Du kan också gå till sidan för en film du har lagt till och klicka på förstoringsglaset "Sök" (**2**) eller använda översikten Önskad för att söka efter saknade eller klippningskriterierna som inte uppfylls.

  - Lägg till och sök efter film när du lägger till en film
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Sök efter en befintlig film
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jacketts /all Endpoint

{#jackett-all-endpoint}

- Jacketts `/all`-endpoint är bekväm, men det är dess enda fördel. Allt annat kan leda till problem, så det krävs att varje spårare läggs till individuellt. Alternativt kan du överväga det Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

- **Uppdatering 1 januari 2022: Jacketts `/all`-endpoint stöds inte längre (t.ex. varningar kommer att visas) från och med 4.0.0.5730 på grund av att det bara orsakar problem.**

- Jacketts /all-endpoint är bekväm, men det är dess enda fördel. Allt annat kan leda till problem, så nu krävs det att varje spårare läggs till individuellt.
- [Även Jacketts utvecklare säger att det bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Att använda /all-endpointen har inga fördelar, bara nackdelar:
  - du förlorar kontrollen över inställningar för specifika indexerare (kategorier, söklägen osv.)
  - att blanda söklägen (IMDB, fråga osv.) kan ge lågkvalitativa resultat
  - indexer-specifika kategorier (\>= 100000) kan inte användas.
  - långsamma indexerare kommer att sakta ner det totala resultatet
  - totalt antal resultat är begränsat till 1000
  - om en av spårarna i /all returnerar ett fel kommer \*Arr att inaktivera den och nu får du inga resultat.

### Lösningar för Jackett /All

- Lägg till varje spårare i Jackett manuellt som en indexerare i \*Arr
- Kolla in [Prowlarr](/prowlarr) som kan synkronisera indexerare med \*Arr och kommer från Lidarr/Radarr/Readarr-utvecklingsteamet.
- Kolla in [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisera indexerare med \*Arr. Men använd inte deras enskilda samlingsendpunkt och använd `multi` om synkronisering kommer att användas.

## Varför finns det två filer? | Varför finns det en fil kvar i nedladdningar?

Detta är förväntat. Med en konfiguration som stöder [hårdlänkar](https://trash-guides.info/hardlinks) kommer inte dubbel utrymme att användas. Nedan följer hur Torrent-processen fungerar.

1. Radarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten. Exempel: filmer, tv, serier, musik osv.
1. Radarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Denna övervakning sker via din nedladdningsklients API.
1. Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (kvot eller tid kan justeras i nedladdningsklienten eller från inom under den specifika nedladdningsklienten). När filer importeras till din mediamapp skapas en hårdlänk till filen om det stöds av din konfiguration, annars kopieras filen om hårdlänkar inte stöds.
1. Om alternativet "Hantering av slutförda nedladdningar - Ta bort slutförda" är aktiverat i Radarrs inställningar kommer Radarr att ta bort den ursprungliga filen och torrenten från din nedladdningsklient, men endast om nedladdningsklienten rapporterar att seedningen är klar och torrenten är stoppad (dvs. pausad). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) för hur du konfigurerar din nedladdningsklient optimalt.

> Hårdlänkar är aktiverade som standard. [En hårdlänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din slutförda nedladdningsmapp och din mediebiblioteksmapp. Om skapandet av hårdlänken misslyckas eller om din konfiguration inte stöder hårdlänkar kommer det att falla tillbaka och kopiera filen.
{.is-info}

## Varför fungerar inte Radarr bakom en omvänd proxy?

- Från och med v3 har Radarr bytt till .NET och en ny webbserver. För att SignalR ska fungera, att knapparna i användargränssnittet ska fungera, att databasändringar ska genomföras och andra saker. Krävs följande tillägg till platsblocket för Radarr:

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- Se till att du **inte** inkluderar `proxy_set_header Connection "Upgrade";` som föreslås i nginx-dokumentationen. **DET HÄR KOMMER INTE ATT FUNGERA**
- [Se detta ASP.NET Core-problem](https://github.com/aspnet/AspNetCore/issues/17081)
- Om du använder en CDN som Cloudflare, se till att websockets är aktiverade för att tillåta websocket-anslutningar.
- Om du har oönskade omdirigeringar, se till att din värdheader vidarebefordras.