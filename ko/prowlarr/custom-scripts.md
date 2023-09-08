# Prowlarr 사용자 지정 스크립트
---
title: Prowlarr 사용자 지정 스크립트
description: 
published: true
date: 2021-12-20T16:40:47.702Z
tags: prowlarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:40:30.916Z
---

사용자 지정 스크립트를 트리거하려면 여기에서 자세한 내용을 찾을 수 있습니다. 스크립트는 [연결 설정](/prowlarr/settings#connections)을 통해 Prowlarr에 추가됩니다.

# 개요

Prowlarr은 에피소드가 새로 가져오거나 이름이 변경될 때 사용자 지정 스크립트를 실행할 수 있습니다. 동작에 따라 다른 매개변수가 제공됩니다. 매개변수는 환경 변수를 통해 스크립트로 전달됩니다.

## Prowlarr 로그

다음은 사용자 지정 스크립트에 대해서만 로그에 기록됩니다:

- 스크립트의 `stdout` 출력은 `Debug`로 기록됩니다.
- 스크립트의 `stderr` 출력은 `Info`로 기록됩니다.
- 스크립트의 트리거는 `Trace`에 기록됩니다.

# 환경 변수

환경 변수는 이벤트 유형에 따라 다릅니다. 자세한 내용은 곧 업데이트될 예정입니다^tm^

> [현재 코드는 여기에서 확인할 수 있습니다. 위키 기여를 환영합니다](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## 테스트 시

Prowlarr에 스크립트를 추가하고 '테스트'를 클릭하면 다음과 같은 매개변수로 스크립트가 호출됩니다. 스크립트는 지원되지 않는 이벤트 유형을 우아하게 무시할 수 있어야 합니다.

| 환경 변수 | 세부 정보 |
| ---------- | --------- |
| `prowlarr_eventtype` | `Test`  |