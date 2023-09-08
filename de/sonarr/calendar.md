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

Der Kalender zeigt dir kürzlich ausgestrahlte Episoden sowie kommende Episoden an.

# iCal-Feed

- Sonarr kann deinen Kalender als iCal-Feed bereitstellen. Dieser enthält die vorherigen [7 Tage](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35) und die nächsten [28 Tage](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36).

> Google Kalender hat interne Probleme, die dazu führen, dass er nicht mehr aktualisiert wird. Dies ist ein Problem von Google und nicht von Sonarr. Oft kann das Problem behoben werden, indem der Kalender entfernt und erneut hinzugefügt wird.
{.is-warning}