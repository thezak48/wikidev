---
title: Sonarr 캘린더
description: 
published: true
date: 2022-04-26T01:49:26.770Z
tags: sonarr, needs-love
editor: markdown
dateCreated: 2021-06-11T23:31:36.392Z
---

# 캘린더

캘린더는 방영된 최신 에피소드와 예정된 에피소드를 보여줍니다.

# iCal 피드

- Sonarr는 캘린더를 iCal 피드로 제공할 수 있습니다. 이 피드에는 이전 [7일](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L35)과 다음 [28일](https://github.com/Sonarr/Sonarr/blob/22f044844c33187450dcc2d6b329ad3e1d241e74/src/NzbDrone.Api/Calendar/CalendarFeedModule.cs#L36)이 포함됩니다.

> Google 캘린더에는 업데이트되지 않는 내부 문제가 있습니다. 이는 Google의 문제이며 Sonarr의 문제가 아닙니다. 캘린더를 제거하고 다시 추가함으로써 문제를 해결할 수 있습니다.
{.is-warning}