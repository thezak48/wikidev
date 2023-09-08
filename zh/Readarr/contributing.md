---
title: Readarr 贡献
description: 
published: true
date: 2022-09-26T15:56:42.368Z
tags: readarr, development, contributing
editor: markdown
dateCreated: 2021-05-25T19:21:59.324Z
---

# 如何贡献

我们一直在寻找人们的帮助，使 Readarr 变得更好，有很多种方式可以贡献。

# 文档

设置指南，[常见问题](/readarr/faq)，我们在 [wiki](https://wiki.servarr.com/readarr) 上获得的信息越多越好。

# 开发

Readarr 使用 C#（后端）和 JS（前端）编写。后端构建在 .NET6 框架上，而前端使用 Reactjs。

## 所需工具

- 推荐使用 Visual Studio 2022 或更高版本（<https://www.visualstudio.com/vs/>）。社区版是免费的并且可用（<https://www.visualstudio.com/downloads/>）。

> 推荐使用 VS 2022 V17.0 或更高版本，因为它包含了 .NET6 SDK
{.is-info}

- 选择一个 HTML/Javascript 编辑器（VS Code/Sublime Text/Webstorm/Atom 等）
- [Git](https://git-scm.com/downloads)
- 需要 [Node.js](https://nodejs.org/) 运行时。支持以下版本：
  - **12.0** 或更高版本
  - **14.0** 或更高版本
  - **16.0** 或更高版本
{.grid-list}

> Readarr **不会** 在旧版本（如 `10.x`、`8.x`、`6.x` 或 12.0 以下的任何版本）上运行！
{.is-warning}

- 构建前端需要 [Yarn](https://yarnpkg.com/getting-started/install)
  - Yarn 已默认包含在 **Node 16.10**+ 中。使用 `corepack enable` 启用它
  - 对于其他 Node 版本，使用 `npm i -g corepack` 安装

## 入门

1. Fork Readarr
1. 将仓库克隆到开发机器上。[*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> 在提交前端更改之前，请确保在代码上运行 `yarn lint --fix` 进行代码检查。
对于 CSS 更改，请使用 `yarn stylelint-windows --fix` {.is-info}

### 构建前端

- 进入克隆的目录
- 安装所需的 Node 包

     ```bash
     yarn install
     ```

- 使用以下命令启动 webpack 监视开发环境中的任何需要后处理的更改：

     ```bash
     yarn start
     ```

### 构建后端

后端解决方案最容易在 Visual Studio 或 Rider 中构建和运行，但是如果只关注前端 UI，也可以从命令行轻松构建，只需安装正确的 SDK 即可。

#### Visual Studio

> 确保启动项目设置为 `Readarr.Console`，框架设置为 `net6.0`
{.is-info}

1. 在 Visual Studio 中首先 `Build` 解决方案，这将确保正确构建所有项目并还原依赖项
1. 然后在 Visual Studio 中 `Debug/Run` 项目以启动 Readarr
1. 打开 <http://localhost:8787>

#### 命令行

1. 清理解决方案

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. 为正确的平台（Posix 或 Windows）还原和构建调试配置

```shell
dotnet msbuild -restore src/Readarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. 从 `/_output` 目录运行生成的可执行文件

## 贡献代码

- 如果您要添加一个新的、已经请求的功能，请在 [GitHub Issues](https://github.com/Readarr/Readarr/issues) 上发表评论，以免重复工作（如果您想添加的内容尚未在那里，请先与我们交流）
- 从 Readarr 的 develop 分支进行变基，不要合并
- 进行有意义的提交，或者将它们合并为一个提交
- 在工作完成之前随时提交拉取请求，这样我们就可以看到它的进展，并提出评论/建议改进
- 如果有任何问题，请在 Discord 上与我们联系
- 添加测试（单元测试/集成测试）
- 为了保持一致性，请使用 \*nix 行尾符进行提交（我们在 Windows 上检出并提交 \*nix）
- 每个拉取请求只包含一个功能/错误修复，以保持代码整洁和易于理解
- 使用 4 个空格而不是制表符，这是 VS 2022 和 WebStorm 的默认设置

## 提交拉取请求

- 只向 `develop` 分支提交拉取请求，永远不要提交到 `master` 分支，如果您向 `master` 分支提交了拉取请求，我们将在其上发表评论并关闭它
- 您可能会收到我们的一些评论或问题，这些评论或问题是为了确保一致性和可维护性
- 我们将尽快回复拉取请求，如果一两天过去了，请与我们联系，我们可能错过了它
- 每个拉取请求应该来自自己的 [feature branch](http://martinfowler.com/bliki/FeatureBranch.html)，而不是来自您的 fork 中的 develop 分支，它应该有一个有意义的分支名称（表示正在添加/修复的内容）
  - `new-feature`（好的）
  - `fix-bug`（好的）
  - `patch`（不好）
  - `develop`（不好）
- 提交应该写为 `New:` 或 `Fixed:`，用于不被视为 `maintenance release` 的更改

## 单元测试

Readarr 使用 nunit 进行单元测试、集成测试和自动化测试套件。

### 运行测试

可以使用包含的 nunit3testadapter nuget 包在 VS 中轻松运行测试，也可以使用包含的 bash 脚本 `test.sh` 在命令行中运行测试。

在 VS 中，只需导航到测试资源管理器并运行或调试您想要检查的测试。

在 VS 中可以一次运行所有测试或逐个运行测试。

从命令行运行 `test.sh` 脚本时，可以使用 3 个参数

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### 编写测试

虽然不总是有趣，但我们鼓励为任何后端代码更改编写单元测试。这将确保更改按照您的意图进行工作，并且未来的更改不会破坏预期的行为。

> 当提交 PR 时，我们要求新代码的测试覆盖率达到 80%
{.is-info}

如果对此有任何疑问，请告诉我们。

# 翻译

Readarr 使用一个自托管的开放访问的 [Weblate](https://translate.servarr.com) 实例来管理其 json 翻译文件。这些文件存储在仓库的 `src/NzbDrone.Core/Localization` 目录中。

## 贡献到现有翻译

Weblate 处理除英语以外的所有语言的字符串的同步和翻译。对于 Readarr 项目，应在 Weblate 上执行已翻译字符串的编辑和现有字符串的翻译。

英语翻译文件 `en.json` 用作所有其他翻译的源文件，并在 GitHub 仓库上进行管理。

## 添加一种语言

向 Readarr 添加翻译需要两个步骤

- 在 weblate 中添加语言
- 在 Readarr 代码库中添加语言

## 在代码中添加翻译字符串

英语翻译文件 `src/NzbDrone.Core/Localization/en.json` 用作所有其他翻译的源文件，并在 GitHub 仓库上进行管理。当在 UI 或后端添加新字符串时，必须在 `en.json` 中添加一个键，并提供英语的默认值。然后可以按以下方式使用该键：

> 不接受用于翻译日志消息的 PR
{.is-warning}

### 后端字符串

可以使用 Localization Service 的 `GetLocalizedString` 方法添加后端字符串

```dotnet
private readonly ILocalizationService _localizationService;

public IndexerCheck(ILocalizationService localizationService)
{
  _localizationService = localizationService;
}
        
var translated = _localizationService.GetLocalizedString("IndexerHealthCheckNoIndexers")
```

### 前端字符串

可以通过导入 translate 函数并使用 `en.json` 中指定的键来将新字符串添加到前端

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```