# TP 2 Exploration de Réseau d’un point de vue client.

## 1 Exploration locale en solo.

#### Interface WiFi : 
*	Nom : Qualcomm Atheros QCA61x4A Wireless Network Adapter
*	Adresse MAC : 98-22-EF-99-4F-75
*	Adresse IP : `10.33.2.188`
*	Adresse réseau :`10.33.0.0`
*	Adresse Broadcast : `10.33.3.255`
#### Interface Ethernet : 
*	Nom : Bluetooth Device (Personal Area Network)
*	Adresse MAC : 98-22-EF-99-4F-76
*	Adresse IP : non-connecté
*	Gateway carte wifi : `10.33.3.253`

#### Pour l'interface GUI : 

    Clique droit sur le petit logo wifi, ouvrir les paramètres réseau et internet. Dans modifier vos paramètres réseau, cliquez sur afficher vos propriétés réseau.

* Adresse ip : `10.33.2.188/22`
* Adresse MAC : 98-22-EF-99-4F-75
* gateway : `10.33.3.253`

    	à quoi sert la gateway dans le réseau d'Ingésup ? 
La gateway sert à connecter ma machine au réseau internet et permet de sortir du reseau pour pouvoir me connecter à un autre réseau. 

## 2. Modifications des informations

### A. Modification d'adresse IP - pt. 1

* première IP du réseau : `10.33.0.1`
* dernière IP du réseau : `10.33.3.254`

#### Pour changer d'adresse IP : 
    Rechercher dans le windows "panneau de configuration", cliquez sur Réseau et internet, puis sur Centre réseau et passage. Cliquez sur votre wifi (il y a le signal à coté). Ensuite cliquez sur propriétés, chercher dans la liste "Protocole Internet version 4(TCP/IPv4)",cliquez dessus puis sur propriétés. Sélectionnez "utiliser l'adresse IP suivante", puis configurer sa nouvelle IP.

### B. NMAP

- découverte de NMAP 

### C. Modification d'adresse IP - pt. 2

- adresse ip fonctionne 
- en modifiant le gateway, on a plus internet car on modifie le routeur de sortie.

## II. Exploration locale en duo

3. Modification d'adresse IP
*  Adresse IP de ma machine : `169.254.167.68`
* Adresse IP de l'autre machine : `169.254.167.69`
* Notre masque réseau : `255.255.255.0 `
