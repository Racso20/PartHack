---
title: "Modelo OSI… Siempre es bueno recordar los conocimientos base."
author: "PartyHack"
header: 
  teaser: "/assets/images/post/2018/modelo-osi.jpg"
---
	

## El modelo OSI (Open Systems Interconnection o Interconexión de Sistemas Abiertos) es una estructura referencial que fue desarrollada en los 80s por la Organización Internacional de Estándares (ISO) con la intención de establecer un marco que sirviera de guía en el desarrollo de protocolos de comunicación. Estos protocolos siguen sus propios estándares internamente pero se manejan dentro de este marco referencial, por tanto, se podría decir que el modelo OSI es un estándar de estándares.

En esencia, la información se transmite de forma vertical a través de las 7 capas desde la aplicación fuente hasta la estructura física (cables que transmiten información en forma de bits) desde donde se transmite de nuevo hacia arriba en la estructura para llegar a la aplicación destino.
Las 7 capas del modelo OSI.

En todas las capas de la red la información se maneja en el formato adecuado, a estos paquetes de data que se mueven a través de las capas se les conoce como PDU (Protocol Data Unit o Unidad de Data del Protocolo) pero su nombre varía de acuerdo a la capa en la que se encuentre debido a las transformaciones que sufre.

1. Capa Física: Es la capa más baja del modelo, se refiere a las características físicas de la red, tales como los tipos de cables empleados para conectar el hardware, los tipos de conectores, el largo de los cables, etc. A manera de ejemplo, el estándar Ethernet de cables 100BASE-TX indica cables de conexión Ethernet rápida, que usan un cable par cruzado capaz de transmisiones en ambas direcciones al mismo tiempo.Es importante notar que en esta capa no se le asigna ningún significado a los bits, son simples 1s y 0s viajando a través de la red y son las capas superiores las que se encargan de interpretarlos.El PDU en esta capa es “bit”.

	![Capa Fisica](/assets/images/post/2018/capa-fisica.jpg)

2. Capa Enlace de Datos: Es la capa que se encarga de darle significado a los bits que fluyen en la red, define el tamaño de cada paquete enviado, la forma en la que se direcciona cada paquete de forma que llegue al destinatario correcto y algún mecanismo para impedir que 2 o más nodos en la red envíen data al mismo tiempo.Esta capa se encarga de detectar y corregir errores para asegurar que la data enviada es igual a la data recibida. Si ocurre algún error insalvable, el estándar debe especificar la manera en la que se va a informar al nodo para que reenvíe la data. En esta capa se encuentra la dirección física del dispositivo (MAC Address), la cual le es asignada en la fábrica. Es también la capa donde se construyen los “túneles” empleados en la construcción de VPNs.El PDU en esta capa es “Frame” o “Trama”.

	![Capa Enlace](/assets/images/post/2018/capa-datos.png)

3. Capa de Red: Se encarga de direccionar los mensajes de red desde una computadora a la otra consiguiendo un camino apropiado a través de la red. Asimismo, Provee al dispositivo de una dirección lógica (El protocolo IP se maneja en esta capa).Un router en esta capa puede encargarse de conectar 2 redes que empleen distintos protocolos en la capa 2. Como por ejemplo, una red que emplea Ethernet con una que emplea el protocolo T1.El PDU en esta capa es “Paquete”

	![Capa Red](/assets/images/post/2018/capa-red.png)

4. Capa de Transporte: Es la capa básica en la cual una computadora en red se comunica con otra computadora en red. Su principal propósito es asegurarse que los paquetes se muevan a través de la red de forma confiable y sin errores. Esto se logra estableciendo conexiones entre dispositivos, confirmando la recepción de los paquetes y reenviando paquetes que no son recibidos o que se corrompen antes de llegar a su destino. En esta capa está el protocolo TCP.El PDU en esta capa es “Segmento”.

	![Capa Trasporte](/assets/images/post/2018/capa-transporte.jpg)

5. Capa de Sesión: Es la encargada de establecer “sesiones” (instancias de comunicación e intercambio de data) entre 2 dispositivos en la red. Una sesión debe establecerse antes de empezar la transmisión de información y debe cerrarse una vez la transmisión ha finalizado.El PDU en esta capa es “Data”.

	![Capa Sesión](/assets/images/post/2018/capa-sesion.jpg)

6. Capa de Presentación: Es la encargada de convertir la data de un tipo de representación a otro. Por ejemplo, en un extremo se puede emplear un proceso de compresión complejo para reducir la cantidad de bits que se transportan por la red y en el otro extremo esos bits se “descomprimen” de forma tal que sean interpretados por la capa de aplicación. Esta capa es también conocida como la capa de sintáxis.El PDU en esta capa es “Data”.

	![Capa Presentacion](/assets/images/post/2018/capa-presentacion.jpg)

7. Capa de Aplicación: Se encarga de manejar las técnicas de red empleadas por las aplicaciones para establecer conexiones, en esta capa se encuentra el protocolo HTTP.El PDU en esta capa es “Data”.

	![Capa Aplicacion](/assets/images/post/2018/capa-aplicacion.gif)

## Cuales son las ventajas del modelo OSI.

- A nivel de Cambio
    Un cambio en una capa afecta muy poco a las demás, permitiendo mayor flexibilidad en los protocolos.
     
- A nivel de Diseño
    Esta separación permite a cada proveedor enfocarse en la capa correspondiente al diseñar un nuevo protocolo, mientras la comunicación con las demás capas se mantenga, el resultado es transparente.
     
- A nivel de Resolución de problemas
    La separación de las capas permite aislar la fuente de un problema particular de una forma más sencilla al poder enfocar los recursos en donde se estén presentando los problemas.
     
- A nivel de Estándares
    Definitivamente la mayor ventaja es poder establecer un grupo de reglas básicas para el manejo de la comunicación entre dispositivos a nivel internacional. Cabe destacar que este modelo es tan sólo una guía y por lo tanto existen casos que se salen de su estructura.

Aunque el modelo de referencia OSI sea universalmente reconocido, el estándar abierto de Internet desde el punto de vista histórico y técnico es el Protocolo de control de transmisión/Protocolo Internet (TCP/IP). El modelo de referencia TCP/IP y la pila de protocolo TCP/IP hacen que sea posible la comunicación entre dos computadores, desde cualquier parte del mundo, a casi la velocidad de la luz. El modelo TCP/IP tiene importancia histórica, al igual que las normas que permitieron el desarrollo de la industria telefónica, de energía eléctrica, el ferrocarril, la televisión y las industrias de vídeos.

- Capa 1 – Enlace

Esta capa combina la capa física y la capa de conexión de datos y enruta la data entre dispositivos en la misma red. Además, maneja el intercambio de data entre la red y otros dispositivos.

- Capa 2 – Internet

Corresponde a la capa de red y emplea la dirección IP que consiste en un identificador de red y un identificador de “Host” para determinar el dispositivo con el que se está comunicando.

- Capa 3 – Transporte

Corresponde a la capa de transporte y es donde se localiza el protocolo TCP (Transport Control Protocol) el cual funciona preguntando a otros dispositivos en la red si están dispuestos a aceptar la información proveniente del dispositivo local.

- Capa 4 – Aplicación

Combina las capas de Sesión, Presentación y Aplicación en una sola. Aquí residen los protocolos para funciones específicas (FTP, SMTP).

## Similitudes

- Ambos se dividen en capas.
- Ambos tienen capas de aplicación, aunque incluyen servicios muy distintos.
- Ambos tienen capas de transporte y de red similares.
- Se supone que la tecnología es de conmutación por paquetes (no de conmutación por circuito)
- Los profesionales de networking deben conocer ambos

### Diferencias

- TCP/IP combina las funciones de la capa de presentación y de sesión en la capa de aplicación
- TCP/IP combina la capas de enlace de datos y la capa física del modelo OSI en una sola capa
- TCP/IP parece ser más simple porque tiene menos capas
- Los protocolos TCP/IP son los estándares en torno a los cuales se desarrolló la Internet, de modo que la credibilidad del modelo TCP/IP se debe en gran parte a sus protocolos. En comparación, las redes típicas no se desarrollan normalmente a partir del protocolo OSI, aunque el modelo OSI se usa como guía.

### Uso de los modelos OSI y TCP/IP

Aunque los protocolos TCP/IP representan los estándares en base a los cuales se ha desarrollado la Internet, este currículum utiliza el modelo OSI por los siguientes motivos:

- Es un estándar mundial, genérico, independiente de los protocolos.
- Es más detallado, lo que hace que sea más útil para la enseñanza y el aprendizaje.
- Al ser más detallado, resulta de mayor utilidad para el diagnóstico de fallas.

Muchos profesionales de networking tienen distintas opiniones con respecto al modelo que se debe usar. Usted debe familiarizarse con ambos modelos. Utilizará el modelo OSI como si fuera un microscopio a través del cual se analizan las redes, pero también utilizará los protocolos de TCP/IP a lo largo del currículum. Recuerde que existe una diferencia entre un modelo (es decir, capas, interfaces y especificaciones de protocolo) y el protocolo real que se usa en networking. Usted usará el modelo OSI y los protocolos TCP/IP.