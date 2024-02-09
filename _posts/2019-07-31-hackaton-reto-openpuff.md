---
title: "Hackaton Telefonica 2019 – Reto 0p3npuff"
author: "31m0"
header: 
  teaser: "/assets/images/ctf.png"
categories:
  - WriteUp
---

Para resolver este reto de stego es necesario, instalar openpuff de la pagina https://www.embeddedsw.net/OpenPuff_download.html

![Open Puff 1](/assets/images/post/2019/open1.png)

Si se utiliza binwalk no aparece nada…

![Open Puff 2](/assets/images/post/2019/open2.png)

Utilizamos file para ver si encontramos algo… pero sin resultados

![Open Puff 3](/assets/images/post/2019/open3.png)

Utilizamos strings para buscar algo interesante…

![Open Puff ](/assets/images/post/2019/open4.png)

Pero aun no encontramos nada…

Viendo el video aparece un extraño numero 333.333.333,33

![Open Puff 5](/assets/images/post/2019/open5.png)

Este numero nos servirá para poder abrir nuestro archivo oculto, lo utilizaremos al final, haremos una búsqueda por el nombre del archivo para ver que nos muestra.

![Open Puff 6](/assets/images/post/2019/open6.png)

![Open Puff 7](/assets/images/post/2019/open7.png)

Lo descargamos y ejecutamos

![Open Puff 8](/assets/images/post/2019/open8.png)

Se nos abrirá una aplicación, la utilizaremos para encontrar el archivo oculto… en cryptography colocamos el numero que encontramos 333.333.333,33 sacamos el ticket b y c

![Open Puff 9](/assets/images/post/2019/open9.png)

Le damos unhide y seleccionamos la ubicación… y nos abrirá un archivo con el  flag.txt

![31mo](https://www.hackthebox.com/badge/image/23069)

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