---
title: Radarr System
description: 
published: true
date: 2022-10-19T22:59:06.531Z
tags: radarr, needs-love
editor: markdown
dateCreated: 2021-05-25T02:28:35.194Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Status](#status)
  - [Sundhed](#sundhed)
    - [Systemadvarsler](#systemadvarsler)
      - [Gren er ikke en gyldig udgavegren](#gren-er-ikke-en-gyldig-udgavegren)
      - [Opdater til .NET-version](#opdater-til-net-version)
        - [Fixing Docker-installationer](#fixing-docker-installationer)
        - [Fixing FreeBSD-installationer](#fixing-freebsd-installationer)
        - [Fixing Standalone-installationer](#fixing-standalone-installationer)
      - [Den aktuelt installerede mono-version er gammel og ikke understøttet](#den-aktuelt-installerede-mono-version-er-gammel-og-ikke-understøttet)
      - [Den aktuelt installerede SQLite-version understøttes ikke](#den-aktuelt-installerede-sqlite-version-understøttes-ikke)
      - [Database mislykkedes integritetskontrol](#database-mislykkedes-integritetskontrol)
      - [Ny opdatering er tilgængelig](#ny-opdatering-er-tilgængelig)
      - [Kan ikke installere opdatering, fordi startmappe ikke kan skrives af brugeren](#kan-ikke-installere-opdatering-fordi-startmappe-ikke-kan-skrives-af-brugeren)
      - [Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering](#opdatering-vil-ikke-være-mulig-for-at-forhindre-sletning-af-appdata-ved-opdatering)
      - [Gren er til en tidligere version](#gren-er-til-en-tidligere-version)
      - [Kunne ikke oprette forbindelse til signalR](#kunne-ikke-oprette-forbindelse-til-signalr)
        - [Nginx](#nginx)
        - [Apache2](#apache2)
        - [Caddy](#caddy)
      - [Kunne ikke løse IP-adressen for den konfigurerede proxyvært](#kunne-ikke-løse-ip-adressen-for-den-konfigurerede-proxyvært)
      - [Proxy mislykkedes test](#proxy-mislykkedes-test)
      - [Systemtid er mere end 1 dag forkert](#systemtid-er-mere-end-1-dag-forkert)
      - [PTP Indexer-indstillinger er forældede](#ptp-indexer-indstillinger-er-forældede)
      - [Mono og x86-bygninger ophører](#mono-og-x86-bygninger-ophører)
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
      - [Fjernfil blev fjernet under behandling](#fjernfil-blev-fjernet-under-behandling)
      - [Fjernsti bruges, og import mislykkedes](#fjernsti-bruges-og-import-mislykkedes)
    - [Håndtering af fuldførte/mislukkede downloads](#håndtering-af-fuldførtemislukkede-downloads)
      - [Håndtering af fuldførte downloads er deaktiveret](#håndtering-af-fuldførte-downloads-er-deaktiveret)
    - [Indexere](#indexere)
      - [Ingen indexere er tilgængelige med automatisk søgning aktiveret, Radarr vil ikke give nogen automatisk søgning](#ingen-indexere-er-tilgængelige-med-automatisk-søgning-aktiveret-radarr-vil-ikke-give-nogen-automatisk-søgning)
      - [Ingen indexere er tilgængelige med RSS-synkronisering aktiveret, Radarr vil ikke hente nye udgivelser automatisk](#ingen-indexere-er-tilgængelige-med-rss-synkronisering-aktiveret-radarr-vil-ikke-hente-nye-udgivelser-automatisk)
      - [Ingen indexere er aktiveret](#ingen-indexere-er-aktiveret)
    - [Aktiverede indexere understøtter ikke søgning](#aktiverede-indexere-understøtter-ikke-søgning)
      - [Ingen indexere er tilgængelige med interaktiv søgning aktiveret](#ingen-indexere-er-tilgængelige-med-interaktiv-søgning-aktiveret)
      - [Indexere er utilgængelige på grund af fejl](#indexere-er-utilgængelige-på-grund-af-fejl)
      - [Jackett All Endpoint Used](#jackett-all-endpoint-used)
        - [Løsninger](#løsninger)
    - [Filmmapper](#filmmapper)
      - [Manglende rodmappe](#manglende-rodmappe)
    - [Film](#film)
      - [Film blev fjernet fra TMDb](#film-blev-fjernet-fra-tmdb)
      - [Lister er utilgængelige på grund af fejl](#lister-er-utilgængelige-på-grund-af-fejl)
    - [Underretninger](#underretninger)
    - [Discord som Slack-underretning](#discord-som-slack-underretning)
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

- Denne side indeholder en liste over sundhedstjekfejl. Disse sundhedstjek udføres periodisk af Radarr og ved visse begivenheder. De resulterende advarsler og fejl vises her for at give råd om, hvordan de kan løses.

### Systemadvarsler

#### Gren er ikke en gyldig udgavegren

- Den gren, du har angivet, er ikke en gyldig udgavegren. Du vil ikke modtage opdateringer. Skift til en af de [aktuelle udgavegrene](/radarr/faq#how-do-i-update-radarr).

#### Opdater til .NET-version

{#update-to-net-core-version}

- Nyere versioner af Radarr er målrettet mod .NET6 eller nyere. Mono-bygninger tilbydes ikke og understøttes ikke fra v4. v3.2.2 er den sidste version af Radarr, der understøtter ældre mono-bygninger. Du kører en af disse ældre mono-bygninger, men din platform understøtter .NET.

Se nedenstående indgange for at se, hvordan du skifter fra ikke-understøttede, udfasede mono-versioner til dotnet.

- [Fixing Docker-installationer](#fixing-docker-installationer)
- [Fixing FreeBSD-installationer](#fixing-freebsd-installationer)
- [Fixing Standalone-installationer](#fixing-standalone-installationer)
{.links-list}

##### Fixing Docker-installationer

- Sørg for, at din gren er korrekt for din Docker-vedligeholder, og træk din container igen

##### Fixing FreeBSD-installationer

- Opdater blot Radarr-porten med `pkg update && pkg upgrade`
- (Valgfrit) Fjern mono-pakken, hvis du ønsker det

##### Fixing Standalone-installationer

Fejl som:

```none
Cannot open assembly '/opt/Radarr/Radarr': File does not contain a valid CIL image
```

- Sikkerhedskopier din eksisterende konfiguration, før du går videre til næste trin.
- Dette bør kun ske på Linux-værter. Installer ikke .NET runtime eller SDK fra Microsoft.
- For at rette problemet skal du downloade den korrekte version til din arkitektur og erstatte dine eksisterende binære filer (programmet)
- Kort sagt skal du slette dine eksisterende binære filer (indholdet eller mappen /opt/Radarr) og erstatte dem med indholdet af .tar.gz-filen, du lige har downloadet, og derefter opdatere din tjenestefil, så den ikke bruger mono.

> SLET IKKE BARE UDVIDELSEN OVER DINE EKSISTERENDE BINÆRE FILER.
> DU SKAL FØRST SLETTE DE GAMLE.
{.is-warning}

- Nedenstående er et fællesskabsudviklet script til at fjerne din mono-installation og erstatte den med .NET-installationen. Bidrag og rettelser er velkomne.
- Dette antager, at du er på Radarr-grenen `master`, så opdater variablen, hvis det er nødvendigt
- Dette antager, at Radarr kører som brugeren `radarr`, så opdater variablene, hvis det er nødvendigt
- Dette antager, at Radarr er installeret i `/opt/Radarr`, så opdater variablene, hvis det er nødvendigt

```bash
#!/bin/bash
## Bruger variabler
installdir="/opt/Radarr"
APPUSER="radarr"
branch="master"
## /Bruger variabler
app="radarr"
ARCH=$(dpkg --print-architecture)
# Stop \*arr
sudo systemctl stop $app
# Få arkitektur
dlbase="https://$app.servarr.com/v1/update/$branch/updatefile?os=linux&runtime=netcore"
case "$ARCH" in
"amd64") DLURL="${dlbase}&arch=x64" ;;
"armhf") DLURL="${dlbase}&arch=arm" ;;
"arm64") DLURL="${dlbase}&arch=arm64" ;;
*)
    echo_error "Arkitektur understøttes ikke"
    exit 1
    ;;
esac
echo "Downloader..."
wget --content-disposition "$DLURL"
tar -xvzf ${app^}.*.tar.gz
echo "Installation af filer er downloadet og udpakket"
echo "Flytter eksisterende installation"
sudo mv "$installdir/" "$installdir.old/"
echo "Installerer..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App er installeret"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### Den aktuelt installerede mono-version er gammel og ikke understøttet

- Radarr er skrevet i .NET og kræver Mono for at køre på meget gamle ARM-processorer. Mono 5.20 er det absolutte minimum for Radarr.
- Opgraderingsproceduren for Mono varierer afhængigt af platformen.

> Mono understøttes ikke længere fra Radarr version 4.0
{.is-warning}

#### Den aktuelt installerede SQLite-version understøttes ikke

- Radarr gemmer sine data i en SQLite-database. SQLite3-biblioteket installeret på dit system er for gammelt. Radarr kræver mindst version 3.9.0.

> Bemærk, at Radarr bruger `libSQLite3.so`, som muligvis eller muligvis ikke er indeholdt i en opgraderingspakke til SQLite3.
{.is-info}

#### Database mislykkedes integritetskontrol

- Dine database(r) mislykkedes en [SQLite Pragma Integrity Check](https://www.sqlite.org/pragma.html#pragma_integrity_check) og har nogle korruptioner.
- Hvis `Radarr.db` er beskadiget, [se denne FAQ-indgang](/radarr/faq#i-am-getting-an-error-database-disk-image-is-malformed)
- Hvis `logs.db` er beskadiget: Stop Radarr, slet `logs.db` og eventuelle `logs.wal`-filer.
- Hvis begge er beskadiget, skal du gennemgå de respektive processer ovenfor.

#### Ny opdatering er tilgængelig

- Glæd dig, udviklerne har udgivet en ny opdatering. Dette betyder generelt fantastiske nye funktioner og løste bunkevis af fejl (ikke sandt?). Tilsyneladende har du ikke aktiveret automatisk opdatering, så du bliver nødt til at finde ud af, hvordan du opdaterer på din platform. At trykke på knappen "Installer" på siden System => Opdateringer er sandsynligvis et godt udgangspunkt.

> Denne advarsel vises ikke, hvis din nuværende version er mindre end 14 dage gammel
{.is-info}

#### Kan ikke installere opdatering, fordi startmappe ikke kan skrives af brugeren

- Dette betyder, at Radarr ikke kan opdatere sig selv. Du bliver nødt til at opdatere Radarr manuelt eller angive tilladelserne for Radarrs startmappe (installationsmappen) for at tillade, at Radarr opdaterer sig selv.

#### Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering

- Radarr har registreret, at AppData-mappen til dit operativsystem er placeret inde i mappen, der indeholder Radarr-binærfilerne. Normalt ville det være C:\ProgramData for Windows og ~/.config for Linux.

- Se på System => Info for at se de aktuelle AppData- og Startmappe-mapper.
- Dette betyder, at Radarr ikke vil kunne opdatere sig selv uden at risikere datatab.
- Hvis du bruger Linux, bliver du sandsynligvis nødt til at ændre hjemmemappen for brugeren, der kører Radarr, og kopiere indholdet af mappen ~/.config/Radarr for at bevare din database.

#### Gren er til en tidligere version

- Opdateringsgrenen, der er konfigureret i Indstillinger/Generelt, er til en tidligere version af Radarr, og derfor vil instansen ikke se korrekte opdateringsoplysninger i System/Opdateringer og modtager muligvis ikke nye opdateringer, når de frigives.

#### Kunne ikke oprette forbindelse til signalR

- signalR driver de dynamiske opdateringer af brugergrænsefladen, så hvis din browser ikke kan oprette forbindelse til signalR på din server, vil du ikke se nogen opdateringer i realtid i brugergrænsefladen.
- Den mest almindelige forekomst af dette er brug af en omvendt proxy eller Cloudflare.
- Cloudflare kræver aktivering af websockets.

##### Nginx

- Nginx kræver følgende tilføjelse til placeringen for appen:

```nginx
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Sørg for ikke at inkludere proxy_set_header Connection "Upgrade"; som angivet i nginx-dokumentationen. DETTE VIL IKKE VIRKE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache2

For Apache2 omvendt proxy skal du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Derefter skal du tilføje denne websocket-tunnelanvisning til din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:7878/$1 [P,L]
```

Hvis du har en omvendt proxy under en undermappe, skal RewriteRule inkludere din basepath, f.eks.

```none
RewriteRule /radarr/(.*) ws://127.0.0.1:7878/radarr/$1 [P,L]
```

Hvis Radarr ikke kører på samme maskine som din omvendte proxy. Erstat 127.0.0.1 med den relevante IP-adresse/DNS-navn for din Radarr-app.

##### Caddy

For Caddy (V1) skal du bruge følgende:
Bemærk: Du skal også tilføje websocket-direktivet til din Radarr-konfiguration

```none
 proxy /radarr 127.0.0.1:7878 {
     websocket
     transparent
 }
```

#### Kunne ikke løse IP-adressen for den konfigurerede proxyvært

- Gennemgå dine proxyindstillinger og sørg for, at de er korrekte
- Sørg for, at din proxy er tændt, fungerer og er tilgængelig

#### Proxy mislykkedes test

- Din konfigurerede proxy mislykkedes at teste med succes, gennemgå HTTP-fejlen, der blev angivet, og/eller kontroller logfilerne for flere detaljer.

#### Systemtid er mere end 1 dag forkert

- Systemtiden er mere end 1 dag forkert. Planlagte opgaver kan muligvis ikke køre korrekt, før tiden er rettet.
- Gennemgå din systemtid og sørg for, at den er synkroniseret med en autoritativ tidsserver og er korrekt

#### PTP Indexer-indstillinger er forældede

- Følgende PassThePopcorn-indexere har forældede indstillinger og bør opdateres.

#### Mono og x86-bygninger ophører

- Mono og x86-bygninger understøttes ikke længere med v4. Hvis du modtager denne fejl, kører du enten mono-versionen af programmet eller x86-versionen. Desværre vil vi på grund af den stigende vanskelighed ved udviklingsstøtte til disse ældre versioner ophøre med deres support og dermed også udgivelserne til dem fremover. Derfor anbefales det at opgradere til et understøttet operativsystem, der ikke kræver hverken x86 eller mono. Du kan også undersøge muligheden for at bruge Docker til dine behov.

### Downloadklienter

#### Ingen downloadklient er tilgængelig

- En korrekt konfigureret og aktiveret downloadklient er påkrævet for, at Radarr kan downloade medier. Da Radarr understøtter forskellige downloadklienter, skal du bestemme, hvilken der passer bedst til dine krav. Hvis du allerede har en downloadklient installeret, skal du konfigurere Radarr til at bruge den og oprette en kategori. Se Indstillinger => Downloadklient.

#### Kan ikke kommunikere med downloadklient

- Radarr kunne ikke kommunikere med den konfigurerede downloadklient. Kontroller, om downloadklienten fungerer, og dobbelttjek URL'en. Dette kan også indikere en godkendelsesfejl.
- Dette skyldes normalt en forkert konfigureret downloadklient. Ting, du normalt kan kontrollere:
  - IP-adressen for dine downloadklienter, hvis de er på samme fysiske maskine, er normalt 127.0.0.1
  - Portnummeret for din downloadklient, disse er udfyldt med standardportnummeret, men hvis du har ændret det, skal du indtaste det samme i Radarr.
  - Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din Radarr-instans og din downloadklient på et lokalt netværk. Se SSL-FAQ-indgangen for mere information.
  - Sørg for, at IPv6 er deaktiveret på systemet, hvis det ikke fungerer
  - Sørg for, at en DNS-server (f.eks. pihole) ikke begrænser hastigheden for forespørgsler

#### Downloadklienter er utilgængelige på grund af fejl

- En eller flere af dine downloadklienter reagerer ikke på anmodninger fra Radarr. Derfor har Radarr besluttet midlertidigt at stoppe forespørgsler til downloadklienten på sin normale 1-minuts cyklus, som normalt bruges til at spore aktive downloads og importere færdige downloads. Men Radarr vil fortsætte med at forsøge at sende downloads til klienten, men vil med stor sandsynlighed mislykkes.
- Du bør inspicere System=>Logs for at se årsagen til fejlene.
- Hvis du ikke længere bruger denne downloadklient, skal du deaktivere den i Radarr for at forhindre fejlene.

#### Aktivér håndtering af fuldførte downloads

- Radarr kræver, at håndtering af fuldførte downloads er aktiveret for at kunne importere filer, der er downloadet af downloadklienten. Det anbefales at aktivere håndtering af fuldførte downloads. (Håndtering af fuldførte downloads er aktiveret som standard for nye brugere.)

#### Docker dårlig fjernsti-mapping

- Denne fejl er normalt forbundet med dårlige Docker-stier inden for enten din downloadklient eller Radarr

- Et eksempel på dette ville være:
  - Downloadklient: Downloadsti: /mnt/user/downloads:/downloads
  - Radarr: Downloadsti: /mnt/user/downloads:/data
- I dette eksempel placerer downloadklienten sine downloads i /downloads og fortæller derefter Radarr, når det er færdigt, at den færdige film er i /downloads. Radarr kommer derefter og siger "Okay, fint, lad mig tjekke i /downloads" Nå, inde i Radarr har du ikke allokeret en /downloads-sti, du har allokeret en /data-sti, så det kaster denne fejl.
- Den nemmeste løsning på dette er KONSISTENS, hvis du bruger en ordning i din downloadklient, skal du bruge den over hele linjen.

- Team Radarr er stor fan af blot at bruge /data.
  - Downloadklient: /mnt/user/data/downloads:/data/downloads
  - Radarr: /mnt/user/data:/data

- Nu kan du inden for downloadklienten angive, hvor i /data du vil placere dine downloads, dette varierer afhængigt af klienten, men du bør kunne fortælle den "Ja, downloadklient, placer mine filer i." /data/torrents (eller usenet)/movies og da du brugte /data i Radarr, når downloadklienten fortæller Radarr, at den er færdig, vil Radarr komme og sige "Fint, jeg har en /data, og jeg kan også se /torrents (eller usenet)/movies alt er i orden i verden."
- Der er mange gode vejledninger: vores wiki [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Disse vejledninger lægger stor vægt på hardlinks og atomic moves, men det generelle koncept med containere og hvordan stibesætning fungerer, er kernen i disse diskussioner.

- Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mere information.

#### Downloader til rodmappe

{#downloads-in-root-folder}

- Inden for applikationen defineres en rodmappe som den konfigurerede mediebibliotekmappe. Dette er ikke rodmappen for et mount. Din downloadklient har en ufuldstændig eller fuldført (eller flytter fuldførte downloads) til din rod (biblioteks)mappe.
- Dette forårsager ofte problemer - herunder datatab - og bør ikke gøres. For at rette dette skal du ændre din downloadklient, så den ikke placerer downloads i din rodmappe. Bemærk, at 'placering' også inkluderer, hvis din downloadklientkategori er indstillet til din rodmappe, eller hvis NZBGet/SABnzbd har sortering aktiveret og sorterer til din rodmappe.
- Bemærk, at denne kontrol ser på alle definerede/konfigurerede rodmappe, der er tilføjet, ikke kun rodmappe, der i øjeblikket er i brug. Med andre ord skal mappen, hvor din downloadklient downloader til eller flytter fuldførte downloads til, ikke være den samme mappe, du har konfigureret som din rod/biblioteks/final destination for medier i *arr-applikationen.
- Konfigurerede rodmappe (også kaldet biblioteksmapper) kan findes i [Indstillinger => Mediehåndtering => Rodmapper](/radarr/settings/#root-folders)
- Et eksempel er, hvis dine downloads går til `\data\downloads`, så har du en rodmappe indstillet som `\data\downloads`.
- Det anbefales at bruge stier som `\data\media\` til din rodmappe/bibliotek og `\data\downloads\` til dine downloads.
- Gennemgå vores [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mere information om den korrekte og optimale stiopsætning. Bemærk, at koncepterne gælder for både docker og ikke-docker

> Din downloadmappe, hvor din downloadklient placerer downloads, og din rod/biblioteksmappe SKAL være adskilte. \*Arr importerer filen(e) fra din downloadklients mappe til dit bibliotek. Downloadklienten skal ikke flytte noget eller downloade noget til dit bibliotek.
{.is-warning}

#### Dårlige indstillinger for downloadklient

- Placeringen, hvor din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan være tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden fjernsti-mapping.

#### Dårlig fjernsti-mapping

- Placeringen, hvor din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan være tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden fjernsti-mapping. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mere information.

#### Tilladelsesfejl

- Radarr eller brugeren radarr, der kører, kan ikke få adgang til placeringen, hvor din downloadklient downloader filer til. Dette er normalt et tilladelsesproblem.

#### Fjernfil blev fjernet under behandling

- En fil, der er tilgængelig via en fjernsti-mapping, ser ud til at være blevet fjernet, før behandlingen blev afsluttet.

#### Fjernsti bruges, og import mislykkedes

- Kontrollér dine logfiler for flere oplysninger; Se vores fejlfindingssider

### Håndtering af fuldførte/mislukkede downloads

#### Håndtering af fuldførte downloads er deaktiveret

- (Denne advarsel genereres kun for eksisterende brugere, før funktionen Håndtering af fuldførte downloads blev implementeret. Denne funktion er deaktiveret som standard for at sikre, at systemet fortsatte med at fungere som forventet for nuværende konfigurationer.)
- Det anbefales at bruge Håndtering af fuldførte downloads, da det giver bedre kompatibilitet med udpaknings- og efterbehandlingslogikken for forskellige downloadklienter. Med det vil Radarr kun importere en download, når downloadklienten rapporterer, at den er klar.
- Hvis du ønsker at aktivere Håndtering af fuldførte downloads, skal du verificere følgende: * Advarsel: Håndtering af fuldførte downloads fungerer kun korrekt, hvis downloadklienten og Radarr er på samme maskine, da den får stien, der skal importeres, direkte fra downloadklienten, ellers er der behov for en fjernkort.

### Indexere

#### Ingen indexere er tilgængelige med automatisk søgning aktiveret, Radarr vil ikke give nogen automatisk søgning

- Med andre ord har du ikke nogen af dine indexere indstillet til at tillade automatisk søgning
- Gå til Indstillinger => Indexere, vælg en indexer, du gerne vil tillade automatisk søgning, og klik derefter på Gem.

#### Ingen indexere er tilgængelige med RSS-synkronisering aktiveret, Radarr vil ikke hente nye udgivelser automatisk

- Radarr bruger RSS-feedet til at opfange nye udgivelser, når de kommer. Mere information om det findes her
- For at rette dette problem skal du gå til Indstillinger => Indexere, vælg en indexer, du har, og aktiver RSS-synkronisering

#### Ingen indexere er aktiveret

- Radarr kræver indexere for at kunne opdage nye udgivelser. Læs venligst wiki'en for instruktioner om, hvordan du tilføjer indexere.

#### Aktiverede indexere understøtter ikke søgning

- Ingen af de indexere, du har aktiveret, understøtter søgning. Dette betyder, at Radarr kun vil være i stand til at finde nye udgivelser via RSS-feeds. Men søgning efter film (enten automatisk søgning eller manuel søgning) vil aldrig give nogen resultater. Den eneste måde at afhjælpe det på er selvfølgelig at tilføje en anden indexer.

#### Ingen indexere er tilgængelige med interaktiv søgning aktiveret

- Ingen af de indexere, du har aktiveret, understøtter interaktiv søgning. Dette betyder, at applikationen kun vil være i stand til at finde nye udgivelser via RSS-feeds eller en automatisk søgning.

#### Indexere er utilgængelige på grund af fejl

- Der opstår fejl, når Radarr forsøgte at bruge en af dine indexere. For at begrænse genforsøg vil Radarr ikke bruge indexeren i en stigende periode (op til 24 timer).
- Denne mekanisme udløses, hvis Radarr ikke kunne få et svar fra indexeren (kan skyldes DNS, proxy/vpn-forbindelse, godkendelse eller en indexer-fejl) eller ikke kunne hente nzb/torrent-filen fra indexeren. Undersøg venligst logfilerne for at afgøre, hvilken slags fejl der forårsagede problemet.
- Du kan forhindre advarslen ved at deaktivere den berørte indexer.
- Kør testen på indexeren for at tvinge Radarr til at kontrollere indexeren igen, bemærk venligst, at sundhedstjekadvarslen ikke altid forsvinder med det samme.

#### Jackett All Endpoint Used

- Jackett /all-endepunktet er praktisk, men det er dens eneste fordel. Alt andet er potentielle problemer, så det er nu påkrævet at tilføje hver tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af /all-endepunktet har ingen fordele, kun ulemper:
  - du mister kontrollen over indexer-specifikke indstillinger (kategorier, søgemetoder osv.)
  - blanding af søgemetoder (IMDB, forespørgsel osv.) kan forårsage resultater af lav kvalitet
  - indexer-specifikke kategorier (\>= 100000) kan ikke bruges.
  - langsomme indexere vil bremse det samlede resultat
  - det samlede antal resultater er begrænset til 1000
  - hvis en af trackerne i /all returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

##### Løsninger

- Tilføj hver tracker i Jackett manuelt som en indexer i \*Arr
- Tjek [Prowlarr](/prowlarr), der kan synkronisere indexere til \*Arr og fra Lidarr/Radarr/Readarr-udviklingsteamet.
- Tjek [NZBHydra2](https://github.com/theotherp/nzbhydra2), der kan synkronisere indexere til \*Arr. Men brug ikke deres enkeltstående samlede endepunkt og brug `multi`, hvis synkroniseringen skal bruges.

### Filmmapper

#### Manglende rodmappe

{#movie-collection-missing-root-folder}

- Denne fejl identificeres normalt, hvis en film eller samling er tildelt en rodmappe, men den rodmappe er ikke længere tilgængelig.
- Denne fejl kan også forekomme, hvis en liste stadig peger på en rodmappe, og den rodmappe ikke længere er tilgængelig.
- Hvis du vil fjerne denne advarsel, skal du blot finde filmen(e) eller samlingen(e), der stadig bruger den gamle rodmappe, og redigere den til den korrekte rodmappe.

##### Filmoversigtstabel

1. Gå til fanen Film (Bibliotek)
1. Tabelvisning og aktiver kolonnen Sti og sorter efter sti

##### Brugerdefineret filter for film

1. Opret et brugerdefineret filter med den gamle rodmappesti
1. Vælg massevisning i øverste bjælke og vælg den nye rodmappe, du vil have, at disse film skal flyttes til, fra rullelisten Rodstier.
1. Derefter modtager du en pop op, der siger "Vil du flytte filmmapperne til 'rodmappe'?" Dette vil også sige, at dette også vil omdøbe filmmappen i henhold til filmmappens format i indstillinger. Vælg blot Nej, hvis du ikke vil have, at Radarr flytter dine filer.
1. Kør sundhedstjekopgaven i System => Opgaver

#### Brugerdefineret filter for samlinger

1. Opret et brugerdefineret filter i Samlinger med den gamle rodmappesti
1. Vælg samlingerne og vælg den nye rodmappe, du vil have, at fremtidige film i disse samlinger skal tildeles.
1. Kør sundhedstjekopgaven i System => Opgaver

### Film

#### Film blev fjernet fra TMDb

- Filmen er knyttet til en TMDb-id, der blev slettet fra TMDb, normalt fordi det var en duplikat, ikke var en film eller ændrede ID af en anden grund. Slettede film modtager ikke nogen opdateringer og bør rettes af brugeren for at sikre fortsat funktionalitet. Fjern filmen fra Radarr uden at slette filerne og prøv derefter at tilføje den igen. Hvis den ikke vises i en søgning, skal du kontrollere Sonarr, fordi det måske er en tv-miniserie som Stephen Kings It.

- Du kan finde og redigere slettede film ved at oprette et brugerdefineret filter ved hjælp af følgende trin:

  1. Klik på Film i venstre menu
  1. Klik på rullemenuen for Filter og vælg "Brugerdefineret filter"
  1. Indtast en etiket, f.eks. "Slettede film"
  1. Opret filteret som følger: `Udgivelsesstatus` er `Slettet`
  1. Klik på Gem og vælg det nyoprettede filter fra rullemenuen for filter

#### Lister er utilgængelige på grund af fejl

- Normalt betyder dette blot, at Radarr ikke længere kan kommunikere via API eller ved at logge ind på din valgte listeleverandør. Dit bedste bud, hvis problemet fortsætter, er at kontakte dem for at udelukke dem, da deres systemer mul

## Kø

- Køen viser dig kørende og kommende opgaver samt en historik over nyligt udførte opgaver og hvor lang tid disse opgaver tog.

# Backup

> Hvis du leder efter hvordan du tager en sikkerhedskopi/gendanner din Radarr-instans, klik [her](/radarr/faq).
{.is-info}

- Inden for Backup-sektionen vil du blive præsenteret for tidligere sikkerhedskopier (medmindre du har en frisk installation, der ikke har lavet nogen sikkerhedskopier).
  
- Backup nu - Denne mulighed udløser en manuel sikkerhedskopi af din Radarr-database.
- Gendan sikkerhedskopi - Dette åbner en ny skærm for at gendanne fra en tidligere sikkerhedskopi.
  - Ved at vælge Vælg fil vil din browser bede dig om at åbne en dialogboks for at gendanne fra en Radarr-zip-sikkerhedskopi.
  
- Hvis du har tidligere sikkerhedskopier og gerne vil downloade dem fra Radarr for at placere dem et andet sted end standard, kan du blot vælge en af disse filer for at downloade dem.
- Til højre for hver af de tidligere downloads har du to muligheder.
  - Gendan (Ur-ikon) - For at gendanne fra en tidligere sikkerhedskopi - Dette åbner et nyt vindue for at bekræfte, at du vil gendanne fra denne sikkerhedskopi.
  - Slet (Skraldespand) - For at slette en tidligere sikkerhedskopi.

# Opdateringer

- Opdateringsskærmen viser de seneste 5 opdateringer, der er foretaget, samt den aktuelle version, du er på.
- Denne side viser også opdateringsnoter fra udviklerne, der fortæller dig, hvad der er blevet rettet eller tilføjet til Radarr (Glæd dig!).
  
> En vedligeholdelsesudgivelse indeholder fejlrettelser og andre forskellige forbedringer. Se på commit-historikken for detaljer.
{.is-info}

# Begivenheder

- Begivenhedstabet viser, hvad der er sket i din Radarr. Dette kan bruges til at diagnosticere mindre problemer. Dette erstatter dog ikke sporingslogfiler, som diskuteres i Logging.

> Begivenheder svarer til INFO-logfiler. {.is-info}

- Komponenter - Denne kolonne fortæller dig, hvilken komponent inden for Radarr der er blevet udløst.
- Besked - Denne kolonne fortæller dig, hvilken besked der er blevet sendt fra komponenten i den foregående kolonne.
- Tandhjulsikon - Denne mulighed giver dig mulighed for at ændre, hvor mange komponenter/beskeder der vises pr. side (standard er 50).
- Muligheder øverst på siden
  - Opdater - Denne mulighed opdaterer den aktuelle side og henter en ny begivenhedslog.
  - Ryd - Dette vil rydde den aktuelle begivenhedslog og give dig mulighed for at starte forfra.

# Logfiler

- Denne side giver dig mulighed for at downloade og se, hvilke aktuelle logfiler der er tilgængelige for Radarr.

- På øverste række er der flere muligheder, der giver dig mulighed for at styre dine logfiler.

- Øverst til venstre på den øverste række er der en rullemenu, der giver dig mulighed for at skifte mellem logfiler og opdateringslogfiler.
  - Logfiler - Hovedkomponenten i enhver support-sag, mere om logfiler kan findes her.
  - Opdateringslogfiler - Dette viser logfilerne, der er forbundet med Radarrs opdateringsskript.

> Hvis du bruger Docker, vil dette være tomt, da du bør opdatere ved at downloade et nyt Docker-billede.
{.is-info}

- Opdater - Dette vil opdatere den aktuelle side og vise eventuelt nyoprettede logfiler.
- Slet - Dette vil rydde alle logfiler og give dig mulighed for at starte forfra.
- Filnavn - Dette viser filnavnet, der er forbundet med loggen.
- Sidst skrevet - Dette er den lokale tid, hvor denne specifikke logfil blev skrevet.
  - Radarr bruger rullende logfiler, der er begrænset til 1 MB hver. Den aktuelle logfil er altid radarr.txt, for de andre filer er radarr.0.txt den næstnyeste (jo højere nummeret er, jo ældre er den) op til i alt 51 logfiler. Denne logfil indeholder `fatal`, `error`, `warn` og `info`-poster.
  - Når Debug-logniveauet er aktiveret, vil der være yderligere rullende logfiler radarr.debug.txt, op til 51 filer. Disse logfiler indeholder `fatal`, `error`, `warn`, `info` og `debug`-poster. Det dækker normalt en periode på ca. 40 timer.
  - Når Trace-logniveauet er aktiveret, vil der være yderligere rullende logfiler radarr.trace.txt, op til 51 filer. Disse logfiler indeholder `fatal`, `error`, `warn`, `info`, `debug` og `trace`-poster. På grund af sporingsnøjagtighed dækker det kun et par timer.