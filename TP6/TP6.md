# TP6 #
## 2. Mise en place du lab ##
### Checklist IP Routeurs ###
#### Définition des IPs statiques : ####
R1:
```
R1#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
Ethernet0/0                10.6.202.254    YES NVRAM  up                    up
Ethernet0/1                10.6.100.1      YES NVRAM  up                    up
Ethernet0/2                10.6.100.5      YES NVRAM  up                    up
Ethernet0/3                unassigned      YES NVRAM  administratively down down
```
R2:
```
R2#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
Ethernet0/0                10.6.100.2      YES NVRAM  up                    up
Ethernet0/1                10.6.100.9      YES NVRAM  up                    up
Ethernet0/2                unassigned      YES NVRAM  administratively down down
Ethernet0/3                unassigned      YES NVRAM  administratively down down
```
R3:
```
R3#show ip int br
Interface                  IP-Address      OK? Method Status                Pocol
Ethernet0/0                10.6.100.10     YES NVRAM  up                    u
Ethernet0/1                10.6.100.14     YES NVRAM  up                    u
Ethernet0/2                10.6.101.1      YES NVRAM  up                    u
Ethernet0/3                unassigned      YES NVRAM  administratively down d
```
R4:
```
R4#show ip int br
Interface                  IP-Address      OK? Method Status                Pocol
Ethernet0/0                10.6.100.6      YES NVRAM  up                    u
Ethernet0/1                10.6.100.13     YES NVRAM  up                    u
Ethernet0/2                unassigned      YES NVRAM  administratively down d
Ethernet0/3                unassigned      YES NVRAM  administratively down d
```
R5:
```
R5#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
Ethernet0/0                10.6.101.2      YES manual up                    up
Ethernet0/1                10.6.201.254    YES manual up                    up
Ethernet0/2                unassigned      YES unset  administratively down down
Ethernet0/3                unassigned      YES unset  administratively down down
```

 #### Définition du nom de domaine ####
R1:
```
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#hostname r1.tp6.b1
r1.tp6.b1(config)#exit
r1.tp6.b1#
```
R2:
```
R2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R2(config)#hostname r2.tp6.b1
r2.tp6.b1(config)#exit
r2.tp6.b1#
```
R3:
```
R3#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R3(config)#hostname r3.tp6.b1
r3.tp6.b1(config)#exit
r3.tp6.b1#

```
R4:
```
R4#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R4(config)#hostname r4.tp6.b1
r4.tp6.b1(config)#exit
r4.tp6.b1#r

```
R5:
```
R5#conf t
R5(config)#hostname r5.tp6.b1
r5.tp6.b1(config)#exit
r5.tp6.b1#

```
### Checklist VMs ###
Toutes les VMs sont ok.

J'ai configuré tous les router. 
### show ip protocols: ###
```
Routing for Networks:
    10.6.101.0 0.0.0.3 area 0
    10.6.201.0 0.0.0.255 area 0
 Reference bandwidth unit is 100 mbps
  Routing Information Sources:
    Gateway         Distance      Last Update
    4.4.4.4              110      00:08:10
    1.1.1.1              110      00:08:10
    2.2.2.2              110      00:08:10
    3.3.3.3              110      00:08:10
  Distance: (default is 110)
```
### show ip ospf neighbor: ###
```
Neighbor ID     Pri   State           Dead Time   Address         Interface
3.3.3.3           1   FULL/DR         00:00:39    10.6.101.1      Ethernet0/0
```