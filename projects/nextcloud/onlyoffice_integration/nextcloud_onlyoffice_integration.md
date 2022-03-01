# Installation Nextcloud with Onlyoffice integration on the same server

1. Установим MariaDB

1. Установим php, php-fpm

1. Установим nginx

1. Развернем NextCloud

1. Произведем тонкие настройки сервера

1. Установим Onlyoffice

## Set up data base server

В качестве СУБД для Nextcloud используется MariaDB:

```
sudo apt install mariadb-server -y
```

Add to autostart and start service:

```
sudo systemctl enable mariadb
```

```
sudo systemctl start mariadb
```

Add password for superuser of mysql:

```
sudo mysqladmin -u root password
```

Connect to MariaDB and create data base and user:

```
sudo mysql -uroot -p
```

```
CREATE DATABASE nextcloud DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
```

```
GRANT ALL PRIVILEGES ON nextcloud.* TO nextcloud@localhost IDENTIFIED BY 'nextcloud';
```

```
\q
```

## Install and setting of web-server

Install php, php-fpm and addition moduls for nextcloud work:

```
sudo apt-get install php php-fpm php-common php-zip php-xml php-intl php-gd php-mysql php-mbstring php-curl php-imagick php-ldap -y
```

Setting php-fpm:

```
sudo vim /etc/php/7.4/fpm/pool.d/www.conf
```

Снимаем комментарий со следующих строк:

```
env[HOSTNAME] = $HOSTNAME
env[PATH] = /usr/local/bin:/usr/bin:/bin
env[TMP] = /tmp 
env[TMPDIR] = /tmp 
env[TEMP] = /tmp
```

Setting php.ini. Uncommenting that string:

```
opcache.enable=1
opcache.enable_cli=1
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=10000
opcache.memory_consumption=128
opcache.save_comments=1
opcache.revalidate_freq=1
```

Add autostart php-fpm and restart:

```
systemctl enable php7.4-fpm
```

```
systemctl restart php7.4-fpm

```

## Install nginx and setup

Install:

```
sudo apt install nginx -y
```

Create virtual server and settup:

```
sudo vim /etc/nginx/conf.d/nextcloud.conf
```

```
server {
        listen 80;
        server_name 192.168.1.107;

        root /var/www/nextcloud;

        add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
        client_max_body_size 20G;
        fastcgi_buffers 64 4K;

        rewrite ^/caldav(.*)$ /remote.php/caldav$1 redirect;
        rewrite ^/carddav(.*)$ /remote.php/carddav$1 redirect;
        rewrite ^/webdav(.*)$ /remote.php/webdav$1 redirect;

        index index.php;
        error_page 403 = /core/templates/403.php;
        error_page 404 = /core/templates/404.php;

        location = /robots.txt {
            allow all;
            log_not_found off;
            access_log off;
        }

        location ~ ^/(data|config|\.ht|db_structure\.xml|README) {
                deny all;
        }

        location ^~ /.well-known {
                location = /.well-known/carddav { return 301 /remote.php/dav/; }
                location = /.well-known/caldav  { return 301 /remote.php/dav/; }
                location ^~ /.well-known{ return 301 /index.php/$uri; }
                try_files $uri $uri/ =404;
        }

        location / {
                rewrite ^/.well-known/host-meta /public.php?service=host-meta last;
                rewrite ^/.well-known/host-meta.json /public.php?service=host-meta-json last;
                rewrite ^(/core/doc/[^\/]+/)$ $1/index.html;
                try_files $uri $uri/ index.php;
        }

        location ~ ^(.+?\.php)(/.*)?$ {
                try_files $1 = 404;
                include fastcgi_params;
                fastcgi_param SCRIPT_FILENAME $document_root$1;
                fastcgi_param PATH_INFO $2;
		fastcgi_param HTTPS off;
                fastcgi_pass unix:/run/php/php7.4-fpm.sock;
        }

        location ~* ^.+\.(jpg|jpeg|gif|bmp|ico|png|css|js|swf)$ {
                expires modified +30d;
                access_log off;
        }
}
```

Проверяем конфигурацию nginx, restart and do autostart:

```
sudo nginx -t
```

```
sudo systemctl enable nginx
```

```
sudo systemctl restart nginx
```

## Install Nextcloud

Install unzip packet:

```
sudo apt install unzip -y
```

Change directory on tmp:

```
cd /tmp
```

Install Nextcloud:

```
sudo wget "link on Downoload Nextcloud"
```

Unzip archive:

```
sudo unzip nextcloud-*.zip
```

Move to /var/www:

```
sudo mv nextcloud /var/www
```

Change mode access:

```
chown -R www-data: /var/www/nextcloud
```

Оптимизируем работу базы данных:

```
sudo -u www-data php /var/www/nextcloud/occ db:convert-filecache-bigint
```

## Upgrade Nextcloud

### Open and edit of file php.ini

```
sudo vim /etc/php/7.4/fpm/php.ini
```

```
memory_limit = 512M
```

Restart php-fpm:

```
systemctl restart php7.4-fpm
```

### Установка рекомендованных отсутствующих модулей php:

```
sudo apt install php-gmp php-bcmath
```

Restart php-fpm:

```
sudo systemctl restart php7.4-fpm
```

### Set up system of cache

**Redis**

Install Redis:

```
sudo apt install redis-server php-redis -y
```

Restart php-fpm:

```
systemctl restart php7.4-fpm
```

Open config file for nextcloud:

```
sudo vim /var/www/nextcloud/config/config.php
```

Add:

```
  'memcache.local' => '\\OC\\Memcache\\Redis',
  'memcache.distributed' => '\\OC\\Memcache\\Redis',
  'memcache.locking' => '\\OC\\Memcache\\Redis',
  'redis' => 
      array (
          'host' => 'localhost',
          'port' => 6379,
      ),
```

**Memcached**

Install:

```
sudo apt install memcached php-memcached -y
```

Autostart:

```
sudo systemctl enable memcached
```

Restart:

```
sudo systemctl restart memcached
```

Open and edit config file for nextcloud:

```
sudo vim /var/www/nextcloud/config/config/php
```

Add:

```
  'memcache.local' => '\\OC\\Memcache\\Memcached',
  'memcache.distributed' => '\\OC\\Memcache\\Memcached',
  'memcached_servers' =>
  array (
    0 =>
    array (
      0 => 'localhost',
      1 => 11211,
    ),
  ),
```

### Указываем регион размещение данного сервера:

Open and redact config file for nextcloud:

```
sudo vim var/www/nextcloud/config/config.php
```

Add:

```
'default_phone_region' => 'RU',
```

### Last step, allow local remove connect of service:

Open and redact config file for nextcloud:

```
sudo vim var/www/nextcloud/config/config.php
```

Add:

```
'allow_local_remote_servers' => true,
```

Add trusted domain:

```
'ip-address of your service, example: onlyoffice'
```

## Install Onlyoffice:

Install data base postgresql:

```
sudo apt install postgresql -y
```

Create basa and user:

```
sudo -i -u postgres psql -c "CREATE DATABASE onlyoffice;"
```

```
sudo -i -u postgres psql -c "CREATE USER onlyoffice WITH password 'onlyoffice';"
```

```
sudo -i -u postgres psql -c "GRANT ALL privileges ON DATABASE onlyoffice TO onlyoffice;"
```

Install rabbitmq and nginx-extras:

```
sudo apt install rabbitmq-server -y
```

```
sudo apt install nginx-extras -y
```

Install gnupg gnupg1 gnupg2:

```
sudo apt install gnupg gnupg1 gnupg2 -y
```

Add GPG-key:

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys CB2DE8E5
```

Add repo:

```
sudo echo "deb https://download.onlyoffice.com/repo/debian squeeze main" | sudo tee /etc/apt/sources.list.d/onlyoffice.list 
```

Update packages:

```
sudo apt update
```

Upgrade packages:

```
sudo apt dist-upgrade -y
```

Install MariaDB-client:

```
sudo apt install mariadb-client -y
```

Install ONLYOFFICE Docs, enter password "onlyoffice":

```
sudo apt install onlyoffice-documentserver -y
```

Edit nginx file for oblyoffice to change port:

```
sudo vim /etc/onlyoffice/documentserver/nginx/ds.conf  
```

Restart nginx 

```
sudo systemctl restart nginx
```
### The end
