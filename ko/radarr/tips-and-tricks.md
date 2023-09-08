---
title: Radarr 팁과 트릭
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-and-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# TRaSH의 사용자 정의 형식

- [TRaSH는 가이드](https://trash-guides.info/Radarr/)를 통해 [Radarr => 설정 => 사용자 정의 형식](/radarr/settings#custom-formats)을 사용하는 방법과 사용자 정의 형식의 공유 저장소를 제공합니다.

# 두 개의 Radarr 인스턴스 동기화

- TRaSH는 [두 인스턴스 동기화에 대한 가이드](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)를 제공합니다.

# 영화 폴더 이름 바꾸기

- [이 FAQ 항목](/radarr/faq#how-can-i-rename-my-movie-folders)을 참조하세요.

# 각 영화를 위한 폴더 생성

- 이는 Radarr로 가져오기를 용이하게 하기 위해 기존 라이브러리를 정리/조직화하는 데 필요합니다. 아래에는 몇 가지 다른 방법이 있습니다.

## Filebot

> Filebot은 Windows, Linux 및 MacOS에서 지원됩니다. {.is-info}

- [Filebot](https://www.filebot.net/)은 영화를 Radarr에서 성공적으로 구문 분석할 수 있는 방식으로 구성하는 데 유용한 유틸리티입니다. 여전히 무료로 다운로드할 수 있는 4.7.9 버전은 SourceForge 미러에서 제공되지만, Windows 및 Apple 스토어에서 유료 버전도 사용할 수 있습니다. Linux에서는 Arch의 AUR 패키지나 Debian/Ubuntu의 `.deb` 파일과 같은 패키지가 있을 수 있습니다. GUI와 CLI 모두를 갖추고 있으므로 대부분의 사용자를 만족시킬 수 있습니다.

- Filebot은 포맷 표현 페이지를 포함하여 많은 도움말이 제공됩니다. 개인적으로는 파일에 품질, 에디션 및/또는 그룹과 같은 유용한 세부 정보가 포함되어 있다면 `{ny}\{fn}`과 같은 것을 사용하는 것이 좋습니다. 그렇지 않은 경우 `{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`와 같은 것을 사용할 수 있습니다. 이는 예를 들어 `Movie (Year)/Movie (Year) [Bluray-1080p]` 또는 `Movie (Year)/Movie (Year) [DVD-480p]`를 생성합니다. Bluray 대신 WEBDL을 사용할 수도 있으며, 이렇게 하면 컬렉션이 해당 형식으로 간주됩니다.

- 향후 영화에도 이러한 패턴을 유지하려면 다음을 설정해야 합니다:

- [설정 => 미디어 관리 (고급 설정 표시) => 영화 이름 지정](/radarr/settings#media-management)

  - 파일: `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - 폴더: `{Movie CleanTitle} {(Release Year)}`

- 참고: 위의 공백을 `.` 또는 `_`로 바꿀 수도 있습니다.

## Files 2 Folder

> Files 2 Folder는 Windows 응용 프로그램입니다. {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/)는 Radarr로 가져오기 위해 영화 라이브러리를 구성하는 데 사용할 수 있습니다. 압축 파일을 컴퓨터에 추출한 다음 .exe 파일을 관리자 권한으로 실행하고, 나타나는 메뉴에서 예를 클릭하면 됩니다.

설치 후 몇 번의 클릭으로 모든 파일을 각각의 폴더로 정리할 수 있습니다.

1. 영화 폴더로 이동합니다.
1. 모든 파일을 선택한 다음 마우스 오른쪽 버튼을 클릭하여 메뉴를 엽니다.
1. 메뉴에서 `files 2 folder` 옵션을 선택합니다.
1. Files 2 Folder 창에서 `Move each file to individual subfolders based on their names`를 선택합니다.
1. 확인을 클릭합니다.
1. 잠시 기다리면 모든 파일이 각각의 폴더에 정리됩니다.

## Linux Bash 스크립트

다음 스크립트는 선택한 폴더 내의 모든 `*.mkv` 파일을 이름을 기반으로 폴더로 이동합니다. 시작/선택한 폴더 내의 하위 폴더로 이동하지 않음에 유의하세요.

```shell
cd /path/to/your/movies/files/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windows 명령 프롬프트

Windows에서 명령 프롬프트(cmd.exe)에서 `관리자로 실행`을 선택합니다. 영화 폴더로 이동합니다. 다음 두 명령을 실행합니다 (복사/붙여넣기는 괜찮으며, 변경할 내용이 없습니다):

`for %i in (*) do md "%~ni"`

이 명령은 디렉토리에 있는 각 파일에 대해 폴더를 생성합니다.

`for %i in (*) do move "%i" "%~ni"`

이 명령은 모든 파일을 새 폴더로 이동합니다.

빈 폴더를 정리해야 하는 경우 다음 명령을 사용할 수 있습니다:

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows PowerShell

또는 Windows에서 PowerShell에서 다음 스크립트를 실행하여 디렉토리의 각 파일을 반복하고 해당 이름과 동일한 폴더로 이동할 수 있습니다.

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```