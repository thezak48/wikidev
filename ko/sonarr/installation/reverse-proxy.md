# Reverse Proxy 구성

외부에서 Sonarr에 접근할 수 있도록 리버스 프록시를 통해 구성하는 예제 설정입니다.

> 이 예제는 기본 포트인 `8989`와 baseurl을 `sonarr`로 설정한 것을 가정합니다. 또한 웹 서버인 nginx와 Sonarr이 동일한 서버에서 `localhost` (127.0.0.1)로 접근 가능하다고 가정합니다. 그렇지 않은 경우 프록시 패스 지시문에 호스트 IP 주소 또는 호스트 이름을 사용하십시오.
{.is-info}

## NGINX

Nginx 구성 파일인 `nginx.conf`의 `server context` 내에 다음 구성을 추가하십시오. 코드 블록은 `server context` 내에 추가되어야 합니다. [전형적인 Nginx 구성의 전체 예제](https://www.nginx.com/resources/wiki/start/topics/examples/full/)를 참조하세요.

- mono 때문에 일반적인 $host 대신 $proxy_host가 필요함에 유의하세요.

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
# API 외부 접근을 위해 NGINX 허용
location ^~ /sonarr/api {
    auth_request      off;
    proxy_pass        http://127.0.0.1:8989;
}

```

Nginx의 구성 파일을 더 잘 구성하기 위해 각 사이트의 구성 파일을 별도의 파일로 저장하는 것이 좋습니다.
이를 위해 `nginx.conf`를 수정하고 `server` 컨텍스트에 `include subfolders-enabled/*.conf`를 추가해야 합니다. 따라서 다음과 같이 보일 것입니다.

```nginx
server {
  listen 80;
  server_name _;
  
  # 더 많은 구성
  
  include subfolders-enabled/*.conf
}
```

이 줄을 추가하면 Nginx 구성에 `.conf`로 끝나는 모든 파일이 포함됩니다. `nginx.conf` 파일이 있는 폴더와 동일한 위치에 `subfolders-enabled`라는 새 폴더를 만드세요. 그 폴더에 .conf로 끝나는 알아볼 수 있는 이름의 파일을 만드세요. 위의 파일에서 구성을 추가하고 Nginx를 재시작하거나 다시로드하세요. Sonarr을 `yourdomain.tld/sonarr`에서 방문할 수 있어야 합니다. tld는 [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)의 약자입니다.

### 서브도메인

대신 sonarr에 서브도메인을 사용할 수도 있습니다. 이 경우 `sonarr.yourdomain.tld`를 방문해야 합니다. 이를 위해 DNS에서 `A 레코드` 또는 `CNAME 레코드`를 구성해야 합니다.
> 많은 무료 DNS 제공업체가 이를 지원하지 않습니다. {.is-warning}

기본적으로 Nginx에는 `sites-enabled` 폴더가 포함되어 있습니다. `nginx.conf`에서 확인할 수 있으며, 포함되어 있지 않은 경우 [include 지시문](http://nginx.org/en/docs/ngx_core_module.html#include)을 사용하여 추가할 수 있습니다. 그리고 매우 중요한 것은 `http context` 내에 있어야 합니다. 이제 sites-enabled 폴더 내에 구성 파일을 만들고 다음 구성을 입력하세요.

> 이 구성에서는 baseurl을 '' (빈 값)로 설정하는 것이 좋습니다. 이 구성은 기본 `8989`를 사용하고 Sonarr이 localhost (127.0.0.1)에서 접근 가능한 것으로 가정합니다. 이 구성에서는 서브도메인 `sonarr`을 선택했습니다 (5번째 줄). {.is-info}

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

이제 Nginx를 재시작하면 선택한 서브도메인에서 Sonarr을 사용할 수 있습니다.

## Apache

기존 VirtualHost 사이트 내에 추가해야 합니다. 도메인 또는 서브도메인의 루트를 사용하려면 `Location` 블록에서 `sonarr`을 제거하고 위치로 `/`를 사용하면 됩니다.

참고: `/`를 위치로 사용하려면 ProxyPass 및 ProxyPassReverse에서 baseurl을 제거하지 마십시오.

```none
<Location /sonarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8989/sonarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8989/sonarr
</Location>
```

`ProxyPreserveHost on`은 리버스 프록시를 사용할 때 apache2가 localhost로 리디렉션되는 것을 방지합니다.

또는 Sonarr을 위한 전체 VirtualHost를 만들기 위해 다음과 같이 할 수 있습니다.

```none
ProxyPass / http://127.0.0.1:8989/sonarr/
ProxyPassReverse / http://127.0.0.1:8989/sonarr/
```

Apache를 통해 추가 인증을 구현하는 경우 다음 경로를 제외해야 합니다.

- `/sonarr/api/`
- `/sonarr/Content/`