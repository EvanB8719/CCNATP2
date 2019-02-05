# TP 4 - Spéléologie réseau : descente dans les couches #
## 2. Création des VMs ##
Checklist :
ip définit
connexion ssh fait
nom de domaine fait
remplissage fichier hosts fait
### Client1 ping router1.tp4 : ###
```
[evan@client1 ~]$ ping router1.tp4
PING router1.tp4 (10.1.0.254) 56(84) bytes of data.
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=1 ttl=64 time=0.958 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=2 ttl=64 time=0.369 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=3 ttl=64 time=0.420 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=4 ttl=64 time=0.340 ms
64 bytes from router1.tp4 (10.1.0.254): icmp_seq=5 ttl=64 time=0.333 ms
^C
--- router1.tp4 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4003ms
rtt min/avg/max/mdev = 0.333/0.484/0.958/0.238 ms
```
### Server1 ping router1.tp4 : ###
```
[serveur@server1 etc]$ ping router1.tp4
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
[router@router1 ~]$ ip route show
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
[serveur@server1 ~]$ ip route show
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

### 1 : vider la table ARP de toutes vos machines -> fait ###

### 2 : Sur client1 : ###
```
[evan@client1 ~]$ ip neigh show
10.1.0.1 dev enp0s3 lladdr 0a:00:27:00:00:03 REACHABLE
Cette ligne nous dit que 10.1.0.1 est accessible et on connait l'adresse physique. Il a fait une requête à l'IP.
```
### 3 : Sur server1 : ###
```
[evan@server1 ~]$ ip neigh show
10.2.0.1 dev enp0s3 lladdr 0a:00:27:00:00:10 REACHABLE
Cette ligne nous dit que 10.2.0.1 est accessible. On connait donc l'adresse physique de 10.2.0.1. Il a fait une requête à l'IP. Cette ligne ne va jamais s'enlever car c'est celle de notre machine.
```
### 4 : Sur client1 aprés le ping du serveur 1 : ###
```
[evan@client1 ~]$ ip neigh show
10.1.0.254 dev enp0s3 lladdr 08:00:27:01:70:2c REACHABLE
10.1.0.1 dev enp0s3 lladdr 0a:00:27:00:00:03 REACHABLE
Une nouvelle ligne, c'est rajouté. Quand on a fait un ping à server1, on est passé par le routeur car elle connait la route pour aller au server1. Dand l'arp, la nouvelle ligne affiche qu'on connait maintenant l'adresse physique de 10.1.0.254 et qu'elle est accessible.
```
### 5 : Sur sever1 : ###
```
[evan@server1 ~]$ ip neigh show
10.2.0.254 dev enp0s3 lladdr 08:00:27:f8:5c:d4 STALE
10.2.0.1 dev enp0s3 lladdr 0a:00:27:00:00:10 DELAY
La requête de l'arp nous as donnée l'adresse physique du routeur 10.2.0.254, mais elle nous dit que la ligne va disparaitre de la table arp. Si elle refait une requête, la table arp affichera la nouvelle requête.
La deuxième ligne nous dit qu'il y a un delay avant qu'elle fasse la requête, elle s'en occupera aprés. Si on refait un ip neigh showdans l'arp, 10.2.0.1 redeviendra accessible.
```
### B. Manip 2 ###

### 1 : vider la table ARP de toutes vos machines -> fait ###

### 2 : Sur router1 : ###
```
[evan@router1 ~]$ ip neigh show
10.1.0.1 dev enp0s3 lladdr 0a:00:27:00:00:03 REACHABLE
La ligne affiche l'adresse physique de 10.1.0.1 et nous dit qu'elle est accessible. Cette ligne ne s'effacera pas de la table arp car c'est la route de notre machine.
```
### 3 : client 1 ping server1 : réussi. ###

### 4 : sur router1 : ###
```
[evan@router1 ~]$ ip neigh show
10.2.0.10 dev enp0s8 lladdr 08:00:27:75:26:da REACHABLE
10.1.0.10 dev enp0s3 lladdr 08:00:27:21:bc:16 REACHABLE
10.1.0.1 dev enp0s3 lladdr 0a:00:27:00:00:03 DELAY
Aprés le ping, on peut voir que le routeur a fait une requête au pc1 et au pc2. La table arp a récupé l'adresse physique du pc1 et pc2 et nous dit qu'ils sont accessible.
La dernière ligne est en delay, elle est en attente et se fera aprés. Si on fait une nouvelle requête, elle sera de nouveau accessible.
```
### C. Manip 3 ###

### 1 : vider la table ARP de toutes vos machines -> fait ###

### 2 : PC : ###

#### table arp : ####
```
PS C:\WINDOWS\system32> arp -a
Interface : 10.1.0.1 --- 0x5
  Adresse Internet      Adresse physique      Type
  10.1.0.255            ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.2.0.1 --- 0x10
  Adresse Internet      Adresse physique      Type
  10.2.0.255            ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
```
### table arp aprés curl : ###
```
[evan@client1 ~]$ ip neigh show
10.1.0.1 dev enp0s3 lladdr 0a:00:27:00:00:03 REACHABLE
10.0.3.2 dev enp0s8 lladdr 52:54:00:12:35:02 REACHABLE
La nouvelle ligne qui vient de s'affciher, est l'adresse IP et physique de la carte NAT que l'on vient d'activée.
```