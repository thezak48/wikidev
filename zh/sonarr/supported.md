---
title: Sonarr支持的功能
description: 
published: true
date: 2023-09-01T16:44:31.667Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:33.769Z
---

> 此页面正在进行中，需要额外的努力。{.is-warning}

此页面是所有“支持”的维基链接（通常在用户界面中为“更多信息”）的消歧页面。

# 下载客户端

{#downloadclient}

- Aria2 {#aria2}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Deluge {#deluge}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Flood {#flood}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Hadouken {#hadouken}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- NZBGet {#nzbget}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Transmission {#transmission}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [请参阅设置页面](/sonarr/settings#download-clients)
- uTorrent {#utorrent}
  - [请参阅设置页面](/sonarr/settings#download-clients)
  - 由于uTorrent是广告软件和曾经的间谍软件，不建议使用。大多数用户使用Qbittorrent
- Vuze {#vuze}
  - [请参阅设置页面](/sonarr/settings#download-clients)

# 索引器

{#indexer}

## Usenet

- Fanzub {#fanzub}
  - 专门用于日本媒体（动画）的Usenet索引器。
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- Newznab {#newznab}
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
  - Newznab是许多Usenet索引站点使用的标准化API。有许多预设可用，但都需要API密钥才能访问。
  - 像[Prowlarr](/prowlarr)和[NZBHydra2](https://github.com/theotherp/nzbhydra2)这样的索引器应用程序可以提供高级功能，如统计跟踪。
- omgwtfnzbs {#omgwtfnzbs}
  - 私有Usenet索引器的过时遗留实现。请改用Newznab。
  - [请参阅设置页面](/sonarr/settings#indexer-settings)

## Torrents

- BroadcasTheNet (BTN) {#broadcasthenet}
  - 私有Tracker
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- FileList {#filelist}
  - 私有Tracker
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- HDBits {#hdbits}
  - 私有Tracker
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 私有Tracker
  > IP Torrents的原生实现不支持搜索。请使用Prowlarr或Jackett作为torznab代替。{.is-info}
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 专门用于日本媒体（动画）的Torrent Tracker。
  - Nyaa仅支持搜索动画系列类型。
  - 本地Sonarr版本存在已知问题
    - [Nyaa种子数/下载数无法正确解析。＃4614](https://github.com/Sonarr/Sonarr/issues/4614)
      - 当/如果合并[拉取请求＃4637](https://github.com/Sonarr/Sonarr/pull/4637)时，可以修复此问题
  - > Nyaa不赞成自动化，并经常会封禁您的IP。{.is-warning}
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 公共Tracker
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- Torrent RSS Feed {#torrentrssindexer}
  - 通用的Torrent RSS feed解析器。
  > RSS feed必须包含`pubdate`。建议同时提供发布大小。{.is-info}
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - 私有索引器
  - [请参阅设置页面](/sonarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab是Torrent和Newznab的谐音。它使用与Newznab API规范相同的结构和语法，但公开了特定于Torrent的属性和.torrent文件。因此，它支持最新的RSS feed和回溯搜索功能。该规范未由Newznab组织维护或支持。（与nZEDb共享相同的API规范）
  - 这主要由[Prowlarr](/prowlarr)和[Jackett](https://github.com/Jackett/Jackett)支持
  - [请参阅设置页面](/sonarr/settings#indexer-settings)

> 许多Torrent Tracker依赖于社区，并可能有规定要求访问站点、积分、投票、评论等。
> 请仔细阅读您的Tracker规则和礼仪，保持社区活跃。
> 如果您违反规则或产生HnRs（Hit and Runs）/低比率而导致帐户被封禁，我们概不负责。{.is-warning}

# 通知

{#notification}

- Boxcar {#boxcar}
- Custom Script {#customscript}
  - 这允许您为特定操作创建自定义脚本，当发生该操作时，脚本将运行。有关更多详细信息，请参阅[自定义脚本](/sonarr/custom-scripts)。
- Discord {#discord}
  - 迄今为止，这是推送Sonarr上发生的操作的最常见方式之一
  - 支持的字段类型：
  `概述，评分，流派，质量，群组，大小，链接，发布，海报，艺术品，自定义格式，自定义格式分数，索引器`
- Email {#email}
  - 只需向自己或您想要打扰的某人发送电子邮件。如果您使用Gmail，则需要启用不安全的应用程序访问权限。如果您使用Gmail并启用了两步验证，您需要使用特定于应用程序的密码。

> 您可以使用“漂亮的地址”（如`SomePrettyName <email@example.org>`）{.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi源自对媒体的热爱。它是一个将您的所有数字媒体集合在一起的娱乐中心，界面美观且用户友好。它是100％免费和开源的，非常可定制，并可在各种设备上运行。它由一支专门的志愿者团队和一个庞大的社区支持。通过将Kodi添加为连接，您可以在Sonarr添加新剧集时更新Kodi的库。
- Mailgun {#mailgun}
- Plex Home Theater {#plexhometheater}
  - 已弃用
- Plex Media Center {#plexclient}
  - 已弃用
- Plex Media Server {#plexserver}
  - 用于自托管Plex系统的服务器，启用此选项类似于Kodi，可以向您的Plex服务器推送更新通知，通知其有新的/升级的剧集可用。
  - 这很少需要，并且仅在Plex无法监视文件系统的更改时才需要。
  - 在Plex无法使用ionotify监视文件系统的少数情况下（例如某些类型的远程挂载和少数旧的网络挂载），建议使用plexautoscan应用程序而不是Plex连接。

> 请注意，这可能会触发对系列所在的库/根文件夹进行完整的库扫描。强烈建议使用仅监视文件系统的本机Plex功能，或使用类似[plexautoscan](https://github.com/l3uddz/plex_autoscan)的工具。{.is-warning}

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - 请参阅此[Tips and Tricks条目](/useful-tools#twitter)
- Webhook {#webhook}

# 列表

{#importlist}

- Sonarr {#sonarrimport}
  - TRaSH有一个[指南](https://trash-guides.info/Sonarr/Tips/Sync-2-radarr-sonarr/)，用于同步两个实例
- Plex Watchlist {#pleximport}
  - 只需为经过身份验证的Plex用户添加一个Plex watchlist到Radarr即可。请注意，您的列表上必须包含剧集。
  - 要拥有多个用户的观看列表，您需要添加每个用户的列表并使用其Plex用户进行身份验证。
- Trakt List {#traktlistimport}
  - 用户名 - 确保输入的是用户的实际用户名，而不是用户的名称
  - 列表 - 确保使用列表URL中呈现的列表名称
  - 示例：`https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - 用户名：`some-user-name`
    - 列表：`trakt-list-name`
- Trakt Popular List {#traktpopularimport}
- Trakt User {#traktuserimport}

> Trakt列表应包含剧集，而不是单个剧集。Sonarr只会匹配和添加剧集。{.is-info}

# 元数据

{#metadata}

- Kodi (XBMC) / Emby {#xbmcmetadata}
  - 启用 - 启用此元数据类型的元数据文件创建
  - 系列元数据 - 创建带有完整系列元数据的`tvshow.nfo`
  - （高级选项）系列元数据URL - 使用TheTVDb系列URL创建`tvshow.nfo`
  - 剧集元数据 - 为每个剧集创建`<filename>.nfo`
  - 系列图像 - 创建各种系列图像，包括海报和横幅，命名为`poster.jpg`和`banner.jpg`
  - 季度图像 - 创建各种季度图像，包括海报和横幅，命名为`season##-poster.jpg`和`season##-banner.jpg`
  - 剧集图像 - 创建各种剧集图像，如缩略图，命名为`<filename>-thumb.jpg`
- Roksbox {#roksboxmetadata}
  - 启用 - 启用此元数据类型的元数据文件创建
  - 剧集元数据 - 为每个剧集创建`Season##\<filename>.xml`
  - 系列图像 - 创建`Series Title.jpg`
  - 季度图像 - 创建`Season ##.jpg`
  - 剧集图像 - 创建`Season##\<filename>.jpg`
- WDTV {#wdtvmetadata}
  - 启用 - 启用此元数据类型的元数据文件创建
  - 剧集元数据 - 为每个剧集创建`Season##\<filename>.xml`
  - 系列图像 - 创建`folder.jpg`
  - 季度图像 - 创建`Season ##\folder.jpg`
  - 剧集图像 - 创建`Season##\<filename>.metathumb`