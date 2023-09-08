## Kan alle filmfilene mine lagres i én mappe?

Ja, Radarr gir deg muligheten til å lagre alle filmfilene dine i én mappe. Du kan konfigurere dette ved å følge disse trinnene:

1. Gå til **Innstillinger** i Radarr-menyen.
2. Velg **Media Management**-fanen.
3. Under **Filbehandling**-delen, aktiver alternativet **Grupper filmen i en enkelt mappe**.
4. Angi den ønskede mappen der alle filmfilene skal lagres.

Merk at hvis du velger å lagre alle filmfilene i én mappe, vil Radarr opprette undermapper for hver film basert på filmens tittel og år. Dette hjelper med å organisere filmene dine og gjør det enklere å finne dem.

- Nei, og grunnen er at Radarr er en forgrening av [Sonarr](/sonarr), der hver serie har en mappe. Denne begrensningen er et kjent problem for mange brukere og kan kanskje bli løst i en fremtidig versjon. Vær oppmerksom på at dette ikke er en enkel endring og krever en fullstendig omskriving av baksystemet.
- [GitHub-problemet for tilpassede mapper](https://github.com/Radarr/Radarr/issues/153) dekker teknisk sett denne forespørselen, men det er ingen garanti for at alle filmfiler i én mappe vil bli implementert på det tidspunktet.
- En litt "hack-ish" løsning er beskrevet nedenfor. Vær oppmerksom på at du ikke må utløse en ny skanning i Radarr, ellers vil filmen vises som manglende, og uansett vil filmen aldri bli oppgradert.
  - Bruk et tilpasset skript
    - Skriptet skal utløses ved import
    - Det skal være designet for å flytte filen når du ønsker det
    - Deretter må det kalle Radarr API-en og endre filmen til "unmonitored" (ikke overvåket).
- Hvis du vil flytte alle filmene dine fra én mappe til individuelle mapper, kan du sjekke ut artikkelen [Tips and Tricks Section => Create a Folder for Each Movie](/radarr/tips-and-tricks#creating-a-folder-for-each-movie)

## Kan jeg legge alle filmene mine i biblioteket i én mappe?

- Nei, se ovenfor.

## Hvordan oppdaterer jeg Radarr?

- Gå til Innstillinger og deretter fanen Generelt og vis avanserte innstillinger (bruk bryteren ved siden av lagre-knappen).

1. Under Oppdateringer-seksjonen endrer du grensenavnet til `master` eller `develop`
1. Lagre

*Dette vil ikke installere bitene fra den grenen umiddelbart, det vil skje under neste oppdatering.*

- ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) - (Standard/Stabil): Den er testet av brukere på utviklings- og nattlige grener, og det er ikke kjent noen større problemer. Denne versjonen vil motta oppdateringer omtrent månedlig. På GitHub er dette `master`-grenen.

- ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) - (Beta): Dette er kanten for testing. Utgitt etter testing i nattlige versjoner for å sikre at det ikke er umiddelbare problemer. Nye funksjoner og feilrettinger utgis først her etter nattlige versjoner. Den kan betraktes som halvstabil, men er fortsatt `beta`. Denne versjonen vil motta oppdateringer enten ukentlig eller annenhver uke, avhengig av utviklingen.

> **Advarsel: Du kan kanskje ikke gå tilbake til `master` etter å ha byttet til denne grenen.** På GitHub er dette et øyeblikksbilde av `develop`-grenen på et bestemt tidspunkt.
{.is-warning}

- ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) - (Alpha/Ustabil): Dette er den aller nyeste versjonen. Den utgis så snart koden er lagt til og består alle automatiserte tester. Denne bygningen er kanskje ikke brukt av oss eller andre brukere ennå. Det er ingen garanti for at den vil kjøre i noen tilfeller. Denne grenen anbefales bare for avanserte brukere. Problemer og egen undersøkelse forventes i denne grenen. ***Bruk denne grenen bare hvis du vet hva du gjør og er villig til å bli skitten på hendene for å gjenopprette en mislykket oppdatering.*** Denne versjonen oppdateres umiddelbart.

> **Advarsel: Du kan kanskje ikke gå tilbake til `master` etter å ha byttet til denne grenen.** På GitHub er dette `develop`-grenen.
{.is-danger}

- Merk: Hvis du har installert via Docker, legg til `:release`, `:latest`, `:testing` eller `:develop` på slutten av kontainermerket, avhengig av hvem som lager byggene dine.

|                                                                    | ![Current Master/Latest](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/master/changes) | ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/develop/changes) | ![Current Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://radarr.servarr.com/v1/update/nightly/changes) |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/radarr)                       | `release`                                                                                                                                                                                        | `testing`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-radarr) | `latest`                                                                                                                                                                                         | `develop`                                                                                                                                                                                         | `nightly`                                                                                                                                                                                          |

### Kan jeg oppdatere Radarr inne i Docker-kontaineren min?

- *Teknisk sett, ja.* **Men du bør absolutt ikke gjøre det.** Det er en primær filosofi i Docker. Problemer med databasen kan oppstå hvis du oppgraderer installasjonen inne i den nyeste `nightly`-versjonen, men deretter oppdaterer Docker-kontaineren selv (og kanskje nedgraderer til en eldre versjon).

### Installere en nyere versjon

#### Native

1. Gå til System og deretter fanen Oppdateringer
1. Nyere versjoner som ikke er installert ennå, vil ha en oppdateringsknapp ved siden av dem. Klikk på den knappen for å installere oppdateringen.

#### Docker

1. Hent bildet på nytt og oppdater kontaineren din

{#rename-folders}

> Den samme prosessen gjelder også for å flytte/endre filbaner for filmer. Hvis du bare oppdaterer banene i Radarr og ikke trenger å flytte filene, velger du ikke "Ja, flytt filer" i trinn 5.
{.is-info}

1. Filmer
1. Filmredigerer
1. Velg hvilke filmer som trenger å få endret mappe
1. Endre rotmappen til samme rotmappe som filmene allerede er i
1. Velg "Ja, flytt filer"

> Hvis du bruker Plex, vil dette utløse ny gjenkjenning av introduksjoner, miniatyrbilder, kapitler og forhåndsvisningsmetadata.
{.is-warning}

## Navngivning av filmfiler og mapper

- For øyeblikket krever Radarr at hver film er i en mappe med formatet `Filmnavn (År)/`, valgfritt er `_` eller `.` gyldige skilletegn. For å lette riktig identifisering av kvalitet og oppløsning under import, er det best med et filnavn som `Filmnavn (År) [Kvalitet-oppløsning].ext`, igjen er `_` eller `.` gyldige skilletegn.

  - Et nyttig verktøy for å gjøre disse endringene i samlingen din er [filebot](http://www.filebot.net/#download), som har en betalt versjon i både Apple og Windows-butikkene, men kan finnes gratis på deres gamle [SourceForge](https://sourceforge.net/projects/filebot/files/latest/download) nettsted. Det har både et GUI og CLI, så du kan bruke det du er komfortabel med. For eksempelet ovenfor, vil `{ny}` utvides til `Navn (År)` og `{vf}` gir oppløsningen som `1080p`. Det er ingenting å slutte kvalitet fra, så du kan jukse ved å bruke `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`, som vil navngi alt lavere enn 720p til `[DVD-572p]` og 720p eller høyere som `[Bluray-1080p]`.

- Se [Tips and Tricks Section => Create a Folder for Each Movie](/radarr/faq)radarr/tips-and-tricks#creating-a-folder-for-each-movie) for mer informasjon.

## Feil navngitte filmmapper

- Navngivningen av filmmapper er basert på metadataen (navn/år) på tidspunktet filmen ble lagt til. Hvis du la til en film før den ble utgitt, kan du måtte bruke trikset med å endre mappenavnet som er nevnt ovenfor for å oppdatere navngivningen av filmmappen til å gjenspeile de nye nåværende dataene.
- Selv om filmene dine allerede er i mapper, kan mappene være navngitt feil. Mappenavnet skal være `Filmnavn (År)`, og det er viktig å ha tittel og år i mappens navn akkurat nå.

  - Eksempler som vil fungere bra:
    - `/mnt/Filmer/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - `/mnt/Barnas Filmer/Frozen (2013)/Frozen (2013) [Bluray-1080p].mkv`
  - Eksempler som vil fungere, men vil kreve manuell håndtering:
    - Etter bokstaver: `/mnt/Filmer/A-D/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Etter vurdering: `/mnt/Filmer/R/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Etter sjanger: `/mnt/Filmer/Crime, Drama, Sci-Fi/A Clockwork Orange (1971)/A Clockwork Orange (1971) [Bluray-1080p].mkv`
    - Disse eksemplene vil kreve manuell håndtering når filmen legges til. Hver av eksemplene vil ha mange rotmapper, som `A-D` og `E-G` i eksempelet med første bokstav, `R` og `PG-13` i eksempelet med vurdering, og du kan gjette deg til variasjonen av sjangermapper. Når du legger til en ny film, må riktig rotmappe velges for at dette formatet skal fungere.
  - Eksempler som ikke vil fungere:
    - Enkeltmappe: `/mnt/Barnas Filmer/Frozen (2013) [Bluray-1080p].mkv`
      - For øyeblikket må filmene bare være i en mappe med navn etter filmen. Det er ingen måte å omgå dette på før utviklingsarbeidet er gjort for å legge til denne funksjonen.
    - **Film**-mappenavn fra v0.2 som inkluderer **fil**-egenskaper i **film**-mappenavnet, for eksempel ``{Movie.Title}.{Release Year}.{Quality.Full}-{MediaInfo.Simple}{`Release.Group}``, vil ikke fungere i v3.
      - Mapper er relatert til filmen og uavhengig av filen. I tillegg vil dette bryte med den planlagte støtten for flere filer per film.
      - Den andre grunnen til at det ble fjernet var at det ofte forårsaket forvirring, databasekorruptering og generelt sett var det bare halvveis implementert.
  - [Tips and Tricks Section => Create a Folder for Each Movie](/radarr/tips-and-tricks#creating-a-folder-for-each-movie) er en flott kilde for å sikre at fil- og mappstrukturen din fungerer bra.

## Kan jeg deaktivere oppdatering av filmer?

- Nei, og du bør heller ikke gjøre det gjennom noen SQL-hacking. Oppdateringsoppgaven for filmer spør den oppstrøms Servarr-proxyen og sjekker om metadataen for hver film (ID-er, rollebesetning, sammendrag, rangering, oversettelser, alternative titler osv.) har blitt oppdatert sammenlignet med det som er i Radarr for øyeblikket. Hvis det er nødvendig, vil den deretter oppdatere de aktuelle filmene.
- En vanlig klage er at oppdateringsoppgaven forårsaker høy I/O-bruk.
- Hovedinnstillingen er "Skann filmmappe etter oppdatering". Hvis disk-I/O-bruken øker under en oppdatering, kan du endre skanneinnstillingen til `Manuell`.
  - Ikke endre dette til `Aldri` med mindre alle endringer i biblioteket ditt (nye filmer, oppgraderinger, slettinger osv.) gjøres gjennom Radarr.
  - Hvis du sletter filmfiler manuelt eller via Plex eller et annet tredjepartsprogram, ikke sett dette til `Aldri`.
- Den andre innstillingen som kan endres, er "Analyser videofiler", som anbefales å være aktivert hvis du bruker tdarr eller på annen måte endrer filene dine eksternt. Hvis du ikke gjør det, kan du trygt deaktivere "Analyser videofiler" for å redusere noe I/O.

## Hvordan kan jeg be om en funksjon for Radarr?

- Dette er enkelt [klikk her](https://github.com/Radarr/Radarr/issues)

## Hjelp, Mac-en min sier at Radarr ikke kan åpnes fordi utvikleren ikke kan verifiseres

- Dette er enkelt, se denne lenken for mer informasjon [her](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac) ![Utvikler kan ikke verifiseres](developer-cannot-be-verified.png "Utvikler kan ikke verifiseres")
- Alternativt kan du måtte signere Radarr selv med `codesign --force --deep -s - /Applications/Radarr.app && xattr -rd com.apple.quarantine`

## Hjelp, Mac-en min sier at Radarr.app er skadet og kan ikke åpnes

- Det skyldes enten en korrupt nedlasting, så prøv igjen, eller [sikkerhetsproblemer, se denne relaterte FAQ-innføringen.](#hjelp-mac-en-min-sier-at-radarr-ikke-kan-åpnes-fordi-utvikleren-ikke-kan-verifiseres)

## Jeg får en feilmelding: Database disk image is malformed

> \* For Radarr-brukere som opplever dette etter oppgradering til v4.X-versjoner. v4-versjoner gjør flere omfattende migreringer fordi hvis databasen din hadde tidligere korrupte steder (som kanskje ikke var oppdagbare tidligere ved kjøring av Radarr), vil migreringen mislykkes. Dette vil føre til at Radarr ikke kan starte. Det er sannsynlig at alle sikkerhetskopiene dine også er korrupte, så det å gjenopprette dem vil sannsynligvis ikke løse problemet.
> \* Hvis den migrerte databasen ikke kan åpnes eller ikke kan gjenopprettes, må du lage en kopi av databasen fra en nylig sikkerhetskopi og bruke databasens gjenopprettingsprosess på den filen, og deretter prøve å starte Radarr med den gjenopprettede sikkerhetskopifilen. Den skal da migrere uten problemer.
{.is-warning}

- **Feilene "Error creating log database" indikerer problemer med logs.db**
  - Dette kan løses raskt ved å endre navn på eller fjerne databasen. Logs-databasen inneholder uviktig informasjon om kommandohistorikk og oppdateringsinstallasjonshistorikk, samt Info-, Warn- og Error-oppføringer.
- **Feilene "Error creating main database" eller generelle "database disk image is malformed" uten spesifisert database indikerer problemer med radarr.db**
  - Fortsett med trinnene nedenfor
- Dette betyr at SQLite-databasen som lagrer mesteparten av informasjonen for Radarr, er korrupt. Du har muligheten til å prøve (en) sikkerhetskopi(er), prøve å gjenopprette den eksisterende databasen, prøve å gjenopprette sikkerhetskopiene, eller hvis alt annet mislykkes, begynne på nytt med en helt ny database.
- Denne feilen kan vises hvis databasefilen ikke kan skrives av brukeren/gruppen \*Arr kjører som. Tillatelser som årsak vil sannsynligvis bare være et problem for nye installasjoner, migrerte installasjoner til en ny server, hvis du nylig har endret tillatelsene for appdata-katalogen din, eller hvis du har endret brukeren og gruppen \*Arr kjører som.
- Det beste og første alternativet ditt er å [prøve å gjenopprette fra en sikkerhetskopi](#hvordan-sikkerhetskopierer-gjenoppretter-jeg-radarr). Imidlertid er det svært usannsynlig at sikkerhetskopien i seg selv vil fungere hvis du mottar denne feilen etter oppgradering til v4, og du må prøve de andre nevnte gjenopprettingsmetodene.
- Du kan også prøve å gjenopprette databasen din. Dette er vanligvis det eneste alternativet når dette problemet oppstår etter en oppdatering. Prøv [sqlite3 `.recover`-kommandoen](/useful-tools#recovering-a-corrupt-db)
  - Hvis sqlite ikke har `.recover` eller du ønsker en mer GUI-vennlig måte (f.eks. Windows), følg [instruksjonene våre på denne wikien.](/useful-tools#recovering-a-corrupt-db-ui)
- En annen mulig årsak til at du får en feil med databasen din, er at du plasserer databasen din på en nettverksstasjon (nfs eller smb eller noe annet som ikke er lokalt). **SQLite er designet for situasjoner der data og program eksisterer på samme maskin.** Derfor må \*Arr AppData-mappen din (/config-monteringspunkt for Docker) være på lokal lagring. [SQLite og nettverksstasjoner fungerer ikke bra sammen og vil til slutt føre til en korrupt database](https://www.sqlite.org/draft/useovernet.html).
- Hvis du bruker mergerFS, må du fjerne `direct_io` siden SQLite bruker mmap, som ikke støttes av `direct_io`, som forklart i mergerFS [dokumentasjonen her](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jeg bruker Radarr på en Mac, og den sluttet plutselig å fungere. Hva skjedde?

- Mest sannsynlig skyldes dette en MacOS-feil som førte til at en av databasene ble korrupt.
- Se den forrige oppføringen om at databasen er korrupt.
- Prøv deretter å starte og se om det fungerer. Hvis det ikke fungerer, trenger du ytterligere støtte. Legg ut i [subredditen vår /r/radarr](http://reddit.com/r/radarr) eller bli med på [discord-serveren vår](https://radarr.video/discord) for hjelp.

## Hvorfor kan ikke Radarr se filene mine på en ekstern server?

- For alle operativsystemer må du sørge for at brukeren/gruppen du kjører \*Arr som, har lese- og skrivetilgang til den monterte disken.
- For Linux, sørg for:
  - Hvis du bruker en NFS-montering, må du sørge for at `nolock` er aktivert for monteringen din.
  - Hvis du bruker en SMB-montering, må du sørge for at `nobrl` er aktivert for monteringen din.
- For Windows: Kort sagt, brukeren \*Arr kjører som (hvis tjeneste) eller under (hvis bakgrunnsprogram) kan ikke få tilgang til filbanen på den eksterne serveren. Dette kan skyldes forskjellige årsaker, men det vanligste er at \*Arr kjører som en tjeneste, noe som forårsaker problemene som beskrives nedenfor.

### Radarr kjører som standard under LocalService-kontoen, som ikke har tilgang til beskyttede eksterne filområder

- Kjør Radarr-tjenesten som en annen bruker som har tilgang til den delte mappen
- Åpne vinduet Administrative Tools \> Services på Windows-serveren din.
- Stopp Radarr-tjenesten.
- Åpne dialogboksen Properties \> Log On.
- Endre brukerkontoen for tjenesten til målbrukerkontoen.
- Kjør Radarr.exe ved hjelp av Startup-mappen

### Du bruker en kartlagt nettverksstasjon (ikke en UNC-bane)

- Endre banene dine til UNC-baner (`\\server\share`)
- Kjør Radarr.exe via Startup-mappen

## Hvordan kan jeg bytte fra Windows-tjenesten til et bakgrunnsprogram?

1. Stopp Radarr
1. Kjør serviceuninstall.exe som er i Radarr-mappen
1. Kjør `Radarr.exe` som administrator én gang for å gi den riktige tillatelser og åpne brannmuren. Når det er fullført, kan du lukke det og kjøre det normalt.
1. (Valgfritt) Legg til en snarvei til .exe-filen i oppstartsprogrammappen for å starte automatisk ved oppstart.

## Hjelp, jeg har låst meg ute

{#help-i-have-forgotten-my-password}

For å deaktivere autentisering (for å tilbakestille glemt brukernavn eller passord), må du redigere `config.xml`, som vil være inne i [Radarr Appdata-katalogen](/radarr/appdata-directory)

1. Åpne config.xml i en tekstredigerer
1. Finn linjen for autentiseringsmetode, som vil være
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Endre linjen `AuthenticationMethod` til `<AuthenticationMethod>None</AuthenticationMethod>`
1. Start Radarr på nytt
1. Radarr vil nå være tilgjengelig uten passord, du bør gå til `Innstillinger: Generelt` i brukergrensesnittet og angi brukernavnet og passordet ditt

## Hvordan kan jeg forhindre at nettleseren åpnes ved oppstart?

Avhengig av operativsystemet ditt, er det flere mulige måter.

- I `Innstillinger` => `Generelt` på noen operativsystemer er det en avmerkingsboks for å åpne nettleseren ved oppstart.
- Når du starter Radarr, kan du legge til `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumentene.
- Stopp Radarr og rediger config.xml-filen, og endre `<LaunchBrowser>True</LaunchBrowser>` til `<LaunchBrowser>False</LaunchBrowser>`.

## Rar grensesnittproblemer

- Hvis du opplever rare grensesnittproblemer som at bibliotekssiden ikke viser noe eller at en bestemt visning eller sortering ikke fungerer, kan du prøve å se i en Chrome Inkognitovindu eller Firefox Privat vindu. Hvis det fungerer fint der, kan du tømme nettleserens hurtigbuffer og informasjonskapsler for din spesifikke IP/domene. For mer informasjon, se artikkelen [Clear Cache Cookies and Local Storage](/useful-tools#clearing-cookies-and-local-storage) på wikien vår.

## Webgrensesnittet lastes bare på localhost på Windows

- Hvis du bare kan nå webgrensesnittet ditt på <http://localhost:7878/> eller <http://127.0.0.1:7878/>, må du kjøre som administrator minst én gang.

## Tillatelser

- Radarr må flytte filer fra der nedlasteren legger dem til den endelige plasseringen, så dette betyr at den må lese/skrive til både kilde- og destinasjonsmappen og filene.
- På Linux, der beste praksis er at tjenester kjører som sin egen bruker, vil dette sannsynligvis bety å bruke en delt gruppe og sette mappe tillatelser til `775` og filer til `664` både i nedlasteren din og . I umask-notasjon vil det være `002`.

## System og logger lastes inn i det uendelige

- Det er easy-privacy-blokkeringslisten. De blokkerer i utgangspunktet alle URL-er med /api/log? i dem. Se gjennom listen og vurder om det å blokkere alle URL-ene der er en fornuftig idé, det er dusinvis av URL-er der som potensielt bryter nettsteder. Du valgte det i annonseblokkereren din. En enkel løsning er å legge domenet Radarr kjører på, til i hvitelisten. Men jeg anbefaler likevel å sjekke listen.

## Pakk ut torrenter

- De fleste torrentklienter har ikke automatisk håndtering av komprimerte arkiver som deres Usenet-motparter. Vi anbefaler [unpackerr](https://github.com/unpackerr/unpackerr).

## uTorrent fungerer ikke lenger

- Sørg for at Web UI er aktivert
- Sørg for at den alternative lytteporten (Avansert => Web UI) ikke er den samme som lytteporten (Tilkoblinger)
- Vi anbefaler å endre den alternative lytteporten for Web UI slik at den ikke påvirker portvideresendingen for tilkoblinger.

## Jeg fikk en popup-melding som sa at config.xml var korrupt, hva nå?

- Radarr kunne ikke lese konfigurasjonsfilen ved oppstart fordi den ble på en eller annen måte korrupt. For å komme tilbake på nett, må du slette `.xml` i [appdata-katalogen](/radarr/appdata-directory), når den er slettet, starter den på standardporten (7878), og du bør nå konfigurere eventuelle innstillinger du konfigurerte på siden for generelle innstillinger.

## Ugyldig sertifikat og andre HTTPS- eller SSL-problemer

- Din nedlastingsklient sluttet å fungere, og du får en feilmelding som `Localhost is an invalid certificate`?
  - Radarr validerer SSL-sertifikater. Hvis det ikke er satt opp et SSL-sertifikat i nedlastingsklienten, eller hvis du bruker et selvsignert HTTPS-sertifikat uten at CA-sertifikatet er lagt til i lokal sertifikatbutikk, vil Radarr nekte å koble til. Gratis, riktig signerte sertifikater er tilgjengelige fra [let's encrypt](https://letsencrypt.org/).
  - Hvis nedlastingsklienten og Radarr kjører på samme maskin, er det ingen grunn til å bruke HTTPS, så den enkleste løsningen er å deaktivere SSL for tilkoblingen. De fleste vil være enige i at det heller ikke er nødvendig i et lokalt nettverk. Det er mulig å deaktivere sertifikatvalidering i avanserte innstillinger hvis du ønsker å beholde en usikker SSL-konfigurasjon.

## VPN-er, Jackett og \*ARR-ene

- Med mindre du er i et undertrykkende land som Kina, Australia eller Sør-Afrika, er det vanligvis bare torrentklienten din som trenger å være bak en VPN. Fordi VPN-tilknytningspunktet deles av mange brukere, kan du oppleve begrensninger i hastigheten, DDOS-beskyttelse og IP-blokkering fra ulike tjenester som hver programvare bruker.
- Med andre ord kan det å plassere \*ARR-ene (Lidarr, Prowlarr, Radarr, Readarr og Lidarr) bak en VPN gjøre applikasjonene ubrukelige i noen tilfeller på grunn av at tjenestene ikke er tilgjengelige.

> **For å være tydelig, det er ikke et spørsmål om VPN-er vil forårsake problemer med \*ARR-ene, men når: bildeleverandører vil blokkere deg, og Cloudflare er foran de fleste \*ARR-servere (oppdateringer, metadata osv.) og kan også blokkere deg**
{.is-warning}

- **Mange private trackere vil utestenge deg hvis du bruker eller får tilgang til dem (f.eks. ved å bruke Jackett eller Prowlarr) via en VPN.**

### Bruk av VPN

- Hvis en VPN er nødvendig og Docker brukes, anbefales det å bruke Hotio eller Binhex's Download Client + VPN-containere.
- Hvis en VPN er nødvendig og Docker ikke brukes, må VPN-klienten ***støtte delt tunnelering slik at bare de nødvendige (nedlastingsklient) appene er bak VPN-en.
- Mange problemer med å få tilgang til trackere kan løses ved å bruke Googles eller Cloudflares DNS-servere i stedet for ISP-ens DNS-servere.
- I noen tilfeller (f.eks. britiske internettleverandører) kan du trenge å plassere torrent-nedlastingsklienten bak en VPN og Jackett/Prowlarr som følger:
  - Plasser Jackett bak VPN-en og sørg for at delt tunnelering tillater lokal tilgang.
  - For Prowlarr konfigurerer du VPN-klienten til å gi en proxy og legger til proxyen i Innstillinger => Indekser. Gi proxyen en tagg, og gi eventuelle indekser som trenger å bruke den samme taggen.
    - Hvis det absolutt er nødvendig, og hvis VPN-en din ikke gir en måte å opprette en proxy på, kan du plassere Prowlarr bak VPN-en og sørge for at delt tunnelering tillater lokal tilgang.

# Vanlige problemer med søk og nedlasting i Radarr

## Hvorfor kan jeg ikke legge til en ny film i Radarr?

{#why-cant-i-add-a-new-movie-to-radarr}

- Radarr bruker [The Movie Database (TMDb)](http://themoviedb.org) for filminformasjon og bilder som fanart, bannere og bakgrunner. Generelt sett er det noen grunner til at du kanskje ikke kan legge til en film:
  - TMDb liker ikke at spesialtegn brukes når du søker etter filmer via API-en (som Radarr bruker), så prøv å søke med et oversatt navn og/eller uten spesialtegn.
  - Du kan også legge til ved hjelp av TMDb-ID eller, hvis TMDb har det, IMDb-ID-en.
  - Filmen er ikke lagt til i TMDb ennå, følg deres [veiledning](https://www.themoviedb.org/bible/new_content#59f7933c9251413e93000006) for å få den lagt til.

## Jackett viser flere resultater enn ved manuell søk

- Dette skyldes vanligvis at du søker i Jackett på en annen måte enn du gjør manuelt. Se vår [feilsøkingsartikkel](/radarr/troubleshooting) for mer informasjon.

## Hvordan bestemmer Radarr året for en film?

- Radarr henter metadata fra [TMDb](https://www.themoviedb.org/)
- Radarr bruker året for den eldste **kinoutgivelsen** og den eldste **premiere**-datoen for å finne riktig film.
  - Merk at hvis det ikke finnes en kinoutgivelse, vil logikken falle tilbake på den eldste fysiske eller digitale utgivelsesdatoen.
- Hvis en film mangler en digital, fysisk, kinoutgivelse eller premiere-dato, bør TMDb oppdateres.
- [TMDb's Contribution Bible](https://www.themoviedb.org/bible/movie/59f3b16d9251414f20000009#59f73d3c9251416e71000013) nevner følgende om utgivelsestypene deres.
  - **Premiere** - En premierevisning kan være en festivalvisning (f.eks. TIFF) eller en premierehendelse med skuespillere og mannskap i en storby (f.eks. LA, London, Toronto).
  - **Kinoutgivelse** - Kan brukes for den opprinnelige utgivelsen og eventuelle påfølgende offisielle utgivelser. Brukes for bred eller mettet utgivelse. I USA regnes 600-1 999 skjermer som bred utgivelse, og 2000+ regnes som mettet utgivelse.
  - **Kinoutgivelse (begrenset)** - Begrenset kinoutgivelse er en distribusjonsstrategi for filmer der en ny film slippes i noen få kinoer over hele landet, vanligvis i større byområder. I USA er antallet kinoer færre enn 600.
  - **Fysisk** - Inkluderer alle VHS-, DVD- og Blu-ray-utgivelser.
  - **Digital** - Alle relevante utgivelser kan legges til, inkludert strømmetjenester, VOD-utleie eller -kjøp. Digitale visninger, inkludert online filmfestivaler og virtuelle kinoutgivelser, regnes også som digitale utgivelser.

## Hvordan håndterer Radarr utenlandske filmer eller utenlandske titler?

> [TRaSH's Custom Format Language Guide](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/#how-to-setup-language-custom-formats) kan være nyttig for å hjelpe deg med å få filmer på det språket du ønsker.{.is-info}

> Fra og med 2023-02-12 vil Radarrs metadata-cache begynne å vurdere en films opprinnelige språk som TMDb's talt språk hvis og bare hvis det bare finnes ett talt språk for filmen på TMDb; ellers vil filmens opprinnelige TMDb-språk bli brukt.
{.is-warning}

## Søk etter ID-er

- **Indekser som støtter søk basert på ID** - Søk på indekser og trackere som støtter søk basert på ID (TMDbId, IMDbId osv.) - som mange Usenet-indekser og mange private torrent-trackere - tekstforespørsler brukes ikke hvis det returneres resultater for et ID-basert søk. Hvis det returneres resultater, vil det ikke falle tilbake til et navn-/tekstsøk. Hvis du mangler resultater fra indeksen din, skyldes det at utgivelsen(e) er knyttet til feil film-ID.
  - Utgivelsens språk kan også hentes fra indeksen eller trackernes utgivelsesspråk i resultatet hvis det er oppgitt, i stedet for å parses fra navnet.

## Tekstsøk

- **Indekser som ikke støtter ID-baserte søk eller ID-baserte søk uten resultater** - Søk vil bruke filmens opprinnelige tittel, engelsk tittel og oversatt tittel fra [hvilke språk du har valgt i filmens kvalitetsprofil og eventuelle tilpassede formater med poengsum i kvalitetsprofilen større enn null](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Parsing (dvs. importering) ser etter en match i alle oversettelser og alternative titler.
  - Utgivelsens språk kan også hentes fra indeksen eller trackernes utgivelsesspråk i resultatet hvis det er oppgitt, i stedet for å parses fra navnet.

## Få utenlandske filmer

- For å få en film på et fremmed språk, sett filmens språk i kvalitetsprofilen til Original (Filmens opprinnelige språk\*), et spesifikt språk for den profilen eller `Any`, og opprett og gi en poengsum større enn 0 [Tilpassede formater med språkbetingelser for å bestemme hvilket språk som skal lastes ned - se TRaSH's Guide for detaljer](https://trash-guides.info/Radarr/Tips/How-to-setup-language-custom-formats/).
- Merk at dette ikke inkluderer noen indeksspråk som er konfigurert som `multi` i indeksens innstillinger.
  - Merk at fra [Radarr v4.1](https://github.com/Radarr/Radarr/commit/ad8629fac981217f5a4a5068da968c29d9ee634c) antas det ikke lenger at `multi` inkluderer engelsk.
  - Brukere kan justere innstillingene per indeks for å definere hvilket språk `multi` indikerer.

## Hvordan håndterer Radarr "multi" i navn?

- Med Radarr v4.1+ antar Radarr at
`multi` bare er filmens språk og **IKKE** engelsk som i tidligere versjoner.
  - Brukere kan justere innstillingene per indeks for å definere hvilket språk `multi` indikerer.
- Merk at `multi`-definisjoner bare hjelper for utgivelsesparsing og ikke for utenlandske titler eller filmsøk.

## Hjelp, filmen er lagt til, men ikke søkt etter

- Radarr søker ikke *aktivt* etter manglende filmer automatisk. I stedet gjøres det en periodisk forespørsel om nye innlegg til alle indekser som er konfigurert for RSS. Når en ønsket film eller en film som ikke oppfyller kuttet dukker opp i den listen, blir den lastet ned. Dette betyr at en film ikke blir lastet ned før den blir lagt ut (eller lagt ut på nytt).
- Hvis du legger til en film som du vil ha nå, er det beste alternativet å merke av for "Start søk etter manglende film" -boksen til venstre for *Legg til film* (**1**) -knappen. Du kan også gå til siden for en film du har lagt til og klikke på forstørrelsesglasset "Søk" (**2**) -knappen eller bruke Wanted-visningen for å søke etter manglende eller kuttet uoppfylte filmer.

  - Legg til og søk etter film når du legger til en film
![addmovie-add-and-search.png](/assets/radarr/addmovie-add-and-search.png)
  - Søk etter en eksisterende film
![searchmovie-movie-page.png](/assets/radarr/searchmovie-movie-page.png)

## Jacketts /all-endepunkt

{#jackett-all-endpoint}

- Jackett `/all`-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nødvendig å legge til hver tracker individuelt. Alternativt kan du vurdere Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

- **Oppdatering 1. januar 2022: Jackett `/all`-endepunktet støttes ikke lenger (dvs. advarsler vil vises) fra og med 4.0.0.5730 på grunn av at det bare skaper problemer.**

- Jackett /all-endepunktet er praktisk, men det er den eneste fordelen. Alt annet kan føre til problemer, så det er nå nødvendig å legge til hver tracker individuelt.
- [Selv Jacketts utviklere sier at det bør unngås og ikke bør brukes.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Bruk av /all-endepunktet har ingen fordeler, bare ulemper:
  - du mister kontrollen over innstillingene for hver enkelt indeks (kategorier, søkemåter osv.)
  - blanding av søkemåter (IMDB, søk, osv.) kan føre til resultater av lav kvalitet
  - indeksspesifikke kategorier (\>= 100000) kan ikke brukes.
  - treg indekser vil bremse ned den totale resultatet
  - totalt antall resultater er begrenset til 1000
  - hvis en av trackerne i /all returnerer en feil, vil \*Arr deaktivere den, og nå får du ingen resultater.

### Løsninger for Jackett /all

- Legg til hver tracker i Jackett manuelt som en indekser i \*Arr
- Sjekk ut [Prowlarr](/prowlarr), som kan synkronisere indekser med \*Arr og er utviklet av Lidarr/Radarr/Readarr-utviklingsteamet.
- Sjekk ut [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekser med \*Arr. Men ikke bruk deres enkeltstående aggregerte endepunkt, og bruk `multi` hvis synkronisering skal brukes.

## Hvorfor er det to filer? | Hvorfor er det en fil igjen i nedlastinger?

Dette er forventet. Med en konfigurasjon som støtter [hardlinker](https://trash-guides.info/hardlinks), vil ikke dobbelt plass bli brukt. Her er hvordan torrentprosessen fungerer.

1. Radarr sender en nedlastingsforespørsel til klienten din og knytter den til etiketten eller kategorinavnet du har konfigurert i innstillingene for nedlastingsklienten. Eksempler: filmer, tv, serier, musikk, osv.
1. Radarr overvåker de aktive nedlastingene i nedlastingsklienten som bruker det kategorinavnet. Denne overvåkingen skjer via nedlastingsklientens API.
1. Fullførte filer blir liggende på sin opprinnelige plassering slik at du kan seede filen (forhold eller tid kan justeres i nedlastingsklienten eller fra Radarr under den spesifikke nedlastingsklienten). Når filene importeres til mediamappen din, vil de bli hardlinket hvis det støttes av oppsettet ditt, eller kopiert hvis hardlinker ikke støttes.
1. Hvis alternativet "Behandling av fullførte nedlastinger - Fjern fullførte" er aktivert i Radarrs innstillinger, vil Radarr slette den opprinnelige filen og torrenten fra nedlastingsklienten, men bare hvis nedlastingsklienten rapporterer at seeding er fullført og torrenten er stoppet (dvs. satt på pause). Se [TRaSH's veiledninger for nedlastingsklienter](https://trash-guides.info/Downloaders/) for hvordan du konfigurerer nedlastingsklienten optimalt.

> Hardlinker er aktivert som standard. [En hardlink vil ikke bruke ekstra diskplass.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringspunktene må være de samme for mappen der fullførte nedlastinger lagres og mediebiblioteket ditt. Hvis opprettelsen av hardlinker mislykkes eller oppsettet ditt ikke støtter hardlinker, vil Radarr falle tilbake og kopiere filen.
{.is-info}

## Hvorfor fungerer ikke Radarr bak en omvendt proxy?

- Fra og med v3 har Radarr byttet til .NET og en ny webserver. For at SignalR skal fungere, for at knappene i brukergrensesnittet skal fungere, for at databaseendringer skal ta effekt og andre ting, kreves følgende tillegg til location-blokken for Radarr:

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $http_connection;
```

- Pass på at du **ikke** inkluderer `proxy_set_header Connection "Upgrade";` som foreslått av nginx-dokumentasjonen. **Dette VIL IKKE fungere**
- [Se dette ASP.NET Core-problemet](https://github.com/aspnet/AspNetCore/issues/17081)
- Hvis du bruker en CDN som Cloudflare, må du sørge for at websockets er aktivert for å tillate websocket-tilkoblinger.
- Hvis du opplever uventede omdirigeringer, må du sørge for at vertshodet ditt videresendes.