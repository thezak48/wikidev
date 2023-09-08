---
title: Prowlarr搜索
description: 
published: true
date: 2022-01-02T23:05:56.758Z
tags: prowlarr
editor: markdown
dateCreated: 2021-06-08T23:31:53.221Z
---

本页面将向您展示如何在Prowlarr中进行搜索。通常情况下，您会通过应用程序进行搜索，但也可以直接在Prowlarr中进行搜索。

# 执行搜索

要发起搜索，请单击左侧菜单中的“搜索”。屏幕底部将显示一个几乎空白的页面，其中包含一些选项。

![search_1_searchscreen.png](/assets/prowlarr/search_1_searchscreen.png)

- 查询 - 在查询字段中输入您的搜索词。
  - 单击放大镜图标以更改搜索类型，可用选项包括：
    - 基本搜索 - 基本文本查询
    - 电视搜索 - 使用在UI中显示的电视参数进行搜索，包括基于ID的搜索（TVDbId、IMDbId、TMDbID等）和季/集搜索
    - 电影搜索 - 使用在UI中显示的电影参数进行搜索，包括基于ID的搜索（TMDbId、IMDbId、Genre等）
    - 音频搜索 - 使用在UI中显示的音乐参数进行搜索，包括艺术家、专辑、标签、流派等
    - 图书搜索 - 使用在UI中显示的图书参数进行搜索，包括作者、标题等

> 这些通常以`{VariableName:SearchValue}`的格式进行格式化，例如，对于“辛普森一家”第32季的电视搜索，搜索输入将是`{TvdbId:71663} {Season:32}`。
{.is-info}

> 请注意，并非所有索引器都支持所有查询类型。
{.is-info}

- 索引器 - 在索引器下拉菜单中选择您的索引器。您可以选择“Usenet”或“Torrents”以自动选择这些类别中的所有索引器，或者您可以从任一组中选择特定的索引器进行搜索。
- 类别 - 从下拉菜单中选择要在索引器上搜索的类别。您可以选择顶级类别（电视、电影等）以自动选择所有子类别，或者您可以从任何组中选择特定的类别。

然后点击“搜索”按钮。您的结果可能需要几秒钟才能显示出来。一旦显示出来，您可以使用“选项”按钮添加或删除列，您可以通过单击列标题或使用“筛选”按钮对结果进行排序和筛选。

您可以通过单击结果右侧的下载图标来下载结果。这将将结果发送到您配置的正确下载客户端。

您可以通过选中左侧的选择框并点击“抓取发布”按钮一次性批量抓取结果。

> 下载的任何内容都将具有您在Prowlarr中设置的类别分配。这可能需要从非标准目录手动导入到您的应用程序中！
{.is-info}

# API端点

## 兼容RSS - 单个索引器Feed

- 标准的Newznab/Torznab兼容端点/参数。您可以根据定义的标准调整查询以满足您的需求。

> 由于该功能的显著缺点，不会添加聚合多索引器端点。
{.is-info}

### 查询中的API密钥

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - 例如 `http://192.168.1.100:9696/11/api?t=search&q=mike&apikey={yourkey}&cat=5000,2000`

### 标头中的API密钥

> 请确保将API密钥作为标头传递，使用`X-Api-Key`作为标头，并将API密钥作为值。
{.is-info}

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/{indexerid}/api?t=search&q={term}&apikey={yourkey}&cat={comma separated list}`
  - 例如 `http://192.168.1.100:9696/{indexerid}/api?t=search&q=mike&cat=5000,2000`

## 搜索Feed

- `http://{prowlarrhost}:{prowlarrport}/{baseurl}/api/v1/search?query={encoded term}&indexerIds={comma separated list}&categories={comma separated list}&type={searchtype}`
  - 例如 `http://192.168.1.100/prowlarr/api/v1/search?query=black%20hawk%20down&indexerIds=-1&categories=2000&type=search`
  - 例如 `http://192.168.1.100/prowlarr/api/v1/search?query=%7BTvdbId%3A71663%7D%20%7BSeason%3A32%7D&categories=5000&type=tvsearch`

参数

- `query` - URL编码的搜索字符串
- `indexerIds` - 逗号分隔的索引器ID列表
  - 在URL中省略该参数以选择所有索引器
  - `-2` 表示所有种子
  - `-1` 表示所有Usenet
  - 索引器ID
- `categories` - 逗号分隔的要使用的类别列表
  - 在URL中省略该参数以选择所有类别
- `type` - 要执行的搜索类型
  - `search` - 基本文本查询
  - `tvsearch` - 电视查询 - 支持电视参数
  - `moviesearch` - 电影查询 - 支持电影参数
  - `audiosearch` - 音频/音乐查询 - 支持音乐参数
  - `booksearch` - 图书查询 - 支持图书参数