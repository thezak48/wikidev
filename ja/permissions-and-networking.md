# ネットワークのトラブルシューティング

- トラブルシューティングには通常 `curl` が必要です
- SSL の場合は、トラブルシューティングには `openssl` が必要です

## SSL の問題

- `curl` は \*Arrs のように SSL 証明書を検証しないため、有効な証明書かどうかを確認するためには openssl を使用する必要があります

- 証明書が有効かどうかを確認するために、openssl を使用して接続/サイトをテストします

```bash
openssl s_client -showcerts -connect <url>:443
```

## 接続できない IPv6 IP

- curl を使用して接続をテストします

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Windows でポートの使用状況を確認する

- netsh を使用して使用中のポートとそれを使用しているもののリストを取得します

```bash
netstat -ab
```

## Windows で URL の予約を確認する

- netsh を使用してアプリがバインドしてリッスンしているポートと URL のリストを取得します

```bash
netsh http show urlacl
```

## Windows で URL の予約を作成する

- netsh を使用して urlacl を作成します。以下の例はポート `7878` を使用する radarr のためのものです

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Linux でポートの使用状況を確認する

- netstat を使用して使用中のポート/アプリのポートを特定します

```bash
sudo netstat -tnlp | grep <:port or app>
```

### 例

- ポート `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- アプリ名が `Radarr` の場合

```bash
sudo netstat -tnlp | grep 'Radarr'
```