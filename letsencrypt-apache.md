# Let's encrypt

```sh
sudo apt install certbot python3-certbot-apache

cd /etc/apache2

cd sites-enabled

cat hrothar.conf

#C ertbot will look for this two parameters on ServerHost to get the certificate
  together with your registered domain names
# make sure that your dns is setup properly and that you can get to your site
   with your dns
... ServerName hrothgar.learn-code.ca
    ServerAlias www.hrothgar.learn-code.ca


# get a certificate: guided prompt
sudo certbot --apache

# this will create new files
 hrothgar-le-ssl.conf
 www-le-ssl.conf

# certfiles are in 
  /etc/letsencrypt/live folder 
  
sudo systemctl reload apache2

# check certbot is auto renew
sudo systemctl status certbot.timer

#

````
