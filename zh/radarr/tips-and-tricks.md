---
title: Radarr技巧与技巧
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-and-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# TRaSH的自定义格式

- [TRaSH有一个指南](https://trash-guides.info/Radarr/)，介绍了如何使用[Radarr => 设置 => 自定义格式](/radarr/settings#custom-formats)，以及一个共享的自定义格式存储库。

# 同步两个Radarr实例

- TRaSH有[一个指南](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)，介绍了如何同步两个实例。

# 重命名电影文件夹

- [请参阅此常见问题解答](/radarr/faq#how-can-i-rename-my-movie-folders)

# 为每个电影创建一个文件夹

- 这只需要清理/整理现有库，以便导入到Radarr中。以下是几种不同的方法。

## Filebot

> Filebot支持Windows、Linux和MacOS {.is-info}

- [Filebot](https://www.filebot.net/)是一个非常好用的实用工具，可以以Radarr可以成功解析的方式组织您的电影。版本4.7.9仍然可以从SourceForge镜像免费下载，但Windows和Apple商店也有付费版本。在Linux上，您选择的发行版可能有一个软件包，比如Arch的AUR软件包或Debian/Ubuntu的`.deb`文件，可以从它们的下载页面下载。它既有GUI又有CLI，所以几乎可以满足所有人的需求。

- 有很好的帮助可用，包括他们的格式表达式页面。我个人的建议是，如果您的文件包含有用的细节，如质量、版本和/或组织，可以使用类似`{ny}\{fn}`的格式，或者如果不包含这些细节，可以使用`{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`，例如，这将产生`Movie (Year)/Movie (Year) [Bluray-1080p]`或`Movie (Year)/Movie (Year) [DVD-480p]`。您也可以使用WEBDL代替Bluray，如果您更希望将您的收藏视为WEBDL。

- 要保持此模式用于将来的电影，您应该设置：

- [设置 => 媒体管理（显示高级设置）=> 电影命名](/radarr/settings#media-management)

  - 文件：`{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - 文件夹：`{Movie CleanTitle} {(Release Year)}`

- 注意：如果您更喜欢这种命名格式，可以将上面的空格替换为`.`或`_`。

## Files 2 Folder

> Files 2 Folder是一个Windows应用程序 {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/)可以将电影库组织起来，以便导入到Radarr中。只需将zip文件解压到计算机上，并以管理员身份运行.exe文件，然后点击“是”将其添加到右键菜单中。

安装完成后，只需点击几下即可将所有文件组织到各自的文件夹中。

1. 浏览到您的电影文件夹
1. 选择所有文件，右键单击以打开菜单
1. 在菜单中选择“files 2 folder”选项
1. 在Files 2 Folder窗口中选择“根据文件名将每个文件移动到单独的子文件夹中”
1. 点击确定
1. 等待片刻，所有文件将被放置在各自的文件夹中。

## Linux Bash脚本

以下脚本将在所选文件夹中获取所有`*.mkv`文件，并将它们移动到以文件名为基础的文件夹中。请注意，这不会进入起始/所选文件夹中的子文件夹。

```shell
cd /path/to/your/movies/files/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windows命令行

在Windows中打开命令行(cmd.exe) `以管理员身份`。导航到您的电影文件夹。运行以下两个命令（复制/粘贴是可以的，没有任何需要更改的内容）：

`for %i in (*) do md "%~ni"`

这将为目录中的每个文件创建一个文件夹。

`for %i in (*) do move "%i" "%~ni"`

这将把所有文件移动到新的目录中。

如果您需要清理空目录，可以使用以下命令：

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows Powershell

或者在Windows中，您可以在Powershell中运行以下脚本，以遍历目录中的每个文件，并将其移动到具有相同名称的文件夹中。

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```