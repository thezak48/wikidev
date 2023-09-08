---
title: Sonarr设置
description: 
published: true
date: 2023-04-29T18:16:05.634Z
tags: sonarr, 需要改进, 设置
editor: markdown
dateCreated: 2021-06-11T23:29:12.300Z
---

# 目录

- [目录](#目录)
- [菜单选项](#菜单选项)
- [媒体管理](#媒体管理)
  - [社区命名建议](#社区命名建议)
  - [剧集命名](#剧集命名)
    - [标准剧集格式](#标准剧集格式)
    - [剧集命名](#剧集命名)
    - [剧集ID](#剧集id)
    - [季](#季)
    - [剧集](#剧集)
    - [播出日期](#播出日期)
    - [剧集标题](#剧集标题)
    - [画质](#画质)
    - [媒体信息](#媒体信息)
    - [其他](#其他)
    - [原始](#原始)
  - [每日剧集格式](#每日剧集格式)
  - [动画剧集格式](#动画剧集格式)
    - [绝对剧集编号](#绝对剧集编号)
  - [剧集文件夹格式](#剧集文件夹格式)
    - [剧集命名](#剧集命名-1)
    - [剧集ID](#剧集id-1)
  - [季文件夹格式](#季文件夹格式)
    - [季](#季-1)
  - [季文件夹格式](#季文件夹格式-1)
    - [特别篇](#特别篇)
  - [多集风格](#多集风格)
  - [文件夹](#文件夹)
  - [导入](#导入)
  - [文件管理](#文件管理)
  - [权限](#权限)
  - [根文件夹](#根文件夹)
- [配置文件](#配置文件)
  - [画质配置](#画质配置)
  - [语言配置](#语言配置)
  - [延迟配置](#延迟配置)
    - [用途](#用途)
    - [延迟配置的工作原理](#延迟配置的工作原理)
      - [示例](#示例)
        - [示例1](#示例1)
        - [示例2](#示例2)
        - [示例3](#示例3)
  - [发布配置](#发布配置)
- [画质](#画质-1)
  - [画质表格含义](#画质表格含义)
  - [定义的画质](#定义的画质)
- [索引器](#索引器)
  - [支持的索引器](#支持的索引器)
    - [索引器设置](#索引器设置)
    - [Usenet索引器配置](#usenet索引器配置)
    - [Torrent Tracker配置](#torrent-tracker配置)
  - [选项](#选项)
- [下载客户端](#下载客户端)
  - [概述](#概述)
  - [下载客户端进程](#下载客户端进程)
  - [Usenet](#usenet)
  - [BitTorrent](#bittorrent)
  - [下载客户端](#下载客户端-1)
    - [支持的下载客户端](#支持的下载客户端)
    - [Usenet客户端设置](#usenet客户端设置)
    - [Torrent客户端设置](#torrent客户端设置)
    - [Torrent客户端删除下载兼容性](#torrent客户端删除下载兼容性)
  - [完成的下载处理](#完成的下载处理)
    - [删除已完成的下载](#删除已完成的下载)
    - [下载失败处理](#下载失败处理)
  - [远程路径映射](#远程路径映射)
- [导入列表](#导入列表)
  - [列表](#列表)
  - [列表排除](#列表排除)
- [连接](#连接)
  - [连接](#连接-1)
  - [连接触发器](#连接触发器)
- [元数据](#元数据)
  - [元数据](#元数据-1)
- [标签](#标签)
- [常规](#常规)
  - [主机](#主机)
  - [安全](#安全)
  - [代理](#代理)
  - [日志](#日志)
  - [分析](#分析)
  - [更新](#更新)
  - [备份](#备份)
- [用户界面](#用户界面)
  - [日历](#日历)
  - [日期](#日期)
  - [样式](#样式)
  
本页面将介绍Sonarr中所有可用的设置及其工作原理。这不是一份全面的“如何设置Sonarr”的文档。请参考[快速入门](/sonarr/quick-start-guide)页面。

# 菜单选项

要进入设置页面，请从左侧菜单中选择“设置”。将显示以下子菜单选项：

![settings_1_menu.png](/assets/sonarr/settings_1_menu.png)

此外，请注意对于每个单独的设置页面，菜单顶部有一些选项：

![settings_2_topmenu.png](/assets/sonarr/settings_2_topmenu.png)

- 隐藏/显示高级选项对于任何标记为“(高级选项)”的项目都很重要，否则它们将不会显示。这些菜单项在截图中以橙色显示。

- 在离开屏幕之前，您必须保存更改。点击磁盘图标即可保存。如果您没有进行任何更改，它将显示“无更改”并变为灰色，如上所示。

# 媒体管理

> 以下设置仅在“显示高级设置”中可见，该选项位于搜索栏下方的顶部栏中{.is-info}

## 社区命名建议

> 下面是来自[TRaSH的指南](https://trash-guides.info/Sonarr/Sonarr-recommended-naming-scheme/)的一些建议{.is-info}

> 警告：从v3.0.6.1431开始，Sonarr现在支持识别Dolby Vision（DV）和高动态范围（HDR）类型。如果您使用的是较低版本，请将`{[MediaInfo VideoDynamicRangeType]}`替换为`{[MediaInfoVideoDynamicRange]}`{.is-warning}

- 标准剧集：`{Series TitleYear} - S{season:00}E{episode:00} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- 每日剧集：`{Series TitleYear} - {Air-Date} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}{[Mediainfo AudioCodec}{ Mediainfo AudioChannels]}{MediaInfo AudioLanguages}{[MediaInfo VideoCodec]}{-Release Group}`

- 动画剧集：`{Series TitleYear} - S{season:00}E{episode:00} - {absolute:000} - {Episode CleanTitle} [{Preferred Words }{Quality Full}]{[MediaInfo VideoDynamicRangeType]}[{MediaInfo VideoBitDepth}bit]{[MediaInfo VideoCodec]}[{Mediainfo AudioCodec} { Mediainfo AudioChannels}]{MediaInfo AudioLanguages}{-Release Group}`

- 季文件夹：`Season {season:00}`

- 多集风格：`Scene`

- 剧集文件夹：`{Series TitleYear} [imdb-{ImdbId}]`

## 剧集命名

- 重命名剧集 - 选中以启用Sonarr重命名文件
  - 如果未选中：
    - 下载客户端导入
      - 非季度包：使用下载客户端的发布标题
      - 季度包：原始文件名
    - 手动（临时）导入：原始文件名

- 替换非法字符 - 如果未选中，Sonarr将删除它们。
  - 这些字符是：`:` `\` `/` `>` `<` `?` `*` `|` `"`

### 标准剧集格式

标准剧集格式 - 设置标准剧集类型剧集的命名约定。单击`?`图标以打开`文件名标记`对话框。

- 下拉框（右上角）
  - 左框 - 空格处理
  - 空格 ( ) - 在命名中使用空格（默认）
  - 句点 (.) - 在命名中使用句点代替空格
  - 下划线 (_) - 在命名中使用下划线代替空格
  - 破折号 (-) - 在命名中使用破折号代替空格
  - 右框 - 大小写处理
  - 默认大小写 - 将标题大写和小写（~驼峰命名）（默认）
  - 大写 - 将标题全部大写
  - 小写 - 将标题全部小写

### 剧集命名

- `{Series Title}` = 剧集名称的标题！
- `{Series CleanTitleYear}` = 剧集名称的标题！2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = 剧集名称的标题！
- `{Series TitleThe}` = 剧集名称的标题！, The
- `{Series TitleYear}` = 剧集名称的标题（2010）
- `{Series Year}` = （2010）

### 剧集ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}`= 54321

### 季

- `{season:0}` = 1
- `{season:00}` =  01

### 剧集

- `{episode:0}` = 1
- `{episode:00}` = 01

### 播出日期

- `{Air-Date}` = 2020-09-03
- `{Air Date}` = 2020 09 03

### 剧集标题

- `{Episode Title}` = 剧集标题
- `{Episode CleanTitle}` =  剧集标题

### 画质

- `{Quality Full}` = HDTV 720p Proper
- `{Quality Title}` = HDTV 720p

### 媒体信息

- `{MediaInfo Simple}` = x264 DTS
- `{MediaInfo Full}` = x264 DTS \[EN+DE\]
- `{MediaInfo AudioCodec}` = DTS
- `{MediaInfo AudioChannels}` = 5.1
- `{MediaInfo AudioLanguagesAll}` = \[DE\]
- `{MediaInfo AudioLanguagesAll}` = \[EN+DE\]
- `{MediaInfo SubtitleLanguages}` = \[EN\]
- `{MediaInfo VideoCodec}` = x264
- `{MediaInfo VideoBitDepth}` = 8
- `{MediaInfo VideoDynamicRange}` = HDR
- `{MediaInfo VideoDynamicRangeType}` = DV HDR10

> `MediaInfo Full`、`AudioLanguages`和`SubtitleLanguages`支持`:EN+DE`后缀，允许您过滤文件名中包含的语言。使用`-DE`来排除特定语言。附加<kb>+</kb>（例如：`:EN+`）将输出`[EN]`、`[EN+--]`或`[--]`，具体取决于排除的语言。例如`{MediaInfo Full:EN+DE}`。
{.is-info}

> 如果只存在一种语言且为EN（英语），则`AudioLanguages`不会显示语言。要获得所需的行为，并且作为显示德语和英语的示例，请改用`{MediaInfo AudioLanguagesAll:DE+EN}`。
{.is-info}

> `MediaInfo VideoDynamicRangeType`将给出可能的值：DV、DV HDR10、HDR10、HDR10Plus、HLG、PQ和HDR
{.is-info}

### 其他

- `{Release Group}` = Rls Grp
- `{Preferred Words}` = iNTERNAL或NF

> \* Preferred words将是与您的任何首选词的字面匹配的单词。上述示例将是首选词`iNTERNAL`，或者类似的首选词`/\b(amzn|amazon)\b(?=[ ._-]web[ ._-]?(dl|rip)\b)/i`将返回`AMZN`或`Amazon`{.is-info}

### 原始

- `{Original Title}` = Series.Title.S01E01.WEBDL.NF.1080P.x264-EVOLVE
- `{Original Filename}` = Series.title.s01e01.WEBDL.NF.1080P.x264-EVOLVE

> 建议使用`Original Title`作为发布名称。
{.is-info}

>`Original Filename`不建议使用。它是字面原始文件名，可能会被混淆`t1i0p3s7i8yu7ti`。
{.is-warning}

## 每日剧集格式

每日剧集格式 - 设置每日剧集类型剧集的命名约定。单击`?`图标以打开`文件名标记`对话框。

有关此对话框的更多信息，请参见[标准剧集格式](/sonarr/settings#standard-episode-format)。

## 动画剧集格式

动画剧集格式 - 设置动画剧集类型剧集的命名约定。单击`?`图标以打开`文件名标记`对话框。

有关此对话框的更多信息，请参见[标准剧集格式](/sonarr/settings#standard-episode-format)。

### 绝对剧集编号

- `{absolute:0}` = 1
- `{absolute:00}` = 01
- `{absolute:000}` =001

## 剧集文件夹格式

（高级选项）- 剧集文件夹 - 设置文件夹的命名约定。单击`?`图标以打开`文件名标记`对话框。

### 剧集命名

- `{Series Title}` = 剧集名称！
- `{Series CleanTitleYear}` = 剧集名称！2010
- `{Series TitleFirstCharacter}` = S
- `{Series CleanTitle}` = 剧集名称！
- `{Series TitleThe}` = 剧集名称！, The
- `{Series TitleYear}` = 剧集名称（2010）
- `{Series Year}` = （2010）

### 剧集ID

- `{ImdbId}` = tt12345
- `{Tmdbid}` = 123456
- `{TvMazeId}` = 54321

## 季文件夹格式

### 季

- `{season:0}` = 1
- `{season:00}` = 01

## 季文件夹格式

### 特别篇

`Specials`（季）文件夹的名称

- `Specials`

> 建议使用`Specials`{.is-info}

## 多集风格

- `Extend` = `S01E01-02-03`
- `Duplicate` = `S01E01.S01E01`
- `Repeat` = `S01E01E02E03`
- `Scene` = `S01E01-E02-E03`
- `Range` = `S01E01-03`
- `Prefixed Range` = `S01E01-E03`

> 建议使用`Scene`{.is-info}

## 文件夹

- 创建空媒体文件夹 - 在磁盘扫描期间创建缺失的剧集文件夹
- 删除空文件夹 - 在磁盘扫描期间和删除剧集文件和季文件时删除空的剧集和季文件夹

## 导入



- SDTV - Standard Definition Television
- WEBDL-480p - Web-DL at 480p resolution
- DVD - DVD quality
- HDTV-720p - High Definition Television at 720p resolution
- WEBDL-720p - Web-DL at 720p resolution
- BluRay-720p - Blu-ray at 720p resolution
- HDTV-1080p - High Definition Television at 1080p resolution
- WEBDL-1080p - Web-DL at 1080p resolution
- BluRay-1080p - Blu-ray at 1080p resolution
- HDTV-2160p - High Definition Television at 2160p resolution
- WEBDL-2160p - Web-DL at 2160p resolution
- BluRay-2160p - Blu-ray at 2160p resolution
- Raw-HD - Raw High Definition
- Full-Bluray - Full Blu-ray quality
- HDTV-4K - High Definition Television at 4K resolution
- WEBDL-4K - Web-DL at 4K resolution
- BluRay-4K - Blu-ray at 4K resolution

- 未知 - 自解释
- SDTV - 从模拟源（通常是有线电视或OTA标清）录制的剧集。图像质量通常很好（对于分辨率来说），通常使用DivX/XviD或MP4进行编码。
- WEBDL-480p - WEB-DL（P2P）是指从流媒体服务（如Netflix、Amazon Video、Hulu、Crunchyroll、Discovery GO、BBC iPlayer等）无损地提取的文件，或者通过在线分发网站（如iTunes）下载的文件。质量非常好，因为它们没有重新编码。视频（H.264或H.265）和音频（AC3/AAC）流通常是从iTunes或Amazon Video中提取的，并重新封装到MKV容器中，而不会损失质量。这些发布的优点是，与BD/DVDRips一样，它们通常没有屏幕上的网络标志。这些几乎和蓝光源一样好，但可能会因为流媒体服务的自适应比特率而出现音频延迟或视觉伪影。如果撕裂者的互联网连接下降到比特率降低的程度，源比特率可能会动态变化，导致画质的变化。大多数受到极大视觉伪影影响的发布都会被NUKED，通常会发布一个PROPER版本来修复自适应比特率的任何异常变化。这将是480p（标清）质量。
- WEBRip-480p - 在WEB-Rip（P2P）中，文件通常使用HLS或RTMP/E协议提取，并从TS、MP4或FLV容器重新封装为MKV。这将是480p（标清）质量。
- DVD - 最终发布的DVD9的重新编码。如果可能的话，这将在零售前发布。对于分辨率来说，它应该是优秀的质量。DVDrips通常以DivX/XviD或MP4格式发布。
- Bluray-480p - 最终发布的蓝光的重新编码，降低到480p分辨率（720x480 @ 16:9，其他宽高比可能是不同的分辨率）。如果可能的话，这将在零售前发布。对于分辨率来说，它应该是优秀的质量。比特率可能会有所不同，但通常编码为DivX、XviD或AVC，并在大大减小文件大小的同时略微降低原始源的感知质量。这些通常是MKV或MP4，但也有一些使用AVI的DivX/XviD。
- HDTV-720p - 最终发布的蓝光的重新编码，但通过高清有线电视或卫星广播（1280x720 @ 16:9，其他宽高比可能是不同的分辨率）。它可能会根据所属网络的运行时间或内容进行修改。通常在零售发布几个月后发布，但有时会在像STARZ或HBO这样的有线频道上发布标准定义电影的放大版本，它们可能是该特定电影的唯一高清副本。这些通常是MKV或MP4。
- HDTV-1080p - 最终发布的蓝光的重新编码，但通过高清有线电视或卫星广播（1920x1080 @ 16:9，其他宽高比可能是不同的分辨率）。它可能会根据所属网络的运行时间或内容进行修改。通常在零售发布几个月后发布，但有时会在像STARZ或HBO这样的有线频道上发布标准定义电影的放大版本，它们可能是该特定电影的唯一高清副本。这些通常是MKV或MP4容器。
- Raw-HD - 高清流的原始源。
- WEBRip-720p - 在WEB-Rip（P2P）中，文件通常使用HLS或RTMP/E协议提取，并从TS、MP4或FLV容器重新封装为MKV。这将是720p质量。
- Bluray-720p - 最终发布的蓝光的重新编码，降低到720p分辨率（1280x720 @ 16:9，其他宽高比可能是不同的分辨率）。如果可能的话，这将在零售前发布。对于分辨率来说，它应该是优秀的质量。比特率可能会有所不同，但通常编码为AVC或HEVC，并在大大减小文件大小的同时略微降低原始源的感知质量。这些通常是MKV或MP4容器。
- WEBDL-1080p - WEB-DL（P2P）是指从流媒体服务（如Netflix、Amazon Video、Hulu、Crunchyroll、Discovery GO、BBC iPlayer等）无损地提取的文件，或者通过在线分发网站（如iTunes）下载的文件。质量非常好，因为它们没有重新编码。视频（H.264或H.265）和音频（AC3/AAC）流通常是从iTunes或Amazon Video中提取的，并重新封装到MKV容器中，而不会损失质量。这些发布的优点是，与BD/DVDRips一样，它们通常没有屏幕上的网络标志。这些几乎和蓝光源一样好，但可能会因为流媒体服务的自适应比特率而出现音频延迟或视觉伪影。如果撕裂者的互联网连接下降到比特率降低的程度，源比特率可能会动态变化，导致画质的变化。大多数受到极大视觉伪影影响的发布都会被NUKED，通常会发布一个PROPER版本来修复自适应比特率的任何异常变化。这将是1080p质量。
- WEBRip-1080p - 在WEB-Rip（P2P）中，文件通常使用HLS或RTMP/E协议提取，并从TS、MP4或FLV容器重新封装为MKV。这将是1080p质量。
- Bluray-1080p - 最终发布的蓝光的重新编码，以其本机1080p分辨率（1920x1080 @ 16:9，其他宽高比可能是不同的分辨率）。如果可能的话，这将在零售前发布。对于分辨率来说，它应该是优秀的质量，与源相同。比特率可能会有所不同，但通常编码为AVC或HEVC，并在大大减小文件大小的同时略微降低原始源的感知质量。这些通常是MKV或MP4容器。
- Remux-1080p - Remux是将蓝光或HD DVD光盘转换为另一种容器格式或仅剥离光盘的菜单和附加材料，同时保持其音频和视频流的内容（也保持当前编解码器），保证与原始光盘上的电影质量完全相同。这是1080p质量。
- HDTV-2160p - TVRip是从捕获卡中捕获的源。HDTV代表从高清电视捕获的源。使用HDTV源，质量有时甚至可以超过DVD。这种格式的电影越来越受欢迎。在某些发布中可以看到一些广告和商业横幅。这是2160p（4K）质量。
- WEBDL-2160p - WEB-DL（P2P）是指从流媒体服务（如Netflix、Amazon Video、Hulu、Crunchyroll、Discovery GO、BBC iPlayer等）无损地提取的文件，或者通过在线分发网站（如iTunes）下载的文件。质量非常好，因为它们没有重新编码。视频（H.264或H.265）和音频（AC3/AAC）流通常是从iTunes或Amazon Video中提取的，并重新封装到MKV容器中，而不会损失质量。这些发布的优点是，与BD/DVDRips一样，它们通常没有屏幕上的网络标志。这些几乎和蓝光源一样好，但可能会因为流媒体服务的自适应比特率而出现音频延迟或视觉伪影。如果撕裂者的互联网连接下降到比特率降低的程度，源比特率可能会动态变化，导致画质的变化。大多数受到极大视觉伪影影响的发布都会被NUKED，通常会发布一个PROPER版本来修复自适应比特率的任何异常变化。这将是2160p（4K）质量。
- WEBRip-2160p - 在WEB-Rip（P2P）中，文件通常使用HLS或RTMP/E协议提取，并从TS、MP4或FLV容器重新封装为MKV。这将是2160p（4K）质量。
- Bluray-2160p - 最终发布的蓝光的重新编码，以其本机2160p分辨率（3840x2160 @ 16:9，其他宽高比可能是不同的分辨率）。4K版本的电影通常使用HEVC编解码器，并且可以是8位或10位色彩重现或来自HDR源。稍微减小文件大小。这些通常是MKV或MP4容器。
- Remux-2160p - Remux是将蓝光或HD DVD光盘转换为另一种容器格式或仅剥离光盘的菜单和附加材料，同时保持其音频和视频流的内容（也保持当前编解码器），保证与原始光盘上的电影质量完全相同。这是2160p（4K）质量。

# 索引器

> 可以在此部分的[更多信息（支持的）](/sonarr/supported#indexers)页面找到有关支持的索引器的信息
{.is-info}

## 支持的索引器

- 支持的索引器列表位于[更多信息（支持的）](/sonarr/supported#indexers)页面上

### 索引器设置

- 单击<kb>+</kb>按钮添加新索引器后，将出现一个新窗口，其中包含许多不同的选项。在本维基中，Sonarr将Usenet索引器和Torrent跟踪器都视为“索引器”。

- 这里有两个部分：Usenet和Torrents。根据您将要使用的下载客户端，您将要选择要使用的索引器类型。

### Usenet索引器配置

- Newznab - 在这里，您将找到流行的Usenet索引器的预设（已填写，您只需要提供您选择的Usenet索引器提供的API密钥），以及创建自定义索引器的能力
- 与Usenet很好地集成的软件有[NZBHydra2](https://github.com/theotherp/nzbhydra2/)或[Prowlarr](/prowlarr)，它们与Usenet和Torrents集成
- 无论您选择预设的索引器还是自定义索引器设置，都将出现一个新窗口以输入所有设置
- 从预设中选择或添加自定义索引器（例如NZBHydra2或Prowlarr）
- 名称 - 索引器在Sonarr中的名称
- 启用RSS - 如果启用，使用此索引器监视所需但缺失或尚未达到其截止时间的文件。
- 启用自动搜索 - 如果启用，使用此索引器进行自动搜索，包括添加时搜索
- 启用交互式搜索 - 如果启用，使用此索引器进行手动交互式搜索。
- URL - 索引器提供的URL，例如`https://api.nzbgeek.info`。
- API路径 - 索引器提供的API路径。通常为`/api`
- API密钥 - 索引器提供的访问API的密钥。
- 类别 - 默认类别将被使用，除非进行编辑。这些默认类别可能不是最佳选择。在编辑此设置时，Sonarr会查询索引器以获取其可用类别，并在可选择的列表中显示它们。一旦切换了类别，旧的默认值将被清除。
- 动画类别 - Sonarr将用于动画搜索的类别。除非进行编辑，否则不会使用任何类别。在编辑此设置时，Sonarr会查询索引器以获取其可用类别，并在可选择的列表中显示它们。一旦切换了类别，旧的默认值将被清除。
- 动画标准格式搜索 - 也使用标准编号搜索动画（仅适用于动画系列类型）[有关系列类型的更多信息请点击此处](/sonarr/faq#whats-the-different-series-types)
- （高级选项）附加参数 - 添加到查询链接的其他Newznab参数
- （高级选项）索引器优先级 - 在发布决胜场景中优先选择此索引器而不是另一个索引器。1是最高优先级，50是最低优先级。
- （高级选项）下载客户端 - 选择并指定用于从此索引器抓取的下载客户端
- 标签 - 仅对具有至少一个匹配标签的系列使用此索引器。留空以用于所有系列。

### Torrent跟踪器配置

- 与Usenet一样，有各种预设的Torrent跟踪器信息。如果您不是这些特定跟踪器的成员，它们对您没有任何帮助。
- 利用与Sonarr不支持的Torrent跟踪器的最佳且最简单的方法之一是使用第二个程序，例如[Prowlarr](/prowlarr)或[Jackett](https://github.com/Jackett/Jackett)。这些软件与Sonarr配合使用，作为一个搜索索引器，存储所有信息并将其发送到Sonarr。
- Torznab - 此选项将为您设置一个Jackett预设，如果您使用多个跟踪器，则需要每个条目都有唯一的名称
- Torznab索引器
- 从预设中选择或添加自定义索引器（例如Jackett或Prowlarr）
- 名称 - 索引器在Sonarr中的名称
- 启用RSS - 如果启用，使用此索引器监视所需但缺失或尚未达到其截止时间的文件。
- 启用自动搜索 - 如果启用，使用此索引器进行自动搜索，包括添加时搜索
- 启用交互式搜索 - 如果启用，使用此索引器进行手动交互式搜索。
- URL - 索引器提供的URL，例如`http://localhost:9117/jackett/api/v2.0/indexers/torrentdb/results/torznab/`。
- API路径 - 索引器提供的API路径。通常为`/api`
- API密钥 - 索引器提供的访问API的密钥。
- 类别 - 默认类别将被使用，除非进行编辑。这些默认类别可能不是最佳选择。在编辑此设置时，Sonarr会查询索引器以获取其可用类别，并在可选择的列表中显示它们。一旦切换了类别，旧的默认值将被清除。
- 动画类别 - Sonarr将用于动画搜索的类别。除非进行编辑，否则不会使用任何类别。在编辑此设置时，Sonarr会查询索引器以获取其可用类别，并在可选择的列表中显示它们。一旦切换了类别，旧的默认值将被清除。
- 动画标准格式搜索 - 也使用标准编号搜索动画（仅适用于动画系列类型）[有关系列类型的更多信息请点击此处](/sonarr/faq#whats-the-different-series-types)
- （高级选项）附加参数 - 添加到查询链接的其他Torznab参数
- （高级选项）最小做种者数 - 从此跟踪器抓取的发布所需的最小做种者数。
- （高级选项）做种比率 - 如果为空，则使用下载客户端的默认值。否则，是下载客户端在此索引器的发布被暂停并被Sonarr删除之前必须满足的最小做种比率（需要启用完成下载处理-删除）。
- （高级选项）做种时间 - 如果为空，则使用下载客户端的默认值。否则，是下载客户端在此索引器的发布被暂停并被Sonarr删除之前必须满足的最小做种时间（以分钟为单位）（需要启用完成下载处理-删除）。
- （高级选项）索引器优先级 - 在发布决胜场景中优先选择此索引器而不是另一个索引器。1是最高优先级，50是最低优先级。
- （高级选项）下载客户端 - 选择并指定用于从此索引器抓取的下载客户端
- 标签 - 仅对具有至少一个匹配标签的系列使用此索引器。留空以用于所有系列。

## 选项

- 最小年龄 - 仅适用于Usenet：在NZB下载之前的最小年龄（以分钟为单位）。使用此功能使新发布的内容有足够的时间传播到您的Usenet提供商。
- 保留时间 - 仅适用于Usenet：将其设置为零以设置为无限保留时间
- 最大大小 - 要抓取的发布的最大大小（以MB为单位）。将其设置为零以设置为无限大小。请注意，这适用于全局设置。
- RSS同步间隔 - 间隔时间（以分钟为单位）。将其设置为零以禁用（这将停止所有自动发布抓取）最小值：10分钟，最大值：120分钟
  - 有关RSS同步如何帮助您的更好理解，请参见[Sonarr如何查找剧集？](/sonarr/faq#how-does-sonarr-find-episodes)

> 如果Sonarr离线时间过长，Sonarr将尝试翻页以查找其处理的最后一个发布，以避免错过发布。只要您的索引器支持翻页，并且时间不长，Sonarr就能够处理它可能错过的发布，并避免您需要搜索错过的发布。{.is-info}

# 下载客户端

> 可以在此部分的[更多信息（支持的）](/sonarr/supported#download-clients)页面找到有关支持的下载客户端的信息
{.is-info}

## 概述

- 下载和导入是大多数人遇到问题的地方。从高层次的角度来看，软件需要能够与您的下载客户端进行通信，并访问其下载的文件。有各种各样的支持的下载客户端和更多各种各样的设置。这意味着虽然有一些常见的设置，但没有一个正确的设置，每个人的设置可能都有所不同。但是也有很多错误的设置。

## 下载客户端流程

## Usenet

- Sonarr allows you to exclude certain series or episodes from being imported or monitored from your lists.
- To exclude a series, go to the series details page and click on the "Exclusions" tab.
- From there, you can add a new exclusion by selecting the list and specifying the series or episode you want to exclude.
- You can also edit or remove existing exclusions from this tab.
- Exclusions will prevent Sonarr from importing or monitoring the excluded series or episodes from your lists.

- 导入列表排除 - 这允许您修剪您不想再次看到的系列列表。一个例子是，如果您的列表恰好包含一部外语系列，您不太可能在您的母语中找到这部电影，也不想用字幕观看它。您可以将系列排除在将来不再添加。然而，在列表排除部分，您可以将其重新添加到列表中，以便当列表再次运行时，它将被读取到您的库中。

# 连接

> 支持的连接类型的信息可以在此部分的[更多信息（支持）](/sonarr/supported#notifications)页面找到
{.is-info}

## 连接

- 连接是Sonarr与外部世界通信的方式。

- 通过按下<kb>+</kb>按钮，您将看到一个新窗口，允许您配置许多不同的端点

- 支持的通知和连接列表位于[更多信息（支持）](/sonarr/supported#notifications)页面

## 连接触发器

- 在抓取时 - 当剧集可供下载并已发送到下载客户端时通知
- 在导入时 - {以前称为下载时} 当剧集成功导入时通知
- 在升级时 - 当剧集升级到更好的质量时通知
- 在重命名时 - 当剧集重命名时通知
- 在系列删除时 - 当系列被删除时通知
- 在剧集文件删除时 - 当剧集文件被删除时通知
- 在升级时删除剧集文件 - 当剧集文件被删除以进行升级时通知
- 在健康问题时 - 在健康检查失败时通知
  - 包括健康警告 - 除了错误外，还通知健康警告。
- 在应用程序更新时 - 当Sonarr更新到新版本时通知

# 元数据

## 元数据

> 支持的元数据消费者的信息可以在此部分的[更多信息（支持）](/sonarr/supported#metadata)页面找到
{.is-info}

- 在这里，您可以选择媒体播放器将使用的元数据类型

- 如果使用的软件是Kodi，那么Kodi将是这里最常用的选项之一。这将允许Sonarr创建一个NFO文件，并将相关的电影海报提取到您的播放器中

# 标签

- Sonarr中的标签部分用于链接Sonarr的不同方面。
- 标签对以下方面特别有用：
  - 延迟配置文件
  - 发布配置文件
  - 索引器
- 标签可用于链接延迟配置文件、发布配置文件、索引器和系列。
- 例如：
  - 您只希望为特定系列使用特定的索引器。您可以创建一个标签，并将该系列和索引器分配给该标签。
  - 您希望特定的发布配置文件仅使用特定的延迟配置文件。您可以创建一个标签，并将该发布配置文件和延迟配置文件分配给该标签。

> 系列将使用具有匹配标签和没有标签的索引器。
{.is-warning}

> 注意：标签不会影响“必须包含”、“不能包含”、“首选”等其他未在上述内容中提到的方面。
{.is-info}

# 常规

## 主机

- 绑定地址 - 有效的IP4地址或'*'表示所有接口
  - 0.0.0.0或`*` - 任何地址都可以连接
  - 127.0.0.1或localhost - 只有本地主机应用程序可以连接
  - 任何其他IP（例如1.2.3.4） - 只有该IP（1.2.3.4）可以连接
- 端口号 - 您希望用于访问Sonarr WebUI的端口号

> 注意：如果使用Docker，请不要触碰此设置。
{.is-warning}

- URL基准 - 用于反向代理支持，默认为空

> 注意：如果使用反向代理（例如：mydomain.com/sonarr），您应该输入'/sonarr'作为URL基准。
{.is-info}

- 实例名称 - 标签页和Syslog应用程序名称中的实例名称

> 如果您运行多个实例，这将在Web浏览器标签名称中添加实例名称。{.is-info}

- 启用SSL - 如果您拥有SSL凭据，并希望对Sonarr的通信进行安全保护，请启用此选项。

> 注意：除非您知道自己在做什么，否则不要使用此选项。
{.is-warning}

## 安全

- 身份验证 - 您希望如何进行身份验证以访问您的Sonarr实例
  - 无 - 您没有身份验证来访问您的Sonarr。通常，如果您是网络的唯一用户，没有任何人在您的网络上关心访问您的Sonarr，或者您的Sonarr没有暴露给Web，那么通常不需要身份验证
  - 基本（浏览器弹出） - 当访问您的Sonarr时，将显示一个小弹出窗口，允许您输入用户名和密码
  - 表单（登录页面） - 此选项将具有类似其他网站的登录屏幕，允许您登录到您的Sonarr
- API密钥 - 这是其他程序与Sonarr通信或使Sonarr与其他程序通信的方式。如果将此密钥提供给具有访问权限的错误人员，可能会对您的库执行各种操作。这就是为什么在日志中API密钥被编辑的原因
- 证书验证 - 更改HTTPS证书验证的严格程度
  - 启用 - 验证所有HTTPS证书（推荐）
  - 对本地地址禁用 - 验证除本地主机和局域网以外的所有HTTPS证书
  - 禁用 - 不验证任何HTTPS证书

## 代理

- 代理 - 此选项允许您通过代理运行Sonarr获取和搜索的信息。如果您所在的国家不允许下载Torrent文件，这可能很有用

- 使用代理 - 启用以使用代理
- 代理类型 - 选择代理类型（HTTPS、Socks4或Socks5）
- 主机名 - 输入代理主机名（不包括http/https或任何其他协议）
- 端口 - 输入代理端口
- 用户名 - 如适用，输入代理用户名
- 密码 - 如适用，输入代理密码
- 忽略的地址 - 输入逗号分隔的绕过代理的地址列表
- 对本地地址绕过代理 - 选中该框以绕过代理访问本地地址。通过URI中缺少句点（.）来识别本地请求，例如<http://webserver/>，或访问本地服务器，包括<http://localhost>、<http://loopback>或<http://127.0.0.1>。当取消选中此选项时，所有Internet请求都将通过代理服务器进行。

## 日志记录

- 日志级别 - 可能是最有用的故障排除工具之一
  - 信息 - 这是Sonarr收集信息的最基本方式，其中包括日志中的非常少量信息。此日志文件包含致命、错误、警告和信息条目。
  - 调试 - 调试将包括Info包含的所有信息以及更多有用的信息。此日志文件包含致命、错误、警告、信息和调试条目
  - 跟踪 - Sonarr的最高级和详细日志记录，跟踪将包括Info和Debug收集的所有信息以及更多信息。这是在Discord或Reddit上进行故障排除时最常要求的日志类型。如果您需要帮助，请选择跟踪日志，并重新执行导致问题的任务以捕获日志。此日志文件包含致命、错误、警告、信息、调试和跟踪条目。

## 分析

- 分析 - 将匿名使用和错误信息发送到Sonarr的服务器（SkyHook）。这包括有关您的浏览器的信息，您使用的Sonarr WebUI页面，错误报告以及操作系统和运行时版本的信息。我们将使用此信息来优先考虑功能和错误修复。

## 更新

- （高级选项）分支 - 这是您正在运行的Sonarr分支。
  - [有关更多信息，请参阅此FAQ条目](/sonarr/faq#how-do-i-update-sonarr)
- 自动 - 自动下载和安装更新。您仍然可以从系统：更新进行安装。注意：Windows用户始终会自动更新。
- 机制 - 使用Sonarr内置更新程序或脚本
  - 内置 - 使用Sonarr自己的更新程序
  - 脚本 - 让Sonarr运行更新脚本
  - Docker - 不要从Docker内部更新Sonarr，而是使用新的更新拉取全新的映像
  - Apt - 由Debian/Ubuntu软件包设置，当更新完全通过Apt进行管理时
- 脚本 - 仅在机制设置为脚本时可见 - 更新脚本的路径
- 更新过程 - Sonarr将下载更新文件，验证其完整性并将其提取到临时位置，然后调用所选的方法。更新过程将在与Sonarr运行相同的用户下运行，它需要有权限更新Sonarr文件以及停止/启动Sonarr。
- 内置 - 内置方法将备份Sonarr文件和设置，停止Sonarr，更新安装并启动Sonarr，如果您的系统无法处理停止Sonarr并将尝试自动重新启动它，最好使用脚本。如果失败，将重新启动上一个版本的Sonarr。
- 脚本 - 脚本应处理与内置更新程序相同的内容，如果您需要处理停止和启动服务（upstart/launchd等），则需要在此处执行。

## 备份

- 备份部分允许您告诉Sonarr如何处理备份

- 文件夹 - 这允许您选择备份位置。在docker中，您将受限于容器允许查看的内容。路径相对于appdata文件夹；如果需要，您可以设置绝对路径以备份到appdata文件夹之外。
- 间隔 - 您希望Sonarr多久进行一次备份
- 保留 - 您希望Sonarr保留每个备份的时间。在创建新备份后，最旧的备份将被删除

# 用户界面

## 日历

- 一周的第一天 - 在这里，您可以选择一周的第一天是什么。
- 周列标题 - 在这里，您可以选择列的标题

## 日期

- 短日期格式 - 您希望Sonarr如何显示短日期？
- 长日期格式 - 您希望Sonarr如何显示长日期格式？
- 时间格式 - 您希望使用12小时制还是24小时制？
- 显示相对日期 - 您希望Sonarr显示相对日期（今天/昨天/等等）还是绝对日期？

## 样式

- 启用色盲模式 - 修改样式以使色盲用户更好地区分颜色编码的信息