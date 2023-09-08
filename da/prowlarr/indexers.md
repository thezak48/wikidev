---
title: Prowlarr Indexers
description: 
published: true
date: 2023-03-30T14:04:26.292Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

Denne side beskriver, hvordan du tilføjer og konfigurerer indexere i Prowlarr.

# Tilføjelse af en Indexer

For at tilføje en indexer skal du først klikke på `Indexers` i venstre side og derefter klikke på <kb>+</kb> `Tilføj Indexer` øverst på siden.

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

Vælg din indexer fra listen eller skriv et delvist navn i feltet for at finde din indexer. Hvis din indexer ikke er på listen, kan du muligvis bruge "Generic Newznab" (til Usenet) eller "Generic Torznab" (til torrents). Ellers besøg vores [Indexer Request site](https://requests.prowlarr.com/).

> Brug af `Generic Newznab` eller `Generic Torznab` forudsætter, at din indexer understøtter standardiserede *znab-formater. Hvis den ikke gør det, vil dette ikke virke.
{.is-info}

> Bemærk: næsten alle Usenet-sider er kompatible med Generic Newznab.
{.is-warning}

> Hvis din tracker eller indexer ikke er på listen og ikke er på vores [supported indexers](/prowlarr/supported-indexers) side, kan du anmode om at få den tilføjet via vores [Indexer Requests Site](https://requests.prowlarr.com)
{.is-info}

# Redigering af en Indexer

For at redigere en indexer skal du først klikke på `Indexers` i venstre side og derefter klikke på skruenøgleikonet helt til højre for den indexer, du ønsker at redigere.

# Visning af en Indexer Id eller URL

For at se detaljer om en indexer skal du først klikke på `Indexers` i venstre side og derefter klikke på Indexer Linket i kolonnen Indexer Name. (Tidligere ikonet (i) til højre)

Tilgængelige detaljer kan omfatte:

- Id i Prowlarr
- Beskrivelse
- Kodning
- Sprog
- Site
- Newznab/Torznab Prowlarr URL
- Site Kapaciteter

# Indexer Indstillinger

Når du har valgt din indexer, vil der være en pop-up med yderligere information, som du skal konfigurere. Bemærk, at de specifikke indstillinger vil ændre sig lidt for hver indexer baseret på deres påkrævede felter og den type indexer, du konfigurerer.

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Navn - Vælg et navn til denne indexer. Når den synkroniseres med dine apps, vil den tilføje `(Prowlarr)` efter det.
- Aktiver - Markér afkrydsningsfeltet for at aktivere denne indexer.
- Omdirigering - Markér afkrydsningsfeltet, hvis der er behov for en omdirigering. Der er kun et par indexere, hvor dette er nødvendigt for at undgå at blive blokeret. Hvis det er aktiveret, vil det sende grab-linket direkte til applikationen i stedet for at proxy det via Prowlarr.

> Omdirigering er normalt kun nødvendig for et par meget specifikke indexere.
{.is-info}

- Synkroniseringsprofil - Vælg din synkroniseringsprofil her. Disse kan oprettes i [`Indstillinger` => `Apps`](/prowlarr/settings#applications). Standardprofilen findes allerede og ser sådan ud:

> Du kan have forskellige indstillinger pr. app ved at oprette flere instanser af indexeret
{.is-info}

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- URL - Vælg den URL, som Prowlarr skal bruge. Hvis den er tom, bruges standard-/første-url'en.
- Download Link - Hvis du tilføjer en torrent indexer, skal du muligvis vælge, hvilken slags download-link du vil bruge.
- (Avanceret indstilling) API-sti - Sti til indexerens API. Typisk `/api`
- Legitimationsoplysninger - Mange indexere og trackere kræver, at du godkender/logge ind på en eller anden måde. Du skal muligvis indtaste en API-nøgle, en RSS-nøgle, en sessions-id, en cookie eller andre legitimationsoplysninger fra din indexer (som normalt findes på din profilside eller under sikkerhed), vælge søgeordrer eller andre indstillinger for din specifikke indexer.
  - API-nøgle
  - RSS-nøgle
  - Sessions-id
  - Cookie
  - Brugernavn/adgangskode
  - osv.
- (Avanceret indstilling) Yderligere parametre - Yderligere parametre, der skal tilføjes til anmodningerne for denne indexer.
- VIP Udløb - Indtast datoen i ISO-format (yyyy-MM-DD) for at få besked 1 uge før udløbet; ellers lad det være tomt
- Tags - Brug tags til at angive standard-downloadklienter, angive Indexer Proxies, angive indexere til applikationer eller bare for at organisere dine indexere.
- (Avanceret indstilling) Forespørgselsbegrænsning - Hvis din indexer begrænser dine API-anmodninger pr. dag, kan du indtaste det antal her for at undgå at overskride grænsen.
- (Avanceret indstilling) Grab-begrænsning - Hvis din indexer begrænser dine Grabs pr. dag, kan du indtaste det antal her for at undgå at overskride grænsen. Når grab-begrænsningen er nået, vil yderligere forespørgsler udløse en ukontrolleret undtagelse i \*Arr Apps. Andre apps kan variere.
- (Avanceret indstilling) Seed Ratio - Kun for Torrent Indexers: Den ratio, som en torrent skal nå, før den stopper, tom er appens standard
- (Avanceret indstilling) Seed Time - Kun for Torrent Indexers: Den tid, som en torrent skal seedes, før den stopper, tom er appens standard. Værdierne er i minutter.
- (Avanceret indstilling) Indexer Prioritet - Prioritet for denne indexer for at foretrække en indexer frem for en anden i release tiebreaker-scenarier. 1 er højeste prioritet, og 50 er laveste prioritet. Disse prioriteter synkroniseres med \*Arr-apps.

- Test din indexer, og hvis der vises et grønt flueben, er du klar til at gemme den. Når du gemmer den, afhængigt af dine synkroniseringsindstillinger, vil den automatisk blive tilføjet til dine apps.

## Tilføjelse af en brugerdefineret YML-definition

- Bemærk, at yml-definitionen er cached i en kort periode, og hvis du foretager ændringer af udviklingsmæssige årsager, skal du vente på cachen eller genstarte Prowlarr.
- Hvis du ønsker at tilføje en brugerdefineret Cardigann-kompatibel YML-definition til en indexer, der ikke understøttes, eller for at teste ændringer i en eksisterende definition:
  - Gå til (eller opret) mappen Custom Indexer Definition med navnet `Custom` inden for mappen `Definitions` i [Prowlarr's App Data folder](/prowlarr/appdata-directory)
    - Eksempelstier:
      - Windows: `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux: `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX: `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - Gem [Cardigann-kompatibel YML-filen](/prowlarr/cardigann-yml-definition) i mappen og sørg for, at Prowlarr har tilladelse til at få adgang til den.

> Filnavnet og id'en i definitionen skal være unik og må ikke konflikte med andre eksisterende definitioner. Det anbefales kraftigt, at navnet i definitionen også er unikt.
{.is-info}

# Understøttede Indexere

- [Se denne wiki-side for en liste over understøttede indexere fra den seneste nightly.](/prowlarr/supported-indexers/)