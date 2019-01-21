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
ping 192.168.102.10

Envoi d’une requête 'Ping'  192.168.102.10 avec 32 octets de données :
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64

* ping VM -> hôte
ping 192.168.102.1
PING 192.168.102.1 (192.168.102.1) 56(84) bytes of data.
64 bytes from 192.168.102.1: icmp_seq=1 ttl=128 time=0.243 ms
64 bytes from 192.168.102.1: icmp_seq=2 ttl=128 time=0.327 ms

##### afficher la table de routage
* de l'hôte :
IPv4 Table de routage
===========================================================================
Itinéraires actifs :
Destination réseau    Masque réseau  Adr. passerelle   Adr. interface Métrique
          0.0.0.0          0.0.0.0    192.168.1.254     192.168.1.22     50
        127.0.0.0        255.0.0.0         On-link         127.0.0.1    331
        127.0.0.1  255.255.255.255         On-link         127.0.0.1    331
  127.255.255.255  255.255.255.255         On-link         127.0.0.1    331
      192.168.1.0    255.255.255.0         On-link      192.168.1.22    306
     192.168.1.22  255.255.255.255         On-link      192.168.1.22    306
    192.168.1.255  255.255.255.255         On-link      192.168.1.22    306
     192.168.56.0    255.255.255.0         On-link      192.168.56.1    281
     192.168.56.1  255.255.255.255         On-link      192.168.56.1    281
   192.168.56.255  255.255.255.255         On-link      192.168.56.1    281
    192.168.102.0    255.255.255.0         On-link     192.168.102.1    281
    192.168.102.1  255.255.255.255         On-link     192.168.102.1    281
  192.168.102.255  255.255.255.255         On-link     192.168.102.1    281
        224.0.0.0        240.0.0.0         On-link         127.0.0.1    331
        224.0.0.0        240.0.0.0         On-link      192.168.56.1    281
        224.0.0.0        240.0.0.0         On-link     192.168.102.1    281
        224.0.0.0        240.0.0.0         On-link      192.168.1.22    306
  255.255.255.255  255.255.255.255         On-link         127.0.0.1    331
  255.255.255.255  255.255.255.255         On-link      192.168.56.1    281
  255.255.255.255  255.255.255.255         On-link     192.168.102.1    281
  255.255.255.255  255.255.255.255         On-link      192.168.1.22    306
===========================================================================
Itinéraires persistants :
  Adresse réseau    Masque réseau  Adresse passerelle Métrique
          0.0.0.0          0.0.0.0    192.168.112.1  Par défaut
===========================================================================

* de la VM :
[evan@localhost ~]$ ip route
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101

### II. Notion de ports SSH
ss -n -p -l

tcp    LISTEN     0      128                          :::22                                     :::*                   users:(("sshd",pid=3154,fd=4))
SSh écoute sur le port 22 du PC

C:\Users\evanb>ssh evan@192.168.102.10 -p 2222
toor@192.168.102.10's password:
Last login: Tue Jan 15 16:43:25 2019 from pc2
[evan@localhost ~]$


#### III. Routage statique

##### 1. Préparation des hôtes (vos PCs)

* ping vers le PC1 : 

PS C:\Users\evanb> ping 192.168.112.9

Envoi d’une requête 'Ping'  192.168.112.9 avec 32 octets de données :
Réponse de 192.168.112.9 : octets=32 temps<1ms TTL=128
Réponse de 192.168.112.9 : octets=32 temps=4 ms TTL=128
Réponse de 192.168.112.9 : octets=32 temps=1 ms TTL=128
Réponse de 192.168.112.9 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 192.168.112.9:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 4ms, Moyenne = 1ms

* ping VM2 et PC2 : 

PS C:\Users\evanb>  ping 192.168.102.10

Envoi d’une requête 'Ping'  192.168.102.10 avec 32 octets de données :
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64
Réponse de 192.168.102.10 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 192.168.102.10:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

[evan@localhost ~]$ ping 192.168.102.1
PING 192.168.102.1 (192.168.102.1) 56(84) bytes of data.
64 bytes from 192.168.102.1: icmp_seq=1 ttl=128 time=0.331 ms
64 bytes from 192.168.102.1: icmp_seq=2 ttl=128 time=0.311 ms
64 bytes from 192.168.102.1: icmp_seq=3 ttl=128 time=0.385 ms
64 bytes from 192.168.102.1: icmp_seq=4 ttl=128 time=0.348 ms
64 bytes from 192.168.102.1: icmp_seq=5 ttl=128 time=0.353 ms
64 bytes from 192.168.102.1: icmp_seq=6 ttl=128 time=0.306 ms
64 bytes from 192.168.102.1: icmp_seq=7 ttl=128 time=0.336 ms
64 bytes from 192.168.102.1: icmp_seq=8 ttl=128 time=0.299 ms
64 bytes from 192.168.102.1: icmp_seq=9 ttl=128 time=0.321 ms
^Z
[1]+  Stopped                 ping 192.168.102.1

### 2. Configuration du routage

Bilan des adresses IP:

        Carte Ethernet PC1 : 192.168.112.9
        Carte Host-Only PC1 : 192.168.101.1
        Carte Host-Only VM1 : 192.168.101.10

        Carte Ethernet PC2 : 192.168.112.22
        Carte Host-Only PC2 : 192.168.102.1
        Carte Host-Only VM2 : 192.168.102.10

#### PC1 et PC2

* ping PC2 au réseau 1 :

PS C:\WINDOWS\system32> route add 192.168.101.0/24 mask 255.255.255.0 192.168.112.9
 OK!
PS C:\WINDOWS\system32> ping 192.168.101.1

Envoi d’une requête 'Ping'  192.168.101.1 avec 32 octets de données :
Réponse de 192.168.101.1 : octets=32 temps<1ms TTL=127
Réponse de 192.168.101.1 : octets=32 temps=1 ms TTL=127
Réponse de 192.168.101.1 : octets=32 temps=1 ms TTL=127
Réponse de 192.168.101.1 : octets=32 temps=1 ms TTL=127

Statistiques Ping pour 192.168.101.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 1ms, Moyenne = 0ms

* VM2 vers réseau 1: 

[evan@localhost ~]$ ping 192.168.101.1
PING 192.168.101.1 (192.168.101.1) 56(84) bytes of data.
64 bytes from 192.168.101.1: icmp_seq=1 ttl=126 time=1.38 ms
64 bytes from 192.168.101.1: icmp_seq=2 ttl=126 time=0.891 ms
64 bytes from 192.168.101.1: icmp_seq=3 ttl=126 time=1.10 ms
64 bytes from 192.168.101.1: icmp_seq=4 ttl=126 time=1.05 ms
64 bytes from 192.168.101.1: icmp_seq=5 ttl=126 time=1.14 ms
^Z
[3]+  Stopped                 ping 192.168.101.1

* VM2 au réseau 12 :

[evan@localhost ~]$ ping 192.168.112.1
PING 192.168.112.1 (192.168.112.1) 56(84) bytes of data.
64 bytes from 192.168.112.1: icmp_seq=1 ttl=127 time=1.27 ms
64 bytes from 192.168.112.1: icmp_seq=2 ttl=127 time=1.21 ms
64 bytes from 192.168.112.1: icmp_seq=3 ttl=127 time=1.34 ms
64 bytes from 192.168.112.1: icmp_seq=4 ttl=127 time=1.15 ms
^C
--- 192.168.112.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 1.159/1.249/1.341/0.067 ms


#### 3. Configuration des noms de domaine

* vm2 à pc1 :
[evan@localhost ~]$ ping pc1.tp3.b1
PING pc1.tp3.b1 (192.168.112.1) 56(84) bytes of data.
64 bytes from pc1.tp3.b1 (192.168.112.1): icmp_seq=1 ttl=127 time=1.00 ms
64 bytes from pc1.tp3.b1 (192.168.112.1): icmp_seq=2 ttl=127 time=1.02 ms
64 bytes from pc1.tp3.b1 (192.168.112.1): icmp_seq=3 ttl=127 time=0.976 ms
64 bytes from pc1.tp3.b1 (192.168.112.1): icmp_seq=4 ttl=127 time=0.988 ms
^C
--- pc1.tp3.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 0.976/1.000/1.028/0.029 ms

* vm2 à pc2 :
[evan@localhost ~]$ ping pc2.tp3.b1
PING pc2.tp3.b1 (192.168.102.1) 56(84) bytes of data.
64 bytes from pc2.tp3.b1 (192.168.102.1): icmp_seq=1 ttl=128 time=1.35 ms
64 bytes from pc2.tp3.b1 (192.168.102.1): icmp_seq=2 ttl=128 time=0.355 ms
64 bytes from pc2.tp3.b1 (192.168.102.1): icmp_seq=3 ttl=128 time=0.299 ms
64 bytes from pc2.tp3.b1 (192.168.102.1): icmp_seq=4 ttl=128 time=0.629 ms
^C
--- pc2.tp3.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3002ms
rtt min/avg/max/mdev = 0.299/0.660/1.357/0.421 ms

* vm2 à vm1 :
[evan@localhost ~]$ ping vm1.tp3.b1
PING vm1.tp3.b1 (192.168.101.10) 56(84) bytes of data.
64 bytes from vm1.tp3.b1 (192.168.101.10): icmp_seq=1 ttl=62 time=1.55 ms
64 bytes from vm1.tp3.b1 (192.168.101.10): icmp_seq=2 ttl=62 time=1.04 ms
64 bytes from vm1.tp3.b1 (192.168.101.10): icmp_seq=3 ttl=62 time=1.30 ms
64 bytes from vm1.tp3.b1 (192.168.101.10): icmp_seq=4 ttl=62 time=1.35 ms
^C
--- vm1.tp3.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 1.048/1.314/1.552/0.181 ms

#### Netcat :

nc vm1.tp3.b1 5454
Test 
Salut
Jsp



















