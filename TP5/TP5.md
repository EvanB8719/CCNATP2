# TP 5. Premier pas dans le monde Cisco #
Preparation des VMs de GNS3 pour commencer le tp.
### Ping client1 à client2 ###
```
[evan@client1 ~]$ ping client2
PING client2 (10.5.2.11) 56(84) bytes of data.
64 bytes from client2 (10.5.2.11): icmp_seq=1 ttl=64 time=2.69 ms
64 bytes from client2 (10.5.2.11): icmp_seq=2 ttl=64 time=1.43 ms
64 bytes from client2 (10.5.2.11): icmp_seq=3 ttl=64 time=1.19 ms
64 bytes from client2 (10.5.2.11): icmp_seq=4 ttl=64 time=1.31 ms
^C
--- client2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 1.193/1.657/2.692/0.604 ms
```
### Ping client1 à server1 ###
```
[evan@client1 ~]$ ping server1
PING server1 (10.5.1.10) 56(84) bytes of data.
64 bytes from server1 (10.5.1.10): icmp_seq=3 ttl=62 time=42.2 ms
64 bytes from server1 (10.5.1.10): icmp_seq=4 ttl=62 time=38.3 ms
64 bytes from server1 (10.5.1.10): icmp_seq=5 ttl=62 time=25.1 ms
64 bytes from server1 (10.5.1.10): icmp_seq=6 ttl=62 time=24.8 ms
64 bytes from server1 (10.5.1.10): icmp_seq=7 ttl=62 time=41.9 ms
^C
--- server1 ping statistics ---
7 packets transmitted, 5 received, 28% packet loss, time 6013ms
rtt min/avg/max/mdev = 24.870/34.496/42.250/7.875 ms 
```
### Ping client2 à client1 ###
```
[evan@client2 ~]$ ping client1
PING client1 (10.5.2.10) 56(84) bytes of data.
64 bytes from client1 (10.5.2.10): icmp_seq=1 ttl=64 time=1.60 ms
64 bytes from client1 (10.5.2.10): icmp_seq=2 ttl=64 time=1.33 ms
64 bytes from client1 (10.5.2.10): icmp_seq=3 ttl=64 time=1.14 ms
64 bytes from client1 (10.5.2.10): icmp_seq=4 ttl=64 time=1.37 ms
64 bytes from client1 (10.5.2.10): icmp_seq=5 ttl=64 time=1.37 ms
^C
--- client1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4022ms
rtt min/avg/max/mdev = 1.147/1.367/1.607/0.153 ms
```
### Ping client2 à server1 ###
```
[evan@client2 ~]$ ping server1
PING server1 (10.5.1.10) 56(84) bytes of data.
64 bytes from server1 (10.5.1.10): icmp_seq=1 ttl=62 time=47.8 ms
64 bytes from server1 (10.5.1.10): icmp_seq=2 ttl=62 time=35.2 ms
64 bytes from server1 (10.5.1.10): icmp_seq=3 ttl=62 time=42.4 ms
64 bytes from server1 (10.5.1.10): icmp_seq=4 ttl=62 time=35.6 ms
64 bytes from server1 (10.5.1.10): icmp_seq=5 ttl=62 time=41.6 ms
^C
--- server1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4016ms
rtt min/avg/max/mdev = 35.297/40.561/47.866/4.692 ms
```
### Ping server1 à client1 ###
```
[evan@server1 ~]$ ping client1
PING client1 (10.5.2.10) 56(84) bytes of data.
64 bytes from client1 (10.5.2.10): icmp_seq=1 ttl=62 time=33.8 ms
64 bytes from client1 (10.5.2.10): icmp_seq=2 ttl=62 time=40.7 ms
64 bytes from client1 (10.5.2.10): icmp_seq=3 ttl=62 time=36.1 ms
64 bytes from client1 (10.5.2.10): icmp_seq=4 ttl=62 time=38.7 ms
^C
--- client1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3010ms
rtt min/avg/max/mdev = 33.856/37.402/40.796/2.634 ms
```
### Ping server1 à client2 ###
```
[evan@server1 ~]$ ping client2
PING client2 (10.5.2.11) 56(84) bytes of data.
64 bytes from client2 (10.5.2.11): icmp_seq=1 ttl=62 time=34.3 ms
64 bytes from client2 (10.5.2.11): icmp_seq=2 ttl=62 time=41.3 ms
64 bytes from client2 (10.5.2.11): icmp_seq=3 ttl=62 time=35.6 ms
64 bytes from client2 (10.5.2.11): icmp_seq=4 ttl=62 time=39.8 ms
^C
--- client2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3016ms
rtt min/avg/max/mdev = 34.319/37.816/41.378/2.910 ms
```
### Route des VMs: ###
```
[evan@client1 ~]$ ip route show
10.5.1.0/24 via 10.5.2.254 dev enp0s3 proto static metric 101
10.5.2.0/24 dev enp0s3 proto kernel scope link src 10.5.2.10 metric 101
192.168.240.0/24 dev enp0s8 proto kernel scope link src 192.168.240.5 metric 100
```
```
[evan@server1 ~]$ ip route show
10.5.1.0/24 via 10.5.2.254 dev enp0s3 proto static metric 101
10.5.2.0/24 dev enp0s3 proto kernel scope link src 10.5.2.11 metric 101
192.168.240.0/24 dev enp0s8 proto kernel scope link src 192.168.240.6 metric 100
```
```
[evan@client2 ~]$ ip route show
10.5.1.0/24 dev enp0s3 proto kernel scope link src 10.5.1.10 metric 101
10.5.2.0/24 via 10.5.1.254 dev enp0s3 proto static metric 101
192.168.240.0/24 dev enp0s8 proto kernel scope link src 192.168.240.4 metric 102
```