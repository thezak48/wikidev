# 反向代理配置

配置 Prowlarr 通过反向代理访问的示例配置。

> 这些示例假设默认端口为 `9696`，并且您设置了一个基本 URL 为 `prowlarr`。它还假设您的 Web 服务器（如 Nginx）和 Prowlarr 在同一台服务器上，可以通过 `localhost` 访问。如果不是这样，请改用主机 IP 地址或完全限定域名。
{.is-info}

## NGINX

将以下配置添加到位于 Nginx 配置根目录的 `nginx.conf` 文件中。代码块应添加到 `server context` 内。[完整的典型 Nginx 配置示例](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> 如果您使用的是非标准的 http/https 服务器端口，请确保您的 Host 标头也包含它，例如：`proxy_set_header Host $host:$server_port` {.is-warning}

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
# 允许通过 NGINX 访问 API/Indexer
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

更好的组织 Nginx 配置文件的方法是将每个站点的配置文件存储在单独的文件中。
为此，需要修改 `nginx.conf`，并在 `server context` 中添加 `include subfolders-enabled/*.conf`。因此，它将类似于以下内容。

```nginx
server {
  listen 80;
  server_name _;
  
  # 更多配置
  
  include subfolders-enabled/*.conf
}
```

添加此行将包含以 `.conf` 结尾的所有文件到 Nginx 配置中。在与 `nginx.conf` 文件位于同一文件夹中创建一个名为 `subfolders-enabled` 的新目录。在该文件夹中创建一个以 `.conf` 结尾的可识别名称的文件。将上述文件中的配置添加到该文件中，然后重新启动或重新加载 Nginx。您应该能够通过 `yourdomain.tld/radarr` 访问 Prowlarr。tld 是 [顶级域名](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains) 的缩写。

### 子域名

或者，您可以使用子域名来访问 Prowlarr。在这种情况下，您将访问 `radarr.yourdomain.tld`。为此，您需要在 DNS 中配置 `A 记录` 或 `CNAME 记录`。
> 许多免费的 DNS 提供商不支持此功能 {.is-warning}

默认情况下，Nginx 包含 `sites-enabled` 文件夹。您可以在 `nginx.conf` 中检查此项，如果没有，可以使用 [include 指令](http://nginx.org/en/docs/ngx_core_module.html#include) 添加它。非常重要的是，它必须位于 `http context` 内。现在，在 `sites-enabled` 文件夹中创建一个配置文件，并输入以下配置。
> 对于此配置，建议将 baseurl 设置为 ''（空）。此配置假设您使用默认的 `7878` 端口，并且 Radarr 在本地主机（127.0.0.1）上可访问。对于此配置，选择了子域名 `radarr`（第 5 行）。
{.is-info}
> 如果您使用的是非标准的 http/https 服务器端口，请确保您的 Host 标头也包含它，例如：`proxy_set_header Host $host:$server_port` {.is-warning}

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

现在重新启动 Nginx，Prowlarr 应该可以在您选择的子域名上访问。

## Apache

这应该添加到现有的 VirtualHost 站点中。如果您希望使用域名或子域名的根目录，请从 `Location` 块中删除 `prowlarr`，并将位置简单地设置为 `/`。

注意：如果您希望将位置设置为 `/`，请不要从 ProxyPass 和 ProxyPassReverse 中删除 baseurl。

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on` 防止 apache2 在使用反向代理时重定向到 localhost。

或者，为 Prowlarr 创建一个完整的 VirtualHost：

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

如果您通过 Apache 实施了任何其他身份验证，您应该排除以下路径：

- `/prowlarr/api/`

### 在反向代理上使用 SSL

如果反向代理执行了 SSL 终止（即访问反向代理的 URL 使用 `https://` 协议），则需要正确设置 `X-Forwarded-Proto`，以告诉 Prowlarr 它应该使用 `https://` 作为其 API 响应。常见的方法是在 `ProxyPassReverse` 配置下添加以下行：

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

请注意，此配置需要启用 `mod_header` Apache 模块，这通常不是默认启用的。