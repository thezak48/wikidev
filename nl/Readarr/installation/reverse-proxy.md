# Reverse Proxy Configuratie

Voorbeeldconfiguraties voor het configureren van Readarr om toegankelijk te zijn vanaf de buitenwereld via een reverse proxy.

> Deze voorbeelden gaan uit van de standaardpoort `8787` en dat je een basis-URL van `readarr` hebt ingesteld. Het gaat er ook vanuit dat je webserver, bijvoorbeeld nginx, en Readarr op dezelfde server draaien en toegankelijk zijn op `localhost` (127.0.0.1). Gebruik anders het IP-adres of de hostnaam van de host in plaats daarvan voor de proxy-doorstuurinstructie.
{.is-info}

## NGINX

Voeg de volgende configuratie toe aan `nginx.conf`, dat zich bevindt in de hoofdmap van je Nginx-configuratie. De codeblok moet worden toegevoegd binnen de `server context`. [Volledig voorbeeld van een typische Nginx-configuratie](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Als je een niet-standaard http/https-serverpoort gebruikt, zorg er dan voor dat je Host-header deze ook bevat, bijvoorbeeld: `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Sta externe toegang tot de API toe via NGINX
location ^~ /readarr/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:8787;
}
```

Een betere manier om je configuratiebestanden voor Nginx te organiseren, is door de configuratie voor elke site in een apart bestand op te slaan.
Om dit te bereiken, moet je `nginx.conf` aanpassen en `include subfolders-enabled/*.conf` toevoegen binnen de `server` context. Het zal er dan ongeveer zo uitzien.

```nginx
server {
  listen 80;
  server_name _;
  
  # meer configuratie
  
  include subfolders-enabled/*.conf
}
```

Door deze regel toe te voegen, worden alle bestanden met de extensie `.conf` opgenomen in de Nginx-configuratie. Maak een nieuwe map genaamd `subfolders-enabled` in dezelfde map als waar je `nginx.conf`-bestand zich bevindt. Maak in die map een bestand met een herkenbare naam dat eindigt op .conf. Voeg de configuratie van hierboven toe aan het bestand en herstart of herlaad Nginx. Je zou Readarr moeten kunnen bezoeken op `joudomein.tld/readarr`. tld staat voor [Top Level Domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Subdomein

Je kunt ook een subdomein gebruiken voor Readarr. In dat geval zou je `readarr.joudomein.tld` bezoeken. Hiervoor moet je een `A-record` of `CNAME-record` configureren in je DNS.
> Veel gratis DNS-providers ondersteunen dit niet {.is-warning}

Standaard bevat Nginx de map `sites-enabled`. Je kunt dit controleren in `nginx.conf`. Als dit niet het geval is, kun je het toevoegen met behulp van de [include directive](http://nginx.org/en/docs/ngx_core_module.html#include). En heel belangrijk, het moet binnen de `http context` staan. Maak nu een configuratiebestand aan in de map sites-enabled en voeg de volgende configuratie toe.

> Voor deze configuratie wordt aanbevolen om baseurl in te stellen op '' (leeg). Deze configuratie gaat ervan uit dat je de standaard `8787` gebruikt en dat Readarr toegankelijk is op localhost (127.0.0.1). Voor deze configuratie is het subdomein `readarr` gekozen (regel 5). {.is-info}

> Als je een niet-standaard http/https-serverpoort gebruikt, zorg er dan voor dat je Host-header deze ook bevat, bijvoorbeeld: `proxy_set_header Host $host:$server_port` {.is-warning}

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

Herstart nu Nginx en Readarr zou beschikbaar moeten zijn op je geselecteerde subdomein.

## Apache

Dit moet worden toegevoegd aan een bestaande VirtualHost-site. Als je de root van een domein of subdomein wilt gebruiken, verwijder dan `readarr` uit het `Location`-blok en gebruik gewoon `/` als de locatie.

Opmerking: Verwijder de baseurl niet uit ProxyPass en ProxyPassReverse als je `/` als de locatie wilt gebruiken.

```none
<Location /readarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8787/readarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8787/readarr
</Location>
```

`ProxyPreserveHost on` voorkomt dat apache2 doorverwijst naar localhost bij gebruik van een reverse proxy.

Of maak een volledige VirtualHost voor Readarr:

```none
ProxyPass / http://127.0.0.1:8787/readarr/
ProxyPassReverse / http://127.0.0.1:8787/readarr/
```

Als je extra authenticatie implementeert via Apache, moet je de volgende paden uitsluiten:

- `/readarr/api/`