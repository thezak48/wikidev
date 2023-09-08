---
title: Sonarr Efterspurgte
description: 
published: true
date: 2021-11-29T22:12:55.806Z
tags: sonarr, needs-love, wanted
editor: markdown
dateCreated: 2021-06-10T01:40:02.329Z
---

# Efterspurgte

Sektionen Efterspurgte => Manglende indeholder en liste over episoder, som du har markeret til overvågning, men som mangler på din disk (ikke er blevet downloadet endnu).

> Dette vil kun omfatte episoder, der er helt manglende på din disk, ikke episoder, der findes på disken, men hvor deres cutoff-profil ikke er opfyldt.
{.is-info}

- "Søg valgte" - Her kan du vælge bestemte episoder, hvis du ønsker at søge efter dem med dine indexere.

- "Fjern overvågning af valgte" - Her kan du vælge bestemte episoder og fjerne overvågningen af dem, hvis du ikke længere er interesseret i dem.

- "Søg alle" - Ved at vælge dette vil der blive sendt en søgning til alle dine indexere for alle aktuelle manglende episoder. Når du trykker på knappen, vil der dukke en dialogboks op med en advarsel til dig, der fortæller dig, hvor mange episoder der vil blive søgt efter. Dette er særligt nyttigt at vide, hvis dine indexere begrænser dine API-opkald.

> Denne søgeproces kan ikke annulleres, når den er startet, uden at genstarte Sonarr.
{.is-info}

Øverst på siden er der `Manuel import`, som giver dig mulighed for at importere mediefiler vilkårligt fra enhver destination, som Sonarr kan få adgang til, for serier, der allerede findes i Sonarr.

- "Flyt automatisk" vil forsøge at matche filerne automatisk til serier/episoder i Sonarr og flytte dem - ikke kopiere eller lave hardlinks - til din biblioteksmappe.
- "Interaktiv import" giver dig mulighed for at gennemgå matchene og justere forskellige specifikationer efter behov. Det giver mulighed for at "Flytte" eller "Kopiere/Hardlinke" dine filer (nederst i venstre hjørne). Sørg for at vælge den korrekte mulighed for dine behov.
  
  > Hvis en mappe har mere end 100 filer i sig, vil Sonarr ikke søge rekursivt i mappen eller forsøge at analysere og matche filerne.
{.is-info}

# Cutoff ikke opfyldt

Sektionen Efterspurgte => Cutoff ikke opfyldt indeholder en liste over episoder, der endnu ikke har nået deres cutoff. Cutoff'en er indstillet i dine profiler.

Cutoff'en er det punkt, hvor du fortæller Sonarr, at kvaliteten af videofilen er god nok for dig, og at du ikke længere ønsker, at Sonarr skal fortsætte med at søge efter noget bedre.

Der er et par muligheder tilgængelige for dig på denne side
![wanted-cut-off-unmet.png](/assets/sonarr/wanted-cut-off-unmet.png)

1. Søg valgte - Ved at vælge episoder på din liste kan du udføre en automatisk søgning for at se, om der er nogen opgraderinger til dine eksisterende filer.
1. Fjern overvågning af valgte - Ved at vælge visse episoder på din liste kan du fortælle Sonarr, at den ikke længere skal lede efter opgraderinger ved at fjerne overvågningen af den pågældende episode.
1. Søg alle - Dette kan være farligt (afhængigt af hvor stor din liste er), da du fortæller Sonarr at søge i alle filer, der ikke har opfyldt cutoff'en. Dette kan være nyttigt, hvis du ikke har en massiv liste.
1. Filtrer - Dette giver dig mulighed for at filtrere dine resultater. Dette er nyttigt, hvis du ønsker at søge efter en bestemt række episoder eller serier.