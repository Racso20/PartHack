---
title: "Herramienta gratuita para buscar vulnerabilidades con OpenVAS en KaliLinux"
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/openvas.png"
---
	

Existen cientos sistemas operativos que se desarrollan para diferentes tareas, en el ambiente de seguridad (…), contamos con un sistema ideal como lo es Kali Linux el cual es una distribución de Linux basada en Debian, muy conocido por todos, cuya finalidad es realizar pruebas avanzadas de penetración y auditoría de seguridad.

Kali incluye cientos de herramientas que han sido enfocadas para llevar a cabo tareas de seguridad de la información, tales como pruebas de penetración, investigación de seguridad, informática forense e ingeniería inversa. El sistema Kali Linux está desarrollado y financiado por Offensive Security, la cual es una de las organizaciones más reconocidas en temas de capacitación en seguridad de la información y nos da garantía de integridad y fiabilidad.

Kali Linux esta disponible para su descarga en el siguiente enlace:

![Kali Linux](/assets/images/kali-linux.jpg)

Aprenderemos a instalar OpenVAS en Kali Linux y de este modo añadir una herramienta mas de vulnerabilidades y análisis de amenazas.

## Que es OpenVAS?

OpenVAS ha sido creado como un framework que implica un conjunto de servicios y herramientas con el propósito de ofrecer una solución integral y amplia a nivel de exploración de vulnerabilidades y gestión de las mismas en múltiples sistemas operativos.
Esta aplicación esta incluida dentro de la solución de gestión de vulnerabilidades comerciales de Greenbone Networks. El escáner de seguridad real de OpenVAS ejecuta de forma frecuente pruebas de vulnerabilidad de red (NVT) en más de 45.000 dispositivos.

OpenVAS es gratuito ya que está bajo la Licencia Pública General de GNU (GNU GPL). A nivel de arquitectura, OpenVAS ejecuta de manera eficaz las Pruebas de vulnerabilidad de red (NVT) con una estructura similar a esta:

![OpenVas 1](/assets/images/post/2018/openvas1.png)

OpenVAS Manager es el servicio central que permite la consolidación del escaneo de vulnerabilidades ofreciendo una solución completa a nivel de administración de vulnerabilidades. Este Manager se encarga de controlar el escáner mediante OTP (OpenVAS Transfer Protocol) y ofrece el OpenVAS Management Protocol (OMP) basado en XML.

A nivel de características de OpenVAS tenemos lo siguiente por categorías:

- Escáner de OpenVAS.
- Capacidad de escanear múltiples hosts de destino simultáneamente.
- Cuenta con OpenVAS Transfer Protocol (OTP).
- Soporta SSL para OTP.
- Soporte de WMI.
- Administrador de OpenVAS.
- Protocolo de gestión OpenVAS (OMP).
- Base de datos SQL (sqlite) para configuraciones y resultados de escaneo.
- Soporte SSL para OMP.
- Puede ejecutar múltiples tareas de escaneo frecuentes.
- Gestión de notas para resultados del escaneo.
- Falsa gestión positiva para obtener resultados de escaneo.
- Escaneos programados.
- Es posible detener, pausar y reanudar tareas de escaneo.
- Incluye el modo Master-Slave el cual permite controlar muchas instancias desde una central única.
- Incluye Reports Format Plugin Framework con varios complementos para: XML, HTML, LateX y muchos más.
- Gestión de usuarios
- Greenbone Security Assistant (GSA)
- Cuenta con un cliente para OMP y OAP.
- Soporta HTTP y HTTPS.
- Posee un servidor web en sí mismo (microhttpd), con lo cual no será necesario un servidor web adicional.
- Sistema integrado de ayuda en línea.
- Soporte multilingüe.

A continuación, veremos el proceso de instalación de OpenVAS en Kali Linux.

En primer lugar, será necesario actualizar todos los paquetes del sistema, para ello ejecutaremos la siguiente línea:

	```apt-get update && apt-get dist-upgrade -y```

1. Instalación de OpenVAS

	![OpenVas 2](/assets/images/post/2018/openvas2.png)

2. Una vez actualizado el sistema, el siguiente paso es proceder con la instalación de OpenVAS, para ello debemos ejecutar el siguiente comando:

	```apt-get install openvas```

	Allí debemos ingresar la letra S para confirmar la descarga e instalación y posteriormente veremos el siguiente mensaje:

	![OpenVas 3](/assets/images/post/2018/openvas3.png)

	También ingresaremos la letra S para confirmar la instalación de esos paquetes. Durante el proceso de instalación veremos el siguiente mensaje

	![OpenVas 4](/assets/images/post/2018/openvas4.png)
	
	Allí podremos confirmar o no que los servicios afectados sean reiniciados automáticamente o no. De este modo solo falta esperar alrededor de 7 minutos para que el proceso concluya.

	En algunos casos, cuando ejecutamos apt-get install openvas se genera el error No se ha podido localizar el paquete openvas.

Para esto, accederemos al directorio /etc/apt/sources.list usando el editor deseado:

	```nano /etc/apt/sources.list```

Allí debemos adicionar las siguientes líneas:

    ```deb http://http.kali.org/kali kali-rolling main contrib non-free
    deb http://old.kali.org/kali sana main non-free contrib
    deb http://old.kali.org/kali moto main non-free contrib```
	
![OpenVas 5](/assets/images/post/2018/openvas5.png)

Guardamos los cambios y ejecutamos apt-get update para actualizar el sistema y de este modo poder descargar e instalar OpenVAS.
Cómo configurar OpenVAS en Kali Linux.

PASO 1: Tan pronto concluya el proceso de instalación de OpenVAS, procedemos a ejecutar el siguiente comando para la configuración de OpenVAS.
	
	```openvas-setup```

PASO 2: Este proceso toma entre 20 a 30 minutos debido a los múltiples valores de configuración que son ejecutados automáticamente ya que se requiere descargar y actualizar todas las definiciones CVE y SCAP requeridas para su óptimo funcionamiento.

PASO 3: Debemos poner atención al resultado del comando durante la configuración de OpenVAS, ya que este genera la contraseña durante la instalación y esta será impresa en la consola al final de la configuración:

![OpenVas 6](/assets/images/post/2018/openvas6.png)

![OpenVas 7](/assets/images/post/2018/openvas7.png)

PASO 4: Verificamos que OpenVAS esté en ejecución con el siguiente comando: netstat -tulpn. Se abrirá automáticamente la aplicación en el navegador web, recuerda permitir la excepción de seguridad para desplegar la administración WEB.

![OpenVas 8](/assets/images/post/2018/openvas8.png)

![OpenVas 9](/assets/images/post/2018/openvas9.png)

Nota: En caso de que no se ejecute automáticamente la aplicación en tu navegador, puedes seguir los siguientes pasos:

Iniciar el servicio de OpenVAS ejecutando lo siguiente: openvas -start

En el navegador ingresamos https://127.0.0.1:9392 se produce una advertencia de seguridad, pulsamos en el botón Forever y accederemos al panel de login donde ingresaremos lo siguiente:

Usuario: admin
Contraseña: La que genero la herramienta en el proceso de configuración, de allí la importancia de copiarla y tenerla en un lugar seguro.

Ingresamos con las credenciales y este será el entorno ofrecido por OpenVAS:

![OpenVas 10](/assets/images/post/2018/openvas10.png)

En el home de administración tendremos múltiples secciones como se detallan a continuación:

### Scan management
Hace referencia a la gestión del escáner la cual nos permite crear nuevas tareas de exploración, modificar aquellas que se hayan creado previamente, revisar las notas o invalidaciones.
### Asset management
Esta es la opción de gestión de activos disponibles en los hosts que han sido analizados, así como el número de vulnerabilidades identificadas.
### Configuration
Allí será posible configurar los objetivos, asignar credenciales de acceso para revisiones de seguridad locales, configurar el escaneo, definir parámetros generales y específicos para el servidor de exploración, programar nuevos escaneos, configurar la generación de los informes, y más.
### Extras
Allí podremos acceder a información sobre las opciones de configuración, o de la gestión de seguridad de la información de OpenVAS.
### Administration
Esta opción nos permite gestionar los usuarios del escáner, la configuración para la sincronización de NVT Feed y despliega las opciones de configuración de OpenVAS.
### Help
Hace referencia a la ayuda para todos los elementos de la interfaz web

**«Saludos colegas y recuerden que en la vida, lo que a veces parece un final, realmente es un nuevo comienzo.»**