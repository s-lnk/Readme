## AWS Ubuntu install nginx server

### Install zip and unpack archive
```
sudo apt-get install unzip
unzip file.zip
```
Install nginx
```
sudo apt-get install nginx
```
Install php
```
sudo apt-get install php8.1-fpm
```
Add repo for PHP exts
```
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install php-curl
sudo service apache2 restart


sudo apt-get install imagemagick

sudo apt-get install php-mysql
sudo apt-get install php-xml
sudo apt-get install curl
sudo apt-get install php-intl
sudo apt-get install php8.1-mbstring
sudo apt-get install php8.1-bcmath
sudo apt-get install php8.1-gd
sudo apt-get install php8.1-imagick
sudo apt-get install php8.1-memcached
sudo apt-get install php8.1-zip
sudo apt-get install php8.1-curl
```

In /etc/php/8.1/fpm/php.ini
```
Enable and set 
max_input_vars = 5000
memory_limit = 256M
post_max_size = 128M
upload_max_filesize = 128M
Enable all other required modules
```
Set folders writeable
```
sudo chmod 777 /var/www/gate7.ee/var/cache
```

Restart Nginx, php
```
sudo systemctl restart nginx
sudo systemctl restart php8.1-fpm
```