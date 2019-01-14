# TP 3 - Plusieurs réseaux : routage statique


## I. Création et utilisation simples d'une VM CentOS

### 1. Création
        déjà fait ensemble en cours
    
### 2. Installation de l'OS
        déjà fait ensemble en cours

### 3. Premier boot
        déjà fait ensemble en cours

### 4. Configuration réseau d'une machine CentOS
        déjà fait ensemble en cours

#### A Faire:
#### A- 

[evan@localhost etc]$ wget www.google.com

--2019-01-08 16:59:57--  http://www.google.com/
Resolving www.google.com (www.google.com)... 216.58.213.132, 2a00:1450:4007:815::2004
Connecting to www.google.com (www.google.com)|216.58.213.132|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
index.html: Permission denied

Cannot write to ‘index.html’ (Permission denied).
[evan@localhost etc]$ sudo wget www.google.com
--2019-01-08 17:00:16--  http://www.google.com/
Resolving www.google.com (www.google.com)... 216.58.213.132, 2a00:1450:4007:815::2004
Connecting to www.google.com (www.google.com)|216.58.213.132|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: ‘index.html’

    [ <=>                                                                           ] 11,317      --.-K/s   in 0.002s

2019-01-08 17:00:16 (4.32 MB/s) - ‘index.html’ saved [11317]
#### B-
[evan@localhost etc]$ ping 192.168.127.10

PING 192.168.127.10 (192.168.127.10) 56(84) bytes of data.
64 bytes from 192.168.127.10: icmp_seq=1 ttl=64 time=0.050 ms
64 bytes from 192.168.127.10: icmp_seq=2 ttl=64 time=0.101 ms
64 bytes from 192.168.127.10: icmp_seq=3 ttl=64 time=0.058 ms
64 bytes from 192.168.127.10: icmp_seq=4 ttl=64 time=0.043 ms
64 bytes from 192.168.127.10: icmp_seq=5 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=6 ttl=64 time=0.038 ms
64 bytes from 192.168.127.10: icmp_seq=7 ttl=64 time=0.038 ms
64 bytes from 192.168.127.10: icmp_seq=8 ttl=64 time=0.038 ms
64 bytes from 192.168.127.10: icmp_seq=9 ttl=64 time=0.052 ms
64 bytes from 192.168.127.10: icmp_seq=10 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=11 ttl=64 time=0.125 ms
64 bytes from 192.168.127.10: icmp_seq=12 ttl=64 time=0.055 ms
64 bytes from 192.168.127.10: icmp_seq=13 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=14 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=15 ttl=64 time=0.038 ms
64 bytes from 192.168.127.10: icmp_seq=16 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=17 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=18 ttl=64 time=0.052 ms
64 bytes from 192.168.127.10: icmp_seq=19 ttl=64 time=0.039 ms
64 bytes from 192.168.127.10: icmp_seq=20 ttl=64 time=0.038 ms
64 bytes from 192.168.127.10: icmp_seq=21 ttl=64 time=0.038 ms
64 bytes from 192.168.127.10: icmp_seq=22 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=23 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=24 ttl=64 time=0.037 ms
64 bytes from 192.168.127.10: icmp_seq=25 ttl=64 time=0.036 ms
^C
--- 192.168.127.10 ping statistics ---
25 packets transmitted, 25 received, 0% packet loss, time 23999ms
rtt min/avg/max/mdev = 0.036/0.046/0.125/0.022 ms

#### C- 
[evan@localhost etc]$ ip route
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101

### 5. Faire joujou avec quelques commandes

#### A Faire:
##### ping 
* ping hôte -> VM


* ping VM -> hôte

##### afficher la table de routage
* de l'hôte :
[evan@localhost ~]$ ip route
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101

* de la VM :
[evan@localhost ~]$ ip route
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101