## Install server

> Install Nignx/Apache, PHP, Mysql & other utilities

```sh
$ sudo apt update
$ sudo add-apt-repository ppa:ondrej/php;
$ sudo apt install php7.3 php7.3-soap php7.3-zip php7.3-curl php7.3-xml php7.3-gd php7.3-intl php7.3-bcmath php7.3-mysql mysql-server php7.3-fpm nginx php7.3-mbstring git vim zip htop -y;
```
** **If you want to install apache server then replace `nginx` with `apache2` in the above command.**

## Switch default PHP

> If you want to install apache server then replace nginx with apache2 in the above command.
```sh
$ sudo update-alternatives --set php /usr/bin/php7.3
```

## Install Composer

> Install composer
```sh
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer;
```
