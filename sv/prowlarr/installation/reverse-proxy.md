# Konfiguration av omvänd proxy

Exempel på konfigurationsinställningar för att konfigurera Prowlarr så att det kan nås via en omvänd proxy.

> Dessa exempel förutsätter att standardporten är `9696` och att du har ställt in en basurl på `prowlarr`. Det förutsätter också att din webbserver, t.ex. nginx, och Prowlarr körs på samma server och kan nås via `localhost`. Om så inte är fallet, använd värdens IP-adress eller en fullständig domännamn istället.
{.is-info}

## NGINX

Lägg till följande konfiguration i `nginx.conf` som finns i rotkatalogen för din Nginx-konfiguration. Kodblocket ska läggas till inuti `server context`. [Här finns ett fullständigt exempel på en typisk Nginx-konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Om du använder en icke-standard HTTP/HTTPS-serverport, se till att din Host-header också inkluderar den, t.ex.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Tillåt API/Indexer extern åtkomst via NGINX
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

Ett bättre sätt att organisera dina konfigurationsfiler för Nginx är att lagra konfigurationen för varje webbplats i en separat fil.
För att göra detta måste du ändra `nginx.conf` och lägga till `include subfolders-enabled/*.conf` i `server`-kontexten. Det kommer att se ut något liknande detta.

```nginx
server {
  listen 80;
  server_name _;
  
  # mer konfiguration
  
  include subfolders-enabled/*.conf
}
```

Genom att lägga till denna rad inkluderas alla filer som slutar med `.conf` i Nginx-konfigurationen. Skapa en ny mapp som heter `subfolders-enabled` i samma mapp som din `nginx.conf`-fil finns. I den mappen skapar du en fil med ett igenkännligt namn som slutar med .conf. Lägg till konfigurationen ovan från filen och starta om eller ladda om Nginx. Du bör kunna besöka Prowlarr på `yourdomain.tld/prowlarr`. tld står för [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomän

Alternativt kan du använda en subdomän för Prowlarr. I det fallet skulle du besöka `prowlarr.yourdomain.tld`. För detta måste du konfigurera en `A-record` eller `CNAME-record` i din DNS.
> Många gratis DNS-leverantörer stöder inte detta {.is-warning}
Som standard inkluderar Nginx mappen `sites-enabled`. Du kan kontrollera detta i `nginx.conf`, om det inte finns kan du lägga till det med hjälp av [include direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Och väldigt viktigt, det måste vara inuti `http context`. Skapa nu en konfigurationsfil i mappen sites-enabled och ange följande konfiguration.
> För denna konfiguration rekommenderas det att ställa in baseurl till '' (tom). Denna konfiguration förutsätter att du använder standardporten `7878` och att Prowlarr är tillgängligt på localhost (127.0.0.1). För denna konfiguration väljs subdomänen `prowlarr` (rad 5).
{.is-info}
> Om du använder en icke-standard HTTP/HTTPS-serverport, se till att din Host-header också inkluderar den, t.ex.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Starta nu om Nginx och Prowlarr bör vara tillgängligt på din valda subdomän.

## Apache

Detta bör läggas till inom en befintlig VirtualHost-webbplats. Om du vill använda rotkatalogen för en domän eller subdomän, ta bort `prowlarr` från `Location`-blocket och använd helt enkelt `/` som plats.

Observera: Ta inte bort baseurl från ProxyPass och ProxyPassReverse om du vill använda `/` som plats.

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on` förhindrar att apache2 omdirigerar till localhost när du använder en omvänd proxy.

Eller för att skapa en hel VirtualHost för Prowlarr:

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

Om du implementerar ytterligare autentisering genom Apache bör du exkludera följande sökvägar:

- `/prowlarr/api/`

### Användning av SSL på omvänd proxy

Om omvänd proxy gör SSL-avslutning (dvs. URL:en för att komma åt omvänd proxy använder protokollet `https://`), måste du tala om för Prowlarr att den ska använda `https://` för sina API-svar genom att ställa in `X-Forwarded-Proto` korrekt. Det vanliga sättet är att lägga till följande rader under konfigurationen för `ProxyPassReverse`:

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

Observera att denna konfiguration kräver att `mod_header`-modulen i Apache är aktiverad, vilket ofta inte är fallet som standard.