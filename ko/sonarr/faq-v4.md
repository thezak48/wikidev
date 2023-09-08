---
title: Sonarr v4 Beta FAQ
description: Sonarr v4 Beta FAQ
published: true
date: 2023-08-28T19:29:38.774Z
tags: 
editor: markdown
dateCreated: 2022-11-25T14:02:10.493Z
---

# Sonarr v4 Beta FAQ

> Sonarr v4는 현재 베타 버전으로, 따라서 오류와 문제가 예상됩니다. v4 베타에 대한 질문, 문제 보고 또는 피드백을 위해 지원 채널을 사용해주세요. 필요한 경우, [Github](https://github.com/Sonarr/Sonarr)에서 이슈를 열라고 요청될 수 있습니다. 원래의 토론 링크와 요청된 모든 정보와 함께 링크를 제공해주세요. {.is-warning}

## 변경 사항

자세한 내용은 [v4 베타 공지](https://www.reddit.com/r/sonarr/comments/z3nb82/sonarr_v4_beta/)를 참조하세요.

다음은 주요 변경 사항 및 더 중요한 변경 사항입니다:

- [강제 인증](#강제-인증)
- Mono => Dotnet (더 빠른 속도; 더 이상 mono 사용 안 함). 이 변경으로 인해 Reverse Proxy 구성 업데이트가 필요할 수 있습니다:
  - [Nginx](#nginx)
  - [Apache](#apache)
- [선호하는 단어가 사라짐](#선호하는-단어를-사용자-정의-형식으로-마이그레이션) 및 사용자 정의 형식으로 대체됨
- [언어 프로필이 사라짐](#언어-프로필이-어디로-갔나요) 및 사용자 정의 형식으로 대체됨
- 다크/라이트 테마
- SysLog 및 인스턴스 이름 지원
- Mass Editor가 [시리즈 개요](#대량 편집기가-어디로-갔나요)로 통합됨
- 훨씬 더 많은 변경 사항

## 강제 인증

Sonarr의 UI에 외부 네트워크에서 액세스할 수 있도록 노출되어 있다면, UI에 액세스하기 위해 인증 방법을 활성화해야 합니다. 이는 트래커 및 인덱서에서도 점점 더 필요로 됩니다.

Sonarr v4부터 인증은 필수입니다.

### 인증 방법

- `Basic` (브라우저 팝업) - Sonarr에 액세스할 때 작은 팝업이 표시되어 사용자 이름과 비밀번호를 입력할 수 있도록 합니다.
- `Forms` (로그인 페이지) - 이 옵션은 Sonarr에 로그인할 수 있도록 다른 웹 사이트와 유사한 로그인 화면을 제공합니다.
- `External` - 구성 파일에서만 구성 가능
  - Authelia, Authetik, NGINX 기본 인증 등과 같은 **외부 인증**을 사용하는 경우, 앱을 종료하고 [구성 파일](/sonarr/appdata-directory)에서 `<AuthenticationMethod>External</AuthenticationMethod>`를 설정한 다음 앱을 다시 시작하여 이중 인증을 방지할 수 있습니다. **파일에 여러 `AuthenticationMethod` 항목을 지원하지 않으며, 최상위 값만 사용됩니다**

### 인증 필요 여부

- 앱을 외부에 노출시키지 않거나 로컬(예: LAN) 액세스에 대해 인증이 필요하지 않으려면 설정 => 일반 보안 => 인증 필요 항목을 `로컬 주소에 대해 비활성화`로 변경하세요.
  - 이에 해당하는 구성 파일은 `<AuthenticationType>DisabledForLocalAddresses</AuthenticationType>`입니다.

## 선호하는 단어를 사용자 정의 형식으로 마이그레이션

선호하는 단어 시스템은 사용자 정의 형식 시스템으로 대체되었습니다. 이를 통해 Sonarr가 내릴 수 있는 결정에 훨씬 더 세분화된 설정이 가능해집니다. 선호하는 단어는 모든 품질 프로필에 적용되었지만, 사용자 정의 형식은 각 품질 프로필에 대해 다른 중요도 수준을 지정할 수 있습니다.

사용자 정의 형식에는 선호하는 단어 시스템과 달리 선호도 수준을 지정할 수 있으므로 원하는 선호도 수준에 도달하면 업그레이드가 중단되도록 설정할 수 있습니다. 예전의 선호하는 단어 시스템은 더 나은 릴리스가 발견되면 항상 업그레이드되었습니다.

### 포함(하지 않음)

포함(해야 함) 및 포함하지 않아야 하는 사항은 v3와 마찬가지로 릴리스 프로필 설정에 유지됩니다.

### 파일 이름 토큰

`{Preferred Words}` 파일 이름 토큰은 파일 이름의 정규식 항목과 일치하는 용어를 사용했습니다.
`{Custom Formats}` 파일 이름 토큰은 파일 이름에 사용되는 사용자 정의 형식 이름을 사용합니다.

> 업그레이드하기 전에 선호하는 단어 릴리스 프로필을 스크린샷 또는 제거하는 것이 좋습니다. 각 선호하는 단어 라인은 마이그레이션 후에 자체 사용자 정의 형식이 됩니다.
{.is-warning}

## 언어 프로필이 어디로 갔나요?

Sonarr v4에서 언어는 다르게 처리됩니다. 이제 이전의 언어 프로필 시스템으로 관리되지 않고, 사용자 정의 형식의 일부가 되었습니다. 원하는 언어를 가져오기 위해 사용자 정의 형식을 생성한 다음, 해당 사용자 정의 형식을 원하는 등급으로 품질 프로필에 추가해 해당 언어의 가져오기를 강제할 수 있습니다.

> TRaSH Guide의 [언어 사용자 정의 형식 설정 방법](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/)을 참조하세요.
{.is-info}

### 영어만

**[TRaSH => 언어: 영어만](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-english-only)**

영어로만 릴리스를 가져오려면 다음 사용자 정의 형식을 사용할 수 있습니다. 이 사용자 정의 형식을 가져오고, 각 품질 프로필에 -10000의 점수로 할당하세요. 최소 사용자 정의 형식 점수가 0이라고 가정하면, 이렇게 하면 영어로 파싱되지 않은 모든 릴리스가 거부됩니다.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "언어: 영어만",
  "name": "언어: 영어 아님",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "영어 아닌 언어",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": 1
      }
    }
  ]
}
```

### 원본만

**[TRaSH => 언어: 원본만](https://trash-guides.info/Sonarr/Tips/How-to-setup-language-custom-formats/#language-original-only)**

시리즈의 TVDb 원본 언어로만 릴리스를 가져오려면 다음 사용자 정의 형식을 사용할 수 있습니다. 이 사용자 정의 형식을 가져오고, 각 품질 프로필에 -10000의 점수로 할당하세요. 최소 사용자 정의 형식 점수가 0이라고 가정하면, 이렇게 하면 TVDb 원본 언어로 파싱되지 않은 모든 릴리스가 거부됩니다.

```json
{
  "trash_id": "guide-only",
  "trash_score": "-10000",
  "trash_description": "언어: 원본만",
  "name": "언어: 원본 아님",
  "includeCustomFormatWhenRenaming": false,
  "specifications": [
    {
      "name": "원본 아닌 언어",
      "implementation": "LanguageSpecification",
      "negate": true,
      "required": false,
      "fields": {
        "value": -2
      }
    }
  ]
}
```

## 내 Reverse Proxy가 더 이상 작동하지 않나요?

Sonarr의 백엔드 변경(모노에서 닷넷으로 마이그레이션)으로 인해 더 이상 작동하지 않을 수 있습니다.

### Nginx

  Nginx 구성 파일을 변경해야 합니다. 다음 줄을 바꿔주세요:
  
  ```nginx
     proxy_set_header   Host $proxy_host;
  ```

  다음 줄로 바꿔주세요:

  ```nginx
    proxy_set_header   Host $host;
  ```

### Apache

  Apache 가상 호스트 구성 파일을 변경해야 합니다. 다음 줄을 추가해주세요:

 ```apache2
      ProxyPreserveHost On
 ```

## 이 새로운 "*Override and add to download queue*" 버튼은 무엇인가요?

대화식 검색을 수행할 때 "Override and add to download queue"라는 두 번째 다운로드 버튼이 추가되었습니다. 이 버튼을 사용하면 두 가지 작업을 수행할 수 있습니다:

- 다운로드가 전송될 다운로드 클라이언트를 선택할 수 있습니다. 이는 동일한 프로토콜에 대해 여러 다운로드 클라이언트(예: 여러 토렌트 클라이언트 인스턴스)를 가지고 있는 경우 Sonarr이 어떤 클라이언트를 사용할지 결정하는 대신 직접 선택할 수 있습니다.
- Sonarr이 릴리스 제목을 잘못 파싱하거나 파싱할 수 없는 경우에 Sonarr의 파싱을 무시하고 릴리스를 가져오고 싶은 경우. 다음 파싱된 필드를 무시할 수 있습니다:
  - 시리즈
  - 시즌 번호
  - 에피소드
  - 품질
  - 언어

## 대량 편집기가 어디로 갔나요?

대량 편집기 독립 페이지가 제거되고 해당 기능이 시리즈 개요 페이지로 통합되었습니다. 쇼를 대량으로 편집하려면 먼저 시리즈 개요 상단의 `Select Series` 버튼을 클릭하고 편집하려는 쇼를 선택하세요.

시즌 패스 페이지도 제거되었습니다. 일부 기능은 시리즈 개요 편집기에 남아 있으며, 테이블 보기를 선택하고 `Select Series`를 누르세요. 선택 모드에서는 시즌 열의 숫자 위로 마우스를 가져가 해당 쇼의 시즌 패스 팝오버에 액세스할 수 있습니다.

## 에피소드의 실행 시간이 0으로 표시됩니다

v4는 TVDb의 에피소드별 실행 시간을 사용합니다. 에피소드의 실행 시간이 0인 경우, 시리즈의 실행 시간으로 대체하려고 시도합니다.
시리즈의 실행 시간도 0인 경우, Sonarr은 첫 번째 에피소드가 방영된 24시간 이내에 방영된 모든 에피소드에 대해 45분의 실행 시간을 사용합니다.