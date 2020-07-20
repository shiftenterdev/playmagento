
!> Coming soon

## Directory Structure

```text
├── registration.php
├── composer.json
├── etc
│   ├── module.xml
│   ├── config.xml
│   ├── db_schema.xml
│   ├── db_schema_whitelist.json
│   ├── schema.graphqls
│   ├── acl.xml
│   ├── di.xml
│   ├── events.xml
│   ├── crontab.xml
│   ├── mview.xml
│   ├── email_templates.xml
│   ├── indexer.xml
│   ├── eav_attributes.xml
│   ├── webapi.xml
│   ├── widget.xml
│   ├── adminhtml
│   │   ├── menu.xml
│   │   ├── routes.xml
│   │   ├── system.xml
│   │   ├── di.xml
│   │   └── events.xml
│   ├── frontend
│   │   ├── routes.xml
│   │   ├── di.xml
│   │   ├── events.xml
│   │   ├── page_types.xml
│   │   └── sections.xml
│   ├── webapi_soap
│   │   └── di.xml
│   └── webapi_rest
│       └── di.xml
├── Block
│   └── Adminhtml
├── Controller
│   └── Adminhtml
├── Helper
│   └── Data.php
├── CustomerData
├── Ui
├── Api
│   └── Data
├── Console
│   └── Command
├── Cron
├── Setup
│   └── Patch
├── Test
├── i18n
│   ├── en_US.csv
│   └── sv_SE.csv
├── Plugin
├── Observer
├── ViewModel
├── Model
│   └── ResourceModel
│       └── Collection.php
└── view
    ├── frontend
    │   ├── layout
    │   ├── templates
    │   ├── web
    │   ├── email
    │   └── requirejs-config.js
    ├── adminhtml
    │   ├── layout
    │   ├── ui_component
    │   ├── template
    │   ├── web
    │   └── requirejs-config.js
    └── base
        ├── layout
        ├── templates
        └── web

```

!> Reference magento customer module

### registratopn.php

```php
<?php


use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(ComponentRegistrar::MODULE, 'Magento_Customer', __DIR__);

```

### etc/module.xml

```xml
<?xml version="1.0"?>

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_Customer" >
        <sequence>
            <module name="Magento_Eav"/>
            <module name="Magento_Directory"/>
        </sequence>
    </module>
</config>

```

### etc/acl.xml
```xml
<?xml version="1.0"?>

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Acl/etc/acl.xsd">
    <acl>
        <resources>
            <resource id="Magento_Backend::admin">
                <resource id="Magento_Customer::customer" title="Customers" translate="title" sortOrder="40">
                    <resource id="Magento_Customer::manage" title="All Customers" translate="title" sortOrder="10">
                        <resource id="Magento_Customer::actions" title="Actions" translate="title" sortOrder="10">
                            <resource id="Magento_Customer::delete" title="Delete" translate="title" sortOrder="10" />
                            <resource id="Magento_Customer::reset_password" title="Reset password" translate="title" sortOrder="20" />
                            <resource id="Magento_Customer::invalidate_tokens" title="Invalidate tokens" translate="title" sortOrder="30" />
                        </resource>
                    </resource>
                    <resource id="Magento_Customer::online" title="Now Online" translate="title" sortOrder="20" />
                    <resource id="Magento_Customer::group" title="Customer Groups" translate="title" sortOrder="30" />
                </resource>
                <resource id="Magento_Backend::stores">
                    <resource id="Magento_Backend::stores_settings">
                        <resource id="Magento_Config::config">
                            <resource id="Magento_Customer::config_customer" title="Customers Section" translate="title" sortOrder="50" />
                        </resource>
                    </resource>
                </resource>
            </resource>
        </resources>
    </acl>
</config>

```

### etc/config.xml
```xml
<?xml version="1.0"?>
<!--
/**
 * Copyright © Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Store:etc/config.xsd">
    <default>
        <customer>
            <account_share>
                <scope>1</scope>
            </account_share>
            <create_account>
                <confirm>0</confirm>
                <default_group>1</default_group>
                <tax_calculation_address_type>billing</tax_calculation_address_type>
                <email_domain>example.com</email_domain>
                <email_identity>general</email_identity>
                <email_template>customer_create_account_email_template</email_template>
                <email_no_password_template>customer_create_account_email_no_password_template</email_no_password_template>
                <email_confirmation_template>customer_create_account_email_confirmation_template</email_confirmation_template>
                <email_confirmed_template>customer_create_account_email_confirmed_template</email_confirmed_template>
                <vat_frontend_visibility>0</vat_frontend_visibility>
            </create_account>
            <default>
                <group>1</group>
            </default>
            <online_customers>
                <section_data_lifetime>60</section_data_lifetime>
            </online_customers>
        </customer>
    </default>
</config>

```

### etc/db_schema.xml
```xml
<?xml version="1.0"?>
<!--
/**
 * Copyright © Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <table name="customer_entity" resource="default" engine="innodb" comment="Customer Entity">
        <column xsi:type="int" name="entity_id" padding="10" unsigned="true" nullable="false" identity="true"
                comment="Entity ID"/>
        <column xsi:type="smallint" name="website_id" padding="5" unsigned="true" nullable="true" identity="false"
                comment="Website ID"/>
        <column xsi:type="varchar" name="email" nullable="true" length="255" comment="Email"/>
        <column xsi:type="smallint" name="group_id" padding="5" unsigned="true" nullable="false" identity="false"
                default="0" comment="Group ID"/>
        <column xsi:type="varchar" name="increment_id" nullable="true" length="50" comment="Increment ID"/>
        <column xsi:type="smallint" name="store_id" padding="5" unsigned="true" nullable="true" identity="false"
                default="0" comment="Store ID"/>
        <column xsi:type="timestamp" name="updated_at" on_update="true" nullable="false" default="CURRENT_TIMESTAMP"
                comment="Updated At"/>
        <column xsi:type="smallint" name="is_active" padding="5" unsigned="true" nullable="false" identity="false"
                default="1" comment="Is Active"/>
        <column xsi:type="smallint" name="disable_auto_group_change" padding="5" unsigned="true" nullable="false"
                identity="false" default="0" comment="Disable automatic group change based on VAT ID"/>
        <column xsi:type="date" name="dob" comment="Date of Birth"/>
        <column xsi:type="varchar" name="password_hash" nullable="true" length="128" comment="Password_hash"/>
        <column xsi:type="datetime" name="rp_token_created_at" on_update="false" nullable="true"
                comment="Reset password token creation time"/>
        <column xsi:type="int" name="default_billing" padding="10" unsigned="true" nullable="true" identity="false"
                comment="Default Billing Address"/>
        <column xsi:type="smallint" name="gender" padding="5" unsigned="true" nullable="true" identity="false"
                comment="Gender"/>
        <column xsi:type="timestamp" name="lock_expires" on_update="false" nullable="true"
                comment="Lock Expiration Date"/>
        <constraint xsi:type="primary" referenceId="PRIMARY">
            <column name="entity_id"/>
        </constraint>
        <constraint xsi:type="foreign" referenceId="CUSTOMER_ENTITY_STORE_ID_STORE_STORE_ID" table="customer_entity"
                    column="store_id" referenceTable="store" referenceColumn="store_id" onDelete="SET NULL"/>
        <constraint xsi:type="foreign" referenceId="CUSTOMER_ENTITY_WEBSITE_ID_STORE_WEBSITE_WEBSITE_ID"
                    table="customer_entity" column="website_id" referenceTable="store_website"
                    referenceColumn="website_id" onDelete="SET NULL"/>
        <constraint xsi:type="unique" referenceId="CUSTOMER_ENTITY_EMAIL_WEBSITE_ID">
            <column name="email"/>
            <column name="website_id"/>
        </constraint>
        <index referenceId="CUSTOMER_ENTITY_STORE_ID" indexType="btree">
            <column name="store_id"/>
        </index>
    </table>
</schema>
```

### etc/adminhtml/menu.xml
```xml
<?xml version="1.0"?>

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Backend:etc/menu.xsd">
    <menu>
        <add id="Magento_Customer::customer" title="Customers" translate="title" module="Magento_Customer" sortOrder="30" resource="Magento_Customer::customer"/>
        <add id="Magento_Customer::customer_manage" title="All Customers" translate="title" module="Magento_Customer" sortOrder="10" parent="Magento_Customer::customer" action="customer/index/" resource="Magento_Customer::manage"/>
        <add id="Magento_Customer::customer_online" title="Now Online" translate="title" module="Magento_Customer" sortOrder="30" parent="Magento_Customer::customer" action="customer/online/" resource="Magento_Customer::online"/>
    </menu>
</config>
```

### etc/adminhtml/routes.xml
```xml
<?xml version="1.0"?>

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="admin">
        <route id="customer" frontName="customer">
            <module name="Magento_Customer" />
        </route>
    </router>
</config>

```

### Controller

### Admin/Controller

### Block

### Admin/Block

### Helper Data

### Ui Component

### Layout

### Templates