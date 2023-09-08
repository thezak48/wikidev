---
title: TheXEM Moderation Guide
description: Guide for hvordan du mapper ulike scenarier i XEM for optimal bruk med Sonarr og annen PVR-programvare.
published: true
date: 2021-11-24T19:26:31.972Z
tags: sonarr, xem
editor: markdown
dateCreated: 2021-10-03T16:48:28.241Z
---

# Innholdsfortegnelse

- [Innholdsfortegnelse](#innholdsfortegnelse)
- [TheXEM Moderation Guide](#thexem-moderation-guide)
- [Navngiving](#navngiving)
- [De forskjellige enhetstypene](#de-forskjellige-enhetstypene)
- [Mappetyper](#mappetyper)
  - [!SxxExx-mapping SxxExx-mapping](#-sxxexx-mapping)
  - [!Absolutt mapping Absolutt mapping](#-absolutt-mapping)
  - [!Fullstendig mapping Fullstendig mapping](#-fullstendig-mapping)
  - [!Direkte mapping Direkte mapping](#-direkte-mapping)
- [Eksempler](#eksempler)
  - [Grunnleggende anime-mapping](#grunnleggende-anime-mapping)
  - [Kompleks anime-mapping](#kompleks-anime-mapping)
  - [Korte vestlige tegneserieprogrammer](#korte-vestlige-tegneserieprogrammer)
  - [Kompleks individuell mapping](#kompleks-individuell-mapping)
- [Begrensninger](#begrensninger)
  - [Bare én nummereringsordning per serie støttes](#bare-én-nummereringsordning-per-serie-støttes)
  - [Bare én hovedenhet støttes](#bare-én-hovedenhet-støttes)
  - [Sletting av hovedkolonnen eller individuelle sesonger i den](#sletting-av-hovedkolonnen-eller-individuelle-sesonger-i-den)
  - [Noen ting kan bare ikke bli kartlagt](#noen-ting-kan-bare-ikke-bli-kartlagt)
- [Trenger du hjelp?](#trenger-du-hjelp)

# TheXEM Moderation Guide

[TheXEM](https://thexem.info) er en tjeneste som gjør det mulig å opprette forbindelser mellom andre tjenester/enheter som bruker forskjellige nummererings- og navngivningssystemer for TV-serieutgivelser. Sonarr bruker TVDB som en datakilde for episodeinformasjonen sin, og noen ganger bruker scene og andre utgivelsesgrupper en annen navngivnings- eller nummereringsordning. Med riktig kartlegging er det mulig å sikre at episode 1 i sesong 1 ifølge TVDB samsvarer med episode 5 i sesong 1 ifølge scenens nummerering, slik at Sonarr kan laste ned riktig episode til tross for at nummereringen er forskjellig.

Denne veiledningen er for personer med en konto på TheXEM og vil guide deg gjennom noen av de vanligste mønstrene du kan bruke. Men først vil vi gå gjennom noen grunnleggende ting.

# Navngiving

Som en konvensjon bruker vi samme navn som TVDB bruker for selve serien. Dette er spesielt interessant for internasjonale serier som anime og kommer i praksis ned til at vi bruker det offisielt lisensierte engelske navnet på serien.

Det er også mulig å legge inn forskjellige aliaser for seriens navn, noe som hovedsakelig brukes for anime, men av og til også er nyttig for "vanlig" TV.

# De forskjellige enhetstypene

TheXEM har fire forskjellige datakilder eller enhetstyper som den for øyeblikket støtter og kan koble sammen etter behov. Disse fire typene er:

- Scene
- [TVDB](https://thetvdb.com)
- [AniDB](https://anidb.net)
- Master

En riktig XEM-kartlegging for en bestemt serie bør *minst* ha en oppføring i scenekolonnen og en oppføring i TVDB-kolonnen med den aktuelle mappetypen (se avsnittet kalt *Mappetyper* nedenfor) mellom dem.

> Serier som ikke har minst en scenekolonne og en TVDB-kolonne er ubrukelige og vil potensielt bli fjernet. Det samme gjelder for serier der det ikke er noen direkte eller indirekte forbindelse mellom scenekolonnen og TVDB-kolonnen.
{.is-warning}

# Mappetyper

TheXEM har tre forskjellige automatiske alternativer for å koble forskjellige enheter sammen: SxxExx-mapping, absolutt mapping og kombinasjonen av begge, fullstendig mapping. I tillegg kan du også direkte mappe episoder på hverandre ved hjelp av direkte mapping. Hver av disse har sin egen bruk og er nyttig i bestemte situasjoner.

## ![SxxExx-mapping](/assets/sonarr/xem-guide/mapping-sxxexx.svg) SxxExx-mapping

Denne typen kartlegging fastslår at mellom de to enhetene den kobler sammen, er sesong- og episodenumrene like, noe som betyr at S01E01 er den samme episoden i begge enhetstypene. Den absolutte nummereringen er imidlertid ikke nødvendigvis den samme.

## ![Absolutt mapping](/assets/sonarr/xem-guide/mapping-abs.svg) Absolutt mapping

Bortsett fra noen få svært spesifikke tilfeller er absolutt mapping nesten utelukkende nyttig for animeserier. Navngivningssystemet for anime som brukes av de fleste utgivelsesgrupper bruker bare et økende episodenummer i stedet for SxxExx-nummerering, som vi kaller absolutt nummerering. Å merke kartleggingen mellom to enheter som "absolutt" forteller tjenester som bruker disse dataene at SxxExx-nummereringen kan være forskjellig eller ikke, men den absolutte nummereringen er i det minste den samme.

## ![Fullstendig mapping](/assets/sonarr/xem-guide/mapping-full.svg) Fullstendig mapping

Fullstendig mapping forteller enhver tjeneste som bruker TheXEM at både den absolutte nummereringen og SxxExx-mappingen er den samme mellom de to enhetene den kobler sammen, noe som betyr at nummereringen er den samme mellom begge enheter.

> Dette betyr at hvis alt du vil legge til i kartleggingen din er en scenekolonne og en TVDB-kolonne med fullstendig mapping mellom dem, er oppføringen for serien din unødvendig, da dette fungerer som standard uten en oppføring på TheXEM.
{.is-info}

## ![Direkte mapping](/assets/sonarr/xem-guide/mapping-direct.svg) Direkte mapping

Direkte mapping er bare mulig mellom hovedenheten og enhetene på hver side av den. Du bør bruke det så sparsomt som mulig, fordi når du begynner å bruke direkte forbindelser, må du fortsette å bruke dem for resten av sesongen og i noen tilfeller for resten av hele serien.

Du kan aktivere direkte mapping ved å klikke på ikonet over den automatiske mappetypen. Du vil se at brukergrensesnittet på siden endrer seg litt for å gi plass til forbindelsene du skal tegne. For å koble en episode til en annen episode, klikker du bare på en episode på venstre side av forbindelsen, etterfulgt av å klikke på den tilsvarende episoden på høyre side. Hvis du gjorde det riktig, vil nettstedet be deg om å bekrefte forbindelsen.

> Det er mulig å koble en enkelt episode på den ene siden til flere episoder på den andre siden, for eksempel hvis TVDB betrakter to episoder som separate episoder mens scenen kombinerer dem til ett nummer. Dette er spesielt interessant for vestlige tegneserier.
{.is-info}

# Eksempler

Det ovennevnte er mye å ta inn, men alt i alt er det bare noen få bruksområder som dekker flertallet av alle serier du noensinne vil trenge å legge til i TheXEM. Følgende er noen svært vanlige typer kartlegging.

## Grunnleggende anime-mapping

Når du mapper en animeserie, bruker vi alltid AniDB-kolonnen. Hvis det er tillatt i kartleggingen du prøver å oppnå, bør du *alltid* prøve å bruke fullstendig mapping mellom scenekolonnen og AniDB-kolonnen.

De fleste animeserier kan direkte mappe mellom scenekolonnen gjennom AniDB og til slutt til TVDB. Et enkelt eksempel er serien [Ronia the Robber's Daughter](https://thexem.info/xem/show/1603). Den trenger kartlegging i utgangspunktet fordi det japanske navnet som brukes av utgivelsesgruppene, ikke samsvarer med det engelske navnet som brukes av TVDB, men ellers er kartleggingen enkel: nummereringen er identisk mellom scenen og AniDB, så vi bruker fullstendig mapping mellom dem, mens det eneste vi vet sikkert mellom AniDB og TVDB er at SxxExx-nummereringen er identisk.

> AniDB nullstiller den absolutte nummereringen mellom hver sesong fordi den betrakter hver sesong som sin egen serie. Når du legger til en ny AniDB-sesong, må du sørge for at du legger inn ID-nummeret for den nye sesongen og at du setter feltet "Ab. Start" for den nye sesongen til 1.
{.is-info}

For et eksempel på en animeserie med flere sesonger, kan du se på [Assassination Classroom](https://thexem.info/xem/show/2817). Legg merke til de separate aliasene for den andre sesongen, som hjelper Sonarr med å forstå at `[Utgivelsesgruppe] Ansatsu Kyoushitsu - 01 (1080p)` tilsvarer S01E01 i TVDB, mens `[Utgivelsesgruppe] Ansatsu Kyoushitsu S2 - 01 (1080p)` tilsvarer S02E01.

## Kompleks anime-mapping

Noen ganger samsvarer ikke TVDBs konsept om en sesong med det AniDB kaller en sesong. Dette skjer spesielt når en anime blir utgitt som en såkalt *split-cour*. Dette viser seg som en gruppe episoder, etterfulgt av en kort pause deretter sendes neste gruppe episoder. Split-cour anime har vanligvis én eller maksimalt to animesesonger mellom seg, og TVDB betrakter vanligvis en anime som split-cour når den andre gruppen med episoder blir kunngjort under den første delens sendetid.

Et eksempel på hvordan dette kan se ut er [That Time I Got Reincarnated as a Slime](https://thexem.info/xem/show/5241). Legg merke til hvordan det TVDB kaller sesong 2 faktisk er delt opp i sesong 2 og 3 så langt AniDB er bekymret. Vi bruker en kobling til hovedenheten her for å gjøre kartleggingen mindre kompleks. I utgangspunktet kombinerer hovedoppføringen den absolutte nummereringen som brukes på TVDB med SxxExx-nummereringen som AniDB bruker. Deretter kobler vi hovedkolonnen til TVDB ved hjelp av absolutt mapping og til AniDB-kolonnen ved hjelp av SxxExx-mapping. Scenekolonnen kan kobles ved hjelp av fullstendig mapping som vanlig.

## Korte vestlige tegneserieprogrammer

Barne-tv-programmer byr ofte på en utfordring når det gjelder kartlegging av episoder, fordi hvis en 30-minutters episode er delt inn i to separate historier, betrakter TVDB disse som to forskjellige episoder, mens scenen vanligvis betrakter dem som én episode. Dette betyr at vi trenger veldig detaljert direkte mapping mellom individuelle episoder.

Et eksempel på dette er serien [Paw Patrol](https://thexem.info/xem/show/4814). Når du holder musepekeren over episoder i hovedkolonnen, vil du se at en enkelt episode på scenens side er koblet til én eller to episoder på TVDB-siden. Denne spesielle typen kartlegging krever kontinuerlig oppdatering når nye episoder av serien sendes.

> Vær oppmerksom på at det kan være fornuftig å kartlegge én episode på den ene siden til flere episoder på den andre siden i tilfeller som dette, men det gir ingen mening å kartlegge flere episoder på den ene siden til flere episoder på den andre siden. Programvaren vil tillate deg å gjøre det, men vær så snill å ikke gjøre det, da Sonarr ikke vil kunne gjøre noe med det.
{.is-warning}

## Kompleks individuell mapping

I noen (heldigvis svært sjeldne!) tilfeller kan kartlegging av episoder på hverandre bli veldig kompleks. TVDB betrakter luftdatoene til hovednettverket til serien som ledende når det gjelder å bestemme episoderekkefølgen. Dette kan gjøre ting veldig komplekst i tilfeller som Firefly eller [Transporter](https://thexem.info/xem/show/1653), som ble sendt av sine opprinnelige nettverk i en rekkefølge som bryter med den kronologiske rekkefølgen. Scenen vil ofte kompensere for dette ved å bruke den kronologiske episoderekkefølgen, noe som resulterer i behov for kompleks individuell mapping for hver episode.

Legg merke til hvordan det ikke er noen automatisk mapping mellom hovedkolonnen og scenekolonnen for Transporter; all mapping oppnås ved hjelp av direkte koblinger mellom episoder.

# Begrensninger

TheXEM har for øyeblikket noen begrensninger som vi vil prøve å dekke her.

## Bare én nummereringsordning per serie støttes

Hvis flere utgivelsesgrupper bruker forskjellige nummereringssystemer, kompliserer dette ting. I slike tilfeller er det noen retningslinjer for uenige kilder.

1. Nummereringen fra scenen har alltid prioritet over nummereringen fra P2P-utgivelser.
2. Hvis det ikke finnes noen scenen-utgivelser for en bestemt serie, velg den som virker mest populær. Dette vil vanligvis komme ned til hvilken gruppe som vanligvis slipper episoder raskest i god kvalitet.
3. I tilfelle anime følger vi nummereringen til SubsPlease/Erai-Raws hvis den er tilgjengelig. Hvis ikke, gjelder den forrige retningslinjen også her.

## Bare én hovedenhet støttes

Du vil bruke hovedenheten i noen relativt sjeldne tilfeller for å opprette direkte koblinger *eller* for å unngå å måtte opprette direkte koblinger. Du kan imidlertid bare bruke én av disse hovedenhetene til å koble to andre enheter. Fordi målet er å sikre at kartleggingen fungerer for hovedbruksområdet med å koble TVDB til scenen, må du sørge for at minst *den* kartleggingen fungerer, og hvis det krever en hovedenhet, er det der du bør prioritere å bruke den.

## Sletting av hovedkolonnen eller individuelle sesonger i den

Når du sletter hovedkolonnen av en hvilken som helst grunn, må du sørge for at det ikke er noen direkte koblinger på individuelle episoder i den. Hvis du sletter sesongen mens koblingene fortsatt er der, **vil kartleggingen være usynlig i grensesnittet, men vil fortsatt eksistere!** Hvis du gjør dette ved et uhell, legger du bare tilbake sesongen du fjernet, angre de individuelle koblingene og slett deretter sesongen igjen.

## Noen ting kan bare ikke bli kartlagt

En av tingene du alltid må huske på er at noen ganger er en serie så rotete eller på annen måte kompleks at den ikke kan kartlegges i TheXEM. Noen ganger vil du kunne kartlegge ett av bruksområdene, noen ganger ikke engang det. I slike tilfeller kan det ofte ikke gjøres noe med det.

# Trenger du hjelp?

Til slutt, hvis du trenger hjelp med noe, eller hvis du rett og slett ikke har en konto på TheXEM, kan du bli med oss på Sonarrs Discord-server i [#xem-kanalen](https://discord.gg/QzDaBmN2J3). Vi hjelper deg gjerne. Vær imidlertid oppmerksom på at svartidene kan være langsomme og avhengige av tidssoneforskjell.
