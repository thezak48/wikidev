---
title: Sonarr Snabbstartsguide
description: 
published: true
date: 2022-07-14T14:07:19.793Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-09-03T19:14:22.283Z
---

# Innehållsförteckning

- [Innehållsförteckning](#innehållsförteckning)
- [Snabbstartsguide för installation](#snabbstartsguide-för-installation)
- [Starta](#starta)
- [Mediehantering](#mediehantering)
  - [Avsnittsnamn](#avsnittsnamn)
  - [Importera](#importera)
  - [Rotmappar](#rotmappar)
- [Profiler](#profiler)
- [Indexerare](#indexerare)
- [Nedladdningsklienter](#nedladdningsklienter)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
- [Hur du importerar ditt befintliga organiserade mediebibliotek](#hur-du-importerar-ditt-befintliga-organiserade-mediebibliotek)
  - [Importera avsnitt](#importera-avsnitt)
    - [Importera befintligt media](#importera-befintligt-media)
    - [Ingen matchning hittades](#ingen-matchning-hittades)
    - [Fixa felaktigt mappnamn efter import](#fixa-felaktigt-mappnamn-efter-import)
- [Lägg till nya serier](#lägg-till-nya-serier)

# Snabbstartsguide för installation

> Den här sidan är fortfarande under arbete och inte komplett. Bidrag är välkomna.

> För en mer detaljerad genomgång av alla inställningar, se [Sonarr => Inställningar](/sonarr/settings)
{.is-info}

I den här guiden kommer vi att försöka förklara den grundläggande installationen du behöver göra för att komma igång med Sonarr. Vi kommer att hoppa över vissa alternativ som du kan se på skärmen. Om du vill gå djupare in på dessa, se den lämpliga sidan i FAQ och dokumentationen för en fullständig förklaring.

> Observera att avancerade alternativ visas i `orange` på skärmbilderna och i GUI-inställningarna. Du måste klicka på `Visa avancerat` längst upp på sidan för att göra dem synliga.
{.is-warning}

# Starta

Efter installation och start öppnar du en webbläsare och går till `http://{din_ip_här}:8989`

![qs_startup.png](/assets/sonarr/qs_startup.png)

# Mediehantering

Först ska vi titta på inställningarna för `Mediehantering` där vi kan ställa in våra önskade namngivnings- och filhanteringsinställningar.

Klicka på `Inställningar` => `Mediehantering` i den vänstra menyn.

## Avsnittsnamn

![qs_episodenaming.png](/assets/sonarr/qs_episodenaming.png)

- Markera rutan för att aktivera Namnge avsnitt.
- Bestäm dina standard-, dagliga och anime-namngivningskonventioner för avsnitt. Du bör granska de rekommenderade namngivningskonventionerna [här](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/).

> Om du väljer att inte inkludera kvalitet/upplösning eller releasegrupp är detta information du inte kan återfå senare. Det rekommenderas starkt att du inkluderar dessa i din namngivningskonvention.
{.is-info}

## Importera

![mm_importing.png](/assets/sonarr/mm_importing.png)

- (Avancerat alternativ) Om du vill att TBA-avsnitt ska importeras omedelbart, ändra "Kräv avsnittstitel" till "Aldrig".
- (Avancerat alternativ) Aktivera `Använd hårddisklänkar istället för att kopiera` för mer information om hur och varför med exempel, se [TRaSH's Hårddisklänkguide](https://trash-guides.info/hardlinks).
- Markera rutan för att importera extra filer och lägg till minst `.srt` i listan.

## Rotmappar

Här kommer vi att lägga till rotmappen som Sonarr kommer att använda för att importera ditt befintliga organiserade mediebibliotek och där Sonarr kommer att importera (kopiera/hårddisklänka/flytta) ditt media efter att din nedladdningsklient har laddat ner det. Det här är mappen där dina serier och avsnitt lagras för att din mediaspelare ska kunna spela upp dem. Det är INTE där du laddar ner filer till!

> \* Användare som inte använder Windows: Om du använder en NFS-montyr, se till att `nolock` är aktiverat.
> \* Om du använder en SMB-montyr, se till att `nobrl` är aktiverat.
{.is-warning}

> **Användaren och gruppen som du har konfigurerat Sonarr att köra som måste ha läs- och skrivrättigheter till denna plats.**
{.is-info}

> **Din nedladdningsmapp och mediamapp kan inte vara samma plats**
{.is-danger}

Glöm inte att spara dina ändringar!

# Profiler

`Inställningar` => `Profiler`

Vi rekommenderar att du skapar dina egna profiler och bara väljer de kvalitetskällor du verkligen vill ha. Det finns dock flera förifyllda kvalitetsprofiler att välja mellan om någon av dem passar. Om du behöver mer information om profiler, se [lämplig wikisida](/sonarr/settings#profiles) för den sektionen.

# Indexerare

`Inställningar` => `Indexerare`

Här lägger du till indexerare/spårare som du kommer att använda för att faktiskt ladda ner dina filer.

När du har klickat på <kb>+</kb>-knappen för att lägga till en ny indexerare kommer du att få upp ett nytt fönster med många olika alternativ. För Sonarr betraktas både Usenet-indexerare och Torrent-spårare som "indexerare".

Här finns två avsnitt: Usenet och Torrents. Beroende på vilken nedladdningsklient du kommer att använda vill du välja vilken typ av indexerare du kommer att använda.

De flesta Usenet-indexerare kräver en API-nyckel, som kan hittas på din profil på indexerarens webbplats.

De flesta Torrent-spårare kräver att [Prowlarr](/prowlarr) eller Jackett används i Sonarr.

Lägg till minst en indexerare för att Sonarr ska fungera korrekt.

> Se [inställningssidan](/sonarr/settings#indexers) och [Mer information (Stödda)](/sonarr/supported#indexers)-sidan för denna sektion för mer information.
{.is-info}

# Nedladdningsklienter

`Inställningar` => `Nedladdningsklienter`

Nedladdning och import är där de flesta personer upplever problem. På en övergripande nivå måste programvaran kunna kommunicera med din nedladdningsklient och ha åtkomst till de filer den laddar ner. Det finns många olika nedladdningsklienter som stöds och ännu fler olika konfigurationer. Det innebär att det finns några vanliga konfigurationer, men det finns ingen rätt konfiguration och varje persons konfiguration kan vara lite annorlunda. Men det finns många felaktiga konfigurationer.

> Se [inställningssidan](/sonarr/settings#download-clients), [Mer information (Stödda)](/sonarr/supported#download-clients)-sidan för denna sektion och [TRaSH's Nedladdningsklientguider](https://trash-guides.info/Downloaders/) för mer information.
{.is-info}

## {.tabset}

### Usenet

{#usenet}

- Sonarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Sonarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- När nedladdningen är klar kommer Sonarr att känna till den slutliga filplatsen enligt rapporterad av din nedladdningsklient. Denna filplats kan vara nästan var som helst, så länge den är någonstans separat från din mediamapp och åtkomlig av Sonarr.
- Sonarr kommer att skanna den avslutade filplatsen efter filer som Sonarr kan använda. Den kommer att analysera filnamnet för att matcha det mot det begärda mediet. Om den kan göra det kommer den att döpa om filen enligt dina specifikationer och flytta den till den angivna medieplatsen.
- Atomiska flyttar (direktflyttar) är aktiverade som standard. Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningsmapp och ditt mediebibliotek. Om den atomiska flytten misslyckas eller din konfiguration inte stöder hårddisklänkar och atomiska flyttar kommer Sonarr att backa och kopiera filen och sedan ta bort den från källan, vilket är intensivt för I/O.
- Om alternativet "Hantering av avslutade nedladdningar - Ta bort" är aktiverat i Sonarrs inställningar kommer överblivna filer från nedladdningen att skickas till papperskorgen eller återvinningen genom en begäran till din klient att ta bort släppet.

### BitTorrent

{#bittorrent}

- Sonarr kommer att skicka en nedladdningsbegäran till din klient och associera den med ett etikett- eller kategorinamn som du har konfigurerat i inställningarna för nedladdningsklienten.
  - Exempel: filmer, tv, serier, musik, etc.
- Sonarr kommer att övervaka dina nedladdningsklients aktiva nedladdningar som använder det kategorinamnet. Detta övervakas via din nedladdningsklients API.
- Färdiga filer lämnas kvar på sin ursprungliga plats för att du ska kunna seeda filen (kvot eller tid kan justeras i nedladdningsklienten eller från Sonarr under den specifika nedladdningsklienten). När filer importeras till din mediamapp kommer Sonarr att skapa en hårddisklänk till filen om det stöds av din konfiguration, annars kopieras filen om hårddisklänkar inte stöds.
- Hårddisklänkar är aktiverade som standard. [En hårddisklänk kommer inte att använda något extra diskutrymme.](https://trash-guides.info/Hardlinks/Hardlinks-and-Instant-Moves/) Filsystemet och monteringspunkterna måste vara desamma för din avslutade nedladdningsmapp och ditt mediebibliotek. Om skapandet av hårddisklänken misslyckas eller din konfiguration inte stöder hårddisklänkar kommer Sonarr att backa och kopiera filen.
- Om alternativet "Hantering av avslutade nedladdningar - Ta bort" är aktiverat i Sonarrs inställningar kommer Sonarr att ta bort torrenten från din klient och be klienten att ta bort torrentdata, men endast om klienten rapporterar att seedningen är klar och torrenten är stoppad (pausad vid slutförande).

# Hur du importerar ditt befintliga organiserade mediebibliotek

> Observera att Sonarr inte regelbundet söker efter avsnitt. Se FAQ-inlägget för detaljer för att förstå hur Sonarr fungerar.
[Hur hittar Sonarr avsnitt?](/sonarr/faq#how-does-sonarr-find-episodes)
{.is-info}

Efter att ha konfigurerat dina profiler/kvalitetsstorlekar och lagt till dina indexerare och nedladdningsklient(er) är det dags att importera ditt befintliga organiserade mediebibliotek.

Kommer snart - Bidrag välkomnas

## Importera befintligt media

Beroende på hur väl dina befintliga seriemappar är namngivna kommer Sonarr att försöka matcha dem med rätt serie. Du bör granska den här listan noggrant innan du importerar.

Biblioteksimport ska endast användas för ett befintligt organiserat bibliotek och får inte användas för en nedladdningsmapp eller för att ad hoc-importera media.

1. Gå till Biblioteksimport
1. Läs och förstå hjälptexten för Biblioteksimport
1. Välj eller lägg till rotmappen (biblioteket) att importera serier från
1. Granska Sonarrs kartläggning/matchning av seriemappar till TVDb-serier
1. Ställ in dina övervakningsinställningar och kvalitetsprofil som lämpligt
1. Klicka på Starta import

### Ingen matchning hittades

1. Sök efter seriens namn eller TVDbId i serieväljaren
1. Se [detta FAQ-inlägg](/sonarr/faq#why-can-i-not-add-a-series) om serien inte kan hittas

### Fixa felaktigt mappnamn efter import

1. Ta bort serien från Sonarr
1. Biblioteksimport
1. Se till att serien är korrekt kartlagd

# Lägg till nya serier

[Hänvisa till bibliotekssidan för ytterligare information](/sonarr/library#add-new)

# Importera avsnitt

- Använd Önskade => Manuell import för att importera avsnittsfiler till sina seriemappar vid behov
- Använd Hantera avsnitt på en seriens sida för att omkartlägga eller kartlägga befintliga avsnittsfiler i en seriemapp