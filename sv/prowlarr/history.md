---
title: Prowlarr Historik
description: 
published: true
date: 2021-11-24T19:23:05.283Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:32:35.055Z
---

Denna sida visar hur du granskar och söker i din historik samt de olika tillgängliga inställningarna.

# Öppna historik

För att komma till historikskärmen, klicka på `Historik` i vänstermenyn.

![hist_1_history.png](/assets/prowlarr/hist_1_history.png)

# Menyalternativ

På toppen av skärmen finns olika menyalternativ:

- Uppdatera låter dig dynamiskt uppdatera historiken och se eventuella nya poster.
- Rensa låter dig rensa hela din historik.

> Var försiktig innan du rensar historiken. Den kommer att raderas helt och kan inte återställas!

- Alternativ låter dig ändra vilka kolumner som visas, ange antalet historikposter per sida och ange antalet dagar innan historiken rensas under schemalagda uppgifter.

- Filter låter dig filtrera historiken för olika typer av åtgärder, som sökningar, hämtningar, osv.

# RSS-sökningar

Automatiserade sökfrågor från dina appar ser ut så här:

![hist_2_search.png](/assets/prowlarr/hist_2_search.png)

Om du har valt kolumnerna kan du se vilken indexer som söktes, vilken kategori som användes, vilken app som gjorde förfrågan och hur lång tid det tog att slutföra frågan. Du kan också klicka på informationsikonen (`i`) till höger för att få mer specifik information. För RSS-flöden finns det ingen faktisk fråga, så det kommer att vara tomt.

![hist_3_rssquery.png](/assets/prowlarr/hist_3_rssquery.png)

# Sökningar med frågor

Specifika sökningar med frågor visar exakt vad som söktes, baserat på varje indexers kapabiliteter. Som du kan se nedan, söktes samma serie/avsnitt på 3 olika indexers, och var och en har olika kapabiliteter:

![hist_4_search.png](/assets/prowlarr/hist_4_search.png)

Om du klickar på informationsikonen (`i`) för någon av dessa sökningar kan du se antalet resultat som returnerades.

![hist_5_results.png](/assets/prowlarr/hist_5_results.png)