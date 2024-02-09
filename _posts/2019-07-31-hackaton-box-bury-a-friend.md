---
title: "Hackaton Telefonica 2019 – Box BuRy A Fr1End"
author: "PartyHack"
header: 
  teaser: "/assets/images/ctf.png"
categories:
  - WriteUp
---


Primero para empezar ocuparemos Nmap para revisar que puertos tiene abiertos la máquina.

![Burry Friend 1](https://miro.medium.com/v2/resize:fit:700/1*YWOVn4xtEvF57SNeNX1WNw.png)

En el puerto 80 se encuentra lo siguiente

![Burry Friend 2](https://miro.medium.com/v2/resize:fit:700/1*oRBNjU0GEC0AeBr2V1Zgzg.png)

En donde si hacen ataque por fuerza bruta para listar directorios no encontraran nada, por lo que tendremos que revisar el siguiente puerto. En donde se observa FTP anónimo al cual nos conectaremos para revisar hint lo que nos indica el mismo reconocimiento de Nmap, pero además revisaremos el directorio del FTP para revisar si hay archivos ocultos.

![Burry Friend 3](https://miro.medium.com/v2/resize:fit:471/1*T7gMg4nFQI586ReaB06uoA.png)

Al descargar hint obtenemos lo siguiente

![Burry Friend 4](https://miro.medium.com/v2/resize:fit:469/1*-d3FbqpPsCqFkTfFXXgQmA.png)

Un mensaje en texto plano y un mensaje cifrado en sha256 el cual corresponde a lo siguiente

![Burry Friend 5](https://miro.medium.com/v2/resize:fit:700/1*uxci_g-OX7UhlP0c2DE9Zw.png)

Además, encontramos la primera flag de la maquina como archivo oculto.

![Burry Friend 6](https://miro.medium.com/v2/resize:fit:299/1*wYXG0lKbKbhyTS8tBN3ZvQ.png)

Ya que tenemos esa palabra debemos entender que hay que ocuparlo en el servicio web el cual nos arrojara lo siguiente.

![Burry Friend 7](https://miro.medium.com/v2/resize:fit:700/1*so2cwg8iBtzf0-xnz2FgvA.png)

Ya que encontramos algo, aplicaremos herramientas para buscar directorios y archivos en la web encontrando lo siguiente.

![Burry Friend 8](https://miro.medium.com/v2/resize:fit:700/1*rqCP9ZcVm3Bb48xwr4Orew.png)

Como el mensaje del FTP decía “Find the secrets” revisaremos secrets.txt, el cual tiene un mensaje cifrado en base64.

RnIxM05kOjZ1akpNRg==

El cual nos arroja las siguientes credenciales:

Fr13Nd

6ujJMF

Revisamos upload.php el cual nos pide autenticación, ocupamos las credenciales obtenidas y entramos.

![Burry Friend 9](https://miro.medium.com/v2/resize:fit:439/1*DzVCWcgd8cXBb1OsEtbrfQ.png)

Teniendo en cuenta que hay un directorio llamado files vacío, entendemos que los archivos se subirán en ese directorio. Por lo que procederemos a subir la Shell reversa en donde nos encontraremos con una validación de Content-Type que debe ser image.

![Burry Friend 10](https://miro.medium.com/v2/resize:fit:491/1*cRCYLI2Fp6dn10sTwAq3Ng.png)

Después de obtener nuestra Shell reversa en el direcotrio /var/www encontraremos nuestra segunda flag oculta.

![Burry Friend 11](https://miro.medium.com/v2/resize:fit:435/1*yqWxRTJyQk3uyp6PzRXIhA.png)

Y dos archivos importantes.

![Burry Friend 12](https://miro.medium.com/v2/resize:fit:616/1*YFtEfkn-W7BBIr-f4rBXiw.png)

En donde la imagen oculta contiene un archivo oculto, así que deberemos ocupar herramientas de esteganografía para encontrar el archivo en donde la contraseña es el nombre de la imagen que no está oculta.

![Burry Friend 13](https://miro.medium.com/v2/resize:fit:626/1*dpdFjXBc2mctXnYwYunWZg.png)

Revisamos el archivo secrets2 el cual contiene credenciales del usuario Billie

![Burry Friend 14](https://miro.medium.com/v2/resize:fit:416/1*KlL4IhR1V1sxnbvgn5VVsg.png)

Nos logeamos como billie y encontraremos nuestra tercera flag en la carpeta en el escritorio

![Burry Friend 15](https://miro.medium.com/v2/resize:fit:391/1*Avohvta6rpuSYIjlQFQp0w.png)

Para elevar privilegios revisaremos si tenemos permisos de sudo y encontramos lo siguiente

![Burry Friend 16](https://miro.medium.com/v2/resize:fit:656/1*eK2FiVecmprjDYY_SFfB0w.png)

Buscamos documentación como escalar con Nmap no interactivo y encontramos la siguiente forma para elevar privilegios.

![Burry Friend 17](https://miro.medium.com/v2/resize:fit:624/1*6H1qyThkpP7_eJxiv64fMA.png)

Posterior a esto encontraremos nuestra última flag en /root/

![Burry Friend 18](https://miro.medium.com/v2/resize:fit:354/1*84VPS3pgBTz8SD_lcG0_MQ.png)

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