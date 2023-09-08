---
title: TheXEM Moderation Guide
description: Gids voor het mappen van verschillende scenario's in XEM voor optimaal gebruik met Sonarr en andere PVR-software.
published: true
date: 2021-11-24T19:26:31.972Z
tags: sonarr, xem
editor: markdown
dateCreated: 2021-10-03T16:48:28.241Z
---

# Inhoudsopgave

- [Inhoudsopgave](#inhoudsopgave)
- [TheXEM Moderation Guide](#thexem-moderation-guide)
- [Naamgeving](#naamgeving)
- [De verschillende entiteitstypen](#de-verschillende-entiteitstypen)
- [Mappen van typen](#mappen-van-typen)
  - [!SxxExx-mapping SxxExx-mapping](#-sxxexx-mapping)
  - [!Absolute-mapping Absolute-mapping](#-absolute-mapping)
  - [!Volledige mapping Volledige mapping](#-volledige-mapping)
  - [!Directe mapping Directe mapping](#-directe-mapping)
- [Voorbeelden](#voorbeelden)
  - [Basis Anime-mapping](#basis-anime-mapping)
  - [Complex anime-mapping](#complex-anime-mapping)
  - [Korte Westerse tekenfilms](#korte-westerse-tekenfilms)
  - [Complex individueel mappen](#complex-individueel-mappen)
- [Beperkingen](#beperkingen)
  - [Er wordt slechts één scènenummeringsschema per serie ondersteund](#er-wordt-slechts-één-scènenummeringsschema-per-serie-ondersteund)
  - [Er wordt slechts één hoofdentiteit ondersteund](#er-wordt-slechts-één-hoofdentiteit-ondersteund)
  - [Het verwijderen van de hoofdkolom of individuele seizoenen daarin](#het-verwijderen-van-de-hoofdkolom-of-individuele-seizoenen-daarin)
  - [Sommige dingen kunnen gewoonweg niet worden gemapt](#sommige-dingen-kunnen-gewoonweg-niet-worden-gemapt)
- [Hulp nodig?](#hulp-nodig)

# TheXEM Moderation Guide

[TheXEM](https://thexem.info) is een service die het mogelijk maakt om verbindingen te maken tussen andere services/entiteiten die verschillende nummering- en benamingsschema's gebruiken voor tv-seriereleases. Sonarr gebruikt TVDB als gegevensbron voor zijn afleveringsinformatie en soms gebruiken scènes en andere releasegroepen een ander benaming- of nummeringsschema. Met de juiste mapping is het mogelijk om ervoor te zorgen dat aflevering 1 van seizoen 1 volgens TVDB overeenkomt met aflevering 5 van seizoen 1 volgens de nummering van de scène, zodat Sonarr de juiste aflevering kan downloaden, ondanks dat de nummering anders is.

Deze gids is bedoeld voor mensen met een account op TheXEM en loodst je door enkele van de meest voorkomende patronen die je kunt gebruiken. Maar eerst zullen we je door enkele basisprincipes leiden.

# Naamgeving

Als conventie gebruiken we dezelfde naam als TVDB voor de show zelf. Dit is met name interessant voor internationale shows zoals anime en komt er in feite op neer dat we de officieel gelicenseerde Engelse naam van de show gebruiken.

Daarnaast is het mogelijk om verschillende aliassen voor de serienaam in te voeren, wat voornamelijk wordt gebruikt voor anime, maar soms ook handig is voor "gewone" tv.

# De verschillende entiteitstypen

TheXEM heeft vier verschillende gegevensbronnen of entiteitstypen die het momenteel ondersteunt en met elkaar kan verbinden wanneer dat nodig is. Deze vier typen zijn:

- Scène
- [TVDB](https://thetvdb.com)
- [AniDB](https://anidb.net)
- Master

Een juiste XEM-mapping voor een bepaalde show moet *ten minste* een vermelding hebben in de scènekolom en een vermelding in de TVDB-kolom met het toepasselijke mappingtype (zie de paragraaf *Mappen van typen* hieronder) daartussen.

> Shows die geen scènekolom en TVDB-kolom hebben, zijn nutteloos en worden mogelijk verwijderd. Hetzelfde geldt voor shows waarin geen directe of indirecte verbinding is tussen de scènekolom en de TVDB-kolom.
{.is-warning}

# Mappen van typen

TheXEM heeft drie verschillende automatische opties om verschillende entiteiten met elkaar te verbinden: SxxExx-mapping, absolute mapping en de combinatie van beide, volledige mapping. Daarnaast kun je ook afleveringen rechtstreeks op elkaar mappen met directe mapping. Elk van deze opties heeft zijn eigen gebruik en is nuttig in specifieke situaties.

## ![SxxExx-mapping](/assets/sonarr/xem-guide/mapping-sxxexx.svg) SxxExx-mapping

Dit type mapping bepaalt dat tussen de twee verbonden entiteiten het seizoens- en afleveringsnummer gelijk zijn, wat betekent dat S01E01 dezelfde aflevering is in beide entiteitstypen. De absolute nummering is echter niet noodzakelijk hetzelfde.

## ![Absolute-mapping](/assets/sonarr/xem-guide/mapping-abs.svg) Absolute-mapping

Afgezien van een paar zeer specifieke gevallen is absolute mapping bijna uitsluitend nuttig voor animeseries. Het animeschema dat de meeste releasegroepen gebruiken, gebruikt gewoon een toenemend afleveringsnummer in plaats van SxxExx-nummering, wat we absolute nummering noemen. Door de mapping tussen twee entiteiten als "absoluut" te markeren, vertelt dit aan services die deze gegevens gebruiken dat de SxxExx-nummering al dan niet kan verschillen, maar dat de absolute nummering in ieder geval hetzelfde is.

## ![Volledige mapping](/assets/sonarr/xem-guide/mapping-full.svg) Volledige mapping

Volledige mapping vertelt elke service die TheXEM gebruikt dat zowel de absolute nummering als de SxxExx-mapping tussen de twee verbonden entiteiten hetzelfde zijn, wat betekent dat de nummering hetzelfde is tussen beide entiteiten.

> Dit betekent dat als je aan je mapping alleen een scènekolom en een TVDB-kolom wilt toevoegen met volledige mapping daartussen, je serie-invoer overbodig is, omdat dit standaard werkt zonder een vermelding op TheXEM.
{.is-info}

## ![Directe mapping](/assets/sonarr/xem-guide/mapping-direct.svg) Directe mapping

Directe mapping is alleen mogelijk tussen het entiteitstype Master en de entiteiten aan beide zijden ervan. Je wilt dit zo min mogelijk gebruiken, omdat zodra je directe verbindingen begint te gebruiken, je deze ten minste voor de rest van het seizoen en in sommige gevallen voor de rest van de hele show moet blijven gebruiken.

Je kunt directe mapping inschakelen door op het pictogram boven het automatische mappingtype te klikken. Je ziet dat de gebruikersinterface van de pagina een beetje verschuift om ruimte te maken voor de verbindingen die je gaat maken. Om een aflevering met een andere aflevering te verbinden, klik je eenvoudigweg op een aflevering aan de linkerkant van de verbinding, gevolgd door het klikken op de overeenkomstige aflevering aan de rechterkant. Als je het goed hebt gedaan, vraagt de site je om de verbinding te bevestigen.

> Het is mogelijk om een enkele aflevering aan één kant te koppelen aan meerdere afleveringen aan de andere kant, bijvoorbeeld als TVDB twee afleveringen als afzonderlijke afleveringen beschouwt terwijl de scène ze samenvoegt tot één nummer. Dit is met name interessant voor westerse tekenfilms.
{.is-info}

# Voorbeelden

Het bovenstaande is veel informatie, maar alles bij elkaar genomen zijn er slechts een handvol gebruiksscenario's die het overgrote deel van alle shows die je ooit aan TheXEM moet toevoegen, bestrijken. Hieronder volgen enkele zeer gebruikelijke soorten mapping.

## Basis Anime-mapping

Bij het mappen van een animeshow gebruiken we altijd de AniDB-kolom. Wanneer dit mogelijk is bij de mapping die je probeert te bereiken, moet je altijd streven naar volledige mapping tussen de scènekolom en de AniDB-kolom.

De meeste animeshows kunnen rechtstreeks worden gemapt tussen de scènekolom via AniDB en uiteindelijk naar TVDB. Een eenvoudig voorbeeld is de show [Ronia the Robber's Daughter](https://thexem.info/xem/show/1603). Het heeft in de eerste plaats mapping nodig omdat de Japanse naam die door releasegroepen wordt gebruikt niet overeenkomt met de Engelse naam die door TVDB wordt gebruikt, maar verder is de mapping eenvoudig: de nummering is identiek tussen de scène en AniDB, dus we gebruiken volledige mapping tussen die twee, terwijl het enige wat we zeker weten tussen AniDB en TVDB is dat de SxxExx-nummering identiek is.

> AniDB reset de absolute nummering tussen elk seizoen omdat het elk seizoen als zijn eigen show beschouwt. Bij het toevoegen van een nieuw AniDB-seizoen moet je ervoor zorgen dat je het ID-nummer invoert en dat je het veld "Ab. Start" voor dat nieuwe seizoen instelt op 1.
{.is-info}

Voor een voorbeeld van een animeshow met meerdere seizoenen, kijk naar [Assassination Classroom](https://thexem.info/xem/show/2817). Let op de aparte aliassen voor het tweede seizoen, die Sonarr helpen begrijpen dat `[Release group] Ansatsu Kyoushitsu - 01 (1080p)` overeenkomt met S01E01 in TVDB, terwijl `[Release group] Ansatsu Kyoushitsu S2 - 01 (1080p)` overeenkomt met S02E01.

## Complex anime-mapping

Soms komt het concept dat TVDB van een seizoen heeft niet overeen met wat AniDB een seizoen noemt. Dit gebeurt met name wanneer een anime wordt uitgebracht als een zogenaamde *split-cour*. Dit presenteert zichzelf als een reeks afleveringen, gevolgd door een korte pauze waarna de volgende reeks afleveringen ook wordt uitgezonden. Split-cour anime heeft meestal één of hooguit twee animeseizoenen tussen zich en TVDB beschouwt een anime meestal als split-cour wanneer de tweede reeks afleveringen wordt aangekondigd tijdens de uitzendtijd van het eerste deel.

Een voorbeeld van hoe dit eruit zou kunnen zien, is [That Time I Got Reincarnated as a Slime](https://thexem.info/xem/show/5241). Let op hoe wat TVDB seizoen 2 noemt eigenlijk is opgesplitst in seizoenen 2 en 3 wat AniDB betreft. We gebruiken hier een link naar de Master-entiteit om de mapping minder complex te maken. In feite combineert de Master-vermelding de absolute nummering zoals gebruikt op TVDB met de SxxExx-nummering die AniDB gebruikt. We linken vervolgens de Master-kolom aan TVDB met absolute mapping en aan de AniDB-kolom met SxxExx-mapping. De scènekolom kan worden gekoppeld met behulp van volledige mapping zoals gebruikelijk.

## Korte Westerse tekenfilms

Kinderprogramma's bieden vaak een uitdaging bij het mappen van de afleveringen, omdat als een aflevering van 30 minuten wordt opgesplitst in twee aparte verhalen, TVDB die als twee verschillende afleveringen beschouwt, terwijl de scène ze meestal als één aflevering beschouwt. Dit betekent dat we zeer gedetailleerde directe mapping tussen individuele afleveringen nodig hebben.

Een voorbeeld hiervan is de show [Paw Patrol](https://thexem.info/xem/show/4814). Wanneer je over afleveringen in de Master-kolom zweeft, zie je dat een enkele aflevering aan de scènekant is gekoppeld aan één of twee afleveringen aan de TVDB-kant. Dit specifieke type mapping vereist voortdurende input naarmate er nieuwe afleveringen van de serie worden uitgezonden.

> Houd er rekening mee dat het zinvol kan zijn om één aflevering aan één kant te koppelen aan meerdere afleveringen aan de andere kant, maar dat het niet zinvol is om meerdere afleveringen aan één kant te koppelen aan meerdere afleveringen aan de andere kant. De software staat je toe om het te doen, maar doe het alsjeblieft niet, omdat Sonarr er niets mee kan doen.
{.is-warning}

## Complex individueel mappen

In sommige (gelukkig zeer zeldzame!) gevallen kan het mappen van afleveringen op elkaar erg complex worden. TVDB beschouwt de uitzenddata van het hoofdnetwerk van de show als leidend bij het bepalen van de volgorde van de afleveringen. Dat kan de zaken echt complex maken in gevallen zoals Firefly of [Transporter](https://thexem.info/xem/show/1653), die door hun oorspronkelijke netwerken werden uitgezonden in een volgorde die de chronologische volgorde doorbreekt. De scène compenseert dit vaak door de chronologische afleveringsvolgorde te gebruiken, wat resulteert in complexe individuele mapping voor elke aflevering.

Let op hoe bij Transporter er geen automatische mapping is tussen de Master-kolom en de scènekolom; alle mapping wordt bereikt door directe links tussen afleveringen.

# Beperkingen

TheXEM heeft momenteel enkele beperkingen die we hier zullen proberen te behandelen.

## Er wordt slechts één scènenummeringsschema per serie ondersteund

Als meerdere releasegroepen verschillende nummeringsschema's gebruiken, wordt dit gecompliceerd. In dergelijke gevallen zijn er een paar richtlijnen in het geval van tegenstrijdige bronnen.

1. Nummering van scènereleases heeft altijd voorrang op die van P2P-releases.
2. Als er geen scènereleases bestaan voor een bepaalde show, kies dan degene die het meest populair lijkt. Dit komt meestal neer op de groep die afleveringen het snelst in goede kwaliteit uitbrengt.
3. In het geval van anime volgen we de nummering van SubsPlease/Erai-Raws indien beschikbaar. Zo niet, dan geldt hier ook de vorige richtlijn.

## Er wordt slechts één hoofdentiteit ondersteund

Je zult het entiteitstype Master in enkele relatief zeldzame gevallen gebruiken om directe verbindingen te maken *of* om te voorkomen dat je directe verbindingen moet maken. Je kunt echter slechts één van die hoofdentiteiten gebruiken om twee andere entiteiten met elkaar te verbinden. Omdat het uiteindelijke doel is om ervoor te zorgen dat de mapping werkt voor het belangrijkste gebruiksscenario van het verbinden van TVDB met de scène, moet je ervoor zorgen dat ten minste *die* mapping werkt en als dat een hoofdentiteit vereist, is dat waar je prioriteit aan moet geven.

## Het verwijderen van de hoofdkolom of individuele seizoenen daarin

Wanneer je om welke reden dan ook de Master-kolom verwijdert, zorg er dan voor dat er geen directe mappings zijn op individuele afleveringen daarin. Als je het seizoen verwijdert terwijl de mappings er nog steeds zijn, **zal de mapping onzichtbaar zijn in de interface, maar zal nog steeds bestaan!** Als je dit per ongeluk doet, voeg dan gewoon het seizoen dat je hebt verwijderd opnieuw toe, maak de individuele links ongedaan en verwijder vervolgens het seizoen opnieuw.

## Sommige dingen kunnen gewoonweg niet worden gemapt

Een van de dingen om altijd in gedachten te houden is dat soms een serie zo verward of anderszins complex is dat deze niet kan worden gemapt in TheXEM. Soms kun je een van de gebruiksscenario's mappen, soms zelfs dat niet. In die gevallen kan er vaak niets aan worden gedaan.

# Hulp nodig?

Tot slot, als je hulp nodig hebt bij iets of als je eenvoudigweg geen account hebt op TheXEM, sluit je dan aan bij ons op de Discord-server van Sonarr in het kanaal [#xem](https://discord.gg/QzDaBmN2J3). We helpen je graag. Houd er echter rekening mee dat de responstijden mogelijk traag zijn en sterk afhankelijk zijn van het tijdsverschil.
