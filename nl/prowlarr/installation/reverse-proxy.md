# Reverse Proxy Configuratie

Voorbeeldconfiguraties voor het configureren van Prowlarr om toegankelijk te zijn via een reverse proxy.

> Deze voorbeelden gaan uit van de standaardpoort `9696` en dat je een basis-URL van `prowlarr` hebt ingesteld. Het gaat er ook vanuit dat je webserver, bijvoorbeeld nginx, en Prowlarr op dezelfde server draaien en toegankelijk zijn op `localhost`. Als dit niet het geval is, gebruik dan het IP-adres van de host of een FQDN.
{.is-info}

## NGINX

Voeg de volgende configuratie toe aan `nginx.conf`, dat zich bevindt in de hoofdmap van je Nginx-configuratie. Het codeblok moet worden toegevoegd binnen de `server-context`. [Volledig voorbeeld van een typische Nginx-configuratie](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Als je een niet-standaard http/https serverpoort gebruikt, zorg er dan voor dat je Host-header deze ook bevat, bijvoorbeeld: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Sta externe toegang tot de API/Indexer toe via NGINX
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

Een betere manier om je configuratiebestanden voor Nginx te organiseren, is door de configuratie voor elke site in een apart bestand op te slaan.
Om dit te bereiken, moet je `nginx.conf` aanpassen en `include subfolders-enabled/*.conf` toevoegen in de `server-context`. Het zal er dan ongeveer zo uitzien.

```nginx
server {
  listen 80;
  server_name _;
  
  # meer configuratie
  
  include subfolders-enabled/*.conf
}
```

Door deze regel toe te voegen, worden alle bestanden met de extensie `.conf` opgenomen in de Nginx-configuratie. Maak een nieuwe map genaamd `subfolders-enabled` in dezelfde map als waar je `nginx.conf`-bestand zich bevindt. Maak in die map een bestand met een herkenbare naam dat eindigt op .conf. Voeg de configuratie van hierboven toe aan het bestand en herstart of herlaad Nginx. Je zou Prowlarr moeten kunnen bezoeken op `joudomein.tld/prowlarr`. tld staat voor [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomein

Je kunt ook een subdomein gebruiken voor Prowlarr. In dat geval zou je `prowlarr.joudomein.tld` bezoeken. Hiervoor moet je een `A-record` of `CNAME-record` configureren in je DNS.
> Veel gratis DNS-providers ondersteunen dit niet {.is-warning}
Standaard bevat Nginx de map `sites-enabled`. Je kunt dit controleren in `nginx.conf`, als dit niet het geval is, kun je het toevoegen met behulp van de [include directive](http://nginx.org/en/docs/ngx_core_module.html#include). En heel belangrijk, het moet zich binnen de `http-context` bevinden. Maak nu een configuratiebestand aan in de map sites-enabled en voeg de volgende configuratie toe.
> Voor deze configuratie wordt aanbevolen om baseurl in te stellen op '' (leeg). Deze configuratie gaat ervan uit dat je de standaard `7878` gebruikt en dat Prowlarr toegankelijk is op localhost (127.0.0.1). Voor deze configuratie is het subdomein `prowlarr` gekozen (regel 5).
{.is-info}
> Als je een niet-standaard http/https serverpoort gebruikt, zorg er dan voor dat je Host-header deze ook bevat, bijvoorbeeld: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Herstart nu Nginx en Prowlarr zou beschikbaar moeten zijn op je geselecteerde subdomein.

## Apache

Dit moet worden toegevoegd aan een bestaande VirtualHost-site. Als je de root van een domein of subdomein wilt gebruiken, verwijder dan `prowlarr` uit het `Location`-blok en gebruik gewoon `/` als de locatie.

Opmerking: Verwijder de baseurl niet uit ProxyPass en ProxyPassReverse als je `/` als de locatie wilt gebruiken.

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on` voorkomt dat apache2 doorverwijst naar localhost bij het gebruik van een reverse proxy.

Of maak een volledige VirtualHost voor Prowlarr:

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

Als je extra authenticatie implementeert via Apache, moet je de volgende paden uitsluiten:

- `/prowlarr/api/`

### SSL gebruiken op de reverse proxy

Als de reverse proxy SSL-terminatie uitvoert (d.w.z. de URL om toegang te krijgen tot de reverse proxy gebruikt het `https://`-protocol), moet je Prowlarr vertellen dat het `https://` moet gebruiken voor zijn API-responses door de `X-Forwarded-Proto` correct in te stellen. De gebruikelijke manier is om de volgende regels toe te voegen onder de `ProxyPassReverse`-configuratie:

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

Merk op dat deze configuratie vereist dat de `mod_header` Apache-module is ingeschakeld, wat vaak niet standaard is ingeschakeld.