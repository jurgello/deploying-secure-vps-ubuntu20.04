# Caddy Web server

Install
```sh

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```
Check service
```sh
sudo systemctl status caddy

```

Configuration

```sh
cd /etc/caddy
ls Caddyfile
mv Caddyfile Caddyfile.dist

```
Caddyfile
```
{
    email   trevor.sawler@gmail.com
}

(static) {
        @static {
                file
                path *.ico *.css *.js *.gif *.jpg *.jpeg *.png *.svg *.woff *.json
        }
        header @static Cache-Control max-age=5184000
}

(security) {
        header {
                # enable HSTS
                Strict-Transport-Security max-age=31536000;
                # disable clients from sniffing the media type
                X-Content-Type-Options nosniff
                # keep referrer data off of HTTP connections
                Referrer-Policy no-referrer-when-downgrade
        }
}

import conf.d/*.conf

```

Make additional conf
```sh
sudo mkdir conf.d
sudo vi hrothgar.conf

```
```
# hrothgar.conf
hrothgar.learn-code.ca {
    encode zstd gzip
    import static
    import security

    root * /var/www/hrothgar

    file_server

    log {
       output file /var/log/caddy/hrothgar-access.log
       format single_field common_log
    } 
}

```
Caddy config file with reverse proxy settings

```
# www.conf
www.learn-code.ca {
    encode zstd gzip
    import static
    import security

    #root * /var/www/www

    #file_server

   reverse_proxy localhost:8080

    log {
       output file /var/log/caddy/hrothgar-access.log
       format single_field common_log
    } 
}

```

