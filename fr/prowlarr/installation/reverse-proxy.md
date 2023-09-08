# Configuration du proxy inverse

Exemples de configuration pour configurer Prowlarr afin qu'il soit accessible via un proxy inverse.

> Ces exemples supposent le port par défaut `9696` et que vous avez défini une baseurl `prowlarr`. Ils supposent également que votre serveur web, par exemple Nginx, et Prowlarr s'exécutent sur le même serveur accessible à `localhost`. Si ce n'est pas le cas, utilisez l'adresse IP de l'hôte ou un FQDN à la place.
{.is-info}

## NGINX

Ajoutez la configuration suivante à `nginx.conf` situé à la racine de votre configuration Nginx. Le bloc de code doit être ajouté à l'intérieur du `contexte du serveur`. [Exemple complet d'une configuration Nginx typique](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

> Si vous utilisez un port de serveur http/https non standard, assurez-vous que votre en-tête Host l'inclut également, par exemple : `proxy_set_header Host $host:$server_port` {.is-warning}

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
# Autoriser l'accès externe à l'API/Indexer via NGINX
location ^~ /prowlarr(/[0-9]+)?/api {
    auth_basic off;
    proxy_pass http://127.0.0.1:9696;
}
```

Une meilleure façon d'organiser vos fichiers de configuration pour Nginx serait de stocker la configuration de chaque site dans un fichier séparé.
Pour cela, il est nécessaire de modifier `nginx.conf` et d'ajouter `include subfolders-enabled/*.conf` dans le `contexte du serveur`. Cela ressemblera à quelque chose comme ceci.

```nginx
server {
  listen 80;
  server_name _;
  
  # plus de configuration
  
  include subfolders-enabled/*.conf
}
```

L'ajout de cette ligne inclura tous les fichiers se terminant par `.conf` dans la configuration de Nginx. Créez un nouveau répertoire appelé `subfolders-enabled` dans le même dossier que votre fichier `nginx.conf`. Dans ce dossier, créez un fichier avec un nom reconnaissable se terminant par .conf. Ajoutez la configuration ci-dessus à partir du fichier et redémarrez ou rechargez Nginx. Vous devriez pouvoir accéder à Prowlarr à l'adresse `votredomaine.tld/prowlarr`. tld est l'abréviation de [Domaine de premier niveau](https://fr.wikipedia.org/wiki/Liste_des_domaines_de_premier_niveau_Internet)

### Sous-domaine

Vous pouvez également utiliser un sous-domaine pour Prowlarr. Dans ce cas, vous accéderiez à `prowlarr.votredomaine.tld`. Pour cela, vous devrez configurer un `enregistrement A` ou un `enregistrement CNAME` dans votre DNS.
> De nombreux fournisseurs DNS gratuits ne prennent pas en charge cela {.is-warning}
Par défaut, Nginx inclut le dossier `sites-enabled`. Vous pouvez vérifier cela dans `nginx.conf`, sinon vous pouvez l'ajouter en utilisant la [directive include](http://nginx.org/en/docs/ngx_core_module.html#include). Et très important, cela doit être à l'intérieur du `contexte http`. Créez maintenant un fichier de configuration à l'intérieur du dossier `sites-enabled` et entrez la configuration suivante.
> Pour cette configuration, il est recommandé de définir baseurl sur '' (vide). Cette configuration suppose que vous utilisez le port par défaut `7878` et que Radarr est accessible sur localhost (127.0.0.1). Pour cette configuration, le sous-domaine `radarr` est choisi (ligne 5).
{.is-info}
> Si vous utilisez un port de serveur http/https non standard, assurez-vous que votre en-tête Host l'inclut également, par exemple : `proxy_set_header Host $host:$server_port` {.is-warning}

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

Redémarrez maintenant Nginx et Prowlarr devrait être disponible à votre sous-domaine sélectionné.

## Apache

Cela doit être ajouté à l'intérieur d'un site VirtualHost existant. Si vous souhaitez utiliser la racine d'un domaine ou d'un sous-domaine, supprimez `prowlarr` du bloc `Location` et utilisez simplement `/` comme emplacement.

Remarque : Ne supprimez pas la baseurl de ProxyPass et ProxyPassReverse si vous souhaitez utiliser `/` comme emplacement.

```none
<Location /prowlarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:9696/prowlarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:9696/prowlarr
</Location>
```

`ProxyPreserveHost on` empêche apache2 de rediriger vers localhost lors de l'utilisation d'un proxy inverse.

Ou pour créer un VirtualHost complet pour Prowlarr :

```none
ProxyPass / http://127.0.0.1:9696/prowlarr/
ProxyPassReverse / http://127.0.0.1:9696/prowlarr/
```

Si vous mettez en place une authentification supplémentaire via Apache, vous devez exclure les chemins suivants :

- `/prowlarr/api/`

### Utilisation de SSL sur le proxy inverse

Si le proxy inverse effectue une terminaison SSL (c'est-à-dire que l'URL d'accès au proxy inverse utilise le protocole `https://`), vous devez indiquer à Prowlarr qu'il doit utiliser `https://` pour ses réponses d'API en définissant correctement `X-Forwarded-Proto`. La méthode courante consiste à ajouter les lignes suivantes sous la configuration `ProxyPassReverse` :

```none
RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
RequestHeader set "X-Forwarded-SSL" expr=%{HTTPS}
```

Notez que cette configuration nécessite l'activation du module Apache `mod_header`, qui n'est souvent pas activé par défaut.