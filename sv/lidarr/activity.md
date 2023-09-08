---
title: Lidarr Aktivitet
description: 
published: true
date: 2022-02-06T09:06:39.366Z
tags: lidarr, behöver-kärlek, aktivitet
editor: markdown
dateCreated: 2021-06-14T21:35:25.390Z
---

# Aktivitet

Aktivitet-fliken är där du kan se tidigare och pågående aktiviteter som \*Arr har utfört. Det inkluderar importeringar, borttagningar, uppgraderingar, hämtningar, namnändringar och misslyckanden.

# Kö

När något laddas ner aktivt och ännu inte har importerats till \*Arr, visas det på Kö-sidan.

Kön visar alla objekt som applikationen kan känna igen och som finns i den angivna nedladdningsklientens kategori (Inställningar => Nedladdningsklient => Kategori). För att visa alla utgåvor, gå till Alternativ => Visa Okända. Kön sparas inte någonstans i applikationen, men uppdateras via ditt nedladdningsklients API-svar.

> För Usenet-klienter kommer \*Arr bara att titta 60 objekt djupt i kön för potentiella importeringar! Det är viktigt att inte överskrida detta, annars måste du rensa upp med manuella importeringar när ditt system blir överbelastat och börjar missa objekt!.
> Ta bort slutförda nedladdningar bör också vara aktiverat för din nedladdningsklient. {.is-warning}

## Kö-åtgärdsikoner

- X - Ta bort objekt från kön
  - Ta bort utgåva från nedladdningsklient - Ta bort utgåva från nedladdningsklienten. Obligatoriskt för omatchade utgåvor
  - Blockera utgåva - Lägg till utgåva i blocklistan
- Människoikon - Manuell importering av utgåva
- Hämta-ikon - Skicka utgåva till nedladdningsklienten

## Kö-statusar

> Observera att nedanstående är ofullständigt {.is-warning}

| Ikon        | Status                   | Beskrivning                                                                                   | Åtgärdssteg                                              |
| ----------- | ------------------------ | --------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| grå klocka  | Utgåva väntar            | Nedladdningen väntar på att nedladdningsklienten ska bli tillgänglig eller att utgåvan uppfyller reglerna för fördröjningsprofilen | N/A                                                      |
| gul         | Varning, kan inte importera | \*Arr kunde inte importera utgåvan. Granska verktygstipset för mer information               | [Se felsökningsguiden](/lidarr/troubleshooting) |
| lila        | Importerar nedladdning   | Nedladdningen importeras                                                                      | N/A                                                      |
|             |                          |                                                                                               |                                                          |
|             |                          |                                                                                               |                                                          |

# Historik

Historik-fliken visar allt som har lämnat kön genom att uppgiften har slutförts/avslutats. Det inkluderar importeringar, misslyckanden, hämtningar, borttagningar och uppgraderingar.

Den vänstra ikonen är åtgärden som utfördes (listan över möjliga åtgärder visas nedan). Du kan filtrera dessa genom att klicka på filterikonen på höger sida. Du kan också visa fler kolumner genom att klicka på Alternativ.

![history2.png](/assets/lidarr/history2.png)

På statusarna `Hämtad` kan du klicka på informationsikonen `i` till höger för att se mer detaljer om nedladdningen (vilken indexer den kom från, URL:en för hämtningen, åldern på uppladdningen, etc.). Du kan också markera detta objekt som misslyckat för att initiera borttagning, blocklistning och ny sökning av objektet.

![history4.png](/assets/lidarr/history4.png)

# Blocklista

> Blocklista kallades tidigare 'Svartlista' {.is-info}

Blocklist-sidan visar objekt som är blocklistade så att de inte laddas ner igen. Dessa är misslyckanden från den automatiska processen eller manuellt markerade misslyckade objekt. Objekt förblir i blocklistan för alltid om du inte tar bort dem manuellt.

![blocklist1.png](/assets/lidarr/blocklist1.png)

Genom att klicka på informationsikonen `i` längst till höger kan du se mer detaljer om det blocklistade objektet och om det markerades som misslyckat manuellt eller misslyckades automatiskt under nedladdningen.

![blocklist2.png](/assets/lidarr/blocklist2.png)

Genom att klicka på `x` längst till höger tar du bort objektet från blocklistan, så att du potentiellt kan hämta det igen om det lades till av misstag.

## Vanliga anledningar till blocklistning

- Användaren markerade nedladdningen som misslyckad manuellt
- Användaren valde "Lägg till i blocklistan" vid borttagning från kön
- Usenet-nedladdningsklienten rapporterade misslyckande vid nedladdning