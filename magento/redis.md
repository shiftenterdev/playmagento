## Installation
>Update your local `apt` package cache and install Redis by typing
```bash
sudo apt update
sudo apt install redis-server
```
> Open this file with your preferred text editor
```bash
$ sudo vi /etc/redis/redis.conf
```

?> The supervised directive is set to no by default. If you are running Ubuntu, which uses the `systemd init` system, change this to systemd
```bash
...

# If you run Redis from upstart or systemd, Redis can interact with your
# supervision tree. Options:
#   supervised no      - no supervision interaction
#   supervised upstart - signal upstart by putting Redis into SIGSTOP mode
#   supervised systemd - signal systemd by writing READY=1 to $NOTIFY_SOCKET
#   supervised auto    - detect upstart or systemd method based on
#                        UPSTART_JOB or NOTIFY_SOCKET environment variables
# Note: these supervision methods only signal "process is ready."
#       They do not enable continuous liveness pings back to your supervisor.
supervised systemd

...
```
> Restart as 
```bash
$ sudo systemctl restart redis.service
```

**Testing:**
```bash
$ sudo systemctl status redis
```

?> To test that Redis is functioning correctly
```bash
$ redis-cli
```
> Then hit `ping` command
```bash
127.0.0.1:6379 > ping
```

```text
#Output

PONG

```


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