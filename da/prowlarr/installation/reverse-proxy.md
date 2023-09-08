# Konfiguration af omvendt proxy

Eksempler på konfigurationsfiler til at konfigurere Prowlarr til at være tilgængelig gennem en omvendt proxy.

> Disse eksempler antager standardporten `9696` og at du har angivet en baseurl på `prowlarr`. Det antages også, at din webserver, f.eks. nginx, og Prowlarr kører på samme server og er tilgængelige på `localhost`. Hvis ikke, skal du i stedet bruge værts-IP-adressen eller et FQDN.
{.is-info}

## NGINX

Tilføj følgende konfiguration til `nginx.conf`, som findes i roden af din Nginx-konfiguration. Kodeblokken skal tilføjes inden for `server-konteksten`. [Fuld eksempel på en typisk Nginx-konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Hvis du bruger en ikke-standard http/https-serverport, skal du sørge for, at din Host-header også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Tillad ekstern adgang til API/Indexer via NGINX
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

En bedre måde at organisere dine konfigurationsfiler til Nginx ville være at gemme konfigurationen for hver side i en separat fil.
For at opnå dette er det nødvendigt at ændre `nginx.conf` og tilføje `include subfolders-enabled/*.conf` i `server`-konteksten. Så det vil se noget ud som dette.

```nginx
server {
  listen 80;
  server_name _;
  
  # mere konfiguration
  
  include subfolders-enabled/*.conf
}
```

Ved at tilføje denne linje inkluderes alle filer, der slutter med `.conf`, i Nginx-konfigurationen. Opret en ny mappe kaldet `subfolders-enabled` i samme mappe som din `nginx.conf`-fil er placeret. I den mappe opret en fil med et genkendeligt navn, der slutter med .conf. Tilføj konfigurationen fra ovenstående fil og genstart eller genindlæs Nginx. Du bør kunne besøge Prowlarr på `yourdomain.tld/radarr`. tld står for [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomæne

Alternativt kan du bruge et subdomæne til Prowlarr. I så fald skal du besøge `radarr.yourdomain.tld`. For at gøre dette skal du konfigurere en `A-record` eller `CNAME-record` i din DNS.
> Mange gratis DNS-udbydere understøtter ikke dette {.is-warning}
Som standard inkluderer Nginx mappen `sites-enabled`. Du kan kontrollere dette i `nginx.conf`. Hvis den ikke er der, kan du tilføje den ved hjælp af [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Og meget vigtigt, det skal være inden for `http-konteksten`. Opret nu en konfigurationsfil i mappen sites-enabled og indtast følgende konfiguration.
> For denne konfiguration anbefales det at indstille baseurl til '' (tom). Denne konfiguration antager, at du bruger standardporten `7878` og at Prowlarr er tilgængelig på localhost (127.0.0.1). For denne konfiguration er subdomænet `radarr` valgt (linje 5).
{.is-info}
> Hvis du bruger en ikke-standard http/https-serverport, skal du sørge for, at din Host-header også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Genstart nu Nginx, og Prowlarr skulle være tilgængelig på dit valgte subdomæne.

## Apache

Dette skal tilføjes inden for en eksisterende VirtualHost-site. Hvis du ønsker at bruge roden af et domæne eller subdomæne, skal du fjerne `prowlarr` fra `Location`-blokken og blot bruge `/` som placering.

Bemærk: Fjern ikke baseurl fra ProxyPass og ProxyPassReverse, hvis du vil bruge `/` som placering.

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on` forhindrer apache2 i at omdirigere til localhost, når der bruges en omvendt proxy.

Eller for at oprette en hel VirtualHost til Prowlarr:

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

Hvis du implementerer yderligere godkendelse gennem Apache, skal du udelade følgende stier:

- `/prowlarr/api/`

### Brug af SSL på omvendt proxy

Hvis omvendt proxy udfører SSL-terminering (dvs. URL'en til at få adgang til omvendt proxy bruger protokollen `https://`), skal du fortælle Prowlarr, at den skal bruge `https://` for sine API-responser ved at indstille `X-Forwarded-Proto` korrekt. Den almindelige måde er at tilføje følgende linjer under konfigurationen for `ProxyPassReverse`:

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

Bemærk, at denne konfiguration kræver aktivering af Apache-modulet `mod_header`, som ofte ikke er aktiveret som standard.