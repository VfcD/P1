# LEMP Tutorial | Linux Nginx MariaDB Php7.0
##### flavoured by: https://www.linuxbabe.com/linux-server/install-nginx-mariadb-php7-lemp-stack-ubuntu-16-04-lts
Raspberry Pi 3 ; Ubuntu MATE for Raspberry Pi 3 ; ubuntu-mate-16.04.2-desktop-armhf-raspberry-pi.img.xz

## for relaxed installing type
	sudo su
## or 	
	su


# Update Ubuntu
	apt update
	apt upgrade


# Install Nginx Web Server
	apt install nginx

## start and autostart nginx
	systemctl start nginx

## check if not already in autostart (enabled)
	systemctl status nginx
	//systemctl enable nginx


# install cool MariaDB
	apt install mariadb-server mariadb-client

## start and autostart MariaDB
	systemctl start mysql

## check if not already in autostart (enabled) 	
	systemctl status mysql
	systemctl enable mysql

## guided post installation security script
	sudo mysql_secure_installation


# install PHP7
	apt install php7.0-fpm php7.0-mbstring php7.0-xml php7.0-mysql php7.0-common php7.0-gd php7.0-json php7.0-cli php7.0-curl

## start and autostart php7.0-fpm
	systemctl start php7.0-fpm
	systemctl enable php7.0-fpm




# default Nginx server block - example

## create a new default server block file under /etc/nginx/conf.d/
  nano /etc/nginx/conf.d/default.conf

## write following code into it. <IP> YOUR SERVER <IP>
        	server {
        	  listen 80;
        	  listen [::]:80;
        	  server_name <IP> YOUR SERVER <IP>;
        	  root /usr/share/nginx/html/;
        	  index index.php index.html index.htm ;

        	  location / {
        	    try_files $uri $uri/ =404;
        	  }

        	  error_page 404 /404.html;
        	  error_page 500 502 503 504 /50x.html;

        	  location = /50x.html {
        	    root /usr/share/nginx/html;
        	  }

        	  location ~ \.php$ {
        	    fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        	    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        	    include fastcgi_params;
        	    include snippets/fastcgi-php.conf;
        	  }

        	  location ~ /\.ht {
        	    deny all;
        	  }
        	}


## remove the default symlink in sites-enabled directory
	rm /etc/nginx/sites-enabled/default

## test nginx configuration and reload it
	nginx -t
	systemctl reload nginx

## test php
	php --version

## create test.php file in the web root directory
	nano /usr/share/nginx/html/test.php

## copy paste
	<?php phpinfo(); ?>

## check the site with
	<IP> YOUR SERVER <IP>/test.php

For your server’s security, you should delete test.php file now.

> reach me via derbarti gmail com
