# Apache

```sh
sudo apt update

sudo apt install apache2

sudo systemctl status apache2

```

## Adding Virtual host 

```sh
cd /var/www
ls 
html

sudo mkdir www
sudo mkdir site2

sudo chown -R jr:jr www
sudo chown -R jr:jr hrothgar

sudo chmod -R 755 www
sudo chmod -R 755 hrothgar

cd www
echo "www site" >> index.html

cd ../hrothgar
echo "hrothgar site " >> index.html

cd /etc/apache2

ls

sites-available
sites-enabled

cd sites-available
ls 
000-default.conf
default-ssl.conf

sudo vi hrothgar.conf

<VirtualHost *:80>
    ServerAdmin me@here.com
    ServerName hrothgar.earn-code.ca
    ServerAlias www.hrothgar.learn-code.ca
    DocumentRoot /var/www/hrothgar
    ErrorLog ${APACHE_LOG_DIR}/hrothgar-error.log
    CustomLog ${APACHE_LOG_DIR}/hrothgar-access.log combined
</VirtualHost>

sudo vi www.conf

<VirtualHost *:80>
    ServerAdmin me@here.com
    ServerName www.earn-code.ca
    DocumentRoot /var/www/www
    ErrorLog ${APACHE_LOG_DIR}/www-error.log
    CustomLog ${APACHE_LOG_DIR}/www-access.log combined
</VirtualHost>

cd ../site-available
# create symlinks
sudo a2ensite www.conf
sudo systemctl reload apache2

sudo a2ensite hrothgar.conf
sudo systemctl reload apache2

sudo a2dissite 000-default.conf
sudo systemctl reload apache2


```