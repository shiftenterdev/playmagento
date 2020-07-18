## Nginx config
> Nginx general configuration
```sh
server {
    listen 80;
    server_name www.domain.com domain.com;

    root /home/ubuntu/domain.com;
    index index.php;


    # log files
    access_log /home/ubuntu/domain.com/access.log;
    error_log /home/ubuntu/domain.com/error.log;

    location = /favicon.ico {
        log_not_found off;
        access_log off;
    }

    location = /robots.txt {
        allow all;
        log_not_found off;
        access_log off;
    }

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires max;
        log_not_found off;
    }

}
```
## Swap memory
> Swap memory for Ubuntu
```sh
sudo fallocate -l 1G /swapfile;
sudo chmod 600 /swapfile;
sudo mkswap /swapfile;
sudo swapon /swapfile;
echo '/swapfile swap swap sw 0 0' | sudo tee -a /etc/fstab
```

## Let's Encrypt
> Installing Certbot
```sh
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx
# for apache
sudo apt-get install python-certbot-apache
sudo certbot --nginx -d example.com -d www.example.com
```

## Nginx 302
> Nginx 302 bad gateway
```sh
$ sudo vi /etc/nginx/nginx.conf
# in http node add
fastcgi_buffers 16 16k; 
fastcgi_buffer_size 32k;

$ sudo service nginx reload/restart
```

## Composer issue
> Composer issues during installation
```sh
composer install --ignore-platform-reqs
php -d memory_limit=-1 /usr/local/bin/composer install
```