## Remove category & products
> Delete all product & categories from mysql
```sql
delete from catalog_product_entity;

SET FOREIGN_KEY_CHECKS = 0;

TRUNCATE TABLE catalog_category_entity;

TRUNCATE TABLE catalog_category_entity_datetime; 
TRUNCATE TABLE catalog_category_entity_decimal; 
TRUNCATE TABLE catalog_category_entity_int; 
TRUNCATE TABLE catalog_category_entity_text; 
TRUNCATE TABLE catalog_category_entity_varchar; 
TRUNCATE TABLE catalog_category_product; 
TRUNCATE TABLE catalog_category_product_index;

INSERT INTO `catalog_category_entity` (`entity_id`, `attribute_set_id`, `parent_id`, `created_at`, `updated_at`, `path`, `position`, `level`, `children_count`) VALUES ('1', '0', '0', CURRENT_TIMESTAMP, CURRENT_TIMESTAMP, '1', '0', '0', '1'),
('2', '3', '1', CURRENT_TIMESTAMP, CURRENT_TIMESTAMP, '1/2', '1', '1', '0');

INSERT INTO `catalog_category_entity_int` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES 
('1', '69', '0', '1', '1'),
('2', '46', '0', '2', '1'),
('3', '69', '0', '2', '1');

INSERT INTO `catalog_category_entity_varchar` (`value_id`, `attribute_id`, `store_id`, `entity_id`, `value`) VALUES 
('1', '45', '0', '1', 'Root Catalog'),
('2', '45', '0', '2', 'Default Category');

DELETE FROM url_rewrite WHERE entity_type = 'category';

SET FOREIGN_KEY_CHECKS = 1;
```

## Dynamic coupon
> Create Coupon Dynamically
```php
$objectManager = \Magento\Framework\App\ObjectManager::getInstance(); 
$state = $objectManager->get('Magento\Framework\App\State');
//$state->setAreaCode('frontend');
$state->setAreaCode('adminhtml');  


$coupon['name'] = 'vip_signup';
$coupon['desc'] = 'Discount for vip signup coupon.';
$coupon['start'] = date('Y-m-d');
$coupon['end'] = '';
$coupon['max_redemptions'] = 1;
$coupon['discount_type'] ='by_percent';
$coupon['discount_amount'] = 15;
$coupon['flag_is_free_shipping'] = 'no';
$coupon['redemptions'] = 1;
$coupon['code'] ='NL01-1234'; //this code will normally be autogenetated but i am hard coding for testing purposes

$shoppingCartPriceRule = $objectManager->create('Magento\SalesRule\Model\Rule');
$shoppingCartPriceRule->setName($coupon['name'])
        ->setDescription($coupon['desc'])
        ->setFromDate($coupon['start'])
        ->setToDate($coupon['end'])
        ->setUsesPerCustomer($coupon['max_redemptions'])
        ->setCustomerGroupIds(array('0','1','2','3',))
        ->setIsActive(1)
        ->setSimpleAction($coupon['discount_type'])
        ->setDiscountAmount($coupon['discount_amount'])
        ->setDiscountQty(1)
        ->setProductIds(array(1,2,3))
        ->setApplyToShipping($coupon['flag_is_free_shipping'])
        ->setTimesUsed($coupon['redemptions'])
        ->setWebsiteIds(array('1'))
        ->setCouponType(2)
        ->setCouponCode($coupon['code'])
        ->setUsesPerCoupon(NULL);
$shoppingCartPriceRule->save();
```