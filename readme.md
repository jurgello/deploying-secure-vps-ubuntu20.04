
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