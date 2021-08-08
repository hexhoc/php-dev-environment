# php-dev-environment

The build consists of the following components:
1. NGINX
2. MySql
3. PHP

Setting Up a Modern PHP Development Environment:
1. NGINX
Create folders structure for logs, config and sites. and mount volumes in this folders.
Place file with config for virtual host in "./config/nginx/" folder

We could just serve files from the /sites (which is /var/www in container) directory, but it’s good practice to keep most PHP files out of the publicly accessible directory. As PHP scripts will need to load files using ../, we’ll put our public directory one level down.

2. PHP
There’s a new service, php, which is using the image php:fpm-latest. For NGINX, you’ll need to use an fpm (FastCGI Process Manager) package.

Because PHP will need to access your .php files from the /var/www directory, you’ll need to mount the volume in the PHP image in the same way you did for the NGINX image. PHP doesn’t need access to the nginx.conf configuration file, so there’s no need to give it access to it.

The app folder is now accessible on the host machine, and in the nginx and php containers.

We extend out php build, and create php.dockerfile in the same folder as your docker-compose.yml and add the following:
docker-php-ext-install pdo pdo_mysql 
pecl install xdebug 
docker-php-ext-enable xdebug


