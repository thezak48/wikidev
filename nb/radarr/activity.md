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

Aktivitet-fanen er der du kan se tidligere og nåværende aktiviteter som \*Arr har gjort. Dette inkluderer importeringer, slettinger, oppgraderinger, henting, omdøpinger og feil.

# Kø

Når noe lastes ned og ikke er importert til \*Arr ennå, vil det vises på Kø-siden.

Køen viser alle elementer som applikasjonen kan gjenkjenne og som er i den angitte nedlastingsklientens kategori (Innstillinger => Nedlastingsklient => Kategori). For å se alle utgivelser, gå til Alternativer => Vis Ukjent. Køen lagres ikke noe sted i applikasjonen, men oppdateres via API-responsene fra nedlastingsklienten din.

> For Usenet-klienter vil \*Arr bare se 60 elementer dypt i køen for potensielle importeringer! Det er viktig å ikke overstige dette, ellers må du rydde opp med manuelle importeringer når systemet ditt blir overbelastet og begynner å gå glipp av elementer!.
> Fjern fullførte nedlastinger bør også være aktivert for nedlastingsklienten din. {.is-warning}

## Ikonhandlinger i Køen

- X - Fjern element fra køen
  - Fjern utgivelse fra nedlastingsklient - Fjern utgivelse fra nedlastingsklienten. Obligatorisk for uoverensstemmende utgivelseselementer
  - Legg utgivelse til blokkeringsliste - Legg utgivelse til blokkeringslisten
- Menneskeikon - Manuell importering av utgivelse
- Hent ikon - Send utgivelse til nedlastingsklient

## Køstatus

> Merk at det nedenfor er ufullstendig {.is-warning}

| Ikon       | Status                   | Beskrivelse                                                                                     | Løsningssteg                                             |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| grå klokke | Utgivelse venter          | Nedlastingen venter på at nedlastingsklienten skal være tilgjengelig eller at utgivelsen skal oppfylle reglene for forsinkelsesprofilen | N/A                                                      |
| gul        | Advarsel: Kan ikke importere | \*Arr kunne ikke importere utgivelsen. Se verktøytips for mer informasjon                    | [Se feilsøkingsveiledningen](/radarr/troubleshooting) |
| lilla      | Importerer nedlasting    | Nedlastingen importeres                                                                           | N/A                                                      |
|            |                          |                                                                                                 |                                                          |
|            |                          |                                                                                                 |                                                          |

# Historikk

Historikkfanen viser alt som har forlatt køen ved at oppgaven er fullført/avsluttet. Dette inkluderer importeringer, feil, hentinger, slettinger og oppgraderinger.

Det venstre ikonet er handlingen som ble utført (listen over mulige handlinger vises nedenfor). Du kan filtrere disse ved å klikke på filterikonet på høyre side. Du kan også vise flere kolonner ved å klikke på Alternativer.

![history2.png](/assets/radarr/history2.png)

På statusene `Hentet` kan du klikke på `i`-ikonet på høyre side for å se flere detaljer om nedlastingen (hvilken indekser den kom fra, URL-en til hentingen, alderen til opplastingen osv.). Du kan også merke dette elementet som mislykket for å starte fjerning, blokkering og ny søk etter elementet.

![history4.png](/assets/radarr/history4.png)

# Blokkeringsliste

> Blokkeringslisten var tidligere kjent som 'Svarteliste' {.is-info}

Blokkeringslistesiden viser elementer som er blokkert slik at de ikke blir lastet ned igjen. Dette er feil fra den automatiske prosessen eller manuelt merkede mislykkede elementer. Elementer forblir i blokkeringslisten for alltid med mindre du fjerner dem manuelt.

![blocklist1.png](/assets/radarr/blocklist1.png)

Ved å klikke på `i`-ikonet helt til høyre vises flere detaljer om oppføringen i blokkeringslisten, og om den ble merket som mislykket manuelt eller automatisk mislykket under nedlastingen.

![blocklist2.png](/assets/radarr/blocklist2.png)

Ved å klikke på `x` helt til høyre fjerner du elementet fra blokkeringslisten, slik at du potensielt kan hente det igjen hvis det ble lagt til ved en feil.

## Vanlige årsaker til blokkering

- Bruker merket nedlastingen som mislykket manuelt
- Bruker valgte "Legg til blokkeringsliste" ved fjerning fra køen
- Usenet-nedlastingsklienten rapporterte feil ved nedlasting av utgivelsen