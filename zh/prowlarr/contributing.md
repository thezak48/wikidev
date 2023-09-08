---
title: Prowlarr 贡献
description: 
published: true
date: 2022-11-16T19:35:23.515Z
tags: prowlarr, development, contributing
editor: markdown
dateCreated: 2021-12-11T19:42:15.627Z
---

# 如何贡献

我们一直在寻找人们的帮助，使 Prowlarr 变得更好，有很多贡献的方式。

# 文档

设置指南，[常见问题](/prowlarr/faq)，我们在 [wiki](https://wiki.servarr.com/prowlarr) 上拥有的信息越多越好。

# 开发

Prowlarr 使用 C#（后端）和 JS（前端）编写。后端基于 .NET6 框架构建，而前端使用 Reactjs。

## 所需工具

- 推荐使用 Visual Studio 2022 或更高版本（<https://www.visualstudio.com/vs/>）。社区版是免费的并且可用（<https://www.visualstudio.com/downloads/>）。

> 推荐使用 VS 2022 V17.0 或更高版本，因为它包含了 .NET6 SDK
{.is-info}

- 选择的 HTML/Javascript 编辑器（VS Code/Sublime Text/Webstorm/Atom 等）
- [Git](https://git-scm.com/downloads)
- 需要 [Node.js](https://nodejs.org/) 运行时。支持以下版本：
  - **12.0** 或更高版本
  - **14.0** 或更高版本
  - **16.0** 或更高版本
{.grid-list}

> Prowlarr **无法** 在旧版本（如 `10.x`、`8.x`、`6.x` 或任何低于 12.0 的版本）上运行！
{.is-warning}

- 需要 [Yarn](https://yarnpkg.com/getting-started/install) 来构建前端
  - Yarn 默认包含在 **Node 16.10**+ 中。可以通过 `corepack enable` 启用它
  - 对于其他 Node 版本，请使用 `npm i -g corepack` 进行安装

## 入门

1. Fork Prowlarr
1. 将存储库克隆到开发机器上。[*info*](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

> 在提交前端更改之前，请确保在代码上运行 `yarn lint --fix` 进行代码检查。
对于 CSS 更改，请使用 `yarn stylelint-windows --fix`
{.is-info}

### 构建前端

- 导航到克隆的目录
- 安装所需的 Node 包

     ```bash
     yarn install
     ```

- 使用以下命令启动 webpack 监视开发环境中需要进行后处理的更改：

     ```bash
     yarn start
     ```

### 构建后端

后端解决方案最方便的方式是在 Visual Studio 或 Rider 中构建和运行，但是如果只关注前端 UI，也可以在命令行中轻松构建，前提是正确的 SDK 已安装。

#### Visual Studio

> 确保启动项目设置为 `Prowlarr.Console`，框架设置为 `net6.0`
{.is-info}

1. 首先，在 Visual Studio 中 `Build` 解决方案，这将确保正确构建所有项目并还原依赖项
1. 然后，在 Visual Studio 中 `Debug/Run` 项目以启动 Prowlarr
1. 打开 <http://localhost:9696>

#### 命令行

1. 清理解决方案

  ```shell
  dotnet clean $slnFile -c Debug
  ```

1. 恢复并构建正确平台的调试配置（Posix 或 Windows）

```shell
dotnet msbuild -restore src/Prowlarr.sln -p:Configuration=Debug -p:Platform=Posix -t:PublishAllRids
```

1. 从 `/_output` 目录运行生成的可执行文件

## 贡献代码

- 如果您要添加一个新的、已经请求的功能，请在 [GitHub Issues](https://github.com/Prowlarr/Prowlarr/issues) 上发表评论，以避免重复工作（如果您想添加的内容尚未在其中，请先与我们交流）
- 从 Prowlarr 的 develop 分支进行变基，不要合并
- 进行有意义的提交，或者将它们合并
- 在工作完成之前，随时进行拉取请求，这样我们就可以看到进展情况，并进行评论/提出改进建议
- 如果有任何问题，请在 Discord 上与我们联系
- 添加测试（单元测试/集成测试）
- 为了保持一致性，请使用 \*nix 行尾符进行提交（我们在 Windows 上检出并提交 \*nix）
- 每个拉取请求只包含一个功能/错误修复，以保持代码整洁和易于理解
- 使用 4 个空格而不是制表符，这是 VS 2022 和 WebStorm 的默认设置

### 贡献索引器

### C# 索引器

- C# 索引器应提交到 [Prowlarr App 存储库](https://github.com/prowlarr/prowlarr) 的 `develop` 分支
- 如果您要贡献 C# 索引器，请将提交命名为：`New: (Indexer) {Indexer Name}`、`New: (Indexer) {Usenet|Torrent} {Indexer Name}`、`New: (Indexer) {Torznab|Newznab} {Indexer Name}`
- 如果您要更新 C# 索引器，请将提交命名为：`Fixed: (Indexer) {Indexer Name} {changes}`，例如 `Fixed: (Indexer) Changed BHD to use API`

### Cardigann（YML）索引器

- Cardigann 和 YML 索引器应提交到 [Prowlarr Indexer 存储库](https://github.com/prowlarr/indexers) 的 `master` 分支
- 有关 Cardigann/YML 索引器的详细信息，请参阅 [Prowlarr Cardigann yml 格式的定义和描述](/prowlarr/cardigann-yml-definition)
- 有关测试自定义 yml 定义的详细信息，请参阅 [索引器页面中的自定义 yml 部分](/prowlarr/indexers#adding-a-custom-yml-definition)

## 发起拉取请求

- 只向 `develop` 分支发起拉取请求，永远不要向 `master` 分支发起拉取请求，如果您向 `master` 分支发起拉取请求，我们将在其上发表评论并关闭它
- 您可能会收到我们的一些评论或问题，这些评论或问题是为了确保一致性和可维护性
- 我们将尽快回复拉取请求，如果经过一天或两天仍未回复，请与我们联系，可能是我们错过了
- 每个拉取请求应来自您自己的 [feature branch](http://martinfowler.com/bliki/FeatureBranch.html)，而不是您的 fork 中的 develop 分支，它应具有有意义的分支名称（表示正在添加/修复的内容）
  - `new-feature`（好的）
  - `fix-bug`（好的）
  - `patch`（不好）
  - `develop`（不好）
- 提交应写为 `New:` 或 `Fixed:`，用于不被视为 `maintenance release` 的更改

## 单元测试

Prowlarr 使用 nunit 进行单元测试、集成测试和自动化测试套件。

### 运行测试

可以使用包含的 nunit3testadapter nuget 包在 VS 中轻松运行测试，也可以使用包含的 bash 脚本 `test.sh` 在命令行中运行测试。

在 VS 中，只需导航到 Test Explorer 并运行或调试您想要检查的测试。

在 VS 中，可以一次运行所有测试，也可以逐个运行测试。

从命令行中，`test.sh` 脚本接受 3 个参数

```bash
test.sh <PLATFORM> <TYPE> <COVERAGE>
```

### 编写测试

尽管并不总是有趣，但我们鼓励为任何后端代码更改编写单元测试。这将确保更改按照您的意图进行，并且未来的更改不会破坏预期的行为。

> 当提交 PR 时，我们要求新代码的测试覆盖率达到 80%
{.is-info}

如果对此有任何疑问，请告诉我们。

# 翻译

Prowlarr 使用自托管的开放访问 [Weblate](https://translate.servarr.com) 实例来管理其 json 翻译文件。这些文件存储在存储库的 `src/NzbDrone.Core/Localization` 目录中。

## 贡献到现有翻译

Weblate 处理除英语以外的所有语言的字符串的同步和翻译。对于 Prowlarr 项目，应在 Weblate 上执行已翻译字符串的编辑和翻译。

英语翻译 `en.json` 用作所有其他翻译的源，并在 GitHub 存储库上进行管理。

## 添加语言

添加 Prowlarr 的翻译需要两个步骤

- 在 weblate 中添加语言
- 在 Prowlarr 代码库中添加语言

## 在代码中添加翻译字符串

英语翻译 `src/NzbDrone.Core/Localization/en.json` 用作所有其他翻译的源，并在 GitHub 存储库上进行管理。当在 UI 或后端添加新字符串时，必须在 `en.json` 中添加一个键，并提供英语的默认值。然后可以按以下方式使用该键：

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