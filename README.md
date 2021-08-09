# php-dev-environment

This is simple docker build for deploying php development environment

The build consists of the following components:
1. NGINX
2. PHP (with xdebug and error report)
3. MySql

## **Installation:**
1. Go to the root of this project folder
2. Type in the terminal -> docker-compose up

Setting Up a Modern PHP Development Environment:

## **1. NGINX**
Create folders structure for logs, config and sites. and mount volumes in this folders.
Place file with config for virtual host in "./config/nginx/" folder

We could just serve files from the /sites (which is /var/www in container) directory, but it’s good practice to keep most PHP files out of the publicly accessible directory. As PHP scripts will need to load files using ../, we’ll put our public directory one level down.

## **2. PHP**
There’s a new service, php, which is using the image php:fpm-latest. For NGINX, you’ll need to use an fpm (FastCGI Process Manager) package.

Because PHP will need to access your .php files from the /var/www directory, you’ll need to mount the volume in the PHP image in the same way you did for the NGINX image. PHP doesn’t need access to the nginx.conf configuration file, so there’s no need to give it access to it.

The app folder is now accessible on the host machine, and in the nginx and php containers.

## **3. MySql**
This time there’s an environment block, which is used to pass some variables to the container when it’s created. These are used to configure the database with the following options. Set your own values for the following variables:

**MYSQL_ROOT_PASSWORD**: the root password for the database. You can use this to log in as root and manage the database.

**MYSQL_USER** and **MYSQL_PASSWORD**: the name and password for a MySQL user that gets created with limited permissions. You’ll want to use this from your PHP scripts.

**MYSQL_DATABASE**: the name of a schema, which is automatically created, that the user defined above has access to.

The example above creates a database called tutorial, which can be access using the user tutorial and password secret.


# How to set up debugging in IDE

## PHP STORM
1. Setting -> PHP. Set php CLI interpreter over docker container.
2. Path mapping is set automatically, check it.
3. Setting -> PHP -> Servers. Set localhost server
4. Settings -> Build, Execution, Deployment -> Docker. Set up docker container

## VS CODE
1. Set up launch.json with this configuration:

        {
            "name": "Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/var/www/": "E:/docker/php-dev-environment/sites/"
              },
              "log": true
        }