# リバースプロキシの設定

Sonarrをリバースプロキシを介して外部からアクセスできるようにするためのサンプル設定例です。

> これらの例では、デフォルトのポート番号`8989`とベースURL`sonarr`が設定されていることを前提としています。また、Webサーバー（例：nginx）とSonarrが同じサーバーで実行され、`localhost`（127.0.0.1）でアクセス可能であることを前提としています。もし異なる場合は、プロキシパスディレクティブにホストのIPアドレスまたはホスト名を使用してください。
{.is-info}

## NGINX

以下の設定をNginxの設定ファイルである`nginx.conf`に追加します。コードブロックは`server context`内に追加する必要があります。[典型的なNginxの設定の完全な例](https://www.nginx.com/resources/wiki/start/topics/examples/full/)を参照してください。

- 注意：monoのため、通常の`$host`ではなく`$proxy_host`が必要です。

```nginx
location ^~ /sonarr {
  proxy_pass         http://127.0.0.1:8989/sonarr;
  proxy_set_header   Host $proxy_host;
  proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
  proxy_set_header   X-Forwarded-Host $host;
  proxy_set_header   X-Forwarded-Proto $scheme;
  proxy_redirect     off;
  proxy_http_version 1.1;
  proxy_set_header   Upgrade $http_upgrade;
  proxy_set_header   Connection $http_connection;
}
# Allow the API External Access via NGINX
location ^~ /sonarr/api {
    auth_request      off;
    proxy_pass        http://127.0.0.1:8989;
}

```

Nginxの設定ファイルを整理するためのより良い方法は、各サイトの設定を別々のファイルに保存することです。
これを実現するには、`nginx.conf`を変更し、`server`コンテキストに`include subfolders-enabled/*.conf`を追加する必要があります。以下のようになります。

```nginx
server {
  listen 80;
  server_name _;
  
  # その他の設定
  
  include subfolders-enabled/*.conf
}
```

この行を追加すると、Nginxの設定に`.conf`で終わるすべてのファイルが含まれます。`nginx.conf`ファイルと同じフォルダに`subfolders-enabled`という名前の新しいディレクトリを作成してください。そのフォルダ内に、`.conf`で終わる認識しやすい名前のファイルを作成し、上記の設定を追加し、Nginxを再起動またはリロードしてください。Sonarrに`yourdomain.tld/sonarr`でアクセスできるはずです。tldは[トップレベルドメイン](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)の略です。

### サブドメイン

代わりに、sonarr用のサブドメインを使用することもできます。この場合、`sonarr.yourdomain.tld`にアクセスします。これには、DNSで`Aレコード`または`CNAMEレコード`を設定する必要があります。
> 多くの無料DNSプロバイダはこれをサポートしていません {.is-warning}

デフォルトでは、Nginxには`sites-enabled`フォルダが含まれています。`nginx.conf`でこれを確認できますが、ない場合は[includeディレクティブ](http://nginx.org/en/docs/ngx_core_module.html#include)を使用して追加できます。そして、非常に重要なのは、`http context`内にある必要があります。次に、sites-enabledフォルダ内に設定ファイルを作成し、次の設定を入力します。

> この設定では、baseurlを''（空）に設定することをお勧めします。この設定では、デフォルトの`8989`を使用し、Sonarrがlocalhost（127.0.0.1）でアクセス可能であることを前提としています。この設定では、サブドメイン`sonarr`が選択されています（5行目）。{.is-info}

```nginx
server {
  listen      80;
  listen [::]:80;

  server_name sonarr.*;

  location / {
    proxy_set_header   Host $proxy_host;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Host $host;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection $http_connection;

    proxy_redirect     off;
    proxy_http_version 1.1;
    
    proxy_pass http://127.0.0.1:8989;
  }
}
```

Nginxを再起動し、選択したサブドメインでSonarrにアクセスできるはずです。

## Apache

これは既存のVirtualHostサイト内に追加する必要があります。ドメインまたはサブドメインのルートを使用する場合は、`Location`ブロックから`sonarr`を削除し、場所として`/`を使用してください。

注意：`ProxyPass`と`ProxyPassReverse`の`baseurl`を削除しないでください。場所として`/`を使用する場合に必要です。

```none
<Location /sonarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8989/sonarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8989/sonarr
</Location>
```

`ProxyPreserveHost on`は、リバースプロキシを使用する際にapache2がlocalhostにリダイレクトしないようにします。

または、Sonarr用の完全なVirtualHostを作成する場合は、次のようにします。

```none
ProxyPass / http://127.0.0.1:8989/sonarr/
ProxyPassReverse / http://127.0.0.1:8989/sonarr/
```

Apacheを使用して追加の認証を実装する場合は、次のパスを除外する必要があります。

- `/sonarr/api/`
- `/sonarr/Content/`