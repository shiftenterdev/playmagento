## Welcome
> Welcome *playmagento.com*
## Install server

> Install Nignx/Apache, PHP, Mysql & other utilities

```bash
$ sudo apt update
$ sudo add-apt-repository ppa:ondrej/php;
$ sudo apt install php7.3 php7.3-soap php7.3-zip php7.3-curl php7.3-xml php7.3-gd php7.3-intl php7.3-bcmath php7.3-mysql mysql-server php7.3-fpm nginx php7.3-mbstring git vim zip htop -y;
```
** **If you want to install apache server then replace `nginx` with `apache2` in the above command.**

## Switch default PHP

> If you want to install apache server then replace nginx with apache2 in the above command.
```bash
$ sudo update-alternatives --set php /usr/bin/php7.3
```

## Install Composer

> Install composer
```sh
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer;
```

## Server restart
> Restart server
```bash
# for apache
sudo service apache2 restart;
# for nginx
sudo service nginx restart;
sudo service php7.3-fpm restart # if required
```
> Auth start server after reboot
```sh
sudo systemctl enable apapche2;
sudo systemctl enable php7.3-fpm;
sudo systemctl enable nginx;
sudo systemctl enable mysql;
```

## Valet(Mac OS)
> Valet for MacOS development platform
```bash
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