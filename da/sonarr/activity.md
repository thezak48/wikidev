---
title: Sonarr Aktivitet
description: 
published: true
date: 2022-02-06T09:07:34.371Z
tags: sonarr
editor: markdown
dateCreated: 2021-06-11T23:32:31.144Z
---

# Aktivitet

Aktivitet fanen er, hvor du kan se tidligere og nuværende aktiviteter, som \*Arr har udført. Dette inkluderer importeringer, sletninger, opgraderinger, hentninger, omdøbninger og fejl.

# Kø

Når noget er i gang med at blive downloadet og endnu ikke er importeret til \*Arr, vil det blive vist på Kø-siden.

Køen viser alle elementer, som applikationen kan genkende, der er i den angivne downloadklients kategori (Indstillinger => Downloadklient => Kategori). For at se alle udgivelser skal du gå til Indstillinger => Vis Ukendte. Køen gemmes ikke nogen steder i applikationen, men opdateres via svar fra din downloadklients API.

> For Usenet-klienter vil \*Arr kun kigge 60 elementer dybt i køen for potentielle importeringer! Det er vigtigt ikke at overskride dette, ellers bliver du nødt til at rydde op med manuelle importeringer, når dit system bliver overbelastet og begynder at gå glip af elementer!.
> Fjern Færdiggjorte Downloads skal også være aktiveret for din downloadklient. {.is-warning}

## Handlingssymboler i Køen

- X - Fjern element fra køen
  - Fjern udgivelse fra downloadklient - Fjern udgivelse fra downloadklient. Obligatorisk for uoverensstemmende udgivelseselementer
  - Bloker udgivelse - Tilføj udgivelse til blokeringsliste
- Menneskeikon - Manuel importering af udgivelse
- Hentikon - Send udgivelse til downloadklient

## Køstatusser

> Bemærk at nedenstående er ufuldstændigt {.is-warning}

| Ikon       | Status                   | Beskrivelse                                                                                     | Løsningsforslag                                         |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| gråt ur    | Udlevering afventer      | Download venter på, at downloadklienten er tilgængelig, eller at udgivelsen opfylder forsinkelsesprofilregler | N/A                                                      |
| gult       | Advarsel - Kan ikke importere | \*Arr kunne ikke importere udgivelsen. Gennemgå værktøjstip for flere detaljer                    | [Se fejlfindingssiden](/sonarr/troubleshooting) |
| lilla      | Importering af download  | Download importeres                                                                           | N/A                                                      |
|            |                          |                                                                                                 |                                                          |
|            |                          |                                                                                                 |                                                          |

# Historik

Historikfanen viser alt, der er fjernet fra køen som følge af, at opgaven er afsluttet. Dette inkluderer importeringer, fejl, hentninger, sletninger og opgraderinger.

Det venstre ikon er handlingen, der blev udført (listen over mulige handlinger vises nedenfor). Du kan filtrere disse ved at klikke på filterikonet i højre side. Du kan også vise flere kolonner ved at klikke på Indstillinger.

![history2.png](/assets/sonarr/history2.png)

I `Hentet`-statusser kan du klikke på `i`-ikonet til højre for at se flere detaljer om downloaden (hvilken indekser den kom fra, URL'en for hentningen, uploadets alder osv.). Du kan også markere dette element som mislykket for at starte en fjernelse, blokering og gen-søgning af elementet.

![history4.png](/assets/sonarr/history4.png)

# Blokeringsliste

> Blokeringslisten blev tidligere kaldt 'Sortliste' {.is-info}

Blokeringslistesiden viser elementer, der er blokeret, så de ikke bliver downloadet igen. Disse er fejl fra den automatiske proces eller manuelt markerede mislykkede elementer. Elementer forbliver på blokeringslisten for evigt, medmindre du fjerner dem manuelt.

![blocklist1.png](/assets/sonarr/blocklist1.png)

Ved at klikke på `i`-ikonet helt til højre vises flere detaljer om det blokerede element og om det blev markeret som mislykket manuelt eller automatisk under download.

![blocklist2.png](/assets/sonarr/blocklist2.png)

Ved at klikke på `x` helt til højre fjernes elementet fra blokeringslisten, så du potentielt kan hente det igen, hvis det blev tilføjet ved en fejl.

## Almindelige årsager til blokering

- Bruger markerede download som mislykket manuelt
- Bruger valgte "Tilføj til blokeringsliste" ved fjernelse fra køen
- Usenet-downloadklient rapporterede fejl ved download af udgivelse