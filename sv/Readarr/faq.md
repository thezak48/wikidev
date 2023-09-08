- Yes, you can disable the refresh books task in Readarr. 
- Go to Settings and then the Tasks tab. 
- Find the task named "Refresh Books" and click on the toggle switch to disable it. 
- Disabling this task will prevent Readarr from automatically refreshing your book library.

- Nej, och du bör inte heller göra det genom någon SQL-hackning. Uppdatera böcker-uppgiften frågar uppströms Servarr-proxy och kontrollerar om metadata för varje bok (ID, rollista, sammanfattning, betyg, översättningar, alternativa titlar, etc.) har uppdaterats jämfört med vad som för närvarande finns i Readarr. Vid behov kommer den sedan att uppdatera de relevanta böckerna.
- En vanlig klagomål är att uppdateringsuppgiften orsakar tung I/O-användning. En inställning som kan orsaka problem är "Skanna om författarmapp efter uppdatering". Om din disk I/O-användning ökar under en uppdatering kan du vilja ändra inställningen för att vara `Manuell`. Ändra inte detta till `Aldrig` om inte alla ändringar i din samling (nya böcker, uppgraderingar, borttagningar etc.) görs genom Readarr. Om du tar bort bokfiler manuellt eller med ett tredjepartsprogram, ställ inte in detta till `Aldrig`.

## Kan jag ha BÅDE en e-bok och en ljudbokversion av samma bok?

- Nej. Med en enda Readarr-instans kan du antingen ha en eller den andra, men inte båda. Om du vill ha båda behöver du köra två separata instanser av Readarr (precis som vissa personer kör 2 instanser av Sonarr eller Radarr för 1080p- och 4K-versioner av sin media).

## Måste jag använda Calibre?

- Nej. I allmänhet erbjuder Calibre vissa ytterligare fördelar, som möjligheten att automatiskt konvertera e-böcker till ett annat format som är specifikt för din e-läsares kapacitet, samt att ansluta till den e-läsaren. Men om du inte använde Calibre innan du installerade Readarr är det förmodligen av begränsad nytta för dig att installera det, och det är ett mycket stort program.

## Varför kan inte Readarr se mina filer på en fjärrserver?

- För alla operativsystem, se till att användaren/gruppen som du kör \*Arr som har läs- och skrivåtkomst till den monterade enheten.
- För Linux, se till att:
  - Om du använder en NFS-montering, se till att nolock är aktiverat för din montering.
  - Om du använder en SMB-montering, se till att nobrl är aktiverat för din montering.
- För Windows: Kort sagt, användaren som \*Arr körs som (om det är en tjänst) eller under (om det är en programfältapp) kan inte komma åt filvägen på fjärrservern. Detta kan bero på olika orsaker, men det vanligaste är att \*Arr körs som en tjänst, vilket orsakar de problem som beskrivs nedan.

### Readarr körs som standard under LocalService-kontot som inte har åtkomst till skyddade fjärrfilresurser

- Kör Readarr-tjänsten som en annan användare som har åtkomst till den resursen
- Öppna fönstret Administrativa verktyg \> Tjänster på din Windows-server.
- Stoppa Readarr-tjänsten.
- Öppna dialogrutan Egenskaper \> Logga på.
- Ändra användarkontot för tjänsten till målkontot.
- Kör Readarr.exe genom att använda mapparna för automatisk start

### Du använder en kartlagd nätverksenhet (inte en UNC-sökväg)

- Ändra dina sökvägar till UNC-sökvägar (`\\server\share`)
- Kör Readarr.exe via mapparna för automatisk start

## Hjälp, jag har låst mig ute

{#hjalp-jag-har-glomt-mitt-losenord}

För att inaktivera autentisering (för att återställa ditt glömda användarnamn eller lösenord) måste du redigera `config.xml`, som kommer att finnas i [Readarr Appdata Directory](/readarr/appdata-directory)

1. Öppna config.xml i en textredigerare
1. Hitta raden för autentiseringsmetod, som kommer att vara
`<AuthenticationMethod>Basic</AuthenticationMethod>` eller `<AuthenticationMethod>Forms</AuthenticationMethod>`
1. Ändra raden för `AuthenticationMethod` till `<AuthenticationMethod>None</AuthenticationMethod>`
1. Starta om Readarr
1. Nu kan du komma åt Readarr utan lösenord, du bör gå till `Inställningar: Allmänt` i användargränssnittet och ange ditt användarnamn och lösenord

## Hur stoppar jag webbläsaren från att starta vid uppstart?

Beroende på ditt operativsystem finns det flera möjliga sätt.

- I `Inställningar` => `Allmänt` på vissa operativsystem finns det en kryssruta för att starta webbläsaren vid uppstart.
- När du startar Readarr kan du lägga till `-nobrowser` (*nix) eller `/nobrowser` (Windows) i argumenten.
- Stoppa Readarr och redigera config.xml-filen och ändra `<LaunchBrowser>True</LaunchBrowser>` till `<LaunchBrowser>False</LaunchBrowser>`.

## Konstiga problem med användargränssnittet

- Om du upplever konstiga problem med användargränssnittet, som att bibliotekssidan inte listar något eller att en viss vy eller sortering inte fungerar, försök att visa sidan i ett inkognitofönster i Chrome eller ett privat fönster i Firefox. Om det fungerar bra där, rensa webbläsarens cache och cookies för din specifika IP/domän. För mer information, se artikeln [Rensa cache, cookies och lokal lagring](/useful-tools#clearing-cookies-and-local-storage) i wikin.

## VPN, Jackett och \*ARRs

- Om du inte befinner dig i ett förtryckande land som Kina, Australien eller Sydafrika är det vanligtvis bara torrentklienten som behöver vara bakom en VPN. Eftersom VPN-ändpunkten delas av många användare kan du och kommer att uppleva begränsningar av hastigheten, DDOS-skydd och IP-blockeringar från olika tjänster som varje program använder.
- Med andra ord kan det göra \*Arrs (Lidarr, Prowlarr, Radarr, Readarr och Lidarr) oanvändbara i vissa fall om de placeras bakom en VPN på grund av att tjänsterna inte är tillgängliga.

> **För att vara tydlig handlar det inte om ifall VPN kommer att orsaka problem med \*Arrs, utan när: bildleverantörer kommer att blockera dig och cloudflare finns framför de flesta \*Arr-servrar (uppdateringar, metadata, etc.) och kan också blockera dig**
{.is-warning}

- **Många privata spårare kommer att blockera dig om du använder eller får åtkomst till dem (t.ex. genom Jackett eller Prowlarr) via en VPN.**

### Användning av en VPN

- Om en VPN krävs och Docker används rekommenderas att använda Hotio eller Binhex's Download Client + VPN Containers.
- Om en VPN krävs och Docker inte används måste din VPN-klient ***stödja split tunneling*** så att endast de nödvändiga (Download Client) apparna är bakom VPN:en.
- Många problem med att komma åt spårare kan lösas genom att använda Googles eller Cloudflares DNS-servrar istället för din internetleverantörs DNS-servrar.
- I vissa fall (t.ex. brittiska internetleverantörer) kan du behöva placera din torrentnedladdningsklient bakom en VPN och Jackett/Prowlarr enligt följande:
  - placera Jackett bakom VPN:en och se till att split tunneling tillåter lokal åtkomst
  - för Prowlarr, konfigurera din VPN-klient för att tillhandahålla en proxy och lägg till proxyt i Inställningar => Indexers. Ge proxyt en tagg och ge samma tagg till de indexers som behöver använda den.
    - Om det absolut krävs och om din VPN inte har något sätt att skapa en proxy kan du placera Prowlarr bakom VPN:en och se till att split tunneling tillåter lokal åtkomst.

## Jacketts /all-endpunkt

{#jackett-all-endpoint}

- Jacketts `/all`-endpunkt är bekväm, men det är den enda fördelen. Allt annat kan orsaka problem, så det krävs att varje spårare läggs till individuellt. Alternativt kan du överväga att använda det Jackett- och NZBHydra2-alternativet [Prowlarr](/prowlarr)
- **Uppdatering 20 januari 2022: Jacketts `/all`-endpunkt stöds inte längre (varningar kommer att visas) från och med 0.1.0.1188 på grund av att den bara orsakar problem.**
- Jacketts /all-endpunkt är bekväm, men det är den enda fördelen. Allt annat kan orsaka problem, så nu krävs det att varje spårare läggs till individuellt.
- [Även Jacketts utvecklare säger att den bör undvikas och inte användas.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Att använda /all-endpunkten har inga fördelar, bara nackdelar:
  - du förlorar kontrollen över specifika inställningar för varje spårare (kategorier, söklägen, etc.)
  - att blanda söklägen (IMDB, fråga, etc.) kan ge lågkvalitativa resultat
  - specifika kategorier för varje spårare (\>= 100000) kan inte användas.
  - långsamma spårare kommer att sakta ner det totala resultatet
  - det totala antalet resultat är begränsat till 1000
  - om en av spårarna i /all returnerar ett fel kommer \*Arr att inaktivera den och du får inga resultat.

### Lösningar för Jacketts /all-endpunkt

- Lägg till varje spårare i Jackett manuellt som en indexer i \*Arr
- Kolla in [Prowlarr](/prowlarr) som kan synkronisera indexers med \*Arr och som kommer från Lidarr/Radarr/Readarr-utvecklingsteamet.
- Kolla in [NZBHydra2](https://github.com/theotherp/nzbhydra2) som kan synkronisera indexers med \*Arr. Men använd inte deras enda aggregat-endpunkt, använd `multi` om synkronisering kommer att användas.

## Varför finns det två filer? | Varför finns det en fil kvar i nedladdningar?

Detta är normalt. Med en konfiguration som stöder [hårddisklänkar](https://trash-guides.info/hardlinks) kommer inte dubbel diskutrymme att användas. Nedan beskrivs hur torrentprocessen fungerar.

1. Readarr skickar en nedladdningsbegäran till din klient och associerar den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten. Exempel: filmer, tv, serier, musik, etc.
1. Readarr övervakar dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Denna övervakning sker via nedladdningsklientens API.
1. Slutförda filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (kvot eller tid kan justeras i nedladdningsklienten eller inom själva programmet under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer de att skapa en hårddisklänk till filen om det stöds av din konfiguration, annars kopieras filen om hårddisklänkar inte stöds.
1. Om alternativet "Hantering av slutförda nedladdningar - Ta bort slutförda" är aktiverat i Readarrs inställningar kommer Readarr att ta bort den ursprungliga filen och torrenten från din nedladdningsklient, men endast om nedladdningsklienten rapporterar att seedningen är klar och torrenten är stoppad.

> Hårddisklänkar är aktiverade som standard. [En hårddisklänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din mapp för slutförda nedladdningar och din mediebiblioteksmapp. Om skapandet av hårddisklänken misslyckas eller om din konfiguration inte stöder hårddisklänkar kommer den att falla tillbaka och kopiera filen.
{.is-info}

## Calibre säger "Calibre rejected duplicate book" men det är det inte

Om du använder Calibre-integrationen kommer Calibre ibland att avvisa en bok och säga att den är en duplicat. Det är förmodligen inte faktiskt en duplicat. Om detta händer kan inte Readarr göra mycket åt det, och du måste sluta övervaka den boken för att förhindra att Readarr fortsätter att försöka hämta den och skicka den till Calibre. Detta är bara en av de roliga nackdelarna med Calibre-integrationen.