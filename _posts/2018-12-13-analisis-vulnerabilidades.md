---
title: "Reporte Responsable de Vulnerabilidades"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/malware.jpg"
---

Para ser sincero hace bastante tiempo que quería hacer esto, y como ya pueden intuir por el título, mi intención en este breve artículo es poder ayudar a las personas que se sienten perdidas muchas veces al no saber si el archivo que acaban de descargar es dañino para su computador, tablet, teléfono celular, etc., pero ojo, el que no seas un experto no quiere decir que sea fácil, esto está asociado a ciertas competencias que de igual forma son necesarias para poder desarrollar un análisis expedito, con esto me refiero a saber virtualizar, saber utilizar comandos, conocimientos básicos en **Linux** y/o **Windows**  y por sobre todo perderle el miedo de una vez por todas al **software malicioso**.

Y por si ya estás asustado, tranquilo, **no veremos lenguaje ensamblador (ASM)** porque ahí sí que podríamos escribir un libro completo e incluso quedaríamos chicos, mi intención es tener una mini guía de lo que se puede hacer antes de la ingeniería inversa a un malware, que de igual forma entregará datos relevantes para determinar si corro el riesgo de infectarme o no.

Creo que explicar lo que es un malware está demás, en especial para los lectores, amigos y miembros de [party-hack](https://twitter.com/Party_Hack){:target="_blank"}, sin embargo como todos en algún momento estuvimos investigando por nuestra cuenta cuando no sabíamos mucho y seguramente existe alguien que necesita saber y quiere conocer este tipo de conceptos ahora o en un futuro, ya que en algún momento de su vida se dio cuenta que esto es lo que le apasiona y quiere seguir aprendiendo, así que antes de iniciar no se debe olvidar que nadie es un experto, todos somos ignorantes y es deber nuestro contribuir y compartir lo poco que en la actualidad sabemos.

## Conceptos

**[Malware](https://es.wikipedia.org/wiki/Malware){:target="_blank"}**: Significa **malicious software** o **programa malicioso** para los que reprobaron inglés como yo, los cuales tienen por finalidad robar información confidencial, credenciales personales, destruir, dañar o cifrar archivos, etc., la gracia de estos software maliciosos es que son a gusto del consumidor, hay de muchos tipos y son desarrollados en distintos [lenguajes](https://es.wikipedia.org/wiki/Lenguaje_de_programaci%C3%B3n){:target="_blank"}, además hubo un periodo en que las víctimas más codiciadas eran las que utilizaban sistemas operativos Windows (ya que era y sigue siendo el [OS](https://es.wikipedia.org/wiki/Sistema_operativo){:target="_blank"} más popular), pero en la actualidad el mercado del malware ha saltado hacia los dispositivos móviles que son el activo más indispensable para la vida humana del siglo XXI.

De lo anterior y por una necesidad sumamente importante nace el **análisis de malware**, el cual podría definirse como el arte de la disección de software malicioso, para entender cómo funciona, cómo identificarlo y derrotarlo.

![Malware 1](/assets/images/post/2018/malware1.jpg)

Después de toda esta introducción comenzamos paso a paso a los que nos convoca.

## Procedimientos iniciales

Hay dos formas de enfrentarse a un software malicioso:

1. Verse afectado por un malware de un momento a otro.
2. Extraerlo de algún PC infectado para su análisis.

<p>Por este motivo, la información inicial siempre será relevante para el analista. Si te ves afectado por el punto número 1 una de las primeras cosas que debes hacer es verificar que tipo de cambio visual hay en el computador, por ejemplo; que las extensiones de los archivos cambien, desaparezcan del escritorio, que se abran múltiples ventanas, etc. Ahora te preguntaras porqué debo verificar la extensión de los archivos, esto se debe a que en el caso de ser atacado por un ransomware y detectar que los archivos se me han cifrado con una extensión *.*crypto por ejemplo, es posible utilizar google para buscar información con respecto a esta extensión y si hacemos una búsqueda rápida podríamos detectar a que nos enfrentamos ya que quizás no seas el único afectado o alguien ya soluciono el tema.</p>

Si quieres conocer más de tipos de extensiones utilizadas por diferentes ransomware te recomiendo visitar el repo de **Kinomakino** el cual posee 191 extensiones diferentes utilizadas por ransomware en este [enlace](https://github.com/kinomakino/ransomware_file_extensions/blob/master/extensions.csv){:target="_blank"}.

Ahora, si la opción a la que te enfrentas es la dos, procura ser muy cuidadoso con la extracción del malware y su posterior descarga en otro equipo, hay gente que hace doble click en un archivo con los ojos, todo un arte.

Para realizar análisis de malware hay dos tipos, uno es el [análisis estático](https://www.welivesecurity.com/la-es/2014/01/21/analisis-estatico-arquitectura-x86/){:target="_blank"} y el otro es el [dinámico](https://www.welivesecurity.com/la-es/2011/12/22/herramientas-analisis-dinamico-malware/){:target="_blank"}, la diferencia entre uno y otro es básicamente que en el estático se estudia composición, código, metadatos, entre otros aspectos y en el dinámico se estudia ejecutando el malware, es decir, analizando mientras este funciona.

## Configuración de laboratorio

Para poder analizar necesitamos un entorno de trabajo, este entorno puede ser configurado por el propio analista, lo primero que puedes hacer es instalar y ejecutar algún software de virtualización como [VMware](https://www.vmware.com/cl.html){:target="_blank"} o [VirtualBox](https://www.virtualbox.org/){:target="_blank"} e instalar algún OS para dejarlo de laboratorio, por lo general utilizar un entorno de Windows puede ser útil debido a que hay muchas amenazas para estos sistemas.

![Malware 2](/assets/images/post/2018/malware2.jpg)

**Nota**: *Siempre ten en cuenta de donde se extrajo el archivo, quizás te entregue más información con respecto a su comportamiento o modo de operar en algún entorno de trabajo.*

Una vez montada alguna imagen ISO (Windows en este caso), debemos tener en consideración lo siguiente:

- **Snapshot o clone**

Toma un snapshot o clona tu máquina virtual, esta no debe ser única por ende siempre ten un respaldo para poder ir comparando comportamientos o simplemente volver a cero luego del análisis.

![Malware 3](/assets/images/post/2018/malware3.jpg)

**Ejemplo de snapshot en VMware**

- **Deshabilitar USB**

	Hay malware que se propaga por medios de extracción USB si no eres cuidadoso quizás puedas infectar este tipo de dispositivos de estar conectado al momento del análisis. (También puedes ocupar un USB para descargar el bicho que quieres analizar, luego de eso deshabilitar)

- **Deshabilitar tarjetas de red**

	Ídem a lo anterior, y propagarse por red es aún más engorroso.

    Ningún tipo de conexión con el anfitrión

El anfitrión es el computador base, desde donde virtualizas, trata de que al momento del análisis no existan carpetas compartidas donde un malware podría pivotear entre equipos.

Una vez terminado esto ya tenemos nuestro laboratorio para el análisis, pero no solamente debemos utilizar este sistema operativo (Windows) para trabajar, es necesario también apoyarse de otros como por ejemplo **Kali Linux**, (a que no se lo esperaban J ) y como muestra para analizar utilizaremos un **bicho que envía múltiples correos electrónicos**.

**Análisis**

Tenemos un bicho en nuestro poder, lo copiaremos en kali  y lo primero que haremos es utilizar el comando “file” el cual sirve para determinar tanto tipo como formato de un archivo:

<p># file &lt;archivo&gt;</p>

![Malware 4](/assets/images/post/2018/malware4.jpg)

Con esto ya vamos obteniendo antecedentes, imaginen que están en la fase de reconocimiento jejeje

Luego de esto, utilizaremos el comando “strings”, este comando es útil si tienes un archivo binario y quieres ver los caracteres imprimibles o legibles de dicho archivo, como se muestra a continuación:

Ejecutamos.

<p># man strings</p>

Esto nos mostrará cierta información referente al comando, sus funcionalidades y opciones a utilizar, pero en este punto debo ser sincero, jamás he ocupado todas las opciones, así que les toca investigar sobre cada una de ellas, pero lo principal es analizar un binario y ver si hay algo de utilidad dentro de lo que es legible o entendible para un analista sin ser experto, aunque como dije anteriormente, de todas formas necesitarás acrecentar tus competencias para poder profundizar más al respecto. La buena noticia sigue siendo que tienes tiempo para seguir aprendiendo. //También puedes ocupar strings –h si quieres ver sólo las opciones.

Luego ejecutamos:

<p># strings &lt;archivo&gt;</p>

![Malware 5](/assets/images/post/2018/malware5.jpg)

![Malware 6](/assets/images/post/2018/malware6.jpg)

En esta parte debemos inspeccionar cada resultado con la finalidad de buscar posibles password, indicios de algún ciclo en la programación, quizás algún DLL, registros que pueda llegar a utilizar, etc. Si tienes dudas apóyate de google, un motor de búsqueda siempre será nuestro mejor aliado.

Si queremos más antecedentes técnicos podemos recopilar los metadatos del archivo para ello hay muchas herramientas que nos pueden servir, y como estamos en kali y ésto tiene que empezar a avanzar más rápido (ya que voy muy lento) utilizaremos [exiftool](https://en.wikipedia.org/wiki/ExifTool){:target="_blank"}.

![Malware 7](/assets/images/post/2018/malware7.png)

Hasta aquí ya vamos bien, pero ahora utilicemos Windows. Tenemos a nuestro bicho esperando por ser analizado en nuestro laboratorio de trabajo, antes de comenzar con el análisis dinámico, fíjate en cada detalle, tienes un OS limpio, con mínimos procesos corriendo, casi ningún archivo en el escritorio, más limpio que el PC del creador de Ccleaner., así que ahora utilizaremos [Regshot](https://sourceforge.net/p/regshot/wiki/Home/){:target="_blank"} una herramienta muy buena y de código abierto (LGPL), la que nos permitirá comparar que modificaciones hay antes y después de la ejecución de nuestro bicho, generando además una especie de reporte para evidenciar de mejor forma las comparaciones.

//Revisa los procesos del sistema limpio, esto para compararlos después una vez infectada la máquina.

El siguiente paso  será abrir la herramienta y tomar un primer “shot” del sistema limpio.

![Malware 8](/assets/images/post/2018/malware8.jpg)

**Nota**: *En esta parte podemos apoyarnos del administrador de tareas para ver procesos, lo cual es muy útil siempre o utilizar una que otra herramienta de [Sysinternals](https://docs.microsoft.com/en-us/sysinternals/){:target="_blank"} como por ejemplo “[Process Monitor](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon){:target="_blank"}”*.

Procura siempre utilizar la opción de tomar **shot** y guardar, ya que posterior a esto haremos la comparación, así que una vez tomada y guardada esta “captura” ejecutamos el bicho malicioso y esperamos algunos minutos para dejar que haga su trabajo, recuerda que no todos funcionan de la misma forma, hay unos 0-day que incluso tienen fecha de iniciación y ahí sí que se pone fea la cosa.

![Malware 9](/assets/images/post/2018/malware9.jpg)

Guardamos el archivo y listo, como ya notaste utilizaremos para este caso un bicho que establece conexiones, ósea es de red. Ahora ejecutamos este bicho.

![Malware 10](/assets/images/post/2018/malware10.jpg)

Luego de ejecutarlo esperamos unos minutos y tomamos el segundo “**shot**” mismo procedimiento, presionamos “**second shot**”, guardamos, le ponemos nombre al archivo y esperamos, una vez listo esto presionamos el botón “compare”.

![Malware 11](/assets/images/post/2018/malware11.jpg)

Esto casi de forma instantánea nos mostrará un **txt** muy interesante, el cual tiene las comparaciones de los dos shots:

![Malware 12](/assets/images/post/2018/malware12.jpg)

Aquí podemos destacar por ejemplo que se borraron dos llaves:

———————————-

Keys deleted: 2

———————————-

HKU\S-1-5-21-2417776187-143840447-2122787933-1000\Software\Microsoft\Windows\CurrentVersion\Internet Settings\5.0\Cache\Extensible Cache\MSHist012018092420181001

HKU\S-1-5-21-2417776187-143840447-2122787933-1000\Software\Microsoft\Windows\CurrentVersion\Internet Settings\5.0\Cache\Extensible Cache\MSHist012018100820181009

Se modificaron 15 valores:

![Malware 13](/assets/images/post/2018/malware13.jpg)

Entre muchos cambios más, si te vas al final del **txt** encontraras el total, que para este caso fueron:

———————————-

**Total changes: 95**

———————————-

Ahora te toca empezar a investigar, ya que nada es 100% automático, estudia los cambios, lo que se eliminó, lo que se modificó y con qué fines, por ejemplo que registros del sistema fueron los primeros en ser afectado para darte una idea de que permisos obtuvo el malware en cuestión.

Ahora apóyate de la comparación de procesos (que supongo no se te olvido hacerlo al principio), y revisa ¿qué cambios notas?

![Malware 14](/assets/images/post/2018/malware14.jpg)

Muy bien, lo hallaste, hay tres procesos raros que no estaban al principio y para más remate con privilegios de admin, quizás buscar alguna información de ellos en internet ayuda a la investigación.

Algunas veces no te enfrentaras al malware como tal, en ocasiones puedes que te topes con el archivo que descarga uno y para esto debes poder identificar que peticiones realiza, donde se quiere conectar y que descarga finalmente, pero si recuerdas al principio te comenté que tienes que deshabilitar las tarjetas de red por seguridad, ¿verdad?, pues no hay problema, existen soluciones para estos dilemas y son los **FakeDNS**.  Estas herramientas permiten visualizar solicitudes como si estuvieras en la Internet normal, respondiendo lo que se le solicite, para este ejemplo utilizaremos “[ApateDNS](https://www.fireeye.com/services/freeware/apatedns.html){:target="_blank"}” al controlar las repuestas podemos ver donde el bicho quería conectarse, quizás no descargue el malware ya que obviamente está en un ambiente controlado, pero si nos puede entregar cierta información con respecto a dónde quiere ir y detectar conexiones remotas indeseadas.

![Malware 15](/assets/images/post/2018/malware15.jpg)

El dominio de la imagen fue adulterado a modo de ejemplo.

También puedes apoyarte de [Wireshark](https://cso.computerworld.es/tendencias/que-es-wireshark-asi-funciona-la-nueva-tendencia-esencial-en-seguridad){:target="_blank"} este software open source para analizar tráfico tiempo real, donde podrás visualizar de una forma amigable lo que sucede en la red, para esto necesitaras habilitar el adaptador de red, así que hay un riesgo, pero así es la vida, un riesgo de todos modos jeje.

![Malware 16](/assets/images/post/2018/malware16.jpg)

Bueno, y si llegamos hasta este punto y aún no eres capaz de decir si el archivo que descargaste es un malware o no, perfecto, entonces debes pedir ayuda a los expertos y cuando digo pedir ayuda no me refiero a llamarlos por teléfono o preguntarle al computin del grupo, simplemente debes buscar la ayuda de [sandbox](https://es.wikipedia.org/wiki/Sandbox){:target="_blank"} online.

Existen hartos en el mercado pero uno de los que más me agrada es [https://valkyrie.comodo.com/](https://valkyrie.comodo.com/){:target="_blank"}

![Malware 17](/assets/images/post/2018/malware17.jpg)

No, no me equivoque, el correo es de [10 minute mail](https://10minutemail.com/10MinuteMail/index.html?dswid=-264){:target="_blank"}, así que si quieres ocúpalo, la clave es 1qazxsw2

Para subir un archivo basta con seguir estas instrucciones destacadas por el óvalo azul:

![Malware 18](/assets/images/post/2018/malware18.jpg)

![Malware 19](/assets/images/post/2018/malware19.jpg)

También hay opción de exportar los resultados, dentro del reporte encontraras un análisis humano en caso de que este bicho haya sido estudiado anteriormente.

![Malware 20](/assets/images/post/2018/malware20.jpg)

Otra herramienta online muy buena es [any.run](https://any.run/){:target="_blank"}, la cual permite interactivamente analizar un malware gracias a su versión gratuita.

![Malware 21](/assets/images/post/2018/malware21.jpg)

**Extra**: *Una utilidad muy buena pero cuando hablamos de ransomware es la herramienta online “[ID Ransomware](https://id-ransomware.malwarehunterteam.com/index.php?lang=es_ES){:target="_blank"}” la cual permite identificar a que bicho te enfrentas, pero ojo, no confundir con un sandbox online, este solo te dirá el nombre del ransomware con el que te infectaste para seguir con tu análisis*.

**Extra 2**: *También hay una web llamada “[no more ransomware](https://www.nomoreransom.org/decryption-tools.html){:target="_blank"}” que en el mejor de los casos te ayudara a descifrar alguno que otro archivo atacado por estos bichos*.

Bueno, creo que con eso estaríamos, serian 15.000 pesos por el tutorial y ya es tarde para escapar porque tu IP quedo registrada y tenemos una tecnología de punta capaz de dar con cualquier individuo en cuestión de segundos, así que vamos soltando los morlacos…

Ya bueno, no mires con cara de “no tengo ni un peso” por esta vez quedará gratis, todo sea por contribuir.

Quizás en este punto estés pensando, “*ya pero… ¿de dónde saco bichos?*” Mi querid@ amig@ si quieres una base de datos donde puedas conseguir estos bichos pero *solo con fines educativos*, puedes encontrar algunos en [https://malwares.underc0de.org/](https://malwares.underc0de.org/){:target="_blank"} debes tener en cuenta que cada malware es distinto y funciona de forma distinta por ende, debes configurar un buen laboratorio de pruebas para cada caso. Además, no olvides desactivar cualquier motor antivirus que tenga tu computador antes de la descarga.

![Malware 22](/assets/images/post/2018/malware22.png)

Así como todo en la vida es práctica, analizar estos archivos no solo te ayudará a entrenar sino que te beneficiará personalmente en seguir creciendo como profesional.

En resumen, quiero que sepas que si te vas a iniciar en este mundo, como consejo debes empezar a interiorizarte con algunos conceptos como: malware (si, entenderlo bien), ingeniería inversa, código malicioso, análisis forense, sandbox por dar un pequeño empujón, y si quieres seguir aprendiendo te recomiendo leer la biblia del análisis de malware jejeje “**practical malware analisys**”, la cual puedes descargar del siguiente [link](https://www.sombrero-blanco.com/descargas/){:target="_blank"}.

![Malware 23](/assets/images/post/2018/malware23.png)

Si todavía requieres ayuda, estudiar sobre herramientas o tienes dudas sobre algo, hay un foro bastante antiguo que te puede servir, me refiero a [indetectables](https://indetectables.net/){:target="_blank"}, aquí encontraras a muchas personas con la misma pasión entre otras cosas.

Para terminar, siéntete en completa libertad de experimentar, no importa si te equivocas, si te sale mal, si al tipo del tutorial le funciona y a ti no, hay millones de formas más. Para llegar a un objetivo existen diferentes caminos y serás más sabio si logras recorrer más de uno para alcanzar tu destino.

<!– Te dejo invitado a comentar sobre otras herramientas o métodos que podrían servir para un análisis de malware sin ser experto, como comunidad hay que apoyarnos y quizás en algunos años tu respuesta pueda ayudar a otros a comenzar.–>

**Happy Party Hacking**  