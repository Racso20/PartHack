---
title: "M4ul3 H4ck – Easy - Peace"
author: "Oscar Bravo"
header: 
  teaser: "/assets/images/post/2022/maule.jpg"
categories:
  - WriteUp
tags:
  - MauleHack
  - CTF
---

Lo único que nos entregan acá es un hash 7ab1156ebd2c00567186a3985e990382 por lo que usamos hash-identifier para qsaber que hash es

	hash-identifier 7ab1156ebd2c00567186a3985e990382

El cual nos devuelve que es un MD5, buscando en internet utilizamos varios decrypt pero sin existo hasta que encontramos la siguiente pagina https://md5.gromweb.com/ quien nos solucionó el hash y nos entregó la flag MH{hola}


![Racso](https://www.hackthebox.com/badge/image/159593)