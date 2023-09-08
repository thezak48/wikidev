# Reverse Proxy-konfiguration

Eksempler på konfigurationsfiler til at konfigurere Lidarr til at være tilgængelig gennem en reverse proxy.

> Disse eksempler antager standardporten `8686` og at du har angivet en baseurl på `lidarr`. Det antages også, at din webserver, f.eks. nginx, og Lidarr kører på samme server, der er tilgængelig på `localhost`. Hvis ikke, skal du i stedet bruge værts-IP-adressen eller en FQDN til proxy pass. {.is-info}

## NGINX

Tilføj følgende konfiguration til `nginx.conf`, der findes i roden af din Nginx-konfiguration. Kodeblokken skal tilføjes inde i `server context`. [Fuld eksempel på en typisk Nginx-konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Hvis du bruger en ikke-standard http/https-serverport, skal du sørge for, at din Host-header også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Tillad ekstern adgang til API'en via NGINX
location ~ /lidarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:8686;
}
```

En bedre måde at organisere dine konfigurationsfiler til Nginx ville være at gemme konfigurationen for hver side i en separat fil.
For at opnå dette er det nødvendigt at ændre `nginx.conf` og tilføje `include subfolders-enabled/*.conf` i `server`-konteksten. Så det vil se noget lignende ud.

```nginx
server {
  listen 80;
  server_name _;
  
  # mere konfiguration
  
  include subfolders-enabled/*.conf
}
```

Ved at tilføje denne linje inkluderes alle filer, der slutter med `.conf`, i Nginx-konfigurationen. Opret en ny mappe kaldet `subfolders-enabled` i samme mappe som din `nginx.conf`-fil er placeret. I den mappe opret en fil med et genkendeligt navn, der slutter med .conf. Tilføj konfigurationen fra ovenstående fil og genstart eller genindlæs Nginx. Du burde kunne besøge Lidarr på `yourdomain.tld/lidarr`. tld står for [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomæne

Alternativt kan du bruge et subdomæne til lidarr. I dette tilfælde ville du besøge `lidarr.yourdomain.tld`. For dette skal du konfigurere en `A-record` eller `CNAME-record` i din DNS.
> Mange gratis DNS-udbydere understøtter ikke dette {.is-warning}
Som standard inkluderer Nginx mappen `sites-enabled`. Du kan tjekke dette i `nginx.conf`, hvis det ikke er tilfældet, kan du tilføje det ved hjælp af [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Og meget vigtigt, det skal være inden for `http context`. Opret nu en konfigurationsfil i mappen sites-enabled og indtast følgende konfiguration.
> For denne konfiguration anbefales det at indstille baseurl til '' (tom). Denne konfiguration antager, at du bruger standardporten `8686` og at Lidarr er tilgængelig på localhost (127.0.0.1). For denne konfiguration er subdomænet `lidarr` valgt (linje 5). {.is-info}
> Hvis du bruger en ikke-standard http/https-serverport, skal du sørge for, at din Host-header også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Genstart nu Nginx, og Lidarr skulle være tilgængelig på dit valgte subdomæne.

## Apache

Dette skal tilføjes inden for en eksisterende VirtualHost-site. Hvis du ønsker at bruge roden af et domæne eller subdomæne, skal du fjerne `lidarr` fra `Location`-blokken og blot bruge `/` som placering.

Bemærk: Fjern ikke baseurl fra ProxyPass og ProxyPassReverse, hvis du ønsker at bruge `/` som placering.

```none
<Location /lidarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8686/lidarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8686/lidarr
</Location>
```

`ProxyPreserveHost on` forhindrer apache2 i at omdirigere til localhost, når der bruges en reverse proxy.

Eller for at oprette en hel VirtualHost til Lidarr:

```none
ProxyPass / http://127.0.0.1:8686/lidarr/
ProxyPassReverse / http://127.0.0.1:8686/lidarr/
```

Hvis du implementerer yderligere godkendelse gennem Apache, skal du udelukke følgende stier:

- `/lidarr/api/`