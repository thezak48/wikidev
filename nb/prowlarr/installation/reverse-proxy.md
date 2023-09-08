# Konfigurasjon av omvendt proxy

Eksempler på konfigurasjon for å gjøre Prowlarr tilgjengelig gjennom en omvendt proxy.

> Disse eksemplene antar at standardporten er `9696` og at du har satt en baseurl på `prowlarr`. Det antas også at webserveren din, for eksempel nginx, og Prowlarr kjører på samme server og er tilgjengelig på `localhost`. Hvis ikke, bruk verts-IP-adressen eller en fullt kvalifisert domenenavn i stedet.
{.is-info}

## NGINX

Legg til følgende konfigurasjon i `nginx.conf`-filen som ligger i rotmappen til Nginx-konfigurasjonen din. Kodeblokken skal legges til inne i `server`-konteksten. [Fullstendig eksempel på en typisk Nginx-konfigurasjon](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Hvis du bruker en ikke-standard http/https-serverport, må du sørge for at vertshodet også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Tillat ekstern tilgang til API/Indexer via NGINX
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

En bedre måte å organisere konfigurasjonsfilene dine for Nginx på er å lagre konfigurasjonen for hver side i en separat fil.
For å oppnå dette må du endre `nginx.conf` og legge til `include subfolders-enabled/*.conf` i `server`-konteksten. Så det vil se noe slik ut.

```nginx
server {
  listen 80;
  server_name _;
  
  # mer konfigurasjon
  
  include subfolders-enabled/*.conf
}
```

Ved å legge til denne linjen vil alle filer som slutter på `.conf` bli inkludert i Nginx-konfigurasjonen. Opprett en ny mappe kalt `subfolders-enabled` i samme mappe som `nginx.conf`-filen din er plassert. I den mappen opprett en fil med et gjenkjennelig navn som slutter med .conf. Legg til konfigurasjonen fra ovenstående fil og start eller last inn Nginx på nytt. Du bør kunne besøke Prowlarr på `yourdomain.tld/radarr`. tld står for [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomene

Alternativt kan du bruke et subdomene for Prowlarr. I så fall vil du besøke `radarr.yourdomain.tld`. For dette må du konfigurere en `A-record` eller `CNAME-record` i DNS-en din.
> Mange gratis DNS-leverandører støtter ikke dette {.is-warning}
Som standard inkluderer Nginx mappen `sites-enabled`. Du kan sjekke dette i `nginx.conf`, hvis ikke kan du legge det til ved å bruke [include-direktivet](http://nginx.org/en/docs/ngx_core_module.html#include). Og veldig viktig, det må være inni `http`-konteksten. Opprett nå en konfigurasjonsfil inne i mappen `sites-enabled` og legg til følgende konfigurasjon.
> For denne konfigurasjonen anbefales det å sette baseurl til '' (tom). Denne konfigurasjonen antar at du bruker standardporten `7878` og at Radarr er tilgjengelig på localhost (127.0.0.1). For denne konfigurasjonen er subdomenet `radarr` valgt (linje 5).
{.is-info}
> Hvis du bruker en ikke-standard http/https-serverport, må du sørge for at vertshodet også inkluderer den, f.eks.: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Start nå Nginx på nytt, og Prowlarr skal være tilgjengelig på ditt valgte subdomene.

## Apache

Dette bør legges til i en eksisterende VirtualHost-side. Hvis du ønsker å bruke roten til et domene eller subdomene, fjern `prowlarr` fra `Location`-blokken og bruk bare `/` som plassering.

Merk: Ikke fjern baseurl fra ProxyPass og ProxyPassReverse hvis du vil bruke `/` som plassering.

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on` forhindrer apache2 i å omdirigere til localhost når du bruker en omvendt proxy.

Eller for å lage en hel VirtualHost for Prowlarr:

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

Hvis du implementerer ekstra autentisering gjennom Apache, bør du ekskludere følgende stier:

- `/prowlarr/api/`

### Bruk av SSL på omvendt proxy

Hvis omvendt proxy utfører SSL-terminering (dvs. URL-en for å få tilgang til omvendt proxy bruker protokollen `https://`), må du fortelle Prowlarr at den skal bruke `https://` for API-responsene sine ved å sette `X-Forwarded-Proto` riktig. Vanlig praksis er å legge til følgende linjer under konfigurasjonen for `ProxyPassReverse`:

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

Merk at denne konfigurasjonen krever at `mod_header`-modulen i Apache er aktivert, noe som ofte ikke er aktivert som standard.