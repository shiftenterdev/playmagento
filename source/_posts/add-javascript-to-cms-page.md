---
extends: _layouts.post
section: content
title: Add javascript to a CMS page
date: 2018-12-23
description: Add a custom javascript to a cms page
categories: [customization, feature]
excerpt: Sometimes in CMS page for additional functionality ...
---

**Sometimes in CMS page for additional functionality we need external javascript to work there.**

First create the custom.js at below location (in your case you have already did this)
```text
app/design/{Vendor_name}/{theme}/web/js/custom.js
```
Now in admin area go to following location 
```text
Admin > Content > Elements > Pages > {page} > {edit} > Design > Layout Update XML
```
Put the below code there in that section
```xml
<head>
    <link src="js/custom.js"/>
</head>
```
> Save the page & flush the cache & you will see it is working


