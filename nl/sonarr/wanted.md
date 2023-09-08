---
title: Sonarr Gewenst
description: 
published: true
date: 2021-11-29T22:12:55.806Z
tags: sonarr, needs-love, gewenst
editor: markdown
dateCreated: 2021-06-10T01:40:02.329Z
---

# Gewenst

De sectie Gewenst => Ontbrekend bevat een lijst met afleveringen die je hebt gemarkeerd om te volgen en die nog ontbreken op je schijf (nog niet gedownload).

> Dit bevat alleen afleveringen die volledig ontbreken op je schijf, niet afleveringen die wel op de schijf staan maar waarvan het afsnijprofiel niet wordt voldaan.
{.is-info}

- "Geselecteerd zoeken" - Hier kun je bepaalde afleveringen selecteren als je ze wilt zoeken met je indexers.

- "Geselecteerde niet volgen" - Hier kun je bepaalde afleveringen selecteren en ze niet meer volgen als je er niet langer in geïnteresseerd bent.

- "Alles zoeken" - Als je dit selecteert, wordt er een zoekopdracht gestuurd naar al je indexers voor alle ontbrekende afleveringen. Zodra je op de knop drukt, verschijnt er een dialoogvenster met een waarschuwing waarin wordt aangegeven hoeveel afleveringen er worden gezocht. Dit is vooral handig om te weten als je indexers je API-oproepen beperken.

> Dit zoekproces kan niet worden geannuleerd nadat het is gestart zonder Sonarr opnieuw te starten.
{.is-info}

Bovenaan de pagina staat `Handmatig importeren`, waarmee je willekeurig mediabestanden kunt importeren vanuit elke locatie waar Sonarr toegang toe heeft voor series die al in Sonarr bestaan.

- "Automatisch verplaatsen" zal proberen om de bestanden automatisch te koppelen aan series/afleveringen in Sonarr en zal ze verplaatsen - niet kopiëren of hardlinken - naar je bibliotheekmap.
- "Interactieve import" stelt je in staat om de overeenkomsten te bekijken en verschillende specificaties aan te passen indien nodig. Het biedt de optie (linksonder) om je bestanden te `Verplaatsen` of `Kopiëren/Hardlinken`. Zorg ervoor dat je de juiste optie kiest voor jouw behoeften.
  
  > Als een map meer dan 100 bestanden bevat, zal Sonarr de map niet recursief doorzoeken en zal het ook niet proberen om de bestanden te analyseren en te koppelen. {.is-info}

# Afsnijprofiel niet voldaan

De sectie Gewenst => Afsnijprofiel niet voldaan bevat een lijst met afleveringen die nog niet aan hun afsnijprofiel voldoen. Het afsnijprofiel wordt ingesteld in je profielen.

Het afsnijprofiel is waar je in feite aan Sonarr aangeeft dat de kwaliteit van het videobestand goed genoeg is voor jou en dat je niet langer wilt dat Sonarr blijft zoeken naar betere kwaliteit.

Op deze pagina heb je een paar opties tot je beschikking
![wanted-cut-off-unmet.png](/assets/sonarr/wanted-cut-off-unmet.png)

1. Geselecteerd zoeken - Door afleveringen op je lijst te selecteren, kun je een automatische zoekopdracht uitvoeren om te zien of er upgrades zijn voor je bestaande bestanden.
1. Geselecteerde niet volgen - Door bepaalde afleveringen op je lijst te selecteren, kun je Sonarr vertellen om niet langer te zoeken naar upgrades door die aflevering niet meer te volgen.
1. Alles zoeken - Dit kan gevaarlijk zijn (afhankelijk van de grootte van je lijst), omdat je Sonarr vertelt om elk bestand dat niet aan het afsnijprofiel voldoet te doorzoeken. Dit kan handig zijn als je geen enorme lijst hebt.
1. Filter - Hiermee kun je je resultaten filteren. Dit is handig als je een specifieke set afleveringen of series wilt zoeken.