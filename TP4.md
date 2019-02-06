# TP 4 - Spéléologie réseau : descente dans les couches #
## 2. Création des VMs ##
fait en cours.
### Client1 ping router1.tp4 : ###
```
[evan@client1 ~]$ ping router1.tp4
PING router1.tp4 (10.1.0.254) 56(84) bytes of data.
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=1 ttl=64 time=0.958 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=2 ttl=64 time=0.369 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=3 ttl=64 time=0.420 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=4 ttl=64 time=0.340 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=5 ttl=64 time=0.333 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=6 ttl=64 time=0.329 ms
^C
--- router1.tp4 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 4003ms
rtt min/avg/max/mdev = 0.333/0.484/0.958/0.238 ms
```
### Server1 ping router1.tp4 : ###
```
[evan@server1 etc]$ ping router1.tp4
PING router1.tp4 (10.2.0.254) 56(84) bytes of data.
64 bytes from router1.tp4 (10.2.0.254): icmp_seq=1 ttl=64 time=0.581 ms
64 bytes from router1.tp4 (10.2.0.254): icmp_seq=2 ttl=64 time=0.320 ms
64 bytes from router1.tp4 (10.2.0.254): icmp_seq=3 ttl=64 time=0.331 ms
64 bytes from router1.tp4 (10.2.0.254): icmp_seq=4 ttl=64 time=0.321 ms
^C
--- router1.tp4 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3000ms
rtt min/avg/max/mdev = 0.320/0.388/0.581/0.112 ms
```
 ## 3. Mise en place du routage statique ##
### 1 : router1 : ###

Il y a des routes net1 et net2 :
```
[evan@router1 ~]$ ip route show
10.1.0.0/24 dev enp0s3 proto kernel scope link src 10.1.0.254 metric 102
10.2.0.0/24 dev enp0s8 proto kernel scope link src 10.2.0.254 metric 103
```
### 2 : client1 : ###

Il y a des routes net1 et net2 :
```
[evan@client1 network-scripts]$ ip route show
10.1.0.0/24 dev enp0s3 proto kernel scope link src 10.1.0.10 metric 100
10.2.0.0/24 via 10.1.0.254 dev enp0s3
```
### 3 : server 1 : ###

Il y a des routes net1 et net2 :
```
[evan@server1 ~]$ ip route show
10.1.0.0/24 via 10.2.0.254 dev enp0s3 proto static metric 100
10.2.0.0/24 dev enp0s3 proto kernel scope link src 10.2.0.10 metric 100
```
### 4 : test : ###

### client1 ping server1 : ###
```
[evan@client1 ~]$ ping 10.2.0.10
PING 10.2.0.10 (10.2.0.10) 56(84) bytes of data.
64 bytes from 10.2.0.10: icmp_seq=1 ttl=63 time=0.957 ms
64 bytes from 10.2.0.10: icmp_seq=2 ttl=63 time=0.565 ms
64 bytes from 10.2.0.10: icmp_seq=3 ttl=63 time=0.541 ms
64 bytes from 10.2.0.10: icmp_seq=4 ttl=63 time=0.607 ms
64 bytes from 10.2.0.10: icmp_seq=5 ttl=63 time=0.613 ms
64 bytes from 10.2.0.10: icmp_seq=6 ttl=63 time=0.603 ms
64 bytes from 10.2.0.10: icmp_seq=7 ttl=63 time=0.597 ms
^C
--- 10.2.0.10 ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6002ms
rtt min/avg/max/mdev = 0.541/0.640/0.957/0.133 ms
```
### server1 ping client1 : ###
```
[serveur@server1 ~]$ ping 10.1.0.10
PING 10.1.0.10 (10.1.0.10) 56(84) bytes of data.
64 bytes from 10.1.0.10: icmp_seq=1 ttl=63 time=0.674 ms
64 bytes from 10.1.0.10: icmp_seq=2 ttl=63 time=0.613 ms
^C
--- 10.1.0.10 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1000ms
rtt min/avg/max/mdev = 0.613/0.643/0.674/0.039 ms
```
## II. Spéléologie réseau ##

## 1. ARP ##


### 2 : Sur client1 : ###
```
[evan@client1 ~]$ ip neigh show
10.1.0.1 dev enp0s8 lladdr 0a:00:27:00:00:05 REACHABLE

```
### 3 : Sur server1 : ###
```
[evan@server1 ~]$ ip neigh show
10.2.0.1 dev enp0s8 lladdr 0a:00:27:00:00:10 REACHABLE
```
### 4 : Sur client1 aprés le ping du serveur 1 : ###
```
[evan@client1 ~]$ ip neigh show
10.1.0.1 dev enp0s8 lladdr 0a:00:27:00:00:05 REACHABLE
10.2.0.254 dev enp0s8 lladdr 0a:00:27:00:00:05 REACHABLE
```
### 5 : Sur sever1 : ###
```
[evan@server1 ~]$ ip neigh show
10.2.0.1 dev enp0s8 lladdr 0a:00:27:00:00:10 DELAY
```
### B. Manip 2 ###

### 1 : vider la table ARP de toutes vos machines -> fait ###

### 2 : Sur router1 : ###
```
[evan@router1 ~]$ ip neigh show
10.1.0.1 dev enp0s8 lladdr 0a:00:27:00:00:05 REACHABLE
10.2.0.1 dev enp0s9 lladdr 0a:00:27:00:00:10 STALE
```
### 3 : client 1 ping server1 : réussi. ###

### 4 : sur router1 : ###
```
[evan@router1 ~]$ ip neigh show
10.1.0.1 dev enp0s8 lladdr 0a:00:27:00:00:05 REACHABLE
10.2.0.1 dev enp0s9 lladdr 0a:00:27:00:00:10 STALE

### 2 : PC : ###

#### table arp : ####
```
PS C:\Users\evanb> arp -a

Interface : 10.1.0.1 --- 0x5
  Adresse Internet      Adresse physique      Type
  10.1.0.10             08-00-27-eb-80-e4     dynamique
  10.1.0.254            08-00-27-14-07-78     dynamique
  10.1.0.255            ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.0.2.3             01-00-5e-00-02-03     statique
  225.0.71.1            01-00-5e-00-47-01     statique
  232.0.10.93           01-00-5e-00-0a-5d     statique
  239.255.3.22          01-00-5e-7f-03-16     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.2.0.1 --- 0x10
  Adresse Internet      Adresse physique      Type
  10.2.0.10             08-00-27-85-c0-bb     dynamique
  10.2.0.254            08-00-27-f9-b4-81     dynamique
  10.2.0.255            ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.0.2.3             01-00-5e-00-02-03     statique
  225.0.71.1            01-00-5e-00-47-01     statique
  232.0.10.93           01-00-5e-00-0a-5d     statique
  239.255.3.22          01-00-5e-7f-03-16     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
```
