---
title: "Hackaton Telefonica 2019 – Box GO"
author: "31m0"
categories:
  - WriteUp
tags:
  - Hackaton
  - Maquina
---


![GO 1](/assets/images/post/2019/go1.jpg)

En lo particular este desafío te mostraba una imagen, preguntando si estabas listo ? Y al mismo presentando un mensaje “Encontrar algo que no esperas en el lugar que nunca imaginaste” de cierto modo era proporcionar la idea de que al final la diferencia la iban a hacer pequeños detalles que ibas a tener que mirar más de una vez. Mientras por el lado de servicios al momento de enumerar con un nmap por defecto solo íbamos a identificar el puerto 80, pero agregando el parámetro -p- íbamos a lograr encontrar el servicio 221 abierto el cual mas adelante nos serviría para realizar las conexiones de ssh con la maquina.

![GO 2](/assets/images/post/2019/go2.jpg)

Por otro lado analizando el sitio podemos observar que los datos de respuesta que se tenia en la cabecera cuando se hacia consulta al servidor, retornaban siempre el mismo valor en la cookie independiente de si te cambiabas de navegador como de IP, este ya era un indicio de que algo raro iba por este lado.

![GO 3](/assets/images/post/2019/go3.png)

Aquí había que entrar a jugar para identificar el tipo algoritmo con el cual fue encodeada la cookie, lo llevamos a un base32 decode y podemos observar que esta nos proporciona una ruta con un login al cual debiamos acceder.

![GO 4](/assets/images/post/2019/go4.png)

Ingresando al portal, este de fondo tenia un mysql con una lógica que filtraba los “or» ante inyección de sql, adicionalmente mientras se jugaba con este login de podia verificar que la inyección también era de tipo blind, pero que al cambiar el “or” por un pipe “|” la inyección ya era viable para acceder al sitio.

![GO 5](/assets/images/post/2019/go5.png)

Posteriormente el sitio tenia la característica de hacer un redireccionamiento cuando te autenticas desde /PuebloPaleta/ci.php a /CiudadLavanda/welcome.php, pero que si capturabas con burp suite u otra herramienta de proxy lograbas identificar que el sitio te retornaba un html con un  cifrado y varias llamas a librerías .js

![GO 6](/assets/images/post/2019/go6.png)

El cifrado estaba hardcodeado en el html, la idea era encontrar el decrypted para encontrar el contenido e ingresar al servidor mediante ssh. Este lo podíamos buscar en google y encontrar el decrypted y encryted ahora solo era borrar las lineas de este ultimo y pasar la variable con el cifrado para encontrar las credenciales del usuario ash e ingresar a por ssh.

![GO 7](/assets/images/post/2019/go7.png)

Ya en el servidor, podíamos observar que uno de los flag se encontraba en el /etc/passwd y que adicionalmente se encontraba repetido por un momento de descuido 😛

![GO 8](/assets/images/post/2019/go8.png)

ash:x:1001:1001:OGT{5bef854dae57360c77718e5324edf253},,,:/home/ash:/bin/rbash Dentro del servidor había un archivo con el nombre de maestropokemon que tenia programado un crontab que te entregaba el mensaje Hi!!

![GO 9](/assets/images/post/2019/go9.png)

Y que cada 2 minutos te iba a entregar las credenciales para ingresar con el usuario haunter y comenzar a buscar la elevación de privilegios.

![GO 10](/assets/images/post/2019/go10.png)

Ahora ir a buscar el flag de user.txt OGT{b62648fe5ad7c02bea5b5b37f1f12b83}

![GO 11](/assets/images/post/2019/go11.png)

Realizando la búsqueda en los directorios ocultos nos encontramos con la carpeta .document en donde podemos encontrar el archivo mewtwo con un contenido en hexadecimal y el cual debía ser invertido con el comando “tac»

![GO 12](/assets/images/post/2019/go12.png)

Adicionalmente al final de la linea encontrábamos la palabra “r3m0v3” la cual debíamos borrar del archivo y pasar a filtrar solo el contenido util con xxd -r file

![GO 13](/assets/images/post/2019/go13.png)

Para así solo descodificar con el base64 decode

![GO 14](/assets/images/post/2019/go14.png)

Ya con esto obtendríamos una key para ingresar con nuevamente por ssh y a la cual debemos dar los permisos necesarios Con la key podíamos ingresar como usuario root y leer el root.txt con el flag.

![GO 15](/assets/images/post/2019/go15.png)

![31mo](https://www.hackthebox.com/badge/image/23069)

Si quieres ver otros Write revisa los siguientes enlaces.

## HAckAtOn Telefónica 2019

### Caja

	Jaws - https://partyhack.cl/hackaton-box-jaw/
	BuRy A Fr1End - https://partyhack.cl/hackaton-box-bury-a-friend/
	Go - https://partyhack.cl/hackaton-box-go/
	Bofetada - https://github.com/s1kr10s/WriteUp
	Cacofonia - https://medium.com/@ctorogar/write-up-cacofon%C3%ADa-47cb732f46f8
	PrueBatch - https://finsin.cl/2019/07/30/escrito-de-hackatontelefonica-pruebatch
	TreasureIsland - https://finsin.cl/2019/07/30/escrito-de-hackatontelefonica-treasure-island
	Bury a Fr1end - https://partyhack.cl/2019/07/31/hackaton-telefonica-2019-box-writeup-bury_a_fr1end

### Reto

	0p3npuff - https://partyhack.cl/hackaton-reto-openpuff/
	Fr34kySh4rk - https://partyhack.cl/hackaton-reto-freakyshark/
	Cr33py - https://partyhack.cl/hackaton-reto-creapy/
	P4st3b1n - https://partyhack.cl/hackaton-reto-pastebin/

