
# Firewall UFW
```sh
sudo ufw allow OpenSSH

sudo ufw status


# allow web traffic
sudo ufw allow www

# allow secure web traffic
sudo ufw allow https

# allow custom port
sudo ufw allow 2222/tcp   # custom ssh port

sudo ufw enable

sudo ufw deny from 10.1.1.1

sudo allow from 10.2.2.2 to any port 22  # allow only 10.2.2.2 to port 22 only

# mysql
sudo ufw allow from 10.10.10.10.0/24 to any port 3306  # not recommended

# delete rules
sudo ufw status numbered
sudo ufw delete 4

# enable/disable firewall
sudo ufw status

sudo nmap -sS remoteserver

```