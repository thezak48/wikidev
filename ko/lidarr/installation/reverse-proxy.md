# Reverse Proxy Configuration

리버스 프록시를 통해 Lidarr에 접근할 수 있도록 구성하는 예제 설정입니다.

> 이 예제는 기본 포트인 `8686`과 `lidarr`을 기본 URL로 설정한 것을 가정합니다. 또한, 웹 서버(예: nginx)와 Lidarr이 동일한 서버에서 실행되고 `localhost`로 접근 가능하다고 가정합니다. 그렇지 않은 경우, 프록시 패스에 호스트 IP 주소나 FQDN을 사용하십시오.
{.is-info}

## NGINX

Nginx 구성 파일인 `nginx.conf`에 다음 구성을 추가하십시오. 코드 블록은 `server context` 내부에 추가되어야 합니다. [전형적인 Nginx 구성의 전체 예제](https://www.nginx.com/resources/wiki/start/topics/examples/full/)를 참조하세요.

> 비표준 http/https 서버 포트를 사용하는 경우, Host 헤더에도 포트를 포함해야 합니다. 예: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Nginx의 구성 파일을 더 잘 구성하기 위해 각 사이트의 구성을 별도의 파일에 저장하는 것이 좋습니다.
이를 위해 `nginx.conf`를 수정하고 `server` context에 `include subfolders-enabled/*.conf`를 추가해야 합니다. 아래와 같이 보일 것입니다.

```nginx
server {
  listen 80;
  server_name _;
  
  # more configuration
  
  include subfolders-enabled/*.conf
}
```

이 줄을 추가하면 `.conf`로 끝나는 모든 파일이 Nginx 구성에 포함됩니다. `nginx.conf` 파일이 있는 폴더와 동일한 위치에 `subfolders-enabled`라는 새 폴더를 만드십시오. 그 폴더에 .conf로 끝나는 알아볼 수 있는 이름의 파일을 만들고 위의 구성을 추가한 다음 Nginx를 재시작하거나 다시 로드하십시오. 이제 `yourdomain.tld/lidarr`에서 Lidarr에 접속할 수 있어야 합니다. tld는 [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)의 약자입니다.

### 서브도메인

대신 lidarr을 위한 서브도메인을 사용할 수도 있습니다. 이 경우 `lidarr.yourdomain.tld`를 방문하면 됩니다. 이를 위해 DNS에서 `A 레코드` 또는 `CNAME 레코드`를 구성해야 합니다.
> 많은 무료 DNS 제공업체에서는 이를 지원하지 않습니다. {.is-warning}
기본적으로 Nginx에는 `sites-enabled` 폴더가 포함되어 있습니다. `nginx.conf`에서 확인할 수 있으며, 없는 경우 [include 지시문](http://nginx.org/en/docs/ngx_core_module.html#include)을 사용하여 추가할 수 있습니다. 그리고 매우 중요한 점은 `http context` 내부에 있어야 합니다. 이제 sites-enabled 폴더에 구성 파일을 만들고 다음 구성을 입력하십시오.
> 이 구성에서는 baseurl을 ''(빈 값)로 설정하는 것이 좋습니다. 이 구성은 기본 `8686`을 사용하고 Lidarr이 localhost(127.0.0.1)에서 접근 가능한 경우를 가정합니다. 이 구성에서는 서브도메인 `lidarr`을 선택했습니다(5번째 줄). {.is-info}
> 비표준 http/https 서버 포트를 사용하는 경우, Host 헤더에도 포트를 포함해야 합니다. 예: `proxy_set_header Host $host:$server_port` {.is-warning}

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

이제 Nginx를 재시작하면 선택한 서브도메인에서 Lidarr에 접속할 수 있습니다.

## Apache

기존 VirtualHost 사이트 내에 추가해야 합니다. 도메인 또는 서브도메인의 루트를 사용하려는 경우, `Location` 블록에서 `lidarr`을 제거하고 위치로 `/`를 사용하면 됩니다.

참고: `/`를 위치로 사용하려는 경우에도 ProxyPass와 ProxyPassReverse에서 baseurl을 제거하지 마십시오.

```none
<Location /lidarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8686/lidarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8686/lidarr
</Location>
```

`ProxyPreserveHost on`은 아파치가 리버스 프록시를 사용할 때 localhost로 리디렉션하는 것을 방지합니다.

또는 Lidarr을 위한 전체 VirtualHost를 만들기 위해 다음 구성을 사용할 수 있습니다.

```none
ProxyPass / http://127.0.0.1:8686/lidarr/
ProxyPassReverse / http://127.0.0.1:8686/lidarr/
```

Apache를 통해 추가 인증을 구현하는 경우 다음 경로를 제외해야 합니다:

- `/lidarr/api/`