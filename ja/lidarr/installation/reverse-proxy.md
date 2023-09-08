# リバースプロキシの設定

Lidarrをリバースプロキシを介してアクセス可能にするためのサンプル設定例です。

> これらの例では、デフォルトのポート`8686`と、ベースURLを`lidarr`に設定したことを前提としています。また、Webサーバー（例：nginx）とLidarrが同じサーバーで実行され、`localhost`でアクセス可能であることを前提としています。そうでない場合は、プロキシパスにホストのIPアドレスまたはFQDNを使用してください。
{.is-info}

## NGINX

Nginxのルートにある`nginx.conf`に以下の設定を追加します。コードブロックは`serverコンテキスト`の内部に追加する必要があります。[典型的なNginxの設定の完全な例](https://www.nginx.com/resources/wiki/start/topics/examples/full/)も参照してください。

> カスタムのhttp/httpsサーバーポートを使用している場合は、Hostヘッダにもそれを含めるようにしてください。例：`proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
location ^~ /lidarr {
    proxy_pass http://127.0.0.1:8686;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_redirect off;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $http_connection;
}
# Allow the API External Access via NGINX
location ~ /lidarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:8686;
}
```

Nginxの設定ファイルを整理するためのより良い方法は、各サイトの設定を別々のファイルに保存することです。
これを実現するには、`nginx.conf`を変更し、`server`コンテキストに`include subfolders-enabled/*.conf`を追加する必要があります。以下のようになります。

```nginx
server {
  listen 80;
  server_name _;
  
  # more configuration
  
  include subfolders-enabled/*.conf
}
```

この行を追加すると、Nginxの設定に`.conf`で終わるすべてのファイルが含まれます。`nginx.conf`ファイルと同じフォルダに`subfolders-enabled`という名前の新しいディレクトリを作成します。そのフォルダ内に、`.conf`で終わる認識しやすい名前のファイルを作成します。ファイルに上記の設定を追加し、Nginxを再起動またはリロードします。`yourdomain.tld/lidarr`でLidarrにアクセスできるはずです。tldは[トップレベルドメイン](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)の略です。

### サブドメイン

代わりに、lidarrにサブドメインを使用することもできます。この場合、`lidarr.yourdomain.tld`にアクセスします。これには、DNSで`Aレコード`または`CNAMEレコード`を設定する必要があります。
> 多くの無料DNSプロバイダはこれをサポートしていません {.is-warning}
デフォルトでは、Nginxには`sites-enabled`フォルダが含まれています。これは`nginx.conf`で確認できますが、含まれていない場合は、[includeディレクティブ](http://nginx.org/en/docs/ngx_core_module.html#include)を使用して追加できます。そして、非常に重要なのは、`httpコンテキスト`の内部にある必要があります。次に、`sites-enabled`フォルダ内に設定ファイルを作成し、次の設定を入力します。
> この設定では、baseurlを''（空）に設定することをお勧めします。この設定では、デフォルトの`8686`を使用し、Lidarrがlocalhost（127.0.0.1）でアクセス可能であることを前提としています。この設定では、サブドメイン`lidarr`が選択されています（5行目）。{.is-info}
> カスタムのhttp/httpsサーバーポートを使用している場合は、Hostヘッダにもそれを含めるようにしてください。例：`proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
server {
  listen      80;
  listen [::]:80;
  server_name lidarr.*;
  location / {
    proxy_set_header   Host $host;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Host $host;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection $http_connection;
    proxy_redirect     off;
    proxy_http_version 1.1;
    
    proxy_pass http://127.0.0.1:8686;
  }
}
```

Nginxを再起動し、選択したサブドメインでLidarrにアクセスできるはずです。

## Apache

これは既存のVirtualHostサイト内に追加する必要があります。ドメインまたはサブドメインのルートを使用する場合は、`Location`ブロックから`lidarr`を削除し、場所として単に`/`を使用してください。

注意：`ProxyPass`と`ProxyPassReverse`からbaseurlを削除しないでください。場所として`/`を使用する場合に必要です。

```none
<Location /lidarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8686/lidarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8686/lidarr
</Location>
```

`ProxyPreserveHost on`は、リバースプロキシを使用する際にapache2がlocalhostにリダイレクトしないようにします。

または、Lidarr用の完全なVirtualHostを作成する場合は、次のようにします。

```none
ProxyPass / http://127.0.0.1:8686/lidarr/
ProxyPassReverse / http://127.0.0.1:8686/lidarr/
```

Apacheを使用して追加の認証を実装する場合は、次のパスを除外する必要があります。

- `/lidarr/api/`