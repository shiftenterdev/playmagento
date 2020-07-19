## Configuration
> Add a configuration similar to the following to `app/etc/env.php`
```php
'cache' =>
array(
   'frontend' =>
   array(
   // Default Cache
      'default' =>
      array(
         'backend' => 'Cm_Cache_Backend_Redis',
         'backend_options' =>
         array(
            'server' => '127.0.0.1',
            'database' => '0',
            'port' => '6379'
            ),
    ),
    // Full page cache
    'page_cache' =>
    array(
      'backend' => 'Cm_Cache_Backend_Redis',
      'backend_options' =>
       array(
         'server' => '127.0.0.1',
         'port' => '6379',
         'database' => '1',
         'compress_data' => '0'
       )
    )
  )
),
```
?> In cli you can set as
```bash
cd /data/web/magento2
bin/magento setup:config:set --cache-backend=redis --cache-backend-redis-server=127.0.0.1 --cache-backend-redis-db=0
```

?> Now flush your cache:
```bash
rm -rf /data/web/magento2/var/cache/*
redis-cli flushall
```