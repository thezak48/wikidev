---
title: Sonarr日历
description: 
published: true
date: 2022-04-26T01:49:26.770Z
tags: sonarr, 需要改进
editor: markdown
dateCreated: 2021-06-11T23:31:36.392Z
---

# 日历

日历会显示最近播出的剧集以及即将播出的剧集。

# iCal 订阅

- Sonarr可以提供你的日历作为iCal订阅。其中包含了过去的[7天](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35)和接下来的[28天](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36)。

> Google日历存在内部问题，导致其不再更新。这是一个Google的问题，而不是Sonarr的问题。通常可以通过删除并重新添加日历来解决此问题。
{.is-warning}