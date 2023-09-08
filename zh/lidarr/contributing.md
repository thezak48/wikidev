---
title: Lidarr 贡献
description: 
published: true
date: 2022-09-26T15:56:35.364Z
tags: lidarr, contributing
editor: markdown
dateCreated: 2021-05-26T02:28:31.770Z
---

# 如何贡献

我们一直在寻找人们的帮助，使 Lidarr 变得更好，有许多贡献的方式。

# 文档

设置指南，[常见问题](/lidarr/faq)，我们在 [wiki](https://wiki.servarr.com/lidarr) 上拥有的信息越多越好。

# 开发

Lidarr 使用 C#（后端）和 JS（前端）编写。后端构建在 .NET6 框架上，而前端使用 Reactjs。

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

> Lidarr **不会**在旧版本（如 `10.x`、`8.x`、`6.x` 或任何低于 12.0 的版本）上运行！
{.is-warning}

- 构建前端需要 [Yarn](https://yarnpkg.com/getting-started/install)
  - Yarn 默认包含在 **Node 16.10**+ 中。使用 `corepack enable` 启用它
  - 对于其他 Node 版本，使用 `npm i -g corepack` 安装

## 入门

1. Fork Lidarr
1. 将仓库克隆到你的开发机器上。[*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> 在提交前端更改之前，请确保在代码上运行 `yarn lint --fix` 进行代码检查。
对于 CSS 更改，请使用 `yarn stylelint-windows --fix` {.is-info}

### 构建前端

- 进入克隆的目录
- 安装所需的 Node 包

     ```bash
     yarn install
     ```

- 使用以下命令启动 webpack 监视开发环境中需要进行后处理的更改：

     ```bash
     yarn start
     ```

### 构建后端

后端解决方案最方便的方式是在 Visual Studio 或 Rider 中构建和运行，但是如果只关注前端 UI 的工作，也可以从命令行轻松构建，前提是已安装了正确的 SDK。

#### Visual Studio

> 确保启动项目设置为 `Lidarr.Console`，框架设置为 `net6.0`
{.is-info}

1. 首先，在 Visual Studio 中 `Build` 解决方案，这将确保所有项目都正确构建并还原依赖项
1. 然后，在 Visual Studio 中 `Debug/Run` 项目以启动 Lidarr
1. 打开 <http://localhost:8686>

#### 命令行

1. 清理解决方案

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. 为正确的平台（Posix 或 Windows）还原和构建调试配置

```shell
dotnet msbuild -restore src/Lidarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. 从 `/_output` 目录运行生成的可执行文件

## 贡献代码

- 如果你正在添加一个新的、已经请求的功能，请在 [GitHub Issues](https://github.com/Lidarr/Lidarr/issues) 上发表评论，以免重复工作（如果你想添加的内容在那里还没有，请先与我们交流）
- 从 Lidarr 的 develop 分支进行变基，不要合并
- 进行有意义的提交，或者将它们合并
- 在工作完成之前，随时进行拉取请求，这样我们就可以看到进展情况，并进行评论/提出改进建议
- 如果有任何问题，请在 Discord 上联系我们
- 添加测试（单元测试/集成测试）
- 为了保持一致性，请使用 \*nix 行尾符进行提交（我们在 Windows 上检出并提交 \*nix）
- 每个拉取请求只包含一个功能/错误修复，以保持代码的清晰和易于理解
- 使用 4 个空格代替制表符，这是 VS 2022 和 WebStorm 的默认设置

## 发起拉取请求

- 只向 `develop` 分支发起拉取请求，永远不要向 `master` 分支发起拉取请求，如果你向 `master` 分支发起拉取请求，我们会在上面发表评论并关闭它
- 我们可能会对你发起的拉取请求进行一些评论或提问，这是为了确保一致性和可维护性
- 我们将尽快回复拉取请求，如果经过一天或两天仍未回复，请联系我们，可能是我们忽略了
- 每个拉取请求应该来自自己的 [feature branch](http://martinfowler.com/bliki/FeatureBranch.html)，而不是你的 fork 中的 develop 分支，它应该有一个有意义的分支名称（表示正在添加/修复的内容）
  - `new-feature`（好的）
  - `fix-bug`（好的）
  - `patch`（不好）
  - `develop`（不好）
- 提交应写为 `New:` 或 `Fixed:`，对于不被视为 `maintenance release` 的更改

## 单元测试

Lidarr 使用 nunit 进行单元测试、集成测试和自动化测试套件。

### 运行测试

可以使用包含的 nunit3testadapter nuget 包在 VS 中轻松运行测试，也可以使用包含的 bash 脚本 `test.sh` 在命令行中运行测试。

在 VS 中，只需导航到测试资源管理器，然后运行或调试你想要检查的测试。

在 VS 中，可以一次运行所有测试，也可以逐个运行测试。

从命令行中，`test.sh` 脚本接受 3 个参数

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### 编写测试

尽管不总是有趣，但我们鼓励为任何后端代码更改编写单元测试。这将确保更改按照你的意图进行，并且未来的更改不会破坏预期的行为。

> 当提交 PR 时，我们要求新代码的测试覆盖率达到 80%
{.is-info}

如果对此有任何疑问，请告诉我们。

# 翻译

Lidarr 使用一个自托管的开放访问的 [Weblate](https://translate.servarr.com) 实例来管理其 json 翻译文件。这些文件存储在仓库的 `src/NzbDrone.Core/Localization` 目录中。

## 贡献到现有翻译

Weblate 处理除英语以外的所有语言的字符串的同步和翻译。对于 Lidarr 项目，应在 Weblate 上执行已翻译字符串的编辑和现有字符串的翻译。

英语翻译文件 `en.json` 用作所有其他翻译的源，它在 GitHub 仓库上进行管理。

## 添加一种语言

向 Lidarr 添加翻译需要两个步骤

- 在 weblate 中添加语言
- 在 Lidarr 代码库中添加语言

## 在代码中添加翻译字符串

英语翻译文件 `src/NzbDrone.Core/Localization/en.json` 用作所有其他翻译的源，它在 GitHub 仓库上进行管理。当在 UI 或后端添加新的字符串时，必须在 `en.json` 中添加一个键，以及英语的默认值。然后可以按以下方式使用该键：

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

可以通过导入 translate 函数并使用 `en.json` 中指定的键将新字符串添加到前端

```js
import translate from 'Utilities/String/translate';

<div>
  {translate('UnableToAddANewIndexerPleaseTryAgain')}
</div>
```