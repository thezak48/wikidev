---
title: Prowlarr Indstillinger
description: 
published: true
date: 2023-03-30T14:07:39.851Z
tags: 
editor: markdown
dateCreated: 2021-06-06T15:04:48.057Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Menuindstillinger](#menuindstillinger)
- [Indexer Proxies](#indexer-proxies)
  - [Proxyindstillinger](#proxyindstillinger)
  - [FlareSolverr Proxyindstillinger](#flaresolverr-proxyindstillinger)
  - [HTTP Proxyindstillinger](#http-proxyindstillinger)
  - [Socks4 Proxyindstillinger](#socks4-proxyindstillinger)
  - [Socks5 Proxyindstillinger](#socks5-proxyindstillinger)
- [Applikationer](#applikationer)
  - [Applikationsindstillinger](#applikationsindstillinger)
  - [Test af applikationen](#test-af-applikationen)
- [Downloadklienter (Prowlarr-søgninger)](#downloadklienter-prowlarr-søgninger)
  - [Usenet-klientindstillinger](#usenet-klientindstillinger)
  - [Torrent-klientindstillinger](#torrent-klientindstillinger)
  - [Test af downloadklienten](#test-af-downloadklienten)
- [Notifikationer](#notifikationer)
  - [Forbindelser](#forbindelser)
  - [Notifikationstriggere](#notifikationstriggere)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Vært](#vært)
  - [Sikkerhed](#sikkerhed)
  - [Proxy](#proxy)
  - [Logning](#logning)
  - [Analyse](#analyse)
  - [Opdateringer](#opdateringer)
  - [Backup](#backup)
- [Brugergrænseflade](#brugergrænseflade)
  - [Datoer](#datoer)
  - [Stil](#stil)
  - [Sprog](#sprog)
  
Denne side vil gennemgå alle indstillingerne i Prowlarr og hvordan de fungerer. Dette er ikke ment som en omfattende "sådan sætter du Prowlarr op". Hvis du ønsker det, skal du bruge [Quick Start](/prowlarr/quick-start-guide)-siden i stedet.

# Menuindstillinger

For at komme til indstillingssiden skal du vælge Indstillinger fra venstremenuen. Følgende undermenuindstillinger vil være tilgængelige:

![settings_1_menu.png](/assets/prowlarr/settings_1_menu.png)

Bemærk også, at der for hver individuel indstillingsside er nogle indstillinger øverst i menuen:

![settings_2_topmenu.png](/assets/prowlarr/settings_2_topmenu.png)

- Skjul/Vis avanceret er vigtigt for alle elementer, der er markeret som `(Avanceret indstilling)`, ellers vises de ikke. Disse menupunkter vises i orange på skærmbillederne.

- Du skal gemme dine ændringer, før du forlader skærmen. Dette gør du ved at klikke på diskikonet. Hvis du ikke har foretaget ændringer, vises "Ingen ændringer" og er gråtonet, som vist ovenfor.

# Indexer Proxies

> Information om understøttede proxytyper kan findes på siden [Mere info (Understøttet)](/prowlarr/supported#indexer-proxies) for denne sektion
{.is-info}

Her kan du tilføje proxier eller Flaresolverr-konfigurationer til de indexere, der kræver dem.

Naviger til `Indstillinger` => `Indexer Proxies`, og klik derefter på <kb>+</kb> for at tilføje en proxy.

![proxies.png](/assets/prowlarr/proxies.png)

## Proxyindstillinger
  
- Navn - Navnet på proxyen i Prowlarr
- Tags - Tags for denne proxy. Proxies gælder for alle matchende (samme tag) indexere. Hvis dette felt er tomt, gælder proxyen for alle indexere.

## FlareSolverr Proxyindstillinger

- Vært - den fulde værtssti (inklusive http og port) til din FlareSolverr-instans
- (Avanceret indstilling) Anmodningstimeout (sekunder) - værdien for [FlareSolver-anmodningsparameteren `maxTimeout`](https://github.com/FlareSolverr/FlareSolverr#-requestget), som Prowlarr skal bruge til FlareSolverr-anmodninger. Skal være mellem `1` sekund og `180` sekunder (standard: `60` sekunder)

> \* En FlareSolverr-proxy bruges kun til anmodninger, hvis og kun hvis Cloudflare opdages af Prowlarr
> \* En FlareSolverr-proxy bruges kun til anmodninger, hvis og kun hvis proxyen og indexeren har matchende tags
> \* **En Flaresolverr-proxy, der er konfigureret uden tags eller ikke har indexere med matchende tags, vil være deaktiveret.**
{.is-info}

## HTTP Proxyindstillinger

- Vært - værtsadressen for din proxy
- Port - porten for din proxy
- Brugernavn - brugernavnet til din proxy
- Adgangskode - adgangskoden til din proxy

## Socks4 Proxyindstillinger

- Vært - værtsadressen for din proxy
- Port - porten for din proxy
- Brugernavn - brugernavnet til din proxy
- Adgangskode - adgangskoden til din proxy

## Socks5 Proxyindstillinger

- Vært - værtsadressen for din proxy
- Port - porten for din proxy
- Brugernavn - brugernavnet til din proxy
- Adgangskode - adgangskoden til din proxy

# Applikationer

> Information om understøttede applikationer kan findes på siden [Mere info (Understøttet)](/prowlarr/supported#applications) for denne sektion
{.is-info}

Her tilføjer du applikationerne, der bruger Prowlarr (Radarr, Sonarr, Lidarr, Readarr osv.) og hvordan de holdes synkroniseret med Prowlarr.

- Klik på `Indstillinger` => `Apps`, og klik derefter på <kb>+</kb> for at tilføje en app.
- Synkroniser appindexere - Udløs en synkronisering af alle indexere til alle applikationer
- Test alle apps - Udløs en test af alle applikationer
  
![addapps.png](/assets/prowlarr/addapps.png)

Alle programmer, du kan tilføje, er opført. Du skal kun tilføje programmer, du allerede har installeret, og hvis du har flere instanser af dem, skal du tilføje hver af dem separat.

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Bemærk: Indexere synkroniseres baseret på de evner/kategorier, de hævder at understøtte. Hvis en indexer kun understøtter `tv`-kategorier, vil den ikke blive synkroniseret med Lidarr, Radarr og Readarr. Den vil kun blive synkroniseret med Sonarr. "Understøttede" kategorier kan vælges som en avanceret indstilling på en app-specifik basis. **Bemærk også, at \*Arrs kun accepterer indexere, hvis testforespørgsler returnerer resultater, der indeholder mindst en af de konfigurerede kategorier.**
{.is-info}

## Applikationsindstillinger

- Navn - Indtast et navn til denne app.
- Synkroniseringsniveau - Vælg synkroniseringsniveauet, der skal bruges
  - `Kun tilføjelse og fjernelse` - Når der tilføjes eller fjernes indexere fra Prowlarr, opdateres denne eksterne app. Hvis indexeret er nede på tidspunktet for synkroniseringen, deaktiveres det på den eksterne app.
  - `Fuld synkronisering` - Fuld synkronisering holder denne apps indexere fuldt synkroniseret. Ændringer foretaget på indexere i Prowlarr synkroniseres derefter til denne app. Enhver ændring foretaget på indstillingerne for disse indexere eksternt inden for denne app vil blive overskrevet af Prowlarr ved næste synkronisering. En liste over faktorer, der bruges til at sammenligne og afgøre, om en synkronisering skal finde sted, kan findes i [FAQ](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Deaktiveret` - forhindrer synkronisering af indexere med programmet.

> `Fuld synkronisering` betyder, at Prowlarr vil overskrive de fleste indstillinger, herunder brugerdefinerede kategorier, der kan konfigureres i Prowlarr. Dog vil indstillinger, der ikke administreres af Prowlarr, ikke blive berørt. Dog vil [næsten alle andre ændringer](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) udløse en synkronisering og overskrive de tilsvarende indstillinger i \*Arr
{.is-warning}

- Tags - Hvis du har tilføjet en tag til din indexer under opsætningen, vil kun indexere med denne tag blive brugt til denne programindgang.
- Prowlarr-server - Indtast Prowlarr-serverens URL (inklusive http, port og baseurl, hvis det er nødvendigt), som appen ville få adgang til, her.

> Bemærk, at hvis du bruger en omvendt proxy, skal du tilføje URL-basen her! Hvis du ikke gør det, vil indexerne blive ødelagt, når de synkroniseres, og hvis du har valgt kun at tilføje og fjerne, vil det ikke blive rettet, når du redigerer det!{.is-info}

- Applikationsserver - Indtast appserverens URL (inklusive http, port og baseurl, hvis det er nødvendigt) for dit program her. Indtast igen den fulde URL-base, hvis den bruges.
- API-nøgle - Indtast API-nøglen for dit program her. For \*Arrs kan denne findes i Indstillinger => Generelt. Du kan få denne fra dit program i fanen `Indstillinger` => `Generelt` og kopiere/indsætte den her.
- (Avanceret indstilling) Synkroniseringskategorier - Vælg de kategorier, der skal synkroniseres til denne app. Indexere, der understøtter disse kategorier, vil blive synkroniseret.
  - Indexerens brugerdefinerede kategorier bliver mappet til standardiserede Torznab/Newznab-kategorier, så søgning efter de standardiserede kategorier inkluderer alle underliggende brugerdefinerede kategorier. Indexerens brugerdefinerede kategorier vises for finjustering, hvis du ikke ønsker dem alle på én gang.
  
## Test af applikationen

Test din indtastning. Hvis der vises et grønt flueben, kan du gemme din indtastning og gentage processen efter behov for hver app, du vil synkronisere med Prowlarr. Hvis det mislykkes, skal du kontrollere din log for fejlen (URL, API-nøgle osv.).

## Synkroniseringsprofiler

Konfigurer synkroniseringsprofilerne til brug for en eller flere applikationer

> Du kan have forskellige indstillinger pr. app ved at oprette flere instanser af indexeret
{.is-info}

- Navn - Unikt navn for synkroniseringsprofilen
- Aktivér RSS - Aktivér RSS-søgninger/forespørgsler for \*Arr-appen for indexere med denne profil
- Aktivér interaktiv søgning - Aktivér interaktive (manuelle) søgninger for \*Arr-appen for indexere med denne profil
- Aktivér automatisk søgning - Aktivér automatisk søgning for \*Arr-appen for indexere med denne profil
- Minimum seedere - Minimum antal seedere, der kræves for, at \*Arr kan hente en torrent fra indexere med denne profil

# Downloadklienter (Prowlarr-søgninger)

{#download-clients}

> Information om understøttede downloadklienter kan findes på siden [Mere info (Understøttet)](/prowlarr/supported#download-clients) for denne sektion
{.is-info}

Hvis du har til hensigt at foretage søgninger direkte i Prowlarr, skal du tilføje downloadklienter. Ellers behøver du ikke at tilføje dem her. For søgninger fra dine apps bruges de downloadklienter, der er konfigureret der.

> Prowlarr synkroniserer ikke downloadklienter med applikationerne.
{.is-info}

Klik på `Indstillinger` => `Downloadklienter`, og klik derefter på <kb>+</kb> for at tilføje en ny downloadklient. Din downloadklient skal allerede være konfigureret i henhold til denne vejledning.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

Vælg den downloadklient, du vil tilføje, og der vises en pop op-boks til indtastning af forbindelsesoplysninger. Disse oplysninger er ens for de fleste klienter. Nogle vil bede om et brugernavn eller adgangskode, nogle vil spørge, om der skal tilføjes nye downloads i en pause/start-tilstand osv.
  
> Klientprioritet betyder kun noget, når der tilføjes 2 af samme type (usenet eller torrent). 1 er den højeste prioritet, og hvis der findes flere klienter af samme type med samme prioritet, vil Prowlarr skifte mellem dem.
{.is-info}

## Usenet-klientindstillinger

- Navn - Navnet på downloadklienten i Prowlarr
- Aktivér - Aktivér denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- API-nøgle - API-nøglen til godkendelse af din klient
- Brugernavn - Brugernavnet til godkendelse af din klient (typisk ikke nødvendigt)
- Adgangskode - Adgangskoden til godkendelse af din klient (typisk ikke nødvendigt)
- Kategori - Kategorien i din downloadklient, som Prowlarr vil bruge
- Prioritet - Prioritet for downloadklienten for tilføjede elementer
- Klientprioritet - Prioritet for downloadklienten i Prowlarr. Der bruges round-robin til klienter af samme type (torrent/usenet), der har samme prioritet.

## Torrent-klientindstillinger

- Navn - Navnet på downloadklienten i Prowlarr
- Aktivér - Aktivér denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient; dette er normalt webgui-porten
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- Brugernavn - Brugernavnet til godkendelse af din klient
- Adgangskode - Adgangskoden til godkendelse af din klient
- Kategori - Kategorien i din downloadklient, som Prowlarr vil bruge
- Prioritet - Prioritet for downloadklienten for tilføjede elementer
- Starttilstand - Starttilstand for torrents (kun Qbittorrent: Tvinger omgåelse af alle seed-grænser)
- Klientprioritet - Prioritet for downloadklienten i Prowlarr. Der bruges round-robin til klienter af samme type (torrent/usenet), der har samme prioritet.

## Test af downloadklienten

Test din indtastning. Hvis der vises et grønt flueben, kan du gemme din indtastning, og gentag efter behov for hver downloadklient, du vil have Prowlarr til at bruge. Hvis det mislykkes, skal du kontrollere din log for fejlen (forbindelse, legitimationsoplysninger osv.).

# Notifikationer

> Information om understøttede notifikationsudbydere kan findes på siden [Mere info (Understøttet)](/prowlarr/supported#notifications) for denne sektion
{.is-info}

## Forbindelser

Forbindelser er, hvordan du vil have Prowlarr til at kommunikere med omverdenen.

- Ved at trykke på <kb>+</kb>-knappen får du vist et nyt vindue, hvor du kan konfigurere mange forskellige slutpunkter

- En liste over understøttede notifikationer og forbindelser findes på [Mere info (Understøttet)](/prowlarr/supported#notifications)

## Notifikationstriggere

- Ved frigivelse - Få besked ved frigivelse fra Prowlarr eller via API'en
  - Inkluder manuelle frigivelser - Få besked ved manuelle frigivelser udløst i Prowlarr's brugergrænseflade
- Ved sundhedsproblem - Få besked ved fejl i sundhedstjek
  - Inkluder sundhedsadvarsler - Få besked ved sundhedsadvarsler udover fejl.
- Ved programopdatering - Få besked, når Prowlarr opdateres til en ny version

# Tags

- Tag-sektionen i Prowlarr bruges til at linke forskellige aspekter af Prowlarr.
- Tags er særligt nyttige til:
  - Aktivering af Flaresolverr-proxy til brug med en indexer; Bemærk, at Flaresolverr-proxies er deaktiveret uden en tag
  - Aktivering af en HTTP- eller SOCKS-proxy til brug med en indexer
  - Specifikation af indexere til visse apps

# Generelt

Her ændrer du generelle applikationsindstillinger som port og logningsniveau.

Klik på `Indstillinger` => `Generelt`.

> Mange af indstillingerne her kan kun ses ved at klikke på "Vis avanceret" øverst på skærmen. Eventuelle menupunkter i orange vises kun, når "Vis avanceret" er aktiveret.
{.is-info}

## Vært

![general_host.png](/assets/prowlarr/general_host.png)

- (Avanceret indstilling) Bind-adresse - Lad denne være `*`, medmindre du har brug for at ændre den. IPv4-adressen/værten på systemet, som Prowlarr skal lytte på. (standard: `*`)
  - Bemærk, at `*` er alle adresser
- Portnummer - porten, som Prowlarr kører på. Den skal være unik. (standard: 9696)
- BaseUrl - Indtast en URL-base her, hvis du bruger en omvendt proxy. (kræver genstart) (standard: blank)
- (Avanceret indstilling) Instansnavn - Navn, der skal bruges til browserfanen og SysLog (hvis aktiveret) (kræver genstart) (standard: Prowlarr)
- (Avanceret indstilling) Brug SSL - Marker dette felt, hvis du bruger en https-adresse til at oprette forbindelse til Prowlarr. Hvis du bruger `localhost` eller en IP-adresse, skal dette næsten ALDRIG være markeret. (standard: false)
- Start browser (kun Windows) - Marker dette felt, hvis du vil have åbnet et browser-vindue, når Prowlarr starter. (standard: ja)

## Sikkerhed

![general_security.png](/assets/prowlarr/general_security.png)

- Godkendelse - Hvordan vil du godkende for at få adgang til din Prowlarr-instans
  - Ingen - Du har ingen godkendelse for at få adgang til din Prowlarr. Typisk hvis du er den eneste bruger på dit netværk, ikke har nogen på dit netværk, der vil have adgang til din Radarr, eller din Radarr ikke er tilgængelig på internettet
  - Grundlæggende (Browser pop-up) - Denne mulighed viser en lille pop-up, når du får adgang til din Prowlarr, der giver dig mulighed for at indtaste et brugernavn og adgangskode
  - Formularer (Login-side) - Denne mulighed har en velkendt login-skærm, ligesom andre websteder har, der giver dig mulighed for at logge ind på din Prowlarr
- API-nøgle - API-nøglen bruges af eksterne apps, der får adgang til Prowlarr. Denne nøgle er hemmelig og må ikke deles med nogen. Hvis den deles, skal du generere en ny og opdatere dine apps.
- Certifikatvalidering - Ændrer hvor streng validering af HTTPS-certifikater er
  - Aktiveret - Valider alle HTTPS-certifikater (anbefales)
  - Deaktiveret for lokale adresser - Valider alle HTTPS-certifikater undtagen dem på localhost og LAN
  - Deaktiveret - Valider ingen HTTPS-certifikater

## Proxy

![general_proxy.png](/assets/prowlarr/general_proxy.png)

Proxy - Denne mulighed giver dig mulighed for at køre den information, din Prowlarr henter og søger efter, gennem en proxy. Dette kan være nyttigt, hvis du befinder dig i et land, der ikke tillader download af torrent-filer.

- Brug Proxy - Aktivér for at bruge en proxy
- Proxytype - Vælg din proxytype (HTTPS, Socks4 eller Socks5)
- Værtsnavn - Indtast dit proxy-værtsnavn (Inkluder ikke http/https eller andre protokoller)
- Port - Indtast din proxy-port
- Brugernavn - Indtast dit proxy-brugernavn, hvis relevant
- Adgangskode - Indtast din proxy-adgangskode, hvis relevant
- Ignorerede adresser - Indtast en kommasepareret liste over adresser, der skal omgå proxyen
- Omgå proxy for lokale adresser - Markér afkrydsningsfeltet for at omgå proxyen for lokale adresser.

## Logning

![general_logging.png](/assets/prowlarr/general_logging.png)

Standardlogniveauet er `Info`. Dette er meget grundlæggende logning. Du kan ændre det her for mere detaljeret logning. Logfilerne vil rotere, så der er ingen fare for at fylde for meget plads.

- Logniveau - Sandsynligvis et af de mest nyttige fejlfindingværktøjer
  - Info - Dette er den mest grundlæggende måde, hvorpå Prowlarr indsamler information. Denne logfil indeholder fatal, fejl, advarsel og info-oplysninger.
  - Debug - Debug inkluderer alle de oplysninger, som Info inkluderer, plus mere information, der kan være nyttig. Denne logfil indeholder fatal, fejl, advarsel, info og debug-oplysninger.
  - Trace - Den mest avancerede og detaljerede logning på Prowlarr. Trace inkluderer alle de oplysninger, der er indsamlet af Info og Debug og mere. Dette er den mest almindelige type log, der bliver bedt om, når der fejlfindes på Discord eller Reddit. Hvis du har brug for hjælp, skal du vælge din log til Trace og gentage den opgave, der gav dig problemer for at fange loggen. Denne logfil indeholder fatal, fejl, advarsel, info, debug og trace-oplysninger.

## Analyse

![general_analytics.png](/assets/prowlarr/general_analytics.png)

- Analyse - Send anonym brugs- og fejlinformation til Prowlarr's servere (Servarr). Dette inkluderer oplysninger om din browser, hvilke Prowlarr WebUI-sider du bruger, fejlrapportering samt OS, runtime-version og relaterede oplysninger. Vi vil bruge disse oplysninger til at prioritere funktioner og fejlrettelser.

## Opdateringer

![general_updates.png](/assets/prowlarr/general_updates.png)

- (Avanceret indstilling) Gren - Dette er grenen af Prowlarr, som du kører på.
  - [Se venligst denne FAQ-indgang for mere information](/prowlarr/faq#how-do-i-update-prowlarr)
- Automatisk - Hent og installer opdateringer automatisk. Du vil stadig kunne installere fra System: Opdateringer. Bemærk: Windows-brugere opdateres altid automatisk.
- Mekanisme - Brug Prowlarr's indbyggede opdateringsværktøj eller et script
  - Indbygget - Brug Prowlarr's eget opdateringsværktøj
  - Script - Få Prowlarr til at køre opdateringsscriptet
  - Docker - Opdater ikke Prowlarr indefra Docker, træk i stedet et helt nyt billede med den nye opdatering
- Script - Synlig kun når mekanismen er indstillet til Script - Sti til opdateringsscript
- Opdateringsproces - Prowlarr vil downloade opdateringsfilen, verificere dens integritet, udpakke den til en midlertidig placering og kalde den valgte metode. Opdateringsprocessen køres under samme bruger, som Prowlarr kører under, og den skal have tilladelser til at opdatere Prowlarr-filerne samt stoppe/starte Prowlarr.
- Indbygget - Den indbyggede metode vil tage backup af Prowlarr-filer og indstillinger, stoppe Prowlarr, opdatere installationen og starte Prowlarr igen. Hvis dit system ikke kan håndtere stop af Prowlarr og vil forsøge at genstarte det automatisk, kan det være bedst at bruge et script i stedet. Hvis opdateringen mislykkes, vil den tidligere version af Prowlarr blive genstartet.
- Script - Scriptet skal håndtere det samme som det indbyggede opdateringsværktøj. Hvis du skal håndtere stop og start af tjenester (upstart/launchd/etc), skal du gøre det her.

## Sikkerhedskopier

![general_backups.png](/assets/prowlarr/general_backups.png)

- (Avanceret indstilling) Mappe - Dette giver dig mulighed for at vælge placeringen for sikkerhedskopier. I Docker vil du være begrænset til, hvad containeren kan se. Stier er relative til appdata-mappen; hvis det er nødvendigt, kan du angive en absolut sti til sikkerhedskopier uden for appdata-mappen.
- (Avanceret indstilling) Interval - Hvor ofte vil du have, at Prowlarr skal lave en sikkerhedskopi
- (Avanceret indstilling) Opbevaring - Hvor længe vil du have, at Prowlarr skal beholde hver sikkerhedskopi. Efter at en ny sikkerhedskopi er lavet, vil den ældste sikkerhedskopi blive fjernet

> Manuelle sikkerhedskopier bevares for evigt, opbevares i samme mappe og har forskellige navne.
{.is-info}

# Brugerflade

## Datoer

- Kort datoformat - Hvordan vil du have, at Prowlarr skal vise korte datoer?
- Langt datoformat - Hvordan vil du have, at Prowlarr skal vise datoer i langt format?
- Tidsformat - Vil du have et 12-timers eller 24-timers format?
- Vis relative datoer - Vil du have, at Prowlarr skal vise relative (I dag/I går/osv.) eller absolutte datoer?

## Stil

- Tema - Vælg farvetemaet, som Prowlarr skal bruge, inspireret af [Theme.Park](https://github.com/GilbN/theme.park)
- Aktivér farveblind tilstand - Ændret stil for at gøre det lettere for farveblinde brugere at skelne farvekodede oplysninger

## Sprog

- Brugerfladesprog - Vælg sproget, som Prowlarr skal bruge i applikationens brugerflade