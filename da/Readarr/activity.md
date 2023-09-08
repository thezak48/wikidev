---
title: Readarr Aktivitet
description: 
published: true
date: 2022-02-06T09:05:37.496Z
tags: 
editor: markdown
dateCreated: 2021-05-25T16:14:58.862Z
---

# Aktivitet

Aktivitet fanen er, hvor du kan se tidligere og nuværende aktiviteter, som \*Arr har udført. Dette inkluderer importeringer, sletninger, opgraderinger, hentninger, omdøbninger og fejl.

# Kø

Når noget bliver downloadet og endnu ikke importeret til \*Arr, vil det blive vist på Kø-siden.

Køen viser alle elementer, som applikationen kan genkende, der er i den angivne downloadklients kategori (Indstillinger => Downloadklient => Kategori). For at se alle udgivelser skal du gå til Indstillinger => Vis Ukendte. Køen gemmes ikke nogen steder i applikationen, men opdateres via svar fra din downloadklients API.

> For Usenet-klienter vil \*Arr kun kigge 60 elementer dybt i køen for potentielle importeringer! Det er vigtigt ikke at overskride dette, ellers bliver du nødt til at rydde op med manuelle importeringer, når dit system bliver overbelastet og begynder at gå glip af elementer!.
> Fjern afsluttede downloads skal også være aktiveret for din downloadklient. {.is-warning}

## Ikonhandlinger i Køen

- X - Fjern element fra køen
  - Fjern udgivelse fra downloadklient - Fjern udgivelse fra downloadklient. Obligatorisk for uoverensstemmende udgivelseselementer
  - Tilføj udgivelse til blokeringsliste - Tilføj udgivelse til blokeringsliste
- Menneskeikon - Manuel importering af udgivelse
- Hentikon - Send udgivelse til downloadklient

## Køstatusser

> Bemærk at nedenstående er ufuldstændigt {.is-warning}

| Ikon       | Status                   | Beskrivelse                                                                                     | Løsningsforslag                                          |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Gråt ur    | Afventer udgivelse       | Download afventer, at downloadklienten er tilgængelig, eller at udgivelsen opfylder forsinkelsesprofilregler | N/A                                                       |
| Gul        | Advarsel - Kan ikke importere | \*Arr kunne ikke importere udgivelsen. Gennemgå værktøjstip for flere detaljer                    | [Se fejlfindingssiden](/readarr/troubleshooting) |
| Lilla      | Importerer download      | Download importeres                                                                           | N/A                                                       |
|            |                          |                                                                                                 |                                                           |
|            |                          |                                                                                                 |                                                           |

# Historik

Historikfanen viser alt, der er blevet fjernet fra køen, fordi opgaven er blevet afsluttet. Dette inkluderer importeringer, fejl, hentninger, sletninger og opgraderinger.

Det venstre ikon er handlingen, der blev udført (listen over mulige handlinger vises nedenfor). Du kan filtrere disse ved at klikke på filterikonet i højre side. Du kan også vise flere kolonner ved at klikke på Indstillinger.

![history2.png](/assets/readarr/history2.png)

På statusserne `Hentet` kan du klikke på `i`-ikonet til højre for at se flere detaljer om downloaden (hvilken indekser den kom fra, URL'en for hentningen, uploadets alder osv.). Du kan også markere dette element som mislykket for at starte en fjernelse, tilføjelse til blokeringslisten og gen-søgning af elementet.

![history4.png](/assets/readarr/history4.png)

# Blokeringsliste

> Blokeringslisten blev tidligere kaldt 'Sortliste' {.is-info}

Blokeringslistesiden viser elementer, der er blokeret, så de ikke bliver downloadet igen. Disse er fejl fra den automatiske proces eller manuelt markerede mislykkede elementer. Elementer forbliver på blokeringslisten for evigt, medmindre du fjerner dem manuelt.

![blocklist1.png](/assets/readarr/blocklist1.png)

Ved at klikke på `i`-ikonet helt til højre kan du se flere detaljer om det blokerede element og om det blev markeret som mislykket manuelt eller automatisk under downloaden.

![blocklist2.png](/assets/readarr/blocklist2.png)

Ved at klikke på `x` helt til højre fjerner du elementet fra blokeringslisten, så du potentielt kan hente det igen, hvis det blev tilføjet ved en fejl.

## Almindelige årsager til blokering

- Bruger markerede download som mislykket manuelt
- Bruger valgte "Tilføj til blokeringsliste" ved fjernelse fra køen
- Usenet-downloadklient rapporterede fejl ved download af udgivelse