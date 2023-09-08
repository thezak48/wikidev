# リバースプロキシの設定

外部からRadarrにアクセスするためのリバースプロキシの設定のサンプル構成例です。

> これらの例では、デフォルトのポート番号`7878`と、ベースURLを`radarr`に設定したことを前提としています。また、Webサーバー（例：nginx）とRadarrが同じサーバーで実行され、`localhost`（127.0.0.1）でアクセス可能であることを前提としています。そうでない場合は、プロキシパスディレクティブにホストのIPアドレスまたはホスト名を使用してください。
{.is-info}

## NGINX

Nginxの設定ファイルである`nginx.conf`に以下の設定を追加します。コードブロックは`serverコンテキスト`の内部に追加する必要があります。[典型的なNginxの設定の完全な例](https://www.nginx.com/resources/wiki/start/topics/examples/full/)も参照してください。

> カスタムのhttp/httpsサーバーポートを使用している場合は、Hostヘッダーにもそれを含めるようにしてください。例：`proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
location ^~ /radarr {
    proxy_pass http://127.0.0.1:7878;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_redirect off;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $http_connection;
}
# APIの外部アクセスをNGINXで許可する
location ^~ /radarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:7878;
}
```

Nginxの設定ファイルを整理するためのより良い方法は、各サイトの設定を別々のファイルに保存することです。
これを実現するには、`nginx.conf`を変更し、`server`コンテキストに`include subfolders-enabled/*.conf`を追加する必要があります。次のようになります。

```nginx
server {
  listen 80;
  server_name _;
  
  # その他の設定
  
  include subfolders-enabled/*.conf
}
```

この行を追加すると、Nginxの設定に`.conf`で終わるすべてのファイルが含まれます。`nginx.conf`ファイルと同じフォルダに`subfolders-enabled`という名前の新しいディレクトリを作成します。そのフォルダ内に、`.conf`で終わる認識しやすい名前のファイルを作成します。ファイルに上記の設定を追加し、Nginxを再起動またはリロードします。Radarrに`yourdomain.tld/radarr`でアクセスできるはずです。tldは[トップレベルドメイン](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)の略です。

### サブドメイン

代わりに、radarr用のサブドメインを使用することもできます。この場合、`radarr.yourdomain.tld`にアクセスします。これには、DNSで`Aレコード`または`CNAMEレコード`を設定する必要があります。
> 多くの無料DNSプロバイダはこれをサポートしていません {.is-warning}

デフォルトでは、Nginxには`sites-enabled`フォルダが含まれています。これを`nginx.conf`で確認できますが、ない場合は[includeディレクティブ](http://nginx.org/en/docs/ngx_core_module.html#include)を使用して追加できます。そして、とても重要なのは、`httpコンテキスト`の内部にある必要があります。次に、sites-enabledフォルダ内に設定ファイルを作成し、次の設定を入力します。

> この設定では、baseurlを''（空）に設定することをお勧めします。この設定では、デフォルトの`7878`を使用し、Radarrがlocalhost（127.0.0.1）でアクセス可能であることを前提としています。この設定では、サブドメイン`radarr`が選択されています（5行目）。{.is-info}

> カスタムのhttp/httpsサーバーポートを使用している場合は、Hostヘッダーにもそれを含めるようにしてください。例：`proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
server {
  listen      80;
  listen [::]:80;

  server_name radarr.*;

  location / {
    proxy_set_header   Host $host;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Host $host;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection $http_connection;

    proxy_redirect     off;
    proxy_http_version 1.1;
    
    proxy_pass http://127.0.0.1:7878;
  }
}
```

Nginxを再起動し、選択したサブドメインでRadarrにアクセスできるはずです。

## Apache

これは既存のVirtualHostサイト内に追加する必要があります。ドメインまたはサブドメインのルートを使用したい場合は、`Location`ブロックから`radarr`を削除し、場所として`/`を使用してください。

注意：`ProxyPass`と`ProxyPassReverse`の`baseurl`を削除しないでください。場所として`/`を使用したい場合に必要です。

```none
<Location /radarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:7878/radarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:7878/radarr
</Location>
```

`ProxyPreserveHost on`は、リバースプロキシを使用する際にapache2がlocalhostにリダイレクトしないようにします。

または、Radarr用の完全なVirtualHostを作成する場合は、次のようにします。

```none
ProxyPass / http://127.0.0.1:7878/radarr/
ProxyPassReverse / http://127.0.0.1:7878/radarr/
```

Apacheを介して追加の認証を実装する場合は、次のパスを除外する必要があります。

- `/radarr/api/`