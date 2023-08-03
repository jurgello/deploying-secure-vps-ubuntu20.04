# Apache - PHP

```sh
sudo apt search php | more

#sudo apt install php php-gd php-mbstring php-xml php-zip

sudo apt update
sudo add add-apt-repository -y ppa:ondrej/php
sudo apt update
sudo apt installphp8.0 php8.0-cli php8.0-common php8.0-curl php8.0-pgsql php8.0-fpm php8.0-gd php8.0-imap php8.0-intl php8.0-mbstring php8.0-mysql php8.0.opcache php8.0-zip

php --version

```

Install PHP apache
```sh
sudo apt install libapache2-mod-php
sudo systemctl start apache2
cd /var/www/hrothgar

vi test.php

```
```
<?php
$world = "world";
echo "Hello, ", $world;
>
```

```sh
sudo systemctl status php8.0-fpm   # PHP 8.0 FastCGI Process Manager

sudo systemctl stop apache2

```

## NGinx PHP



## Adding Virtual host
config: hrothgar.conf
```
server {
    listen 80;
    listen [::]:80;

    root /var/www/hrothgar;
    index index.html index.htm index.php;

    server_name hrothgar.learn-code.ca;

    location / {
        try_files $uri $uri/ = 404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.0 fpm.sock;
    }
}


```

```sh
sudo systemctl start nginx

```

## Caddy -PHP

```
# hrothgar.conf
hrothgar.learn-code.ca {
    encode zstd gzip
    import static
    import security

    root * /var/www/hrothgar

    file_server

    php_factcgi unix//var/run/php/php8.0-fpm.sock

    log {
       output file /var/log/caddy/hrothgar-access.log
       format single_field common_log
    } 
}


```

```sh
sudo systemctl start caddy

```

## Install Composer - 
A dependency Manager for PHP

```sh
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

sudo mv composer.phar /usr/local/bin/composer

composer --help
```