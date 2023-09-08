---
title: Calendrier Sonarr
description: 
published: true
date: 2022-04-26T01:49:26.770Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-06-11T23:31:36.392Z
---

# Calendrier

Le calendrier vous montre les épisodes récemment diffusés, ainsi que les épisodes à venir.

# Flux iCal

- Sonarr peut fournir votre calendrier sous forme de flux iCal. Celui-ci contiendra les [7 derniers jours](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35) précédents et les [28 prochains jours](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36).

> Google Calendar rencontre des problèmes internes qui font qu'il ne se met plus à jour. Il s'agit d'un problème de Google et non de Sonarr. Il peut souvent être résolu en supprimant et en réajoutant le calendrier.
{.is-warning}