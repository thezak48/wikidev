---
title: Readarr System
description: 
published: true
date: 2022-05-05T12:52:16.242Z
tags: readarr, needs-love, system
editor: markdown
dateCreated: 2021-06-20T19:54:43.262Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Status](#status)
  - [Sundhed](#sundhed)
    - [Systemadvarsler](#systemadvarsler)
      - [Gren er ikke en gyldig udgivelsesgren](#gren-er-ikke-en-gyldig-udgivelsesgren)
      - [Den aktuelt installerede SQLite-version understøttes ikke](#den-aktuelt-installerede-sqlite-version-understøttes-ikke)
      - [Ny opdatering er tilgængelig](#ny-opdatering-er-tilgængelig)
      - [Kan ikke installere opdatering, fordi startmappe ikke kan skrives af brugeren](#kan-ikke-installere-opdatering-fordi-startmappe-ikke-kan-skrives-af-brugeren)
      - [Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering](#opdatering-vil-ikke-være-mulig-for-at-forhindre-sletning-af-appdata-ved-opdatering)
      - [Gren er til en tidligere version](#gren-er-til-en-tidligere-version)
      - [Kunne ikke oprette forbindelse til signalR](#kunne-ikke-oprette-forbindelse-til-signalr)
        - [Nginx](#nginx)
      - [Kunne ikke løse IP-adressen for den konfigurerede proxyvært](#kunne-ikke-løse-ip-adressen-for-den-konfigurerede-proxyvært)
      - [Proxy mislykkedes test](#proxy-mislykkedes-test)
      - [Systemtid er mere end 1 dag forkert](#systemtid-er-mere-end-1-dag-forkert)
    - [Downloadklienter](#downloadklienter)
      - [Ingen downloadklient er tilgængelig](#ingen-downloadklient-er-tilgængelig)
      - [Kan ikke kommunikere med downloadklient](#kan-ikke-kommunikere-med-downloadklient)
      - [Downloadklienter er utilgængelige på grund af fejl](#downloadklienter-er-utilgængelige-på-grund-af-fejl)
      - [Aktivér håndtering af fuldførte downloads](#aktiver-håndtering-af-fuldførte-downloads)
      - [Docker dårlig fjernsti-mapping](#docker-dårlig-fjernsti-mapping)
      - [Downloader til rodmappe](#downloader-til-rodmappe)
      - [Dårlige indstillinger for downloadklient](#dårlige-indstillinger-for-downloadklient)
      - [Dårlig fjernsti-mapping](#dårlig-fjernsti-mapping)
      - [Tilladelsesfejl](#tilladelsesfejl)
      - [Forfattermount er skrivebeskyttet](#forfattermount-er-skrivebeskyttet)
      - [Fjernfil blev fjernet under behandling](#fjernfil-blev-fjernet-under-behandling)
      - [Fjernsti bruges, og import mislykkedes](#fjernsti-bruges-og-import-mislykkedes)
    - [Håndtering af fuldførte/mislukkede downloads](#håndtering-af-fuldførtemislukkede-downloads)
      - [Håndtering af fuldførte downloads er deaktiveret](#håndtering-af-fuldførte-downloads-er-deaktiveret)
    - [Indekser](#indekser)
      - [Ingen indekser er tilgængelige med automatisk søgning aktiveret, Readarr vil ikke give nogen automatisk søgning](#ingen-indekser-er-tilgængelige-med-automatisk-søgning-aktiveret-readarr-vil-ikke-give-nogen-automatisk-søgning)
      - [Ingen indekser er tilgængelige med RSS-synkronisering aktiveret, Readarr vil ikke hente nye udgivelser automatisk](#ingen-indekser-er-tilgængelige-med-rss-synkronisering-aktiveret-readarr-vil-ikke-hente-nye-udgivelser-automatisk)
      - [Ingen indekser er aktiveret](#ingen-indekser-er-aktiveret)
    - [Aktiverede indekser understøtter ikke søgning](#aktiverede-indekser-understøtter-ikke-søgning)
      - [Ingen indekser er tilgængelige med interaktiv søgning aktiveret](#ingen-indekser-er-tilgængelige-med-interaktiv-søgning-aktiveret)
      - [Indekser er utilgængelige på grund af fejl](#indekser-er-utilgængelige-på-grund-af-fejl)
      - [Jackett bruger alle slutpunkter](#jackett-bruger-alle-slutpunkter)
        - [Løsninger](#løsninger)
    - [Bogmapper](#bogmapper)
      - [Manglende rodmappe](#manglende-rodmappe)
    - [Importlister](#importlister)
      - [Importlister er utilgængelige på grund af fejl](#importlister-er-utilgængelige-på-grund-af-fejl)
  - [Diskplads](#diskplads)
  - [Om](#om)
  - [Mere info](#mere-info)
- [Opgaver](#opgaver)
  - [Planlagt](#planlagt)
  - [Kø](#kø)
- [Backup](#backup)
- [Opdateringer](#opdateringer)
- [Hændelser](#hændelser)
- [Logfiler](#logfiler)

# Status

## Sundhed

- Denne side indeholder en liste over fejl ved sundhedstjek. Disse sundhedstjek udføres periodisk af Readarr og ved visse begivenheder. De resulterende advarsler og fejl vises her for at give råd om, hvordan de kan løses.

### Systemadvarsler

#### Gren er ikke en gyldig udgivelsesgren

- Den gren, du har angivet, er ikke en gyldig udgivelsesgren. Du vil ikke modtage opdateringer. Skift til en af de [aktuelle udgivelsesgrene](/readarr/faq#how-do-i-update-readarr).

#### Den aktuelt installerede SQLite-version understøttes ikke

- Readarr gemmer sine data i en SQLite-database. SQLite3-biblioteket, der er installeret på dit system, er for gammelt. Readarr kræver mindst version 3.9.0. Bemærk, at Readarr bruger `libSQLite3.so`, som muligvis er indeholdt i en opgraderingspakke til SQLite3.

> Bemærk, at Readarr bruger `libSQLite3.so`, som muligvis er indeholdt i en opgraderingspakke til SQLite3.
{.is-info}

#### Ny opdatering er tilgængelig

Glæd dig, udviklerne har udgivet en ny opdatering. Dette betyder generelt fantastiske nye funktioner og løste fejl (ikke sandt?). Tilsyneladende har du ikke aktiveret automatisk opdatering, så du bliver nødt til at finde ud af, hvordan du opdaterer på din platform. Det er sandsynligvis en god start at trykke på knappen "Installer" på siden System => Opdateringer.

> Denne advarsel vises ikke, hvis din nuværende version er mindre end 14 dage gammel.
{.is-info}

#### Kan ikke installere opdatering, fordi startmappe ikke kan skrives af brugeren

- Dette betyder, at Readarr ikke kan opdatere sig selv. Du bliver nødt til at opdatere Readarr manuelt eller ændre tilladelserne for Readarrs startmappe (installationsmappen) for at tillade Readarr at opdatere sig selv.

#### Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering

- Readarr har registreret, at AppData-mappen til dit operativsystem er placeret inde i mappen, der indeholder Readarr-binærerne. Normalt ville det være C:\ProgramData for Windows og ~/.config for Linux.

- Se på System => Info for at se de aktuelle AppData- og startmapper.
- Dette betyder, at Readarr ikke kan opdatere sig selv uden at risikere datatab.
- Hvis du bruger Linux, skal du sandsynligvis ændre hjemmemappen for brugeren, der kører Readarr, og kopiere indholdet af mappen ~/.config/Readarr for at bevare din database.

#### Gren er til en tidligere version

- Opdateringsgrenen, der er konfigureret i Indstillinger/Generelt, er til en tidligere version af Readarr, og derfor vil instansen ikke se korrekte opdateringsoplysninger i System/Opdateringer-feedet og modtage nye opdateringer, når de frigives.

#### Kunne ikke oprette forbindelse til signalR

- signalR driver de dynamiske UI-opdateringer, så hvis din browser ikke kan oprette forbindelse til signalR på din server, vil du ikke se nogen opdateringer i realtid i brugergrænsefladen.

- Den mest almindelige forekomst af dette er brug af en omvendt proxy eller Cloudflare.
- Cloudflare kræver aktivering af websockets.

##### Nginx

- Nginx kræver følgende tilføjelse til placeringen for appen:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Sørg for ikke at inkludere proxy_set_header Connection "Upgrade"; som foreslået af nginx-dokumentationen. DETTE VIL IKKE VIRKE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

For Apache2 omvendt proxy skal du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Derefter tilføjer du denne websocket-tunnelanvisning til din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8787/$1 [P,L]
```

For Caddy (V1) skal du bruge dette:
Bemærk: Du skal også tilføje websocket-anvisningen til din Readarr-konfiguration

```none
 proxy /readarr 127.0.0.1:8787 {
     websocket
     transparent
 }
```

#### Kunne ikke løse IP-adressen for den konfigurerede proxyvært

- Gennemgå dine proxyindstillinger og sørg for, at de er korrekte.
- Sørg for, at din proxy er tændt, fungerer og er tilgængelig.

#### Proxy mislykkedes test

- Din konfigurerede proxy mislykkedes at teste med succes. Gennemgå den angivne HTTP-fejl og/eller kontroller logfilerne for flere detaljer.

#### Systemtid er mere end 1 dag forkert

- Systemtiden er mere end 1 dag forkert. Planlagte opgaver kan muligvis ikke køre korrekt, før tiden er rettet.
- Gennemgå din systemtid og sørg for, at den er synkroniseret med en autoritativ tidsserver og er korrekt.

### Downloadklienter

#### Ingen downloadklient er tilgængelig

- En korrekt konfigureret og aktiveret downloadklient er påkrævet for, at Readarr kan downloade medier. Da Readarr understøtter forskellige downloadklienter, bør du bestemme, hvilken der passer bedst til dine krav. Hvis du allerede har en downloadklient installeret, skal du konfigurere Readarr til at bruge den og oprette en kategori. Se Indstillinger => Downloadklient.

#### Kan ikke kommunikere med downloadklient

- Readarr kunne ikke kommunikere med den konfigurerede downloadklient. Kontroller, om downloadklienten er i drift, og dobbelttjek URL'en. Dette kan også indikere en godkendelsesfejl.
- Dette skyldes normalt en forkert konfigureret downloadklient. Ting, du normalt kan kontrollere:
- IP-adressen for dine downloadklienter, hvis de er på samme fysiske maskine, er normalt 127.0.0.1
- Portnummeret, som din downloadklient bruger, er udfyldt med standardportnummeret, men hvis du har ændret det, skal du indtaste det samme i Readarr.
- Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din Readarr-instans og din downloadklient på et lokalt netværk. Se SSL-FAQ'en for mere information.

#### Downloadklienter er utilgængelige på grund af fejl

{#downloadklienter-er-utilgængelige-på-grund-af-fejl}

- En eller flere af dine downloadklienter svarer ikke på anmodninger fra Readarr. Derfor har Readarr besluttet midlertidigt at stoppe forespørgsler til downloadklienten på den normale 1-minuts cyklus, som normalt bruges til at spore aktive downloads og importere færdige downloads. Dog vil Readarr fortsætte med at forsøge at sende downloads til klienten, men vil med stor sandsynlighed mislykkes.
- Du bør inspicere System=>Logfiler for at se årsagen til fejlene.
- Hvis du ikke længere bruger denne downloadklient, skal du deaktivere den i Readarr for at forhindre fejl.

#### Aktiver håndtering af fuldførte downloads

- Readarr kræver, at håndtering af fuldførte downloads er aktiveret for at kunne importere filer, der er downloadet af downloadklienten. Det anbefales at aktivere håndtering af fuldførte downloads.
- (Håndtering af fuldførte downloads er aktiveret som standard for nye brugere.)

#### Docker dårlig fjernsti-mapping

- Denne fejl er normalt forbundet med dårlige Docker-stier i enten din downloadklient eller Readarr.

- Et eksempel på dette ville være:
  - Downloadklient: Downloadsti: /mnt/user/downloads:/downloads
  - Readarr: Downloadsti: /mnt/user/downloads:/data
- I dette eksempel placerer downloadklienten sine downloads i /downloads og fortæller derfor Readarr, når det er færdigt, at den færdige bog er i /downloads. Readarr kommer derefter og siger "Okay, fint, lad mig tjekke i /downloads" Nå, inde i Readarr har du ikke tildelt en /downloads-sti, du har tildelt en /data-sti, så det kaster denne fejl.
- Den nemmeste løsning på dette er KONSISTENS, hvis du bruger en ordning i din downloadklient, skal du bruge den på tværs af hele systemet.

- Team Readarr er stor fan af simpelthen at bruge /data.
  - Downloadklient: /mnt/user/data/downloads:/data/downloads
  - Readarr: /mnt/user/data:/data

- Nu kan du inden for downloadklienten angive, hvor i /data du vil placere dine downloads, nu varierer dette afhængigt af klienten, men du bør kunne fortælle den "Ja, downloadklient, placer mine filer i." /data/torrents (eller usenet)/books og da du brugte /data i Readarr, når downloadklienten fortæller Readarr, at den er færdig, vil Readarr komme og sige "Fedt, jeg har en /data, og jeg kan også se /torrents (eller usenet)/books alt er i orden i verden."
- Der er mange gode vejledninger: vores wiki [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Disse vejledninger lægger stor vægt på hardlinks og atomiske flytninger, men det generelle koncept med containere og hvordan sti-mapping fungerer, er kernen i disse diskussioner.

- Hvis du krydser operativsystemer eller nativ og Docker, har du brug for en fjernsti-mapping. Se [TRaSH's fjernsti-vejledning til Radarr, men konceptet er det samme for alle \*Arrs](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mere information.

- Hvis du får denne fejl med Calibre, kan Redarr ikke få adgang til Calibres bibliotek. Løsningen er den samme - ret de inkonsekvente monteringer for dine containere. Alternativt kan du oprette en fjernsti-mapping for at kortlægge stien til Calibre-biblioteket til den Readarr-tilgængelige sti. En fjernsti-mapping er kun nødvendig, hvis du krydser operativsystemer eller servere. Hvis alt er i Docker, er det bedst at rette dine monteringer i stedet.

#### Downloader til rodmappe

{#downloads-in-root-folder}

- Inden for applikationen defineres en rodmappe som den konfigurerede mediebibliotekmappe. Dette er ikke rodmappen for et mount. Din downloadklient downloader ufuldstændige eller fuldstændige downloads (eller flytter fuldførte downloads) til din rod (biblioteks)mappe.
- Dette forårsager ofte problemer - herunder datatab - og bør ikke gøres. For at løse dette skal du ændre din downloadklient, så den ikke placerer downloads inden for din rodmappe. Bemærk, at 'placering' også inkluderer, hvis din downloadklientkategori er indstillet til din rodmappe, eller hvis NZBGet/SABnzbd har sortering aktiveret og sorterer til din rodmappe.
- Bemærk, at denne kontrol ser på alle definerede/konfigurerede rodmapper, der er tilføjet, ikke kun rodmapper, der i øjeblikket er i brug. Med andre ord skal mappen, hvor din downloadklient downloader til eller flytter fuldførte downloads til, ikke være den samme mappe, du har konfigureret som din rod/biblioteks/final mediedestinationsmappe i *arr-applikationen.
- Konfigurerede rodmapper (også kaldet biblioteksmapper) kan findes i [Indstillinger => Mediehåndtering => Rodmapper](/readarr/settings/#root-folders)
- Et eksempel er, hvis dine downloads går til `\data\downloads`, så har du en rodmappe, der er indstillet som `\data\downloads`.
- Det anbefales at bruge stier som `\data\media\` til din rodmappe/bibliotek og `\data\downloads\` til dine downloads.
- Gennemgå vores [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mere information om den korrekte og optimale stiopsætning. Bemærk, at koncepterne gælder for både Docker og ikke-Docker.

> Din downloadmappe, hvor din downloadklient placerer downloads, og din rod/biblioteksmappe SKAL være adskilte. \*Arr importerer filen(e) fra din downloadklients mappe til dit bibliotek. Downloadklienten skal ikke flytte noget eller downloade noget til dit bibliotek.
{.is-warning}

#### Dårlige indstillinger for downloadklient

- Den placering, din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan være tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden en fjernsti-mapping.

#### Dårlig fjernsti-mapping

- Placeringen, som din downloadklient downloader filer til, forårsager problemer. Tjek logfilerne for yderligere information. Dette kan skyldes tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden en fjernstimapning af sti. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Readarr/Readarr-remote-path-mapping/) for mere information.

#### Tilladelsesfejl

- Readarr eller brugeren, som Readarr kører som, kan ikke få adgang til placeringen, som din downloadklient downloader filer til. Dette er typisk et tilladelsesproblem.

#### Forfattermount er skrivebeskyttet

{#author-mount-ro}

- Mount, der indeholder en sti til en forfatter, er monteret som skrivebeskyttet. Tjek dine mountindstillinger og ejerskab/tilladelser.

#### Fjernfil blev fjernet under behandling

- En fil, der er tilgængelig via en fjernstimapning af sti, ser ud til at være blevet fjernet, inden behandlingen blev afsluttet.

#### Fjernsti bruges, og import mislykkedes

- Tjek dine logfiler for mere information; Henvis til vores fejlfinding.

### Håndtering af fuldførte/mislukkede downloads

#### Håndtering af fuldførte downloads er deaktiveret

- (Denne advarsel genereres kun for eksisterende brugere, før funktionen Håndtering af fuldførte downloads blev implementeret. Denne funktion er som standard deaktiveret for at sikre, at systemet fortsatte med at fungere som forventet for nuværende konfigurationer.)
- Det anbefales at bruge Håndtering af fuldførte downloads, da det giver bedre kompatibilitet med udpaknings- og efterbehandlingslogikken for forskellige downloadklienter. Med det vil Readarr kun importere en download, når downloadklienten rapporterer, at den er klar.
- Hvis du ønsker at aktivere Håndtering af fuldførte downloads, skal du verificere følgende: * Advarsel: Håndtering af fuldførte downloads fungerer kun korrekt, hvis downloadklienten og Readarr er på samme maskine, da den får stien, der skal importeres, direkte fra downloadklienten, ellers er en fjernmapning nødvendig.

### Indekser

#### Ingen indekser er tilgængelige med aktiveret automatisk søgning, Readarr vil ikke give nogen automatisk søgeresultater

- Enkelt sagt har du ikke nogen af dine indekser indstillet til at tillade automatisk søgning
- Gå til Indstillinger => Indekser, vælg en indekser, du gerne vil tillade automatisk søgning, og klik derefter på Gem.

#### Ingen indekser er tilgængelige med aktiveret RSS-synkronisering, Readarr vil ikke hente nye udgivelser automatisk

- Så Readarr bruger RSS-feedet til at opfange nye udgivelser, når de kommer. Mere information om dette kan findes her
- For at rette dette problem skal du gå til Indstillinger => Indekser, vælge en indekser, du har, og aktivere RSS-synkronisering

#### Ingen indekser er aktiveret

- Readarr kræver indekser for at kunne opdage nye udgivelser. Læs venligst wiki'en for instruktioner om, hvordan du tilføjer indekser.

### Aktiverede indekser understøtter ikke søgning

- Ingen af de indekser, du har aktiveret, understøtter søgning. Dette betyder, at Readarr kun vil kunne finde nye udgivelser via RSS-feeds. Men søgning efter bøger (enten automatisk søgning eller manuel søgning) vil aldrig give nogen resultater. Den eneste måde at rette det på er at tilføje en anden indekser.

#### Ingen indekser er tilgængelige med aktiveret interaktiv søgning

- Ingen af de indekser, du har aktiveret, understøtter interaktiv søgning. Dette betyder, at applikationen kun vil kunne finde nye udgivelser via RSS-feeds eller en automatisk søgning.

#### Indekser er utilgængelige på grund af fejl

- Der opstår fejl, når Readarr forsøger at bruge en af dine indekser. For at begrænse forsøgene vil Readarr ikke bruge indekseren i en stigende periode (op til 24 timer).
- Denne mekanisme udløses, hvis Readarr ikke kunne få et svar fra indekseren (kan skyldes DNS, proxy/vpn-forbindelse, godkendelse eller en indekserfejl) eller ikke kunne hente nzb/torrent-filen fra indekseren. Tjek logfilerne for at finde ud af, hvilken slags fejl der forårsager problemet.
- Du kan forhindre advarslen ved at deaktivere den berørte indekser.
- Kør testen på indekseren for at tvinge Readarr til at kontrollere indekseren igen. Bemærk, at advarslen om sundhedstjekket ikke altid forsvinder med det samme.

#### Jackett All Endpoint Used

- Jackett /all-endepunktet er praktisk, men det er også dets eneste fordel. Alt andet kan være potentielle problemer, så det er nu påkrævet at tilføje hver enkelt tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brugen af /all-endepunktet har ingen fordele, kun ulemper:
  - Du mister kontrollen over indekser-specifikke indstillinger (kategorier, søgemetoder osv.)
  - Blanding af søgemetoder (IMDB, forespørgsel osv.) kan medføre resultater af lav kvalitet
  - Indekser-specifikke kategorier (\>= 100.000) kan ikke bruges.
  - Langsomme indekser vil sænke den samlede ydeevne
  - Det samlede antal resultater er begrænset til 1000
  - Hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

##### Løsninger

- Tilføj hver enkelt tracker i Jackett manuelt som en indekser i \*Arr
- Tjek [Prowlarr](/prowlarr), som kan synkronisere indekser til \*Arr, og det er udviklet af Lidarr/Radarr/Readarr-udviklingsteamet.
- Tjek [NZBHydra2](https://github.com/theotherp/nzbhydra2), som kan synkronisere indekser til \*Arr. Men brug ikke deres enkeltstående aggregat-endepunkt og brug `multi`, hvis synkronisering skal bruges.

### Bogmapper

#### Manglende rodmappe

- Denne fejl identificeres typisk, hvis en forfatter leder efter en rodmappe, men den rodmappe er ikke længere tilgængelig.
- Denne fejl kan også opstå, hvis en liste stadig peger på en rodmappe, men den rodmappe ikke længere er tilgængelig.
- Hvis du vil fjerne denne advarsel, skal du blot finde albummet, der stadig bruger den gamle rodmappe, og redigere det til den korrekte rodmappe.

- Den nemmeste måde at finde problemforfatteren på er:

  - Gå til fanen Forfatter (Bibliotek)
  - Opret en brugerdefineret filter med den gamle rodmappesti
  - Vælg massevis redigering i toppen af siden, og vælg den nye rodmappesti, som du vil flytte disse forfattere til, fra rullemenuen Rodstier.
  - Derefter får du en pop op-besked, der siger Vil du flytte forfattermapperne til 'rodmappe'? Dette vil også sige Dette vil også omdøbe forfattermappen i henhold til forfattermappenformatet i indstillingerne. Vælg blot Nej, hvis du ikke vil have, at Lidarr flytter dine filer.
  - Kør sundhedstjekopgaven i System => Opgaver

### Importlister

#### Importlister er utilgængelige på grund af fejl

- Dette betyder typisk, at Readarr ikke længere kan kommunikere via API eller ved at logge ind på din valgte listeleverandør. Hvis problemet fortsætter, er det bedste, du kan gøre, at kontakte dem for at udelukke dem, da deres systemer kan være overbelastede fra tid til anden.

## Diskplads

- Denne sektion viser dig tilgængelig diskplads
- I Docker kan dette være lidt tricky, da det typisk viser den tilgængelige plads inden for dit Docker-billede

## Om

- Dette vil fortælle dig om din aktuelle installation af Readarr

## Mere information

- Hjemmeside: Readarr's hjemmeside
- Wiki: Du er allerede her
- Reddit: r/readarr
- Discord: Deltag i vores Discord
- Donationer: Hvis du har lyst til at donere, kan du klikke her
- Donationer til Sonarr: Hvis du har lyst til at donere til projektet, der startede det hele, kan du klikke her
- Kilde: GitHub
- Funktionanmodninger: Har du en god idé, så læg den her

# Opgaver

## Planlagte

- Denne sektion viser alle planlagte opgaver, som Readarr kører

- Application Check Update - Dette vil køre på den viste tidsplan i brugergrænsefladen og kontrollere, om Readarr er på den nyeste version, og derefter udløse opdateringsskriptet for at opdatere Readarr. Indstillinger => Opdatering

> Bemærk: Hvis du bruger Docker, vil dette ikke opdatere din container, da der skal downloades et nyt billede.
{.is-warning}

- Backup - Dette vil køre en sikkerhedskopi af din Readarr's database på en fastsat tidsplan. Flere detaljer om dette kan findes her. Yderligere oplysninger om sikkerhedskopier kan findes under System => Sikkerhedskopier.
- Check Health - Check Health vil køre på den viste tidsplan i brugergrænsefladen og kontrollere den generelle sundhedstilstand for din Readarr. For at se en liste over mulige sundhedsrelaterede problemer, se Wiki-indgangen om sundhedstjek.
- Housekeeping - På den viste tidsplan i brugergrænsefladen vil dette støve af, feje og støvsuge gulvene, moppe, skinne og endda lave pæne, foldede noter kun til dig. Men det tager ikke skraldet ud. Det blev bare ikke betalt nok for det.
- Import List Sync - På den viste tidsplan i brugergrænsefladen vil dette køre dine lister og importere eventuelle nye bøger. Flere oplysninger om lister kan findes under Indstillinger => Lister.
- Messaging Cleanup - På den viste tidsplan i brugergrænsefladen rydder dette op i de meddelelser, der vises i nederste venstre hjørne af Readarr
- Refresh Author - Dette opdaterer alle forfattere i dit bibliotek.
- Refresh Monitored Downloads - Dette opdaterer downloadkøen, der findes under Aktivitet. Det pinger i bund og grund din downloadklient for at tjekke, om der er færdige downloads.
- Rescan folders - Dette scanner alle bogmapper for at se, om en bog eksisterer eller ej, og opdaterer status for den derefter.
- RSS Sync - Dette vil køre RSS-synkroniseringen. Dette kan ændres under indstillinger => muligheder. Yderligere information om RSS-funktionen kan findes i vores FAQ
  
> Alle disse opgaver kan køres manuelt uden for deres planlagte tidspunkter ved at klikke på ikonet helt til højre for hver af opgaverne.
{.is-info}

## Kø

Køen viser kørende og kommende opgaver samt en historik over nyligt kørte opgaver og hvor lang tid disse opgaver tog.

# Sikkerhedskopi

> Hvis du vil vide, hvordan du sikkerhedskopierer/gendanner din Readarr-instans, skal du klikke [her](/readarr/faq).
{.is-info}

- Inden for sikkerhedskopisektionen vil du blive præsenteret for tidligere sikkerhedskopier (medmindre du har en frisk installation, der ikke har foretaget nogen sikkerhedskopier).
  
- Backup nu - Denne mulighed udløser en manuel sikkerhedskopiering af din Readarr's database
- Gendan sikkerhedskopi - Dette åbner en ny skærm til at gendanne fra en tidligere sikkerhedskopi
  - Ved at vælge Vælg fil vil din browser åbne en dialogboks, der giver dig mulighed for at gendanne fra en Readarr-zipsikkerhedskopi
  
- Hvis du har tidligere sikkerhedskopier og gerne vil downloade dem fra Readarr for at placere dem et ikke-standard sted, kan du blot vælge en af disse filer for at downloade dem
- Til højre for hver af de tidligere downloads har du to muligheder.
  - Gendan (Ur-ikon) - For at gendanne fra en tidligere sikkerhedskopi - Dette åbner et nyt vindue for at bekræfte, at du vil gendanne fra denne sikkerhedskopi
  - Slet (Skraldespand) - For at slette en tidligere sikkerhedskopi

# Opdateringer

- Opdateringsskærmen viser de seneste 5 opdateringer, der er foretaget, samt den aktuelle version, du er på.
- Denne side viser også opdateringsnoterne fra udviklerne, der fortæller dig, hvad der er blevet rettet eller tilføjet til Readarr (Fryd dig!)
  
> En vedligeholdelsesudgivelse indeholder fejlrettelser og andre forskellige forbedringer. Se på commit-historikken for detaljer.
{.is-info}

# Hændelser

- Hændelsestaben viser, hvad der er sket i din Readarr. Dette kan bruges til at diagnosticere mindre problemer. Dette erstatter dog ikke sporingslogfiler, som diskuteres i Logging.

> Hændelser svarer til INFO-logfiler. {.is-info}

- Komponenter - Denne kolonne fortæller dig, hvilken komponent inden for Readarr der er blevet udløst
- Besked - Denne kolonne fortæller dig, hvilken besked der er blevet sendt fra komponenten fra den foregående kolonne.
- Tandhjulsikon - Denne mulighed giver dig mulighed for at ændre, hvor mange komponenter/beskeder der vises pr. side (Standard er 50)
- Muligheder øverst på siden
  - Opdater - Denne mulighed vil opdatere den aktuelle side og hente en ny hændelseslog
  - Ryd - Dette vil rydde den aktuelle hændelseslog og give dig mulighed for at starte forfra

# Logfiler

- Denne side giver dig mulighed for at downloade og se, hvilke aktuelle logfiler der er tilgængelige for Readarr

- På den øverste række er der flere muligheder, der giver dig mulighed for at styre dine logfiler.

- Den øverste række helt til venstre er der en rullemenu, der giver dig mulighed for at skifte mellem logfiler og opdateringslogfiler
  - Logfiler - Hovedingrediensen i enhver supportanmodning. Du kan finde mere om logfiler her.
  - Opdateringslogfiler - Dette vil vise logfilerne, der er forbundet med Readarr's opdateringsskript

> Hvis du bruger Docker, vil dette være tomt, da du skal opdatere ved at downloade et nyt Docker-billede
{.is-info}

- Opdater - Dette vil opdatere den aktuelle side og vise eventuelle nyoprettede logfiler
- Slet - Dette vil rydde alle logfiler og give dig mulighed for at starte forfra
- Filnavn - Dette vil vise filnavnet, der er forbundet med loggen
- Sidst skrevet - Dette er den lokale tid, som denne specifikke logfil blev skrevet til.
  - Readarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid readarr.txt, og for de andre filer er readarr.0.txt den næstnyeste (jo højere nummer, jo ældre er den) op til i alt 51 logfiler. Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.
  - Når fejlfinding af logniveau er aktiveret, vil der være yderligere readarr.debug.txt-rullende logfiler, op til 51 filer. Disse logfiler indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. De dækker normalt en periode på ca. 40 timer.
  - Når sporingslogniveau er aktiveret, vil der være yderligere readarr.trace.txt-rullende logfiler, op til 51 filer. Disse logfiler indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af sporingsnøjagtigheden dækker de kun et par timer ad gangen.