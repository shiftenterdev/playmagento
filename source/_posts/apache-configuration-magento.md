---
extends: _layouts.post
section: content
title: Apache configuration for Magento
date: 2018-11-21
categories: [apache,configuration]
description: Apache configuration for Magento
---

Create a virtual host `website.com.conf` in the following location

```text
/etc/apache2/sites-enabled/
```

The configuration is

```apache
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
}
```

**Please note that the file must have `.conf` extension**