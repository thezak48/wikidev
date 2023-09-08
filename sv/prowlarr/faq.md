---
title: Prowlarr FAQ
description: Prowlarr FAQ
published: true
date: 2023-08-28T19:29:30.585Z
tags: prowlarr, faq
editor: markdown
dateCreated: 2021-11-03T03:01:18.079Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
  - [Tvingad autentisering](#tvingad-autentisering)
  - [Hur återställer jag statistik?](#hur-återställer-jag-statistik)
  - [Kategori saknas eller är inte tillgänglig](#kategori-saknas-eller-är-inte-tillgänglig)
  - [Kan jag lägga till vilken (generisk) Torznab- eller Newznab-indexer som helst?](#kan-jag-lägga-till-vilken-generisk-torznab-eller-newznab-indexer-som-helst)
  - [Kan jag lägga till vilken (generisk) Torrent RSS-feed som helst?](#kan-jag-lägga-till-vilken-generisk-torrent-rss-feed-som-helst)
  - [Kan jag använda flaresolverr-indexers?](#kan-jag-använda-flaresolverr-indexers)
  - [Hur kan jag lägga till en indexer som är nere eller inte fungerar?](#hur-kan-jag-lägga-till-en-indexer-som-är-nere-eller-inte-fungerar)
  - [Prowlarr synkroniseras inte med Sonarr](#prowlarr-synkroniseras-inte-med-sonarr)
  - [Prowlarr synkroniseras inte med X Indexer till App](#prowlarr-synkroniseras-inte-med-x-indexer-till-app)
  - [Vilka \*Arr Indexer-inställningar jämförs för fullständig synkronisering av appen?](#vilka-arr-indexer-inställningar-jämförs-för-fullständig-synkronisering-av-appen)
  - [Hur uppdaterar jag Prowlarr?](#hur-uppdaterar-jag-prowlarr)
    - [Kan jag uppdatera Prowlarr inuti min Docker-container?](#kan-jag-uppdatera-prowlarr-inuti-min-docker-container)
    - [Installation av en nyare version](#installation-av-en-nyare-version)
      - [Lokal installation](#lokal-installation)
      - [Docker](#docker)
  - [Kan jag växla från `nightly` tillbaka till `develop`?](#kan-jag-växla-från-nightly-tillbaka-till-develop)
  - [Kan jag växla mellan grenar?](#kan-jag-växla-mellan-grenar)
  - [Hjälp, min Mac säger att Prowlarr inte kan öppnas eftersom utvecklaren inte kan verifieras](#hjälp-min-mac-säger-att-prowlarr-inte-kan-öppnas-eftersom-utvecklaren-inte-kan-verifieras)
  - [Hjälp, min Mac säger att Prowlarr.app är skadad och kan inte öppnas](#hjälp-min-mac-säger-att-prowlarrapp-är-skadad-och-kan-inte-öppnas)
  - [Hur begär jag en funktion för Prowlarr?](#hur-begär-jag-en-funktion-för-prowlarr)
  - [Jag får ett felmeddelande: Databasens diskavbildning är skadad](#jag-får-ett-felmeddelande-databasens-diskavbildning-är-skadad)
  - [Jag använder Prowlarr på en Mac och det slutade plötsligt fungera. Vad har hänt?](#jag-använder-prowlarr-på-en-mac-och-det-slutade-plötsligt-fungera-vad-har-hänt)
  - [Hur byter jag från Windows-tjänsten till en fältapp?](#hur-byter-jag-från-windows-tjänsten-till-en-fältapp)
  - [Hur säkerhetskopierar/återställer jag Prowlarr?](#hur-säkerhetskopieraråterställer-jag-prowlarr)
    - [Säkerhetskopiering av Prowlarr](#säkerhetskopiering-av-prowlarr)
      - [Använda inbyggd säkerhetskopiering](#använda-inbyggd-säkerhetskopiering)
      - [Använda filsystemet direkt](#använda-filsystemet-direkt)
    - [Återställning från säkerhetskopia](#återställning-från-säkerhetskopia)
      - [Använda zip-säkerhetskopia](#använda-zip-säkerhetskopia)
      - [Använda filsystemets säkerhetskopia](#använda-filsystemets-säkerhetskopia)
      - [Återställning av filsystemet på Synology NAS](#återställning-av-filsystemet-på-synology-nas)
  - [WebUI laddas bara på localhost på Windows](#webui-laddas-bara-på-localhost-på-windows)
  - [Hitta kakor](#hitta-kakor)
  - [uTorrent fungerar inte längre](#utorrent-fungerar-inte-längre)
  - [Jag fick ett popup-fönster som sa att config.xml var korrupt, vad gör jag nu?](#jag-fick-ett-popup-fönster-som-sa-att-configxml-var-korrupt-vad-gör-jag-nu)
  - [Ogiltigt certifikat och andra HTTPS- eller SSL-problem](#ogiltigt-certifikat-och-andra-https-eller-ssl-problem)
  - [Hjälp, jag har låst mig själv](#hjälp-jag-har-låst-mig-själv)
  - [Konstiga UI-problem](#konstiga-ui-problem)
  - [VPN, Prowlarr och \*ARRs](#vpn-prowlarr-och-arrs)
  - [Hur stoppar jag webbläsaren från att starta vid uppstart?](#hur-stoppar-jag-webbläsaren-från-att-starta-vid-uppstart)
  - [Kan jag enkelt lägga till alla indexers på en gång?](#kan-jag-enkelt-lägga-till-alla-indexers-på-en-gång)

## Tvingad autentisering

Om Prowlarr är exponerad så att användargränssnittet kan nås utanför ditt lokala nätverk bör du ha någon form av autentiseringsmetod aktiverad för att komma åt användargränssnittet. Detta krävs också alltmer av spårare och indexers.

Från och med Prowlarr v1 är autentisering obligatorisk.

### Autentiseringsmetod

- `Basic` (webbläsarpopup) - När du kommer åt din Prowlarr visas en liten popup där du kan ange användarnamn och lösenord.
- `Forms` (inloggningssida) - Denna metod har en bekant inloggningsskärm, liknande andra webbplatser, där du kan logga in på din Prowlarr.
- `External` - Konfigureras endast via konfigurationsfilen
  - Om du använder **extern autentisering** som Authelia, Authetik, NGINX Basic auth, etc. kan du undvika dubbel autentisering genom att stänga av appen, ange `<AuthenticationMethod>External</AuthenticationMethod>` i [konfigurationsfilen](/prowlarr/appdata-directory) och starta om appen. **Observera att flera `AuthenticationMethod`-poster i filen inte stöds och endast det översta värdet används**

### Obligatorisk autentisering

- Om du inte exponerar appen externt och/eller inte vill ha autentisering krävd för lokal (t.ex. LAN) åtkomst kan du ändra i Inställningar => Allmänt => Autentisering krävs till `Inaktiverad för lokala adresser`
  - Motsvarande i konfigurationsfilen är `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`
  
## Hur återställer jag statistik?

- För att återställa din statistik och rensa historiken gör följande:

1. Historik => Alternativ
1. Ställ in Historikrensning till `1`. Detta behåller endast historiken och statistiken fram till igår.
1. Gå till System => Uppgifter
1. Kör uppgiften "Rensa historik"
1. Kör uppgiften "Städning"
1. Återgå till Historik => Alternativ
1. Ställ in Historikrensning till önskad period för att behålla historik och statistik

## Kategori saknas eller är inte tillgänglig

- Observera att anpassade/ikke-standardiserade indexer-specifika kategorier mappas till standardkategorier, så sökningar i standardkategorier kommer att inkludera alla anpassade kategorier. Granska din specifika indexers kategorimappningsdefinition för detaljer.

## Kan jag lägga till vilken (generisk) Torrent RSS-feed som helst?

Ja. Använd "TorrentRSS".

Följande attribut är obligatoriska:

- guid
- title
- infohash
- enclosure eller link

Följande attribut är valfria, men rekommenderade:

- size
- pubDate

## Kan jag lägga till vilken (generisk) Torznab- eller Newznab-indexer som helst?

- Ja.
- Gå till `Indexers` => `Lägg till indexer` (<kb>+</kb>) => `Generisk Torznab` eller `Generisk Newznab`

## Kan jag använda flaresolverr-indexers?

- Ja.

1. Konfigurera din flaresolverr-instans genom att lägga till den som en proxy i [Inställningar => Indexers](/prowlarr/settings#indexer-proxies)
1. Lägg till en tagg på den skapade flaresovlerr-proxyn
1. Lägg till samma tagg på din [Indexer](/prowlarr/indexers)

> Taggarna måste matcha och Cloudflare måste upptäckas för att Flaresolverr ska användas. En Flaresolverr-proxy inaktiveras om inga taggar används.
{.is-warning}

> [Se TRaSH's guider om "Hur man konfigurerar Flaresolverr"](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/) för mer information
{.is-info}

## Hur kan jag lägga till en indexer som är nere eller inte fungerar?

- Följ de vanliga stegen för att lägga till indexern, men notera följande ändringar.
- Avmarkera (inaktivera) rutan "Aktiverad"
- Klicka på "Spara"
- Klicka på "Spara" igen för att tvinga en sparning
- Redigera indexern (skiftnyckelikonen)
- Markera (aktivera) rutan "Aktiverad"
- Klicka på "Spara"
- Klicka på "Spara" igen för att tvinga en sparning

## Prowlarr synkroniseras inte med Sonarr

- Prowlarr stöder endast Sonarr v3+
- Sonarr v2 (tidigare nzbdrone) stöds inte av Prowlarr eller allmänt och har varit slutet av livet sedan mars 2021

## Prowlarr synkroniseras inte med X Indexer till App

- Prowlarr synkroniseras endast om "Lägg till och ta bort" eller "Fullständig synkronisering" är aktiverat för appen.
- Endast i fall där en app och indexer har matchande taggar eller inga taggar alls kommer en indexer att synkroniseras med en app.
- Indexers synkroniseras baserat på de funktioner/kategorier de påstår sig stödja.
  - Om en indexer endast stöder TV-kategorier kommer den inte att synkroniseras med Lidarr, Radarr och Readarr.
- En given indexer synkroniseras endast med Sonarr om "Stödda" kategorier kan väljas som en avancerad inställning för varje app.
- Indexers kommer inte att försöka synkroniseras om de specifika kategorierna som stöds av indexeraren inte är valda i Inställningar => Applikation => {App} => Synkronisera kategorier (avancerade inställningar) och loggarna kommer inte att visa någon indikation på ett synkroniseringsförsök.
- Den vanligaste orsaken till detta är att \*Arrs bara accepterar indexers vars testförfrågningar returnerar resultat som innehåller minst en av de konfigurerade kategorierna. Med andra ord, om du synkroniserar med en app och indexerarens tomma förfrågan inte returnerar resultat med något släpp inom de kategorier som är konfigurerade för appen kommer den inte att kunna lägga till indexeraren i \*Arr.
- Det specifika felet kommer att vara en HTTP 400 från \*Arr som anger `Query successful, but no results in the configured categories were returned from your indexer. This may be an issue with the indexer or your indexer category settings.` (Förfrågan lyckades, men inga resultat i de konfigurerade kategorierna returnerades från din indexer. Detta kan vara ett problem med indexeraren eller dina indexerarkategorinställningar.)
  - Det kan vara så att indexeraren helt enkelt inte kan användas med den \*Arr. Detta är vanligt när man försöker använda offentliga trackers eller usenet-indexers med Readarr och Lidarr.
  - Justera de synkroniserade kategorierna i de avancerade inställningarna för \*Arr-applikationen i Prowlarr
    - Observera att vissa spårare - främst "dåliga" offentliga spårare - kräver att man väljer och synkroniserar kategorin "8000 - Annat". Detta anges ofta - men inte alltid - i spårens detaljer i Prowlarr.
  - Försök igen senare
  - Om problemet kvarstår kan du ha en korrupt databas. Kontrollera dina loggar efter förekomster av `Database disk image is malformed` eller `Error creating main database`. Se [denna rubrik](https://wiki.servarr.com/prowlarr/faq#i-am-getting-an-error-database-disk-image-is-malformed) för möjliga lösningar.

## Vilka \*Arr Indexer-inställningar jämförs för fullständig synkronisering av appen?

- App/Prowlarr: Indexernamn
- App/Prowlarr: Aktivera/inaktivera RSS
- App/Prowlarr: Aktivera/inaktivera automatisk sökning
- App/Prowlarr: Aktivera/inaktivera interaktiv sökning
- App/Prowlarr: Indexerprioritet
- App/Prowlarr: API-nyckel
- App/Prowlarr: URL
- App/Prowlarr: Bas-URL
- App/Prowlarr: Port
- App/Prowlarr: Kategorier
- App/Prowlarr: Seed Ratio och Seed Time
- App/Prowlarr: Minimum Seeders
- App/Prowlarr: *Alla andra inställningar som kan konfigureras/styras i Prowlarr*
- Prowlarr: Implementation (t.ex. YML eller C#)

Med fullständig synkronisering aktiverad, om något av ovanstående ändras mellan \*Arr-appen och Prowlarr kommer indexeraren att synkroniseras och uppdateras i \*Arr.

## Hur uppdaterar jag Prowlarr?

- Gå till Inställningar och sedan fliken Allmänt och visa avancerade inställningar (använd växlingen bredvid spara-knappen).

1. Under avsnittet Uppdateringar ändrar du grennamnet till `master`, `develop` eller `nightly`
1. Spara

*Detta kommer inte att installera bitarna från den grenen omedelbart, det kommer att ske under nästa uppdatering.*

- `master` - ![Current Master/Stable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) -    (Standard/Stabil): Den har testats av användare på utvecklings- och nightly-grenarna och det är inte känt att den har några större problem. På GitHub är detta `master`-grenen.

- `develop` - ![Current Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) -  (Beta): Detta är den testande kanten. Släpps efter att ha testats i nightly för att säkerställa att det inte finns några omedelbara problem. Nya funktioner och buggfixar släpps här först efter nightly. Det kan anses vara halvstabilt, men är fortfarande `beta`.

> På GitHub är detta en ögonblicksbild av `develop`-grenen vid en specifik tidpunkt.
{.is-warning}

- `nightly` - ![Current Nightly/Unstable](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) -  (Alpha/Ostabilt): Detta är den senaste utvecklingsversionen. Den släpps så snart koden har skickats och passerat alla automatiserade tester. Denna version kan ännu inte ha använts av oss eller andra användare. Det finns ingen garanti för att den ens kommer att köras i vissa fall. Denna gren rekommenderas endast för avancerade användare. Problem och egen undersökning förväntas i denna gren. ***Använd denna gren endast om du vet vad du gör och är villig att ta dig an problem om en uppdatering misslyckas.*** Denna version uppdateras omedelbart.

> **Varning: Du kanske inte kan gå tillbaka till `develop` efter att ha växlat till denna gren.** På GitHub är detta `develop`-grenen.
{.is-danger}

- Observera: Om du installerar via Docker lägger du till `:latest`, `:testing`, `:develop` eller `:nightly` i slutet av din container-tagg beroende på vem som gör dina byggen.

|                                                                      | `master` (stabilt) ![Nuvarande Master/Stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Master&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/master/changes) | `develop` (beta) ![Nuvarande Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Develop&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/develop/changes) | `nightly` (instabil) ![Nuvarande Nightly/Alpha](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=Nightly&query=%24%5B0%5D.version&url=https://prowlarr.servarr.com/v1/update/nightly/changes) |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [hotio](https://hotio.dev/containers/prowlarr)                       | `senaste`                                                                                                                                                                                                             | `testing`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-prowlarr) | `senaste`                                                                                                                                                                                                             | `develop`                                                                                                                                                                                                            | `nightly`                                                                                                                                                                                                                 |

### Kan jag uppdatera Prowlarr inuti min Docker-container?

- *Tekniskt sett, ja.* **Men du bör absolut inte göra det.** Det är en grundläggande filosofi för Docker. Det kan uppstå databasproblem om du uppgraderar din installation till den senaste `nightly`-versionen, men sedan uppdaterar själva Docker-containern (vilket kan innebära att du nedgraderar till en äldre version).

### Installera en nyare version

#### Nativ

1. Gå till System och sedan fliken Uppdateringar.
1. Nyare versioner som inte är installerade än kommer att ha en uppdateringsknapp bredvid dem. Klicka på den knappen för att installera uppdateringen.

#### Docker

1. Dra om ditt tag och uppdatera din container.

## Kan jag byta från `nightly` tillbaka till `develop`?

## Kan jag byta mellan grenar?

- Om versionen är identisk kan du byta, annars kontrollera med utvecklingsteamet om du kan byta från `nightly` till `develop`; eller från `develop` till `nightly` för din specifika byggversion.
- Om du inte följer dessa instruktioner kan din Prowlarr sluta fungera eller kasta fel. Du har blivit varnad
  - De vanligaste felen är databasfel som rör saknade kolumner eller tabeller.

## Hjälp, min Mac säger att Prowlarr inte kan öppnas eftersom utvecklaren inte kan verifieras

- Detta är enkelt, se den här länken för mer information [här](https://support.apple.com/sv-se/guide/mac-help/open-a-mac-app-from-an-unidentified-developer-mh40616/mac)
- Alternativt kan du behöva självsignera Prowlarr `codesign --force --deep -s - /Applications/Prowlarr.app && xattr -rd com.apple.quarantine`

![faq_1_mac.png](/assets/general/faq_1_mac.png)

## Hjälp, min Mac säger att Prowlarr.app är skadad och kan inte öppnas

Det beror antingen på en korrupt nedladdning (så försök igen), eller säkerhetsproblem som besvarades strax ovanför detta.

## Hur begär jag en funktion för Prowlarr?

För att begära en funktion för Prowlarr, sök först på GitHub för att se till att ingen liknande begäran redan finns, och klicka sedan [här](https://github.com/Prowlarr/Prowlarr/issues/new?assignees=&labels=feature+request&template=feature_request.md&title=) för att lägga till din begäran.

## Jag får ett felmeddelande: Databasdiskbilden är skadad

- **Felmeddelanden som `Error creating log database` indikerar problem med logs.db**
  - Detta kan snabbt åtgärdas genom att byta namn på eller ta bort databasen. Loggdatabasen innehåller oviktig information om kommandohistorik och uppdateringsinstallationshistorik, samt Info-, Warn- och Error-poster.
- **Felmeddelanden som `Error creating main database` eller generella `database disk image is malformed` utan angiven databas indikerar problem med prowlarr.db**
  - Fortsätt med de nedan angivna stegen
- Detta innebär att din SQLite-databas som lagrar det mesta av informationen för Prowlarr är korrupt. Dina alternativ är att försöka (en) säkerhetskopiering(ar), försöka återställa den befintliga databasen, försöka återställa säkerhetskopiering(ar), eller om allt annat misslyckas börja om med en helt ny databas.
- Detta fel kan visas om databasfilen inte kan skrivas av användaren/gruppen som \*Arr körs som. Problem med behörigheter kommer troligen bara att vara ett problem för nya installationer, migrerade installationer till en ny server, om du nyligen har ändrat behörigheterna för din appdata-katalog eller om du har ändrat användaren och gruppen som \*Arr körs som.
- Ditt bästa och första alternativ är att [försöka återställa från en säkerhetskopia](#how-do-i-backuprestore-my-prowlarr)
- Du kan också försöka återställa din databas. Detta är vanligtvis det enda alternativet när detta problem uppstår efter en uppdatering. Prova [sqlite3-kommandot `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Om din sqlite inte har `.recover` eller om du vill ha ett mer GUI-vänligt sätt (t.ex. Windows) kan du följa [våra instruktioner på denna wiki.](/useful-tools#recovering-a-corrupt-db-ui)
- En annan möjlig orsak till att du får ett fel med din databas är att du placerar din databas på en nätverksenhet (nfs eller smb eller något annat som inte är lokalt). **SQLite är utformat för situationer där data och applikationen existerar på samma maskin.** Därför måste din \*Arr AppData-mapp (/config-mount för docker) vara på lokal lagring. [SQLite och nätverksenheter fungerar inte bra tillsammans och kommer så småningom att orsaka en skadad databas](https://www.sqlite.org/draft/useovernet.html).
- Om du använder mergerFS måste du ta bort `direct_io` eftersom SQLite använder mmap som inte stöds av `direct_io`, som förklaras i mergerFS [dokumentationen här](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jag använder Prowlarr på en Mac och det slutade plötsligt att fungera. Vad har hänt?

- Detta beror förmodligen på en bugg i MacOS som orsakade att Prowlarr-databasen blev korrupt. Se FAQ-posten om att återställa en korrupt databas.

## Hur byter jag från Windows-tjänsten till en fältapp?

- Stäng av Prowlarr
- Kör serviceuninstall.exe som finns i Prowlarr-mappen
- Kör Prowlarr.exe som administratör en gång för att ge den korrekta behörigheten och öppna brandväggen. När det är klart kan du stänga det och köra det normalt.
- (Valfritt) Lägg till en genväg till Prowlarr.exe i mappen för automatisk start för att starta vid uppstart.

## Hur säkerhetskopierar/återställer jag Prowlarr?

### Säkerhetskopiera Prowlarr

#### Använda inbyggd säkerhetskopiering

- Gå till System => Säkerhetskopiering i Prowlarr UI
- Klicka på Säkerhetskopieringsknappen
- Ladda ner zip-filen efter att säkerhetskopieringen har skapats för att spara den på ett säkert ställe

#### Använda filsystemet direkt

- Hitta platsen för AppData-katalogen för Prowlarr  
  - Via Prowlarr UI, gå till System => Om  
  - [Prowlarr Appdata-katalog](/prowlarr/appdata-directory)
- Stoppa Prowlarr - Detta förhindrar att databasen blir korrupt
- Kopiera innehållet till en säker plats

### Återställa från säkerhetskopia

> Att återställa till ett operativsystem som använder olika sökvägar kommer inte att fungera (Windows till Linux, Linux till Windows, Windows till OS X eller OS X till Windows), att flytta mellan OS X och Linux kan fungera, eftersom båda använder sökvägar som innehåller `/` istället för `\` som Windows använder, men det stöds inte. Du måste manuellt redigera alla sökvägar i databasen.
{.is-warning}

#### Använda zip-säkerhetskopia

- Installera om Prowlarr (om tillämpligt / inte redan installerat)
- Kör Prowlarr
- Gå till System => Säkerhetskopiering
- Välj Återställ säkerhetskopia
- Välj Välj fil
- Välj din säkerhetskopierings-zip-fil
- Välj Återställ

#### Använda filsystemets säkerhetskopiering

- Installera om Prowlarr (om tillämpligt / inte redan installerat)
- Hitta platsen för AppData-katalogen för Prowlarr  
  - Kör Prowlarr en gång och gå via UI till System => Om  
  - [Prowlarr Appdata-katalog](/prowlarr/appdata-directory)
- Stoppa Prowlarr
- Ta bort innehållet i AppData-katalogen **(inklusive .db-wal/.db-journal-filerna om de finns)**
- Återställ från din säkerhetskopia
- Starta Prowlarr
- Så länge sökvägarna är desamma kommer allt att fortsätta där det slutade

#### Återställning av filsystem på Synology NAS

> VARNING: Återställning på en Synology kräver kunskap om Linux och Root SSH-åtkomst till Synology-enheten.
{.is-warning}

- Installera om Prowlarr (om tillämpligt / inte redan installerat)
- Hitta platsen för AppData-katalogen för Prowlarr  
  - Kör Prowlarr en gång och gå via UI till System => Om  
  - [Prowlarr Appdata-katalog](/prowlarr/appdata-directory)
- Stoppa Prowlarr
- Anslut till Synology NAS via SSH och logga in som root  

> På vissa installationer är användaren annorlunda än nedanstående kommandon: `chown -R sc-Prowlarr:Prowlarr *` {.is-info}

- Kör följande kommandon:

    ```shell
        rm -r /usr/local/Prowlarr/var/.config/Prowlarr/Prowlarr.db
        cp -f /tmp/Prowlarr_backup/* /usr/local/Prowlarr/var/.config/Prowlarr/
    ```

- Uppdatera behörigheterna för filerna:

    ```shell
        cd /usr/local/Prowlarr/var/.config/Prowlarr/
        chown -R Prowlarr:users *
        chmod -R 0644 *
    ```

- Starta Prowlarr

## WebUI laddas bara på localhost på Windows

Om du bara kan nå din webbgränssnitt på `http://localhost:9696/` eller `http://127.0.0.1:9696`, måste du köra Prowlarr som administratör åtminstone en gång, kanske alltid.

## Hitta kakor

Vissa webbplatser kan inte loggas in automatiskt och kräver att du loggar in manuellt och sedan ger kakorna till Prowlarr för att det ska fungera. [Se den här artikeln för mer information.](/useful-tools#finding-cookies)

## uTorrent fungerar inte längre

- Se till att webbgränssnittet är aktiverat

![faq_4_utorrent.png](/assets/general/faq_4_utorrent.png)

- Aktivera webbgränssnittet

![faq_5_utorrent.png](/assets/general/faq_5_utorrent.png)

- Se till att alternativet Alt Listening Port (Avancerat => Web UI) inte är samma som Listening Port (Anslutningar). Vi rekommenderar att du ändrar Web UI Alt Listening Port för att inte störa vidarebefordran av portar för anslutningar.

![faq_6_utorrent.png](/assets/general/faq_6_utorrent.png)

## Jag fick ett popup-fönster som sa att config.xml var korrupt, vad gör jag nu?

Prowlarr kunde inte läsa din konfigurationsfil vid start eftersom den på något sätt blev korrupt. För att få Prowlarr tillbaka online måste du ta bort `.xml` i din AppData-mapp. När du har tagit bort filen startar du Prowlarr och den kommer att starta på standardporten (9696). Du bör nu konfigurera om alla inställningar du konfigurerade på sidan för allmänna inställningar.

## Ogiltigt certifikat och andra HTTPS- eller SSL-problem

Din nedladdningsklient slutade fungera och du får ett felmeddelande som säger "Localhost har ett ogiltigt certifikat"?

Prowlarr validerar SSL-certifikat. Om det inte finns något SSL-certifikat inställt i nedladdningsklienten, eller om du använder ett självsignerat https-certifikat utan att ha lagt till CA-certifikatet i din lokala certifikatbutik, kommer Prowlarr att vägra att ansluta. Gratis korrekt signerade certifikat finns tillgängliga från Let's Encrypt.

Om din nedladdningsklient och Prowlarr är på samma maskin finns det ingen anledning att använda HTTPS, så det enklaste sättet är att inaktivera SSL för anslutningen. De flesta skulle hålla med om att det inte är nödvändigt i ett lokalt nätverk heller. Det är möjligt att inaktivera validering av certifikat i avancerade inställningar om du vill behålla en osäker SSL-konfiguration.

## Hjälp, jag har låst mig ute

{#help-i-have-forgotten-my-password}

För att inaktivera autentisering (för att återställa ditt glömda användarnamn eller lösenord) måste du redigera `config.xml` som kommer att finnas i [Prowlarr Appdata-mappen](/prowlarr/appdata-directory).

1. Öppna config.xml i en textredigerare.
2. Hitta raden för autentiseringsmetod som kommer att vara antingen `<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`.
3. Ändra raden för `AuthenticationMethod` till `<AuthenticationMethod>None</AuthenticationMethod>`.
4. Starta om Prowlarr.
5. Prowlarr kommer nu att vara tillgängligt utan lösenord. Du bör gå till `Inställningar: Allmänt` i gränssnittet och ange ditt användarnamn och lösenord.

## Konstiga UI-problem

- Om du upplever några konstiga UI-problem eller om en viss vy eller sortering inte fungerar, försök att visa det i ett Chrome Inkognitofönster eller Firefox Privat fönster. Om det fungerar bra där, rensa webbläsarens cache och cookies för din specifika IP/domän. För mer information, se artikeln [Rensa cache, cookies och lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wikin.

## VPN, Jackett och \*ARRs

- Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika är det vanligtvis bara torrentklienten som behöver vara bakom en VPN. Eftersom VPN-ändpunkten delas av många användare kan du och kommer att uppleva begränsningar av hastigheten, DDOS-skydd och IP-blockeringar från olika tjänster som varje program använder.
- Med andra ord kan att placera \*ARRs (Lidarr, Prowlarr, Radarr, Readarr och Lidarr) bakom en VPN göra applikationerna oanvändbara i vissa fall på grund av att tjänsterna inte är tillgängliga.

> **För att vara tydlig handlar det inte om ifall VPN kommer att orsaka problem med \*ARRs, utan när: bildleverantörer kommer att blockera dig och Cloudflare finns framför de flesta \*ARR-servrar (uppdateringar, metadata osv.) och kan också blockera dig**
{.is-warning}

- **Många privata spårare kommer att blockera dig om du använder eller får åtkomst till dem (t.ex. genom att använda Jackett eller Prowlarr) via en VPN.**

### Användning av VPN

- Om en VPN krävs och Docker används rekommenderas det att använda Hotio eller Binhex's Download Client + VPN Containers.
- Om en VPN krävs och Docker inte används måste din VPN-klient ***stödja*** split tunneling så att endast de nödvändiga (nedladdningsklient) apparna är bakom VPN:en.
- Många problem med att få åtkomst till spårare kan lösas genom att använda Googles eller Cloudflares DNS-servrar istället för din internetleverantörs DNS-servrar.
- I vissa fall (t.ex. brittiska internetleverantörer) kan du behöva placera din torrentnedladdningsklient bakom en VPN och Jackett/Prowlarr enligt följande:
  - placera Jackett bakom VPN:en och se till att split tunneling tillåter lokal åtkomst
  - för Prowlarr konfigurerar du din VPN-klient för att tillhandahålla en proxy och lägger till proxyn i Inställningar => Indexers. Ge proxyn en tagg och ge samma tagg till indexers som behöver använda den.
    - Om det absolut krävs och om din VPN inte erbjuder ett sätt att skapa en proxy kan du placera Prowlarr bakom VPN:en och se till att split tunneling tillåter lokal åtkomst.

## Hur stoppar jag webbläsaren från att starta vid uppstart?

Beroende på ditt operativsystem finns det flera möjliga sätt.

- I `Inställningar` => `Allmänt` på vissa operativsystem finns det en kryssruta för att starta webbläsaren vid uppstart.
- När du startar Prowlarr kan du lägga till `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumenten.
- Stoppa Prowlarr och redigera config.xml-filen och ändra `<LaunchBrowser>True</LaunchBrowser>` till `<LaunchBrowser>False</LaunchBrowser>`.

## Kan jag enkelt lägga till alla indexers på en gång?

Nej. Detta skulle inte vara en bra sak att göra, och den här funktionen kommer inte att läggas till. Det är mycket bättre att välja dina indexers noggrant, vara uppmärksam på statistiken för att ta bort indexers som är för långsamma eller inte ger några träffar. En korrekt beskärning och underhåll av dina indexers kommer att ge mycket bättre resultat övergripande och snabbare resultat vid sökningar från dina appar.