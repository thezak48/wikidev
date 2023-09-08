---
title: Prowlarr System
description: 
published: true
date: 2023-05-31T11:54:59.064Z
tags: prowlarr, system
editor: markdown
dateCreated: 2021-08-03T21:21:08.969Z
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
      - [Kunne ikke løse IP-adressen for den konfigurerede proxyvært](#kunne-ikke-løse-ip-adressen-for-den-konfigurerede-proxyvært)
      - [Proxy mislykkedes test](#proxy-mislykkedes-test)
      - [Systemtiden er mere end 1 dag forkert](#systemtiden-er-mere-end-1-dag-forkert)
    - [Downloadklienter](#downloadklienter)
      - [Ingen downloadklient er tilgængelig](#ingen-downloadklient-er-tilgængelig)
      - [Kan ikke kommunikere med downloadklient](#kan-ikke-kommunikere-med-downloadklient)
      - [Downloadklienter er utilgængelige på grund af fejl](#downloadklienter-er-utilgængelige-på-grund-af-fejl)
      - [Dårlige indstillinger for downloadklient](#dårlige-indstillinger-for-downloadklient)
    - [Indekser](#indekser)
      - [Indekser har ingen definition](#indekser-har-ingen-definition)
      - [Indekser er forældede](#indekser-er-forældede)
        - [Forældet på grund af kodeændringer](#forældet-på-grund-af-kodeændringer)
        - [Forældet på grund af webstedsfjernelse](#forældet-på-grund-af-webstedsfjernelse)
      - [Ingen indekser er aktiveret](#ingen-indekser-er-aktiveret)
      - [Indekser er utilgængelige på grund af fejl](#indekser-er-utilgængelige-på-grund-af-fejl)
      - [Indekser VIP udløber](#indekser-vip-udløber)
      - [Indekser VIP udløbet](#indekser-vip-udløbet)
    - [Applikationer](#applikationer)
      - [Applikationer er utilgængelige på grund af fejl](#applikationer-er-utilgængelige-på-grund-af-fejl)
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

Denne side indeholder en liste over sundhedstjekfejl. Disse sundhedstjek udføres periodisk af Prowlarr og ved visse begivenheder. De resulterende advarsler og fejl vises her for at give råd om, hvordan de kan løses.

### Systemadvarsler

#### Gren er ikke en gyldig udgivelsesgren

- Den gren, du har angivet, er ikke en gyldig udgivelsesgren. Du vil ikke modtage opdateringer. Skift til en af de [aktuelle udgivelsesgrene](/prowlarr/faq#how-do-i-update-prowlarr).

#### Den aktuelt installerede SQLite-version understøttes ikke

- Prowlarr gemmer sine data i en SQLite-database. Den SQLite3-bibliotek, der er installeret på dit system, er for gammel. Prowlarr kræver mindst version 3.9.0. Bemærk, at Prowlarr bruger `libSQLite3.so`, som muligvis er indeholdt i en SQLite3-opgraderingspakke.

#### Ny opdatering er tilgængelig

- Fryd dig, udviklerne har udgivet en ny opdatering. Dette betyder generelt fantastiske nye funktioner og løste fejl (ikke sandt?). Tilsyneladende har du ikke aktiveret automatisk opdatering, så du bliver nødt til at finde ud af, hvordan du opdaterer på din platform. At trykke på knappen "Installer" på siden System => Opdateringer er sandsynligvis et godt udgangspunkt.

> Denne advarsel vises ikke, hvis din nuværende version er mindre end 14 dage gammel
{.is-info}

#### Kan ikke installere opdatering, fordi startmappe ikke kan skrives af brugeren

- Dette betyder, at Prowlarr ikke kan opdatere sig selv. Du bliver nødt til at opdatere Prowlarr manuelt eller indstille tilladelserne for Prowlarrs startmappe (installationsmappen) for at tillade Prowlarr at opdatere sig selv.

#### Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering

- Prowlarr har registreret, at AppData-mappen til dit operativsystem er placeret inde i mappen, der indeholder Prowlarr-binærerne. Normalt ville det være C:\ProgramData for Windows og ~/.config for Linux.

- Se på System => Info for at se de aktuelle AppData- og startmapper.
- Dette betyder, at Prowlarr ikke vil kunne opdatere sig selv uden at risikere datatab.
- Hvis du bruger Linux, skal du sandsynligvis ændre hjemmemappen for den bruger, der kører Prowlarr, og kopiere indholdet af mappen ~/.config/Prowlarr til at bevare din database.

#### Gren er til en tidligere version

- Opdateringsgrenen, der er konfigureret i Indstillinger/Generelt, er til en tidligere version af Prowlarr, og derfor vil instansen ikke se korrekte opdateringsoplysninger i System/Opdateringer og modtager muligvis ikke nye opdateringer, når de frigives.

#### Kunne ikke oprette forbindelse til signalR

- signalR driver de dynamiske brugergrænsefladeopdateringer, så hvis din browser ikke kan oprette forbindelse til signalR på din server, vil du ikke se nogen opdateringer i realtid i brugergrænsefladen.

- Den mest almindelige forekomst af dette er brug af en omvendt proxy eller Cloudflare
  - Cloudflare kræver aktivering af websockets.
  - Nginx kræver følgende tilføjelse til placeringen af appen:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Sørg for ikke at inkludere proxy_set_header Connection "Upgrade"; som foreslået af nginx-dokumentationen. DETTE VIL IKKE VIRKE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

- For Apache2 omvendt proxy skal du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Derefter tilføjer du denne websocket-tunnelanvisning til din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:9696/$1 [P,L]
```

Hvis du har en omvendt proxy under en undermappe, skal RewriteRule inkludere din basepath, f.eks.

```none
RewriteRule /prowlarr/(.*) ws://127.0.0.1:9696/prowlarr/$1 [P,L]
```

Hvis Prowlarr ikke kører på samme maskine som din omvendte proxy, skal du erstatte 127.0.0.1 med den korrekte IP-adresse/DNS-navn for din Prowlarr-app.

- For Caddy (V1) skal du bruge dette:

> Bemærk: Du skal også tilføje websocket-direktivet til din prowlarr-konfiguration{.is-info}

```none
 proxy /prowlarr 127.0.0.1:9696 {
     websocket
     transparent
 }
```

#### Kunne ikke løse IP-adressen for den konfigurerede proxyvært

- Gennemgå dine proxyindstillinger og sørg for, at de er korrekte.
- Sørg for, at din proxy er tændt, fungerer og er tilgængelig.

#### Proxy mislykkedes test

- Din konfigurerede proxy mislykkedes testen, kontroller den HTTP-fejl, der blev angivet, og/eller kontroller logfilerne for flere detaljer.

#### Systemtiden er mere end 1 dag forkert

- Systemtiden er mere end 1 dag forkert. Planlagte opgaver kan muligvis ikke køre korrekt, før tiden er rettet.
- Gennemgå din systemtid og sørg for, at den er synkroniseret med en autoritativ tidsserver og er korrekt.

### Downloadklienter

#### Ingen downloadklient er tilgængelig

- En korrekt konfigureret og aktiveret downloadklient er påkrævet for, at Prowlarr kan downloade medier. Da Prowlarr understøtter forskellige downloadklienter, bør du bestemme, hvilken der bedst opfylder dine krav. Hvis du allerede har en downloadklient installeret, skal du konfigurere Prowlarr til at bruge den og oprette en kategori. Se Indstillinger => Downloadklient.

#### Kan ikke kommunikere med downloadklient

- Prowlarr kunne ikke kommunikere med den konfigurerede downloadklient. Verificer, om downloadklienten er funktionsdygtig, og dobbelttjek URL'en. Dette kan også indikere en godkendelsesfejl.
- Dette skyldes normalt en forkert konfigureret downloadklient. Ting, du normalt kan kontrollere:
- IP-adressen for dine downloadklienter, hvis de kører på samme fysiske maskine, er normalt 127.0.0.1
- Portnummeret, som din downloadklient bruger, disse er udfyldt med standardportnummeret, men hvis du har ændret det, skal du indtaste det samme i Prowlarr.
- Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din Prowlarr-instans og din downloadklient på et lokalt netværk. Se SSL-FAQ'en for mere information.
- Brug af rutorrent kræver specielle indstillingsændringer, da det kræver https.

#### Downloadklienter er utilgængelige på grund af fejl

- En eller flere af dine downloadklienter reagerer ikke på anmodninger fra Prowlarr. Derfor har Prowlarr besluttet midlertidigt at stoppe forespørgsler til downloadklienten på dens normale 1-minuts cyklus, som normalt bruges til at spore aktive downloads og importere færdige downloads. Prowlarr vil dog fortsætte med at forsøge at sende downloads til klienten, men vil sandsynligvis mislykkes.
- Du bør inspicere System=>Logfiler for at se årsagen til fejlene.
- Hvis du ikke længere bruger denne downloadklient, skal du deaktivere den i Prowlarr for at forhindre fejl.

#### Dårlige indstillinger for downloadklient

- Stedet, hvor din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan skyldes tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden en fjernsti.

### Indekser

#### Indekser har ingen definition

- Dine indekser har ingen eksisterende definition (fil), dette skyldes normalt, at din indekser ikke længere understøttes og er blevet fjernet, eller at Cardigann YML-definitionen ikke længere er tilgængelig.

#### Indekser er forældede

- Din indeksers definition er forældet og forældet. Dette har to årsager, som er angivet nedenfor

##### Forældet på grund af kodeændringer

- På grund af kodeændringer er indekserne forældede som konfigureret i øjeblikket. Fjern og tilføj indekserne til Prowlarr for at løse problemet.
- Dette skyldes normalt konvertering af API'er eller fra YML til C# eller omvendt.

##### Forældet på grund af webstedsfjernelse

- Visse websteder kan anmodes om at blive fjernet fra Prowlarr eller Jackett. Disse kan derefter markeres som forældede.
  - [TVVault](https://github.com/Prowlarr/Prowlarr/issues/573) i [Prowlarr #700](https://github.com/Prowlarr/Prowlarr/pull/700)
  - Audiobookbay har anmodet om, at Prowlarr ikke får adgang til deres API
  - Ebookbay har anmodet om, at Prowlarr ikke får adgang til deres API
  - Rarbg har [lukket ned fra og med 2023-05-31](https://torrentfreak.com/iconic-torrent-site-rarbg-shuts-down-all-content-releases-stop-230531/)

#### Ingen indekser er aktiveret

- Prowlarr kræver indekser for at kunne opdage nye udgivelser. Læs venligst instruktionerne i wikien om, hvordan du tilføjer indekser.

#### Indekser er utilgængelige på grund af fejl

- Der opstår fejl, når Prowlarr forsøger at bruge en af dine indekser. For at begrænse forsøgene vil Prowlarr ikke bruge indekseren i en stigende periode (op til 24 timer).
- Kontrollér hændelser og filtrer efter advarsler for at få en hurtig idé om, hvilke problemer der er opstået historisk set.
- Denne mekanisme udløses, hvis Prowlarr ikke kunne få et svar fra indekseren (kan skyldes DNS, proxy/vpn-forbindelse, godkendelse eller en indeksfejl) eller ikke kunne hente nzb-/torrentfilen fra indekseren. Inspect logs for at bestemme, hvilken slags fejl der forårsager problemet.
- Du kan forhindre advarslen ved at deaktivere den berørte indekser.
- Kør testen på indekseren for at tvinge Prowlarr til at kontrollere indekseren igen, bemærk venligst, at sundhedstjekadvarslen ikke altid forsvinder med det samme.

#### Indekser VIP udløber

- Dit VIP-abonnement eller fordele til din indekser udløber inden for de næste 7 dage eller mindre baseret på udløbsdatoen, du har konfigureret for din indekser i Prowlarr.

#### Indekser VIP udløbet

- Dit VIP-abonnement eller fordele til din indekser er udløbet baseret på udløbsdatoen, du har konfigureret for indekseren i Prowlarr.

### Applikationer

#### Applikationer er utilgængelige på grund af fejl

- Der opstår fejl, når Prowlarr forsøger at bruge en af dine applikationer. For at begrænse forsøgene vil Prowlarr ikke bruge applikationen i en stigende periode (op til 24 timer).
- Denne mekanisme udløses, hvis Prowlarr ikke kunne få et svar fra applikationen (kan skyldes DNS, forbindelse, godkendelse eller applikationsfejl). Inspect logs for at bestemme, hvilken slags fejl der forårsager problemet.
- Kontrollér hændelser og filtrer efter advarsler for at få en hurtig idé om, hvilke problemer der er opstået historisk set.
- Prowlarr vil ikke kunne synkronisere med applikationen, og det er mere end sandsynligt, at applikationen ikke vil kunne bruge Prowlarrs indekser.
- Du kan forhindre advarslen ved at deaktivere den berørte applikation.
- Kør testen på applikationen for at tvinge Prowlarr til at kontrollere applikationen igen, bemærk venligst, at sundhedstjekadvarslen ikke altid forsvinder med det samme.

## Diskplads

Denne sektion viser dig tilgængelig diskplads.
I Docker kan dette være tricky, da det typisk vil vise dig den tilgængelige plads inden for dit Docker-billede.

## Om

Dette vil fortælle dig om din aktuelle installation af Prowlarr.

## Mere info

Hjemmeside: Prowlarrs hjemmeside
Wiki: Du er allerede her
Reddit: r/prowlarr
Discord: Deltag i vores discord
Donationer: Hvis du har lyst til at donere, skal du klikke her
Donationer til Sonarr: Hvis du har lyst til at donere til projektet, der startede det hele, skal du klikke her
Kilde: GitHub
Funktionsanmodninger: Har du en god idé, så del den her

# Opgaver

## Planlagt

Denne side viser alle planlagte opgaver, som Prowlarr kører

- Application Check Update - Dette vil køre på den viste tidsplan i brugergrænsefladen og kontrollere, om Prowlarr er på den nyeste version, og derefter udløse opdateringsskriptet for at opdatere Prowlarr. Indstillinger => Opdatering

> Bemærk: Hvis du bruger Docker, opdaterer dette ikke din container, da der skal downloades et nyt billede.
{.is-warning}

- Backup - Dette vil køre en sikkerhedskopi af din Prowlarr-database på en fastsat tidsplan. Flere detaljer om dette kan findes her. Yderligere oplysninger om sikkerhedskopier kan findes under System => Sikkerhedskopier.
- Check Health - Check Health vil køre på den viste tidsplan i brugergrænsefladen og kontrollere den generelle sundhedstilstand for din Prowlarr. Se en liste over mulige sundhedsrelaterede problemer i Wiki-indgangen om sundhedstjek.
- Housekeeping - På den viste tidsplan i brugergrænsefladen fjerner denne opgave støv, fejer og støvsuger gulvene, vasker, skinner og laver endda pæne, foldede noter kun til dig. Men det tager ikke skraldet ud. Det blev bare ikke betalt nok for det.
- Messaging Cleanup - På den viste tidsplan i brugergrænsefladen rydder dette op i de beskeder, der vises i nederste venstre hjørne af Prowlarr.

> Alle disse opgaver kan køres manuelt uden for deres planlagte tidspunkter ved at klikke på ikonet helt til højre for hver af opgaverne.
{.is-info}

## Kø

Køen viser kommende opgaver samt en historik over nyligt kørte opgaver samt hvor lang tid disse opgaver tog.

# Backup

> Denne sektion vil være mere tilpasset knapperne og den overordnede pointe på siden.
> Hvis du leder efter hjælp til at sikkerhedskopiere/gendanne din Prowlarr-instans, [se vores FAQ](/prowlarr/faq).
{.is-info}

Inden for sikkerhedskopieringssektionen vil du blive præsenteret for tidligere sikkerhedskopier (medmindre du har en frisk installation, der ikke har foretaget nogen sikkerhedskopier).

Her har du to muligheder øverst på skærmen:

- Sikkerhedskopier nu - Denne mulighed udløser en manuel sikkerhedskopiering af din Prowlarr-database.
- Gendan sikkerhedskopi - Dette åbner en ny skærm for at gendanne fra en tidligere sikkerhedskopi. Ved at vælge Vælg fil vil din browser bede dig om at åbne en dialogboks for at gendanne fra en Prowlarr-zip-sikkerhedskopi.

Hvis du har tidligere sikkerhedskopier og gerne vil downloade dem fra Prowlarr for at placere dem et andet sted end standard, kan du blot vælge en af disse filer for at downloade dem. Til højre for hver af de tidligere downloads har du to muligheder.

- Én - For at gendanne fra en tidligere sikkerhedskopi - Dette åbner et nyt vindue for at bekræfte, at du vil gendanne fra denne sikkerhedskopi.
- To - For at slette en tidligere sikkerhedskopi

# Opdateringer

Opdateringsskærmen viser de seneste 5 opdateringer, der er foretaget, samt den aktuelle version, du bruger.
Denne side viser også opdateringsnoterne fra udviklerne, der fortæller dig, hvad der er blevet rettet eller tilføjet til Prowlarr (Glæd dig!)

> En vedligeholdelsesudgivelse indeholder fejlrettelser og forskellige forbedringer. Se commit-historikken for detaljer.
{.is-info}

# Hændelser

Fanen Hændelser viser, hvad der er sket i din Prowlarr. Dette kan bruges til at diagnosticere mindre problemer. Bemærk dog, at dette ikke erstatter sporingslogfiler, som diskuteres i Logging. Hændelser svarer til INFO-logfiler.

- Komponenter - Denne kolonne fortæller dig, hvilken komponent inden for Prowlarr der er blevet udløst.
- Besked - Denne kolonne fortæller dig, hvilken besked der er blevet sendt fra komponenten i den foregående kolonne.
- Gear-ikon - Denne mulighed giver dig mulighed for at ændre, hvor mange komponenter/beskeder der vises pr. side (standard er 50).
- Muligheder øverst på siden
  - Opdater - Denne mulighed opdaterer den aktuelle side og henter en ny hændelseslog.
  - Ryd - Dette vil rydde den aktuelle hændelseslog og give dig en frisk start.

# Logfiler

Denne side giver dig mulighed for at downloade og se, hvilke aktuelle logfiler der er tilgængelige for Prowlarr.

På øverste række er der flere muligheder, der giver dig kontrol over dine logfiler.

- Øverst til venstre er der en dropdown-menu, der giver dig mulighed for at skifte mellem logfiler og opdateringslogfiler.
  - Logfiler - Hovedkomponenten i enhver support-sag. Du kan finde mere om logfiler her.
  - Opdateringslogfiler - Dette viser logfilerne, der er forbundet med Prowlarrs opdateringsskript.

> Hvis du bruger Docker, vil dette være tomt, da du bør opdatere ved at downloade et nyt Docker-billede.
{.is-info}

- Opdater - Dette opdaterer den aktuelle side og viser eventuelle nyoprettede logfiler.
- Slet - Dette vil rydde alle logfiler og give dig en frisk start.
- Filnavn - Dette viser filnavnet, der er forbundet med loggen.
- Sidst skrevet - Dette er den lokale tid, hvor denne specifikke logfil blev skrevet.
  - Prowlarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid prowlarr.txt, og for de andre filer er prowlarr.0.txt den næstnyeste (jo højere nummer, jo ældre er den) op til i alt 51 logfiler. Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.
  - Når fejlfinding-logniveauet er aktiveret, vil der være yderligere prowlarr.debug.txt-rullende logfiler, op til 51 filer. Disse logfiler indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. De dækker normalt en periode på ca. 40 timer.
  - Når sporingslogniveauet er aktiveret, vil der være yderligere prowlarr.trace.txt-rullende logfiler, op til 51 filer. Disse logfiler indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af sporingslogfilernes omfang dækker de kun et par timer ad gangen.