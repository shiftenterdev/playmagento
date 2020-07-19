## Welcome `v1.0`
?> Welcome **playmagento.com** `v1.0` :100:

!> This documentation is still on development.
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
```bash
sudo systemctl enable apapche2;
sudo systemctl enable php7.3-fpm;
sudo systemctl enable nginx;
sudo systemctl enable mysql;
```

## Install Nodejs
> Install nodejs using Binary Distributions
**Node.js v14.x:**
```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_14.x | bash -
apt-get install -y nodejs
```

**Node.js v12.x:**
```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_12.x | bash -
apt-get install -y nodejs
```

**Node.js v10.x:**
```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt-get install -y nodejs
```

**Node.js LTS (v12.x):**
```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_lts.x | bash -
apt-get install -y nodejs
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