---
extends: _layouts.post
section: content
title: Working with CSS in Magento
date: 2019-02-05
description: Working with CSS in Magento
featured: true
categories: [basic]
excerpt: We need to follow some rules or pattern to work with css in magento...
---

We need to follow some rules or pattern to work with css in magento.

Your custom `default_head_blocks.xml` should be located as follows:

```xml
<theme_dir>/Magento_Theme/layout/default_head_blocks.xml.
```

For example, to include `<theme_dir>/web/css/custom.css`:

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <head>
        <css src="css/custom.css" rel="stylesheet" type="text/css"  />
    </head>
</page>
```

To include an external CSS file, add `<css src="URL to External Source" src_type="url" rel="stylesheet" type="text/css" />`.

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <head>
        <css src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap-theme.min.css"  src_type="url" rel="stylesheet" type="text/css"  />
    </head>
</page>
```