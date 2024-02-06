---
title: "Hackaton Telefonica 2019 – Reto Fr34kySh4rk"
author: "31m0"
header: 
  teaser: "/assets/images/ctf.png"
---

En este reto nos entregan el archivo fr3akysh4rk.pcapng el cual corresponde a un archivo de captura de trafico que podemos abrir con wireshark, al abrirlo nos aparece el siguiente error

![Freaky Shark 1](/assets/images/post/2019/freaky1.png)

Si lo ignoramos y buscamos en la captura no nos llevara a ningun lado si utilizamos follow stream no nos arroja ningún dato interesante….

![Freaky Shark 2](/assets/images/post/2019/freaky2.png)

Bueno como wireshark no nos entrega nada interesante lo analizaremos con otras herramientas utilizaremos file para analizarlo

![Freaky Shark 3](/assets/images/post/2019/freaky3.png)

Nos dice que efectivamente es una captura de trafico… veremos que nos arroja al utilizar strings….

![Freaky Shark 4](/assets/images/post/2019/freaky4.png)

Afinaremos un poco la búsqueda, para ello utilizaremos strings y añadiremos el comando grep, con el cual filtraremos por las primeras 3 letras del flag

![Freaky Shark 5](/assets/images/post/2019/freaky5.png)

y efectivamente nos entrega el flag del reto

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