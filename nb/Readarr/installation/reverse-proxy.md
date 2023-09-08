# Konfigurasjon av omvendt proxy

Eksempler på konfigurasjon for å gjøre Readarr tilgjengelig fra utsiden ved hjelp av en omvendt proxy.

> Disse eksemplene antar at standardporten er `8787` og at du har satt en baseurl til `readarr`. Det antas også at webserveren din, for eksempel nginx, og Readarr kjører på samme server og er tilgjengelig på `localhost` (127.0.0.1). Hvis ikke, bruk IP-adressen eller vertsnavnet til serveren i stedet for proxy pass-direktivet.
{.is-info}

## NGINX

Legg til følgende konfigurasjon i `nginx.conf`-filen som ligger i rotmappen til Nginx-konfigurasjonen din. Kodeblokken skal legges til inne i `server`-konteksten. [Fullstendig eksempel på en typisk Nginx-konfigurasjon](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Hvis du bruker en ikke-standard http/https-port, må du også sørge for at vertshodet inkluderer denne, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
location ^~ /readarr {
    proxy_pass http://127.0.0.1:8787;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_redirect off;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $http_connection;
}
# Tillat ekstern tilgang til API-en via NGINX
location ^~ /readarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:8787;
}
```

En bedre måte å organisere konfigurasjonsfilene dine for Nginx på er å lagre konfigurasjonen for hver side i en separat fil.
For å oppnå dette må du endre `nginx.conf` og legge til `include subfolders-enabled/*.conf` i `server`-konteksten. Det vil se omtrent slik ut:

```nginx
server {
  listen 80;
  server_name _;
  
  # mer konfigurasjon
  
  include subfolders-enabled/*.conf
}
```

Ved å legge til denne linjen vil alle filer som slutter på `.conf` bli inkludert i Nginx-konfigurasjonen. Opprett en ny mappe med navnet `subfolders-enabled` i samme mappe som `nginx.conf`-filen din befinner seg. I den mappen opprett en fil med et gjenkjennelig navn som slutter på `.conf`. Legg til konfigurasjonen fra ovenstående fil og start eller last inn Nginx på nytt. Du bør nå kunne besøke Readarr på `yourdomain.tld/readarr`. `tld` står for [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomene

Alternativt kan du bruke et subdomene for Readarr. I så fall vil du besøke `readarr.yourdomain.tld`. For å oppnå dette må du konfigurere en `A-record` eller `CNAME-record` i DNS-en din.
> Mange gratis DNS-leverandører støtter ikke dette {.is-warning}

Som standard inkluderer Nginx mappen `sites-enabled`. Du kan sjekke dette i `nginx.conf`. Hvis den ikke er der, kan du legge den til ved hjelp av [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Og veldig viktig, den må være inne i `http`-konteksten. Opprett nå en konfigurasjonsfil inne i `sites-enabled`-mappen og legg til følgende konfigurasjon.

> For denne konfigurasjonen anbefales det å sette baseurl til '' (tom). Denne konfigurasjonen antar at du bruker standardporten `8787` og at Readarr er tilgjengelig på localhost (127.0.0.1). For denne konfigurasjonen er subdomenet `readarr` valgt (linje 5). {.is-info}

> Hvis du bruker en ikke-standard http/https-port, må du også sørge for at vertshodet inkluderer denne, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

```nginx
server {
  listen      80;
  listen [::]:80;

  server_name readarr.*;

  location / {
    proxy_set_header   Host $host;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Host $host;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection $http_connection;

    proxy_redirect     off;
    proxy_http_version 1.1;
    
    proxy_pass http://127.0.0.1:8787;
  }
}
```

Start Nginx på nytt og Readarr skal nå være tilgjengelig på ditt valgte subdomene.

## Apache

Dette bør legges til innenfor en eksisterende VirtualHost-nettside. Hvis du ønsker å bruke roten til et domene eller subdomene, fjern `readarr` fra `Location`-blokken og bruk bare `/` som plassering.

Merk: Ikke fjern baseurl fra ProxyPass og ProxyPassReverse hvis du ønsker å bruke `/` som plassering.

```none
<Location /readarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8787/readarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8787/readarr
</Location>
```

`ProxyPreserveHost on` forhindrer apache2 i å omdirigere til localhost når du bruker en omvendt proxy.

Eller for å opprette en hel VirtualHost for Readarr:

```none
ProxyPass / http://127.0.0.1:8787/readarr/
ProxyPassReverse / http://127.0.0.1:8787/readarr/
```

Hvis du implementerer ekstra autentisering gjennom Apache, bør du ekskludere følgende stier:

- `/readarr/api/`