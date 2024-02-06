---
title: "Hackaton Telefonica 2019 – Reto 0p3npuff"
author: "31m0"
header: 
  teaser: "/assets/images/ctf.png"
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