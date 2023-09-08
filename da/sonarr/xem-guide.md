---
title: TheXEM Moderation Guide
description: Guide til hvordan man mapper forskellige scenarier i XEM for optimal brug med Sonarr og anden PVR-software.
published: true
date: 2021-11-24T19:26:31.972Z
tags: sonarr, xem
editor: markdown
dateCreated: 2021-10-03T16:48:28.241Z
---

# Indholdsfortegnelse

- [Indholdsfortegnelse](#indholdsfortegnelse)
- [TheXEM Moderation Guide](#thexem-moderation-guide)
- [Navngivning](#navngivning)
- [De forskellige enhedstyper](#de-forskellige-enhedstyper)
- [Mappetyper](#mappetyper)
  - [!SxxExx-mapping SxxExx-mapping](#sxxexx-mapping)
  - [!Absolut mapping Absolut mapping](#absolut-mapping)
  - [!Fuldt mapping Fuldt mapping](#fuldt-mapping)
  - [!Direkte mapping Direkte mapping](#direkte-mapping)
- [Eksempler](#eksempler)
  - [Basal anime-mapping](#basal-anime-mapping)
  - [Kompleks anime-mapping](#kompleks-anime-mapping)
  - [Korte vestlige tegnefilmsserier](#korte-vestlige-tegnefilmsserier)
  - [Kompleks individuel mapping](#kompleks-individuel-mapping)
- [Begrænsninger](#begrænsninger)
  - [Der kan kun være én scene-nummereringsskema pr. serie](#der-kan-kun-være-én-scene-nummereringsskema-pr-serie)
  - [Der kan kun være én master-enhed](#der-kan-kun-være-én-master-enhed)
  - [Sletning af master-kolonnen eller individuelle sæsoner i den](#sletning-af-master-kolonnen-eller-individuelle-sæsoner-i-den)
  - [Nogle ting kan bare ikke mappes](#nogle-ting-kan-bare-ikke-mappes)
- [Brug for hjælp?](#brug-for-hjælp)

# TheXEM Moderation Guide

[TheXEM](https://thexem.info) er en service, der gør det muligt at oprette forbindelser mellem andre tjenester/enheder, der bruger forskellige nummerering og navngivningsskemaer til udgivelser af tv-serier. Sonarr bruger TVDB som en datakilde til sine episodeoplysninger, og nogle gange bruger scene og andre udgivelsesgrupper en anden navngivnings- eller nummereringsskema. Med den rette mapping er det muligt at sikre, at episode 1 i sæson 1 ifølge TVDB matcher episode 5 i sæson 1 ifølge scenens nummerering, så Sonarr kan downloade den korrekte episode, selvom nummereringen er forskellig.

Denne guide er til personer med en konto på TheXEM og vil guide dig gennem nogle af de mere almindelige mønstre, som du måske ønsker at bruge. Men først vil vi guide dig gennem nogle af grundlæggende ting.

# Navngivning

Som en konvention bruger vi det samme navn, som TVDB bruger til selve tv-serien. Dette er særligt interessant for internationale shows som anime og betyder i bund og grund, at vi bruger det officielt licenserede engelske navn på showet.

Derudover er det muligt at indtaste forskellige aliaser for seriens navn, hvilket primært bruges til anime, men lejlighedsvis også er nyttigt for "almindelig" tv.

# De forskellige enhedstyper

TheXEM har fire forskellige datakilder eller enhedstyper, som den i øjeblikket understøtter og kan forbinde med hinanden efter behov. Disse fire typer er:

- Scene
- [TVDB](https://thetvdb.com)
- [AniDB](https://anidb.net)
- Master

En korrekt XEM-mapping for en bestemt serie skal *mindst* have en indtastning i scene-kolonnen og en indtastning i TVDB-kolonnen med den relevante mappetype (se afsnittet kaldet *Mappetyper* nedenfor) mellem dem.

> Serier, der ikke har mindst en scene-kolonne og en TVDB-kolonne, er ubrugelige og vil potentielt blive fjernet. Det samme gælder for serier, hvor der ikke er nogen direkte eller indirekte forbindelse mellem scene-kolonnen og TVDB-kolonnen.
{.is-warning}

# Mappetyper

TheXEM har tre forskellige automatiske muligheder for at forbinde forskellige enheder med hinanden: SxxExx-mapping, absolut mapping og kombinationen af begge, fuldt mapping. Derudover kan du også direkte mappe episoder på hinanden ved hjælp af direkte mapping. Hver af disse har sin egen anvendelse og er nyttig i specifikke situationer.

## ![SxxExx-mapping](/assets/sonarr/xem-guide/mapping-sxxexx.svg) SxxExx-mapping

Denne type mapping fastlægger, at mellem de to enheder, den forbinder, er sæson- og episodenumrene ens, hvilket betyder, at S01E01 er den samme episode i begge enhedstyper. Den absolutte nummerering er dog ikke nødvendigvis den samme.

## ![Absolut mapping](/assets/sonarr/xem-guide/mapping-abs.svg) Absolut mapping

Bortset fra nogle få meget specifikke tilfælde er absolut mapping næsten udelukkende nyttigt for anime-serier. Anime-navngivningsskemaet, som de fleste udgivelsesgrupper bruger, bruger bare et stigende episodenummer i stedet for SxxExx-nummerering, hvilket vi kalder absolut nummerering. Hvis du markerer mappingen mellem to enheder som "absolut", fortæller det tjenester, der bruger disse data, at SxxExx-nummereringen kan være forskellig eller ikke, men den absolutte nummerering er i det mindste den samme.

## ![Fuldt mapping](/assets/sonarr/xem-guide/mapping-full.svg) Fuldt mapping

Fuldt mapping fortæller enhver tjeneste, der bruger TheXEM, at både den absolutte nummerering og SxxExx-mappingen er den samme mellem de to enheder, den forbinder, hvilket betyder, at nummereringen er den samme mellem begge enheder.

> Dette betyder, at hvis alt, hvad du vil tilføje til din mapping, er en scene-kolonne og en TVDB-kolonne med fuldt mapping mellem dem, er din seriens indtastning overflødig, da dette fungerer som standard uden en indtastning på TheXEM.
{.is-info}

## ![Direkte mapping](/assets/sonarr/xem-guide/mapping-direct.svg) Direkte mapping

Direkte mapping er kun muligt mellem Master-enhedstypen og enhederne på hver side af den. Du bør bruge det så sparsomt som muligt, fordi når du begynder at bruge direkte forbindelser, skal du blive ved med at bruge dem i resten af sæsonen og i nogle tilfælde i resten af hele showet.

Du kan aktivere direkte mapping ved at klikke på ikonet over den automatiske mappingstype. Du vil se, at brugergrænsefladen på siden ændrer sig lidt for at give plads til de forbindelser, du er ved at tegne. For at forbinde en episode til en anden episode skal du blot klikke på en episode på venstre side af forbindelsen og derefter klikke på den tilsvarende episode på højre side. Hvis du har gjort det godt, vil webstedet bede dig om at bekræfte forbindelsen.

> Det er muligt at linke en enkelt episode på den ene side til flere episoder på den anden side, f.eks. hvis TVDB betragter to episoder som separate episoder, mens scenen kombinerer dem til ét nummer. Dette er særligt interessant for vestlige tegnefilm.
{.is-info}

# Eksempler

Det ovenstående er meget at tage ind, men alt i alt er der kun en håndfuld anvendelsestilfælde, der dækker langt størstedelen af alle shows, som du nogensinde får brug for at tilføje til TheXEM. Følgende er nogle meget almindelige typer af mapping.

## Basal anime-mapping

Når du mapper en anime-serie, bruger vi altid AniDB-kolonnen. Hvis det er muligt med den mapping, du forsøger at opnå, bør du *altid* sigte mod at bruge fuldt mapping mellem scene-kolonnen og AniDB-kolonnen.

De fleste anime-serier kan direkte mappes mellem scene-kolonnen gennem AniDB og endelig til TVDB. Et simpelt eksempel ville være showet [Ronia the Robber's Daughter](https://thexem.info/xem/show/1603). Det har brug for mapping i første omgang, fordi det japanske navn, som udgivelsesgrupper bruger, ikke matcher det engelske navn, som TVDB bruger, men ellers er mappingen simpel: nummereringen er identisk mellem scene og AniDB, så vi bruger fuldt mapping mellem dem, mens det eneste, vi ved med sikkerhed mellem AniDB og TVDB, er, at SxxExx-nummereringen er identisk.

> AniDB nulstiller den absolutte nummerering mellem hver sæson, fordi den betragter hver sæson som sit eget show. Når du tilføjer en ny AniDB-sæson, skal du sørge for at indtaste dens ID-nummer og indstille feltet "Ab. Start" for den nye sæson til 1.
{.is-info}

For et eksempel på en anime-serie med flere sæsoner, kan du se på [Assassination Classroom](https://thexem.info/xem/show/2817). Bemærk de separate aliaser for den anden sæson, som hjælper Sonarr med at finde ud af, at `[Udgivelsesgruppe] Ansatsu Kyoushitsu - 01 (1080p)` svarer til S01E01 i TVDB, mens `[Udgivelsesgruppe] Ansatsu Kyoushitsu S2 - 01 (1080p)` svarer til S02E01.

## Kompleks anime-mapping

Nogle gange stemmer TVDB's opfattelse af en sæson ikke overens med det, AniDB kalder en sæson. Dette sker især, når en anime udgives som en såkaldt *split-cour*. Dette viser sig som en række episoder, efterfulgt af en kort pause, hvorefter næste sæt episoder også sendes. Split-cour anime har typisk en eller højst to anime-sæsoner mellem sig, og TVDB betragter mest en anime split-cour, når det andet sæt episoder annonceres i løbet af den første parts sendetid.

Et eksempel på, hvordan dette kan se ud, er [That Time I Got Reincarnated as a Slime](https://thexem.info/xem/show/5241). Bemærk, hvordan det, TVDB kalder sæson 2, faktisk er opdelt i sæson 2 og 3, så vidt AniDB er bekymret. Vi bruger et link til Master-enheden her for at gøre mappingen mindre kompleks. I bund og grund kombinerer Master-indtastningen den absolutte nummerering, som bruges på TVDB, med SxxExx-nummereringen, som AniDB bruger. Derefter linker vi Master-kolonnen til TVDB ved hjælp af absolut mapping og til AniDB-kolonnen ved hjælp af SxxExx-mapping. Scene-kolonnen kan linkes ved hjælp af fuldt mapping som sædvanligt.

## Korte vestlige tegnefilmsserier

Børnetegnefilm giver ofte en udfordring, når episoderne skal mappes, fordi hvis en 30-minutters episode er opdelt i to separate historier, betragter TVDB dem som to forskellige episoder, mens scenen generelt betragter dem som en enkelt episode. Dette betyder, at vi har brug for meget detaljeret direkte mapping mellem individuelle episoder.

Et eksempel på dette er showet [Paw Patrol](https://thexem.info/xem/show/4814). Når du holder musen over episoderne i Master-kolonnen, vil du se, at en enkelt episode på scenens side er linket til en eller to episoder på TVDB-siden. Denne særlige type mapping kræver konstant input, da nye episoder af serien sendes.

> Husk på, at det kan give mening at mappe en episode på den ene side til flere episoder på den anden side, men at mappe flere episoder på den ene side til flere episoder på den anden side ikke giver mening. Softwaren vil tillade dig at gøre det, men lad være med det, da Sonarr ikke vil kunne gøre noget med det.
{.is-warning}

## Kompleks individuel mapping

I nogle (heldigvis meget sjældne!) tilfælde kan mapping af episoder på hinanden blive meget kompleks. TVDB betragter sendetidspunkterne for showets hovednetværk som førende, når det kommer til at bestemme episodernes rækkefølge. Det kan gøre tingene virkelig komplekse i tilfælde som Firefly eller [Transporter](https://thexem.info/xem/show/1653), der blev sendt af deres oprindelige netværk i en rækkefølge, der bryder den kronologiske rækkefølge. Scenen vil ofte kompensere for dette ved at bruge den kronologiske episoderækkefølge, hvilket resulterer i behov for kompleks individuel mapping for hver episode.

Bemærk, hvordan der ikke er nogen automatisk mapping mellem Master-kolonnen og Scene-kolonnen med Transporter; al mapping opnås ved direkte links mellem episoder.

# Begrænsninger

TheXEM har i øjeblikket nogle få begrænsninger, som vi vil forsøge at dække her.

## Der kan kun være én scene-nummereringsskema pr. serie

Hvis flere udgivelsesgrupper bruger forskellige nummereringsskemaer, komplicerer dette tingene. Der er derfor nogle retningslinjer i tilfælde af uenige kilder.

1. Scene-udgivelsernes nummerering har altid prioritet over P2P-udgivelsernes nummerering.
2. Hvis der ikke findes scene-udgivelser for en bestemt serie, skal du vælge den, der virker mest populær. Dette vil normalt komme ned til hvilken gruppe, der har tendens til at udgive episoderne hurtigst i ordentlig kvalitet.
3. I tilfælde af anime følger vi nummereringen fra SubsPlease/Erai-Raws, hvis det er tilgængeligt. Hvis ikke, gælder den tidligere retningslinje også her.

## Der kan kun være én master-enhed

Du vil bruge Master-enhedstypen i nogle relativt sjældne tilfælde for at oprette direkte forbindelser *eller* for at undgå at skulle oprette direkte forbindelser. Du kan dog kun bruge en af disse master-enheder til at forbinde to andre enheder. Fordi det endelige mål er at sikre, at mapping fungerer for hovedanvendelsestilfældet med at forbinde TVDB til scenen, skal du sørge for, at mindst *den* mapping fungerer, og hvis det kræver en master-enhed, er det der, du skal prioritere at bruge den.

## Sletning af master-kolonnen eller individuelle sæsoner i den

Når du sletter Master-kolonnen af en eller anden grund, skal du sørge for, at der ikke er direkte mapping på individuelle episoder i den. Hvis du sletter sæsonen, mens mappingen stadig er der, **vil mappingen være usynlig i brugergrænsefladen, men vil stadig eksistere!** Hvis du gør dette ved et uheld, skal du blot tilføje sæsonen, du fjernede, fortryde de individuelle links og derefter slette sæsonen igen.

## Nogle ting kan bare ikke mappes

En af de ting, du altid skal huske på, er, at nogle gange er en serie så rodet eller på anden måde kompleks, at den ikke kan mappes i TheXEM. Nogle gange vil du være i stand til at mappe en af brugstilfældene, nogle gange ikke engang det. I disse tilfælde kan der ofte ikke rigtig gøres noget ved det.

# Brug for hjælp?

Endelig, hvis du har brug for hjælp til noget, eller hvis du simpelthen ikke har en konto på TheXEM, skal du være velkommen til at deltage i Sonarr's Discord-server i [#xem-kanalen](https://discord.gg/QzDaBmN2J3). Vi vil være glade for at hjælpe. Vær dog opmærksom på, at svartiderne kan være langsomme og meget afhængige af tidszoneforskellen.