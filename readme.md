# Setup Secure VPS - Ubuntu 20.04

Enable Firewall

```sh
ufw allow OpenSSH
ufw enable
ufw status

```

## Create user
Login as root

```sh
adduser jr

# grant sudo access to user
usermod -aG sudo jr

ssh jr@remote-ip

```

Update OS

```sh

sudo apt update

sudo apt upgrade 

sudo reboot

```

Delete user

```sh
sudo userdel user

```
## Locking Down SSH

### Generating ssh keys
Generate ssh keys on local machine
```sh
ssh-keygen -t rsa 

```

### Copy ssh public key to the server

```sh
ssh-copy-id jr@remoteserver
#test
ssh jr@remoteserver

```

### Requiring keys for ssh connections

```sh
ssh jr@remoteserver

cd /etc/ssh
sudo cp sshd_config sshd_config.dist
sudo sshd_config
...
PasswordAuthentication  no
PermitRootLogin no

# restart ssh

sudo systemctl restart ssh


```



### Lock down ssh to permit only what we need
```sh
sudo vi sshd_config
...
MaxAuthTries 3
PermitEmptyPaswords no

sudo systemctl restart ssh
```

### Install fail2ban

```sh
ssh jr@remoteserver
sudo apt update
sudo apt install fail2ban

sudo systemctl start fail2ban
sudo systemctl enable fail2ban  # enable start service on reboot

cd /etc/fail2ban
sudo vi jail.local
[sshd]
enabled = true
port = 22
filter = sshd
logpath = /var/log/auth.log
maxretry = 3

sudo systemctl restart fail2ban

```

### SFTP
```sh
sftp jr@remoteserver

```


## Firewall UFW
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