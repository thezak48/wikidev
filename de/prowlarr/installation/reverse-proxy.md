# Reverse Proxy Konfiguration

Beispielkonfigurationen für die Konfiguration von Prowlarr für den Zugriff über einen Reverse Proxy.

> Diese Beispiele gehen davon aus, dass der Standardport `9696` verwendet wird und dass Sie eine Basis-URL von `prowlarr` festgelegt haben. Es wird auch davon ausgegangen, dass Ihr Webserver, z.B. Nginx, und Prowlarr auf demselben Server ausgeführt werden und unter `localhost` erreichbar sind. Andernfalls verwenden Sie stattdessen die IP-Adresse des Hosts oder einen FQDN.
{.is-info}

## NGINX

Fügen Sie die folgende Konfiguration zur `nginx.conf` hinzu, die sich im Stammverzeichnis Ihrer Nginx-Konfiguration befindet. Der Codeblock sollte innerhalb des `server context` hinzugefügt werden. [Vollständiges Beispiel einer typischen Nginx-Konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Wenn Sie einen nicht standardmäßigen HTTP/HTTPS-Serverport verwenden, stellen Sie sicher, dass auch Ihr Host-Header diesen enthält, z.B.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Erlaube den externen Zugriff auf die API/Indexer über NGINX
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

Eine bessere Möglichkeit, Ihre Konfigurationsdateien für Nginx zu organisieren, besteht darin, die Konfiguration für jede Website in einer separaten Datei zu speichern.
Um dies zu erreichen, müssen Sie `nginx.conf` ändern und `include subfolders-enabled/*.conf` im `server`-Kontext hinzufügen. Es sollte dann etwa so aussehen.

```nginx
server {
  listen 80;
  server_name _;
  
  # weitere Konfiguration
  
  include subfolders-enabled/*.conf
}
```

Durch das Hinzufügen dieser Zeile werden alle Dateien mit der Endung `.conf` in die Nginx-Konfiguration einbezogen. Erstellen Sie ein neues Verzeichnis namens `subfolders-enabled` im selben Ordner wie Ihre `nginx.conf`-Datei. Erstellen Sie in diesem Ordner eine Datei mit einem erkennbaren Namen, die mit `.conf` endet. Fügen Sie die obige Konfiguration aus der Datei hinzu und starten oder laden Sie Nginx neu. Sie sollten Radarr unter `yourdomain.tld/radarr` aufrufen können. "tld" steht für [Top-Level-Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomain

Alternativ können Sie eine Subdomain für Radarr verwenden. In diesem Fall würden Sie `radarr.yourdomain.tld` aufrufen. Dafür müssen Sie einen `A record` oder `CNAME record` in Ihrem DNS konfigurieren.
> Viele kostenlose DNS-Anbieter unterstützen dies nicht {.is-warning}
Standardmäßig enthält Nginx den Ordner `sites-enabled`. Sie können dies in `nginx.conf` überprüfen. Wenn nicht, können Sie ihn mit der [include directive](http://nginx.org/en/docs/ngx_core_module.html#include) hinzufügen. Und ganz wichtig, es muss sich im `http context` befinden. Erstellen Sie nun eine Konfigurationsdatei im Ordner `sites-enabled` und geben Sie die folgende Konfiguration ein.
> Für diese Konfiguration wird empfohlen, baseurl auf '' (leer) zu setzen. Diese Konfiguration geht davon aus, dass Sie den Standardport `7878` verwenden und Radarr auf dem localhost (127.0.0.1) erreichbar ist. Für diese Konfiguration wird die Subdomain `radarr` gewählt (Zeile 5).
{.is-info}
> Wenn Sie einen nicht standardmäßigen HTTP/HTTPS-Serverport verwenden, stellen Sie sicher, dass auch Ihr Host-Header diesen enthält, z.B.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Starten Sie nun Nginx neu und Prowlarr sollte unter Ihrer ausgewählten Subdomain verfügbar sein.

## Apache

Dies sollte innerhalb einer vorhandenen VirtualHost-Site hinzugefügt werden. Wenn Sie die Wurzel einer Domain oder Subdomain verwenden möchten, entfernen Sie `prowlarr` aus dem `Location`-Block und verwenden Sie einfach `/` als Standort.

Hinweis: Entfernen Sie die baseurl nicht aus ProxyPass und ProxyPassReverse, wenn Sie `/` als Standort verwenden möchten.

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on` verhindert, dass Apache2 bei Verwendung eines Reverse Proxys auf localhost umleitet.

Oder für die Erstellung eines vollständigen VirtualHosts für Prowlarr:

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

Wenn Sie eine zusätzliche Authentifizierung über Apache implementieren, sollten Sie die folgenden Pfade ausschließen:

- `/prowlarr/api/`

### Verwendung von SSL auf dem Reverse Proxy

Wenn der Reverse Proxy SSL-Terminierung durchführt (d.h. die URL zum Zugriff auf den Reverse Proxy verwendet das `https://`-Protokoll), müssen Sie Prowlarr mitteilen, dass es `https://` für seine API-Antworten verwenden soll, indem Sie `X-Forwarded-Proto` korrekt setzen. Der übliche Weg besteht darin, die folgenden Zeilen unter der `ProxyPassReverse`-Konfiguration hinzuzufügen:

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

Beachten Sie, dass diese Konfiguration das Aktivieren des `mod_header` Apache-Moduls erfordert, das oft nicht standardmäßig aktiviert ist.