---
title: Readarr 支持的功能
description: 
published: true
date: 2022-01-07T19:44:47.143Z
tags: 
editor: markdown
dateCreated: 2021-06-23T07:55:28.684Z
---

> 本页面正在制作中，需要额外的努力{.is-warning}

本页面是所有“支持的”维基链接（通常在用户界面中为“更多信息”）的消歧页面。

# 下载客户端

{#downloadclient}

- Aria2 {#aria2}
  - [请参考设置页面](/readarr/settings#download-clients)
- Deluge {#deluge}
  - [请参考设置页面](/readarr/settings#download-clients)
- Download Station {#torrentdownloadstation}
  - [请参考设置页面](/readarr/settings#download-clients)
- Download Station {#usenetdownloadstation}
  - [请参考设置页面](/readarr/settings#download-clients)
- Flood {#flood}
  - [请参考设置页面](/readarr/settings#download-clients)
- Hadouken {#hadouken}
  - [请参考设置页面](/readarr/settings#download-clients)
- NZBGet {#nzbget}
  - [请参考设置页面](/readarr/settings#download-clients)
- NZBVortex {#nzbvortex}
  - [请参考设置页面](/readarr/settings#download-clients)
- Pneumatic {#pneumatic}
  - [请参考设置页面](/readarr/settings#download-clients)
- qBittorrent {#qbittorrent}
  - [请参考设置页面](/readarr/settings#download-clients)
- rTorrent {#rtorrent}
  - [请参考设置页面](/readarr/settings#download-clients)
- SABnzbd {#sabnzbd}
  - [请参考设置页面](/readarr/settings#download-clients)
- Torrent Blackhole {#torrentblackhole}
  - [请参考设置页面](/readarr/settings#download-clients)
- Transmission {#transmission}
  - [请参考设置页面](/readarr/settings#download-clients)
- Usenet Blackhole {#usenetblackhole}
  - [请参考设置页面](/readarr/settings#download-clients)
- uTorrent {#utorrent}
  - [请参考设置页面](/readarr/settings#download-clients)
  - 由于uTorrent是广告软件，曾经是间谍软件，不推荐使用。大多数用户使用qBittorrent
- Vuze {#vuze}
  - [请参考设置页面](/readarr/settings#download-clients)

# 索引器

{#indexer}

## Usenet

- Newznab {#newznab}
  - [请参考设置页面](/readarr/settings#indexer-settings)
  - Newznab是许多Usenet索引站点使用的标准化API。有许多预设可用，但都需要API密钥才能访问。
  - 像[Prowlarr](/prowlarr)和[NZBHydra2](https://github.com/theotherp/nzbhydra2)这样的索引器应用程序可以提供高级功能，如统计跟踪。
- omgwtfnzbs {#omgwtfnzbs}
  - 私人Usenet索引站点
  - [请参考设置页面](/readarr/settings#indexer-settings)

## Torrents

- FileList {#filelist}
  - [请参考设置页面](/readarr/settings#indexer-settings)
- Gazelle API {#gazelle}
  - [请参考设置页面](/readarr/settings#indexer-settings)
- IP Torrents {#iptorrents}
  - 私人Tracker
  > IP Torrents的原生实现不支持搜索{.is-info}
  - [请参考设置页面](/readarr/settings#indexer-settings)
- Nyaa {#nyaa}
  - 专门用于日本媒体（动漫）的Torrent Tracker。
  > Nyaa不赞成自动化，并经常会封禁您的IP{.is-info}
  - [请参考设置页面](/readarr/settings#indexer-settings)
- Rarbg {#rarbg}
  - 公共Tracker
  - [请参考设置页面](/readarr/settings#indexer-settings)
- Torrent RSS Feed {#torrentrssindexer}
  - 通用的Torrent RSS feed解析器。
  > RSS feed必须包含`pubdate`。建议同时包含发布大小{.is-info}
  - [请参考设置页面](/readarr/settings#indexer-settings)
- TorrentLeech {#torrentleech}
  - 私人索引器
  - [请参考设置页面](/readarr/settings#indexer-settings)
- Torznab {#torznab}
  - Torznab是Torrent和Newznab的谐音。它使用与Newznab API规范相同的结构和语法，但公开了特定于Torrent的属性和.torrent文件。因此，它支持最新的RSS feed和回溯搜索功能。该规范不受Newznab组织的维护和支持。（与nZEDb共享相同的API规范）
  - 这主要由[Prowlarr](/prowlarr)和[Jackett](https://github.com/Jackett/Jackett)支持
  - [请参考设置页面](/readarr/settings#indexer-settings)

# 通知

{#notification}

- Boxcar {#boxcar}
- Custom Script {#customscript}
  - 这允许您为特定操作编写自定义脚本，当发生该操作时，脚本将运行。有关更多详细信息，请参阅[自定义脚本](/readarr/custom-scripts)。
- Discord {#discord}
  - 远远是推送Readarr上发生的操作的最常见方式之一
- Email {#email}
  - 只需向自己或您想要打扰的某人发送电子邮件。如果您使用Gmail，则需要启用不安全的应用程序访问权限。如果您使用Gmail并启用了两步验证，则需要使用特定于应用程序的密码。

 > 您可以使用“漂亮的地址”（如`SomePrettyName <email@example.org>`）{.is-info}

- GoodReads 书架 {#goodreadsbookshelf}
- GoodReads 拥有的书籍 {#goodreadsownedbooks}
- Gotify {#gotify}
- Join {#join}
- Mailgun {#mailgun}
- Notifiarr {#notifiarr}
  - 请参阅[有用的工具 - Notifiarr](/useful-tools#notifiarr-fka-discord-notifier)中的条目
- Prowl {#prowl}
- Pushbullet {#pushbullet}
- Pushover {#pushover}
- SendGrid {#sendgrid}
- Slack {#slack}
- Subsonic {#subsonic}
- Synology 索引器 {#synologyindexer}
- Telegram {#telegram}
- Twitter {#twitter}
  - 请参阅此[技巧和技巧条目](/useful-tools#twitter)
- Webhook {#webhook}

# 列表

{#importlist}

- GoodReads 书架 {#goodreadsbookshelf}
  - (高级选项) 用户ID - 如果不是您的用户ID，请在此处输入用户ID。
  - 书架 - 从GoodReads选择要导入的书架
  - 与GoodReads进行身份验证 - 单击按钮与GoodReads进行身份验证。

> 可以将多个GoodReads用户作为单独的列表添加。除了使用经过身份验证的用户外，还可以通过启用高级选项并输入用户ID，然后单击与GoodReads进行身份验证以获取用户的书架。{.is-info}

- GoodReads 拥有的书籍 {#goodreadsownedbooks}
  - (高级选项) 用户ID - 如果不是您的用户ID，请在此处输入用户ID。
  - 书架 - 从GoodReads选择要导入的书架
  - 与GoodReads进行身份验证 - 单击按钮与GoodReads进行身份验证。

> 可以将多个GoodReads用户作为单独的列表添加。除了使用经过身份验证的用户外，还可以通过启用高级选项并输入用户ID，然后单击与GoodReads进行身份验证以获取用户的书架。{.is-info}

- GoodReads 列表 {#goodreadslistimportlist}
  - 列表ID - 输入要添加为列表的GoodReads公共列表ID
- GoodReads 系列 {#goodreadsseriesimportlist}
  - 系列ID - 输入要添加为列表的GoodReads系列ID
- LazyLibrarian {#lazylibrarianimport}
  - URL - 您的LazyLibrarian实例的URL
  - API密钥 - 您的LazyLibrarian实例的API密钥
- Readarr {#readarrimport}
  - 完整URL - 要从中导入的Readarr实例的完整URL，例如`http://localhost:8787/readarr`
  - API密钥 - 要从中导入的Readarr实例的API密钥
  - 配置文件 - 要从中导入的Readarr实例的配置文件
  - 标签 - 要从中导入的Readarr实例的标签

# 元数据

{#metadata}

- Calibre {#calibre}
  - [请参考设置页面](/readarr/settings#write-metadata-to-book-files)
- 音频标签 {#audiotagging}
  - [请参考设置页面](/readarr/settings#write-metadata-to-book-files)