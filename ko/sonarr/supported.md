---
title: Sonarr 지원
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> 이 페이지는 작업 중이며 추가 노력이 필요합니다. {.is-warning}

이 페이지는 모든 "지원" 위키 링크 (일반적으로 UI에서 `자세히 알아보기`로 표시됨)에 대한 구분 페이지입니다.

# 다운로드 클라이언트

{#downloadclient}

- Aria2 {#aria2}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Flood {#flood}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)
  - uTorrent는 광고 지원 소프트웨어이자 이전에 스파이웨어였기 때문에 권장되지 않습니다. 대부분의 사용자는 Qbittorrent를 사용합니다.
- Vuze {#vuze}
  - [설정 페이지를 참조하세요](/sonarr/settings#download-clients)

# 인덱서

{#indexer}

## 유즈넷

- Fanzub {#fanzub}
  - 일본 미디어 (애니메이션) 전용 유즈넷 인덱서입니다.
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
  - Newznab은 많은 유즈넷 인덱싱 사이트에서 사용되는 표준화된 API입니다. 많은 프리셋이 제공되지만, 모두 접근하려면 API 키가 필요합니다.
  - [Prowlarr](/prowlarr) 및 [NZBHydra2](https://github.com/theotherp/nzbhydra2)와 같은 인덱서 애플리케이션은 통계 추적과 같은 고급 기능을 제공할 수 있습니다.
- omgwtfnzbs {#omgwtfnzbs}
  - 사라진 개인 유즈넷 인덱서의 구현입니다. 대신 Newznab을 사용하세요.
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)

## 토렌트

- BroadcasTheNet (BTN) {#broadcasthenet}
  - 비공개 트래커
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - 비공개 트래커
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - 비공개 트래커
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 비공개 트래커
  > IP Torrents의 기본 구현은 검색을 지원하지 않습니다. 대신 Prowlarr이나 Jackett을 통해 torznab으로 사용하세요. {.is-info}
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 일본 미디어 (애니메이션) 전용 토렌트 트래커입니다.
  - Nyaa는 애니메이션 시리즈 유형에 대해서만 검색을 지원합니다.
  - 기존 Sonarr 버전과 관련된 알려진 문제가 있습니다.
    - [Nyaa seeders/leechers not parsed properly anymore. #4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - 이 문제는 [Pull Request #4637](https://github.com/Sonarr/Sonarr/pull/4637)이 병합될 때 수정될 수 있습니다.
  - > Nyaa는 자동화를 비난하며 IP를 자주 차단할 수 있습니다. {.is-warning}
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 공개 트래커
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- Torrent RSS 피드 {#torrentrssindexer}
  - 일반적인 토렌트 RSS 피드 파서입니다.
  > RSS 피드에는 `pubdate`가 포함되어야 합니다. 릴리스 크기도 권장됩니다. {.is-info}
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - 비공개 인덱서
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab은 Torrent와 Newznab의 언어장난입니다. Newznab API 사양과 동일한 구조와 구문을 사용하지만 토렌트 특정 속성과 .torrent 파일을 노출합니다. 따라서 최신 RSS 피드 및 백로그 검색 기능을 지원합니다. 이 사양은 Newznab 조직에서 유지 관리되거나 지원되지 않습니다. (동일한 API 사양은 nZEDb와 공유됩니다)
  - 이는 주로 [Prowlarr](/prowlarr) 및 [Jackett](https://github.com/Jackett/Jackett)에서 지원됩니다.
  - [설정 페이지를 참조하세요](/sonarr/settings#indexer-settings)

> 많은 토렌트 트래커가 커뮤니티에 의존하며 사이트 방문, 카르마, 투표, 댓글 등을 규정하는 규칙을 가지고 있을 수 있습니다.
> 트래커 규칙과 예의를 검토하고 커뮤니티를 활발하게 유지하세요.
> 규칙을 어기거나 Hit and Runs (HnRs)/저비율을 발생시켜 계정이 차단되는 경우 책임지지 않습니다. {.is-warning}

# 알림

{#notification}

- Boxcar {#boxcar}
- 사용자 지정 스크립트 {#customscript}
  - 특정 작업이 발생할 때 사용자 정의 스크립트를 실행할 수 있습니다. 자세한 내용은 [사용자 정의 스크립트](/sonarr/custom-scripts)를 참조하세요.
- Discord {#discord}
  - Sonarr에서 발생하는 작업에 대한 알림을 전송하는 가장 일반적인 방법 중 하나입니다.
  - 지원되는 필드 유형:
  `개요, 평점, 장르, 품질, 그룹, 크기, 링크, 릴리스, 포스터, 팬아트, 사용자 정의 형식, 사용자 정의 형식 점수, 인덱서`
- 이메일 {#email}
  - 이메일로 자신이나 알림을 받고 싶은 사람에게 간단히 메시지를 보낼 수 있습니다. Gmail을 사용하는 경우, 보안 수준이 낮은 앱을 사용하도록 설정해야 합니다. Gmail을 사용하고 2단계 인증이 활성화된 경우에는 앱별 비밀번호를 사용해야 합니다.

> `SomePrettyName <email@example.org>`와 같은 "예쁜 주소"를 사용할 수 있습니다. {.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi는 미디어에 대한 애정에서 시작되었습니다. 모든 디지털 미디어를 아름답고 사용자 친화적인 패키지로 통합하는 엔터테인먼트 허브입니다. 100% 무료이며 오픈 소스이며 매우 사용자 정의가 가능하며 다양한 장치에서 실행됩니다. 봉사자로 구성된 헌신적인 팀과 거대한 커뮤니티의 지원을 받고 있습니다. Kodi를 연결하여 Sonarr에 새로운 에피소드가 추가되었을 때 Kodi의 라이브러리를 업데이트할 수 있습니다.
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - 사용되지 않음
- Plex Media Center {#plexclient}
  - 사용되지 않음
- Plex Media Server {#plexserver}
  - 자체 호스팅 Plex 시스템의 서버입니다. 이를 활성화하면 Kodi와 마찬가지로 새로운/업그레이드된 에피소드가 사용 가능하다는 알림을 Plex 서버에 전송할 수 있습니다.
  - 이는 거의 필요하지 않으며 Plex가 파일 시스템의 변경 사항을 감시하지 못하는 경우에만 필요합니다.
  - 일부 원격 마운트 및 일부 오래된 네트워크 마운트와 같은 특정 유형의 Plex가 ionotify를 사용하여 파일 시스템을 감시하지 못하는 경우에는 Plex 연결 대신 plexautoscan 앱을 사용하는 것이 좋습니다.

> 이로 인해 시리즈가 있는 라이브러리/루트 폴더에 대한 전체 라이브러리 스캔이 트리거될 수 있습니다. 파일 시스템을 감시하는 기본 Plex 기능을 사용하거나 [plexautoscan](https://github.com/l3uddz/plex_autoscan)과 같은 도구를 사용하는 것이 강력히 권장됩니다. {.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology 인덱서 {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - 이 [팁 및 트릭 항목](/useful-tools#twitter)을 참조하세요.
- Webhook {#webhook}

# 목록

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH는 [두 인스턴스 동기화에 대한 가이드](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)를 제공합니다.
- Plex 워치리스트 {#pleximport}
  - 인증된 Plex 사용자의 Plex 워치리스트를 Radarr에 추가하세요. 리스트에는 쇼가 포함되어 있어야 합니다.
  - 여러 사용자의 워치리스트를 사용하려면 각 사용자의 리스트를 추가하고 해당 Plex 사용자로 인증해야 합니다.
- Trakt 리스트 {#traktlistimport}
  - 사용자 이름 - 사용자의 실제 사용자 이름이 아닌 사용자 이름을 입력하세요.
  - 리스트 - 리스트 URL에서 제시된 대로 리스트 이름을 사용하세요.
  - 예: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - 사용자 이름: `some-user-name`
    - 리스트: `trakt-list-name`
- Trakt 인기 리스트 {#traktpopularimport}
- Trakt 사용자 {#traktuserimport}

> Trakt 리스트에는 쇼가 포함되어야 하며 개별 에피소드는 포함되지 않습니다. Sonarr은 쇼만 일치시키고 추가합니다. {.is-info}

# 메타데이터

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - 활성화 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
  - 시리즈 메타데이터 - 전체 시리즈 메타데이터가 포함된 `tvshow.nfo`를 생성합니다.
  - (고급 옵션) 시리즈 메타데이터 URL - TheTVDb 시리즈 URL이 포함된 `tvshow.nfo`를 생성합니다.
  - 에피소드 메타데이터 - 각 에피소드에 대해 `<filename>.nfo`를 생성합니다.
  - 시리즈 이미지 - `poster.jpg` 및 `banner.jpg`와 같이 포스터 및 배너를 포함한 다양한 시리즈 이미지를 생성합니다.
  - 시즌 이미지 - `season##-poster.jpg` 및 `season##-banner.jpg`와 같이 포스터 및 배너를 포함한 다양한 시즌 이미지를 생성합니다.
  - 에피소드 이미지 - `<filename>-thumb.jpg`와 같이 썸네일을 포함한 다양한 에피소드 이미지를 생성합니다.
- Roksbox {#roksboxmetadata}
  - 활성화 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
  - 에피소드 메타데이터 - 각 에피소드에 대해 `Season##\<filename>.xml`을 생성합니다.
  - 시리즈 이미지 - `Series Title.jpg`를 생성합니다.
  - 시즌 이미지 - `Season ##.jpg`를 생성합니다.
  - 에피소드 이미지 - `Season##\<filename>.jpg`를 생성합니다.
- WDTV {#wdtvmetadata}
  - 활성화 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
  - 에피소드 메타데이터 - 각 에피소드에 대해 `Season##\<filename>.xml`을 생성합니다.
  - 시리즈 이미지 - `folder.jpg`를 생성합니다.
  - 시즌 이미지 - `Season ##\folder.jpg`를 생성합니다.
  - 에피소드 이미지 - `Season##\<filename>.metathumb`를 생성합니다.