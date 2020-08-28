---
extends: _layouts.post
section: content
title: Install Nodejs
date: 2018-11-21
categories: [feature]
description: Install Nodejs
---

Install nodejs using Binary Distributions
> Node.js v14.x

```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_14.x | bash -
apt-get install -y nodejs
```

> Node.js v12.x
```sh
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_12.x | bash -
apt-get install -y nodejs
```