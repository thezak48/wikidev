# Konfiguration av omvänd proxy

Exempel på konfigurationsinställningar för att konfigurera Lidarr så att den kan nås via en omvänd proxy.

> Dessa exempel förutsätter att standardporten är `8686` och att du har ställt in en basurl på `lidarr`. Det förutsätter också att din webbserver, t.ex. nginx, och Lidarr körs på samma server som är åtkomlig via `localhost`. Om inte, använd värdens IP-adress eller en FQDN istället för proxy pass.
{.is-info}

## NGINX

Lägg till följande konfiguration i `nginx.conf` som finns i rotkatalogen för din Nginx-konfiguration. Kodblocket ska läggas till inuti `server context`. [Fullständigt exempel på en typisk Nginx-konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Om du använder en icke-standard HTTP/HTTPS-serverport, se till att din Host-header också inkluderar den, t.ex.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Tillåt API-extern åtkomst via NGINX
location ~ /lidarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:8686;
}
```

Ett bättre sätt att organisera dina konfigurationsfiler för Nginx är att lagra konfigurationen för varje webbplats i en separat fil.
För att uppnå detta måste du ändra `nginx.conf` och lägga till `include subfolders-enabled/*.conf` i `server`-kontexten. Det kommer att se ut något så här.

```nginx
server {
  listen 80;
  server_name _;
  
  # mer konfiguration
  
  include subfolders-enabled/*.conf
}
```

Genom att lägga till denna rad inkluderas alla filer som slutar med `.conf` i Nginx-konfigurationen. Skapa en ny mapp som heter `subfolders-enabled` i samma mapp som din `nginx.conf`-fil finns. I den mappen skapar du en fil med ett igenkännligt namn som slutar med .conf. Lägg till konfigurationen ovan från filen och starta om eller ladda om Nginx. Du bör kunna besöka Lidarr på `yourdomain.tld/lidarr`. tld står för [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomän

Alternativt kan du använda en subdomän för Lidarr. I det här fallet skulle du besöka `lidarr.yourdomain.tld`. För detta måste du konfigurera en `A-record` eller `CNAME-record` i din DNS.
> Många gratis DNS-leverantörer stöder inte detta {.is-warning}
Som standard inkluderar Nginx mappen `sites-enabled`. Du kan kontrollera detta i `nginx.conf`, om inte kan du lägga till det med hjälp av [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Och väldigt viktigt, det måste vara inuti `http context`. Skapa nu en konfigurationsfil i mappen sites-enabled och ange följande konfiguration.
> För denna konfiguration rekommenderas det att ställa in baseurl till '' (tom). Denna konfiguration förutsätter att du använder standardporten `8686` och att Lidarr är åtkomlig på localhost (127.0.0.1). För denna konfiguration väljs subdomänen `lidarr` (rad 5). {.is-info}
> Om du använder en icke-standard HTTP/HTTPS-serverport, se till att din Host-header också inkluderar den, t.ex.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Starta nu om Nginx och Lidarr bör vara tillgängligt på din valda subdomän.

## Apache

Detta bör läggas till inom en befintlig VirtualHost-webbplats. Om du vill använda roten för en domän eller subdomän, ta bort `lidarr` från `Location`-blocket och använd helt enkelt `/` som plats.

Observera: Ta inte bort baseurl från ProxyPass och ProxyPassReverse om du vill använda `/` som plats.

```none
<Location /lidarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8686/lidarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8686/lidarr
</Location>
```

`ProxyPreserveHost on` förhindrar att apache2 omdirigerar till localhost vid användning av en omvänd proxy.

Eller för att skapa en hel VirtualHost för Lidarr:

```none
ProxyPass / http://127.0.0.1:8686/lidarr/
ProxyPassReverse / http://127.0.0.1:8686/lidarr/
```

Om du implementerar någon ytterligare autentisering genom Apache bör du exkludera följande sökvägar:

- `/lidarr/api/`