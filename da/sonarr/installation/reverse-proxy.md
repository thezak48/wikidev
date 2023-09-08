# Konfiguration af omvendt proxy

Eksempler på konfigurationsfiler til at konfigurere Sonarr til at være tilgængelig fra omverdenen gennem en omvendt proxy.

> Disse eksempler antager standardporten `8989` og at du har angivet en baseurl på `sonarr`. Det antages også, at din webserver, f.eks. nginx, og Sonarr kører på samme server og er tilgængelige på `localhost` (127.0.0.1). Hvis ikke, skal du i stedet bruge værts-IP-adressen eller værtsnavnet til proxy pass-direktivet.
{.is-info}

## NGINX

Tilføj følgende konfiguration til `nginx.conf`, som er placeret i roden af din Nginx-konfiguration. Kodeblokken skal tilføjes inde i `server-context`. [Fuld eksempel på en typisk Nginx-konfiguration](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

- Bemærk, at `$proxy_host` er nødvendig i stedet for den typiske `$host` på grund af mono.

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
# Tillad ekstern adgang til API'en via NGINX
location ^~ /sonarr/api {
    auth_request      off;
    proxy_pass        http://127.0.0.1:8989;
}

```

En bedre måde at organisere dine konfigurationsfiler til Nginx på ville være at gemme konfigurationen for hver side i en separat fil.
For at opnå dette er det nødvendigt at ændre `nginx.conf` og tilføje `include subfolders-enabled/*.conf` i `server`-konteksten. Så det vil se noget lignende ud.

```nginx
server {
  listen 80;
  server_name _;
  
  # mere konfiguration
  
  include subfolders-enabled/*.conf
}
```

Ved at tilføje denne linje inkluderes alle filer, der slutter med `.conf`, i Nginx-konfigurationen. Opret en ny mappe kaldet `subfolders-enabled` i samme mappe som din `nginx.conf`-fil er placeret. I den mappe skal du oprette en fil med et genkendeligt navn, der slutter med `.conf`. Tilføj konfigurationen fra ovenstående fil og genstart eller genindlæs Nginx. Du burde kunne besøge Sonarr på `ditdomæne.tld/sonarr`. "tld" står for [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomæne

Alternativt kan du bruge et subdomæne til Sonarr. I dette tilfælde vil du besøge `sonarr.ditdomæne.tld`. For dette skal du konfigurere en `A-record` eller `CNAME-record` i din DNS.
> Mange gratis DNS-udbydere understøtter ikke dette {.is-warning}

Som standard inkluderer Nginx mappen `sites-enabled`. Du kan tjekke dette i `nginx.conf`. Hvis det ikke er tilfældet, kan du tilføje det ved hjælp af [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Og meget vigtigt, det skal være inden for `http-konteksten`. Opret nu en konfigurationsfil i mappen `sites-enabled` og indtast følgende konfiguration.

> For denne konfiguration anbefales det at indstille baseurl til '' (tom). Denne konfiguration antager, at du bruger standardporten `8989` og at Sonarr er tilgængelig på localhost (127.0.0.1). For denne konfiguration er subdomænet `sonarr` valgt (linje 5). {.is-info}

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

Genstart nu Nginx, og Sonarr burde være tilgængelig på dit valgte subdomæne.

## Apache

Dette skal tilføjes inden for en eksisterende VirtualHost-site. Hvis du ønsker at bruge roden af et domæne eller subdomæne, skal du fjerne `sonarr` fra `Location`-blokken og blot bruge `/` som placering.

Bemærk: Fjern ikke baseurl fra ProxyPass og ProxyPassReverse, hvis du ønsker at bruge `/` som placering.

```none
<Location /sonarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8989/sonarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8989/sonarr
</Location>
```

`ProxyPreserveHost on` forhindrer apache2 i at omdirigere til localhost, når der bruges en omvendt proxy.

Eller for at oprette en hel VirtualHost til Sonarr:

```none
ProxyPass / http://127.0.0.1:8989/sonarr/
ProxyPassReverse / http://127.0.0.1:8989/sonarr/
```

Hvis du implementerer yderligere godkendelse gennem Apache, skal du udelukke følgende stier:

- `/sonarr/api/`
- `/sonarr/Content/`