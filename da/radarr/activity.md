---
title: Radarr Aktivitet
description: 
published: true
date: 2022-02-06T09:07:15.520Z
tags: radarr
editor: markdown
dateCreated: 2021-05-25T01:28:36.350Z
---

# Aktivitet

Aktivitet fanen er, hvor du kan se tidligere og nuværende aktiviteter, som \*Arr har udført. Dette inkluderer importeringer, sletninger, opgraderinger, hentninger, omdøbninger og fejl.

# Kø

Når noget bliver downloadet og endnu ikke importeret til \*Arr, vil det blive vist på Kø siden.

Køen viser alle elementer, som applikationen kan genkende, der er i den specificerede downloadklients kategori (Indstillinger => Downloadklient => Kategori). For at se alle udgivelser skal du gå til Indstillinger => Vis Ukendte. Køen bliver ikke gemt nogen steder i applikationen, men bliver opdateret via API-respons fra din downloadklient.

> For Usenet-klienter vil \*Arr kun kigge 60 elementer dybt i køen for potentielle importeringer! Det er vigtigt ikke at overskride dette, ellers bliver du nødt til at rydde op med manuelle importeringer, når dit system bliver overbelastet og begynder at gå glip af elementer!.
> Fjern Færdiggjorte Downloads skal også være aktiveret for din downloadklient. {.is-warning}

## Kø Handling Ikoner

- X - Fjern Element fra Kø
  - Fjern Udgivelse fra Downloadklient - Fjern Udgivelse fra Downloadklient. Obligatorisk for uoverensstemmende udgivelseselementer
  - Bloker Udgivelse - Tilføj Udgivelse til Blokeringsliste
- Menneskeikon - Manuel Importering af Udgivelse
- Hentikon - Send Udgivelse til Downloadklient

## Kø Statusser

> Bemærk at nedenstående er ufuldstændigt {.is-warning}

| Ikon       | Status                   | Beskrivelse                                                                                     | Løsningsforslag                                         |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| gråt ur    | Udlevering Afventer      | Download afventer, at Downloadklienten er tilgængelig, eller at udgivelsen opfylder forsinkelsesprofilregler | N/A                                                      |
| gult       | Advarsel Kan Ikke Importeres | \*Arr kunne ikke importere udgivelsen. Gennemgå værktøjstippen for flere detaljer                    | [Se Fejlfinding Guiden](/radarr/troubleshooting) |
| lilla      | Download Importeres      | Download importeres                                                                           | N/A                                                      |
|            |                          |                                                                                                 |                                                          |
|            |                          |                                                                                                 |                                                          |

# Historik

Historik fanen viser alt, der er fjernet fra køen ved at opgaven er blevet afsluttet. Dette inkluderer importeringer, fejl, hentninger, sletninger og opgraderinger.

Det venstre ikon er handlingen, der blev udført (listen over mulige handlinger vises nedenfor). Du kan filtrere disse ved at klikke på filterikonet i højre side. Du kan også vise flere kolonner ved at klikke på Indstillinger.

![history2.png](/assets/radarr/history2.png)

På `Hentet` statusser kan du klikke på `i` ikonet til højre for at se flere detaljer om downloaden (hvilken indekser den kom fra, URL'en for hentningen, uploadets alder osv.). Du kan også markere dette element som mislykket for at starte en fjernelse, blokering og gen-søgning af elementet.

![history4.png](/assets/radarr/history4.png)

# Blokeringsliste

> Blokeringsliste blev tidligere kendt som 'Sorteringsliste' {.is-info}

Blokeringslistesiden viser dig elementer, der er blokeret, så de ikke bliver downloadet igen. Disse er fejl fra den automatiske proces eller manuelt markerede mislykkede elementer. Elementer forbliver på blokeringslisten for evigt, medmindre du fjerner dem manuelt.

![blocklist1.png](/assets/radarr/blocklist1.png)

Ved at klikke på `i` ikonet helt til højre vises flere detaljer om det blokerede element og om det blev markeret som mislykket manuelt eller automatisk mislykkedes under download.

![blocklist2.png](/assets/radarr/blocklist2.png)

Ved at klikke på `x` helt til højre fjernes elementet fra blokeringslisten, så du potentielt kan hente det igen, hvis det blev tilføjet ved en fejl.

## Almindelige Blokeringsliste Årsager

- Bruger Markeret Download som Mislykket Manuelt
- Bruger Valgte "Tilføj til Blokeringsliste" ved fjernelse fra køen
- Usenet Downloadklient rapporterede fejl ved download af udgivelse