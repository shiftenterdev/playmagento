---
extends: _layouts.post
section: content
title: Setup your environment(LAMP/LEMP)
date: 2020-01-28
description: Setup nginx,apache,mysql,git, switch php, composer, server restart, valet
categories: [setup]
featured: true
excerpt: Before starting any cms or framework we need to setupup our working environment. Thats why..
---


Before starting any cms or framework we need to setupup our working environment. Thats why we setup our development environment first. As we have basically tow options `Apache(LAMP)` or `Nginx(LEMP)`
### Basic setup
> Install Nignx/Apache, PHP, Mysql & other utilities

```sh
sudo apt update
sudo add-apt-repository ppa:ondrej/php;
sudo apt install php7.3 php7.3-soap php7.3-zip php7.3-curl \
	php7.3-xml php7.3-gd php7.3-intl php7.3-bcmath php7.3-mysql \
	mysql-server php7.3-fpm nginx php7.3-mbstring git vim zip htop -y;
```

> If you want to install `apache server` then replace `nginx` with `apache2` in the above command.

---

### Switch default PHP

> If you have multiple php version you can switch as below.

```sh
sudo update-alternatives --set php /usr/bin/php7.3
```

---

### Install Composer

```sh
curl -sS https://getcomposer.org/installer | sudo php -- \
	--install-dir=/usr/local/bin --filename=composer;
```
---

### Server Restart

```sh
# for apache
sudo service apache2 restart;
# for nginx
sudo service nginx restart;
sudo service php7.3-fpm restart # if required
```
> If you want automatically start server after reboot then 
```sh
sudo systemctl enable apapche2;
sudo systemctl enable php7.3-fpm;
sudo systemctl enable nginx;
sudo systemctl enable mysql;
```
---
### Install Valet(Optional)
> If you are a Mac user then Valet might be a good option for you
```sh
brew install php
composer global require laravel/valet
echo 'export PATH="/Users/user/.composer/vendor/bin:$PATH"' >> ~/.bashrc
valet start
brew install mysql@5.7
brew services start mysql@5.7
valet use php@7.2
# secure site
valet secure laravel
# unsecure site
valet unsecure laravel
```