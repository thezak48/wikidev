---
title: Readarr 지원
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> 이 페이지는 작업 중이며 추가 노력이 필요합니다.{.is-warning}

이 페이지는 모든 "지원" 위키 링크(일반적으로 UI에서 `더 많은 정보`로 표시됨)에 대한 구분 페이지입니다.

# 다운로드 클라이언트

{#downloadclient}

- Aria2 {#aria2}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Flood {#flood}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)
  - uTorrent는 광고가 포함되어 있고 이전에 스파이웨어였으므로 권장되지 않습니다. 대부분의 사용자는 qBittorrent를 사용합니다.
- Vuze {#vuze}
  - [설정 페이지를 참조하세요](/readarr/settings#download-clients)

# 인덱서

{#indexer}

## 유즈넷

- Newznab {#newznab}
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
  - Newznab은 많은 유즈넷 인덱싱 사이트에서 사용되는 표준화된 API입니다. 많은 프리셋이 제공되지만 모두 접근하려면 API 키가 필요합니다.
  - [Prowlarr](/prowlarr) 및 [NZBHydra2](https://github.com/theotherp/nzbhydra2)와 같은 인덱서 애플리케이션은 통계 추적과 같은 고급 기능을 제공할 수 있습니다.
- omgwtfnzbs {#omgwtfnzbs}
  - 개인 유즈넷 인덱서
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)

## 토렌트

- FileList {#filelist}
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 비공개 트래커
  > IP Torrents의 기본 구현은 검색을 지원하지 않습니다.{.is-info}
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 일본 미디어(애니메이션) 전용 토렌트 트래커입니다.
  > Nyaa는 자동화를 금지하며 IP를 자주 차단할 수 있습니다.{.is-info}
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 공개 트래커
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
- Torrent RSS 피드 {#torrentrssindexer}
  - 일반적인 토렌트 RSS 피드 파서입니다.
  > RSS 피드에는 `pubdate`가 포함되어야 합니다. 릴리스 크기도 권장됩니다.{.is-info}
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - 비공개 인덱서
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab은 Torrent와 Newznab의 조합어입니다. Newznab API 사양과 동일한 구조와 구문을 사용하지만 토렌트 특정 속성과 .torrent 파일을 노출합니다. 따라서 최신 RSS 피드와 백로그 검색 기능을 지원합니다. 이 사양은 Newznab 조직에서 유지 관리되거나 지원되지 않습니다.(동일한 API 사양은 nZEDb와 공유됩니다)
  - 이는 주로 [Prowlarr](/prowlarr) 및 [Jackett](https://github.com/Jackett/Jackett)에서 지원됩니다.
  - [설정 페이지를 참조하세요](/readarr/settings#indexer-settings)

# 알림

{#notification}

- Boxcar {#boxcar}
- Custom Script {#customscript}
  - 이를 통해 특정 작업이 발생할 때 사용자 정의 스크립트를 실행할 수 있습니다. 자세한 내용은 [사용자 정의 스크립트](/readarr/custom-scripts)를 참조하세요.
- Discord {#discord}
  - Readarr에서 발생하는 작업에 대한 알림을 푸시하는 가장 일반적인 방법 중 하나입니다.
- Email {#email}
  - 이메일로 자신이나 알림을 받고 싶은 다른 사람에게 간단히 메시지를 보낼 수 있습니다. Gmail을 사용하는 경우 보안 수준이 낮은 앱을 사용하도록 설정해야 합니다. Gmail을 사용하고 2단계 인증이 활성화된 경우 앱별 비밀번호를 사용해야 합니다.

 > `SomePrettyName <email@example.org>`와 같은 "예쁜 주소"를 사용할 수 있습니다.{.is-info}

- GoodReads 책장 {#goodreadsbookshelf}
- GoodReads 소유한 책 {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - [유용한 도구 - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier) 항목을 참조하세요.
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

- GoodReads 책장 {#goodreadsbookshelf}
  - (고급 옵션) 사용자 ID - 여기에 사용자 ID가 아닌 다른 사용자 ID를 입력합니다.
  - 책장 - GoodReads에서 가져올 책장을 선택합니다.
  - GoodReads와 인증 - GoodReads와 인증하려면 버튼을 클릭하세요.

> 여러 GoodReads 사용자를 별도의 목록으로 추가할 수 있습니다. 인증된 사용자 외에도 고급 옵션을 활성화하고 사용자 ID를 입력한 다음 GoodReads와 인증을 클릭하여 사용자의 책장을 가져올 수 있습니다.{.is-info}

- GoodReads 소유한 책 {#goodreadsownedbooks}
  - (고급 옵션) 사용자 ID - 여기에 사용자 ID가 아닌 다른 사용자 ID를 입력합니다.
  - 책장 - GoodReads에서 가져올 책장을 선택합니다.
  - GoodReads와 인증 - GoodReads와 인증하려면 버튼을 클릭하세요.

> 여러 GoodReads 사용자를 별도의 목록으로 추가할 수 있습니다. 인증된 사용자 외에도 고급 옵션을 활성화하고 사용자 ID를 입력한 다음 GoodReads와 인증을 클릭하여 사용자의 책장을 가져올 수 있습니다.{.is-info}

- GoodReads 목록 {#goodreadslistimportlist}
  - 목록 ID - 추가할 공개 GoodReads 목록의 ID를 입력하세요.
- GoodReads 시리즈 {#goodreadsseriesimportlist}
  - 시리즈 ID - 추가할 GoodReads 시리즈의 ID를 입력하세요.
- LazyLibrarian {#lazylibrarianimport}
  - URL - LazyLibrarian 인스턴스의 URL
  - API 키 - LazyLibrarian 인스턴스의 API 키
- Readarr {#readarrimport}
  - 전체 URL - 가져올 Readarr 인스턴스의 전체 URL(예: `http://localhost:8787/readarr`)
  - API 키 - 가져올 Readarr 인스턴스의 API 키
  - 프로필 - 가져올 Readarr 인스턴스의 프로필
  - 태그 - 가져올 Readarr 인스턴스의 태그

# 메타데이터

{#metadata}

- Calibre {#calibre}
  - [설정 페이지를 참조하세요](/readarr/settings#write-metadata-to-book-files)
- 오디오 태깅 {#audiotagging}
  - [설정 페이지를 참조하세요](/readarr/settings#write-metadata-to-book-files)