## Installation
> Varnish installation
```bash
$ sudo apt install varnish -y
$ varnish -V
$ systemctl start varnish
$ systemctl enable varnish
$ sudo netstat -putln | grep varnishd
```
**For Apache server**
```bash
$ sudo a2enmod proxy  
$ sudo a2enmod proxy_http 
$ sudo a2enmod headers
$ sudo vi /etc/apache2/ports.conf
```
?> Set listen port to `8080` instead `80` and in virtual host config set port to `8080` as well.

```bash
<VirtualHost *:8080>
# Then restart the server
$ sudo systemctl restart apache2
```

**For Nginx server**

?> Set listen port to `8080` instead of `80`.