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