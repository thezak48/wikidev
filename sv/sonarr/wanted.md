---
title: Sonarr Eftersökt
description: 
published: true
date: 2021-11-29T22:12:55.806Z
tags: sonarr, behöver-kärlek, eftersökt
editor: markdown
dateCreated: 2021-06-10T01:40:02.329Z
---

# Eftersökt

Avsnitt som saknas i avsnittet Eftersökt => Saknas innehåller en lista över avsnitt som du har markerat för övervakning och som saknas på din hårddisk (har ännu inte laddats ner).

> Detta inkluderar endast avsnitt som helt saknas på din hårddisk, inte avsnitt som finns på hårddisken men inte uppfyller ditt avskärningsprofil.
{.is-info}

- "Sök valda" - Här kan du välja vissa avsnitt om du vill söka efter dem med dina indexerare.

- "Avmarkera valda" - Här kan du välja vissa avsnitt och avmarkera dem om du inte längre är intresserad av dem.

- "Sök alla" - Om du väljer detta skickas en sökning till alla dina indexerare för alla aktuella saknade avsnitt. När du trycker på knappen visas en dialogruta med en varning som informerar dig om hur många avsnitt som kommer att sökas; detta är särskilt användbart att veta om dina indexerare begränsar dina API-anrop.

> Denna sökningsprocess kan inte avbrytas när den har startat utan att starta om Sonarr.
{.is-info}

Överst på sidan finns `Manuell import` som gör att du kan godtyckligt importera mediefiler från vilken destination som helst som Sonarr kan komma åt för serier som redan finns i Sonarr.

- Flytta automatiskt kommer att försöka matcha filerna automatiskt med serier/avsnitt i Sonarr och flytta dem - inte kopiera eller skapa hårda länkar - till din biblioteksmapp.
- Interaktiv import kommer att låta dig granska matchningarna och justera olika specifikationer vid behov. Det ger möjligheten (nederst till vänster) att `Flytta` eller `Kopiera/Skapa hårda länkar` för dina filer. Se till att välja rätt alternativ för dina behov.
  
  > Om en mapp innehåller mer än 100 filer kommer Sonarr inte att söka mappen rekursivt eller försöka tolka och matcha filerna.
{.is-info}

# Avskärning inte uppfylld

Avsnitt som inte uppfyller avskärningen i avsnittet Eftersökt => Avskärning inte uppfylld innehåller en lista över avsnitt som ännu inte har nått sin avskärning. Avskärningen ställs in i dina profiler.

Avskärningen är där du i princip berättar för Sonarr att videofilen har tillräckligt bra kvalitet för dig och att du inte längre vill att Sonarr ska fortsätta söka efter bättre kvalitet.

Det finns några alternativ tillgängliga för dig på denna sida
![wanted-cut-off-unmet.png](/assets/sonarr/wanted-cut-off-unmet.png)

1. Sök valda - Genom att välja avsnitt på din lista kan du utföra en automatisk sökning för att se om det finns några uppgraderingar till dina befintliga filer.
1. Avmarkera valda - Genom att välja vissa avsnitt på din lista kan du tala om för Sonarr att inte längre leta efter några uppgraderingar genom att avmarkera det avsnittet.
1. Sök alla - Detta kan vara farligt (beroende på hur stor din lista är) eftersom du talar om för Sonarr att söka igenom varje fil som inte har uppfyllt avskärningen. Detta kan vara användbart om du inte har en massiv lista.
1. Filter - Detta gör att du kan filtrera dina resultat. Detta är användbart om du vill söka efter en specifik uppsättning avsnitt eller serier.