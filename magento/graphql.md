## Introduction
!> Graphql support in Magento from version `2.3`.

?> The default endpoint is `/graphql` means `https://website.com/graphql`

**Sample Query:**
```bash
{
  storeConfig {
    id
    code
    website_id
    locale
    base_currency_code
    default_display_currency_code
    timezone
    weight_unit
    base_url
    base_link_url
    base_static_url
    base_media_url
    secure_base_url
    secure_base_link_url
    secure_base_static_url
    secure_base_media_url
    store_name
  }
}
```

**Response:**
```sh
{
  "data": {
    "storeConfig": {
      "id": 1,
      "code": "default",
      "website_id": 1,
      "locale": "en_US",
      "base_currency_code": "USD",
      "default_display_currency_code": "USD",
      "timezone": "America/Chicago",
      "weight_unit": "lbs",
      "base_url": "http://magento2.vagrant193/",
      "base_link_url": "http://magento2.vagrant193/",
      "base_static_url": "http://magento2.vagrant193/pub/static/version1536249714/",
      "base_media_url": "http://magento2.vagrant193/pub/media/",
      "secure_base_url": "http://magento2.vagrant193/",
      "secure_base_link_url": "http://magento2.vagrant193/",
      "secure_base_static_url": "http://magento2.vagrant193/pub/static/version1536249714/",
      "secure_base_media_url": "http://magento2.vagrant193/pub/media/",
      "store_name": "My Store"
    }
  }
}

```

## Create Module

?> Here is step by step process of how to create a Graphql Module.

> Let's we will be going to create a Brand module with graphql.

?> First create `registration.php` and `etc/module.xml` file.
?> Now create `db_schema.xml` file in `etc` directory. 
!> This schema is for your reference.
```xml
<?xml version="1.0"?>
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <table name="brands" resource="default" engine="innodb" comment="Catalog Product Table">
        <column xsi:type="int" name="entity_id" padding="10" unsigned="true" nullable="false" identity="true"
                comment="Entity ID"/>
        <column xsi:type="varchar" name="name" nullable="false" length="32" default="simple"/>
        <column xsi:type="varchar" name="image" nullable="true" length="255" />
        <column xsi:type="text" name="description" nullable="true"/>
        <column xsi:type="timestamp" name="created_at" on_update="false" nullable="false" default="CURRENT_TIMESTAMP"
                comment="Creation Time"/>
        <column xsi:type="timestamp" name="updated_at" on_update="true" nullable="false" default="CURRENT_TIMESTAMP"
                comment="Update Time"/>
        <constraint xsi:type="primary" referenceId="PRIMARY">
            <column name="entity_id"/>
        </constraint>
    </table>
</schema>
```

?> Then create `schema.graphqls` file in `etc` directory
```graphql
type Query {
    brands (
        title: String @doc(description: "Brand Title")
    ):Brands @resolver(class: "Goo\\Brand\\Model\\Resolver\\Brand") @doc(description: "find brands")
    allBrands : AllBrands @resolver(class: "Goo\\Brand\\Model\\Resolver\\AllBrands") @doc(description: "Get the all the brands")
}
type Brands @doc(description: "Get brand information"){
    items: [branditems] @doc(descriptions:"text")
}
type AllBrands @doc(description: "Get brand information"){
    items: [branditems] @doc(descriptions:"text")
}
type branditems @doc(description: "text"){
    title: String @doc(description: "Brand title")
    description: String @doc(description: "description")
    image: String @doc(description: "image")
}
```
4. Now we need to create those resolver class referenced in the graphql schema.
```php
<?php
declare(strict_types=1);
namespace Goo\Brand\Model\Resolver;
use Goo\Brand\Model\ResourceModel\Brand\Collection;
use Magento\Framework\Exception\NoSuchEntityException;
use Magento\Framework\GraphQl\Config\Element\Field;
use Magento\Framework\GraphQl\Exception\GraphQlInputException;
use Magento\Framework\GraphQl\Exception\GraphQlNoSuchEntityException;
use Magento\Framework\GraphQl\Query\ResolverInterface;
use Magento\Framework\GraphQl\Schema\Type\ResolveInfo;
/**
 * Order sales field resolver, used for GraphQL request processing
 */
class Brand implements ResolverInterface
{
    /**
     * @var Collection
     */
    private $collectionFactory;
    /**
     * @var \Magento\Store\Model\StoreManagerInterface
     */
    private $storeManager;

    public function __construct(
        Collection $collectionFactory,
        \Magento\Store\Model\StoreManagerInterface $storeManager
    )
    {
        $this->collectionFactory = $collectionFactory;
        $this->storeManager = $storeManager;
    }

    /**
     * @inheritdoc
     */
    public function resolve(
        Field $field,
        $context,
        ResolveInfo $info,
        array $value = null,
        array $args = null
    )
    {
        return $this->getPostData($args);
    }

    private function getPostData($args): array
    {
        $mediaUrl =$this->storeManager->getStore()->getBaseUrl(\Magento\Framework\UrlInterface::URL_TYPE_MEDIA);
        if (!isset($args['title'])) {
            try {
                $result = [];
                $data = $this->collectionFactory
                    ->addFieldToSelect(['name', 'description', 'image']);

                foreach ($data as $key => $item) {
                    if ($item->getData()) {
                        $result['items'][$key] = [
                            'title' => $item->getName(),
                            'description' => $item->getDescription(),
                            'image' => $mediaUrl.str_replace('/pub/media/','',$item->getImage()),
                        ];
                    }
                }
                return $result;

            } catch (NoSuchEntityException $e) {
                throw new GraphQlNoSuchEntityException(__($e->getMessage()), $e);
            }
            return $result;
        }else{
            $result = [];
            $title = $args['title'];
            $data = $this->collectionFactory
                ->addFieldToFilter('name',$title)
                ->addFieldToSelect(['name', 'description', 'image']);
            foreach ($data as $key => $item) {
                if ($item->getData()) {
                    $result['items'][$key] = [
                        'title' => $item->getName(),
                        'description' => $item->getDescription(),
                        'image' => $mediaUrl.str_replace('/pub/media/','',$item->getImage()),
                    ];
                }
            }
            return  $result;
        }
    }
}
```

```php
<?php

declare(strict_types=1);

namespace Goo\Brand\Model\Resolver;

use Goo\Brand\Model\ResourceModel\Brand\Collection;
use Magento\Framework\Exception\NoSuchEntityException;
use Magento\Framework\GraphQl\Config\Element\Field;
use Magento\Framework\GraphQl\Exception\GraphQlInputException;
use Magento\Framework\GraphQl\Exception\GraphQlNoSuchEntityException;
use Magento\Framework\GraphQl\Query\ResolverInterface;
use Magento\Framework\GraphQl\Schema\Type\ResolveInfo;

/**
 * Order sales field resolver, used for GraphQL request processing
 */
class AllBrands implements ResolverInterface
{
    /**
     * @var Collection
     */
    private $collectionFactory;
    /**
     * @var \Magento\Store\Model\StoreManagerInterface
     */
    private $storeManager;

    public function __construct(
        Collection $collectionFactory,
        \Magento\Store\Model\StoreManagerInterface $storeManager
    )
    {
        $this->collectionFactory = $collectionFactory;
        $this->storeManager = $storeManager;
    }

    /**
     * @inheritdoc
     */
    public function resolve(
        Field $field,
        $context,
        ResolveInfo $info,
        array $value = null,
        array $args = null
    )
    {
        return $this->getBrandsData();
    }

    /**
     * @return array
     * @throws GraphQlNoSuchEntityException
     * @throws NoSuchEntityException
     */
    private function getBrandsData(): array
    {
        $mediaUrl =$this->storeManager->getStore()->getBaseUrl(\Magento\Framework\UrlInterface::URL_TYPE_MEDIA);
        try {
            $result = [];
            $data = $this->collectionFactory
                ->addFieldToSelect(['name', 'description', 'image']);

            foreach ($data as $key => $item) {
                if ($item->getData()) {
                    $result['items'][$key] = [
                        'title' => $item->getName(),
                        'description' => $item->getDescription(),
                        'image' => $mediaUrl.str_replace('/pub/media/','',$item->getImage()),
                    ];
                }
            }
            return $result;

        } catch (NoSuchEntityException $e) {
            throw new GraphQlNoSuchEntityException(__($e->getMessage()), $e);
        }
    }
}
```