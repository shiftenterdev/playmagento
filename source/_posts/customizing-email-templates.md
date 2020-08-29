---
extends: _layouts.post
section: content
title: Customizing Email templates
date: 2018-11-21
categories: [feature]
description: Customizing Email templates
---

Email templates are stored in the `<module_dir>/view/<area>/email` directory of their respective modules. For example, the template for the new order transactional email for the Sales module is located in

```text
<Magento_Sales_module_dir>/view/frontend/email/order_new.html
```

### Customize email templates using a theme

Override email templates by creating templates in a new directory in your custom theme, using this pattern: `<theme_dir>/<ModuleVendorName>_<ModuleName>/email`. 

For example, to override the New Order email template, create a template named order_new.html in the `<theme_dir>/Magento_Sales/email` directory.

### Customize header and footer templates

Every frontend email template includes a header and footer template using these two directives: `{{template config_path="design/email/header_template"}}` and `{{template config_path="design/email/footer_template"}}`. By default, those two directives load contents from these files:

```text
<Magento_Email_module_dir>/view/frontend/email/header.html

<Magento_Email_module_dir>/view/frontend/email/footer.html
```