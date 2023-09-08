---
title: Lidarr Aktivitet
description: 
published: true
date: 2022-02-06T09:06:39.366Z
tags: lidarr, needs-love, activity
editor: markdown
dateCreated: 2021-06-14T21:35:25.390Z
---

# Aktivitet

Aktivitet fanen er, hvor du kan se tidligere og nuværende aktiviteter, som \*Arr har udført. Dette inkluderer importeringer, sletninger, opgraderinger, hentninger, omdøbninger og fejl.

# Kø

Når noget bliver downloadet og endnu ikke importeret til \*Arr, vil det blive vist på Kø siden.

Køen viser alle elementer, som applikationen kan genkende, der er i den specificerede downloadklients kategori (Indstillinger => Downloadklient => Kategori). For at se alle udgivelser skal du gå til Indstillinger => Vis Ukendte. Køen bliver ikke gemt nogen steder i applikationen, men bliver opdateret via API-respons fra din downloadklient.

> For Usenet-klienter vil \*Arr kun kigge 60 elementer dybt i køen for potentielle importeringer! Det er vigtigt ikke at overskride dette, ellers bliver du nødt til at rydde op med manuelle importeringer, når dit system bliver overbelastet og begynder at gå glip af elementer!.
> Fjern fuldførte downloads skal også være aktiveret for din downloadklient. {.is-warning}

## Handlingssymboler i Køen

- X - Fjern element fra køen
  - Fjern udgivelse fra downloadklient - Fjern udgivelse fra downloadklient. Obligatorisk for uoverensstemmende udgivelseselementer
  - Tilføj udgivelse til blokeringsliste - Tilføj udgivelse til blokeringsliste
- Menneskeikon - Manuel importering af udgivelse
- Hentikon - Send udgivelse til downloadklient

## Køstatusser

> Bemærk at nedenstående er ufuldstændigt {.is-warning}

| Ikon        | Status                   | Beskrivelse                                                                                     | Løsningsforslag                                          |
| ----------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Gråt ur     | Udlevering afventer      | Download afventer, at downloadklienten er tilgængelig, eller at udgivelsen opfylder forsinkelsesprofilregler | N/A                                                      |
| Gul         | Advarsel - Kan ikke importere | \*Arr kunne ikke importere udgivelsen. Se værktøjstip for flere detaljer                    | [Se fejlfindingssiden](/lidarr/troubleshooting) |
| Lilla       | Importering af download   | Download bliver importeret                                                                           | N/A                                                      |
|             |                          |                                                                                                 |                                                          |
|             |                          |                                                                                                 |                                                          |

# Historik

Historikfanen viser alt, der er blevet fjernet fra køen, fordi opgaven er blevet afsluttet. Dette inkluderer importeringer, fejl, hentninger, sletninger og opgraderinger.

Det venstre ikon er handlingen, der blev udført (listen over mulige handlinger vises nedenfor). Du kan filtrere disse ved at klikke på filterikonet i højre side. Du kan også vise flere kolonner ved at klikke på Indstillinger.

![history2.png](/assets/lidarr/history2.png)

På `Hentede` statusser kan du klikke på `i` ikonet til højre for at se flere detaljer om downloaden (hvilken indekser den kom fra, URL'en for hentningen, uploadets alder osv.). Du kan også markere dette element som mislykket for at starte en fjernelse, blokeringsliste og gen-søgning af elementet.

![history4.png](/assets/lidarr/history4.png)

# Blokeringsliste

> Blokeringsliste blev tidligere kaldt 'Sortliste' {.is-info}

Blokeringslistesiden viser elementer, der er blokeret, så de ikke bliver downloadet igen. Disse er fejl fra den automatiske proces eller manuelt markerede mislykkede elementer. Elementer forbliver på blokeringslisten for evigt, medmindre du fjerner dem manuelt.

![blocklist1.png](/assets/lidarr/blocklist1.png)

Ved at klikke på `i` ikonet helt til højre kan du se flere detaljer om det blokerede element og om det blev markeret som mislykket manuelt eller automatisk under download.

![blocklist2.png](/assets/lidarr/blocklist2.png)

Ved at klikke på `x` helt til højre fjerner du elementet fra blokeringslisten, så du potentielt kan hente det igen, hvis det blev tilføjet ved en fejl.

## Almindelige årsager til blokering

- Bruger markerede download som mislykket manuelt
- Bruger valgte "Tilføj til blokeringsliste" ved fjernelse fra køen
- Usenet-downloadklient rapporterede fejl ved download af udgivelse