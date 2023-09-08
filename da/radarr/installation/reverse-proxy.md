# Konfiguration af omvendt proxy

Eksempler på konfigurationsfiler til at konfigurere Radarr, så den kan tilgås udefra gennem en omvendt proxy.

> Disse eksempler antager, at standardporten er `7878`, og at du har angivet en baseurl på `radarr`. Det antages også, at din webserver, f.eks. nginx, og Radarr kører på samme server og er tilgængelige på `localhost` (127.0.0.1). Hvis dette ikke er tilfældet, skal du i stedet bruge værts-IP-adressen eller værtsnavnet i proxy pass-direktivet.
{.is-info}

## NGINX

Tilføj følgende konfiguration til `nginx.conf`, som findes i roden af din Nginx-konfiguration. Kodeblokken skal tilføjes inde i `server context`. [Fuld eksempel på en typisk Nginx-konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Hvis du bruger en ikke-standard HTTP/HTTPS-serverport, skal du sørge for, at din Host-header også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Tillad ekstern adgang til API'en via NGINX
location ^~ /radarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:7878;
}
```

En bedre måde at organisere dine konfigurationsfiler til Nginx på ville være at gemme konfigurationen for hver side i en separat fil.
For at opnå dette skal du ændre `nginx.conf` og tilføje `include subfolders-enabled/*.conf` i `server`-konteksten. Så det vil se sådan ud.

```nginx
server {
  listen 80;
  server_name _;
  
  # mere konfiguration
  
  include subfolders-enabled/*.conf
}
```

Ved at tilføje denne linje inkluderes alle filer, der slutter med `.conf`, i Nginx-konfigurationen. Opret en ny mappe kaldet `subfolders-enabled` i samme mappe som din `nginx.conf`-fil er placeret. I den mappe skal du oprette en fil med et genkendeligt navn, der slutter med `.conf`. Tilføj konfigurationen fra ovenstående fil, og genstart eller genindlæs Nginx. Du bør nu kunne besøge Radarr på `yourdomain.tld/radarr`. tld står for [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomæne

Alternativt kan du bruge et subdomæne til Radarr. I dette tilfælde ville du besøge `radarr.yourdomain.tld`. For at gøre dette skal du konfigurere en `A-record` eller `CNAME-record` i din DNS.
> Mange gratis DNS-udbydere understøtter ikke dette {.is-warning}

Som standard inkluderer Nginx mappen `sites-enabled`. Du kan tjekke dette i `nginx.conf`. Hvis den ikke er der, kan du tilføje den ved hjælp af [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Og meget vigtigt, det skal være inden for `http`-konteksten. Opret nu en konfigurationsfil i mappen `sites-enabled` og indtast følgende konfiguration.

> For denne konfiguration anbefales det at indstille baseurl til '' (tom). Denne konfiguration antager, at du bruger standardporten `7878`, og at Radarr er tilgængelig på localhost (127.0.0.1). For denne konfiguration er subdomænet `radarr` valgt (linje 5). {.is-info}

> Hvis du bruger en ikke-standard HTTP/HTTPS-serverport, skal du sørge for, at din Host-header også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Genstart nu Nginx, og Radarr skal være tilgængelig på dit valgte subdomæne.

## Apache

Dette skal tilføjes inden for en eksisterende VirtualHost-site. Hvis du ønsker at bruge roden af et domæne eller subdomæne, skal du fjerne `radarr` fra `Location`-blokken og blot bruge `/` som placering.

Bemærk: Fjern ikke baseurl fra ProxyPass og ProxyPassReverse, hvis du vil bruge `/` som placering.

```none
<Location /radarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:7878/radarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:7878/radarr
</Location>
```

`ProxyPreserveHost on` forhindrer apache2 i at omdirigere til localhost, når der bruges en omvendt proxy.

Eller for at oprette en hel VirtualHost til Radarr:

```none
ProxyPass / http://127.0.0.1:7878/radarr/
ProxyPassReverse / http://127.0.0.1:7878/radarr/
```

Hvis du implementerer yderligere godkendelse gennem Apache, skal du udelukke følgende stier:

- `/radarr/api/`