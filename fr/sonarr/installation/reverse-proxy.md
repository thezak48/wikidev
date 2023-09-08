# Configuration du proxy inverse

Exemples de configuration pour configurer Sonarr de manière à ce qu'il soit accessible depuis l'extérieur via un proxy inverse.

> Ces exemples supposent le port par défaut `8989` et que vous avez défini une baseurl `sonarr`. Ils supposent également que votre serveur web, par exemple Nginx, et Sonarr s'exécutent sur le même serveur accessible à `localhost` (127.0.0.1). Si ce n'est pas le cas, utilisez plutôt l'adresse IP de l'hôte ou le nom d'hôte pour la directive de proxy pass.
{.is-info}

## NGINX

Ajoutez la configuration suivante à `nginx.conf` situé à la racine de votre configuration Nginx. Le bloc de code doit être ajouté à l'intérieur du `contexte du serveur`. [Exemple complet d'une configuration Nginx typique](https://www.nginx.com/resources/wiki/start/topics/examples/full/)

- Notez que $proxy_host est nécessaire plutôt que le $host habituel en raison de mono.

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
# Autoriser l'accès externe à l'API via NGINX
location ^~ /sonarr/api {
    auth_request      off;
    proxy_pass        http://127.0.0.1:8989;
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

L'ajout de cette ligne inclura tous les fichiers se terminant par `.conf` dans la configuration de Nginx. Créez un nouveau répertoire appelé `subfolders-enabled` dans le même dossier que votre fichier `nginx.conf`. Dans ce dossier, créez un fichier avec un nom reconnaissable se terminant par .conf. Ajoutez la configuration ci-dessus à partir du fichier et redémarrez ou rechargez Nginx. Vous devriez pouvoir accéder à Sonarr à l'adresse `votredomaine.tld/sonarr`. tld est l'abréviation de [Domaine de premier niveau](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)

### Sous-domaine

Vous pouvez également utiliser un sous-domaine pour Sonarr. Dans ce cas, vous accéderiez à `sonarr.votredomaine.tld`. Pour cela, vous devez configurer un `enregistrement A` ou `enregistrement CNAME` dans votre DNS.
> De nombreux fournisseurs DNS gratuits ne prennent pas en charge cela {.is-warning}

Par défaut, Nginx inclut le dossier `sites-enabled`. Vous pouvez vérifier cela dans `nginx.conf`, sinon vous pouvez l'ajouter en utilisant la [directive include](http://nginx.org/en/docs/ngx_core_module.html#include). Et très important, il doit être à l'intérieur du `contexte http`. Créez maintenant un fichier de configuration à l'intérieur du dossier `sites-enabled` et entrez la configuration suivante.

> Pour cette configuration, il est recommandé de définir baseurl sur '' (vide). Cette configuration suppose que vous utilisez le port `8989` par défaut et que Sonarr est accessible sur localhost (127.0.0.1). Pour cette configuration, le sous-domaine `sonarr` est choisi (ligne 5). {.is-info}

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

Redémarrez maintenant Nginx et Sonarr devrait être disponible à votre sous-domaine sélectionné.

## Apache

Cela doit être ajouté à l'intérieur d'un site VirtualHost existant. Si vous souhaitez utiliser la racine d'un domaine ou d'un sous-domaine, supprimez `sonarr` du bloc `Location` et utilisez simplement `/` comme emplacement.

Remarque : Ne supprimez pas la baseurl de ProxyPass et ProxyPassReverse si vous souhaitez utiliser `/` comme emplacement.

```none
<Location /sonarr>
  ProxyPreserveHost on
    ProxyPass http://127.0.0.1:8989/sonarr connectiontimeout=5 timeout=300
    ProxyPassReverse http://127.0.0.1:8989/sonarr
</Location>
```

`ProxyPreserveHost on` empêche apache2 de rediriger vers localhost lors de l'utilisation d'un proxy inverse.

Ou pour créer un VirtualHost complet pour Sonarr :

```none
ProxyPass / http://127.0.0.1:8989/sonarr/
ProxyPassReverse / http://127.0.0.1:8989/sonarr/
```

Si vous mettez en place une authentification supplémentaire via Apache, vous devez exclure les chemins suivants :

- `/sonarr/api/`
- `/sonarr/Content/`