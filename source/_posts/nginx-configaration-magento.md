---
extends: _layouts.post
section: content
title: Nginx configuration for Magento
date: 2018-11-21
categories: [nginx,configuration]
description: Nginx configuration for Magento
---

Create a virtual host in the following location

```text
/etc/nginx/sites-enabled/
```

The configuration is

```nginx
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

> If you have more than one magento project for Nginx then you can ignore upstream `fastcgi_backend` node for later project’s virtual host.