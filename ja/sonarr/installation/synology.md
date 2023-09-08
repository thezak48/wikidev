---
title: Sonarr Synology インストール
description: Sonarr の Synology インストールガイド
published: true
date: 2023-07-03T20:23:52.657Z
tags: sonarr
editor: markdown
dateCreated: 2021-07-10T16:07:37.425Z
---

# Synology

- [SynoCommunity は Synology NAS パッケージを作成、サポート、メンテナンスしています](https://synocommunity.com/package/nzbdrone)

> NAS パッケージはメンテナンスが不十分で頻繁に更新されません。もし NAS が Docker をサポートしている場合は、[Docker を実行することを強くお勧めします](https://trash-guides.info/Hardlinks/How-to-setup-for/Synology/)。NAS パッケージは更新が設定されておらず、データベースを手動で削除しない限り Sonarr を再インストールすることはできません。{.is-info}

- [SynoCommunity は必要な Mono パッケージも作成、サポート、メンテナンスしています](https://synocommunity.com/package/mono)

## Synology Mono SSL エラー

> SynoCommunity のメンテナンスが不十分な Mono パッケージのバグにより、Mono の更新後や新規インストール後に Sonarr が接続に失敗します。これは、[SynoCommunity のバグレポート #5051](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1009758625) の手順に従うことで解決できます。[このコメント](https://github.com/SynoCommunity/spksrc/issues/5051#issuecomment-1153245799)によると、DSM7 ユーザーは追加の手順が必要です。
{.is-danger}

1. DSM 内で、*コントロールパネル => ターミナルと SNMP* で SSH サービスを有効にし、適用をクリックします。
1. [Terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac)（MacOS）を使用して `ssh -l [管理者ユーザー名] [NAS アドレス]` で NAS に接続するか、[Putty](https://www.putty.org/)（Windows）を使用して NAS のネットワークアドレスに接続します。
1. 必要な管理者パスワードを入力し、Enter キーを押します。
1. 下記の DSM バージョンに合わせた適切なコマンドを入力し、Enter キーを押します。
1. 必要な管理者パスワードを入力し、Enter キーを押します。完了すると、*Import process completed* という行が表示されます。
1. `exit` と入力し、Enter キーを押して SSH セッションを切断します。
1. DSM 内で、*コントロールパネル => ターミナルと SNMP* で SSH サービスを無効にし、適用をクリックします。
1. 完了後、Sonarr のエラーは数分で自動的に消えるはずです。

### Synology DSM6 Mono 修正コマンド

```shell
sudo /var/packages/mono/target/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
```

### Synology DSM7 Mono 修正コマンド

```shell
sudo /volume1/@appstore/mono/bin/cert-sync /etc/ssl/certs/ca-certificates.crt
sudo chmod -R a+rX /usr/share/.mono
```