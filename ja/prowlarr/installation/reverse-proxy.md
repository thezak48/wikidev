# リバースプロキシの設定

Prowlarrをリバースプロキシを介してアクセス可能にするためのサンプル設定例です。

> これらの例では、デフォルトのポート番号が`9696`であり、ベースURLが`prowlarr`に設定されていることを前提としています。また、Webサーバー（例：nginx）とProwlarrが同じサーバーで実行され、`localhost`でアクセス可能であることを前提としています。そうでない場合は、ホストのIPアドレスまたはFQDNを使用してください。
{.is-info}

## NGINX

以下の設定をNginx設定のルートにある`nginx.conf`に追加します。コードブロックは`server context`の内部に追加する必要があります。[典型的なNginx設定の完全な例](https://www.nginx.com/resources/wiki/start/topics/examples/full/)も参照してください。

> 非標準のhttp/httpsサーバーポートを使用している場合は、Hostヘッダーにもそれを含めるようにしてください。例：`proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
location ~ /prowlarr {
    proxy_pass http://127.0.0.1:9696;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_redirect off;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $http_connection;
}
# Allow the API/Indexer External Access via NGINX
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

Nginxの設定ファイルを整理するためのより良い方法は、各サイトの設定を別々のファイルに保存することです。
これを実現するには、`nginx.conf`を変更し、`server`コンテキストに`include subfolders-enabled/*.conf`を追加する必要があります。次のようになります。

```nginx
server {
  listen 80;
  server_name _;
  
  # more configuration
  
  include subfolders-enabled/*.conf
}
```

この行を追加すると、Nginxの設定に`.conf`で終わるすべてのファイルが含まれます。`nginx.conf`ファイルと同じフォルダに`subfolders-enabled`という名前の新しいディレクトリを作成します。そのフォルダに、`.conf`で終わる認識しやすい名前のファイルを作成します。ファイルに上記の設定を追加し、Nginxを再起動またはリロードします。`yourdomain.tld/radarr`にアクセスできるはずです。tldは[トップレベルドメイン](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)の略です。

### サブドメイン

代わりに、radarrのためにサブドメインを使用することもできます。この場合、`radarr.yourdomain.tld`にアクセスします。これには、DNSで`Aレコード`または`CNAMEレコード`を設定する必要があります。
> 多くの無料DNSプロバイダはこれをサポートしていません {.is-warning}
デフォルトでは、Nginxには`sites-enabled`フォルダが含まれています。これを`nginx.conf`で確認できますが、含まれていない場合は、[includeディレクティブ](http://nginx.org/en/docs/ngx_core_module.html#include)を使用して追加できます。そして、非常に重要なのは、それが`http context`の内部にある必要があります。次に、sites-enabledフォルダ内に設定ファイルを作成し、次の設定を入力します。
> この設定では、baseurlを''（空）に設定することをお勧めします。この設定では、デフォルトの`7878`を使用し、Radarrがlocalhost（127.0.0.1）でアクセス可能であることを前提としています。この設定では、サブドメイン`radarr`が選択されています（5行目）。
{.is-info}
> 非標準のhttp/httpsサーバーポートを使用している場合は、Hostヘッダーにもそれを含めるようにしてください。例：`proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
server {
  listen      80;
  listen [::]:80;
  server_name prowlarr.*;
  location / {
    proxy_set_header   Host $host;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Host $host;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection $http_connection;
    proxy_redirect     off;
    proxy_http_version 1.1;
    
    proxy_pass http://127.0.0.1:9696;
  }
}
```

Nginxを再起動すると、選択したサブドメインでProwlarrにアクセスできるようになります。

## Apache

これは既存のVirtualHostサイト内に追加する必要があります。ドメインまたはサブドメインのルートを使用する場合は、`Location`ブロックから`prowlarr`を削除し、場所として単に`/`を使用してください。

注意：`ProxyPass`と`ProxyPassReverse`の`baseurl`を削除しないでください。場所として`/`を使用する場合に使用する場合、これらの設定が必要です。

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on`は、リバースプロキシを使用する際にapache2がlocalhostにリダイレクトしないようにします。

または、Prowlarr用の完全なVirtualHostを作成する場合は、次のようにします。

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

Apacheを介して追加の認証を実装する場合は、次のパスを除外する必要があります。

- `/prowlarr/api/`

### リバースプロキシでSSLを使用する場合

リバースプロキシがSSL終端を行う場合（リバースプロキシへのアクセスURLが`https://`プロトコルを使用している場合）、Prowlarrに正しい`https://`を使用してAPIレスポンスを行うようにするために、`X-Forwarded-Proto`を適切に設定する必要があります。一般的な方法は、次の行を`ProxyPassReverse`の設定の下に追加することです。

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

この設定では、通常デフォルトで有効になっていない`mod_header` Apacheモジュールを有効にする必要があります。