## Mysql MacOS
> Sometime it says yout mysql blow away. Edit file `/etc/my.cnf`
```bash
# Default Homebrew MySQL server config
[mysqld]
# Only allow connections from localhost
bind-address = 127.0.0.1
default-authentication-plugin = mysql_native_password
max_allowed_packet = 256M
wait_timeout = 28800
```