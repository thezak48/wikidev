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

Aktivitet-fanen er der du kan se tidligere og nåværende aktiviteter som \*Arr har gjort. Dette inkluderer importeringer, slettinger, oppgraderinger, henting, omdøpinger og feil.

# Kø

Når noe lastes ned og ikke er importert til \*Arr ennå, vil det vises på Kø-siden.

Køen viser alle elementer som applikasjonen kan gjenkjenne som er i den angitte nedlastingsklientens kategori (Innstillinger => Nedlastingsklient => Kategori). For å se alle utgivelser, velg Alternativer => Vis Ukjent. Køen lagres ikke noe sted i applikasjonen, men oppdateres via svar fra nedlastingsklientens API.

> For Usenet-klienter vil \*Arr bare se 60 elementer dypt i køen for potensielle importeringer! Det er viktig å ikke overskride dette, ellers må du rydde opp med manuelle importeringer når systemet ditt blir overbelastet og begynner å gå glipp av elementer!.
> Fjern fullførte nedlastinger bør også være aktivert for nedlastingsklienten din. {.is-warning}

## Handlingssymboler for Kø

- X - Fjern element fra køen
  - Fjern utgivelse fra nedlastingsklient - Fjern utgivelse fra nedlastingsklient. Obligatorisk for uoverensstemmende utgivelser
  - Legg utgivelse til blokkeringsliste - Legg utgivelse til blokkeringsliste
- Menneskeikon - Manuell importering av utgivelse
- Hentikon - Send utgivelse til nedlastingsklient

## Køstatus

> Merk at nedenstående er ufullstendig {.is-warning}

| Ikon       | Status                   | Beskrivelse                                                                                     | Løsningsforslag                                          |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| grå klokke | Utgivelse venter          | Nedlastingen venter på at nedlastingsklienten skal være tilgjengelig eller at utgivelsen skal oppfylle forsinkelsesprofilreglene | N/A                                                       |
| gul        | Advarsel, kan ikke importere | \*Arr kunne ikke importere utgivelsen. Se verktøytips for mer informasjon                    | [Se feilsøkingsveiledningen](/readarr/troubleshooting) |
| lilla      | Importerer nedlasting       | Nedlastingen importeres                                                                           | N/A                                                       |
|            |                          |                                                                                                 |                                                           |
|            |                          |                                                                                                 |                                                           |

# Historikk

Historikkfanen viser alt som har forlatt køen ved at oppgaven er fullført/avsluttet. Dette inkluderer importeringer, feil, hentinger, slettinger og oppgraderinger.

Det venstre ikonet er handlingen som ble utført (listen over mulige handlinger vises nedenfor). Du kan filtrere disse ved å klikke på filterikonet på høyre side. Du kan også vise flere kolonner ved å klikke på Alternativer.

![history2.png](/assets/readarr/history2.png)

På statusene `Hentet` kan du klikke på `i`-ikonet på høyre side for å se flere detaljer om nedlastingen (hvilken indekser den kom fra, URL-en til hentingen, alderen til opplastingen osv.). Du kan også merke dette elementet som mislykket for å starte fjerning, blokkering og ny søk etter elementet.

![history4.png](/assets/readarr/history4.png)

# Blokkeringsliste

> Blokkeringsliste ble tidligere kalt 'Svarteliste' {.is-info}

Blokkeringslistesiden viser elementer som er blokkert slik at de ikke blir lastet ned igjen. Dette er feil fra den automatiske prosessen eller manuelt merkede mislykkede elementer. Elementer forblir i blokkeringslisten for alltid med mindre du fjerner dem manuelt.

![blocklist1.png](/assets/readarr/blocklist1.png)

Ved å klikke på `i`-ikonet helt til høyre får du mer detaljer om oppføringen i blokkeringslisten, og om den ble merket som mislykket manuelt eller automatisk mislykket under nedlastingen.

![blocklist2.png](/assets/readarr/blocklist2.png)

Ved å klikke på `x` helt til høyre fjerner du elementet fra blokkeringslisten, slik at du potensielt kan hente det igjen hvis det ble lagt til ved en feil.

## Vanlige årsaker til blokkering

- Bruker merket nedlastingen som mislykket manuelt
- Bruker valgte "Legg til blokkeringsliste" ved fjerning fra køen
- Usenet-nedlastingsklienten rapporterte nedlastingsfeil for utgivelsen