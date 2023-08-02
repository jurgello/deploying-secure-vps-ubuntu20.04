# Nginx


```sh
sudo apt install nginx
sudo systemctl status nginx


```

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
}


```

```
config: www.conf
server {
    listen 80;
    listen [::]:80;

    root /var/www/www;
    index index.html index.htm index.php;

    server_name wwww.learn-code.ca;

    location / {
        try_files $uri $uri/ = 404;
    }
}


```

```sh
cd /etc/nginx/site-enabled
sudo ln -s /etc/nginx/sites-available/hrothgar.conf .
sudo ln -s /etc/nginx/sites-available/www.conf .

# test nginx config
sudo nginx -t

sudo systemctl reload nginx
```

## Setup lets encrypt
```sh
sudo apt update
sudo apt install certbot python3-certbot-nginx

```

Install certificates for domain
```sh
sudo certbot --nginx -d hrothgar.learn-code.ca
sudo certbot --nginx -d www.learn-code.ca
sudo systemctl reload nginx
```

Logs
```
cd /var/log/nginx

```

Start/stop
```sh
sudo systemctl status nginx
sudo systemctl stop|start|enable|disable nginx

sudo systemctl stop certbot.timer
sudo systemctl disable certbot.timer

```