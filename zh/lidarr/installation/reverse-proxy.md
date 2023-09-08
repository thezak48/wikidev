# 反向代理配置

配置Lidarr通过反向代理访问的示例配置。

> 这些示例假设默认端口为`8686`，并且您设置了`lidarr`的基本URL。它还假设您的Web服务器（例如nginx）和Lidarr在同一台服务器上，可以通过`localhost`访问。如果不是这样，请使用主机IP地址或FDQN代替代理传递。
{.is-info}

## NGINX

将以下配置添加到位于Nginx配置根目录中的`nginx.conf`文件中。代码块应添加到`server context`内。[完整的典型Nginx配置示例](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> 如果您使用的是非标准的http/https服务器端口，请确保您的Host标头也包含它，例如：`proxy_set_header Host $host:$server_port` {.is-warning}

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
# 允许通过NGINX访问API外部
location ~ /lidarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:8686;
}
```

更好的组织Nginx配置文件的方法是将每个站点的配置存储在单独的文件中。
为此，需要修改`nginx.conf`并在`server context`中添加`include subfolders-enabled/*.conf`。所以它看起来像这样。

```nginx
server {
  listen 80;
  server_name _;
  
  # 更多配置
  
  include subfolders-enabled/*.conf
}
```

添加此行将包含以`.conf`结尾的所有文件到Nginx配置中。在与`nginx.conf`文件位于同一文件夹中创建一个名为`subfolders-enabled`的新目录。在该文件夹中创建一个以`.conf`结尾的可识别名称的文件。从文件中添加上述配置，然后重新启动或重新加载Nginx。您应该能够在`yourdomain.tld/lidarr`访问Lidarr。tld是[顶级域名](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)的缩写。

### 子域名

或者，您可以使用lidarr的子域名。在这种情况下，您将访问`lidarr.yourdomain.tld`。为此，您需要在DNS中配置`A记录`或`CNAME记录`。
> 许多免费的DNS提供商不支持此功能 {.is-warning}
默认情况下，Nginx包含`sites-enabled`文件夹。您可以在`nginx.conf`中检查此设置，如果没有，可以使用[include指令](http://nginx.org/en/docs/ngx_core_module.html#include)添加它。非常重要的是，它必须位于`http context`内。现在，在`sites-enabled`文件夹中创建一个配置文件，并输入以下配置。
> 对于此配置，建议将baseurl设置为''（空）。此配置假设您使用默认的`8686`端口，并且Lidarr在本地主机（127.0.0.1）上可访问。对于此配置，选择了子域名`lidarr`（第5行）。{.is-info}
> 如果您使用的是非标准的http/https服务器端口，请确保您的Host标头也包含它，例如：`proxy_set_header Host $host:$server_port` {.is-warning}

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

现在重新启动Nginx，您应该能够在所选的子域名上访问Lidarr。

## Apache

这应该添加到现有的VirtualHost站点中。如果您希望使用域或子域的根目录，请从`Location`块中删除`lidarr`，并将位置简单地使用`/`。

注意：如果要将位置设置为`/`，请不要从ProxyPass和ProxyPassReverse中删除baseurl。

```none
<Location /lidarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8686/lidarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8686/lidarr
</Location>
```

`ProxyPreserveHost on` 防止apache2在使用反向代理时重定向到localhost。

或者为Lidarr创建一个完整的VirtualHost：

```none
ProxyPass / http://127.0.0.1:8686/lidarr/
ProxyPassReverse / http://127.0.0.1:8686/lidarr/
```

如果您通过Apache实施了任何其他身份验证，应该排除以下路径：

- `/lidarr/api/`