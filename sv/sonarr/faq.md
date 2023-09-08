# Sonarr FAQ

<!-- # Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Sonarr-grunder](#sonarr-grunder)
  - [Hur hittar Sonarr avsnitt?](#hur-hittar-sonarr-avsnitt)
  - [Hur jämförs möjliga nedladdningar?](#hur-jämförs-möjliga-nedladdningar)
  - [Vanliga frågor om föredragna ord](#vanliga-frågor-om-föredragna-ord)
  - [Hur byter jag från Windows-tjänsten till en fältapp?](#hur-byter-jag-från-windows-tjänsten-till-en-fältapp)
  - [Hur säkerhetskopierar/återställer jag min Sonarr?](#hur-säkerhetskopieraråterställer-jag-min-sonarr)
    - [Säkerhetskopiering av Sonarr](#säkerhetskopiering-av-sonarr)
      - [Använda inbyggd säkerhetskopiering](#använda-inbyggd-säkerhetskopiering)
      - [Använda filsystemet direkt](#använda-filsystemet-direkt)
    - [Återställning från säkerhetskopiering](#återställning-från-säkerhetskopiering)
      - [Använda zip-säkerhetskopiering](#använda-zip-säkerhetskopiering)
      - [Använda filsystemets säkerhetskopiering](#använda-filsystemets-säkerhetskopiering)
      - [Återställning av filsystem på Synology NAS](#återställning-av-filsystem-på-synology-nas)
  - [Hjälp, jag har låst mig själv](#hjälp-jag-har-låst-mig-själv)
  - [Varför finns det två filer? \| Varför finns det en fil kvar i nedladdningar?](#varför-finns-det-två-filer-varför-finns-det-en-fil-kvar-i-nedladdningar)
  - [Jag ser att funktion/bugg X har åtgärdats, varför kan jag inte se det?](#jag-ser-att-funktionbugg-x-har-åtgärdats-varför-kan-jag-inte-se-det)
  - [Avsnittsframsteg - Hur beräknas det?](#avsnittsframsteg-hur-beräknas-det)
  - [Hur får jag åtkomst till Sonarr från en annan dator?](#hur-får-jag-åtkomst-till-sonarr-från-en-annan-dator)
  - [Varför uppdaterar Sonarr seriens information så ofta?](#varför-uppdaterar-sonarr-seriens-information-så-ofta)
  - [Varför finns det ett nummer bredvid Aktivitet?](#varför-finns-det-ett-nummer-bredvid-aktivitet)
  - [Vad är de olika serietyperna?](#vad-är-de-olika-serietyperna)
    - [Serietyper](#serietyper)
    - [Exempel på serietyper](#exempel-på-serietyper)
      - [Daglig](#daglig)
      - [Standard](#standard)
      - [Anime](#anime)
  - [Hur kan jag döpa om mina seriemappar?](#hur-kan-jag-döpa-om-mina-seriemappar)
  - [Hur uppdaterar jag Sonarr?](#hur-uppdaterar-jag-sonarr)
    - [Installation av en nyare version](#installation-av-en-nyare-version)
      - [Inbyggd](#inbyggd)
      - [Docker](#docker)
  - [Kan jag växla från `develop` tillbaka till `main`?](#kan-jag-växla-från-develop-tillbaka-till-main)
  - [Kan jag växla mellan grenar?](#kan-jag-växla-mellan-grenar)
- [Sonarr och serieproblem + metadata](#sonarr-och-serieproblem-metadata)
  - [Hur hanterar Sonarr scennummerproblem (American Dad!, etc)?](#hur-hanterar-sonarr-scennummerproblem-american-dad-etc)
    - [Hur Sonarr hanterar scennummerproblem](#hur-sonarr-hanterar-scennummerproblem)
    - [Problematiserade serier](#problematiserade-serier)
  - [Varför kan inte Sonarr importera avsnittsfiler för serie X? / Varför kan inte Sonarr hitta utgåvor för serie X?](#varför-kan-inte-sonarr-importera-avsnittsfiler-för-serie-x-varför-kan-inte-sonarr-hitta-utgåvor-för-serie-x)
  - [TVDb uppdateras, varför uppdateras inte Sonarr?](#tvdb-uppdateras-varför-uppdateras-inte-sonarr)
  - [Varför kan jag inte lägga till en serie?](#varför-kan-jag-inte-lägga-till-en-serie)
  - [Varför kan jag inte lägga till en serie när jag vet TVDb-ID?](#varför-kan-jag-inte-lägga-till-en-serie-när-jag-vet-tvdb-id)
  - [Titelslug i användning](#titelslug-i-användning)
  - [Avsnitt har inte ett absolut nummer](#avsnitt-har-inte-ett-absolut-nummer)
  - [Avsnittets sändningstider](#avsnittets-sändningstider)
- [Vanliga problem med Sonarr](#vanliga-problem-med-sonarr)
  - [Sökvägen är redan konfigurerad för en befintlig serie](#sökvägen-är-redan-konfigurerad-för-en-befintlig-serie)
  - [Avsnittet har inte för alltid](#system-logs-loads-forever)
  - [Konstiga UI-problem](#konstiga-ui-problem)
  - [Webbgränssnittet laddas bara på localhost på Windows](#webbgränssnittet-laddas-bara-på-localhost-på-windows)
  - [uTorrent fungerar inte längre](#utorrent-fungerar-inte-längre)
  - [Kräver Sonarr ett SABnzbd-postbehandlingskript för att importera nedladdade avsnitt?](#kräver-sonarr-ett-sabnzbd-postbehandlingskript-för-att-importera-nedladdade-avsnitt)
  - [Jag fick ett popup-fönster som sa att config.xml var korrupt, vad gör jag nu?](#jag-fick-ett-popup-fönster-som-sa-att-configxml-var-korrupt-vad-gör-jag-nu)
  - [Sonarr på Synology slutade fungera (SSL)](#sonarr-på-synology-slutade-fungera-ssl)
  - [Ogiltigt certifikat och andra HTTPS- eller SSL-problem](#ogiltigt-certifikat-och-andra-https-eller-ssl-problem)
  - [Hur stoppar jag webbläsaren från att starta vid uppstart?](#hur-stoppar-jag-webbläsaren-från-att-starta-vid-uppstart)
  - [VPN, Jackett och \*ARRs](#vpn-jackett-och-arrs)
  - [Jag ser loggmeddelanden för program som jag inte har/vill ha](#jag-ser-loggmeddelanden-för-program-som-jag-inte-harvill-ha)
  - [Seedingtorrentar raderas inte automatiskt](#seedingtorrentar-raderas-inte-automatiskt)
  - [Hjälp, min Mac säger att Sonarr inte kan öppnas eftersom utvecklaren inte kan verifieras](#hjälp-min-mac-säger-att-sonarr-inte-kan-öppnas-eftersom-utvecklaren-inte-kan-verifieras)
  - [Hjälp, min Mac säger att Sonarr.app är skadad och kan inte öppnas](#hjälp-min-mac-säger-att-sonarrapp-är-skadad-och-kan-inte-öppnas)
  - [Jag får ett felmeddelande: Databasens diskavbildning är skadad](#jag-får-ett-felmeddelande-databasens-diskavbildning-är-skadad)
  - [Jag använder Sonarr på en Mac och den slutade plötsligt fungera. Vad hände?](#jag-använder-sonarr-på-en-mac-och-den-slutade-plötsligt-fungera-vad-hände)
  - [Varför kan inte Sonarr se mina filer på en fjärrserver?](#varför-kan-inte-sonarr-se-mina-filer-på-en-fjärrserver)
    - [Sonarr körs som standard under LocalService-kontot som inte har åtkomst till skyddade fjärrfilresurser](#sonarr-körs-som-standard-under-localservice-kontot-som-inte-har-åtkomst-till-skyddade-fjärrfilresurser)
    - [Du använder en kartad nätverksenhet (inte en UNC-sökväg)](#du-använder-en-kartad-nätverksenhet-inte-en-unc-sökväg)
  - [Kartade nätverksenheter vs UNC-sökvägar](#kartade-nätverksenheter-vs-unc-sökvägar)
  - [Sonarr fungerar inte på Big Sur](#sonarr-fungerar-inte-på-big-sur)
  - [Mitt anpassade skript slutade fungera efter uppgradering från v2](#mitt-anpassade-skript-slutade-fungera-efter-uppgradering-från-v2)
- [Vanliga problem med sökning och nedladdning i Sonarr](#vanliga-problem-med-sökning-och-nedladdning-i-sonarr)
  - [Lyckad fråga - Inga resultat returnerade](#lyckad-fråga-inga-resultat-returnerade)
  - [Varför hämtade inte Sonarr ett avsnitt som jag förväntade mig?](#varför-hämtade-inte-sonarr-ett-avsnitt-som-jag-förväntade-mig)
  - [Hittade matchande serier via hämtningshistorik, men utgåvan matchades med serien efter ID. Automatisk import är inte möjlig](#hittade-matchande-serier-via-hämtningshistorik-men-utgåvan-matchades-med-serien-efter-id-automatisk-import-är-inte-möjlig)
  - [Varför importerar inte Sonarr ett TBA-avsnitt?](#varför-importerar-inte-sonarr-ett-tba-avsnitt)
  - [Sonarr säger Okänd serie vid sökningar eller import](#sonarr-säger-okänd-serie-vid-sökningar-eller-import)
  - [Jacketts /all slutpunkt](#jacketts-all-slutpunkt)
    - [Jackett /All-lösningar](#jackett-all-lösningar)
  - [Jackett visar fler resultat än Sonarr vid manuell sökning](#jackett-visar-fler-resultat-än-sonarr-vid-manuell-sökning)
  - [Hitta kakor](#hitta-kakor)
  - [Packa upp torrents](#packa-upp-torrents)
  - [Behörigheter](#behörigheter) -->

# Sonarr-grunder

## Hur hittar Sonarr avsnitt?

- Sonarr söker *inte* regelbundet efter avsnittsfiler som saknas eller inte har uppnått sin kvalitetsmål. Istället frågar den dina indexerare och spårare ganska ofta efter *alla* nyuppladdade avsnitt/nyuppladdade utgåvor och jämför sedan det med sin lista över avsnitt som saknas eller behöver uppgraderas. Alla matchningar laddas ner. Detta gör att Sonarr kan täcka en bibliotek av *vilken storlek som helst* med bara 24-100 förfrågningar per dag (RSS-intervall på 15-60 minuter). Om du förstår detta kommer du att inse att det bara täcker *framtiden* dock.
- Så hur hanterar du nuet och det förflutna? När du lägger till en serie måste du ange rätt sökväg, profil och övervakningsstatus och sedan använda kryssrutan Starta sökning efter saknade. Om serien inte har haft några avsnitt och inte har släppts ännu behöver du inte starta en sökning.
- Med andra ord kommer Sonarr bara att hitta utgåvor som nyligen har laddats upp till dina indexerare. Den kommer inte aktivt att försöka hitta utgåvor som laddades upp i det förflutna.
- Om du redan har lagt till serien, men nu vill söka efter den, har du några valmöjligheter. Du kan gå till seriens sida och använda sökknappen, vilket kommer att göra en sökning och sedan automatiskt välja avsnitt. Du kan söka efter enskilda avsnitt eller säsonger automatiskt eller manuellt. Eller så kan du gå till fliken [Efterfrågade](/sonarr/wanted) och söka därifrån.
- Om Sonarr har varit offline under en längre tid kommer Sonarr att försöka bläddra tillbaka för att hitta den senaste utgåvan som bearbetades för att undvika att missa en utgåva. Så länge din indexerare stöder bläddring och det inte har gått för lång tid kommer Sonarr att kunna bearbeta de utgåvor som den skulle ha missat och undvika att du behöver utföra en sökning efter de missade avsnitten.

### Fall när automatisk sökning ändå sker

Aktiv sökning (via indexerarens API) utförs endast i följande situationer. Observera att samma regler som vanligt gäller: serien + avsnittet måste vara övervakat och avsnitt utan sändningstid ignoreras

- Utlöst automatisk eller manuell sökning
  - Användar- eller API-utlöst sökning. Utförs vanligtvis genom att klicka på knapparna Automatisk eller Manuell sökning på ett specifikt avsnitt, säsong eller serie.
- Lägga till en serie med hjälp av knappen Lägg till och sök
- Använda Efterfrågade => Saknas eller Efterfrågade => Avskuren för att göra en eller flera sökningar
- Nyligen sända avsnitt som har lagts till efter sändning
  - Om ett nytt avsnitt läggs till i Sonarr som sändes de senaste 14 dagarna eller inom 1 dag framåt i tiden (för att täcka de avsnitt som kan släppas lite tidigt) kommer Sonarr **att söka** efter dessa avsnitt efter att seriemappen har skannats om (för att fånga upp saker som importerats utanför Sonarr)

## Hur jämförs möjliga nedladdningar?

> Generellt sett prioriteras kvalitet framför allt. Om du inte vill att kvalitet ska vara den främsta prioriteringen kan du slå samman dina kvaliteter. [Se TRaSH:s guide](https://trash-guides.info/merge-quality)
{.is-info}

- Den aktuella logiken [kan alltid hittas här](https://github.com/Sonarr/Sonarr/blob/develop/src/NzbDrone.Core/DecisionEngine/DownloadDecisionComparer.cs#L31-L40s).

- Från och med 2022-01-23 är logiken följande:

1. Kvalitet
1. Språk
1. Poäng för föredragna ord\*
1. Protokoll (som konfigurerat i den relevanta fördröjningsprofilen)
1. Antal avsnitt\*
1. Avsnittsnummer
1. Indexerprioritet
1. Seeds/Peers (om Torrent)
1. Ålder (om Usenet)
1. Storlek

> REPACKS och PROPERs är v2 av kvaliteter och rankas därför över en icke-repack av samma kvalitet. [Ställ in Mediahantering => Filhantering `Download Proper & Repacks` till "Do Not Prefer"](/sonarr/settings#file-management) och använd en föredragen ord-reguljärexpression av `/\b(repack|proper)\b/i` med en positiv poäng som föreslagits av [TRaSH:s guider](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#p2p-groups-repackproper)
{.is-warning}

> \* Föredragna ord uppgraderar alltid en utgåva även om kvalitets- och/eller språggränsen har uppnåtts. Detta inkluderar om profilen har inaktiverat uppgraderingar.
> \* Föredragna ord åsidosätter den vanliga preferensen för säsongspaket. Detta är [Sonarr Github Issue #3562](https://github.com/Sonarr/Sonarr/issues/3562). För att föredra säsongspaket när du använder föredragna ord måste du [lägga till en preferens för säsongspaket också](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

## Vanliga frågor om föredragna ord

- För poängen för filen på disken: Det befintliga namnet på filen och "ursprungligt scen-namn" för utgåvan utvärderas för föredragna ord. Den högre poängen av de två tas.

- Hur inkluderas föredragna ord vid namngivning?

  - För Sonarr kan du använda token `{Preferred Words}` i din namngivningsschema och även aktivera `Include Preferred when Renaming` i utgåveprofilen. Ta en titt [på TRaSH:s rekommenderade namngivningsschema](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/) för exempel på rekommenderade namngivningsscheman för Sonarr. Att använda token i ditt namngivningsschema kan hjälpa till med nedladdningsloopproblem.

- Från och med v3.0.7 kan du nu också inkludera föredragna ord på en utgåveprofilbasis `{Preferred Words:<Utgåveprofilnamn>}`

- Föredragna ord uppgraderar alltid en utgåva även om kvalitets- och/eller språggränsen har uppnåtts. Detta inkluderar om profilen har inaktiverat `Upgrades`

> Föredragna ord åsidosätter den vanliga preferensen för säsongspaket. Detta är [Sonarr Github Issue #3562](https://github.com/Sonarr/Sonarr/issues/3562). För att föredra säsongspaket när du använder föredragna ord måste du [lägga till en preferens för säsongspaket också](https://trash-guides.info/Sonarr/Sonarr-Release-Profile-RegEx/#optional-prefer-season-packs)
{.is-info}

- Taggar kan användas för att styra vilka serier en utgåveprofil gäller för; se inställningsposten för utgåveprofiler för mer information

- För ytterligare information om föredragna ord och utgåveprofiler [se inställningssidan](/sonarr/settings#release-profiles)

## Hur byter jag från Windows-tjänsten till en fältapp?

1. Stäng ner Sonarr.
1. Kör serviceuninstall.exe som finns i Sonarr-mappen.
1. Kör Sonarr.exe som administratör en gång för att ge det korrekta behörigheter och öppna brandväggen. När det är klart kan du stänga ner det och köra det som vanligt.
1. (Valfritt) Skapa en genväg till Sonarr.exe i mappen för autostart för att starta det automatiskt vid uppstart.

## Hur säkerhetskopierar/återställer jag min Sonarr?

### Säkerhetskopiering av Sonarr

#### Använda inbyggd säkerhetskopiering

- Gå till System => Backup i Sonarr-gränssnittet.
- Klicka på Säkerhetskopiera-knappen.
- Ladda ner zip-filen efter att säkerhetskopieringen har skapats för att spara den på ett säkert ställe.

#### Använda filsystemet direkt

- Hitta platsen för AppData-mappen för Sonarr.
  - Gå till System => Om i Sonarr-gränssnittet.
  - [Sonarr Appdata-mapp](/sonarr/appdata-directory)
- Stoppa Sonarr - Detta förhindrar att databasen blir korrupt.
- Kopiera innehållet till en säker plats.

### Återställning från säkerhetskopia

> Att återställa till ett operativsystem som använder olika sökvägar fungerar inte (Windows till Linux, Linux till Windows, Windows till OS X eller OS X till Windows). Att flytta mellan OS X och Linux kan fungera, eftersom båda använder sökvägar som innehåller `/` istället för `\` som Windows använder, men det stöds inte. Du måste manuellt redigera alla sökvägar i databasen eller använda [Toolbarr](https://github.com/Notifiarr/toolbarr).
{.is-warning}

#### Använda zip-säkerhetskopia

- Installera om Sonarr (om tillämpligt / inte redan installerat).
- Kör Sonarr.
- Gå till System => Backup.
- Välj Återställ säkerhetskopia.
- Välj Välj fil.
- Välj din säkerhetskopierings-zip-fil.
- Välj Återställ.

#### Använda filsystemets säkerhetskopia

- Installera om Sonarr (om tillämpligt / inte redan installerat).
- Hitta platsen för AppData-mappen för Sonarr.
  - Kör Sonarr en gång och gå till System => Om i gränssnittet.
  - [Sonarr Appdata-mapp](/sonarr/appdata-directory)
- Stoppa Sonarr.
- Radera innehållet i AppData-mappen **(inklusive .db-wal/.db-journal-filerna om de finns)**.
- Återställ från din säkerhetskopia.
- Starta Sonarr.
- Så länge sökvägarna är desamma kommer allt att fortsätta där det slutade.

#### Återställning av filsystem på Synology NAS

> VARNING: Att återställa på en Synology kräver kunskap om Linux och Root SSH-åtkomst till Synology-enheten.
{.is-warning}

- Installera om Sonarr (om tillämpligt / inte redan installerat).
- Hitta platsen för AppData-mappen för Sonarr.
  - Kör Sonarr en gång och gå till System => Om i gränssnittet.
  - [Sonarr Appdata-mapp](/sonarr/appdata-directory)
- Stoppa Sonarr.
- Anslut till Synology NAS via SSH och logga in som root.

> På vissa installationer är användaren annorlunda än nedanstående kommandon: `chown -R sc-Sonarr:Sonarr *` {.is-info}

- Kör följande kommandon:

```shell
rm -r /usr/local/Sonarr/var/.config/Sonarr/Sonarr.db
cp -f /tmp/Sonarr_backup/* /usr/local/Sonarr/var/.config/Sonarr/
```

- Uppdatera behörigheterna för filerna:

 ```shell
cd /usr/local/Sonarr/var/.config/Sonarr/
chown -R Sonarr:users *
chmod -R 0644 *
```

- Starta Sonarr.

## Hjälp, jag har låst mig ute

{#help-i-have-forgotten-my-password}

> Om du använder v4 av Sonarr är inte autentiseringsmetoden `None` längre giltig - se denna [FAQ](/sonarr/faq-v4) {.is-info}

För att inaktivera autentisering (för att återställa ditt glömda användarnamn eller lösenord) måste du redigera `config.xml` som kommer att finnas i [Sonarr Appdata-mapp](/sonarr/appdata-directory).

1. Öppna config.xml i en textredigerare.
1. Hitta raden för autentiseringsmetoden som kommer att vara antingen
   `<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`.
1. Ändra raden för `AuthenticationMethod` till `<AuthenticationMethod>None</AuthenticationMethod>`.
1. Starta om Sonarr.
1. Sonarr kommer nu vara tillgängligt utan lösenord. Du bör gå till `Inställningar: Allmänt` i gränssnittet och ange ditt användarnamn och lösenord.

## Varför finns det två filer? \| Varför finns det en fil kvar i nedladdningar?

Detta är normalt. Med en konfiguration som stöder [hårdlänkar](https://trash-guides.info/hardlinks) används inte dubbel diskutrymme. Nedan beskrivs hur Torrent-processen fungerar.

1. Sonarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten. Exempel: filmer, tv, serier, musik, etc.
1. Sonarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Denna övervakning sker via nedladdningsklientens API.
1. Färdiga filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (kvot eller tid kan justeras i nedladdningsklienten eller från Sonarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer filen att hårdlänkas om det stöds av din konfiguration, annars kopieras filen om hårdlänkar inte stöds.
1. Om alternativet "Hantera färdiga nedladdningar - Ta bort färdiga" är aktiverat i Sonarrs inställningar kommer Sonarr att ta bort den ursprungliga filen och torrenten från din nedladdningsklient, men endast om nedladdningsklienten rapporterar att seedningen är klar och torrenten är stoppad (dvs. pausad). Se [TRaSH's Download Client Guides](https://trash-guides.info/Downloaders/) för hur du konfigurerar din nedladdningsklient optimalt.

> Hårdlänkar är aktiverade som standard. [En hårdlänk använder inte något extra diskutrymme](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/). Filsystemet och monteringspunkterna måste vara desamma för din färdiga nedladdningsmapp och din mediebiblioteksmapp. Om skapandet av hårdlänken misslyckas eller om din konfiguration inte stöder hårdlänkar kommer den att använda kopiering som reservåtgärd.{.is-info}

## Jag ser att funktionen/felen X har åtgärdats, varför kan jag inte se det?

Sonarr består av två huvudgrenar av kod, `main` och `develop`.

- `main` släpps regelbundet när grenen `develop` är stabil.
- `develop` är för förhandsversionstestning och användare som vill vara på den senaste utvecklingsversionen. När en funktion markeras som i `develop` kommer den bara att vara tillgänglig för användare som kör grenen `develop`, när den har flyttats till live (i `main`) släpps den officiellt.

## Avsnittsframsteg - Hur beräknas det?

- Det finns två delar av avsnittsräkningen, en är antalet avsnitt (Avsnittsräkning) och den andra är antalet avsnitt med filer (Avsnittsfilräkning), var och en använder något olika logik för att ge dig den övergripande framstegen för en serie eller säsong.

  - Avsnittsräkning => Avsnittet har redan sänts OCH övervakas ELLER - Avsnittet har en fil
  - Avsnittsfilräkning => Avsnittet har en fil

- Om en serie har 10 avsnitt som alla har sänts och du inte har några filer för dem kommer du att ha 0/10 avsnitt, om du inte övervakar alla avsnitt i den serien kommer du att ha 0/0 och om du får alla avsnitt för den serien, oavsett om avsnitten övervakas eller inte, kommer du att ha 10/10 avsnitt.

## Hur får jag åtkomst till Sonarr från en annan dator?

- Som standard lyssnar inte Sonarr på förfrågningar från alla system (när det inte körs som administratör), det kommer bara att lyssna på localhost, detta beror på hur webbservern som Sonarr använder integreras med Windows (detta gäller även för nuvarande alternativ). Om Sonarr körs som administratör kommer det att registrera sig korrekt med Windows och öppna brandväggen så att det kan nås från andra system i ditt nätverk. Körning som administratör behöver bara göras en gång (om du ändrar porten måste det köras om).

## Varför uppdaterar Sonarr seriens information så ofta?

- Sonarr uppdaterar seriens och avsnittens information samt skannar disken efter filer var 12:e timme. Detta kan verka aggressivt, men det är en mycket viktig process. Uppdateringen av data från vår TVDb-proxy är viktig eftersom ny avsnittsinformation synkroniseras ner, sändningsdatum, antal avsnitt, status (fortsätter/avslutad). Även program som inte sänds uppdateras med ny information.
- Diskskanningen är mindre viktig, men används för att kontrollera efter nya filer som inte sorterades av Sonarr och upptäcka borttagna filer.
- Den mest tidskrävande delen är informationsuppdateringen (förutsatt rimlig diskåtkomsthastighet), större program tar längre tid på grund av antalet avsnitt som måste bearbetas.

> Det går inte att inaktivera denna uppgift. Om denna uppgift körs tillräckligt länge för att du ska tycka att den är ett problem är det något annat som pågår som behöver lösas istället för att stoppa denna uppgift.
{.is-warning}

## Varför finns det ett nummer bredvid Aktivitet?

- Detta nummer visar antalet avsnitt i din nedladdningsklients kö och de senaste 60 objekten i dess historik som ännu inte har importerats. Om numret är blått fungerar det normalt och bör importera avsnitt när de är klara. Gult betyder att det finns en varning för ett avsnitt. Rött betyder att det har uppstått ett fel. I fallet med gult (varning) och rött (fel) måste du titta på kön under Aktivitet för att se vad problemet är (håll muspekaren över ikonen för att få mer information).
- Du måste ta bort objektet från din nedladdningsklients kö eller historik för att ta bort dem från Sonarrs kö.

## Vad är de olika seriekategorierna?

- Seriekategori påverkar hur Sonarr söker efter serier. En seriekategori baseras på hur serien släpps på indexeringssajter och är inte nödvändigtvis den verkliga 'typen' av serien.
- De flesta program bör vara `Standard`. För dagliga program som vanligtvis släpps med ett datum bör `Daily` användas. Slutligen finns det anime där `Anime` *vanligtvis* är rätt, men ibland kan `Standard` fungera bättre, så prova det *andra* om du har problem.
- Observera att om serietypen är inställd på anime och om ingen av dina aktiverade indexeringssajter har några anime-kategorier konfigurerade kommer indexeraren att hoppas över och det kan verka som att den inte söker.
- Observera att anime-typen inte har någon koncept om säsongspaket eller säsonger och kommer att orsaka att varje avsnitt söks individuellt.
- Observera att inte alla indexerare stöder sökningar efter säsong/avsnitt (standard).
- Seriekategorier kan ändras från Massredigeraren eller från `Redigera` när du tittar på en serie. Observera att serietypen kan väljas vid import.

- Om **Anime** används som serietyp - är det [möjligt att även söka indexeraren med standardtypen.](/sonarr/settings#indexers)

### Seriekategorierna

- **Anime** - Avsnitt släppta med hjälp av ett absolut avsnittsnummer
- **Daily** - Avsnitt släppta dagligen eller mer sällan som använder åååå-mm-dd (2017-05-25)
- **Standard** - Avsnitt släppta med mönstret SxxEyy

### Exempel på seriekategorier

Nedan finns några exempel på namn på släpp för varje serietyp. Den specifika delen som skiljer dem åt är markerad med fetstil.

> Om **Anime** används som serietyp - är det [möjligt att även söka indexeraren med standardtypen.](/sonarr/settings#indexers)
{.is-info}

#### Daily

Loggarna kommer att visa `Söker indexerare för [The Witcher : 2021-12-20]`

- Some.Daily.Show.**2021.03.04**.1080p.HDTV.x264-DARKSPORT
- A.Daily.Show.with.Some.Guy.**2021.03.03**.1080p.CC.WEB-DL.AAC2.0.x264-null
- DailyShow.**2021.03.08**.720p.HDTV.x264-NTb

#### Standard

Loggarna kommer att visa `Söker indexerare för [The Witcher : S01E09]`

- The.Show.**S20E03**.Episode.Title.Part.3.1080p.HULU.WEB-DL.DDP5.1.H.264-NTb
- Another.Show.**S03E08**.1080p.WEB.H264-GGEZ
- GreatShow.**S17E02**.1080p.HDTV.x264-DARKFLiX

#### Anime

Loggarna kommer att visa `Söker indexerare för [The Witcher : S01E09 (09)]`

- Anime.Origins.**E04**.File.4\_.Monkey.WEB-DL.H.264.1080p.AAC2.0.AC3.5.1.Srt.EngCC-Pikanet128.1272903A
- \[Coalgirls\] Human X Monkey **148** (1920x1080 Blu-ray FLAC) \[63B8AC67\]
- \[KaiDubs\] Series x Title (2011) - **142** \[1080p\] \[English Dub\] \[CC\] \[AS-DL\] \[A24AB2E5\]

## Hur kan jag byta namn på mina seriemappar?

{#rename-folders}

> Samma process gäller också för att flytta/ändra sökvägar för serier{.is-info}

Om du har justerat formatet för ditt serienamn efter att Sonarr redan har skapat några seriemappar kommer inte Sonarr automatiskt att byta namn på befintliga mappar. För att utlösa en namnändring av dessa mappar bör följande steg vidtas:

1. Serier
1. Massredigeraren
1. Välj vilka serier som behöver byta namn på mappen
1. Ändra rotmappen till samma rotmapp som serien redan finns i
1. Välj "Ja, flytta filer" för att få

> Om du använder Plex eller Emby kommer detta att utlösa omidentifiering av intros, miniatyrer, kapitel och förhandsvisningsmetadata.
{.is-warning}

## Hur uppdaterar jag Sonarr?

- Gå till Inställningar och sedan fliken Allmänt och visa avancerade inställningar (använd växlingen bredvid spara-knappen).

1. Under avsnittet Uppdateringar ändra grennamnet till `main` eller `develop`.
1. Spara.

*Detta kommer inte att installera bitarna från den grenen omedelbart, det kommer att hända under nästa uppdatering.*

- main - ![Nuvarande huvudversion/stabil](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Standard/Stabil): Detta har testats av användare på nightly-grenen (`develop`) och det är inte känt att det har några stora problem. Den här grenen bör användas av majoriteten av användarna. På GitHub är detta huvudgrenen (`main`).
- develop - ![Nuvarande utvecklingsversion/nattlig](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alfa/Ostabilt): Detta är nu samma som main för användare som inte använder Docker och troligen den sista v3-versionen.

> ~~**Varning: Du kanske inte kan gå tillbaka till `main` efter att ha bytt till den här grenen.** På GitHub är detta utvecklingsgrenen (`develop`).~~
{.is-danger}

- v4 develop - ![Nuvarande v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) - (Alfa/Ostabilt): **För användare som inte använder Docker är grenen `develop` när v4 är installerat. För användare som använder Docker är detta troligen taggen `develop`** Detta är det senaste för Sonarr v4 Beta. Det släpps så snart kod har begåtts och passerat alla automatiserade tester. Denna version kan ännu inte ha använts av oss eller andra användare. Det finns ingen garanti för att den ens kommer att fungera i vissa fall. Denna gren rekommenderas endast för avancerade användare. Problem och egen felsökning förväntas i denna gren. På GitHub är detta utvecklingsgrenen (`develop`).

> **Varning: Du kan inte gå tillbaka till (v3) `main` eller (v3) `develop` efter att ha bytt till v4-grenen utan att installera om och hitta en v3-säkerhetskopia.** På GitHub är detta utvecklingsgrenen (`develop`).
{.is-danger}

> v3 **icke-Docker**-installationer kan **inte** uppgraderas direkt till v4 och kräver installation av Sonarr v4
{.is-info}

- Observera: Om din installation görs via Docker lägg till `:release`, `:latest`, `:nightly` eller `:develop` i slutet av din behållartagg beroende på vem som gör dina byggen.

|                                                                    | `main` (stabilt) ![Nuvarande Main/Senaste](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Main&query=%24%5B%27v3-stable%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v3) (beta) ![Nuvarande v3 Develop/Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=Develop&query=%24%5B%27v3-nightly%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) | `develop` (v4) (v4 beta) ![Nuvarande v4 Beta](https://img.shields.io/badge/dynamic/json?color=f5f5f5&label=v4-preview&query=%24%5B%27v4-preview%27%5D.version&url=https%3A%2F%2Fservices.sonarr.tv%2Fv1%2Freleases) |
|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [hotio](https://hotio.dev/containers/sonarr)                       | `release`                                                                                                                                                                                             | `nightly`                                                                                                                                                                                                   | `v4`                                                                                                                                                                                                            |
| [LinuxServer.io](https://docs.linuxserver.io/images/docker-sonarr) | `latest`                                                                                                                                                                                              | `3.0.10`                                                                                                                                                                                                     | `develop`                                                                                                                                                                                                       |

### Installera en nyare version

#### Native

1. Gå till System och sedan till fliken Updates.
1. Nyare versioner som inte är installerade än kommer att ha en uppdateringsknapp bredvid dem. Klicka på den knappen för att installera uppdateringen.

> v3 kan inte uppdateras till beta v4 och kräver manuell installation. Se [v4 Beta Announcement](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/) för mer information.
{.is-info}

#### Docker

1. Dra om din tagg och uppdatera din container.

## Kan jag växla från `develop` tillbaka till `main`?

- Se posten nedan

## Kan jag växla mellan grenar?

> Du kan (nästan) alltid öka din risk.{.is-info}

- `main` kan gå till `develop`
- Se nedan eller kontrollera med utvecklingsteamet för att se om du kan växla från `develop` till `main` för din specifika version.
- Om du inte följer dessa instruktioner kan det resultera i att din Sonarr blir oanvändbar eller kastar fel. Du har blivit varnad. Om följande fel uppstår använder du en nyare databas med en äldre \*Arr-version som inte stöds. Uppgradera \*Arr till den version du tidigare hade eller en nyare.
  - Exempel på felmeddelanden:
    - `Error parsing column 45 (Language=31 - Int64)`
    - `The DataMapper was unable to load the following field: 'Languages' value`
    - `ID does not match a known language Parameter name: id`
    - Andra liknande databasfel som rör saknade kolumner eller tabeller.
- **Uppdatering 7 augusti 2022**
  - `3.0.9.1549` har släppts som main/stabil
  - För de som är på develop och fortfarande är på `3.0.9.1549` eller lägre kan du säkert gå tillbaka till main
  - Om du har en nyare version kan du *fastna* på nightly/develop tills en ny stabil version släpps. Om du har en säkerhetskopia från innan du uppgraderade förbi den ovan nämnda versionen kan du installera om och återställa säkerhetskopian. Kontrollera med utvecklingsteamet för att se om du kan gå tillbaka säkert.

# Sonarr och problem med serier + metadata

## Hur hanterar Sonarr problem med numrering av scener (American Dad!, etc)?

### Hur Sonarr hanterar problem med numrering av scener

- Sonarr förlitar sig på [TheXEM](http://thexem.info/), en community-driven webbplats som låter användare skapa kartläggningar av program som scenerna (de som postar filerna) och TheTVDb (som vanligtvis följer nätverkets numrering). Det finns redan ett antal program där, men det är enkelt att lägga till ett till och vanligtvis accepteras ändringarna inom ett par dagar (om de är korrekta). TheXEM används för att korrigera skillnader i avsnittsnumrering (olikhet om ett avsnitt är en special eller inte) samt skillnader i säsongnummer, som att avsnitt släpps som S10E01, men TheTVDb listar samma avsnitt som S2017E01.
- XEM fixar vanligtvis problemen när releasegruppernas numrering inte matchar TVDb-numreringen så att Sonarr inte fungerar. Där kommer [XEM](http://thexem.info) in i bilden och skapar en karta för Sonarr att titta på.
- Releasegrupper släpper dubbla avsnitt i en enda fil eftersom det är så de sänds, men TVDb markerar varje avsnitt individuellt.
- Releasegrupper använder ett år för säsongen S2010 och TVDb använder S01.
- [XEM](http://thexem.info) fungerar i de flesta fall och håller allt smidigt utan att du någonsin märker det. Men som med det mesta kommer det alltid att finnas *problemfall* och i det här fallet finns det en lista över dem.

> Vissa indexerare eller releasegrupper kan följa TVDb istället för `Scene` (dvs. XEM).
> Om detta observeras, skicka in dem via scenkartläggningsformuläret.
{.is-info}

- [Tjänster för begärda kartläggningar *Granska och se till att aliaset och releasen inte redan har begärts eller lagts till*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Tjänster för begäran om scenkartläggning *Gör en ny begäran om ett alias. Se till att formuläret fylls i fullständigt*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

### Problemprogram

> Detta är på inget sätt en heltäckande lista över program som har kända problem med scenkartläggning; men dessa är några vanliga exempel.
{.is-info}

- Detta är en ofullständig lista över kända program och hur/varför de är problematiska:
- American Dad {#problemshow-americandad}
  - På grund av förändringar i nätverkets säsonger är American Dad vanligtvis fel med 1 säsong mellan releaser och TVDb. Se XEM-kartan för detaljer.
  - [American Dad](https://thexem.info/xem/show/4948) är för närvarande på S19 baserat på TVDb eller S18 baserat på Scene vid tidpunkten för denna skrivning. Så om du söker i Sonarr efter Säsong 19 kommer du **endast** att få resultat för Säsong 18 på grund av XEM-kartan.
  - Om du har en indexerare / releasegrupp med avsnitt från Säsong 19, skicka in dem via scenkartläggningsformuläret och se till att de inte redan har begärts
    - [Tjänster för begärda kartläggningar *Granska och se till att aliaset och releasen inte redan har begärts eller lagts till*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Tjänster för begäran om scenkartläggning *Gör en ny begäran om ett alias. Se till att formuläret fylls i fullständigt*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- Paw Patrol {#problemshow-pawpatrol}
  - Dubbla avsnittsfiler jämfört med enskilda avsnitt på TVDb, men inte alla avsnitt är dubbla, så kartläggningen kan bli felaktig och peka på vilka som är enskilda avsnitt och vilka som är dubbla.
- Pokémon {#problemshow-pokemon}
  - På TheXem följer [Pokemon](http://thexem.info/xem/show/4638) *dubbade* avsnitt. Så om du vill ha textade avsnitt kan du ha otur. Om vissa releasegrupper följer TVDb och inte XEM-kartläggning, skicka in dem via scenkartläggningsformuläret och se till att de inte redan har begärts
    - [Tjänster för begärda kartläggningar *Granska och se till att aliaset och releasen inte redan har begärts eller lagts till*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
    - [Tjänster för begäran om scenkartläggning *Gör en ny begäran om ett alias. Se till att formuläret fylls i fullständigt*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
   {.links-list}
- La Casa de Papel / Money Heist  {#problemshow-moneyheist}
  - TVDb har den ursprungliga sändningsordningen från det spanska nätverket, men Netflix köpte rättigheterna och klippte om serien till ett annat antal avsnitt. Detta gör att "säsong 5" importeras över befintliga "säsong 3"-avsnitt. [Ytterligare information finns i denna reddit-tråd](https://old.reddit.com/r/sonarr/comments/pdrr6l/money_heist_mess/)
- Kamen Rider {#problemshow-kamenrider}
  - Antologien ([TVDb ID 74096](https://thetvdb.com/series/kamen-rider)) bör användas i Sonarr för automatisering, eftersom detta program har både en antologi (som samlar alla säsonger) och de individuella säsongerna som listas som separata poster på TVDb. På grund av att antologin har individuella säsongsnamn i [TheXEM](https://thexem.info/xem/show/5376) är det inte möjligt att lägga till de individuella säsongsposterna i Sonarr utan att manuellt ladda ner och importera releaser.
- Bleach: Thousand-Year Blood War {#problemshow-bleach}
  - Den nyaste säsongen av Bleach: Thousand-Year Blood War släpps med olika namnscheman, vilket gör det svårt att automatisera och potentiellt skriva över några av dina befintliga avsnitt. Den kan bara automatiseras om din releasegrupp antingen:
    - Släpper avsnitten med S17Exx-numrering, eller
    - Släpper dem med rätt titel för Säsong 2-serien (hittas här <https://thexem.info/xem/show/5476>) och har börjat denna nya båge vid absolut avsnittsnummer 1.
- Great Asian Railway Journeys {#problemshow-greatasianrail}
  - Great Asian Railway Journeys sändes först som 20 mindre avsnitt, men sändes senare om som 10 långa avsnitt. Dessa längre kombinerade avsnitt lades till som Specials och bör namnges därefter. (S00E01, osv, ...)
- Horizon {#problemshow-horizon}
  - Ett program som sporadiskt sänder avsnitt sedan 1964. Detta gör kartläggningen särskilt svår, som du kan se på [TheXEM](https://thexem.info/xem/show/5495). De intresserade kan hitta den ursprungliga diskussionen på Sonarr discord [här](https://discord.com/channels/383686866005917708/649018968559845376/1046898050909622312).
- Kaleidoscope (2023) {#problemshow-kaleidoscope}
  - Kaleidoscope (2023) släpptes på Netflix som en icke-linjär serie, vilket innebär att varje användare fick en annan ordning när de tittade på serien. Detta orsakar ett problem för Sonarr eftersom releasegrupper har olika avsnittsordning för programmet. För att förhindra felaktig kartläggning av avsnitt kommer Sonarr inte automatiskt att hämta avsnitt och du måste hämta och importera avsnitten manuellt. Du kan matcha dem baserat på avsnittstitel eller genom att förhandsgranska de första sekunderna och se vilken färg avsnittet har som matchar titeln.

Några exempel på andra program som vanligtvis har problem, de flesta av dem kan lösas genom TheXEM-mappningar är: Arrested Development, Kitchen Nightmares (US), Mythbusters, Pawn Stars.

## Varför kan inte Sonarr importera avsnittsfiler för serie X? / Varför kan inte Sonarr hitta utgåvor för serie X?

Det kan finnas flera anledningar till varför Sonarr inte kan hitta eller importera avsnitt för en viss serie.

> Sonarr använder inte alias eller översättningar (t.ex. titlar på främmande språk) från TVDb.
{.is-warning}

> **För indexerare som stöder sökningar baserade på ID**, används seriens TVDbID eller IMDbID för sökning. Serietitlar och eventuella alias används endast om ID-baserade sökningar inte ger några resultat.
{.is-info}

- Sonarr förlitar sig på att kunna matcha titlar, ofta använder uppladdarna olika titlar för avsnitten, t.ex. `CSI: Crime Scene Investigation` postas bara som `CSI`, så Sonarr kan inte matcha namnen utan hjälp. Detta hanteras av Scene Mapping som Sonarr-teamet underhåller.
- Du kan också vilja granska [FAQ-posten för problematiska program och problem med numrering av releasegrupp vs. TVDb](#how-does-sonarr-handle-scene-numbering-issues-american-dad-etc)

> **För all japansk anime måste alias läggas till på [thexem.info](https://thexem.info)**, för andra serier för att begära en ny mappning, se stegen nedan. Mer information finns hos några av XEM-personerna som hänger i #XEM-kanalen på Sonarr Discord.
{.is-danger}

- [Tjänster begärda mappningar *Granska och se till att aliaset och utgåvan inte redan har begärts eller lagts till*](https://docs.google.com/spreadsheet/ccc?key=0Atcf2VZ47O8tdGdQN1ZTbjFRanhFSTBlU0xhbzhuMGc#gid=0)
- [Tjänster Scene Mapping-begäran *Gör en ny begäran om ett alias. Se till att formuläret fylls i fullständigt*](https://docs.google.com/forms/d/15S6FKZf5dDXOThH4Gkp3QCNtS9Q-AmxIiOpEBJJxi-o/viewform)
{.links-list}

> Vanligtvis läggs tjänstebegäranden till inom 1-5 dagar
{.is-info}

> Begär inte en mappning för japansk anime; använd XEM för det.
> Mer information finns hos några av XEM-personerna som hänger i [\#XEM-kanalen på Sonarr Discord](https://discord.gg/Z3D6u5hBJb)
{.is-danger}

> Om en icke-japansk serie kräver säsongsmappning (t.ex. släppt som S25E26 men TVDB är S26E2, då krävs en XEM-mappning. Detta kan inte göras med tjänstemappning.
{.is-info}

> Serien "Helt Perfekt" med TVDb-ID: 343189 och 252077 är svår att automatisera på grund av att TVDb har samma namn för båda programmen, vilket bryter mot TVDb:s egna regler. Det första inlägget för serien får namnet. Alla framtida inlägg för serien måste ha året som en del av seriens namn. Men ett undantag för scenen har lagts till för att mappa utgåvor (skiftlägeskänslig mappning) Helt Perfekt-utgåvor som innehåller `NORWEGIAN` -\> `252077` och innehåller `SWEDISH` -\> `343189`
{.is-info}

## TVDb uppdateras, varför uppdateras inte Sonarr?

{#tvdb}

- TVDb har en cache på 24 timmar på sin API.
- TVDb:s API måste sedan fylla på genom sin CDN-cache, vilket tar flera timmar.
- Sonarrs Skyhook har en mycket mindre cache på några timmar ovanpå det.
- Dessutom körs Sonarr bara uppdatering av serier var 12:e timme. Denna uppgift kan köras manuellt från System => Uppgifter; "Uppdatera alla" från Serieindex eller köras manuellt för en specifik serie på den seriens sida.

- Därför tar det vanligtvis mellan 36 och 48 timmar (24 + ~3 + ~3 + 12) för en ändring på TVDb att automatiskt komma in i Sonarr.
- Om en serie eller avsnitt saknas på TVDb tar det 36 till 48 timmar från det att de läggs till för att visas i din Sonarr-instans.

{#missing-episodes}

- Om du vet att en uppdatering av TVDb gjordes för mer än 48 timmar sedan, diskutera det gärna på vår [Discord](https://discord.sonarr.tv/).

## Varför kan jag inte lägga till en serie?

{#why-can-i-not-add-a-new-series}

- Om TheTVDb inte är tillgängligt kan Sonarr inte få sökresultat och du kommer inte att kunna lägga till några nya serier genom att söka. Du kan eventuellt lägga till en ny serie genom TVDbID om du vet vad det är, gränssnittet förklarar hur du lägger till det med ett ID.
- Sonarr kan inte lägga till någon serie som inte har en engelsk titel. Om du försöker lägga till en serie via TVDbID som inte har en engelsk titel kommer serien inte att hittas. Om ingen engelsk titel finns för den serien på TheTVDb måste den läggas till och sedan [måste man vänta på att TVDb:s cache rensas](#tvdb).
- Programmet måste vara en TV-serie och inte en film. Den måste också finnas på TVDb. Om den finns på IMDB, TMDB eller någon annanstans, men inte på TVDb kan du inte lägga till programmet.
- Serien måste finnas på TVDb
- Vissa serier kan faktiskt betraktas som fortsättningar och säsonger i sin primära serie.
  - Några kända serier/säsonger är:
  - [Dexter New Blood var Säsong 9](https://thetvdb.com/series/dexter/seasons/official/9) men det är nu [sin egen serie](https://thetvdb.com/series/dexter-new-blood)

## Varför kan jag inte lägga till en serie när jag vet TVDb-ID:t?

{#why-cant-i-add-a-new-series-when-i-know-the-tvdb-id}

- Sonarr kan inte lägga till någon serie som inte har en engelsk titel. Om du försöker lägga till en serie via TVDbID som inte har en engelsk titel kommer serien inte att hittas. Om ingen engelsk titel finns för den serien på TheTVDb måste den läggas till (om den är tillgänglig).
- Kontrollera URL:en/serien - Sonarr stöder inte filmer; använd [Radarr](/radarr) för filmer

## Titelslug används redan

- Det finns två huvudsakliga orsaker till detta fel som listas nedan.

## Dubblettitlar utan år

- Detta fel uppstår ofta när två serier har samma titel på TheTVDB, om så är fallet bör det andra programmet ha året tillagt i seriens titel.
  - Serie A
  - Serie A (2021)
- För att rätta till detta, vänta på att någon till slut (kanske) uppdaterar TVDb eller uppdatera TVDb själv. När det är rättat **och när det har godkänts av TVDb:s moderatorer**, på grund av [TVDb:s API-problem](#tvdb-is-updated-why-isnt-sonarr), när det är uppdaterat måste du vänta 30+ timmar innan den rättade titeln kan användas i Sonarr.

## Dubblettitlar med skiljetecken

- Det kommer också att hända med två liknande namngivna serier som bara kan skilja sig åt genom skiljetecken, om så är fallet, rapportera detta på [Sonarr Discord](https://discord.sonarr.tv/).
  - Joe's Show (2022)
  - Joes Show (2022)

## Avsnittet har inte ett absolut nummer

- Avsnitten på TVDb har inget absolut nummer tilldelat. Uppdatera serien på TVDb om det behövs och vänta sedan 36-48 timmar för att uppdateringen ska rensa TVDb:s interna cache och laddas in i Sonarr

## Sändningstider för avsnitt

- Inom Sonarr baseras sändningsdatum och -tider som visas i webbläsaren på klientens tid/tidszon, alla tider skickas från Sonarr till webbläsaren som UTC-tider (ISO-8601-formaterade för att vara exakta)
- TVDb föreskriver - med undantag för streamingtjänster - att sändningstiden och datumet baseras på den primära sändningsnätverkets lokala tid i landets mest populära stad. [Se TVDb:s FAQ-post för detaljer](https://support.thetvdb.com/kb/faq.php?id=29)
- Avsnittets sändningsdatum och sändningstid på TVDb konverteras till UTC och använder Sonarrs tidszon som är kartlagd i Skyhook av Sonarr-teamet för det nätverk som TVDb har för serien.
  - I det sällsynta fallet att ett nätverk inte är kartlagt kommer tiden i TVDb att antas vara US EST (UTC-5).
  - Om sändningstiden inte verkar stämma överens när man konverterar från sändningstidens lokala tidszon för nätverket till webbläsarens tidszon är det troligt att nätverket behöver kartläggas i Skyhook. [Kontakta utvecklingsteamet på Discord](https://discord.sonarr.tv/) för support med att uppdatera nätverkets tidszon.  

# Vanliga problem med Sonarr

## Sökvägen är redan konfigurerad för en befintlig serie

- Biblioteksimporten visar "Befintlig" eller så får du ett felmeddelande "Sökvägen är konfigurerad för en befintlig serie"
- Detta inträffar när du försöker lägga till en serie eller redigera en befintlig series sökväg som redan är tilldelad en annan serie.
- Troligtvis orsakades detta av att du inte rättade till en felmatchad serie när du importerade ditt bibliotek.
- Hitta och rätta till filmen som redan är tilldelad den seriens sökväg.
  - Serieindex
  - Tabellvy
  - Alternativ => Lägg till sökväg som en kolumn
  - Sortera och hitta filmen på den noterade problematiska sökvägen.
- Alternativt kan du ta bort serien med den befintliga sökvägen från Sonarr

## System och loggar laddas för evigt

- Det beror på easy-privacy blocklist. De blockerar i princip alla URL:er med /api/log? i sig. Granska listan och avgör om du tycker att det är en vettig idé att blockera alla URL:er i den, det finns dussintals URL:er där som potentiellt bryter webbplatser. Du valde det i din annonsblockerare. Det enklaste sättet är att lägga till domänen där Sonarr körs på i vitlistan. Men jag rekommenderar fortfarande att du kontrollerar listan.

## Konstiga UI-problem

- Om du upplever några konstiga UI-problem, som att bibliotekssidan inte listar något eller att en viss vy eller sortering inte fungerar, försök att visa det i ett Chrome Inkognitofönster eller Firefox Privat fönster. Om det fungerar bra där, rensa webbläsarens cache och cookies för din specifika IP/domän. För mer information, se [Rensa cache, cookies och lokal lagring](/useful-tools#clearing-cookies-and-local-storage) wiki-artikeln.

## Webbgränssnittet laddas bara på localhost på Windows

- Om du bara kan nå ditt webbgränssnitt på <http://localhost:8989/> eller <http://127.0.0.1:8989>, måste du köra Sonarr som administratör minst en gång.

## Jag fick ett popup-fönster som sa att config.xml är korrupt, vad gör jag nu?

- Sonarr kunde inte läsa din konfigurationsfil vid start eftersom den blev korrupt på något sätt. För att få Sonarr tillbaka online måste du ta bort `.xml` i din [AppData-mapp](/sonarr/appdata-directory) när du har tagit bort den startar du Sonarr och den startar på standardporten (8989), du bör nu konfigurera om eventuella inställningar du konfigurerade på sidan för allmänna inställningar.

## Ogiltigt certifikat och andra HTTPS- eller SSL-problem

- Om du inte använder Windows är det troligt att dina monos certifikat är föråldrade och behöver synkroniseras. [Se avsnittet om mono ssl i installationsartikeln för detaljer](/sonarr/installation#mono-ssl-issues)
- Din nedladdningsklient slutade fungera och du får ett fel som "Localhost har ett ogiltigt certifikat"?
  - Sonarr validerar nu SSL-certifikat. Om det inte finns något SSL-certifikat som är inställt i nedladdningsklienten, eller om du använder ett självsignerat https-certifikat utan att lägga till CA-certifikatet i din lokala certifikatbutik, kommer Sonarr att vägra att ansluta. Gratis korrekt signerade certifikat finns tillgängliga från [let's encrypt](https://letsencrypt.org/).
  - Om din nedladdningsklient och Sonarr är på samma maskin finns det ingen anledning att använda HTTPS, så det enklaste sättet är att inaktivera SSL för anslutningen. De flesta skulle hålla med om att det inte är nödvändigt i ett lokalt nätverk heller. Det är möjligt att inaktivera certifikatvalidering i avancerade inställningar om du vill behålla en osäker SSL-konfiguration.

## Hur stoppar jag webbläsaren från att starta vid uppstart?

Beroende på ditt operativsystem finns det flera möjliga sätt.

- I `Inställningar` => `Allmänt` på vissa operativsystem finns det en kryssruta för att starta webbläsaren vid uppstart.
- När du startar Sonarr kan du lägga till `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumenten.
- Stoppa Sonarr och redigera config.xml-filen och ändra `<LaunchBrowser>True</LaunchBrowser>` till `<LaunchBrowser>False</LaunchBrowser>`.

## VPN, Jackett och \*ARRs

- Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika är det vanligtvis bara torrentklienten som behöver vara bakom en VPN. Eftersom VPN-ändpunkten delas av många användare kan du och kommer att uppleva hastighetsbegränsningar, DDOS-skydd och IP-blockeringar från olika tjänster som varje program använder.
- Med andra ord kan det att sätta \*Arrs (Lidarr, Prowlarr, Radarr, Readarr och Lidarr) bakom en VPN göra applikationerna oanvändbara i vissa fall på grund av att tjänsterna inte är tillgängliga.

> **För att vara tydlig handlar det inte om ifall VPN kommer att orsaka problem med \*Arrs, utan när: bildleverantörer kommer att blockera dig och cloudflare finns framför de flesta \*Arr-servrar (uppdateringar, metadata osv.) och kan också blockera dig**
{.is-warning}

- **Många privata spårare kommer att blockera dig om du använder eller får åtkomst till dem (dvs. använder Jackett eller Prowlarr) via en VPN.**

### Användning av en VPN

- Om en VPN krävs och Docker används rekommenderas det att använda Hotio eller Binhexs Download Client + VPN Containers.
- Om en VPN krävs och Docker inte används måste din VPN-klient ***stödja split tunneling*** så att endast de nödvändiga (nedladdningsklient) apparna är bakom VPN:n.
- Många problem med att komma åt spårare kan lösas genom att använda Googles eller Cloudflares DNS-servrar istället för din internetleverantörs DNS-servrar.
- I vissa fall (t.ex. brittiska internetleverantörer) kan du behöva placera din torrentnedladdningsklient bakom en VPN och Jackett/Prowlarr enligt följande:
  - placera Jackett bakom VPN:n och se till att split tunneling tillåter lokal åtkomst
  - för Prowlarr konfigurerar du din VPN-klient för att tillhandahålla en proxy och lägger till proxyn i Inställningar => Indexerare. Ge proxyn en tagg och ge samma tagg till alla indexerare som behöver använda den.
    - Om det absolut krävs och om din VPN inte har ett sätt att skapa en proxy kan du placera Prowlarr bakom VPN:n och se till att split tunneling tillåter lokal åtkomst.

## Jag ser loggmeddelanden för program som jag inte har/vill ha

- Dessa meddelanden är helt normala och kommer från RSS-flödena som Sonarr kontrollerar för att se om det finns avsnitt du vill ha, vanligtvis visas dessa bara i debug-/trace-loggning, men om det uppstår ett problem med att bearbeta en post kan du se en varning eller ett felmeddelande. Det är säkert att ignorera varningar/felmeddelanden eftersom de gäller program som du inte vill ha, om det gäller ett program du vill ha, öppna en supporttråd på forumet.

## Delningstorrentar raderas inte automatiskt

- När en torrent som fortfarande delas importeras kopieras den eller skapas en hård länk (om det är aktiverat och *möjligt*) så att torrentklienten kan fortsätta dela. I en idealisk konfiguration kommer torrentnedladdningsmappen och biblioteksmappen att vara på samma filsystem och *se ut som det* (Docker och nätverksdelningar gör det lätt att göra fel), vilket gör att hård länkning är möjligt och minimerar slöseri med utrymme.
- Dessutom kan du konfigurera dina mål för seedtid/-förhållande i Sonarr eller din nedladdningsklient, ställa in din nedladdningsklient att *pausa* eller *stoppa* när de uppnås och aktivera "Ta bort" under "Avslutade och misslyckade nedladdningar". På så sätt kommer torrenter som är färdiga att sluta dela att tas bort från nedladdningsklienten av Sonarr.

## Hjälp, min Mac säger att Sonarr inte kan öppnas eftersom utvecklaren inte kan verifieras

- Detta är enkelt, se denna länk för mer information [här](https://support.apple.com/sv-se/guide/mac-help/mh40616/mac)
[![Utvecklaren kan inte verifieras](/assets/general/faq_1_mac.png)]

## Hjälp, min Mac säger att Sonarr.app är skadad och kan inte öppnas

- Det beror antingen på en korrupt nedladdning, så försök igen eller [säkerhetsproblem, se denna relaterade FAQ-post.](#help-my-mac-says-sonarr-cannot-be-opened-because-the-developer-cannot-be-verified)

## Jag får ett felmeddelande: Databasens diskavbildning är skadad

> Du kan få detta efter att ha uppgraderat sqlite3 till 3.41. Sonarr v3.0.9 stöder inte sqlite3 3.41 på grund av en brytande standardändring. [Information om problemet finns i Sonarr GHI #5464](https://github.com/Sonarr/Sonarr/issues/5464)
> Detta är löst med Sonarr v3.0.10 och användare bör uppgradera Sonarr därefter.
{.is-warning}

- **Fel med `Error creating log database` indikerar problem med logs.db**
  - Detta kan snabbt åtgärdas genom att byta namn på eller ta bort databasen. Logs-databasen innehåller oviktig information om kommandohistorik och uppdateringsinstallationshistorik, samt Info-, Warn- och Error-poster.
- **Fel med `Error creating main database` eller generellt `database disk image is malformed` utan angiven databas indikerar problem med sonarr.db**
  - Fortsätt med de nedan angivna stegen.
- Detta innebär att din SQLite-databas som lagrar största delen av informationen för Sonarr är korrupt. Dina alternativ är att försöka använda (en) säkerhetskopia(r), försöka återställa den befintliga databasen, försöka återställa säkerhetskopiorna eller om inget annat fungerar börja om med en helt ny databas.
- Detta fel kan visas om databasfilen inte kan skrivas av användaren/gruppen som \*Arr körs som. Problem med behörigheter kommer troligen bara att vara ett problem för nya installationer, migrerade installationer till en ny server, om du nyligen har ändrat behörigheterna för din appdata-katalog eller om du har ändrat användaren och gruppen som \*Arr körs som.
- Ditt bästa och första alternativ är att [försöka återställa från en säkerhetskopia](#how-do-i-backuprestore-my-sonarr)
- Du kan också försöka återställa din databas. Detta är vanligtvis det enda alternativet när detta problem uppstår efter en uppdatering. Prova [sqlite3-kommandot `.recover`](/useful-tools#recovering-a-corrupt-db)
  - Om din sqlite inte har `.recover` eller om du vill ha ett mer användarvänligt sätt (t.ex. för Windows) kan du följa [våra instruktioner på denna wiki](/useful-tools#recovering-a-corrupt-db-ui)
- En annan möjlig orsak till att du får ett fel med din databas är att du placerar din databas på en nätverksenhet (nfs eller smb eller något annat som inte är lokalt). **SQLite är utformat för situationer där data och program existerar på samma maskin.** Därför måste din \*Arr AppData-mapp (/config-montering för docker) vara på lokal lagring. [SQLite och nätverksenheter fungerar inte bra tillsammans och kommer så småningom att orsaka en felaktig databas](https://www.sqlite.org/draft/useovernet.html).
- Om du använder mergerFS måste du ta bort `direct_io` eftersom SQLite använder mmap som inte stöds av `direct_io`, som förklaras i mergerFS [dokumentationen här](https://github.com/trapexit/mergerfs#plex-doesnt-work-with-mergerfs)

## Jag använder Sonarr på en Mac och det slutade plötsligt fungera. Vad har hänt?

- Troligen beror detta på en bugg i MacOS som orsakade att en av Sonarr-databaserna blev korrupt.
- [Följ dessa steg för att lösa problemet](#i-am-getting-an-error-database-disk-image-is-malformed)
- Försök sedan starta Sonarr och se om det fungerar. Om det inte fungerar behöver du ytterligare support. Skriv ett inlägg på vår [reddit](http://reddit.com/r/Sonarr) eller gå med i [discord](https://discord.sonarr.tv/) för hjälp.

## Varför kan inte Sonarr se mina filer på en fjärrserver?

- För alla operativsystem, se till att användaren/gruppen som \*Arr körs som har läs- och skrivåtkomst till den monterade enheten.
- För Linux, se till att:
  - Om du använder en NFS-montering, se till att `nolock` är aktiverat för din montering.
  - Om du använder en SMB-montering, se till att `nobrl` är aktiverat för din montering.
- För Windows: Kort sagt kan användaren som \*Arr körs som (om det är en tjänst) eller under (om det är en programfält-app) inte komma åt filvägen på fjärrservern. Detta kan bero på olika orsaker, men den vanligaste är att \*Arr körs som en tjänst, vilket orsakar de problem som beskrivs nedan.

### Sonarr körs som standard under LocalService-kontot, som inte har åtkomst till skyddade fjärrfilresurser

- Kör Sonarr-tjänsten som en annan användare som har åtkomst till den resursen
- Öppna fönstret Administrativa verktyg \> Tjänster på din Windows-server.
- Stoppa Sonarr-tjänsten.
- Öppna dialogrutan Egenskaper \> Logga på.
- Ändra användarkontot för tjänsten till målkontot.
- Kör Sonarr.exe genom att använda mapparna för automatisk start

### Du använder en mappad nätverksenhet (inte en UNC-sökväg)

- Ändra dina sökvägar till UNC-sökvägar (`\\server\share`)
- Kör Sonarr.exe via mapparna för automatisk start

## Mappade nätverksenheter kontra UNC-sökvägar

- Användning av mappade nätverksenheter fungerar generellt sett inte särskilt bra, särskilt när Sonarr är konfigurerat att köras som en tjänst. Det bättre sättet att konfigurera delade resurser är att använda UNC-sökvägar. Så istället för `X:\TV` använder du `\\Server\TV`.

- En viktig sak att komma ihåg är att Sonarr får sökvägsinformation från nedladdaren, så du måste *också* konfigurera NZBGet, SABNzbd eller någon annan nedladdare att använda UNC-sökvägar.

## Sonarr kommer inte att fungera på Big Sur

Kör

```shell
chmod +x /Applications/Sonarr.app/Contents/MacOS/Sonarr
```

## Mitt anpassade skript slutade fungera efter uppgradering från v2

- Du har förmodligen skickat argument i din anslutning... vilket inte stöds.
- För att åtgärda detta:
  1. Ändra ditt argument till att vara din sökväg
  1. Se till att shebang i ditt skript matchar din pwsh-sökväg (om du inte har en shebang-definition där, lägg till den)
  1. Se till att pwsh-skriptet är körbart

# Vanliga problem med Sonarr-sökning och nedladdning

## Framgångsrik fråga - Inga resultat returnerade

- [Se den här felsökningsposten](/sonarr/troubleshooting#query-successful-no-results-returned)

## Varför hämtade inte Sonarr en episod som jag förväntade mig?

Först, se till att du har läst och förstått avsnittet ovan som heter ["Hur hittar Sonarr episoder?](#how-does-sonarr-find-episodes) Se sedan till att minst en av dina indexerare har den episod du förväntade dig att hämta.

1. Klicka på ikonen "Manuell sökning" bredvid episodlistningen i Sonarr. Finns det några resultat? Om inte har antingen Sonarr problem med att kommunicera med dina indexerare, eller så har dina indexerare inte episoden, eller så är episoden felaktigt namngiven/kategoriserad på indexeraren.
1. **Om det finns resultat från steg 1**, kontrollera bredvid dem efter en röd utropsteckenikon. Hovra över ikonen för att se varför den utgåvan inte är en kandidat för automatiska nedladdningar. Om varje resultat har ikonen kommer ingen automatisk nedladdning att ske.
1. **Om det finns minst ett giltigt manuellt sökresultat från steg 2**, borde en automatisk nedladdning ha skett. Om det inte gjorde det är den mest troliga orsaken ett tillfälligt kommunikationsproblem som hindrar en RSS-synkronisering från din indexerare. Det rekommenderas att ha flera indexerare för bästa resultat.
1. **Om det inte finns något manuellt resultat från en serie, men du kan hitta den när du bläddrar på indexerarens webbplats** - Detta kan bero på olika orsaker, till exempel att utgåvan inte är korrekt taggad på din indexerare vilket gör att den inte returneras till Sonarr vid en automatisk sökning. Denna [felsökningspost](/sonarr/troubleshooting#searches-indexers-and-trackers) ger några tips om hur du kan fastställa orsaken. Att ha flera indexerare aktiva kan hjälpa till att lösa detta genom att ge fler källor till samma innehåll.

## Hittade matchande serier via hämtningshistorik, men utgåvan matchades med serien via ID. Automatisk import är inte möjlig

- Se [den här felsökningsposten](/sonarr/troubleshooting#found-matching-series-via-grab-history-but-series-was-matched-by-series-id-automatic-import-is-not-possible)

- På TVDb, när episodnamn är okända kommer de att ha titeln TBA och det finns en cache på 24 timmar på TVDb API. Vanligtvis tar ändringar på TVDb-webbplatsen 24-48 timmar att nå Sonarr på grund av TVDb-cache (24 timmar), skyhook-cache (några timmar) och serieuppdateringsintervallet (var 12:e timme). Inställningen [Episode Title Required](/sonarr/settings#importing) i Sonarr styr importbeteendet när titeln är TBA, men efter 48 timmar från sändningstillfället kommer utgåvan att importeras även om titeln fortfarande är TBA. Det finns heller ingen automatisk uppföljningsomdöpning av filer med TBA-titel. Observera att TBA-timern beräknas från episodens sändningsdatum och tid, inte från när du har hämtat den eller uppladdningstiden.

## Sonarr säger Okänd serie vid sökningar eller import

- Se posten [Varför kan inte Sonarr importera episodfiler för serie X? / Varför kan inte Sonarr hitta utgåvor för serie X?](/sonarr/faq#why-cant-sonarr-import-episode-files-for-series-x-why-cant-sonarr-find-releases-for-series-x)

## Jacketts /all-slutpunkt

{#jackett-all-endpoint}

- Jackett `/all`-slutpunkten är bekväm, men det är dess enda fördel. Allt annat kan orsaka problem, så det krävs att varje tracker läggs till individuellt. Alternativt kan du kanske vilja kolla in Jackett & NZBHydra2-alternativet [Prowlarr](/prowlarr)

- **Uppdatering 5 februari 2022: \*Arr Support har upphört för jackett `\all`-slutpunkten. Jackett /all-slutpunkten stöds inte längre (t.ex. varningar kommer att visas) från och med v3.0.6.1457 på grund av att den bara orsakar problem.**

- Jackett `/all`-slutpunkten är bekväm, men det är dess enda fördel. Allt annat kan orsaka problem, så nu krävs det att varje tracker läggs till individuellt.
- [Även Jacketts utvecklare säger att den bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Att använda /all-slutpunkten har inga fördelar, bara nackdelar:
  - du förlorar kontrollen över indexer-specifika inställningar (kategorier, söklägen, etc.)
  - blandning av söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
  - indexer-specifika kategorier (\>= 100000) kan inte användas.
  - långsamma indexerare kommer att sakta ner det totala resultatet
  - totala resultat är begränsade till 1000
  - om en av spårarna i /all returnerar ett fel kommer \*Arr att inaktivera den och nu får du inga resultat.

### Lösningar för Jackett /All

- Lägg till varje tracker i Jackett manuellt som en indexerare i \*Arr
- Kolla in [Prowlarr](/prowlarr) som kan synkronisera indexerare med \*Arr och kommer från Lidarr/Radarr/Readarr-utvecklingsteamet.
- Kolla in [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisera indexerare med \*Arr. Men använd inte deras enskilda samlade slutpunkt och använd `multi` om synkronisering kommer att användas.

## Jackett visar fler resultat än Sonarr vid manuell sökning

- Kontrollera dina konfigurerade kategorier för din tracker i Sonarr
- Detta beror vanligtvis på att Sonarr söker i Jackett på ett annat sätt än du gör. [Se den här felsökningsartikeln för mer information](/sonarr/troubleshooting#searches-indexers-and-trackers).

## Att hitta kakor

- Vissa webbplatser kan inte loggas in automatiskt och kräver att du loggar in manuellt och sedan ger kakorna till Sonarr för att det ska fungera. [Se den här artikeln för detaljer](/useful-tools#finding-cookies)

## Packa upp torrents

- De flesta torrentklienter har inte automatisk hantering av komprimerade arkiv som deras Usenet-motsvarigheter. Vi rekommenderar [unpackerr](https://github.com/unpackerr/unpackerr).

## Behörigheter

- Sonarr kommer att behöva flytta filer från där nedladdaren placerar dem till den slutliga platsen, så det betyder att Sonarr kommer att behöva läsa/skriva till både käll- och destinationsmappen och filerna.
- På Linux, där bästa praxis innebär att tjänster körs som sin egen användare, kommer detta förmodligen att innebära att du använder en delad grupp och ställer in mappbehörigheter till `775` och filer till `664` både i din nedladdare och Sonarr. I umask-notation skulle det vara `002`.

## Tvångsautentisering

- I Sonarr v4 (beta) är autentisering obligatorisk. Se [Sonarr v4 FAQ - Tvångsautentisering](/sonarr/faq-v4#forced-authentication) för detaljer