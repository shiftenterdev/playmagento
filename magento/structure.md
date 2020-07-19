
!> Coming soon

## Directory Structure

```text


```

## registratopn.php

```php
<?php


use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(ComponentRegistrar::MODULE, 'Magento_Customer', __DIR__);

```

## etc/module.xml

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

## etc/acl.xml
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

## etc/config.xml
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
            <account_information>
                <change_email_template>customer_account_information_change_email_template</change_email_template>
                <change_email_and_password_template>customer_account_information_change_email_and_password_template</change_email_and_password_template>
            </account_information>
            <password>
                <forgot_email_identity>support</forgot_email_identity>
                <forgot_email_template>customer_password_forgot_email_template</forgot_email_template>
                <remind_email_template>customer_password_remind_email_template</remind_email_template>
                <reset_link_expiration_period>2</reset_link_expiration_period>
                <reset_password_template>customer_password_reset_password_template</reset_password_template>
                <required_character_classes_number>3</required_character_classes_number>
                <minimum_password_length>8</minimum_password_length>
                <lockout_failures>10</lockout_failures>
                <lockout_threshold>10</lockout_threshold>
                <autocomplete_on_storefront>0</autocomplete_on_storefront>
            </password>
            <address>
                <street_lines>2</street_lines>
                <prefix_show />
                <prefix_options />
                <middlename_show />
                <suffix_show />
                <suffix_options />
                <dob_show />
                <gender_show />
                <telephone_show>req</telephone_show>
                <company_show>opt</company_show>
                <fax_show/>
            </address>
            <startup>
                <redirect_dashboard>0</redirect_dashboard>
            </startup>
            <online_customers>
                <section_data_lifetime>60</section_data_lifetime>
            </online_customers>
        </customer>
    </default>
</config>

```

## etc/db_schema.xml
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
        <column xsi:type="timestamp" name="created_at" on_update="false" nullable="false" default="CURRENT_TIMESTAMP"
                comment="Created At"/>
        <column xsi:type="timestamp" name="updated_at" on_update="true" nullable="false" default="CURRENT_TIMESTAMP"
                comment="Updated At"/>
        <column xsi:type="smallint" name="is_active" padding="5" unsigned="true" nullable="false" identity="false"
                default="1" comment="Is Active"/>
        <column xsi:type="smallint" name="disable_auto_group_change" padding="5" unsigned="true" nullable="false"
                identity="false" default="0" comment="Disable automatic group change based on VAT ID"/>
        <column xsi:type="varchar" name="created_in" nullable="true" length="255" comment="Created From"/>
        <column xsi:type="varchar" name="prefix" nullable="true" length="40" comment="Name Prefix"/>
        <column xsi:type="varchar" name="firstname" nullable="true" length="255" comment="First Name"/>
        <column xsi:type="varchar" name="middlename" nullable="true" length="255" comment="Middle Name/Initial"/>
        <column xsi:type="varchar" name="lastname" nullable="true" length="255" comment="Last Name"/>
        <column xsi:type="varchar" name="suffix" nullable="true" length="40" comment="Name Suffix"/>
        <column xsi:type="date" name="dob" comment="Date of Birth"/>
        <column xsi:type="varchar" name="password_hash" nullable="true" length="128" comment="Password_hash"/>
        <column xsi:type="varchar" name="rp_token" nullable="true" length="128" comment="Reset password token"/>
        <column xsi:type="datetime" name="rp_token_created_at" on_update="false" nullable="true"
                comment="Reset password token creation time"/>
        <column xsi:type="int" name="default_billing" padding="10" unsigned="true" nullable="true" identity="false"
                comment="Default Billing Address"/>
        <column xsi:type="int" name="default_shipping" padding="10" unsigned="true" nullable="true" identity="false"
                comment="Default Shipping Address"/>
        <column xsi:type="varchar" name="taxvat" nullable="true" length="50" comment="Tax/VAT Number"/>
        <column xsi:type="varchar" name="confirmation" nullable="true" length="64" comment="Is Confirmed"/>
        <column xsi:type="smallint" name="gender" padding="5" unsigned="true" nullable="true" identity="false"
                comment="Gender"/>
        <column xsi:type="smallint" name="failures_num" padding="6" unsigned="false" nullable="true" identity="false"
                default="0" comment="Failure Number"/>
        <column xsi:type="timestamp" name="first_failure" on_update="false" nullable="true" comment="First Failure"/>
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
        <index referenceId="CUSTOMER_ENTITY_WEBSITE_ID" indexType="btree">
            <column name="website_id"/>
        </index>
        <index referenceId="CUSTOMER_ENTITY_FIRSTNAME" indexType="btree">
            <column name="firstname"/>
        </index>
        <index referenceId="CUSTOMER_ENTITY_LASTNAME" indexType="btree">
            <column name="lastname"/>
        </index>
    </table>
</schema>
```

## Controller

## Admin/Controller

## Block

## Admin/Block

## Helper Data

## Ui Component

## Layout

## Templates