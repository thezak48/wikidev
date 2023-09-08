---
title: Radarrのヒントとトリック
description: 
published: true
date: 2022-03-24T02:53:26.272Z
tags: radarr, needs-love, tips-and-tricks
editor: markdown
dateCreated: 2021-08-14T15:12:58.934Z
---

# TRaSHのカスタムフォーマット

- [TRaSHによるガイド](https://trash-guides.info/Radarr/)では、[Radarr => 設定 => カスタムフォーマット](/radarr/settings#custom-formats)の使い方について解説しており、カスタムフォーマットの共有リポジトリも提供しています。

# 2つのRadarrインスタンスの同期

- TRaSHによる[ガイド](https://trash-guides.info/Radarr/Tips/Sync-2-radarr-sonarr/)で、2つのインスタンスの同期方法について説明しています。

# 映画フォルダの名前変更

- [このFAQエントリ](/radarr/faq#how-can-i-rename-my-movie-folders)を参照してください。

# 各映画のフォルダの作成

- これは、既存のライブラリを整理し、Radarrへのインポートを容易にするために必要です。以下にいくつかの異なる方法があります。

## Filebot

> FilebotはWindows、Linux、MacOSでサポートされています {.is-info}

- [Filebot](https://www.filebot.net/)は、Radarrが正常に解析できるように映画を整理するための素晴らしいユーティリティです。バージョン4.7.9は、SourceForgeのミラーから無料でダウンロードできますが、WindowsストアとAppleストアには有料版もあります。Linuxでは、ArchのAURパッケージやDebian/Ubuntuの`.deb`ファイルなど、選択したディストリビューションにパッケージが用意されている場合があります。GUIとCLIの両方を備えているため、ほとんどのユーザーに満足してもらえるはずです。

- 彼らのフォーマット式のページを含む素晴らしいヘルプが利用可能です。私の個人的な提案は、ファイルに品質、エディション、および/またはグループなどの有用な詳細が含まれている場合は`{ny}\{fn}`のようなものを使用することです。それらが含まれていない場合は、`{ny}/{ny} [{dim[0] >= 1280 ? 'Bluray' : 'DVD'}-{vf}]`を使用することができます。これにより、例えば`Movie (Year)/Movie (Year) [Bluray-1080p]`または`Movie (Year)/Movie (Year) [DVD-480p]`が生成されます。Blurayの代わりに、コレクションをWEBDLとして扱いたい場合は、それを使用することもできます。

- 将来の映画にこのパターンを維持するためには、次の設定を行う必要があります。

- [設定 => メディア管理（詳細設定表示） => 映画の命名](/radarr/settings#media-management)

  - ファイル: `{Movie CleanTitle} {(Release Year)} {Edition Tags} {\[Quality Title]}`
  - フォルダ: `{Movie CleanTitle} {(Release Year)}`

- 注意: 上記のスペースは、`.`または`_`に置き換えることもできます。

## Files 2 Folder

> Files 2 FolderはWindowsアプリケーションです {.is-info}

[Files 2 Folder](http://www.dcmembers.com/skwire/download/files-2-folder/)は、Radarrへのインポートのために映画ライブラリを整理することができます。zipファイルをコンピュータに展開し、.exeを管理者として実行し、右クリックメニューに追加するためには「はい」をクリックしてください。

インストール後、すべてのファイルを個別のフォルダに整理するためには、以下の手順を実行します。

1. 映画フォルダに移動します。
1. すべてのファイルを選択し、右クリックしてメニューを表示します。
1. メニューで「files 2 folder」オプションを選択します。
1. Files 2 Folderウィンドウで、「Move each file to individual subfolders based on their names」を選択します。
1. OKをクリックします。
1. しばらく待つと、すべてのファイルが個別のフォルダに整理されます。

## Linux Bashスクリプト

次のスクリプトは、選択したフォルダ内のすべての`*.mkv`ファイルを、その名前に基づいてフォルダに移動します。なお、これは開始/選択したフォルダ内のサブフォルダには入りません。

```shell
cd /path/to/your/movies/files/
find . -maxdepth 1 -type f -iname "*.mkv" -exec sh -c 'mkdir "${1%.*}" ; mv "${1%}" "${1%.*}" ' _ {} \;
```

## Windowsコマンドライン

Windowsのコマンドライン（cmd.exe）で管理者としてコマンドラインに移動します。映画フォルダに移動します。次の2つのコマンドを実行します（コピー/貼り付けで問題ありません、変更する必要はありません）。

`for %i in (*) do md "%~ni"`

これにより、ディレクトリ内のすべてのファイルに対してフォルダが作成されます。

`for %i in (*) do move "%i" "%~ni"`

これにより、すべてのファイルが新しいディレクトリに移動されます。

空のディレクトリをクリーンアップする必要がある場合は、次のコマンドを使用します。

`for /f "usebackq delims=" %d in ("dir /ad/b/s | sort /R") do rd "%d"`

## Windows Powershell

または、Windowsでは、Powershellで次のスクリプトを実行して、ディレクトリ内の各ファイルを繰り返し処理し、同じ名前のフォルダに移動することもできます。

```powershell
Get-ChildItem -File 
  | ForEach-Object {
    $dir = New-Item -ItemType Directory -Name $_.BaseName -Force
    $_ | Move-Item -Destination $dir
  }
```