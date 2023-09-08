# Status

## Health

- Denne side indeholder en liste over fejl ved helbredstjek. Disse helbredstjek udføres periodisk af Sonarr og ved visse begivenheder. De resulterende advarsler og fejl vises her for at give råd om, hvordan de kan løses.

### Systemadvarsler

#### Den aktuelt installerede .NET Framework er gammel og ikke understøttet

- Sonarr bruger .NET Framework. Vi skal bygge Sonarr mod den laveste understøttede version, der stadig bruges af vores brugere. Af og til øger vi den version, vi bygger mod, for at kunne udnytte nye funktioner. Tilsyneladende har du ikke anvendt de passende Windows-opdateringer i et stykke tid og skal opgradere .NET for at kunne bruge nyere versioner af Sonarr.

- Opgradering af .NET Framework er meget enkelt på Windows, selvom det ofte kræver en genstart.

#### Den aktuelt installerede .NET Framework er understøttet, men opgradering anbefales

- Sonarr bruger .NET Framework. Vi skal bygge Sonarr mod den laveste understøttede version, der stadig bruges af vores brugere. Opgradering til nyere versioner giver os mulighed for at bygge mod nyere versioner og bruge nye Framework-funktioner.

- Opgradering af .NET Framework er meget enkelt på Windows, selvom det ofte kræver en

#### Den aktuelt installerede mono-version er gammel og ikke understøttet

- Sonarr v4 er skrevet i .NET, og v3 krævede Mono. Mono 5.20 er det absolutte minimum for Sonarr.
- Opgraderingsproceduren for Mono varierer afhængigt af platformen.

> Mono understøttes ikke længere fra Sonarr version 4.0
{.is-warning}

#### Den aktuelt installerede SQLite-version understøttes ikke

- Sonarr gemmer sine data i en SQLite-database. Den SQLite3-bibliotek, der er installeret på dit system, er for gammel. Sonarr kræver mindst version 3.9.0.

> Bemærk, at Sonarr bruger `libSQLite3.so`, som muligvis er indeholdt i en opgraderingspakke til SQLite3.
{.is-info}

#### Besked fra pakkevedligeholder

- Din pakkevedligeholder har en besked til dig. Dette styres af din vedligeholder og ikke af Sonarr.

#### Der er en ny opdatering tilgængelig

- Glæd dig, udviklerne har udgivet en ny opdatering. Dette betyder generelt fantastiske nye funktioner og rettede fejl (ikke sandt?). Tilsyneladende har du ikke aktiveret automatisk opdatering, så du bliver nødt til at finde ud af, hvordan du opdaterer på din platform. Det er sandsynligvis en god start at trykke på knappen "Installer" på siden System => Opdateringer.

> Denne advarsel vises ikke, hvis din nuværende version er mindre end 14 dage gammel
{.is-info}

#### Kan ikke installere opdatering, fordi startmappe og/eller UI-mappe ikke kan skrives af brugeren

{#cannot-install-update-because-UI-folder-is-not-writable-by-the-user}

{#cannot-install-update-because-startup-folder-is-not-writable-by-the-user}

Dette betyder, at Sonarr ikke kan opdatere sig selv. Du bliver nødt til at opdatere Sonarr manuelt eller angive tilladelserne for Sonarrs startmappe (installationsmappen) for at tillade Sonarr at opdatere sig selv.

#### Kan ikke installere opdatering, fordi startmappe er i en App Translocation-mappe

I macOS Sierra tilføjede Apple en mærkelig sikkerhedsfunktion kaldet App Translocation (nogle gange kendt som Gatekeeper Path Randomization), hvilket betyder, at efter at have downloadet en applikation, hvis du ikke flytter den resulterende applikation et eller andet sted (hvor som helst!), med Finder (du skal bruge Finder!), vil applikationen køres, som om den er placeret på en tilfældigt valgt sti af systemet.

#### Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering

Sonarr har registreret, at AppData-mappen til dit operativsystem er placeret inde i mappen, der indeholder Sonarr-binærerne. Normalt ville det være C:\ProgramData for Windows og ~/.config for Linux.

Se på System => Info for at se de aktuelle AppData- og Startmappe. Dette betyder, at Sonarr ikke kan opdatere sig selv uden at risikere datatab.
Hvis du bruger Linux, skal du sandsynligvis ændre hjemmemappen for brugeren, der kører Sonarr, og kopiere indholdet af mappen ~/.config/Sonarr for at bevare din database.

#### Kunne ikke løse IP-adressen for den konfigurerede proxyvært

Gennemgå dine proxyindstillinger og sørg for, at de er korrekte
Sørg for, at din proxy er tændt, fungerer og er tilgængelig

#### Proxy mislykkedes test

Din konfigurerede proxy mislykkedes at teste succesfuldt, gennemgå den angivne HTTP-fejl og/eller kontroller logfilerne for flere detaljer.

#### Systemtiden er mere end 1 dag forkert

Systemtiden er mere end 1 dag forkert. Planlagte opgaver kan muligvis ikke køre korrekt, før tiden er rettet
Gennemgå din systemtid og sørg for, at den er synkroniseret med en autoritativ tidsserver og er nøjagtig

#### MediaInfo-bibliotek kunne ikke indlæses

MediaInfo-biblioteket kunne ikke indlæses. Sonarr kræver MediaInfo (`libmediainfo`) for at evaluere videoattributterne for filer.

#### Mono Legacy TLS er aktiveret

{#sonarr-mono-4.x-tls-workaround-still-enabled-consider-removing-mono_tls_provider-legacy-environment-option}

Mono 4.x TLS-workaround er stadig aktiveret, overvej at fjerne MONO_TLS_PROVIDER=legacy-miljøindstillingen.

### Downloadklienter

#### Ingen downloadklient er tilgængelig

En korrekt konfigureret og aktiveret downloadklient er påkrævet for, at Sonarr kan downloade medier. Da Sonarr understøtter forskellige downloadklienter, skal du bestemme, hvilken der passer bedst til dine krav. Hvis du allerede har en downloadklient installeret, skal du konfigurere Sonarr til at bruge den og oprette en kategori. Se Indstillinger => Downloadklient.

#### Kan ikke kommunikere med downloadklient

Sonarr kunne ikke kommunikere med den konfigurerede downloadklient. Kontroller, om downloadklienten fungerer, og dobbelttjek URL'en. Dette kan også indikere en godkendelsesfejl.
Dette skyldes normalt en forkert konfigureret downloadklient. Ting, du normalt kan kontrollere:
IP-adressen for dine downloadklienter, hvis de er på samme fysiske maskine, er dette normalt 127.0.0.1
Portnummeret, som din downloadklient bruger, er disse udfyldt med standardportnummeret, men hvis du har ændret det, skal du indtaste det samme i Sonarr.
Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din Sonarr-instans og din downloadklient på et lokalt netværk. Se SSL FAQ-indgangen for mere information.

#### Downloadklienter er utilgængelige på grund af fejl

En eller flere af dine downloadklienter reagerer ikke på anmodninger fra Sonarr. Derfor har Sonarr besluttet midlertidigt at stoppe forespørgslen til downloadklienten på dens normale 1-minuts cyklus, som normalt bruges til at spore aktive downloads og importere færdige downloads. Dog vil Sonarr fortsætte med at forsøge at sende downloads til klienten, men vil med stor sandsynlighed mislykkes.
Du bør inspicere System => Logfiler for at se årsagen til fejlene.
Hvis du ikke længere bruger denne downloadklient, skal du deaktivere den i Sonarr for at forhindre fejl.

#### Aktivér håndtering af fuldførte downloads

- Sonarr kræver håndtering af fuldførte downloads for at kunne importere filer, der er downloadet af downloadklienten. Det anbefales at aktivere håndtering af fuldførte downloads.
(Håndtering af fuldførte downloads er aktiveret som standard...)

#### Docker dårlig fjernsti-mapping

- Denne fejl er normalt forbundet med dårlige docker-stier inden for enten din downloadklient eller Sonarr

- Et eksempel på dette ville være:
  - Downloadklient: Downloadsti: /mnt/user/downloads:/downloads
  - Radarr: Downloadsti: /mnt/user/downloads:/data
- Inden for dette eksempel placerer downloadklienten sine downloads i /downloads og fortæller derfor Radarr, når det er færdigt, at den færdige film er i /downloads. Sonarr kommer derefter og siger "Okay, fint, lad mig tjekke i /downloads" Nå, inde i Radarr har du ikke tildelt en /downloads-sti, du har tildelt en /data-sti, så det kaster denne fejl.
- Den nemmeste løsning på dette er KONSISTENS, hvis du bruger en ordning i din downloadklient, skal du bruge den over hele linjen.

- Team Sonarr er stor fan af simpelthen at bruge /data.
  - Downloadklient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nu kan du inden for downloadklienten angive, hvor i /data du vil placere dine downloads, nu varierer dette afhængigt af klienten, men du bør kunne fortælle den "Ja, downloadklient, placer mine filer i." /data/torrents (eller usenet)/movies og da du brugte /data i Radarr, når downloadklienten fortæller Radarr, at den er færdig, vil Radarr komme og sige "Fedt, jeg har en /data, og jeg kan også se /torrents (eller usenet)/movies alt er i orden i verden."
- Der er mange gode vejledninger: vores wiki [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Disse vejledninger lægger stor vægt på hardlinks og atomiske flytninger, men konceptet med containere og hvordan stibilledning fungerer, er kernen i disse diskussioner.

- Se [TRaSH's fjernsti-guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mere information.

#### Downloader i rodmappen

{#downloads-in-root-folder}

- Inden for applikationen defineres en rodmappe som den konfigurerede mediebibliotekmappe. Dette er ikke rodmappen for et mount. Din downloadklient har en ufuldstændig eller fuldstændig (eller flytter fuldførte downloads) til din rod (bibliotek) mappe.
- Dette forårsager ofte problemer - herunder datatab - og bør ikke gøres. For at løse dette skal du ændre din downloadklient, så den ikke placerer downloads inden for din rodmappe. Bemærk, at 'placering' også inkluderer, hvis din downloadklientkategori er indstillet til din rodmappe, eller hvis NZBGet/SABnzbd har sorteret aktiveret og sorterer til din rodmappe.
- Bemærk, at denne kontrol ser på alle definerede/konfigurerede rodmapper, der er tilføjet, ikke kun rodmapper, der i øjeblikket er i brug. Med andre ord skal mappen, hvor din downloadklient downloader til eller flytter fuldførte downloads til, ikke være den samme mappe, du har konfigureret som din rod/bibliotek/afsluttende mediemålmappe i *arr-applikationen.
- Konfigurerede rodmapper (også kendt som biblioteksmapper) kan findes i [Indstillinger => Mediehåndtering => Rodmapper](/sonarr/settings/#root-folders)
- Et eksempel er, hvis dine downloads går til `/data/downloads`, så har du en rodmappe indstillet som `/data/downloads`.
- Det anbefales at bruge stier som `/data/media/` til din rodmappe/bibliotek og `/data/downloads/` til dine downloads.
- Gennemgå vores [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mere information om den korrekte og optimale stiopsætning. Bemærk, at koncepterne gælder for både docker og ikke-docker

> Din downloadmappe, hvor din downloadklient placerer downloads, og din rod/bibliotekmappe SKAL være adskilte. \*Arr importerer filen(e) fra din downloadklients mappe til dit bibliotek. Downloadklienten skal ikke flytte noget eller downloade noget til dit bibliotek.
{.is-warning}

#### Dårlige indstillinger for downloadklient

- Placeringen, som din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan være tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden fjernsti-mapping.

#### Dårlig fjernsti-mapping

- Placeringen, som din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan være tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden fjernsti-mapping. Se [TRaSH's fjernsti-guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mere information.

#### Tilladelsesfejl

- Sonarr eller brugeren, som Sonarr kører som, kan ikke få adgang til placeringen, som din downloadklient downloader filer til. Dette er normalt et tilladelsesproblem.

#### Fjernfil blev fjernet under behandling

- En fil, der er tilgængelig via en fjernsti-mapping, ser ud til at være blevet fjernet, inden behandlingen blev afsluttet.

#### Fjernsti bruges, og import mislykkedes

- Kontrollér dine logfiler for mere information; Se vores fejlfindingsoversigter for mere information

### Downloading into Root Folder

{#downloads-in-root-folder}

- Inden for applikationen defineres en rodmappe som den konfigurerede mediebibliotekmappe. Dette er ikke rodmappe for et mount. Din downloadklient har en ufuldstændig eller fuldstændig (eller flytter fuldførte downloads) til din rod (biblioteks)mappe.
- Dette forårsager ofte problemer - herunder datatab - og bør ikke gøres. For at rette dette skal du ændre din downloadklient, så den ikke placerer downloads i din rodmappe. Bemærk, at 'placering' også inkluderer, hvis din downloadklients kategori er indstillet til din rodmappe, eller hvis NZBGet/SABnzbd har sortering aktiveret og sorterer til din rodmappe.
- Bemærk, at denne kontrol ser på alle definerede/konfigurerede rodmapper, der er tilføjet, ikke kun rodmapper, der i øjeblikket er i brug. Med andre ord skal mappen, din downloadklient downloader til eller flytter fuldførte downloads til, ikke være den samme mappe, du har konfigureret som din rod/biblioteks/endelige mediedestinationsmappe i *arr-applikationen.
- Konfigurerede rodmapper (også kendt som biblioteksmapper) kan findes i [Indstillinger => Mediehåndtering => Rodmapper](/sonarr/settings/#root-folders)
- Et eksempel er, hvis dine downloads går til `/data/downloads`, så har du en rodmappe indstillet som `/data/downloads`.
- Det anbefales at bruge stier som `/data/media/` til din rodmappe/bibliotek og `/data/downloads/` til dine downloads.
- Gennemgå vores [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mere information om den korrekte og optimale stiopsætning. Bemærk, at koncepterne gælder for både docker og ikke-docker

> Din downloadmappe, hvor din downloadklient placerer downloads, og din rod/bibliotekmappe SKAL være adskilte. \*Arr importerer fil(er) fra din downloadklients mappe til dit bibliotek. Downloadklienten skal ikke flytte noget eller downloade noget til dit bibliotek.
{.is-warning}

#### Behandling af fuldførte downloads er deaktiveret

{#completedfailed-download-handling}

- Det er nødvendigt at bruge behandling af fuldførte downloads, da det giver bedre kompatibilitet for udpaknings- og efterbehandlingslogikken for forskellige downloadklienter. Med det vil Sonarr kun importere en download, når downloadklienten rapporterer, at den er klar.
- Hvis behandling af fuldførte downloads er deaktiveret:
  - Alle import skal håndteres manuelt
  - Denne sundhedskontrol vil fortsætte og kan ikke afvises eller deaktiveres
  - Episoder vil altid mangle i Sonarr og være berettiget til at blive hentet i evighed
    - Episoder, der manuelt er flyttet og omdøbt af brugeren til seriens mappe i Sonarrs biblioteksmappe, vil muligvis blive opdaget af den to gange daglige genindlæsning, hvis de er navngivet korrekt, og vil derfor ikke mangle på det tidspunkt.
  - Brugeren skal manuelt fjerne overvågning eller konfigurere et brugerdefineret script til at fjerne overvågning af episoder.
  - FlexGet er sandsynligvis et bedre værktøj til ens brugssag, hvis man ikke ønsker at bruge Sonarrs funktioner til mediebiblioteksstyring og blot har brug for noget til at analysere RSS-feeds og sende udgivelser til downloadklienten

> \* Behandling af fuldførte downloads fungerer kun korrekt, hvis downloadklienten og Sonarr er på samme maskine, da den får stien, der skal importeres, direkte fra downloadklienten, ellers er der brug for en fjernkortlægning.
> \* Behandling af fuldførte downloads kræver, at Sonarr har læse- og skriveadgang til den fuldførte downloadmappe
{.is-warning}

### Indekseringssteder

#### Ingen indekseringssteder er tilgængelige med aktiveret automatisk søgning, Sonarr vil ikke give nogen automatiske søgeresultater

- Ganske enkelt betyder det, at du ikke har nogen af dine indekseringssteder indstillet til at tillade automatisk søgning
Gå til Indstillinger > Indekseringssteder, vælg et indekseringssted, du gerne vil tillade automatisk søgning, og klik derefter på Gem.

#### Ingen indekseringssteder er tilgængelige med aktiveret RSS-synkronisering, Sonarr vil ikke automatisk hente nye udgivelser

{#no-indexers-available-with-rss-sync-enabled,-sonarr-will-not-grab-new-releases-automatically}
{#all-rss-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Sonarr bruger RSS-feedet til at finde nye udgivelser, når de kommer. [Se FAQ'en for mere information](/sonarr/faq#how-does-sonarr-find-episodes)
- For at rette dette problem skal du gå til Indstillinger > Indekseringssteder, vælge et indekseringssted, du har, og aktivere RSS-synkronisering.

#### Ingen indekseringssteder er aktiveret

- Sonarr kræver indekseringssteder for at kunne opdage nye udgivelser. Alle dine indekseringssteder er deaktiverede, eller du har ikke tilføjet nogen indekseringssteder.

#### Aktiverede indekseringssteder understøtter ikke søgning

{#all-search-capable-indexers-are-temporarily-unavailable-due-to-recent-indexer-errors}

- Ingen af de indekseringssteder, du har aktiveret og tilgængelige, understøtter søgning. Dette betyder, at Sonarr kun vil være i stand til at finde nye udgivelser via RSS-feeds. Men søgning efter serier (enten automatisk søgning eller manuel søgning) vil aldrig give nogen resultater. Den eneste måde at afhjælpe det på er at tilføje et andet indekseringssted.

#### Ingen indekseringssteder er tilgængelige med aktiveret interaktiv søgning

{#no-indexers-available-with-interactive-search-enabled-sonarr-will-not-provide-any-interactive-search-results}

- Ingen af de indekseringssteder, du har aktiveret og tilgængelige, understøtter interaktiv søgning. Dette betyder, at applikationen kun vil være i stand til at finde nye udgivelser via RSS-feeds eller en automatisk søgning.

#### Indekseringssteder er utilgængelige på grund af fejl

- Der opstår fejl, når Sonarr forsøger at bruge en af dine indekseringssteder. For at begrænse genforsøg vil Sonarr ikke bruge indekseringsstedet i en stigende periode (op til 24 timer).
- Denne mekanisme udløses, hvis Sonarr ikke kunne få et svar fra indekseringsstedet (kan skyldes DNS, proxy/vpn-forbindelse, godkendelse eller en indekseringsfejl) eller ikke kunne hente nzb/torrent-filen fra indekseringsstedet. Undersøg venligst logfilerne for at afgøre, hvilken slags fejl der har forårsaget problemet.
- Du kan forhindre denne advarsel ved at deaktivere det berørte indekseringssted.
- Kør en `Test` på indekseringsstedet for at tvinge Sonarr til at kontrollere indekseringsstedet igen; bemærk venligst, at sundhedskontroladvarslen ikke altid forsvinder øjeblikkeligt, og du skal muligvis køre opgaven `Check Health`

#### Jackett All Endpoint Used

- Jackett /all-endepunktet er praktisk, men det er dens eneste fordel. Alt andet er potentielle problemer, så det er nu nødvendigt at tilføje hver enkelt tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af /all-endepunktet har ingen fordele, kun ulemper:
  - du mister kontrollen over indekseringsspecifikke indstillinger (kategorier, søgemetoder osv.)
  - blanding af søgemetoder (IMDB, forespørgsel osv.) kan medføre resultater af lav kvalitet
  - indekseringsspecifikke kategorier (\>= 100.000) kan ikke bruges.
  - langsomme indekseringssteder vil sænke den samlede hastighed
  - det samlede antal resultater er begrænset til 1000
  - hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

##### Løsninger

- Tilføj hver enkelt tracker i Jackett manuelt som et indekseringssted i \*Arr
- Tjek [Prowlarr](/prowlarr), som kan synkronisere indekseringssteder til \*Arr og er udviklet af Lidarr/Radarr/Readarr-udviklingsteamet.
- Tjek [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekseringssteder til \*Arr. Men brug ikke deres enkeltstående samlede endepunkt og brug `multi`, hvis synkroniseringen skal bruges.

### Medier og lister

#### Serier fjernet fra TheTVDB

- Den berørte serie/serier blev fjernet fra [The TVDb](https://thetvdb.com). Dette sker normalt, fordi serien er en duplikat eller betragtes som en del af en anden serie. Alternativt kan TVDb behandle den som en serie; forhåbentlig gør TMDb det også, så [Radarr](/radarr) kan bruges i stedet. For at rette dette skal du fjerne den berørte serie og tilføje den korrekte serie, hvis det er relevant.

#### Lister er utilgængelige på grund af fejl

{#import-lists-are-unavailable-due-to-failures}

- Typisk betyder dette simpelthen, at Sonarr ikke længere kan kommunikere via API eller ved at logge ind på din valgte listeleverandør. Hvis problemet fortsætter, er det bedste, du kan gøre, at kontakte dem for at udelukke dem, da deres systemer måske er overbelastede fra tid til anden.
- Gennemgå System => Begivenheder filtreret efter Advarsel (Advarsler og Fejl) for at se de historiske fejl eller tjek logfilerne for detaljer.

#### Importliste mangler rodmappe

- En eller flere af dine importlister er konfigureret til en rodmappe, der ikke er tilgængelig for Sonarr.
- Dette kan skyldes tilladelsesproblemer, manglende montering eller simpelthen behovet for at opdatere listerne efter at have omorganiseret din opsætning.

#### Manglende rodmappe

- Der er tilføjet en rodmappe til Sonarr, og den eksisterer ikke eller er ikke tilgængelig
- Denne fejl identificeres normalt, hvis en serie leder efter en rodmappe, men den rodmappe er ikke længere tilgængelig.
- Denne fejl kan også være, hvis en liste stadig peger på en rodmappe, men den rodmappe ikke længere er tilgængelig.
- Hvis du vil fjerne denne advarsel, skal du blot finde serien, der stadig bruger den gamle rodmappe, og redigere den til den korrekte rodmappe.

- Den nemmeste måde at finde problemserien på er:

  - Gå til fanen Masseeditor
  - Opret en brugerdefineret filter med den gamle rodmappesti
  - Vælg masseredigering i øverste bjælke, og vælg den nye rodmappesti, som du vil have, at disse serier skal flyttes til, fra rullemenuen Rodstier.
  - Derefter får du en pop op-meddelelse, der siger Vil du flytte seriemapperne til 'rodmappe'? Dette vil også sige Dette vil også omdøbe seriemappen i henhold til seriemappeformatet i indstillingerne. Vælg blot Nej, hvis du ikke vil have, at Lidarr flytter dine filer
  - Kør opgaven Check Health i System => Opgaver

#### Sti til serie er skrivebeskyttet

{#series-mount-ro}

En montering, der indeholder en sti til en serie, er skrivebeskyttet og kan ikke skrives til af den bruger, som Sonarr kører som.

## Diskplads

- Denne sektion viser dig tilgængelig diskplads
- I Docker kan dette være tricky, da det typisk viser den tilgængelige plads inden for dit Docker-billede.

## Om

- Dette vil fortælle dig om din aktuelle installation af Sonarr.

## Mere information

- Hjemmeside: Sonarrs [hjemmeside](https://www.sonarr.tv)
- Wiki: Du er allerede her.
- Reddit: [r/sonarr](https://www.reddit.com/r/sonarr)
- Discord: Deltag i vores [discord](https://discord.sonarr.tv/)
- Donationer: Hvis du har lyst til at donere, kan du klikke [her](https://sonarr.tv/donate).
- Kilde: [GitHub](https://www.github.com/sonarr/sonarr)
- Funktionanmodninger: Har du en god idé, så læg den [her](https://www.github.com/sonarr/sonarr/issues).

# Opgaver

## Planlagte

- Denne sektion viser alle planlagte opgaver, som Sonarr kører

- Applikationskontrolopdatering - Dette vil køre hver på den viste tidsplan i brugergrænsefladen og kontrollere, om Sonarr er på den nyeste version, og derefter udløse opdateringsskriptet for at opdatere Sonarr. Indstillinger => Opdatering

> Bemærk: Hvis du bruger Docker, vil dette ikke opdatere din container, da der skal downloades et nyt billede.
{.is-warning}

- Backup - Dette vil køre en sikkerhedskopi af din Sonarrs database på en fastsat tidsplan. Flere detaljer om dette kan findes her. Yderligere oplysninger om sikkerhedskopier kan findes under System => Sikkerhedskopier.
- Kontroller sundhed - Kontroller sundhed vil køre på den viste tidsplan i brugergrænsefladen og kontrollere den generelle sundhedstilstand for din Sonarr. For at se en liste over mulige sundhedsrelaterede problemer, se Wiki-indgangen om sundhedskontroller.
- Rens papirkurven - Papirkurven tømmes på den viste tidsplan i brugergrænsefladen. Dette vil kun blive brugt, hvis papirkurven er indstillet i Filhåndtering
- Husarbejde - På den viste tidsplan i brugergrænsefladen fjerner dette støv, fejer og støvsuger gulvene, gulvvasker, skinner og laver endda pæne små foldede noter kun til dig. Men det tager ikke skraldet ud. Det blev bare ikke betalt nok for det.
- Importlistesynkronisering - På den viste tidsplan i brugergrænsefladen kører dette dine lister og importerer eventuelle mulige nye serier. Flere oplysninger om lister kan findes under Indstillinger => Lister.
- Rensning af meddelelser - På den viste tidsplan i brugergrænsefladen rydder dette op i de meddelelser, der vises i nederste venstre hjørne af Sonarr
- Opdater overvågede downloads - Dette går igennem og opdaterer downloadkøen, der findes under Aktivitet. Det pinger i bund og grund din downloadklient for at kontrollere, om der er fuldførte downloads.
- Opdater serier - Dette går igennem og opdaterer al metadata for alle overvågede og ikke-overvågede serier
- RSS-synkronisering - Dette vil køre RSS-synkroniseringen. Dette kan ændres under Indstillinger => Indekseringssteder => Indstillinger. Yderligere information om RSS-funktionen kan findes på vores [FAQ](/sonarr/faq)
  
> Alle disse opgaver kan køres manuelt uden for deres planlagte tidspunkter ved at klikke på ikonet helt til højre for hver af opgaverne.
{.is-info}

## Kø

Køen viser kørende og kommende opgaver samt en historik over nyligt kørte opgaver og hvor lang tid disse opgaver tog.

# Sikkerhedskopi

> Hvis du vil vide, hvordan du sikkerhedskopierer/gendanner din Sonarr-instans, skal du klikke [her](/sonarr/faq).
{.is-info}

I sikkerhedskopisektionen får du vist tidligere sikkerhedskopier (medmindre du har en frisk installation, der ikke har foretaget nogen sikkerhedskopier).
  
- Sikkerhedskopier nu - Denne mulighed udløser en manuel sikkerhedskopiering af din Sonarrs database
- Gendan sikkerhedskopi - Dette åbner en ny skærm til at gendanne fra en tidligere sikkerhedskopi
  - Ved at vælge Vælg fil vil dette få din browser til at åbne en dialogboks til at gendanne fra en Sonarr-zipsikkerhedskopi
  
- Hvis du har nogen tidligere sikkerhedskopier og gerne vil downloade dem fra Sonarr for at placere dem et ikke-standard sted, kan du blot vælge en af disse filer for at downloade dem
- Til højre for hver af de tidligere downloads har du to muligheder.

  - Gendan (Ur-ikon) - For at gendanne fra en tidligere sikkerhedskopi - Dette åbner et nyt vindue for at bekræfte, at du vil gendanne fra denne sikkerhedskopi
  - Slet (Skraldespand) - For at slette en tidligere sikkerhedskopi

# Opdateringer

Opdateringsskærmen viser de seneste 5 opdateringer, der er foretaget, samt den aktuelle version, du er på.
Denne side vil også vise opdateringsnoterne fra udviklerne, der fortæller dig, hvad der er blevet rettet eller tilføjet til Sonarr (Fryd dig!)
  
> En vedligeholdelsesudgivelse indeholder fejlrettelser og andre forskellige forbedringer. Se på forpligtelseshistorikken på Github for detaljer.
{.is-info}

# Begivenheder

Begivenhedstaben viser, hvad der er sket i din Sonarr. Dette kan bruges til at diagnosticere mindre problemer. Dette erstatter dog ikke sporingslogfiler, der diskuteres i Logging.

> Begivenheder svarer til INFO-logfiler. {.is-info}

- Komponenter - Denne kolonne fortæller dig, hvilken komponent inden for Sonarr der er blevet udløst
- Besked - Denne kolonne fortæller dig, hvilken besked der er blevet sendt fra komponenten fra den foregående kolonne.
- Tandhjulsikon - Denne mulighed giver dig mulighed for at ændre, hvor mange komponenter/beskeder der vises pr. side (Standard er 50)
- Muligheder øverst på siden
  - Opdater - Denne mulighed vil opdatere den aktuelle side og hente en ny begivenhedslog
  - Ryd - Dette vil rydde den aktuelle begivenhedslog og give dig mulighed for at starte forfra

# Logfiler

- Denne side giver dig mulighed for at downloade og se, hvilke aktuelle logfiler der er tilgængelige for Sonarr.

- På den øverste række er der flere muligheder, der giver dig mulighed for at styre dine logfiler.

- Den øverste række helt til venstre er der en rullemenu, der giver dig mulighed for at skifte mellem logfiler og opdateringslogfiler
  - Logfiler - Brødet og smørret i enhver support-sag, mere om logfiler kan findes her.
  - Opdateringslogfiler - Dette vil vise logfilerne, der er forbundet med Sonarrs opdateringsskript

> Hvis du bruger Docker, vil dette være tomt, da du skal opdatere ved at downloade et nyt Docker-billede
{.is-info}

- Opdater - Dette vil opdatere den aktuelle side og vise eventuelle nyoprettede logfiler
- Slet - Dette vil rydde alle logfiler og give dig mulighed for at starte forfra
- Filnavn - Dette vil vise filnavnet, der er forbundet med loggen
- Sidst skrevet - Dette er den lokale tid, som denne specifikke logfil blev skrevet til.
  - Sonarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid sonarr.txt, for de andre filer er sonarr.0.txt den næstnyeste (jo højere nummeret er, jo ældre er den) op til i alt 51 logfiler. Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.
  - Når fejlfindingslogniveauet er aktiveret, vil der være yderligere sonarr.debug.txt-rullende logfiler, op til 51 filer. Denne logfil indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. Den dækker normalt en periode på ~40 timer.
  - Når sporingslogniveauet er aktiveret, vil der være yderligere sonarr.trace.txt-rullende logfiler, op til 51 filer. Denne logfil indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af sporingsnøjagtighed dækker den kun et par timer maksimalt.