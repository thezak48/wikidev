# Reverse Proxy Konfiguration

Beispielkonfigurationen zur Konfiguration von Radarr, um über einen Reverse Proxy aus der Außenwelt erreichbar zu sein.

> Diese Beispiele gehen davon aus, dass der Standardport `7878` verwendet wird und dass Sie eine Basis-URL von `radarr` festgelegt haben. Es wird auch davon ausgegangen, dass Ihr Webserver, z.B. Nginx, und Radarr auf demselben Server ausgeführt werden und unter `localhost` (127.0.0.1) erreichbar sind. Andernfalls verwenden Sie stattdessen die IP-Adresse oder den Hostnamen des Hosts für die Proxy-Pass-Anweisung.
{.is-info}

## NGINX

Fügen Sie die folgende Konfiguration zur `nginx.conf` hinzu, die sich im Stammverzeichnis Ihrer Nginx-Konfiguration befindet. Der Codeblock sollte innerhalb des `server-Kontexts` hinzugefügt werden. [Vollständiges Beispiel einer typischen Nginx-Konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Wenn Sie einen nicht standardmäßigen HTTP/HTTPS-Serverport verwenden, stellen Sie sicher, dass der Host-Header auch diesen enthält, z.B.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Ermöglichen Sie den externen Zugriff auf die API über NGINX
location ^~ /radarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:7878;
}
```

Eine bessere Möglichkeit, Ihre Konfigurationsdateien für Nginx zu organisieren, besteht darin, die Konfiguration für jede Website in einer separaten Datei zu speichern.
Um dies zu erreichen, müssen Sie `nginx.conf` ändern und `include subfolders-enabled/*.conf` im `server-Kontext` hinzufügen. Es sollte also etwa so aussehen.

```nginx
server {
  listen 80;
  server_name _;
  
  # weitere Konfiguration
  
  include subfolders-enabled/*.conf
}
```

Durch das Hinzufügen dieser Zeile werden alle Dateien mit der Endung `.conf` in die Nginx-Konfiguration aufgenommen. Erstellen Sie ein neues Verzeichnis namens `subfolders-enabled` im selben Ordner wie Ihre `nginx.conf`-Datei. Erstellen Sie in diesem Ordner eine Datei mit einem erkennbaren Namen, die mit `.conf` endet. Fügen Sie die obige Konfiguration aus der Datei hinzu und starten oder laden Sie Nginx neu. Sie sollten Radarr unter `yourdomain.tld/radarr` aufrufen können. tld steht für [Top-Level-Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomain

Alternativ können Sie eine Subdomain für Radarr verwenden. In diesem Fall würden Sie `radarr.yourdomain.tld` aufrufen. Dafür müssen Sie einen `A-Record` oder `CNAME-Record` in Ihrem DNS konfigurieren.
> Viele kostenlose DNS-Anbieter unterstützen dies nicht {.is-warning}

Standardmäßig enthält Nginx den Ordner `sites-enabled`. Sie können dies in `nginx.conf` überprüfen. Wenn nicht, können Sie es mit der [include-Anweisung](http://nginx.org/en/docs/ngx_core_module.html#include) hinzufügen. Und ganz wichtig, es muss sich im `http-Kontext` befinden. Erstellen Sie nun eine Konfigurationsdatei im Ordner `sites-enabled` und geben Sie die folgende Konfiguration ein.

> Für diese Konfiguration wird empfohlen, die Basis-URL auf '' (leer) zu setzen. Diese Konfiguration geht davon aus, dass Sie den Standardport `7878` verwenden und Radarr unter localhost (127.0.0.1) erreichbar ist. Für diese Konfiguration wird die Subdomain `radarr` gewählt (Zeile 5). {.is-info}

> Wenn Sie einen nicht standardmäßigen HTTP/HTTPS-Serverport verwenden, stellen Sie sicher, dass der Host-Header auch diesen enthält, z.B.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Starten Sie nun Nginx neu und Radarr sollte unter Ihrer ausgewählten Subdomain verfügbar sein.

## Apache

Dies sollte zu einer vorhandenen VirtualHost-Site hinzugefügt werden. Wenn Sie die Wurzel einer Domain oder Subdomain verwenden möchten, entfernen Sie `radarr` aus dem `Location`-Block und verwenden Sie einfach `/` als Standort.

Hinweis: Entfernen Sie die Basis-URL nicht aus ProxyPass und ProxyPassReverse, wenn Sie `/` als Standort verwenden möchten.

```none
<Location /radarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:7878/radarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:7878/radarr
</Location>
```

`ProxyPreserveHost on` verhindert, dass Apache2 bei Verwendung eines Reverse Proxys auf localhost umleitet.

Oder um einen vollständigen VirtualHost für Radarr zu erstellen:

```none
ProxyPass / http://127.0.0.1:7878/radarr/
ProxyPassReverse / http://127.0.0.1:7878/radarr/
```

Wenn Sie eine zusätzliche Authentifizierung über Apache implementieren, sollten Sie die folgenden Pfade ausschließen:

- `/radarr/api/`