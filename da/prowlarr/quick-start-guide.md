---
title: Prowlarr Hurtigstartguide
description: 
published: true
date: 2023-04-06T16:04:33.682Z
tags: 
editor: markdown
dateCreated: 2023-04-06T16:04:33.682Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Indexere](#indexere)
- [Apps](#apps)
  - [Applikationsindstillinger](#applikationsindstillinger)
- [Downloadklienter](#downloadklienter)
  - [Usenet-klientindstillinger](#usenet-klientindstillinger)
  - [Torrent-klientindstillinger](#torrent-klientindstillinger)
  - [Test af downloadklienten](#test-af-downloadklienten)
- [Opsætning fuldført](#opsætning-fuldført)

> Denne side er stadig under udarbejdelse og er ikke fuldendt.

> For en mere detaljeret gennemgang af alle indstillinger, se [Prowlarr => Indstillinger](/prowlarr/settings)

I denne guide vil vi forsøge at forklare den grundlæggende opsætning, du skal udføre for at komme i gang med Prowlarr. Vi vil springe nogle indstillinger over, som du måske ser på skærmen. Hvis du vil dykke dybere ned i disse indstillinger, kan du se den relevante side i FAQ'en og dokumentationen for en fuld forklaring.

> Bemærk venligst, at inden for skærmbillederne og GUI-indstillingerne i `orange` er avancerede indstillinger, så du skal klikke på `Vis avanceret` øverst på siden for at gøre dem synlige.

# Indexere

Det første, du skal konfigurere i Prowlarr, er indexere. Du vil tilføje hver indexer individuelt til Prowlarr.

Klik på `Indexere` og klik derefter på + for at tilføje en ny indexer.

![addindexer.png](/assets/prowlarr/addindexer.png)

Alle indexere, du kan tilføje (usenet og torrent), er opført, og du kan skrive for at matche delvist med en eksisterende indtastning. Hvis indexeret, du vil tilføje, ikke findes på listen, kan du tilføje "Generic Newznab" (til usenet) eller "Generic Torznab" (til torrents).

![addgeneric.png](/assets/prowlarr/addgeneric.png)

Nogle indexere har specielle indstillinger, men de fleste er standard, som vist.

![addnewindexer.png](/assets/prowlarr/addnewindexer.png)

- Navn - Vælg et navn til denne indexer. Når den synkroniseres med dine apps, vil den tilføje `(Prowlarr)` efter navnet.
- Aktiver - Markér afkrydsningsfeltet for at aktivere denne indexer.
- Omdiriger - Markér afkrydsningsfeltet, hvis en omdirigering er nødvendig. Der er kun et par indexere, hvor dette er nødvendigt for at undgå at blive blokeret. Hvis det er aktiveret, vil det sende downloadlinket direkte til applikationen i stedet for at proxy det via Prowlarr.

> Omdirigering er normalt kun nødvendig for en håndfuld meget specifikke indexere.

- Synkroniseringsprofil - Vælg din synkroniseringsprofil her. Disse kan oprettes i [`Indstillinger` => `Apps`](/prowlarr/settings#applications). Standardprofilen, Standard, eksisterer allerede og ser sådan ud:

> Du kan have forskellige indstillinger pr. app ved at oprette flere forekomster af indexeret.

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Vælg URL'en, som Prowlarr skal bruge. Hvis feltet er tomt, bruges standard-/første URL.
- Downloadlink - Hvis du tilføjer en torrent-indexer, skal du muligvis vælge, hvilken type downloadlink, der skal bruges.
- (Avanceret indstilling) API-sti - Sti til indexerens API. Typisk `/api`
- Legitimationsoplysninger - Mange indexere og trackere kræver, at du godkender/logge ind på en eller anden måde. Du skal muligvis indtaste en API-nøgle, en RSS-nøgle, en sessions-id, en cookie eller andre legitimationsoplysninger fra din indexer (som normalt findes på din profilside eller under sikkerhed), vælge søgeordrer eller andre indstillinger for din specifikke indexer.
  - API-nøgle
  - RSS-nøgle
  - Sessions-id
  - Cookie
  - Brugernavn/adgangskode
  - osv.
- (Avanceret indstilling) Yderligere parametre - Yderligere parametre, der skal tilføjes til anmodningerne for denne indexer.
- VIP-udløb - Indtast datoen i ISO-format (yyyy-MM-DD) for at få besked 1 uge før udløbet; ellers lad feltet være tomt
- Tags - Brug tags til at angive standard-downloadklienter, angive indexer-proxies, angive indexere til applikationer eller bare til at organisere dine indexere.
- (Avanceret indstilling) Søgebegrænsning - Hvis din indexer begrænser dine API-forespørgsler pr. dag, kan du indtaste det antal her for at undgå at overskride grænsen.
- (Avanceret indstilling) Grab-begrænsning - Hvis din indexer begrænser dine grabs pr. dag, kan du indtaste det antal her for at undgå at overskride grænsen. Når grab-begrænsningen er nået, vil yderligere forespørgsler udløse en ukontrolleret undtagelse i \*Arr-apps. Andre apps kan variere.
- (Avanceret indstilling) Seed-forhold - Kun for torrent-indexere: Forholdet, som en torrent skal nå, før den stopper. Hvis feltet er tomt, bruges standardindstillingen for appen.
- (Avanceret indstilling) Seed-tid - Kun for torrent-indexere: Tiden, som en torrent skal seedes, før den stopper. Hvis feltet er tomt, bruges standardindstillingen for appen.
- (Avanceret indstilling) Indexer-prioritet - Vælg indexer-prioriteten her fra 1-50 (1 er højest). Disse prioriteter synkroniseres med dine apps.

Test din indtastning. Hvis der vises et grønt flueben, kan du gemme din indtastning og gentage processen for hver indexer, du vil bruge med Prowlarr. Hvis det mislykkes, skal du kontrollere din log for fejlen (URL, API-nøgle osv.).

# Apps

Efter du har tilføjet dine indexere, forbinder vi derefter Prowlarr med dine andre apps.

Klik på `Indstillinger` => `Apps` og klik derefter på + for at tilføje en understøttet app.

![addapps.png](/assets/prowlarr/addapps.png)

Alle programmer, du kan tilføje, er opført. Du skal kun tilføje programmer, du allerede har installeret, og hvis du har flere forekomster af dem, skal du tilføje hver af dem separat.

> De aktuelt understøttede apps kan findes på siden [Mere info (Understøttet)](/prowlarr/supported#applications) for denne sektion

Når du tilføjer en app, skal du indtaste værdier i pop op-vinduet:

![addlidarr.png](/assets/prowlarr/addlidarr.png)

> Bemærk: Indexere synkroniseres baseret på de kapabiliteter/kategorier, de hævder at understøtte. Hvis en indexer kun understøtter `tv`-kategorier, vil den ikke blive synkroniseret med Lidarr, Radarr og Readarr. Den vil kun blive synkroniseret med Sonarr. "Understøttede" kategorier kan vælges som en avanceret indstilling på app-basis. **Bemærk også, at \*Arrs kun accepterer indexere, hvis testforespørgsler returnerer resultater, der indeholder mindst en af de konfigurerede kategorier.**

## Applikationsindstillinger

- Navn - Indtast et navn for denne app.
- Synkroniseringsniveau - Vælg synkroniseringsniveauet, der skal bruges
  - `Tilføj og fjern kun` - Når der tilføjes eller fjernes indexere fra Prowlarr, opdateres denne fjernapp. Hvis indexeret er nede på tidspunktet for synkroniseringen, deaktiveres det på fjernappen.
  - `Fuld synkronisering` - Fuld synkronisering holder denne apps indexere fuldt synkroniseret. Ændringer foretaget på indexere i Prowlarr synkroniseres derefter til denne app. Eventuelle ændringer foretaget på indstillingerne for disse indexere eksternt inden for denne app vil blive overskrevet af Prowlarr ved næste synkronisering. En liste over faktorer, der bruges til at sammenligne og afgøre, om en synkronisering skal finde sted, kan findes i [FAQ'en](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync)
  - `Deaktiveret` - forhindrer synkronisering af indexere med programmet.

> `Fuld synkronisering` betyder, at Prowlarr vil overskrive de fleste indstillinger, herunder brugerens valgte kategorier, der kan konfigureres i Prowlarr. Dog vil indstillinger, der ikke administreres af Prowlarr, ikke blive berørt. Dog vil [næsten alle andre ændringer](/prowlarr/faq#what-arr-indexer-settings-are-compared-for-app-full-sync) udløse en synkronisering og overskrive de tilsvarende indstillinger i \*Arr.
{.is-warning}

- Tags - Hvis du har tilføjet en tag til din indexer under opsætningen, vil kun indexere med denne tag blive brugt til denne programindtastning.
- Prowlarr-server - Indtast Prowlarr-serverens URL (inklusive http, port og baseurl, hvis det er nødvendigt), som appen ville få adgang til, her.

> Bemærk, at hvis du bruger en omvendt proxy, skal du tilføje URL-basen til dette! Hvis du ikke gør det, vil indexerne ikke blive synkroniseret, og hvis du har valgt Tilføj og fjern kun, vil det ikke blive rettet, når du redigerer det!

- Applikationsserver - Indtast app-serverens URL (inklusive http, port og baseurl, hvis det er nødvendigt) for dit program her. Indtast igen den fulde URL-base, hvis den bruges.
- API-nøgle - Indtast API-nøglen for dit program her. For \*Arrs kan denne findes i Indstillinger => Generelt. Du kan få denne fra dit program i fanen `Indstillinger` => `Generelt` og kopiere/indsætte den her.
- (Avanceret indstilling) Synkroniseringskategorier - Vælg de kategorier, der skal synkroniseres med denne app. Indexere, der understøtter disse kategorier, vil blive synkroniseret.
  - Individuelle brugerdefinerede kategorier bliver mappet til standard Torznab/Newznab-kategorier, så søgning efter standardiserede kategorier inkluderer alle underliggende brugerdefinerede kategorier. Individuelle brugerdefinerede kategorier vises for finjustering, hvis du ikke ønsker dem alle på én gang.

> Når du gemmer dette, vil det synkronisere dine indexere med appen. De tilføjes alle med det navn, du har valgt til din indexer plus (Prowlarr) efter det. f.eks. `{Indexer Navn} (Prowlarr)`

![nzbgeek.png](/assets/prowlarr/nzbgeek.png)

Du bør derefter gå ind i dit program og deaktivere versionen af indexeret, der ikke er fra Prowlarr. Når alt fungerer problemfrit, kan du slette disse indtastninger og kun efterlade (Prowlarr)-versionerne.

Du kan ønske at gå ind i dine programmer og kontrollere kategorierne for Prowlarr-indexerne. Standardkategorier, der skal mappes til appen, kan konfigureres som en avanceret indstilling for appen i Prowlarr.

> **Bemærk venligst, at brugerdefinerede/ikke-standard indexer-specifikke kategorier bliver mappet til standardkategorier, så søgning efter standardkategorier vil omfatte alle brugerdefinerede kategorier**

## Synkroniseringsprofiler

Konfigurer synkroniseringsprofilerne, der skal bruges for (en) applikation(er)

- Navn - Unikt navn for synkroniseringsprofilen
- Aktivér RSS - Aktivér RSS-søgninger/forespørgsler for indexere med denne profil i \*Arr-appen
- Aktivér interaktiv søgning - Aktivér interaktive (manuelle) søgninger for indexere med denne profil i \*Arr-appen
- Aktivér automatisk søgning - Aktivér automatisk søgning for indexere med denne profil i \*Arr-appen
- Minimum seedere - Minimum antal seedere, der kræves for, at \*Arr kan downloade en torrent fra indexere med denne profil

# Downloadklienter (Prowlarr-søgninger)

> Hvis du har til hensigt at foretage søgninger direkte i Prowlarr, skal du tilføje downloadklienter. Ellers behøver du ikke at tilføje dem her. Søgninger fra dine apps bruger de konfigurerede downloadklienter der i stedet.

> Downloadklienter er kun til Prowlarr-søgninger i appen og synkroniseres ikke med apps. Der er ingen planer om at tilføje en sådan funktionalitet.

Klik på `Indstillinger` => `Downloadklienter` og klik derefter på + for at tilføje en ny downloadklient. Din downloadklient skal allerede være konfigureret i overensstemmelse med denne vejledning.

![downloadclients.png](/assets/prowlarr/downloadclients.png)

> De aktuelt understøttede downloadklienter kan findes på siden [Mere info (Understøttet)](/prowlarr/supported#downloadclient) for denne sektion

Vælg den downloadklient, du vil tilføje, og der vises en pop op-boks til at indtaste forbindelsesoplysninger. Disse oplysninger er ens for de fleste klienter. Nogle vil bede om et brugernavn eller adgangskode, nogle vil spørge, om nye downloads skal tilføjes i en paused/start-tilstand osv.  
![nzbget.png](/assets/prowlarr/nzbget.png)

> Klientprioritet betyder kun noget, når der tilføjes 2 af samme type (usenet eller torrent). 1 er den højeste prioritet, og hvis der findes flere klienter af samme type og med samme prioritet, vil Prowlarr skifte mellem dem.

## Usenet-klientindstillinger

- Navn - Navnet på downloadklienten i Prowlarr
- Aktivér - Aktivér denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxys.
- API-nøgle - API-nøglen til at godkende over for din klient
- Brugernavn - Brugernavnet til at godkende over for din klient (normalt ikke nødvendigt)
- Adgangskode - Adgangskoden til at godkende over for din klient (normalt ikke nødvendigt)
- Kategori - Kategorien i din downloadklient, som Prowlarr vil bruge
- Prioritet - Downloadklientprioritet for tilføjede elementer
- Klientprioritet - Prioritet for downloadklienten i Prowlarr. Der bruges round-robin for klienter af samme type (torrent/usenet), der har samme prioritet.

## Torrent-klientindstillinger

- Navn - Navnet på downloadklienten i Prowlarr
- Aktivér - Aktivér denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxys.
- Brugernavn - Brugernavnet til at godkende over for din klient
- Adgangskode - Adgangskoden til at godkende over for din klient
- Kategori - Kategorien i din downloadklient, som Prowlarr vil bruge
- Prioritet - Downloadklientprioritet for tilføjede elementer
- Initial State - Starttilstand for torrents (kun Qbittorrent: Tvinger til at omgå alle seed-tærskler)
- Klientprioritet - Prioritet for downloadklienten i Prowlarr. Der bruges round-robin for klienter af samme type (torrent/usenet), der har samme prioritet.

## Test af downloadklienten

Test din indtastning. Hvis der vises et grønt flueben, kan du gemme din indtastning og gentage processen for hver downloadklient, du vil bruge med Prowlarr. Hvis det mislykkes, skal du kontrollere din log for fejlen (forbindelse, legitimationsoplysninger osv.).

# Opsætning fuldført

Det er det for det grundlæggende! Du kan derefter tilføje meddelelser og andre mere avancerede opsætningsmuligheder efter behov. Disse er dokumenteret på den fulde indstillingsside.