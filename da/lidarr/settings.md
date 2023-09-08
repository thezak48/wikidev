---
title: Lidarr Indstillinger
description: 
published: true
date: 2022-07-24T14:21:19.994Z
tags: lidarr, needs-love, indstillinger
editor: markdown
dateCreated: 2021-06-14T21:36:07.513Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [Indstillinger](#indstillinger)
- [Downloadklienter](#downloadklienter)
  - [Oversigt](#oversigt)
  - [Processer for downloadklient](#processer-for-downloadklient)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [Downloadklienter](#downloadklienter-1)
    - [Understøttede downloadklienter](#understøttede-downloadklienter)
    - [Indstillinger for Usenet-klient](#indstillinger-for-usenet-klient)
    - [Indstillinger for Torrent-klient](#indstillinger-for-torrent-klient)
    - [Kompatibilitet med fjernelse af download i Torrent-klient](#kompatibilitet-med-fjernelse-af-download-i-torrent-klient)
  - [Håndtering af fuldførte downloads](#håndtering-af-fuldførte-downloads)
    - [Fjern fuldførte downloads](#fjern-fuldførte-downloads)
    - [Håndtering af mislykkede downloads](#håndtering-af-mislykkede-downloads)
  - [Fjernstyring af sti-mapping](#fjernstyring-af-sti-mapping)
- [Importlister](#importlister)
  - [Importlister](#importlister-1)
  - [Undtagelser for importlister](#undtagelser-for-importlister)
  - [Tilføjelse af en importliste](#tilføjelse-af-en-importliste)
- [Forbindelser](#forbindelser)
- [Tags](#tags)
- [Generelt](#generelt)
  - [Opdateringer](#opdateringer)

# Indstillinger

Denne side er under udarbejdelse, og bidrag - baseret på andre \*Arr-sider - er både velkomne og stærkt opfordrede.

# Downloadklienter

> Oplysninger om understøttede downloadklienter kan findes på siden [Mere info (Understøttet)](/lidarr/supported#downloadklienter) for dette afsnit
{.is-info}

## Oversigt

- Download og import er, hvor de fleste mennesker oplever problemer. Set fra et overordnet perspektiv skal softwaren kunne kommunikere med din downloadklient og have adgang til de filer, den downloader. Der er mange forskellige understøttede downloadklienter og endnu flere forskellige opsætninger. Dette betyder, at selvom der er nogle fælles opsætninger, er der ikke én rigtig opsætning, og alle opsætninger kan være lidt forskellige. Men der er mange forkerte opsætninger.

## Processer for downloadklient

## Usenet

- Lidarr vil sende en downloadanmodning til din klient og associere den med et label eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Lidarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er fuldført, vil Lidarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe og tilgængelig for Lidarr.
- Lidarr vil scanne denne fuldførte filplacering for filer, som Lidarr kan bruge. Den vil analysere filnavnet for at matche det med det ønskede medie. Hvis det kan gøre det, vil den omdøbe filen i henhold til dine specifikationer og flytte den til den angivne medieplacering.
- Atomiske flytninger (øjeblikkelige flytninger) er aktiveret som standard. Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis den atomiske flytning mislykkes, eller din opsætning ikke understøtter hardlinks og atomiske flytninger, vil Lidarr falde tilbage og kopiere filen og derefter slette den fra kilden, hvilket er IO-intensivt.
- Hvis indstillingen "Fuldført downloadhåndtering - Fjern" er aktiveret i Lidarrs indstillinger, vil resterende filer fra downloaden blive sendt til papirkurven eller genbrugsbeholderen via en anmodning til din klient om at slette/fjerne udgivelsen.

## BitTorrent

- Lidarr vil sende en downloadanmodning til din klient og associere den med et label eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
  - Eksempler: film, tv, serier, musik osv.
- Lidarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Færdige filer efterlades på deres oprindelige placering for at give dig mulighed for at seede filen (ratio eller tid kan justeres i downloadklienten eller fra Lidarr under den specifikke downloadklient). Når filer importeres til din mediemappe, vil Lidarr oprette en hardlink til filen, hvis det understøttes af din opsætning, eller kopiere den, hvis hardlinks ikke understøttes.
- Hardlinks er aktiveret som standard. [Et hardlink vil ikke bruge yderligere diskplads.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet og monteringerne skal være de samme for din fuldførte downloadmappe og dit mediebibliotek. Hvis oprettelsen af hardlinket mislykkes, eller din opsætning ikke understøtter hardlinks, vil Lidarr falde tilbage og kopiere filen.
- Hvis indstillingen "Fuldført downloadhåndtering - Fjern" er aktiveret i Lidarrs indstillinger, vil Lidarr slette torrenten fra din klient og bede klienten om at fjerne torrentdataene, men kun hvis klienten rapporterer, at seeding er fuldført, og torrenten er stoppet (pauser ved fuldførelse).

## Downloadklienter

Klik på `Indstillinger => Downloadklienter` og klik derefter på <kb>+</kb> for at tilføje en ny downloadklient. Din downloadklient skal allerede være konfigureret og kørende.

### Understøttede downloadklienter

- En liste over understøttede downloadklienter findes på siden [Mere info (Understøttet)](/lidarr/supported#downloadklienter) for dette afsnit

Vælg den downloadklient, du ønsker at tilføje, og der vil være en pop-up-boks til at indtaste forbindelsesoplysninger. Disse oplysninger er ens for de fleste klienter. Nogle vil bede om et brugernavn eller adgangskode, nogle vil spørge, om der skal tilføjes nye downloads i en paused/start-tilstand osv.

### Indstillinger for Usenet-klient

- Navn - Navnet på downloadklienten i Lidarr
- Aktiver - Aktivér denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- API-nøgle - API-nøglen til at godkende din klient
- Brugernavn - Brugernavnet til at godkende din klient (typisk ikke nødvendigt)
- Adgangskode - Adgangskoden til at godkende din klient (typisk ikke nødvendigt)
- Kategori - Kategorien i din downloadklient, som \*Arr vil bruge. For at undgå uvedkommende downloads i Aktivitet anbefales det stærkt at angive en kategori.
- Prioritet for nyligt udgivet - downloadklientprioritet for nyligt udgivet medie
- Prioritet for ældre udgivet - downloadklientprioritet for medie, der ikke er udgivet for nyligt
- (Avanceret indstilling) Klientprioritet - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet

### Indstillinger for Torrent-klient

- Navn - Navnet på downloadklienten i Lidarr
- Aktiver - Aktivér denne downloadklient
- Vært - URL'en for din downloadklient
- Port - Porten for din downloadklient; dette er typisk webgui-porten
- Brug SSL - Brug en sikker forbindelse til din downloadklient. Vær opmærksom på denne almindelige fejl.
- (Avanceret indstilling) URL-base - Tilføj et præfiks til URL'en; dette er ofte nødvendigt for omvendte proxier.
- Brugernavn - Brugernavnet til at godkende din klient
- Adgangskode - Adgangskoden til at godkende din klient
- Kategori - Kategorien i din downloadklient, som \*Arr vil bruge. For at undgå uvedkommende downloads i Aktivitet anbefales det stærkt at angive en kategori.
- Kategori efter import - kategorien, der skal angives efter, at udgivelsen er downloadet og importeret. Bemærk, at dette bryder fjernelse af fuldførte downloadhåndtering.
- Prioritet for nyligt udgivet - downloadklientprioritet for nyligt udgivet medie
- Prioritet for ældre udgivet - downloadklientprioritet for medie, der ikke er udgivet for nyligt
- Starttilstand - Starttilstand for torrents (kun Qbittorrent: Tvungen omgåelse af alle seed-tærskler)
- (Avanceret indstilling) - Prioritet for downloadklienten. Round-Robin bruges til klienter af samme type (torrent/usenet), der har samme prioritet. 1 er højeste prioritet, og 50 er laveste prioritet

### Kompatibilitet med fjernelse af download i Torrent-klient

Lidarr kan kun indstille seed-forhold/tid på klienter, der understøtter indstillingen af denne værdi via deres API, når torrenten tilføjes. Seed-mål kan indstilles globalt i klienten selv eller pr. tracker i \*Arr-indstillingerne for hver indexer. Se tabellen nedenfor for klientkompatibilitet.

|      Klient       |                                Forhold                                |                                   Tid                                    |
| :---------------: | :------------------------------------------------------------------: | :----------------------------------------------------------------------: |
|       Aria2       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|      Deluge       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
| Download Station  | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|       Flood       |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|     Hadouken      | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|    qBittorrent    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|     rTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
| Torrent Blackhole | ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical) |   ![Ikke understøttet](https://img.shields.io/badge/Understøttet-Nej-critical)   |
|   Transmission    |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   | ![Idle Limit](https://img.shields.io/badge/Understøttet-Idle%20Limit*-blue) |
|     uTorrent      |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |
|       Vuze        |   ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)   |     ![Understøttet](https://img.shields.io/badge/Understøttet-Ja-success)     |

> ![Idle Limit](https://img.shields.io/badge/Understøttet-Idle%20Limit*-blue) - Transmission har internt en kontrol af inaktiv tid, men Lidarr sammenligner den med seed-tiden, hvis inaktivitetsgrænsen er indstillet på en per-torrent-basis. Dette gøres som en løsning på Transmission's API-begrænsninger.{.is-info}

## Håndtering af fuldførte downloads

- Håndtering af fuldførte downloads er, hvordan Lidarr importerer medier fra din downloadklient til dine seriemapper.

- Aktivér (Avanceret global indstilling) - Importér automatisk fuldførte downloads fra downloadklienten
- Fjern (Indstillinger pr. klient) - Fjern fuldførte downloads, når de er færdige (usenet) eller stoppet/fuldført (torrents)
  - For torrents kræver dette, at din downloadklient sættes på pause, når seed-målene nås. Det kræver også, at seed-målene understøttes af Lidarr i henhold til tabellen ovenfor. Torrents skal også forblive i samme kategori.

### Fjern fuldførte downloads

- Lidarr vil sende en downloadanmodning til din klient og associere den med et label eller en kategorinavn, som du har konfigureret i indstillingerne for downloadklienten.
- Lidarr vil overvåge dine downloadklienters aktive downloads, der bruger det kategorinavn. Dette overvåges via din downloadklients API.
- Når downloaden er fuldført, vil Lidarr kende den endelige filplacering, som rapporteres af din downloadklient. Denne filplacering kan være næsten hvor som helst, så længe den er et separat sted fra din mediemappe.
- Lidarr vil scanne denne fuldførte filplacering for videofiler. Den vil analysere videofilens navn for at matche den med en episode. Hvis det kan gøre det, vil den omdøbe filen i henhold til dine specifikationer og flytte den til den angivne biblioteksmappe.
- Resterende filer fra downloaden vil blive sendt til papirkurven eller genbrugsbeholderen.

Hvis du downloader ved hjælp af en BitTorrent-klient, er processen lidt anderledes:

- Færdige filer efterlades på deres oprindelige placering for at give dig mulighed for at seede. Når filer importeres til din tildelte biblioteksmappe, vil Lidarr forsøge at oprette en hardlink til filen eller falde tilbage til at kopiere (bruge dobbelt plads), hvis hardlinks ikke understøttes.
- Hvis indstillingen "Fuldført downloadhåndtering - Fjern" er aktiveret i indstillingerne, vil Lidarr bede torrentklienten om at slette den oprindelige fil og torrent, men dette vil kun ske, hvis klienten rapporterer, at seeding er fuldført, torrenten er i samme kategori (dvs. ikke bruger en kategori efter import), seed-målet nås og torrenten er sat på pause (stoppet).

### Håndtering af mislykkede downloads

- Håndtering af mislykkede downloads er kun kompatibel med SABnzbd og NZBGet.
- Håndtering af mislykkede downloads gælder ikke for torrents, og der er heller ikke planer om at tilføje en sådan funktionalitet.

- Der er flere komponenter, der udgør processen for håndtering af mislykkede downloads:

- Kontroller downloader:
  - Kø - Kontroller din downloaders kø for krypterede udgivelser, der er markeret som mislykket på grund af adgangskodebeskyttelse
  - Historik - Kontroller din downloaders historik for fejl (f.eks. ikke nok blokke til reparation eller fejl ved udpakning)
- Når Lidarr finder en mislykket download, starter den behandlingen og gør følgende:
  - Tilføjer en mislykket begivenhed til Lidarrs historik
  - Fjerner den mislykkede download fra downloadklienten for at frigøre plads og rydde downloadede filer (valgfrit)
  - Begynder at søge efter en erstatningsfil (valgfrit)
  - Blokeringsliste (tidligere kendt som 'Blacklisting') tillader automatisk spring over af nzbs, når de mislykkes. Dette betyder, at nzb aldrig vil blive downloadet automatisk af Lidarr igen (du kan stadig tvinge downloaden via en manuel søgning).
  - Der er 2 avancerede indstillinger (på siden 'Downloadklient' indstillinger), der styrer adfærden for mislykket download i Lidarr, i øjeblikket er de alle aktiveret som standard.

- Genhent - Kontroller, om Lidarr skal søge efter den samme fil efter en fejl
- (Avanceret indstilling) Fjern - Om downloaden automatisk skal fjernes fra downloadklienten, når fejlen opdages

## Fjernstyring af sti-mapping

- Fjernstyring af sti-mapping fungerer som en simpel søgning efter fjernsti og erstatning med lokal sti. Dette bruges primært til enten sammensmeltede lokale/fjernopsætninger ved hjælp af mergerfs eller lignende eller bruges, når applikationen og downloadklienten ikke er på samme server.
- En fjern sti-mapping bruges, når din downloadklient rapporterer en sti for fuldførte data enten på en anden server eller på en måde, som \*Arr ikke adresserer den mappe.
- Generelt er en fjern sti-mapping kun nødvendig, hvis din downloadklient er på Linux, når \*Arr er på Windows eller omvendt. En fjern sti-mapping kan også være nødvendig, hvis du blander Docker og Native klienter eller hvis du bruger en fjernserver.
- En fjern sti-mapping er en DUM søgning/erstatning (hvor den finder den FJERNEDE værdi, erstatter den med den LOKALE værdi for den angivne vært).
- Hvis fejlmeddelelsen om en dårlig sti ikke indeholder den ERSTATTEDE værdi, fungerer sti-mappingen ikke, som du forventer. Den typiske løsning er at tilføje og fjerne mappingen.
- [Se TRaSH's vejledning for yderligere oplysninger om fjern sti-mapping](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)

> Hvis både \*Arr og din Download Client er Docker-containere, er det sjældent nødvendigt med en fjernsti-kortlægning. Det anbefales, at du [gennemgår Docker-guiden](/docker-guide) og/eller [følger TRaSH's vejledning](https://trash-guides.info/hardlinks)
{.is-info}

# Importlister

> Information om understøttede listetyper findes på siden [Mere info (Understøttet)](/lidarr/supported#lists) for dette afsnit
{.is-info}

Importlister giver dig mulighed for at tilføje elementer til Lidarr fra Spotify eller Last.fm. Dette har potentialet til at tilføje mange uventede elementer til din Lidarr-database, så brug det med forsigtighed.

<!-- ![importlists.png](/assets/readarr/importlists.png) -->

## Importlister

Dette viser de lister, du i øjeblikket har, og giver dig mulighed for at tilføje nye lister. Tilføjelse af lister dækkes mere detaljeret nedenfor.

## Importliste-undtagelser

Alt på denne liste er blevet udelukket fra at blive tilføjet af lister og vil aldrig blive tilføjet fra nogen liste. Du kan fjerne elementer fra listen ved at klikke på dem.

## Tilføjelse af en importliste

Efter at have klikket på <kb>+</kb>, skal du vælge hvilken type liste, du gerne vil tilføje:

<!-- ![addlist.png](/assets/readarr/addlist.png) -->

I dette tilfælde vil vi tilføje en Spotify Gemte albums-liste.

<!-- ![bookshelflist.png](/assets/readarr/bookshelflist.png) -->

- Navn - Indtast et navn til denne liste.
- Aktivér automatisk tilføjelse - Hvis aktiveret, tilføjes alt på listen automatisk til Lidarr.

> Dette vil tilføje ALLE ALBUMS fra den kunstner til Lidarr!

- Overvågning - Vælg dit overvågningsniveau for tilføjede elementer. Gyldige muligheder er `Ingen`, `Specifikt album` og `Alle kunstneralbums`. Alle albums tilføjes til Lidarr, men overvåges eller overvåges ikke baseret på dette valg.
- Rodmappe - Vælg rodmappe for kunstnere, der tilføjes fra denne liste.
- Overvåg nye albums - Vælg, hvad Lidarr skal gøre med fremtidige albums fra den tilføjede kunstner. Gyldige muligheder er `Alle albums`, `Ingen`, `Nye`.
- Kvalitetsprofil - Vælg din kvalitetsprofil for kunstnere, der tilføjes fra denne liste.
- Metadataprofil - Vælg din metadataprofil for kunstnere, der tilføjes fra denne liste.
- Lidarr-tags - Vælg hvilke tags der gælder for kunstnere, der tilføjes fra denne liste.

> Det anbefales kraftigt, at du tilføjer et beskrivende tag her. Ellers vil du ikke vide, hvilken liste der har tilføjet disse elementer til Lidarr, og når de er tilføjet, kan du aldrig få denne information igen! Denne information logges ikke!

Lister synkroniseres som standard hver 24. time, men kan også udløses manuelt fra siden `System` => `Opgaver`. Du kan ikke automatisere denne proces hurtigere end det.

# Forbindelser

> Information om understøttede forbindelsestyper findes på siden [Mere info (Understøttet)](/lidarr/supported#notifications) for dette afsnit
{.is-info}

# Tags

- Tag-sektionen i Lidarr bruges til at linke forskellige aspekter af Lidarr.
- Tags er særligt nyttige til:

  - Forsinkelsesprofiler
  - Udgivelsesprofiler
  - Indekser

- Tags kan bruges til at linke Forsinkelsesprofiler, Udgivelsesprofiler, Indekser og Kunstnere/Albums sammen.
- For eksempel:
  - Du vil have en bestemt kunstner/album til kun at bruge en bestemt indekser. Du ville oprette en tag og tildele kunstner/albummet og indekseren den tag.
  - Du vil have en bestemt Udgivelsesprofil til kun at bruge en bestemt Forsinkelsesprofil. Du ville oprette en tag og tildele Udgivelsesprofilen og Forsinkelsesprofilen den tag.

> Bemærk: Tags påvirker ikke nogen "Kvalitetsprofiler", "Metadataprofiler" eller andre aspekter, der ikke er nævnt ovenfor.
{.is-info}

# Generelt

## Opdateringer

- (Avanceret indstilling) Gren - Dette er grenen af Lidarr, som du kører på.
  - [Se venligst denne FAQ-indgang for mere information](/lidarr/faq#how-do-i-update-lidarr)
- Automatisk - Hent og installer opdateringer automatisk. Du vil stadig kunne installere fra System: Opdateringer. Bemærk: Windows-brugere opdateres altid automatisk.
- Mekanisme - Brug Lidarr's indbyggede opdateringsværktøj eller et script
  - Indbygget - Brug Lidarr's eget opdateringsværktøj
  - Script - Få Lidarr til at køre opdateringsscriptet
  - Docker - Opdater ikke Lidarr indefra Docker, i stedet træk en helt ny image med den nye opdatering
- Script - Synlig kun når mekanismen er indstillet til Script - Sti til opdateringsscript
- Opdateringsproces - Lidarr vil downloade opdateringsfilen, verificere dens integritet og udpakke den til en midlertidig placering og kalde den valgte metode. Opdateringsprocessen køres under samme bruger som Lidarr kører under, den skal have tilladelser til at opdatere Lidarr-filerne samt stoppe/starte Lidarr.
- Indbygget - Den indbyggede metode vil tage en sikkerhedskopi af Lidarr-filer og -indstillinger, stoppe Lidarr, opdatere installationen og starte Lidarr igen. Hvis dit system ikke kan håndtere at stoppe Lidarr og vil forsøge at genstarte det automatisk, kan det være bedst at bruge et script i stedet. Hvis opdateringen mislykkes, vil den tidligere version af Lidarr blive genstartet.
- Script - Scriptet skal håndtere det samme som det indbyggede opdateringsværktøj. Hvis du skal håndtere stop og start af tjenester (upstart/launchd/etc), skal du gøre det her.