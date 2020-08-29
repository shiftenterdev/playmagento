---
extends: _layouts.post
section: content
title: Download magento using composer
date: 2018-11-21
categories: [apache,configuration]
description: Download magento using composer
---

First we need to set the composer token for proper magento package dependency. These tokens are ensure you that if you had any purchased module through **Magento Markeplace** they will also auto download.

### Set global magento2 token for composer

```bash
sudo chown -R ubuntu ~/.composer
composer.phar global config http-basic.repo.magento.com <public_key> <private_key>
# Example
composer global config http-basic.repo.magento.com f92d6b866405d0799d86b41ffe00e342 378bc0e72c91dcaa404266bdf87ee961
```

### Download Magento

Download magento project from git using compose

```bash
cd /var/www/website.com
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.3.5-p1 .
```