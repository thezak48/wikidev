---
title: Sonarr カレンダー
description: 
published: true
date: 2022-04-26T01:49:26.770Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-06-11T23:31:36.392Z
---

# カレンダー

カレンダーでは、最近放送されたエピソードと今後のエピソードを表示します。

# iCal フィード

- Sonarr はカレンダーを iCal フィードとして提供することができます。これには、[過去7日間](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35)と[次の28日間](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36)が含まれます。

> Google カレンダーには内部の問題があり、更新が行われなくなることがあります。これは Google の問題であり、Sonarr の問題ではありません。カレンダーを削除して再追加することで解決することがあります。
{.is-warning}