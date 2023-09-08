---
title: Lidarr 지원
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> 이 페이지는 작업 중이며 추가 노력이 필요합니다.{.is-warning}

이 페이지는 모든 "지원" 위키 링크(일반적으로 UI에서 `자세히 알아보기`로 표시됨)에 대한 구분 페이지입니다.

# 다운로드 클라이언트

{#downloadclient}

- Deluge {#deluge}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Flood {#flood}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)
  - uTorrent는 광고 지원 및 이전에 스파이웨어였기 때문에 권장되지 않습니다. 대부분의 사용자는 qBittorrent를 사용합니다.
- Vuze {#vuze}
  - [설정 페이지를 참조하세요](/lidarr/settings#download-clients)

# 인덱서

{#indexer}

## 유즈넷

- Newznab {#newznab}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
  - Newznab은 많은 유즈넷 인덱싱 사이트에서 사용되는 표준화된 API입니다. 많은 프리셋이 제공되지만, 모두 접근하려면 API 키가 필요합니다.
  - [Prowlarr](/prowlarr) 및 [NZBHydra2](https://github.com/theotherp/nzbhydra2)와 같은 인덱서 애플리케이션은 통계 추적과 같은 고급 기능을 제공할 수 있습니다.

## 토렌트

- FileList {#filelist}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 비공개 트래커
  > IP Torrents의 기본 구현은 검색을 지원하지 않습니다{.is-info}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 공개 트래커
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- Torrent RSS 피드 {#torrentrssindexer}
  - 일반적인 토렌트 RSS 피드 파서입니다.
  > RSS 피드에는 `pubdate`가 포함되어야 합니다. 릴리스 크기도 권장됩니다{.is-info}
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - 비공개 인덱서
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab은 Torrent와 Newznab의 언어 장난입니다. Newznab API 사양과 동일한 구조와 구문을 사용하지만 토렌트 특정 속성과 .torrent 파일을 노출합니다. 따라서 최신 RSS 피드와 백로그 검색 기능을 지원합니다. 이 사양은 Newznab 조직에서 유지 관리되거나 지원되지 않습니다.(동일한 API 사양은 nZEDb와 공유됩니다)
  - 이는 주로 [Prowlarr](/prowlarr) 및 [Jackett](https://github.com/Jackett/Jackett)에서 지원됩니다.
  - [설정 페이지를 참조하세요](/lidarr/settings#indexer-settings)

# 알림

{#notification}

- Boxcar {#boxcar}
- 사용자 지정 스크립트 {#customscript}
  - 특정 작업이 발생할 때 사용자 정의 스크립트를 실행할 수 있습니다. 자세한 내용은 [사용자 정의 스크립트](/lidarr/custom-scripts)를 참조하세요.
- Discord {#discord}
  - Lidarr에서 발생하는 작업에 대한 알림을 푸시하는 가장 일반적인 방법 중 하나입니다.
- 이메일 {#email}
  - 이메일로 자신이나 알림을 받고 싶은 사람에게 간단히 메시지를 보낼 수 있습니다. Gmail을 사용하는 경우, 보안 수준이 낮은 앱을 사용하도록 설정해야 합니다. Gmail을 사용하고 2단계 인증이 활성화된 경우, 앱별 비밀번호를 사용해야 합니다.

 > `SomePrettyName <email@example.org>`와 같은 "예쁜 주소"를 사용할 수 있습니다{.is-info}

- Emby (미디어 브라우저) {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi는 미디어에 대한 애정에서 시작되었습니다. 모든 디지털 미디어를 아름답고 사용자 친화적인 패키지로 통합하는 엔터테인먼트 허브입니다. 100% 무료이며 오픈 소스이며 매우 사용자 정의가 가능하며 다양한 장치에서 실행됩니다. 봉사자들과 거대한 커뮤니티의 지원을 받고 있습니다. Kodi를 연결하여 Lidarr에 새로운 곡이 추가될 때 Kodi의 라이브러리를 업데이트할 수 있습니다.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - [유용한 도구 - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier) 항목을 참조하세요.
- Plex 미디어 서버 {#plexserver}
  - 자체 호스팅 Plex 시스템의 서버입니다. 이를 활성화하면 Kodi와 마찬가지로 새로운/업그레이드된 에피소드가 사용 가능하다는 알림을 Plex 서버에 푸시할 수 있습니다.
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology 인덱서 {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - [팁과 트릭 항목](/useful-tools#twitter)을 참조하세요.
- Webhook {#webhook}

# 목록

{#importlist}

- Headphones {#headphonesimport}
- Last.fm 태그 {#lastfmtag}
- Last.fm 사용자 {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr 목록 {#lidarrlists}
- MusicBrainz 시리즈 {#musicbrainzseries}
- Spotify 팔로우한 아티스트 {#spotifyfollowedartists}
- Spotify 플레이리스트 {#spotifyplaylist}
- Spotify 저장한 앨범 {#spotifysavedalbums}

# 메타데이터

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}