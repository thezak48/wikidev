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

Kalenderen viser deg nylig sendte episoder, samt kommende episoder.

# iCal-feed

- Sonarr kan gi deg kalenderen din som en iCal-feed. Denne vil inneholde de siste [7 dagene](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35) og de neste [28 dagene](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36)

> Google Calendar har interne problemer som resulterer i at den ikke lenger oppdateres. Dette er et problem med Google og ikke Sonarr. Det kan ofte løses ved å fjerne og legge til kalenderen på nytt.
{.is-warning}