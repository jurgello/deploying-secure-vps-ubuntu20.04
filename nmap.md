Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
jr@jr-m7390:~/Ws/udemy/tsawler/deploying-secure-VPS-Ubuntu20.04$ sudo nmap -sS marikaresort.com
Starting Nmap 7.80 ( https://nmap.org ) at 2023-07-13 17:05 CDT
Nmap scan report for marikaresort.com (188.166.238.28)
Host is up (0.25s latency).
rDNS record for 188.166.238.28: marika-01
Not shown: 991 closed ports
PORT     STATE    SERVICE
22/tcp   open     ssh
25/tcp   filtered smtp
80/tcp   open     http
135/tcp  filtered msrpc
139/tcp  filtered netbios-ssn
443/tcp  open     https
445/tcp  filtered microsoft-ds
5432/tcp open     postgresql
8080/tcp open     http-proxy

Nmap done: 1 IP address (1 host up) scanned in 9.55 seconds
jr@jr-m7390:~/Ws/udemy/tsawler/deploying-secure-VPS-Ubuntu20.04$ 


jr@marika-sgp1-01:~$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
jr@marika-sgp1-01:~$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
Nginx Full                 ALLOW       Anywhere                  
22/tcp                     ALLOW       Anywhere                  
80/tcp                     ALLOW       Anywhere                  
443                        ALLOW       Anywhere                  
OpenSSH                    ALLOW       Anywhere                  
Nginx Full (v6)            ALLOW       Anywhere (v6)             
22/tcp (v6)                ALLOW       Anywhere (v6)             
80/tcp (v6)                ALLOW       Anywhere (v6)             
443 (v6)                   ALLOW       Anywhere (v6)             
OpenSSH (v6)               ALLOW       Anywhere (v6)    

# Not working:firewall eanbled
jr@jr-m7390:~$ sudo nmap -sS marikaresort.com
[sudo] password for jr:       
Starting Nmap 7.80 ( https://nmap.org ) at 2023-07-13 17:31 CDT
Nmap scan report for marikaresort.com (188.166.238.28)
Host is up (0.29s latency).
rDNS record for 188.166.238.28: marika-01
Not shown: 996 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
5432/tcp open  postgresql

Nmap done: 1 IP address (1 host up) scanned in 17.72 seconds

# Working: firewall disabled

jr@jr-m7390:~$ sudo nmap -sS marikaresort.com
Starting Nmap 7.80 ( https://nmap.org ) at 2023-07-13 17:33 CDT
Nmap scan report for marikaresort.com (188.166.238.28)
Host is up (0.31s latency).
rDNS record for 188.166.238.28: marika-01
Not shown: 991 closed ports
PORT     STATE    SERVICE
22/tcp   open     ssh              ok
25/tcp   filtered smtp
80/tcp   open     http             ok
135/tcp  filtered msrpc
139/tcp  filtered netbios-ssn
443/tcp  open     https            ok
445/tcp  filtered microsoft-ds
5432/tcp open     postgresql       ok
8080/tcp open     http-proxy

Nmap done: 1 IP address (1 host up) scanned in 19.92 seconds



Firewall is active and enabled on system startup
jr@marika-sgp1-01:~$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
Nginx Full                 ALLOW       Anywhere                  
22/tcp                     ALLOW       Anywhere                  
80/tcp                     ALLOW       Anywhere                  
443                        ALLOW       Anywhere                  
OpenSSH                    ALLOW       Anywhere                  
8080/tcp                   ALLOW       Anywhere                  
Nginx Full (v6)            ALLOW       Anywhere (v6)             
22/tcp (v6)                ALLOW       Anywhere (v6)             
80/tcp (v6)                ALLOW       Anywhere (v6)             
443 (v6)                   ALLOW       Anywhere (v6)             
OpenSSH (v6)               ALLOW       Anywhere (v6)             
8080/tcp (v6)              ALLOW       Anywhere (v6)   


