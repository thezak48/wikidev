---
title: Sonarr 기여하기
description: 
published: true
date: 2023-09-03T13:55:05.394Z
tags: sonarr
editor: markdown
dateCreated: 2021-06-11T23:10:04.820Z
---

# 기여하는 방법

Sonarr을 더욱 개선하기 위해 도움을 주실 분들을 항상 찾고 있습니다. 기여할 수 있는 여러 가지 방법이 있습니다.

# 문서화

설치 가이드, [FAQ](/sonarr/faq), [위키](https://wiki.servarr.com/sonarr)에 있는 정보가 많을수록 좋습니다.

# 개발

Sonarr은 C# (백엔드)과 JS (프론트엔드)로 작성되었습니다. 백엔드는 .NET6 프레임워크로 구축되었으며, 프론트엔드는 Reactjs를 사용합니다.

## 필요한 도구

- Visual Studio 2022 이상을 권장합니다 (<https://www.visualstudio.com/vs/>). 커뮤니티 버전은 무료이며 작동합니다 (<https://www.visualstudio.com/downloads/>).

> .NET6 SDK가 포함된 VS 2022 V17.0 이상을 권장합니다.
{.is-info}

- 원하는 HTML/Javascript 편집기 (VS Code/Sublime Text/Webstorm/Atom 등)
- [Git](https://git-scm.com/downloads)
- [Node.js](https://nodejs.org/) 런타임이 필요합니다. 다음 버전이 지원됩니다:
  - **12.0** 이상
  - **14.0** 이상
  - **16.0** 이상
{.grid-list}

> Sonarr은 `10.x`, `8.x`, `6.x` 또는 12.0 미만의 이전 버전에서는 실행되지 **않습니다**!
{.is-warning}

- 프론트엔드 빌드에는 [Yarn](https://yarnpkg.com/getting-started/install)이 필요합니다.
  - Yarn은 **Node 16.10** 이상에서 기본으로 제공됩니다. `corepack enable`로 활성화할 수 있습니다.
  - 다른 Node 버전에서는 `npm i -g corepack`으로 설치하세요.

## 시작하기

1. Sonarr을 포크합니다.
1. 리포지토리를 개발 컴퓨터에 클론합니다. [*정보*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> 커밋하기 전에 프론트엔드 변경 사항에 대해 코드에 `yarn lint --fix`를 실행하세요.
CSS 변경 사항에 대해서는 `yarn stylelint-windows --fix`를 실행하세요. {.is-info}

### 프론트엔드 빌드하기

- 클론한 디렉토리로 이동합니다.
- 필요한 Node 패키지를 설치합니다.

     ```bash
     yarn install
     ```

- 개발 환경에서 후처리가 필요한 변경 사항을 모니터링하기 위해 webpack을 시작합니다.

     ```bash
     yarn start
     ```

### 백엔드 빌드하기

백엔드 솔루션은 주로 Visual Studio나 Rider에서 빌드하고 실행할 수 있지만, 프론트엔드 UI에만 중점을 둘 경우 올바른 SDK가 설치되어 있을 때 명령줄에서도 쉽게 빌드할 수 있습니다.

#### Visual Studio

> 시작 프로젝트가 `Sonarr.Console`이고 프레임워크가 `net6.0`으로 설정되어 있는지 확인하세요.
{.is-info}

1. Visual Studio에서 솔루션을 먼저 `빌드`합니다. 이렇게 하면 모든 프로젝트가 올바르게 빌드되고 종속성이 복원됩니다.
1. 다음으로 Visual Studio에서 프로젝트를 `디버그/실행`하여 Sonarr을 시작합니다.
1. <http://localhost:8989>를 엽니다.

#### 명령줄

1. 솔루션을 정리합니다.

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. 올바른 플랫폼 (Posix 또는 Windows)의 디버그 구성을 복원하고 빌드합니다.

```shell
dotnet msbuild -restore src/Sonarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. `/_output`에서 생성된 실행 파일을 실행합니다.

## 코드 기여하기

- 이미 요청된 새로운 기능을 추가하는 경우, 작업이 중복되지 않도록 [GitHub Issues](https://github.com/Sonarr/Sonarr/issues)에 의견을 남겨주세요 (이미 있는 기능 외에 추가하려는 기능이 있는 경우 먼저 저희에게 문의해주세요).
- Sonarr의 develop 브랜치에서 리베이스를 수행하세요. 병합하지 마세요.
- 의미 있는 커밋 또는 커밋을 스쿼시하세요.
- 작업이 완료되기 전에 pull request를 만들어도 괜찮습니다. 이렇게 하면 우리가 작업 상황을 확인하고 의견을 제시하거나 개선을 제안할 수 있습니다.
- 질문이 있으면 Discord에서 문의하세요.
- 테스트 (단위/통합)를 추가하세요.
- 일관성을 위해 \*nix 줄 바꿈으로 커밋하세요 (Windows에서 체크아웃하고 \*nix로 커밋합니다).
- 코드를 깨끗하고 이해하기 쉽게 유지하기 위해 각 pull request에는 하나의 기능/버그 수정만 포함하세요.
- VS 2022와 WebStorm의 기본값인 탭 대신 4개의 공백을 사용하세요.

## Pull Request

- `main`이 아닌 `develop`에만 pull request를 생성하세요. `main`에 PR을 생성하면 우리가 의견을 남기고 닫을 것입니다.
- 우리로부터 몇 가지 의견이나 질문을 받을 수 있습니다. 이는 일관성과 유지 관리성을 보장하기 위한 것입니다.
- pull request에 가능한 빨리 응답하려고 노력하겠지만, 하루나 이틀이 지나도록 응답이 없으면 Discord에서 문의해주세요. 놓친 경우일 수도 있습니다.
- 각 PR은 자체 [기능 브랜치](http://martinfowler.com/bliki/FeatureBranch.html)에서 develop이 아닌 포크에서 가져와야 하며, 의미 있는 브랜치 이름 (추가/수정되는 내용)을 가져야 합니다.
  - `new-feature` (좋음)
  - `fix-bug` (좋음)
  - `patch` (나쁨)
  - `develop` (나쁨)
- 커밋은 `New:` 또는 `Fixed:`로 작성되어야 합니다. 이는 `maintenance release`로 간주되지 않는 변경 사항입니다.

## 단위 테스트

Sonarr은 단위, 통합 및 자동화 테스트 스위트로 nunit을 사용합니다.

### 테스트 실행

테스트는 포함된 nunit3testadapter nuget 패키지를 사용하여 VS에서 쉽게 실행할 수 있으며, 포함된 bash 스크립트 `test.sh`를 사용하여 명령줄에서 실행할 수도 있습니다.

VS에서는 테스트 탐색기로 이동하여 확인하려는 테스트를 실행하거나 디버그할 수 있습니다.

VS에서는 한 번에 모든 테스트를 실행하거나 하나씩 실행할 수 있습니다.

명령줄에서 `test.sh` 스크립트는 3개의 매개변수를 사용합니다.

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### 테스트 작성

항상 재미있지는 않지만, 백엔드 코드 변경에 대해 단위 테스트를 작성하는 것을 권장합니다. 이렇게 하면 변경 사항이 의도한 대로 작동하고 향후 변경 사항이 예상된 동작을 깨뜨리지 않는지 확인할 수 있습니다.

> PR을 제출할 때는 새로운 코드의 80% 커버리지가 필요합니다.
{.is-info}

이에 대해 질문이 있으면 알려주세요.

# 번역

Sonarr은 자체 호스팅된 오픈 액세스 [Weblate](https://translate.servarr.com) 인스턴스를 사용하여 json 번역 파일을 관리합니다. 이 파일은 리포지토리의 `src/NzbDrone.Core/Localization`에 저장됩니다.

## 기존 번역에 기여하기

Weblate는 영어 이외의 모든 언어에 대한 동기화 및 번역을 처리합니다. 지원되는 언어의 번역된 문자열을 편집하거나 기존 문자열을 번역하려면 Sonarr 프로젝트에서 Weblate를 사용하세요.

영어 번역인 `en.json`은 다른 모든 번역의 원본이며 GitHub 리포지토리에서 관리됩니다.

## 언어 추가하기

Sonarr에 번역을 추가하려면 두 단계가 필요합니다.

- Weblate에 언어 추가하기
- Sonarr 코드베이스에 언어 추가하기

## 코드에서 번역 문자열 추가하기

영어 번역인 `src/NzbDrone.Core/Localization/en.json`은 다른 모든 번역의 원본이며 GitHub 리포지토리에서 관리됩니다. UI 또는 백엔드에 새로운 문자열을 추가할 때는 `en.json`에 키와 영어의 기본값을 추가해야 합니다. 이 키는 다음과 같이 사용할 수 있습니다:

> 로그 메시지의 번역에 대한 PR은 허용되지 않습니다.
{.is-warning}

### 백엔드 문자열

백엔드 문자열은 Localization Service의 `GetLocalizedString` 메서드를 사용하여 추가할 수 있습니다.

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### 프론트엔드 문자열

새로운 문자열은 번역 함수를 가져와서 `en.json`에서 지정된 키를 사용하여 프론트엔드에 추가할 수 있습니다.

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```