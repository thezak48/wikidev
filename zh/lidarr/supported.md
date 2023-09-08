---
title: Lidarr 支持的功能
description: 
published: true
date: 2022-06-17T08:57:21.618Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:13.803Z
---

> 本页面正在编写中，需要额外的努力{.is-warning}

本页面是所有“支持的”维基链接（通常在用户界面中为“更多信息”）的消歧页面。

# 下载客户端

{#downloadclient}

- Deluge {#deluge}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Flood {#flood}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Hadouken {#hadouken}
  - [请参考设置页面](/lidarr/settings#download-clients)
- NZBGet {#nzbget}
  - [请参考设置页面](/lidarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [请参考设置页面](/lidarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [请参考设置页面](/lidarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [请参考设置页面](/lidarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Transmission {#transmission}
  - [请参考设置页面](/lidarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [请参考设置页面](/lidarr/settings#download-clients)
- uTorrent {#utorrent}
  - [请参考设置页面](/lidarr/settings#download-clients)
  - 由于uTorrent是广告软件和曾经的间谍软件，不推荐使用。大多数用户使用qBittorrent。
- Vuze {#vuze}
  - [请参考设置页面](/lidarr/settings#download-clients)

# 索引器

{#indexer}

## Usenet

- Newznab {#newznab}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
  - Newznab是许多Usenet索引站点使用的标准化API。有许多预设可用，但所有预设都需要API密钥才能访问。
  - 索引器应用程序，如[Prowlarr](/prowlarr)和[NZBHydra2](https://github.com/theotherp/nzbhydra2)，可以提供高级功能，如统计跟踪。

## Torrents

- FileList {#filelist}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- Headphones VIP {#headphones}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 私有Tracker
  > IP Torrents的原生实现不支持搜索{.is-info}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- omgwtfnzbs {#omgwtfnzbs}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 公共Tracker
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- Redacted {#redacted}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- Torrent RSS Feed {#torrentrssindexer}
  - 通用的Torrent RSS feed解析器。
  > RSS feed必须包含`pubdate`。建议同时包含发布大小{.is-info}
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - 私有索引器
  - [请参考设置页面](/lidarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab是Torrent和Newznab的组合词。它使用与Newznab API规范相同的结构和语法，但公开了特定于Torrent的属性和.torrent文件。因此，它支持最近的RSS feed和历史搜索功能。该规范未由Newznab组织维护或支持。（与nZEDb共享相同的API规范）
  - 这主要由[Prowlarr](/prowlarr)和[Jackett](https://github.com/Jackett/Jackett)支持
  - [请参考设置页面](/lidarr/settings#indexer-settings)

# 通知

{#notification}

- Boxcar {#boxcar}
- 自定义脚本 {#customscript}
  - 这允许您为特定操作编写自定义脚本，当发生该操作时，脚本将运行。有关更多详细信息，请参阅[自定义脚本](/lidarr/custom-scripts)。
- Discord {#discord}
  - 这是将Lidarr上发生的操作推送通知的最常见方法之一
- 电子邮件 {#email}
  - 可以向自己或其他人发送电子邮件通知。如果使用Gmail，请启用较不安全的应用程序访问权限。如果使用Gmail并启用了两步验证，则需要使用特定于应用程序的密码。

 > 您可以使用“漂亮的地址”（如`SomePrettyName <email@example.org>`）{.is-info}

- Emby（媒体浏览器）{#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi源于对媒体的热爱。它是一个将您的所有数字媒体整合到一个美观且用户友好的界面中的娱乐中心。它是100％免费和开源的，非常可定制，并可在各种设备上运行。它由一支专门的志愿者团队和一个庞大的社区支持。通过将Kodi作为连接添加，您可以在Lidarr添加新歌曲时更新Kodi的库。
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - 请参阅[有用的工具 - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)中的条目
- Plex Media Server {#plexserver}
  - 用于自托管Plex系统的服务器，启用此功能类似于Kodi，可以向Plex服务器推送更新通知，通知其有新的/升级的剧集可用。
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - 请参阅此[技巧和窍门条目](/useful-tools#twitter)
- Webhook {#webhook}

# 列表

{#importlist}

- Headphones {#headphonesimport}
- Last.fm 标签 {#lastfmtag}
- Last.fm 用户 {#lastfmuser}
- Lidarr {#lidarrimport}
- Lidarr 列表 {#lidarrlists}
- MusicBrainz 系列 {#musicbrainzseries}
- Spotify 关注的艺术家 {#spotifyfollowedartists}
- Spotify 播放列表 {#spotifyplaylist}
- Spotify 保存的专辑 {#spotifysavedalbums}

# 元数据

{#metadata}

- Kodi（XBMC）/ Emby {#xbmcmetadata}
- Roksbox {#roksboxmetadata}
- WDTV {#wdtvmetadata}