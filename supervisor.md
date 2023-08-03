# Supervisor

```sh

sudo apt update

sudo apt install supervisor

cd /etc/supervisor
ls

conf.d supervisor.conf

```
```sh
cd /etc/supervisor/conf.d
sudo vi rps.conf

```

```
# rps.conf

[program:rps]
command=/home/jr/rock-paper-scissors
directory=/home/jr
autorestart=true
autostart=true
stdout_logfile=/home/tcs/rps.log

```

```sh
sudo supervisorctl
supervisor> status
supervisor> reread
rps:available
supervisor> update
rps: added process group
supervisor> status
rps  RUNNING pid 10156, uptime 0:00:02

supervisor> quit

ps ax | grep rock

supervisor> stop rps
rps: stopped

supervisor> start rps
rps: started


curl localhost:8080 | more
```