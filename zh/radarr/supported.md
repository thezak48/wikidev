---
title: Radarr支持的功能
description: 
published: true
date: 2023-09-01T16:45:41.479Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:24.002Z
---

# 目录

> 此页面正在进行中，需要额外的努力{.is-warning}

此页面是所有`支持的`维基链接（通常是UI中的“更多信息”）的消歧页面。

# 下载客户端

{#downloadclient}

- Aria2 {#aria2}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Deluge {#deluge}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Flood {#flood}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Hadouken {#hadouken}
  - [请参阅设置页面](/radarr/settings#download-clients)
- NZBGet {#nzbget}
  - [请参阅设置页面](/radarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [请参阅设置页面](/radarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [请参阅设置页面](/radarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [请参阅设置页面](/radarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Transmission {#transmission}
  - [请参阅设置页面](/radarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [请参阅设置页面](/radarr/settings#download-clients)
- uTorrent {#utorrent}
  - [请参阅设置页面](/radarr/settings#download-clients)
  - 由于uTorrent是广告软件和曾经的间谍软件，不建议使用。大多数用户使用Qbittorrent。
- Vuze {#vuze}
  - [请参阅设置页面](/radarr/settings#download-clients)

# 索引器

{#indexer}

## Usenet

- Newznab {#newznab}
  - [请参阅设置页面](/radarr/settings#indexer-settings)
  - Newznab是许多Usenet索引站点使用的标准化API。有许多预设可用，但所有预设都需要API密钥才能访问。
  - 像[Prowlarr](/prowlarr)和[NZBHydra2](https://github.com/theotherp/nzbhydra2)这样的索引器应用程序可以提供高级功能，如统计跟踪。
- omgwtfnzbs {#omgwtfnzbs}
  - 私有Usenet索引器的已废弃的旧实现。请改用Newznab。
  - [请参阅设置页面](/radarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - 私有Tracker
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- HDBits {#hdbits}
  - 私有Tracker
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 私有Tracker
  > IP Torrents的原生实现不支持搜索。请使用Prowlarr或Jackett作为torznab使用 {.is-info}
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 专门用于日本媒体（动漫）的Torrent Tracker。
  > Nyaa不赞成自动化，并经常会封禁您的IP。{.is-info}
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- Pass The Popcorn (PTP) {#passthepopcorn}
  - 私有Tracker
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 公共Tracker
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- Torrent RSS Feed {#torrentrssindexer}
  - 通用Torrent RSS feed解析器。
  > RSS feed必须包含`pubdate`。建议还提供发布大小。{.is-info}
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- TorrentPotato {#torrentpotato}
  - 旧版Couchpotato的Torznab格式。
  - [请参阅设置页面](/radarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab是Torrent和Newznab的谐音。它使用与Newznab API规范相同的结构和语法，但公开了特定于Torrent的属性和.torrent文件。因此，它支持最新的RSS feed和回溯搜索功能。该规范未由Newznab组织维护或支持。（与nZEDb共享相同的API规范）
  - 这主要由[Prowlarr](/prowlarr)和[Jackett](https://github.com/Jackett/Jackett)支持
  - [请参阅设置页面](/radarr/settings#indexer-settings)

> 许多Torrent Tracker依赖于社区，并可能制定了要求访问网站、获得声望、投票、评论等的规则。
> 请仔细阅读您的Tracker规则和礼仪，保持您的社区活跃。
> 如果您违反规则或积累了过多的Hit and Runs（HnRs）/低比率，我们不负责您的帐户被封禁。{.is-warning}

# 通知

{#notification}

- Boxcar {#boxcar}
- 自定义脚本 {#customscript}
  - 这允许您为特定操作创建自定义脚本，当发生此操作时，脚本将运行。有关更多详细信息，请参阅[自定义脚本](/radarr/custom-scripts)。
- Discord {#discord}
  - 到目前为止，这是推送Radarr上发生的操作的最常见方式
- 电子邮件 {#email}
  - 只需向自己或您想要打扰的某人发送电子邮件。如果您使用Gmail，则需要启用不安全的应用程序。如果您使用Gmail并启用了两步验证，则需要使用特定于应用程序的密码。

> 您可以使用“漂亮的地址”（如`SomePrettyName <email@example.org>`）{.is-info}

- Emby {#mediabrowser}
- Gotify {#gotify}
- Join {#join}
- Kodi {#xbmc}
  - Kodi源于对媒体的热爱。它是一个将您的所有数字媒体整合到一个美观且用户友好的软件包中的娱乐中心。它是100%免费和开源的，非常可定制，并可在各种设备上运行。它由一支专门的志愿者团队和一个庞大的社区支持。通过将Kodi作为连接添加到Radarr中，您可以在Radarr添加新电影时更新Kodi的库。
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - 有关[有用的工具-Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)的条目
- Plex Media Server {#plexserver}
  - 用于自托管Plex系统的服务器，启用此选项类似于Kodi，它将允许您向Plex服务器推送更新，通知其有新的/升级的电影可用。
  - 这很少需要，只有在Plex无法监视文件系统的更改时才需要。
  - 在Plex无法使用ionotify监视文件系统的少数情况下，例如某些类型的远程挂载和少数旧的网络挂载，建议使用plexautoscan应用程序而不是Plex连接
- 使用[plexautoscan](https://github.com/l3uddz/plex_autoscan)等工具也是一个选择。

- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushcut {#pushcut}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Synology Indexer {#synologyindexer}
- Telegram {#telegram}
- Trakt {#trakt}
- Twitter {#twitter}
  - 请参阅此[Tips and Tricks条目](/useful-tools#twitter)
- Webhook {#webhook}

# 列表

{#importlist}

- CouchPotato {#couchpotatoimport}
- 自定义列表 {#radarrlistimport}
- IMDb列表 {#imdblistimport}
  - 要添加IMDb Watchlist，请转到您的列表并单击编辑。确保隐私设置设置为公开。在地址栏中，您将找到需要输入到Radarr中的`lsxxxxxx`号码。

    1. 转到您的IMDB列表设置
    1. 确保隐私设置为`Public`（即`Disabled`）
    1. 使用URL中的`ls`号码

  ![imdb-list-ls.png](/assets/radarr/imdb-list-ls.png)
- Plex Watchlist {#plex}
  - 需要：v4.1.0.6176+
  - 只需为经过身份验证的Plex用户在Radarr中添加Plex watchlist。请注意，您的列表必须包含电影。
  - 要拥有多个用户的观看列表，您需要添加每个用户的列表并使用其Plex用户进行身份验证。
- Radarr {#radarrimport}
  - TRaSH有一个[指南](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)来同步两个实例
- RSS列表 {#rssimport}
- StevenLu自定义 {#stevenluimport}
	- 允许您以json格式创建自定义电影列表。
  	您的feed对于每部电影都需要提供`title`或`imdb_id`，两者都可以提供。
  		> 请注意，`imdb_id`比`title`更安全，因为它不需要广泛搜索
    这是一个有效的样本json： 
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
      - 可以在items中添加其他键（将被忽略）
      - 对于空列表，只需返回一个空的json数组`[]`
- StevenLu列表 {#stevenlu2import}
- TMDb Collection {#tmdbcollectionimport}
  - 在Radarr v4.2中不再支持Collection列表，已迁移到Radarr中的collections。有关更多详细信息，请参阅[集合](/radarr/library#collections)部分。
- TMDb公司 {#tmdbcompanyimport}
- TMDb关键字 {#tmdbkeywordimport}
- TMDb列表 {#tmdblistimport}
- TMDb人物 {#tmdbpersonimport}
  - 如果TMDb人物的URL是`https://www.themoviedb.org/person/500-tom-cruise`，则人物ID是`500`
- TMDb热门 {#tmdbpopularimport}
  - Top使用<https://developers.themoviedb.org/3/movies/get-top-rated-movies>
  - Popular使用<https://developers.themoviedb.org/3/movies/get-popular-movies>
  - Theaters使用<https://developers.themoviedb.org/3/movies/get-now-playing>
  - Upcoming使用<https://developers.themoviedb.org/3/movies/get-upcoming>
- TMDb用户 {#tmdbuserimport}
- Trakt列表 {#traktlistimport}
  - 用户名 - 确保输入实际用户的用户名，而不是用户的名称
  - 列表 - 确保使用列表URL中呈现的列表名称
  - 示例：`https://trakt.tv/users/some-user-name/lists/trakt-list-name?sort=rank,asc`
    - 用户名：`some-user-name`
    - 列表：`trakt-list-name`
- Trakt热门列表 {#traktpopularimport}
- Trakt用户 {#traktuserimport}
  - 当使用自己的观看列表时，应使用此类型

# 元数据

{#metadata}

- Emby（旧版） {#mediabrowsermetadata}
  - 启用 - 启用此元数据类型的元数据文件创建
  - 电影元数据 - 启用此元数据类型的元数据文件创建
- Kodi（XBMC）/ Emby {#xbmcmetadata}
  - 启用 - 启用此元数据类型的元数据文件创建
  - 电影元数据 - 创建包含电影元数据的`<filename>.nfo`文件
  - （高级选项）电影元数据URL - 创建具有TMDb和IMDb电影URL的`movie.nfo`文件
  - 元数据语言 - 选择Radarr应使用的语言来写入元数据（如果该语言可用）
  - 电影图片 - 创建各种季节图片，包括海报和横幅
  - 使用Movie.nfo - 将nfo文件写为`movie.nfo`而不是默认值
  - 集合名称 - Radarr将集合名称写入.nfo文件
- Roksbox {#roksboxmetadata}
  - 启用 - 启用此元数据类型的元数据文件创建
  - 电影元数据 - 为每部电影创建xml文件
  - 电影图片 - 创建`Movie.jpg`
- WDTV {#wdtvmetadata}
  - 启用 - 启用此元数据类型的元数据文件创建
  - 电影元数据 - 为每个剧集创建`<filename>.xml`
  - 电影图片 - 创建`folder.jpg`