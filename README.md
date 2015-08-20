# Wordpress Docker image fork from official?
## Why another fork ?

* To include GD with Freetype support in order to use Wordpress plugin Really Simple CAPTCHA with Contact Form 7.
* Have a image without compiler in it (gcc, g++ ...).
* Add PHP modules by simply installing packages.


More details now.

Wordpress official image is based on lib-apache image which is based on debian:jessie.

In debian:jessie image php package is not available, so it was compiled with some modules (including GD but without Freetype support) and install is non standard directory (/usr/local/....).

After that 2 possibilities:
 * Compile GD with Freetype support, I try and failed ;)
 * Change base image with Ubuntu. In this OS you just need to install php, php5-gd to have GD with Freetype support.

I choose the second solution :)

## Prerequisites
Have a mariadb container running.

## Run the container
 ```docker run -d --link *your_db_container*:mysql -p 80:80 -p 443:443 --name *your_wordpress* daone/wordpress```

### WP data outside the container
 Add ```-v *your_path*:/var/www/html``` to ```docker run``` command.

### SSL certificate
 Comming soon ....

## Use docker-compose
 Modify docker-compose.yml (https://github.com/daonerz/wordpress) to suit your needs.

 To start, launch the following command in the directory where docker-compose.yml is present:
 ```docker-compose up -d```

 It include a container to backup your wordpress.

### backup
 ```docker exec *backup-container* backup```

### restore
 ```docker exec *backup-container* restore YYYYmmdd```
