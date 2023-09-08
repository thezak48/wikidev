---
title: Radarr 지원
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# 목차

> 이 페이지는 작업 중이며 추가 노력이 필요합니다.{.is-warning}

이 페이지는 모든 `지원` 위키 링크 (일반적으로 UI의 "자세한 정보"를 의미함)의 구분 페이지입니다.

# 다운로드 클라이언트

{#downloadclient}

- Aria2 {#aria2}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Flood {#flood}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)
  - uTorrent는 광고가 포함되어 있고 이전에 스파이웨어였으므로 권장되지 않습니다. 대부분의 사용자는 Qbittorrent를 사용합니다.
- Vuze {#vuze}
  - [설정 페이지를 참조하세요](/radarr/settings#download-clients)

# 인덱서

{#indexer}

## 유즈넷

- Newznab {#newznab}
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
  - Newznab은 많은 유즈넷 인덱싱 사이트에서 사용되는 표준화된 API입니다. 많은 프리셋이 제공되지만 모두 접근하려면 API 키가 필요합니다.
  - [Prowlarr](/prowlarr) 및 [NZBHydra2](https://github.com/theotherp/nzbhydra2)와 같은 인덱서 애플리케이션은 통계 추적과 같은 고급 기능을 제공할 수 있습니다.
- omgwtfnzbs {#omgwtfnzbs}
  - 사라진 레거시 유즈넷 인덱서의 구현입니다. 대신 Newznab을 사용하세요.
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)

## 토렌트

- FileList {#filelist}
  - 비공개 트래커
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - 비공개 트래커
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 비공개 트래커
  > IP Torrents의 기본 구현은 검색을 지원하지 않습니다. 대신 torznab으로 Prowlarr이나 Jackett를 통해 사용하세요 {.is-info}
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 일본 미디어 (애니메이션) 전용 토렌트 트래커입니다.
  > Nyaa는 자동화를 비난하며 IP를 자주 차단할 수 있습니다. {.is-info}
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - 비공개 트래커
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 공개 트래커
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- Torrent RSS 피드 {#torrentrssindexer}
  - 일반적인 토렌트 RSS 피드 파서입니다.
  > RSS 피드에는 `pubdate`가 포함되어야 합니다. 릴리스 크기도 권장됩니다. {.is-info}
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - Torznab 이전 형식의 Couchpotato입니다.
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab은 Torrent와 Newznab의 조합어입니다. Newznab API 사양과 동일한 구조와 구문을 사용하지만 토렌트 특정 속성과 .torrent 파일을 노출합니다. 따라서 최신 RSS 피드와 백로그 검색 기능을 지원합니다. 이 사양은 Newznab 조직에서 유지 관리되거나 지원되지 않습니다. (동일한 API 사양은 nZEDb와 공유됩니다)
  - 이는 주로 [Prowlarr](/prowlarr) 및 [Jackett](https://github.com/Jackett/Jackett)에서 지원됩니다.
  - [설정 페이지를 참조하세요](/radarr/settings#indexer-settings)

> 많은 토렌트 트래커는 커뮤니티에 의존하며 사이트 방문, 카르마, 투표, 댓글 등을 요구하는 규칙을 가질 수 있습니다.
> 트래커 규칙과 예의를 검토하고 커뮤니티를 활발하게 유지하세요.
> 규칙을 어기거나 Hit and Runs (HnRs)/저비율을 발생시켜 계정이 차단되는 경우 책임지지 않습니다.{.is-warning}

# 알림

{#notification}

- Boxcar {#boxcar}
- 사용자 정의 스크립트 {#customscript}
  - 특정 작업이 발생할 때 사용자 정의 스크립트를 실행할 수 있습니다. 자세한 내용은 [사용자 정의 스크립트](/radarr/custom-scripts)를 참조하세요.
- Discord {#discord}
  - Radarr에서 발생하는 작업에 대한 알림을 전송하는 가장 일반적인 방법 중 하나입니다.
- 이메일 {#email}
  - 이메일로 자신이나 알림을 받고 싶은 다른 사람에게 간단히 메시지를 보낼 수 있습니다. Gmail을 사용하는 경우 보안 수준이 낮은 앱을 사용하도록 설정해야 합니다. Gmail을 사용하고 2단계 인증이 활성화된 경우 App 전용 비밀번호를 사용해야 합니다.

> `SomePrettyName <email@example.org>`와 같은 "예쁜 주소"를 사용할 수 있습니다.{.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi는 미디어에 대한 애정에서 시작되었습니다. 모든 디지털 미디어를 아름답고 사용자 친화적인 패키지로 통합하는 엔터테인먼트 허브입니다. 100% 무료이며 오픈 소스이며 매우 사용자 정의가 가능하며 다양한 장치에서 실행됩니다. 봉사자들과 거대한 커뮤니티의 지원을 받고 있습니다. Kodi를 연결하면 Radarr에 새 영화가 추가될 때 Kodi의 라이브러리를 업데이트할 수 있습니다.
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - [유용한 도구 - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier) 항목을 참조하세요.
- Plex 미디어 서버 {#plexserver}
  - 자체 호스팅 Plex 시스템의 서버입니다. 이를 활성화하면 Plex 서버에 새로운/업그레이드된 영화가 있는지 알리는 업데이트를 보낼 수 있습니다.
  - 이는 거의 필요하지 않으며 Plex가 파일 시스템의 변경 사항을 감시하지 못하는 경우에만 필요합니다.
  - Plex가 ionotify를 사용하여 파일 시스템을 감시할 수 없는 특정 유형의 원격 마운트 및 일부 오래된 네트워크 마운트와 같은 소수의 상황에서는 Plex 연결 대신 plexautoscan 앱을 사용하는 것이 좋습니다.
- [plexautoscan](https://github.com/l3uddz/plex_autoscan)과 같은 도구를 사용할 수도 있습니다.

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology 인덱서 {#synologyindexer}
- Telegram {#telegram}
- Trakt {#trakt}
- Twitter {#twitter}
  - [팁과 트릭 항목](/useful-tools#twitter)을 참조하세요.
- Webhook {#webhook}

# 목록

{#importlist}

- CouchPotato {#couchpotatoimport}
- 사용자 정의 목록 {#radarrlistimport}
- IMDb 목록 {#imdblistimport}
  - IMDb Watchlist를 추가하려면 목록으로 이동한 다음 편집을 클릭하세요. 개인 정보 설정이 공개로 설정되어 있는지 확인하세요. 주소 표시줄에서 `lsxxxxxx` 숫자를 찾아 Radarr에 입력해야 합니다.

    1. IMDB 목록 설정으로 이동합니다.
    1. 개인 정보를 `공개`로 설정합니다 (즉, `비활성화`).
    1. URL 내의 `ls` 번호를 사용합니다.

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex 워치리스트 {#plex}
  - 필요한 버전: v4.1.0.6176 이상
  - 인증된 Plex 사용자의 Plex 워치리스트를 Radarr에 추가합니다. 목록에 영화가 포함되어 있어야 합니다.
  - 여러 사용자의 워치리스트를 사용하려면 각 사용자의 목록을 추가하고 해당 Plex 사용자로 인증해야 합니다.
- Radarr {#radarrimport}
  - TRaSH에는 [두 인스턴스 동기화에 대한 가이드](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)가 있습니다.
- RSS 목록 {#rssimport}
- StevenLu 사용자 정의 {#stevenluimport}
	- JSON 형식의 사용자 정의 영화 목록을 만들 수 있습니다.
  	피드에는 각 영화에 대해 `title` 또는 `imdb_id` 중 하나가 필요합니다. 둘 다 제공할 수 있습니다.
  		> `imdb_id`는 넓은 검색을 필요로하지 않기 때문에 `title`보다 안전합니다.
    다음은 유효한 샘플 JSON입니다 : 
      ```
      [
          {
            "title": "The Wastetown",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/6J32RMp8uko8CUEM3rYP962hQun.jpg",
            "imdb_id": "tt22889064"
          },
          {
            "title": "Wild Sunflowers",
            "poster_url": "https://www.themoviedb.org/t/p/w300_and_h450_bestv2/tHK4c0UZKrqkmXZ2HJeGNhNetRz.jpg",
            "imdb_id": "tt13774830"
          }
      ]
      ```
      - 항목에 추가 키를 추가할 수 있습니다 (무시됨)
      - 빈 목록의 경우 빈 JSON 배열을 반환하세요 `[]`
- StevenLu 목록 {#stevenlu2import}
- TMDb 컬렉션 {#tmdbcollectionimport}
  - Radarr v4.2에서는 컬렉션 목록을 더 이상 지원하지 않으며 Radarr 내의 컬렉션으로 마이그레이션되었습니다. 자세한 내용은 [컬렉션](/radarr/library#collections) 섹션을 참조하세요.
- TMDb 회사 {#tmdbcompanyimport}
- TMDb 키워드 {#tmdbkeywordimport}
- TMDb 목록 {#tmdblistimport}
- TMDb 인물 {#tmdbpersonimport}
  - TMDb 인물 URL이 `https://www.themoviedb.org/person/500-tom-cruise`인 경우 인물 ID는 `500`입니다.
- TMDb 인기 {#tmdbpopularimport}
  - Top은 <https://developers.themoviedb.org/3/movies/get-top-rated-movies>를 사용합니다.
  - 인기는 <https://developers.themoviedb.org/3/movies/get-popular-movies>를 사용합니다.
  - 상영 중은 <https://developers.themoviedb.org/3/movies/get-now-playing>를 사용합니다.
  - 개봉 예정은 <https://developers.themoviedb.org/3/movies/get-upcoming>을 사용합니다.
- TMDb 사용자 {#tmdbuserimport}
- Trakt 목록 {#traktlistimport}
  - 사용자 이름 - 사용자의 실제 사용자 이름이 아닌 사용자 이름을 입력하세요.
  - 목록 - 목록 URL에 표시된대로 목록 이름을 사용하세요.
  - 예: `https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - 사용자 이름: `some-user-name`
    - 목록: `trakt-list-name`
- Trakt 인기 목록 {#traktpopularimport}
- Trakt 사용자 {#traktuserimport}
  - 자체 워치리스트를 사용할 때 이 유형을 사용해야 합니다.

# 메타데이터

{#metadata}

- Emby (레거시) {#mediabrowsermetadata}
  - 활성화 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
  - 영화 메타데이터 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
- Kodi (XBMC) / Emby {#xbmcmetadata}
  - 활성화 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
  - 영화 메타데이터 - 영화 메타데이터가 포함된 `<파일명>.nfo`를 생성합니다.
  - (고급 옵션) 영화 메타데이터 URL - TMDb 및 IMDb 영화 URL이 포함된 `movie.nfo`를 생성합니다.
  - 메타데이터 언어 - 사용 가능한 경우 Radarr이 메타데이터를 작성하는 데 사용할 언어를 선택합니다.
  - 영화 이미지 - 포스터 및 배너를 포함한 다양한 시즌 이미지를 생성합니다.
  - Movie.nfo 사용 - 기본 대신 `movie.nfo`로 nfo 파일을 작성합니다.
  - 컬렉션 이름 - Radarr은 .nfo 파일에 컬렉션 이름을 작성합니다.
- Roksbox {#roksboxmetadata}
  - 활성화 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
  - 영화 메타데이터 - 각 영화에 대한 xml 파일을 생성합니다.
  - 영화 이미지 - `Movie.jpg`를 생성합니다.
- WDTV {#wdtvmetadata}
  - 활성화 - 이 메타데이터 유형에 대한 메타데이터 파일 생성을 활성화합니다.
  - 영화 메타데이터 - 각 에피소드에 대한 `<파일명>.xml`을 생성합니다.
  - 영화 이미지 - `folder.jpg`를 생성합니다.