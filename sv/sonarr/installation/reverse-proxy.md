# Konfiguration av omvänd proxy

Exempel på konfigurationsinställningar för att konfigurera Sonarr så att den kan nås från omvärlden genom en omvänd proxy.

> Dessa exempel förutsätter att standardporten är `8989` och att du har ställt in en basurl på `sonarr`. Det förutsätter också att din webbserver, t.ex. nginx, och Sonarr körs på samma server och är åtkomliga via `localhost` (127.0.0.1). Om inte, använd värdens IP-adress eller värdnamn istället för proxy pass direktivet.
{.is-info}

## NGINX

Lägg till följande konfiguration i `nginx.conf` som finns i rotkatalogen för din Nginx-konfiguration. Kodblocket ska läggas till inuti `server context`. [Fullständigt exempel på en typisk Nginx-konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

- Observera att $proxy_host behövs istället för den vanliga $host på grund av mono.

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
# Tillåt API-extern åtkomst via NGINX
location ^~ /sonarr/api {
    auth_request      off;
    proxy_pass        http://127.0.0.1:8989;
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

Genom att lägga till denna rad inkluderas alla filer som slutar med `.conf` i Nginx-konfigurationen. Skapa en ny mapp som heter `subfolders-enabled` i samma mapp som din `nginx.conf`-fil finns. I den mappen skapar du en fil med ett igenkännligt namn som slutar med .conf. Lägg till konfigurationen ovan från filen och starta om eller ladda om Nginx. Du bör kunna besöka Sonarr på `yourdomain.tld/sonarr`. tld står för [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomän

Alternativt kan du använda en subdomän för Sonarr. I det här fallet skulle du besöka `sonarr.yourdomain.tld`. För detta måste du konfigurera en `A-record` eller `CNAME-record` i din DNS.
> Många gratis DNS-leverantörer stöder inte detta {.is-warning}

Som standard inkluderar Nginx mappen `sites-enabled`. Du kan kontrollera detta i `nginx.conf`, om inte kan du lägga till det med hjälp av [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Och riktigt viktigt, det måste vara inuti `http context`. Skapa nu en konfigurationsfil i mappen sites-enabled och ange följande konfiguration.

> För denna konfiguration rekommenderas det att ställa in baseurl till '' (tom). Denna konfiguration förutsätter att du använder standardporten `8989` och att Sonarr är åtkomlig på localhost (127.0.0.1). För denna konfiguration väljs subdomänen `sonarr` (rad 5). {.is-info}

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

Starta nu om Nginx och Sonarr bör vara tillgängligt på din valda subdomän.

## Apache

Detta bör läggas till inom en befintlig VirtualHost-webbplats. Om du vill använda roten för en domän eller subdomän, ta bort `sonarr` från `Location`-blocket och använd helt enkelt `/` som plats.

Observera: Ta inte bort baseurl från ProxyPass och ProxyPassReverse om du vill använda `/` som plats.

```none
<Location /sonarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8989/sonarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8989/sonarr
</Location>
```

`ProxyPreserveHost on` förhindrar att apache2 omdirigerar till localhost när du använder en omvänd proxy.

Eller för att skapa en hel VirtualHost för Sonarr:

```none
ProxyPass / http://127.0.0.1:8989/sonarr/
ProxyPassReverse / http://127.0.0.1:8989/sonarr/
```

Om du implementerar någon ytterligare autentisering genom Apache bör du exkludera följande sökvägar:

- `/sonarr/api/`
- `/sonarr/Content/`