---
extends: _layouts.post
section: content
title: Install magento
date: 2019-08-01
categories: [magento]
description: Install magento
---

If you already download magento using composer, now we are ready for fresh installation. Before that we need to complete two steps.

1. Setup project permission
2. Create a database(Mysql) for the project.

### Project permission

```sh
find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +;
find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +;
chown -R :www-data .;
chmod u+x bin/magento;
```

### Create database 
```sh
sudo mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'";
mysql -uroot -p -e "CREATE DATABASE project_database";
```

Now we are fully ready for installation

### Magento 2.0.0 - 2.3.5-p2

```sh
$ php bin/magento setup:install --base-url=http://magento.test \
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


### Magento 2.4.0
```sh
$ php bin/magento setup:install --base-url=http://magento240.test \
--db-host=127.0.0.1 \
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
--search-engine=elasticsearch7 \
--elasticsearch-host=127.0.0.1 \
--elasticsearch-port=9200 \
--elasticsearch-index-prefix=magento2 \
--elasticsearch-timeout=15 \
--elasticsearch-enable-auth=false \
--use-rewrites=1
```

**Other option for 2.4.0 is `--elasticsearch-username`,`--elasticsearch-password`. Since Elasticsearch is now required for magento form version 2.4.0**