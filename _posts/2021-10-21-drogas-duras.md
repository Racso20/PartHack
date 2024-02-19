---
title: "Kavacon 2021 – Drogas Duras"
author: "Oscar Bravo"
header: 
  teaser: "/assets/images/post/2021/kavacon.png"
categories:
  - WriteUp
---



### USER

En primer llugar hacemos un nmap a la ip y obtenemos lo siguiente
```
Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-21 19:40 -03
Nmap scan report for 10.4.4.123
Host is up (0.053s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 62:a3:bc:f1:98:aa:d6:30:9c:f0:85:b7:b2:7c:f4:09 (RSA)
|   256 b2:4c:19:f3:d7:a2:05:45:b5:b1:f4:dc:11:92:f0:b4 (ECDSA)
|_  256 f0:89:8e:f2:09:e2:67:c8:0d:67:e5:40:e8:c5:76:85 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Say my name
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.18 (91%), Linux 4.15 - 5.6 (90%), Linux 5.0 (90%), Linux 2.6.32 (90%), Linux 3.4 (90%), Linux 3.5 (90%), Linux 3.7 (90%), Linux 4.2 (90%), Synology DiskStation Manager 5.1 (90%), Linux 5.0 - 5.4 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.15 seconds
```

No hay mucha información así que nos enfocamos en la web y nos damos cuenta que es una web de la serie «BREAKING BAD» escrita en php

![Drogas Duras 1](/assets/images/post/2021/drogas-duras.png)

Donde nos pide usuario y password con la frase «SAY MY NAME», esto hace alusión a cuando Walter White la dice en la Temporada 5 episodio 7 donde la respuesta era Heisenberg

![Drogas Duras 2](/assets/images/post/2021/drogas-duras1.png)

con esto debemos buscar el pass, para ello entramos a robots.txt y nos dice que hay un pista.html al entrar nos aparece una frase «estas seguro que estas en el lugar correcto? recuerda las tecnologias implementadas» como la tecnología de la web es php cambiamos pista.html a pista.php donde aparece la frase «toma mi boleto de loteria es la llave donde encontrarme».

El boleto de lotería, hacia alusión a las coordenadas de la plata de Walter White, buscando en internet obtenemos los datos
10 cosas que no sabías de 'Breaking Bad'

![Drogas Duras 3](/assets/images/post/2021/drogas-duras2.jpg)

Por lo tanto ahora tenemos usuario y password heisenberg:034059020106036052, al tratar de ingresarlas vemos que solo permite datos hasta 5 caracteres, por lo que cambiamos en el inspectos y accedemos correctamente. Pero no muestra nada, por lo que buscamos el codigo fuente y obtenemos un código c2t5bGVyLnBocA que en base64 es skyler.php

![Drogas Duras 4](/assets/images/post/2021/drogas-duras3.jpg)
![Drogas Duras 5](/assets/images/post/2021/drogas-duras4.jpg)


Entramos a skyler.php y pasa lo mismo, la web solo muestra una imagen, pero en el código fuente aparece información.

	ICAgICAgICA8Yz4KICAgICAgICAgUmZnbmYgcmEgY3J5dnRlYiEhIQoKICAgICAgICAgUGJhIGRodnJhIHBlcnJmIGRociByZmduZiB1bm95bmFxYiBudWJlbj8gbnBuZmIgZm5vcmYgcGhuYXFiIHRuYWIgcmEgaGEgbvFiPwogICAgICAgICBhYiB6ciBwZXJyZXZuZiBmdiBnciB5YiBxdndyZW4sIGdoIGFiIHliIHBlcnJldm5mCiAgICAgICAgIGZub3JmIGRociBjbmZuZXZuIGZ2IHFyIGNlYmFnYiBhYiBpYmwgbiBnZW5vbnduZT8KICAgICAgICAgaGEgYXJ0YnB2YiB5YiBmaHN2cHZyYWdyenJhZ3IgdGVuYXFyICBwYnpiIGNuZW4gaXJhcXJlIG5wcHZiYXJmIHJhIG9ieWZuIFFSRk5DTkVSUFJFVk4uCiAgICAgICAgIFJmZ24gcHluZWIgZGhyIGFiIGZub3JmIHBiYSBkaHZyYSByZmduZiB1bm95bmFxYiwgZ3IgcW5lciBoYW4gY3ZmZ24gZ2ggcGVycmYgZGhyIGZ2IHpyIHpuYXFuZiBoYSBjbmVuenJnZWIgc3Z5cmFuenIgCiAgICAgICAgIHJmZ25lciByYSBjcnl2dGViPyBBQiBGWExZUkUhISwgaGEgdWJ6b2VyIGdicG4geW4gY2hyZWduIGwgeXIgcXZmY25lbmEgZnIgZ2VuZ24gcXIgenY/IGFiIExCIEZCTCBSWSBESFIgR0JQTiBZTiBDSFJFR04hISEKICAgICAgICA8L2M+Cg

![Drogas Duras 6](/assets/images/post/2021/drogas-duras5.jpg)

Este código es un base64 con un rot13, al decodificarlo obtenemos

     <p>
         Estas en peligro!!!

         Con quien crees que estas hablando ahora? acaso sabes cuando gano en un año?
         no me creerias si te lo dijera, tu no lo creerias
         sabes que pasaria si de pronto no voy a trabajar?
         un negocio lo suficientemente grande  como para vender acciones en bolsa DESAPARECERIA.
         Esta claro que no sabes con quien estas hablando, te dare una pista tu crees que si me mandas un parametro filename 
         estare en peligro? NO SKYLER!!, un hombre toca la puerta y le disparan se trata de mi? no YO SOY EL QUE TOCA LA PUERTA!!!
        </p>

Lo que nos hace suponer que podemos usar el parametro filename para acceder a archivos, se prueba con el metodo GET y no muestra nada, pero con la ayuda de BURPSUITE mandamo POST y obtenemos los datos.

![Drogas Duras 7](/assets/images/post/2021/drogas-duras6.jpg)

Empezamos a buscar pero no encontramos información util, por lo que empezamos a leer los archivos en la web para ver si un programador dejó alguna pista con wrapper de php. Para ello usamos aquel que codifica los archivos en base64 (como no carga <?php ?> permite enviar la web codificada y decodificarla a la salida.

![Drogas Duras 8](/assets/images/post/2021/drogas-duras7.jpg)

Probamos pinkman:2563601029543 en ssh y tenemos acceso como usuario.

![Drogas Duras 9](/assets/images/post/2021/drogas-duras8.jpg)

***flag{M3t4nF3t4M1n4_4ZuL}***

ROOT

Vemos que el usuario tiene permiso en docker por lo que usamos GTFObins para ver si existe un escalada de privilegios y efectimente hay una que permite levantar shell con el comando

```docker run -v /:/mnt --rm -it alpine chroot /mnt bash```

Al ejecutarlo obtenemos una bash con acceso root y podemos leer la flag

![Drogas Duras 10](/assets/images/post/2021/drogas-duras9.jpg)

***flag{Qu1er0_k_tu_m3_m4t3s}***

![Racso](https://www.hackthebox.com/badge/image/159593)