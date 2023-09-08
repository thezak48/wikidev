---
title: Sonarr Wanted
description: 
published: true
date: 2021-11-29T22:12:55.806Z
tags: sonarr, needs-love, wanted
editor: markdown
dateCreated: 2021-06-10T01:40:02.329Z
---

# Ønsket

Wanted => Mangler-seksjonen inneholder en liste over episoder du har merket for overvåking som mangler på disken din (har ikke blitt lastet ned ennå).

> Dette vil bare inkludere episoder som er helt fraværende fra disken din, ikke episoder som eksisterer på disken, men som ikke oppfyller kuttprofilen sin.
{.is-info}

- "Søk valgte" - Her kan du velge visse episoder hvis du ønsker å søke etter dem med indekserne dine.

- "Slutt å overvåke valgte" - Her kan du velge visse episoder og slutte å overvåke dem hvis du ikke lenger er interessert i dem.

- "Søk alle" - Hvis du velger dette, vil det sende en søk til alle indekserne dine for alle gjeldende manglende episoder. Når du trykker på den, vil en dialogboks dukke opp med en advarsel til deg, som forteller deg hvor mange episoder som vil bli søkt etter. Dette er spesielt nyttig å vite hvis indekserne dine begrenser API-kallene dine.

> Denne søkeprosessen kan ikke avbrytes når den er startet uten å starte Sonarr på nytt.
{.is-info}

Øverst på siden er `Manuell import` som lar deg vilkårlig importere mediefiler fra hvilken som helst destinasjon Sonarr kan få tilgang til for serier som allerede eksisterer i Sonarr.

- "Flytt automatisk" vil forsøke å automatisk matche filene til serier/episoder i Sonarr og vil flytte - ikke kopiere eller hardlenke - dem til biblioteksmappen din.
- "Interaktiv import" vil la deg gjennomgå kampene og justere ulike spesifikasjoner etter behov. Det gir deg muligheten (nederst til venstre) til å `Flytte` eller `Kopiere/Hardlenke` filene dine. Pass på å velge riktig alternativ for dine behov.
  
  > Hvis en mappe har mer enn 100 filer i seg, vil Sonarr ikke søke rekursivt i mappen eller forsøke å analysere og matche filene.
{.is-info}

# Kuttprofil ikke oppfylt

Wanted => Kuttprofil ikke oppfylt-seksjonen inneholder en liste over episoder som ennå ikke har nådd kuttprofilen sin. Kuttprofilen er satt opp i profilene dine.

Kuttprofilen er der du i praksis forteller Sonarr at kvaliteten på videofilen er god nok for deg, og du ønsker ikke lenger at Sonarr skal fortsette å lete etter bedre kvalitet.

Det er et par alternativer tilgjengelig for deg på denne siden
![wanted-cut-off-unmet.png](/assets/sonarr/wanted-cut-off-unmet.png)

1. Søk valgte - Ved å velge episoder på listen din kan du utføre et automatisk søk for å se om det er noen oppgraderinger til eksisterende filer.
1. Slutt å overvåke valgte - Ved å velge visse episoder på listen din kan du fortelle Sonarr å ikke lenger lete etter oppgraderinger ved å slutte å overvåke den episoden.
1. Søk alle - Dette kan være farlig (avhengig av hvor stor listen din er), da du forteller Sonarr å søke gjennom hver fil som ikke har oppfylt kuttprofilen. Dette kan være nyttig hvis du ikke har en massiv liste.
1. Filtrer - Dette vil tillate deg å filtrere resultatene dine. Dette er nyttig hvis du ønsker å søke etter en bestemt serie eller sett med episoder.