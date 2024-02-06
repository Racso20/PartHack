---
title: "Hackaton Telefonica 2019 – Reto P4st3b1n"
author: "Ricardo Monreal"
header: 
  teaser: "/assets/images/ctf.png"
---

Este desafío parte por un link a un supuesto “leak” en pastebin https://pastebin.com/6f090H8Z

![Paste Bin 1](/assets/images/post/2019/paste1.png)

Este texto es una serie de caracteres que asimilan ser un texto en base64, pero cuando se intenta decodificar se entienden pocas palabras.

![Paste Bin 2](/assets/images/post/2019/paste2.png)

Al revisar que las primeras 2 letras son PK y luego aparece algo similar a un nombre de archivo “flag.txt” podemos pensar que se trata de un archivo en vez de un texto por lo que realizamos la decodificación hacia un archivo y luego lo identificamos con file:

![Paste Bin 3](/assets/images/post/2019/paste3.png)

Ahora sabemos que el archivo es un archivo .zip, pero al intentar descomprimirlo vemos que necesita una clave que no tenemos.

![Paste Bin 4](/assets/images/post/2019/paste4.png)

Con esto necesitamos usar un diccionario, y buscando en Kali tenemos el rockyou (un clásico en los diccionarios) por lo que usamos alguna de las herramientas de revisión de las claves:

![Paste Bin 5](/assets/images/post/2019/paste5.png)

Al ejecutar la fuerza bruta tenemos que la clave es “Inparadise”

![Paste Bin 6](/assets/images/post/2019/paste6.png)
