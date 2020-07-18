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