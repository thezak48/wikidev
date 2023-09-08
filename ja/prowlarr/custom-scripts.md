---
title: Prowlarrのカスタムスクリプト
description: 
published: true
date: 2021-12-20T16:40:47.702Z
tags: prowlarr, needs-love, custom scripts
editor: markdown
dateCreated: 2021-06-23T06:40:30.916Z
---

カスタムスクリプトをトリガーしたい場合は、[こちら](/prowlarr/settings#connections)で詳細を確認できます。スクリプトは、Prowlarrの[接続設定](/prowlarr/settings#connections)を介して追加されます。

# 概要

Prowlarrは、エピソードが新しくインポートされたり名前が変更されたりしたときに、カスタムスクリプトを実行することができます。アクションに応じて、異なるパラメータが提供されます。パラメータは環境変数を介してスクリプトに渡されます。

## Prowlarrのログ

以下の内容は、カスタムスクリプトにのみログが記録されます。

- スクリプトの`stdout`出力は`Debug`としてログに記録されます。
- スクリプトの`stderr`出力は`Info`としてログに記録されます。
- スクリプトのトリガーは`Trace`にログが記録されます。

# 環境変数

環境変数はイベントの種類によって異なります。詳細は近日中に提供されます^tm^

> [現時点では、こちらのコードを確認できます。ウィキへの貢献も歓迎しています](https://github.com/Prowlarr/Prowlarr/blob/develop/src/NzbDrone.Core/Notifications/CustomScript/CustomScript.cs)
{.is-info}

## テスト時

Prowlarrにスクリプトを追加し、「テスト」をクリックすると、以下のパラメータでスクリプトが呼び出されます。スクリプトは、サポートされていないイベントの種類を優雅に無視できるようにする必要があります。

| 環境変数 | 詳細 |
| --------- | ----- |
| `prowlarr_eventtype` | `Test` |