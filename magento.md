## Nginx virtual host

> Create Virtual Host nginx
```sh
upstream fastcgi_backend {
    # use tcp connection
    # server  127.0.0.1:9000;
    # or socket
    server   unix:/var/run/php/php7.3-fpm.sock;
}

server {
   listen 80;
   server_name website.com www.website.com;
 
   set MAGE_ROOT /var/www/website.com;
   set MAGE_MODE default;
 
   include /var/www/website.com/nginx.conf.sample;
   error_log /var/www/website.com/error_log warn; 
}
```
> Location
```sh
/etc/nginx/sites-enabled/
```
** **If you have more than one magento project for Nginx Then you can ignore `upstream fastcgi_backend` node for later project’s virtual host.**

## Apache virtual host

> Create Virtual Host Apache2
```sh
<VirtualHost *:80>
	ServerName website.com
	ServerAlias www.website.com
	DocumentRoot /var/www/website.com
	<Directory /var/www/website.com>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Require all granted
	</Directory> 
	ErrorLog /var/www/website.com/error.log
</VirtualHost>
```
> Location
```sh
/etc/apache2/sites-enabled/
```

## Restart server
> Restart server
```sh
# for apache
sudo service apache2 restart;
# for nginx
sudo service nginx restart;
sudo service php7.3-fpm restart # if required
```

## Magento composer token
> Set global magento2 token for composer
```sh
sudo chown -R ubuntu ~/.composer
composer.phar global config http-basic.repo.magento.com <public_key> <private_key>
# Example
composer global config http-basic.repo.magento.com f92d6b866405d0799d86b41ffe00e342 378bc0e72c91dcaa404266bdf87ee961
```

## Download Magento
> Download magento project from git using composer
```sh
cd /var/www/website.com
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.3.5-p1 .
```

## Project permission
> Give Project file specific Permission
```sh
find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +;
find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +;
chown -R :www-data .;
chmod u+x bin/magento;
```
## Create Database
> Create Database
```sh
sudo mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'";
mysql -uroot -p -e "CREATE DATABASE project_database";
```

## Install Magento
> Install Magento Project via cli
```sh
$ bin/magento setup:install --base-url=http://magento.test \
--db-host=localhost \
--db-name=database \
--db-user=root \
--db-password=root \
--admin-firstname=System \
--admin-lastname=Admin \
--admin-email=user@example.com \
--admin-user=admin \
--admin-password=admin \
--backend-frontname=admin \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1
```