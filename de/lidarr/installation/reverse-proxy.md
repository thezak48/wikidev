# Reverse Proxy Konfiguration

Beispielkonfigurationen zur Konfiguration von Lidarr für den Zugriff über einen Reverse Proxy.

> Diese Beispiele gehen davon aus, dass der Standardport `8686` verwendet wird und dass Sie eine Basis-URL von `lidarr` festgelegt haben. Es wird auch davon ausgegangen, dass Ihr Webserver, z.B. Nginx, und Lidarr auf demselben Server ausgeführt werden und unter `localhost` erreichbar sind. Andernfalls verwenden Sie stattdessen die IP-Adresse des Hosts oder einen FQDN für den Proxy-Pass.
{.is-info}

## NGINX

Fügen Sie die folgende Konfiguration zur `nginx.conf` hinzu, die sich im Stammverzeichnis Ihrer Nginx-Konfiguration befindet. Der Codeblock sollte innerhalb des `server`-Kontexts hinzugefügt werden. [Vollständiges Beispiel einer typischen Nginx-Konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Wenn Sie einen nicht standardmäßigen HTTP/HTTPS-Serverport verwenden, stellen Sie sicher, dass der Host-Header auch den Port enthält, z.B.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Ermöglichen Sie den externen Zugriff auf die API über NGINX
location ~ /lidarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:8686;
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

Durch das Hinzufügen dieser Zeile werden alle Dateien mit der Endung `.conf` in die Nginx-Konfiguration einbezogen. Erstellen Sie ein neues Verzeichnis namens `subfolders-enabled` im selben Ordner wie Ihre `nginx.conf`-Datei. Erstellen Sie in diesem Ordner eine Datei mit einem erkennbaren Namen, die mit `.conf` endet. Fügen Sie die oben genannte Konfiguration aus der Datei hinzu und starten oder laden Sie Nginx neu. Sie sollten Lidarr unter `yourdomain.tld/lidarr` aufrufen können. "tld" steht für [Top-Level-Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains).

### Subdomain

Alternativ können Sie eine Subdomain für Lidarr verwenden. In diesem Fall würden Sie `lidarr.yourdomain.tld` aufrufen. Dafür müssen Sie einen `A-Record` oder `CNAME-Record` in Ihrer DNS-Konfiguration festlegen.
> Viele kostenlose DNS-Anbieter unterstützen dies nicht {.is-warning}
Standardmäßig enthält Nginx den Ordner `sites-enabled`. Sie können dies in `nginx.conf` überprüfen. Wenn er nicht vorhanden ist, können Sie ihn mit der [include-Direktive](http://nginx.org/en/docs/ngx_core_module.html#include) hinzufügen. Und ganz wichtig, es muss sich im `http`-Kontext befinden. Erstellen Sie nun eine Konfigurationsdatei im Ordner `sites-enabled` und geben Sie die folgende Konfiguration ein.
> Für diese Konfiguration wird empfohlen, die Basis-URL auf '' (leer) zu setzen. Diese Konfiguration geht davon aus, dass Sie den Standardport `8686` verwenden und Lidarr auf dem Localhost (127.0.0.1) erreichbar ist. Für diese Konfiguration wird die Subdomain `lidarr` gewählt (Zeile 5). {.is-info}
> Wenn Sie einen nicht standardmäßigen HTTP/HTTPS-Serverport verwenden, stellen Sie sicher, dass der Host-Header auch den Port enthält, z.B.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Starten Sie nun Nginx neu und Lidarr sollte unter Ihrer ausgewählten Subdomain verfügbar sein.

## Apache

Dies sollte innerhalb einer vorhandenen VirtualHost-Site hinzugefügt werden. Wenn Sie die Wurzel einer Domain oder Subdomain verwenden möchten, entfernen Sie `lidarr` aus dem `Location`-Block und verwenden Sie einfach `/` als Ort.

Hinweis: Entfernen Sie die Basis-URL nicht aus ProxyPass und ProxyPassReverse, wenn Sie `/` als Ort verwenden möchten.

```none
<Location /lidarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8686/lidarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8686/lidarr
</Location>
```

`ProxyPreserveHost on` verhindert, dass Apache2 bei Verwendung eines Reverse Proxys auf localhost umleitet.

Oder um einen vollständigen VirtualHost für Lidarr zu erstellen:

```none
ProxyPass / http://127.0.0.1:8686/lidarr/
ProxyPassReverse / http://127.0.0.1:8686/lidarr/
```

Wenn Sie zusätzliche Authentifizierung über Apache implementieren, sollten Sie die folgenden Pfade ausschließen:

- `/lidarr/api/`