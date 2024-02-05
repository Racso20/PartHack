---
title: "Reporte Responsable de Vulnerabilidades"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/smishing.jpg"
---

Hola comunidad,

Luego de leer un par de publicaciones en linkedin, proponer ideas de un bugbounty para pymes en Chile de forma gratuita sin mucha aceptación por miedo o quizás desconocimiento, y hablar en varias ocasiones con colegas de como reportar vulnerabilidades de forma responsable, me tome un poco de tiempo fominguero para escribir estas pocas lineas de texto y explicar mi experiencia en este tipo de actividades.

Comencé en esto por ahí por el 1999, cuando recien estaban los sistemas de reserva en linea para los resort, y como era un tanto inquieto, realicé un upload de un exe en un sistema de upload de un reconocido hotel de México, y adivinen, plaaaaaf, la adrenalina corría por mis venas, tenia el control total del server, no voy a dar el nombre del hotel, pero me contacté por latinchat de StartMedia, si mal no recuerdo, con la encargada de informática de esos año y reporté el problema, cuando me pidió verificar el compromiso y abrí la bandeja del CDROM me sentía un dios jajajajaja un amo de tomo y lomo…, que buenos tiempos. Pero en fin, luego hicimos buenas migas y estuvimos en contacto por muchos años. El tema es que ese fue mi primer reporte responsable de una vulnerabilidad, y si bien es cierto en ese momento era solo un juego, años mas tarde me dedico 100% a lo que me apasiona, “romper cosas”.

Hoy veo a muchos colegas realizando esta actividad con una serie de problemas, sin ir mas lejos, hace unos años atrás apareció una iniciativa bastante interesante en Chile, de la mano de Fernando Lagos, llamada Secureless.org, en donde la comunidad reportaba brechas de seguridad y realizaban el “intento” de contactar a los afectado, que en muchas ocasiones no se llegaba a puerto por falta de información pública del responsable al cual se le debía reportar. Ahí es donde está el primer problema con el cual nos vamos en enfrentar, quizás hoy se hace más sencillo solucionar esto, ya que existen muchas redes sociales en donde podemos hacer OSINT y buscar al responsable de la organización o al encargado de seguridad, aquí les dejo algunos tips de como buscarlos.

- Linkedin, en donde gran parte de los profesionales ponen sus cargos y organizaciones donde trabajan (Aplica a Público y Privado)
- Crawling del sitio web de la organización, en búsqueda de correos electrónicos para hacer mas sencilla la tarea (Aplica a Público y Privado)
- Buscar un número de teléfono y llamar directamente, para solicitar hablar con el encargado de informática o seguridad (Explicar bien que no es el jefe de los guardias jajajajaja)
- Comunicarse con el CSIRT del estado a [csirt@interior.gob.cl](mailto:csirt@interior.gob.cl){:target="_blank"}, ellos podrán indicar los contactos directos de las diferentes unidades de cada ministerio encargado de la seguridad informática (Solo Público)

Con esto ya pueden acotar un poco la búsqueda del responsable.

Solo como aclaración para poder continuar, el objetivo de los que les voy a contar es para reportar vulnerabilidades de forma responsable, eso quiere decir que mi mente no está pensando en lucrar, sino en entrenarse con la realidad y no con laboratorios pre configurados a prueba de certificaciones, esta es mi manera de entretenerme y entrenarme.

Bueno, una vez que ya tienen a su target identificado, yo utilizo un formato que me ha dado buenos resultados para que no me agarren a chuchadas y me traten como delincuente, a continuación se los explico.

Estimad@ **“NOMBRE_DEL_TARGET”**, tu nombre me lo dio **“NOMBRE_DEL_REFERIDO”** mediante **“REDSOCIAL O METODO DE BUSQUEDA”**. Mantengo en copia a CSIRT del Interior.

Con esto el “TARGET” puede saber por donde lo identificamos y genera la primera confianza de transparencia, como así tambien nombrar a referidos que nos dieron su nombre como encargada. Si está reportando al una entidad de gobierno, mantengan en copia al CSIRT, esto generará seriedad, y si es a un privado, copien al jefe del “TARGET”, esto generará compromiso. Recuerden utilizar un correo serio, no un **“supersayayin_hacker_blackhat_anonymous@gmail.com”**

Mi nombre es **“NOMBRE_COMPPLETO_DEL_QUE_REPORTA”**, te contacto ya que encontré una vulnerabilidad en el sitio web de **“INSTITUCIÓN_AFECTADA”** que a continuación detallo:

Presentarse con el nombre completo genera transparencia y luego ir directo al grano, no es necesario mas bla bla, nuestro objetivo es reportar y listo.

Para el reporte técnico me voy a poner en el supuesto de que se encontró una vulnerabilidad en un aplicativo web, ya que están de moda y son los objetivos mas comunes para entrenarse.

**Ethical hacker:** Pablo Ramirez Hoffmann

(Identifiquen quien fue el o los integrantes que descubrieron el bug)

**Empresa que reporta:** Pentest SPA

(Ojalá puedan reportar a través de una empresa u organización, esto le dará mas seriedad)

**Empresa Afectada:** GOBIERNO

(Identifiquen claramente cual es la organización afectada por el bug)

**Host afectado:** http://www.depreca.cl

(Indiquen cual es el dominio afectado, para que sea mas fácil su identificación por parte del TARGET, muchas veces las organizaciones tienen mas de un dominio)

**URI & Variable Afectada:**

- /virtual/inicio/inicio2/SERVICIOS/imponentesonline/logeo.asp
	- link (Variable)
	- permisos (Variable)

(Es muy importante que detallen bien los componentes del aplicativo web en donde encontramos el bug, así será mucho mas facil para el afectado poder identificarlo)

**Tipo de vulnerabilidad:** Cross Site Scripting

(Indiquen el tipo de vulnerabilidad que descubrieron, así el TARGET puede determinar a que se ve enfrentado)

**Vector de ataque:** Remoto

El vector de ataque se refiere a como se deben conectar al sitio web para poder realizar el ataque, existen 4 tipos según CVSS, los cuales son Remoto, Adyacente, Local o física.

**Nivel de Severidad:** Crítico

El nivel de criticidad está dado por varias variables, en este caso utilizo CVSS y para calcularlo se realiza mediante la calculador de [FIRST](https://www.first.org/cvss/calculator/3.0){:target="_blank"}

**Complejidad de explotación:** Baja

La complejidad de acceso también lo entrega CVSS y pueden interiorizarse mas en la documentación del estándar [https://www.first.org/cvss/specification-document](https://www.first.org/cvss/specification-document){:target="_blank"}

**Sistema afectado:** Aplicativo Web

Esto puede varias según su objetivo de prueba, pueden ser servicios, sistemas operativos, aplicativos web, equipos de comunicación, etc. Es ideal poner algún screenshot en donde el TARGET pueda visualizar el sitio web afectado, a veces es mas fácil para ellos mirarlos.

**Método de explotación:** GET

Con esto indicamos cual es el método HTTP que utilizamos para explotar el bug y va a depender de cual es el tipo de sistema afectado y su vector de ataque.

**PoC Realizada:** modificación del valor de la variable permiso=1 a permiso=<script>alert(‘XSS’);</script>.

Esta es la prueba de concepto que utilizamos para verificar el bug y agregamos un screenshot o video del payload enviado y con los resultados obtenidos.

**La vulnerabilidad podría ser utilizada para generar ataques de “VARIANTES_DE_ATAQUE_QUE_PUEDEN_SER_APROVECHADO_POR_EL_BUG” con el dominio «DOMINIO_AFECTADO”, entre otro tipo de ataques.**

(Con esto le damos luces a nuestro TARGET de como los delincuentes informáticos podrían aprovechar el bug y causar un poco de pánico para que consideren el reporte)

**La intensión de esta alerta es “solo” reportar la vulnerabilidad, para que el fabricante, desarrollador, administrador de sistema o encargado de seguridad tome las acciones pertinentes, la vulnerabilidad no se ha reportado públicamente y no se hará hasta que se tomen las medidas correctivas o a menos que el afectado indique lo contrario.**

Con esto le indicamos a nuestro TARGET que nuestro objetivo es solo reportar y ayudar, no se explayen mucho, no es necesario y finalmente cierren el texto con que la vulnerabilidad no se hará pública hasta que sea remediada, no pongan limites de fecha ni nada, eso suena matonezco.

Luego mantengan un dialogo cercano el TARGET, que el ego no supere al espirito de ayudar y aportar con su granito de arena a la sociedad…

Espero les sirva.

Que el ciber dios los mantenga libre de malware y mantengan su mente inquieta, recuerden que no están haciendo nada malo, es solo entrenamiento y un aporte para la sociedad.
