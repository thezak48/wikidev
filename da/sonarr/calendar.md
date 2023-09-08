---
title: Sonarr Kalender
description: 
published: true
date: 2022-04-26T01:49:26.770Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-06-11T23:31:36.392Z
---

# Kalender

Kalenderen viser dig nyligt udsendte episoder samt kommende episoder.

# iCal-feed

- Sonarr kan give dig din kalender som en iCal-feed. Denne vil indeholde de foregående [7 dage](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35) og de næste [28 dage](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36).

> Google Kalender har interne problemer, der resulterer i, at den ikke længere opdateres. Dette er et problem hos Google og ikke hos Sonarr. Det kan ofte løses ved at fjerne og tilføje kalenderen igen.
{.is-warning}