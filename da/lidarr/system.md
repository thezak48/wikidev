Jeg er ved at oversætte dokumentationen for at hjælpe brugerne. Oversæt Markdown-indholdet, jeg vil indsætte senere, til dansk. Du skal følge reglerne nedenfor strengt. - Ændr aldrig Markdown-markupstrukturen. Tilføj eller fjern ikke links. Ændr ikke nogen URL. - Ændr aldrig indholdet af kodeblokke, selvom de ser ud til at have en fejl. - Bevar altid de originale linjeskift. Tilføj eller fjern ikke blanke linjer. - Rør aldrig ved permalinks som f.eks. `{/*eksempler*/}` i slutningen af hver overskrift. - Rør aldrig ved HTML-lignende tags som f.eks. `<Notes>`.

---
title: Lidarr System
description: 
published: true
date: 2022-10-31T04:35:13.645Z
tags: lidarr, needs-love, system
editor: markdown
dateCreated: 2021-06-14T21:36:28.225Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Status](#status)
  - [Sundhed](#sundhed)
    - [Systemadvarsler](#systemadvarsler)
      - [Gren er ikke en gyldig udgivelsesgren](#gren-er-ikke-en-gyldig-udgivelsesgren)
      - [Opdater til .NET-version](#opdater-til-net-version)
        - [Fixing Docker-installationer](#fixing-docker-installationer)
        - [Fixing Standalone-installationer](#fixing-standalone-installationer)
      - [Den aktuelt installerede mono-version er gammel og ikke understøttet](#den-aktuelt-installerede-mono-version-er-gammel-og-ikke-understøttet)
      - [Den aktuelt installerede SQLite-version understøttes ikke](#den-aktuelt-installerede-sqlite-version-understøttes-ikke)
      - [Ny opdatering er tilgængelig](#ny-opdatering-er-tilgængelig)
      - [Kan ikke installere opdatering, fordi startmappe ikke kan skrives af brugeren](#kan-ikke-installere-opdatering-fordi-startmappe-ikke-kan-skrives-af-brugeren)
      - [Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering](#opdatering-vil-ikke-være-mulig-for-at-forhindre-sletning-af-appdata-ved-opdatering)
      - [Gren er til en tidligere version](#gren-er-til-en-tidligere-version)
      - [Kunne ikke oprette forbindelse til signalR](#kunne-ikke-oprette-forbindelse-til-signalr)
        - [NGINX](#nginx)
        - [Apache](#apache)
        - [Caddy](#caddy)
      - [Kunne ikke løse IP-adressen for den konfigurerede proxyvært](#kunne-ikke-løse-ip-adressen-for-den-konfigurerede-proxyvært)
      - [Proxy mislykkedes test](#proxy-mislykkedes-test)
      - [Systemtiden er mere end 1 dag forkert](#systemtiden-er-mere-end-1-dag-forkert)
      - [Mono Legacy TLS aktiveret](#mono-legacy-tls-aktiveret)
      - [Mono og x86-builds ophører](#mono-og-x86-builds-ophører)
      - [FPcalc skal opdateres](#fpcalc-skal-opdateres)
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
      - [Ingen indexere er tilgængelige med automatisk søgning aktiveret, Lidarr vil ikke give nogen automatisk søgning](#ingen-indexere-er-tilgængelige-med-automatisk-søgning-aktiveret-lidarr-vil-ikke-give-nogen-automatisk-søgning)
      - [Ingen indexere er tilgængelige med RSS-synkronisering aktiveret, Lidarr vil ikke hente nye udgivelser automatisk](#ingen-indexere-er-tilgængelige-med-rss-synkronisering-aktiveret-lidarr-vil-ikke-hente-nye-udgivelser-automatisk)
      - [Ingen indexere er aktiveret](#ingen-indexere-er-aktiveret)
    - [Aktiverede indexere understøtter ikke søgning](#aktiverede-indexere-understøtter-ikke-søgning)
      - [Ingen indexere er tilgængelige med interaktiv søgning aktiveret](#ingen-indexere-er-tilgængelige-med-interaktiv-søgning-aktiveret)
      - [Indexere er utilgængelige på grund af fejl](#indexere-er-utilgængelige-på-grund-af-fejl)
      - [Jackett All Endpoint brugt](#jackett-all-endpoint-brugt)
        - [Løsninger](#løsninger)
    - [Kunstnermapper](#kunstnermapper)
      - [Manglende rodmappe](#manglende-rodmappe)
      - [Lister er utilgængelige på grund af fejl](#lister-er-utilgængelige-på-grund-af-fejl)
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

> Advarsel: Denne side er under udarbejdelse og er i øjeblikket et udkast baseret på Readarr
{.is-danger}

# Status

## Sundhed

Denne side indeholder en liste over fejl ved sundhedstjek. Disse sundhedstjek udføres periodisk af Lidarr og ved visse begivenheder. De resulterende advarsler og fejl vises her for at give råd om, hvordan de kan løses.

### Systemadvarsler

#### Gren er ikke en gyldig udgivelsesgren

Den gren, du har angivet, er ikke en gyldig udgivelsesgren. Du vil ikke modtage opdateringer. Skift til en af de [aktuelle udgivelsesgrene](/lidarr/faq#how-do-i-update-lidarr)

#### Opdater til .NET-version

{#update-to-net-core-version}

- Nyere versioner af Lidarr er målrettet mod .NET6 eller nyere. Vi vil ikke længere levere legacy mono-builds efter udgivelsen af 1.0. Du kører en af disse legacy-builds, men din platform understøtter .NET.

##### Fixing Docker-installationer

- Træk din container igen

##### Fixing Standalone-installationer

- Lav en sikkerhedskopi af din eksisterende konfiguration, før du går videre til næste trin.
- Dette skal kun ske på Linux-værter. Installer ikke .NET-runtime eller SDK fra Microsoft.
- For at rette problemet skal du downloade den korrekte version til din arkitektur og erstatte dine eksisterende binære filer (applikation)
- Kort sagt skal du slette dine eksisterende binære filer (indhold eller mappe i /opt/Lidarr) og erstatte dem med indholdet af .tar.gz-filen, du lige har downloadet.

> SLET IKKE BARE UDVIDELSEN OVER DINE EKSISTERENDE BINÆRE FILER.
> DU SKAL FØRST SLETTE DE GAMLE.
{.is-warning}

- Nedenstående er et af samfundet udviklet script til at fjerne din mono-installation og erstatte den med .NET-installationen. Bidrag og rettelser er velkomne.
- Dette antager, at du er på `master` Lidarr-grenen, opdater variablen om nødvendigt
- Dette antager, at Lidarr kører som brugeren `lidarr`, opdater variablene om nødvendigt
- Dette antager, at Lidarr er installeret i `/opt/Lidarr`, opdater variablene om nødvendigt

```bash
#!/bin/bash
## Bruger variabler
installdir="/opt/Lidarr"
APPUSER="lidarr"
branch="master"
## /Bruger variabler
app="lidarr"
ARCH=$(dpkg --print-architecture)
# Stop \*arr
sudo systemctl stop $app
# få arkitektur
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
echo "Installation af filer downloadet og udpakket"
echo "Flytter eksisterende installation"
sudo mv "$installdir/" "$installdir.old/"
echo "Installerer..."
sudo mv "${app^}" "$installdir"
sudo chown $APPUSER:$APPUSER -R $installdir
sudo sed -i "s|ExecStart=/usr/bin/mono --debug /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo sed -i "s|ExecStart=/usr/bin/mono /opt/${app^}/${app^}.exe|ExecStart=/opt/${app^}/${app^}|g" /etc/systemd/system/$app.service
sudo systemctl daemon-reload
echo "App installeret"
sudo rm -rf "$installdir.old/"
rm -rf "${app^}.*.tar.gz"
sudo systemctl start $app
```

#### Den aktuelt installerede mono-version er gammel og ikke understøttet

- Lidarr er skrevet i .NET og kræver Mono for at køre på meget gamle ARM-processorer. Bemærk, at Mono-builds ikke længere understøttes efter v1.0
- Mono 5.20 er det absolutte minimum for Lidarr.
- Opgraderingsproceduren for Mono varierer afhængigt af platformen.

#### Den aktuelt installerede SQLite-version understøttes ikke

- Lidarr gemmer sine data i en SQLite-database. Den SQLite3-bibliotek, der er installeret på dit system, er for gammel. Lidarr kræver mindst version 3.9.0. Bemærk, at Lidarr bruger `libSQLite3.so`, som muligvis er indeholdt i en opgraderingspakke til SQLite3.

#### Ny opdatering er tilgængelig

- Glæd dig, udviklerne har udgivet en ny opdatering. Dette betyder generelt fantastiske nye funktioner og rettelser af bunker af fejl (ikke sandt?). Tilsyneladende har du ikke aktiveret automatisk opdatering, så du bliver nødt til at finde ud af, hvordan du opdaterer på din platform. At trykke på knappen "Installer" på siden `System => Opdateringer` er sandsynligvis et godt udgangspunkt.

> Denne advarsel vises ikke, hvis din nuværende version er mindre end 14 dage gammel
{.is-info}

#### Kan ikke installere opdatering, fordi startmappe ikke kan skrives af brugeren

- Dette betyder, at Lidarr ikke kan opdatere sig selv. Du bliver nødt til at opdatere Lidarr manuelt eller angive tilladelserne for Lidarrs startmappe (installationsmappen) for at tillade Lidarr at opdatere sig selv.

#### Opdatering vil ikke være mulig for at forhindre sletning af AppData ved opdatering

- Lidarr har registreret, at AppData-mappen til dit operativsystem er placeret inde i mappen, der indeholder Lidarr-binærfilerne. Normalt ville det være `C:\ProgramData` for Windows og `~/.config` for Linux.

- Se på `System => Info` for at se de aktuelle AppData- og startmappemapper.
- Dette betyder, at Lidarr ikke vil kunne opdatere sig selv uden at risikere datatab.
- Hvis du er på Linux, skal du sandsynligvis ændre hjemmemappen for den bruger, der kører Lidarr, og kopiere indholdet af mappen `~/.config/Lidarr` for at bevare din database.

#### Gren er til en tidligere version

- Opdateringsgrenen, der er konfigureret i `Indstillinger => Generelt`, er til en tidligere version af Lidarr, og derfor vil instansen ikke se korrekte opdateringsoplysninger i feedet `System => Opdateringer` og modtager muligvis ikke nye opdateringer ved udgivelse.

#### Kunne ikke oprette forbindelse til signalR

- signalR driver de dynamiske UI-opdateringer, så hvis din browser ikke kan oprette forbindelse til signalR på din server, vil du ikke se nogen opdateringer i realtid i brugergrænsefladen.

- Den mest almindelige forekomst af dette er brug af en omvendt proxy eller cloudflare
- Cloudflare kræver aktivering af websockets.

##### NGINX

- Nginx kræver følgende tilføjelse til placeringen af appen:

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> Sørg for ikke at inkludere `proxy_set_header Connection "Upgrade";` som foreslået af nginx-dokumentationen. DETTE VIL IKKE VIRKE
> Se <https://github.com/aspnet/AspNetCore/issues/17081>
{.is-warning}

##### Apache

- For Apache2 omvendt proxy skal du aktivere følgende moduler: proxy, proxy_http og proxy_wstunnel. Derefter skal du tilføje denne websocket-tunnelanvisning til din vhost-konfiguration:

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8686/$1 [P,L]
```

##### Caddy

- For Caddy (V1) skal du bruge dette:
- Bemærk: Du skal også tilføje websocket-direktivet til din Lidarr-konfiguration

```none
 proxy /lidarr 127.0.0.1:8686 {
     websocket
     transparent
 }
```

#### Kunne ikke løse IP-adressen for den konfigurerede proxyvært

- Gennemgå dine proxyindstillinger og sørg for, at de er korrekte
- Sørg for, at din proxy er tændt, fungerer og er tilgængelig

#### Proxy mislykkedes test

- Din konfigurerede proxy mislykkedes at teste med succes, gennemgå HTTP-fejlen, der blev angivet, og/eller kontroller logfilerne for flere detaljer.

#### Systemtiden er mere end 1 dag forkert

- Systemtiden er mere end 1 dag forkert. Planlagte opgaver kan muligvis ikke køre korrekt, før tiden er rettet
- Gennemgå din systemtid og sørg for, at den er synkroniseret med en autoritativ tidsserver og er nøjagtig

#### Mono Legacy TLS aktiveret

- Mono 4.x tls-workaround er stadig aktiveret, overvej at fjerne miljøindstillingen `MONO_TLS_PROVIDER=legacy`

#### Mono og x86-builds ophører

- Mono- og x86-builds vil ikke længere blive understøttet i den næste version af applikationen. Hvis du modtager denne fejl, kører du mono-versionen af applikationen eller x86-versionen. Desværre vil vi på grund af stigende vanskeligheder med udviklingsstøtte til disse legacy-versioner ophøre med deres support og dermed udgivelser for dem fremover. Derfor anbefales det at opgradere til et understøttet operativsystem, der ikke kræver hverken x86 eller mono. Du kan også overveje at bruge Docker til dine behov.

#### FPcalc skal opdateres

{#fpcalc-upgrade}

- Lidarr bruger chromaprint audio fingerprinting til at identificere spor. Dette afhænger af en ekstern binær `fpcalc`, der distribueres med Lidarr v1 til Windows, Linux og macOS, men skal leveres uafhængigt på freeBSD.
- Sørg for, at den medfølgende fpcalc-binær, der følger med Lidarr, er eksekverbar (755 tilladelser). Denne fil findes i Lidarrs installationsmappe (f.eks. `/opt/Lidarr/fpcalc`). Hvis den ikke er eksekverbar, skal du rette dens tilladelser med følgende kommando og genstarte Lidarr.
  - Bemærk, at `sudo` muligvis kræves for at udføre rettelsen, eller din sti til Lidarrs binærmappe kan være anderledes afhængigt af dit miljø og opsætning.

```bash
chmod +x /opt/Lidarr/fpcalc
```

> Nedenstående oplysninger gælder kun for legacy v0.8.0-builds.
{.is-info}

- For at rette dette på en nativ Linux-instans skal du installere den passende pakke ved hjælp af din pakkehåndterer og sikre dig, at fpcalc er på din PATH (dette kan kontrolleres ved hjælp af kommandoen `which fpcalc` og verificere, at den korrekte placering af fpcalc returneres):

| Distribution  |       Pakke        |
| :-----------: | :----------------: |
| Debian/Ubuntu | libchromaprint-tools |
| Fedora/CentOS |  chromaprint-tools   |
|     Arch      |     chromaprint      |
|   OpenSUSE    |  chromaprint-fpcalc  |
|   Synology    |     chromaprint      |

### Downloadklienter

#### Ingen downloadklient er tilgængelig

- En korrekt konfigureret og aktiveret downloadklient er påkrævet for, at Lidarr kan downloade medier. Da Lidarr understøtter forskellige downloadklienter, skal du bestemme, hvilken der passer bedst til dine krav. Hvis du allerede har en downloadklient installeret, skal du konfigurere Lidarr til at bruge den og oprette en kategori. Se `Indstillinger => Downloadklient`.

#### Kan ikke kommunikere med downloadklient

- Lidarr kunne ikke kommunikere med den konfigurerede downloadklient. Bekræft venligst, at downloadklienten fungerer, og dobbelttjek URL'en. Dette kan også indikere en godkendelsesfejl.
- Dette skyldes normalt en forkert konfigureret downloadklient. Ting, du normalt kan kontrollere:
  - Din downloadklients IP-adresse - hvis det hele er på samme fysiske maskine, er det normalt `127.0.0.1`
  - Portnummeret, som din downloadklient bruger - disse er udfyldt med standardportnummeret, men hvis du har ændret det, skal du indtaste det samme i Lidarr.
  - Sørg for, at SSL-kryptering ikke er aktiveret, hvis du bruger både din Lidarr-instans og din downloadklient på et lokalt netværk (dvs. over almindelig HTTP). Se SSL-FAQ'en for mere information.

#### Downloadklienter er utilgængelige på grund af fejl

- En eller flere af dine downloadklienter reagerer ikke på anmodninger fra Lidarr. Derfor har Lidarr besluttet midlertidigt at stoppe forespørgsler til downloadklienten på dens normale 1-minuts cyklus, som normalt bruges til at spore aktive downloads og importere færdige downloads. Lidarr vil dog fortsætte med at forsøge at sende downloads til klienten, men vil med stor sandsynlighed mislykkes.
- Du bør inspicere `System => Logs` for at se årsagen til fejlene.
- Hvis du ikke længere bruger denne downloadklient, skal du deaktivere den i Lidarr for at forhindre fejlene.

#### Aktivér håndtering af fuldførte downloads

- Lidarr kræver, at "Håndtering af fuldførte downloads" er aktiveret for at kunne importere filer, der er downloadet af downloadklienten. Det anbefales at aktivere "Håndtering af fuldførte downloads". (Det er aktiveret som standard for nye brugere.)

#### Docker dårlig fjernsti-mapping

- Denne fejl er normalt forbundet med dårlige docker-stier i enten din downloadklient eller Lidarr

- Et eksempel på dårlige (inkonsekvente) stier ville være:
  - Downloadklient: `/mnt/user/downloads:/downloads`
  - Lidarr:   `/mnt/user/downloads:/data`
- I dette eksempel placerer downloadklienten sine downloads i `/downloads` og fortæller Lidarr, når det er færdigt, at den færdige bog er i `/downloads`. Lidarr kommer derefter og siger "Okay, fint, lad mig tjekke i `/downloads`." Nå, inde i Lidarr har du ikke allokeret en `/downloads`-sti, du har allokeret en `/data`-sti, så det kaster denne fejl.
- Den nemmeste løsning på dette er KONSISTENS - hvis du bruger en ordning i din downloadklient, skal du bruge den over hele linjen.

- Team Lidarr er stor fan af simpelthen at bruge /data.

  - Downloadklient: `/mnt/user/data/downloads:/data/downloads`
  - Lidarr: `/mnt/user/data:/data`

- Nu kan du inden for downloadklienten angive, hvor i `/data` du vil placere dine downloads, nu varierer dette afhængigt af klienten, men du skal kunne fortælle den "Ja, downloadklient, placer mine filer i `/data/downloads/movies`", og da du brugte `/data` i Lidarr, når downloadklienten fortæller Lidarr, at den er færdig, vil Lidarr komme og sige "Fedt, jeg har en `/data`, og jeg kan også se `/data/downloads/movies`, alt er i orden i verden."
- Der er mange gode vejledninger: vores wiki [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves)](https://trash-guides.info/hardlinks/). Nu lægger disse vejledninger stor vægt på hardlinks og atomic moves, men den generelle koncept med containere og hvordan sti-mapping fungerer, er kernen i disse diskussioner.
- Hvis du krydser operativsystemer eller native og docker, har du brug for en fjernsti-mapping. Se [TRaSH's Remote Path Guide for Radarr](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) og [Sonarr](https://trash-guides.info/Sonarr/Sonarr-remote-path-mapping/) for mere information.

#### Downloader til rodmappe

{#downloads-in-root-folder}

- Inden for applikationen defineres en rodmappe som den konfigurerede mediebibliotekmappe. Dette er ikke rodmappen for et monteringspunkt. Din downloadklient downloader ufuldstændige eller fuldstændige downloads (eller flytter fuldførte downloads) til din rod (biblioteks)mappe.
- Dette forårsager ofte problemer - herunder datatab - og bør ikke gøres. For at rette dette skal du ændre din downloadklient, så den ikke placerer downloads inden for din rodmappe. Bemærk, at 'placering' også inkluderer, hvis din downloadklients kategori er indstillet til din rodmappe, eller hvis NZBGet/SABnzbd har sortering aktiveret og sorterer til din rodmappe.
- Bemærk, at denne kontrol ser på alle definerede/konfigurerede rodmapper, der er tilføjet, ikke kun rodmapper, der i øjeblikket er i brug. Med andre ord skal mappen, hvor din downloadklient downloader til eller flytter fuldførte downloads til, ikke være den samme mappe, du har konfigureret som din rod/biblioteks/final destination for medier i *arr-applikationen.
- Konfigurerede rodmapper (også kendt som biblioteksmapper) kan findes i [Indstillinger => Mediehåndtering => Rodmapper](/lidarr/settings/#root-folders)
- Et eksempel er, hvis dine downloads går til `\data\downloads`, så har du en rodmappe, der er indstillet som `\data\downloads`.
- Det anbefales at bruge stier som `\data\media\` til din rodmappe/bibliotek og `\data\downloads\` til dine downloads.
- Gennemgå vores [Docker Guide](/docker-guide) og TRaSH's [Hardlinks and Instant Moves (Atomic-Moves) Guide](https://trash-guides.info/hardlinks/) for mere information om den korrekte og optimale stiopsætning. Bemærk, at koncepterne gælder for både docker og ikke-docker

> Din downloadmappe, hvor din downloadklient placerer downloads, og din rod/biblioteksmappe SKAL være adskilte. \*Arr importerer filen(e) fra din downloadklients mappe til dit bibliotek. Downloadklienten skal ikke flytte noget eller downloade noget til dit bibliotek.
{.is-warning}

#### Dårlige indstillinger for downloadklient

- Placeringen, som din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan være tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden en fjernsti-mapping.

#### Dårlig fjernsti-mapping

- Placeringen, som din downloadklient downloader filer til, forårsager problemer. Kontrollér logfilerne for yderligere oplysninger. Dette kan være tilladelser eller forsøg på at gå fra Windows til Linux eller Linux til Windows uden en fjernsti-mapping. Se [TRaSH's Remote Path Guide](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/) for mere information.

#### Tilladelsesfejl

- Lidarr (eller brugeren, som Lidarr kører som), kan ikke få adgang til placeringen, som din downloadklient downloader filer til. Dette er normalt et tilladelsesproblem.

#### Fjernfil blev fjernet under behandling

- En fil, der er tilgængelig via en fjernsti-mapping, ser ud til at være blevet fjernet, før behandlingen blev afsluttet.

#### Fjernsti bruges, og import mislykkedes

- Kontrollér dine logfiler for flere oplysninger. Se vores [Fejlfinding Guides](/lidarr/troubleshooting).

### Håndtering af fuldførte/mislukkede downloads

#### Håndtering af fuldførte downloads er deaktiveret

- Lidarr kræver, at "Håndtering af fuldførte downloads" er aktiveret for at kunne importere filer, der er downloadet af downloadklienten. Det anbefales at aktivere "Håndtering af fuldførte downloads". (Det er aktiveret som standard for nye brugere.)

### Indexere

#### Ingen indexere er tilgængelige med automatisk søgning aktiveret, Lidarr vil ikke give nogen automatisk søgning

- Med andre ord har du ikke nogen af dine indexere indstillet til at tillade automatisk søgning
- Gå til `Indstillinger => Indexere`, vælg en indexer, du gerne vil tillade automatisk søgning, og klik derefter på Gem.

#### Ingen indexere er tilgængelige med RSS-synkronisering aktiveret, Lidarr vil ikke hente nye udgivelser automatisk

- Lidarr bruger RSS-feedet til at opfange nye udgivelser, når de kommer. Mere information om dette kan findes her
- For at rette dette problem skal du gå til `Indstillinger => Indexere`, vælge en indexer, du har, og aktivere RSS-synkronisering

#### Ingen indexere er aktiveret

- Lidarr kræver indexere for at kunne opdage nye udgivelser. Læs venligst wikien for instruktioner om, hvordan du tilføjer indexere.

### Aktiverede indexere understøtter ikke søgning

- Ingen af de indexere, du har aktiveret, understøtter søgning. Dette betyder, at Lidarr kun vil være i stand til at finde nye udgivelser via RSS-feeds. Men søgning efter film (enten automatisk søgning eller manuel søgning) vil aldrig give nogen resultater. Den eneste måde at afhjælpe det på er selvfølgelig at tilføje en anden indexer.

#### Ingen indexere er tilgængelige med interaktiv søgning aktiveret

- Ingen af de indexere, du har aktiveret, understøtter interaktiv søgning. Dette betyder, at applikationen kun vil være i stand til at finde nye udgivelser via RSS-feeds eller en automatisk søgning.

#### Indexere er utilgængelige på grund af fejl

- Der opstår fejl, mens Lidarr forsøgte at bruge en af dine indexere. For at begrænse antallet af forsøg vil Lidarr ikke bruge indexeren i en stigende mængde tid (op til 24 timer).
- Denne mekanisme udløses, hvis Lidarr ikke kunne få et svar fra indexeren (kan skyldes DNS, proxy/VPN-forbindelse, godkendelse eller en indexer-fejl) eller ikke kunne hente nzb/torrent-filen fra indexeren.
- Gennemgå logfilerne for at bestemme, hvilken slags fejl der forårsager problemet.
- Du kan forhindre advarslen ved at deaktivere den berørte indexer.
- Kør testen på indexeren for at tvinge Lidarr til at kontrollere indexeren igen, bemærk venligst, at sundhedstjekadvarslen ikke altid forsvinder med det samme.

#### Jackett All Endpoint brugt

- Jackett `/all`-endpointen er praktisk, men det er dens eneste fordel. Alt andet er potentielle problemer, så det er nu nødvendigt at tilføje hver enkelt tracker individuelt.
- [Selv Jacketts udviklere siger, at det bør undgås og ikke bør bruges.](https://github.com/Jackett/Jackett#aggregate-indexers)
- Brug af `/all`-endpointen har ingen fordele, kun ulemper:
  - du mister kontrollen over indstillinger for specifikke indexere (kategorier, søgemetoder osv.)
  - blanding af søgemetoder (IMDB, forespørgsel osv.) kan give resultater af lav kvalitet
  - kategorier for specifikke indexere (>= 100000) kan ikke bruges.
  - langsomme indexere vil sænke den samlede hastighed
  - det samlede antal resultater er begrænset til 1000
  - hvis en af ​​trackerne returnerer en fejl, vil \*Arr deaktivere den, og nu får du ingen resultater.

##### Løsninger

- Tilføj hver enkelt tracker i Jackett manuelt som en indexer i \*Arr
- Se [Prowlarr](/prowlarr), der kan synkronisere indexere til \*Arr og fra Lidarr/Radarr/Readarr-udviklingsteamet.
- Se [NZBHydra2](https://github.com/theotherp/nzbhydra2), der kan synkronisere indexere til \*Arr. Brug dog ikke deres enkeltstående samlede endpoint og brug `multi`, hvis synkronisering skal bruges.

### Kunstnermapper

#### Manglende rodmappe

- Denne fejl identificeres normalt, hvis en kunstner leder efter en rodmappe, men den rodmappe er ikke længere tilgængelig.
- Denne fejl kan også opstå, hvis en liste stadig peger på en rodmappe, men den rodmappe ikke længere er tilgængelig.
- Hvis du vil fjerne denne advarsel, skal du blot finde albummet, der stadig bruger den gamle rodmappe, og redigere det til den korrekte rodmappe.

- Den nemmeste måde at finde kunstneren med problemet er at:

  - Gå til fanen Kunstner (Bibliotek)
  - Opret en brugerdefineret filter med den gamle rodmappesti
  - Vælg massevisning i øverste bjælke og vælg den nye rodsti, du vil flytte disse kunstnere til, fra rullelisten Rodstier.
  - Derefter får du en pop op-meddelelse, der siger Vil du flytte kunstnermapperne til 'rodsti'? Dette vil også sige Dette vil også omdøbe kunstnermappen i henhold til kunstnermappenformatet i indstillinger. Vælg bare Nej, hvis du ikke vil have, at Lidarr flytter dine filer
  - Kør sundhedstjekopgaven i System => Opgaver

#### Lister er utilgængelige på grund af fejl

- Normalt betyder dette bare, at Lidarr ikke længere kan kommunikere via API eller ved at logge ind på din valgte listeleverandør. Dit bedste bud, hvis problemet fortsætter, er at kontakte dem for at udelukke dem, da deres systemer måske er overbelastede fra tid til anden.
- Gennemgå System => Hændelser filtreret efter Advarsel (Advarsler og Fejl) for at se de historiske fejl eller kontrollere logfilerne for detaljer.
- Gennemgå System => Hændelser filtreret efter Advarsel (Advarsler og Fejl) for at se de historiske fejl eller kontrollere logfilerne for detaljer.

## Diskplads

- Denne sektion viser dig tilgængelig diskplads
- I docker kan dette være vanskeligt, da det normalt viser den tilgængelige plads inden for dit Docker-billede

## Om

- Dette vil fortælle dig om din aktuelle installation af Lidarr

## Mere info

- Hjemmeside: Lidarrs hjemmeside
- Wiki: Du er allerede her
- Reddit: r/lid