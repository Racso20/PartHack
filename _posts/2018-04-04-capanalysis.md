---
title: "Analizador de paquetes CapAnalysis"
author: "Felipe Castañeda"
---

![Capanalysis](/assets/images/capanalysis.png)

CapAnalysis es una herramienta web con licencia OpenSource, desarrollado para analistas de seguridad, administradores de sistemas y todos los que necesitan analizar grandes cantidades de tráfico de red.

CapAnalysis realiza la indexación del conjunto de datos de archivos PCAP y presenta sus contenidos en muchas formas, comenzando por una lista de flujos / flujos TCP, UDP o ESP, pasando a la representación geográfica de las conexiones.

## Filtrado de archivos PCAP

En CapAnalysis posee un poderoso conjunto de filtros muy sencillo de utilizar, algunos filtros disponibles son:

- **Filter files**: Permite el filtrado de archivos.
- **Filter IP/Ports**: Permite filtrar por IP y/o Puerto.
- **Filter country**: Permite filtrar por geolocalización.
- **Filter data size**: Permite filtrar por el tamaño de los datos.
- **Filter protocols**: Permite filtrar por protocolos.
- **Filter date and time**: Permite filtrar por fecha y hora.
	
![Filtrado](/assets/images/filtrado.jpg)

Para cada conjunto de datos, compuesto por uno o más archivos PCAP, CapAnalysis recopila información para cada flujo de paquetes UDP y TCP. Para los flujos TCP, es capaz de identificar el número de bytes perdidos, para cada dirección, y el total de bytes intercambiados eliminando del recuento los paquetes retransmitidos. Esta última característica es posible porque CapAnalysis es capaz de volver a montar las secuencias TCP para realizar su análisis.

## Inspección profunda de paquetes

CapAnalysis durante el análisis de tráfico de red intenta identificar el protocolo de cada flujo. Para hacer eso usa la Inspección profunda de paquetes.
Los protocolos que CapAnalysis puede identificar son más de 140 y dentro de este conjunto de protocolos se encuentran:

| VNC         | RDP           | SSL          | Yahoo       | SSH         | MGCP        | Google      |   IPSEC     |
| ----------- | -----------   | -----------  | ----------- | ----------- | ----------- | ----------- | ----------- |
| PCAnywhere  | WindowsUpdate | Apple iTunes | FaceBook    | SIP         | RTCP        | DropBox     | Twitter     |
| TeamViewer  | Skype         | Spotify      | TeamSpeak   | RTP         | YouTube     | Oracle      | WhatsApp    |

## Protocolos
![Protocolo](/assets/images/protocolo.jpg)

## Estadísticas
![Estadística](/assets/images/estadistica.jpg)

## Vista de Resumen
![Resumen](/assets/images/resumen.jpg)

## GeoLocalización
![Geolocalizacion](/assets/images/geolocalizacion.jpg)

## Como Instalar CapAnalysis

CapAnalisys esta diseñado para sistemas basados en Debian y Ubuntu con arquitecturas de 32 y 64 bits. Para comenzar con la instalación primero se debe descargar la aplicación desde los siguientes enlaces:

- (Debian 32 bits)[http://sourceforge.net/projects/capanalysis/files/version%201.2.2/capanalysis_1.2.2_i386.deb/download]{:target="_blank"}
- (Debian 64 bits)[http://sourceforge.net/projects/capanalysis/files/version%201.2.2/capanalysis_1.2.2_amd64.deb/download]{:target="_blank"}
- (Ubuntu 32 bits)[http://sourceforge.net/projects/capanalysis/files/version%201.2.2/capanalysis_1.2.2_i386.deb/download]{:target="_blank"}
- (Ubuntu 64 bits)[http://sourceforge.net/projects/capanalysis/files/version%201.2.2/capanalysis_1.2.2_amd64.deb/download]{:target="_blank"}
	
Para simplificar este proceso ocuparemos la herramienta Gdebi, la cual nos permite instalar archivos DEB en nuestro sistema de forma simple.

Para instalar Gdebi se utiliza el siguiente comando:
```sudo apt-get install gdebi```

una vez descargado CapAnalysis nos dirigimos al directorio donde se encuentra el archivo capanalysis_1.2.2_amd64.deb y haciendo clic con el botón derecho del mouse, seleccionamos instalador de paquetes GDebi.

![Paquete](/assets/images/paquete.jpg)

Presionar el botón «Instalar paquete» y se iniciará el proceso de instalación

![Instalador](/assets/images/instalador.jpg)

Una vez completada la instalación GDebi nos mostrará un cuadro con el estado de finalización.

![Finalizado](/assets/images/finalizado.jpg)

## Configuración

Para acceder a CapAnalysis se debe ingresar con su navegador a la siguiente dirección http: // localhost: 9877
Al iniciar por primera vez presionaremos el botón «New Password»

![Capturar](/assets/images/capturar.jpg)

Finalmente podemos concluir que CapAnalysis es una herramienta muy sencilla de usar, que nos ayudara en nuestros análisis.