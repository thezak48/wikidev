---
title: Sonarr Kalender
description: 
published: true
date: 2022-04-26T01:49:26.770Z
tags: sonarr, behöver-kärlek
editor: markdown
dateCreated: 2021-06-11T23:31:36.392Z
---

# Kalender

Kalendern visar nyligen sända avsnitt samt kommande avsnitt.

# iCal-flöde

- Sonarr kan tillhandahålla din kalender som ett iCal-flöde. Detta kommer att innehålla de senaste [7 dagarna](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35) och de kommande [28 dagarna](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36)

> Google Kalender har interna problem som gör att den inte längre uppdateras. Detta är ett problem med Google och inte med Sonarr. Det kan ofta lösas genom att ta bort och lägga till kalendern igen.
{.is-warning}