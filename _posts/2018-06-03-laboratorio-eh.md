---
title: "Laboratorio de Hacking Ético básico"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/labeh.jpg"
categories:
  - Tecnología
---
	

Cuando hablamos de hacking ético nos referimos a la acción de efectuar pruebas de intrusión controladas sobre  sistemas  informáticos;  es  decir  que  el  consultor  o pentester, actuará desde el punto de vista de un cracker, para tratar de encontrar vulnerabilidades en los equipos auditados que puedan ser explotadas, brindándole  en  algunos  casos acceso  al  sistema  afectado inclusive;  pero  siempre  en  un ambiente  supervisado,  en  el  que  no  se  ponga  en  riesgo  la operatividad  de  los servicios informáticos de la organización cliente.

Es  importante  enfatizar  que  aunque  es  indudable  que  el  pentester  debe  poseer conocimientos  sólidos  sobre  tecnología  para  poder  efectuar  un  hacking ético, saber de informática no es suficiente para ejecutar con éxito una auditoría de este tipo.  Se  requiere además  seguir  una metodología  que permita  llevar  un  orden  en nuestro  trabajo  para  optimizar el tiempo  en la  fase  de  explotación,  además  de aplicar el sentido común y experiencia.

Fases del hacking Tanto el auditor como el cracker siguen un orden lógico de pasos al momento de ejecutar un hacking, a estos pasos agrupados se los denomina fases. Existe un consenso generalizado entre las entidades y profesionales de seguridad informática de que dichas fases son 5 en el siguiente orden:  

1. Reconocimiento
2. Escaneo
3. Obtener acceso
4. Mantener acceso
5. Borrar huellas

Usualmente dichas fases se representan como un ciclo al que se denomina comúnmente círculo del hacking con el ánimo de enfatizar que el cracker luego de borrar sus huellas puede afectar el sistema, el auditor de seguridad informática que ejecuta un servicio de hacking ético presenta una leve variación en la ejecución de las fases de esta forma:  

1. Reconocimiento
2. Escaneo
3. Obtener acceso
4. Escribir Informe
5. Presentar Informe

De esta manera el hacker ético se detiene en la fase 3 del círculo del hacking para reportar sus hallazgos y realizar recomendaciones de remediación al cliente.

![Etico 1](/assets/images/post/2018/etico1.png)

En este laboratorio se hará la fase 1 la cual consisten en hacer reconocimiento a determinado cliente o red. **FASE 1** El reconocimiento o footprinting, es la primera fase en la ejecución de un hacking ético o no ético y consiste en descubrir la mayor cantidad de información relevante de la organización cliente o víctima.

- **Reconocimiento pasivo:** Cuando no se tiene una interacción directa con el cliente o víctima. Por ejemplo, entramos a un buscador como Google e indagamos por el nombre de la empresa auditada, entre los resultados conseguimos el nombre de la página web del cliente y descubrimos que el nombre del servidor web, luego hacemos una búsqueda DNS y se obtienela dirección IP de ese servidor. También se puede buscar información del cliente o en empresa por medio de las redes sociales como Facebook, twitter, linkedin, entre otros.
- **Reconocimiento activo:** En este tipo de reconocimiento hay una interacción directa con el objetivo o víctima. Ejemplos de reconocimiento activo:
- **Barridos de ping:** para determinar los equipos públicos activos dentro de un rango de IP’s.
- **Conexión a un puerto de un aplicativo:** para obtener un banner y tratar de determinar la versión.
- **Uso de ingeniería social:** para obtener información confidencial.
- **Hacer un mapeo de red:** para determinar la existencia de un firewall o router de borde.

Who-Is El Who-Is es un protocolo que permite hacer consultas a un repositorio en Internet para recuperar información acerca de la propiedad de un nombre de dominio o una dirección IP. Cuando una organización solicita un nombre para su dominio a su proveedor de Internet (ISP), éste lo registra en la base Who-Is correspondiente. En el caso de los dominios de alto nivel (.com, .org, .net, .biz, .mil, etc.) es usualmente el ARIN (American Registry for Internet Numbers) quien guarda estainformación en su base   Who-Is; pero en el caso de los dominios de países (.ve, .ec, .co, .us, .uk, etc.) quien guarda la información normalmente es el NIC   (Network Information Center) del país respectivo.   Se puede consultar tanto de la página de internet o por medio del comando. **PROCEDIMIENTORECONOCIMIENTO – ESCANEO google, nslookup whois. Aplicativo como maltego.Google** Buscar por el nombre de la empresa víctima, la cual será por ahora el proyecto Scanme de Nmap.   Abrir google y buscar “scanme nmap” 

![Etico 2](/assets/images/post/2018/etico2.png)

Arroja cerca de 8.210 resultados relacionadas con la organización NMAP, pero, la que interesa es scanme.nmap.org.   Luego se realizará la resolución de nombres DNS. **nslookup** Este comando se utiliza para hacer consulta de nombres. Abrir la terminal de Kali-Linux y escribir: *nslookupscanme.nmap.org*

![Etico 3](/assets/images/post/2018/etico3.png)

<p>El resultado es una dirección Ipv4 (45.33.32.156) Ahora se realizará 2 tipos de consultas, el servicio de nombres NS y el servicio de correo MX para el dominio de nuestro objetivo, en este caso nmap.org set type = [ NS | MX ] Escriba: set type=NS nmap.org</p>

![Etico 4](/assets/images/post/2018/etico4.png)

En la Figura se observa que al establecer el tipo de consulta como NS, nos devuelve información respecto a los servidores de nombres para el dominio en que se encuentra nuestro objetivo.   Escriba: set type=MX nmap.org

![Etico 5](/assets/images/post/2018/etico5.png)

La figura muestra la consulta tipo MX (mail exchanger), brinda además información acerca de quiénes son los servidores de correo para dicho dominio. Estas simples consultas adicionales nos reportan valiosa información de la red pública de nuestro objetivo, como por ejemplo:

- Que en realidad el dominio nmap.org está alojado en un servidor de hosting externo provisto por la empresa Linode.
- Que el servicio de correo es provisto por el servidor es googlemail.com con IP diferente a la del servidor scanme.nmap.org

**Whois** Por ejemplo se va a consultar sobre la empresa Microsoft, como su dominio es microsoft.com entonces sepuede acudir al ARIN para nuestra consulta. En internet podemos consultar páginas como http://whois.arin.net y https://www.whois.net/ entre otras. Para ello apuntamos nuestro navegador a http://whois.arin.net y en la caja de texto denominada “SEARCH WHOISRWS” ingresamos el nombre de la organización, para este ejemplo: Microsoft

![Etico 6](/assets/images/post/2018/etico6.png)

![Etico 7](/assets/images/post/2018/etico7.png)

![Etico 8](/assets/images/post/2018/etico8.png)

Nos arroja resultados acerca de las redes, números de sistemas autónomos y clientes. Si abrimos la primera red nos dará más información.

![Etico 9](/assets/images/post/2018/etico9.png)

Como por ejemplo el rango de direcciones Ips, el día de registros, país, entre otros.   Ahora utilizando la otra página de internet: https://www.whois.net/

![Etico 10](/assets/images/post/2018/etico10.png)

También nos arroja información del dominio, ciudad, código postal, nombre del administrador, teléfono, etc.   Utilizando el comando whois Para saber la dirección Ip de una página se tiene que hacer una conexión mediante el comando ping.   Escriba: ping www.microsoft.com

![Etico 11](/assets/images/post/2018/etico11.png)

Después de obtener la dirección Ip detenga el escaneo de ping. Escriba: whois 23.218.210.155

![Etico 12](/assets/images/post/2018/etico12.png)

![Etico 13](/assets/images/post/2018/etico13.png)

Da como resultado nombre de la red, días de registros, direcciones, código postal, ciudad, país, entre otros. Programa maltego Aplicaciones–> Kali Linux–> Recopilación de información–> Analisis DNS–>Maltego Aplicaciones–> Kali Linux–>Top 10 security tools–> Maltego

1. Cuando se inicia, toca registrarse para poder usar este programa.
2. Luego agregamos un dominio, en este caso es google.com
3. Nos arroja varios resultados, como por ejemplo picasa.google.com, earth.google.com, docs.google.com, play.google.com, etc. Y así sucesivamente podemos trabajar con uno de estos subdominios.

![Etico 14](/assets/images/post/2018/etico14.png)

![Etico 15](/assets/images/post/2018/etico15.png)

Trabajaremos con www.google.com y nos da como resultado varias direcciones de dominios por ejemplo la 173.194.64.147, 173.194.64.103, 173.194.64.104. Estos resultados también los podemos ver en forma gráfica de burbujas (BubbleView) o en una lista (Entity list).

![Etico 16](/assets/images/post/2018/etico16.png)

**Metagoofil Metagoofil** es una herramienta diseñada para capturar información mediante la extracción de metadatos desde documentos públicos (pdf, doc, xls, ppt, odp, ods, docx, pptx, xlsx) correspondientes a la empresa objetivo.   Abrir la terminal y escribir: **metagoofil**

(Si no tienen la herramienta instalada en Kali ejecutar este comando: *apt-get install metagoofil*)

![Etico 17](/assets/images/post/2018/etico17.png)

La opción “-d” define el dominio a buscar. La opción “-t” define el tipo de archivo a descargar (pdf, doc, xls, ppt, odp, ods, docx, pptx, xlsx) La opción “-l” limita los resultados de búsqueda (por defecto a 200). La opción “-n” limita los archivos a descargar. La opción “-o” define un directorio de trabajo (La ubicación para guardar los archivos descargados). La opción “-f” define un archivo de salida Escribir: **metagoofil -d nmap.org -t pdf -l 200 -n 10 -o /tmp/ -f /tmp/resultados_mgf.html**

![Etico 18](/assets/images/post/2018/etico18.png)

![Etico 19](/assets/images/post/2018/etico19.png)

usuarios, software y correos encontrados  

![Etico 20](/assets/images/post/2018/etico20.png)

El resultado son 41 archivos en formato pdf encontrados y 10 archivos en formato pdf descargados. También da una lista de 5 usuarios, lista de software encontrado en la cual aparecen diferentes versiones de lectores de pdf y por último da una lista de correos encontrados.

Esta guía ha sido creada en base a los conocimientos del señor Caballero Alonso.

*«Espero que esta guía básica haya sido de tu agrado e interés,  a lo mejor te servirá como una ventana para activar tu curiosidad y explorar en busca de nuevos conocimientos. Suerte»*

*«Cuando es evidente que los objetivos no se pueden alcanzar, no ajustes los objetivos, ajusta tus pasos. CONFUCIO»*
